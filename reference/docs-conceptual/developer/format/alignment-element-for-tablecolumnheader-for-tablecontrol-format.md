---
ms.date: 09/13/2016
ms.topic: reference
title: Elemento Alignment para TableColumnHeader para TableControl (formato)
description: Elemento Alignment para TableColumnHeader para TableControl (formato)
ms.openlocfilehash: cf8b90c12c28951283b5870186e2c88d427318a5
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92666817"
---
# <a name="alignment-element-for-tablecolumnheader-for-tablecontrol-format"></a>Elemento Alignment para TableColumnHeader para TableControl (formato)

Define como os dados em um cabeçalho de coluna são exibidos.

Elemento de configuração (Format) elemento ViewDefinitions (Format) exibição de elemento (Format) TableControl Element (Format) TableHeaders elemento (Format) TableColumnHeader elemento (Format) o elemento de alinhamento para TableColumnHeader (Format)

## <a name="syntax"></a>Sintaxe

```xml
<Alignment>AlignmentType</Alignment>
```

## <a name="attributes-and-elements"></a>Atributos e elementos

As seções a seguir descrevem os atributos, os elementos filho e o elemento pai do `Alignment` elemento.

### <a name="attributes"></a>Atributos

nenhuma.

### <a name="child-elements"></a>Elementos filho

nenhuma.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento TableColumnHeader (formato)](./tablecolumnheader-element-format.md)|Define um rótulo, a largura e o alinhamento dos dados para uma coluna da tabela.|

## <a name="text-value"></a>Valor de texto

Especifique um dos valores a seguir. Esses valores não diferenciam maiúsculas de minúsculas.

À esquerda alinha os dados exibidos na coluna à esquerda, esse será o padrão se esse elemento não for especificado.

Alinha à direita os dados exibidos na coluna à direita.

Centraliza os dados exibidos na coluna.

## <a name="remarks"></a>Comentários

Para obter mais informações sobre os componentes de uma exibição de tabela, consulte [criando uma exibição de tabela](./creating-a-table-view.md).

## <a name="example"></a>Exemplo

Este exemplo mostra um `TableColumnHeader` elemento cujos dados estão alinhados à esquerda.

```xml
<TableColumnHeader>
  <Label>Column 1</Label)
  <Width>16</Width>
  <Alignment>Left</Alignment>
</TableColumnHeader>
```

## <a name="see-also"></a>Consulte Também

[Criar uma exibição de tabela](./creating-a-table-view.md)

[Elemento TableColumnHeader (formato)](./tablecolumnheader-element-format.md)

[Escrever um arquivo de formatação do PowerShell](./writing-a-powershell-formatting-file.md)
