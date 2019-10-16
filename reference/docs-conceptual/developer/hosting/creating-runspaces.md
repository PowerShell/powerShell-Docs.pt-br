---
title: Criando espaços de Runspaces | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 17f323c3-e873-449e-8a28-477f1c6b5e12
caps.latest.revision: 6
ms.openlocfilehash: b4e61600f68521e4e7ab56ceae3349381e88a70a
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72367575"
---
# <a name="creating-runspaces"></a><span data-ttu-id="ce3f3-102">Criar runspaces</span><span class="sxs-lookup"><span data-stu-id="ce3f3-102">Creating Runspaces</span></span>

<span data-ttu-id="ce3f3-103">Um runspace é o ambiente operacional para os comandos que são invocados por um aplicativo host.</span><span class="sxs-lookup"><span data-stu-id="ce3f3-103">A runspace is the operating environment for the commands that are invoked by a host application.</span></span> <span data-ttu-id="ce3f3-104">Esse ambiente inclui os comandos e dados atualmente presentes e as restrições de idioma que se aplicam atualmente.</span><span class="sxs-lookup"><span data-stu-id="ce3f3-104">This environment includes the commands and data that are currently present, and any language restrictions that currently apply.</span></span>

 <span data-ttu-id="ce3f3-105">Os aplicativos host podem usar o runspace padrão fornecido pelo Windows PowerShell, que inclui todos os comandos de núcleo disponíveis, ou criar um runspace personalizado que inclui apenas um subconjunto dos comandos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="ce3f3-105">Host applications can use the default runspace that is provided by Windows PowerShell, which includes all available core commands, or create a custom runspace that includes only a subset of the available commands.</span></span> <span data-ttu-id="ce3f3-106">Para criar um runspace personalizado, você cria um objeto [System. Management. Automation. Runspaces. Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) e o atribui ao runspace.</span><span class="sxs-lookup"><span data-stu-id="ce3f3-106">To create a customized runspace, you create an [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) object and assign it to your runspace.</span></span>

## <a name="runspace-tasks"></a><span data-ttu-id="ce3f3-107">Tarefas do runspace</span><span class="sxs-lookup"><span data-stu-id="ce3f3-107">Runspace tasks</span></span>

1. [<span data-ttu-id="ce3f3-108">Criando um InitialSessionState</span><span class="sxs-lookup"><span data-stu-id="ce3f3-108">Creating an InitialSessionState</span></span>](./creating-an-initialsessionstate.md)

2. [<span data-ttu-id="ce3f3-109">Criando um runspace restrito</span><span class="sxs-lookup"><span data-stu-id="ce3f3-109">Creating a constrained runspace</span></span>](./creating-a-constrained-runspace.md)

3. [<span data-ttu-id="ce3f3-110">Criando vários Runspaces</span><span class="sxs-lookup"><span data-stu-id="ce3f3-110">Creating multiple runspaces</span></span>](./creating-multiple-runspaces.md)

## <a name="see-also"></a><span data-ttu-id="ce3f3-111">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="ce3f3-111">See Also</span></span>
