---
title: Exemplo de código RunSpace05 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9688cd69-07ea-4ea0-8822-0a4850bcf86c
caps.latest.revision: 7
ms.openlocfilehash: a99d0cc0dd35ae4c1a52e3624a9dd5af2a26c97a
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72360135"
---
# <a name="runspace05-code-sample"></a><span data-ttu-id="af84c-102">Exemplo de código RunSpace05</span><span class="sxs-lookup"><span data-stu-id="af84c-102">RunSpace05 Code Sample</span></span>

<span data-ttu-id="af84c-103">Este é o código-fonte do exemplo Runspace05 descrito em [Configurando um runspace usando RunspaceConfiguration](https://msdn.microsoft.com/en-us/42681d19-2d05-4975-befd-afb1990e79b2).</span><span class="sxs-lookup"><span data-stu-id="af84c-103">Here is the source code for the Runspace05 sample that is described in [Configuring a Runspace Using RunspaceConfiguration](https://msdn.microsoft.com/en-us/42681d19-2d05-4975-befd-afb1990e79b2).</span></span> <span data-ttu-id="af84c-104">Este exemplo mostra como criar as informações de configuração do runspace, criar um runspace, criar um pipeline com um único comando e, em seguida, executar o pipeline.</span><span class="sxs-lookup"><span data-stu-id="af84c-104">This sample shows how to create the runspace configuration information, create a runspace, create a pipeline with a single command, and then execute the pipeline.</span></span> <span data-ttu-id="af84c-105">O comando executado é o cmdlet `Get-Process`.</span><span class="sxs-lookup"><span data-stu-id="af84c-105">The command that is executed is the `Get-Process` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="af84c-106">Você pode baixar o C# arquivo de origem (runspace05.cs) usando o Microsoft Windows Software Development Kit para Windows Vista e Microsoft .NET Framework 3,0 Runtime Components.</span><span class="sxs-lookup"><span data-stu-id="af84c-106">You can download the C# source file (runspace05.cs) by using the Microsoft Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="af84c-107">Para obter instruções de download, consulte [como instalar o Windows PowerShell e baixar o SDK do Windows PowerShell](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="af84c-107">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="af84c-108">Os arquivos de origem baixados estão disponíveis no diretório de **exemplos do \<PowerShell >** .</span><span class="sxs-lookup"><span data-stu-id="af84c-108">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="af84c-109">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="af84c-109">Code Sample</span></span>

[!code-csharp[Runspace05.cs](../../../../powershell-sdk-samples/SDK-2.0/csharp/Runspace05/Runspace05.cs#L11-L86 "Runspace05.cs")]

## <a name="see-also"></a><span data-ttu-id="af84c-110">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="af84c-110">See Also</span></span>

[<span data-ttu-id="af84c-111">Guia do programador do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="af84c-111">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="af84c-112">SDK do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="af84c-112">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
