---
ms.date: 06/05/2017
keywords: powershell, cmdlet
title: Trabalhando com arquivos e pastas
ms.openlocfilehash: 743e261d2f5e8bfa39f2731fca7fea6e5678c711
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "70215527"
---
# <a name="working-with-files-and-folders"></a>Trabalhando com arquivos e pastas

Navegar pelas unidades do Windows PowerShell e manipular os itens nelas é semelhante a manipular arquivos e pastas em unidades de disco físico do Windows. Esta seção discute como lidar com tarefas de manipulação de arquivos e pastas específicas usando o PowerShell.

## <a name="listing-all-the-files-and-folders-within-a-folder"></a>Listar todos os arquivos e pastas dentro de uma pasta

Você pode obter todos os itens diretamente em uma pasta usando **Get-ChildItem**. Adicione o parâmetro opcional **Force** para exibir itens ocultos ou do sistema. Por exemplo, este comando exibe o conteúdo direto da unidade do Windows PowerShell C (que é a mesma que a unidade física C do Windows):

```powershell
Get-ChildItem -Path C:\ -Force
```

O comando lista apenas os itens contidos diretamente, similar ao uso do comando **DIR** do Cmd.exe ou do **ls** em um shell do UNIX. Para mostrar os itens contidos, também é necessário especificar o parâmetro **-Recurse**. (Isso pode levar muitíssimo tempo para ser concluído.) Para listar todos os itens na unidade C:

```powershell
Get-ChildItem -Path C:\ -Force -Recurse
```

**Get-ChildItem** pode filtrar itens com seus parâmetros **Path**, **Filter**, **Include** e **Exclude**, mas eles normalmente se baseiam apenas no nome. Você pode executar a filtragem complexa com base em outras propriedades de itens usando **Where-Object**.

O comando a seguir localiza todos os executáveis na pasta Arquivos de Programa que foi modificado após 1º de outubro de 2005 e que não são menores que 1 megabyte nem maiores que 10 megabytes:

```powershell
Get-ChildItem -Path $env:ProgramFiles -Recurse -Include *.exe | Where-Object -FilterScript {($_.LastWriteTime -gt '2005-10-01') -and ($_.Length -ge 1mb) -and ($_.Length -le 10mb)}
```

## <a name="copying-files-and-folders"></a>Copiar arquivos e pastas

A cópia é feita com **Copy-Item**. O comando a seguir faz backup de C:\\boot.ini em C:\\boot.bak:

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak
```

Se o arquivo de destino já existir, a tentativa de cópia falhará. Para substituir um destino pré-existente, use o parâmetro **Force**:

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak -Force
```

Esse comando funciona mesmo quando o destino é somente leitura.

Copiar a pasta funciona da mesma maneira. Este comando copia a pasta c:\\temp\\test1 na nova pasta c:\\temp\\DeleteMe recursivamente:

```powershell
Copy-Item C:\temp\test1 -Recurse C:\temp\DeleteMe
```

Você também pode copiar uma seleção de itens. O comando a seguir copia todos os arquivos .txt contidos em qualquer lugar em c:\\data em c:\\temp\\text:

```powershell
Copy-Item -Filter *.txt -Path c:\data -Recurse -Destination C:\temp\text
```

Você ainda pode usar outras ferramentas para realizar cópias do sistema de arquivos. XCOPY, ROBOCOPY e objetos COM, como o **Scripting.FileSystemObject,** todos eles funcionam no Windows PowerShell. Por exemplo, você pode usar a classe **Scripting.FileSystem COM** do Windows Script Host para fazer backup de C:\\boot.ini em C:\\boot.bak:

```powershell
(New-Object -ComObject Scripting.FileSystemObject).CopyFile('C:\boot.ini', 'C:\boot.bak')
```

## <a name="creating-files-and-folders"></a>Criar arquivos e pastas

Criar novos itens funciona da mesma forma em todos os provedores do Windows PowerShell. Se um provedor do Windows PowerShell tiver mais de um tipo de item, por exemplo, se o provedor do Sistema de Arquivos do Windows PowerShell fizer distinção entre arquivos e diretórios, você precisará especificar o tipo de item.

Este comando cria uma nova pasta C:\\temp\\Nova Pasta:

```powershell
New-Item -Path 'C:\temp\New Folder' -ItemType Directory
```

Este comando cria um novo arquivo vazio C:\\temp\\New Folder\\file.txt

```powershell
New-Item -Path 'C:\temp\New Folder\file.txt' -ItemType File
```

## <a name="removing-all-files-and-folders-within-a-folder"></a>Remover todos os arquivos e pastas dentro de uma pasta

É possível remover os itens contidos usando **Remove-Item**, mas você será solicitado a confirmar a remoção se o item contiver qualquer outra coisa. Por exemplo, se você tentar excluir a pasta C:\\temp\\DeleteMe que contém outros itens, o Windows PowerShell solicitará sua confirmação antes de excluí-la:

```
Remove-Item -Path C:\temp\DeleteMe

Confirm
The item at C:\temp\DeleteMe has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

Se você não quiser ser solicitado para cada item contido, especifique o parâmetro **Recurse**:

```powershell
Remove-Item -Path C:\temp\DeleteMe -Recurse
```

## <a name="mapping-a-local-folder-as-a-drive"></a>Mapear uma pasta local como uma unidade

Você também pode mapear uma pasta local usando o comando **New-PSDrive**. O comando a seguir cria uma unidade local P: com raiz no diretório Arquivos de Programa locais, visível somente na sessão do PowerShell:

```powershell
New-PSDrive -Name P -Root $env:ProgramFiles -PSProvider FileSystem
```

Assim como ocorre com unidades de rede, unidades mapeadas no Windows PowerShell ficam visíveis imediatamente para o shell do Windows PowerShell.
Para criar uma unidade mapeada visível no Explorador de Arquivos, é necessário o parâmetro **-Persist**. No entanto, somente caminhos remotos podem ser usados com Persist.


## <a name="reading-a-text-file-into-an-array"></a>Ler um arquivo de texto em uma matriz

Um dos formatos mais comuns de armazenamento para dados de texto é em um arquivo com linhas separadas, tratadas como elementos de dados distintos. O cmdlet **Get-Content** pode ser usado para ler um arquivo inteiro em uma única etapa, como mostrado aqui:

```
PS> Get-Content -Path C:\boot.ini
[boot loader]
timeout=5
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional"
 /noexecute=AlwaysOff /fastdetect
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS=" Microsoft Windows XP Professional
with Data Execution Prevention" /noexecute=optin /fastdetect
```

**Get-Content** já trata os dados lidos do arquivo como uma matriz, com um elemento por linha do conteúdo do arquivo. Você pode confirmar isso verificando o **Length** do conteúdo retornado:

```
PS> (Get-Content -Path C:\boot.ini).Length
6
```

Esse comando é mais útil para obter listas de informações no Windows PowerShell diretamente. Por exemplo, você pode armazenar uma lista de nomes de computador ou de endereços IP em um arquivo C:\\temp\\domainMembers.txt, com um nome em cada linha do arquivo. Você pode usar **Get-Content** para recuperar o conteúdo do arquivo e colocá-lo na variável **$Computers**:

```powershell
$Computers = Get-Content -Path C:\temp\DomainMembers.txt
```

**$Computers** agora é uma matriz que contém um nome do computador em cada elemento.
