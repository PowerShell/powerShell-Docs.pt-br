---
title: Exemplos de cmdlet | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b99d53fc-0af9-426b-82ce-09955e031d4b
caps.latest.revision: 13
ms.openlocfilehash: 0fa4a5f804586c51ae6a36121f9aab041b0989cc
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72365875"
---
# <a name="cmdlet-samples"></a><span data-ttu-id="a8d79-102">Amostras de cmdlet</span><span class="sxs-lookup"><span data-stu-id="a8d79-102">Cmdlet Samples</span></span>

<span data-ttu-id="a8d79-103">Esta seção descreve o código de exemplo que é fornecido no SDK do Windows PowerShell 2,0.</span><span class="sxs-lookup"><span data-stu-id="a8d79-103">This section describes sample code that is provided in the Windows PowerShell 2.0 SDK.</span></span> <span data-ttu-id="a8d79-104">Você pode copiar o código dos tópicos nesta seção ou abrir os arquivos de origem instalados com o SDK.</span><span class="sxs-lookup"><span data-stu-id="a8d79-104">You can copy code from the topics in this section, or open the source files installed with the SDK.</span></span> <span data-ttu-id="a8d79-105">O [SDK (Software Development Kit) do Windows PowerShell 2,0](https://www.microsoft.com/en-us/download/details.aspx?id=2560) fornece arquivos leiame, arquivos de origem e arquivos de projeto do Visual Studio para cada exemplo.</span><span class="sxs-lookup"><span data-stu-id="a8d79-105">The [Windows PowerShell 2.0 Software Development Kit (SDK)](https://www.microsoft.com/en-us/download/details.aspx?id=2560) provides ReadMe files, source files, and Visual Studio project files for each sample.</span></span> <span data-ttu-id="a8d79-106">Com o SDK instalado, você pode encontrar os exemplos na pasta `<Drive>:\Program Files (x86)\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\`.</span><span class="sxs-lookup"><span data-stu-id="a8d79-106">With the SDK installed, you can find the samples under the `<Drive>:\Program Files (x86)\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\` folder.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="a8d79-107">Nesta seção</span><span class="sxs-lookup"><span data-stu-id="a8d79-107">In This Section</span></span>

<span data-ttu-id="a8d79-108">[Exemplo de GetProcessSample01](./getprocesssample01-sample.md) Este exemplo mostra como escrever um cmdlet que recupera os processos no computador local.</span><span class="sxs-lookup"><span data-stu-id="a8d79-108">[GetProcessSample01 Sample](./getprocesssample01-sample.md) This sample shows how to write a cmdlet that retrieves the processes on the local computer.</span></span>

<span data-ttu-id="a8d79-109">[Exemplo de GetProcessSample02](./getprocesssample02-sample.md) Este exemplo mostra como escrever um cmdlet que recupera os processos no computador local.</span><span class="sxs-lookup"><span data-stu-id="a8d79-109">[GetProcessSample02 Sample](./getprocesssample02-sample.md) This sample shows how to write a cmdlet that retrieves the processes on the local computer.</span></span> <span data-ttu-id="a8d79-110">Ele fornece um parâmetro de nome que pode ser usado para especificar os processos a serem recuperados.</span><span class="sxs-lookup"><span data-stu-id="a8d79-110">It provides a Name parameter that can be used to specify the processes to be retrieved.</span></span>

<span data-ttu-id="a8d79-111">[Exemplo de GetProcessSample03](./getprocesssample03-sample.md) Este exemplo mostra como escrever um cmdlet que recupera os processos no computador local.</span><span class="sxs-lookup"><span data-stu-id="a8d79-111">[GetProcessSample03 Sample](./getprocesssample03-sample.md) This sample shows how to write a cmdlet that retrieves the processes on the local computer.</span></span> <span data-ttu-id="a8d79-112">Ele fornece um parâmetro de nome que pode aceitar um objeto do pipeline ou um valor de uma propriedade de um objeto cujo nome de propriedade é igual ao nome do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a8d79-112">It provides a Name parameter that can accept an object from the pipeline or a value from a property of an object whose property name is the same as the parameter name.</span></span>

<span data-ttu-id="a8d79-113">[Exemplo de GetProcessSample04](./getprocesssample04-sample.md) Este exemplo mostra como escrever um cmdlet que recupera os processos no computador local.</span><span class="sxs-lookup"><span data-stu-id="a8d79-113">[GetProcessSample04 Sample](./getprocesssample04-sample.md) This sample shows how to write a cmdlet that retrieves the processes on the local computer.</span></span> <span data-ttu-id="a8d79-114">Ele gera um erro de não encerramento se ocorrer um erro durante a recuperação de um processo.</span><span class="sxs-lookup"><span data-stu-id="a8d79-114">It generates a nonterminating error if an error occurs while retrieving a process.</span></span>

<span data-ttu-id="a8d79-115">[Exemplo de GetProcessSample05](./getprocesssample05-sample.md) Este exemplo mostra uma versão completa do cmdlet Get-proc.</span><span class="sxs-lookup"><span data-stu-id="a8d79-115">[GetProcessSample05 Sample](./getprocesssample05-sample.md) This sample shows a complete version of the Get-Proc cmdlet.</span></span>

<span data-ttu-id="a8d79-116">[Exemplo de StopProcessSample01](./stopprocesssample01-sample.md) Este exemplo mostra como escrever um cmdlet que solicita comentários do usuário antes de tentar parar um processo e como implementar um parâmetro `PassThru` que indica que o usuário deseja que o cmdlet retorne um objeto.</span><span class="sxs-lookup"><span data-stu-id="a8d79-116">[StopProcessSample01 Sample](./stopprocesssample01-sample.md) This sample shows how to write a cmdlet that requests feedback from the user before it attempts to stop a process, and how to implement a `PassThru` parameter that indicates that the user wants the cmdlet to return an object.</span></span>

<span data-ttu-id="a8d79-117">[Exemplo de StopProcessSample02](./stopprocesssample02-sample.md) Este exemplo mostra como escrever um cmdlet que grava mensagens de depuração, detalhadas e de aviso ao parar os processos no computador local.</span><span class="sxs-lookup"><span data-stu-id="a8d79-117">[StopProcessSample02 Sample](./stopprocesssample02-sample.md) This sample shows how to write a cmdlet that writes debug, verbose, and warning messages while stopping processes on the local computer.</span></span>

<span data-ttu-id="a8d79-118">[Exemplo de StopProcessSample03](./stopprocesssample03-sample.md) Este exemplo mostra como escrever um cmdlet cujos parâmetros têm aliases e que dão suporte a caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="a8d79-118">[StopProcessSample03 Sample](./stopprocesssample03-sample.md) This sample shows how to write a cmdlet whose parameters have aliases and that support wildcard characters.</span></span>

<span data-ttu-id="a8d79-119">[Exemplo de StopProcessSample04](./stopprocesssample04-sample.md) Este exemplo mostra como escrever um cmdlet que declara conjuntos de parâmetros, especifica o conjunto de parâmetros padrão e pode aceitar um objeto de entrada.</span><span class="sxs-lookup"><span data-stu-id="a8d79-119">[StopProcessSample04 Sample](./stopprocesssample04-sample.md) This sample shows how to write a cmdlet that declares parameter sets, specifies the default parameter set, and can accept an input object.</span></span>

<span data-ttu-id="a8d79-120">[Exemplo de Events01](./events01-sample.md) Este exemplo mostra como criar um cmdlet que permite ao usuário se registrar para eventos gerados por [System. IO. FileSystemWatcher](/dotnet/api/System.IO.FileSystemWatcher).</span><span class="sxs-lookup"><span data-stu-id="a8d79-120">[Events01 Sample](./events01-sample.md) This sample shows how to create a cmdlet that allows the user to register for events raised by [System.IO.Filesystemwatcher](/dotnet/api/System.IO.FileSystemWatcher).</span></span> <span data-ttu-id="a8d79-121">Com esse cmdlet, os usuários podem, por exemplo, registrar uma ação a ser executada quando um arquivo é criado em um diretório específico.</span><span class="sxs-lookup"><span data-stu-id="a8d79-121">With this cmdlet users can, for example, register an action to execute when a file is created under a specific directory.</span></span> <span data-ttu-id="a8d79-122">Este exemplo deriva da classe base [Microsoft. PowerShell. Commands. Objecteventregistrationbase](/dotnet/api/Microsoft.PowerShell.Commands.ObjectEventRegistrationBase) .</span><span class="sxs-lookup"><span data-stu-id="a8d79-122">This sample derives from the [Microsoft.PowerShell.Commands.Objecteventregistrationbase](/dotnet/api/Microsoft.PowerShell.Commands.ObjectEventRegistrationBase) base class.</span></span>

## <a name="see-also"></a><span data-ttu-id="a8d79-123">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="a8d79-123">See Also</span></span>

<span data-ttu-id="a8d79-124">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md) (Escrevendo um Cmdlet do Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="a8d79-124">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md)</span></span>