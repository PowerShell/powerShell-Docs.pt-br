---
title: Elemento PropertyName para ItemSelectionCondition para GroupBy (Format) | Microsoft Docs
ms.date: 09/13/2016
ms.openlocfilehash: f6d671035bfd2ef6323b638fdd951bb020bd6548
ms.sourcegitcommit: 0907b8c6322d2c7c61b17f8168d53452c8964b41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/05/2020
ms.locfileid: "87780875"
---
# <a name="propertyname-element-for-itemselectioncondition-for-groupby-format"></a><span data-ttu-id="b15bd-102">Elemento PropertyName para ItemSelectionCondition para GroupBy (formato)</span><span class="sxs-lookup"><span data-stu-id="b15bd-102">PropertyName Element for ItemSelectionCondition for GroupBy (Format)</span></span>

<span data-ttu-id="b15bd-103">Especifica a propriedade .NET que dispara a condição.</span><span class="sxs-lookup"><span data-stu-id="b15bd-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="b15bd-104">Quando essa propriedade está presente ou quando é avaliada como `true` , a condição é atendida e o controle é usado.</span><span class="sxs-lookup"><span data-stu-id="b15bd-104">When this property is present or when it evaluates to `true`, the condition is met, and the control is used.</span></span> <span data-ttu-id="b15bd-105">Esse elemento é usado ao definir como um novo grupo de objetos é exibido.</span><span class="sxs-lookup"><span data-stu-id="b15bd-105">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="b15bd-106">Elemento de configuração (Format) elemento ViewDefinitions (Format) View element (Format) elemento GroupBy para View (Format) CustomControl Element para GroupBy (Format) CustomEntries Element for CustomControl para o elemento de CustomEntry GroupBy (Format) para CustomControl para GroupBy (Format) o elemento CustomItem para CustomEntry para o elemento ExpressionBinding de GroupBy (Format) para CustomItem para o elemento GroupBy (Format) ItemSelectionCondition para ExpressionBinding para o elemento GroupBy (Format) PropertyName para ItemSelectionCondition para GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="b15bd-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) CustomItem Element for CustomEntry for GroupBy (Format) ExpressionBinding Element for CustomItem for GroupBy (Format) ItemSelectionCondition Element for ExpressionBinding for GroupBy (Format) PropertyName Element for ItemSelectionCondition for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="b15bd-107">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="b15bd-107">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="b15bd-108">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="b15bd-108">Attributes and Elements</span></span>

<span data-ttu-id="b15bd-109">As seções a seguir descrevem atributos, elementos filho e o elemento pai do `PropertyName` elemento.</span><span class="sxs-lookup"><span data-stu-id="b15bd-109">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="b15bd-110">Atributos</span><span class="sxs-lookup"><span data-stu-id="b15bd-110">Attributes</span></span>

<span data-ttu-id="b15bd-111">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="b15bd-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="b15bd-112">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="b15bd-112">Child Elements</span></span>

<span data-ttu-id="b15bd-113">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="b15bd-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="b15bd-114">Elementos pai</span><span class="sxs-lookup"><span data-stu-id="b15bd-114">Parent Elements</span></span>

|<span data-ttu-id="b15bd-115">Elemento</span><span class="sxs-lookup"><span data-stu-id="b15bd-115">Element</span></span>|<span data-ttu-id="b15bd-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="b15bd-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="b15bd-117">Elemento ItemSelectionCondition para ExpressionBinding para GroupBy (formato)</span><span class="sxs-lookup"><span data-stu-id="b15bd-117">ItemSelectionCondition Element for ExpressionBinding for GroupBy (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-groupby-format.md)|<span data-ttu-id="b15bd-118">Define a condição que deve existir para que esse controle seja usado.</span><span class="sxs-lookup"><span data-stu-id="b15bd-118">Defines the condition that must exist for this control to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="b15bd-119">Valor de texto</span><span class="sxs-lookup"><span data-stu-id="b15bd-119">Text Value</span></span>

<span data-ttu-id="b15bd-120">Especifique o nome da Propriedade do .NET que dispara a condição.</span><span class="sxs-lookup"><span data-stu-id="b15bd-120">Specify the name of the .NET property that triggers the condition.</span></span>

## <a name="remarks"></a><span data-ttu-id="b15bd-121">Comentários</span><span class="sxs-lookup"><span data-stu-id="b15bd-121">Remarks</span></span>

<span data-ttu-id="b15bd-122">Se esse elemento for usado, você não poderá especificar o elemento [scriptblock](./scriptblock-element-for-itemselectioncondition-for-groupby-format.md) ao definir a condição de seleção.</span><span class="sxs-lookup"><span data-stu-id="b15bd-122">If this element is used, you cannot specify the [ScriptBlock](./scriptblock-element-for-itemselectioncondition-for-groupby-format.md) element when defining the selection condition.</span></span>

## <a name="see-also"></a><span data-ttu-id="b15bd-123">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="b15bd-123">See Also</span></span>

[<span data-ttu-id="b15bd-124">Elemento ScriptBlock para ItemSelectionCondition para GroupBy (formato)</span><span class="sxs-lookup"><span data-stu-id="b15bd-124">ScriptBlock Element for ItemSelectionCondition for GroupBy (Format)</span></span>](./scriptblock-element-for-itemselectioncondition-for-groupby-format.md)

[<span data-ttu-id="b15bd-125">Elemento ItemSelectionCondition para ExpressionBinding para GroupBy (formato)</span><span class="sxs-lookup"><span data-stu-id="b15bd-125">ItemSelectionCondition Element for ExpressionBinding for GroupBy (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-groupby-format.md)

[<span data-ttu-id="b15bd-126">Escrever um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="b15bd-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
