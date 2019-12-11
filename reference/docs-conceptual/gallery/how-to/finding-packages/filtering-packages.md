---
ms.date: 06/12/2017
contributor: JKeithB
keywords: galeria,powershell,cmdlet,psgallery
title: Filtrando resultados da pesquisa
ms.openlocfilehash: 13270a310613a974e1588a9f56d443a936cfebb8
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "71328037"
---
# <a name="filtering-search-results"></a><span data-ttu-id="5b6e4-103">Filtrando resultados da pesquisa</span><span class="sxs-lookup"><span data-stu-id="5b6e4-103">Filtering search results</span></span>

<span data-ttu-id="5b6e4-104">A [guia Pacotes](https://www.powershellgallery.com/packages) exibe todos os pacotes disponíveis na Galeria do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b6e4-104">The [Packages tab](https://www.powershellgallery.com/packages) displays all available packages in the PowerShell Gallery.</span></span>

<span data-ttu-id="5b6e4-105">Há várias maneiras de filtrar, classificar e pesquisar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="5b6e4-105">There are several ways to filter, sort, and search the packages.</span></span>
<span data-ttu-id="5b6e4-106">Para ver mais detalhes sobre um pacote específico, clique nele.</span><span class="sxs-lookup"><span data-stu-id="5b6e4-106">To see more details about a particular package, click the package.</span></span>

## <a name="filter-by"></a><span data-ttu-id="5b6e4-107">Filtrar Por</span><span class="sxs-lookup"><span data-stu-id="5b6e4-107">Filter By</span></span>

<span data-ttu-id="5b6e4-108">O menu suspenso em "Filtrar Por" permite aos usuários filtrar os resultados por:</span><span class="sxs-lookup"><span data-stu-id="5b6e4-108">The drop-down under "Filter By" allows users to filter the results by:</span></span>
- <span data-ttu-id="5b6e4-109">Incluir pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="5b6e4-109">Include Prerelease</span></span>
- <span data-ttu-id="5b6e4-110">Apenas estável</span><span class="sxs-lookup"><span data-stu-id="5b6e4-110">Stable Only</span></span>

<span data-ttu-id="5b6e4-111">Para saber mais sobre itens de "pré-lançamento" e "estáveis", confira o artigo [Prerelease Versioning Added to PowerShellGet and PowerShell Gallery](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) (Controle de versão de pré-lançamento adicionado ao PowerShellGet e à Galeria do PowerShell), no blog da equipe do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b6e4-111">For information about "Prerelease" and "Stable", see [Prerelease Versioning Added to PowerShellGet and PowerShell Gallery](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) in the PowerShell Team Blog.</span></span>

<span data-ttu-id="5b6e4-112">Com as caixas de seleção no menu suspenso, os usuários podem filtrar os resultados por:</span><span class="sxs-lookup"><span data-stu-id="5b6e4-112">The checkboxes under the drop-down allow users to filter the results by:</span></span>
- <span data-ttu-id="5b6e4-113">Tipos de Pacote</span><span class="sxs-lookup"><span data-stu-id="5b6e4-113">Package Types</span></span>
  - <span data-ttu-id="5b6e4-114">Módulo</span><span class="sxs-lookup"><span data-stu-id="5b6e4-114">Module</span></span>
  - <span data-ttu-id="5b6e4-115">script</span><span class="sxs-lookup"><span data-stu-id="5b6e4-115">Script</span></span>
- <span data-ttu-id="5b6e4-116">Categorias</span><span class="sxs-lookup"><span data-stu-id="5b6e4-116">Categories</span></span>
  - <span data-ttu-id="5b6e4-117">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="5b6e4-117">Cmdlet</span></span>
  - <span data-ttu-id="5b6e4-118">Recurso de DSC</span><span class="sxs-lookup"><span data-stu-id="5b6e4-118">DSC Resource</span></span>
  - <span data-ttu-id="5b6e4-119">Função</span><span class="sxs-lookup"><span data-stu-id="5b6e4-119">Function</span></span>
  - <span data-ttu-id="5b6e4-120">Capacidade da função</span><span class="sxs-lookup"><span data-stu-id="5b6e4-120">Role Capability</span></span>
  - <span data-ttu-id="5b6e4-121">Fluxo de Trabalho</span><span class="sxs-lookup"><span data-stu-id="5b6e4-121">Workflow</span></span>

<span data-ttu-id="5b6e4-122">Para ver somente módulos na Galeria do PowerShell, marque a opção Módulo nos Tipos de Pacote.</span><span class="sxs-lookup"><span data-stu-id="5b6e4-122">To see only modules in the PowerShell Gallery, check Module in the Package Types.</span></span>
<span data-ttu-id="5b6e4-123">Da mesma forma, para ver somente scripts na Galeria do PowerShell, marque a opção Script nos Tipos de Pacote.</span><span class="sxs-lookup"><span data-stu-id="5b6e4-123">Similarly, to see only scripts in the PowerShell Gallery, check Script in the Package Types.</span></span>

> [!NOTE]
> <span data-ttu-id="5b6e4-124">Os filtros são inclusivos.</span><span class="sxs-lookup"><span data-stu-id="5b6e4-124">Filters are inclusive.</span></span>
> <span data-ttu-id="5b6e4-125">Exemplo: um pacote que contém cmdlets e funções será exibido se Cmdlet ou Função (ou ambos) estiverem marcados.</span><span class="sxs-lookup"><span data-stu-id="5b6e4-125">Example: A package containing both cmdlets and functions will appear if either Cmdlet or Function (or both) are checked.</span></span>
> <span data-ttu-id="5b6e4-126">Se nenhum dos dois for selecionado, o pacote não será exibido.</span><span class="sxs-lookup"><span data-stu-id="5b6e4-126">If neither are selected, the package will not appear.</span></span>
> <span data-ttu-id="5b6e4-127">De forma semelhante, se todas as categorias forem selecionadas, apenas pacotes que contêm uma dessas categorias serão exibidos.</span><span class="sxs-lookup"><span data-stu-id="5b6e4-127">Similarly, if all categories are selected, only packages containing one of those categories will appear.</span></span>
> <span data-ttu-id="5b6e4-128">**Pacotes que não pertencem a nenhuma dessas categorias não serão exibidos.**</span><span class="sxs-lookup"><span data-stu-id="5b6e4-128">**Packages that do not belong to any of those categories will not appear.**</span></span>

## <a name="sort-by"></a><span data-ttu-id="5b6e4-129">Classificar Por</span><span class="sxs-lookup"><span data-stu-id="5b6e4-129">Sort By</span></span>

<span data-ttu-id="5b6e4-130">O menu suspenso Classificar Por permite aos usuários classificar os resultados por:</span><span class="sxs-lookup"><span data-stu-id="5b6e4-130">The Sort By drop-down allows users to sort the results by:</span></span>
- <span data-ttu-id="5b6e4-131">Popularidade – a popularidade é determinada pela Contagem de Downloads</span><span class="sxs-lookup"><span data-stu-id="5b6e4-131">Popularity - Popularity is determined by Download Count</span></span>
- <span data-ttu-id="5b6e4-132">A a Z – em ordem alfabética por nome do pacote</span><span class="sxs-lookup"><span data-stu-id="5b6e4-132">A-Z - Alphabetically by package name</span></span>
- <span data-ttu-id="5b6e4-133">Recentes – os pacotes aparecem na ordem da data de publicação</span><span class="sxs-lookup"><span data-stu-id="5b6e4-133">Recent - Packages appear in order of publish date</span></span>

## <a name="search-box"></a><span data-ttu-id="5b6e4-134">Caixa de Pesquisa</span><span class="sxs-lookup"><span data-stu-id="5b6e4-134">Search Box</span></span>

<span data-ttu-id="5b6e4-135">A Caixa de Pesquisa permite que os usuários pesquisem pacotes por palavras-chave.</span><span class="sxs-lookup"><span data-stu-id="5b6e4-135">The Search Box allows users to search the packages on keywords.</span></span>
<span data-ttu-id="5b6e4-136">Para saber mais, confira [Sintaxe de Pesquisa da Galeria](search-syntax.md).</span><span class="sxs-lookup"><span data-stu-id="5b6e4-136">For more information, see [Gallery Search Syntax](search-syntax.md).</span></span>
