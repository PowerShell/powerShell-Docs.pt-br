---
title: Elemento TypeName para EntrySelectedBy para WideEntry (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 81a91c74-6229-4b64-aa2b-9123e8b7e9e5
caps.latest.revision: 11
ms.openlocfilehash: be35f6e9e2ad0b2d9a21a91c053aa0f70cafaf9c
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72361615"
---
# <a name="typename-element-for-entryselectedby-for-wideentry-format"></a><span data-ttu-id="1d1a2-102">Elemento TypeName para EntrySelectedBy para WideEntry (formato)</span><span class="sxs-lookup"><span data-stu-id="1d1a2-102">TypeName Element for EntrySelectedBy for WideEntry (Format)</span></span>

<span data-ttu-id="1d1a2-103">Especifica um tipo .NET para a definição.</span><span class="sxs-lookup"><span data-stu-id="1d1a2-103">Specifies a .NET type for the definition.</span></span> <span data-ttu-id="1d1a2-104">A definição é usada sempre que este objeto é exibido.</span><span class="sxs-lookup"><span data-stu-id="1d1a2-104">The definition is used whenever this object is displayed.</span></span>

<span data-ttu-id="1d1a2-105">Elemento de configuração (Format) elemento ViewDefinitions (Format) View element (Format) WideControl elemento (Format) WideEntries Element (Format) WideEntry elemento (Format) EntrySelectedBy Element para WideEntry (Format) TypeName Element para WideEntry ( Ao</span><span class="sxs-lookup"><span data-stu-id="1d1a2-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element (Format) EntrySelectedBy Element for WideEntry (Format) TypeName Element for WideEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="1d1a2-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="1d1a2-106">Syntax</span></span>

```xml
<TypeName>Nameof.NetType</TypeName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="1d1a2-107">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="1d1a2-107">Attributes and Elements</span></span>

<span data-ttu-id="1d1a2-108">As seções a seguir descrevem os atributos, os elementos filho e o elemento pai do elemento `TypeName`.</span><span class="sxs-lookup"><span data-stu-id="1d1a2-108">The following sections describe the attributes, child elements, and the parent element of the `TypeName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="1d1a2-109">Atributos</span><span class="sxs-lookup"><span data-stu-id="1d1a2-109">Attributes</span></span>

<span data-ttu-id="1d1a2-110">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="1d1a2-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="1d1a2-111">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="1d1a2-111">Child Elements</span></span>

<span data-ttu-id="1d1a2-112">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="1d1a2-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="1d1a2-113">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="1d1a2-113">Parent Elements</span></span>

|<span data-ttu-id="1d1a2-114">Elemento</span><span class="sxs-lookup"><span data-stu-id="1d1a2-114">Element</span></span>|<span data-ttu-id="1d1a2-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="1d1a2-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="1d1a2-116">Elemento EntrySelectedBy para WideEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="1d1a2-116">EntrySelectedBy Element for WideEntry (Format)</span></span>](./entryselectedby-element-for-wideentry-format.md)|<span data-ttu-id="1d1a2-117">Define os tipos .NET que usam essa entrada ampla ou a condição que deve existir para que essa entrada seja usada.</span><span class="sxs-lookup"><span data-stu-id="1d1a2-117">Defines the .NET types that use this wide entry or the condition that must exist for this entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="1d1a2-118">Valor de texto</span><span class="sxs-lookup"><span data-stu-id="1d1a2-118">Text Value</span></span>

<span data-ttu-id="1d1a2-119">Especifique o nome totalmente qualificado do tipo .NET, como `System.IO.DirectoryInfo`.</span><span class="sxs-lookup"><span data-stu-id="1d1a2-119">Specify the fully qualified name of the .NET type, such as `System.IO.DirectoryInfo`.</span></span>

## <a name="remarks"></a><span data-ttu-id="1d1a2-120">Comentários</span><span class="sxs-lookup"><span data-stu-id="1d1a2-120">Remarks</span></span>

<span data-ttu-id="1d1a2-121">Cada entrada larga deve especificar um ou mais tipos .NET, um conjunto de seleção ou a condição de seleção que deve existir para a definição a ser usada.</span><span class="sxs-lookup"><span data-stu-id="1d1a2-121">Each wide entry must specify one or more .NET types, a selection set, or the selection condition that must exist for the definition to be used.</span></span>

<span data-ttu-id="1d1a2-122">Para obter mais informações sobre outros componentes de uma exibição ampla, consulte [criando uma exibição ampla](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="1d1a2-122">For more information about other components of a wide view, see [Creating a Wide View](./creating-a-wide-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="1d1a2-123">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="1d1a2-123">See Also</span></span>

[<span data-ttu-id="1d1a2-124">Criando uma exibição ampla</span><span class="sxs-lookup"><span data-stu-id="1d1a2-124">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="1d1a2-125">Elemento EntrySelectedBy para WideEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="1d1a2-125">EntrySelectedBy Element for WideEntry (Format)</span></span>](./entryselectedby-element-for-wideentry-format.md)

[<span data-ttu-id="1d1a2-126">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d1a2-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)