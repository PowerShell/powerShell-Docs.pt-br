---
ms.date: 09/06/2019
keywords: powershell, cmdlet
title: Novidades no ISE do PowerShell 5.0
ms.openlocfilehash: 1f5d32d583165ff8ead0a95b1c882386cf654326
ms.sourcegitcommit: 2aec310ad0c0b048400cb56f6fa64c1e554c812a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2020
ms.locfileid: "83809132"
---
# <a name="whats-new-in-the-windows-powershell-50-ise"></a><span data-ttu-id="a6c95-103">Novidades no ISE do Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="a6c95-103">What's New in the Windows PowerShell 5.0 ISE</span></span>

<span data-ttu-id="a6c95-104">Este tópico explica os recursos novos e atualizados introduzidos na versão 5.0 do ISE (Ambiente de Script Integrado) do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a6c95-104">This topic explains the new and updated features that have been introduced in version 5.0 of the Windows PowerShell Integrated Scripting Environment (ISE).</span></span>

> [!NOTE]
> <span data-ttu-id="a6c95-105">O ISE do PowerShell não está mais no desenvolvimento ativo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a6c95-105">The PowerShell ISE is no longer in active feature development.</span></span> <span data-ttu-id="a6c95-106">Como componente de remessa do Windows, ele continua com suporte oficial para correções de segurança e serviços de alta prioridade.</span><span class="sxs-lookup"><span data-stu-id="a6c95-106">As a shipping component of Windows, it continues to be officially supported for security and high-priority servicing fixes.</span></span>
> <span data-ttu-id="a6c95-107">No momento, não há planos de remover o ISE do Windows.</span><span class="sxs-lookup"><span data-stu-id="a6c95-107">We currently have no plans to remove the ISE from Windows.</span></span>
>
> <span data-ttu-id="a6c95-108">Não há suporte para o ISE no PowerShell v6 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="a6c95-108">There is no support for the ISE in PowerShell v6 and beyond.</span></span> <span data-ttu-id="a6c95-109">Os usuários que buscam substituir o ISE devem usar o [Visual Studio Code](https://code.visualstudio.com/) com o [PowerShell Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell).</span><span class="sxs-lookup"><span data-stu-id="a6c95-109">Users looking for replacement for the ISE should use [Visual Studio Code](https://code.visualstudio.com/) with the [PowerShell Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell).</span></span>

## <a name="feature-description"></a><span data-ttu-id="a6c95-110">Descrição do recurso</span><span class="sxs-lookup"><span data-stu-id="a6c95-110">Feature description</span></span>

<span data-ttu-id="a6c95-111">O ISE do Windows PowerShell é um aplicativo host que permite gravar, executar e testar scripts e módulos em um ambiente gráfico e intuitivo.</span><span class="sxs-lookup"><span data-stu-id="a6c95-111">The Windows PowerShell ISE is a host application that enables you to write, run, and test scripts and modules in a graphical and intuitive environment.</span></span> <span data-ttu-id="a6c95-112">Recursos importantes como coloração de sintaxe, preenchimento de guias, depuração visual, conformidade com Unicode e Ajuda contextual permitem uma experiência avançada de script.</span><span class="sxs-lookup"><span data-stu-id="a6c95-112">Key features such as syntax-coloring, tab completion, visual debugging, Unicode compliance, and context-sensitive Help provide a rich scripting experience.</span></span>

<span data-ttu-id="a6c95-113">Para obter mais informações, confira [Apresentamos o ISE do Windows PowerShell](../ise/Introducing-the-Windows-PowerShell-ISE.md).</span><span class="sxs-lookup"><span data-stu-id="a6c95-113">For more information, see [Introducing the Windows PowerShell ISE](../ise/Introducing-the-Windows-PowerShell-ISE.md).</span></span>

<span data-ttu-id="a6c95-114">A tabela a seguir lista os recursos novos e alterados para esta versão do ISE do Windows PowerShell no Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a6c95-114">The following table lists the new and changed features for this release of Windows PowerShell ISE in Windows PowerShell.</span></span>

## <a name="intellisense"></a><span data-ttu-id="a6c95-115">IntelliSense</span><span class="sxs-lookup"><span data-stu-id="a6c95-115">IntelliSense</span></span>

> <span data-ttu-id="a6c95-116">Adicionado no ISE 3.0</span><span class="sxs-lookup"><span data-stu-id="a6c95-116">Added in ISE 3.0</span></span>

<span data-ttu-id="a6c95-117">O IntelliSense é um recurso de assistência de preenchimento automático que faz parte do ISE do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a6c95-117">IntelliSense is an automatic-completion assistance feature that is part of Windows PowerShell ISE.</span></span>
<span data-ttu-id="a6c95-118">O IntelliSense exibe menus clicáveis dos cmdlets, parâmetros, valores de parâmetro, arquivos ou pastas potencialmente correspondentes conforme você digita.</span><span class="sxs-lookup"><span data-stu-id="a6c95-118">IntelliSense displays clickable menus of potentially matching cmdlets, parameters, parameter values, files, or folders as you type.</span></span>

<span data-ttu-id="a6c95-119">**Qual é o valor adicionado por esta alteração?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-119">**What value does this change add?**</span></span>

<span data-ttu-id="a6c95-120">Com a adição do IntelliSense, é mais fácil descobrir cmdlets e sintaxes ao usar o ISE do Windows PowerShell para criar scripts.</span><span class="sxs-lookup"><span data-stu-id="a6c95-120">With the addition of IntelliSense, it's easier to discover cmdlets and syntax when you use Windows PowerShell ISE to create scripts.</span></span> <span data-ttu-id="a6c95-121">Você também pode usar o ISE do Windows PowerShell para conhecer o Windows PowerShell enquanto cria novos scripts.</span><span class="sxs-lookup"><span data-stu-id="a6c95-121">You can also use Windows PowerShell ISE to learn Windows PowerShell while you create new scripts.</span></span>

<span data-ttu-id="a6c95-122">**O que passou a funcionar de maneira diferente?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-122">**What works differently?**</span></span>

<span data-ttu-id="a6c95-123">Quando você digita cmdlets no ISE do Windows PowerShell, é exibido um menu de rolagem clicável que permite navegar e selecionar os comandos apropriados.</span><span class="sxs-lookup"><span data-stu-id="a6c95-123">When you type cmdlets in the Windows PowerShell ISE, a scrollable and clickable menu displays, allowing you to browse and select the appropriate commands.</span></span>

## <a name="snippets"></a><span data-ttu-id="a6c95-124">Snippets</span><span class="sxs-lookup"><span data-stu-id="a6c95-124">Snippets</span></span>

> <span data-ttu-id="a6c95-125">Adicionado no ISE 3.0</span><span class="sxs-lookup"><span data-stu-id="a6c95-125">Added in ISE 3.0</span></span>

<span data-ttu-id="a6c95-126">*Snippets de código* são sessões de código Windows PowerShell curtas que você pode inserir nos scritps que cria no ISE do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a6c95-126">*Snippets* are short sections of Windows PowerShell code that you can insert into the scripts you create in Windows PowerShell ISE.</span></span> <span data-ttu-id="a6c95-127">O ISE do Windows PowerShell vem com um conjunto padrão de snippets.</span><span class="sxs-lookup"><span data-stu-id="a6c95-127">Windows PowerShell ISE comes with a default set of snippets.</span></span> <span data-ttu-id="a6c95-128">Você pode adicionar snippets usando o cmdlet `New-Snippet` enquanto trabalha no ISE do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a6c95-128">You can add snippets by using the `New-Snippet` cmdlet while working in Windows PowerShell ISE.</span></span>

<span data-ttu-id="a6c95-129">**Qual é o valor adicionado por esta alteração?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-129">**What value does this change add?**</span></span>

<span data-ttu-id="a6c95-130">Usando snippets, você pode montar e criar scripts para automatizar seu ambiente rapidamente.</span><span class="sxs-lookup"><span data-stu-id="a6c95-130">By using snippets, you can quickly assemble and create scripts to automate your environment.</span></span>

<span data-ttu-id="a6c95-131">**O que passou a funcionar de maneira diferente?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-131">**What works differently?**</span></span>

<span data-ttu-id="a6c95-132">Para usar snippets no Windows PowerShell 3.0 ou posterior, no menu **Editar**, clique em **Iniciar Snippets** ou pressione <kbd>Ctrl</kbd>+<kbd>J</kbd>.</span><span class="sxs-lookup"><span data-stu-id="a6c95-132">To use snippets in Windows PowerShell 3.0 or later, on the **Edit** menu, click **Start Snippets**, or press <kbd>Ctrl</kbd>+<kbd>J</kbd>.</span></span>

## <a name="add-on-tools"></a><span data-ttu-id="a6c95-133">Ferramentas complementares</span><span class="sxs-lookup"><span data-stu-id="a6c95-133">Add-on tools</span></span>

> <span data-ttu-id="a6c95-134">Adicionado no PowerShell 3.0</span><span class="sxs-lookup"><span data-stu-id="a6c95-134">Added in PowerShell 3.0</span></span>

<span data-ttu-id="a6c95-135">Agora o ISE do Windows PowerShell dá suporte a ferramentas complementares usando o modelo de objeto.</span><span class="sxs-lookup"><span data-stu-id="a6c95-135">Windows PowerShell ISE now supports add-on tools using the object model.</span></span> <span data-ttu-id="a6c95-136">Esses complementos são controles do WPF (Windows Presentation Foundation), exibidos como um painel vertical ou horizontal no console.</span><span class="sxs-lookup"><span data-stu-id="a6c95-136">These add-ons are Windows Presentation Foundation (WPF) controls that are displayed as a vertical or horizontal pane in the console.</span></span> <span data-ttu-id="a6c95-137">Várias ferramentas complementares em um painel são exibidas como um controle com guias.</span><span class="sxs-lookup"><span data-stu-id="a6c95-137">Multiple add-on tools in a pane are displayed as a tabbed control.</span></span> <span data-ttu-id="a6c95-138">Você também pode adicionar ou remover ferramentas complementares produzidas por terceiros.</span><span class="sxs-lookup"><span data-stu-id="a6c95-138">You can also add or remove add-on tools that are produced by non-Microsoft parties.</span></span> <span data-ttu-id="a6c95-139">Para obter mais informações, confira [Objetivo do modelo de objeto de script do ISE do Windows PowerShell](../ise/object-model/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md).</span><span class="sxs-lookup"><span data-stu-id="a6c95-139">For more information, see [The Purpose of the Windows PowerShell ISE Scripting Object Model](../ise/object-model/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md).</span></span>

<span data-ttu-id="a6c95-140">**Qual é o valor adicionado por esta alteração?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-140">**What value does this change add?**</span></span>

<span data-ttu-id="a6c95-141">Os complementos permitem estender e personalizar o ISE do Windows PowerShell com ferramentas que adicionam funcionalidades e podem melhorar sua experiência com scripts.</span><span class="sxs-lookup"><span data-stu-id="a6c95-141">Add-ons allow you to extend and customize Windows PowerShell ISE with tools that add functionality and enhance your scripting experience.</span></span>

<span data-ttu-id="a6c95-142">**O que passou a funcionar de maneira diferente?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-142">**What works differently?**</span></span>

<span data-ttu-id="a6c95-143">O ISE do Windows PowerShell 3.0 e posterior vêm com o complemento **Comandos**.</span><span class="sxs-lookup"><span data-stu-id="a6c95-143">Windows PowerShell ISE 3.0 and later come with the **Commands** add-on.</span></span> <span data-ttu-id="a6c95-144">O complemento **Comandos** permite que você procure cmdlets e acesse a Ajuda para os cmdlets lado a lado com os Painéis de **Script** e **Console**.</span><span class="sxs-lookup"><span data-stu-id="a6c95-144">The **Commands** add-on allows you to browse cmdlets, and access help about the cmdlets side-by-side with the **Script** and **Console** Panes.</span></span>

<span data-ttu-id="a6c95-145">Complementos adicionais podem ser encontrados usando o comando **Abrir o Site de Ferramentas Complementares** no menu **Complementos**.</span><span class="sxs-lookup"><span data-stu-id="a6c95-145">Additional add-ons can be found by using the **Open Add-on Tools Website** command on the **Add-ons** menu.</span></span>

## <a name="restart-manager-and-auto-save"></a><span data-ttu-id="a6c95-146">Gerenciador de Reinicialização e Salvamento Automático</span><span class="sxs-lookup"><span data-stu-id="a6c95-146">Restart manager and auto-save</span></span>

> <span data-ttu-id="a6c95-147">Adicionado no PowerShell 3.0</span><span class="sxs-lookup"><span data-stu-id="a6c95-147">Added in PowerShell 3.0</span></span>

<span data-ttu-id="a6c95-148">O ISE do Windows PowerShell agora salva automaticamente os scripts abertos a cada dois minutos em uma localização separada.</span><span class="sxs-lookup"><span data-stu-id="a6c95-148">Windows PowerShell ISE now automatically saves your open scripts every two minutes, in a separate location.</span></span> <span data-ttu-id="a6c95-149">Quando o ISE do Windows PowerShell é reiniciado após uma falha inesperada ou uma reinicialização, ele recupera os scripts que estavam abertos na última sessão, mesmo que os scripts não tenham sido salvos.</span><span class="sxs-lookup"><span data-stu-id="a6c95-149">When Windows PowerShell ISE restarts after an unexpected crash or reboot, it recovers scripts that were open in the last session, even if the scripts weren't saved.</span></span>

<span data-ttu-id="a6c95-150">Para alterar o intervalo de salvamento automático, execute o seguinte comando no painel de console: `$psise.Options.AutoSaveMinuteInterval`.</span><span class="sxs-lookup"><span data-stu-id="a6c95-150">To change the automatic saving interval, run the following command in the Console pane: `$psise.Options.AutoSaveMinuteInterval`.</span></span>

<span data-ttu-id="a6c95-151">**Qual é o valor adicionado por esta alteração?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-151">**What value does this change add?**</span></span>

<span data-ttu-id="a6c95-152">Agora você pode trabalhar no ISE do Windows PowerShell sabendo que os scripts abertos são salvos automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a6c95-152">You can now work within Windows PowerShell ISE knowing that your open scripts are automatically saved.</span></span>

<span data-ttu-id="a6c95-153">**O que passou a funcionar de maneira diferente?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-153">**What works differently?**</span></span>

<span data-ttu-id="a6c95-154">O ISE do Windows PowerShell 2.0 não salva automaticamente os scripts.</span><span class="sxs-lookup"><span data-stu-id="a6c95-154">Windows PowerShell ISE 2.0 doesn't save the scripts automatically.</span></span>

## <a name="most-recently-used-list"></a><span data-ttu-id="a6c95-155">Lista de recém-usados</span><span class="sxs-lookup"><span data-stu-id="a6c95-155">Most-recently used list</span></span>

> <span data-ttu-id="a6c95-156">Adicionado no PowerShell 3.0</span><span class="sxs-lookup"><span data-stu-id="a6c95-156">Added in PowerShell 3.0</span></span>

<span data-ttu-id="a6c95-157">O ISE do Windows PowerShell agora tem uma lista de arquivos recém-usados.</span><span class="sxs-lookup"><span data-stu-id="a6c95-157">Windows PowerShell ISE now has a most-recently used list for files.</span></span> <span data-ttu-id="a6c95-158">Quando você abre um arquivo no ISE do Windows PowerShell, ele é adicionado à lista de recém-usados no menu **Arquivo**.</span><span class="sxs-lookup"><span data-stu-id="a6c95-158">When you open a file in Windows PowerShell ISE, the file is added to the most-recently used list on the **File** menu.</span></span>

<span data-ttu-id="a6c95-159">Para alterar o número padrão de arquivos na lista de recém-usados, execute o seguinte comando no Painel de Console: `$psise.Options.MruCount`.</span><span class="sxs-lookup"><span data-stu-id="a6c95-159">To change the default number of files in the most-recently used list, run the following command in the Console Pane: `$psise.Options.MruCount`.</span></span>

<span data-ttu-id="a6c95-160">**Qual é o valor adicionado por esta alteração?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-160">**What value does this change add?**</span></span>

<span data-ttu-id="a6c95-161">Agora você pode usar a lista de recém-usados para acessar facilmente os arquivos mais usados.</span><span class="sxs-lookup"><span data-stu-id="a6c95-161">You can now use the most-recently used list to easily access your frequently used files.</span></span>

<span data-ttu-id="a6c95-162">**O que passou a funcionar de maneira diferente?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-162">**What works differently?**</span></span>

<span data-ttu-id="a6c95-163">O ISE do Windows PowerShell 2.0 não tem uma lista arquivos usados recentemente.</span><span class="sxs-lookup"><span data-stu-id="a6c95-163">Windows PowerShell ISE 2.0 doesn't have a most-recently used list.</span></span>

## <a name="console-pane"></a><span data-ttu-id="a6c95-164">Painel de Console</span><span class="sxs-lookup"><span data-stu-id="a6c95-164">Console Pane</span></span>

> <span data-ttu-id="a6c95-165">Adicionado no PowerShell 3.0</span><span class="sxs-lookup"><span data-stu-id="a6c95-165">Added in PowerShell 3.0</span></span>

<span data-ttu-id="a6c95-166">Os Painéis de Comando e Saída separados que estavam disponíveis na primeira versão do ISE do Windows PowerShell foram combinados em um Painel de Console único.</span><span class="sxs-lookup"><span data-stu-id="a6c95-166">The separate Command and Output Panes that were available in the first release of Windows PowerShell ISE have been combined into a single Console Pane.</span></span> <span data-ttu-id="a6c95-167">O Painel do Console é semelhante, em termos de função e aparência, a um console típico do Windows PowerShell, mas inclui os aprimoramentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6c95-167">The Console Pane is similar in function and appearance to a typical Windows PowerShell console, but it includes the following enhancements:</span></span>

- <span data-ttu-id="a6c95-168">Cores de sintaxe para texto de entrada (não para texto de saída), incluindo sintaxe XML</span><span class="sxs-lookup"><span data-stu-id="a6c95-168">Syntax coloring for input text (not output text), including XML syntax</span></span>
- <span data-ttu-id="a6c95-169">IntelliSense</span><span class="sxs-lookup"><span data-stu-id="a6c95-169">IntelliSense</span></span>
- <span data-ttu-id="a6c95-170">Correspondência de chaves</span><span class="sxs-lookup"><span data-stu-id="a6c95-170">Brace matching</span></span>
- <span data-ttu-id="a6c95-171">Indicação de erros</span><span class="sxs-lookup"><span data-stu-id="a6c95-171">Error indication</span></span>
- <span data-ttu-id="a6c95-172">Suporte total a Unicode</span><span class="sxs-lookup"><span data-stu-id="a6c95-172">Full Unicode support</span></span>
- <span data-ttu-id="a6c95-173">Ajuda contextual com <kbd>F1</kbd></span><span class="sxs-lookup"><span data-stu-id="a6c95-173"><kbd>F1</kbd> context-sensitive help</span></span>
- <span data-ttu-id="a6c95-174">Show-Command contextual com <kbd>Ctrl</kbd>+<kbd>F1</kbd></span><span class="sxs-lookup"><span data-stu-id="a6c95-174"><kbd>Ctrl</kbd>+<kbd>F1</kbd> context-sensitive Show-Command</span></span>
- <span data-ttu-id="a6c95-175">Suporte a scripts complexos e leitura da direita para a esquerda</span><span class="sxs-lookup"><span data-stu-id="a6c95-175">Complex script and right-to-left support</span></span>
- <span data-ttu-id="a6c95-176">Suporte a fontes</span><span class="sxs-lookup"><span data-stu-id="a6c95-176">Font support</span></span>
- <span data-ttu-id="a6c95-177">Zoom</span><span class="sxs-lookup"><span data-stu-id="a6c95-177">Zoom</span></span>
- <span data-ttu-id="a6c95-178">Modos de seleção de linha e seleção de blocos</span><span class="sxs-lookup"><span data-stu-id="a6c95-178">Line-select and block-select modes</span></span>
- <span data-ttu-id="a6c95-179">Preservação do conteúdo digitado na linha de comando quando você pressiona a <kbd>Seta para cima</kbd> para exibir o histórico no console</span><span class="sxs-lookup"><span data-stu-id="a6c95-179">Preservation of typed content at the command line when you press the <kbd>UpArrow</kbd> to view history in the console</span></span>

<span data-ttu-id="a6c95-180">**Qual é o valor adicionado por esta alteração?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-180">**What value does this change add?**</span></span>

<span data-ttu-id="a6c95-181">A adição dessas alterações do Painel de Console fornece uma experiência de script que é mais consistente com a interface do console.</span><span class="sxs-lookup"><span data-stu-id="a6c95-181">The addition of these Console Pane changes provides a scripting experience that is more consistent with the console interface.</span></span>

<span data-ttu-id="a6c95-182">**O que passou a funcionar de maneira diferente?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-182">**What works differently?**</span></span>

<span data-ttu-id="a6c95-183">O ISE do Windows PowerShell 2.0 tem Painéis de Comando e de Saída separados.</span><span class="sxs-lookup"><span data-stu-id="a6c95-183">Windows PowerShell ISE 2.0 has separate Command and Output Panes.</span></span>

## <a name="command-line-switches"></a><span data-ttu-id="a6c95-184">Opções de linha de comando</span><span class="sxs-lookup"><span data-stu-id="a6c95-184">Command-line switches</span></span>

> <span data-ttu-id="a6c95-185">Adicionado no PowerShell 3.0</span><span class="sxs-lookup"><span data-stu-id="a6c95-185">Added in PowerShell 3.0</span></span>

<span data-ttu-id="a6c95-186">Se você iniciar o ISE do Windows PowerShell com a linha de comando (digitando **powershell_ise.exe**), será possível adicionar as novas opções de linha de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="a6c95-186">If you start Windows PowerShell ISE from the command line (by typing **powershell_ise.exe**), you can add the following new command-line switches.</span></span>

- <span data-ttu-id="a6c95-187">`-NoProfile`: inicia o ISE do Windows PowerShell sem executar `$profile`</span><span class="sxs-lookup"><span data-stu-id="a6c95-187">`-NoProfile`: Starts Windows PowerShell ISE without running `$profile`</span></span>
- <span data-ttu-id="a6c95-188">`-Help`: exibe uma janela Ajuda</span><span class="sxs-lookup"><span data-stu-id="a6c95-188">`-Help`: Displays a Help window</span></span>
- <span data-ttu-id="a6c95-189">`-mta`: inicia o ISE do Windows PowerShell no modo Multi-Threaded Apartment.</span><span class="sxs-lookup"><span data-stu-id="a6c95-189">`-mta`: Starts Windows PowerShell ISE in multithreaded apartment mode.</span></span> <span data-ttu-id="a6c95-190">O modo de operação padrão do ISE do Windows PowerShell é o modo Single-Threaded Apartment ou `-sta`.</span><span class="sxs-lookup"><span data-stu-id="a6c95-190">The default operation mode for Windows PowerShell ISE is single-threaded apartment mode, or `-sta`.</span></span>

<span data-ttu-id="a6c95-191">**Qual é o valor adicionado por esta alteração?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-191">**What value does this change add?**</span></span>

<span data-ttu-id="a6c95-192">A adição dessas opções de linha de comando permite controlar o ambiente no qual o ISE do Windows PowerShell é executado.</span><span class="sxs-lookup"><span data-stu-id="a6c95-192">The addition of these command-line switches allows you to control the environment in which the Windows PowerShell ISE runs.</span></span>

<span data-ttu-id="a6c95-193">**O que passou a funcionar de maneira diferente?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-193">**What works differently?**</span></span>

<span data-ttu-id="a6c95-194">O ISE do Windows PowerShell 2.0 não reconhece essas opções de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="a6c95-194">Windows PowerShell ISE 2.0 doesn't recognize these command-line switches.</span></span>

## <a name="new-editor-features"></a><span data-ttu-id="a6c95-195">Novos recursos do editor</span><span class="sxs-lookup"><span data-stu-id="a6c95-195">New editor features</span></span>

> <span data-ttu-id="a6c95-196">Adicionado no PowerShell 3.0</span><span class="sxs-lookup"><span data-stu-id="a6c95-196">Added in PowerShell 3.0</span></span>

<span data-ttu-id="a6c95-197">Outros recursos de edição do ISE do Windows PowerShell incluem:</span><span class="sxs-lookup"><span data-stu-id="a6c95-197">Other Windows PowerShell ISE editing features include:</span></span>

- <span data-ttu-id="a6c95-198">**Cores de sintaxe de XML** – Agora o ISE do Windows PowerShell tem sintaxe XML colorida da mesma maneira que a sintaxe colorida do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a6c95-198">**XML syntax coloring** - Windows PowerShell ISE now colors XML syntax in the same way as it colors Windows PowerShell syntax.</span></span>
- <span data-ttu-id="a6c95-199">**Correspondência de chaves** – O ISE do Windows PowerShell inclui o realce e a correspondência de chaves e pode ser usado das seguintes maneiras: (por exemplo, o uso do comando **Ir para Correspondência** ou <kbd>Ctrl</kbd>+<kbd>]</kbd> localizará a chave de fechamento, se você tiver selecionado uma chave de abertura).</span><span class="sxs-lookup"><span data-stu-id="a6c95-199">**Brace matching** - Windows PowerShell ISE includes brace matching and highlighting, and can be used in the following ways: (for example, using the **Go to Match** command or <kbd>Ctrl</kbd>+<kbd>]</kbd> locates the closing brace, if you have an opening brace selected).</span></span>
- <span data-ttu-id="a6c95-200">**Exibição de estrutura de tópicos** O Painel de Script dá suporte à exibição das estruturas de tópicos, que permitem recolher ou expandir seções de códigos com cliques nos sinais de adição ou subtração na margem esquerda.</span><span class="sxs-lookup"><span data-stu-id="a6c95-200">**Outline view** The Script Pane supports outlining, which allows collapsing or expanding sections of code by clicking plus or minus signs in the left margin.</span></span> <span data-ttu-id="a6c95-201">Você pode usar chaves ou as marcas `#region` e `#endregion` para marcar o início ou o final de uma seção recolhível.</span><span class="sxs-lookup"><span data-stu-id="a6c95-201">You can use braces or the `#region` and `#endregion` tags to mark the beginning or end of a collapsible section.</span></span> <span data-ttu-id="a6c95-202">Para expandir ou recolher todas as regiões, pressione <kbd>Ctrl</kbd>+<kbd>M</kbd>.</span><span class="sxs-lookup"><span data-stu-id="a6c95-202">To expand or collapse all regions, press <kbd>Ctrl</kbd>+<kbd>M</kbd>.</span></span>
- <span data-ttu-id="a6c95-203">**Edição de texto com arrastar e soltar** – O ISE do Windows PowerShell agora dá suporte à edição de texto ao arrastar e soltar.</span><span class="sxs-lookup"><span data-stu-id="a6c95-203">**Drag and drop text editing** - Windows PowerShell ISE now supports drag and drop text editing.</span></span> <span data-ttu-id="a6c95-204">Você pode selecionar qualquer bloco de texto e arrastar o texto para outro local no editor ou no console para mover o texto.</span><span class="sxs-lookup"><span data-stu-id="a6c95-204">You can select any block of text and drag that text to another location in the editor or the console to move the text.</span></span> <span data-ttu-id="a6c95-205">Se você mantiver a tecla <kbd>Ctrl</kbd> pressionada enquanto arrasta o texto selecionado, quando soltar o botão do mouse, o texto será copiado para o novo local.</span><span class="sxs-lookup"><span data-stu-id="a6c95-205">If you hold down the <kbd>Ctrl</kbd> key while you drag the selected text, when you release the mouse button the text is copied to the new location.</span></span> <span data-ttu-id="a6c95-206">Nesta versão do ISE do Windows PowerShell, quando você arrasta e solta arquivos no ISE do Windows PowerShell, ele abre o arquivo.</span><span class="sxs-lookup"><span data-stu-id="a6c95-206">In this version of Windows PowerShell ISE, when you drag and drop files onto Windows PowerShell ISE, Windows PowerShell ISE opens the file.</span></span>
- <span data-ttu-id="a6c95-207">**Analisar a exibição de erro** – Erros de análise são indicados com um sublinhado vermelho.</span><span class="sxs-lookup"><span data-stu-id="a6c95-207">**Parse error display** - Parse errors are indicated with red underlines.</span></span> <span data-ttu-id="a6c95-208">Quando você passa o cursor sobre um erro indicado, o texto da dica de ferramenta exibe o problema encontrado no código.</span><span class="sxs-lookup"><span data-stu-id="a6c95-208">When you hover over an indicated error, tooltip text displays the problem that was found in the code.</span></span>
- <span data-ttu-id="a6c95-209">**Zoom** – É possível definir o percentual de zoom do conteúdo do console usando o Controle Deslizante de Zoom (no canto inferior direito da janela do ISE do Windows PowerShell) ou digitando o comando `$psise.options.Zoom` no Painel de Console.</span><span class="sxs-lookup"><span data-stu-id="a6c95-209">**Zoom** - The zoom percentage of the console's content can be set by using the zoom slider (in the lower right corner of Windows PowerShell ISE window), or by entering the command `$psise.options.Zoom` in the Console Pane.</span></span>
- <span data-ttu-id="a6c95-210">**Copiar e colar rich text** – A cópia para a área de transferência no ISE do Windows PowerShell preserva as informações de fonte, tamanho e cor da seleção original.</span><span class="sxs-lookup"><span data-stu-id="a6c95-210">**Rich text copy and paste** - Copying to the clipboard in Windows PowerShell ISE preserves the font, size, and color information of the original selection.</span></span>
- <span data-ttu-id="a6c95-211">**Seleção de bloco** – Você pode selecionar um bloco de texto mantendo a tecla <kbd>ALT</kbd> pressionada enquanto seleciona o texto no Painel de Script com o mouse ou pressionando <kbd>Alt</kbd>+<kbd>Shift</kbd>+<kbd>Seta</kbd>.</span><span class="sxs-lookup"><span data-stu-id="a6c95-211">**Block selection** - You can select a block of text by holding down the <kbd>ALT</kbd> key while selecting text in the Script Pane with your mouse, or by pressing <kbd>Alt</kbd>+<kbd>Shift</kbd>+<kbd>Arrow</kbd>.</span></span>

<span data-ttu-id="a6c95-212">**Qual é o valor adicionado por esta alteração?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-212">**What value does this change add?**</span></span>

<span data-ttu-id="a6c95-213">Os recursos de edição adicionais fornecem um ambiente de edição mais consistente e eficiente.</span><span class="sxs-lookup"><span data-stu-id="a6c95-213">The additional editing features provide a more consistent and powerful editing environment.</span></span>

<span data-ttu-id="a6c95-214">**O que passou a funcionar de maneira diferente?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-214">**What works differently?**</span></span>

<span data-ttu-id="a6c95-215">Esses aprimoramentos na edição não estavam presentes no ISE do Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="a6c95-215">These editing enhancements weren't present in Windows PowerShell ISE 2.0.</span></span>

## <a name="new-help-viewer-window"></a><span data-ttu-id="a6c95-216">Janela do novo visualizador da ajuda</span><span class="sxs-lookup"><span data-stu-id="a6c95-216">New Help viewer window</span></span>

> <span data-ttu-id="a6c95-217">Adicionado no PowerShell 3.0</span><span class="sxs-lookup"><span data-stu-id="a6c95-217">Added in PowerShell 3.0</span></span>

<span data-ttu-id="a6c95-218">Se você pressionar <kbd>F1</kbd> quando o cursor estiver em um cmdlet ou se parte de um cmdlet estiver realçada, o novo visualizador da Ajuda abrirá uma ajuda contextual sobre o cmdlet realçado.</span><span class="sxs-lookup"><span data-stu-id="a6c95-218">If you press <kbd>F1</kbd> when your cursor is in a cmdlet, or you have part of a cmdlet highlighted, the new Help viewer opens context-sensitive Help about the highlighted cmdlet.</span></span> <span data-ttu-id="a6c95-219">Para exibir a ajuda **Sobre** do Windows PowerShell, digite `operators` no painel de console e pressione <kbd>F1</kbd>.</span><span class="sxs-lookup"><span data-stu-id="a6c95-219">To display Windows PowerShell **About** help, type `operators` in the console pane, and then press <kbd>F1</kbd>.</span></span>

<span data-ttu-id="a6c95-220">Antes de usar este recurso, baixe a versão mais atual dos tópicos de ajuda do Windows PowerShell do site da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a6c95-220">Before you use this feature, download the most current version of Windows PowerShell Help topics from the Microsoft website.</span></span> <span data-ttu-id="a6c95-221">O método mais simples para baixar os tópicos da Ajuda é executar o cmdlet `Update-Help` no painel de console durante a execução do ISE do Windows PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="a6c95-221">The simplest method for downloading the Help topics is to run the `Update-Help` cmdlet in the Console Pane when running Windows PowerShell ISE as administrator.</span></span>

<span data-ttu-id="a6c95-222">Você pode alterar onde a tecla <kbd>F1</kbd> busca Ajuda.</span><span class="sxs-lookup"><span data-stu-id="a6c95-222">You can alter where the <kbd>F1</kbd> key looks for Help.</span></span> <span data-ttu-id="a6c95-223">No menu **Ferramentas**/**Opções**, na guia **Configurações Gerais** em **Outras Configurações**, você pode marcar ou desmarcar a caixa de seleção **Usar conteúdo da ajuda local em vez de conteúdo online**.</span><span class="sxs-lookup"><span data-stu-id="a6c95-223">In the **Tools**/**Options** menu, on the **General Settings** tab, under **Other Settings**, you can set or clear the checkbox **Use local help content instead of online content**.</span></span> <span data-ttu-id="a6c95-224">Quando marcada, o cliente procurará o cmdlet Help na Ajuda baixada que se encontra na pasta de módulos.</span><span class="sxs-lookup"><span data-stu-id="a6c95-224">When checked, the client looks for the cmdlet Help in the downloaded Help found in the modules folder.</span></span> <span data-ttu-id="a6c95-225">Se a caixa de seleção for desmarcada, o cliente procurará na ajuda online.</span><span class="sxs-lookup"><span data-stu-id="a6c95-225">If the checkbox is cleared, the client looks for help online.</span></span>

<span data-ttu-id="a6c95-226">**Qual é o valor adicionado por esta alteração?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-226">**What value does this change add?**</span></span>

<span data-ttu-id="a6c95-227">A ajuda contextual sem deixar seu cmdlet ou script atual fornece uma experiência integrada de aprendizado.</span><span class="sxs-lookup"><span data-stu-id="a6c95-227">Context-sensitive Help without leaving your current cmdlet or script provides an integrated learning experience.</span></span>

<span data-ttu-id="a6c95-228">**O que passou a funcionar de maneira diferente?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-228">**What works differently?**</span></span>

<span data-ttu-id="a6c95-229">Pressionar <kbd>F1</kbd> em versões anteriores do ISE do Windows PowerShell abria o arquivo de ajuda no computador local.</span><span class="sxs-lookup"><span data-stu-id="a6c95-229">Pressing <kbd>F1</kbd> in previous versions of Windows PowerShell ISE opened the help file on the local computer.</span></span> <span data-ttu-id="a6c95-230">No ISE do Windows PowerShell 3.0 e posterior, é aberta uma janela que contém a ajuda para o cmdlet que é configurável e pesquisável.</span><span class="sxs-lookup"><span data-stu-id="a6c95-230">In Windows PowerShell ISE 3.0 and later, a window opens that contains the help for the cmdlet that is searchable and configurable.</span></span> <span data-ttu-id="a6c95-231">Essa experiência da ajuda é uma novidade no ISE do Windows PowerShell 3.0 e a Ajuda Atualizável é uma novidade no Windows PowerShell 3.0.</span><span class="sxs-lookup"><span data-stu-id="a6c95-231">This Help experience is new for Windows PowerShell ISE 3.0, and Updatable Help is new for Windows PowerShell 3.0.</span></span>

## <a name="show-command-cmdlet"></a><span data-ttu-id="a6c95-232">Cmdlet Show-Command</span><span class="sxs-lookup"><span data-stu-id="a6c95-232">Show-Command cmdlet</span></span>

> <span data-ttu-id="a6c95-233">Adicionado no PowerShell 3.0</span><span class="sxs-lookup"><span data-stu-id="a6c95-233">Added in PowerShell 3.0</span></span>

<span data-ttu-id="a6c95-234">O cmdlet `Show-Command` permite compor ou executar um cmdlet ou uma função com o preenchimento de um formulário gráfico.</span><span class="sxs-lookup"><span data-stu-id="a6c95-234">The `Show-Command` cmdlet enables you to compose or run a cmdlet or function by filling in a graphical form.</span></span> <span data-ttu-id="a6c95-235">O formulário permite que os usuários trabalhem com o Windows PowerShell em um ambiente gráfico.</span><span class="sxs-lookup"><span data-stu-id="a6c95-235">The form lets users work with Windows PowerShell in a graphical environment.</span></span>
<span data-ttu-id="a6c95-236">`Show-Command` também permite que os desenvolvedores de scripts avançados criem rapidamente uma GUI baseada no Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a6c95-236">`Show-Command` also enables advanced scripters to create a quick Windows PowerShell-based GUI.</span></span>

<span data-ttu-id="a6c95-237">**Qual é o valor adicionado por esta alteração?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-237">**What value does this change add?**</span></span>

<span data-ttu-id="a6c95-238">Usando `Show-Command` em seus scripts do Windows PowerShell, é possível fornecer aos usuários o ambiente gráfico com o qual eles estão familiarizados.</span><span class="sxs-lookup"><span data-stu-id="a6c95-238">By using `Show-Command` in your Windows PowerShell scripts, you can provide your users with the graphical environment with which they're familiar.</span></span> <span data-ttu-id="a6c95-239">`Show-Command` também pode ajudar os usuários iniciantes a aprender o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a6c95-239">`Show-Command` can also help introductory users learn Windows PowerShell.</span></span>

<span data-ttu-id="a6c95-240">**O que passou a funcionar de maneira diferente?**</span><span class="sxs-lookup"><span data-stu-id="a6c95-240">**What works differently?**</span></span>

<span data-ttu-id="a6c95-241">`Show-Command` é o novo ISE do Windows PowerShell 3.0.</span><span class="sxs-lookup"><span data-stu-id="a6c95-241">`Show-Command` is new Windows PowerShell ISE 3.0.</span></span>

## <a name="see-also"></a><span data-ttu-id="a6c95-242">Confira também</span><span class="sxs-lookup"><span data-stu-id="a6c95-242">See also</span></span>

<span data-ttu-id="a6c95-243">Para obter mais informações sobre como usar o ISE do Windows PowerShell, confira [Explorar o Ambiente de Script Integrado do Windows PowerShell](../ise/exploring-the-windows-powershell-ise.md).</span><span class="sxs-lookup"><span data-stu-id="a6c95-243">For more information about using Windows PowerShell ISE, see [Exploring the Windows PowerShell Integrated Scripting Environment](../ise/exploring-the-windows-powershell-ise.md).</span></span>
