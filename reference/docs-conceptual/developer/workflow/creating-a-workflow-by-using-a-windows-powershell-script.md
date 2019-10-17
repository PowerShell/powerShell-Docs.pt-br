---
title: Criando um fluxo de trabalho usando um script do Windows PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 70532e7e-9cac-43c3-9687-e77011ecc878
caps.latest.revision: 4
ms.openlocfilehash: 5eb2186cbceee21f8b4a8c88b812e9c71f15e0af
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72366025"
---
# <a name="creating-a-workflow-by-using-a-windows-powershell-script"></a><span data-ttu-id="d96ab-102">Criar um fluxo de trabalho pelo uso de um script do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d96ab-102">Creating a Workflow by Using a Windows PowerShell Script</span></span>

<span data-ttu-id="d96ab-103">Você pode criar um fluxo de trabalho escrevendo um script do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d96ab-103">You can create a workflow by writing a Windows PowerShell script.</span></span> <span data-ttu-id="d96ab-104">Para criar um fluxo de trabalho, use a palavra-chave Workflow seguida por um nome para o fluxo de trabalho antes do corpo do script.</span><span class="sxs-lookup"><span data-stu-id="d96ab-104">To create a workflow, use the workflow keyword followed by a name for the workflow before the body of the script.</span></span> <span data-ttu-id="d96ab-105">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d96ab-105">For example:</span></span>

```powershell

workflow Invoke-HelloWorld {"Hello World from workflow"}
```

<span data-ttu-id="d96ab-106">Você encontra o fluxo de trabalho da mesma maneira que faria com qualquer outro comando do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d96ab-106">You find the workflow in the same way you would any other Windows PowerShell command.</span></span>

## <a name="implementing-parallel-and-sequence"></a><span data-ttu-id="d96ab-107">Implementando paralelo e sequência</span><span class="sxs-lookup"><span data-stu-id="d96ab-107">Implementing Parallel and Sequence</span></span>

<span data-ttu-id="d96ab-108">O [Windows Workflow Foundation](https://msdn.microsoft.com/en-us/library/ms735967.aspx) dá suporte à execução de atividades em paralelo.</span><span class="sxs-lookup"><span data-stu-id="d96ab-108">[Windows Workflow Foundation](https://msdn.microsoft.com/en-us/library/ms735967.aspx) supports execution of activities in parallel.</span></span> <span data-ttu-id="d96ab-109">Para implementar esse recurso em um script do Windows PowerShell, use a palavra-chave `parallel` na frente de um bloco de script.</span><span class="sxs-lookup"><span data-stu-id="d96ab-109">To implement this capability in a Windows PowerShell script, use the `parallel` keyword in front of a script block.</span></span> <span data-ttu-id="d96ab-110">Você também pode usar a construção `foreach -parallel` para iterar por meio de uma coleção de objetos em paralelo.</span><span class="sxs-lookup"><span data-stu-id="d96ab-110">You can also use the `foreach -parallel` construction to iterate through a collection of objects in parallel.</span></span> <span data-ttu-id="d96ab-111">Para executar um grupo de atividades em ordem sequencial dentro de um bloco paralelo, coloque esse grupo de atividades em um bloco de script e preceda o bloco com a palavra-chave Sequence.</span><span class="sxs-lookup"><span data-stu-id="d96ab-111">To execute a group of activities in sequential order within a parallel block, enclose that group of activities in a script block and precede the block with the sequence keyword.</span></span>

## <a name="joining-computers-to-a-domain"></a><span data-ttu-id="d96ab-112">Unindo computadores a um domínio</span><span class="sxs-lookup"><span data-stu-id="d96ab-112">Joining Computers to a Domain</span></span>

<span data-ttu-id="d96ab-113">O script a seguir cria um fluxo de trabalho que verifica o status de domínio de um grupo de computadores especificados pelo usuário, une-os a um domínio se eles ainda não estiverem associados e, em seguida, verifica o status novamente.</span><span class="sxs-lookup"><span data-stu-id="d96ab-113">The following script creates a workflow that checks the domain status of a group of user-specified computers, joins them to a domain if they are not already joined, and then checks the status again.</span></span> <span data-ttu-id="d96ab-114">Esta é uma versão de script do fluxo de trabalho XAML explicada na [criação de um fluxo de trabalho com atividades do Windows PowerShell](./creating-a-workflow-with-windows-powershell-activities.md).</span><span class="sxs-lookup"><span data-stu-id="d96ab-114">This is a script version of the XAML workflow explained in [Creating a Workflow with Windows PowerShell Activities](./creating-a-workflow-with-windows-powershell-activities.md).</span></span>

```powershell
workflow Join-Domain
{
    param([string[]] $ComputerName, [PSCredential] $DomainCred, [PsCredential] $MachineCred)

    foreach -parallel($Computer in $ComputerName)
    {
        sequence {
        Get-WmiObject -PSComputerName $Computer -PSCredential $MachineCred
        Add-Computer -PSComputerName $Computer -PSCredential $DomainCred
        Restart-Computer -ComputerName $Computer -Credential $MachineCred -For PowerShell -Force -Wait -PSComputerName ""
        Get-WmiObject -PSComputerName $Computer -PSCredential $MachineCred
        }
    }
 }

```