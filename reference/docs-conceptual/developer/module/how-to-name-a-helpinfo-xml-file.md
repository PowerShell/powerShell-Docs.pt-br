---
title: Como nomear um arquivo XML HelpInfo | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 64e85b53-5aeb-4d6c-903c-af4ab62f11c1
caps.latest.revision: 7
ms.openlocfilehash: 462cd7bd486a5924bb2bc43e0ac8d1558e30e657
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "72367195"
---
# <a name="how-to-name-a-helpinfo-xml-file"></a><span data-ttu-id="93f81-102">Como nomear um arquivo XML HelpInfo</span><span class="sxs-lookup"><span data-stu-id="93f81-102">How to Name a HelpInfo XML File</span></span>

<span data-ttu-id="93f81-103">Este tópico explica o formato de nome necessário para os arquivos de informações de ajuda atualizáveis, normalmente conhecidos como arquivos XML HelpInfo.</span><span class="sxs-lookup"><span data-stu-id="93f81-103">This topic explains the required name format for the Updatable Help Information files, commonly known as HelpInfo XML files.</span></span>

## <a name="how-to-name-a-helpinfo-xml-file"></a><span data-ttu-id="93f81-104">Como nomear um arquivo XML HelpInfo</span><span class="sxs-lookup"><span data-stu-id="93f81-104">How to Name a HelpInfo XML File</span></span>

<span data-ttu-id="93f81-105">Um arquivo XML HelpInfo deve ter um nome com o formato a seguir.</span><span class="sxs-lookup"><span data-stu-id="93f81-105">A HelpInfo XML file must have a name with the following format.</span></span>

`<ModuleName>_<ModuleGUID>_HelpInfo.xml`

<span data-ttu-id="93f81-106">Os elementos do nome são os seguintes.</span><span class="sxs-lookup"><span data-stu-id="93f81-106">The elements of the name are as follows.</span></span>

<span data-ttu-id="93f81-107">ModuleName o valor da propriedade **Name** do objeto **ModuleInfo** que o cmdlet [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) retorna.</span><span class="sxs-lookup"><span data-stu-id="93f81-107">ModuleName The value of the **Name** property of the **ModuleInfo** object that the [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) cmdlet returns.</span></span>

<span data-ttu-id="93f81-108">ModuleGUID o valor da chave **GUID** no manifesto do módulo.</span><span class="sxs-lookup"><span data-stu-id="93f81-108">ModuleGUID The value of the **GUID** key in the module manifest.</span></span>

<span data-ttu-id="93f81-109">Por exemplo, se o nome do módulo for "TestModule" e o GUID do módulo for 9cabb9ad-f2ac-4914-a46b-bfc1bebf07f9, o nome do arquivo XML HelpInfo para o módulo seria:</span><span class="sxs-lookup"><span data-stu-id="93f81-109">For example, if the module name is "TestModule" and the module GUID is 9cabb9ad-f2ac-4914-a46b-bfc1bebf07f9, the name of the HelpInfo XML file for the module would be:</span></span>

`TestModule_9cabb9ad-f2ac-4914-a46b-bfc1bebf07f9_HelpInfo.xml`