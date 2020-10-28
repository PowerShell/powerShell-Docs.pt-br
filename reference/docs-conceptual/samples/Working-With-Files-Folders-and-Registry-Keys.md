---
ms.date: 07/28/2020
keywords: powershell, cmdlet
title: Trabalhando com pastas de arquivos e chaves de Registro
description: Este artigo discute como lidar com as tarefas de manipulação de chave do Registro usando o PowerShell.
ms.openlocfilehash: 6f653c1fb409a238aa05658e89261a12e96f6fe1
ms.sourcegitcommit: 9080316e3ca4f11d83067b41351531672b667b7a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/24/2020
ms.locfileid: "92499970"
---
# <a name="working-with-files-folders-and-registry-keys"></a>Trabalhando com arquivos, pastas e chaves do Registro

O Windows PowerShell usa o substantivo **Item** para se referir a itens encontrados em uma unidade do Windows PowerShell.
Ao lidar com o provedor do Sistema de arquivos do Windows PowerShell, um **Item** pode ser um arquivo, uma pasta ou uma unidade do Windows PowerShell. Listar e trabalhar com esses itens são tarefas críticas básicas na maioria das configurações administrativas, por isso abordaremos essas tarefas com mais detalhes.

## <a name="enumerating-files-folders-and-registry-keys-get-childitem"></a>Enumerando arquivos, pastas e chaves do registro (Get-ChildItem)

Como a obtenção de uma coleção de itens de uma localização específica é uma tarefa comum, o cmdlet `Get-ChildItem` foi desenvolvido especificamente para retornar todos os itens encontrados em um contêiner, como uma pasta.

Se você quiser retornar todos os arquivos e pastas contidos diretamente na pasta C:\\Windows, digite:

```
PS> Get-ChildItem -Path C:\Windows
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-16   8:10 AM          0 0.log
-a---        2005-11-29   3:16 PM         97 acc1.txt
-a---        2005-10-23  11:21 PM       3848 actsetup.log
...
```

A listagem é semelhante ao que seria exibido quando você inserisse o comando `dir` no **Cmd.exe** ou o comando `ls` em um shell de comando do UNIX.

Você pode executar listagens muito complexas usando parâmetros do cmdlet `Get-ChildItem`. Examinaremos alguns cenários em seguida. É possível ver a sintaxe do cmdlet `Get-ChildItem` digitando:

```powershell
Get-Command -Name Get-ChildItem -Syntax
```

Esses parâmetros podem ser misturados e combinados para obter uma saída altamente personalizável.

### <a name="listing-all-contained-items--recurse"></a>Listando todos os itens contidos (-Recurse)

Para ver tanto os itens em uma pasta do Windows e os itens contidos em subpastas, use o parâmetro **Recurse** de `Get-ChildItem`. A lista exibe tudo dentro da pasta do Windows, bem como os itens em suas subpastas. Por exemplo:

```
PS> Get-ChildItem -Path C:\WINDOWS -Recurse

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS\AppPatch
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM    1852416 AcGenral.dll
...
```

### <a name="filtering-items-by-name--name"></a>Filtrar itens por nome (-Name)

Para exibir somente os nomes dos itens, use o parâmetro **Name** de `Get-Childitem`:

```
PS> Get-ChildItem -Path C:\WINDOWS -Name
addins
AppPatch
assembly
...
```

### <a name="forcibly-listing-hidden-items--force"></a>Forçar a listagem de itens ocultos (-Force)

Itens que são normalmente invisíveis no Explorador de Arquivos ou no Cmd.exe não são exibidos na saída de um comando `Get-ChildItem`. Para exibir itens ocultos, use o parâmetro **Force** do `Get-ChildItem`.
Por exemplo:

```powershell
Get-ChildItem -Path C:\Windows -Force
```

Esse parâmetro é chamado Force porque com ele você pode forçar a substituição do comportamento normal do comando `Get-ChildItem`. O Force é um parâmetro amplamente usado que força uma ação que um cmdlet normalmente não executa, embora ele não executará qualquer ação que comprometa a segurança do sistema.

### <a name="matching-item-names-with-wildcards"></a>Correspondendo nomes de itens com curingas

O comando `Get-ChildItem` aceita curingas no caminho dos itens a serem listados.

Como a correspondência de curingas é identificada pelo mecanismo do Windows PowerShell, todos os cmdlets que aceitam curingas usam a mesma notação e têm o mesmo comportamento de correspondência. A notação de curinga do Windows PowerShell inclui:

- O asterisco (`*`) corresponde a zero ou a mais ocorrências de qualquer caractere.

- O ponto de interrogação (`?`) corresponde exatamente a um caractere.

- Os caracteres de colchete esquerdo (`[`) e de colchete direito (`]`) envolvem um conjunto de caracteres a serem correspondidos.

Aqui estão alguns exemplos de como a especificação de curinga funciona.

Para localizar todos os arquivos no diretório do Windows com o sufixo `.log` e exatamente cinco caracteres no nome de base, digite o seguinte comando:

```
PS> Get-ChildItem -Path C:\Windows\?????.log

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
...
-a---        2006-05-11   6:31 PM     204276 ocgen.log
-a---        2006-05-11   6:31 PM      22365 ocmsn.log
...
-a---        2005-11-11   4:55 AM         64 setup.log
-a---        2005-12-15   2:24 PM      17719 VxSDM.log
...
```

Para localizar todos os arquivos que começam com a letra `x` no diretório do Windows, digite:

```powershell
Get-ChildItem -Path C:\Windows\x*
```

Para localizar todos os arquivos cujos nomes começam com "x" ou "z", digite:

```powershell
Get-ChildItem -Path C:\Windows\[xz]*
```

Para obter mais informações sobre curingas, confira [about_Wildcards](/powershell/module/microsoft.powershell.core/about/about_wildcards).

### <a name="excluding-items--exclude"></a>Excluindo itens (-Exclude)

Você pode excluir itens específicos usando o parâmetro **Exclude** de `Get-ChildItem`. Isso permite executar filtragem complexa em uma única instrução.

Por exemplo, suponha que você está tentando localizar a DLL de Serviço de Tempo do Windows na pasta **System32** , e tudo o que você lembra do nome da DLL é que começa com "W" e contém "32".

Uma expressão como `w*32*.dll` encontrará todas as DLLs que atendem às condições, mas talvez seja interessante filtrar ainda mais os arquivos e omitir arquivos win32. Você pode omitir esses arquivos usando o parâmetro **Exclude** com o padrão `win*`:

```
PS> Get-ChildItem -Path C:\WINDOWS\System32\w*32*.dll -Exclude win*

    Directory: C:\WINDOWS\System32

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a---           3/18/2019  9:43 PM         495616 w32time.dll
-a---           3/18/2019  9:44 PM          35328 w32topl.dll
-a---           1/24/2020  5:44 PM         401920 Wldap32.dll
-a---          10/10/2019  5:40 PM         442704 ws2_32.dll
-a---           3/18/2019  9:44 PM          66048 wsnmp32.dll
-a---           3/18/2019  9:44 PM          18944 wsock32.dll
-a---           3/18/2019  9:44 PM          64792 wtsapi32.dll
```

### <a name="mixing-get-childitem-parameters"></a>Mesclando parâmetros do Get-ChildItem

Você pode usar vários parâmetros do cmdlet `Get-ChildItem` no mesmo comando. Antes de mesclar parâmetros, certifique-se de que você compreende a correspondência de curingas. Por exemplo, o comando a seguir não retorna nenhum resultado:

```powershell
Get-ChildItem -Path C:\Windows\*.dll -Recurse -Exclude [a-y]*.dll
```

Não haverá nenhum resultado, mesmo que haja duas DLLs que comecem com a letra "z" na pasta Windows.

Nenhum resultado foi retornado, pois especificamos o curinga como parte do caminho. Mesmo que o comando seja recursivo, o cmdlet `Get-ChildItem` restringiu os itens àqueles que estão na pasta do Windows com nomes que terminam com `.dll`.

Para especificar uma pesquisa recursiva de arquivos cujos nomes correspondem a um padrão especial, use o parâmetro **Include** .

```
PS> Get-ChildItem -Path C:\Windows -Include *.dll -Recurse -Exclude [a-y]*.dll

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows\System32\Setup

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM       8261 zoneoc.dll

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows\System32

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM     337920 zipfldr.dll
```
