---
ms.date: 08/27/2018
keywords: powershell, cmdlet
title: Usando variáveis para armazenar objetos
ms.openlocfilehash: 2d20d84e48d3f68cab5c1ffa05d689b46415ebc8
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "67030361"
---
# <a name="using-variables-to-store-objects"></a>Usando variáveis para armazenar objetos

O PowerShell funciona com objetos. O PowerShell permite que você crie objetos nomeados, conhecidos como variáveis.
Os nomes de variáveis podem incluir o caractere de sublinhado e quaisquer caracteres alfanuméricos. Quando usada no PowerShell, uma variável é sempre especificada usando o caractere \$ seguido pelo nome da variável.

## <a name="creating-a-variable"></a>Criar uma variável

Você pode criar uma variável digitando um nome de variável válido:

```
PS> $loc
PS>
```

Este exemplo não retorna resultados porque `$loc` não tem um valor. Você pode criar uma variável e atribuir a ela um valor na mesma etapa. O PowerShell só criará a variável se ela não existir.
Caso contrário, ele atribuirá o valor especificado à variável existente. O exemplo a seguir armazena o local atual na variável `$loc`:

```powershell
$loc = Get-Location
```

O PowerShell não exibe qualquer saída quando você digita esse comando. O PowerShell envia a saída de "Get-Location" para `$loc`. No PowerShell, os dados que não estão atribuídos ou redirecionados são enviados para a tela. A sua localização atual aparece ao digitar `$loc`:

```
PS> $loc

Path
----
C:\temp
```

Use `Get-Member` para exibir informações sobre o conteúdo das variáveis. `Get-Member` mostra que `$loc` é um objeto **PathInfo**, assim como a saída de `Get-Location`:

```powershell
PS> $loc | Get-Member -MemberType Property

   TypeName: System.Management.Automation.PathInfo

Name         MemberType Definition
----         ---------- ----------
Drive        Property   System.Management.Automation.PSDriveInfo Drive {get;}
Path         Property   System.String Path {get;}
Provider     Property   System.Management.Automation.ProviderInfo Provider {...
ProviderPath Property   System.String ProviderPath {get;}
```

## <a name="manipulating-variables"></a>Manipular variáveis

O PowerShell fornece vários comandos para manipular variáveis. Você pode ver uma listagem completa em um formato legível digitando:

```powershell
Get-Command -Noun Variable | Format-Table -Property Name,Definition -AutoSize -Wrap
```

O PowerShell também cria diversas variáveis definidas pelo sistema. Você pode usar o cmdlet `Remove-Variable` para remover as variáveis que não são controladas pelo PowerShell da sessão atual. Digite o seguinte comando a seguir para limpar todas as variáveis:

```powershell
Remove-Variable -Name * -Force -ErrorAction SilentlyContinue
```

Após a execução do comando anterior, o cmdlet `Get-Variable` mostra as variáveis de sistema do PowerShell.

O PowerShell também cria uma unidade de variável. Use o exemplo a seguir para exibir todas as variáveis do PowerShell usando a unidade de variável:

```powershell
Get-ChildItem variable:
```

## <a name="using-cmdexe-variables"></a>Usar variáveis do cmd.exe

O PowerShell pode usar as mesmas variáveis de ambiente disponíveis a qualquer processo do Windows, incluindo **cmd.exe**. Essas variáveis são expostas por meio de uma unidade chamada `env:`. Exiba essas variáveis digitando o seguinte comando:

```powershell
Get-ChildItem env:
```

Os cmdlets `*-Variable` padrão não são projetados para funcionar com variáveis de ambiente. Variáveis de ambiente são acessadas usando o prefixo de unidade `env:`. Por exemplo, a variável **% SystemRoot %** no **cmd.exe** contém nome do diretório raiz do sistema operacional. No PowerShell, use `$env:SystemRoot` para acessar o mesmo valor.

```
PS> $env:SystemRoot
C:\WINDOWS
```

Você também pode criar e modificar variáveis de ambiente do PowerShell. As variáveis de ambiente do PowerShell seguem as mesmas regras para variáveis de ambiente usadas em outro lugar no sistema operacional. O exemplo a seguir cria uma nova variável de ambiente:

```powershell
$env:LIB_PATH='/usr/local/lib'
```

Embora não seja necessário, é comum usar letras maiúsculas nos nomes de variáveis de ambientes.
