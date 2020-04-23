---
ms.date: 12/31/2019
keywords: powershell, cmdlet
title: O objeto ISEFileCollection
ms.openlocfilehash: 4192afa9dc91d9ea4c4c084d3ba0175483620229
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "75736208"
---
# <a name="the-isefilecollection-object"></a><span data-ttu-id="59a75-103">O objeto ISEFileCollection</span><span class="sxs-lookup"><span data-stu-id="59a75-103">The ISEFileCollection Object</span></span>

<span data-ttu-id="59a75-104">O objeto **ISEFileCollection** é uma coleção de objetos **ISEFile**.</span><span class="sxs-lookup"><span data-stu-id="59a75-104">The **ISEFileCollection** object is a collection of **ISEFile** objects.</span></span> <span data-ttu-id="59a75-105">Um exemplo é a coleção `$psISE.CurrentPowerShellTab.Files`.</span><span class="sxs-lookup"><span data-stu-id="59a75-105">An example is the `$psISE.CurrentPowerShellTab.Files` collection.</span></span>

## <a name="methods"></a><span data-ttu-id="59a75-106">Métodos</span><span class="sxs-lookup"><span data-stu-id="59a75-106">Methods</span></span>

### <a name="add-fullpath-"></a><span data-ttu-id="59a75-107">Add\( \[FullPath\] \)</span><span class="sxs-lookup"><span data-stu-id="59a75-107">Add\( \[FullPath\] \)</span></span>

<span data-ttu-id="59a75-108">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="59a75-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="59a75-109">Cria e retorna um novo arquivo sem título e o adiciona à coleção.</span><span class="sxs-lookup"><span data-stu-id="59a75-109">Creates and returns a new untitled file and adds it to the collection.</span></span> <span data-ttu-id="59a75-110">A propriedade **IsUntitled** do arquivo recém-criado é `$true`.</span><span class="sxs-lookup"><span data-stu-id="59a75-110">The **IsUntitled** property of the newly created file is `$true`.</span></span>

<span data-ttu-id="59a75-111">**\[FullPath\]** – Cadeia de caracteres opcional, o caminho totalmente especificado do arquivo.</span><span class="sxs-lookup"><span data-stu-id="59a75-111">**\[FullPath\]** - Optional string The fully specified path of the file.</span></span> <span data-ttu-id="59a75-112">Uma exceção será gerada se você incluir o parâmetro **FullPath** e um caminho relativo ou se você usar um nome de arquivo em vez do caminho completo.</span><span class="sxs-lookup"><span data-stu-id="59a75-112">An exception is generated if you include the **FullPath** parameter and a relative path, or if you use a file name instead of the full path.</span></span>

```powershell
# Adds a new untitled file to the collection of files in the current PowerShell tab.
$newFile = $psISE.CurrentPowerShellTab.Files.Add()

# Adds a file specified by its full path to the collection of files in the current PowerShell tab.
$psISE.CurrentPowerShellTab.Files.Add("$pshome\Examples\profile.ps1")
```

### <a name="remove-file-force-"></a><span data-ttu-id="59a75-113">Remove\( File, \[Force\] \)</span><span class="sxs-lookup"><span data-stu-id="59a75-113">Remove\( File, \[Force\] \)</span></span>

<span data-ttu-id="59a75-114">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="59a75-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="59a75-115">Remove um arquivo especificado da guia atual do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59a75-115">Removes a specified file from the current PowerShell tab.</span></span>

<span data-ttu-id="59a75-116">**File** – cadeia de caracteres, o arquivo ISEFile que você deseja remover da coleção.</span><span class="sxs-lookup"><span data-stu-id="59a75-116">**File** - String The ISEFile file that you want to remove from the collection.</span></span> <span data-ttu-id="59a75-117">Se o arquivo não tiver sido salvo, esse método disparará uma exceção.</span><span class="sxs-lookup"><span data-stu-id="59a75-117">If the file has not been saved, this method throws an exception.</span></span> <span data-ttu-id="59a75-118">Use o parâmetro de comutador **Force** para forçar a remoção de um arquivo que não foi salvo.</span><span class="sxs-lookup"><span data-stu-id="59a75-118">Use the **Force** switch parameter to force the removal of an unsaved file.</span></span>

<span data-ttu-id="59a75-119">**\[Force\]** – Booliano opcional, se definido como `$true`, concederá permissão para remover o arquivo mesmo se ele não tiver sido salvo após o último uso.</span><span class="sxs-lookup"><span data-stu-id="59a75-119">**\[Force\]** - optional Boolean If set to `$true`, grants permission to remove the file even if it has not been saved after last use.</span></span> <span data-ttu-id="59a75-120">O padrão é `$false`.</span><span class="sxs-lookup"><span data-stu-id="59a75-120">The default is `$false`.</span></span>

```powershell
# Removes the first opened file from the file collection associated with the current PowerShell tab.
# If the file has not yet been saved, then an exception is generated.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile)

# Removes the first opened file from the file collection associated with the current PowerShell tab, even if it has not been saved.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile, $true)
```

### <a name="setselectedfile-selectedfile-"></a><span data-ttu-id="59a75-121">SetSelectedFile\( selectedFile \)</span><span class="sxs-lookup"><span data-stu-id="59a75-121">SetSelectedFile\( selectedFile \)</span></span>

<span data-ttu-id="59a75-122">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="59a75-122">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="59a75-123">Escolhe o arquivo especificado pelo parâmetro **SelectedFile**.</span><span class="sxs-lookup"><span data-stu-id="59a75-123">Selects the file that is specified by the **SelectedFile** parameter.</span></span>

<span data-ttu-id="59a75-124">**SelectedFile** – Microsoft.PowerShell.Host.ISE.ISEFile, o arquivo ISEFile que você quer escolher.</span><span class="sxs-lookup"><span data-stu-id="59a75-124">**SelectedFile** - Microsoft.PowerShell.Host.ISE.ISEFile The ISEFile file that you want to select.</span></span>

```powershell
# Selects the specified file.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.SetSelectedFile($firstfile)
```

## <a name="see-also"></a><span data-ttu-id="59a75-125">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="59a75-125">See Also</span></span>

- [<span data-ttu-id="59a75-126">O objeto ISEFile</span><span class="sxs-lookup"><span data-stu-id="59a75-126">The ISEFile Object</span></span>](The-ISEFile-Object.md)
- [<span data-ttu-id="59a75-127">Objetivo do modelo de objeto de script do ISE do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="59a75-127">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="59a75-128">A hierarquia de modelo de objeto do ISE</span><span class="sxs-lookup"><span data-stu-id="59a75-128">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
