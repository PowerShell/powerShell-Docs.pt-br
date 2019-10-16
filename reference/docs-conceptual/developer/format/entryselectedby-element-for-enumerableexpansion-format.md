---
title: Elemento EntrySelectedBy para EnumerableExpansion (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3af6aff8-4c2d-4f08-9bb1-e1f3ed3e583e
caps.latest.revision: 11
ms.openlocfilehash: 6a371bdbb85d07730c32931a4a79ee40856ce298
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72368795"
---
# <a name="entryselectedby-element-for-enumerableexpansion-format"></a><span data-ttu-id="19874-102">Elemento EntrySelectedBy para EnumerableExpansion (formato)</span><span class="sxs-lookup"><span data-stu-id="19874-102">EntrySelectedBy Element for EnumerableExpansion (Format)</span></span>

<span data-ttu-id="19874-103">Define os tipos .NET que usam essa definição ou a condição que deve existir para que essa definição seja usada.</span><span class="sxs-lookup"><span data-stu-id="19874-103">Defines the .NET types that use this definition or the condition that must exist for this definition to be used.</span></span>

<span data-ttu-id="19874-104">Elemento de configuração (Format) DefaultSettings Element (Format) elemento EnumerableExpansions (Format) elemento EnumerableExpansion Element (Format) EntrySelectedBy elemento para EnumerableExpansion (Format)</span><span class="sxs-lookup"><span data-stu-id="19874-104">Configuration Element (Format) DefaultSettings Element (Format) EnumerableExpansions Element (Format) EnumerableExpansion Element (Format) EntrySelectedBy Element for EnumerableExpansion (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="19874-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="19874-105">Syntax</span></span>

```xml
<EntrySelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <SelectionCondition>...</SelectionCondition>
</EntrySelectedBy>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="19874-106">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="19874-106">Attributes and Elements</span></span>

<span data-ttu-id="19874-107">As seções a seguir descrevem atributos, elementos filho e o elemento pai do elemento `EntrySelectedBy`.</span><span class="sxs-lookup"><span data-stu-id="19874-107">The following sections describe attributes, child elements, and the parent element of the `EntrySelectedBy` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="19874-108">Atributos</span><span class="sxs-lookup"><span data-stu-id="19874-108">Attributes</span></span>

<span data-ttu-id="19874-109">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="19874-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="19874-110">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="19874-110">Child Elements</span></span>

|<span data-ttu-id="19874-111">Elemento</span><span class="sxs-lookup"><span data-stu-id="19874-111">Element</span></span>|<span data-ttu-id="19874-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="19874-112">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="19874-113">Elemento SelectionCondition para EntrySelectedBy para EnumerableExpansion (Format)</span><span class="sxs-lookup"><span data-stu-id="19874-113">SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)|<span data-ttu-id="19874-114">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="19874-114">Optional element.</span></span><br /><br /> <span data-ttu-id="19874-115">Define a condição que deve existir para expandir os objetos de coleção dessa definição.</span><span class="sxs-lookup"><span data-stu-id="19874-115">Defines the condition that must exist to expand the collection objects of this definition.</span></span>|
|[<span data-ttu-id="19874-116">Elemento SelectionSetName para EntrySelectedBy para EnumerableExpansion (Format)</span><span class="sxs-lookup"><span data-stu-id="19874-116">SelectionSetName Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-enumerableexpansion-format.md)|<span data-ttu-id="19874-117">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="19874-117">Optional element.</span></span><br /><br /> <span data-ttu-id="19874-118">Especifica um conjunto de tipos .NET que usam essa definição de como os objetos de coleção são expandidos.</span><span class="sxs-lookup"><span data-stu-id="19874-118">Specifies a set of .NET types that use this definition of how collection objects are expanded.</span></span>|
|[<span data-ttu-id="19874-119">Elemento TypeName para EntrySelectedBy para EnumerableExpansion (Format)</span><span class="sxs-lookup"><span data-stu-id="19874-119">TypeName Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./typename-element-for-entryselectedby-for-enumerableexpansion-format.md)|<span data-ttu-id="19874-120">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="19874-120">Optional element.</span></span><br /><br /> <span data-ttu-id="19874-121">Especifica um tipo .NET que usa essa definição de como os objetos de coleção são expandidos.</span><span class="sxs-lookup"><span data-stu-id="19874-121">Specifies a .NET type that uses this definition of how collection objects are expanded.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="19874-122">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="19874-122">Parent Elements</span></span>

|<span data-ttu-id="19874-123">Elemento</span><span class="sxs-lookup"><span data-stu-id="19874-123">Element</span></span>|<span data-ttu-id="19874-124">Descrição</span><span class="sxs-lookup"><span data-stu-id="19874-124">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="19874-125">Elemento EnumerableExpansion (Format)</span><span class="sxs-lookup"><span data-stu-id="19874-125">EnumerableExpansion Element (Format)</span></span>](./enumerableexpansion-element-format.md)|<span data-ttu-id="19874-126">Define como os objetos de coleção .NET específicos são expandidos quando são exibidos em uma exibição.</span><span class="sxs-lookup"><span data-stu-id="19874-126">Defines how specific .NET collection objects are expanded when they are displayed in a view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="19874-127">Comentários</span><span class="sxs-lookup"><span data-stu-id="19874-127">Remarks</span></span>

<span data-ttu-id="19874-128">Você deve especificar pelo menos um tipo, um conjunto de seleção ou uma condição de seleção para uma entrada de definição.</span><span class="sxs-lookup"><span data-stu-id="19874-128">You must specify at least one type, selection set, or selection condition for a definition entry.</span></span> <span data-ttu-id="19874-129">Não há nenhum limite máximo para o número de elementos filho que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="19874-129">There is no maximum limit to the number of child elements that you can use.</span></span>

<span data-ttu-id="19874-130">As condições de seleção são usadas para definir uma condição que deve existir para a definição a ser usada, como quando um objeto tem uma propriedade específica ou que um valor de propriedade ou script específico é avaliado como `true`.</span><span class="sxs-lookup"><span data-stu-id="19874-130">Selection conditions are used to define a condition that must exist for the definition to be used, such as when an object has a specific property or that a specific property value or script evaluates to `true`.</span></span> <span data-ttu-id="19874-131">Para obter mais informações sobre condições de seleção, consulte [definindo condições para exibir dados](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="19874-131">For more information about selection conditions, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="19874-132">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="19874-132">See Also</span></span>

[<span data-ttu-id="19874-133">Definindo condições para exibir dados</span><span class="sxs-lookup"><span data-stu-id="19874-133">Defining Conditions for Displaying Data</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="19874-134">Elemento EnumerableExpansion (Format)</span><span class="sxs-lookup"><span data-stu-id="19874-134">EnumerableExpansion Element (Format)</span></span>](./enumerableexpansion-element-format.md)

[<span data-ttu-id="19874-135">Elemento SelectionCondition para EntrySelectedBy para EnumerableExpansion (Format)</span><span class="sxs-lookup"><span data-stu-id="19874-135">SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)

[<span data-ttu-id="19874-136">Elemento SelectionSetName para EntrySelectedBy para EnumerableExpansion (Format)</span><span class="sxs-lookup"><span data-stu-id="19874-136">SelectionSetName Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-enumerableexpansion-format.md)

[<span data-ttu-id="19874-137">Elemento TypeName para EntrySelectedBy para EnumerableExpansion (Format)</span><span class="sxs-lookup"><span data-stu-id="19874-137">TypeName Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./typename-element-for-entryselectedby-for-enumerableexpansion-format.md)

[<span data-ttu-id="19874-138">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="19874-138">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
