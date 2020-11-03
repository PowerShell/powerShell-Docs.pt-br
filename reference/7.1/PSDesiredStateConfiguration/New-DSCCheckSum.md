---
external help file: PSDesiredStateConfiguration-help.xml
keywords: powershell, cmdlet
Locale: en-US
Module Name: PSDesiredStateConfiguration
ms.date: 06/09/2017
online version: https://docs.microsoft.com/powershell/module/psdesiredstateconfiguration/new-dscchecksum?view=powershell-7.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: New-DscChecksum
ms.openlocfilehash: 6085585a50f8d3ac8adb34d4d9e3e376a1bc17cd
ms.sourcegitcommit: 9b28fb9a3d72655bb63f62af18b3a5af6a05cd3f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/07/2020
ms.locfileid: "93194669"
---
# <span data-ttu-id="dcb37-103">New-DscChecksum</span><span class="sxs-lookup"><span data-stu-id="dcb37-103">New-DscChecksum</span></span>

## <span data-ttu-id="dcb37-104">SINOPSE</span><span class="sxs-lookup"><span data-stu-id="dcb37-104">SYNOPSIS</span></span>
<span data-ttu-id="dcb37-105">Cria arquivos de soma de verificação para documentos DSC e recursos DSC.</span><span class="sxs-lookup"><span data-stu-id="dcb37-105">Creates checksum files for DSC documents and DSC resources.</span></span>

## <span data-ttu-id="dcb37-106">SYNTAX</span><span class="sxs-lookup"><span data-stu-id="dcb37-106">SYNTAX</span></span>

```
New-DscChecksum [-Path] <String[]> [[-OutPath] <String>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## <span data-ttu-id="dcb37-107">DESCRIPTION</span><span class="sxs-lookup"><span data-stu-id="dcb37-107">DESCRIPTION</span></span>

<span data-ttu-id="dcb37-108">O cmdlet **New-DSCCheckSum** gera arquivos de soma de verificação para documentos de DSC (configuração de estado desejado) do PowerShell e recursos de DSC compactados.</span><span class="sxs-lookup"><span data-stu-id="dcb37-108">The **New-DSCCheckSum** cmdlet generates checksum files for PowerShell Desired State Configuration (DSC) documents and compressed DSC resources.</span></span>
<span data-ttu-id="dcb37-109">Esse cmdlet gera um arquivo de soma de verificação para cada configuração e recurso a ser usado no modo de pull.</span><span class="sxs-lookup"><span data-stu-id="dcb37-109">This cmdlet generates a checksum file for each configuration and resource to be used in pull mode.</span></span>
<span data-ttu-id="dcb37-110">O serviço DSC usa as somas de verificação para verificar se a configuração e os recursos corretos existem no nó de destino.</span><span class="sxs-lookup"><span data-stu-id="dcb37-110">The DSC service uses the checksums to make sure that the correct configuration and resources exist on the target node.</span></span>
<span data-ttu-id="dcb37-111">Coloque as somas de verificação junto com os documentos DSC associados e os recursos de DSC compactados no armazenamento do serviço DSC.</span><span class="sxs-lookup"><span data-stu-id="dcb37-111">Place the checksums together with the associated DSC documents and compressed DSC resources in the DSC service store.</span></span>

## <span data-ttu-id="dcb37-112">EXEMPLOS</span><span class="sxs-lookup"><span data-stu-id="dcb37-112">EXAMPLES</span></span>

### <span data-ttu-id="dcb37-113">Exemplo 1: criar arquivos de soma de verificação para todas as configurações em um caminho específico</span><span class="sxs-lookup"><span data-stu-id="dcb37-113">Example 1: Create checksum files for all configurations in a specific path</span></span>

```
PS C:\> New-DscCheckSum -Path "C:\DSC\Configurations\"
```

<span data-ttu-id="dcb37-114">Este comando cria arquivos de soma de verificação para todas as configurações no caminho C:\DSC\Configurations.</span><span class="sxs-lookup"><span data-stu-id="dcb37-114">This command creates checksum files for all configurations in the path C:\DSC\Configurations.</span></span>
<span data-ttu-id="dcb37-115">Todos os arquivos de soma de verificação que já existem são ignorados.</span><span class="sxs-lookup"><span data-stu-id="dcb37-115">Any checksum files that already exist are skipped.</span></span>

### <span data-ttu-id="dcb37-116">Exemplo 2: criar arquivos de soma de verificação para todas as configurações em um caminho específico e substituir os arquivos de soma de verificação existentes</span><span class="sxs-lookup"><span data-stu-id="dcb37-116">Example 2: Create checksum files for all configurations in a specific path and overwrite the existing checksum files</span></span>

```
PS C:\> New-DscCheckSum -Path "C:\DSC\Configurations\" -Force
```

<span data-ttu-id="dcb37-117">Este comando cria novos arquivos de soma de verificação para todas as configurações no caminho C:\DSC\Configurations.</span><span class="sxs-lookup"><span data-stu-id="dcb37-117">This command creates new checksum files for all configurations in the path C:\DSC\Configurations.</span></span>
<span data-ttu-id="dcb37-118">A especificação do parâmetro *Force* faz com que o comando Substitua todos os arquivos de soma de verificação que já existem.</span><span class="sxs-lookup"><span data-stu-id="dcb37-118">Specifying the *Force* parameter causes the command to overwrite any checksum files that already exist.</span></span>

## <span data-ttu-id="dcb37-119">PARAMETERS</span><span class="sxs-lookup"><span data-stu-id="dcb37-119">PARAMETERS</span></span>

### <span data-ttu-id="dcb37-120">-Confirm</span><span class="sxs-lookup"><span data-stu-id="dcb37-120">-Confirm</span></span>

<span data-ttu-id="dcb37-121">Solicita sua confirmação antes de executar o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dcb37-121">Prompts you for confirmation before running the cmdlet.</span></span>

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="dcb37-122">-Force</span><span class="sxs-lookup"><span data-stu-id="dcb37-122">-Force</span></span>

<span data-ttu-id="dcb37-123">Indica que o cmdlet substitui o arquivo de saída especificado se ele já existir.</span><span class="sxs-lookup"><span data-stu-id="dcb37-123">Indicates that the cmdlet overwrites the specified output file if it already exists.</span></span>

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="dcb37-124">-OutPath</span><span class="sxs-lookup"><span data-stu-id="dcb37-124">-OutPath</span></span>

<span data-ttu-id="dcb37-125">Especifica o caminho e o nome do arquivo de soma de verificação de saída.</span><span class="sxs-lookup"><span data-stu-id="dcb37-125">Specifies the path and file name of the output checksum file.</span></span>

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="dcb37-126">-Path</span><span class="sxs-lookup"><span data-stu-id="dcb37-126">-Path</span></span>

<span data-ttu-id="dcb37-127">Especifica o caminho do arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="dcb37-127">Specifies the path of the input file.</span></span>

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases: ConfigurationPath

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="dcb37-128">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="dcb37-128">-WhatIf</span></span>

<span data-ttu-id="dcb37-129">Mostra o que aconteceria se o cmdlet fosse executado.</span><span class="sxs-lookup"><span data-stu-id="dcb37-129">Shows what would happen if the cmdlet runs.</span></span>
<span data-ttu-id="dcb37-130">O cmdlet não é executado.</span><span class="sxs-lookup"><span data-stu-id="dcb37-130">The cmdlet is not run.</span></span>

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: wi

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="dcb37-131">CommonParameters</span><span class="sxs-lookup"><span data-stu-id="dcb37-131">CommonParameters</span></span>

<span data-ttu-id="dcb37-132">Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="dcb37-132">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span> <span data-ttu-id="dcb37-133">Para obter mais informações, confira [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="dcb37-133">For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).</span></span>

## <span data-ttu-id="dcb37-134">ENTRADAS</span><span class="sxs-lookup"><span data-stu-id="dcb37-134">INPUTS</span></span>

### <span data-ttu-id="dcb37-135">Nenhum</span><span class="sxs-lookup"><span data-stu-id="dcb37-135">None</span></span>

## <span data-ttu-id="dcb37-136">SAÍDAS</span><span class="sxs-lookup"><span data-stu-id="dcb37-136">OUTPUTS</span></span>

### <span data-ttu-id="dcb37-137">System.Object</span><span class="sxs-lookup"><span data-stu-id="dcb37-137">System.Object</span></span>

## <span data-ttu-id="dcb37-138">OBSERVAÇÕES</span><span class="sxs-lookup"><span data-stu-id="dcb37-138">NOTES</span></span>

## <span data-ttu-id="dcb37-139">LINKS RELACIONADOS</span><span class="sxs-lookup"><span data-stu-id="dcb37-139">RELATED LINKS</span></span>

[<span data-ttu-id="dcb37-140">Visão geral da Desired State Configuration do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcb37-140">Windows PowerShell Desired State Configuration Overview</span></span>](/powershell/scripting/dsc/overview/dscforengineers)

