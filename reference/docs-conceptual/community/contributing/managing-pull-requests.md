---
title: Como gerenciamos solicitações de pull
description: Este artigo explica como a equipe do PowerShell-Docs gerencia solicitações de pull.
ms.date: 03/05/2020
ms.topic: conceptual
ms.openlocfilehash: b9b37816dfdf38e4d8b7c2d66799164d0e97d257
ms.sourcegitcommit: 18d832858a7b8ea094763afa753e0f48f01372e7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/10/2020
ms.locfileid: "79060381"
---
# <a name="managing-pull-requests"></a>Gerenciar solicitações de pull

Este artigo documenta como gerenciamos solicitações de pull no repositório do PowerShell-Docs. O artigo foi projetado para ser um auxílio de trabalho para membros da equipe do PowerShell-Docs. Publicamos aqui para fornecer transparência quanto ao processo para nossos colaboradores públicos.

## <a name="best-practices"></a>Práticas recomendadas

- A pessoa que envia a PR (solicitação de pull) não deve mesclá-la sem uma revisão em pares.
- Atribua o revisor em pares quando a PR for enviada. A atribuição antecipada permite que o revisor responda mais cedo com comentários editoriais.
- Use os comentários para descrever a natureza da alteração ou o tipo de revisão solicitada. Mencione o revisor com @mention. Por exemplo, se a alteração for secundária, e você não precisar de uma revisão técnica completa, explique isso em um comentário.

## <a name="pr-process-steps"></a>Etapas do processo de PR

1. Autor: criar a PR
   - Vincular quaisquer problemas resolvidos pela PR
   - Usar o recurso [autoclose](https://help.github.com/en/articles/closing-issues-using-keywords) do GitHub para fechar o problema
1. Autor: atribuir revisor em pares
1. Revisor: fazer a revisão e inserir comentários (conforme necessário)
1. Autor: incorporar comentários da revisão
1. Ambos: revisar a renderização de versão prévia
1. Ambos: revisar o relatório de validação, corrigir erros e avisos
1. Autor: adicionar comentário de aprovação (incluir informações do Acrolinx)
1. Revisor: marcar a revisão como "Aprovada"
1. Administrador do repositório: mesclar a PR (confira abaixo os critérios)

## <a name="content-reviewer-checklist"></a>Lista de verificação do revisor de conteúdo

Confira a [lista de verificação editorial](editorial-checklist.md) para obter uma listagem mais abrangente.

- Revisar gramática, estilo, concisão, precisão técnica
- Verificar se os exemplos ainda se aplicam à versão de destino
- Conferir a renderização de versão prévia
- Conferir os metadados – ms.date, remover ms.assetid, garantir os campos obrigatórios
- Validar a correção de markdown
  - Conferir o guia de estilo para a formatação de conteúdo específico
- Reorganizar os exemplos da seguinte maneira:
  - Sentença(s) de introdução
  - Código e saída
  - Explicação detalhada do código (conforme necessário)
- Verificar a precisão dos hiperlinks
  - Substituir ou remover links TechNet/MSDN
  - Garantir o número mínimo de redirecionamentos para o destino
  - Garantir o HTTPS
  - Corrigir tipo de link
    - Links para arquivos locais
    - Links de URL para arquivos fora do docset
  - Remover localidades de URLs
  - Simplificar URLs que apontam para `docs.microsoft.com`

## <a name="branch-merge-process"></a>Processo de mesclagem de branch

O branch de preparo é o único que deve ser mesclado no branch dinâmico. As mesclagens de branches de curta duração (trabalho) devem ser restringidas.

| *Mesclar de/para*  | *branch-lançamento* | *staging*        | *dinâmico*      |
| ---------------- |:----------------:|:----------------:|:-----------:|
| *branch-trabalho* | squash e mesclar | squash e mesclar | Não permitido |
| *branch-lançamento* | &mdash;          | mesclar            | Não permitido |
| *staging*        | trocar base           | &mdash;          | mesclar       |

### <a name="pr-merger-checklist"></a>Lista de verificação de mesclagem de PR

- Revisão de conteúdo concluída
- Branch de destino correto para a alteração
- Sem conflitos de mesclagem
- Todas as validações e etapas de build aprovadas
  - Avisos e sugestões devem ser corrigidos (confira [Observações](#notes) para ver exceções)
  - Nenhum link desfeito
- Mesclar de acordo com a tabela

### <a name="notes"></a>Observações

Os seguintes avisos podem ser ignorados:

```
Can't find service name for `<version>/<modulepath>/About/About.md`
```

```
Metadata with following name(s) are not allowed to be set in Yaml header, or as file level
metadata in docfx.json, or as global metadata in docfx.json: `locale`. They are generated by
Docs platform, so the values set in these 3 places will be ignored. Please remove them from all
3 places to resolve the warning.
```

Quando uma PR é mesclada, o HEAD do branch de destino é alterado. Qualquer PR aberta com base no HEAD anterior agora está desatualizada. A PR desatualizada pode ser mesclada usando direitos de administrador para substituir os avisos de mesclagem no GitHub. Isso é seguro caso as PRs mescladas anteriormente não tenham tocado os mesmos arquivos. No entanto, a opção mais segura é clicar no botão **Atualizar Branch**. Você pode ter conflitos não resolvidos que precisam ser corrigidos.

## <a name="publishing-to-live"></a>Publicar no site dinâmico

Periodicamente, as alterações acumuladas no branch `staging` precisam ser publicadas no site dinâmico. Isso exige a mesclagem do branch `staging` no branch `live`.

- O branch `staging` deve ser mesclado no `live` pelo menos uma vez por semana.
- O branch `staging` deve ser mesclado no `live` após qualquer alteração significativa.
  - Alterações em 50 ou mais arquivos
  - Depois de mesclar um branch de lançamento
  - Alterações nas configurações de repositório ou docset (docfx.json, configurações OPS, scripts de compilação etc.)
  - Alterações no arquivo de redirecionamento
  - Alterações no TOC
  - Depois de mesclar um branch de "projeto" (reorganização de conteúdo, atualização em massa etc.)