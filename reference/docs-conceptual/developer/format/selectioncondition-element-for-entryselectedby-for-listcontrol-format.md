---
title: Elemento SelectionCondition para EntrySelectedBy para ListControl (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7649d5d0-2b56-49b5-a670-dde46caca343
caps.latest.revision: 11
ms.openlocfilehash: 7150b29ad84dfb587215ee3e64c356adbd5a6305
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "74417545"
---
# <a name="selectioncondition-element-for-entryselectedby-for-listcontrol-format"></a><span data-ttu-id="6a8d5-102">Elemento SelectionCondition para EntrySelectedBy para ListControl (formato)</span><span class="sxs-lookup"><span data-stu-id="6a8d5-102">SelectionCondition Element for EntrySelectedBy for ListControl (Format)</span></span>

<span data-ttu-id="6a8d5-103">Define a condição que deve existir para usar essa definição da exibição de lista.</span><span class="sxs-lookup"><span data-stu-id="6a8d5-103">Defines the condition that must exist to use this definition of the list view.</span></span> <span data-ttu-id="6a8d5-104">Não há nenhum limite para o número de condições de seleção que podem ser especificadas para uma definição de lista.</span><span class="sxs-lookup"><span data-stu-id="6a8d5-104">There is no limit to the number of selection conditions that can be specified for a list definition.</span></span>

<span data-ttu-id="6a8d5-105">Elemento de configuração (Format) elemento ViewDefinitions (Format) View element (Format) ListControl elemento (Format) ListEntries Element (Format) o elemento ListEntry (Format) o elemento EntrySelectedBy para o elemento ListEntry (Format) SelectionCondition para EntrySelectedBy para ListEntry (formato)</span><span class="sxs-lookup"><span data-stu-id="6a8d5-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element (Format) ListEntry Element (Format) EntrySelectedBy Element for ListEntry (Format) SelectionCondition Element for EntrySelectedBy for ListEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="6a8d5-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="6a8d5-106">Syntax</span></span>

```xml
<SelectionCondition>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</SelectionCondition>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="6a8d5-107">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="6a8d5-107">Attributes and Elements</span></span>

<span data-ttu-id="6a8d5-108">As seções a seguir descrevem atributos, elementos filho e o elemento pai do elemento `SelectionCondition`.</span><span class="sxs-lookup"><span data-stu-id="6a8d5-108">The following sections describe attributes, child elements, and the parent element of the `SelectionCondition` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="6a8d5-109">Atributos</span><span class="sxs-lookup"><span data-stu-id="6a8d5-109">Attributes</span></span>

<span data-ttu-id="6a8d5-110">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="6a8d5-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="6a8d5-111">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="6a8d5-111">Child Elements</span></span>

|<span data-ttu-id="6a8d5-112">Elemento</span><span class="sxs-lookup"><span data-stu-id="6a8d5-112">Element</span></span>|<span data-ttu-id="6a8d5-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="6a8d5-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="6a8d5-114">Elemento PropertyName para SelectionCondition para EntrySelectedBy para ListEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="6a8d5-114">PropertyName Element for SelectionCondition for EntrySelectedBy for ListEntry (Format)</span></span>](./propertyname-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format.md)|<span data-ttu-id="6a8d5-115">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="6a8d5-115">Optional element.</span></span><br /><br /> <span data-ttu-id="6a8d5-116">Especifica a propriedade .NET que dispara a condição.</span><span class="sxs-lookup"><span data-stu-id="6a8d5-116">Specifies the .NET property that triggers the condition.</span></span>|
|[<span data-ttu-id="6a8d5-117">Elemento ScriptBlock para SelectionCondition para EntrySelectedBy para ListEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="6a8d5-117">ScriptBlock Element for SelectionCondition for EntrySelectedBy for ListEntry (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format.md)|<span data-ttu-id="6a8d5-118">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="6a8d5-118">Optional element.</span></span><br /><br /> <span data-ttu-id="6a8d5-119">Especifica o script que dispara a condição.</span><span class="sxs-lookup"><span data-stu-id="6a8d5-119">Specifies the script that triggers the condition.</span></span>|
|[<span data-ttu-id="6a8d5-120">Elemento SelectionSetName para SelectionCondition para EntrySelectedBy para ListEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="6a8d5-120">SelectionSetName Element for SelectionCondition for EntrySelectedBy for ListEntry (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-listentry-format.md)|<span data-ttu-id="6a8d5-121">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="6a8d5-121">Optional element.</span></span><br /><br /> <span data-ttu-id="6a8d5-122">Especifica o conjunto de tipos .NET que disparam a condição.</span><span class="sxs-lookup"><span data-stu-id="6a8d5-122">Specifies the set of .NET types that trigger the condition.</span></span>|
|[<span data-ttu-id="6a8d5-123">Elemento TypeName para SelectionCondition para EntrySelectedBy para ListEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="6a8d5-123">TypeName Element for SelectionCondition for EntrySelectedBy for ListEntry (Format)</span></span>](./typename-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format.md)|<span data-ttu-id="6a8d5-124">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="6a8d5-124">Optional element.</span></span><br /><br /> <span data-ttu-id="6a8d5-125">Especifica um tipo .NET que dispara a condição.</span><span class="sxs-lookup"><span data-stu-id="6a8d5-125">Specifies a .NET type that triggers the condition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="6a8d5-126">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="6a8d5-126">Parent Elements</span></span>

|<span data-ttu-id="6a8d5-127">Elemento</span><span class="sxs-lookup"><span data-stu-id="6a8d5-127">Element</span></span>|<span data-ttu-id="6a8d5-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="6a8d5-128">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="6a8d5-129">Elemento EntrySelectedBy para TableRowEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="6a8d5-129">EntrySelectedBy Element for TableRowEntry (Format)</span></span>](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)|<span data-ttu-id="6a8d5-130">Define os tipos .NET que usam essa entrada de tabela ou a condição que deve existir para que essa entrada seja usada.</span><span class="sxs-lookup"><span data-stu-id="6a8d5-130">Defines the .NET types that use this table entry or the condition that must exist for this entry to be used.</span></span>|

## <a name="remarks"></a><span data-ttu-id="6a8d5-131">Comentários</span><span class="sxs-lookup"><span data-stu-id="6a8d5-131">Remarks</span></span>

<span data-ttu-id="6a8d5-132">lWhen você está definindo uma condição de seleção, os seguintes requisitos se aplicam:</span><span class="sxs-lookup"><span data-stu-id="6a8d5-132">lWhen you are defining a selection condition, the following requirements apply:</span></span>

- <span data-ttu-id="6a8d5-133">A condição de seleção deve especificar pelo menos um nome de propriedade ou um bloco de script, mas não pode especificar ambos.</span><span class="sxs-lookup"><span data-stu-id="6a8d5-133">The selection condition must specify a least one property name or a script block, but cannot specify both.</span></span>

- <span data-ttu-id="6a8d5-134">A condição de seleção pode especificar qualquer número de tipos .NET ou conjuntos de seleção, mas não pode especificar ambos.</span><span class="sxs-lookup"><span data-stu-id="6a8d5-134">The selection condition can specify any number of .NET types or selection sets, but cannot specify both.</span></span>

<span data-ttu-id="6a8d5-135">Para obter mais informações sobre como usar condições de seleção, consulte [definindo condições para quando os dados são exibidos](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="6a8d5-135">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="6a8d5-136">Para obter mais informações sobre outros componentes de um modo de exibição de lista, consulte [criando uma exibição de lista](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="6a8d5-136">For more information about other components of a list view, see [Creating a List View](./creating-a-list-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="6a8d5-137">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="6a8d5-137">See Also</span></span>

[<span data-ttu-id="6a8d5-138">Criando um modo de exibição de lista</span><span class="sxs-lookup"><span data-stu-id="6a8d5-138">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="6a8d5-139">Definindo condições para quando os dados são exibidos</span><span class="sxs-lookup"><span data-stu-id="6a8d5-139">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="6a8d5-140">Elemento ListEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="6a8d5-140">ListEntry Element (Format)</span></span>](./listentry-element-for-listcontrol-format.md)

[<span data-ttu-id="6a8d5-141">Elemento SelectionSetName para EntrySelectedBy para ListEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="6a8d5-141">SelectionSetName Element for EntrySelectedBy for ListEntry (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md)

[<span data-ttu-id="6a8d5-142">Elemento TypeName para EntrySelectedBy para ListEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="6a8d5-142">TypeName Element for EntrySelectedBy for ListEntry (Format)</span></span>](/powershell/scripting/developer/format/typename-element-for-entryselectedby-for-listcontrol-format)

[<span data-ttu-id="6a8d5-143">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="6a8d5-143">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
