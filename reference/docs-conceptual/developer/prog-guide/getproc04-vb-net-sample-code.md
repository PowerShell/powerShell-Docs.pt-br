---
title: Código de exemplo do GetProc04 (VB.NET) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5d22f47b-3679-4587-a559-94454415d2dd
caps.latest.revision: 5
ms.openlocfilehash: f2164b97e4f3b3346e66d00834aa299659b62b33
ms.sourcegitcommit: d43f66071f1f33b350d34fa1f46f3a35910c5d24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2019
ms.locfileid: "74416099"
---
# <a name="getproc04-vbnet-sample-code"></a><span data-ttu-id="74f06-102">Código de exemplo GetProc04 (VB.NET)</span><span class="sxs-lookup"><span data-stu-id="74f06-102">GetProc04 (VB.NET) Sample Code</span></span>

<span data-ttu-id="74f06-103">O código a seguir mostra a implementação de um cmdlet `Get-Process` que relata erros de não encerramento.</span><span class="sxs-lookup"><span data-stu-id="74f06-103">The following code shows the implementation of a `Get-Process` cmdlet that reports nonterminating errors.</span></span> <span data-ttu-id="74f06-104">Essa implementação chama o método [System. Management. Automation. cmdlet. WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) para relatar erros de não encerramento.</span><span class="sxs-lookup"><span data-stu-id="74f06-104">This implementation calls the [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) method to report nonterminating errors.</span></span>

> [!NOTE]
> <span data-ttu-id="74f06-105">Você pode baixar o C# arquivo de origem (getprov04.cs) para este cmdlet Get-proc usando o kit de desenvolvimento de software do Microsoft Windows para Windows Vista e .NET Framework os componentes de tempo de execução do 3,0.</span><span class="sxs-lookup"><span data-stu-id="74f06-105">You can download the C# source file (getprov04.cs) for this Get-Proc cmdlet using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="74f06-106">Para obter instruções de download, consulte [como instalar o Windows PowerShell e baixar o SDK do Windows PowerShell](/powershell/scripting/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="74f06-106">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/scripting/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="74f06-107">Os arquivos de origem baixados estão disponíveis no **\<exemplos do PowerShell >** diretório.</span><span class="sxs-lookup"><span data-stu-id="74f06-107">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="74f06-108">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="74f06-108">Code Sample</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplesgetproc04#GetProc04vball](Msh_samplesgetproc04#GetProc04vball)]  -->

## <a name="see-also"></a><span data-ttu-id="74f06-109">Consulte também</span><span class="sxs-lookup"><span data-stu-id="74f06-109">See Also</span></span>

[<span data-ttu-id="74f06-110">Guia do programador do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="74f06-110">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="74f06-111">SDK do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="74f06-111">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
