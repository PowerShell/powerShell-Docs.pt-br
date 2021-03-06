---
description: Impede que um script seja executado sem os elementos necessários.
Locale: en-US
ms.date: 12/14/2020
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_requires?view=powershell-7&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Requires
ms.openlocfilehash: 73c225f493fb671b34925d0127cc0d5cff0ab33e
ms.sourcegitcommit: 9a86cac80402d8193147058d4ba50e07b26059dd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97490577"
---
# <a name="about-requires"></a>Sobre o requer

## <a name="short-description"></a>Descrição breve
Impede que um script seja executado sem os elementos necessários.

## <a name="long-description"></a>Descrição longa

A `#Requires` instrução impede que um script seja executado, a menos que a versão do PowerShell, os módulos (e a versão) ou snap-ins (e a versão) e os pré-requisitos de edição sejam atendidos. Se os pré-requisitos não forem atendidos, o PowerShell não executará o script.

### <a name="syntax"></a>Sintaxe

```
#Requires -Version <N>[.<n>]
#Requires -PSSnapin <PSSnapin-Name> [-Version <N>[.<n>]]
#Requires -Modules { <Module-Name> | <Hashtable> }
#Requires -PSEdition <PSEdition-Name>
#Requires -ShellId <ShellId> -PSSnapin <PSSnapin-Name> [-Version <N>[.<n>]]
#Requires -RunAsAdministrator
```

Para obter mais informações sobre a sintaxe, consulte [ScriptRequirements](/dotnet/api/system.management.automation.language.scriptrequirements).

### <a name="rules-for-use"></a>Regras para uso

Um script pode incluir mais de uma `#Requires` instrução. As `#Requires` instruções podem aparecer em qualquer linha em um script.

Colocar uma `#Requires` instrução dentro de uma função não limita seu escopo. Todas as `#Requires` instruções são sempre aplicadas globalmente e devem ser atendidas, antes que o script possa ser executado.

> [!WARNING]
> Embora uma `#Requires` instrução possa aparecer em qualquer linha em um script, sua posição em um script não afeta a sequência de seu aplicativo. O estado global que a `#Requires` instrução apresenta deve ser atendido antes da execução do script.

Exemplo:

```powershell
Get-Module AzureRM.Netcore | Remove-Module
#Requires -Modules AzureRM.Netcore
```

Você pode imaginar que o código acima não deve ser executado porque o módulo necessário foi removido antes da `#Requires` instrução. No entanto, o `#Requires` estado precisava ser atendido antes que o script pudesse ser executado. Em seguida, a primeira linha do script invalidará o estado necessário.

### <a name="parameters"></a>Parâmetros

#### <a name="-assembly-assembly-path--net-assembly-specification"></a>-Assembly \<Assembly path> |\<.NET assembly specification>

> [!IMPORTANT]
> A `-Assembly` sintaxe foi preterida. Ele não serve nenhuma função. A sintaxe foi adicionada no PowerShell 5,1, mas o código de suporte nunca foi implementado. A sintaxe ainda é aceita para compatibilidade com versões anteriores.

Especifica o caminho para o arquivo DLL do assembly ou um nome de assembly .NET. O parâmetro **assembly** foi introduzido no PowerShell 5,0. Para obter mais informações sobre assemblies .NET, consulte [nomes de assembly](/dotnet/standard/assembly/names).

Por exemplo:

```
#Requires -Assembly path\to\foo.dll
```

```
#Requires -Assembly "System.Management.Automation, Version=3.0.0.0,
  Culture=neutral, PublicKeyToken=31bf3856ad364e35"
```

#### <a name="-version-nn"></a>-Versão \<N\> [. \<n\> ]

Especifica a versão mínima do PowerShell que o script requer. Insira um número de versão principal e um número de versão secundária opcional.

Por exemplo:

```powershell
#Requires -Version 6.0
```

#### <a name="-pssnapin-pssnapin-name--version-nn"></a>-PSSnapin \<PSSnapin-Name\> [-Version \<N\> [. \<n\> ]]

Especifica um snap-in do PowerShell que o script requer. Insira o nome do snap-in e um número de versão opcional.

Por exemplo:

```powershell
#Requires -PSSnapin DiskSnapin -Version 1.2
```

#### <a name="-modules-module-name--hashtable"></a>-Módulos \<Module-Name\> |\<Hashtable\>

Especifica os módulos do PowerShell que o script requer. Insira o nome do módulo e um número de versão opcional.

Se os módulos necessários não estiverem na sessão atual, o PowerShell os importará.
Se os módulos não puderem ser importados, o PowerShell lançará um erro de encerramento.

Para cada módulo, digite o nome do módulo ( \<String\> ) ou uma tabela de hash. O valor pode ser uma combinação de cadeias de caracteres e tabelas de hash. A tabela de hash tem as seguintes chaves.

- `ModuleName` - **Necessário** Especifica o nome do módulo.
- `GUID` - **Opcional** Especifica o GUID do módulo.
- Também é **necessário** especificar uma das três chaves abaixo. Essas chaves não podem ser usadas juntas.
  - `ModuleVersion` -Especifica uma versão mínima aceitável do módulo.
  - `RequiredVersion` -Especifica uma versão exata e necessária do módulo.
  - `MaximumVersion` -Especifica a versão máxima aceitável do módulo.

> [!NOTE]
> `RequiredVersion` foi adicionado no Windows PowerShell 5,0.
> `MaximumVersion` foi adicionado no Windows PowerShell 5,1.

Por exemplo:

Exigir que `AzureRM.Netcore` (versão `0.12.0` ou superior) esteja instalado.

```powershell
#Requires -Modules @{ ModuleName="AzureRM.Netcore"; ModuleVersion="0.12.0" }
```

Exigir que `AzureRM.Netcore` (**apenas** a versão `0.12.0` ) esteja instalado.

```powershell
#Requires -Modules @{ ModuleName="AzureRM.Netcore"; RequiredVersion="0.12.0" }
```

Requer que `AzureRM.Netcore` (versão `0.12.0` ou menos) esteja instalado.

```powershell
#Requires -Modules @{ ModuleName="AzureRM.Netcore"; MaximumVersion="0.12.0" }
```

Exigir que qualquer versão do `AzureRM.Netcore` e do `PowerShellGet` esteja instalada.

```powershell
#Requires -Modules AzureRM.Netcore, PowerShellGet
```

Ao usar a `RequiredVersion` chave, verifique se a cadeia de caracteres de versão corresponde exatamente à cadeia de caracteres de versão que você precisa.

```powershell
Get-Module AzureRM.Netcore -ListAvailable
```

```Output
    Directory: /home/azureuser/.local/share/powershell/Modules

ModuleType Version Name            PSEdition ExportedCommands
---------- ------- ----            --------- ----------------
Script     0.12.0  AzureRM.Netcore Core
```

O exemplo a seguir falha porque **0,12** não corresponde exatamente a **0.12.0**.

```powershell
#Requires -Modules @{ ModuleName="AzureRM.Netcore"; RequiredVersion="0.12" }
```

#### <a name="-psedition-psedition-name"></a>-PSEdition \<PSEdition-Name\>

Especifica uma edição do PowerShell que o script requer. Os valores válidos são **Core** para PowerShell Core e **Desktop** para Windows PowerShell.

Por exemplo:

```powershell
#Requires -PSEdition Core
```

#### <a name="-shellid"></a>-ShellId

Especifica o shell que o script requer. Insira a ID do Shell. Se você usar o parâmetro **ShellId** , também deverá incluir o parâmetro **PSSnapin** .
Você pode encontrar a **ShellId** atual consultando a `$ShellId` variável automática.

Por exemplo:

```powershell
#Requires -ShellId MyLocalShell -PSSnapin Microsoft.PowerShell.Core
```

> [!NOTE]
> Este parâmetro destina-se ao uso em mini-shells, que foram preteridos.

#### <a name="-runasadministrator"></a>-RunAsAdministrator

Quando esse parâmetro de opção é adicionado à sua `#Requires` instrução, ele especifica que a sessão do PowerShell na qual você está executando o script deve ser iniciada com direitos de usuário elevados. O parâmetro **RunAsAdministrator** é ignorado em um sistema operacional não Windows. O parâmetro **RunAsAdministrator** foi introduzido no PowerShell 4,0.

Por exemplo:

```powershell
#Requires -RunAsAdministrator
```

### <a name="examples"></a>Exemplos

O script a seguir tem duas `#Requires` instruções. Se os requisitos especificados em ambas as instruções não forem atendidos, o script não é executado. Cada `#Requires` instrução deve ser o primeiro item em uma linha:

```powershell
#Requires -Modules AzureRM.Netcore
#Requires -Version 6.0
Param
(
    [parameter(Mandatory=$true)]
    [String[]]
    $Path
)
...
```

## <a name="see-also"></a>Confira também

[about_Automatic_Variables](about_Automatic_Variables.md)

[about_Language_Keywords](about_Language_Keywords.md)
