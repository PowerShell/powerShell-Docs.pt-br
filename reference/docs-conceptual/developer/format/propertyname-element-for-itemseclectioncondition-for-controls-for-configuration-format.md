---
ms.date: 09/13/2016
ms.topic: reference
title: Elemento PropertyName para ItemSelectionCondition para Controls para Configuration (formato)
description: Elemento PropertyName para ItemSelectionCondition para Controls para Configuration (formato)
ms.openlocfilehash: 860683eb54b2a3579767640c1d3f0937897b8f8e
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92655136"
---
# <a name="propertyname-element-for-itemseclectioncondition-for-controls-for-configuration-format"></a>Elemento PropertyName para ItemSelectionCondition para Controls para Configuration (formato)

Especifica a propriedade .NET que dispara a condição. Quando essa propriedade está presente ou quando é avaliada como `true` , a condição é atendida e o controle é usado. Esse elemento é usado ao definir um controle comum que pode ser usado por todas as exibições no arquivo de formatação.

Elemento de configuração (Format) controla o elemento de controle de configuração (formato) para controles para o elemento de configuração (Format) CustomControl para controle para o elemento de configuração (Format) CustomEntries para CustomControl para o elemento de configuração (Format) CustomEntry para CustomControl para controles para a configuração (Format) elemento CustomItem para CustomEntry para controles para o elemento ExpressionBinding de configuração para CustomItem para controles para o elemento Configuration (Format) ItemSelectionCondition para ExpressionBinding para controles para o elemento de configuração (Format) PropertyName para ItemSeclectionCondition para controles para configuração (Format)

## <a name="syntax"></a>Sintaxe

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a>Atributos e elementos

As seções a seguir descrevem atributos, elementos filho e o elemento pai do `PropertyName` elemento.

### <a name="attributes"></a>Atributos

nenhuma.

### <a name="child-elements"></a>Elementos filho

nenhuma.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento ItemSelectionCondition para ExpressionBinding para Controls para Configuration (formato)](./itemselectioncondition-element-for-expressionbinding-for-controls-for-configuration-format.md)|Define a condição que deve existir para que esse controle seja usado.|

## <a name="text-value"></a>Valor de texto

Especifique o nome da Propriedade do .NET que dispara a condição.

## <a name="remarks"></a>Comentários

Se esse elemento for usado, você não poderá especificar o elemento [scriptblock](./scriptblock-element-for-itemseclectioncondition-for-controls-for-configuration-format.md) ao definir a condição de seleção.

## <a name="see-also"></a>Consulte Também

[Elemento ScriptBlock para ItemSeletionCondition para Controls para Configuration (formato)](./scriptblock-element-for-itemseclectioncondition-for-controls-for-configuration-format.md)

[Elemento ItemSelectionCondition para ExpressionBinding para Controls para Configuration (formato)](./itemselectioncondition-element-for-expressionbinding-for-controls-for-configuration-format.md)

[Escrever um arquivo de formatação do PowerShell](./writing-a-powershell-formatting-file.md)
