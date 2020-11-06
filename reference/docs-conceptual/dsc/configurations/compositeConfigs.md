---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Aninhar configurações
description: A DSC permite criar configurações compostas aninhando uma configuração dentro de outra.
ms.openlocfilehash: d7a81cb9673126e92e9185aacf19c5c7c17da8ca
ms.sourcegitcommit: 488a940c7c828820b36a6ba56c119f64614afc29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92667412"
---
# <a name="nesting-dsc-configurations"></a><span data-ttu-id="ea2dc-104">Aninhar configurações do DSC</span><span class="sxs-lookup"><span data-stu-id="ea2dc-104">Nesting DSC configurations</span></span>

<span data-ttu-id="ea2dc-105">Uma configuração aninhada (também chamada de configuração composta) é uma configuração chamada de dentro de outra configuração, como se fosse um recurso.</span><span class="sxs-lookup"><span data-stu-id="ea2dc-105">A nested configuration (also called composite configuration) is a configuration that's called within another configuration as if it were a resource.</span></span> <span data-ttu-id="ea2dc-106">Ambas as configurações devem ser definidas no mesmo arquivo.</span><span class="sxs-lookup"><span data-stu-id="ea2dc-106">Both configurations must be defined in the same file.</span></span>

<span data-ttu-id="ea2dc-107">Vejamos um exemplo simples:</span><span class="sxs-lookup"><span data-stu-id="ea2dc-107">Let's look at a simple example:</span></span>

```powershell
Configuration FileConfig
{
    param (
        [Parameter(Mandatory = $true)]
        [String] $CopyFrom,

        [Parameter(Mandatory = $true)]
        [String] $CopyTo
    )

    Import-DscResource -ModuleName PSDesiredStateConfiguration

    File FileTest
    {
        SourcePath = $CopyFrom
        DestinationPath = $CopyTo
        Ensure = 'Present'
    }
}

Configuration NestedFileConfig
{
    Node localhost
    {
        FileConfig NestedConfig
        {
            CopyFrom = 'C:\Test\TestFile.txt'
            CopyTo = 'C:\Test2'
        }
    }
}
```

<span data-ttu-id="ea2dc-108">Neste exemplo, `FileConfig` usa dois parâmetros obrigatórios: **CopyFrom** e **CopyTo** , que são utilizados como valores para as propriedades **SourcePath** e **DestinationPath** no bloco de recursos `File`.</span><span class="sxs-lookup"><span data-stu-id="ea2dc-108">In this example, `FileConfig` takes two mandatory parameters, **CopyFrom** and **CopyTo** , which are used as the values for the **SourcePath** and **DestinationPath** properties in the `File` resource block.</span></span> <span data-ttu-id="ea2dc-109">A configuração `NestedConfig` chama `FileConfig` como se fosse um recurso.</span><span class="sxs-lookup"><span data-stu-id="ea2dc-109">The `NestedConfig` configuration calls `FileConfig` as if it were a resource.</span></span> <span data-ttu-id="ea2dc-110">As propriedades do bloco de recursos `NestedConfig` ( **CopyFrom** e **CopyTo** ) são os parâmetros da configuração `FileConfig`.</span><span class="sxs-lookup"><span data-stu-id="ea2dc-110">The properties in the `NestedConfig` resource block ( **CopyFrom** and **CopyTo** ) are the parameters of the `FileConfig` configuration.</span></span>

<span data-ttu-id="ea2dc-111">Atualmente, a DSC não dá suporte a configurações aninhadas em configurações aninhadas.</span><span class="sxs-lookup"><span data-stu-id="ea2dc-111">DSC doesn't currently support nesting configurations within nested configurations.</span></span> <span data-ttu-id="ea2dc-112">Só é possível aninhar uma configuração com uma camada de profundidade.</span><span class="sxs-lookup"><span data-stu-id="ea2dc-112">You can only nest a configuration one layer deep.</span></span>

## <a name="see-also"></a><span data-ttu-id="ea2dc-113">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="ea2dc-113">See Also</span></span>

- [<span data-ttu-id="ea2dc-114">Recursos de composição: usando uma configuração DSC como um recurso</span><span class="sxs-lookup"><span data-stu-id="ea2dc-114">Composite resources--Using a DSC configuration as a resource</span></span>](../resources/authoringResourceComposite.md)
