---
external help file: Microsoft.PowerShell.Commands.Utility.dll-Help.xml
keywords: powershell, cmdlet
Locale: en-US
Module Name: Microsoft.PowerShell.Utility
ms.date: 08/23/2019
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/show-markdown?view=powershell-7.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Show-Markdown
ms.openlocfilehash: f4740bca33bd70d4d8eca51ed45ba6204b5d2acb
ms.sourcegitcommit: 9b28fb9a3d72655bb63f62af18b3a5af6a05cd3f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/07/2020
ms.locfileid: "93193258"
---
# Show-Markdown

## SINOPSE
Mostra um arquivo ou uma cadeia de caracteres de redução no console de forma amigável usando sequências de escape VT100 ou em um navegador usando HTML.

## SYNTAX

### Caminho (padrão)

```
Show-Markdown [-Path] <String[]> [-UseBrowser] [<CommonParameters>]
```

### InputObject

```
Show-Markdown -InputObject <PSObject> [-UseBrowser] [<CommonParameters>]
```

### LiteralPath

```
Show-Markdown -LiteralPath <String[]> [-UseBrowser] [<CommonParameters>]
```

## DESCRIPTION

O `Show-Markdown` cmdlet é usado para renderizar a redução em um formato legível por humanos, seja em um terminal ou em um navegador.

`Show-Markdown` pode retornar uma cadeia de caracteres que inclui as sequências de escape VT100 que o terminal renderiza (se ele der suporte a sequências de escape VT100). Isso é usado principalmente para exibir arquivos de redução em um terminal. Você também pode obter essa cadeia de caracteres por meio da `ConvertFrom-Markdown` especificação do parâmetro **AsVT100EncodedString** .

`Show-Markdown` também tem a capacidade de abrir um navegador e mostrar uma versão renderizada da redução. Ele renderiza a redução ao transformá-lo em HTML e abrir o arquivo HTML no navegador padrão.

Você pode alterar como os `Show-Markdown` renderizações são reparados em um terminal usando o `Set-MarkdownOption` .

Esse cmdlet foi introduzido no PowerShell 6,1.

## EXEMPLOS

### Exemplo 1: exemplo simples especificando um caminho

```powershell
Show-Markdown -Path ./README.md
```

### Exemplo 2: exemplo simples especificando uma cadeia de caracteres

```powershell
@"
# Show-Markdown

## Markdown

You can now interact with Markdown via PowerShell!

*stars*
__underlines__
"@ | Show-Markdown
```

### Exemplo 2: abrindo a redução em um navegador

```powershell
Show-Markdown -Path ./README.md -UseBrowser
```

## PARAMETERS

### -InputObject

Uma cadeia de caracteres de redução que será mostrada no terminal. Se você não passar um formato com suporte, o `Show-Markdown` emitirá um erro.

```yaml
Type: System.Management.Automation.PSObject
Parameter Sets: InputObject
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -LiteralPath

Especifica o caminho para um arquivo de redução. Ao contrário do parâmetro Path, o valor de LiteralPath é usado exatamente como digitado. Nenhum caractere é interpretado como caractere curinga. Se o caminho incluir caracteres de escape, coloque-o entre aspas simples. Aspas simples instruem o PowerShell a não interpretar nenhum caractere como sequências de escape.

```yaml
Type: System.String[]
Parameter Sets: LiteralPath
Aliases: PSPath, LP

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Path

Especifica o caminho para um arquivo de redução a ser renderizado.

```yaml
Type: System.String[]
Parameter Sets: Path
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: True
```

### -UseBrowser

Compila a entrada de redução como HTML e a abre no navegador padrão.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters

Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable. Para obter mais informações, confira [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## ENTRADAS

### System. Management. Automation. PSObject

### System.String[]

## SAÍDAS

### System.String

## OBSERVAÇÕES

## LINKS RELACIONADOS

[ConvertFrom-Markdown](ConvertFrom-Markdown.md)

