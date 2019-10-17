---
title: Visão geral da ajuda atualizável | Microsoft Docs
ms.custom: ''
ms.date: 03/22/2012
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Windows PowerShell 3.0
ms.assetid: 3f7388a9-9fa8-42bc-b294-538c9a01e30a
caps.latest.revision: 12
ms.openlocfilehash: f2dfb9642ba2dde38124142b659b425bbbb00f37
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72366955"
---
# <a name="updatable-help-overview"></a><span data-ttu-id="ed8a3-102">Visão geral da ajuda atualizável</span><span class="sxs-lookup"><span data-stu-id="ed8a3-102">Updatable Help Overview</span></span>

<span data-ttu-id="ed8a3-103">Este documento fornece uma introdução básica ao design e operação do recurso de ajuda atualizável do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-103">This document provides a basic introduction to the design and operation of the Windows PowerShell Updatable Help feature.</span></span> <span data-ttu-id="ed8a3-104">Ele foi projetado para autores de módulo e outros que fornecem tópicos de ajuda do Windows PowerShell para os usuários.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-104">It is designed for module authors and others who deliver Windows PowerShell help topics to users.</span></span>

## <a name="introduction"></a><span data-ttu-id="ed8a3-105">Introdução</span><span class="sxs-lookup"><span data-stu-id="ed8a3-105">Introduction</span></span>

<span data-ttu-id="ed8a3-106">Os tópicos de ajuda do Windows PowerShell são parte integrante da experiência do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-106">Windows PowerShell help topics are an integral part of the Windows PowerShell experience.</span></span> <span data-ttu-id="ed8a3-107">Assim como os módulos do Windows PowerShell, os tópicos da ajuda são continuamente atualizados e aprimorados pelos autores e pelas contribuições da comunidade de usuários do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-107">Like Windows PowerShell modules, help topics are continually updated and improved by the authors and by the contributions of the community of Windows PowerShell users.</span></span>

<span data-ttu-id="ed8a3-108">O recurso de *ajuda atualizável* , introduzido no Windows PowerShell 3,0, garante que os usuários tenham as versões mais recentes dos tópicos da ajuda no prompt de comando, mesmo para comandos internos do Windows PowerShell, sem baixar novos módulos ou executar Windows Update .</span><span class="sxs-lookup"><span data-stu-id="ed8a3-108">The *Updatable Help* feature, introduced in Windows PowerShell 3.0, ensures that users have the newest versions of help topics at the command prompt, even for built-in Windows PowerShell commands, without downloading new modules or running Windows Update.</span></span> <span data-ttu-id="ed8a3-109">A ajuda atualizável torna a atualização simples, fornecendo cmdlets que baixam as versões mais recentes dos tópicos de ajuda da Internet e as instalam nos subdiretórios corretos no computador local do usuário.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-109">Updatable Help makes updating simple by providing cmdlets that download the newest versions of help topics from the Internet and install them in the correct subdirectories on the user's local computer.</span></span> <span data-ttu-id="ed8a3-110">Até mesmo os usuários que estão atrás de firewalls podem usar os novos cmdlets para obter ajuda atualizada de um compartilhamento de arquivos interno.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-110">Even users who are behind firewalls can use the new cmdlets to get updated help from an internal file share.</span></span>

<span data-ttu-id="ed8a3-111">A ajuda atualizável tem suporte total de todos os módulos do Windows PowerShell no Windows® 8 e do Windows Server® 2012, e seus recursos estão disponíveis para todos os autores de módulo do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-111">Updatable Help is fully supported by all Windows PowerShell modules in Windows® 8 and Windows Server® 2012, and its features are available to all Windows PowerShell module authors.</span></span> <span data-ttu-id="ed8a3-112">A ajuda atualizável dá suporte apenas a arquivos de ajuda baseados em XML.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-112">Updatable Help supports only XML-based help files.</span></span> <span data-ttu-id="ed8a3-113">Ele não oferece suporte à ajuda baseada em comentários.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-113">It does not support comment-based help.</span></span>

<span data-ttu-id="ed8a3-114">A ajuda atualizável inclui os seguintes recursos.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-114">Updatable Help includes the following features.</span></span>

- <span data-ttu-id="ed8a3-115">O cmdlet [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) , que determina se os usuários têm os arquivos de ajuda mais recentes para um módulo e, caso contrário, baixa os arquivos de ajuda mais recentes da Internet, os descompactam e os instala nos subdiretórios de módulo corretos no computador do usuário.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-115">The [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) cmdlet, which determines whether users have the newest help files for a module and, if not, downloads the newest help files from the Internet, unpacks them, and installs them in the correct module subdirectories on the user's computer.</span></span>
  <span data-ttu-id="ed8a3-116">Os usuários podem usar o cmdlet [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) para exibir imediatamente os tópicos da ajuda recém-instalados.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-116">Users can use the [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) cmdlet to view the newly-installed help topics immediately.</span></span>
  <span data-ttu-id="ed8a3-117">Eles não precisam reiniciar o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-117">They do not need to restart PowerShell.</span></span>

- <span data-ttu-id="ed8a3-118">O cmdlet [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) , que baixa os arquivos de ajuda mais recentes da Internet e os salva em um diretório do sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-118">The [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) cmdlet, which downloads the newest help files from the Internet and saves them in a file system directory.</span></span> <span data-ttu-id="ed8a3-119">Os usuários podem usar o cmdlet `Update-Help` para obter arquivos de ajuda do diretório do sistema de arquivos e descompactá-los e instalá-los nos subdiretórios do módulo no computador do usuário.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-119">Users can use the `Update-Help` cmdlet to get help files from the file system directory, and unpack and install them in the module subdirectories on the user's computer.</span></span> <span data-ttu-id="ed8a3-120">O cmdlet `Save-Help` foi projetado para usuários que têm acesso limitado ou sem Internet e para empresas que preferem limitar o acesso à Internet.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-120">The `Save-Help` cmdlet is designed for users who have limited or no Internet access and for enterprises who prefer to limit Internet access.</span></span>

- <span data-ttu-id="ed8a3-121">**Ajuda para um módulo**.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-121">**Help for a Module**.</span></span> <span data-ttu-id="ed8a3-122">Os arquivos de ajuda para um módulo são gerenciados e entregues como uma unidade, para que os usuários possam obter todos os arquivos de ajuda para os módulos que usam.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-122">Help files for a module are managed and delivered as a unit, so users can get all of the help files for the modules they use.</span></span> <span data-ttu-id="ed8a3-123">A ajuda atualizável tem suporte apenas para módulos, não para snap-ins do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-123">Updatable help is supported only for modules, not for Windows PowerShell snap-ins.</span></span>

- <span data-ttu-id="ed8a3-124">**Suporte à versão**.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-124">**Version support**.</span></span> <span data-ttu-id="ed8a3-125">A ajuda atualizável usa quatro posições padrão (N1. N2. N3. N4) números de versão.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-125">Updatable Help uses standard four-position (N1.N2.N3.N4) version numbers.</span></span> <span data-ttu-id="ed8a3-126">A ajuda atualizável baixa arquivos de ajuda quando o número de versão dos arquivos de ajuda no computador do usuário (ou no diretório `Save-Help`) é menor do que o número de versão dos arquivos de ajuda no local da Internet.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-126">Updatable Help downloads help files when the version number of the help files on the user's computer (or in the `Save-Help` directory) is lower than the version number of the  help files at the Internet location.</span></span>

- <span data-ttu-id="ed8a3-127">**Suporte a vários idiomas**.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-127">**Multi-language support**.</span></span> <span data-ttu-id="ed8a3-128">A ajuda atualizável oferece suporte a arquivos de ajuda de módulo em várias culturas de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-128">Updatable Help supports module help files in multiple UI cultures.</span></span> <span data-ttu-id="ed8a3-129">Nomes de arquivo de ajuda atualizáveis incluem códigos de idioma padrão, como "en-US" e "ja-JP", e os cmdlets `Update-Help` e `Save-Help` colocam os arquivos de ajuda em subdiretórios específicos à linguagem do diretório do módulo.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-129">Updatable Help file names include standard language codes, such as "en-US" and "ja-JP", and the `Update-Help` and `Save-Help` cmdlets place the help files into language-specific subdirectories of the module directory.</span></span>

- <span data-ttu-id="ed8a3-130">**Ajuda gerada automaticamente**.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-130">**Auto-generated help**.</span></span> <span data-ttu-id="ed8a3-131">O cmdlet [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) exibe a ajuda básica para comandos que não têm arquivos de ajuda.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-131">The [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) cmdlet displays basic help for commands that do not have help files.</span></span> <span data-ttu-id="ed8a3-132">A ajuda gerada automaticamente inclui a sintaxe e os aliases de comando e instruções para usar a ajuda online e a ajuda atualizável.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-132">The auto-generated help includes the command syntax and aliases, and instructions for using online help and Updatable Help.</span></span>

- <span data-ttu-id="ed8a3-133">**Ajuda online aprimorada**.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-133">**Enhanced Online help**.</span></span> <span data-ttu-id="ed8a3-134">O acesso fácil à ajuda online não requer mais arquivos de ajuda.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-134">Easy access to online help no longer requires help files.</span></span> <span data-ttu-id="ed8a3-135">O parâmetro **online** do cmdlet `Get-Help` agora Obtém a URL de um tópico da ajuda online do valor da propriedade **HelpUri** de qualquer comando, se não for possível encontrar a URL da ajuda online em um arquivo de ajuda.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-135">The **Online** parameter of the `Get-Help` cmdlet now gets the URL of an online help topic from the value of the **HelpUri** property of any command, if it cannot find the online help URL in a help file.</span></span> <span data-ttu-id="ed8a3-136">Você pode preencher a propriedade **HelpUri** adicionando um atributo **HelpUri** ao código de cmdlets, funções e comandos CIM, ou usando o **. Vincular** diretiva de ajuda baseada em comentário em fluxos de trabalho e scripts.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-136">You can populate the **HelpUri** property by adding a **HelpUri** attribute to the code of cmdlets, functions, and CIM commands, or by using the **.Link** comment-based help directive in workflows and scripts.</span></span>

  <span data-ttu-id="ed8a3-137">Para tornar os arquivos de ajuda atualizáveis, os módulos do Windows PowerShell no Windows 8 e no Windows Server vNext não vêm com os arquivos de ajuda.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-137">To make our help files updatable, the Windows PowerShell modules in Windows 8 and Windows Server vNext do not come with help files.</span></span> <span data-ttu-id="ed8a3-138">Os usuários podem usar a ajuda atualizável para instalar os arquivos de ajuda e atualizá-los.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-138">Users can use Updatable Help to install help files and update them.</span></span> <span data-ttu-id="ed8a3-139">Os autores de outros módulos podem incluir arquivos de ajuda em módulos ou omiti-los.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-139">Authors of other modules can include help files in modules or omit them.</span></span> <span data-ttu-id="ed8a3-140">O suporte para a ajuda atualizável é opcional, mas recomendado.</span><span class="sxs-lookup"><span data-stu-id="ed8a3-140">Support for Updatable Help is optional, but recommended.</span></span>