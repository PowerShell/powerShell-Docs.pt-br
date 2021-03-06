---
ms.date: 09/13/2016
ms.topic: reference
title: Elemento CustomControlName para GroupBy (formato)
description: Elemento CustomControlName para GroupBy (formato)
ms.openlocfilehash: 03664fe4d5559312e2720a3892493c90c15f7501
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92655416"
---
# <a name="customcontrolname-element-for-groupby-format"></a>Elemento CustomControlName para GroupBy (formato)

Especifica o nome de um controle personalizado que é usado para exibir o novo grupo. Esse elemento é usado ao definir uma tabela, lista, exibição de controle largo ou personalizada.

Elemento de configuração (Format) elemento ViewDefinitions (Format) exibir elemento (Format) elemento GroupBy para View (Format) CustomControlName element de GroupBy (Format)

## <a name="syntax"></a>Sintaxe

```xml
<CustomControlName>ControlName</CustomControlName>
```

## <a name="attributes-and-elements"></a>Atributos e elementos

As seções a seguir descrevem os atributos, os elementos filho e os elementos pai do `CustomControlName` elemento.

### <a name="attributes"></a>Atributos

nenhuma.

### <a name="child-elements"></a>Elementos filho

nenhuma.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento GroupBy para View (formato)](./groupby-element-for-view-format.md)|Define como o Windows PowerShell exibe um novo grupo de objetos.|

## <a name="text-value"></a>Valor de texto

Especifique o nome do controle personalizado usado para exibir um novo grupo.

## <a name="remarks"></a>Comentários

Você pode criar controles comuns que podem ser usados por todas as exibições de um arquivo de formatação e pode criar controles de exibição que podem ser usados por uma exibição específica. Os seguintes elementos especificam os nomes desses controles personalizados:

- [Elemento Name para Control para Controls para Configuration (formato)](./name-element-for-control-for-controls-for-configuration-format.md)

- [Elemento Name para Control para Controls para View (formato)](./name-element-for-control-for-controls-for-view-format.md)

## <a name="see-also"></a>Consulte Também

[Elemento GroupBy para View (formato)](./groupby-element-for-view-format.md)

[Elemento Name para Control para Controls para Configuration (formato)](./name-element-for-control-for-controls-for-configuration-format.md)

[Elemento Name para Control para Controls para View (formato)](./name-element-for-control-for-controls-for-view-format.md)

[Escrever um arquivo de formatação do PowerShell](./writing-a-powershell-formatting-file.md)
