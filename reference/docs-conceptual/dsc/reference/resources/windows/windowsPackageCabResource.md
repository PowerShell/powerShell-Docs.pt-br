---
ms.date: 09/20/2019
keywords: DSC,powershell,configuração,instalação
title: Recurso de DSC WindowsPackageCab
ms.openlocfilehash: ec465b2c3b1d180ba46ee24a61f2be1129148962
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71954633"
---
# <a name="dsc-windowspackagecab-resource"></a><span data-ttu-id="e5fc2-103">Recurso de DSC WindowsPackageCab</span><span class="sxs-lookup"><span data-stu-id="e5fc2-103">DSC WindowsPackageCab Resource</span></span>

> <span data-ttu-id="e5fc2-104">Aplica-se a: Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="e5fc2-104">Applies To: Windows PowerShell 5.1</span></span>

<span data-ttu-id="e5fc2-105">O **WindowsPackageCab** no DSC (Desired State Configuration) do Windows PowerShell fornece um mecanismo para instalar ou desinstalar pacotes de gabinete (.cab) do Windows em um nó de destino.</span><span class="sxs-lookup"><span data-stu-id="e5fc2-105">The **WindowsPackageCab** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to install or uninstall Windows cabinet (.cab) packages on a target node.</span></span>

<span data-ttu-id="e5fc2-106">O nó de destino deve ter o módulo PowerShell do DISM instalado.</span><span class="sxs-lookup"><span data-stu-id="e5fc2-106">The target node must have the DISM PowerShell module installed.</span></span> <span data-ttu-id="e5fc2-107">Para obter informações, consulte [Usar DISM no Windows PowerShell](/windows-hardware/manufacture/desktop/use-dism-in-windows-powershell-s14).</span><span class="sxs-lookup"><span data-stu-id="e5fc2-107">For information, see [Use DISM in Windows PowerShell](/windows-hardware/manufacture/desktop/use-dism-in-windows-powershell-s14).</span></span>

## <a name="syntax"></a><span data-ttu-id="e5fc2-108">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="e5fc2-108">Syntax</span></span>

```Syntax
{
    Name = [string]
    SourcePath = [string]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    Ensure = [string] { Absent | Present }
    [ PsDscRunAsCredential = [PSCredential] ]
}
```

## <a name="properties"></a><span data-ttu-id="e5fc2-109">Propriedades</span><span class="sxs-lookup"><span data-stu-id="e5fc2-109">Properties</span></span>

|<span data-ttu-id="e5fc2-110">Propriedade</span><span class="sxs-lookup"><span data-stu-id="e5fc2-110">Property</span></span> |<span data-ttu-id="e5fc2-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="e5fc2-111">Description</span></span> |
|---|---|
|<span data-ttu-id="e5fc2-112">Nome</span><span class="sxs-lookup"><span data-stu-id="e5fc2-112">Name</span></span> |<span data-ttu-id="e5fc2-113">Indica o nome do pacote para o qual você deseja garantir um estado específico.</span><span class="sxs-lookup"><span data-stu-id="e5fc2-113">Indicates the name of the package for you want to ensure a specific state.</span></span> |
|<span data-ttu-id="e5fc2-114">SourcePath</span><span class="sxs-lookup"><span data-stu-id="e5fc2-114">SourcePath</span></span> |<span data-ttu-id="e5fc2-115">Indica o caminho em que o pacote reside.</span><span class="sxs-lookup"><span data-stu-id="e5fc2-115">Indicates the path where the package resides.</span></span> |
|<span data-ttu-id="e5fc2-116">LogPath</span><span class="sxs-lookup"><span data-stu-id="e5fc2-116">LogPath</span></span> |<span data-ttu-id="e5fc2-117">Indica o caminho completo em que você deseja que o provedor salve um arquivo de log para instalar ou desinstalar o pacote.</span><span class="sxs-lookup"><span data-stu-id="e5fc2-117">Indicates the full path where you want the provider to save a log file to install or uninstall the package.</span></span> |

## <a name="common-properties"></a><span data-ttu-id="e5fc2-118">Propriedades comuns</span><span class="sxs-lookup"><span data-stu-id="e5fc2-118">Common properties</span></span>

|<span data-ttu-id="e5fc2-119">Propriedade</span><span class="sxs-lookup"><span data-stu-id="e5fc2-119">Property</span></span> |<span data-ttu-id="e5fc2-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="e5fc2-120">Description</span></span> |
|---|---|
|<span data-ttu-id="e5fc2-121">DependsOn</span><span class="sxs-lookup"><span data-stu-id="e5fc2-121">DependsOn</span></span> |<span data-ttu-id="e5fc2-122">Indica que a configuração de outro recurso deve ser executada antes de ele ser configurado.</span><span class="sxs-lookup"><span data-stu-id="e5fc2-122">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="e5fc2-123">Por exemplo, se a ID do bloco de script de configuração do recurso que você deseja executar primeiro for ResourceName e seu tipo for ResourceType, a sintaxe para usar essa propriedade será `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="e5fc2-123">For example, if the ID of the resource configuration script block that you want to run first is ResourceName and its type is ResourceType, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span> |
|<span data-ttu-id="e5fc2-124">Ensure</span><span class="sxs-lookup"><span data-stu-id="e5fc2-124">Ensure</span></span> |<span data-ttu-id="e5fc2-125">Indica se o pacote foi instalado.</span><span class="sxs-lookup"><span data-stu-id="e5fc2-125">Indicates if the package is installed.</span></span> <span data-ttu-id="e5fc2-126">Defina esta propriedade como **Absent** para garantir que o pacote não seja instalado (ou desinstalar o pacote, se ele estiver instalado).</span><span class="sxs-lookup"><span data-stu-id="e5fc2-126">Set this property to **Absent** to ensure the package is not installed (or uninstall the package if it is installed).</span></span> <span data-ttu-id="e5fc2-127">Defina-a como **Present** para garantir que o pacote seja instalado.</span><span class="sxs-lookup"><span data-stu-id="e5fc2-127">Set it to **Present** to ensure the package is installed.</span></span> <span data-ttu-id="e5fc2-128">**Ensure** é uma propriedade obrigatória no recurso **WindowsPackageCab**.</span><span class="sxs-lookup"><span data-stu-id="e5fc2-128">**Ensure** is a required property on the **WindowsPackageCab** resource.</span></span> |
|<span data-ttu-id="e5fc2-129">PsDscRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="e5fc2-129">PsDscRunAsCredential</span></span> |<span data-ttu-id="e5fc2-130">Define a credencial para executar todo o recurso.</span><span class="sxs-lookup"><span data-stu-id="e5fc2-130">Sets the credential for running the entire resource as.</span></span> |

## <a name="example"></a><span data-ttu-id="e5fc2-131">Exemplo</span><span class="sxs-lookup"><span data-stu-id="e5fc2-131">Example</span></span>

<span data-ttu-id="e5fc2-132">A configuração de exemplo a seguir usa parâmetros de entrada e garante que o arquivo .cab especificado pelo parâmetro `$Name` esteja instalado.</span><span class="sxs-lookup"><span data-stu-id="e5fc2-132">The following example configuration takes input parameters, and ensures that the .cab file specified by the `$Name` parameter is installed.</span></span>

```powershell
Configuration Sample_WindowsPackageCab
{
    param
    (
        [Parameter (Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $Name,

        [Parameter (Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $SourcePath,

        [Parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $LogPath
    )

    Import-DscResource -ModuleName 'PSDscResources'

    WindowsPackageCab WindowsPackageCab1
    {
        Name = $Name
        Ensure = 'Present'
        SourcePath = $SourcePath
        LogPath = $LogPath
    }
}
```