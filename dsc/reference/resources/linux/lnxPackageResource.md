---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Recurso nxPackage de DSC para Linux
ms.openlocfilehash: 64bb89a95bd6cbaea4e74b8a9979de52428fef3f
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54047010"
---
# <a name="dsc-for-linux-nxpackage-resource"></a><span data-ttu-id="cb3a4-103">Recurso nxPackage de DSC para Linux</span><span class="sxs-lookup"><span data-stu-id="cb3a4-103">DSC for Linux nxPackage Resource</span></span>

<span data-ttu-id="cb3a4-104">O recurso **nxPackage** na Configuração de Estado Desejado (DSC) do Windows PowerShell fornece um mecanismo para gerenciar pacotes em um nó do Linux.</span><span class="sxs-lookup"><span data-stu-id="cb3a4-104">The **nxPackage** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage packages on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="cb3a4-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="cb3a4-105">Syntax</span></span>

```
nxPackage <string> #ResourceName
{
    Name = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ PackageManager = <string> { Yum | Apt | Zypper } ]
    [ PackageGroup = <bool>]
    [ Arguments = <string> ]
    [ ReturnCode = <uint32> ]
    [ LogPath = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="cb3a4-106">Propriedades</span><span class="sxs-lookup"><span data-stu-id="cb3a4-106">Properties</span></span>

|  <span data-ttu-id="cb3a4-107">Propriedade</span><span class="sxs-lookup"><span data-stu-id="cb3a4-107">Property</span></span> |  <span data-ttu-id="cb3a4-108">Descrição</span><span class="sxs-lookup"><span data-stu-id="cb3a4-108">Description</span></span> |
|---|---|
| <span data-ttu-id="cb3a4-109">Nome</span><span class="sxs-lookup"><span data-stu-id="cb3a4-109">Name</span></span>| <span data-ttu-id="cb3a4-110">O nome do pacote para o qual você deseja garantir um estado específico.</span><span class="sxs-lookup"><span data-stu-id="cb3a4-110">The name of the package for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="cb3a4-111">Ensure</span><span class="sxs-lookup"><span data-stu-id="cb3a4-111">Ensure</span></span>| <span data-ttu-id="cb3a4-112">Determina se é necessário verificar se o pacote existe.</span><span class="sxs-lookup"><span data-stu-id="cb3a4-112">Determines whether to check if the package exists.</span></span> <span data-ttu-id="cb3a4-113">Defina essa propriedade como "Present" para garantir que o pacote exista.</span><span class="sxs-lookup"><span data-stu-id="cb3a4-113">Set this property to "Present" to ensure the package exists.</span></span> <span data-ttu-id="cb3a4-114">Defina-a como "Absent" para garantir que o pacote não exista.</span><span class="sxs-lookup"><span data-stu-id="cb3a4-114">Set it to "Absent" to ensure the package does not exist.</span></span> <span data-ttu-id="cb3a4-115">O valor padrão é "Present".</span><span class="sxs-lookup"><span data-stu-id="cb3a4-115">The default value is "Present".</span></span>|
| <span data-ttu-id="cb3a4-116">PackageManager</span><span class="sxs-lookup"><span data-stu-id="cb3a4-116">PackageManager</span></span>| <span data-ttu-id="cb3a4-117">Há suporte para os valores "yum", "apt" e "zypper".</span><span class="sxs-lookup"><span data-stu-id="cb3a4-117">Supported values are "yum", "apt", and "zypper".</span></span> <span data-ttu-id="cb3a4-118">Especifica o gerenciador de pacotes que deve ser usado ao instalar pacotes.</span><span class="sxs-lookup"><span data-stu-id="cb3a4-118">Specifies the package manager to use when installing packages.</span></span> <span data-ttu-id="cb3a4-119">Se **FilePath** for especificado, o caminho fornecido será usado para instalar o pacote.</span><span class="sxs-lookup"><span data-stu-id="cb3a4-119">If **FilePath** is specified, the provided path will be used to install the package.</span></span> <span data-ttu-id="cb3a4-120">Caso contrário, será usado um Gerenciador de Pacotes para instalar o pacote por meio de um repositório pré-configurado.</span><span class="sxs-lookup"><span data-stu-id="cb3a4-120">Otherwise, a Package Manager will be used to install the package from a pre-configured repository.</span></span> <span data-ttu-id="cb3a4-121">Se não for fornecido o **PackageManager** ou o **FilePath**, o gerenciador de pacotes padrão para o sistema será usado.</span><span class="sxs-lookup"><span data-stu-id="cb3a4-121">If neither **PackageManager** nor **FilePath** are provided, the default package manager for the system will be used.</span></span>|
| <span data-ttu-id="cb3a4-122">FilePath</span><span class="sxs-lookup"><span data-stu-id="cb3a4-122">FilePath</span></span>| <span data-ttu-id="cb3a4-123">O caminho do arquivo em que o pacote reside</span><span class="sxs-lookup"><span data-stu-id="cb3a4-123">The file path where the package resides</span></span>|
| <span data-ttu-id="cb3a4-124">PackageGroup</span><span class="sxs-lookup"><span data-stu-id="cb3a4-124">PackageGroup</span></span>| <span data-ttu-id="cb3a4-125">Se for **$true**, o **Nome** deverá ser o nome de um grupo de pacotes para usar com um **PackageManager**.</span><span class="sxs-lookup"><span data-stu-id="cb3a4-125">If **$true**, the **Name** is expected to be the name of a package group for use with a **PackageManager**.</span></span> <span data-ttu-id="cb3a4-126">**PackageGroup** não é válido ao fornecer um **FilePath**.</span><span class="sxs-lookup"><span data-stu-id="cb3a4-126">**PacakgeGroup** is not valid when providing a **FilePath**.</span></span>|
| <span data-ttu-id="cb3a4-127">Argumentos</span><span class="sxs-lookup"><span data-stu-id="cb3a4-127">Arguments</span></span>| <span data-ttu-id="cb3a4-128">Uma cadeia de caracteres de argumentos que será passada para o pacote exatamente conforme fornecido.</span><span class="sxs-lookup"><span data-stu-id="cb3a4-128">A string of arguments that will be passed to the package exactly as provided.</span></span>|
| <span data-ttu-id="cb3a4-129">ReturnCode</span><span class="sxs-lookup"><span data-stu-id="cb3a4-129">ReturnCode</span></span>| <span data-ttu-id="cb3a4-130">O código de retorno esperado.</span><span class="sxs-lookup"><span data-stu-id="cb3a4-130">The expected return code.</span></span> <span data-ttu-id="cb3a4-131">Se o código de retorno real não corresponder ao valor esperado fornecido aqui, a configuração gerará um erro.</span><span class="sxs-lookup"><span data-stu-id="cb3a4-131">If the actual return code does not match the expected value provided here, the configuration will return an error.</span></span>|
| <span data-ttu-id="cb3a4-132">DependsOn</span><span class="sxs-lookup"><span data-stu-id="cb3a4-132">DependsOn</span></span> | <span data-ttu-id="cb3a4-133">Indica que a configuração de outro recurso deve ser executada antes de ele ser configurado.</span><span class="sxs-lookup"><span data-stu-id="cb3a4-133">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="cb3a4-134">Por exemplo, se a **ID** do bloco de script de configuração do recurso que você deseja executar primeiro for **ResourceName** e seu tipo for **ResourceType**, a sintaxe para usar essa propriedade será `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="cb3a4-134">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="cb3a4-135">Exemplo</span><span class="sxs-lookup"><span data-stu-id="cb3a4-135">Example</span></span>

<span data-ttu-id="cb3a4-136">O exemplo a seguir assegura que o pacote denominado "httpd" seja instalado em um computador Linux usando o gerenciador de pacotes “Yum”.</span><span class="sxs-lookup"><span data-stu-id="cb3a4-136">The following example ensures that the package named "httpd" is installed on a Linux computer, using the “Yum” package manager.</span></span>

```
Import-DSCResource -Module nx

Node $node {
nxPackage httpd
{
    Name = "httpd"
    Ensure = "Present"
    PackageManager = "Yum"
}
}
```