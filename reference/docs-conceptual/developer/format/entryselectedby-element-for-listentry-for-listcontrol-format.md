---
title: Elemento EntrySelectedBy para ListEntry para ListControl (Format) | Microsoft Docs
ms.date: 09/13/2016
ms.openlocfilehash: d6ab1c08dd353da74d1a7d27c569d2fa86e083c3
ms.sourcegitcommit: 0907b8c6322d2c7c61b17f8168d53452c8964b41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/05/2020
ms.locfileid: "87774109"
---
# <a name="entryselectedby-element-for-listentry-for-listcontrol-format"></a><span data-ttu-id="b51bb-102">Elemento EntrySelectedBy para ListEntry para ListControl (formato)</span><span class="sxs-lookup"><span data-stu-id="b51bb-102">EntrySelectedBy Element for ListEntry for ListControl (Format)</span></span>

<span data-ttu-id="b51bb-103">Define os tipos .NET que usam essa definição de exibição de lista ou a condição que deve existir para que essa definição seja usada.</span><span class="sxs-lookup"><span data-stu-id="b51bb-103">Defines the .NET types that use this list view definition or the condition that must exist for this definition to be used.</span></span> <span data-ttu-id="b51bb-104">Na maioria dos casos, apenas uma definição é necessária para uma exibição de lista.</span><span class="sxs-lookup"><span data-stu-id="b51bb-104">In most cases only one definition is needed for a list view.</span></span> <span data-ttu-id="b51bb-105">No entanto, você pode fornecer várias definições para o modo de exibição de lista se quiser usar a mesma exibição de lista para exibir dados diferentes para objetos diferentes.</span><span class="sxs-lookup"><span data-stu-id="b51bb-105">However, you can provide multiple definitions for the list view if you want to use the same list view to display different data for different objects.</span></span>

<span data-ttu-id="b51bb-106">Elemento de configuração (Format) elemento ViewDefinitions (Format) View element (Format) ListControl Element (Format) o elemento ListEntries para o elemento ListControl (Format) ListEntry para ListEntry para o elemento ListControl (Format) EntrySelectedBy para ListEntry para ListControl (Format)</span><span class="sxs-lookup"><span data-stu-id="b51bb-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element for ListControl (Format) ListEntry Element for ListEntry for ListControl (Format) EntrySelectedBy Element for ListEntry for ListControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="b51bb-107">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="b51bb-107">Syntax</span></span>

```xml
<EntrySelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <SelectionCondition>...</SelectionCondition>
</EntrySelectedBy>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="b51bb-108">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="b51bb-108">Attributes and Elements</span></span>

<span data-ttu-id="b51bb-109">As seções a seguir descrevem os atributos, os elementos filho e o elemento pai do `EntrySelectedBy` elemento.</span><span class="sxs-lookup"><span data-stu-id="b51bb-109">The following sections describe the attributes, child elements, and the parent element of the `EntrySelectedBy` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="b51bb-110">Atributos</span><span class="sxs-lookup"><span data-stu-id="b51bb-110">Attributes</span></span>

<span data-ttu-id="b51bb-111">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="b51bb-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="b51bb-112">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="b51bb-112">Child Elements</span></span>

|<span data-ttu-id="b51bb-113">Elemento</span><span class="sxs-lookup"><span data-stu-id="b51bb-113">Element</span></span>|<span data-ttu-id="b51bb-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="b51bb-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="b51bb-115">Elemento SelectionCondition para EntrySelectedBy para ListControl (formato)</span><span class="sxs-lookup"><span data-stu-id="b51bb-115">SelectionCondition Element for EntrySelectedBy for ListControl  (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)|<span data-ttu-id="b51bb-116">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="b51bb-116">Optional element.</span></span><br /><br /> <span data-ttu-id="b51bb-117">Define a condição que deve existir para esta definição de exibição de lista ser usada.</span><span class="sxs-lookup"><span data-stu-id="b51bb-117">Defines the condition that must exist for this list view definition to be used.</span></span>|
|[<span data-ttu-id="b51bb-118">Elemento SelectionSetName para EntrySelectedBy para ListControl (formato)</span><span class="sxs-lookup"><span data-stu-id="b51bb-118">SelectionSetName Element for EntrySelectedBy for ListControl (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md)|<span data-ttu-id="b51bb-119">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="b51bb-119">Optional element.</span></span><br /><br /> <span data-ttu-id="b51bb-120">Especifica um conjunto de tipos .NET que usam esta definição de exibição de lista.</span><span class="sxs-lookup"><span data-stu-id="b51bb-120">Specifies a set of .NET types that use this list view definition.</span></span>|
|[<span data-ttu-id="b51bb-121">Elemento TypeName para EntrySelectedBy para ListControl (formato)</span><span class="sxs-lookup"><span data-stu-id="b51bb-121">TypeName Element for EntrySelectedBy for ListControl (Format)</span></span>](./typename-element-for-entryselectedby-for-listcontrol-format.md)|<span data-ttu-id="b51bb-122">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="b51bb-122">Optional element.</span></span><br /><br /> <span data-ttu-id="b51bb-123">Especifica um tipo .NET que usa essa definição de exibição de lista.</span><span class="sxs-lookup"><span data-stu-id="b51bb-123">Specifies a .NET type that uses this list view definition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="b51bb-124">Elementos pai</span><span class="sxs-lookup"><span data-stu-id="b51bb-124">Parent Elements</span></span>

|<span data-ttu-id="b51bb-125">Elemento</span><span class="sxs-lookup"><span data-stu-id="b51bb-125">Element</span></span>|<span data-ttu-id="b51bb-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="b51bb-126">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="b51bb-127">Elemento ListEntry para ListControl (formato)</span><span class="sxs-lookup"><span data-stu-id="b51bb-127">ListEntry Element for ListControl (Format)</span></span>](./listentry-element-for-listcontrol-format.md)|<span data-ttu-id="b51bb-128">Define como as linhas da lista são exibidas.</span><span class="sxs-lookup"><span data-stu-id="b51bb-128">Defines how the rows of the list are displayed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="b51bb-129">Comentários</span><span class="sxs-lookup"><span data-stu-id="b51bb-129">Remarks</span></span>

<span data-ttu-id="b51bb-130">Você deve especificar pelo menos um tipo, um conjunto de seleção ou uma condição de seleção para uma definição de exibição de lista.</span><span class="sxs-lookup"><span data-stu-id="b51bb-130">You must specify at least one type, selection set, or selection condition for a list view definition.</span></span> <span data-ttu-id="b51bb-131">Não há nenhum limite máximo para o número de elementos filho que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="b51bb-131">There is no maximum limit to the number of child elements that you can use.</span></span>

<span data-ttu-id="b51bb-132">As condições de seleção são usadas para definir uma condição que deve existir para que a definição seja usada, como quando um objeto tem uma propriedade específica ou que um valor de propriedade ou script específico é avaliado como `true` .</span><span class="sxs-lookup"><span data-stu-id="b51bb-132">Selection conditions are used to define a condition that must exist for the definition to be used, such as when an object has a specific property or that a specific property value or script evaluates to `true`.</span></span> <span data-ttu-id="b51bb-133">Para obter mais informações sobre condições de seleção, consulte [definindo condições para quando os dados são exibidos](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="b51bb-133">For more information about selection conditions, see [Defining Conditions for when Data is displayed](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="b51bb-134">Para obter mais informações sobre os componentes de um modo de exibição de lista, consulte [criando uma exibição de lista](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="b51bb-134">For more information about the components of a list view, see [Creating a List View](./creating-a-list-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="b51bb-135">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b51bb-135">Example</span></span>

<span data-ttu-id="b51bb-136">O exemplo a seguir mostra como definir os objetos para um modo de exibição de lista usando o nome do tipo .NET.</span><span class="sxs-lookup"><span data-stu-id="b51bb-136">The following example shows how to define the objects for a list view using their .NET type name.</span></span>

```xml
<ListEntry>
  <EntrySelectedBy>
    <TypeName>NameofDotNetType</TypeName>>
  </EntrySelectedBy>
</ListEntry>
```

## <a name="see-also"></a><span data-ttu-id="b51bb-137">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="b51bb-137">See Also</span></span>

[<span data-ttu-id="b51bb-138">Elemento ListEntry para ListControl (formato)</span><span class="sxs-lookup"><span data-stu-id="b51bb-138">ListEntry Element for ListControl (Format)</span></span>](./listentry-element-for-listcontrol-format.md)

[<span data-ttu-id="b51bb-139">Elemento SelectionCondition para EntrySelectedBy para ListControl (formato)</span><span class="sxs-lookup"><span data-stu-id="b51bb-139">SelectionCondition Element for EntrySelectedBy for ListControl (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)

[<span data-ttu-id="b51bb-140">Elemento SelectionSetName para EntrySelectedBy para ListControl (formato)</span><span class="sxs-lookup"><span data-stu-id="b51bb-140">SelectionSetName Element for EntrySelectedBy for ListControl (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md)

[<span data-ttu-id="b51bb-141">Elemento TypeName para EntrySelectedBy para ListControl (formato)</span><span class="sxs-lookup"><span data-stu-id="b51bb-141">TypeName Element for EntrySelectedBy for ListControl (Format)</span></span>](./typename-element-for-entryselectedby-for-listcontrol-format.md)

[<span data-ttu-id="b51bb-142">Criar uma exibição de lista</span><span class="sxs-lookup"><span data-stu-id="b51bb-142">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="b51bb-143">Definindo condições para quando os dados são exibidos</span><span class="sxs-lookup"><span data-stu-id="b51bb-143">Defining Conditions for when Data is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="b51bb-144">Escrever um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="b51bb-144">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
