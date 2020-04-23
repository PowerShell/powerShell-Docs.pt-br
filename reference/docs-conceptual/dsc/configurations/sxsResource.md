---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Importar uma versão específica de um recurso instalado
ms.openlocfilehash: 5ed81e11aa67eb6590d958647f48a33b1b5f1c0e
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "71953983"
---
# <a name="import-a-specific-version-of-an-installed-resource"></a><span data-ttu-id="1a3f7-103">Importar uma versão específica de um recurso instalado</span><span class="sxs-lookup"><span data-stu-id="1a3f7-103">Import a specific version of an installed resource</span></span>

> <span data-ttu-id="1a3f7-104">Aplica-se a: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="1a3f7-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="1a3f7-105">No PowerShell 5.0, versões separadas de recursos DSC podem ser instaladas em um computador lado a lado.</span><span class="sxs-lookup"><span data-stu-id="1a3f7-105">In PowerShell 5.0, separate versions of DSC resources can be installed on a computer side by side.</span></span> <span data-ttu-id="1a3f7-106">Um módulo de recursos pode armazenar versões separadas de um recurso em pastas nomeadas por versão.</span><span class="sxs-lookup"><span data-stu-id="1a3f7-106">A resource module can store separate versions of a resource in version named folders.</span></span>

## <a name="installing-separate-resource-versions-side-by-side"></a><span data-ttu-id="1a3f7-107">Instalando versões separadas de recursos lado a lado</span><span class="sxs-lookup"><span data-stu-id="1a3f7-107">Installing separate resource versions side by side</span></span>

<span data-ttu-id="1a3f7-108">Você pode usar os parâmetros **MinimumVersion**, **MaximumVersion** e **RequiredVersion** do cmdlet [Install-Module](/powershell/module/PowershellGet/Install-Module) para especificar qual versão de um módulo instalar.</span><span class="sxs-lookup"><span data-stu-id="1a3f7-108">You can use the **MinimumVersion**, **MaximumVersion**, and **RequiredVersion** parameters of the [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet to specify which version of a module to install.</span></span> <span data-ttu-id="1a3f7-109">Se você chamar **Install-Module** sem especificar uma versão, a versão mais recente será instalada.</span><span class="sxs-lookup"><span data-stu-id="1a3f7-109">Calling **Install-Module** without specifying a version installs the most recent version.</span></span>

<span data-ttu-id="1a3f7-110">Por exemplo, há várias versões do módulo **xFailOverCluster**, cada uma com um recurso **xCluster**.</span><span class="sxs-lookup"><span data-stu-id="1a3f7-110">For example, there are multiple versions of the **xFailOverCluster** module, each of which contains an **xCluster** resource.</span></span> <span data-ttu-id="1a3f7-111">Chamar **Install-Module** sem especificar o número de uma versão instala a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="1a3f7-111">Calling **Install-Module** without specifying the version number installs the most recent version of the module.</span></span>

```powershell
PS> Install-Module xFailOverCluster
PS> Get-DscResource xCluster
```

```output
ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, ...
```

<span data-ttu-id="1a3f7-112">Para instalar a versão específica de um módulo, especifique **RequiredVersion** de 1.1.0.0.</span><span class="sxs-lookup"><span data-stu-id="1a3f7-112">To install a specific version of a module, specify a **RequiredVersion** of 1.1.0.0.</span></span> <span data-ttu-id="1a3f7-113">Isso instala a versão especificada lado a lado com a versão instalada.</span><span class="sxs-lookup"><span data-stu-id="1a3f7-113">This installs the specified version side by side with the installed version.</span></span>

```powershell
PS> Install-Module xFailOverCluster -RequiredVersion 1.1
```

<span data-ttu-id="1a3f7-114">Agora você verá as duas versões do módulo listadas ao usar `Get-DSCResource`.</span><span class="sxs-lookup"><span data-stu-id="1a3f7-114">Now, you see both version of the module listed when you use `Get-DSCResource`.</span></span>

```powershell
PS> Get-DscResource xCluster
```

```output
ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.1        {DomainAdministratorCredential, Name, ...
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, Name, ...
```

## <a name="specifying-a-resource-version-in-a-configuration"></a><span data-ttu-id="1a3f7-115">Especificando uma versão do recurso em uma configuração</span><span class="sxs-lookup"><span data-stu-id="1a3f7-115">Specifying a resource version in a configuration</span></span>

<span data-ttu-id="1a3f7-116">Se você tiver recursos separados instalados em um computador, deve especificar a versão do recurso ao usá-lo em uma configuração.</span><span class="sxs-lookup"><span data-stu-id="1a3f7-116">If you have separate resource versions installed on a computer, you must specify the version of that resource when you use it in a configuration.</span></span> <span data-ttu-id="1a3f7-117">Faça isso especificando o parâmetro **ModuleVersion** da palavra-chave **Import-DscResource**.</span><span class="sxs-lookup"><span data-stu-id="1a3f7-117">You do this by specifying the **ModuleVersion** parameter of the **Import-DscResource** keyword.</span></span> <span data-ttu-id="1a3f7-118">Se você não especificar a versão de um módulo de um recurso do qual tem mais de uma versão instalada, a configuração vai gerar um erro.</span><span class="sxs-lookup"><span data-stu-id="1a3f7-118">If you fail to specify the version of a resource module of a resource of which you have more than one version installed, the configuration generates an error.</span></span>

<span data-ttu-id="1a3f7-119">A configuração a seguir mostra como especificar a versão do recurso a ser chamado:</span><span class="sxs-lookup"><span data-stu-id="1a3f7-119">The following configuration shows how to specify the version of the resource to call:</span></span>

```powershell
configuration VersionTest
{
    Import-DscResource -ModuleName xFailOverCluster -ModuleVersion 1.1

    Node 'localhost'
    {
       xCluster ClusterTest
       {
            Name                          = 'TestCluster'
            StaticIPAddress               = '10.0.0.3'
            DomainAdministratorCredential = Get-Credential
        }
     }
}
```

><span data-ttu-id="1a3f7-120">Observação: o parâmetro ModuleVersion de Import-DscResource não está disponível no PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="1a3f7-120">Note: The ModuleVersion parameter of Import-DscResource is not available in PowerShell 4.0.</span></span> <span data-ttu-id="1a3f7-121">No PowerShell 4.0, é possível especificar uma versão de módulo passando um objeto de especificação de módulo para o parâmetro ModuleName de Import-DscResource.</span><span class="sxs-lookup"><span data-stu-id="1a3f7-121">In PowerShell 4.0, you can specify a module version by passing a module specification object to the ModuleName parameter of Import-DscResource.</span></span> <span data-ttu-id="1a3f7-122">Um objeto de especificação de módulo é uma tabela de hash que contém as chaves ModuleName e RequiredVersion.</span><span class="sxs-lookup"><span data-stu-id="1a3f7-122">A module specification object is a hash table that contains ModuleName and RequiredVersion  keys.</span></span> <span data-ttu-id="1a3f7-123">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1a3f7-123">For example:</span></span>

```powershell
configuration VersionTest
{
    Import-DscResource -ModuleName (@{ModuleName='xFailOverCluster'; RequiredVersion='1.1'} )

    Node 'localhost'
    {
       xCluster ClusterTest
       {
            Name                          = 'TestCluster'
            StaticIPAddress               = '10.0.0.3'
            DomainAdministratorCredential = Get-Credential
        }
     }
}
```

<span data-ttu-id="1a3f7-124">Isso também funcionará no PowerShell 5.0, mas é recomendável que você use o parâmetro **ModuleVersion**.</span><span class="sxs-lookup"><span data-stu-id="1a3f7-124">This will also work in PowerShell 5.0, but it is recommended that you use the **ModuleVersion** parameter.</span></span>

## <a name="see-also"></a><span data-ttu-id="1a3f7-125">Confira também</span><span class="sxs-lookup"><span data-stu-id="1a3f7-125">See also</span></span>

- [<span data-ttu-id="1a3f7-126">Configurações DSC</span><span class="sxs-lookup"><span data-stu-id="1a3f7-126">DSC Configurations</span></span>](configurations.md)
- [<span data-ttu-id="1a3f7-127">Recursos de DSC</span><span class="sxs-lookup"><span data-stu-id="1a3f7-127">DSC Resources</span></span>](../resources/resources.md)
