---
ms.date: 09/20/2019
keywords: DSC,powershell,configuração,instalação
title: Recurso nxFileLine de DSC para Linux
ms.openlocfilehash: 2e94bab318b5db65df88d268a88585079bab89bf
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "71953213"
---
# <a name="dsc-for-linux-nxfileline-resource"></a><span data-ttu-id="253e8-103">Recurso nxFileLine de DSC para Linux</span><span class="sxs-lookup"><span data-stu-id="253e8-103">DSC for Linux nxFileLine Resource</span></span>

<span data-ttu-id="253e8-104">O recurso **nxFileLine** na Configuração de Estado Desejado (DSC) do PowerShell fornece um mecanismo para gerenciar linhas dentro de um arquivo de configuração em um nó do Linux.</span><span class="sxs-lookup"><span data-stu-id="253e8-104">The **nxFileLine** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage lines within a configuration file on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="253e8-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="253e8-105">Syntax</span></span>

```Syntax
nxFileLine <string> #ResourceName
{
    FilePath = <string>
    ContainsLine = <string>
    [ DoesNotContainPattern = <string> ]
    [ DependsOn = <string[]> ]
}
```

## <a name="properties"></a><span data-ttu-id="253e8-106">Propriedades</span><span class="sxs-lookup"><span data-stu-id="253e8-106">Properties</span></span>

|<span data-ttu-id="253e8-107">Propriedade</span><span class="sxs-lookup"><span data-stu-id="253e8-107">Property</span></span> |<span data-ttu-id="253e8-108">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="253e8-108">Description</span></span> |
|---|---|
|<span data-ttu-id="253e8-109">FilePath</span><span class="sxs-lookup"><span data-stu-id="253e8-109">FilePath</span></span> |<span data-ttu-id="253e8-110">O caminho completo até o arquivo para gerenciar linhas no nó de destino.</span><span class="sxs-lookup"><span data-stu-id="253e8-110">The full path to the file to manage lines in on the target node.</span></span> |
|<span data-ttu-id="253e8-111">ContainsLine</span><span class="sxs-lookup"><span data-stu-id="253e8-111">ContainsLine</span></span> |<span data-ttu-id="253e8-112">Uma linha para garantir que exista no arquivo.</span><span class="sxs-lookup"><span data-stu-id="253e8-112">A line to ensure exists in the file.</span></span> <span data-ttu-id="253e8-113">Essa linha será acrescentada ao arquivo caso não exista nele.</span><span class="sxs-lookup"><span data-stu-id="253e8-113">This line will be appended to the file if it does not exist in the file.</span></span> <span data-ttu-id="253e8-114">**ContainsLine** é obrigatório, mas poderá ser definido como uma cadeia de caracteres vazia (`ContainsLine = ""`) se não for necessário.</span><span class="sxs-lookup"><span data-stu-id="253e8-114">**ContainsLine** is mandatory, but can be set to an empty string (`ContainsLine = ""`) if it is not needed.</span></span> |
|<span data-ttu-id="253e8-115">DoesNotContainPattern</span><span class="sxs-lookup"><span data-stu-id="253e8-115">DoesNotContainPattern</span></span> |<span data-ttu-id="253e8-116">Um padrão de expressão regular para linhas que não devem existir no arquivo.</span><span class="sxs-lookup"><span data-stu-id="253e8-116">A regular expression pattern for lines that should not exist in the file.</span></span> <span data-ttu-id="253e8-117">Para todas as linhas existentes no arquivo que correspondem a essa expressão regular, a linha será removida do arquivo.</span><span class="sxs-lookup"><span data-stu-id="253e8-117">For any lines that exist in the file that match this regular expression, the line will be removed from the file.</span></span> |

## <a name="common-properties"></a><span data-ttu-id="253e8-118">Propriedades comuns</span><span class="sxs-lookup"><span data-stu-id="253e8-118">Common properties</span></span>

|<span data-ttu-id="253e8-119">Propriedade</span><span class="sxs-lookup"><span data-stu-id="253e8-119">Property</span></span> |<span data-ttu-id="253e8-120">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="253e8-120">Description</span></span> |
|---|---|
|<span data-ttu-id="253e8-121">DependsOn</span><span class="sxs-lookup"><span data-stu-id="253e8-121">DependsOn</span></span> |<span data-ttu-id="253e8-122">Indica que a configuração de outro recurso deve ser executada antes de ele ser configurado.</span><span class="sxs-lookup"><span data-stu-id="253e8-122">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="253e8-123">Por exemplo, se a ID do bloco de script de configuração do recurso que você deseja executar primeiro for ResourceName e seu tipo for ResourceType, a sintaxe para usar essa propriedade será `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="253e8-123">For example, if the ID of the resource configuration script block that you want to run first is ResourceName and its type is ResourceType, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span> |

## <a name="example"></a><span data-ttu-id="253e8-124">Exemplo</span><span class="sxs-lookup"><span data-stu-id="253e8-124">Example</span></span>

<span data-ttu-id="253e8-125">Este exemplo demonstra como usar o recurso **nxFileLine** para configurar o arquivo `/etc/sudoers`, garantindo que o usuário: monuser esteja configurado como não requiretty.</span><span class="sxs-lookup"><span data-stu-id="253e8-125">This example demonstrates using the **nxFileLine** resource to configure the `/etc/sudoers` file, ensuring that the user: monuser is configured to not requiretty.</span></span>

```powershell
Import-DscResource -Module nx

nxFileLine DoNotRequireTTY
{
   FilePath = "/etc/sudoers"
   ContainsLine = 'Defaults:monuser !requiretty'
   DoesNotContainPattern = "Defaults:monuser[ ]+requiretty"
}
```