---
title: Elemento ViewSelectedBy (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: acdeef4d-3554-4f39-a7e6-a684e3848fd7
caps.latest.revision: 19
ms.openlocfilehash: efc1c5d1338889ecd0be7150b7733842ce78979e
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72367965"
---
# <a name="viewselectedby-element-format"></a><span data-ttu-id="7986e-102">Elemento ViewSelectedBy (formato)</span><span class="sxs-lookup"><span data-stu-id="7986e-102">ViewSelectedBy Element (Format)</span></span>

<span data-ttu-id="7986e-103">Define os objetos .NET que são exibidos pela exibição.</span><span class="sxs-lookup"><span data-stu-id="7986e-103">Defines the .NET objects that are displayed by the view.</span></span> <span data-ttu-id="7986e-104">Cada exibição deve especificar pelo menos um objeto .NET.</span><span class="sxs-lookup"><span data-stu-id="7986e-104">Each view must specify at least one .NET object.</span></span>

<span data-ttu-id="7986e-105">Elemento ViewDefinitions (Format) View element (Format) ViewSelectedBy elemento (Format)</span><span class="sxs-lookup"><span data-stu-id="7986e-105">ViewDefinitions Element (Format) View Element (Format) ViewSelectedBy Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="7986e-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="7986e-106">Syntax</span></span>

```xml
<ViewSelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>SelectionSet</SelectionSetName>
</ViewSelectedBy>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="7986e-107">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="7986e-107">Attributes and Elements</span></span>

<span data-ttu-id="7986e-108">As seções a seguir descrevem os atributos, os elementos filho e o elemento pai do elemento `ViewSelectedBy`.</span><span class="sxs-lookup"><span data-stu-id="7986e-108">The following sections describe the attributes, child elements, and parent element of the `ViewSelectedBy` element.</span></span> <span data-ttu-id="7986e-109">Esse elemento deve conter pelo menos um elemento filho `TypeName` ou `SelectionSetName`.</span><span class="sxs-lookup"><span data-stu-id="7986e-109">This element must contain at least one `TypeName` or `SelectionSetName` child element.</span></span> <span data-ttu-id="7986e-110">Não há nenhum limite para o número de elementos filho que podem ser especificados, nem sua ordem significativa.</span><span class="sxs-lookup"><span data-stu-id="7986e-110">There is no limit to the number of child elements that can be specified nor is their order significant.</span></span>

### <a name="attributes"></a><span data-ttu-id="7986e-111">Atributos</span><span class="sxs-lookup"><span data-stu-id="7986e-111">Attributes</span></span>

<span data-ttu-id="7986e-112">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="7986e-112">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="7986e-113">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="7986e-113">Child Elements</span></span>

|<span data-ttu-id="7986e-114">Elemento</span><span class="sxs-lookup"><span data-stu-id="7986e-114">Element</span></span>|<span data-ttu-id="7986e-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="7986e-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="7986e-116">Elemento TypeName para ViewSelectedBy (Format)</span><span class="sxs-lookup"><span data-stu-id="7986e-116">TypeName Element for ViewSelectedBy (Format)</span></span>](./typename-element-for-viewselectedby-format.md)|<span data-ttu-id="7986e-117">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="7986e-117">Optional element.</span></span><br /><br /> <span data-ttu-id="7986e-118">Especifica um objeto .NET que é exibido pela exibição.</span><span class="sxs-lookup"><span data-stu-id="7986e-118">Specifies a .NET object that is displayed by the view.</span></span>|
|[<span data-ttu-id="7986e-119">Elemento SelectionSetName para ViewSelectedBy (Format)</span><span class="sxs-lookup"><span data-stu-id="7986e-119">SelectionSetName Element for ViewSelectedBy (Format)</span></span>](./selectionsetname-element-for-viewselectedby-format.md)|<span data-ttu-id="7986e-120">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="7986e-120">Optional element.</span></span><br /><br /> <span data-ttu-id="7986e-121">Especifica um conjunto de objetos .NET que são exibidos pela exibição.</span><span class="sxs-lookup"><span data-stu-id="7986e-121">Specifies a set of .NET objects that are displayed by the view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="7986e-122">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="7986e-122">Parent Elements</span></span>

|<span data-ttu-id="7986e-123">Elemento</span><span class="sxs-lookup"><span data-stu-id="7986e-123">Element</span></span>|<span data-ttu-id="7986e-124">Descrição</span><span class="sxs-lookup"><span data-stu-id="7986e-124">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="7986e-125">Elemento View (formato)</span><span class="sxs-lookup"><span data-stu-id="7986e-125">View Element (Format)</span></span>](./view-element-format.md)|<span data-ttu-id="7986e-126">Define uma exibição que exibe um ou mais objetos .NET.</span><span class="sxs-lookup"><span data-stu-id="7986e-126">Defines a view that displays one or more .NET objects.</span></span>|

## <a name="remarks"></a><span data-ttu-id="7986e-127">Comentários</span><span class="sxs-lookup"><span data-stu-id="7986e-127">Remarks</span></span>

<span data-ttu-id="7986e-128">Para obter mais informações sobre como esse elemento é usado em diferentes exibições, consulte [componentes de exibição de tabela](./creating-a-table-view.md), componentes de exibição de [lista](./creating-a-list-view.md), [componentes de exibição ampla](./creating-a-wide-view.md)e [componentes de controle personalizado](./creating-custom-controls.md).</span><span class="sxs-lookup"><span data-stu-id="7986e-128">For more information about how this element is used in different views, see [Table View Components](./creating-a-table-view.md), [List View Components](./creating-a-list-view.md), [Wide View Components](./creating-a-wide-view.md), and [Custom Control Components](./creating-custom-controls.md).</span></span>

<span data-ttu-id="7986e-129">O elemento `SelectionSetName` é usado quando o arquivo de formatação define um conjunto de objetos que são exibidos por vários modos de exibição.</span><span class="sxs-lookup"><span data-stu-id="7986e-129">The `SelectionSetName` element is used when the formatting file defines a set of objects that are displayed by multiple views.</span></span> <span data-ttu-id="7986e-130">Para obter mais informações sobre como os conjuntos de seleção são definidos e referenciados, consulte [definindo conjuntos de objetos](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="7986e-130">For more information about how selection sets are defined and referenced, see [Defining Sets of Objects](./defining-selection-sets.md).</span></span>

## <a name="example"></a><span data-ttu-id="7986e-131">Exemplo</span><span class="sxs-lookup"><span data-stu-id="7986e-131">Example</span></span>

<span data-ttu-id="7986e-132">O exemplo a seguir mostra como especificar o objeto [System. ServiceProcess. ServiceController](/dotnet/api/System.ServiceProcess.ServiceController) para uma exibição de lista.</span><span class="sxs-lookup"><span data-stu-id="7986e-132">The following example shows how to specify the [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) object for a list view.</span></span> <span data-ttu-id="7986e-133">O mesmo esquema é usado para exibições de tabela, ampla e personalizadas.</span><span class="sxs-lookup"><span data-stu-id="7986e-133">The same schema is used for table, wide, and custom views.</span></span>

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <ListControl>...</ListControl>
</View>
```

## <a name="see-also"></a><span data-ttu-id="7986e-134">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="7986e-134">See Also</span></span>

[<span data-ttu-id="7986e-135">Criando um modo de exibição de lista</span><span class="sxs-lookup"><span data-stu-id="7986e-135">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="7986e-136">Criando uma exibição de tabela</span><span class="sxs-lookup"><span data-stu-id="7986e-136">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="7986e-137">Criando uma exibição ampla</span><span class="sxs-lookup"><span data-stu-id="7986e-137">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="7986e-138">Criando controles personalizados</span><span class="sxs-lookup"><span data-stu-id="7986e-138">Creating Custom Controls</span></span>](./creating-custom-controls.md)

[<span data-ttu-id="7986e-139">Definindo conjuntos de seleção</span><span class="sxs-lookup"><span data-stu-id="7986e-139">Defining Selection Sets</span></span>](./defining-selection-sets.md)

[<span data-ttu-id="7986e-140">Elemento SelectionSetName para ViewSelectedBy (Format)</span><span class="sxs-lookup"><span data-stu-id="7986e-140">SelectionSetName Element for ViewSelectedBy (Format)</span></span>](./selectionsetname-element-for-viewselectedby-format.md)

[<span data-ttu-id="7986e-141">Elemento TypeName (formato)</span><span class="sxs-lookup"><span data-stu-id="7986e-141">TypeName Element (Format)</span></span>](./typename-element-for-viewselectedby-format.md)

[<span data-ttu-id="7986e-142">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="7986e-142">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)