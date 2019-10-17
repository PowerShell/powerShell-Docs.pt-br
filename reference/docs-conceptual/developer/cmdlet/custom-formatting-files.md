---
title: Arquivos de formatação personalizados | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 85d27545-8097-4010-9947-6d8b3ce2eac0
caps.latest.revision: 15
ms.openlocfilehash: 71c1c181058c5646c817b90d9832976a78c6c7de
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72369825"
---
# <a name="custom-formatting-files"></a><span data-ttu-id="c2415-102">Arquivos de formatação personalizada</span><span class="sxs-lookup"><span data-stu-id="c2415-102">Custom Formatting Files</span></span>

<span data-ttu-id="c2415-103">O formato de exibição dos objetos retornados por cmdlets, funções e scripts é definido usando arquivos de formatação (arquivos Format. ps1xml).</span><span class="sxs-lookup"><span data-stu-id="c2415-103">The display format for the objects returned by cmdlets, functions, and scripts are defined using formatting files (format.ps1xml files).</span></span> <span data-ttu-id="c2415-104">Vários desses arquivos são fornecidos pelo Windows PowerShell para definir o formato de exibição padrão para os objetos retornados pelos cmdlets do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2415-104">Several of these files are provided by Windows PowerShell to define the default display format for those objects returned by Windows PowerShell cmdlets.</span></span> <span data-ttu-id="c2415-105">No entanto, você também pode criar seus próprios arquivos de formatação personalizados para substituir os formatos de exibição padrão ou para definir a exibição de objetos retornados por seus próprios comandos.</span><span class="sxs-lookup"><span data-stu-id="c2415-105">However, you can also create your own custom formatting files to overwrite the default display formats or to define the display of objects returned by your own commands.</span></span>

<span data-ttu-id="c2415-106">O Windows PowerShell usa os dados nesses arquivos de formatação para determinar o que é exibido e como os dados são formatados.</span><span class="sxs-lookup"><span data-stu-id="c2415-106">Windows PowerShell uses the data in these formatting files to determine what is displayed and how the data is formatted.</span></span> <span data-ttu-id="c2415-107">Os dados exibidos podem incluir as propriedades de um objeto ou o valor de um bloco de script.</span><span class="sxs-lookup"><span data-stu-id="c2415-107">The displayed data can include the properties of an object or the value of a script block.</span></span>  <span data-ttu-id="c2415-108">Blocos de script são usados se você quiser exibir algum valor que não esteja disponível diretamente das propriedades de um objeto.</span><span class="sxs-lookup"><span data-stu-id="c2415-108">Script blocks are used if you want to display some value that is not available directly from the properties of an object.</span></span> <span data-ttu-id="c2415-109">Por exemplo, talvez você queira adicionar o valor de duas propriedades de um objeto e exibir a soma como uma parte separada dos dados.</span><span class="sxs-lookup"><span data-stu-id="c2415-109">For example, you may want to add the value of two properties of an object and display the sum as a separate piece of data.</span></span> <span data-ttu-id="c2415-110">Ao escrever seu próprio arquivo de formatação, você precisará definir *modos* de exibição para os objetos que deseja exibir.</span><span class="sxs-lookup"><span data-stu-id="c2415-110">When you write your own formatting file, you will need to define *views* for the objects that you want to display.</span></span> <span data-ttu-id="c2415-111">Você pode definir uma única exibição para cada objeto, pode definir uma única exibição para vários objetos ou pode definir várias exibições para o mesmo objeto.</span><span class="sxs-lookup"><span data-stu-id="c2415-111">You can define a single view for each object, you can define a single view for multiple objects, or you can define multiple views for the same object.</span></span> <span data-ttu-id="c2415-112">Não há nenhum limite para o número de exibições que você pode definir.</span><span class="sxs-lookup"><span data-stu-id="c2415-112">There is no limit to the number of views that you can define.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2415-113">Os arquivos de formatação não determinam os elementos de um objeto que são retornados para o pipeline.</span><span class="sxs-lookup"><span data-stu-id="c2415-113">Formatting files do not determine the elements of an object that are returned to the pipeline.</span></span> <span data-ttu-id="c2415-114">Quando um objeto é retornado para o pipeline, todos os membros desse objeto estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="c2415-114">When an object is returned to the pipeline, all members of that object are available.</span></span>

## <a name="format-views"></a><span data-ttu-id="c2415-115">Exibições de formato</span><span class="sxs-lookup"><span data-stu-id="c2415-115">Format Views</span></span>

<span data-ttu-id="c2415-116">As exibições de formatação podem exibir objetos em um formato de tabela, um formato de lista, um formato amplo e um formato personalizado.</span><span class="sxs-lookup"><span data-stu-id="c2415-116">Formatting views can display objects in a table format, a list format, a wide format, and a custom format.</span></span> <span data-ttu-id="c2415-117">Na maior parte, cada definição de formatação é descrita por um conjunto de marcas XML que descrevem uma exibição.</span><span class="sxs-lookup"><span data-stu-id="c2415-117">For the most part, each formatting definition is described by a set of XML tags that describe a view.</span></span> <span data-ttu-id="c2415-118">Cada exibição contém o nome da exibição, os objetos que usam a exibição e os elementos da exibição, como as informações de coluna e linha de uma exibição de tabela.</span><span class="sxs-lookup"><span data-stu-id="c2415-118">Each view contains the name of the view, the objects that use the view, and the elements of the view, such as the column and row information for a table view.</span></span>

<span data-ttu-id="c2415-119">As exibições a seguir estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="c2415-119">The following views are available.</span></span>

<span data-ttu-id="c2415-120">Exibição de tabela lista as propriedades de um objeto ou um valor de bloco de script em uma ou mais colunas.</span><span class="sxs-lookup"><span data-stu-id="c2415-120">Table view Lists the properties of an object or a script block value in one or more columns.</span></span> <span data-ttu-id="c2415-121">Cada coluna representa uma propriedade do objeto ou um valor de bloco de script.</span><span class="sxs-lookup"><span data-stu-id="c2415-121">Each column represents a property of the object or a script block value.</span></span> <span data-ttu-id="c2415-122">Você pode definir um modo de exibição de tabela que exibe todas as propriedades de um objeto, um subconjunto das propriedades de um objeto ou uma combinação de propriedades e valores de bloco de script.</span><span class="sxs-lookup"><span data-stu-id="c2415-122">You can define a table view that displays all the properties of an object, a subset of the properties of an object, or a combination of properties and script block values.</span></span> <span data-ttu-id="c2415-123">Cada linha da tabela representa um objeto retornado.</span><span class="sxs-lookup"><span data-stu-id="c2415-123">Each row of the table represents a returned object.</span></span> <span data-ttu-id="c2415-124">Para obter mais informações sobre essa exibição, consulte [exibição de tabela](../format/creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="c2415-124">For more information about this view, see [Table View](../format/creating-a-table-view.md).</span></span>

<span data-ttu-id="c2415-125">A exibição de lista lista as propriedades de um objeto ou um valor de bloco de script em uma única coluna.</span><span class="sxs-lookup"><span data-stu-id="c2415-125">List view Lists the properties of an object or a script block value in a single column.</span></span> <span data-ttu-id="c2415-126">Cada linha da lista exibe um rótulo opcional ou o nome da propriedade seguido pelo valor da propriedade ou bloco de script.</span><span class="sxs-lookup"><span data-stu-id="c2415-126">Each row of the list displays an optional label or the property name followed by the value of the property or script block.</span></span> <span data-ttu-id="c2415-127">Para obter mais informações sobre essa exibição, consulte [exibição de lista](../format/creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="c2415-127">For more information about this view, see [List View](../format/creating-a-list-view.md).</span></span>

<span data-ttu-id="c2415-128">Exibição ampla lista uma única propriedade de um objeto ou um valor de bloco de script em uma ou mais colunas.</span><span class="sxs-lookup"><span data-stu-id="c2415-128">Wide view Lists a single property of an object or a script block value in one or more columns.</span></span> <span data-ttu-id="c2415-129">Não há rótulo ou cabeçalho para esta exibição.</span><span class="sxs-lookup"><span data-stu-id="c2415-129">There is no label or header for this view.</span></span> <span data-ttu-id="c2415-130">Para obter mais informações sobre essa exibição, consulte [Wide View](../format/creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="c2415-130">For more information about this view, see [Wide View](../format/creating-a-wide-view.md).</span></span>

<span data-ttu-id="c2415-131">Exibição personalizada exibe uma exibição personalizável de propriedades de objeto ou valores de bloco de script que não aderem à estrutura rígida de exibições de tabela, exibições de lista ou exibições amplas.</span><span class="sxs-lookup"><span data-stu-id="c2415-131">Custom view Displays a customizable view of object properties or script block values that does not adhere to the rigid structure of table views, list views, or wide views.</span></span> <span data-ttu-id="c2415-132">Você pode definir uma exibição personalizada autônoma ou pode definir uma exibição personalizada que é usada por outra exibição, como uma exibição de tabela ou exibição de lista.</span><span class="sxs-lookup"><span data-stu-id="c2415-132">You can define a standalone custom view, or you can define a custom view that is used by another view, such as a table view or list view.</span></span> <span data-ttu-id="c2415-133">Para obter mais informações sobre essa exibição, consulte [modo de exibição personalizado](../format/creating-custom-controls.md).</span><span class="sxs-lookup"><span data-stu-id="c2415-133">For more information about this view, see [Custom View](../format/creating-custom-controls.md).</span></span>

## <a name="view-xml-elements"></a><span data-ttu-id="c2415-134">Exibir elementos XML</span><span class="sxs-lookup"><span data-stu-id="c2415-134">View XML Elements</span></span>

<span data-ttu-id="c2415-135">O exemplo a seguir mostra as marcas XML usadas para definir um modo de exibição de tabela que contém duas colunas.</span><span class="sxs-lookup"><span data-stu-id="c2415-135">The following example shows the XML tags used to define a table view that contains two columns.</span></span> <span data-ttu-id="c2415-136">O elemento [ViewDefinitions](../format/viewdefinitions-element-format.md) é o elemento contêiner para todas as exibições definidas no arquivo de formatação.</span><span class="sxs-lookup"><span data-stu-id="c2415-136">The [ViewDefinitions](../format/viewdefinitions-element-format.md) element is the container element for all the views defined in the formatting file.</span></span> <span data-ttu-id="c2415-137">O elemento [View](../format/view-element-format.md) define a tabela, lista, largura ou exibição personalizada específica.</span><span class="sxs-lookup"><span data-stu-id="c2415-137">The [View](../format/view-element-format.md) element defines the specific table, list, wide, or custom view.</span></span> <span data-ttu-id="c2415-138">Dentro de cada exibição, o elemento [Name](../format/name-element-for-view-format.md) especifica o nome da exibição, o elemento [ViewSelectedBy](../format/viewselectedby-element-format.md) define os objetos que usam a exibição e os elementos de controle diferentes (como o elemento `TableControl`) definem o formato da exibição.</span><span class="sxs-lookup"><span data-stu-id="c2415-138">Within each view, the [Name](../format/name-element-for-view-format.md) element specifies the name of the view, the [ViewSelectedBy](../format/viewselectedby-element-format.md) element defines the objects that use the view, and the different control elements (such as the `TableControl` element) define the format of the view.</span></span>

```xml
ViewDefinitions
  <View>
    <Name>Name of View</Name>
    <ViewSelectedBy>
      <TypeName>Object to display using this view</TypeName>
      <TypeName>Object to display using this view</TypeName>
    </ViewSelectedBy>
    <TableControl>
      <TableHeaders>
        <TableColumnHeader>
          <Width></Width>
        </TableColumnHeader>
        <TableColumnHeader>
          <Width></Width>
        </TableColumnHeader>
      </TableHeaders>
      <TableRowEntries>
        <TableRowEntry>
          <TableColumnItems>
            <TableColumnItem>
              <PropertyName>Header for column 1</PropertyName>
            </TableColumnItem>
            <TableColumnItem>
              <PropertyName>Header for column 2</PropertyName>
            </TableColumnItem>
          </TableColumnItems>
        </TableRowEntry>
      </TableRowEntries>
    </TableControl)
  </View>
</ViewDefinitions>

```

## <a name="see-also"></a><span data-ttu-id="c2415-139">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="c2415-139">See Also</span></span>

[<span data-ttu-id="c2415-140">Exibição de tabela</span><span class="sxs-lookup"><span data-stu-id="c2415-140">Table View</span></span>](../format/creating-a-table-view.md)

[<span data-ttu-id="c2415-141">Exibição de lista</span><span class="sxs-lookup"><span data-stu-id="c2415-141">List View</span></span>](../format/creating-a-list-view.md)

[<span data-ttu-id="c2415-142">Exibição ampla</span><span class="sxs-lookup"><span data-stu-id="c2415-142">Wide View</span></span>](../format/creating-a-wide-view.md)

[<span data-ttu-id="c2415-143">Exibição personalizada</span><span class="sxs-lookup"><span data-stu-id="c2415-143">Custom View</span></span>](../format/creating-custom-controls.md)

<span data-ttu-id="c2415-144">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md) (Escrevendo um Cmdlet do Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="c2415-144">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md)</span></span>