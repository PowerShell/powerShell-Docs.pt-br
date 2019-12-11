---
ms.date: 06/05/2017
keywords: powershell, cmdlet
title: O objeto ISEFile
ms.openlocfilehash: ebb5a35f6ea9d93eab633b9f4e6c84e4fddd6ae8
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "67028949"
---
# <a name="the-isefile-object"></a><span data-ttu-id="1a66b-103">O objeto ISEFile</span><span class="sxs-lookup"><span data-stu-id="1a66b-103">The ISEFile Object</span></span>

<span data-ttu-id="1a66b-104">Um objeto **ISEFile** representa um arquivo no ISE (Ambiente de Script Integrado) do Windows PowerShell®.</span><span class="sxs-lookup"><span data-stu-id="1a66b-104">An **ISEFile** object represents a file in Windows PowerShell® Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="1a66b-105">É uma instância da classe Microsoft.PowerShell.Host.ISE.ISEFile.</span><span class="sxs-lookup"><span data-stu-id="1a66b-105">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEFile class.</span></span> <span data-ttu-id="1a66b-106">Este tópico lista os métodos e as propriedades do membro.</span><span class="sxs-lookup"><span data-stu-id="1a66b-106">This topic lists its member methods and member properties.</span></span> <span data-ttu-id="1a66b-107">O **$psISE.CurrentFile** e os arquivos da coleção de arquivos em uma guia do PowerShell são todas as instâncias da classe Microsoft.PowerShell.Host.ISE.ISEFile.</span><span class="sxs-lookup"><span data-stu-id="1a66b-107">The **$psISE.CurrentFile** and the files in the Files collection in a PowerShell tab are all instances of the Microsoft.PowerShell.Host.ISE.ISEFile class.</span></span>

## <a name="methods"></a><span data-ttu-id="1a66b-108">Métodos</span><span class="sxs-lookup"><span data-stu-id="1a66b-108">Methods</span></span>

### <a name="save-saveencoding-"></a><span data-ttu-id="1a66b-109">Save\( \[saveEncoding\] \)</span><span class="sxs-lookup"><span data-stu-id="1a66b-109">Save\( \[saveEncoding\] \)</span></span>

<span data-ttu-id="1a66b-110">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1a66b-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1a66b-111">Salva o arquivo no disco.</span><span class="sxs-lookup"><span data-stu-id="1a66b-111">Saves the file to disk.</span></span>

<span data-ttu-id="1a66b-112">**\[saveEncoding\]** – [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) opcional Um parâmetro opcional de codificação de caracteres a ser usado para o arquivo salvo.</span><span class="sxs-lookup"><span data-stu-id="1a66b-112">**\[saveEncoding\]** - optional [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) An optional character encoding parameter to be used for the saved file.</span></span> <span data-ttu-id="1a66b-113">O valor padrão é **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="1a66b-113">The default value is **UTF8**.</span></span>

### <a name="exceptions"></a><span data-ttu-id="1a66b-114">Exceções</span><span class="sxs-lookup"><span data-stu-id="1a66b-114">Exceptions</span></span>

- <span data-ttu-id="1a66b-115">**System.IO.IOException**: não foi possível salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="1a66b-115">**System.IO.IOException**: The file could not be saved.</span></span>

```powershell
# Save the file using the default encoding (UTF8)
$psISE.CurrentFile.Save()

# Save the file as ASCII.
$psISE.CurrentFile.Save([System.Text.Encoding]::ASCII)

# Gets the current encoding.
$myfile = $psISE.CurrentFile
$myfile.Encoding
```

### <a name="saveasfilename-saveencoding"></a><span data-ttu-id="1a66b-116">SaveAs\(filename, \[saveEncoding\]\)</span><span class="sxs-lookup"><span data-stu-id="1a66b-116">SaveAs\(filename, \[saveEncoding\]\)</span></span>

<span data-ttu-id="1a66b-117">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1a66b-117">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1a66b-118">Salva o arquivo com o nome de arquivo e codificação especificados.</span><span class="sxs-lookup"><span data-stu-id="1a66b-118">Saves the file with the specified file name and encoding.</span></span>

<span data-ttu-id="1a66b-119">**filename** – cadeia de caracteres, o nome a ser usado para salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="1a66b-119">**filename** - String The name to be used to save the file.</span></span>

<span data-ttu-id="1a66b-120">**\[saveEncoding\]** – [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) opcional Um parâmetro opcional de codificação de caracteres a ser usado para o arquivo salvo.</span><span class="sxs-lookup"><span data-stu-id="1a66b-120">**\[saveEncoding\]** - optional [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) An optional character encoding parameter to be used for the saved file.</span></span> <span data-ttu-id="1a66b-121">O valor padrão é **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="1a66b-121">The default value is **UTF8**.</span></span>

### <a name="exceptions"></a><span data-ttu-id="1a66b-122">Exceções</span><span class="sxs-lookup"><span data-stu-id="1a66b-122">Exceptions</span></span>

- <span data-ttu-id="1a66b-123">**System.ArgumentNullException**: o parâmetro **filename** é nulo.</span><span class="sxs-lookup"><span data-stu-id="1a66b-123">**System.ArgumentNullException**: The **filename** parameter is null.</span></span>
- <span data-ttu-id="1a66b-124">**System.ArgumentException**: o parâmetro **filename** está vazio.</span><span class="sxs-lookup"><span data-stu-id="1a66b-124">**System.ArgumentException**: The **filename** parameter is empty.</span></span>
- <span data-ttu-id="1a66b-125">**System.IO.IOException**: não foi possível salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="1a66b-125">**System.IO.IOException**: The file could not be saved.</span></span>

```powershell
# Save the file with a full path and name.
$fullpath = "c:\temp\newname.txt"
$psISE.CurrentFile.SaveAs($fullPath)
# Save the file with a full path and name and explicitly as UTF8.
$psISE.CurrentFile.SaveAs($fullPath, [System.Text.Encoding]::UTF8)
```

## <a name="properties"></a><span data-ttu-id="1a66b-126">Propriedades</span><span class="sxs-lookup"><span data-stu-id="1a66b-126">Properties</span></span>

### <a name="displayname"></a><span data-ttu-id="1a66b-127">DisplayName</span><span class="sxs-lookup"><span data-stu-id="1a66b-127">DisplayName</span></span>

<span data-ttu-id="1a66b-128">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1a66b-128">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1a66b-129">A propriedade somente leitura que obtém a cadeia que contém o nome de exibição deste arquivo.</span><span class="sxs-lookup"><span data-stu-id="1a66b-129">The read-only property that gets the string that contains the display name of this file.</span></span> <span data-ttu-id="1a66b-130">O nome é mostrado na guia **Arquivo** na parte superior do editor.</span><span class="sxs-lookup"><span data-stu-id="1a66b-130">The name is shown on the **File** tab at the top of the editor.</span></span> <span data-ttu-id="1a66b-131">A presença de um asterisco \(\*\) ao final do nome indica que o arquivo tem alterações que não foram salvas.</span><span class="sxs-lookup"><span data-stu-id="1a66b-131">The presence of an asterisk \(\*\) at the end of the name indicates that the file has changes that have not been saved.</span></span>

```powershell
# Shows the display name of the file.
$psISE.CurrentFile.DisplayName
```

### <a name="editor"></a><span data-ttu-id="1a66b-132">Editor</span><span class="sxs-lookup"><span data-stu-id="1a66b-132">Editor</span></span>

<span data-ttu-id="1a66b-133">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1a66b-133">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1a66b-134">A propriedade somente leitura que obtém o [objeto editor](The-ISEEditor-Object.md) usado para o arquivo especificado.</span><span class="sxs-lookup"><span data-stu-id="1a66b-134">The read-only property that gets the [editor object](The-ISEEditor-Object.md) that is used for the specified file.</span></span>

```powershell
# Gets the editor and the text.
$psISE.CurrentFile.Editor.Text
```

### <a name="encoding"></a><span data-ttu-id="1a66b-135">Codificando</span><span class="sxs-lookup"><span data-stu-id="1a66b-135">Encoding</span></span>

<span data-ttu-id="1a66b-136">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1a66b-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1a66b-137">A propriedade somente leitura que obtém a codificação original do arquivo.</span><span class="sxs-lookup"><span data-stu-id="1a66b-137">The read-only property that gets the original file encoding.</span></span> <span data-ttu-id="1a66b-138">Este é um objeto **System.Text.Encoding**.</span><span class="sxs-lookup"><span data-stu-id="1a66b-138">This is a **System.Text.Encoding** object.</span></span>

```powershell
# Shows the encoding for the file.
$psISE.CurrentFile.Encoding
```

### <a name="fullpath"></a><span data-ttu-id="1a66b-139">FullPath</span><span class="sxs-lookup"><span data-stu-id="1a66b-139">FullPath</span></span>

<span data-ttu-id="1a66b-140">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1a66b-140">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1a66b-141">A propriedade somente leitura que obtém a cadeia de caracteres que especifica o caminho completo do arquivo aberto.</span><span class="sxs-lookup"><span data-stu-id="1a66b-141">The read-only property that gets the string that specifies the full path of the opened file.</span></span>

```powershell
# Shows the full path for the file.
$psISE.CurrentFile.FullPath
```

### <a name="issaved"></a><span data-ttu-id="1a66b-142">IsSaved</span><span class="sxs-lookup"><span data-stu-id="1a66b-142">IsSaved</span></span>

<span data-ttu-id="1a66b-143">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1a66b-143">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1a66b-144">A propriedade Boolean somente leitura que retornará **$true** se o arquivo foi salvo depois de ter sido modificado pela última vez.</span><span class="sxs-lookup"><span data-stu-id="1a66b-144">The read-only Boolean property that returns **$true** if the file has been saved after it was last modified.</span></span>

```powershell
# Determines whether the file has been saved since it was last modified.
$myfile = $psISE.CurrentFile
$myfile.IsSaved
```

### <a name="isuntitled"></a><span data-ttu-id="1a66b-145">IsUntitled</span><span class="sxs-lookup"><span data-stu-id="1a66b-145">IsUntitled</span></span>

<span data-ttu-id="1a66b-146">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="1a66b-146">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1a66b-147">A propriedade somente leitura que retornará **$true** se o arquivo nunca recebeu um título.</span><span class="sxs-lookup"><span data-stu-id="1a66b-147">The read-only property that returns **$true** if the file has never been given a title.</span></span>

```powershell
# Determines whether the file has never been given a title.
$psISE.CurrentFile.IsUntitled
$psISE.CurrentFile.SaveAs("temp.txt")
$psISE.CurrentFile.IsUntitled
```

## <a name="see-also"></a><span data-ttu-id="1a66b-148">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="1a66b-148">See Also</span></span>

- [<span data-ttu-id="1a66b-149">O ISEFileCollectionObject</span><span class="sxs-lookup"><span data-stu-id="1a66b-149">The ISEFileCollectionObject</span></span>](The-ISEFileCollection-Object.md)
- [<span data-ttu-id="1a66b-150">Objetivo do modelo de objeto de script do ISE do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1a66b-150">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="1a66b-151">A hierarquia de modelo de objeto do ISE</span><span class="sxs-lookup"><span data-stu-id="1a66b-151">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
