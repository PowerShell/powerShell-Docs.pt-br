---
ms.date: 09/13/2016
ms.topic: reference
title: Elemento CustomEntries para CustomControl para GroupBy (formato)
description: Elemento CustomEntries para CustomControl para GroupBy (formato)
ms.openlocfilehash: cde59d38b83930cb64a3a0040891783e4ab96723
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92666783"
---
# <a name="customentries-element-for-customcontrol-for-groupby-format"></a>Elemento CustomEntries para CustomControl para GroupBy (formato)

Fornece as definições para o controle. Esse elemento é usado ao definir como um novo grupo de objetos é exibido.

Elemento de configuração (Format) elemento ViewDefinitions (Format) exibir elemento (Format) elemento GroupBy para View (Format) CustomControl Element para GroupBy (Format) CustomEntries Element for CustomControl para GroupBy (Format)

## <a name="syntax"></a>Sintaxe

```xml
<CustomEntries>
  <CustomEntry>...</CustomEntry>
</CustomEntries>
```

## <a name="attributes-and-elements"></a>Atributos e elementos

As seções a seguir descrevem atributos, elementos filho e elementos pai do `CustomEntries` elemento. Não há nenhum limite máximo para o número de elementos filho que podem ser especificados.

### <a name="attributes"></a>Atributos

nenhuma.

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento CustomEntry para CustomControl para GroupBy (formato)](./customentry-element-for-customcontrol-for-groupby-format.md)|Elemento necessário.<br /><br /> Fornece uma definição do controle.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento CustomControl para GroupBy (formato)](./customcontrol-element-for-groupby-format.md)|Define o controle personalizado que exibe o novo grupo.|

## <a name="remarks"></a>Comentários

Na maioria dos casos, um controle tem apenas uma definição, que é especificada em um único `CustomEntry` elemento. No entanto, é possível fornecer várias definições se você quiser usar o mesmo controle para exibir diferentes grupos. Nesses casos, você pode definir um `CustomEntry` elemento para um grupo.

## <a name="see-also"></a>Consulte Também

[Elemento CustomEntry para CustomEntries para Controls para configuração (formato)](./customentry-element-for-customentries-for-controls-for-view-format.md)

[Elemento CustomControl para GroupBy (formato)](./customcontrol-element-for-groupby-format.md)

[Escrever um arquivo de formatação do PowerShell](./writing-a-powershell-formatting-file.md)
