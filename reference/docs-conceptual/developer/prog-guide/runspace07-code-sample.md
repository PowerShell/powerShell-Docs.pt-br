---
title: Exemplo de código RunSpace07 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8ad306d9-45c2-4d55-8e64-fdcba43402c5
caps.latest.revision: 6
ms.openlocfilehash: 55005a254ef50a2230121095770899cb3b9b70f1
ms.sourcegitcommit: 7f2479edd329dfdc55726afff7019d45e45f9156
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80978212"
---
# <a name="runspace07-code-sample"></a><span data-ttu-id="643be-102">Exemplo de código RunSpace07</span><span class="sxs-lookup"><span data-stu-id="643be-102">RunSpace07 Code Sample</span></span>

<span data-ttu-id="643be-103">Aqui está o código-fonte para o exemplo de Runspace07 descrito em [criando um aplicativo de console que adiciona comandos a um pipeline](https://msdn.microsoft.com/01eb7808-e97b-4905-80be-9e2fa38c262e).</span><span class="sxs-lookup"><span data-stu-id="643be-103">Here is the source code for the Runspace07 sample described in [Creating a Console Application That Adds Commands to a Pipeline](https://msdn.microsoft.com/01eb7808-e97b-4905-80be-9e2fa38c262e).</span></span>
<span data-ttu-id="643be-104">Esse aplicativo de exemplo cria um runspace, cria um pipeline, adiciona dois comandos ao pipeline e, em seguida, executa o pipeline.</span><span class="sxs-lookup"><span data-stu-id="643be-104">This sample application creates a runspace, creates a pipeline, adds two commands to the pipeline, and then executes the pipeline.</span></span> <span data-ttu-id="643be-105">Os comandos adicionados ao pipeline são os cmdlets `Get-Process` e `Measure-Object`.</span><span class="sxs-lookup"><span data-stu-id="643be-105">The commands added to the pipeline are the `Get-Process` and `Measure-Object` cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="643be-106">Você pode baixar o C# arquivo de origem (runspace07.cs) usando o Microsoft Windows Software Development Kit para Windows Vista e Microsoft .NET Framework 3,0 Runtime Components.</span><span class="sxs-lookup"><span data-stu-id="643be-106">You can download the C# source file (runspace07.cs) using the Microsoft Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="643be-107">Para obter instruções de download, consulte [como instalar o Windows PowerShell e baixar o SDK do Windows PowerShell](/powershell/scripting/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="643be-107">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/scripting/developer/installing-the-windows-powershell-sdk).</span></span>
> <span data-ttu-id="643be-108">Os arquivos de origem baixados estão disponíveis no **\<exemplos do PowerShell >** diretório.</span><span class="sxs-lookup"><span data-stu-id="643be-108">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="643be-109">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="643be-109">Code Sample</span></span>

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/Runspace07/Runspace07.cs" range="11-108":::

## <a name="see-also"></a><span data-ttu-id="643be-110">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="643be-110">See Also</span></span>

[<span data-ttu-id="643be-111">Guia do programador do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="643be-111">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="643be-112">SDK do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="643be-112">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
