---
title: Palavras-chave de ajuda com base em comentários | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ab90ec96-77f5-42e3-9c7e-2f4156ec207f
caps.latest.revision: 6
ms.openlocfilehash: 534a6c9a43326c8a01b2181c7a799286fa4d3997
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72361355"
---
# <a name="comment-based-help-keywords"></a><span data-ttu-id="15639-102">Palavras-chave de ajuda baseada em comentários</span><span class="sxs-lookup"><span data-stu-id="15639-102">Comment-Based Help Keywords</span></span>

<span data-ttu-id="15639-103">Este tópico lista e descreve as palavras-chave na Ajuda baseada em comentários.</span><span class="sxs-lookup"><span data-stu-id="15639-103">This topic lists and describes the keywords in comment-based help.</span></span>

## <a name="keywords-in-comment-based-help"></a><span data-ttu-id="15639-104">Palavras-chave na Ajuda baseada em comentários</span><span class="sxs-lookup"><span data-stu-id="15639-104">Keywords in Comment-Based Help</span></span>

<span data-ttu-id="15639-105">Veja a seguir as palavras-chave de ajuda com base em comentários válidas.</span><span class="sxs-lookup"><span data-stu-id="15639-105">The following are valid comment-based Help keywords.</span></span> <span data-ttu-id="15639-106">Eles são listados na ordem em que normalmente aparecem em um tópico da ajuda junto com o uso pretendido.</span><span class="sxs-lookup"><span data-stu-id="15639-106">They are listed in the order in which they typically appear in a Help topic along with their intended use.</span></span> <span data-ttu-id="15639-107">Essas palavras-chave podem aparecer em qualquer ordem na Ajuda baseada em comentários e não diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="15639-107">These keywords can appear in any order in the comment-based Help, and they are not case-sensitive.</span></span>

<span data-ttu-id="15639-108">Observe que a palavra-chave `.ExternalHelp` tem precedência sobre todas as outras palavras-chaves de ajuda baseadas em comentários.</span><span class="sxs-lookup"><span data-stu-id="15639-108">Note that the `.ExternalHelp` keyword takes precedence over all other comment-based help keywords.</span></span> <span data-ttu-id="15639-109">Quando `.ExternalHelp` estiver presente, o cmdlet [Microsoft. PowerShell. Commands. GetHelpCommand](/dotnet/api/Microsoft.PowerShell.Commands.gethelpcommand) não exibirá ajuda baseada em comentários, mesmo quando ele não encontrar um arquivo de ajuda que corresponda ao valor da palavra-chave.</span><span class="sxs-lookup"><span data-stu-id="15639-109">When `.ExternalHelp` is present, the [Microsoft.PowerShell.Commands.GetHelpCommand](/dotnet/api/Microsoft.PowerShell.Commands.gethelpcommand) cmdlet does not display comment-based help, even when it cannot find a help file that matches the value of the keyword.</span></span>

<span data-ttu-id="15639-110">`.Synopsis` uma breve descrição da função ou do script.</span><span class="sxs-lookup"><span data-stu-id="15639-110">`.Synopsis` A brief description of the function or script.</span></span> <span data-ttu-id="15639-111">Essa palavra-chave pode ser usada apenas uma vez em cada tópico.</span><span class="sxs-lookup"><span data-stu-id="15639-111">This keyword can be used only once in each topic.</span></span>

<span data-ttu-id="15639-112">`.Description` uma descrição detalhada da função ou do script.</span><span class="sxs-lookup"><span data-stu-id="15639-112">`.Description` A detailed description of the function or script.</span></span> <span data-ttu-id="15639-113">Essa palavra-chave pode ser usada apenas uma vez em cada tópico.</span><span class="sxs-lookup"><span data-stu-id="15639-113">This keyword can be used only once in each topic.</span></span>

<span data-ttu-id="15639-114">`.Parameter` *\<Parameter-Name >* a descrição de um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="15639-114">`.Parameter` *\<Parameter-Name>* The description of a parameter.</span></span> <span data-ttu-id="15639-115">Você pode incluir uma palavra-chave `.Parameter` para cada parâmetro na função ou script.</span><span class="sxs-lookup"><span data-stu-id="15639-115">You can include a `.Parameter` keyword for each parameter in the function or script.</span></span>

<span data-ttu-id="15639-116">As palavras-chave `.Parameter` podem aparecer em qualquer ordem no bloco de comentários, mas a ordem na qual os parâmetros aparecem na instrução `Param` ou declaração de função determina a ordem na qual os parâmetros aparecem no tópico da ajuda.</span><span class="sxs-lookup"><span data-stu-id="15639-116">The `.Parameter` keywords can appear in any order in the comment block, but the order in which the parameters appear in the `Param` statement or function declaration determines the order in which the parameters appear in Help topic.</span></span> <span data-ttu-id="15639-117">Para alterar a ordem dos parâmetros no tópico da ajuda, altere a ordem dos parâmetros na instrução `Param` ou na declaração da função.</span><span class="sxs-lookup"><span data-stu-id="15639-117">To change the order of parameters in the Help topic, change the order of the parameters in the `Param` statement or function declaration.</span></span>

<span data-ttu-id="15639-118">Você também pode especificar uma descrição de parâmetro colocando um comentário na instrução `Param` imediatamente antes do nome da variável de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="15639-118">You can also specify a parameter description by placing a comment in the `Param` statement immediately before the parameter variable name.</span></span> <span data-ttu-id="15639-119">Se você usar um comentário de instrução `Param` e uma palavra-chave `.Parameter`, a descrição associada à palavra-chave `.Parameter` será usada e o comentário da instrução `Param` será ignorado.</span><span class="sxs-lookup"><span data-stu-id="15639-119">If you use both a `Param` statement comment and a `.Parameter` keyword, the description associated with the `.Parameter` keyword is used, and the `Param` statement comment is ignored.</span></span>

<span data-ttu-id="15639-120">`.Example` um comando de exemplo que usa a função ou o script, opcionalmente seguido por saída de exemplo e uma descrição.</span><span class="sxs-lookup"><span data-stu-id="15639-120">`.Example` A sample command that uses the function or script, optionally followed by sample output and a description.</span></span> <span data-ttu-id="15639-121">Repita essa palavra-chave para cada exemplo.</span><span class="sxs-lookup"><span data-stu-id="15639-121">Repeat this keyword for each example.</span></span>

<span data-ttu-id="15639-122">`.Inputs` os tipos de Microsoft .NET estrutura de objetos que podem ser canalizados para a função ou o script.</span><span class="sxs-lookup"><span data-stu-id="15639-122">`.Inputs` The Microsoft .NET Framework types of objects that can be piped to the function or script.</span></span> <span data-ttu-id="15639-123">Você também pode incluir uma descrição dos objetos de entrada.</span><span class="sxs-lookup"><span data-stu-id="15639-123">You can also include a description of the input objects.</span></span>

<span data-ttu-id="15639-124">`.Outputs` o .NET Framework tipo dos objetos que o cmdlet retorna.</span><span class="sxs-lookup"><span data-stu-id="15639-124">`.Outputs` The .NET Framework type of the objects that the cmdlet returns.</span></span> <span data-ttu-id="15639-125">Você também pode incluir uma descrição dos objetos retornados.</span><span class="sxs-lookup"><span data-stu-id="15639-125">You can also include a description of the returned objects.</span></span>

<span data-ttu-id="15639-126">`.Notes` informações adicionais sobre a função ou o script.</span><span class="sxs-lookup"><span data-stu-id="15639-126">`.Notes` Additional information about the function or script.</span></span>

<span data-ttu-id="15639-127">`.Link` o nome de um tópico relacionado.</span><span class="sxs-lookup"><span data-stu-id="15639-127">`.Link` The name of a related topic.</span></span> <span data-ttu-id="15639-128">Repita essa palavra-chave para cada tópico relacionado.</span><span class="sxs-lookup"><span data-stu-id="15639-128">Repeat this keyword for each related topic.</span></span> <span data-ttu-id="15639-129">Esse conteúdo aparece na seção links relacionados do tópico da ajuda.</span><span class="sxs-lookup"><span data-stu-id="15639-129">This content appears in the Related Links section of the Help topic.</span></span>

<span data-ttu-id="15639-130">O conteúdo da palavra-chave `.Link` também pode incluir um Uniform Resource Identifier (URI) para uma versão online do mesmo tópico da ajuda.</span><span class="sxs-lookup"><span data-stu-id="15639-130">The `.Link` keyword content can also include a Uniform Resource Identifier (URI) to an online version of the same Help topic.</span></span> <span data-ttu-id="15639-131">A versão online é aberta quando você usa o parâmetro `Online` de Get-Help.</span><span class="sxs-lookup"><span data-stu-id="15639-131">The online version opens when you use the `Online` parameter of Get-Help.</span></span> <span data-ttu-id="15639-132">O URI deve começar com "http" ou "https".</span><span class="sxs-lookup"><span data-stu-id="15639-132">The URI must begin with "http" or "https".</span></span>

<span data-ttu-id="15639-133">`.Component` a tecnologia ou o recurso que a função ou o script usa, ou ao qual ele está relacionado.</span><span class="sxs-lookup"><span data-stu-id="15639-133">`.Component` The technology or feature that the function or script uses, or to which it is related.</span></span> <span data-ttu-id="15639-134">Esse conteúdo é exibido quando o comando Get-Help inclui o parâmetro `Component` de Get-Help.</span><span class="sxs-lookup"><span data-stu-id="15639-134">This content appears when the Get-Help command includes the `Component` parameter of Get-Help.</span></span>

<span data-ttu-id="15639-135">`.Role` a função de usuário para o tópico da ajuda.</span><span class="sxs-lookup"><span data-stu-id="15639-135">`.Role` The user role for the Help topic.</span></span> <span data-ttu-id="15639-136">Esse conteúdo é exibido quando o comando Get-Help inclui o parâmetro `Role` de Get-Help.</span><span class="sxs-lookup"><span data-stu-id="15639-136">This content appears when the Get-Help command includes the `Role` parameter of Get-Help.</span></span>

<span data-ttu-id="15639-137">`.Functionality` o uso pretendido da função.</span><span class="sxs-lookup"><span data-stu-id="15639-137">`.Functionality` The intended use of the function.</span></span> <span data-ttu-id="15639-138">Esse conteúdo é exibido quando o comando Get-Help inclui o parâmetro `Functionality` de Get-Help.</span><span class="sxs-lookup"><span data-stu-id="15639-138">This content appears when the Get-Help command includes the `Functionality` parameter of Get-Help.</span></span>

<span data-ttu-id="15639-139">`.ForwardHelpTargetName` `<Command-Name>` redireciona para o tópico da ajuda para o comando especificado.</span><span class="sxs-lookup"><span data-stu-id="15639-139">`.ForwardHelpTargetName` `<Command-Name>` Redirects to the Help topic for the specified command.</span></span> <span data-ttu-id="15639-140">Você pode redirecionar os usuários para qualquer tópico da ajuda, incluindo tópicos de ajuda para uma função, script, cmdlet ou provedor.</span><span class="sxs-lookup"><span data-stu-id="15639-140">You can redirect users to any Help topic, including Help topics for a function, script, cmdlet, or provider.</span></span>

<span data-ttu-id="15639-141">`.ForwardHelpCategory` `<Category>` especifica a categoria de ajuda do item em ForwardHelpTargetName.</span><span class="sxs-lookup"><span data-stu-id="15639-141">`.ForwardHelpCategory` `<Category>` Specifies the Help category of the item in ForwardHelpTargetName.</span></span> <span data-ttu-id="15639-142">Os valores válidos são alias, cmdlet, ArquivoDeAjuda, função, provedor, geral, perguntas frequentes, Glossário, ScriptCommand, ExternalScript, filtro ou todos.</span><span class="sxs-lookup"><span data-stu-id="15639-142">Valid values are Alias, Cmdlet, HelpFile, Function, Provider, General, FAQ, Glossary, ScriptCommand, ExternalScript, Filter, or All.</span></span> <span data-ttu-id="15639-143">Use essa palavra-chave para evitar conflitos quando houver comandos com o mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="15639-143">Use this keyword to avoid conflicts when there are commands with the same name.</span></span>

<span data-ttu-id="15639-144">`.RemoteHelpRunspace` `<PSSession-variable>` especifica uma sessão que contém o tópico da ajuda.</span><span class="sxs-lookup"><span data-stu-id="15639-144">`.RemoteHelpRunspace` `<PSSession-variable>` Specifies a session that contains the Help topic.</span></span> <span data-ttu-id="15639-145">Insira uma variável que contenha uma PSSession.</span><span class="sxs-lookup"><span data-stu-id="15639-145">Enter a variable that contains a PSSession.</span></span> <span data-ttu-id="15639-146">Essa palavra-chave é usada pelo cmdlet `Export-PSSession` para localizar os tópicos da ajuda para os comandos exportados.</span><span class="sxs-lookup"><span data-stu-id="15639-146">This keyword is used by the `Export-PSSession` cmdlet to find the Help topics for the exported commands.</span></span>

<span data-ttu-id="15639-147">`.ExternalHelp` `<XML Help File>` especifica o caminho e/ou o nome de um arquivo de ajuda baseado em XML para o script ou a função.</span><span class="sxs-lookup"><span data-stu-id="15639-147">`.ExternalHelp` `<XML Help File>` Specifies the path and/or name of an XML-based Help file for the script or function.</span></span>

<span data-ttu-id="15639-148">A palavra-chave `.ExternalHelp` informa o cmdlet [Microsoft. PowerShell. Commands. GetHelpCommand](/dotnet/api/Microsoft.PowerShell.Commands.gethelpcommand) para obter ajuda para o script ou a função em um arquivo baseado em XML.</span><span class="sxs-lookup"><span data-stu-id="15639-148">The `.ExternalHelp` keyword tells the [Microsoft.PowerShell.Commands.GetHelpCommand](/dotnet/api/Microsoft.PowerShell.Commands.gethelpcommand) cmdlet to get help for the script or function in an XML-based file.</span></span> <span data-ttu-id="15639-149">O **.** A palavra-chave ExternalHelp é necessária ao usar um arquivo de ajuda baseado em XML para um script ou uma função.</span><span class="sxs-lookup"><span data-stu-id="15639-149">The **.ExternalHelp** keyword is required when using an XML-based help file for a script or function.</span></span> <span data-ttu-id="15639-150">Sem ele, `Get-Help` não encontrará um arquivo de ajuda para a função ou o script.</span><span class="sxs-lookup"><span data-stu-id="15639-150">Without it, `Get-Help` will not find a help file for the function or script.</span></span>

<span data-ttu-id="15639-151">A palavra-chave `.ExternalHelp` tem precedência sobre todas as outras palavras-chaves de ajuda baseadas em comentários.</span><span class="sxs-lookup"><span data-stu-id="15639-151">The `.ExternalHelp` keyword takes precedence over all other comment-based help keywords.</span></span> <span data-ttu-id="15639-152">Quando `.ExternalHelp` estiver presente, o cmdlet [Microsoft. PowerShell. Commands. GetHelpCommand](/dotnet/api/Microsoft.PowerShell.Commands.gethelpcommand) não exibirá ajuda baseada em comentários, mesmo quando ele não encontrar um arquivo de ajuda que corresponda ao valor da palavra-chave.</span><span class="sxs-lookup"><span data-stu-id="15639-152">When `.ExternalHelp` is present, the [Microsoft.PowerShell.Commands.GetHelpCommand](/dotnet/api/Microsoft.PowerShell.Commands.gethelpcommand) cmdlet does not display comment-based help, even when it cannot find a help file that matches the value of the keyword.</span></span>

<span data-ttu-id="15639-153">Quando a função é exportada por um módulo de script, o valor de `.ExternalHelp` deve ser um nome de arquivo sem um caminho.</span><span class="sxs-lookup"><span data-stu-id="15639-153">When the function is exported by a script module, the value of `.ExternalHelp` should be a file name without a path.</span></span> <span data-ttu-id="15639-154">`Get-Help` procura o arquivo em um subdiretório específico da localidade do diretório do módulo.</span><span class="sxs-lookup"><span data-stu-id="15639-154">`Get-Help` looks for the file in a locale-specific subdirectory of the module directory.</span></span> <span data-ttu-id="15639-155">Não há requisitos para o nome do arquivo, mas uma prática recomendada é usar o seguinte formato de nome de arquivo: `<ScriptModule>.psm1-help.xml`.</span><span class="sxs-lookup"><span data-stu-id="15639-155">There are no requirements for the file name, but a best practice is to use the following file name format: `<ScriptModule>.psm1-help.xml`.</span></span>

<span data-ttu-id="15639-156">Quando a função não estiver associada a um módulo, inclua um caminho e um nome de arquivo no valor de **.** Palavra-chave ExternalHelp.</span><span class="sxs-lookup"><span data-stu-id="15639-156">When the function is not associated with a module, include a path and file name in the value of the **.ExternalHelp** keyword.</span></span> <span data-ttu-id="15639-157">Se o caminho especificado para o arquivo XML contiver subdiretórios específicos da cultura da interface do usuário, `Get-Help` pesquisará recursivamente os subdiretórios para um arquivo XML com o nome do script ou função de acordo com os padrões de fallback de idioma estabelecidos para o Windows , assim como acontece com todos os tópicos de ajuda baseados em XML.</span><span class="sxs-lookup"><span data-stu-id="15639-157">If the specified path to the XML file contains UI-culture-specific subdirectories, `Get-Help` searches the subdirectories recursively for an XML file with the name of the script or function in accordance with the language fallback standards established for Windows, just as it does for all XML-based Help topics.</span></span>

<span data-ttu-id="15639-158">Para obter mais informações sobre o formato de arquivo de ajuda baseado em XML da ajuda do cmdlet, consulte [a ajuda do cmdlet Writing Windows PowerShell](./writing-help-for-windows-powershell-cmdlets.md).</span><span class="sxs-lookup"><span data-stu-id="15639-158">For more information about the cmdlet Help XML-based Help file format, see [Writing Windows PowerShell Cmdlet Help](./writing-help-for-windows-powershell-cmdlets.md).</span></span>