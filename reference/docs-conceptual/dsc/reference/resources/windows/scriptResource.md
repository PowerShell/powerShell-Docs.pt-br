---
ms.date: 09/20/2019
keywords: DSC,powershell,configuração,instalação
title: Recurso Script de DSC
ms.openlocfilehash: e09e86011fa7dbb2a4d7f28b5032b4328b6f6ec2
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "71953063"
---
# <a name="dsc-script-resource"></a>Recurso Script de DSC

> Aplica-se a: Windows PowerShell 4.0, Windows PowerShell 5.x

O recurso **Script** na Configuração de Estado Desejado (DSC) do Windows PowerShell fornece um mecanismo para executar blocos de script do Windows PowerShell em nós de destino. O recurso **Script** usa as propriedades **GetScript**, **SetScript** e **TestScript** que contêm blocos de script definidos para executar as operações de estado de DSC correspondentes.

## <a name="syntax"></a>Sintaxe

```Syntax
Script [string] #ResourceName
{
    GetScript = [string]
    SetScript = [string]
    TestScript = [string]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
    [ PsDscRunAsCredential = [PSCredential] ]
}
```

> [!NOTE]
> Os blocos **GetScript**, **TestScript** e **SetScript** são armazenados como cadeias de caracteres.

## <a name="properties"></a>Propriedades

|Propriedade |Descrição |
|---|---|
|GetScript |Um bloco de script que retorna o estado atual do Node. |
|SetScript |Um bloco de script usado pelo DSC para impor a conformidade quando o Node não estiver no estado desejado. |
|TestScript |Um bloco de script que determina se o Node está no estado desejado. |
|Credential |Indica as credenciais que devem ser usadas para executar esse script, caso sejam necessárias. |

## <a name="common-properties"></a>Propriedades comuns

|Propriedade |Descrição |
|---|---|
|DependsOn |Indica que a configuração de outro recurso deve ser executada antes de ele ser configurado. Por exemplo, se a ID do bloco de script de configuração do recurso que você deseja executar primeiro for ResourceName e seu tipo for ResourceType, a sintaxe para usar essa propriedade será `DependsOn = "[ResourceType]ResourceName"`. |
|PsDscRunAsCredential |Define a credencial para executar todo o recurso. |

> [!NOTE]
> A propriedade comum **PsDscRunAsCredential** foi adicionada ao WMF 5.0 para permitir a execução de qualquer recurso de DSC no contexto de outras credenciais. Para saber mais, confira [Usar credenciais com recursos de DSC](../../../configurations/runasuser.md).

### <a name="additional-information"></a>Informações adicionais

#### <a name="getscript"></a>GetScript

O DSC não usa a saída do **GetScript**. O cmdlet [Get-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration) executa o **GetScript** para recuperar o estado atual do nó. **GetScript** não exige um valor retornado. Se você especificar um valor retornado, ele deverá ser uma tabela de hash que contenha uma chave **Result** cujo valor seja uma cadeia de caracteres.

#### <a name="testscript"></a>TestScript

O **TestScript** é executado pelo DSC para determinar se o **SetScript** deve ser executado. Se o **TestScript** retornar `$false`, o DSC executará o **SetScript** para colocar o nó de volta no estado desejado. Ele deve retornar um valor booliano. Um resultado de `$true` indica que o nó está em conformidade e **SetScript** não deve ser executado.

O cmdlet [Test-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Test-DscConfiguration) executa **TestScript** para recuperar a conformidade de nós com os recursos de **Script**.
No entanto, nesse caso, **SetScript** não é executado, não importa o que o bloco **TestScript** retorna.

> [!NOTE]
> Toda a saída do **TestScript** faz parte de seu valor retornado. O PowerShell interpreta a saída não suprimida como diferente de zero, o que significa que o **TestScript** retornará `$true` independentemente do estado do nó. Isso resulta em resultados imprevisíveis, falsos positivos e causa dificuldades durante a solução de problemas.

#### <a name="setscript"></a>SetScript

**SetScript** modifica o nó para impor o estado desejado. Ele será chamado pelo DSC se o bloco de script **TestScript** retornar `$false`. O **SetScript** não deve ter nenhum valor retornado.

## <a name="examples"></a>Exemplos

### <a name="example-1-write-sample-text-using-a-script-resource"></a>Exemplo 1: Escrever texto de exemplo usando um recurso de Script

Este exemplo testa a existência de `C:\TempFolder\TestFile.txt` em cada nó. Se não existir, ele o criará usando o `SetScript`. O `GetScript` retorna o conteúdo do arquivo, e seu valor de retorno não é usado.

```powershell
Configuration ScriptTest
{
    Import-DscResource -ModuleName 'PSDesiredStateConfiguration'

    Node localhost
    {
        Script ScriptExample
        {
            SetScript = {
                $sw = New-Object System.IO.StreamWriter("C:\TempFolder\TestFile.txt")
                $sw.WriteLine("Some sample string")
                $sw.Close()
            }
            TestScript = { Test-Path "C:\TempFolder\TestFile.txt" }
            GetScript = { @{ Result = (Get-Content C:\TempFolder\TestFile.txt) } }
        }
    }
}
```

### <a name="example-2-compare-version-information-using-a-script-resource"></a>Exemplo 2: Comparar informações de versão usando um recurso de Script

Este exemplo recupera as informações da versão *compatível* de um arquivo de texto no computador de criação e as armazenam na variável `$version`. Ao gerar o arquivo MOF do nó, o DSC substitui as variáveis `$using:version` em cada bloco de script pelo valor da variável `$version`.
Durante a execução, a versão *compatível* é armazenada em um arquivo de texto em cada Node, comparada e atualizada em execuções subsequentes.

```powershell
$version = Get-Content 'version.txt'

Configuration ScriptTest
{
    Import-DscResource -ModuleName 'PSDesiredStateConfiguration'

    Node localhost
    {
        Script UpdateConfigurationVersion
        {
            GetScript = {
                $currentVersion = Get-Content (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
                return @{ 'Result' = "$currentVersion" }
            }
            TestScript = {
                # Create and invoke a scriptblock using the $GetScript automatic variable, which contains a string representation of the GetScript.
                $state = [scriptblock]::Create($GetScript).Invoke()

                if( $state['Result'] -eq $using:version )
                {
                    Write-Verbose -Message ('{0} -eq {1}' -f $state['Result'],$using:version)
                    return $true
                }
                Write-Verbose -Message ('Version up-to-date: {0}' -f $using:version)
                return $false
            }
            SetScript = {
                $using:version | Set-Content -Path (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
            }
        }
    }
}
```