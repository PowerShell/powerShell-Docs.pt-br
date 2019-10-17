---
title: Elemento PropertyName para SelectionCondition para EntrySelectedBy para EnumerableExpansion (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9ae11924-0072-451e-bf70-c5ffb25dccc0
caps.latest.revision: 13
ms.openlocfilehash: 0c20512e660c8d2b61d063dbd7078b55b23efeb8
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72362315"
---
# <a name="propertyname-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format"></a><span data-ttu-id="3faae-102">Elemento PropertyName para SelectionCondition para EntrySelectedBy para EnumerableExpansion (formato)</span><span class="sxs-lookup"><span data-stu-id="3faae-102">PropertyName Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>

<span data-ttu-id="3faae-103">Especifica a propriedade .NET que dispara a condição.</span><span class="sxs-lookup"><span data-stu-id="3faae-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="3faae-104">Quando essa propriedade está presente ou quando é avaliada como `true`, a condição é atendida e a definição é usada.</span><span class="sxs-lookup"><span data-stu-id="3faae-104">When this property is present or when it evaluates to `true`, the condition is met, and the definition is used.</span></span>

<span data-ttu-id="3faae-105">Elemento de configuração (Format) DefaultSettings Element (Format) EnumerableExpansions elemento (Format) EnumerableExpansion Element (Format) EntrySelectedBy elemento para EnumerableExpansion (Format) SelectionCondition Element for EntrySelectedBy para Elemento EnumerableExpansion (Format) PropertyName para SelectionCondition para EntrySelectedBy para EnumerableExpansion (Format)</span><span class="sxs-lookup"><span data-stu-id="3faae-105">Configuration Element (Format) DefaultSettings Element (Format) EnumerableExpansions Element (Format) EnumerableExpansion Element (Format) EntrySelectedBy Element for EnumerableExpansion (Format) SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format) PropertyName Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="3faae-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="3faae-106">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="3faae-107">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="3faae-107">Attributes and Elements</span></span>

<span data-ttu-id="3faae-108">As seções a seguir descrevem atributos, elementos filho e o elemento pai do elemento `PropertyName`.</span><span class="sxs-lookup"><span data-stu-id="3faae-108">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="3faae-109">Atributos</span><span class="sxs-lookup"><span data-stu-id="3faae-109">Attributes</span></span>

<span data-ttu-id="3faae-110">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="3faae-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="3faae-111">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="3faae-111">Child Elements</span></span>

<span data-ttu-id="3faae-112">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="3faae-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="3faae-113">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="3faae-113">Parent Elements</span></span>

|<span data-ttu-id="3faae-114">Elemento</span><span class="sxs-lookup"><span data-stu-id="3faae-114">Element</span></span>|<span data-ttu-id="3faae-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="3faae-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="3faae-116">Elemento SelectionCondition para EntrySelectedBy para EnumerableExpansion (Format)</span><span class="sxs-lookup"><span data-stu-id="3faae-116">SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)|<span data-ttu-id="3faae-117">Define a condição que deve existir para expandir os objetos de coleção dessa definição.</span><span class="sxs-lookup"><span data-stu-id="3faae-117">Defines the condition that must exist to expand the collection objects of this definition.</span></span>|

## <a name="text-value"></a><span data-ttu-id="3faae-118">Valor de texto</span><span class="sxs-lookup"><span data-stu-id="3faae-118">Text Value</span></span>

<span data-ttu-id="3faae-119">Especifique o nome da propriedade .NET.</span><span class="sxs-lookup"><span data-stu-id="3faae-119">Specify the .NET property name.</span></span>

## <a name="remarks"></a><span data-ttu-id="3faae-120">Comentários</span><span class="sxs-lookup"><span data-stu-id="3faae-120">Remarks</span></span>

<span data-ttu-id="3faae-121">A condição de seleção deve especificar pelo menos um nome de propriedade ou um script a ser avaliado, mas não pode especificar ambos.</span><span class="sxs-lookup"><span data-stu-id="3faae-121">The selection condition must specify at least one property name or a script to evaluate, but cannot specify both.</span></span> <span data-ttu-id="3faae-122">Para obter mais informações sobre como usar condições de seleção, consulte [definindo condições para quando os dados são exibidos](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="3faae-122">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="3faae-123">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="3faae-123">See Also</span></span>

[<span data-ttu-id="3faae-124">Definindo condições para quando os dados são exibidos</span><span class="sxs-lookup"><span data-stu-id="3faae-124">Defining Conditions for When Data is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="3faae-125">Elemento ScriptBlock para SelectionCondition para EntrySelectedBy para EnumerableExpansion (Format)</span><span class="sxs-lookup"><span data-stu-id="3faae-125">ScriptBlock Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md)

[<span data-ttu-id="3faae-126">Elemento SelectionCondition para EntrySelectedBy para EnumerableExpansion (Format)</span><span class="sxs-lookup"><span data-stu-id="3faae-126">SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)

[<span data-ttu-id="3faae-127">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="3faae-127">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)