---
ms.date: 08/14/2018
keywords: powershell, cmdlet
title: Como gravar e executar scripts no ISE do Windows PowerShell
ms.openlocfilehash: be54e26965a6d2f1472059820080a6a06c47dd26
ms.sourcegitcommit: a6e54a305fdeb6482321c77da8066d2f991c93e1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2019
ms.locfileid: "74117562"
---
# <a name="how-to-write-and-run-scripts-in-the-windows-powershell-ise"></a>Como gravar e executar scripts no ISE do Windows PowerShell

Este artigo descreve como criar, editar, executar e salvar scripts no Painel de Script.

## <a name="how-to-create-and-run-scripts"></a>Como criar e executar scripts

Você pode abrir e editar arquivos do Windows PowerShell no Painel de Script. Tipos de arquivos específicos de interesse no Windows PowerShell são arquivos de script (.ps1), arquivos de dados de script (.psd1) e arquivos de módulo de script (.psm1). Esses tipos de arquivo são coloridos por sintaxe no editor do Painel de Script. Outros tipos de arquivo comuns que você pode abrir no Painel de Script são arquivos de configuração (.ps1xml), arquivos XML e arquivos de texto.

> [!NOTE]
> A política de execução do Windows PowerShell determina se você pode executar scripts e carregar perfis e arquivos de configuração do Windows PowerShell. A política de execução padrão, Restricted, impede a execução de todos os scripts e impede o carregamento dos perfis. Para alterar a política de execução para permitir que os perfis sejam carregados usados, consulte [Set-ExecutionPolicy](/powershell/module/microsoft.powershell.security/set-executionpolicy) e [about_Signing](/powershell/module/microsoft.powershell.core/about/about_signing).

### <a name="to-create-a-new-script-file"></a>Para criar um novo arquivo de script

Na barra de ferramentas, clique em **Novo** ou, no menu **Arquivo**, clique em **Novo**. O arquivo criado aparece em uma nova guia do arquivo sob a guia atual do PowerShell. Lembre-se de que as guias do PowerShell são visíveis apenas quando há mais de uma. Por padrão, um arquivo de script de tipo (.ps1) é criado, mas pode ser salvo com um novo nome e uma extensão. Vários arquivos de script podem ser criados na mesma guia do PowerShell.

### <a name="to-open-an-existing-script"></a>Para abrir um script existente

Na barra de ferramentas, clique em **Abrir** ou, no menu **Arquivo**, clique em **Abrir**. Na caixa de diálogo **Abrir**, selecione o arquivo que você deseja abrir. O arquivo aberto aparece em uma nova guia.

### <a name="to-close-a-script-tab"></a>Para fechar uma guia de script

Clique no ícone **Fechar** (X) da guia de arquivo que você quer fechar ou selecione o menu **Arquivo** e clique em **Fechar**.

Se o arquivo tiver sido alterado desde que foi salvo pela última vez, você precisará salvá-lo ou descartá-lo.

### <a name="to-display-the-file-path"></a>Para exibir o caminho do arquivo

Na guia arquivo, aponte para o nome do arquivo. O caminho totalmente qualificado para o arquivo de script é exibido em uma dica de ferramenta.

### <a name="to-run-a-script"></a>Para executar um script

Na barra de ferramentas, clique em **Executar Script** ou, no menu **Arquivo**, clique em **Executar**.

### <a name="to-run-a-portion-of-a-script"></a>Para executar uma parte de um script

1. No Painel de Script, selecione uma parte de um script.
2. No menu **Arquivo**, clique em **Executar Seleção** ou, na barra de ferramentas, clique em **Executar Seleção**.

### <a name="to-stop-a-running-script"></a>Para interromper um script em execução

Há várias maneiras para interromper um script em execução.

- Clique em **Parar Operação** na barra de ferramentas
- Pressione Ctrl+Break
- Selecione o menu **Arquivo** e clique em **Parar Operação**.

Pressionar **Ctrl+C** também funciona, a menos que algum texto esteja selecionado no momento, quando então **Ctrl+C** é mapeado para a função de cópia do texto selecionado.

## <a name="how-to-write-and-edit-text-in-the-script-pane"></a>Como gravar e editar texto no Painel de Script

Você pode copiar, recortar, colar, localizar e substituir texto no Painel de Script. Você também pode desfazer e refazer a última ação que você acabou de executar. Os atalhos de teclado para essas ações são os mesmos usados para todos os aplicativos do Windows.

### <a name="to-enter-text-in-the-script-pane"></a>Para inserir texto no Painel de Script

1. Mova o cursor para o Painel de Script clicando em qualquer lugar no Painel de Script ou clicando em **Ir para o Painel de Script** no menu **Exibição**.
2. Crie um script. A coloração de sintaxe e o preenchimento com tabulação fornece uma experiência mais avançada de edição no ISE do Windows PowerShell.
3. Consulte [Como usar o preenchimento com Tab no Painel de Script e no Painel de Console](How-to-Use-Tab-Completion-in-the-Script-Pane-and-Console-Pane.md) para obter detalhes sobre como usar o recurso de preenchimento com Tab para ajudar na digitação.

### <a name="to-find-text-in-the-script-pane"></a>Para localizar texto no Painel de Script

1. Para localizar texto em qualquer lugar, pressione **Ctrl+F** ou, no menu **Editar**, clique em **Localizar no Script**.
2. Para localizar texto após o cursor, pressione **F3** ou, no menu **Editar**, clique em **Localizar Próximo no Script**.
3. Para localizar o texto antes do cursor, pressione **Shift+F3** ou, no menu **Editar**, clique em **Localizar Anterior no Script**.

### <a name="to-find-and-replace-text-in-the-script-pane"></a>Para localizar e substituir texto no Painel de Script

Pressione **Ctrl+H** ou, no menu **Editar**, clique em **Substituir no Script**. Insira o texto que você deseja localizar e o texto de substituição, depois pressione **Enter**.

### <a name="to-go-to-a-particular-line-of-text-in-the-script-pane"></a>Para ir para uma determinada linha de texto no Painel de Script

1. No Painel de Script, pressione **Ctrl+G** ou, no menu **Editar**, clique em **Ir para a Linha**.

2. Insira um número de linha.

### <a name="to-copy-text-in-the-script-pane"></a>Para copiar o texto no Painel de Script

1. No Painel de Script, selecione o texto que você deseja copiar.

2. Pressione **Ctrl+C** ou, na barra de ferramentas, clique no ícone **Copiar** ou, no menu **Editar**, clique em **Copiar**.

### <a name="to-cut-text-in-the-script-pane"></a>Para recortar texto no Painel de Script

1. No Painel de Script, selecione o texto que você deseja recortar.
2. Pressione **Ctrl+X** ou, na barra de ferramentas, clique no ícone **Recortar** ou, no menu **Editar**, clique em **Recortar**.

### <a name="to-paste-text-into-the-script-pane"></a>Para colar o texto no Painel de Script

Pressione **Ctrl+V** ou, na barra de ferramentas, clique no ícone **Colar** ou, no menu **Editar**, clique em **Colar**.

### <a name="to-undo-an-action-in-the-script-pane"></a>Para desfazer uma ação no Painel de Script

Pressione **Ctrl+Z** ou, na barra de ferramentas, clique no ícone **Desfazer** ou, no menu **Editar**, clique em **Desfazer**.

### <a name="to-redo-an-action-in-the-script-pane"></a>Para refazer uma ação no Painel de Script

Pressione **Ctrl+Y** ou, na barra de ferramentas, clique no ícone **Refazer** ou, no menu **Editar**, clique em **Refazer**.

## <a name="how-to-save-a-script"></a>Como salvar um script

Um asterisco é exibido ao lado do nome do script para marcar um arquivo que não foi salvo desde que ele foi alterado. O asterisco desaparece quando o arquivo é salvo.

### <a name="to-save-a-script"></a>Para salvar um script

Pressione **Ctrl+S** ou, na barra de ferramentas, clique no ícone **Salvar** ou, no menu **Arquivo**, clique em **Salvar**.

### <a name="to-save-and-name-a-script"></a>Para salvar e nomear um script

1. No menu **Arquivo**, clique em **Salvar Como**. A caixa de diálogo **Salvar Como** é exibida.
2. Na caixa **Nome do arquivo**, insira um nome para o arquivo.
3. Na caixa **Salvar como tipo**, selecione um tipo de arquivo. Por exemplo, na caixa **Salvar como tipo**, selecione "Scripts do PowerShell (\*.ps1)".
4. Clique em **Salvar**.

### <a name="to-save-a-script-in-ascii-encoding"></a>Para salvar um script em codificação ASCII

Por padrão, o ISE do Windows PowerShell salva novos arquivos de script (.ps1), arquivos de dados de script (.psd1) e arquivos de módulo de script (.psm1) como Unicode (BigEndianUnicode). Para salvar um script em outra codificação, como ASCII (ANSI), use os métodos **Save** ou **SaveAs** no objeto [$psISE.CurrentFile](object-model/the-ise-object-model-hierarchy.md).

O comando a seguir salva um novo script como MyScript.ps1 com codificação ASCII.

```powershell
$psISE.CurrentFile.SaveAs("MyScript.ps1", [System.Text.Encoding]::ASCII)
```

O comando a seguir substitui o arquivo de script atual por um arquivo com o mesmo nome, mas com codificação ASCII.

```powershell
$psISE.CurrentFile.Save([System.Text.Encoding]::ASCII)
```

O comando a seguir obtém a codificação do arquivo atual.

```powershell
$psISE.CurrentFile.encoding
```

O ISE do Windows PowerShell dá suporte às seguintes opções de codificação: ASCII, BigEndianUnicode, Unicode, UTF32, UTF7, UTF8 e padrão. O valor da opção Padrão varia de acordo com o sistema.

O ISE do Windows PowerShell não altera a codificação dos arquivos de script quando você usa os comandos Salvar ou Salvar como.

## <a name="see-also"></a>Consulte Também

- [Explorando o ISE do Windows PowerShell](exploring-the-windows-powershell-ise.md)
