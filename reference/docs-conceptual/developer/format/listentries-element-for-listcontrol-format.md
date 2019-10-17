---
title: Elemento ListEntries para ListControl (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b62e81cc-4175-40fa-829f-634245b09f86
caps.latest.revision: 12
ms.openlocfilehash: aaf16702e485135b5299ccb43a2b62db2d9f5762
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72362755"
---
# <a name="listentries-element-for-listcontrol-format"></a><span data-ttu-id="f8cdb-102">Elemento ListEntries para ListControl (formato)</span><span class="sxs-lookup"><span data-stu-id="f8cdb-102">ListEntries Element for ListControl (Format)</span></span>

<span data-ttu-id="f8cdb-103">Fornece as definições da exibição de lista.</span><span class="sxs-lookup"><span data-stu-id="f8cdb-103">Provides the definitions of the list view.</span></span> <span data-ttu-id="f8cdb-104">A exibição de lista deve especificar uma ou mais definições.</span><span class="sxs-lookup"><span data-stu-id="f8cdb-104">The list view must specify one or more definitions.</span></span>

<span data-ttu-id="f8cdb-105">Elemento de configuração (Format) elemento ViewDefinitions (Format) View element (Format) ListControl Element (Format) o elemento ListEntries (Format)</span><span class="sxs-lookup"><span data-stu-id="f8cdb-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="f8cdb-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="f8cdb-106">Syntax</span></span>

```xml
<ListEntries>
  <ListEntry>...</ListEntry>
</ListEntries>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="f8cdb-107">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="f8cdb-107">Attributes and Elements</span></span>

<span data-ttu-id="f8cdb-108">As seções a seguir descrevem os atributos, os elementos filho e o elemento pai do elemento `ListEntries`.</span><span class="sxs-lookup"><span data-stu-id="f8cdb-108">The following sections describe the attributes, child elements, and the parent element of the `ListEntries` element.</span></span> <span data-ttu-id="f8cdb-109">Pelo menos um elemento filho deve ser especificado.</span><span class="sxs-lookup"><span data-stu-id="f8cdb-109">At least one child element must be specified.</span></span>

### <a name="attributes"></a><span data-ttu-id="f8cdb-110">Atributos</span><span class="sxs-lookup"><span data-stu-id="f8cdb-110">Attributes</span></span>

<span data-ttu-id="f8cdb-111">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="f8cdb-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="f8cdb-112">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="f8cdb-112">Child Elements</span></span>

|<span data-ttu-id="f8cdb-113">Elemento</span><span class="sxs-lookup"><span data-stu-id="f8cdb-113">Element</span></span>|<span data-ttu-id="f8cdb-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="f8cdb-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="f8cdb-115">Elemento ListEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="f8cdb-115">ListEntry Element (Format)</span></span>](./listentry-element-for-listcontrol-format.md)|<span data-ttu-id="f8cdb-116">Fornece uma definição da exibição de lista.</span><span class="sxs-lookup"><span data-stu-id="f8cdb-116">Provides a definition of the list view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="f8cdb-117">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="f8cdb-117">Parent Elements</span></span>

|<span data-ttu-id="f8cdb-118">Elemento</span><span class="sxs-lookup"><span data-stu-id="f8cdb-118">Element</span></span>|<span data-ttu-id="f8cdb-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="f8cdb-119">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="f8cdb-120">Elemento ListControl (formato)</span><span class="sxs-lookup"><span data-stu-id="f8cdb-120">ListControl Element (Format)</span></span>](./listcontrol-element-format.md)|<span data-ttu-id="f8cdb-121">Define um formato de lista para a exibição.</span><span class="sxs-lookup"><span data-stu-id="f8cdb-121">Defines a list format for the view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="f8cdb-122">Comentários</span><span class="sxs-lookup"><span data-stu-id="f8cdb-122">Remarks</span></span>

<span data-ttu-id="f8cdb-123">Para obter mais informações sobre exibições de lista, consulte [exibição de lista](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="f8cdb-123">For more information about list views, see [List View](./creating-a-list-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="f8cdb-124">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f8cdb-124">Example</span></span>

<span data-ttu-id="f8cdb-125">Este exemplo mostra os elementos XML que definem a exibição de lista para o objeto [System. ServiceProcess. ServiceController](/dotnet/api/System.ServiceProcess.ServiceController) .</span><span class="sxs-lookup"><span data-stu-id="f8cdb-125">This example shows the XML elements that define the list view for the [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) object.</span></span>

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <ListControl>
    <ListEntries>
      <ListEntry>
        <ListItems>...</ListItems>
      </ListEntry>
    </ListEntries>
  </ListControl>
</View>
```

## <a name="see-also"></a><span data-ttu-id="f8cdb-126">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="f8cdb-126">See Also</span></span>

[<span data-ttu-id="f8cdb-127">Elemento ListControl (formato)</span><span class="sxs-lookup"><span data-stu-id="f8cdb-127">ListControl Element (Format)</span></span>](./listcontrol-element-format.md)

[<span data-ttu-id="f8cdb-128">Elemento ListEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="f8cdb-128">ListEntry Element (Format)</span></span>](./listentry-element-for-listcontrol-format.md)

[<span data-ttu-id="f8cdb-129">Exibição de lista</span><span class="sxs-lookup"><span data-stu-id="f8cdb-129">List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="f8cdb-130">Escrevendo um arquivo de tipos e formatação do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8cdb-130">Writing a Windows PowerShell Formatting and Types File</span></span>](./writing-a-powershell-formatting-file.md)