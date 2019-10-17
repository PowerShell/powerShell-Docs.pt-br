---
title: Elemento ExpressionBinding para CustomItem para CustomControl para exibição (formato) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7f5ebea5-ee9c-4b90-a116-12a1daa28fc7
caps.latest.revision: 7
ms.openlocfilehash: 226bbea1d7613ad3099e05e8caa9817ff16c1f42
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72363145"
---
# <a name="expressionbinding-element-for-customitem-for-customcontrol-for-view-format"></a><span data-ttu-id="a127d-102">Elemento ExpressionBinding para CustomItem para CustomControl para View (formato)</span><span class="sxs-lookup"><span data-stu-id="a127d-102">ExpressionBinding Element for CustomItem for CustomControl for View (Format)</span></span>

<span data-ttu-id="a127d-103">Define os dados que são exibidos pelo controle.</span><span class="sxs-lookup"><span data-stu-id="a127d-103">Defines the data that is displayed by the control.</span></span> <span data-ttu-id="a127d-104">Esse elemento é usado ao definir um modo de exibição de controle personalizado.</span><span class="sxs-lookup"><span data-stu-id="a127d-104">This element is used when defining a custom control view.</span></span>

<span data-ttu-id="a127d-105">Elemento de configuração (Format) elemento ViewDefinitions (Format) View element (Format) CustomControl Element para View (Format) CustomEntries Element for CustomControl para View (Format) CustomEntry Element for CustomEntries for CustomControl for View ( Format) elemento CustomItem para CustomEntry para CustomControl para exibição (Format) o elemento ExpressionBinding para CustomItem para CustomControl para a exibição (Format)</span><span class="sxs-lookup"><span data-stu-id="a127d-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element for View (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for CustomControl for View (Format) CustomItem Element for CustomEntry for CustomControl for View (Format) ExpressionBinding Element for CustomItem for CustomControl for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="a127d-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="a127d-106">Syntax</span></span>

```xml
<ExpressionBinding>
  <CustomControl>...</CustomControl>
  <CustomControlName>NameofCommonCustomControl</CustomControlName>
  <EnumerateCollection/>
  <ItemSelectionCondition>...</ItemSelectionCondition>
  <PropertyName>Nameof.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate></ScriptBlock>
</ExpressionBinding>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="a127d-107">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="a127d-107">Attributes and Elements</span></span>

<span data-ttu-id="a127d-108">As seções a seguir descrevem atributos, elementos filho e o elemento pai do elemento `ExpressionBinding`.</span><span class="sxs-lookup"><span data-stu-id="a127d-108">The following sections describe attributes, child elements, and the parent element of the `ExpressionBinding` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="a127d-109">Atributos</span><span class="sxs-lookup"><span data-stu-id="a127d-109">Attributes</span></span>

<span data-ttu-id="a127d-110">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="a127d-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="a127d-111">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="a127d-111">Child Elements</span></span>

|<span data-ttu-id="a127d-112">Elemento</span><span class="sxs-lookup"><span data-stu-id="a127d-112">Element</span></span>|<span data-ttu-id="a127d-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="a127d-113">Description</span></span>|
|-------------|-----------------|
|`CustomControl Element`|<span data-ttu-id="a127d-114">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="a127d-114">Optional element.</span></span><br /><br /> <span data-ttu-id="a127d-115">Define um controle que é usado por este controle.</span><span class="sxs-lookup"><span data-stu-id="a127d-115">Defines a control that is used by this control.</span></span>|
|[<span data-ttu-id="a127d-116">Elemento CustomControlName para ExpressionBinding para CustomControl para View (Format)</span><span class="sxs-lookup"><span data-stu-id="a127d-116">CustomControlName Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./customcontrolname-element-for-expressionbinding-for-customcontrol-for-view-format.md)|<span data-ttu-id="a127d-117">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="a127d-117">Optional element.</span></span><br /><br /> <span data-ttu-id="a127d-118">Especifica o nome de um controle comum ou um controle de exibição.</span><span class="sxs-lookup"><span data-stu-id="a127d-118">Specifies the name of a common control or a view control.</span></span>|
|[<span data-ttu-id="a127d-119">Elemento enumeracollection para ExpressionBinding para CustomControl para exibição (formato)</span><span class="sxs-lookup"><span data-stu-id="a127d-119">EnumerateCollection Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./enumeratecollection-element-for-expressionbinding-for-customcontrol-for-view-format.md)|<span data-ttu-id="a127d-120">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="a127d-120">Optional element.</span></span><br /><br /> <span data-ttu-id="a127d-121">Especificado que os elementos das coleções são exibidos.</span><span class="sxs-lookup"><span data-stu-id="a127d-121">Specified that the elements of collections are displayed.</span></span>|
|[<span data-ttu-id="a127d-122">Elemento ItemSelectionCondition para ExpressionBinding para CustomControl para View (Format)</span><span class="sxs-lookup"><span data-stu-id="a127d-122">ItemSelectionCondition Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-customcontrol-format.md)|<span data-ttu-id="a127d-123">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="a127d-123">Optional element.</span></span><br /><br /> <span data-ttu-id="a127d-124">Define a condição que deve existir para que esse controle seja usado.</span><span class="sxs-lookup"><span data-stu-id="a127d-124">Defines the condition that must exist for this control to be used.</span></span>|
|[<span data-ttu-id="a127d-125">Elemento PropertyName para ExpressionBinding para CustomControl para exibição (Format)</span><span class="sxs-lookup"><span data-stu-id="a127d-125">PropertyName Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./propertyname-element-for-expressionbinding-for-customcontrol-for-view-format.md)|<span data-ttu-id="a127d-126">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="a127d-126">Optional element.</span></span><br /><br /> <span data-ttu-id="a127d-127">Especifica a propriedade .NET cujo valor é exibido pelo controle.</span><span class="sxs-lookup"><span data-stu-id="a127d-127">Specifies the .NET property whose value is displayed by the control.</span></span>|
|[<span data-ttu-id="a127d-128">Elemento ScriptBlock para ExpressionBinding para CustomCustomControl para View (Format)</span><span class="sxs-lookup"><span data-stu-id="a127d-128">ScriptBlock Element for ExpressionBinding for CustomCustomControl for View (Format)</span></span>](./scriptblock-element-for-expressionbinding-for-customcontrol-for-view-format.md)|<span data-ttu-id="a127d-129">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="a127d-129">Optional element.</span></span><br /><br /> <span data-ttu-id="a127d-130">Especifica o script cujo valor é exibido pelo controle.</span><span class="sxs-lookup"><span data-stu-id="a127d-130">Specifies the script whose value is displayed by the control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="a127d-131">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="a127d-131">Parent Elements</span></span>

|<span data-ttu-id="a127d-132">Elemento</span><span class="sxs-lookup"><span data-stu-id="a127d-132">Element</span></span>|<span data-ttu-id="a127d-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="a127d-133">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="a127d-134">Elemento CustomItem para CustomEntry para CustomControl para exibição (formato)</span><span class="sxs-lookup"><span data-stu-id="a127d-134">CustomItem Element for CustomEntry for CustomControl for View (Format)</span></span>](./customitem-element-for-customentry-for-customcontrol-for-view-format.md)|<span data-ttu-id="a127d-135">Define quais dados são exibidos pelo modo de exibição de controle personalizado e como eles são exibidos.</span><span class="sxs-lookup"><span data-stu-id="a127d-135">Defines what data is displayed by the custom control view and how it is displayed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="a127d-136">Comentários</span><span class="sxs-lookup"><span data-stu-id="a127d-136">Remarks</span></span>

## <a name="see-also"></a><span data-ttu-id="a127d-137">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="a127d-137">See Also</span></span>

[<span data-ttu-id="a127d-138">Elemento CustomControlName para ExpressionBinding para CustomControl para View (Format)</span><span class="sxs-lookup"><span data-stu-id="a127d-138">CustomControlName Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./customcontrolname-element-for-expressionbinding-for-customcontrol-for-view-format.md)

[<span data-ttu-id="a127d-139">Elemento enumeracollection para ExpressionBinding para CustomControl para exibição (formato)</span><span class="sxs-lookup"><span data-stu-id="a127d-139">EnumerateCollection Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./enumeratecollection-element-for-expressionbinding-for-customcontrol-for-view-format.md)

[<span data-ttu-id="a127d-140">Elemento ItemSelectionCondition para ExpressionBinding para CustomControl para View (Format)</span><span class="sxs-lookup"><span data-stu-id="a127d-140">ItemSelectionCondition Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-customcontrol-format.md)

[<span data-ttu-id="a127d-141">Elemento PropertyName para ExpressionBinding para CustomControl para exibição (Format)</span><span class="sxs-lookup"><span data-stu-id="a127d-141">PropertyName Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./propertyname-element-for-expressionbinding-for-customcontrol-for-view-format.md)

[<span data-ttu-id="a127d-142">Elemento ScriptBlock para ExpressionBinding para CustomControl para View (Format)</span><span class="sxs-lookup"><span data-stu-id="a127d-142">ScriptBlock Element for ExpressionBinding for CustomControl for View (Format)</span></span>](./scriptblock-element-for-expressionbinding-for-customcontrol-for-view-format.md)

[<span data-ttu-id="a127d-143">Elemento CustomItem para CustomEntry para CustomControl para exibição (formato)</span><span class="sxs-lookup"><span data-stu-id="a127d-143">CustomItem Element for CustomEntry for CustomControl for View (Format)</span></span>](./customitem-element-for-customentry-for-customcontrol-for-view-format.md)

[<span data-ttu-id="a127d-144">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="a127d-144">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)