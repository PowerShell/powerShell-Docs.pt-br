---
ms.date: 06/09/2020
ms.topic: reference
title: Palavras-chave de ajuda baseada em comentários
description: Palavras-chave de ajuda baseada em comentários
ms.openlocfilehash: d87dde8700813767f6c09cfce70ed06c7964ebc7
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92645479"
---
# <a name="comment-based-help-keywords"></a>Palavras-chave de ajuda baseada em comentários

Este tópico lista e descreve as palavras-chave na Ajuda baseada em comentários.

## <a name="keywords-in-comment-based-help"></a>Palavras-chave na ajuda Comment-Based

Veja a seguir as palavras-chave de ajuda com base em comentários válidas. Eles são listados na ordem em que normalmente aparecem em um tópico da ajuda junto com o uso pretendido. Essas palavras-chave podem aparecer em qualquer ordem na Ajuda baseada em comentários e não diferenciam maiúsculas de minúsculas.

Observe que a `.EXTERNALHELP` palavra-chave tem precedência sobre todas as outras palavras-chaves de ajuda baseadas em comentários.
Quando `.EXTERNALHELP` o estiver presente, o cmdlet [Microsoft. PowerShell. Commands. GetHelpCommand](/dotnet/api/Microsoft.PowerShell.Commands.gethelpcommand) não exibirá ajuda baseada em comentários, mesmo quando ele não encontrar um arquivo de ajuda que corresponda ao valor da palavra-chave.

## <a name="synopsis"></a>. Resumo

Uma breve descrição da função ou do script. Essa palavra-chave pode ser usada apenas uma vez em cada tópico.

## <a name="description"></a>. NDESCRIÇÃO

Uma descrição detalhada da função ou do script. Essa palavra-chave pode ser usada apenas uma vez em cada tópico.

## <a name="parameter-parameter-name"></a>. METER \<Parameter-Name>

A descrição de um parâmetro. Você pode incluir uma `.PARAMETER` palavra-chave para cada parâmetro na função ou script.

As `.PARAMETER` palavras-chave podem aparecer em qualquer ordem no bloco de comentários, mas a ordem na qual os parâmetros aparecem na `Param` instrução ou declaração de função determina a ordem na qual os parâmetros aparecem no tópico da ajuda. Para alterar a ordem dos parâmetros no tópico da ajuda, altere a ordem dos parâmetros na `Param` instrução ou na declaração da função.

Você também pode especificar uma descrição de parâmetro colocando um comentário na `Param` instrução imediatamente antes do nome da variável de parâmetro. Se você usar um `Param` Comentário de instrução e uma `.PARAMETER` palavra-chave, a descrição associada à `.PARAMETER` palavra-chave será usada e o `Param` Comentário da instrução será ignorado.

## <a name="example"></a>. EXEMPLO

Um comando de exemplo que usa a função ou o script, opcionalmente seguido por saída de exemplo e uma descrição. Repita essa palavra-chave para cada exemplo.

## <a name="inputs"></a>. INFORMAÇÕES

Os tipos de Microsoft .NET Framework de objetos que podem ser canalizados para a função ou o script. Você também pode incluir uma descrição dos objetos de entrada.

## <a name="outputs"></a>. PRODUZ

O tipo de .NET Framework dos objetos que o cmdlet retorna. Você também pode incluir uma descrição dos objetos retornados.

## <a name="notes"></a>. REGISTRA

Informações adicionais sobre a função ou o script.

## <a name="link"></a>. CRIAR

O nome de um tópico relacionado. Repita essa palavra-chave para cada tópico relacionado. Esse conteúdo aparece na seção links relacionados do tópico da ajuda.

O `.LINK` conteúdo da palavra-chave também pode incluir um URI (Uniform Resource Identifier) em uma versão online do mesmo tópico da ajuda. A versão online é aberta quando você usa o `Online` parâmetro de `Get-Help` . O URI deve começar com "http" ou "https".

## <a name="component"></a>. COMPONENTE

O nome da tecnologia ou do recurso que a função ou o script usa, ou ao qual ele está relacionado.
O parâmetro de **componente** do `Get-Help` usa esse valor para filtrar os resultados da pesquisa retornados por `Get-Help` .

## <a name="role"></a>. Cargo

O nome da função de usuário para o tópico da ajuda. O parâmetro de **função** de `Get-Help` usa esse valor para filtrar os resultados de pesquisa retornados por `Get-Help` .

## <a name="functionality"></a>. FUNÇÃO

As palavras-chave que descrevem o uso pretendido da função. O parâmetro de **funcionalidade** do `Get-Help` usa esse valor para filtrar os resultados da pesquisa retornados por `Get-Help` .

## <a name="forwardhelptargetname-command-name"></a>. FORWARDHELPTARGETNAME \<Command-Name>

Redireciona para o tópico da ajuda para o comando especificado. Você pode redirecionar os usuários para qualquer tópico da ajuda, incluindo tópicos de ajuda para uma função, script, cmdlet ou provedor.

## <a name="forwardhelpcategory-category"></a>. FORWARDHELPCATEGORY \<Category>

Especifica a categoria de ajuda do item no `.FORWARDHELPTARGETNAME` . Use essa palavra-chave para evitar conflitos quando houver comandos com o mesmo nome.

Os valores válidos são:

- Alias
- Cmdlet
- HelpFile
- Função
- Provedor
- Geral
- Perguntas frequentes
- Glossário
- ScriptCommand
- ExternalScript
- Filtrar
- Tudo

## <a name="remotehelprunspace-pssession-variable"></a>. REMOTEHELPRUNSPACE \<PSSession-variable>

Especifica uma sessão que contém o tópico da ajuda. Insira uma variável que contenha uma PSSession. Essa palavra-chave é usada pelo `Export-PSSession` cmdlet para localizar os tópicos da ajuda para os comandos exportados.

## <a name="externalhelp-xml-help-file"></a>. EXTERNALHELP \<XML Help File>

Especifica o caminho e/ou o nome de um arquivo de ajuda baseado em XML para o script ou função.

A `.EXTERNALHELP` palavra-chave informa ao cmdlet [Microsoft. PowerShell. Commands. GetHelpCommand](/dotnet/api/Microsoft.PowerShell.Commands.gethelpcommand) para obter ajuda para o script ou a função em um arquivo baseado em XML. A `.EXTERNALHELP` palavra-chave é necessária ao usar um arquivo de ajuda baseado em XML para um script ou uma função. Sem ele, `Get-Help` o não encontrará um arquivo de ajuda para a função ou o script.

A `.EXTERNALHELP` palavra-chave tem precedência sobre todas as outras palavras-chaves de ajuda baseadas em comentários. Quando `.EXTERNALHELP` o estiver presente, o cmdlet [Microsoft. PowerShell. Commands. GetHelpCommand](/dotnet/api/Microsoft.PowerShell.Commands.gethelpcommand) não exibirá ajuda baseada em comentários, mesmo quando ele não encontrar um arquivo de ajuda que corresponda ao valor da palavra-chave.

Quando a função é exportada por um módulo de script, o valor de `.EXTERNALHELP` deve ser um nome de arquivo sem um caminho. `Get-Help` procura o arquivo em um subdiretório específico da localidade do diretório do módulo. Não há requisitos para o nome de arquivo, mas uma prática recomendada é usar o seguinte formato de nome de arquivo: `<ScriptModule>.psm1-help.xml` .

Quando a função não estiver associada a um módulo, inclua um caminho e um nome de arquivo no valor da `.EXTERNALHELP` palavra-chave. Se o caminho especificado para o arquivo XML contiver subdiretórios específicos da cultura da interface do usuário, `Get-Help` o pesquisará os subdiretórios recursivamente para um arquivo XML com o nome do script ou da função de acordo com os padrões de fallback de idioma estabelecidos para o Windows, assim como faz para todos os tópicos de ajuda baseados em XML.

Para obter mais informações sobre o formato de arquivo de ajuda baseado em XML da ajuda do cmdlet, consulte [a ajuda do cmdlet Writing Windows PowerShell](./writing-help-for-windows-powershell-cmdlets.md).
