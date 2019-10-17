---
title: Exemplos de código de cmdlet | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6fed2f68-ce6d-4a8f-bf21-f94f27a155c2
caps.latest.revision: 9
ms.openlocfilehash: 936728d64f30a08fb9e2fa9ccef103683594aa3e
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72364495"
---
# <a name="examples-of-cmdlet-code"></a><span data-ttu-id="8753f-102">Exemplos de código do cmdlet</span><span class="sxs-lookup"><span data-stu-id="8753f-102">Examples of Cmdlet Code</span></span>

<span data-ttu-id="8753f-103">Esta seção contém exemplos de código de cmdlet que você pode usar para começar a escrever seus próprios cmdlets.</span><span class="sxs-lookup"><span data-stu-id="8753f-103">This section contains examples of cmdlet code that you can use to start writing your own cmdlets.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8753f-104">Se você quiser obter instruções passo a passo para escrever cmdlets, consulte [tutoriais para escrever cmdlets](./tutorials-for-writing-cmdlets.md).</span><span class="sxs-lookup"><span data-stu-id="8753f-104">If you want step-by-step instructions for writing cmdlets, see [Tutorials for Writing Cmdlets](./tutorials-for-writing-cmdlets.md).</span></span>

## <a name="in-this-section"></a><span data-ttu-id="8753f-105">Nesta seção</span><span class="sxs-lookup"><span data-stu-id="8753f-105">In This Section</span></span>

<span data-ttu-id="8753f-106">[Como escrever um cmdlet simples](./how-to-write-a-simple-cmdlet.md) Este exemplo mostra a estrutura básica do código do cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8753f-106">[How to Write a Simple Cmdlet](./how-to-write-a-simple-cmdlet.md) This example shows the basic structure of cmdlet code.</span></span>

<span data-ttu-id="8753f-107">[Como declarar parâmetros de cmdlet](./how-to-declare-cmdlet-parameters.md) Este exemplo mostra como declarar os diferentes tipos de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="8753f-107">[How to Declare Cmdlet Parameters](./how-to-declare-cmdlet-parameters.md) This example shows how to declare the different types of parameters.</span></span>

<span data-ttu-id="8753f-108">[Como declarar conjuntos de parâmetros](./how-to-declare-parameter-sets.md) Este exemplo mostra como declarar conjuntos de parâmetros que podem alterar a ação que um cmdlet executa.</span><span class="sxs-lookup"><span data-stu-id="8753f-108">[How to Declare Parameter Sets](./how-to-declare-parameter-sets.md) This example shows how to declare sets of parameters that can change the action a cmdlet performs.</span></span>

<span data-ttu-id="8753f-109">[Como validar a entrada de parâmetro](./how-to-validate-parameter-input.md) Estes exemplos mostram como validar a entrada de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="8753f-109">[How to Validate Parameter Input](./how-to-validate-parameter-input.md) These examples show how to validate parameter input.</span></span>

<span data-ttu-id="8753f-110">[Como declarar parâmetros dinâmicos](./how-to-declare-dynamic-parameters.md) Este exemplo mostra como declarar um parâmetro que é adicionado no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="8753f-110">[How to Declare Dynamic Parameters](./how-to-declare-dynamic-parameters.md) This example shows how to declare a parameter that is added at runtime.</span></span>

<span data-ttu-id="8753f-111">[Como invocar scripts dentro de um cmdlet](./how-to-invoke-scripts-within-a-cmdlet.md) Este exemplo mostra como invocar um script que é fornecido a um cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8753f-111">[How to Invoke Scripts Within a Cmdlet](./how-to-invoke-scripts-within-a-cmdlet.md) This example shows how to invoke a script that is supplied to a cmdlet.</span></span>

<span data-ttu-id="8753f-112">[Como substituir métodos de processamento de entrada](./how-to-override-input-processing-methods.md) Esses exemplos mostram a estrutura básica usada para substituir os métodos BeginProcessing, ProcessRecord e endprocessor.</span><span class="sxs-lookup"><span data-stu-id="8753f-112">[How To Override Input Processing Methods](./how-to-override-input-processing-methods.md) These examples show the basic structure used to override the BeginProcessing, ProcessRecord, and EndProcessing methods.</span></span>

<span data-ttu-id="8753f-113">[Como dar suporte a chamadas de ShouldProcess](./how-to-request-confirmations.md) Este exemplo mostra como os métodos [System. Management. Automation. cmdlet. ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) e [System. Management. Automation. cmdlet. ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) devem ser chamados de dentro de um cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8753f-113">[How to Support ShouldProcess Calls](./how-to-request-confirmations.md) This example shows how the [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) and [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) methods should be called from within a cmdlet.</span></span>

<span data-ttu-id="8753f-114">[Como dar suporte a transações](./how-to-support-transactions.md) Este exemplo mostra como indicar que o cmdlet dá suporte a transações e como implementar a ação que é executada quando o cmdlet é usado em uma transação.</span><span class="sxs-lookup"><span data-stu-id="8753f-114">[How to Support Transactions](./how-to-support-transactions.md) This example shows how to indicate that the cmdlet supports transactions and how to implement the action that is taken when the cmdlet is used within a transaction.</span></span>

<span data-ttu-id="8753f-115">[Como dar suporte a trabalhos](./how-to-support-jobs.md) Este exemplo mostra como dar suporte a trabalhos quando você escreve cmdlets.</span><span class="sxs-lookup"><span data-stu-id="8753f-115">[How to Support Jobs](./how-to-support-jobs.md) This example shows how to support jobs when you write cmdlets.</span></span>

<span data-ttu-id="8753f-116">[Como invocar um cmdlet de dentro de um cmdlet](./how-to-invoke-a-cmdlet-from-within-a-cmdlet.md) Este exemplo mostra como invocar um cmdlet de dentro de outro cmdlet, que permite adicionar a funcionalidade do cmdlet invocado ao cmdlet que você está desenvolvendo.</span><span class="sxs-lookup"><span data-stu-id="8753f-116">[How to Invoke a Cmdlet From Within a Cmdlet](./how-to-invoke-a-cmdlet-from-within-a-cmdlet.md) This example shows how to invoke a cmdlet from within another cmdlet, which allows you to add the functionality of the invoked cmdlet to the cmdlet you are developing.</span></span>

## <a name="see-also"></a><span data-ttu-id="8753f-117">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="8753f-117">See Also</span></span>

<span data-ttu-id="8753f-118">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md) (Escrevendo um Cmdlet do Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="8753f-118">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md)</span></span>