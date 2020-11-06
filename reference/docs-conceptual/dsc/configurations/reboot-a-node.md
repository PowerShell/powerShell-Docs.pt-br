---
ms.date: 01/17/2019
keywords: DSC,powershell,configuração,instalação
title: Reiniciar um nó
description: Muitas definições de configuração podem exigir a reinicialização do computador para que a alteração da configuração seja concluída. Este artigo explica como gerenciar reinicializações em uma configuração.
ms.openlocfilehash: d2b0f77c34ebcb006821da1f4f8d7c4b046f7a95
ms.sourcegitcommit: 488a940c7c828820b36a6ba56c119f64614afc29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92645109"
---
# <a name="reboot-a-node"></a><span data-ttu-id="99c41-105">Reiniciar um nó</span><span class="sxs-lookup"><span data-stu-id="99c41-105">Reboot a Node</span></span>

> [!NOTE]
> <span data-ttu-id="99c41-106">Este tópico aborda a reinicialização de um nó.</span><span class="sxs-lookup"><span data-stu-id="99c41-106">This topic talks about how to reboot a Node.</span></span> <span data-ttu-id="99c41-107">Para que a reinicialização seja bem-sucedida, as configurações do LCM **ActionAfterReboot** e **RebootNodeIfNeeded** precisam ser definidas corretamente.</span><span class="sxs-lookup"><span data-stu-id="99c41-107">In order for the reboot to be successful the **ActionAfterReboot** and **RebootNodeIfNeeded** LCM settings need to be configured properly.</span></span> <span data-ttu-id="99c41-108">Para ler sobre as configurações do Gerenciador de Configurações Local, confira [Configurar o Gerenciador de Configurações Local](../managing-nodes/metaConfig.md) ou [Configurar o Gerenciador de Configurações Local (v4)](../managing-nodes/metaConfig4.md).</span><span class="sxs-lookup"><span data-stu-id="99c41-108">To read about Local Configuration Manager settings, see [Configure the Local Configuration Manager](../managing-nodes/metaConfig.md), or [Configure the Local Configuration Manager (v4)](../managing-nodes/metaConfig4.md).</span></span>

<span data-ttu-id="99c41-109">É possível reinicializar nós de dentro de um recurso usando o sinalizador `$global:DSCMachineStatus`.</span><span class="sxs-lookup"><span data-stu-id="99c41-109">Nodes can be rebooted from within a resource, by using the `$global:DSCMachineStatus` flag.</span></span> <span data-ttu-id="99c41-110">Definir esse sinalizador como `1` na função `Set-TargetResource` força o LCM a reinicializar o nó diretamente após o método **Set** do recurso atual.</span><span class="sxs-lookup"><span data-stu-id="99c41-110">Setting this flag to `1` in the `Set-TargetResource` function forces the LCM to reboot the Node directly after the **Set** method of the current resource.</span></span> <span data-ttu-id="99c41-111">Com esse sinalizador, o recurso **PendingReboot** no módulo do Recurso DSC [ComputerManagementDsc](https://github.com/PowerShell/ComputerManagementDsc) detectará se há uma reinicialização pendente fora do DSC.</span><span class="sxs-lookup"><span data-stu-id="99c41-111">Using this flag, the **PendingReboot** resource in the [ComputerManagementDsc](https://github.com/PowerShell/ComputerManagementDsc) DSC Resource module detects if a reboot is pending outside of DSC.</span></span>

<span data-ttu-id="99c41-112">Suas [configurações](configurations.md) podem executar etapas que exigem a reinicialização do nó.</span><span class="sxs-lookup"><span data-stu-id="99c41-112">Your [configurations](configurations.md) may perform steps that require the Node to reboot.</span></span> <span data-ttu-id="99c41-113">Essas etapas poderiam incluir:</span><span class="sxs-lookup"><span data-stu-id="99c41-113">This could include things such as:</span></span>

- <span data-ttu-id="99c41-114">Atualizações do Windows</span><span class="sxs-lookup"><span data-stu-id="99c41-114">Windows updates</span></span>
- <span data-ttu-id="99c41-115">Instalações de software</span><span class="sxs-lookup"><span data-stu-id="99c41-115">Software install</span></span>
- <span data-ttu-id="99c41-116">Renomeações de arquivo</span><span class="sxs-lookup"><span data-stu-id="99c41-116">File renames</span></span>
- <span data-ttu-id="99c41-117">Renomeações de computador</span><span class="sxs-lookup"><span data-stu-id="99c41-117">Computer rename</span></span>

<span data-ttu-id="99c41-118">O recurso **PendingReboot** verifica locais específicos do computador para determinar se uma reinicialização está pendente.</span><span class="sxs-lookup"><span data-stu-id="99c41-118">The **PendingReboot** resource checks specific computer locations to determine if a reboot is pending.</span></span> <span data-ttu-id="99c41-119">Se o nó exigir uma reinicialização fora do DSC, o recurso **PendingReboot** definirá o sinalizador `$global:DSCMachineStatus` como `1`, forçando uma reinicialização e resolvendo a condição pendente.</span><span class="sxs-lookup"><span data-stu-id="99c41-119">If the Node requires a reboot outside of DSC, the **PendingReboot** resource sets the `$global:DSCMachineStatus` flag to `1` forcing a reboot and resolving the pending condition.</span></span>

> [!NOTE]
> <span data-ttu-id="99c41-120">Qualquer recurso de DSC pode instruir o LCM a reinicializar o nó definindo esse sinalizador na função `Set-TargetResource`.</span><span class="sxs-lookup"><span data-stu-id="99c41-120">Any DSC resource can instruct the LCM to reboot the node by setting this flag in the `Set-TargetResource` function.</span></span> <span data-ttu-id="99c41-121">Para obter mais informações, confira [Escrevendo um recurso personalizado de DSC com MOF](../resources/authoringResourceMOF.md).</span><span class="sxs-lookup"><span data-stu-id="99c41-121">For more information, see [Writing a custom DSC resource with MOF](../resources/authoringResourceMOF.md).</span></span>

## <a name="syntax"></a><span data-ttu-id="99c41-122">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="99c41-122">Syntax</span></span>

```
PendingReboot [String] #ResourceName
{
    Name = [string]
    [DependsOn = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
    [SkipCcmClientSDK = [bool]]
    [SkipComponentBasedServicing = [bool]]
    [SkipPendingComputerRename = [bool]]
    [SkipPendingFileRename = [bool]]
    [SkipWindowsUpdate = [bool]]
}
```

## <a name="properties"></a><span data-ttu-id="99c41-123">Propriedades</span><span class="sxs-lookup"><span data-stu-id="99c41-123">Properties</span></span>

| <span data-ttu-id="99c41-124">Propriedade</span><span class="sxs-lookup"><span data-stu-id="99c41-124">Property</span></span> | <span data-ttu-id="99c41-125">Descrição</span><span class="sxs-lookup"><span data-stu-id="99c41-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="99c41-126">Name</span><span class="sxs-lookup"><span data-stu-id="99c41-126">Name</span></span>| <span data-ttu-id="99c41-127">Parâmetro obrigatório que deve ser exclusivo por instância do recurso dentro de uma configuração.</span><span class="sxs-lookup"><span data-stu-id="99c41-127">Required parameter that must be unique per instance of the resource within a configuration.</span></span>|
| <span data-ttu-id="99c41-128">SkipComponentBasedServicing</span><span class="sxs-lookup"><span data-stu-id="99c41-128">SkipComponentBasedServicing</span></span> | <span data-ttu-id="99c41-129">Ignorar reinicializações disparadas pelo componente de Serviço Baseado em Componente.</span><span class="sxs-lookup"><span data-stu-id="99c41-129">Skip reboots triggered by the Component-Based Servicing component.</span></span> |
| <span data-ttu-id="99c41-130">SkipWindowsUpdate</span><span class="sxs-lookup"><span data-stu-id="99c41-130">SkipWindowsUpdate</span></span> | <span data-ttu-id="99c41-131">Ignorar reinicializações disparadas pelo Windows Update.</span><span class="sxs-lookup"><span data-stu-id="99c41-131">Skip reboots triggered by Windows Update.</span></span>|
| <span data-ttu-id="99c41-132">SkipPendingFileRename</span><span class="sxs-lookup"><span data-stu-id="99c41-132">SkipPendingFileRename</span></span> | <span data-ttu-id="99c41-133">Ignorar reinicializações com renomeação de arquivo pendente.</span><span class="sxs-lookup"><span data-stu-id="99c41-133">Skip pending file rename reboots.</span></span> |
| <span data-ttu-id="99c41-134">SkipCcmClientSDK</span><span class="sxs-lookup"><span data-stu-id="99c41-134">SkipCcmClientSDK</span></span> | <span data-ttu-id="99c41-135">Ignorar reinicializações disparadas pelo cliente do ConfigMgr.</span><span class="sxs-lookup"><span data-stu-id="99c41-135">Skip reboots triggered by the ConfigMgr client.</span></span> |
| <span data-ttu-id="99c41-136">SkipComputerRename</span><span class="sxs-lookup"><span data-stu-id="99c41-136">SkipComputerRename</span></span> | <span data-ttu-id="99c41-137">Ignorar reinicializações disparadas por renomeações de computador.</span><span class="sxs-lookup"><span data-stu-id="99c41-137">Skip reboots triggered by Computer renames.</span></span> |
| <span data-ttu-id="99c41-138">PSDSCRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="99c41-138">PSDSCRunAsCredential</span></span> | <span data-ttu-id="99c41-139">Com suporte na v5.</span><span class="sxs-lookup"><span data-stu-id="99c41-139">Supported in v5.</span></span> <span data-ttu-id="99c41-140">Executa o recurso como o usuário especificado.</span><span class="sxs-lookup"><span data-stu-id="99c41-140">Executes the resource as the specified user.</span></span> |
| <span data-ttu-id="99c41-141">DependsOn</span><span class="sxs-lookup"><span data-stu-id="99c41-141">DependsOn</span></span> | <span data-ttu-id="99c41-142">Indica que a configuração de outro recurso deve ser executada antes de ele ser configurado.</span><span class="sxs-lookup"><span data-stu-id="99c41-142">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="99c41-143">Por exemplo, se a ID do bloco de script de configuração do recurso que você deseja executar primeiro for **ResourceName** e seu tipo for **ResourceType** , a sintaxe para usar essa propriedade será `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="99c41-143">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType** , the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span> <span data-ttu-id="99c41-144">Para obter mais informações, confira [Usando DependsOn](resource-depends-on.md)</span><span class="sxs-lookup"><span data-stu-id="99c41-144">For more information, see [Using DependsOn](resource-depends-on.md)</span></span>|

## <a name="example"></a><span data-ttu-id="99c41-145">Exemplo</span><span class="sxs-lookup"><span data-stu-id="99c41-145">Example</span></span>

<span data-ttu-id="99c41-146">O exemplo a seguir instala o Microsoft Exchange usando o recurso [xExchange](https://github.com/PowerShell/xExchange).</span><span class="sxs-lookup"><span data-stu-id="99c41-146">The following example installs Microsoft Exchange using the [xExchange](https://github.com/PowerShell/xExchange) resource.</span></span> <span data-ttu-id="99c41-147">Durante a instalação, o recurso **PendingReboot** é usado para reinicializar o nó.</span><span class="sxs-lookup"><span data-stu-id="99c41-147">Throughout the install, the **PendingReboot** resource is used to reboot the Node.</span></span>

> [!NOTE]
> <span data-ttu-id="99c41-148">Esse exemplo requer a credencial de uma conta com direitos para adicionar um servidor do Exchange à floresta.</span><span class="sxs-lookup"><span data-stu-id="99c41-148">This example requires the credential of an account that has rights to add an Exchange server to the forest.</span></span> <span data-ttu-id="99c41-149">Para obter mais informações sobre como usar credenciais na DSC, confira [Lidando com Credenciais na DSC](../configurations/configDataCredentials.md)</span><span class="sxs-lookup"><span data-stu-id="99c41-149">For more information on using credentials in DSC, see [Handling Credentials in DSC](../configurations/configDataCredentials.md)</span></span>

```powershell
$ConfigurationData = @{
    AllNodes = @(
        @{
            NodeName                    = '*'
            PSDSCAllowPlainTextPassword = $true
        },
        @{
            NodeName = 'DSCPULL-1'
        }
    )
}

Configuration Example
{
    param
    (
        [Parameter(Mandatory = $true)]
        [System.Management.Automation.PSCredential]
        $ExchangeAdminCredential
    )

    Import-DscResource -Module xExchange
    Import-DscResource -Module ComputerManagementDsc

    Node $AllNodes.NodeName
    {
        # Copy the Exchange setup files locally
        File ExchangeBinaries
        {
            Ensure          = 'Present'
            Type            = 'Directory'
            Recurse         = $true
            SourcePath      = '\\rras-1\Binaries\E15CU6'
            DestinationPath = 'C:\Binaries\E15CU6'
        }

        # Check if a reboot is needed before installing Exchange
        PendingReboot BeforeExchangeInstall
        {
            Name       = 'BeforeExchangeInstall'
            DependsOn  = '[File]ExchangeBinaries'
        }

        # Do the Exchange install
        xExchInstall InstallExchange
        {
            Path       = 'C:\Binaries\E15CU6\Setup.exe'
            Arguments  = '/mode:Install /role:Mailbox /Iacceptexchangeserverlicenseterms'
            Credential = $ExchangeAdminCredential
            DependsOn  = '[PendingReboot]BeforeExchangeInstall'
        }

        # See if a reboot is required after installing Exchange
        PendingReboot AfterExchangeInstall
        {
            Name      = 'AfterExchangeInstall'
            DependsOn = '[xExchInstall]InstallExchange'
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="99c41-150">Este exemplo pressupõe que você tenha configurado o Gerenciador de Configurações Local para permitir reinicializações e continuar a configuração após uma reinicialização.</span><span class="sxs-lookup"><span data-stu-id="99c41-150">This example assumes that you have configured your Local Configuration Manager to allow reboots and continue the configuration after a reboot.</span></span>

## <a name="where-to-download"></a><span data-ttu-id="99c41-151">Onde baixar</span><span class="sxs-lookup"><span data-stu-id="99c41-151">Where to Download</span></span>

<span data-ttu-id="99c41-152">Você pode baixar os recursos usados neste tópico nos seguintes locais ou usando a Galeria do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99c41-152">You can download the resources used in this topic at the following locations, or by using the PowerShell gallery.</span></span>

- [<span data-ttu-id="99c41-153">ComputerManagementDsc</span><span class="sxs-lookup"><span data-stu-id="99c41-153">ComputerManagementDsc</span></span>](https://github.com/PowerShell/ComputerManagementDsc)
- [<span data-ttu-id="99c41-154">xExchange</span><span class="sxs-lookup"><span data-stu-id="99c41-154">xExchange</span></span>](https://github.com/PowerShell/xExchange)
