---
ms.date: 09/13/2016
ms.topic: reference
title: Elemento TypeName para EntrySelectedBy para Controls para CustomEntry (formato)
description: Elemento TypeName para EntrySelectedBy para Controls para CustomEntry (formato)
ms.openlocfilehash: 72bb88bccc2bbd62f7ed160b820cf9169cb69341
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92645742"
---
# <a name="typename-element-for-entryselectedby-for-customentry-for-view-format"></a>Elemento TypeName para EntrySelectedBy para Controls para CustomEntry (formato)

Especifica um tipo .NET que usa essa definição do modo de exibição de controle personalizado. Não há nenhum limite para o número de tipos que podem ser especificados para uma definição.

Elemento de configuração (Format) elemento ViewDefinitions (Format) View element (Format) CustomControl elemento (Format) CustomEntries Element for CustomControl para View (Format) CustomEntry Element for CustomEntries para o elemento View (Format) EntrySelectedBy para CustomEntry para o elemento View (Format) TypeName para EntrySelectedBy para CustomEntry para View (Format)

## <a name="syntax"></a>Sintaxe

```xml
<TypeName>Nameof.NetType</TypeName>
```

## <a name="attributes-and-elements"></a>Atributos e elementos

As seções a seguir descrevem atributos, elementos filho e o elemento pai do `TypeName` elemento.

### <a name="attributes"></a>Atributos

nenhuma.

### <a name="child-elements"></a>Elementos filho

nenhuma.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento EntrySelectedBy para CustomEntry para exibição (formato)](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)|Define os tipos .NET que usam essa definição de exibição de controle personalizado ou a condição que deve existir para que essa definição seja usada.|

## <a name="text-value"></a>Valor de texto

Especifique o nome totalmente qualificado do tipo .NET, como `System.IO.DirectoryInfo` .

## <a name="remarks"></a>Comentários

Cada definição de exibição de controle personalizado deve ter pelo menos um nome de tipo, um conjunto de seleção ou uma condição de seleção definida.

Para obter mais informações sobre os componentes de um modo de exibição de controle personalizado, consulte [criando controles personalizados](./creating-custom-controls.md).

## <a name="see-also"></a>Consulte Também

[Criar controles personalizados](./creating-custom-controls.md)

[Elemento EntrySelectedBy para CustomEntry para exibição (formato)](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)

[Escrever um arquivo de formatação do PowerShell](./writing-a-powershell-formatting-file.md)
