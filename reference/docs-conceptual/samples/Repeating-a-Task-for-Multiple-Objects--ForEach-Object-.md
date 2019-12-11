---
ms.date: 06/05/2017
keywords: powershell, cmdlet
title: Repetir uma tarefa para vários objetos ForEach Object
ms.openlocfilehash: 1442507c4213476f65df3401c1021f8d0fc31956
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "67030808"
---
# <a name="repeating-a-task-for-multiple-objects-foreach-object"></a>Repetir uma tarefa para vários objetos (ForEach-Object)

O cmdlet **ForEach-Object** usa blocos de script e o descritor `$_` do objeto de pipeline atual para que você possa executar um comando em cada objeto no pipeline. Isso pode ser usado para executar algumas tarefas complicadas.

Uma situação em que isso pode ser útil é manipular dados para torná-los mais úteis. Por exemplo, a classe Win32_LogicalDisk do WMI pode ser usada para retornar informações de espaço livre para cada disco local. Contudo, os dados são retornados em bytes, o que dificulta a leitura:

```
PS> Get-WmiObject -Class Win32_LogicalDisk

DeviceID     : C:
DriveType    : 3
ProviderName :
FreeSpace    : 50665070592
Size         : 203912880128
VolumeName   : Local Disk
```

Podemos pode converter o valor de FreeSpace em megabytes dividindo cada valor por 1024 duas vezes. Após a primeira divisão, os dados estão em quilobytes e após a segunda divisão estão em megabytes. Você pode fazer isso em um bloco de script do ForEach-Object digitando:

```
PS> Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {($_.FreeSpace)/1024.0/1024.0}
48318.01171875
```

Infelizmente, a saída agora é de dados sem nenhum rótulo associado. Como propriedades WMI como esta são somente leitura, não é possível converter diretamente o FreeSpace. Se você digitar:

```powershell
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

Receberá uma mensagem de erro:

```output
"FreeSpace" is a ReadOnly property.
At line:1 char:70
+ Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.F <<<< r
eeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

Você pode reorganizar os dados usando algumas técnicas avançadas, mas uma abordagem mais simples é criar um novo objeto usando **Select-Object**.
