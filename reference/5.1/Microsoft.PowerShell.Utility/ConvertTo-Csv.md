---
external help file: Microsoft.PowerShell.Commands.Utility.dll-Help.xml
Locale: en-US
Module Name: Microsoft.PowerShell.Utility
ms.date: 1/7/2019
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/convertto-csv?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: ConvertTo-Csv
ms.openlocfilehash: be590368539f396f0aac694e9565674393543f2c
ms.sourcegitcommit: 560a9f3c3148acab4655e91e8b07745ab74d5d26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/09/2020
ms.locfileid: "96913195"
---
# ConvertTo-Csv

## SINOPSE
Converte objetos .NET em uma série de cadeias de caracteres CSV (valores separados por vírgula).

## SYNTAX

### Delimitador (padrão)

```
ConvertTo-Csv [-InputObject] <psobject> [[-Delimiter] <char>] [-NoTypeInformation]
 [<CommonParameters>]
```

### parâmetro

```
ConvertTo-Csv [-InputObject] <psobject> [-UseCulture] [-NoTypeInformation] [<CommonParameters>]
```

## DESCRIPTION

O `ConvertTo-CSV` cmdlet retorna uma série de cadeias de caracteres CSV (valores separados por vírgula) que representam os objetos que você envia. Você pode usar o `ConvertFrom-Csv` cmdlet para recriar objetos a partir de cadeias de caracteres CSV. Os objetos convertidos de CSV são valores de cadeia de caracteres dos objetos originais que contêm valores de propriedade e nenhum método.

Você pode usar o `Export-Csv` cmdlet para converter objetos em cadeias de caracteres CSV. `Export-CSV` é semelhante a `ConvertTo-CSV` , exceto pelo fato de salvar as cadeias de caracteres CSV em um arquivo.

O `ConvertTo-CSV` cmdlet tem parâmetros para especificar um delimitador diferente de uma vírgula ou usar a cultura atual como o delimitador.

## EXEMPLOS

### Exemplo 1: converter um objeto em CSV

Este exemplo converte um objeto de **processo** em uma cadeia de caracteres CSV.

```powershell
Get-Process -Name 'PowerShell' | ConvertTo-Csv -NoTypeInformation
```

```Output
"Name","SI","Handles","VM","WS","PM","NPM","Path","Company","CPU","FileVersion", ...
"powershell","11","691","2204036739072","175943680","132665344","33312", ...
```

O `Get-Process` cmdlet obtém o objeto de **processo** e usa o parâmetro **Name** para especificar o processo do PowerShell. O objeto de processo é enviado pelo pipeline para o `ConvertTo-CSV` cmdlet. O `ConvertTo-CSV` cmdlet converte o objeto em cadeias de caracteres CSV. O parâmetro **NoTypeInformation** remove o cabeçalho de informações **#TYPE** da saída CSV.

### Exemplo 2: converter um objeto DateTime em CSV

Este exemplo converte um objeto **DateTime** em uma cadeia de caracteres CSV.

```powershell
$Date = Get-Date
ConvertTo-Csv -InputObject $Date -Delimiter ';' -NoTypeInformation
```

```Output
"DisplayHint";"DateTime";"Date";"Day";"DayOfWeek";"DayOfYear";"Hour";"Kind";"Millisecond";"Minute";"Month";"Second";"Ticks";"TimeOfDay";"Year"
"DateTime";"Friday, January 4, 2019 14:40:51";"1/4/2019 00:00:00";"4";"Friday";"4";"14";"Local";"711";"40";"1";"51";"636822096517114991";"14:40:51.7114991";"2019"
```

O `Get-Date` cmdlet obtém o objeto **DateTime** e o salva na `$Date` variável. O `ConvertTo-Csv` cmdlet converte o objeto **DateTime** em cadeias de caracteres. O parâmetro **InputObject** usa o objeto **DateTime** armazenado na `$Date` variável. O parâmetro **delimitador** especifica um ponto e vírgula para separar os valores da cadeia de caracteres. O parâmetro **NoTypeInformation** remove o cabeçalho de informações **#TYPE** da saída CSV.

### Exemplo 3: converter o log de eventos do PowerShell em CSV

Este exemplo converte o log de eventos do Windows para o PowerShell em uma série de cadeias de caracteres CSV.

```powershell
(Get-Culture).TextInfo.ListSeparator
Get-WinEvent -LogName 'Windows PowerShell' | ConvertTo-Csv -UseCulture -NoTypeInformation
```

```Output
,
"Message","Id","Version","Qualifiers","Level","Task","Opcode","Keywords","RecordId", ...
"Error Message = System error","403",,"0","4","4",,"36028797018963968","46891","PowerShell", ...
```

O `Get-Culture` cmdlet usa as propriedades aninhadas **TextInfo** e **ListSeparator** e exibe o separador de lista padrão da cultura atual. O `Get-WinEvent` cmdlet obtém os objetos de log de eventos e usa o parâmetro **LogName** para especificar o nome do arquivo de log. Os objetos de log de eventos são enviados pelo pipeline para o `ConvertTo-Csv` cmdlet. O `ConvertTo-Csv` cmdlet converte os objetos de log de eventos em uma série de cadeias de caracteres CSV. O parâmetro **UseCulture** usa o separador de lista padrão da cultura atual como o delimitador. O parâmetro **NoTypeInformation** remove o cabeçalho de informações **#TYPE** da saída CSV.

## PARAMETERS

### -Delimitador

Especifica o delimitador para separar os valores de propriedade em cadeias de caracteres CSV. O padrão é uma vírgula ( `,` ). Insira um caractere, como dois-pontos ( `:` ). Para especificar um ponto e vírgula ( `;` ), coloque-o entre aspas simples.

```yaml
Type: System.Char
Parameter Sets: Delimiter
Aliases:

Required: False
Position: 1
Default value: comma (,)
Accept pipeline input: False
Accept wildcard characters: False
```

### -InputObject

Especifica os objetos que são convertidos em cadeias de caracteres CSV. Insira uma variável que contém os objetos ou digite um comando ou uma expressão que obtém os objetos. Você também pode canalizar objetos para `ConvertTo-CSV` .

```yaml
Type: System.Management.Automation.PSObject
Parameter Sets: (All)
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName, ByValue)
Accept wildcard characters: False
```

### -NoTypeInformation

Remove o cabeçalho de informações **#TYPE** da saída. Esse parâmetro se tornou o padrão no PowerShell 6,0 e está incluído para compatibilidade com versões anteriores.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: NTI

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -UseCulture

Usa o separador de lista para a cultura atual como o delimitador de item. Para localizar o separador de lista para uma cultura, use o seguinte comando: `(Get-Culture).TextInfo.ListSeparator` .

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: UseCulture
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters

Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable. Para obter mais informações, confira [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## ENTRADAS

### System. Management. Automation. PSObject

É possível canalizar qualquer objeto que tenha um adaptador de sistema de tipo estendido (ETS) para o `ConvertTo-CSV` .

## SAÍDAS

### System.String

A saída CSV é retornada como uma coleção de cadeias de caracteres.

## OBSERVAÇÕES

No formato CSV, cada objeto é representado por uma lista separada por vírgulas de seu valor de propriedade. Os valores de propriedade são convertidos em cadeias de caracteres usando o método **ToString ()** do objeto. As cadeias de caracteres são representadas pelo nome do valor da propriedade. `ConvertTo-CSV` não exporta os métodos do objeto.

As cadeias de caracteres CSV são saídas da seguinte maneira:

- Por padrão, a primeira cadeia de caracteres contém o cabeçalho de informações **#TYPE** seguido pelo nome totalmente qualificado do tipo de objeto. Por exemplo, **#TYPE System. Diagnostics. Process**.
- Se **NoTypeInformation** for usado, a primeira cadeia de caracteres incluirá os cabeçalhos de coluna. Os cabeçalhos contêm os nomes de Propriedade do primeiro objeto como uma lista separada por vírgulas.
- As cadeias de caracteres restantes contêm listas separadas por vírgulas dos valores de propriedade de cada objeto.

Quando você envia vários objetos ao `ConvertTo-CSV` , `ConvertTo-CSV` o ordena as cadeias de caracteres com base nas propriedades do primeiro objeto que você envia. Se os objetos restantes não tiverem uma das propriedades especificadas, o valor da propriedade desse objeto será nulo, conforme representado por duas vírgulas consecutivas. Se os objetos restantes têm propriedades adicionais, esses valores das propriedades serão ignorados.

## LINKS RELACIONADOS

[ConvertFrom-Csv](ConvertFrom-Csv.md)

[Export-CSV](Export-Csv.md)

[Import-Csv](Import-Csv.md)
