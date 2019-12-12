---
title: Código deC#exemplo GetProc02 () | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e4e1eee3-316b-43a4-8a60-313391619be6
caps.latest.revision: 6
ms.openlocfilehash: 5989b1e7030375b1bacdd9b82c25c1a8288fd637
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "72360365"
---
# <a name="getproc02-c-sample-code"></a><span data-ttu-id="a08ad-102">Código de exemplo GetProc02 (C#)</span><span class="sxs-lookup"><span data-stu-id="a08ad-102">GetProc02 (C#) Sample Code</span></span>

<span data-ttu-id="a08ad-103">O código a seguir mostra a implementação de um cmdlet `Get-Process` que aceita a entrada de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="a08ad-103">The following code shows the implementation of a `Get-Process` cmdlet that accepts command-line input.</span></span> <span data-ttu-id="a08ad-104">Observe que essa implementação define um parâmetro `Name` para permitir a entrada da linha de comando e usa o método [WriteObject (System. Object, System. Boolean)](/dotnet/api/system.management.automation.cmdlet.writeobject?view=pscore-6.2.0#System_Management_Automation_Cmdlet_WriteObject_System_Object_System_Boolean_) como o mecanismo de saída para enviar objetos de saída para o pipeline.</span><span class="sxs-lookup"><span data-stu-id="a08ad-104">Notice that this implementation defines a `Name` parameter to allow command-line input, and it uses the [WriteObject(System.Object,System.Boolean)](/dotnet/api/system.management.automation.cmdlet.writeobject?view=pscore-6.2.0#System_Management_Automation_Cmdlet_WriteObject_System_Object_System_Boolean_) method as the output mechanism for sending output objects to the pipeline.</span></span>

## <a name="code-sample"></a><span data-ttu-id="a08ad-105">Exemplo de Código</span><span class="sxs-lookup"><span data-stu-id="a08ad-105">Code Sample</span></span>

[!code-csharp[GetProcessSample02.cs](../../../../powershell-sdk-samples/SDK-2.0/csharp/GetProcessSample02/GetProcessSample02.cs#L11-L76 "GetProcessSample02.cs")]

## <a name="see-also"></a><span data-ttu-id="a08ad-106">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="a08ad-106">See Also</span></span>

[<span data-ttu-id="a08ad-107">SDK do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a08ad-107">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
