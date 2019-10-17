---
title: Elemento TypeName para EntrySelectedBy para TableControl (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fd872ada-d476-4c4d-a788-ccac3f983070
caps.latest.revision: 10
ms.openlocfilehash: 7bbb47268a23fcb37a34e2287a6ce949313a13bb
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72361625"
---
# <a name="typename-element-for-entryselectedby-for-tablecontrol-format"></a><span data-ttu-id="0de3d-102">Elemento TypeName para EntrySelectedBy para TableControl (formato)</span><span class="sxs-lookup"><span data-stu-id="0de3d-102">TypeName Element for EntrySelectedBy for TableControl (Format)</span></span>

<span data-ttu-id="0de3d-103">Especifica um tipo .NET que usa essa entrada da exibição de tabela.</span><span class="sxs-lookup"><span data-stu-id="0de3d-103">Specifies a .NET type that uses this entry of the table view.</span></span> <span data-ttu-id="0de3d-104">Não há nenhum limite para o número de tipos que podem ser especificados para uma entrada de tabela.</span><span class="sxs-lookup"><span data-stu-id="0de3d-104">There is no limit to the number of types that can be specified for a table entry.</span></span>

<span data-ttu-id="0de3d-105">Elemento de configuração (Format) elemento ViewDefinitions (Format) View element (Format) TableControl elemento (Format) TableRowEntries Element (Format) TableRowEntry elemento (Format) EntrySelectedBy Element (Format) TypeName Element para EntrySelectedBy para TableRowEntry (formato)</span><span class="sxs-lookup"><span data-stu-id="0de3d-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableRowEntries Element (Format) TableRowEntry Element (Format) EntrySelectedBy Element (Format) TypeName Element for EntrySelectedBy for TableRowEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="0de3d-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="0de3d-106">Syntax</span></span>

```xml
<TypeName>Nameof.NetType</TypeName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="0de3d-107">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="0de3d-107">Attributes and Elements</span></span>

<span data-ttu-id="0de3d-108">As seções a seguir descrevem atributos, elementos filho e o elemento pai do elemento `TypeName`.</span><span class="sxs-lookup"><span data-stu-id="0de3d-108">The following sections describe attributes, child elements, and the parent element of the `TypeName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="0de3d-109">Atributos</span><span class="sxs-lookup"><span data-stu-id="0de3d-109">Attributes</span></span>

<span data-ttu-id="0de3d-110">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="0de3d-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="0de3d-111">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="0de3d-111">Child Elements</span></span>

<span data-ttu-id="0de3d-112">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="0de3d-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="0de3d-113">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="0de3d-113">Parent Elements</span></span>

|<span data-ttu-id="0de3d-114">Elemento</span><span class="sxs-lookup"><span data-stu-id="0de3d-114">Element</span></span>|<span data-ttu-id="0de3d-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="0de3d-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0de3d-116">Elemento EntrySelectedBy (Format)</span><span class="sxs-lookup"><span data-stu-id="0de3d-116">EntrySelectedBy Element (Format)</span></span>](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)|<span data-ttu-id="0de3d-117">Define os tipos .NET que usam essa entrada ou a condição que deve existir para que essa entrada seja usada.</span><span class="sxs-lookup"><span data-stu-id="0de3d-117">Defines the .NET types that use this entry or the condition that must exist for this entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="0de3d-118">Valor de texto</span><span class="sxs-lookup"><span data-stu-id="0de3d-118">Text Value</span></span>

<span data-ttu-id="0de3d-119">Especifique o nome do tipo .NET.</span><span class="sxs-lookup"><span data-stu-id="0de3d-119">Specify the name of the .NET type.</span></span>

## <a name="remarks"></a><span data-ttu-id="0de3d-120">Comentários</span><span class="sxs-lookup"><span data-stu-id="0de3d-120">Remarks</span></span>

<span data-ttu-id="0de3d-121">Cada entrada de lista deve ter pelo menos um nome de tipo, um conjunto de seleção ou uma condição de seleção definida.</span><span class="sxs-lookup"><span data-stu-id="0de3d-121">Each list entry must have at least one type name, selection set, or selection condition defined.</span></span>

<span data-ttu-id="0de3d-122">Para obter mais informações sobre os componentes de uma exibição de tabela, consulte [criando uma exibição de tabela](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="0de3d-122">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="0de3d-123">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="0de3d-123">See Also</span></span>

[<span data-ttu-id="0de3d-124">Criando uma exibição de tabela</span><span class="sxs-lookup"><span data-stu-id="0de3d-124">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="0de3d-125">Elemento EntrySelectedBy (Format)</span><span class="sxs-lookup"><span data-stu-id="0de3d-125">EntrySelectedBy Element (Format)</span></span>](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)

[<span data-ttu-id="0de3d-126">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="0de3d-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)