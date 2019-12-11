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
# <a name="repeating-a-task-for-multiple-objects-foreach-object"></a><span data-ttu-id="19f06-103">Repetir uma tarefa para vários objetos (ForEach-Object)</span><span class="sxs-lookup"><span data-stu-id="19f06-103">Repeating a Task for Multiple Objects (ForEach-Object)</span></span>

<span data-ttu-id="19f06-104">O cmdlet **ForEach-Object** usa blocos de script e o descritor `$_` do objeto de pipeline atual para que você possa executar um comando em cada objeto no pipeline.</span><span class="sxs-lookup"><span data-stu-id="19f06-104">The **ForEach-Object** cmdlet uses script blocks and the `$_` descriptor for the current pipeline object to let you run a command on each object in the pipeline.</span></span> <span data-ttu-id="19f06-105">Isso pode ser usado para executar algumas tarefas complicadas.</span><span class="sxs-lookup"><span data-stu-id="19f06-105">This can be used to perform some complicated tasks.</span></span>

<span data-ttu-id="19f06-106">Uma situação em que isso pode ser útil é manipular dados para torná-los mais úteis.</span><span class="sxs-lookup"><span data-stu-id="19f06-106">One situation where this can be useful is manipulating data to make it more useful.</span></span> <span data-ttu-id="19f06-107">Por exemplo, a classe Win32_LogicalDisk do WMI pode ser usada para retornar informações de espaço livre para cada disco local.</span><span class="sxs-lookup"><span data-stu-id="19f06-107">For example, the Win32_LogicalDisk class from WMI can be used to return free space information for each local disk.</span></span> <span data-ttu-id="19f06-108">Contudo, os dados são retornados em bytes, o que dificulta a leitura:</span><span class="sxs-lookup"><span data-stu-id="19f06-108">The data is returned in terms of bytes, however, which makes it difficult to read:</span></span>

```
PS> Get-WmiObject -Class Win32_LogicalDisk

DeviceID     : C:
DriveType    : 3
ProviderName :
FreeSpace    : 50665070592
Size         : 203912880128
VolumeName   : Local Disk
```

<span data-ttu-id="19f06-109">Podemos pode converter o valor de FreeSpace em megabytes dividindo cada valor por 1024 duas vezes. Após a primeira divisão, os dados estão em quilobytes e após a segunda divisão estão em megabytes.</span><span class="sxs-lookup"><span data-stu-id="19f06-109">We can convert the FreeSpace value to megabytes by dividing each value by 1024 twice; after the first division, the data is in kilobytes, and after the second division it is megabytes.</span></span> <span data-ttu-id="19f06-110">Você pode fazer isso em um bloco de script do ForEach-Object digitando:</span><span class="sxs-lookup"><span data-stu-id="19f06-110">You can do that in a ForEach-Object script block by typing:</span></span>

```
PS> Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {($_.FreeSpace)/1024.0/1024.0}
48318.01171875
```

<span data-ttu-id="19f06-111">Infelizmente, a saída agora é de dados sem nenhum rótulo associado.</span><span class="sxs-lookup"><span data-stu-id="19f06-111">Unfortunately, the output is now data with no associated label.</span></span> <span data-ttu-id="19f06-112">Como propriedades WMI como esta são somente leitura, não é possível converter diretamente o FreeSpace.</span><span class="sxs-lookup"><span data-stu-id="19f06-112">Because WMI properties such as this are read-only, you cannot directly convert FreeSpace.</span></span> <span data-ttu-id="19f06-113">Se você digitar:</span><span class="sxs-lookup"><span data-stu-id="19f06-113">If you type this:</span></span>

```powershell
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

<span data-ttu-id="19f06-114">Receberá uma mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="19f06-114">You get an error message:</span></span>

```output
"FreeSpace" is a ReadOnly property.
At line:1 char:70
+ Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.F <<<< r
eeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

<span data-ttu-id="19f06-115">Você pode reorganizar os dados usando algumas técnicas avançadas, mas uma abordagem mais simples é criar um novo objeto usando **Select-Object**.</span><span class="sxs-lookup"><span data-stu-id="19f06-115">You could reorganize the data by using some advanced techniques, but a simpler approach is to create a new object, by using **Select-Object**.</span></span>
