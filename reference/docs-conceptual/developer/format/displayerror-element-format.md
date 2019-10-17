---
title: Elemento DisplayError (Format) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 45c45800-a87d-456e-b07c-12d4d8c27c67
caps.latest.revision: 8
ms.openlocfilehash: 2c6a3d678ca68dc0d189f6ab981fdea5fef894cb
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72363985"
---
# <a name="displayerror-element-format"></a><span data-ttu-id="aeb9b-102">Elemento DisplayError (formato)</span><span class="sxs-lookup"><span data-stu-id="aeb9b-102">DisplayError Element (Format)</span></span>

<span data-ttu-id="aeb9b-103">Especifica que a cadeia de caracteres #ERR é exibida quando ocorre um erro exibindo uma parte dos dados.</span><span class="sxs-lookup"><span data-stu-id="aeb9b-103">Specifies that the string #ERR is displayed when an error occurs displaying a piece of data.</span></span>

<span data-ttu-id="aeb9b-104">Elemento de configuração (Format) DefaultSettings Element (Format) elemento DisplayError (Format)</span><span class="sxs-lookup"><span data-stu-id="aeb9b-104">Configuration Element (Format) DefaultSettings Element (Format) DisplayError Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="aeb9b-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="aeb9b-105">Syntax</span></span>

```xml
<DisplayError/>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="aeb9b-106">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="aeb9b-106">Attributes and Elements</span></span>

<span data-ttu-id="aeb9b-107">As seções a seguir descrevem atributos, elementos filho e o elemento pai do elemento `DisplayError`.</span><span class="sxs-lookup"><span data-stu-id="aeb9b-107">The following sections describe attributes, child elements, and the parent element of the `DisplayError` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="aeb9b-108">Atributos</span><span class="sxs-lookup"><span data-stu-id="aeb9b-108">Attributes</span></span>

<span data-ttu-id="aeb9b-109">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="aeb9b-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="aeb9b-110">Elementos filhos</span><span class="sxs-lookup"><span data-stu-id="aeb9b-110">Child Elements</span></span>

<span data-ttu-id="aeb9b-111">Nenhum.</span><span class="sxs-lookup"><span data-stu-id="aeb9b-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="aeb9b-112">Elementos pais</span><span class="sxs-lookup"><span data-stu-id="aeb9b-112">Parent Elements</span></span>

|<span data-ttu-id="aeb9b-113">Elemento</span><span class="sxs-lookup"><span data-stu-id="aeb9b-113">Element</span></span>|<span data-ttu-id="aeb9b-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="aeb9b-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="aeb9b-115">Elemento DefaultSettings (formato)</span><span class="sxs-lookup"><span data-stu-id="aeb9b-115">DefaultSettings Element (Format)</span></span>](./defaultsettings-element-format.md)|<span data-ttu-id="aeb9b-116">Define as configurações comuns que se aplicam a todas as exibições do arquivo de formatação.</span><span class="sxs-lookup"><span data-stu-id="aeb9b-116">Defines common settings that apply to all the views of the formatting file.</span></span>|

## <a name="remarks"></a><span data-ttu-id="aeb9b-117">Comentários</span><span class="sxs-lookup"><span data-stu-id="aeb9b-117">Remarks</span></span>

<span data-ttu-id="aeb9b-118">Por padrão, quando ocorre um erro durante a tentativa de exibir um dado, o local dos dados é deixado em branco.</span><span class="sxs-lookup"><span data-stu-id="aeb9b-118">By default, when an error occurs while trying to display a piece of data, the location of the data is left blank.</span></span> <span data-ttu-id="aeb9b-119">Quando esse elemento é definido como true, a cadeia de caracteres #ERR será exibida.</span><span class="sxs-lookup"><span data-stu-id="aeb9b-119">When this element is set to true, the #ERR string will be displayed.</span></span>

## <a name="see-also"></a><span data-ttu-id="aeb9b-120">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="aeb9b-120">See Also</span></span>

[<span data-ttu-id="aeb9b-121">Elemento DefaultSettings (formato)</span><span class="sxs-lookup"><span data-stu-id="aeb9b-121">DefaultSettings Element (Format)</span></span>](./defaultsettings-element-format.md)

[<span data-ttu-id="aeb9b-122">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="aeb9b-122">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)