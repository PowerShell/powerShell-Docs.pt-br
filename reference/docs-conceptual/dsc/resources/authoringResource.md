---
ms.date: 07/08/2020
keywords: DSC,powershell,configuração,instalação
title: Criar recursos personalizados de configuração de estado desejado do Windows PowerShell
description: Este artigo fornece uma visão geral do desenvolvimento de recursos e links para artigos com exemplos e informações específicas.
ms.openlocfilehash: ff9a0c8ae10583155217fbeccc62e6e1c94f9a11
ms.sourcegitcommit: 488a940c7c828820b36a6ba56c119f64614afc29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92656402"
---
# <a name="build-custom-windows-powershell-desired-state-configuration-resources"></a><span data-ttu-id="9dd24-104">Criar recursos personalizados de configuração de estado desejado do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="9dd24-104">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>

> <span data-ttu-id="9dd24-105">Aplica-se a: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="9dd24-105">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="9dd24-106">A Configuração de Estado Desejado (DSC) do Windows PowerShell tem recursos internos que podem ser usados para configurar seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="9dd24-106">Windows PowerShell Desired State Configuration (DSC) has built-in resources that you can use to configure your environment.</span></span> <span data-ttu-id="9dd24-107">Este artigo fornece uma visão geral do desenvolvimento de recursos e links para artigos com exemplos e informações específicas.</span><span class="sxs-lookup"><span data-stu-id="9dd24-107">This article provides an overview of developing resources and links to articles with specific information and examples.</span></span>

## <a name="dsc-resource-components"></a><span data-ttu-id="9dd24-108">Componentes de recursos de DSC</span><span class="sxs-lookup"><span data-stu-id="9dd24-108">DSC resource components</span></span>

<span data-ttu-id="9dd24-109">Um recurso de DSC é um módulo do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9dd24-109">A DSC resource is a Windows PowerShell module.</span></span> <span data-ttu-id="9dd24-110">O módulo contém o esquema (a definição das propriedades configuráveis) e a implementação (o código que faz o trabalho real especificado por uma configuração) do recurso.</span><span class="sxs-lookup"><span data-stu-id="9dd24-110">The module contains both the schema (the definition of the configurable properties) and the implementation (the code that does the actual work specified by a configuration) for the resource.</span></span> <span data-ttu-id="9dd24-111">Um esquema de recursos de DSC pode ser definido em um arquivo MOF e a implementação é executada por um módulo de script.</span><span class="sxs-lookup"><span data-stu-id="9dd24-111">A DSC resource schema can be defined in a MOF file, and the implementation is performed by a script module.</span></span> <span data-ttu-id="9dd24-112">Começando com o suporte das classes do PowerShell na versão 5, o esquema e a implementação podem ser definidos em uma classe.</span><span class="sxs-lookup"><span data-stu-id="9dd24-112">Beginning with the support of PowerShell classes in version 5, the schema and implementation can both be defined in a class.</span></span> <span data-ttu-id="9dd24-113">Os artigos a seguir descrevem detalhadamente como criar recursos de DSC.</span><span class="sxs-lookup"><span data-stu-id="9dd24-113">The following articles describe in more detail how to create DSC resources.</span></span>

- [<span data-ttu-id="9dd24-114">Escrevendo um recurso personalizado de DSC com MOF</span><span class="sxs-lookup"><span data-stu-id="9dd24-114">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md)
- [<span data-ttu-id="9dd24-115">Implementando um recurso de DSC em C#</span><span class="sxs-lookup"><span data-stu-id="9dd24-115">Implementing a DSC resource in C#</span></span>](authoringResourceMofCS.md)
- [<span data-ttu-id="9dd24-116">Escrevendo um recurso personalizado de DSC com classes do PowerShell</span><span class="sxs-lookup"><span data-stu-id="9dd24-116">Writing a custom DSC resource with PowerShell classes</span></span>](authoringResourceClass.md)
- [<span data-ttu-id="9dd24-117">Recursos de composição: usando uma configuração DSC como um recurso</span><span class="sxs-lookup"><span data-stu-id="9dd24-117">Composite resources: Using a DSC configuration as a resource</span></span>](authoringResourceComposite.md)
- [<span data-ttu-id="9dd24-118">Usando a ferramenta Designer de Recursos</span><span class="sxs-lookup"><span data-stu-id="9dd24-118">Using the Resource Designer tool</span></span>](authoringResourceMofDesigner.md)
