---
title: Elemento CustomItem para CustomEntry para controles para View (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 33cb5350-73ef-4b79-a879-0edf051869e4
caps.latest.revision: 7
ms.openlocfilehash: 174ba6a14819f823ec39f72e49a626e781221d8c
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72363935"
---
# <a name="customitem-element-for-customentry-for-controls-for-view-format"></a><span data-ttu-id="a928a-102">Elemento CustomItem para CustomEntry para Controls para View (formato)</span><span class="sxs-lookup"><span data-stu-id="a928a-102">CustomItem Element for CustomEntry for Controls for View (Format)</span></span>

<span data-ttu-id="a928a-103">Define quais dados são exibidos pelo controle e como eles são exibidos.</span><span class="sxs-lookup"><span data-stu-id="a928a-103">Defines what data is displayed by the control and how it is displayed.</span></span> <span data-ttu-id="a928a-104">Esse elemento é usado ao definir controles que podem ser usados por uma exibição.</span><span class="sxs-lookup"><span data-stu-id="a928a-104">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="a928a-105">Elemento de configuração (Format) elemento ViewDefinitions (Format) exibir elemento (Format) controle elemento (Format) elemento Control para controles para o elemento View (Format) CustomControl para controle para controles para o elemento View (Format) CustomEntries para CustomControl para o elemento View (Format) CustomEntry para CustomEntries para controles para View (Format) CustomItem Element for CustomEntry para Controls for View (Format)</span><span class="sxs-lookup"><span data-stu-id="a928a-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) CustomItem Element for CustomEntry for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="a928a-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="a928a-106">Syntax</span></span>

```xml
<CustomItem>
  <ExpressionBinding>...</ExpressionBinding>
  <NewLine/>
  <Text>TextToDisplay</Text>
  <Frame>...<Frame>
</CustomItem>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="a928a-107">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="a928a-107">Attributes and Elements</span></span>

<span data-ttu-id="a928a-108">As seções a seguir descrevem atributos, elementos filho e o elemento pai do elemento `CustomItem`.</span><span class="sxs-lookup"><span data-stu-id="a928a-108">The following sections describe attributes, child elements, and the parent element of the `CustomItem` element.</span></span> <span data-ttu-id="a928a-109">Para obter mais informações, consulte comentários.</span><span class="sxs-lookup"><span data-stu-id="a928a-109">For more information, see Remarks.</span></span>

### <a name="attributes"></a><span data-ttu-id="a928a-110">Atributos</span><span class="sxs-lookup"><span data-stu-id="a928a-110">Attributes</span></span>

<span data-ttu-id="a928a-111">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="a928a-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="a928a-112">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="a928a-112">Child Elements</span></span>

|<span data-ttu-id="a928a-113">Elemento</span><span class="sxs-lookup"><span data-stu-id="a928a-113">Element</span></span>|<span data-ttu-id="a928a-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="a928a-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="a928a-115">Elemento ExpressionBinding para CustomItem para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="a928a-115">ExpressionBinding Element for CustomItem for Controls for View (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)|<span data-ttu-id="a928a-116">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="a928a-116">Optional element.</span></span><br /><br /> <span data-ttu-id="a928a-117">Define os dados que são exibidos pelo controle.</span><span class="sxs-lookup"><span data-stu-id="a928a-117">Defines the data that is displayed by the control.</span></span>|
|[<span data-ttu-id="a928a-118">Elemento frame para CustomItem para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="a928a-118">Frame Element for CustomItem for Controls for View (Format)</span></span>](./frame-element-for-customitem-for-controls-for-view-format.md)|<span data-ttu-id="a928a-119">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="a928a-119">Optional element.</span></span><br /><br /> <span data-ttu-id="a928a-120">Define como os dados são exibidos, como deslocar os dados para a esquerda ou para a direita.</span><span class="sxs-lookup"><span data-stu-id="a928a-120">Defines how the data is displayed, such as shifting the data to the left or right.</span></span>|
|[<span data-ttu-id="a928a-121">Elemento de nova linha para CustomItem para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="a928a-121">NewLine Element for CustomItem for Controls for View (Format)</span></span>](./newline-element-for-customitem-for-controls-for-view-format.md)|<span data-ttu-id="a928a-122">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="a928a-122">Optional element.</span></span><br /><br /> <span data-ttu-id="a928a-123">Adiciona uma linha em branco à exibição do controle.</span><span class="sxs-lookup"><span data-stu-id="a928a-123">Adds a blank line to the display of the control.</span></span>|
|[<span data-ttu-id="a928a-124">Elemento Text para CustomItem para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="a928a-124">Text Element for CustomItem for Controls for View (Format)</span></span>](./text-element-for-customitem-for-controls-for-view-format.md)|<span data-ttu-id="a928a-125">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="a928a-125">Optional element.</span></span><br /><br /> <span data-ttu-id="a928a-126">Adiciona texto, como parênteses ou colchetes, à exibição do controle.</span><span class="sxs-lookup"><span data-stu-id="a928a-126">Adds text, such as parentheses or brackets, to the display of the control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="a928a-127">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="a928a-127">Parent Elements</span></span>

|<span data-ttu-id="a928a-128">Elemento</span><span class="sxs-lookup"><span data-stu-id="a928a-128">Element</span></span>|<span data-ttu-id="a928a-129">Descrição</span><span class="sxs-lookup"><span data-stu-id="a928a-129">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="a928a-130">Elemento CustomEntry para CustomEntries para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="a928a-130">CustomEntry Element for CustomEntries for Controls for View (Format)</span></span>](./customentry-element-for-customentries-for-controls-for-view-format.md)|<span data-ttu-id="a928a-131">Fornece uma definição do controle.</span><span class="sxs-lookup"><span data-stu-id="a928a-131">Provides a definition of the control.</span></span>|

## <a name="remarks"></a><span data-ttu-id="a928a-132">Comentários</span><span class="sxs-lookup"><span data-stu-id="a928a-132">Remarks</span></span>

<span data-ttu-id="a928a-133">Ao especificar os elementos filho do elemento `CustomItem`, tenha em mente o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a928a-133">When specifying the child elements of the `CustomItem` element, keep the following in mind:</span></span>

- <span data-ttu-id="a928a-134">Os elementos filho devem ser adicionados na seguinte sequência: `ExpressionBinding`, `NewLine`, `Text` e `Frame`.</span><span class="sxs-lookup"><span data-stu-id="a928a-134">The child elements must be added in the following sequence: `ExpressionBinding`, `NewLine`, `Text`, and `Frame`.</span></span>

- <span data-ttu-id="a928a-135">Não há nenhum limite máximo para o número de sequências que você pode especificar.</span><span class="sxs-lookup"><span data-stu-id="a928a-135">There is no maximum limit to the number of sequences that you can specify.</span></span>

- <span data-ttu-id="a928a-136">Em cada sequência, não há nenhum limite máximo para o número de elementos `ExpressionBinding` que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="a928a-136">In each sequence, there is no maximum limit to the number of `ExpressionBinding` elements that you can use.</span></span>

## <a name="see-also"></a><span data-ttu-id="a928a-137">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="a928a-137">See Also</span></span>

[<span data-ttu-id="a928a-138">Elemento ExpressionBinding para CustomItem para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="a928a-138">ExpressionBinding Element for CustomItem for Controls for View (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)

[<span data-ttu-id="a928a-139">Elemento frame para CustomItem para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="a928a-139">Frame Element for CustomItem for Controls for View (Format)</span></span>](./frame-element-for-customitem-for-controls-for-view-format.md)

[<span data-ttu-id="a928a-140">Elemento de nova linha para CustomItem para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="a928a-140">NewLine Element for CustomItem for Controls for View (Format)</span></span>](./newline-element-for-customitem-for-controls-for-view-format.md)

[<span data-ttu-id="a928a-141">Elemento Text para CustomItem para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="a928a-141">Text Element for CustomItem for Controls for View (Format)</span></span>](./text-element-for-customitem-for-controls-for-view-format.md)

[<span data-ttu-id="a928a-142">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="a928a-142">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)