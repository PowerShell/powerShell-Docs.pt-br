---
ms.date: 2017-06-05T00:00:00.000Z
keywords: PowerShell, cmdlet
title: O objeto ISEFileCollection
ms.assetid: 0f86a427-ea38-4bce-85f8-06c98d30d508
ms.openlocfilehash: 284891c9812a22bb1759678074dc7f967f324c0b
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="the-isefilecollection-object"></a>O objeto ISEFileCollection
  O objeto **ISEFileCollection** é uma coleção de objetos **ISEFile**. Um exemplo é a coleção $psISE.CurrentPowerShellTab.Files.

## <a name="methods"></a>Métodos

### <a name="add-fullpath-"></a>Add\( \[fullPath\] \)
  Suportado no Windows PowerShell ISE 2.0 e posteriores. 

 Cria e retorna um novo arquivo sem título e o adiciona à coleção. A propriedade **IsUntitled** do arquivo recém-criado é **$true**.

 **\[fullPath\]** – cadeia de caracteres opcional, o caminho totalmente especificado do arquivo. Uma exceção será gerada se você incluir o parâmetro **fullPath** e um caminho relativo ou se você usar um nome de arquivo em vez do caminho completo.

```
# Adds a new untitled file to the collection of files in the current PowerShell tab.
$newFile = $psISE.CurrentPowerShellTab.Files.Add()

# Adds a file specified by its full path to the collection of files in the current PowerShell tab.
$psISE.CurrentPowerShellTab.Files.Add("$pshome\Examples\profile.ps1")

```

### <a name="remove-file-force-"></a>Remove\( File, \[Force\] \)
  Suportado no Windows PowerShell ISE 2.0 e posteriores. 

 Remove um arquivo especificado da guia atual do PowerShell.

 **File** – cadeia de caracteres, o arquivo ISEFile que você deseja remover da coleção. Se o arquivo não tiver sido salvo, esse método disparará uma exceção. Use o parâmetro de comutador **Force** para forçar a remoção de um arquivo que não foi salvo.

 **\[Force\]** – booliano opcional, se definido como **$true**, concederá permissão para remover o arquivo mesmo se ele não tiver sido salvo após o último uso. O padrão é **$false**.

```
# Removes the first opened file from the file collection associated with the current PowerShell tab.
# If the file has not yet been saved, then an exception is generated.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile)

# Removes the first opened file from the file collection associated with the current PowerShell tab, even if it has not been saved.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile, $true)
```

### <a name="setselectedfile-selectedfile-"></a>SetSelectedFile\( selectedFile \)
  Suportado no Windows PowerShell ISE 2.0 e posteriores. 

 Seleciona o arquivo especificado pelo parâmetro **selectedFile**.

 **selectedFile** – Microsoft.PowerShell.Host.ISE.ISEFile, o arquivo ISEFile que você quer selecionar.

```

# Selects the specified file.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.SetSelectedFile($firstfile)

```

## <a name="see-also"></a>Consulte Também
- [O objeto ISEFile](The-ISEFile-Object.md) 
- [O modelo de objeto de script do ISE do Windows PowerShell](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [Referência de modelo de objeto do ISE do Windows PowerShell](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [A hierarquia de modelo de objeto do ISE](The-ISE-Object-Model-Hierarchy.md)

  