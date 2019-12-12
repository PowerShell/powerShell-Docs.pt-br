---
title: Elemento ListControl (formato) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 37beeb0b-7a81-4747-becb-e309e17278fb
caps.latest.revision: 12
ms.openlocfilehash: 7a117c25b0d117dc846ba8e060e31e838b5edd52
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "72362775"
---
# <a name="listcontrol-element-format"></a><span data-ttu-id="113f7-102">Elemento ListControl (formato)</span><span class="sxs-lookup"><span data-stu-id="113f7-102">ListControl Element (Format)</span></span>

<span data-ttu-id="113f7-103">Define um formato de lista para a exibição.</span><span class="sxs-lookup"><span data-stu-id="113f7-103">Defines a list format for the view.</span></span>

<span data-ttu-id="113f7-104">Elemento de configuração (Format) elemento ViewDefinitions (Format) View element (Format) elemento ListControl (Format)</span><span class="sxs-lookup"><span data-stu-id="113f7-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="113f7-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="113f7-105">Syntax</span></span>

```xml
<ListControl>
  <ListEntries>...</ListEntries>
</ListControl>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="113f7-106">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="113f7-106">Attributes and Elements</span></span>

<span data-ttu-id="113f7-107">As seções a seguir descrevem os atributos, os elementos filho e o elemento pai do elemento `ListControl`.</span><span class="sxs-lookup"><span data-stu-id="113f7-107">The following sections describe the attributes, child elements, and the parent element of the `ListControl` element.</span></span> <span data-ttu-id="113f7-108">Este elemento deve conter apenas um único elemento filho.</span><span class="sxs-lookup"><span data-stu-id="113f7-108">This element must contain only a single child element.</span></span>

### <a name="attributes"></a><span data-ttu-id="113f7-109">Atributos</span><span class="sxs-lookup"><span data-stu-id="113f7-109">Attributes</span></span>

<span data-ttu-id="113f7-110">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="113f7-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="113f7-111">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="113f7-111">Child Elements</span></span>

|<span data-ttu-id="113f7-112">Elemento</span><span class="sxs-lookup"><span data-stu-id="113f7-112">Element</span></span>|<span data-ttu-id="113f7-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="113f7-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="113f7-114">Elemento ListEntries (formato)</span><span class="sxs-lookup"><span data-stu-id="113f7-114">ListEntries Element (Format)</span></span>](./listentries-element-for-listcontrol-format.md)|<span data-ttu-id="113f7-115">Elemento obrigatório.</span><span class="sxs-lookup"><span data-stu-id="113f7-115">Required element.</span></span><br /><br /> <span data-ttu-id="113f7-116">Fornece as definições da exibição de lista.</span><span class="sxs-lookup"><span data-stu-id="113f7-116">Provides the definitions of the list view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="113f7-117">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="113f7-117">Parent Elements</span></span>

|<span data-ttu-id="113f7-118">Elemento</span><span class="sxs-lookup"><span data-stu-id="113f7-118">Element</span></span>|<span data-ttu-id="113f7-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="113f7-119">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="113f7-120">Elemento View (formato)</span><span class="sxs-lookup"><span data-stu-id="113f7-120">View Element (Format)</span></span>](./view-element-format.md)|<span data-ttu-id="113f7-121">Define uma exibição que é usada para exibir os membros de um ou mais objetos.</span><span class="sxs-lookup"><span data-stu-id="113f7-121">Defines a view that is used to display the members of one or more objects.</span></span>|

## <a name="remarks"></a><span data-ttu-id="113f7-122">Comentários</span><span class="sxs-lookup"><span data-stu-id="113f7-122">Remarks</span></span>

<span data-ttu-id="113f7-123">Para obter mais informações sobre como criar um modo de exibição de lista, consulte [criando uma exibição de lista](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="113f7-123">For more information about creating a list view, see [Creating a List View](./creating-a-list-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="113f7-124">Exemplo</span><span class="sxs-lookup"><span data-stu-id="113f7-124">Example</span></span>

<span data-ttu-id="113f7-125">Este exemplo mostra um modo de exibição de lista para o objeto [System. ServiceProcess. ServiceController](/dotnet/api/System.ServiceProcess.ServiceController) .</span><span class="sxs-lookup"><span data-stu-id="113f7-125">This example shows a list view for the [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) object.</span></span>

```
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <ListControl>
    <ListEntries>
      <ListEntry>...</ListEntry>
    </ListEntries>
  </ListControl>
</View>
```

## <a name="see-also"></a><span data-ttu-id="113f7-126">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="113f7-126">See Also</span></span>

[<span data-ttu-id="113f7-127">Elemento View (formato)</span><span class="sxs-lookup"><span data-stu-id="113f7-127">View Element (Format)</span></span>](./view-element-format.md)

[<span data-ttu-id="113f7-128">Elemento ListEntries (formato)</span><span class="sxs-lookup"><span data-stu-id="113f7-128">ListEntries Element (Format)</span></span>](./listentries-element-for-listcontrol-format.md)

[<span data-ttu-id="113f7-129">Criando um modo de exibição de lista</span><span class="sxs-lookup"><span data-stu-id="113f7-129">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="113f7-130">Escrevendo um arquivo de tipos e formatação do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="113f7-130">Writing a Windows PowerShell Formatting and Types File</span></span>](./writing-a-powershell-formatting-file.md)
