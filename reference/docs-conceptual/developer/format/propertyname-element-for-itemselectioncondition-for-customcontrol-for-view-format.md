---
title: Elemento PropertyName para ItemSelectionCondition para CustomControl para exibição (formato) | Microsoft Docs
ms.date: 09/13/2016
ms.openlocfilehash: 0131fa86be4be4daec1d9d24b50397fb8529f050
ms.sourcegitcommit: 0907b8c6322d2c7c61b17f8168d53452c8964b41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/05/2020
ms.locfileid: "87785567"
---
# <a name="propertyname-element-for-itemselectioncondition-for-customcontrol-for-view-format"></a><span data-ttu-id="5b524-102">Elemento PropertyName para ItemSelectionCondition para CustomControl para View (formato)</span><span class="sxs-lookup"><span data-stu-id="5b524-102">PropertyName Element for ItemSelectionCondition for CustomControl for View (Format)</span></span>

<span data-ttu-id="5b524-103">Especifica a propriedade .NET que dispara a condição.</span><span class="sxs-lookup"><span data-stu-id="5b524-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="5b524-104">Quando essa propriedade está presente ou quando é avaliada como `true` , a condição é atendida e o controle é usado.</span><span class="sxs-lookup"><span data-stu-id="5b524-104">When this property is present or when it evaluates to `true`, the condition is met, and the control is used.</span></span> <span data-ttu-id="5b524-105">Esse elemento é usado ao definir um modo de exibição de controle personalizado.</span><span class="sxs-lookup"><span data-stu-id="5b524-105">This element is used when defining a custom control view.</span></span>

<span data-ttu-id="5b524-106">Elemento de configuração (Format) elemento ViewDefinitions (Format) View element (Format) CustomControl elemento (Format) CustomEntries Element for CustomControl para View (Format) CustomEntry Element for CustomEntries para o elemento View (Format) CustomItem para CustomEntry para exibição (Format) o elemento ExpressionBinding para CustomItem para CustomControl para o elemento View (Format) ItemSelectionCondition para a associação de expressão para CustomControl para o elemento View (Format) PropertyName para ItemSelectionCondition para CustomControl para View (Format</span><span class="sxs-lookup"><span data-stu-id="5b524-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for View (Format) CustomItem Element for CustomEntry for View (Format) ExpressionBinding Element for CustomItem for CustomControl for View (Format) ItemSelectionCondition Element for Expression Binding for CustomControl for View (Format) PropertyName Element for ItemSelectionCondition for CustomControl for View (Format</span></span>

## <a name="syntax"></a><span data-ttu-id="5b524-107">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="5b524-107">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="5b524-108">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="5b524-108">Attributes and Elements</span></span>

<span data-ttu-id="5b524-109">As seções a seguir descrevem atributos, elementos filho e o elemento pai do `PropertyName` elemento.</span><span class="sxs-lookup"><span data-stu-id="5b524-109">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="5b524-110">Atributos</span><span class="sxs-lookup"><span data-stu-id="5b524-110">Attributes</span></span>

<span data-ttu-id="5b524-111">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="5b524-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="5b524-112">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="5b524-112">Child Elements</span></span>

<span data-ttu-id="5b524-113">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="5b524-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="5b524-114">Elementos pai</span><span class="sxs-lookup"><span data-stu-id="5b524-114">Parent Elements</span></span>

|<span data-ttu-id="5b524-115">Elemento</span><span class="sxs-lookup"><span data-stu-id="5b524-115">Element</span></span>|<span data-ttu-id="5b524-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="5b524-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="5b524-117">Elemento ItemSelectionCondition para a associação de expressão para CustomControl para exibição (formato)</span><span class="sxs-lookup"><span data-stu-id="5b524-117">ItemSelectionCondition Element for Expression Binding for CustomControl for View (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-customcontrol-format.md)|<span data-ttu-id="5b524-118">Define a condição que deve existir para que esse controle seja usado.</span><span class="sxs-lookup"><span data-stu-id="5b524-118">Defines the condition that must exist for this control to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="5b524-119">Valor de texto</span><span class="sxs-lookup"><span data-stu-id="5b524-119">Text Value</span></span>

<span data-ttu-id="5b524-120">Especifique o nome da Propriedade do .NET que dispara a condição.</span><span class="sxs-lookup"><span data-stu-id="5b524-120">Specify the name of the .NET property that triggers the condition.</span></span>

## <a name="remarks"></a><span data-ttu-id="5b524-121">Comentários</span><span class="sxs-lookup"><span data-stu-id="5b524-121">Remarks</span></span>

<span data-ttu-id="5b524-122">Se esse elemento for usado, você não poderá especificar o elemento [scriptblock](./scriptblock-element-for-itemselectioncondition-for-customcontrol-for-view-format.md) ao definir a condição de seleção.</span><span class="sxs-lookup"><span data-stu-id="5b524-122">If this element is used, you cannot specify the [ScriptBlock](./scriptblock-element-for-itemselectioncondition-for-customcontrol-for-view-format.md) element when defining the selection condition.</span></span>

## <a name="see-also"></a><span data-ttu-id="5b524-123">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="5b524-123">See Also</span></span>

[<span data-ttu-id="5b524-124">Elemento ScriptBlock para ItemSelectionCondition para CustomControl para View (formato)</span><span class="sxs-lookup"><span data-stu-id="5b524-124">ScriptBlock Element for ItemSelectionCondition for CustomControl for View (Format)</span></span>](./scriptblock-element-for-itemselectioncondition-for-customcontrol-for-view-format.md)

[<span data-ttu-id="5b524-125">Elemento ItemSelectionCondition para a associação de expressão para CustomControl para exibição (formato)</span><span class="sxs-lookup"><span data-stu-id="5b524-125">ItemSelectionCondition Element for Expression Binding for CustomControl for View (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-customcontrol-format.md)

[<span data-ttu-id="5b524-126">Escrever um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b524-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
