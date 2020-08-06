---
title: Elemento ItemSelectionCondition para ExpressionBinding para CustomControl (Format) | Microsoft Docs
ms.date: 09/13/2016
ms.openlocfilehash: 6a5c66a63c02980b16c2d2d9dd689410c8aec51c
ms.sourcegitcommit: 0907b8c6322d2c7c61b17f8168d53452c8964b41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/05/2020
ms.locfileid: "87781181"
---
# <a name="itemselectioncondition-element-for-expressionbinding-for-customcontrol-format"></a><span data-ttu-id="90961-102">Elemento ItemSelectionCondition para ExpressionBinding para CustomControl (formato)</span><span class="sxs-lookup"><span data-stu-id="90961-102">ItemSelectionCondition Element for ExpressionBinding for CustomControl (Format)</span></span>

<span data-ttu-id="90961-103">Define a condição que deve existir para que esse controle seja usado.</span><span class="sxs-lookup"><span data-stu-id="90961-103">Defines the condition that must exist for this control to be used.</span></span> <span data-ttu-id="90961-104">Não há nenhum limite para o número de condições de seleção que podem ser especificadas para um item de controle.</span><span class="sxs-lookup"><span data-stu-id="90961-104">There is no limit to the number of selection conditions that can be specified for a control item.</span></span> <span data-ttu-id="90961-105">Esse elemento é usado ao definir um modo de exibição de controle personalizado.</span><span class="sxs-lookup"><span data-stu-id="90961-105">This element is used when defining a custom control view.</span></span>

<span data-ttu-id="90961-106">Elemento de configuração (Format) elemento ViewDefinitions (Format) View element (Format) CustomControl elemento (Format) CustomEntries Element for CustomControl para View (Format) CustomEntry Element for CustomEntries para o elemento View (Format) CustomItem para CustomEntry para o elemento View (Format) ExpressionBinding para CustomItem para CustomControl para o elemento View (Format) ItemSelectionCondition para a associação de expressão para CustomControl para a exibição (Format)</span><span class="sxs-lookup"><span data-stu-id="90961-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for View (Format) CustomItem Element for CustomEntry for View (Format) ExpressionBinding Element for CustomItem for CustomControl for View (Format) ItemSelectionCondition Element for Expression Binding for CustomControl for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="90961-107">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="90961-107">Syntax</span></span>

```xml
<ItemSelectionCondition>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</ItemSelectionCondition>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="90961-108">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="90961-108">Attributes and Elements</span></span>

<span data-ttu-id="90961-109">As seções a seguir descrevem atributos, elementos filho e o elemento pai do `ItemSelectionCondition` elemento.</span><span class="sxs-lookup"><span data-stu-id="90961-109">The following sections describe attributes, child elements, and the parent element of the `ItemSelectionCondition` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="90961-110">Atributos</span><span class="sxs-lookup"><span data-stu-id="90961-110">Attributes</span></span>

<span data-ttu-id="90961-111">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="90961-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="90961-112">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="90961-112">Child Elements</span></span>

|<span data-ttu-id="90961-113">Elemento</span><span class="sxs-lookup"><span data-stu-id="90961-113">Element</span></span>|<span data-ttu-id="90961-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="90961-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="90961-115">Elemento PropertyName para ItemSelectionCondition para CustomControl para exibição (formato</span><span class="sxs-lookup"><span data-stu-id="90961-115">PropertyName Element for ItemSelectionCondition for CustomControl for View (Format</span></span>](./propertyname-element-for-itemselectioncondition-for-customcontrol-for-view-format.md)|<span data-ttu-id="90961-116">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="90961-116">Optional element.</span></span><br /><br /> <span data-ttu-id="90961-117">Especifica a propriedade .NET que dispara a condição.</span><span class="sxs-lookup"><span data-stu-id="90961-117">Specifies the .NET property that triggers the condition.</span></span>|
|[<span data-ttu-id="90961-118">Elemento ScriptBlock para ItemSelectionCondition para CustomControl para View (formato)</span><span class="sxs-lookup"><span data-stu-id="90961-118">ScriptBlock Element for ItemSelectionCondition for CustomControl for View (Format)</span></span>](./scriptblock-element-for-itemselectioncondition-for-customcontrol-for-view-format.md)|<span data-ttu-id="90961-119">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="90961-119">Optional element.</span></span><br /><br /> <span data-ttu-id="90961-120">Especifica o script que dispara a condição.</span><span class="sxs-lookup"><span data-stu-id="90961-120">Specifies the script that triggers the condition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="90961-121">Elementos pai</span><span class="sxs-lookup"><span data-stu-id="90961-121">Parent Elements</span></span>

|<span data-ttu-id="90961-122">Elemento</span><span class="sxs-lookup"><span data-stu-id="90961-122">Element</span></span>|<span data-ttu-id="90961-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="90961-123">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="90961-124">Elemento ExpressionBinding para CustomItem para CustomControl para View (formato)</span><span class="sxs-lookup"><span data-stu-id="90961-124">ExpressionBinding Element for CustomItem for CustomControl for View (Format)</span></span>](./expressionbinding-element-for-customitem-for-customcontrol-for-view-format.md)|<span data-ttu-id="90961-125">Define os dados que são exibidos pelo controle.</span><span class="sxs-lookup"><span data-stu-id="90961-125">Defines the data that is displayed by the control.</span></span>|

## <a name="remarks"></a><span data-ttu-id="90961-126">Comentários</span><span class="sxs-lookup"><span data-stu-id="90961-126">Remarks</span></span>

<span data-ttu-id="90961-127">Você pode especificar um nome de propriedade ou um script para essa condição, mas não pode especificar ambos.</span><span class="sxs-lookup"><span data-stu-id="90961-127">You can specify one property name or a script for this condition but cannot specify both.</span></span>

## <a name="see-also"></a><span data-ttu-id="90961-128">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="90961-128">See Also</span></span>

[<span data-ttu-id="90961-129">Escrever um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="90961-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)

[<span data-ttu-id="90961-130">Elemento ExpressionBinding para CustomItem para CustomControl para View (formato)</span><span class="sxs-lookup"><span data-stu-id="90961-130">ExpressionBinding Element for CustomItem for CustomControl for View (Format)</span></span>](./expressionbinding-element-for-customitem-for-customcontrol-for-view-format.md)
