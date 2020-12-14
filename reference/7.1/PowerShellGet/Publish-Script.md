---
external help file: PSModule-help.xml
keywords: powershell, cmdlet
Locale: en-US
Module Name: PowerShellGet
ms.date: 03/27/2020
online version: https://docs.microsoft.com/powershell/module/powershellget/publish-script?view=powershell-7.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Publish-Script
ms.openlocfilehash: e7ac362b853a006da25bacccaa64f671cac30814
ms.sourcegitcommit: 22c93550c87af30c4895fcb9e9dd65e30d60ada0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2020
ms.locfileid: "94892162"
---
# <span data-ttu-id="9ee87-103">Publish-Script</span><span class="sxs-lookup"><span data-stu-id="9ee87-103">Publish-Script</span></span>

## <span data-ttu-id="9ee87-104">SINOPSE</span><span class="sxs-lookup"><span data-stu-id="9ee87-104">SYNOPSIS</span></span>
<span data-ttu-id="9ee87-105">Publica um script.</span><span class="sxs-lookup"><span data-stu-id="9ee87-105">Publishes a script.</span></span>

## <span data-ttu-id="9ee87-106">SYNTAX</span><span class="sxs-lookup"><span data-stu-id="9ee87-106">SYNTAX</span></span>

### <span data-ttu-id="9ee87-107">PathParameterSet (padrão)</span><span class="sxs-lookup"><span data-stu-id="9ee87-107">PathParameterSet (Default)</span></span>

```
Publish-Script -Path <String> [-NuGetApiKey <String>] [-Repository <String>]
 [-Credential <PSCredential>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]
```

### <span data-ttu-id="9ee87-108">LiteralPathParameterSet</span><span class="sxs-lookup"><span data-stu-id="9ee87-108">LiteralPathParameterSet</span></span>

```
Publish-Script -LiteralPath <String> [-NuGetApiKey <String>] [-Repository <String>]
 [-Credential <PSCredential>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## <span data-ttu-id="9ee87-109">DESCRIPTION</span><span class="sxs-lookup"><span data-stu-id="9ee87-109">DESCRIPTION</span></span>

<span data-ttu-id="9ee87-110">O `Publish-Script` cmdlet publica o script especificado na galeria online.</span><span class="sxs-lookup"><span data-stu-id="9ee87-110">The `Publish-Script` cmdlet publishes the specified script to the online gallery.</span></span>

## <span data-ttu-id="9ee87-111">EXEMPLOS</span><span class="sxs-lookup"><span data-stu-id="9ee87-111">EXAMPLES</span></span>

### <span data-ttu-id="9ee87-112">Exemplo 1: criar um arquivo de script, adicionar conteúdo a ele e publicá-lo</span><span class="sxs-lookup"><span data-stu-id="9ee87-112">Example 1: Create a script file, add content to it, and publish it</span></span>

<span data-ttu-id="9ee87-113">O `New-ScriptFileInfo` cmdlet cria um arquivo de script chamado `Demo-Script.ps1` .</span><span class="sxs-lookup"><span data-stu-id="9ee87-113">The `New-ScriptFileInfo` cmdlet creates a script file named `Demo-Script.ps1`.</span></span> <span data-ttu-id="9ee87-114">`Get-Content` exibe o conteúdo de `Demo-Script.ps1` .</span><span class="sxs-lookup"><span data-stu-id="9ee87-114">`Get-Content` displays the content of `Demo-Script.ps1`.</span></span> <span data-ttu-id="9ee87-115">O `Add-Content` cmdlet adiciona uma função e um fluxo de trabalho ao `Demo-Script.ps1` .</span><span class="sxs-lookup"><span data-stu-id="9ee87-115">The `Add-Content` cmdlet adds a function and a workflow to `Demo-Script.ps1`.</span></span>

```powershell
$newScriptInfo = @{
  Path = 'D:\ScriptSharingDemo\Demo-Script.ps1'
  Version = '1.0'
  Author = 'author@contoso.com'
  Description = "my test script file description goes here"
}
New-ScriptFileInfo @newScriptInfo
Get-Content -Path $newScriptInfo.Path
```

```Output
<#PSScriptInfo

.VERSION 1.0

.AUTHOR pattif@microsoft.com

.COMPANYNAME

.COPYRIGHT

.TAGS

.LICENSEURI

.PROJECTURI

.ICONURI

.EXTERNALMODULEDEPENDENCIES

.REQUIREDSCRIPTS

.EXTERNALSCRIPTDEPENDENCIES

.RELEASENOTES
#>

<#
.DESCRIPTION
 my test script file description goes here
#>
Param()
```

```powershell
Add-Content -Path D:\ScriptSharingDemo\Demo-Script.ps1 -Value @"

Function Demo-ScriptFunction { 'Demo-ScriptFunction' }

Workflow Demo-ScriptWorkflow { 'Demo-ScriptWorkflow' }

Demo-ScriptFunction
Demo-ScriptWorkflow
"@
Test-ScriptFileInfo -Path D:\ScriptSharingDemo\Demo-Script.ps1
```

```Output
Version    Name                 Author                   Description
-------    ----                 ------                   -----------
1.0        Demo-Script          author@contoso.com       my test script file description goes here
```

```powershell
Publish-Script -Path D:\ScriptSharingDemo\Demo-Script.ps1 -Repository LocalRepo1
Find-Script -Repository LocalRepo1 -Name "Demo-Script"
```

```Output
Version    Name                 Type       Repository    Description
-------    ----                 ----       ----------    -----------
1.0        Demo-Script          Script     LocalRepo1    my test script file description goes here
```

<span data-ttu-id="9ee87-116">O `Test-ScriptFileInfo` cmdlet é validado `Demo-Script.ps1` .</span><span class="sxs-lookup"><span data-stu-id="9ee87-116">The `Test-ScriptFileInfo` cmdlet validates `Demo-Script.ps1`.</span></span> <span data-ttu-id="9ee87-117">O `Publish-Script` cmdlet publica o script no repositório **LocalRepo1** .</span><span class="sxs-lookup"><span data-stu-id="9ee87-117">The `Publish-Script` cmdlet publishes the script to the **LocalRepo1** repository.</span></span> <span data-ttu-id="9ee87-118">Por fim.</span><span class="sxs-lookup"><span data-stu-id="9ee87-118">Finally.</span></span> <span data-ttu-id="9ee87-119">`Find-Script` é usado para pesquisar `Demo-Script.ps1` no repositório **LocalRepo1** .</span><span class="sxs-lookup"><span data-stu-id="9ee87-119">`Find-Script` is used to search for `Demo-Script.ps1` in the **LocalRepo1** repository.</span></span>

## <span data-ttu-id="9ee87-120">PARAMETERS</span><span class="sxs-lookup"><span data-stu-id="9ee87-120">PARAMETERS</span></span>

### <span data-ttu-id="9ee87-121">-Confirm</span><span class="sxs-lookup"><span data-stu-id="9ee87-121">-Confirm</span></span>

<span data-ttu-id="9ee87-122">Solicita sua confirmação antes de executar o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9ee87-122">Prompts you for confirmation before running the cmdlet.</span></span>

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

### <span data-ttu-id="9ee87-123">-Credential</span><span class="sxs-lookup"><span data-stu-id="9ee87-123">-Credential</span></span>

```yaml
Type: System.Management.Automation.PSCredential
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### <span data-ttu-id="9ee87-124">-Force</span><span class="sxs-lookup"><span data-stu-id="9ee87-124">-Force</span></span>

<span data-ttu-id="9ee87-125">Força o comando a ser executado sem solicitar a confirmação do usuário.</span><span class="sxs-lookup"><span data-stu-id="9ee87-125">Forces the command to run without asking for user confirmation.</span></span>

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

### <span data-ttu-id="9ee87-126">-LiteralPath</span><span class="sxs-lookup"><span data-stu-id="9ee87-126">-LiteralPath</span></span>

<span data-ttu-id="9ee87-127">Especifica um caminho para um ou mais locais.</span><span class="sxs-lookup"><span data-stu-id="9ee87-127">Specifies a path to one or more locations.</span></span> <span data-ttu-id="9ee87-128">Ao contrário do parâmetro **path** , o valor do parâmetro **LiteralPath** é usado exatamente como inserido.</span><span class="sxs-lookup"><span data-stu-id="9ee87-128">Unlike the **Path** parameter, the value of the **LiteralPath** parameter is used exactly as entered.</span></span> <span data-ttu-id="9ee87-129">Nenhum caractere é interpretado como caractere curinga.</span><span class="sxs-lookup"><span data-stu-id="9ee87-129">No characters are interpreted as wildcards.</span></span> <span data-ttu-id="9ee87-130">Se o caminho incluir caracteres de escape, coloque-os entre aspas simples.</span><span class="sxs-lookup"><span data-stu-id="9ee87-130">If the path includes escape characters, enclose them in single quotation marks.</span></span> <span data-ttu-id="9ee87-131">As aspas simples instruem o Windows PowerShell a nunca interpretar caracteres como sequências de escape.</span><span class="sxs-lookup"><span data-stu-id="9ee87-131">Single quotation marks tell Windows PowerShell not to interpret any characters as escape sequences.</span></span>

```yaml
Type: System.String
Parameter Sets: LiteralPathParameterSet
Aliases: PSPath

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### <span data-ttu-id="9ee87-132">-NuGetApiKey</span><span class="sxs-lookup"><span data-stu-id="9ee87-132">-NuGetApiKey</span></span>

<span data-ttu-id="9ee87-133">Especifica a chave de API que você deseja usar para publicar um script na galeria online.</span><span class="sxs-lookup"><span data-stu-id="9ee87-133">Specifies the API key that you want to use to publish a script to the online gallery.</span></span> <span data-ttu-id="9ee87-134">A chave de API é parte do seu perfil na galeria online.</span><span class="sxs-lookup"><span data-stu-id="9ee87-134">The API key is part of your profile in the online gallery.</span></span> <span data-ttu-id="9ee87-135">Para obter mais informações, consulte [Gerenciando chaves de API](/powershell/scripting/gallery/how-to/managing-profile/creating-apikeys).</span><span class="sxs-lookup"><span data-stu-id="9ee87-135">For more information see [Managing API keys](/powershell/scripting/gallery/how-to/managing-profile/creating-apikeys).</span></span>

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="9ee87-136">-Path</span><span class="sxs-lookup"><span data-stu-id="9ee87-136">-Path</span></span>

<span data-ttu-id="9ee87-137">Especifica um caminho para um ou mais locais.</span><span class="sxs-lookup"><span data-stu-id="9ee87-137">Specifies a path to one or more locations.</span></span> <span data-ttu-id="9ee87-138">Caracteres curinga são permitidos.</span><span class="sxs-lookup"><span data-stu-id="9ee87-138">Wildcards are permitted.</span></span> <span data-ttu-id="9ee87-139">O local padrão é o diretório atual.</span><span class="sxs-lookup"><span data-stu-id="9ee87-139">The default location is the current directory.</span></span>

```yaml
Type: System.String
Parameter Sets: PathParameterSet
Aliases:

Required: True
Position: Named
Default value: <Current location>
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: True
```

### <span data-ttu-id="9ee87-140">-Repositório</span><span class="sxs-lookup"><span data-stu-id="9ee87-140">-Repository</span></span>

<span data-ttu-id="9ee87-141">Especifica o nome amigável de um repositório que foi registrado pela execução `Register-PSRepository` .</span><span class="sxs-lookup"><span data-stu-id="9ee87-141">Specifies the friendly name of a repository that has been registered by running `Register-PSRepository`.</span></span>

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="9ee87-142">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="9ee87-142">-WhatIf</span></span>

<span data-ttu-id="9ee87-143">Mostra o que aconteceria se o cmdlet fosse executado.</span><span class="sxs-lookup"><span data-stu-id="9ee87-143">Shows what would happen if the cmdlet runs.</span></span> <span data-ttu-id="9ee87-144">O cmdlet não é executado.</span><span class="sxs-lookup"><span data-stu-id="9ee87-144">The cmdlet is not run.</span></span>

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

### <span data-ttu-id="9ee87-145">CommonParameters</span><span class="sxs-lookup"><span data-stu-id="9ee87-145">CommonParameters</span></span>

<span data-ttu-id="9ee87-146">Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9ee87-146">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span> <span data-ttu-id="9ee87-147">Para obter mais informações, confira [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="9ee87-147">For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).</span></span>

## <span data-ttu-id="9ee87-148">ENTRADAS</span><span class="sxs-lookup"><span data-stu-id="9ee87-148">INPUTS</span></span>

### <span data-ttu-id="9ee87-149">System.String</span><span class="sxs-lookup"><span data-stu-id="9ee87-149">System.String</span></span>

### <span data-ttu-id="9ee87-150">System. Management. Automation. PSCredential</span><span class="sxs-lookup"><span data-stu-id="9ee87-150">System.Management.Automation.PSCredential</span></span>

## <span data-ttu-id="9ee87-151">SAÍDAS</span><span class="sxs-lookup"><span data-stu-id="9ee87-151">OUTPUTS</span></span>

### <span data-ttu-id="9ee87-152">System.Object</span><span class="sxs-lookup"><span data-stu-id="9ee87-152">System.Object</span></span>

## <span data-ttu-id="9ee87-153">OBSERVAÇÕES</span><span class="sxs-lookup"><span data-stu-id="9ee87-153">NOTES</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ee87-154">A partir de abril de 2020, o Galeria do PowerShell não dá mais suporte às versões 1,0 e 1,1 da segurança da camada de transporte (TLS).</span><span class="sxs-lookup"><span data-stu-id="9ee87-154">As of April 2020, the PowerShell Gallery no longer supports Transport Layer Security (TLS) versions 1.0 and 1.1.</span></span> <span data-ttu-id="9ee87-155">Se você não estiver usando o TLS 1,2 ou superior, receberá um erro ao tentar acessar o Galeria do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ee87-155">If you are not using TLS 1.2 or higher, you will receive an error when trying to access the PowerShell Gallery.</span></span> <span data-ttu-id="9ee87-156">Use o comando a seguir para garantir que você esteja usando o TLS 1,2:</span><span class="sxs-lookup"><span data-stu-id="9ee87-156">Use the following command to ensure you are using TLS 1.2:</span></span>
>
> `[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12`
>
> <span data-ttu-id="9ee87-157">Para obter mais informações, consulte o [comunicado](https://devblogs.microsoft.com/powershell/powershell-gallery-tls-support/) no blog do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ee87-157">For more information, see the [announcement](https://devblogs.microsoft.com/powershell/powershell-gallery-tls-support/) in the PowerShell blog.</span></span>

## <span data-ttu-id="9ee87-158">LINKS RELACIONADOS</span><span class="sxs-lookup"><span data-stu-id="9ee87-158">RELATED LINKS</span></span>

[<span data-ttu-id="9ee87-159">Find-Script</span><span class="sxs-lookup"><span data-stu-id="9ee87-159">Find-Script</span></span>](Find-Script.md)

[<span data-ttu-id="9ee87-160">Install-Script</span><span class="sxs-lookup"><span data-stu-id="9ee87-160">Install-Script</span></span>](Install-Script.md)

[<span data-ttu-id="9ee87-161">Publish-Script</span><span class="sxs-lookup"><span data-stu-id="9ee87-161">Publish-Script</span></span>](Publish-Script.md)

[<span data-ttu-id="9ee87-162">Save-Script</span><span class="sxs-lookup"><span data-stu-id="9ee87-162">Save-Script</span></span>](Save-Script.md)

[<span data-ttu-id="9ee87-163">Update-Script</span><span class="sxs-lookup"><span data-stu-id="9ee87-163">Update-Script</span></span>](Update-Script.md)
