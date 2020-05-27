---
ms.date: 12/31/2019
keywords: powershell, cmdlet
title: O objeto ISEEditor
ms.openlocfilehash: cb63acebc1a8bb9fa6cc07199088ae0d5441bc91
ms.sourcegitcommit: 2aec310ad0c0b048400cb56f6fa64c1e554c812a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2020
ms.locfileid: "83809692"
---
# <a name="the-iseeditor-object"></a><span data-ttu-id="1c87c-103">O objeto ISEEditor</span><span class="sxs-lookup"><span data-stu-id="1c87c-103">The ISEEditor Object</span></span>

<span data-ttu-id="1c87c-104">Um objeto **ISEEditor** é uma instância da classe Microsoft.PowerShell.Host.ISE.ISEEditor.</span><span class="sxs-lookup"><span data-stu-id="1c87c-104">An **ISEEditor** object is an instance of the Microsoft.PowerShell.Host.ISE.ISEEditor class.</span></span> <span data-ttu-id="1c87c-105">O painel de Console é um objeto **ISEEditor**.</span><span class="sxs-lookup"><span data-stu-id="1c87c-105">The Console pane is an **ISEEditor** object.</span></span> <span data-ttu-id="1c87c-106">Cada objeto [ISEFile](The-ISEFile-Object.md) tem um objeto **ISEEditor** associado.</span><span class="sxs-lookup"><span data-stu-id="1c87c-106">Each [ISEFile](The-ISEFile-Object.md) object has an associated **ISEEditor** object.</span></span> <span data-ttu-id="1c87c-107">As seções a seguir listam os métodos e as propriedades de um objeto **ISEEditor**.</span><span class="sxs-lookup"><span data-stu-id="1c87c-107">The following sections list the methods and properties of an **ISEEditor** object.</span></span>

## <a name="methods"></a><span data-ttu-id="1c87c-108">Métodos</span><span class="sxs-lookup"><span data-stu-id="1c87c-108">Methods</span></span>

### <a name="clear"></a><span data-ttu-id="1c87c-109">Clear\(\)</span><span class="sxs-lookup"><span data-stu-id="1c87c-109">Clear\(\)</span></span>

<span data-ttu-id="1c87c-110">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1c87c-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1c87c-111">Apaga o texto no editor.</span><span class="sxs-lookup"><span data-stu-id="1c87c-111">Clears the text in the editor.</span></span>

```powershell
# Clears the text in the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Clear()
```

### <a name="ensurevisibleint-linenumber"></a><span data-ttu-id="1c87c-112">EnsureVisible\(int lineNumber\)</span><span class="sxs-lookup"><span data-stu-id="1c87c-112">EnsureVisible\(int lineNumber\)</span></span>

<span data-ttu-id="1c87c-113">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1c87c-113">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1c87c-114">Rola o editor de modo que a linha que corresponde ao valor do parâmetro **lineNumber** especificado fique visível.</span><span class="sxs-lookup"><span data-stu-id="1c87c-114">Scrolls the editor so that the line that corresponds to the specified **lineNumber** parameter value is visible.</span></span> <span data-ttu-id="1c87c-115">Gerará uma exceção se o número de linha especificado estiver fora do intervalo de 1, último número da linha, que define os números de linha válidos.</span><span class="sxs-lookup"><span data-stu-id="1c87c-115">It throws an exception if the specified line number is outside the range of 1,last line number, which defines the valid line numbers.</span></span>

<span data-ttu-id="1c87c-116">**lineNumber** O número da linha que deve ficar visível.</span><span class="sxs-lookup"><span data-stu-id="1c87c-116">**lineNumber** The number of the line that is to be made visible.</span></span>

```powershell
# Scrolls the text in the Script pane so that the fifth line is in view.
$psISE.CurrentFile.Editor.EnsureVisible(5)
```

### <a name="focus"></a><span data-ttu-id="1c87c-117">Focus\(\)</span><span class="sxs-lookup"><span data-stu-id="1c87c-117">Focus\(\)</span></span>

<span data-ttu-id="1c87c-118">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1c87c-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1c87c-119">Define o foco para o editor.</span><span class="sxs-lookup"><span data-stu-id="1c87c-119">Sets the focus to the editor.</span></span>

```powershell
# Sets focus to the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Focus()
```

### <a name="getlinelengthint-linenumber-"></a><span data-ttu-id="1c87c-120">GetLineLength\(int lineNumber \)</span><span class="sxs-lookup"><span data-stu-id="1c87c-120">GetLineLength\(int lineNumber \)</span></span>

<span data-ttu-id="1c87c-121">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1c87c-121">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1c87c-122">Obtém o comprimento da linha como um inteiro para a linha especificada pelo número de linha.</span><span class="sxs-lookup"><span data-stu-id="1c87c-122">Gets the line length as an integer for the line that is specified by the line number.</span></span>

<span data-ttu-id="1c87c-123">**lineNumber** O número da linha cujo comprimento será obtido.</span><span class="sxs-lookup"><span data-stu-id="1c87c-123">**lineNumber** The number of the line of which to get the length.</span></span>

<span data-ttu-id="1c87c-124">**Returns** O comprimento da linha no número de linha especificado.</span><span class="sxs-lookup"><span data-stu-id="1c87c-124">**Returns** The line length for the line at the specified line number.</span></span>

```powershell
# Gets the length of the first line in the text of the Command pane.
$psISE.CurrentPowerShellTab.ConsolePane.GetLineLength(1)
```

### <a name="gotomatch"></a><span data-ttu-id="1c87c-125">GoToMatch\(\)</span><span class="sxs-lookup"><span data-stu-id="1c87c-125">GoToMatch\(\)</span></span>

<span data-ttu-id="1c87c-126">Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="1c87c-126">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="1c87c-127">Moverá o cursor do sistema para o caractere correspondente se a propriedade **CanGoToMatch** do objeto editor for `$true`, o que ocorrerá quando o cursor vier imediatamente antes de um parêntese de abertura, colchete ou chave – `(`,`[`,`{` – ou imediatamente após um parêntese de fechamento, colchete ou chave – `)`,`]`,`}`.</span><span class="sxs-lookup"><span data-stu-id="1c87c-127">Moves the caret to the matching character if the **CanGoToMatch** property of the editor object is `$true`, which occurs when the caret is immediately before an opening parenthesis, bracket, or brace - `(`,`[`,`{` - or immediately after a closing parenthesis, bracket, or brace - `)`,`]`,`}`.</span></span> <span data-ttu-id="1c87c-128">O cursor é colocado antes de um caractere de abertura ou depois de um caractere de fechamento.</span><span class="sxs-lookup"><span data-stu-id="1c87c-128">The caret is placed before an opening character or after a closing character.</span></span> <span data-ttu-id="1c87c-129">Se a propriedade **CanGoToMatch** for `$false`, esse método nada fará.</span><span class="sxs-lookup"><span data-stu-id="1c87c-129">If the **CanGoToMatch** property is `$false`, then this method does nothing.</span></span>

```powershell
# Goes to the matching character if CanGoToMatch() is $true
$psISE.CurrentPowerShellTab.ConsolePane.GoToMatch()
```

### <a name="inserttext-text-"></a><span data-ttu-id="1c87c-130">InsertText\( text \)</span><span class="sxs-lookup"><span data-stu-id="1c87c-130">InsertText\( text \)</span></span>

<span data-ttu-id="1c87c-131">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1c87c-131">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1c87c-132">Substitui a seleção por texto ou inserções de texto na posição do cursor atual.</span><span class="sxs-lookup"><span data-stu-id="1c87c-132">Replaces the selection with text or inserts text at the current caret position.</span></span>

<span data-ttu-id="1c87c-133">**text** – cadeia de caracteres, o texto a ser inserido.</span><span class="sxs-lookup"><span data-stu-id="1c87c-133">**text** - String The text to insert.</span></span>

<span data-ttu-id="1c87c-134">Veja o [Exemplo de script](#scripting-example), posteriormente neste tópico.</span><span class="sxs-lookup"><span data-stu-id="1c87c-134">See the [Scripting Example](#scripting-example) later in this topic.</span></span>

### <a name="select-startline-startcolumn-endline-endcolumn-"></a><span data-ttu-id="1c87c-135">Select\( startLine, startColumn, endLine, endColumn \)</span><span class="sxs-lookup"><span data-stu-id="1c87c-135">Select\( startLine, startColumn, endLine, endColumn \)</span></span>

<span data-ttu-id="1c87c-136">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1c87c-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1c87c-137">Seleciona o texto dos parâmetros **startLine**, **startColumn**, **endLine** e **endColumn**.</span><span class="sxs-lookup"><span data-stu-id="1c87c-137">Selects the text from the **startLine**, **startColumn**, **endLine**, and **endColumn** parameters.</span></span>

<span data-ttu-id="1c87c-138">**startLine** – inteiro, a linha na qual a seleção começa.</span><span class="sxs-lookup"><span data-stu-id="1c87c-138">**startLine** - Integer The line where the selection starts.</span></span>

<span data-ttu-id="1c87c-139">**startColumn** – inteiro, a coluna na linha inicial na qual a seleção começa.</span><span class="sxs-lookup"><span data-stu-id="1c87c-139">**startColumn** - Integer The column within the start line where the selection starts.</span></span>

<span data-ttu-id="1c87c-140">**endLine** – inteiro, a linha na qual a seleção é encerrada.</span><span class="sxs-lookup"><span data-stu-id="1c87c-140">**endLine** - Integer The line where the selection ends.</span></span>

<span data-ttu-id="1c87c-141">**endColumn** – inteiro, a coluna na linha final na qual a seleção é encerrada.</span><span class="sxs-lookup"><span data-stu-id="1c87c-141">**endColumn** - Integer The column within the end line where the selection ends.</span></span>

<span data-ttu-id="1c87c-142">Veja o [Exemplo de script](#scripting-example), posteriormente neste tópico.</span><span class="sxs-lookup"><span data-stu-id="1c87c-142">See the  [Scripting Example](#scripting-example) later in this topic.</span></span>

### <a name="selectcaretline"></a><span data-ttu-id="1c87c-143">SelectCaretLine\(\)</span><span class="sxs-lookup"><span data-stu-id="1c87c-143">SelectCaretLine\(\)</span></span>

<span data-ttu-id="1c87c-144">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1c87c-144">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1c87c-145">Seleciona toda a linha de texto que contém atualmente o circunflexo.</span><span class="sxs-lookup"><span data-stu-id="1c87c-145">Selects the entire line of text that currently contains the caret.</span></span>

```powershell
# First, set the caret position on line 5.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
# Now select that entire line of text
$psISE.CurrentFile.Editor.SelectCaretLine()
```

### <a name="setcaretposition-linenumber-columnnumber-"></a><span data-ttu-id="1c87c-146">SetCaretPosition\( lineNumber, columnNumber \)</span><span class="sxs-lookup"><span data-stu-id="1c87c-146">SetCaretPosition\( lineNumber, columnNumber \)</span></span>

<span data-ttu-id="1c87c-147">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1c87c-147">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1c87c-148">Define a posição do cursor no número de linha e no número da coluna.</span><span class="sxs-lookup"><span data-stu-id="1c87c-148">Sets the caret position at the line number and the column number.</span></span> <span data-ttu-id="1c87c-149">Gerará uma exceção se o número de linha do cursor ou o número da coluna do cursor estiverem fora de seus respectivos intervalos válidos.</span><span class="sxs-lookup"><span data-stu-id="1c87c-149">It throws an exception if either the caret line number or the caret column number are out of their respective valid ranges.</span></span>

<span data-ttu-id="1c87c-150">**lineNumber** – inteiro, o número de linha do cursor do sistema.</span><span class="sxs-lookup"><span data-stu-id="1c87c-150">**lineNumber** - Integer The caret line number.</span></span>

<span data-ttu-id="1c87c-151">**columnNumber** – inteiro, o número da coluna do cursor do sistema.</span><span class="sxs-lookup"><span data-stu-id="1c87c-151">**columnNumber** - Integer The caret column number.</span></span>

```powershell
# Set the CaretPosition.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
```

### <a name="toggleoutliningexpansion"></a><span data-ttu-id="1c87c-152">ToggleOutliningExpansion\(\)</span><span class="sxs-lookup"><span data-stu-id="1c87c-152">ToggleOutliningExpansion\(\)</span></span>

<span data-ttu-id="1c87c-153">Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="1c87c-153">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="1c87c-154">Faz com que toda a estrutura de tópicos se expanda ou se recolha.</span><span class="sxs-lookup"><span data-stu-id="1c87c-154">Causes all the outline sections to expand or collapse.</span></span>

```powershell
# Toggle the outlining expansion
$psISE.CurrentFile.Editor.ToggleOutliningExpansion()
```

## <a name="properties"></a><span data-ttu-id="1c87c-155">Propriedades</span><span class="sxs-lookup"><span data-stu-id="1c87c-155">Properties</span></span>

### <a name="cangotomatch"></a><span data-ttu-id="1c87c-156">CanGoToMatch</span><span class="sxs-lookup"><span data-stu-id="1c87c-156">CanGoToMatch</span></span>

<span data-ttu-id="1c87c-157">Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="1c87c-157">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="1c87c-158">A propriedade booliana somente leitura para indicar se o cursor está ao lado de um parêntese, colchete ou chave – `()`, `[]`, `{}`.</span><span class="sxs-lookup"><span data-stu-id="1c87c-158">The read-only Boolean property to indicate whether the caret is next to a parenthesis, bracket, or brace - `()`, `[]`, `{}`.</span></span> <span data-ttu-id="1c87c-159">Se o cursor estiver imediatamente antes do caractere de abertura ou imediatamente após o caractere de fechamento de um par, o valor da propriedade será `$true`.</span><span class="sxs-lookup"><span data-stu-id="1c87c-159">If the caret is immediately before the opening character or immediately after the closing character of a pair, then this property value is `$true`.</span></span> <span data-ttu-id="1c87c-160">Caso contrário, será `$false`.</span><span class="sxs-lookup"><span data-stu-id="1c87c-160">Otherwise, it is `$false`.</span></span>

```powershell
# Test to see if the caret is next to a parenthesis, bracket, or brace
$psISE.CurrentFile.Editor.CanGoToMatch
```

### <a name="caretcolumn"></a><span data-ttu-id="1c87c-161">CaretColumn</span><span class="sxs-lookup"><span data-stu-id="1c87c-161">CaretColumn</span></span>

<span data-ttu-id="1c87c-162">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1c87c-162">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1c87c-163">A propriedade somente leitura que obtém o número da coluna que corresponde à posição do cursor.</span><span class="sxs-lookup"><span data-stu-id="1c87c-163">The read-only property that gets the column number that corresponds to the position of the caret.</span></span>

```powershell
# Get the CaretColumn.
$psISE.CurrentFile.Editor.CaretColumn
```

### <a name="caretline"></a><span data-ttu-id="1c87c-164">CaretLine</span><span class="sxs-lookup"><span data-stu-id="1c87c-164">CaretLine</span></span>

<span data-ttu-id="1c87c-165">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1c87c-165">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1c87c-166">A propriedade somente leitura que obtém o número da linha que contém o cursor.</span><span class="sxs-lookup"><span data-stu-id="1c87c-166">The read-only property that gets the number of the line that contains the caret.</span></span>

```powershell
# Get the CaretLine.
$psISE.CurrentFile.Editor.CaretLine
```

### <a name="caretlinetext"></a><span data-ttu-id="1c87c-167">CaretLineText</span><span class="sxs-lookup"><span data-stu-id="1c87c-167">CaretLineText</span></span>

<span data-ttu-id="1c87c-168">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1c87c-168">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1c87c-169">A propriedade somente leitura que obtém a linha completa de texto que contém o cursor.</span><span class="sxs-lookup"><span data-stu-id="1c87c-169">The read-only property that gets the complete line of text that contains the caret.</span></span>

```powershell
# Get all of the text on the line that contains the caret.
$psISE.CurrentFile.Editor.CaretLineText
```

### <a name="linecount"></a><span data-ttu-id="1c87c-170">LineCount</span><span class="sxs-lookup"><span data-stu-id="1c87c-170">LineCount</span></span>

<span data-ttu-id="1c87c-171">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1c87c-171">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1c87c-172">A propriedade somente leitura que obtém a contagem de linha do editor.</span><span class="sxs-lookup"><span data-stu-id="1c87c-172">The read-only property that gets the line count from the editor.</span></span>

```powershell
# Get the LineCount.
$psISE.CurrentFile.Editor.LineCount
```

### <a name="selectedtext"></a><span data-ttu-id="1c87c-173">SelectedText</span><span class="sxs-lookup"><span data-stu-id="1c87c-173">SelectedText</span></span>

<span data-ttu-id="1c87c-174">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1c87c-174">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1c87c-175">A propriedade somente leitura que obtém o texto selecionado do editor.</span><span class="sxs-lookup"><span data-stu-id="1c87c-175">The read-only property that gets the selected text from the editor.</span></span>

<span data-ttu-id="1c87c-176">Veja o [Exemplo de script](#scripting-example), posteriormente neste tópico.</span><span class="sxs-lookup"><span data-stu-id="1c87c-176">See the  [Scripting Example](#scripting-example) later in this topic.</span></span>

### <a name="text"></a><span data-ttu-id="1c87c-177">Texto</span><span class="sxs-lookup"><span data-stu-id="1c87c-177">Text</span></span>

<span data-ttu-id="1c87c-178">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1c87c-178">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1c87c-179">A propriedade de leitura/gravação que obtém ou define o texto no editor.</span><span class="sxs-lookup"><span data-stu-id="1c87c-179">The read/write property that gets or sets the text in the editor.</span></span>

<span data-ttu-id="1c87c-180">Veja o [Exemplo de script](#scripting-example), posteriormente neste tópico.</span><span class="sxs-lookup"><span data-stu-id="1c87c-180">See the [Scripting Example](#scripting-example) later in this topic.</span></span>

## <a name="scripting-example"></a><span data-ttu-id="1c87c-181">Exemplo de Script</span><span class="sxs-lookup"><span data-stu-id="1c87c-181">Scripting Example</span></span>

```powershell
# This illustrates how you can use the length of a line to
# select the entire line and shows how you can make it lowercase.
# You must run this in the Console pane. It will not run in the Script pane.
# Begin by getting a variable that points to the editor.
$myEditor = $psISE.CurrentFile.Editor
# Clear the text in the current file editor.
$myEditor.Clear()

# Make sure the file has five lines of text.
$myEditor.InsertText("LINE1 `n")
$myEditor.InsertText("LINE2 `n")
$myEditor.InsertText("LINE3 `n")
$myEditor.InsertText("LINE4 `n")
$myEditor.InsertText("LINE5 `n")

# Use the GetLineLength method to get the length of the third line.
$endColumn = $myEditor.GetLineLength(3)
# Select the text in the first three lines.
$myEditor.Select(1, 1, 3, $endColumn + 1)
$selection = $myEditor.SelectedText
# Clear all the text in the editor.
$myEditor.Clear()
# Add the selected text back, but in lower case.
$myEditor.InsertText($selection.ToLower())
```

## <a name="see-also"></a><span data-ttu-id="1c87c-182">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="1c87c-182">See Also</span></span>

- [<span data-ttu-id="1c87c-183">O objeto ISEFile</span><span class="sxs-lookup"><span data-stu-id="1c87c-183">The ISEFile Object</span></span>](The-ISEFile-Object.md)
- [<span data-ttu-id="1c87c-184">O objeto PowerShellTab</span><span class="sxs-lookup"><span data-stu-id="1c87c-184">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md)
- [<span data-ttu-id="1c87c-185">Objetivo do modelo de objeto de script do ISE do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c87c-185">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="1c87c-186">A hierarquia de modelo de objeto do ISE</span><span class="sxs-lookup"><span data-stu-id="1c87c-186">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
