---
ms.date: 01/02/2020
keywords: powershell, cmdlet
title: Como usar o preenchimento com Tab no Painel de Script e no Painel de Console
ms.openlocfilehash: 07cf9ff75db8d33ed018542153bfcd7503035e40
ms.sourcegitcommit: 2aec310ad0c0b048400cb56f6fa64c1e554c812a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2020
ms.locfileid: "83808822"
---
# <a name="how-to-use-tab-completion-in-the-script-pane-and-console-pane"></a>Como usar o preenchimento com Tab no Painel de Script e no Painel de Console

O preenchimento com Tab fornece ajuda automática quando você está digitando no Painel de Script ou no Painel de Comando. Use as seguintes etapas para aproveitar esse recurso:

## <a name="to-automatically-complete-a-command-entry"></a>Para preencher automaticamente uma entrada de comando

No Painel de Comando ou Painel de Script, digite alguns caracteres de um comando e, em seguida, pressione <kbd>TAB</kbd> para escolher o texto de preenchimento desejado. Se vários itens começam com o texto que você digitou inicialmente, continue a pressionar <kbd>TAB</kbd> até que o item desejado seja exibido. O preenchimento com Tab pode ajudar na digitação do nome de um cmdlet, nome de parâmetro, nome de variável, nome de propriedade do objeto ou um caminho de arquivo.

> [!NOTE]
> No Painel de Script, pressionar <kbd>TAB</kbd> preencherá automaticamente um comando somente quando você estiver editando arquivos `.ps1`, `.psd1` ou `.psm1`. O preenchimento com Tab funciona a qualquer momento quando você está digitando no Painel de Comando.

## <a name="to-automatically-complete-a-cmdlet-parameter-entry"></a>Para preencher automaticamente uma entrada de parâmetro de cmdlet

No Painel de Comando ou de Script, digite um cmdlet seguido por um traço e pressione <kbd>TAB</kbd>.

Por exemplo, digite `Get-Process -` e pressione <kbd>TAB</kbd> várias vezes para exibir cada um dos parâmetros do cmdlet sucessivamente.

## <a name="see-also"></a>Consulte Também

- [Apresentando o ISE do Windows PowerShell](Introducing-the-Windows-PowerShell-ISE.md)
- [Como criar uma guia do PowerShell](How-to-Create-a-PowerShell-Tab-in-Windows-PowerShell-ISE.md)
