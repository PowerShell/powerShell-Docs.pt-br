---
external help file: PSModule-help.xml
keywords: powershell, cmdlet
Locale: en-US
Module Name: PowerShellGet
ms.date: 06/09/2017
online version: https://docs.microsoft.com/powershell/module/powershellget/get-psrepository?view=powershell-6&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Get-PSRepository
ms.openlocfilehash: b4d786cdac183917428b0846ad3c88d41b083ac5
ms.sourcegitcommit: 9b28fb9a3d72655bb63f62af18b3a5af6a05cd3f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/07/2020
ms.locfileid: "93194313"
---
# <span data-ttu-id="e8b50-103">Get-PSRepository</span><span class="sxs-lookup"><span data-stu-id="e8b50-103">Get-PSRepository</span></span>

## <span data-ttu-id="e8b50-104">SINOPSE</span><span class="sxs-lookup"><span data-stu-id="e8b50-104">SYNOPSIS</span></span>
<span data-ttu-id="e8b50-105">Obtém repositórios do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e8b50-105">Gets PowerShell repositories.</span></span>

## <span data-ttu-id="e8b50-106">SYNTAX</span><span class="sxs-lookup"><span data-stu-id="e8b50-106">SYNTAX</span></span>

```
Get-PSRepository [[-Name] <String[]>] [<CommonParameters>]
```

## <span data-ttu-id="e8b50-107">DESCRIPTION</span><span class="sxs-lookup"><span data-stu-id="e8b50-107">DESCRIPTION</span></span>

<span data-ttu-id="e8b50-108">O cmdlet **Get-PSRepository** Obtém repositórios de módulo do PowerShell que são registrados para o usuário atual.</span><span class="sxs-lookup"><span data-stu-id="e8b50-108">The **Get-PSRepository** cmdlet gets PowerShell module repositories that are registered for the current user.</span></span>

## <span data-ttu-id="e8b50-109">EXEMPLOS</span><span class="sxs-lookup"><span data-stu-id="e8b50-109">EXAMPLES</span></span>

### <span data-ttu-id="e8b50-110">Exemplo 1: obter todos os repositórios de módulo</span><span class="sxs-lookup"><span data-stu-id="e8b50-110">Example 1: Get all module repositories</span></span>

```
PS C:\> Get-PSRepository
Name                                     SourceLocation                                     OneGetProvider       InstallationPolicy
----                                     --------------                                     --------------       ------------------
PSGallery                                http://go.micro...                                 NuGet                Untrusted
myNuGetSource                            https://myget.c...                                 NuGet                Trusted
```

<span data-ttu-id="e8b50-111">Esse comando obtém todos os repositórios de módulo registrados para o usuário atual.</span><span class="sxs-lookup"><span data-stu-id="e8b50-111">This command gets all module repositories registered for the current user.</span></span>

### <span data-ttu-id="e8b50-112">Exemplo 2: obter repositórios de módulo por nome</span><span class="sxs-lookup"><span data-stu-id="e8b50-112">Example 2: Get module repositories by name</span></span>

```
PS C:\> Get-PSRepository -Name "*NuGet*"
```

<span data-ttu-id="e8b50-113">Esse comando obtém todos os repositórios de módulo que incluem o NuGet em seus nomes.</span><span class="sxs-lookup"><span data-stu-id="e8b50-113">This command gets all module repositories that include NuGet in their names.</span></span>

### <span data-ttu-id="e8b50-114">Exemplo 3: obter um repositório de módulo e formatar a saída</span><span class="sxs-lookup"><span data-stu-id="e8b50-114">Example 3: Get a module repository and format the output</span></span>

```
PS C:\> Get-PSRepository -Name "Local01" | Format-List * -Force
Name                      : local01
SourceLocation            : http://manikb-dev:8765/api/v2/
Trusted                   : True
Registered                : True
InstallationPolicy        : Trusted
PackageManagementProvider : NuGet
PublishLocation           : http://pattif-dev:8765/api/v2/package/
ScriptSourceLocation      : http://pattif-dev:8765/api/v2/artifacts/psscript
ScriptPublishLocation     : http://pattif-dev:8765/api/v2/package/
ProviderOptions           : {}
```

<span data-ttu-id="e8b50-115">Esse comando obtém o repositório chamado Local01 e usa o operador de pipeline para passar esse objeto para o cmdlet Format-List.</span><span class="sxs-lookup"><span data-stu-id="e8b50-115">This command gets the repository named Local01 and uses the pipeline operator to pass that object to the Format-List cmdlet.</span></span>

## <span data-ttu-id="e8b50-116">PARAMETERS</span><span class="sxs-lookup"><span data-stu-id="e8b50-116">PARAMETERS</span></span>

### <span data-ttu-id="e8b50-117">-Name</span><span class="sxs-lookup"><span data-stu-id="e8b50-117">-Name</span></span>

<span data-ttu-id="e8b50-118">Especifica os nomes dos repositórios a serem obtidos.</span><span class="sxs-lookup"><span data-stu-id="e8b50-118">Specifies the names of the repositories to get.</span></span>

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### <span data-ttu-id="e8b50-119">CommonParameters</span><span class="sxs-lookup"><span data-stu-id="e8b50-119">CommonParameters</span></span>

<span data-ttu-id="e8b50-120">Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e8b50-120">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span> <span data-ttu-id="e8b50-121">Para obter mais informações, confira [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="e8b50-121">For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).</span></span>

## <span data-ttu-id="e8b50-122">ENTRADAS</span><span class="sxs-lookup"><span data-stu-id="e8b50-122">INPUTS</span></span>

### <span data-ttu-id="e8b50-123">System.String[]</span><span class="sxs-lookup"><span data-stu-id="e8b50-123">System.String[]</span></span>

## <span data-ttu-id="e8b50-124">SAÍDAS</span><span class="sxs-lookup"><span data-stu-id="e8b50-124">OUTPUTS</span></span>

### <span data-ttu-id="e8b50-125">System.Object</span><span class="sxs-lookup"><span data-stu-id="e8b50-125">System.Object</span></span>

## <span data-ttu-id="e8b50-126">OBSERVAÇÕES</span><span class="sxs-lookup"><span data-stu-id="e8b50-126">NOTES</span></span>

## <span data-ttu-id="e8b50-127">LINKS RELACIONADOS</span><span class="sxs-lookup"><span data-stu-id="e8b50-127">RELATED LINKS</span></span>

[<span data-ttu-id="e8b50-128">Register-PSRepository</span><span class="sxs-lookup"><span data-stu-id="e8b50-128">Register-PSRepository</span></span>](Register-PSRepository.md)

[<span data-ttu-id="e8b50-129">Set-PSRepository</span><span class="sxs-lookup"><span data-stu-id="e8b50-129">Set-PSRepository</span></span>](Set-PSRepository.md)

[<span data-ttu-id="e8b50-130">Unregister-PSRepository</span><span class="sxs-lookup"><span data-stu-id="e8b50-130">Unregister-PSRepository</span></span>](Unregister-PSRepository.md)
