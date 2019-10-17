---
title: Elemento SelectionSetName para SelectionCondition para EntrySelectedBy para WideEntry (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a13a429c-a31b-4e29-828c-c0c0917b5415
caps.latest.revision: 11
ms.openlocfilehash: baea89e4b259611dfa45b6bcf94fa0bf2df6b9de
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72368405"
---
# <a name="selectionsetname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format"></a><span data-ttu-id="b844e-102">Elemento SelectionSetName para SelectionCondition para EntrySelectedBy para WideEntry (formato)</span><span class="sxs-lookup"><span data-stu-id="b844e-102">SelectionSetName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>

<span data-ttu-id="b844e-103">Especifica o conjunto de tipos .NET que disparam a condição.</span><span class="sxs-lookup"><span data-stu-id="b844e-103">Specifies the set of .NET types that trigger the condition.</span></span> <span data-ttu-id="b844e-104">Quando qualquer um dos tipos nesse conjunto estiver presente, a condição será atendida e o objeto será exibido usando essa definição da exibição ampla.</span><span class="sxs-lookup"><span data-stu-id="b844e-104">When any of the types in this set are present, the condition is met, and the object is displayed by using this definition of the wide view.</span></span>

<span data-ttu-id="b844e-105">Elemento de configuração (Format) elemento ViewDefinitions (Format) View element (Format) WideControl elemento (Format) WideEntries Element (Format) WideEntry elemento (Format) EntrySelectedBy Element para WideEntry (Format) SelectionCondition Element para EntrySelectedBy para WideEntry (Format) SelectionSetName elemento para SelectionCondition para EntrySelectedBy para WideEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="b844e-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element (Format) EntrySelectedBy Element for WideEntry (Format) SelectionCondition Element for EntrySelectedBy for WideEntry (Format) SelectionSetName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="b844e-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="b844e-106">Syntax</span></span>

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="b844e-107">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="b844e-107">Attributes and Elements</span></span>

<span data-ttu-id="b844e-108">As seções a seguir descrevem atributos, elementos filho e o elemento pai do elemento `SelectionSetName`.</span><span class="sxs-lookup"><span data-stu-id="b844e-108">The following sections describe attributes, child elements, and the parent element of the `SelectionSetName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="b844e-109">Atributos</span><span class="sxs-lookup"><span data-stu-id="b844e-109">Attributes</span></span>

<span data-ttu-id="b844e-110">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="b844e-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="b844e-111">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="b844e-111">Child Elements</span></span>

<span data-ttu-id="b844e-112">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="b844e-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="b844e-113">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="b844e-113">Parent Elements</span></span>

|<span data-ttu-id="b844e-114">Elemento</span><span class="sxs-lookup"><span data-stu-id="b844e-114">Element</span></span>|<span data-ttu-id="b844e-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="b844e-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="b844e-116">Elemento SelectionCondition para EntrySelectedBy para WideEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="b844e-116">SelectionCondition Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)|<span data-ttu-id="b844e-117">Define a condição que deve existir para que essa definição seja usada.</span><span class="sxs-lookup"><span data-stu-id="b844e-117">Defines the condition that must exist for this definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="b844e-118">Valor de texto</span><span class="sxs-lookup"><span data-stu-id="b844e-118">Text Value</span></span>

<span data-ttu-id="b844e-119">Especifique o nome do conjunto de seleção.</span><span class="sxs-lookup"><span data-stu-id="b844e-119">Specify the name of the selection set.</span></span>

## <a name="remarks"></a><span data-ttu-id="b844e-120">Comentários</span><span class="sxs-lookup"><span data-stu-id="b844e-120">Remarks</span></span>

<span data-ttu-id="b844e-121">A condição de seleção pode especificar um conjunto de seleção ou um tipo .NET, mas não pode especificar ambos.</span><span class="sxs-lookup"><span data-stu-id="b844e-121">The selection condition can specify a selection set or .NET type, but cannot specify both.</span></span> <span data-ttu-id="b844e-122">Para obter mais informações sobre como usar condições de seleção, consulte [definindo condições para quando os dados são exibidos](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="b844e-122">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="b844e-123">Os conjuntos de seleção são grupos comuns de objetos .NET que podem ser usados por qualquer exibição que o arquivo de formatação define.</span><span class="sxs-lookup"><span data-stu-id="b844e-123">Selection sets are common groups of .NET objects that can be used by any view that the formatting file defines.</span></span> <span data-ttu-id="b844e-124">Para obter mais informações sobre como criar e referenciar conjuntos de seleção, consulte [definindo conjuntos de objetos](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="b844e-124">For more information about creating and referencing selection sets, see [Defining Sets of Objects](./defining-selection-sets.md).</span></span>

<span data-ttu-id="b844e-125">Para obter mais informações sobre outros componentes de uma exibição ampla, consulte [criando uma exibição ampla](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="b844e-125">For more information about other components of a wide view, see [Creating a Wide View](./creating-a-wide-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="b844e-126">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="b844e-126">See Also</span></span>

[<span data-ttu-id="b844e-127">Criando uma exibição ampla</span><span class="sxs-lookup"><span data-stu-id="b844e-127">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="b844e-128">Definindo condições para quando os dados são exibidos</span><span class="sxs-lookup"><span data-stu-id="b844e-128">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="b844e-129">Definindo conjuntos de seleção</span><span class="sxs-lookup"><span data-stu-id="b844e-129">Defining Selection Sets</span></span>](./defining-selection-sets.md)

[<span data-ttu-id="b844e-130">Elemento SelectionCondition para EntrySelectedBy para WideEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="b844e-130">SelectionCondition Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)

[<span data-ttu-id="b844e-131">Elemento TypeName para SelectionCondition para EntrySelectedBy para WideEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="b844e-131">TypeName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>](./typename-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format.md)

[<span data-ttu-id="b844e-132">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="b844e-132">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)