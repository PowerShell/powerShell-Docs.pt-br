---
ms.date: 09/20/2019
keywords: DSC,powershell,configuração,instalação
title: Recurso do ServiceSet DSC
ms.openlocfilehash: 97c25f46940d69ed6c696e2692e29131e9a997b0
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71953023"
---
# <a name="dsc-serviceset-resource"></a><span data-ttu-id="57efa-103">Recurso do ServiceSet DSC</span><span class="sxs-lookup"><span data-stu-id="57efa-103">DSC ServiceSet Resource</span></span>

> <span data-ttu-id="57efa-104">Aplica-se a: Windows PowerShell 4.0, Windows PowerShell 5.x</span><span class="sxs-lookup"><span data-stu-id="57efa-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.x</span></span>

<span data-ttu-id="57efa-105">O recurso **ServiceSet** na DSC (Configuração de Estado Desejado) do Windows PowerShell oferece um mecanismo para gerenciar serviços no nó de destino.</span><span class="sxs-lookup"><span data-stu-id="57efa-105">The **ServiceSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage services on the target node.</span></span> <span data-ttu-id="57efa-106">Esse recurso é um [recurso composto](../../../resources/authoringResourceComposite.md) que chama o [Recurso de serviço](serviceResource.md) para cada serviço especificado na propriedade **Name**.</span><span class="sxs-lookup"><span data-stu-id="57efa-106">This resource is a [composite resource](../../../resources/authoringResourceComposite.md) that calls the [Service resource](serviceResource.md) for each service specified in the **Name** property.</span></span>

<span data-ttu-id="57efa-107">Use esse recurso quando desejar configurar vários serviços para o mesmo estado.</span><span class="sxs-lookup"><span data-stu-id="57efa-107">Use this resource when you want to configure a number of services to the same state.</span></span>

## <a name="syntax"></a><span data-ttu-id="57efa-108">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="57efa-108">Syntax</span></span>

```Syntax
ServiceSet [string] #ResourceName
{
    Name = [string[]]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ PsDscRunAsCredential = [PSCredential] ]
}
```

## <a name="properties"></a><span data-ttu-id="57efa-109">Propriedades</span><span class="sxs-lookup"><span data-stu-id="57efa-109">Properties</span></span>

|<span data-ttu-id="57efa-110">Propriedade</span><span class="sxs-lookup"><span data-stu-id="57efa-110">Property</span></span> |<span data-ttu-id="57efa-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="57efa-111">Description</span></span> |
|---|---|
|<span data-ttu-id="57efa-112">Nome</span><span class="sxs-lookup"><span data-stu-id="57efa-112">Name</span></span> |<span data-ttu-id="57efa-113">Indica os nomes do serviço.</span><span class="sxs-lookup"><span data-stu-id="57efa-113">Indicates the service names.</span></span> <span data-ttu-id="57efa-114">Observe que, às vezes, isso é diferente dos nomes de exibição.</span><span class="sxs-lookup"><span data-stu-id="57efa-114">Note that sometimes this is different from the display names.</span></span> <span data-ttu-id="57efa-115">É possível obter uma lista dos serviços e seus estados atuais com o cmdlet `Get-Service`.</span><span class="sxs-lookup"><span data-stu-id="57efa-115">You can get a list of the services and their current state with the `Get-Service` cmdlet.</span></span> |
|<span data-ttu-id="57efa-116">StartupType</span><span class="sxs-lookup"><span data-stu-id="57efa-116">StartupType</span></span> |<span data-ttu-id="57efa-117">Indica o tipo de inicialização para os serviços.</span><span class="sxs-lookup"><span data-stu-id="57efa-117">Indicates the startup type for the services.</span></span> <span data-ttu-id="57efa-118">Os valores permitidos para essa propriedade são: **Automático**, **Desabilitado** e **Manual**.</span><span class="sxs-lookup"><span data-stu-id="57efa-118">The values that are allowed for this property are: **Automatic**, **Disabled**, and **Manual**.</span></span> |
|<span data-ttu-id="57efa-119">BuiltInAccount</span><span class="sxs-lookup"><span data-stu-id="57efa-119">BuiltInAccount</span></span> |<span data-ttu-id="57efa-120">Indica a conta de credenciais a ser usada para os serviços.</span><span class="sxs-lookup"><span data-stu-id="57efa-120">Indicates the sign-in account to use for the services.</span></span> <span data-ttu-id="57efa-121">Os valores permitidos para essa propriedade são: **LocalService**, **LocalSystem** e **NetworkService**.</span><span class="sxs-lookup"><span data-stu-id="57efa-121">The values that are allowed for this property are: **LocalService**, **LocalSystem**, and **NetworkService**.</span></span> |
|<span data-ttu-id="57efa-122">Estado</span><span class="sxs-lookup"><span data-stu-id="57efa-122">State</span></span> |<span data-ttu-id="57efa-123">Indica o estado que você deseja garantir para os serviços: **Parado** ou **Em execução**.</span><span class="sxs-lookup"><span data-stu-id="57efa-123">Indicates the state you want to ensure for the services: **Stopped** or **Running**.</span></span> |
|<span data-ttu-id="57efa-124">Credential</span><span class="sxs-lookup"><span data-stu-id="57efa-124">Credential</span></span> |<span data-ttu-id="57efa-125">Indica as credenciais para a conta sob a qual o serviço será executado.</span><span class="sxs-lookup"><span data-stu-id="57efa-125">Indicates credentials for the account that the service resource will run under.</span></span> <span data-ttu-id="57efa-126">Essa propriedade e a propriedade **BuiltinAccount** não podem ser usadas juntas.</span><span class="sxs-lookup"><span data-stu-id="57efa-126">This property and the **BuiltinAccount** property cannot be used together.</span></span> |

## <a name="common-properties"></a><span data-ttu-id="57efa-127">Propriedades comuns</span><span class="sxs-lookup"><span data-stu-id="57efa-127">Common properties</span></span>

|<span data-ttu-id="57efa-128">Propriedade</span><span class="sxs-lookup"><span data-stu-id="57efa-128">Property</span></span> |<span data-ttu-id="57efa-129">Descrição</span><span class="sxs-lookup"><span data-stu-id="57efa-129">Description</span></span> |
|---|---|
|<span data-ttu-id="57efa-130">DependsOn</span><span class="sxs-lookup"><span data-stu-id="57efa-130">DependsOn</span></span> |<span data-ttu-id="57efa-131">Indica que a configuração de outro recurso deve ser executada antes de ele ser configurado.</span><span class="sxs-lookup"><span data-stu-id="57efa-131">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="57efa-132">Por exemplo, se a ID do bloco de script de configuração do recurso que você deseja executar primeiro for ResourceName e seu tipo for ResourceType, a sintaxe para usar essa propriedade será `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="57efa-132">For example, if the ID of the resource configuration script block that you want to run first is ResourceName and its type is ResourceType, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span> |
|<span data-ttu-id="57efa-133">Ensure</span><span class="sxs-lookup"><span data-stu-id="57efa-133">Ensure</span></span> |<span data-ttu-id="57efa-134">Indica se os serviços existem no sistema.</span><span class="sxs-lookup"><span data-stu-id="57efa-134">Indicates whether the services exist on the system.</span></span> <span data-ttu-id="57efa-135">Defina essa propriedade como **Ausente** para garantir que os serviços não existam.</span><span class="sxs-lookup"><span data-stu-id="57efa-135">Set this property to **Absent** to ensure that the services do not exist.</span></span> <span data-ttu-id="57efa-136">Defini-la como **Present** garantirá que os serviços de destino existam.</span><span class="sxs-lookup"><span data-stu-id="57efa-136">Setting it to **Present** ensures that target services exist.</span></span> <span data-ttu-id="57efa-137">O valor padrão é **Present**.</span><span class="sxs-lookup"><span data-stu-id="57efa-137">The default value is **Present**.</span></span> |
|<span data-ttu-id="57efa-138">PsDscRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="57efa-138">PsDscRunAsCredential</span></span> |<span data-ttu-id="57efa-139">Define a credencial para executar todo o recurso.</span><span class="sxs-lookup"><span data-stu-id="57efa-139">Sets the credential for running the entire resource as.</span></span> |

> [!NOTE]
> <span data-ttu-id="57efa-140">A propriedade comum **PsDscRunAsCredential** foi adicionada ao WMF 5.0 para permitir a execução de qualquer recurso de DSC no contexto de outras credenciais.</span><span class="sxs-lookup"><span data-stu-id="57efa-140">The **PsDscRunAsCredential** common property was added in WMF 5.0 to allow running any DSC resource in the context of other credentials.</span></span> <span data-ttu-id="57efa-141">Para saber mais, confira [Usar credenciais com recursos de DSC](../../../configurations/runasuser.md).</span><span class="sxs-lookup"><span data-stu-id="57efa-141">For more information, see [Use Credentials with DSC Resources](../../../configurations/runasuser.md).</span></span>

## <a name="example"></a><span data-ttu-id="57efa-142">Exemplo</span><span class="sxs-lookup"><span data-stu-id="57efa-142">Example</span></span>

<span data-ttu-id="57efa-143">A configuração a seguir inicia os serviços "Áudio do Windows" e "Serviços de Área de Trabalho Remota".</span><span class="sxs-lookup"><span data-stu-id="57efa-143">The following configuration starts the "Windows Audio" and "Remote Desktop Services" services.</span></span>

```powershell
configuration ServiceSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {
        ServiceSet ServiceSetExample
        {
            Name        = @("TermService", "Audiosrv")
            StartupType = "Manual"
            State       = "Running"
        }
    }
}
```