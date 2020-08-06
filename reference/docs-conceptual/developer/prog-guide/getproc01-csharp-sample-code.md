---
title: Código de exemplo de GetProc01 (C#) | Microsoft Docs
ms.date: 09/13/2016
ms.openlocfilehash: 883beb9dd1328a1897b9b61656a98cf515a21be7
ms.sourcegitcommit: 0907b8c6322d2c7c61b17f8168d53452c8964b41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/05/2020
ms.locfileid: "87778893"
---
# <a name="getproc01-c-sample-code"></a><span data-ttu-id="219bc-102">Código de exemplo GetProc01 (C#)</span><span class="sxs-lookup"><span data-stu-id="219bc-102">GetProc01 (C#) Sample Code</span></span>

<span data-ttu-id="219bc-103">O código a seguir mostra a implementação do cmdlet de exemplo GetProc01.</span><span class="sxs-lookup"><span data-stu-id="219bc-103">The following code shows the implementation of the GetProc01 sample cmdlet.</span></span> <span data-ttu-id="219bc-104">Observe que o cmdlet é simplificado deixando o trabalho real de recuperação do processo com o método [System. Diagnostics. Process. GetProcesses \*](/dotnet/api/System.Diagnostics.Process.GetProcesses) .</span><span class="sxs-lookup"><span data-stu-id="219bc-104">Notice that the cmdlet is simplified by leaving the actual work of process retrieval to the [System.Diagnostics.Process.Getprocesses\*](/dotnet/api/System.Diagnostics.Process.GetProcesses) method.</span></span>

> [!NOTE]
> <span data-ttu-id="219bc-105">Você pode baixar o arquivo de origem do C# (getproc01.cs) para este cmdlet Get-proc usando o Microsoft Windows Software Development Kit para Windows Vista e .NET Framework os componentes de tempo de execução do 3,0.</span><span class="sxs-lookup"><span data-stu-id="219bc-105">You can download the C# source file (getproc01.cs) for this Get-Proc cmdlet using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="219bc-106">Para obter instruções de download, consulte [como instalar o Windows PowerShell e baixar o SDK do Windows PowerShell](/powershell/scripting/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="219bc-106">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/scripting/developer/installing-the-windows-powershell-sdk).</span></span>
> <span data-ttu-id="219bc-107">Os arquivos de origem baixados estão disponíveis no **\<PowerShell Samples>** diretório.</span><span class="sxs-lookup"><span data-stu-id="219bc-107">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="219bc-108">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="219bc-108">Code Sample</span></span>

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/GetProcessSample01/GetProcessSample01.cs" range="11-126":::

## <a name="see-also"></a><span data-ttu-id="219bc-109">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="219bc-109">See Also</span></span>

[<span data-ttu-id="219bc-110">Guia do programador do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="219bc-110">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="219bc-111">SDK do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="219bc-111">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
