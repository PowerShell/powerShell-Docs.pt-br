---
title: Elemento GroupBy para exibição (formato) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 67a2b061-2a4a-4ad1-84f9-cdbefb64aaab
caps.latest.revision: 8
ms.openlocfilehash: abb8b91626128b3deaa2db24a9fd8b34a6563410
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72363625"
---
# <a name="groupby-element-for-view-format"></a><span data-ttu-id="b47a4-102">Elemento GroupBy para View (formato)</span><span class="sxs-lookup"><span data-stu-id="b47a4-102">GroupBy Element for View (Format)</span></span>

<span data-ttu-id="b47a4-103">Define como um novo grupo de objetos é exibido.</span><span class="sxs-lookup"><span data-stu-id="b47a4-103">Defines how a new group of objects is displayed.</span></span> <span data-ttu-id="b47a4-104">Esse elemento é usado ao definir uma tabela, lista, largura ou exibição de controle personalizado.</span><span class="sxs-lookup"><span data-stu-id="b47a4-104">This element is used when defining a table, list, wide, or custom control view.</span></span>

<span data-ttu-id="b47a4-105">Elemento de configuração (Format) elemento ViewDefinitions (Format) exibir elemento (Format) elemento GroupBy para View (Format)</span><span class="sxs-lookup"><span data-stu-id="b47a4-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="b47a4-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="b47a4-106">Syntax</span></span>

```xml
<GroupBy>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
  <Label>TextToDisplay</Label>
  <CustomControl>...</CustomControl>
  <CustomControlName>NameOfControl</CustomControlName>
</GroupBy>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="b47a4-107">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="b47a4-107">Attributes and Elements</span></span>

<span data-ttu-id="b47a4-108">As seções a seguir descrevem atributos, elementos filho e elementos pai.</span><span class="sxs-lookup"><span data-stu-id="b47a4-108">The following sections describe attributes, child elements, and parent elements.</span></span>

### <a name="attributes"></a><span data-ttu-id="b47a4-109">Atributos</span><span class="sxs-lookup"><span data-stu-id="b47a4-109">Attributes</span></span>

<span data-ttu-id="b47a4-110">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="b47a4-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="b47a4-111">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="b47a4-111">Child Elements</span></span>

|<span data-ttu-id="b47a4-112">Elemento</span><span class="sxs-lookup"><span data-stu-id="b47a4-112">Element</span></span>|<span data-ttu-id="b47a4-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="b47a4-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="b47a4-114">Elemento CustomControl para GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="b47a4-114">CustomControl Element for GroupBy (Format)</span></span>](./customcontrol-element-for-groupby-format.md)|<span data-ttu-id="b47a4-115">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="b47a4-115">Optional element.</span></span><br /><br /> <span data-ttu-id="b47a4-116">Define o controle personalizado que exibe novos grupos.</span><span class="sxs-lookup"><span data-stu-id="b47a4-116">Defines the custom control that display new groups.</span></span>|
|[<span data-ttu-id="b47a4-117">Elemento CustomControlName para GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="b47a4-117">CustomControlName Element for GroupBy (Format)</span></span>](./customcontrolname-element-for-groupby-format.md)|<span data-ttu-id="b47a4-118">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="b47a4-118">Optional element.</span></span><br /><br /> <span data-ttu-id="b47a4-119">Especifica o nome de um controle usado para exibir o novo grupo.</span><span class="sxs-lookup"><span data-stu-id="b47a4-119">Specifies the name of a control that is used to display the new group.</span></span>|
|[<span data-ttu-id="b47a4-120">Elemento Label para GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="b47a4-120">Label Element for GroupBy (Format)</span></span>](./label-element-for-groupby-format.md)|<span data-ttu-id="b47a4-121">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="b47a4-121">Optional element.</span></span><br /><br /> <span data-ttu-id="b47a4-122">Especifica um rótulo que é exibido quando um novo grupo é encontrado.</span><span class="sxs-lookup"><span data-stu-id="b47a4-122">Specifies a label that is displayed when a new group is encountered.</span></span>|
|[<span data-ttu-id="b47a4-123">Elemento PropertyName para GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="b47a4-123">PropertyName Element for GroupBy (Format)</span></span>](./propertyname-element-for-groupby-format.md)|<span data-ttu-id="b47a4-124">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="b47a4-124">Optional element.</span></span><br /><br /> <span data-ttu-id="b47a4-125">Especifica a propriedade .NET que inicia um novo grupo sempre que seu valor é alterado.</span><span class="sxs-lookup"><span data-stu-id="b47a4-125">Specifies the .NET property the starts a new group whenever its value changes.</span></span>|
|[<span data-ttu-id="b47a4-126">Elemento ScriptBlock para GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="b47a4-126">ScriptBlock Element for GroupBy (Format)</span></span>](./scriptblock-element-for-groupby-format.md)|<span data-ttu-id="b47a4-127">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="b47a4-127">Optional element.</span></span><br /><br /> <span data-ttu-id="b47a4-128">Especifica o script que inicia um novo grupo sempre que seu valor é alterado.</span><span class="sxs-lookup"><span data-stu-id="b47a4-128">Specifies the script that starts a new group whenever its value changes.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="b47a4-129">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="b47a4-129">Parent Elements</span></span>

|<span data-ttu-id="b47a4-130">Elemento</span><span class="sxs-lookup"><span data-stu-id="b47a4-130">Element</span></span>|<span data-ttu-id="b47a4-131">Descrição</span><span class="sxs-lookup"><span data-stu-id="b47a4-131">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="b47a4-132">Elemento View (formato)</span><span class="sxs-lookup"><span data-stu-id="b47a4-132">View Element (Format)</span></span>](./view-element-format.md)|<span data-ttu-id="b47a4-133">Define uma exibição que exibe um ou mais objetos .NET.</span><span class="sxs-lookup"><span data-stu-id="b47a4-133">Defines a view that displays one or more .NET objects.</span></span>|

## <a name="remarks"></a><span data-ttu-id="b47a4-134">Comentários</span><span class="sxs-lookup"><span data-stu-id="b47a4-134">Remarks</span></span>

<span data-ttu-id="b47a4-135">Ao definir como um novo grupo de objetos é exibido, você deve especificar a propriedade ou o script que iniciará o novo grupo; no entanto, você não pode especificar ambos.</span><span class="sxs-lookup"><span data-stu-id="b47a4-135">When defining how a new group of objects is displayed, you must specify the property or script that will start the new group; however, you cannot specify both.</span></span>

## <a name="see-also"></a><span data-ttu-id="b47a4-136">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="b47a4-136">See Also</span></span>

[<span data-ttu-id="b47a4-137">Elemento CustomControlName para GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="b47a4-137">CustomControlName Element for GroupBy (Format)</span></span>](./customcontrolname-element-for-groupby-format.md)

[<span data-ttu-id="b47a4-138">Elemento Label para GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="b47a4-138">Label Element for GroupBy (Format)</span></span>](./label-element-for-groupby-format.md)

[<span data-ttu-id="b47a4-139">Elemento PropertyName para GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="b47a4-139">PropertyName Element for GroupBy (Format)</span></span>](./propertyname-element-for-groupby-format.md)

[<span data-ttu-id="b47a4-140">Elemento ScriptBlock para GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="b47a4-140">ScriptBlock Element for GroupBy (Format)</span></span>](./scriptblock-element-for-groupby-format.md)

[<span data-ttu-id="b47a4-141">Elemento View (formato)</span><span class="sxs-lookup"><span data-stu-id="b47a4-141">View Element (Format)</span></span>](./view-element-format.md)

[<span data-ttu-id="b47a4-142">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="b47a4-142">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)