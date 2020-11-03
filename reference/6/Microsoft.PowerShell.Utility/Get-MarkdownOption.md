---
external help file: Microsoft.PowerShell.Commands.Utility.dll-Help.xml
Module Name: Microsoft.PowerShell.Utility
online version: https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Utility/Get-MarkdownOption?view=powershell-6&WT.mc_id=ps-gethelp
ms.date: 01/30/2020
schema: 2.0.0
ms.openlocfilehash: df141d99080a0d893d72691f6032684097dfd966
ms.sourcegitcommit: bc9a4904c2b1561386d748fc9ac242699d2f1694
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/04/2020
ms.locfileid: "93192576"
---
# Get-MarkdownOption

## SINOPSE
Retorna as cores e os estilos atuais usados para renderizar o conteúdo de redução no console.

## SYNTAX

```
Get-MarkdownOption [<CommonParameters>]
```

## DESCRIPTION

Retorna as cores e os estilos atuais usados para renderizar o conteúdo de redução no console. As cadeias de caracteres exibidas na saída desse cmdlet contêm os códigos de escape ANSI usados para alterar a cor e o estilo do texto de redução que está sendo renderizado.

Para obter mais informações sobre a redução, consulte o site do [CommonMark](https://commonmark.org/) .

## EXEMPLOS

### Exemplo 1-obter as cores e o estilo atuais

```powershell
Get-MarkdownOption
```

```Output
Header1         : [7m
Header2         : [4;93m
Header3         : [4;94m
Header4         : [4;95m
Header5         : [4;96m
Header6         : [4;97m
Code            : [48;2;155;155;155;38;2;30;30;30m
Link            : [4;38;5;117m
Image           : [33m
EmphasisBold    : [1m
EmphasisItalics : [36m
```

> [!NOTE]
> Os valores de cadeia de caracteres mostrados na saída são os caracteres que seguem o caractere de **escape** ( `[char]0x1B` ) para a sequência de escape ANSI. Para obter mais informações sobre os códigos de escape ANSI funcionam, consulte [ANSI_escape_code](https://en.wikipedia.org/wiki/ANSI_escape_code).

## PARAMETERS

### CommonParameters

Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable. Para obter mais informações, confira [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## ENTRADAS

### Nenhum

## SAÍDAS

### Microsoft. PowerShell. MarkdownRender. PSMarkdownOptionInfo

## OBSERVAÇÕES

## LINKS RELACIONADOS

[Set-MarkdownOption](Set-MarkdownOption.md)

[ConvertFrom-Markdown](ConvertFrom-Markdown.md)

[Show-Markdown](Show-Markdown.md)

[ANSI_escape_code](https://en.wikipedia.org/wiki/ANSI_escape_code)

[CommonMark](https://commonmark.org/)