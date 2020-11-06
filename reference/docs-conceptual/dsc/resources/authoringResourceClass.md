---
ms.date: 07/08/2020
keywords: DSC,powershell,configuração,instalação
title: Escrevendo um recurso personalizado de DSC com classes do PowerShell
description: Este artigo mostra como criar um recurso simples que gerencia um arquivo em um caminho especificado.
ms.openlocfilehash: 72a828795c29e10ff66f164b8871b0fea7a1e0a8
ms.sourcegitcommit: 488a940c7c828820b36a6ba56c119f64614afc29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92667310"
---
# <a name="writing-a-custom-dsc-resource-with-powershell-classes"></a>Escrevendo um recurso personalizado de DSC com classes do PowerShell

> Aplica-se a: Windows PowerShell 5.0

Com a introdução de classes do PowerShell no Windows PowerShell 5.0, já é possível definir um recurso de DSC criando uma classe. A classe define o esquema e a implementação do recurso; portanto, não há necessidade de criar um arquivo MOF separado. A estrutura de pastas para um recurso baseado em classe também é mais simples, pois uma pasta **DSCResources** não é necessária.

Em um recurso de DSC baseado em classes, o esquema é definido como propriedades da classe que pode ser modificado com atributos para especificar o tipo de propriedade... O recurso é implementado pelos métodos `Get()` , `Set()` e `Test()` (equivalentes às funções `Get-TargetResource`, `Set-TargetResource` e `Test-TargetResource` em um recurso de script).

Neste artigo, criaremos um recurso simples chamado **FileResource** , que gerencia um arquivo em um caminho especificado.

Para obter mais informações sobre recursos de DSC, consulte [Criar recursos personalizados de configuração de estado desejado do Windows PowerShell](authoringResource.md)

> [!Note]
> coleções genéricas não são permitidas em recursos baseados em classe.

## <a name="folder-structure-for-a-class-resource"></a>Estrutura de pastas para um recurso de classe

Para implementar um recurso personalizado de DSC com uma classe do PowerShell, crie a seguinte estrutura de pastas.
A classe é definida em `MyDscResource.psm1` e o manifesto de módulo é definido em `MyDscResource.psd1`.

```
$env:ProgramFiles\WindowsPowerShell\Modules (folder)
    |- MyDscResource (folder)
        MyDscResource.psm1
        MyDscResource.psd1
```

## <a name="create-the-class"></a>Criar a classe

A palavra-chave class é utilizada para criar uma classe do PowerShell. Para especificar que uma classe é um recurso de DSC, use o atributo `DscResource()` . O nome da classe é o nome do recurso de DSC.

```powershell
[DscResource()]
class FileResource {
}
```

### <a name="declare-properties"></a>Declarar propriedades

O esquema do recurso de DSC é definido como propriedades da classe. Declaramos três propriedades da seguinte maneira.

```powershell
[DscProperty(Key)]
[string]$Path

[DscProperty(Mandatory)]
[Ensure] $Ensure

[DscProperty(Mandatory)]
[string] $SourcePath

[DscProperty(NotConfigurable)]
[Nullable[datetime]] $CreationTime
```

Observe que as propriedades são modificadas por atributos. O significado dos atributos é o seguinte:

- **DscProperty(Key)** : a propriedade é obrigatória. A propriedade é uma chave. Os valores de todas as propriedades marcadas como chaves devem se combinar para identificar exclusivamente uma instância de recursos dentro de uma configuração.
- **DscProperty(Mandatory)** : a propriedade é obrigatória.
- **DscProperty(NotConfigurable)** : a propriedade é somente leitura. As propriedades marcadas com esse atributo não podem ser definidas por uma configuração, mas são preenchidas pelo método `Get()` quando presentes.
- **DscProperty()** : a propriedade é configurável, mas não é obrigatória.

As propriedades `$Path` e `$SourcePath` são ambas cadeias de caracteres. O `$CreationTime` é uma propriedade [DateTime](/dotnet/api/system.datetime). A propriedade `$Ensure` é um tipo de enumeração definido da seguinte maneira.

```powershell
enum Ensure
{
    Absent
    Present
}
```

### <a name="implementing-the-methods"></a>Implementando os métodos

Os métodos `Get()` , `Set()` e `Test()` são análogos às funções `Get-TargetResource`, `Set-TargetResource` e `Test-TargetResource` em um recurso de script.

Esse código também inclui a função `CopyFile()`, uma função auxiliar que copia o arquivo de `$SourcePath` para `$Path`.

```powershell
    <#
        This method is equivalent of the Set-TargetResource script function.
        It sets the resource to the desired state.
    #>
    [void] Set()
    {
        $fileExists = $this.TestFilePath($this.Path)

        if ($this.ensure -eq [Ensure]::Present)
        {
            if(-not $fileExists)
            {
                $this.CopyFile()
            }
        }
        else
        {
            if ($fileExists)
            {
                Write-Verbose -Message "Deleting the file $($this.Path)"
                Remove-Item -LiteralPath $this.Path -Force
            }
        }
    }

    <#
        This method is equivalent of the Test-TargetResource script function.
        It should return True or False, showing whether the resource
        is in a desired state.
    #>
    [bool] Test()
    {
        $present = $this.TestFilePath($this.Path)

        if ($this.Ensure -eq [Ensure]::Present)
        {
            return $present
        }
        else
        {
            return -not $present
        }
    }

    <#
        This method is equivalent of the Get-TargetResource script function.
        The implementation should use the keys to find appropriate resources.
        This method returns an instance of this class with the updated key
         properties.
    #>
    [FileResource] Get()
    {
        $present = $this.TestFilePath($this.Path)

        if ($present)
        {
            $file = Get-ChildItem -LiteralPath $this.Path
            $this.CreationTime = $file.CreationTime
            $this.Ensure = [Ensure]::Present
        }
        else
        {
            $this.CreationTime = $null
            $this.Ensure = [Ensure]::Absent
        }

        return $this
    }

    <#
        Helper method to check if the file exists and it is file
    #>
    [bool] TestFilePath([string] $location)
    {
        $present = $true

        $item = Get-ChildItem -LiteralPath $location -ErrorAction Ignore

        if ($item -eq $null)
        {
            $present = $false
        }
        elseif ($item.PSProvider.Name -ne "FileSystem")
        {
            throw "Path $($location) is not a file path."
        }
        elseif ($item.PSIsContainer)
        {
            throw "Path $($location) is a directory path."
        }

        return $present
    }

    <#
        Helper method to copy file from source to path
    #>
    [void] CopyFile()
    {
        if (-not $this.TestFilePath($this.SourcePath))
        {
            throw "SourcePath $($this.SourcePath) is not found."
        }

        [System.IO.FileInfo] $destFileInfo = New-Object -TypeName System.IO.FileInfo($this.Path)

        if (-not $destFileInfo.Directory.Exists)
        {
            Write-Verbose -Message "Creating directory $($destFileInfo.Directory.FullName)"

            <#
                Use CreateDirectory instead of New-Item to avoid code
                to handle the non-terminating error
            #>
            [System.IO.Directory]::CreateDirectory($destFileInfo.Directory.FullName)
        }

        if (Test-Path -LiteralPath $this.Path -PathType Container)
        {
            throw "Path $($this.Path) is a directory path"
        }

        Write-Verbose -Message "Copying $($this.SourcePath) to $($this.Path)"

        # DSC engine catches and reports any error that occurs
        Copy-Item -LiteralPath $this.SourcePath -Destination $this.Path -Force
    }
```

### <a name="the-complete-file"></a>O arquivo completo

Segue o arquivo de classe completo.

```powershell
enum Ensure
{
    Absent
    Present
}

<#
   This resource manages the file in a specific path.
   [DscResource()] indicates the class is a DSC resource
#>

[DscResource()]
class FileResource
{
    <#
       This property is the fully qualified path to the file that is
       expected to be present or absent.

       The [DscProperty(Key)] attribute indicates the property is a
       key and its value uniquely identifies a resource instance.
       Defining this attribute also means the property is required
       and DSC will ensure a value is set before calling the resource.

       A DSC resource must define at least one key property.
    #>
    [DscProperty(Key)]
    [string]$Path

    <#
        This property indicates if the settings should be present or absent
        on the system. For present, the resource ensures the file pointed
        to by $Path exists. For absent, it ensures the file point to by
        $Path does not exist.

        The [DscProperty(Mandatory)] attribute indicates the property is
        required and DSC will guarantee it is set.

        If Mandatory is not specified or if it is defined as
        Mandatory=$false, the value is not guaranteed to be set when DSC
        calls the resource.  This is appropriate for optional properties.
    #>
    [DscProperty(Mandatory)]
    [Ensure] $Ensure

    <#
       This property defines the fully qualified path to a file that will
       be placed on the system if $Ensure = Present and $Path does not
        exist.

       NOTE: This property is required because [DscProperty(Mandatory)] is
        set.
    #>
    [DscProperty(Mandatory)]
    [string] $SourcePath

    <#
       This property reports the file's create timestamp.

       [DscProperty(NotConfigurable)] attribute indicates the property is
       not configurable in DSC configuration.  Properties marked this way
       are populated by the Get() method to report additional details
       about the resource when it is present.

    #>
    [DscProperty(NotConfigurable)]
    [Nullable[datetime]] $CreationTime

    <#
        This method is equivalent of the Set-TargetResource script function.
        It sets the resource to the desired state.
    #>
    [void] Set()
    {
        $fileExists = $this.TestFilePath($this.Path)
        if ($this.ensure -eq [Ensure]::Present)
        {
            if (-not $fileExists)
            {
                $this.CopyFile()
            }
        }
        else
        {
            if ($fileExists)
            {
                Write-Verbose -Message "Deleting the file $($this.Path)"
                Remove-Item -LiteralPath $this.Path -Force
            }
        }
    }

    <#
        This method is equivalent of the Test-TargetResource script function.
        It should return True or False, showing whether the resource
        is in a desired state.
    #>
    [bool] Test()
    {
        $present = $this.TestFilePath($this.Path)

        if ($this.Ensure -eq [Ensure]::Present)
        {
            return $present
        }
        else
        {
            return -not $present
        }
    }

    <#
        This method is equivalent of the Get-TargetResource script function.
        The implementation should use the keys to find appropriate resources.
        This method returns an instance of this class with the updated key
         properties.
    #>
    [FileResource] Get()
    {
        $present = $this.TestFilePath($this.Path)

        if ($present)
        {
            $file = Get-ChildItem -LiteralPath $this.Path
            $this.CreationTime = $file.CreationTime
            $this.Ensure = [Ensure]::Present
        }
        else
        {
            $this.CreationTime = $null
            $this.Ensure = [Ensure]::Absent
        }

        return $this
    }

    <#
        Helper method to check if the file exists and it is file
    #>
    [bool] TestFilePath([string] $location)
    {
        $present = $true

        $item = Get-ChildItem -LiteralPath $location -ea Ignore
        if ($item -eq $null)
        {
            $present = $false
        }
        elseif ($item.PSProvider.Name -ne "FileSystem")
        {
            throw "Path $($location) is not a file path."
        }
        elseif ($item.PSIsContainer)
        {
            throw "Path $($location) is a directory path."
        }

        return $present
    }

    <#
        Helper method to copy file from source to path
    #>
    [void] CopyFile()
    {
        if (-not $this.TestFilePath($this.SourcePath))
        {
            throw "SourcePath $($this.SourcePath) is not found."
        }

        [System.IO.FileInfo] $destFileInfo = new-object System.IO.FileInfo($this.Path)
        if (-not $destFileInfo.Directory.Exists)
        {
            Write-Verbose -Message "Creating directory $($destFileInfo.Directory.FullName)"

            <#
                Use CreateDirectory instead of New-Item to avoid code
                 to handle the non-terminating error
            #>
            [System.IO.Directory]::CreateDirectory($destFileInfo.Directory.FullName)
        }

        if (Test-Path -LiteralPath $this.Path -PathType Container)
        {
            throw "Path $($this.Path) is a directory path"
        }

        Write-Verbose -Message "Copying $($this.SourcePath) to $($this.Path)"

        # DSC engine catches and reports any error that occurs
        Copy-Item -LiteralPath $this.SourcePath -Destination $this.Path -Force
    }
} # This module defines a class for a DSC "FileResource" provider.
```

## <a name="create-a-manifest"></a>Criar um manifesto

Para disponibilizar um recurso baseado em classes para o mecanismo de DSC, você precisa incluir uma declaração `DscResourcesToExport` no arquivo de manifesto que instrui o módulo para exportar recursos. Nosso manifesto tem essa aparência:

```powershell
@{

# Script module or binary module file associated with this manifest.
RootModule = 'MyDscResource.psm1'

DscResourcesToExport = 'FileResource'

# Version number of this module.
ModuleVersion = '1.0'

# ID used to uniquely identify this module
GUID = '81624038-5e71-40f8-8905-b1a87afe22d7'

# Author of this module
Author = 'Microsoft Corporation'

# Company or vendor of this module
CompanyName = 'Microsoft Corporation'

# Copyright statement for this module
Copyright = '(c) 2014 Microsoft. All rights reserved.'

# Description of the functionality provided by this module
# Description = ''

# Minimum version of the Windows PowerShell engine required by this module
PowerShellVersion = '5.0'

# Name of the Windows PowerShell host required by this module
# PowerShellHostName = ''
}
```

## <a name="test-the-resource"></a>Testar o recurso

Depois de salvar a classe e os arquivos de manifesto na estrutura de pastas, conforme descrito anteriormente, você pode criar uma configuração que use o novo recurso. Para obter informações sobre como executar uma configuração DSC, consulte [Impondo configurações](../pull-server/enactingConfigurations.md). A configuração a seguir verificará se o arquivo em `c:\test\test.txt` existe e, em caso negativo, copia o arquivo de `c:\test.txt` (você deve criar `c:\test.txt` antes de executar a configuração).

```powershell
Configuration Test
{
    Import-DSCResource -module MyDscResource
    FileResource file
    {
        Path = "C:\test\test.txt"
        SourcePath = "c:\test.txt"
        Ensure = "Present"
    }
}
Test
Start-DscConfiguration -Wait -Force Test
```

## <a name="supporting-psdscrunascredential"></a>Dando suporte a PsDscRunAsCredential

> [Observação] **PsDscRunAsCredential** tem suporte no PowerShell 5.0 e versões posteriores.

A propriedade **PsDscRunAsCredential** pode ser usada no bloco de recurso [Configurações DSC](../configurations/configurations.md) para especificar que o recurso deve ser executado em um conjunto de credenciais específico. Para obter mais informações, veja [Executando o DSC com as credenciais do usuário](../configurations/runAsUser.md).

### <a name="require-or-disallow-psdscrunascredential-for-your-resource"></a>Solicitar ou desautorizar PsDscRunAsCredential para o recurso

O atributo `DscResource()` usa um parâmetro opcional **RunAsCredential**. Esse parâmetro usa um dos três valores:

- `Optional` **PsDscRunAsCredential** é opcional para as configurações que chamam esse recurso. Esse é o valor padrão.
- `Mandatory` **PsDscRunAsCredential** deve ser usado para qualquer configuração que chame esse recurso.
- `NotSupported` As configurações que chamam este recurso não podem usar o **PsDscRunAsCredential**.
- `Default` Igual a `Optional`.

Por exemplo, use o seguinte atributo para especificar que o recurso personalizado não dá suporte ao uso de **PsDscRunAsCredential** :

```powershell
[DscResource(RunAsCredential=NotSupported)]
class FileResource {
}
```

### <a name="declaring-multiple-class-resources-in-a-module"></a>Declarando vários recursos de classe em um módulo

Um módulo pode definir vários recursos DSC baseados em classe. Você pode criar a estrutura de pasta das seguintes maneiras:

1. Defina o primeiro recurso no arquivo `<ModuleName>.psm1` e os próximos na pasta **DSCResources**.

   ```
   $env:ProgramFiles\WindowsPowerShell\Modules (folder)
        |- MyDscResource (folder)
           |- MyDscResource.psm1
              MyDscResource.psd1
        |- DSCResources
           |- SecondResource.psm1
   ```

1. Defina todos os recursos na pasta **DSCResources**.

   ```
   $env:ProgramFiles\WindowsPowerShell\Modules (folder)
        |- MyDscResource (folder)
           |- MyDscResource.psm1
              MyDscResource.psd1
        |- DSCResources
           |- FirstResource.psm1
              SecondResource.psm1
   ```

> [!NOTE]
> Nos exemplos acima, adicione todos os arquivos PSM1 em **DSCResources** à chave **NestedModules** no seu arquivo PSD1.

### <a name="access-the-user-context"></a>Acessar o contexto do usuário

Para acessar o contexto do usuário de dentro de um recurso personalizado, você pode usar a variável automática `$global:PsDscContext`.

Por exemplo, o código a seguir escreveria o contexto do usuário em que o recurso está em execução para o fluxo de saída detalhada:

```powershell
if (PsDscContext.RunAsUser) {
    Write-Verbose "User: $global:PsDscContext.RunAsUser";
}
```

## <a name="see-also"></a>Consulte Também

[Criar recursos personalizados de configuração de estado desejado do Windows PowerShell](authoringResource.md)
