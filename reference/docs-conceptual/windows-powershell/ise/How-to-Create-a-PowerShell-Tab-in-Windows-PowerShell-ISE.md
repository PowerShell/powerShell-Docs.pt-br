---
ms.date: 01/02/2020
title: Como criar uma guia do PowerShell no ISE do Windows PowerShell
description: As guias no ISE (Ambiente de Script Integrado) do Windows PowerShell permitem criar e usar simultaneamente vários ambientes de execução dentro do mesmo aplicativo. Cada guia do PowerShell corresponde a uma sessão ou ambiente de execução separado.
ms.openlocfilehash: 62054014be9890b3fa0296f717f65a85534628d8
ms.sourcegitcommit: 488a940c7c828820b36a6ba56c119f64614afc29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92663788"
---
# <a name="how-to-create-a-powershell-tab-in-windows-powershell-ise"></a>Como criar uma guia do PowerShell no ISE do Windows PowerShell

As guias no ISE (Ambiente de Script Integrado) do Windows PowerShell permitem criar e usar simultaneamente vários ambientes de execução dentro do mesmo aplicativo. Cada guia do PowerShell corresponde a uma sessão ou ambiente de execução separado.

> [!NOTE]
> Variáveis, funções e aliases que você criar em uma guia não serão transferidos para outra. Eles são sessões diferentes do Windows PowerShell.

Use as etapas a seguir para abrir ou fechar uma guia no Windows PowerShell. Para renomear uma guia, defina a propriedade [DisplayName](object-model/The-PowerShellTab-Object.md#displayname) no objeto de script de guia do Windows PowerShell.

## <a name="to-create-and-use-a-new-powershell-tab"></a>Para criar e usar uma nova guia do PowerShell

No menu **Arquivo** , clique em **Nova Guia do PowerShell** . A nova guia do PowerShell sempre é aberta como a janela ativa. Guias do PowerShell são numeradas incrementalmente na ordem em que são abertas. Cada guia é associada à sua própria janela de console do Windows PowerShell. Você pode ter até 32 guias do PowerShell com sua própria sessão aberta de cada vez (isso é limitado a 8 no ISE do Windows PowerShell 2.0.)

Observe que clicar nos ícones **Novo** ou **Abrir** na barra de ferramentas não cria uma nova guia com uma sessão separada. Em vez disso, esses botões abrem um arquivo de script novo ou existente na guia ativa no momento com uma sessão. Você pode deixar vários arquivos de script abertos com cada guia e a sessão. As guias de script para uma sessão só aparecem abaixo das guias de sessão quando a sessão associada estiver ativa.

Para tornar uma guia do PowerShell ativa, clique nela. Para selecionar todas as guias do PowerShell que estão abertas no menu **Exibir** , clique na guia do PowerShell que você deseja usar.

## <a name="to-create-and-use-a-new-remote-powershell-tab"></a>Para criar e usar uma nova guia remota do PowerShell

No menu **Arquivo** , clique em **Nova Guia Remota do PowerShell** para estabelecer uma sessão em um computador remoto. Uma caixa de diálogo é exibida e solicita que você insira os detalhes necessários para estabelecer a conexão remota. A guia remota funciona como uma guia local do PowerShell, mas os comandos e os scripts são executados no computador remoto.

## <a name="to-close-a-powershell-tab"></a>Para fechar uma guia do PowerShell

Para fechar uma guia, você pode usar qualquer uma das seguintes técnicas:

- Clique na guia que você deseja fechar.

- No menu **Arquivo** , clique em **Fechar Guia do PowerShell** ou no botão Fechar ( **X** ) em uma guia ativa para fechá-la.

Se tiver arquivos não salvos abertos na guia do PowerShell que você está fechando, será solicitado salvá-los ou descartá-los. Para obter mais informações sobre como salvar um script, consulte [Como salvar um script](How-to-Write-and-Run-Scripts-in-the-Windows-PowerShell-ISE.md#how-to-save-a-script).

## <a name="see-also"></a>Consulte Também

- [Apresentando o ISE do Windows PowerShell](Introducing-the-Windows-PowerShell-ISE.md)
- [Como usar o Painel de Console com o ISE do Windows PowerShell](How-to-Use-the-Console-Pane-in-the-Windows-PowerShell-ISE.md)
