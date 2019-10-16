---
title: Elemento CustomEntry para CustomControl para controles para configuração (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9dfba86f-29b2-473c-9e98-9d679176acce
caps.latest.revision: 11
ms.openlocfilehash: 497485a388d1cdc834ecc1d1079b0714a7d7f9db
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72364065"
---
# <a name="customentry-element-for-customcontrol-for-controls-for-configuration-format"></a><span data-ttu-id="decf5-102">Elemento CustomEntry para CustomControl para Controls para Configuration (formato)</span><span class="sxs-lookup"><span data-stu-id="decf5-102">CustomEntry Element for CustomControl for Controls for Configuration (Format)</span></span>

<span data-ttu-id="decf5-103">Fornece uma definição do controle comum.</span><span class="sxs-lookup"><span data-stu-id="decf5-103">Provides a definition of the common control.</span></span> <span data-ttu-id="decf5-104">Esse elemento é usado ao definir um controle comum que pode ser usado por todas as exibições no arquivo de formatação.</span><span class="sxs-lookup"><span data-stu-id="decf5-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="decf5-105">Elemento de configuração (Format) controla o elemento de controle de configuração (formato) para controles para o elemento de configuração (Format) CustomControl para controle para o elemento de configuração (Format) CustomEntries para CustomControl para configuração ( Format) elemento CustomEntry para CustomControl para controles para configuração (Format)</span><span class="sxs-lookup"><span data-stu-id="decf5-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="decf5-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="decf5-106">Syntax</span></span>

```xml
<CustomEntry>
  <EntrySelectedBy>...</EntrySelectedBy>
  <CustomItem>...</CustomItem>
</CustomEntry>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="decf5-107">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="decf5-107">Attributes and Elements</span></span>

<span data-ttu-id="decf5-108">As seções a seguir descrevem atributos, elementos filho e o elemento pai do elemento `CustomEntry`.</span><span class="sxs-lookup"><span data-stu-id="decf5-108">The following sections describe attributes, child elements, and the parent element of the `CustomEntry` element.</span></span> <span data-ttu-id="decf5-109">Você deve especificar os itens exibidos pela definição.</span><span class="sxs-lookup"><span data-stu-id="decf5-109">You must specify the items displayed by the definition.</span></span>

### <a name="attributes"></a><span data-ttu-id="decf5-110">Atributos</span><span class="sxs-lookup"><span data-stu-id="decf5-110">Attributes</span></span>

<span data-ttu-id="decf5-111">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="decf5-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="decf5-112">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="decf5-112">Child Elements</span></span>

|<span data-ttu-id="decf5-113">Elemento</span><span class="sxs-lookup"><span data-stu-id="decf5-113">Element</span></span>|<span data-ttu-id="decf5-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="decf5-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="decf5-115">Elemento EntrySelectedBy para CustomEntry para controles para configuração (Format)</span><span class="sxs-lookup"><span data-stu-id="decf5-115">EntrySelectedBy Element for CustomEntry for Controls for Configuration (Format)</span></span>](./entryselectedby-element-for-customentry-for-controls-for-configuration-format.md)|<span data-ttu-id="decf5-116">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="decf5-116">Optional element.</span></span><br /><br /> <span data-ttu-id="decf5-117">Define os tipos .NET que usam a definição do controle comum ou a condição que deve existir para que esse controle seja usado.</span><span class="sxs-lookup"><span data-stu-id="decf5-117">Defines the .NET types that use the definition of the common control or the condition that must exist for this control to be used.</span></span>|
|[<span data-ttu-id="decf5-118">Elemento CustomItem para CustomEntry para controles de configuração</span><span class="sxs-lookup"><span data-stu-id="decf5-118">CustomItem Element for CustomEntry for Controls for Configuration</span></span>](./customitem-element-for-customentry-for-controls-for-configuration-format.md)|<span data-ttu-id="decf5-119">Elemento obrigatório.</span><span class="sxs-lookup"><span data-stu-id="decf5-119">Required element.</span></span><br /><br /> <span data-ttu-id="decf5-120">Define quais dados são exibidos pelo controle e como eles são exibidos.</span><span class="sxs-lookup"><span data-stu-id="decf5-120">Defines what data is displayed by the control and how it is displayed.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="decf5-121">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="decf5-121">Parent Elements</span></span>

|<span data-ttu-id="decf5-122">Elemento</span><span class="sxs-lookup"><span data-stu-id="decf5-122">Element</span></span>|<span data-ttu-id="decf5-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="decf5-123">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="decf5-124">Elemento CustomEntries para CustomControl para configuração (formato)</span><span class="sxs-lookup"><span data-stu-id="decf5-124">CustomEntries Element for CustomControl for Configuration (Format)</span></span>](./customentries-element-for-customcontrol-for-controls-for-configuration-format.md)|<span data-ttu-id="decf5-125">Fornece as definições do controle comum.</span><span class="sxs-lookup"><span data-stu-id="decf5-125">Provides the definitions of the common control.</span></span>|

## <a name="remarks"></a><span data-ttu-id="decf5-126">Comentários</span><span class="sxs-lookup"><span data-stu-id="decf5-126">Remarks</span></span>

<span data-ttu-id="decf5-127">Na maioria dos casos, apenas uma definição é necessária para cada controle personalizado comum, mas é possível ter várias definições se você quiser usar o mesmo controle para exibir diferentes objetos .NET.</span><span class="sxs-lookup"><span data-stu-id="decf5-127">In most cases, only one definition is required for each common custom control, but it is possible to have multiple definitions if you want to use the same control to display different .NET objects.</span></span> <span data-ttu-id="decf5-128">Nesses casos, você pode fornecer uma definição separada para cada objeto ou conjunto de objetos.</span><span class="sxs-lookup"><span data-stu-id="decf5-128">In those cases, you can provide a separate definition for each object or set of objects.</span></span>

## <a name="see-also"></a><span data-ttu-id="decf5-129">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="decf5-129">See Also</span></span>

[<span data-ttu-id="decf5-130">Elemento CustomEntries para CustomControl para configuração (formato)</span><span class="sxs-lookup"><span data-stu-id="decf5-130">CustomEntries Element for CustomControl for Configuration (Format)</span></span>](./customentries-element-for-customcontrol-for-controls-for-configuration-format.md)

[<span data-ttu-id="decf5-131">Elemento CustomItem para CustomEntry para controles de configuração</span><span class="sxs-lookup"><span data-stu-id="decf5-131">CustomItem Element for CustomEntry for Controls for Configuration</span></span>](./customitem-element-for-customentry-for-controls-for-configuration-format.md)

[<span data-ttu-id="decf5-132">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="decf5-132">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
