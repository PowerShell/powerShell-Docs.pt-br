---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Aninhar configurações
ms.openlocfilehash: 54162cd72d2d1e7773e3be636bfa681329854498
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "71954553"
---
# <a name="nesting-dsc-configurations"></a><span data-ttu-id="08e57-103">Aninhar configurações do DSC</span><span class="sxs-lookup"><span data-stu-id="08e57-103">Nesting DSC configurations</span></span>

<span data-ttu-id="08e57-104">Uma configuração aninhada (também chamada de configuração composta) é uma configuração chamada de dentro de outra configuração, como se fosse um recurso.</span><span class="sxs-lookup"><span data-stu-id="08e57-104">A nested configuration (also called composite configuration) is a configuration that is called within another configuration as if it were a resource.</span></span>
<span data-ttu-id="08e57-105">Ambas as configurações devem ser definidas no mesmo arquivo.</span><span class="sxs-lookup"><span data-stu-id="08e57-105">Both configurations must be defined in the same file.</span></span>

<span data-ttu-id="08e57-106">Vejamos um exemplo simples:</span><span class="sxs-lookup"><span data-stu-id="08e57-106">Let's look at a simple example:</span></span>

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

<span data-ttu-id="08e57-107">Neste exemplo, `FileConfig` usa dois parâmetros obrigatórios: **CopyFrom** e **CopyTo**, que são utilizados como valores para as propriedades **SourcePath** e **DestinationPath** no bloco de recursos `File`.</span><span class="sxs-lookup"><span data-stu-id="08e57-107">In this example, `FileConfig` takes two mandatory parameters,  **CopyFrom** and **CopyTo**, which are used as the values for the **SourcePath** and **DestinationPath** properties in the `File` resource block.</span></span>
<span data-ttu-id="08e57-108">A configuração `NestedConfig` chama `FileConfig` como se fosse um recurso.</span><span class="sxs-lookup"><span data-stu-id="08e57-108">The `NestedConfig` configuration calls `FileConfig` as if it were a resource.</span></span>
<span data-ttu-id="08e57-109">As propriedades do bloco de recursos `NestedConfig` (**CopyFrom** e **CopyTo**) são os parâmetros da configuração `FileConfig`.</span><span class="sxs-lookup"><span data-stu-id="08e57-109">The properties in the `NestedConfig` resource block (**CopyFrom** and **CopyTo**) are the parameters of the `FileConfig` configuration.</span></span>

## <a name="see-also"></a><span data-ttu-id="08e57-110">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="08e57-110">See Also</span></span>

- [<span data-ttu-id="08e57-111">Recursos de composição: usando uma configuração DSC como um recurso</span><span class="sxs-lookup"><span data-stu-id="08e57-111">Composite resources--Using a DSC configuration as a resource</span></span>](../resources/authoringResourceComposite.md)