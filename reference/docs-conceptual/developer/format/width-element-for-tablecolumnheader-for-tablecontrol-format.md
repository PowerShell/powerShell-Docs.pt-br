---
title: Elemento Width para TableColumnHeader para TableControl (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 94eb0535-8002-4f17-9a2b-4be75ec20e5c
caps.latest.revision: 18
ms.openlocfilehash: 4a25c9d81df670dc10955065bfb66766cdb1bd33
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72367865"
---
# <a name="width-element-for-tablecolumnheader-for-tablecontrol-format"></a><span data-ttu-id="6c78f-102">Elemento Width para TableColumnHeader para TableControl (formato)</span><span class="sxs-lookup"><span data-stu-id="6c78f-102">Width Element for TableColumnHeader for TableControl (Format)</span></span>

<span data-ttu-id="6c78f-103">Define a largura (em caracteres) de uma coluna.</span><span class="sxs-lookup"><span data-stu-id="6c78f-103">Defines the width (in characters) of a column.</span></span>

<span data-ttu-id="6c78f-104">Elemento de configuração (Format) elemento ViewDefinitions (Format) exibir elemento (Format) TableControl Element (Format) TableHeaders elemento para TableControl (Format) TableColumnHeader Element TableHeaders for TableControl (Format) largura Element para TableColumnHeader para TableControl (formato)</span><span class="sxs-lookup"><span data-stu-id="6c78f-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableHeaders Element for TableControl (Format) TableColumnHeader Element TableHeaders for TableControl (Format) Width Element for TableColumnHeader for TableControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="6c78f-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="6c78f-105">Syntax</span></span>

```xml
<Width>NumberOfCharacters</Width>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="6c78f-106">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="6c78f-106">Attributes and Elements</span></span>

<span data-ttu-id="6c78f-107">As seções a seguir descrevem os atributos, os elementos filho e o elemento pai do elemento `Width` usado ao definir cabeçalhos de coluna.</span><span class="sxs-lookup"><span data-stu-id="6c78f-107">The following sections describe the attributes, child elements, and parent element of the `Width` element used when defining column headers.</span></span>

### <a name="attributes"></a><span data-ttu-id="6c78f-108">Atributos</span><span class="sxs-lookup"><span data-stu-id="6c78f-108">Attributes</span></span>

<span data-ttu-id="6c78f-109">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="6c78f-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="6c78f-110">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="6c78f-110">Child Elements</span></span>

<span data-ttu-id="6c78f-111">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="6c78f-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="6c78f-112">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="6c78f-112">Parent Elements</span></span>

|<span data-ttu-id="6c78f-113">Elemento</span><span class="sxs-lookup"><span data-stu-id="6c78f-113">Element</span></span>|<span data-ttu-id="6c78f-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="6c78f-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="6c78f-115">Elemento TableColumnHeader para TableHeaders para TableControl (Format)</span><span class="sxs-lookup"><span data-stu-id="6c78f-115">TableColumnHeader Element for TableHeaders for TableControl (Format)</span></span>](./tablecolumnheader-element-format.md)|<span data-ttu-id="6c78f-116">Define um rótulo, uma largura e um alinhamento dos dados para uma coluna da tabela.</span><span class="sxs-lookup"><span data-stu-id="6c78f-116">Defines a label, width, and alignment of the data for a column of the table.</span></span>|

## <a name="text-value"></a><span data-ttu-id="6c78f-117">Valor de texto</span><span class="sxs-lookup"><span data-stu-id="6c78f-117">Text Value</span></span>

<span data-ttu-id="6c78f-118">Quando possível, especifique uma largura (em caracteres) que seja maior que o comprimento dos valores de propriedade exibidos.</span><span class="sxs-lookup"><span data-stu-id="6c78f-118">When at all possible, specify a width (in characters) that is greater than the length of the displayed property values.</span></span>

## <a name="remarks"></a><span data-ttu-id="6c78f-119">Comentários</span><span class="sxs-lookup"><span data-stu-id="6c78f-119">Remarks</span></span>

<span data-ttu-id="6c78f-120">Para obter mais informações sobre os componentes de uma exibição de tabela, consulte [criando uma exibição de tabela](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="6c78f-120">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="6c78f-121">Exemplo</span><span class="sxs-lookup"><span data-stu-id="6c78f-121">Example</span></span>

<span data-ttu-id="6c78f-122">O exemplo a seguir mostra um elemento `TableColumnHeader` cuja largura é 16 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6c78f-122">The following example shows a `TableColumnHeader` element whose width is 16 characters.</span></span>

```xml
<TableColumnHeader>
  <Label>Column 1</Label)
  <Width>16</Width>
  <Alignment>Left</Alignment>
</TableColumnHeader>
```

## <a name="see-also"></a><span data-ttu-id="6c78f-123">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="6c78f-123">See Also</span></span>

[<span data-ttu-id="6c78f-124">Criando uma exibição de tabela</span><span class="sxs-lookup"><span data-stu-id="6c78f-124">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="6c78f-125">Elemento TableColumnHeader para TableHeader para TableControl (Format)</span><span class="sxs-lookup"><span data-stu-id="6c78f-125">TableColumnHeader Element for TableHeader for TableControl (Format)</span></span>](./tablecolumnheader-element-format.md)

[<span data-ttu-id="6c78f-126">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c78f-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
