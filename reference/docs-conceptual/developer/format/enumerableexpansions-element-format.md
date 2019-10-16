---
title: Elemento EnumerableExpansions (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 50c33892-2ade-44c2-906c-81e5f5ca21f2
caps.latest.revision: 9
ms.openlocfilehash: 1ecbda8a3b623757517019105e3b1ee46ccbb55c
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72363295"
---
# <a name="enumerableexpansions-element-format"></a><span data-ttu-id="51718-102">Elemento EnumerableExpansions (formato)</span><span class="sxs-lookup"><span data-stu-id="51718-102">EnumerableExpansions Element (Format)</span></span>

<span data-ttu-id="51718-103">Define como os objetos de coleção .NET são expandidos quando são exibidos em uma exibição.</span><span class="sxs-lookup"><span data-stu-id="51718-103">Defines how .NET collection objects are expanded when they are displayed in a view.</span></span>

<span data-ttu-id="51718-104">Elemento de configuração (Format) DefaultSettings Element (Format) elemento EnumerableExpansions (Format)</span><span class="sxs-lookup"><span data-stu-id="51718-104">Configuration Element (Format) DefaultSettings Element (Format) EnumerableExpansions Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="51718-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="51718-105">Syntax</span></span>

```xml
<EnumerableExpansions>
  <EnumerableExpansion>...</EnumerableExpansion>
</EnumerableExpansions>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="51718-106">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="51718-106">Attributes and Elements</span></span>

<span data-ttu-id="51718-107">As seções a seguir descrevem atributos, elementos filho e o elemento pai do elemento `EnumerableExpansions`.</span><span class="sxs-lookup"><span data-stu-id="51718-107">The following sections describe attributes, child elements, and the parent element of the `EnumerableExpansions` element.</span></span> <span data-ttu-id="51718-108">Não há nenhum limite para o número de elementos filho que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="51718-108">There is no limit to the number of child elements that you can use.</span></span>

### <a name="attributes"></a><span data-ttu-id="51718-109">Atributos</span><span class="sxs-lookup"><span data-stu-id="51718-109">Attributes</span></span>

<span data-ttu-id="51718-110">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="51718-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="51718-111">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="51718-111">Child Elements</span></span>

|<span data-ttu-id="51718-112">Elemento</span><span class="sxs-lookup"><span data-stu-id="51718-112">Element</span></span>|<span data-ttu-id="51718-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="51718-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="51718-114">Elemento EnumerableExpansion (Format)</span><span class="sxs-lookup"><span data-stu-id="51718-114">EnumerableExpansion Element (Format)</span></span>](./enumerableexpansion-element-format.md)|<span data-ttu-id="51718-115">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="51718-115">Optional element.</span></span><br /><br /> <span data-ttu-id="51718-116">Define os objetos de coleção .NET específicos que são expandidos quando são exibidos em uma exibição.</span><span class="sxs-lookup"><span data-stu-id="51718-116">Defines the specific .NET collection objects that are expanded when they are displayed in a view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="51718-117">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="51718-117">Parent Elements</span></span>

|<span data-ttu-id="51718-118">Elemento</span><span class="sxs-lookup"><span data-stu-id="51718-118">Element</span></span>|<span data-ttu-id="51718-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="51718-119">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="51718-120">Elemento DefaultSettings (formato)</span><span class="sxs-lookup"><span data-stu-id="51718-120">DefaultSettings Element (Format)</span></span>](./defaultsettings-element-format.md)|<span data-ttu-id="51718-121">Define as configurações comuns que se aplicam a todas as exibições do arquivo de formatação.</span><span class="sxs-lookup"><span data-stu-id="51718-121">Defines common settings that apply to all the views of the formatting file.</span></span>|

## <a name="remarks"></a><span data-ttu-id="51718-122">Comentários</span><span class="sxs-lookup"><span data-stu-id="51718-122">Remarks</span></span>

<span data-ttu-id="51718-123">Esse elemento é usado para definir como os objetos de coleção e os objetos na coleção são exibidos.</span><span class="sxs-lookup"><span data-stu-id="51718-123">This element is used to define how collection objects and the objects in the collection are displayed.</span></span> <span data-ttu-id="51718-124">Nesse caso, um objeto de coleção refere-se a qualquer objeto que ofereça suporte à interface **System. Collections. ICollection** .</span><span class="sxs-lookup"><span data-stu-id="51718-124">In this case, a collection object refers to any object that supports the  **System.Collections.ICollection** interface.</span></span>

## <a name="see-also"></a><span data-ttu-id="51718-125">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="51718-125">See Also</span></span>

[<span data-ttu-id="51718-126">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="51718-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
