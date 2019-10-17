---
title: Referência do Windows PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Windows PowerShell SDK
ms.assetid: cbba4879-bcac-484a-9906-4bbe2cd1eb33
caps.latest.revision: 11
ms.openlocfilehash: 48b2b2b9ab2a39cf185ed54bcfa99d46562e13b6
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72366275"
---
# <a name="windows-powershell-reference"></a><span data-ttu-id="d628b-102">Referência do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d628b-102">Windows PowerShell Reference</span></span>

<span data-ttu-id="d628b-103">O Windows PowerShell é um ambiente conectado à estrutura Microsoft .NET projetado para automação administrativa.</span><span class="sxs-lookup"><span data-stu-id="d628b-103">Windows PowerShell is a Microsoft .NET Framework-connected environment designed for administrative automation.</span></span> <span data-ttu-id="d628b-104">O Windows PowerShell fornece uma nova abordagem para a criação de comandos, a composição de soluções e a criação de ferramentas de gerenciamento baseadas em interface gráfica do usuário.</span><span class="sxs-lookup"><span data-stu-id="d628b-104">Windows PowerShell provides a new approach to building commands, composing solutions, and creating graphical user interface-based management tools.</span></span>

<span data-ttu-id="d628b-105">O Windows PowerShell permite que um administrador de sistema Automatize a administração de recursos do sistema pela execução de comandos diretamente ou por meio de scripts.</span><span class="sxs-lookup"><span data-stu-id="d628b-105">Windows PowerShell enables a system administrator to automate the administration of system resources by the execution of commands either directly or through scripts.</span></span>

## <a name="developer-audience"></a><span data-ttu-id="d628b-106">Público do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="d628b-106">Developer Audience</span></span>

<span data-ttu-id="d628b-107">O SDK (Software Development Kit) do Windows PowerShell foi escrito para desenvolvedores de comando que exigem informações de referência sobre as APIs fornecidas pelo Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d628b-107">The Windows PowerShell Software Development Kit (SDK) is written for command developers who require reference information about the APIs provided by Windows PowerShell.</span></span> <span data-ttu-id="d628b-108">Os desenvolvedores de comando usam o Windows PowerShell para criar comandos e provedores que estendem as tarefas que podem ser executadas pelo Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d628b-108">Command developers use Windows PowerShell to create both commands and providers that extend the tasks that can be performed by Windows PowerShell.</span></span>

## <a name="windows-powershell-resources"></a><span data-ttu-id="d628b-109">Recursos do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d628b-109">Windows PowerShell Resources</span></span>

<span data-ttu-id="d628b-110">Além do SDK do Windows PowerShell, os recursos a seguir fornecem mais informações.</span><span class="sxs-lookup"><span data-stu-id="d628b-110">In addition to the Windows PowerShell SDK, the following resources provide more information.</span></span>

<span data-ttu-id="d628b-111">[Introdução com o Windows PowerShell](/powershell/scripting/getting-started/getting-started-with-windows-powershell) Fornece uma introdução ao Windows PowerShell: a linguagem, os cmdlets, os provedores e o uso de objetos.</span><span class="sxs-lookup"><span data-stu-id="d628b-111">[Getting Started with Windows PowerShell](/powershell/scripting/getting-started/getting-started-with-windows-powershell) Provides an introduction to Windows PowerShell: the language, the cmdlets, the providers, and the use of objects.</span></span>

<span data-ttu-id="d628b-112">[Escrevendo um módulo do Windows PowerShell](./module/writing-a-windows-powershell-module.md) Fornece informações e exemplos para administradores, desenvolvedores de scripts e desenvolvedores de cmdlets que precisam empacotar e distribuir suas soluções do Windows PowerShell usando módulos do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d628b-112">[Writing a Windows PowerShell Module](./module/writing-a-windows-powershell-module.md) Provides information and examples for administrators, script developers, and cmdlet developers who need to package and distribute their Windows PowerShell solutions using Windows PowerShell modules.</span></span>

<span data-ttu-id="d628b-113">[Escrevendo um cmdlet do Windows PowerShell](./cmdlet/writing-a-windows-powershell-cmdlet.md) Fornece informações e exemplos de código para gerentes de programa que estão criando cmdlets e para desenvolvedores que estão implementando código de cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d628b-113">[Writing a Windows PowerShell Cmdlet](./cmdlet/writing-a-windows-powershell-cmdlet.md) Provides information and code examples for program managers who are designing cmdlets and for developers who are implementing cmdlet code.</span></span>

<span data-ttu-id="d628b-114">[Blog da equipe do Windows PowerShell](https://blogs.msdn.microsoft.com/PowerShell/) O melhor recurso para aprender e colaborar com outros usuários do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d628b-114">[Windows PowerShell Team Blog](https://blogs.msdn.microsoft.com/PowerShell/) The best resource for learning from and collaborating with other Windows PowerShell users.</span></span> <span data-ttu-id="d628b-115">Leia o blog da equipe do Windows PowerShell e ingresse no fórum de usuário do Windows PowerShell (Microsoft. Public. Windows. PowerShell).</span><span class="sxs-lookup"><span data-stu-id="d628b-115">Read the Windows PowerShell Team blog, and then join the Windows PowerShell User Forum (microsoft.public.windows.powershell).</span></span> <span data-ttu-id="d628b-116">Use o Windows Live Search para encontrar outros Blogs e recursos do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d628b-116">Use Windows Live Search to find other Windows PowerShell blogs and resources.</span></span> <span data-ttu-id="d628b-117">Em seguida, ao desenvolver sua experiência, colabore livremente suas ideias.</span><span class="sxs-lookup"><span data-stu-id="d628b-117">Then, as you develop your expertise, freely contribute your ideas.</span></span>

<span data-ttu-id="d628b-118">[Navegador de módulo do PowerShell](/powershell/module/) Fornece as versões mais recentes dos tópicos de ajuda da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="d628b-118">[PowerShell module browser](/powershell/module/) Provides the latest versions of the command-line Help topics.</span></span>

## <a name="class-libraries"></a><span data-ttu-id="d628b-119">Bibliotecas de classes</span><span class="sxs-lookup"><span data-stu-id="d628b-119">Class Libraries</span></span>

<span data-ttu-id="d628b-120">[System. Management. Automation](/dotnet/api/System.Management.Automation) esse namespace é o namespace raiz do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d628b-120">[System.Management.Automation](/dotnet/api/System.Management.Automation) This namespace is the root namespace for Windows PowerShell.</span></span> <span data-ttu-id="d628b-121">Ele contém as classes, as enumerações e as interfaces necessárias para implementar cmdlets personalizados.</span><span class="sxs-lookup"><span data-stu-id="d628b-121">It contains the classes, enumerations, and interfaces required to implement custom cmdlets.</span></span> <span data-ttu-id="d628b-122">Em particular, a classe [System. Management. Automation. cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) é a classe base da qual todas as classes de cmdlet devem ser derivadas.</span><span class="sxs-lookup"><span data-stu-id="d628b-122">In particular, the [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) class is the base class from which all cmdlet classes must be derived.</span></span> <span data-ttu-id="d628b-123">Para obter mais informações sobre cmdlets, consulte.</span><span class="sxs-lookup"><span data-stu-id="d628b-123">For more information about cmdlets, see.</span></span>

<span data-ttu-id="d628b-124">[System. Management. Automation. Provider](/dotnet/api/System.Management.Automation.Provider) este namespace contém as classes, as enumerações e as interfaces necessárias para implementar um provedor do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d628b-124">[System.Management.Automation.Provider](/dotnet/api/System.Management.Automation.Provider) This namespace contains the classes, enumerations, and interfaces required to implement a Windows PowerShell provider.</span></span> <span data-ttu-id="d628b-125">Em particular, a classe [System. Management. Automation. Provider. cmdletprovider](/dotnet/api/System.Management.Automation.Provider.CmdletProvider) é a classe base da qual todas as classes de provedor do Windows PowerShell devem ser derivadas.</span><span class="sxs-lookup"><span data-stu-id="d628b-125">In particular, the [System.Management.Automation.Provider.Cmdletprovider](/dotnet/api/System.Management.Automation.Provider.CmdletProvider) class is the base class from which all Windows PowerShell provider classes must be derived.</span></span>

<span data-ttu-id="d628b-126">[Microsoft. PowerShell. Commands](/dotnet/api/Microsoft.PowerShell.Commands) este namespace contém as classes para os cmdlets e provedores implementados pelo Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d628b-126">[Microsoft.PowerShell.Commands](/dotnet/api/Microsoft.PowerShell.Commands) This namespace contains the classes for the cmdlets and providers implemented by Windows PowerShell.</span></span> <span data-ttu-id="d628b-127">Da mesma forma, é recomendável que você crie um *seu*. Namespace de comandos para os cmdlets que você implementa.</span><span class="sxs-lookup"><span data-stu-id="d628b-127">Similarly, it is recommended that you create a *YourName*.Commands namespace for those cmdlets that you implement.</span></span>

<span data-ttu-id="d628b-128">[System. Management. Automation. host](/dotnet/api/System.Management.Automation.Host) esse namespace contém as classes, enumerações e interfaces que o cmdlet usa para definir a interação entre o usuário e o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d628b-128">[System.Management.Automation.Host](/dotnet/api/System.Management.Automation.Host) This namespace contains the classes, enumerations, and interfaces that the cmdlet uses to define the interaction between the user and Windows PowerShell.</span></span>

<span data-ttu-id="d628b-129">[System. Management. Automation. Internal](/dotnet/api/System.Management.Automation.Internal) este namespace contém as classes base usadas por outras classes de namespace.</span><span class="sxs-lookup"><span data-stu-id="d628b-129">[System.Management.Automation.Internal](/dotnet/api/System.Management.Automation.Internal) This namespace contains the base classes used by other namespace classes.</span></span> <span data-ttu-id="d628b-130">Por exemplo, a classe [System. Management. Automation. Internal. Cmdletmetadataattribute](/dotnet/api/System.Management.Automation.Internal.CmdletMetadataAttribute) é a classe base para a classe [System. Management. Automation. CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute) .</span><span class="sxs-lookup"><span data-stu-id="d628b-130">For example, the [System.Management.Automation.Internal.Cmdletmetadataattribute](/dotnet/api/System.Management.Automation.Internal.CmdletMetadataAttribute) class is the base class for the [System.Management.Automation.CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute) class.</span></span>

<span data-ttu-id="d628b-131">[System. Management. Automation. Runspaces](/dotnet/api/System.Management.Automation.Runspaces) este namespace contém as classes, enumerações e interfaces usadas para criar um runspace do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d628b-131">[System.Management.Automation.Runspaces](/dotnet/api/System.Management.Automation.Runspaces) This namespace contains the classes, enumerations, and interfaces used to create a Windows PowerShell runspace.</span></span> <span data-ttu-id="d628b-132">Nesse contexto, o runspace do Windows PowerShell é o contexto no qual um ou mais pipelines do Windows PowerShell invocam cmdlets.</span><span class="sxs-lookup"><span data-stu-id="d628b-132">In this context, the Windows PowerShell runspace is the context in which one or more Windows PowerShell pipelines invoke cmdlets.</span></span> <span data-ttu-id="d628b-133">Ou seja, os cmdlets funcionam dentro do contexto de um runspace do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d628b-133">That is, cmdlets work within the context of a Windows PowerShell runspace.</span></span> <span data-ttu-id="d628b-134">Para obter mais informações aboutWindows de espaços de Tróia do PowerShell, consulte espaços de informações do [Windows PowerShell](https://msdn.microsoft.com/en-us/a1582cfe-f06d-4aff-adc6-71f49a860ce9).</span><span class="sxs-lookup"><span data-stu-id="d628b-134">For more information aboutWindows PowerShell runspaces, see [Windows PowerShell Runspaces](https://msdn.microsoft.com/en-us/a1582cfe-f06d-4aff-adc6-71f49a860ce9).</span></span>