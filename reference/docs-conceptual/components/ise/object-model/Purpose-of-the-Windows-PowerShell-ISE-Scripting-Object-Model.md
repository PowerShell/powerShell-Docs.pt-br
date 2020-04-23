---
ms.date: 12/31/2019
keywords: powershell, cmdlet
title: Objetivo do modelo de objeto de script do ISE do Windows PowerShell
ms.openlocfilehash: 1f48df112bd19297baa311116e79d3d7603d7c81
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "75736225"
---
# <a name="purpose-of-the-windows-powershell-ise-scripting-object-model"></a>Objetivo do modelo de objeto de script do ISE do Windows PowerShell

Objetos são associados com a forma e a função do ISE (Ambiente de Script Integrado) do Windows PowerShell. A referência de modelo de objeto fornece detalhes sobre as propriedades e os métodos de membros que esses objetos expõem. Exemplos são fornecidos para mostrar como você pode usar scripts para acessar diretamente esses métodos e propriedades. O modelo de objeto de script facilita a gama de tarefas a seguir.

## <a name="customizing-the-appearance-of-windows-powershell-ise"></a>Personalizando a aparência do ISE do Windows PowerShell

Você pode usar o modelo de objeto para modificar as configurações e opções do aplicativo. Por exemplo, você pode modificá-las da seguinte forma:

- Mudar a cor de erros, avisos, saídas detalhadas e saídas de depuração.
- Obter ou definir cores de tela de fundo para o painel de Comando, painel de Saída e o painel de Script.
- Definir a cor de primeiro plano para o painel de Saída.
- Definir o nome e tamanho da fonte para o ISE do Windows PowerShell.
- Configurar alertas. Essa configuração inclui advertências que são emitidas quando um arquivo é aberto em várias guias do PowerShell ou quando um script no arquivo é executado antes que o arquivo seja salvo.
- Alternar entre uma exibição em que o painel Script e Painel de saída estão lado em uma exibição em que o painel Script está na parte superior do Painel de saída.
- Encaixar o painel de Comando na parte inferior ou superior do painel de Saída.

## <a name="enhancing-the-functionality-of-windows-powershell-ise"></a>Melhorando a funcionalidade do ISE do Windows PowerShell

Você pode usar o modelo de objeto para melhorar a funcionalidade do ISE do Windows PowerShell. Por exemplo, você pode:

- Adicionar e modificar a instância do próprio ISE do Windows PowerShell. Por exemplo, para alterar os menus, você pode adicionar novos itens de menu e mapear os novos itens de menu para os scripts.
- Crie scripts que realizam algumas das tarefas que podem ser executadas usando os comandos de menu e botões no ISE do Windows PowerShell. Por exemplo, você pode adicionar, remover ou selecionar uma guia PowerShell.
- Complemente tarefas que podem ser realizadas usando comandos e botões de menu. Por exemplo, você pode renomear uma guia do PowerShell.
- Manipule buffers de texto para os painéis de Comando, Saída e Script associados a um arquivo. Por exemplo, você pode:
  - Obtenha ou defina todo o texto.
  - Obtenha ou defina uma seleção de texto.
  - Execute um script ou uma parte selecionada de um script.
  - Role uma linha até uma exibição.
  - Insira texto em uma posição de cursor.
  - Selecione um bloco de texto.
  - Obtenha o último número de linha.
- Execute operações de arquivo. Por exemplo, você pode:
  - Abrir um arquivo, salvar um arquivo ou salvar um arquivo usando um nome diferente.
  - Determine se um arquivo foi alterado depois que foi salvo pela última vez.
  - Obtenha o nome do arquivo.
  - Selecione um arquivo.

## <a name="automating-tasks"></a>Automatizando tarefas

Você pode usar o modelo de objeto de script para criar atalhos de teclado para operações frequentes.

## <a name="see-also"></a>Confira também

- [A hierarquia de modelo de objeto do ISE](The-ISE-Object-Model-Hierarchy.md)
