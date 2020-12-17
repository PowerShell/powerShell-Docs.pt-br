---
ms.date: 12/31/2019
title: O objeto ISEFile
description: Um objeto ISEFile representa um arquivo no Windows PowerShell ISE.
ms.openlocfilehash: b5ea70219787f254fe85d728518cbc4746c00250
ms.sourcegitcommit: 2c311274ce721cd1072dcf2dc077226789e21868
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2020
ms.locfileid: "94391486"
---
# <a name="the-isefile-object"></a>O objeto ISEFile

Um objeto **ISEFile** representa um arquivo no ISE (Ambiente de Script Integrado) do Windows PowerShell. É uma instância da classe **Microsoft.PowerShell.Host.ISE.ISEFile**. Este tópico lista os métodos e as propriedades do membro. O `$psISE.CurrentFile` e os arquivos da coleção de arquivos em uma guia do PowerShell são instâncias da classe \*\***Microsoft.PowerShell.Host.ISE.ISEFile**.

## <a name="methods"></a>Métodos

### <a name="save-saveencoding-"></a>Save\( \[saveEncoding\] \)

Suportado no Windows PowerShell ISE 2.0 e posteriores.

Salva o arquivo no disco.

`[saveEncoding]` – [System.Text.Encoding](/dotnet/api/system.text.encoding) opcional Um parâmetro de codificação de caracteres opcional a ser usado no arquivo salvo. O valor padrão é **UTF8**.

### <a name="exceptions"></a>Exceções

- **System.IO.IOException**: não foi possível salvar o arquivo.

```powershell
# Save the file using the default encoding (UTF8)
$psISE.CurrentFile.Save()

# Save the file as ASCII.
$psISE.CurrentFile.Save([System.Text.Encoding]::ASCII)

# Gets the current encoding.
$myfile = $psISE.CurrentFile
$myfile.Encoding
```

### <a name="saveasfilename-saveencoding"></a>SaveAs\(filename, \[saveEncoding\]\)

Suportado no Windows PowerShell ISE 2.0 e posteriores.

Salva o arquivo com o nome de arquivo e codificação especificados.

**filename** – cadeia de caracteres, o nome a ser usado para salvar o arquivo.

`[saveEncoding]` – [System.Text.Encoding](/dotnet/api/system.text.encoding) opcional Um parâmetro de codificação de caracteres opcional a ser usado no arquivo salvo. O valor padrão é **UTF8**.

### <a name="exceptions"></a>Exceções

- **System.ArgumentNullException**: o parâmetro **filename** é nulo.
- **System.ArgumentException**: o parâmetro **filename** está vazio.
- **System.IO.IOException**: não foi possível salvar o arquivo.

```powershell
# Save the file with a full path and name.
$fullpath = "c:\temp\newname.txt"
$psISE.CurrentFile.SaveAs($fullPath)
# Save the file with a full path and name and explicitly as UTF8.
$psISE.CurrentFile.SaveAs($fullPath, [System.Text.Encoding]::UTF8)
```

## <a name="properties"></a>Propriedades

### <a name="displayname"></a>DisplayName

Suportado no Windows PowerShell ISE 2.0 e posteriores.

A propriedade somente leitura que obtém a cadeia que contém o nome de exibição deste arquivo. O nome é mostrado na guia **Arquivo** na parte superior do editor. A presença de um asterisco `(*)` ao final do nome indica que o arquivo tem alterações que não foram salvas.

```powershell
# Shows the display name of the file.
$psISE.CurrentFile.DisplayName
```

### <a name="editor"></a>Editor

Suportado no Windows PowerShell ISE 2.0 e posteriores.

A propriedade somente leitura que obtém o [objeto editor](The-ISEEditor-Object.md) usado para o arquivo especificado.

```powershell
# Gets the editor and the text.
$psISE.CurrentFile.Editor.Text
```

### <a name="encoding"></a>Codificação

Suportado no Windows PowerShell ISE 2.0 e posteriores.

A propriedade somente leitura que obtém a codificação original do arquivo. Este é um objeto **System.Text.Encoding**.

```powershell
# Shows the encoding for the file.
$psISE.CurrentFile.Encoding
```

### <a name="fullpath"></a>FullPath

Suportado no Windows PowerShell ISE 2.0 e posteriores.

A propriedade somente leitura que obtém a cadeia de caracteres que especifica o caminho completo do arquivo aberto.

```powershell
# Shows the full path for the file.
$psISE.CurrentFile.FullPath
```

### <a name="issaved"></a>IsSaved

Suportado no Windows PowerShell ISE 2.0 e posteriores.

A propriedade booliana somente leitura que retornará `$true` se o arquivo tiver sido salvo depois de ter sido modificado pela última vez.

```powershell
# Determines whether the file has been saved since it was last modified.
$myfile = $psISE.CurrentFile
$myfile.IsSaved
```

### <a name="isuntitled"></a>IsUntitled

Suportado no Windows PowerShell ISE 2.0 e posteriores.

A propriedade somente leitura que retornará `$true` se o arquivo nunca tiver recebido um título.

```powershell
# Determines whether the file has never been given a title.
$psISE.CurrentFile.IsUntitled
$psISE.CurrentFile.SaveAs("temp.txt")
$psISE.CurrentFile.IsUntitled
```

## <a name="see-also"></a>Consulte Também

- [O ISEFileCollectionObject](The-ISEFileCollection-Object.md)
- [Objetivo do modelo de objeto de script do ISE do Windows PowerShell](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [A hierarquia de modelo de objeto do ISE](The-ISE-Object-Model-Hierarchy.md)
