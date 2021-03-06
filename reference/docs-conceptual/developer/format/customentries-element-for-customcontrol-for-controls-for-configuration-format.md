---
ms.date: 09/13/2016
ms.topic: reference
title: Elemento CustomEntries para CustomControl para Controls para Configuration (formato)
description: Elemento CustomEntries para CustomControl para Controls para Configuration (formato)
ms.openlocfilehash: 86c2b517d0d7075a355a3190a14e25d9dd4fe374
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92655397"
---
# <a name="customentries-element-for-customcontrol-for-controls-for-configuration-format"></a>Elemento CustomEntries para CustomControl para Controls para Configuration (formato)

Fornece as definições de um controle comum. Esse elemento é usado ao definir um controle comum que pode ser usado por todas as exibições no arquivo de formatação.

Elemento de configuração (Format) controla o elemento de controle de configuração (formato) para controles para o elemento de configuração (Format) CustomControl para controle para o elemento de configuração (Format) CustomEntries para CustomControl para configuração (Format)

## <a name="syntax"></a>Sintaxe

```xml
<CustomEntries>
  <CustomEntry>...</CustomEntry>
</CustomEntries>

```

## <a name="attributes-and-elements"></a>Atributos e elementos

As seções a seguir descrevem atributos, elementos filho e o elemento pai do `CustomEntries` elemento. Você deve especificar um ou mais elementos filho.

### <a name="attributes"></a>Atributos

nenhuma.

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento CustomEntry para CustomControl para Controls para Configuration (formato)](./customentry-element-for-customcontrol-for-controls-for-configuration-format.md)|Fornece uma definição do controle comum.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento CustomControl para controle de configuração (formato)](./customcontrol-element-for-control-for-controls-for-configuration-format.md)|Define um controle comum.|

## <a name="remarks"></a>Comentários

Na maioria dos casos, um controle tem apenas uma definição, que é definida em um único `CustomEntry` elemento. No entanto, é possível ter várias definições se você quiser usar o mesmo controle para exibir diferentes objetos .NET. Nesses casos, você pode definir um `CustomEntry` elemento para cada objeto ou conjunto de objetos.

## <a name="see-also"></a>Consulte Também

[Elemento CustomControl para controle de configuração (formato)](./customcontrol-element-for-control-for-controls-for-configuration-format.md)

[Elemento CustomEntry para CustomControl para Controls para Configuration (formato)](./customentry-element-for-customcontrol-for-controls-for-configuration-format.md)

[Escrever um arquivo de formatação do PowerShell](./writing-a-powershell-formatting-file.md)
