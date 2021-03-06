---
ms.date: 09/13/2016
ms.topic: reference
title: Elemento CustomEntry para CustomControl para Controls para Configuration (formato)
description: Elemento CustomEntry para CustomControl para Controls para Configuration (formato)
ms.openlocfilehash: 3967be86a1d6c12c7215ef19d50bac9fafd5ad6d
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92648289"
---
# <a name="customentry-element-for-customcontrol-for-controls-for-configuration-format"></a>Elemento CustomEntry para CustomControl para Controls para Configuration (formato)

Fornece uma definição do controle comum. Esse elemento é usado ao definir um controle comum que pode ser usado por todas as exibições no arquivo de formatação.

Elemento de configuração (Format) controla o elemento de controle de configuração (formato) para controles para o elemento de configuração (Format) CustomControl para controle para o elemento de configuração (Format) CustomEntries para CustomControl para o elemento de configuração (Format) CustomEntry para CustomControl para controles para a configuração (Format)

## <a name="syntax"></a>Sintaxe

```xml
<CustomEntry>
  <EntrySelectedBy>...</EntrySelectedBy>
  <CustomItem>...</CustomItem>
</CustomEntry>

```

## <a name="attributes-and-elements"></a>Atributos e elementos

As seções a seguir descrevem atributos, elementos filho e o elemento pai do `CustomEntry` elemento. Você deve especificar os itens exibidos pela definição.

### <a name="attributes"></a>Atributos

nenhuma.

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento EntrySelectedBy para CustomEntry para Controls para Configuration (formato)](./entryselectedby-element-for-customentry-for-controls-for-configuration-format.md)|Elemento opcional.<br /><br /> Define os tipos .NET que usam a definição do controle comum ou a condição que deve existir para que esse controle seja usado.|
|[Elemento CustomItem para CustomEntry para controles de configuração](./customitem-element-for-customentry-for-controls-for-configuration-format.md)|Elemento necessário.<br /><br /> Define quais dados são exibidos pelo controle e como eles são exibidos.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento CustomEntries para CustomControl para configuração (formato)](./customentries-element-for-customcontrol-for-controls-for-configuration-format.md)|Fornece as definições do controle comum.|

## <a name="remarks"></a>Comentários

Na maioria dos casos, apenas uma definição é necessária para cada controle personalizado comum, mas é possível ter várias definições se você quiser usar o mesmo controle para exibir diferentes objetos .NET. Nesses casos, você pode fornecer uma definição separada para cada objeto ou conjunto de objetos.

## <a name="see-also"></a>Consulte Também

[Elemento CustomEntries para CustomControl para configuração (formato)](./customentries-element-for-customcontrol-for-controls-for-configuration-format.md)

[Elemento CustomItem para CustomEntry para controles de configuração](./customitem-element-for-customentry-for-controls-for-configuration-format.md)

[Escrever um arquivo de formatação do PowerShell](./writing-a-powershell-formatting-file.md)
