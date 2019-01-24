---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Recurso do WindowsFeatureSet DSC
ms.openlocfilehash: 8b7c7e72dd58459bd19cb723e5790a82841515c0
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046996"
---
# <a name="dsc-windowsfeatureset-resource"></a><span data-ttu-id="0f119-103">Recurso do WindowsFeatureSet DSC</span><span class="sxs-lookup"><span data-stu-id="0f119-103">DSC WindowsFeatureSet Resource</span></span>

> <span data-ttu-id="0f119-104">Aplica-se a: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="0f119-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="0f119-105">O recurso **WindowsFeatureSet** na Configuração de Estado Desejado (DSC) do Windows PowerShell fornece um mecanismo para garantir que funções e recursos sejam adicionados ou removidos em um nó de destino.</span><span class="sxs-lookup"><span data-stu-id="0f119-105">The **WindowsFeatureSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that roles and features are added or removed on a target node.</span></span>
<span data-ttu-id="0f119-106">Esse recurso é um [recurso composto](../../../resources/authoringResourceComposite.md) que chama o [recurso WindowsFeature](windowsfeatureResource.md) para cada recurso especificado na propriedade `Name`.</span><span class="sxs-lookup"><span data-stu-id="0f119-106">This resource is a [composite resource](../../../resources/authoringResourceComposite.md) that calls the [WindowsFeature resource](windowsfeatureResource.md) for each feature specified in the `Name` property.</span></span>

<span data-ttu-id="0f119-107">Use esse recurso quando desejar configurar vários Recursos do Windows para o mesmo estado.</span><span class="sxs-lookup"><span data-stu-id="0f119-107">Use this resource when you want to configure a number of Windows Features to the same state.</span></span>

## <a name="syntax"></a><span data-ttu-id="0f119-108">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="0f119-108">Syntax</span></span>

```
WindowsFeatureSet [string] #ResourceName
{
    Name = [string[]]
    [ Ensure = [string] { Absent | Present }  ]
    [ Source = [string] ]
    [ IncludeAllSubFeature = [bool] ]
    [ Credential = [PSCredential] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a><span data-ttu-id="0f119-109">Propriedades</span><span class="sxs-lookup"><span data-stu-id="0f119-109">Properties</span></span>

|  <span data-ttu-id="0f119-110">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0f119-110">Property</span></span>  |  <span data-ttu-id="0f119-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="0f119-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="0f119-112">Nome</span><span class="sxs-lookup"><span data-stu-id="0f119-112">Name</span></span>| <span data-ttu-id="0f119-113">Os nomes de funções ou recursos que você deseja garantir são adicionados ou removidos.</span><span class="sxs-lookup"><span data-stu-id="0f119-113">The names of the roles or features that you want to ensure are added or removed.</span></span> <span data-ttu-id="0f119-114">É igual à propriedade **Name** do cmdlet [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx), e não o nome de exibição das funções ou recursos.</span><span class="sxs-lookup"><span data-stu-id="0f119-114">This is the same as the **Name** property of the [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) cmdlet, and not the display name of the roles or features.</span></span>|
| <span data-ttu-id="0f119-115">Credential</span><span class="sxs-lookup"><span data-stu-id="0f119-115">Credential</span></span>| <span data-ttu-id="0f119-116">As credenciais que devem ser usadas para adicionar ou remover as funções ou os recursos.</span><span class="sxs-lookup"><span data-stu-id="0f119-116">The credentials to use to add or remove the roles or features.</span></span>|
| <span data-ttu-id="0f119-117">Ensure</span><span class="sxs-lookup"><span data-stu-id="0f119-117">Ensure</span></span>| <span data-ttu-id="0f119-118">Indica se as funções ou os recursos são adicionados.</span><span class="sxs-lookup"><span data-stu-id="0f119-118">Indicates whether the roles or features are added.</span></span> <span data-ttu-id="0f119-119">Para garantir que as funções ou os recursos sejam adicionados, defina essa propriedade como "Presente"; para garantir que as funções ou os recursos sejam removido, defina a propriedade como "Ausente".</span><span class="sxs-lookup"><span data-stu-id="0f119-119">To ensure that the roles or features are added, set this property to "Present" To ensure that the roles or features are removed, set the property to "Absent".</span></span>|
| <span data-ttu-id="0f119-120">IncludeAllSubFeature</span><span class="sxs-lookup"><span data-stu-id="0f119-120">IncludeAllSubFeature</span></span>| <span data-ttu-id="0f119-121">Defina essa propriedade como **$true** para incluir todos os sub-recursos com os recursos especificados com a propriedade **Nome**.</span><span class="sxs-lookup"><span data-stu-id="0f119-121">Set this property to **$true** to include all required subfeatures with of the features you specify with the **Name** property.</span></span>|
| <span data-ttu-id="0f119-122">LogPath</span><span class="sxs-lookup"><span data-stu-id="0f119-122">LogPath</span></span>| <span data-ttu-id="0f119-123">O caminho até um arquivo de log em que você deseja que o provedor de recursos registre a operação.</span><span class="sxs-lookup"><span data-stu-id="0f119-123">The path to a log file where you want the resource provider to log the operation.</span></span>|
| <span data-ttu-id="0f119-124">DependsOn</span><span class="sxs-lookup"><span data-stu-id="0f119-124">DependsOn</span></span>| <span data-ttu-id="0f119-125">Indica que a configuração de outro recurso deve ser executada antes de ele ser configurado.</span><span class="sxs-lookup"><span data-stu-id="0f119-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="0f119-126">Por exemplo, se a ID do bloco de script de configuração do recurso que você deseja executar primeiro for __ResourceName__ e seu tipo for __ResourceType__, a sintaxe para usar essa propriedade será `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="0f119-126">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="0f119-127">Origem</span><span class="sxs-lookup"><span data-stu-id="0f119-127">Source</span></span>| <span data-ttu-id="0f119-128">Indica o local do arquivo de origem que deve ser usado para a instalação, se necessário.</span><span class="sxs-lookup"><span data-stu-id="0f119-128">Indicates the location of the source file to use for installation, if necessary.</span></span>|

## <a name="example"></a><span data-ttu-id="0f119-129">Exemplo</span><span class="sxs-lookup"><span data-stu-id="0f119-129">Example</span></span>

<span data-ttu-id="0f119-130">A configuração a seguir garante que os recursos **Servidor Web** (IIS) e **Servidor SMTP** e todos os sub-recursos de cada um sejam instalados.</span><span class="sxs-lookup"><span data-stu-id="0f119-130">The following configuration ensures that the **Web-Server** (IIS) and **SMTP Server** features, and all subfeatures of each, are installed.</span></span>

```powershell
configuration FeatureSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        WindowsFeatureSet WindowsFeatureSetExample
        {
            Name                    = @("SMTP-Server", "Web-Server")
            Ensure                  = 'Present'
            IncludeAllSubFeature    = $true
        }
    }
}
```