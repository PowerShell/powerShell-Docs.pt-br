---
ms.date: 07/08/2020
keywords: DSC,powershell,configuração,instalação
title: Escrevendo um recurso de DSC de instância única (melhor prática)
description: Este artigo descreve a melhor prática para a definição de um recurso de DSC que permite uma única instância em uma configuração.
ms.openlocfilehash: 4744136b5a733c86b517b239b2c37ce57a4246f7
ms.sourcegitcommit: 488a940c7c828820b36a6ba56c119f64614afc29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92662639"
---
# <a name="writing-a-single-instance-dsc-resource-best-practice"></a>Escrevendo um recurso de DSC de instância única (melhor prática)

> [!NOTE]
> Este artigo descreve a melhor prática para a definição de um recurso de DSC que permite uma única instância em uma configuração. Atualmente, não há nenhum recurso interno do DSC para fazer isso. Isso pode mudar no futuro.

Há situações em que você não deseja permitir que um recurso seja usado várias vezes em uma configuração. Por exemplo, um uma implementação anterior do recurso [xTimeZone](https://github.com/PowerShell/xTimeZone), uma configuração poderia chamar o recurso várias vezes, configurando o fuso horário para uma definição diferente em cada bloco de recurso:

```powershell
Configuration SetTimeZone
{
    Param
    (
        [String[]]$NodeName = $env:COMPUTERNAME

    )

    Import-DSCResource -ModuleName xTimeZone


    Node $NodeName
    {
         xTimeZone TimeZoneExample
         {

            TimeZone = 'Eastern Standard Time'
         }

         xTimeZone TimeZoneExample2
         {

            TimeZone = 'Pacific Standard Time'

         }

    }
}
```

Isso ocorre devido à forma como as chaves de recurso de DSC funcionam. Um recurso deve ter pelo menos uma propriedade de chave. Uma instância do recurso é considerada exclusiva se a combinação de valores de todas as suas propriedades de chave for exclusiva. Em sua implementação anterior, o recurso [xTimeZone](https://github.com/PowerShell/xTimeZone) apresentava apenas uma propriedade -- **TimeZone** , que obrigatoriamente tinha que ser uma chave. Por isso, uma configuração, como mostrado acima seria compilada e executada sem aviso. Cada um do blocos de recurso de **xTimeZone** é considerado exclusivo. Isso faria com que a configuração fosse aplicada várias vezes ao nó, alternando o fuso horário.

Para garantir que uma configuração possa definir o fuso horário para um nó de destino somente uma vez, o recurso foi atualizado para adicionar uma segunda propriedade, **IsSingleInstance** , que se tornou a propriedade principal. O **IsSingleInstance** foi limitado a um único valor, "Yes" (Sim) usando um **ValueMap**. O esquema MOF antigo para o recurso foi:

```powershell
[ClassVersion("1.0.0.0"), FriendlyName("xTimeZone")]
class xTimeZone : OMI_BaseResource
{
    [Key, Description("Specifies the TimeZone.")] String TimeZone;
};
```

O esquema MOF atualizado para o recurso é:

```powershell
[ClassVersion("1.0.0.0"), FriendlyName("xTimeZone")]
class xTimeZone : OMI_BaseResource
{
    [Key, Description("Specifies the resource is a single instance, the value must be 'Yes'"), ValueMap{"Yes"}, Values{"Yes"}] String IsSingleInstance;
    [Required, Description("Specifies the TimeZone.")] String TimeZone;
};
```

O script de recurso também foi atualizado para usar o novo parâmetro. Veja como o script de recurso foi alterado:

```powershell
function Get-TargetResource
{
    [CmdletBinding()]
    [OutputType([Hashtable])]
    param
    (
        [parameter(Mandatory = $true)]
        [ValidateSet('Yes')]
        [String]
        $IsSingleInstance,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $TimeZone
    )

    #Get the current TimeZone
    $CurrentTimeZone = Get-TimeZone

    $returnValue = @{
        TimeZone = $CurrentTimeZone
        IsSingleInstance = 'Yes'
    }

    #Output the target resource
    $returnValue
}

function Set-TargetResource
{
    [CmdletBinding()]
    param
    (
        [parameter(Mandatory = $true)]
        [ValidateSet('Yes')]
        [String]
        $IsSingleInstance,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $TimeZone
    )

    #Output the result of Get-TargetResource function.
    $CurrentTimeZone = Get-TimeZone

    Write-Verbose -Message "Replace the System Time Zone to $TimeZone"

    try
    {
        if($CurrentTimeZone -ne $TimeZone)
        {
            Write-Verbose -Verbose "Setting the TimeZone"
            Set-TimeZone -TimeZone $TimeZone
        }
        else
        {
            Write-Verbose -Verbose "TimeZone already set to $TimeZone"
        }
    }
    catch
    {
        $ErrorMsg = $_.Exception.Message
        Write-Verbose -Verbose $ErrorMsg
    }
}


function Test-TargetResource
{
    [CmdletBinding()]
    [OutputType([Boolean])]
    param
    (
        [parameter(Mandatory = $true)]
        [ValidateSet('Yes')]
        [String]
        $IsSingleInstance,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $TimeZone
    )

    #Output from Get-TargetResource
    $CurrentTimeZone = Get-TimeZone

    if($TimeZone -eq $CurrentTimeZone)
    {
        return $true
    }
    else
    {
        return $false
    }
}

Function Get-TimeZone {
    [CmdletBinding()]
    param()

    & tzutil.exe /g
}

Function Set-TimeZone {
    [CmdletBinding()]
    param(
        [Parameter(Mandatory=$true)]
        [System.String]
        $TimeZone
    )

    try
    {
        & tzutil.exe /s $TimeZone
    }
    catch
    {
        $ErrorMsg = $_.Exception.Message
        Write-Verbose $ErrorMsg
    }
}

Export-ModuleMember -Function *-TargetResource
```

Observe que a propriedade **TimeZone** propriedade não é mais uma chave. Agora, se uma configuração tentar definir o fuso horário duas vezes (usando dois blocos **xTimeZone** diferentes com valores de **TimeZone** diferentes), tentar compilar a configuração vai gerar um erro:

```Output
Test-ConflictingResources : A conflict was detected between resources '[xTimeZone]TimeZoneExample (::15::10::xTimeZone)' and
'[xTimeZone]TimeZoneExample2 (::22::10::xTimeZone)' in node 'CONTOSO-CLIENT'. Resources have identical key properties but there are differences in the
following non-key properties: 'TimeZone'. Values 'Eastern Standard Time' don't match values 'Pacific Standard Time'. Please update these property
values so that they are identical in both cases.
At line:271 char:9
+         Test-ConflictingResources $keywordName $canonicalizedValue $k ...
+         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Write-Error], InvalidOperationException
    + FullyQualifiedErrorId : ConflictingDuplicateResource,Test-ConflictingResources
Errors occurred while processing configuration 'SetTimeZone'.
At C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateConfiguration\PSDesiredStateConfiguration.psm1:3705 char:5
+     throw $ErrorRecord
+     ~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (SetTimeZone:String) [], InvalidOperationException
    + FullyQualifiedErrorId : FailToProcessConfiguration
```
