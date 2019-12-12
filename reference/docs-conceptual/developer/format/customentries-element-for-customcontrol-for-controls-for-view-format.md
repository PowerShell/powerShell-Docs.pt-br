---
title: Elemento CustomEntries para CustomControl para controles para View (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3485958a-ba87-4932-907c-a8f140c4abdb
caps.latest.revision: 8
ms.openlocfilehash: 4856aee930285781a101868bd6cb67824585bce1
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "72368805"
---
# <a name="customentries-element-for-customcontrol-for-controls-for-view-format"></a><span data-ttu-id="d913b-102">Elemento CustomEntries para CustomControl para Controls para View (formato)</span><span class="sxs-lookup"><span data-stu-id="d913b-102">CustomEntries Element for CustomControl for Controls for View (Format)</span></span>

<span data-ttu-id="d913b-103">Fornece as definições para o controle.</span><span class="sxs-lookup"><span data-stu-id="d913b-103">Provides the definitions for the control.</span></span> <span data-ttu-id="d913b-104">Esse elemento é usado ao definir controles que podem ser usados por uma exibição.</span><span class="sxs-lookup"><span data-stu-id="d913b-104">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="d913b-105">Elemento de configuração (Format) elemento ViewDefinitions (Format) exibir elemento (Format) controle elemento (Format) elemento Control para controles para o elemento View (Format) CustomControl para controle para controles para o elemento View (Format) CustomEntries para CustomControl para controles para exibição (formato)</span><span class="sxs-lookup"><span data-stu-id="d913b-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="d913b-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="d913b-106">Syntax</span></span>

```xml
<CustomEntries>
  <CustomEntry>...</CustomEntry>
</CustomEntries>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="d913b-107">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="d913b-107">Attributes and Elements</span></span>

<span data-ttu-id="d913b-108">As seções a seguir descrevem atributos, elementos filho e elementos pai do elemento `CustomEntries`.</span><span class="sxs-lookup"><span data-stu-id="d913b-108">The following sections describe attributes, child elements, and parent elements of the `CustomEntries` element.</span></span> <span data-ttu-id="d913b-109">Não há nenhum limite máximo para o número de elementos filho que podem ser especificados.</span><span class="sxs-lookup"><span data-stu-id="d913b-109">There is no maximum limit to the number of child elements that can be specified.</span></span>

### <a name="attributes"></a><span data-ttu-id="d913b-110">Atributos</span><span class="sxs-lookup"><span data-stu-id="d913b-110">Attributes</span></span>

<span data-ttu-id="d913b-111">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="d913b-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="d913b-112">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="d913b-112">Child Elements</span></span>

|<span data-ttu-id="d913b-113">Elemento</span><span class="sxs-lookup"><span data-stu-id="d913b-113">Element</span></span>|<span data-ttu-id="d913b-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="d913b-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="d913b-115">Elemento CustomEntry para CustomEntries para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="d913b-115">CustomEntry Element for CustomEntries for Controls for View (Format)</span></span>](./customentry-element-for-customentries-for-controls-for-view-format.md)|<span data-ttu-id="d913b-116">Elemento obrigatório.</span><span class="sxs-lookup"><span data-stu-id="d913b-116">Required element.</span></span><br /><br /> <span data-ttu-id="d913b-117">Fornece uma definição do controle.</span><span class="sxs-lookup"><span data-stu-id="d913b-117">Provides a definition of the control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="d913b-118">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="d913b-118">Parent Elements</span></span>

|<span data-ttu-id="d913b-119">Elemento</span><span class="sxs-lookup"><span data-stu-id="d913b-119">Element</span></span>|<span data-ttu-id="d913b-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="d913b-120">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="d913b-121">Elemento CustomControl para controle de controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="d913b-121">CustomControl Element for Control for Controls for View (Format)</span></span>](./customcontrol-element-for-control-for-controls-for-view-format.md)|<span data-ttu-id="d913b-122">Define o controle usado pela exibição.</span><span class="sxs-lookup"><span data-stu-id="d913b-122">Defines the control used by the view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="d913b-123">Comentários</span><span class="sxs-lookup"><span data-stu-id="d913b-123">Remarks</span></span>

<span data-ttu-id="d913b-124">Na maioria dos casos, um controle tem apenas uma definição, que é especificada em um único elemento `CustomEntry`.</span><span class="sxs-lookup"><span data-stu-id="d913b-124">In most cases, a control has only one definition, which is specified in a single `CustomEntry` element.</span></span> <span data-ttu-id="d913b-125">No entanto, é possível fornecer várias definições se você quiser usar o mesmo controle para exibir diferentes objetos .NET.</span><span class="sxs-lookup"><span data-stu-id="d913b-125">However, it is possible to provide multiple definitions if you want to use the same control to display different .NET objects.</span></span> <span data-ttu-id="d913b-126">Nesses casos, você pode definir um elemento `CustomEntry` para cada objeto ou conjunto de objetos.</span><span class="sxs-lookup"><span data-stu-id="d913b-126">In those cases, you can define a `CustomEntry` element for each object or set of objects.</span></span>

## <a name="see-also"></a><span data-ttu-id="d913b-127">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="d913b-127">See Also</span></span>

[<span data-ttu-id="d913b-128">Elemento CustomEntry para CustomEntries para controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="d913b-128">CustomEntry Element for CustomEntries for Controls for View (Format)</span></span>](./customentry-element-for-customentries-for-controls-for-view-format.md)

[<span data-ttu-id="d913b-129">Elemento CustomControl para controle de controles para View (Format)</span><span class="sxs-lookup"><span data-stu-id="d913b-129">CustomControl Element for Control for Controls for View (Format)</span></span>](./customcontrol-element-for-control-for-controls-for-view-format.md)

[<span data-ttu-id="d913b-130">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="d913b-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
