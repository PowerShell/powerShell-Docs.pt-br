---
external help file: Microsoft.PowerShell.Commands.Utility.dll-Help.xml
keywords: powershell, cmdlet
Locale: en-US
Module Name: Microsoft.PowerShell.Utility
ms.date: 11/01/2020
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/get-culture?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Get-Culture
ms.openlocfilehash: 214bdd9296dbdbec166e30ba1da0b7976a664ec8
ms.sourcegitcommit: fcf7bd222f5ee3fdbe21ffddcae47050cffe7e42
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93239927"
---
# Get-Culture

## SINOPSE
Obtém a cultura atual definida no sistema operacional.

## SYNTAX

```
Get-Culture [<CommonParameters>]
```

## DESCRIPTION

O `Get-Culture` cmdlet obtém informações sobre as configurações de cultura atuais. Isso inclui informações sobre as configurações de idioma atuais no sistema, como o layout do teclado e o formato de exibição de itens como números, moeda e datas.

Você também pode usar o `Get-UICulture` cmdlet, que obtém a cultura da interface do usuário atual no sistema e o cmdlet [set-Culture](/powershell/module/international/set-culture) no módulo internacional. A cultura da interface do usuário determina quais cadeias de caracteres de texto serão usadas para elementos de interface do usuário, como menus e mensagens.

## EXEMPLOS

### Exemplo 1: obter configurações de cultura

```powershell
Get-Culture
```

```Output
LCID             Name             DisplayName
----             ----             -----------
1033             en-US            English (United States)
```

Este comando exibe informações sobre as configurações regionais do computador.

### Exemplo 2: Formatar as propriedades de um objeto de cultura

```powershell
PS C:\> $C = Get-Culture
PS C:\> $C | Format-List -Property *
Parent                         : en
LCID                           : 1033
KeyboardLayoutId               : 1033
Name                           : en-US
IetfLanguageTag                : en-US
DisplayName                    : English (United States)
NativeName                     : English (United States)
EnglishName                    : English (United States)
TwoLetterISOLanguageName       : en
ThreeLetterISOLanguageName     : eng
ThreeLetterWindowsLanguageName : ENU
CompareInfo                    : CompareInfo - 1033
TextInfo                       : TextInfo - 1033
IsNeutralCulture               : False
CultureTypes                   : SpecificCultures, InstalledWin32Cultures, FrameworkCultures
NumberFormat                   : System.Globalization.NumberFormatInfo
DateTimeFormat                 : System.Globalization.DateTimeFormatInfo
Calendar                       : System.Globalization.GregorianCalendar
OptionalCalendars              : {System.Globalization.GregorianCalendar, System.Globalization.GregorianCalendar}
UseUserOverride                : True
IsReadOnly                     : False

PS C:\> $C.Calendar
MinSupportedDateTime : 1/1/0001 12:00:00 AM
MaxSupportedDateTime : 12/31/9999 11:59:59 PM
AlgorithmType        : SolarCalendar
CalendarType         : Localized
Eras                 : {1}
TwoDigitYearMax      : 2029
IsReadOnly           : False

PS C:\> $C.DateTimeFormat
AMDesignator                     : AM
Calendar                         : System.Globalization.GregorianCalendar
DateSeparator                    : /
FirstDayOfWeek                   : Sunday
CalendarWeekRule                 : FirstDay
FullDateTimePattern              : dddd, MMMM dd, yyyy h:mm:ss tt
LongDatePattern                  : dddd, MMMM dd, yyyy
LongTimePattern                  : h:mm:ss tt
MonthDayPattern                  : MMMM dd
PMDesignator                     : PM
RFC1123Pattern                   : ddd, dd MMM yyyy HH':'mm':'ss 'GMT'
ShortDatePattern                 : M/d/yyyy
ShortTimePattern                 : h:mm tt
SortableDateTimePattern          : yyyy'-'MM'-'dd'T'HH':'mm':'ss
TimeSeparator                    : :
UniversalSortableDateTimePattern : yyyy'-'MM'-'dd HH':'mm':'ss'Z'
YearMonthPattern                 : MMMM, yyyy
AbbreviatedDayNames              : {Sun, Mon, Tue, Wed...}
ShortestDayNames                 : {Su, Mo, Tu, We...}
DayNames                         : {Sunday, Monday, Tuesday, Wednesday...}
AbbreviatedMonthNames            : {Jan, Feb, Mar, Apr...}
MonthNames                       : {January, February, March, April...}
IsReadOnly                       : False
NativeCalendarName               : Gregorian Calendar
AbbreviatedMonthGenitiveNames    : {Jan, Feb, Mar, Apr...}
MonthGenitiveNames               : {January, February, March, April...}

PS C:\> $C.DateTimeFormat.FirstDayOfWeek
Sunday
```

Este exemplo demonstra a enorme quantidade de dados do objeto de cultura. Ele mostra como exibir as propriedades e subpropriedades do objeto.

O primeiro comando usa o `Get-Culture` cmdlet para obter as configurações de cultura atuais no computador.
Ele armazena o objeto de cultura resultante na `$C` variável.

O segundo comando exibe todas as propriedades do objeto de cultura. Ele usa um operador de pipeline ( `|` ) para enviar o objeto de cultura `$C` para o `Format-List` cmdlet. Ele usa o parâmetro **Property** para exibir todas as `*` Propriedades () do objeto. Esse comando pode ser abreviado como `$c | fl *` .

Os comandos restantes exploram as propriedades do objeto cultura usando a notação de ponto para exibir os valores das propriedades do objeto. Você pode usar essa notação para exibir o valor de qualquer propriedade do objeto.

O terceiro comando usa a notação de ponto para exibir o valor da propriedade **Calendar** do objeto Culture.

O quarto comando usa a notação de ponto para exibir o valor da propriedade **DataTimeFormat** do objeto Culture.

Muitas propriedades de objeto têm propriedades. O quinto comando usa a notação de ponto para exibir o valor da propriedade **FirstDayOfWeek** da propriedade **DateTimeFormat** .

## PARAMETERS

### CommonParameters

Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable. Para obter mais informações, confira [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## ENTRADAS

### Nenhum

Não é possível redirecionar a entrada para este cmdlet.

## SAÍDAS

### System. Globalization. CultureInfo

`Get-Culture` Retorna um objeto que representa a cultura atual.

## OBSERVAÇÕES

Você também pode usar as `$PsCulture` `$PsUICulture` variáveis e. A `$PsCulture` variável armazena o nome da cultura atual e a `$PsUICulture` variável armazena o nome da cultura da interface do usuário atual.

## LINKS RELACIONADOS

[Set-Culture](/powershell/module/international/set-culture)

[Get-UICulture](Get-UICulture.md)
