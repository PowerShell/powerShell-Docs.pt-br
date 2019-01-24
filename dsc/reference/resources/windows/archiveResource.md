---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Recurso Archive da DSC
ms.openlocfilehash: d5ccd242d000a0907c6768f30923764be6bf20a3
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54047021"
---
# <a name="dsc-archive-resource"></a><span data-ttu-id="d0a7d-103">Recurso Archive da DSC</span><span class="sxs-lookup"><span data-stu-id="d0a7d-103">DSC Archive Resource</span></span>

> <span data-ttu-id="d0a7d-104">Aplica-se a: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="d0a7d-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="d0a7d-105">O recurso Archive na Configuração de Estado Desejado (DSC) do Windows PowerShell fornece um mecanismo para descompactar arquivos mortos (.zip) em um caminho específico.</span><span class="sxs-lookup"><span data-stu-id="d0a7d-105">The Archive resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to unpack archive (.zip) files at a specific path.</span></span>

## <a name="syntax"></a><span data-ttu-id="d0a7d-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="d0a7d-106">Syntax</span></span>
```MOF
Archive [string] #ResourceName
{
    Destination = [string]
    Path = [string]
    [ Checksum = [string] { CreatedDate | ModifiedDate | SHA-1 | SHA-256 | SHA-512 } ]
    [ DependsOn = [string[]] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Force = [bool] ]
    [ Validate = [bool] ]
}
```

## <a name="properties"></a><span data-ttu-id="d0a7d-107">Propriedades</span><span class="sxs-lookup"><span data-stu-id="d0a7d-107">Properties</span></span>

|  <span data-ttu-id="d0a7d-108">Propriedade</span><span class="sxs-lookup"><span data-stu-id="d0a7d-108">Property</span></span>  |  <span data-ttu-id="d0a7d-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="d0a7d-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="d0a7d-110">Destination</span><span class="sxs-lookup"><span data-stu-id="d0a7d-110">Destination</span></span>| <span data-ttu-id="d0a7d-111">Especifica o local onde você deseja garantir que o conteúdo do arquivo seja extraído.</span><span class="sxs-lookup"><span data-stu-id="d0a7d-111">Specifies the location where you want to ensure the archive contents are extracted.</span></span>|
| <span data-ttu-id="d0a7d-112">Caminho</span><span class="sxs-lookup"><span data-stu-id="d0a7d-112">Path</span></span>| <span data-ttu-id="d0a7d-113">Especifica o caminho de origem do arquivo morto.</span><span class="sxs-lookup"><span data-stu-id="d0a7d-113">Specifies the source path of the archive file.</span></span>|
| <span data-ttu-id="d0a7d-114">__Checksum__</span><span class="sxs-lookup"><span data-stu-id="d0a7d-114">__Checksum__</span></span>| <span data-ttu-id="d0a7d-115">Define o tipo que deve ser usado para determinar se dois arquivos são iguais.</span><span class="sxs-lookup"><span data-stu-id="d0a7d-115">Defines the type to use when determining whether two files are the same.</span></span> <span data-ttu-id="d0a7d-116">Se __Checksum__ não for especificado, somente o nome de arquivo ou diretório será usado para comparação.</span><span class="sxs-lookup"><span data-stu-id="d0a7d-116">If __Checksum__ is not specified, only the file or directory name is used for comparison.</span></span> <span data-ttu-id="d0a7d-117">Os valores válidos incluem: SHA-1, SHA-256, SHA-512, createdDate, modifiedDate e none (padrão).</span><span class="sxs-lookup"><span data-stu-id="d0a7d-117">Valid values include: SHA-1, SHA-256, SHA-512, createdDate, modifiedDate, none (default).</span></span> <span data-ttu-id="d0a7d-118">Se você especificar __Checksum__ sem __Validate__, ocorrerá uma falha na configuração.</span><span class="sxs-lookup"><span data-stu-id="d0a7d-118">If you specify __Checksum__ without __Validate__, the configuration will fail.</span></span>|
| <span data-ttu-id="d0a7d-119">Ensure</span><span class="sxs-lookup"><span data-stu-id="d0a7d-119">Ensure</span></span>| <span data-ttu-id="d0a7d-120">Determina se é necessário verificar se o conteúdo do arquivo existe em __Destination__.</span><span class="sxs-lookup"><span data-stu-id="d0a7d-120">Determines whether to check if the content of the archive exists at the __Destination__.</span></span> <span data-ttu-id="d0a7d-121">Defina essa propriedade como __Present__ para garantir que o conteúdo exista.</span><span class="sxs-lookup"><span data-stu-id="d0a7d-121">Set this property to __Present__ to ensure the contents exist.</span></span> <span data-ttu-id="d0a7d-122">Defina-a como __Absent__ para garantir que não exista.</span><span class="sxs-lookup"><span data-stu-id="d0a7d-122">Set it to __Absent__ to ensure they do not exist.</span></span> <span data-ttu-id="d0a7d-123">O valor padrão é __Present__.</span><span class="sxs-lookup"><span data-stu-id="d0a7d-123">The default value is __Present__.</span></span>|
| <span data-ttu-id="d0a7d-124">DependsOn</span><span class="sxs-lookup"><span data-stu-id="d0a7d-124">DependsOn</span></span> | <span data-ttu-id="d0a7d-125">Indica que a configuração de outro recurso deve ser executada antes de ele ser configurado.</span><span class="sxs-lookup"><span data-stu-id="d0a7d-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="d0a7d-126">Por exemplo, se a ID do bloco de script de configuração do recurso que você deseja executar primeiro for ResourceName e seu tipo for __ResourceType__, a sintaxe para usar essa propriedade será `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="d0a7d-126">For example, if the ID of the resource configuration script block that you want to run first is ResourceName and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="d0a7d-127">Validar</span><span class="sxs-lookup"><span data-stu-id="d0a7d-127">Validate</span></span>| <span data-ttu-id="d0a7d-128">Usa a propriedade Checksum para determinar se o arquivo corresponde à assinatura.</span><span class="sxs-lookup"><span data-stu-id="d0a7d-128">Uses the Checksum property to determine if the archive matches the signature.</span></span> <span data-ttu-id="d0a7d-129">Se você especificar Checksum sem Validate, ocorrerá uma falha na configuração.</span><span class="sxs-lookup"><span data-stu-id="d0a7d-129">If you specify Checksum without Validate, the configuration will fail.</span></span> <span data-ttu-id="d0a7d-130">Se você especificar Validate sem Checksum, uma soma de verificação SHA-256 será usada por padrão.</span><span class="sxs-lookup"><span data-stu-id="d0a7d-130">If you specify Validate without Checksum, a SHA-256 checksum is used by default.</span></span>|
| <span data-ttu-id="d0a7d-131">Force</span><span class="sxs-lookup"><span data-stu-id="d0a7d-131">Force</span></span>| <span data-ttu-id="d0a7d-132">Determinadas operações de arquivo (como substituição de um arquivo ou exclusão de um diretório que não esteja vazio) resultarão em erro.</span><span class="sxs-lookup"><span data-stu-id="d0a7d-132">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="d0a7d-133">O uso da propriedade Force substitui esses erros.</span><span class="sxs-lookup"><span data-stu-id="d0a7d-133">Using the Force property overrides such errors.</span></span> <span data-ttu-id="d0a7d-134">O valor padrão é False.</span><span class="sxs-lookup"><span data-stu-id="d0a7d-134">The default value is False.</span></span>|

## <a name="example"></a><span data-ttu-id="d0a7d-135">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d0a7d-135">Example</span></span>

<span data-ttu-id="d0a7d-136">O exemplo a seguir mostra como usar o recurso Archive para garantir que o conteúdo de um arquivo morto chamado Test.zip exista e seja extraído em um destino específico.</span><span class="sxs-lookup"><span data-stu-id="d0a7d-136">The following example shows how to use the Archive resource to ensure that the contents of an archive file called Test.zip exist and are extracted at a given destination.</span></span>

```
Archive ArchiveExample {
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Path = "C:\Users\Public\Documents\Test.zip"
    Destination = "C:\Users\Public\Documents\ExtractionPath"
}
```