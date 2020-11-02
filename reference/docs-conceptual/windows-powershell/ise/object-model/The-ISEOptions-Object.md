---
ms.date: 12/31/2019
title: O objeto ISEOptions
description: O objeto ISEOptions representa várias configurações para o ISE do Windows PowerShell.
ms.openlocfilehash: 4f790550796f40c7a2d4882cc0444fa7a55eeee9
ms.sourcegitcommit: 488a940c7c828820b36a6ba56c119f64614afc29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92661020"
---
# <a name="the-iseoptions-object"></a>O objeto ISEOptions

O objeto **ISEOptions** representa várias configurações para o ISE do Windows PowerShell. Ele é uma instância da classe **Microsoft.PowerShell.Host.ISE.ISEOptions** .

O objeto **ISEOptions** fornece os seguintes métodos e propriedades.

## <a name="methods"></a>Métodos

### <a name="restoredefaultconsoletokencolors"></a>RestoreDefaultConsoleTokenColors\(\)

Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.

Restaura os valores padrão das cores do token no painel de Console.

```powershell
# Changes the color of the commands in the Console pane to red and then restores it to its default value.
$psISE.Options.ConsoleTokenColors["Command"] = 'red'
$psISE.Options.RestoreDefaultConsoleTokenColors()
```

### <a name="restoredefaults"></a>RestoreDefaults\(\)

Suportado no Windows PowerShell ISE 2.0 e posteriores.

Restaura os valores padrão das cores de todas as configurações de opções no painel de Console. Ele também redefine o comportamento de várias mensagens de aviso que fornecem a caixa de seleção padrão para impedir que a mensagem seja mostrada novamente.

```powershell
# Changes the background color in the Console pane and then restores it to its default value.
$psISE.Options.ConsolePaneBackgroundColor = 'orange'
$psISE.Options.RestoreDefaults()
```

### <a name="restoredefaulttokencolors"></a>RestoreDefaultTokenColors\(\)

Suportado no Windows PowerShell ISE 2.0 e posteriores.

Restaura os valores padrão das cores do token no painel de script.

```powershell
# Changes the color of the comments in the Script pane to red and then restores it to its default value.
$psISE.Options.TokenColors["Comment"] = 'red'
$psISE.Options.RestoreDefaultTokenColors()
```

### <a name="restoredefaultxmltokencolors"></a>RestoreDefaultXmlTokenColors\(\)

Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.

Restaura os valores padrão das cores do token para elementos XML exibidos no ISE do Windows PowerShell. Consulte também [XmlTokenColors](#xmltokencolors).

```powershell
# Changes the color of the comments in XML data to red and then restores it to its default value.
$psISE.Options.XmlTokenColors["Comment"] = 'red'
$psISE.Options.RestoreDefaultXmlTokenColors()
```

## <a name="properties"></a>Propriedades

### <a name="autosaveminuteinterval"></a>AutoSaveMinuteInterval

Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.

Especifica o número de minutos entre as operações de salvamento automático de seus arquivos pelo ISE do Windows PowerShell. O valor padrão é 2 minutos. O valor é um inteiro.

```powershell
# Changes the number of minutes between automatic save operations to every 3 minutes.
$psISE.Options.AutoSaveMinuteInterval = 3
```

### <a name="commandpanebackgroundcolor"></a>CommandPaneBackgroundColor

Esse recurso está presente no ISE do Windows PowerShell 2.0, mas foi removido ou renomeado em versões posteriores do ISE. Para versões posteriores, consulte [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).

Especifica a cor da tela de fundo para o painel de comando. É uma instância da classe **System.Windows.Media.Color** .

```powershell
# Changes the background color of the Command pane to orange.
$psISE.Options.CommandPaneBackgroundColor = 'orange'
```

### <a name="commandpaneup"></a>CommandPaneUp

Esse recurso está presente no ISE do Windows PowerShell 2.0, mas foi removido ou renomeado em versões posteriores do ISE.

Especifica se o painel de comando está localizado acima do painel de saída.

```powershell
# Moves the Command pane to the top of the screen.
$psISE.Options.CommandPaneUp  = $true
```

### <a name="consolepanebackgroundcolor"></a>ConsolePaneBackgroundColor

Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.

Especifica a cor da tela de fundo do painel de Console. É uma instância da classe **System.Windows.Media.Color** .

```powershell
# Changes the background color of the Console pane to red.
$psISE.Options.ConsolePaneBackgroundColor = 'red'
```

### <a name="consolepaneforegroundcolor"></a>ConsolePaneForegroundColor

Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.

Especifica a cor de primeiro plano do texto no painel de Console.

```powershell
# Changes the foreground color of the text in the Console pane to yellow.
$psISE.Options.ConsolePaneForegroundColor  = 'yellow'
```

### <a name="consolepanetextbackgroundcolor"></a>ConsolePaneTextBackgroundColor

Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.

Especifica a cor da tela de fundo do texto no painel de Console.

```powershell
# Changes the background color of the Console pane text to pink.
$psISE.Options.ConsolePaneTextBackgroundColor = 'pink'
```

### <a name="consoletokencolors"></a>ConsoleTokenColors

Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.

Especifica as cores dos tokens do IntelliSense no painel de Console de ISE do Windows PowerShell. Essa propriedade é um objeto de dicionário que contém pares de nome/valor de tipos de token e cores para o painel de Console. Para alterar as cores dos tokens do IntelliSense no painel de Script, consulte [TokenColors](#tokencolors).
Para redefinir as cores aos valores padrão, consulte [RestoreDefaultConsoleTokenColors](#restoredefaultconsoletokencolors).
As cores do token podem ser definidas para o seguinte: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable.

```powershell
# Sets the color of commands to green.
$psISE.Options.ConsoleTokenColors["Command"] = 'green'
# Sets the color of keywords to magenta.
$psISE.Options.ConsoleTokenColors["Keyword"] = 'magenta'
```

### <a name="debugbackgroundcolor"></a>DebugBackgroundColor

Suportado no Windows PowerShell ISE 2.0 e posteriores.

Especifica a cor da tela de fundo para o texto de depuração que aparece no painel de Console. É uma instância da classe **System.Windows.Media.Color** .

```powershell
# Changes the background color for the debug text that appears in the Console pane to blue.
$psISE.Options.DebugBackgroundColor = '#0000FF'
```

### <a name="debugforegroundcolor"></a>DebugForegroundColor

Suportado no Windows PowerShell ISE 2.0 e posteriores.

Especifica a cor de primeiro plano para o texto de depuração que aparece no painel de Console. É uma instância da classe **System.Windows.Media.Color** .

```powershell
# Changes the foreground color for the debug text that appears in the Console pane to yellow.
$psISE.Options.DebugForegroundColor = 'yellow'
```

### <a name="defaultoptions"></a>DefaultOptions

Suportado no Windows PowerShell ISE 2.0 e posteriores.

Uma coleção de propriedades que especificam os valores padrão a serem usados quando os métodos Reset são usados.

```powershell
# Displays the name of the default options. This example is from ISE 4.0.
$psISE.Options.DefaultOptions
```

```Output
SelectedScriptPaneState                   : Top
ShowDefaultSnippets                       : True
ShowToolBar                               : True
ShowOutlining                             : True
ShowLineNumbers                           : True
TokenColors                               : {[Attribute, #FF00BFFF], [Command, #FF0000FF], [CommandArgument, #FF8A2BE2], [CommandParameter, #FF000080]...}
ConsoleTokenColors                        : {[Attribute, #FFB0C4DE], [Command, #FFE0FFFF], [CommandArgument, #FFEE82EE], [CommandParameter, #FFFFE4B5]...}
XmlTokenColors                            : {[Comment, #FF006400], [CommentDelimiter, #FF008000], [ElementName, #FF8B0000], [MarkupExtension, #FFFF8C00]...}
DefaultOptions                            : Microsoft.PowerShell.Host.ISE.ISEOptions
FontSize                                  : 9
Zoom                                      : 100
FontName                                  : Lucida Console
ErrorForegroundColor                      : #FFFF0000
ErrorBackgroundColor                      : #00FFFFFF
WarningForegroundColor                    : #FFFF8C00
WarningBackgroundColor                    : #00FFFFFF
VerboseForegroundColor                    : #FF00FFFF
VerboseBackgroundColor                    : #00FFFFFF
DebugForegroundColor                      : #FF00FFFF
DebugBackgroundColor                      : #00FFFFFF
ConsolePaneBackgroundColor                : #FF012456
ConsolePaneTextBackgroundColor            : #FF012456
ConsolePaneForegroundColor                : #FFF5F5F5
ScriptPaneBackgroundColor                 : #FFFFFFFF
ScriptPaneForegroundColor                 : #FF000000
ShowWarningForDuplicateFiles              : True
ShowWarningBeforeSavingOnRun              : True
UseLocalHelp                              : True
AutoSaveMinuteInterval                    : 2
MruCount                                  : 10
ShowIntellisenseInConsolePane             : True
ShowIntellisenseInScriptPane              : True
UseEnterToSelectInConsolePaneIntellisense : True
UseEnterToSelectInScriptPaneIntellisense  : True
IntellisenseTimeoutInSeconds              : 3
```

### <a name="errorbackgroundcolor"></a>ErrorBackgroundColor

Suportado no Windows PowerShell ISE 2.0 e posteriores.

Especifica a cor da tela de fundo para o texto de erro que aparece no painel de Console. É uma instância da classe **System.Windows.Media.Color** .

```powershell
# Changes the background color for the error text that appears in the Console pane to black.
$psISE.Options.ErrorBackgroundColor = 'black'
```

### <a name="errorforegroundcolor"></a>ErrorForegroundColor

Suportado no Windows PowerShell ISE 2.0 e posteriores.

Especifica a cor de primeiro plano para o texto de erro que aparece no painel de Console. É uma instância da classe **System.Windows.Media.Color** .

```powershell
# Changes the foreground color for the error text that appears in the console pane to green.
$psISE.Options.ErrorForegroundColor = 'green'
```

### <a name="fontname"></a>FontName

Suportado no Windows PowerShell ISE 2.0 e posteriores.

Especifica o nome da fonte atualmente em uso, tanto no painel do Script quanto no painel de Console.

```powershell
# Changes the font used in both panes.
$psISE.Options.FontName = 'Courier New'
```

### <a name="fontsize"></a>FontSize

Suportado no Windows PowerShell ISE 2.0 e posteriores.

Especifica o tamanho da fonte como um inteiro. Ele é usado no painel de Script, no painel de Comando e no painel de Saída. O intervalo de valores válidos é de 8 a 32.

```powershell
# Changes the font size in all panes.
$psISE.Options.FontSize = 20
```

### <a name="intellisensetimeoutinseconds"></a>IntellisenseTimeoutInSeconds

Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.

Especifica o número de segundos que IntelliSense usa para tentar resolver o texto atualmente digitado.
Após esse número de segundos, o IntelliSense expira e permite que você continue digitando. O valor padrão é de 3 segundos. O valor é um inteiro.

```powershell
# Changes the number of seconds for IntelliSense syntax recognition to 5.
$psISE.Options.IntellisenseTimeoutInSeconds = 5
```

### <a name="mrucount"></a>MruCount

Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.

Especifica o número de arquivos abertos recentemente que o ISE do Windows PowerShell acompanha e exibe na parte inferior do menu **Abrir Arquivo** . O valor padrão é 10. O valor é um inteiro.

```powershell
# Changes the number of recently used files that appear at the bottom of the File Open menu to 5.
$psISE.Options.MruCount = 5
```

### <a name="outputpanebackgroundcolor"></a>OutputPaneBackgroundColor

Esse recurso está presente no ISE do Windows PowerShell 2.0, mas foi removido ou renomeado em versões posteriores do ISE. Para versões posteriores, consulte [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).

A propriedade de leitura/gravação que obtém ou define a cor da tela de fundo para o Painel de saída em si. É uma instância da classe **System.Windows.Media.Color** .

```powershell
# Changes the background color of the Output pane to gold.
$psISE.Options.OutputPaneForegroundColor = 'gold'
```

### <a name="outputpanetextforegroundcolor"></a>OutputPaneTextForegroundColor

Esse recurso está presente no ISE do Windows PowerShell 2.0, mas foi removido ou renomeado em versões posteriores do ISE. Para versões posteriores, consulte [ConsolePaneForegroundColor](#consolepaneforegroundcolor).

A propriedade de leitura/gravação que muda a cor do primeiro plano do texto no Painel de saída no ISE do Windows PowerShell 2.0.

```powershell
# Changes the foreground color of the text in the Output Pane to blue.
$psISE.Options.OutputPaneTextForegroundColor  = 'blue'
```

### <a name="outputpanetextbackgroundcolor"></a>OutputPaneTextBackgroundColor

Esse recurso está presente no ISE do Windows PowerShell 2.0, mas foi removido ou renomeado em versões posteriores do ISE. Para versões posteriores, consulte [ConsolePaneTextBackgroundColor](#consolepanetextbackgroundcolor).

A propriedade de leitura/gravação que muda a cor da tela de fundo do texto no painel Saída.

```powershell
# Changes the background color of the Output pane text to pink.
$psISE.Options.OutputPaneTextBackgroundColor = 'pink'
```

### <a name="scriptpanebackgroundcolor"></a>ScriptPaneBackgroundColor

Suportado no Windows PowerShell ISE 2.0 e posteriores.

A propriedade de leitura/gravação que obtém ou define a cor da tela de fundo dos arquivos. É uma instância da classe **System.Windows.Media.Color** .

```powershell
# Sets the color of the script pane background to yellow.
$psISE.Options.ScriptPaneBackgroundColor = 'yellow'
```

### <a name="scriptpaneforegroundcolor"></a>ScriptPaneForegroundColor

Suportado no Windows PowerShell ISE 2.0 e posteriores.

A propriedade de leitura/gravação que obtém ou define a cor de primeiro plano de arquivos de não script no painel Script.
Para definir a cor de primeiro plano dos arquivos de script, use [TokenColors](#tokencolors).

```powershell
# Sets the foreground to color of non-script files in the script pane to green.
$psISE.Options.ScriptPaneBackgroundColor = 'green'
```

### <a name="selectedscriptpanestate"></a>SelectedScriptPaneState

Suportado no Windows PowerShell ISE 2.0 e posteriores.

A propriedade de leitura/gravação que obtém ou define a posição do painel Script no visor. A cadeia de caracteres pode ser "Maximizada", "Na parte superior" ou à "Direita".

```powershell
# Moves the Script Pane to the top.
$psISE.Options.SelectedScriptPaneState = 'Top'
# Moves the Script Pane to the right.
$psISE.Options.SelectedScriptPaneState = 'Right'
# Maximizes the Script Pane
$psISE.Options.SelectedScriptPaneState = 'Maximized'
```

### <a name="showdefaultsnippets"></a>ShowDefaultSnippets

Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.

Especifica se a lista <kbd>CTRL</kbd>+<kbd>J</kbd> de snippets inclui o conjunto inicial incluído no Windows PowerShell. Quando definido como `$false`, somente snippets definidos pelo usuário aparecem na lista <kbd>CTRL</kbd>+<kbd>J</kbd>.
O valor padrão é `$true`.

```powershell
# Hide the default snippets from the CTRL+J list.
$psISE.Options.ShowDefaultSnippets = $false
```

### <a name="showintellisenseinconsolepane"></a>ShowIntellisenseInConsolePane

Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.

Especifica se o IntelliSense oferece sugestões de sintaxe, parâmetro e valor no painel de Console.
O valor padrão é `$true`.

```powershell
# Turn off IntelliSense in the console pane.
$psISE.Options.ShowIntellisenseInConsolePane = $false
```

### <a name="showintellisenseinscriptpane"></a>ShowIntellisenseInScriptPane

Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.

Especifica se o IntelliSense oferece sugestões de sintaxe, parâmetro e valor no painel do Script.
O valor padrão é `$true`.

```powershell
# Turn off IntelliSense in the Script pane.
$psISE.Options.ShowIntellisenseInScriptPane = $false
```

### <a name="showlinenumbers"></a>ShowLineNumbers

Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.

Especifica se o painel de Script exibe os números de linha na margem esquerda. O valor padrão é `$true`.

```powershell
# Turn off line numbers in the Script pane.
$psISE.Options.ShowLineNumbers = $false
```

### <a name="showoutlining"></a>ShowOutlining

Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.

Especifica se o painel de Script exibe colchetes expansíveis e recolhíveis próximos às seções de código na margem esquerda. Quando eles são exibidos, você pode clicar nos ícones de subtração `-` ao lado de um bloco de texto para recolhê-los ou clicar no ícone de adição `+` para expandir um bloco de texto. O valor padrão é `$true`.

```powershell
# Turn off outlining in the Script pane.
$psISE.Options.ShowOutlining = $false
```

### <a name="showtoolbar"></a>ShowToolBar

Suportado no Windows PowerShell ISE 2.0 e posteriores.

Especifica se a barra de ferramentas ISE aparece na parte superior da janela de ISE do Windows PowerShell. O valor padrão é `$true`.

```powershell
# Show the toolbar.
$psISE.Options.ShowToolBar = $true
```

### <a name="showwarningbeforesavingonrun"></a>ShowWarningBeforeSavingOnRun

Suportado no Windows PowerShell ISE 2.0 e posteriores.

Especifica se uma mensagem de aviso aparece quando um script é salvo automaticamente antes de ser executado.
O valor padrão é `$true`.

```powershell
# Enable the warning message when an attempt
# is made to run a script without saving it first.
$psISE.Options.ShowWarningBeforeSavingOnRun = $true
```

### <a name="showwarningforduplicatefiles"></a>ShowWarningForDuplicateFiles

Suportado no Windows PowerShell ISE 2.0 e posteriores.

Especifica se uma mensagem de aviso aparece quando o mesmo arquivo é aberto em diferentes guias do PowerShell. Se definido como `$true`, para abrir o mesmo arquivo em várias guias, exibe esta mensagem: "Uma cópia desse arquivo está aberta em outra guia do Windows PowerShell. As alterações feitas neste arquivo afetarão todas as cópias abertas". O valor padrão é `$true`.

```powershell
# Enable the warning message when a file is
# opened in multiple PowerShell tabs.
$psISE.Options.ShowWarningForDuplicateFiles = $true
```

### <a name="tokencolors"></a>TokenColors

Suportado no Windows PowerShell ISE 2.0 e posteriores.

Especifica as cores de tokens do IntelliSense no painel de script do ISE do Windows PowerShell. Essa propriedade é um objeto de dicionário que contém pares de nome/valor de tipos de token e cores para o painel Script. Para alterar as cores dos tokens IntelliSense no painel de Console, consulte [ConsoleTokenColors](#consoletokencolors).
Para redefinir as cores aos valores padrão, consulte [RestoreDefaultTokenColors](#restoredefaulttokencolors).
As cores do token podem ser definidas para o seguinte: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable.

```powershell
# Sets the color of commands to green.
$psISE.Options.TokenColors["Command"] = "green"
# Sets the color of keywords to magenta.
$psISE.Options.TokenColors["Keyword"] = "magenta"
```

### <a name="useentertoselectinconsolepaneintellisense"></a>UseEnterToSelectInConsolePaneIntellisense

Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.

Especifica se você pode usar a tecla Enter para selecionar uma opção IntelliSense fornecida no painel de Console. O valor padrão é `$true`.

```powershell
# Turn off using the ENTER key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense = $false
```

### <a name="useentertoselectinscriptpaneintellisense"></a>UseEnterToSelectInScriptPaneIntellisense

Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.

Especifica se você pode usar a tecla Enter para selecionar uma opção IntelliSense fornecida no painel Script. O valor padrão é `$true`.

```powershell
# Turn on using the Enter key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense = $true
```

### <a name="uselocalhelp"></a>UseLocalHelp

Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.

Especifica se a Ajuda instalada localmente ou a Ajuda da biblioteca do TechNet online aparece quando você pressiona <kbd>F1</kbd> com o cursor posicionado em uma palavra-chave. Se definida como `$true`, uma janela pop-up mostra o conteúdo da Ajuda instalada localmente. Você pode instalar os arquivos de Ajuda, executando o comando `Update-Help`. Se definida como `$false`, seu navegador abrirá uma página na biblioteca do TechNet.

```powershell
# Sets the option for the online help to be displayed.
$psISE.Options.UseLocalHelp = $false
# Sets the option for the local Help to be displayed.
$psISE.Options.UseLocalHelp = $true
```

### <a name="verbosebackgroundcolor"></a>VerboseBackgroundColor

Suportado no Windows PowerShell ISE 2.0 e posteriores.

Especifica a cor da tela de fundo para o texto detalhado que aparece no painel de Console. É um objeto **System.Windows.Media.Color** .

```powershell
# Changes the background color for verbose text to blue.
$psISE.Options.VerboseBackgroundColor ='#0000FF'
```

### <a name="verboseforegroundcolor"></a>VerboseForegroundColor

Suportado no Windows PowerShell ISE 2.0 e posteriores.

Especifica a cor de primeiro plano para o texto detalhado que aparece no painel de Console. É um objeto **System.Windows.Media.Color** .

```powershell
# Changes the foreground color for verbose text to yellow.
$psISE.Options.VerboseForegroundColor = 'yellow'
```

### <a name="warningbackgroundcolor"></a>WarningBackgroundColor

Suportado no Windows PowerShell ISE 2.0 e posteriores.

Especifica a cor da tela de fundo para o texto de aviso que aparece no painel de Console. É um objeto **System.Windows.Media.Color** .

```powershell
# Changes the background color for warning text to blue.
$psISE.Options.WarningBackgroundColor = '#0000FF'
```

### <a name="warningforegroundcolor"></a>WarningForegroundColor

Suportado no Windows PowerShell ISE 2.0 e posteriores.

Especifica a cor de primeiro plano para o texto detalhado que aparece no painel de Saída. É um objeto **System.Windows.Media.Color** .

```powershell
# Changes the foreground color for warning text to yellow.
$psISE.Options.WarningForegroundColor = 'yellow'
```

### <a name="xmltokencolors"></a>XmlTokenColors

Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.

Especifica um objeto de dicionário que contém pares de nome/valor de tipos e cores de token para o conteúdo XML exibido no ISE do Windows PowerShell. As cores do token podem ser definidas para o seguinte: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable. Veja também [RestoreDefaultXmlTokenColors](#restoredefaultxmltokencolors).

```powershell
# Sets the color of XML element names to green.
$psISE.Options.XmlTokenColors["ElementName"] = 'green'
# Sets the color of XML comments to magenta.
$psISE.Options.XmlTokenColors["Comment"] = 'magenta'
```

### <a name="zoom"></a>Zoom

Com suporte no Windows PowerShell ISE 3.0 e posterior, não está presente em versões anteriores.

Especifica o tamanho relativo do texto, nos painéis de Console e Script. O valor padrão é 100.
Valores menores podem fazer com que o texto no ISE do Windows PowerShell pareça menor, enquanto números maiores fazem com que o texto pareça maior. O valor é um número inteiro que varia de 20 a 400.

```powershell
# Changes the text in the Windows PowerShell ISE to be double its normal size.
$psISE.Options.Zoom = 200
```

## <a name="see-also"></a>Consulte Também

- [Objetivo do modelo de objeto de script do ISE do Windows PowerShell](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [A hierarquia de modelo de objeto do ISE](The-ISE-Object-Model-Hierarchy.md)
