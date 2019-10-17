---
title: Elemento ListEntry para ListControl (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6d16bca8-d025-432d-aa84-8b607b8af3ae
caps.latest.revision: 12
ms.openlocfilehash: 1a3bafd4ca94aee70e869c699f7a4ef8befc5511
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72362745"
---
# <a name="listentry-element-for-listcontrol-format"></a><span data-ttu-id="a5922-102">Elemento ListEntry para ListControl (formato)</span><span class="sxs-lookup"><span data-stu-id="a5922-102">ListEntry Element for ListControl (Format)</span></span>

<span data-ttu-id="a5922-103">Fornece uma definição da exibição de lista.</span><span class="sxs-lookup"><span data-stu-id="a5922-103">Provides a definition of the list view.</span></span>

<span data-ttu-id="a5922-104">Elemento de configuração (Format) elemento ViewDefinitions (Format) View element (Format) ListControl Element (Format) o elemento ListEntries (Format) ListEntry Element (Format)</span><span class="sxs-lookup"><span data-stu-id="a5922-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element (Format) ListEntry Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="a5922-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="a5922-105">Syntax</span></span>

```xml
<ListEntry>
  <EntrySelectedBy>...</EntrySelectedBy>
  <ListItems>...</ListItems>
</ListEntry>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="a5922-106">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="a5922-106">Attributes and Elements</span></span>

<span data-ttu-id="a5922-107">As seções a seguir descrevem os atributos, os elementos filho e o elemento pai do elemento `ListEntry`.</span><span class="sxs-lookup"><span data-stu-id="a5922-107">The following sections describe the attributes, child elements, and the parent element of the `ListEntry` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="a5922-108">Atributos</span><span class="sxs-lookup"><span data-stu-id="a5922-108">Attributes</span></span>

<span data-ttu-id="a5922-109">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="a5922-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="a5922-110">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="a5922-110">Child Elements</span></span>

|<span data-ttu-id="a5922-111">Elemento</span><span class="sxs-lookup"><span data-stu-id="a5922-111">Element</span></span>|<span data-ttu-id="a5922-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="a5922-112">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="a5922-113">Elemento EntrySelectedBy para ListEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="a5922-113">EntrySelectedBy Element for ListEntry (Format)</span></span>](./entryselectedby-element-for-listentry-for-listcontrol-format.md)|<span data-ttu-id="a5922-114">Elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="a5922-114">Optional element.</span></span><br /><br /> <span data-ttu-id="a5922-115">Define os objetos .NET que usam essa definição de exibição de lista ou a condição que deve existir para que essa definição seja usada.</span><span class="sxs-lookup"><span data-stu-id="a5922-115">Defines the .NET objects that use this list view definition or the condition that must exist for this definition to be used.</span></span>|
|[<span data-ttu-id="a5922-116">Elemento ListItems (formato)</span><span class="sxs-lookup"><span data-stu-id="a5922-116">ListItems Element (Format)</span></span>](./listitems-element-for-listentry-for-listcontrol-format.md)|<span data-ttu-id="a5922-117">Elemento obrigatório.</span><span class="sxs-lookup"><span data-stu-id="a5922-117">Required element.</span></span><br /><br /> <span data-ttu-id="a5922-118">Define as propriedades e os scripts cujos valores são exibidos pela exibição de lista.</span><span class="sxs-lookup"><span data-stu-id="a5922-118">Defines the properties and scripts whose values are displayed by the list view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="a5922-119">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="a5922-119">Parent Elements</span></span>

|<span data-ttu-id="a5922-120">Elemento</span><span class="sxs-lookup"><span data-stu-id="a5922-120">Element</span></span>|<span data-ttu-id="a5922-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="a5922-121">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="a5922-122">Elemento ListEntries (formato)</span><span class="sxs-lookup"><span data-stu-id="a5922-122">ListEntries Element (Format)</span></span>](./listentries-element-for-listcontrol-format.md)|<span data-ttu-id="a5922-123">Fornece as definições da exibição de lista.</span><span class="sxs-lookup"><span data-stu-id="a5922-123">Provides the definitions of the list view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="a5922-124">Comentários</span><span class="sxs-lookup"><span data-stu-id="a5922-124">Remarks</span></span>

<span data-ttu-id="a5922-125">Uma exibição de lista é um formato de lista que exibe valores de propriedade ou valores de script para cada objeto.</span><span class="sxs-lookup"><span data-stu-id="a5922-125">A list view is a list format that displays property values or script values for each object.</span></span> <span data-ttu-id="a5922-126">Para obter mais informações sobre exibições de lista, consulte [criando uma exibição de lista](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="a5922-126">For more information about list views, see [Creating a List View](./creating-a-list-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="a5922-127">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a5922-127">Example</span></span>

<span data-ttu-id="a5922-128">Este exemplo mostra os elementos XML que definem a exibição de lista para o objeto [System. ServiceProcess. ServiceController](/dotnet/api/System.ServiceProcess.ServiceController) .</span><span class="sxs-lookup"><span data-stu-id="a5922-128">This example shows the XML elements that define the list view for the [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) object.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="a5922-129">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="a5922-129">See Also</span></span>

[<span data-ttu-id="a5922-130">Criando um modo de exibição de lista</span><span class="sxs-lookup"><span data-stu-id="a5922-130">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="a5922-131">Elemento EntrySelectedBy para ListEntry (Format)</span><span class="sxs-lookup"><span data-stu-id="a5922-131">EntrySelectedBy Element for ListEntry (Format)</span></span>](./entryselectedby-element-for-listentry-for-listcontrol-format.md)

[<span data-ttu-id="a5922-132">Elemento ListEntries (formato)</span><span class="sxs-lookup"><span data-stu-id="a5922-132">ListEntries Element (Format)</span></span>](./listentries-element-for-listcontrol-format.md)

[<span data-ttu-id="a5922-133">Elemento ListItems (formato)</span><span class="sxs-lookup"><span data-stu-id="a5922-133">ListItems Element (Format)</span></span>](./listitems-element-for-listentry-for-listcontrol-format.md)

[<span data-ttu-id="a5922-134">Escrevendo um arquivo de tipos e formatação do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5922-134">Writing a Windows PowerShell Formatting and Types File</span></span>](./writing-a-powershell-formatting-file.md)