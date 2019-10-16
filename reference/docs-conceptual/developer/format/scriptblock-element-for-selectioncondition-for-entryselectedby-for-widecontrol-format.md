---
title: Elemento ScriptBlock para SelectionCondition para EntrySelectedBy para WideControl (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5ec68309-7826-4643-a521-e29c996663fb
caps.latest.revision: 11
ms.openlocfilehash: 649a978e21e9421a3f3e953261e1d309e23c3f9c
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72368555"
---
# <a name="scriptblock-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format"></a><span data-ttu-id="744d8-102">Elemento ScriptBlock para SelectionCondition para EntrySelectedBy para WideControl (formato)</span><span class="sxs-lookup"><span data-stu-id="744d8-102">ScriptBlock Element for SelectionCondition for EntrySelectedBy for WideControl (Format)</span></span>

<span data-ttu-id="744d8-103">Especifica o script que dispara a condição.</span><span class="sxs-lookup"><span data-stu-id="744d8-103">Specifies the script that triggers the condition.</span></span> <span data-ttu-id="744d8-104">Quando esse script é avaliado como `true`, a condição é atendida e a definição de entrada larga é usada.</span><span class="sxs-lookup"><span data-stu-id="744d8-104">When this script is evaluated to `true`, the condition is met, and the wide entry definition is used.</span></span>

<span data-ttu-id="744d8-105">Elemento de configuração (Format) elemento ViewDefinitions (Format) View element (Format) WideControl elemento (Format) WideEntries Element (Format) WideEntry elemento (Format) EntrySelectedBy Element para WideEntry (Format) SelectionCondition Element para EntrySelectedBy para o elemento ScriptBlock WideEntry (Format) para SelectionCondition para EntrySelectedBy para WideEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="744d8-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element (Format) EntrySelectedBy Element for WideEntry (Format) SelectionCondition Element for EntrySelectedBy for WideEntry (Format) ScriptBlock Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="744d8-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="744d8-106">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="744d8-107">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="744d8-107">Attributes and Elements</span></span>

<span data-ttu-id="744d8-108">As seções a seguir descrevem atributos, elementos filho e o elemento pai do elemento `ScriptBlock`.</span><span class="sxs-lookup"><span data-stu-id="744d8-108">The following sections describe attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="744d8-109">Atributos</span><span class="sxs-lookup"><span data-stu-id="744d8-109">Attributes</span></span>

<span data-ttu-id="744d8-110">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="744d8-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="744d8-111">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="744d8-111">Child Elements</span></span>

<span data-ttu-id="744d8-112">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="744d8-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="744d8-113">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="744d8-113">Parent Elements</span></span>

|<span data-ttu-id="744d8-114">Elemento</span><span class="sxs-lookup"><span data-stu-id="744d8-114">Element</span></span>|<span data-ttu-id="744d8-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="744d8-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="744d8-116">Elemento SelectionCondition para EntrySelectedBy para WideEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="744d8-116">SelectionCondition Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)|<span data-ttu-id="744d8-117">Define a condição que deve existir para que essa definição seja usada.</span><span class="sxs-lookup"><span data-stu-id="744d8-117">Defines the condition that must exist for this definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="744d8-118">Valor de texto</span><span class="sxs-lookup"><span data-stu-id="744d8-118">Text Value</span></span>

<span data-ttu-id="744d8-119">Especifique o script que é avaliado.</span><span class="sxs-lookup"><span data-stu-id="744d8-119">Specify the script that is evaluated.</span></span>

## <a name="remarks"></a><span data-ttu-id="744d8-120">Comentários</span><span class="sxs-lookup"><span data-stu-id="744d8-120">Remarks</span></span>

<span data-ttu-id="744d8-121">A condição de seleção deve especificar pelo menos um nome de script ou propriedade a ser avaliado, mas não pode especificar ambos.</span><span class="sxs-lookup"><span data-stu-id="744d8-121">The selection condition must specify at least one script or property name to evaluate, but cannot specify both.</span></span> <span data-ttu-id="744d8-122">Para obter mais informações sobre como usar condições de seleção, consulte [definindo condições para quando os dados são exibidos](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="744d8-122">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="744d8-123">Para obter mais informações sobre outros componentes de uma exibição ampla, consulte [Wide View](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="744d8-123">For more information about other components of a wide view, see [Wide View](./creating-a-wide-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="744d8-124">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="744d8-124">See Also</span></span>

[<span data-ttu-id="744d8-125">Criando uma exibição ampla</span><span class="sxs-lookup"><span data-stu-id="744d8-125">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="744d8-126">Definindo condições para quando os dados são exibidos</span><span class="sxs-lookup"><span data-stu-id="744d8-126">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="744d8-127">Elemento PropertyName para SelectionCondition para EntrySelectedBy para WideEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="744d8-127">PropertyName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>](./propertyname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format.md)

[<span data-ttu-id="744d8-128">Elemento SelectionCondition para EntrySelectedBy para WideEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="744d8-128">SelectionCondition Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)

[<span data-ttu-id="744d8-129">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="744d8-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
