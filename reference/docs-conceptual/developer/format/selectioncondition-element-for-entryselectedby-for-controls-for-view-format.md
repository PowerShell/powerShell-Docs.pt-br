---
title: Elemento SelectionCondition para EntrySelectedBy para controles para View (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2623407e-fa10-4d27-a804-204f6d50ef22
caps.latest.revision: 6
ms.openlocfilehash: ea15e647a9dd7a7064718a0c536c4a3178d62d95
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72362045"
---
# <a name="selectioncondition-element-for-entryselectedby-for-controls-for-view-format"></a><span data-ttu-id="8f3e2-102">Elemento SelectionCondition para EntrySelectedBy para Controls para View (formato)</span><span class="sxs-lookup"><span data-stu-id="8f3e2-102">SelectionCondition Element for EntrySelectedBy for Controls for View (Format)</span></span>

<span data-ttu-id="8f3e2-103">Define uma condição que deve existir para que a definição de controle seja usada.</span><span class="sxs-lookup"><span data-stu-id="8f3e2-103">Defines a condition that must exist for the control definition to be used.</span></span> <span data-ttu-id="8f3e2-104">Esse elemento é usado ao definir controles que podem ser usados por uma exibição.</span><span class="sxs-lookup"><span data-stu-id="8f3e2-104">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="8f3e2-105">Elemento de configuração (Format) elemento ViewDefinitions (Format) exibir elemento (Format) controle elemento (Format) elemento Control para controles para o elemento View (Format) CustomControl para controle para controles para o elemento View (Format) CustomEntries para CustomControl para controles para o elemento View (Format) CustomEntry para CustomEntries para controles para o elemento View (Format) EntrySelectedBy para CustomEntry para controles para o elemento View (Format) SelectionCondition para EntrySelectedBy para controles para View ( Ao</span><span class="sxs-lookup"><span data-stu-id="8f3e2-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for Controls for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) EntrySelectedBy Element for CustomEntry for Controls for View (Format) SelectionCondition Element for EntrySelectedBy for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="8f3e2-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="8f3e2-106">Syntax</span></span>

```xml
<SelectionCondition>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</SelectionCondition>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="8f3e2-107">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="8f3e2-107">Attributes and Elements</span></span>

<span data-ttu-id="8f3e2-108">As seções a seguir descrevem atributos, elementos filho e o elemento pai do elemento `SelectionCondition`.</span><span class="sxs-lookup"><span data-stu-id="8f3e2-108">The following sections describe attributes, child elements, and the parent element of the `SelectionCondition` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="8f3e2-109">Atributos</span><span class="sxs-lookup"><span data-stu-id="8f3e2-109">Attributes</span></span>

<span data-ttu-id="8f3e2-110">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="8f3e2-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="8f3e2-111">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="8f3e2-111">Child Elements</span></span>

|<span data-ttu-id="8f3e2-112">Elemento</span><span class="sxs-lookup"><span data-stu-id="8f3e2-112">Element</span></span>|<span data-ttu-id="8f3e2-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="8f3e2-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="8f3e2-114">Elemento PropertyName para SelectionCondition para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="8f3e2-114">PropertyName Element for SelectionCondition for Controls for View (Format)</span></span>](./propertyname-element-for-selectioncondition-for-controls-for-view-format.md)|<span data-ttu-id="8f3e2-115">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="8f3e2-115">Optional element.</span></span><br /><br /> <span data-ttu-id="8f3e2-116">Especifica uma propriedade .NET que dispara a condição.</span><span class="sxs-lookup"><span data-stu-id="8f3e2-116">Specifies a .NET property that triggers the condition.</span></span>|
|[<span data-ttu-id="8f3e2-117">Elemento ScriptBlock para SelectionCondition para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="8f3e2-117">ScriptBlock Element for SelectionCondition for Controls for View (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-controls-for-view-format.md)|<span data-ttu-id="8f3e2-118">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="8f3e2-118">Optional element.</span></span><br /><br /> <span data-ttu-id="8f3e2-119">Especifica o script que dispara a condição.</span><span class="sxs-lookup"><span data-stu-id="8f3e2-119">Specifies the script that triggers the condition.</span></span>|
|[<span data-ttu-id="8f3e2-120">Elemento SelectionSetName para SelectionCondition para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="8f3e2-120">SelectionSetName Element for SelectionCondition for Controls for View (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-controls-for-view-format.md)|<span data-ttu-id="8f3e2-121">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="8f3e2-121">Optional element.</span></span><br /><br /> <span data-ttu-id="8f3e2-122">Especifica o conjunto de tipos .NET que dispara a condição.</span><span class="sxs-lookup"><span data-stu-id="8f3e2-122">Specifies the set of .NET types that triggers the condition.</span></span>|
|[<span data-ttu-id="8f3e2-123">Elemento TypeName para SelectionCondition para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="8f3e2-123">TypeName Element for SelectionCondition for Controls for View (Format)</span></span>](./typename-element-for-selectioncondition-for-controls-for-view-format.md)|<span data-ttu-id="8f3e2-124">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="8f3e2-124">Optional element.</span></span><br /><br /> <span data-ttu-id="8f3e2-125">Especifica um tipo .NET que dispara a condição.</span><span class="sxs-lookup"><span data-stu-id="8f3e2-125">Specifies a .NET type that triggers the condition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="8f3e2-126">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="8f3e2-126">Parent Elements</span></span>

|<span data-ttu-id="8f3e2-127">Elemento</span><span class="sxs-lookup"><span data-stu-id="8f3e2-127">Element</span></span>|<span data-ttu-id="8f3e2-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="8f3e2-128">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="8f3e2-129">Elemento EntrySelectedBy para CustomEntry para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="8f3e2-129">EntrySelectedBy Element for CustomEntry for Controls for View (Format)</span></span>](./entryselectedby-element-for-customentry-for-controls-for-view-format.md)|<span data-ttu-id="8f3e2-130">Define os tipos .NET que usam essa definição de controle ou a condição que deve existir para que essa definição seja usada.</span><span class="sxs-lookup"><span data-stu-id="8f3e2-130">Defines the .NET types that use this control definition or the condition that must exist for this definition to be used.</span></span>|

## <a name="remarks"></a><span data-ttu-id="8f3e2-131">Comentários</span><span class="sxs-lookup"><span data-stu-id="8f3e2-131">Remarks</span></span>

<span data-ttu-id="8f3e2-132">Quando você está definindo uma condição de seleção, os seguintes requisitos se aplicam:</span><span class="sxs-lookup"><span data-stu-id="8f3e2-132">When you are defining a selection condition, the following requirements apply:</span></span>

- <span data-ttu-id="8f3e2-133">A condição de seleção deve especificar pelo menos um nome de propriedade ou um bloco de script, mas não pode especificar ambos.</span><span class="sxs-lookup"><span data-stu-id="8f3e2-133">The selection condition must specify a least one property name or a script block, but cannot specify both.</span></span>

- <span data-ttu-id="8f3e2-134">A condição de seleção pode especificar qualquer número de tipos .NET ou conjuntos de seleção, mas não pode especificar ambos.</span><span class="sxs-lookup"><span data-stu-id="8f3e2-134">The selection condition can specify any number of .NET types or selection sets, but cannot specify both.</span></span>

<span data-ttu-id="8f3e2-135">Para obter mais informações sobre como usar condições de seleção, consulte [definindo condições para quando os dados são exibidos](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="8f3e2-135">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="8f3e2-136">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="8f3e2-136">See Also</span></span>

[<span data-ttu-id="8f3e2-137">Elemento PropertyName para SelectionCondition para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="8f3e2-137">PropertyName Element for SelectionCondition for Controls for View (Format)</span></span>](./propertyname-element-for-selectioncondition-for-controls-for-view-format.md)

[<span data-ttu-id="8f3e2-138">Elemento ScriptBlock para SelectionCondition para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="8f3e2-138">ScriptBlock Element for SelectionCondition for Controls for View (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-controls-for-view-format.md)

[<span data-ttu-id="8f3e2-139">Elemento SelectionSetName para SelectionCondition para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="8f3e2-139">SelectionSetName Element for SelectionCondition for Controls for View (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-controls-for-view-format.md)

[<span data-ttu-id="8f3e2-140">Elemento TypeName para SelectionCondition para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="8f3e2-140">TypeName Element for SelectionCondition for Controls for View (Format)</span></span>](./typename-element-for-selectioncondition-for-controls-for-view-format.md)

[<span data-ttu-id="8f3e2-141">Elemento EntrySelectedBy para CustomEntry para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="8f3e2-141">EntrySelectedBy Element for CustomEntry for Controls for View (Format)</span></span>](./entryselectedby-element-for-customentry-for-controls-for-view-format.md)

[<span data-ttu-id="8f3e2-142">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f3e2-142">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)