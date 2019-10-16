---
title: Elemento SelectionSetName para EntrySelectedBy para WideControl (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c9c6e18f-6cca-465c-bd20-3969e7897a96
caps.latest.revision: 10
ms.openlocfilehash: 6b6a4a4647412d11d947f1dc4ea12d1e05ff536e
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72361975"
---
# <a name="selectionsetname-element-for-entryselectedby-for-widecontrol-format"></a><span data-ttu-id="d84ed-102">Elemento SelectionSetName para EntrySelectedBy para WideControl (formato)</span><span class="sxs-lookup"><span data-stu-id="d84ed-102">SelectionSetName Element for EntrySelectedBy for WideControl (Format)</span></span>

<span data-ttu-id="d84ed-103">Especifica um conjunto de objetos .NET para a definição.</span><span class="sxs-lookup"><span data-stu-id="d84ed-103">Specifies a set of .NET objects for the definition.</span></span> <span data-ttu-id="d84ed-104">A definição é usada sempre que um desses objetos é exibido.</span><span class="sxs-lookup"><span data-stu-id="d84ed-104">The definition is used whenever one of these objects is displayed.</span></span>

<span data-ttu-id="d84ed-105">Elemento de configuração (Format) elemento ViewDefinitions (Format) View element (Format) WideControl elemento (Format) WideEntries Element (Format) WideEntry elemento (Format) EntrySelectedBy Element para WideEntry (Format) SelectionSetName Element para EntrySelectedBy para WideEntry (formato)</span><span class="sxs-lookup"><span data-stu-id="d84ed-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element (Format) EntrySelectedBy Element for WideEntry (Format) SelectionSetName Element for EntrySelectedBy for WideEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="d84ed-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="d84ed-106">Syntax</span></span>

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="d84ed-107">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="d84ed-107">Attributes and Elements</span></span>

<span data-ttu-id="d84ed-108">As seções a seguir descrevem os atributos, os elementos filho e o elemento pai do elemento `SelectionSetName`.</span><span class="sxs-lookup"><span data-stu-id="d84ed-108">The following sections describe the attributes, child elements, and the parent element of the `SelectionSetName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="d84ed-109">Atributos</span><span class="sxs-lookup"><span data-stu-id="d84ed-109">Attributes</span></span>

<span data-ttu-id="d84ed-110">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="d84ed-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="d84ed-111">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="d84ed-111">Child Elements</span></span>

<span data-ttu-id="d84ed-112">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="d84ed-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="d84ed-113">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="d84ed-113">Parent Elements</span></span>

|<span data-ttu-id="d84ed-114">Elemento</span><span class="sxs-lookup"><span data-stu-id="d84ed-114">Element</span></span>|<span data-ttu-id="d84ed-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="d84ed-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="d84ed-116">Elemento EntrySelectedBy para WideEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="d84ed-116">EntrySelectedBy Element for WideEntry (Format)</span></span>](./entryselectedby-element-for-wideentry-format.md)|<span data-ttu-id="d84ed-117">Define os tipos .NET que usam essa entrada ampla ou a condição que deve existir para que essa entrada seja usada.</span><span class="sxs-lookup"><span data-stu-id="d84ed-117">Defines the .NET types that use this wide entry or the condition that must exist for this entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="d84ed-118">Valor de texto</span><span class="sxs-lookup"><span data-stu-id="d84ed-118">Text Value</span></span>

<span data-ttu-id="d84ed-119">Especifique o nome do conjunto de seleção.</span><span class="sxs-lookup"><span data-stu-id="d84ed-119">Specify the name of the selection set.</span></span>

## <a name="remarks"></a><span data-ttu-id="d84ed-120">Comentários</span><span class="sxs-lookup"><span data-stu-id="d84ed-120">Remarks</span></span>

<span data-ttu-id="d84ed-121">Cada definição deve especificar um nome de tipo, um conjunto de seleção ou uma condição de seleção.</span><span class="sxs-lookup"><span data-stu-id="d84ed-121">Each definition must specify one type name, selection set, or selection condition.</span></span>

<span data-ttu-id="d84ed-122">Os conjuntos de seleção são normalmente usados quando você deseja definir um grupo de objetos que são usados em várias exibições.</span><span class="sxs-lookup"><span data-stu-id="d84ed-122">Selection sets are typically used when you want to define a group of objects that are used in multiple views.</span></span> <span data-ttu-id="d84ed-123">Por exemplo, talvez você queira criar uma exibição de tabela e uma exibição de lista para o mesmo conjunto de objetos.</span><span class="sxs-lookup"><span data-stu-id="d84ed-123">For example, you might want to create a table view and a list view for the same set of objects.</span></span> <span data-ttu-id="d84ed-124">Para obter mais informações sobre como definir conjuntos de seleção, consulte [definindo conjuntos de objetos para uma exibição](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="d84ed-124">For more information about defining selection sets, see [Defining Sets of Objects for a View](./defining-selection-sets.md).</span></span>

<span data-ttu-id="d84ed-125">Para obter mais informações sobre outros componentes de uma exibição ampla, consulte [criando uma exibição ampla](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="d84ed-125">For more information about other components of a wide view, see [Creating a Wide View](./creating-a-wide-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="d84ed-126">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="d84ed-126">See Also</span></span>

[<span data-ttu-id="d84ed-127">Criando uma exibição ampla</span><span class="sxs-lookup"><span data-stu-id="d84ed-127">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="d84ed-128">Definindo conjuntos de seleção</span><span class="sxs-lookup"><span data-stu-id="d84ed-128">Defining Selection Sets</span></span>](./defining-selection-sets.md)

[<span data-ttu-id="d84ed-129">Elemento EntrySelectedBy para WideEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="d84ed-129">EntrySelectedBy Element for WideEntry (Format)</span></span>](./entryselectedby-element-for-wideentry-format.md)

[<span data-ttu-id="d84ed-130">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="d84ed-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
