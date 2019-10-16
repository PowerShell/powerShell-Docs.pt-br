---
title: Elemento ScriptBlock para SelectionCondition para EntrySelectedBy para ListControl (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4a1adad7-e864-4892-9d26-a6476a9698d2
caps.latest.revision: 7
ms.openlocfilehash: b65d953169f6daf15fb617ce4d0303cf4cb584ee
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72368585"
---
# <a name="scriptblock-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format"></a><span data-ttu-id="4e06c-102">Elemento ScriptBlock para SelectionCondition para EntrySelectedBy para ListControl (formato)</span><span class="sxs-lookup"><span data-stu-id="4e06c-102">ScriptBlock Element for SelectionCondition for EntrySelectedBy for ListControl (Format)</span></span>

<span data-ttu-id="4e06c-103">Especifica o script que dispara a condição.</span><span class="sxs-lookup"><span data-stu-id="4e06c-103">Specifies the script that triggers the condition.</span></span> <span data-ttu-id="4e06c-104">Quando esse script é avaliado como `true`, a condição é atendida e a entrada da lista é usada.</span><span class="sxs-lookup"><span data-stu-id="4e06c-104">When this script is evaluated to `true`, the condition is met, and the list entry is used.</span></span>

<span data-ttu-id="4e06c-105">Elemento de configuração (Format) elemento ViewDefinitions (Format) View element (Format) ListControl elemento (Format) ListEntries Element (Format) o elemento ListEntry (Format) o elemento EntrySelectedBy para o elemento ListEntry (Format) SelectionCondition para EntrySelectedBy para o elemento ScriptBlock ListEntry (Format) para SelectionCondition para EntrySelectedBy para ListEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="4e06c-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element (Format) ListEntry Element (Format) EntrySelectedBy Element for ListEntry (Format) SelectionCondition Element for EntrySelectedBy for ListEntry (Format) ScriptBlock Element for SelectionCondition for EntrySelectedBy for ListEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="4e06c-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="4e06c-106">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="4e06c-107">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="4e06c-107">Attributes and Elements</span></span>

<span data-ttu-id="4e06c-108">As seções a seguir descrevem atributos, elementos filho e o elemento pai do elemento `ScriptBlock`.</span><span class="sxs-lookup"><span data-stu-id="4e06c-108">The following sections describe attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="4e06c-109">Atributos</span><span class="sxs-lookup"><span data-stu-id="4e06c-109">Attributes</span></span>

<span data-ttu-id="4e06c-110">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="4e06c-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="4e06c-111">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="4e06c-111">Child Elements</span></span>

<span data-ttu-id="4e06c-112">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="4e06c-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="4e06c-113">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="4e06c-113">Parent Elements</span></span>

|<span data-ttu-id="4e06c-114">Elemento</span><span class="sxs-lookup"><span data-stu-id="4e06c-114">Element</span></span>|<span data-ttu-id="4e06c-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="4e06c-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="4e06c-116">Elemento SelectionCondition para EntrySelectedBy para ListEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="4e06c-116">SelectionCondition Element for EntrySelectedBy for ListEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)|<span data-ttu-id="4e06c-117">Define a condição que deve existir para que essa entrada de lista seja usada.</span><span class="sxs-lookup"><span data-stu-id="4e06c-117">Defines the condition that must exist for this list entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="4e06c-118">Valor de texto</span><span class="sxs-lookup"><span data-stu-id="4e06c-118">Text Value</span></span>

<span data-ttu-id="4e06c-119">Especifique o script que é avaliado.</span><span class="sxs-lookup"><span data-stu-id="4e06c-119">Specify the script that is evaluated.</span></span>

## <a name="remarks"></a><span data-ttu-id="4e06c-120">Comentários</span><span class="sxs-lookup"><span data-stu-id="4e06c-120">Remarks</span></span>

<span data-ttu-id="4e06c-121">A condição de seleção deve especificar pelo menos um nome de script ou propriedade a ser avaliado, mas não pode especificar ambos.</span><span class="sxs-lookup"><span data-stu-id="4e06c-121">The selection condition must specify a least one script or property name to evaluate, but cannot specify both.</span></span> <span data-ttu-id="4e06c-122">(Para obter mais informações sobre como as condições de seleção podem ser usadas, consulte [definindo condições para quando uma entrada ou item de exibição é usado](./defining-conditions-for-displaying-data.md).)</span><span class="sxs-lookup"><span data-stu-id="4e06c-122">(For more information about how selection conditions can be used, see [Defining Conditions for when a View Entry or Item is Used](./defining-conditions-for-displaying-data.md).)</span></span>

<span data-ttu-id="4e06c-123">Para obter mais informações sobre os outros componentes de um modo de exibição de lista, consulte [exibição de lista](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="4e06c-123">For more information about the other components of a list view, see [List View](./creating-a-list-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4e06c-124">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="4e06c-124">See Also</span></span>

[<span data-ttu-id="4e06c-125">Elemento ListEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="4e06c-125">ListEntry Element (Format)</span></span>](./listentry-element-for-listcontrol-format.md)

[<span data-ttu-id="4e06c-126">Elemento PropertyName para SelectionCondition para EntrySelectedBy para ListEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="4e06c-126">PropertyName Element for SelectionCondition for EntrySelectedBy for ListEntry (Format)</span></span>](./propertyname-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format.md)

[<span data-ttu-id="4e06c-127">Elemento SelectionCondition para EntrySelectedBy para ListEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="4e06c-127">SelectionCondition Element for EntrySelectedBy for ListEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)

[<span data-ttu-id="4e06c-128">Exibição de lista</span><span class="sxs-lookup"><span data-stu-id="4e06c-128">List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="4e06c-129">Definindo condições para quando uma entrada ou item de exibição é usado</span><span class="sxs-lookup"><span data-stu-id="4e06c-129">Defining Conditions for when a View Entry or Item is Used</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="4e06c-130">Escrevendo um arquivo de tipos e formatação do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e06c-130">Writing a Windows PowerShell Formatting and Types File</span></span>](./writing-a-powershell-formatting-file.md)
