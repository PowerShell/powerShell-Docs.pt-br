---
title: Criando uma interface do usuário personalizada | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d7286443-eed4-43d5-b809-50cdcdcba088
caps.latest.revision: 4
ms.openlocfilehash: 23518c625fe1138e1bd2bcc895274cb21d7daf8a
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72367625"
---
# <a name="creating-a-custom-user-interface"></a><span data-ttu-id="4828e-102">Criar uma interface do usuário personalizada</span><span class="sxs-lookup"><span data-stu-id="4828e-102">Creating a custom user interface</span></span>

<span data-ttu-id="4828e-103">O Windows PowerShell fornece classes e interfaces abstratas que permitem criar uma interface do usuário interativa personalizada que hospeda o mecanismo do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4828e-103">Windows PowerShell provides abstract classes and interfaces that allow you to create a custom interactive UI that hosts the Windows PowerShell engine.</span></span> <span data-ttu-id="4828e-104">Para criar uma interface do usuário personalizada, você deve implementar a classe [System. Management. Automation. host. PSHost](/dotnet/api/System.Management.Automation.Host.PSHost) .</span><span class="sxs-lookup"><span data-stu-id="4828e-104">To create a custom UI, you must implement the [System.Management.Automation.Host.PSHost](/dotnet/api/System.Management.Automation.Host.PSHost) class.</span></span> <span data-ttu-id="4828e-105">Opcionalmente, você também pode implementar as classes [System. Management. Automation. host. Pshostrawuserinterface](/dotnet/api/System.Management.Automation.Host.PSHostRawUserInterface)e [System. Management. Automation. host. Pshostuserinterface](/dotnet/api/System.Management.Automation.Host.PSHostUserInterface) e o [ System. Management. Automation. host. Ihostsupportsinteractivesession](/dotnet/api/System.Management.Automation.Host.IHostSupportsInteractiveSession) e [System. Management. Automation. host. Ihostuisupportsmultiplechoiceselection](/dotnet/api/System.Management.Automation.Host.IHostUISupportsMultipleChoiceSelection) interfaces.</span><span class="sxs-lookup"><span data-stu-id="4828e-105">Optionally, you can also implement the [System.Management.Automation.Host.Pshostrawuserinterface](/dotnet/api/System.Management.Automation.Host.PSHostRawUserInterface)and [System.Management.Automation.Host.Pshostuserinterface](/dotnet/api/System.Management.Automation.Host.PSHostUserInterface) classes, and the [System.Management.Automation.Host.Ihostsupportsinteractivesession](/dotnet/api/System.Management.Automation.Host.IHostSupportsInteractiveSession) and [System.Management.Automation.Host.Ihostuisupportsmultiplechoiceselection](/dotnet/api/System.Management.Automation.Host.IHostUISupportsMultipleChoiceSelection) interfaces.</span></span>
