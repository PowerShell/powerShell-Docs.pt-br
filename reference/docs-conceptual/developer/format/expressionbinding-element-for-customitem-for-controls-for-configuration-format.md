---
ms.date: 09/13/2016
ms.topic: reference
title: Elemento ExpressionBinding para CustomItem para Controls para Configuration (formato)
description: Elemento ExpressionBinding para CustomItem para Controls para Configuration (formato)
ms.openlocfilehash: 1abcf2173e18d45839161b4c7e59f1ad238f81a1
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92655334"
---
# <a name="expressionbinding-element-for-customitem-for-controls-for-configuration-format"></a>Elemento ExpressionBinding para CustomItem para Controls para Configuration (formato)

Define os dados que são exibidos pelo controle. Esse elemento é usado ao definir um controle comum que pode ser usado por todas as exibições no arquivo de formatação.

Elemento de configuração (Format) controla o elemento de controle de configuração (formato) para controles para o elemento de configuração (Format) CustomControl para controle para o elemento de configuração (Format) CustomEntries para CustomControl para o elemento de configuração (Format) CustomEntry para CustomControl para controles para o elemento de configuração (Format) CustomItem para CustomEntry para os controles do elemento ExpressionBinding de configuração para CustomItem para controles de configuração

## <a name="syntax"></a>Sintaxe

```xml
<ExpressionBinding>
  <CustomControl>...</CustomControl>
  <CustomControlName>NameofCommonCustomControl</CustomControlName>
  <EnumerateCollection/>
  <ItemSelectionCondition>...</ItemSelectionCondition>
  <PropertyName>Nameof.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate></ScriptBlock>
</ExpressionBinding>
```

## <a name="attributes-and-elements"></a>Atributos e elementos

As seções a seguir descrevem atributos, elementos filho e o elemento pai do `ExpressionBinding` elemento.

### <a name="attributes"></a>Atributos

nenhuma.

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|`CustomControl Element`|Elemento opcional.<br /><br /> Define um controle que é usado por este controle.|
|[Elemento CustomControlName para ExpressionBinding para Controls para Configuration (formato)](./customcontrolname-element-for-expressionbinding-for-controls-for-configuration-format.md)|Elemento opcional.<br /><br /> Especifica o nome de um controle comum ou um controle de exibição.|
|[Elemento EnumerateCollection para ExpressionBinding para Controls para Configuration (formato)](./enumeratecollection-element-for-expressionbinding-for-controls-for-configuration-format.md)|Elemento opcional.<br /><br /> Especificado que os elementos das coleções são exibidos pelo controle.|
|[Elemento ItemSelectionCondition para ExpressionBinding para Controls para Configuration (formato)](./itemselectioncondition-element-for-expressionbinding-for-controls-for-configuration-format.md)|Elemento opcional.<br /><br /> Define a condição que deve existir para que esse controle comum seja usado.|
|[Elemento PropertyName para ExpressionBinding para Controls para Configuration (formato)](./propertyname-element-for-expressionbinding-for-controls-for-configuration-format.md)|Elemento opcional.<br /><br /> Especifica a propriedade .NET cujo valor é exibido pelo controle comum.|
|[Elemento ScriptBlock para ExpressionBinding para Controls para Configuration (formato)](./scriptblock-element-for-expressionbinding-for-controls-for-configuration-format.md)|Elemento opcional.<br /><br /> Especifica o script cujo valor é exibido pelo controle comum.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento CustomItem para CustomEntry para controles de configuração](./customitem-element-for-customentry-for-controls-for-configuration-format.md)|Define quais dados são exibidos pelo modo de exibição de controle personalizado e como eles são exibidos.|

## <a name="remarks"></a>Comentários

## <a name="see-also"></a>Consulte Também

[Elemento CustomItem para CustomEntry para controles de configuração](./customitem-element-for-customentry-for-controls-for-configuration-format.md)

[Escrever um arquivo de formatação do PowerShell](./writing-a-powershell-formatting-file.md)
