---
title: Elemento CustomControl para GroupBy (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2472e256-8f4f-4288-8b67-a3300649dafa
caps.latest.revision: 9
ms.openlocfilehash: 2e84e770a345e272d4c5917b00afe7520840e1db
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72368955"
---
# <a name="customcontrol-element-for-groupby-format"></a><span data-ttu-id="cdc89-102">Elemento CustomControl para GroupBy (formato)</span><span class="sxs-lookup"><span data-stu-id="cdc89-102">CustomControl Element for GroupBy (Format)</span></span>

<span data-ttu-id="cdc89-103">Define o controle personalizado que exibe o novo grupo.</span><span class="sxs-lookup"><span data-stu-id="cdc89-103">Defines the custom control that displays the new group.</span></span>

<span data-ttu-id="cdc89-104">Elemento de configuração (Format) elemento ViewDefinitions (Format) exibir elemento (Format) elemento GroupBy para o elemento View (Format) CustomControl para GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="cdc89-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="cdc89-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="cdc89-105">Syntax</span></span>

```xml
<CustomControl>
  <CustomEntries>...</CustomEntries>
<CustomControl>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="cdc89-106">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="cdc89-106">Attributes and Elements</span></span>

<span data-ttu-id="cdc89-107">As seções a seguir descrevem os atributos, os elementos filho e o elemento pai do elemento `CustomControl`.</span><span class="sxs-lookup"><span data-stu-id="cdc89-107">The following sections describe the attributes, child elements, and parent element of the `CustomControl` element.</span></span> <span data-ttu-id="cdc89-108">Você pode especificar qualquer número de elementos filho e listá-los em qualquer ordem.</span><span class="sxs-lookup"><span data-stu-id="cdc89-108">You can specify any number of child elements and list them in any order.</span></span>

### <a name="attributes"></a><span data-ttu-id="cdc89-109">Atributos</span><span class="sxs-lookup"><span data-stu-id="cdc89-109">Attributes</span></span>

<span data-ttu-id="cdc89-110">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="cdc89-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="cdc89-111">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="cdc89-111">Child Elements</span></span>

|<span data-ttu-id="cdc89-112">Elemento</span><span class="sxs-lookup"><span data-stu-id="cdc89-112">Element</span></span>|<span data-ttu-id="cdc89-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="cdc89-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="cdc89-114">Elemento CustomEntries para CustomControl para GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="cdc89-114">CustomEntries Element for CustomControl for GroupBy (Format)</span></span>](./customentries-element-for-customcontrol-for-groupby-format.md)|<span data-ttu-id="cdc89-115">Elemento obrigatório.</span><span class="sxs-lookup"><span data-stu-id="cdc89-115">Required element.</span></span><br /><br /> <span data-ttu-id="cdc89-116">Fornece as definições para o controle.</span><span class="sxs-lookup"><span data-stu-id="cdc89-116">Provides the definitions for the control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="cdc89-117">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="cdc89-117">Parent Elements</span></span>

|<span data-ttu-id="cdc89-118">Elemento</span><span class="sxs-lookup"><span data-stu-id="cdc89-118">Element</span></span>|<span data-ttu-id="cdc89-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="cdc89-119">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="cdc89-120">Elemento GroupBy para exibição (formato)</span><span class="sxs-lookup"><span data-stu-id="cdc89-120">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)|<span data-ttu-id="cdc89-121">Define como o Windows PowerShell exibe um novo grupo de objetos.</span><span class="sxs-lookup"><span data-stu-id="cdc89-121">Defines how Windows PowerShell displays a new group of objects.</span></span>|

## <a name="remarks"></a><span data-ttu-id="cdc89-122">Comentários</span><span class="sxs-lookup"><span data-stu-id="cdc89-122">Remarks</span></span>

## <a name="see-also"></a><span data-ttu-id="cdc89-123">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="cdc89-123">See Also</span></span>

[<span data-ttu-id="cdc89-124">Elemento CustomEntries para CustomControl para GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="cdc89-124">CustomEntries Element for CustomControl for GroupBy (Format)</span></span>](./customentries-element-for-customcontrol-for-groupby-format.md)

[<span data-ttu-id="cdc89-125">Elemento GroupBy para exibição (formato)</span><span class="sxs-lookup"><span data-stu-id="cdc89-125">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)

[<span data-ttu-id="cdc89-126">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="cdc89-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)