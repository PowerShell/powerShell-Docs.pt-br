---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Configurar uma máquina virtual na inicialização inicial usando DSC
ms.openlocfilehash: 48f5e30bed0b97b80724fbf95ec604ede9f2ea5d
ms.sourcegitcommit: c4906f4c9fa4ef1a16dcd6dd00ff960d19446d71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/01/2020
ms.locfileid: "89236281"
---
# <a name="configure-a-virtual-machines-at-initial-boot-up-by-using-dsc"></a><span data-ttu-id="9182e-103">Configurar uma máquina virtual na inicialização inicial usando DSC</span><span class="sxs-lookup"><span data-stu-id="9182e-103">Configure a virtual machines at initial boot-up by using DSC</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9182e-104">Aplica-se a: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="9182e-104">Applies To: Windows PowerShell 5.0</span></span>

## <a name="requirements"></a><span data-ttu-id="9182e-105">Requisitos</span><span class="sxs-lookup"><span data-stu-id="9182e-105">Requirements</span></span>

> [!NOTE]
> <span data-ttu-id="9182e-106">A chave do Registro **DSCAutomationHostEnabled** descrita neste tópico não está disponível no PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="9182e-106">The **DSCAutomationHostEnabled** registry key described in this topic is not available in PowerShell 4.0.</span></span>
> <span data-ttu-id="9182e-107">Para obter informações sobre como configurar novas máquinas virtuais na inicialização inicial no PowerShell 4.0, veja [Want to Automatically Configure Your Machines Using DSC at Initial Boot-up?](https://blogs.msdn.microsoft.com/powershell/2014/02/28/want-to-automatically-configure-your-machines-using-dsc-at-initial-boot-up/) (Deseja configurar seus computadores automaticamente usando DSC na inicialização inicial?)</span><span class="sxs-lookup"><span data-stu-id="9182e-107">For information on how to configure new virtual machines at initial boot-up in PowerShell 4.0, see [Want to Automatically Configure Your Machines Using DSC at Initial Boot-up?](https://blogs.msdn.microsoft.com/powershell/2014/02/28/want-to-automatically-configure-your-machines-using-dsc-at-initial-boot-up/)</span></span>

<span data-ttu-id="9182e-108">Para executar esses exemplos, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="9182e-108">To run these examples, you will need:</span></span>

- <span data-ttu-id="9182e-109">Um VHD inicializável com o qual trabalhar.</span><span class="sxs-lookup"><span data-stu-id="9182e-109">A bootable VHD to work with.</span></span> <span data-ttu-id="9182e-110">Você pode baixar um arquivo ISO com uma cópia de avaliação do Windows Server 2016 no [Centro de Avaliação TechNet](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016).</span><span class="sxs-lookup"><span data-stu-id="9182e-110">You can download an ISO with an evaluation copy of Windows Server 2016 at [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016).</span></span>
  <span data-ttu-id="9182e-111">Você pode encontrar instruções sobre como criar um VHD de uma imagem ISO em [Criando discos rígidos virtuais inicializáveis](/previous-versions/windows/it-pro/windows-7/gg318049(v=ws.10)).</span><span class="sxs-lookup"><span data-stu-id="9182e-111">You can find instructions on how to create a VHD from an ISO image at [Creating Bootable Virtual Hard Disks](/previous-versions/windows/it-pro/windows-7/gg318049(v=ws.10)).</span></span>
- <span data-ttu-id="9182e-112">Um computador host com Hyper-V habilitado.</span><span class="sxs-lookup"><span data-stu-id="9182e-112">A host computer that has Hyper-V enabled.</span></span> <span data-ttu-id="9182e-113">Para obter informações, consulte [Visão geral do Hyper-V](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11)).</span><span class="sxs-lookup"><span data-stu-id="9182e-113">For information, see [Hyper-V overview](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11)).</span></span>

  <span data-ttu-id="9182e-114">Usando o DSC, você pode automatizar a instalação e a configuração de software em um computador na inicialização inicial.</span><span class="sxs-lookup"><span data-stu-id="9182e-114">By using DSC, you can automate software installation and configuration for a computer at initial boot-up.</span></span>
  <span data-ttu-id="9182e-115">Você faz isso inserindo um documento MOF de configuração ou então uma metaconfiguração em uma mídia inicializável (como um VHD), de modo que eles sejam executados durante o processo inicial de inicialização.</span><span class="sxs-lookup"><span data-stu-id="9182e-115">You do this by either injecting a configuration MOF document or a metaconfiguration into bootable media (such as a VHD) so that they are run during the initial boot-up process.</span></span>
  <span data-ttu-id="9182e-116">Esse comportamento é especificado pela chave do Registro [DSCAutomationHostEnabled](DSCAutomationHostEnabled.md) em `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System`.</span><span class="sxs-lookup"><span data-stu-id="9182e-116">This behavior is specified by the [DSCAutomationHostEnabled registry key](DSCAutomationHostEnabled.md) registry key under `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System`.</span></span>
  <span data-ttu-id="9182e-117">Por padrão, o valor dessa chave é 2, o que permite que o DSC seja executado no momento da inicialização.</span><span class="sxs-lookup"><span data-stu-id="9182e-117">By default, the value of this key is 2, which allows DSC to run at boot time.</span></span>

  <span data-ttu-id="9182e-118">Se você não quiser que o DSC seja executado no momento da inicialização, defina o valor da chave do Registro [DSCAutomationHostEnabled](DSCAutomationHostEnabled.md) como 0.</span><span class="sxs-lookup"><span data-stu-id="9182e-118">If you do not want DSC to run at boot time, set the value of the [DSCAutomationHostEnabled registry key](DSCAutomationHostEnabled.md) registry key to 0.</span></span>

- <span data-ttu-id="9182e-119">Inserir um documento MOF de configuração em um VHD</span><span class="sxs-lookup"><span data-stu-id="9182e-119">Inject a configuration MOF document into a VHD</span></span>
- <span data-ttu-id="9182e-120">Inserir uma metaconfiguração DSC em um VHD</span><span class="sxs-lookup"><span data-stu-id="9182e-120">Inject a DSC metaconfiguration into a VHD</span></span>
- <span data-ttu-id="9182e-121">Desabilite a DSC no momento da inicialização</span><span class="sxs-lookup"><span data-stu-id="9182e-121">Disable DSC at boot time</span></span>

> [!NOTE]
> <span data-ttu-id="9182e-122">Você pode inserir tanto `Pending.mof` quanto `MetaConfig.mof` em um computador simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="9182e-122">You can inject both `Pending.mof` and `MetaConfig.mof` into a computer at the same time.</span></span>
> <span data-ttu-id="9182e-123">Se ambos os arquivos estiverem presentes, as configurações especificadas em `MetaConfig.mof` têm precedência.</span><span class="sxs-lookup"><span data-stu-id="9182e-123">If both files are present, the settings specified in `MetaConfig.mof` take precedence.</span></span>

## <a name="inject-a-configuration-mof-document-into-a-vhd"></a><span data-ttu-id="9182e-124">Inserir um documento MOF de configuração em um VHD</span><span class="sxs-lookup"><span data-stu-id="9182e-124">Inject a configuration MOF document into a VHD</span></span>

<span data-ttu-id="9182e-125">Para aplicar uma configuração na inicialização inicial, você pode inserir um documento MOF configuração compilado no VHD como seu arquivo `Pending.mof`.</span><span class="sxs-lookup"><span data-stu-id="9182e-125">To enact a configuration at initial boot-up, you can inject a compiled configuration MOF document into the VHD as its `Pending.mof` file.</span></span>
<span data-ttu-id="9182e-126">Se a chave do Registro **DSCAutomationHostEnabled** estiver definida como 2 (o valor padrão), o DSC aplicará a configuração definida por `Pending.mof` quando o computador for inicializado pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="9182e-126">If the **DSCAutomationHostEnabled** registry key is set to 2 (the default value), DSC will apply the configuration defined by `Pending.mof` when the computer boots up for the first time.</span></span>

<span data-ttu-id="9182e-127">Neste exemplo, usaremos a configuração a seguir, que instalará o IIS no novo computador:</span><span class="sxs-lookup"><span data-stu-id="9182e-127">For this example, we will use the following configuration, which will install IIS on the new computer:</span></span>

```powershell
Configuration SampleIISInstall
{
    Import-DscResource -ModuleName 'PSDesiredStateConfiguration'

    node ('localhost')
    {
        WindowsFeature IIS
        {
            Ensure = 'Present'
            Name   = 'Web-Server'
        }
    }
}
```

### <a name="to-inject-the-configuration-mof-document-on-the-vhd"></a><span data-ttu-id="9182e-128">Para inserir o documento de configuração de MOF no VHD</span><span class="sxs-lookup"><span data-stu-id="9182e-128">To inject the configuration MOF document on the VHD</span></span>

1. <span data-ttu-id="9182e-129">Chamando o cmdlet [Mount-VHD](/powershell/module/hyper-v/mount-vhd), monte o VHD no qual você deseja inserir a configuração.</span><span class="sxs-lookup"><span data-stu-id="9182e-129">Mount the VHD into which you want to inject the configuration by calling the [Mount-VHD](/powershell/module/hyper-v/mount-vhd) cmdlet.</span></span> <span data-ttu-id="9182e-130">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9182e-130">For example:</span></span>

   ```powershell
   Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

2. <span data-ttu-id="9182e-131">Em um computador executando o PowerShell 5.0 ou posterior, salve a configuração acima (**SampleIISInstall**) como um arquivo de script (.ps1) do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9182e-131">On a computer running PowerShell 5.0 or later, save the above configuration (**SampleIISInstall**) as a PowerShell script (.ps1) file.</span></span>

3. <span data-ttu-id="9182e-132">No console do PowerShell, navegue até a pasta na qual você salvou o arquivo .ps1.</span><span class="sxs-lookup"><span data-stu-id="9182e-132">In a PowerShell console, navigate to the folder where you saved the .ps1 file.</span></span>

4. <span data-ttu-id="9182e-133">Execute os seguintes comandos do PowerShell para compilar o documento MOF (para obter informações sobre compilação de configurações DSC, consulte [Configurações DSC](../configurations/configurations.md)):</span><span class="sxs-lookup"><span data-stu-id="9182e-133">Run the following PowerShell commands to compile the MOF document (for information about compiling DSC configurations, see [DSC Configurations](../configurations/configurations.md):</span></span>

   ```powershell
   . .\SampleIISInstall.ps1
   SampleIISInstall
   ```

5. <span data-ttu-id="9182e-134">Isso criará um arquivo `localhost.mof` em uma nova pasta chamada `SampleIISInstall`.</span><span class="sxs-lookup"><span data-stu-id="9182e-134">This will create a `localhost.mof` file in a new folder named `SampleIISInstall`.</span></span>
   <span data-ttu-id="9182e-135">Renomear e mover esse arquivo para o local apropriado no VHD como `Pending.mof`, usando o cmdlet [Move-Item](/powershell/module/microsoft.powershell.management/move-item).</span><span class="sxs-lookup"><span data-stu-id="9182e-135">Rename and move that file into the proper location on the VHD as `Pending.mof` by using the [Move-Item](/powershell/module/microsoft.powershell.management/move-item) cmdlet.</span></span> <span data-ttu-id="9182e-136">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9182e-136">For example:</span></span>

   ```powershell
       Move-Item -Path C:\DSCTest\SampleIISInstall\localhost.mof -Destination E:\Windows\System32\Configuration\Pending.mof
   ```

6. <span data-ttu-id="9182e-137">Chamando o cmdlet [Dismount-VHD](/powershell/module/hyper-v/dismount-vhd), desmonte o VHD.</span><span class="sxs-lookup"><span data-stu-id="9182e-137">Dismount the VHD by calling the [Dismount-VHD](/powershell/module/hyper-v/dismount-vhd) cmdlet.</span></span> <span data-ttu-id="9182e-138">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9182e-138">For example:</span></span>

   ```powershell
   Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

7. <span data-ttu-id="9182e-139">Crie uma VM usando o VHD no qual você instalou o documento MOF do DSC.</span><span class="sxs-lookup"><span data-stu-id="9182e-139">Create a VM by using the VHD where you installed the DSC MOF document.</span></span>

<span data-ttu-id="9182e-140">Após a inicialização inicial e a instalação do sistema operacional, o IIS será instalado.</span><span class="sxs-lookup"><span data-stu-id="9182e-140">After initial boot-up and operating system installation, IIS will be installed.</span></span>
<span data-ttu-id="9182e-141">Você pode verificar isso chamando o cmdlet [Get-WindowsFeature](/powershell/module/servermanager/get-windowsfeature).</span><span class="sxs-lookup"><span data-stu-id="9182e-141">You can verify this by calling the [Get-WindowsFeature](/powershell/module/servermanager/get-windowsfeature) cmdlet.</span></span>

## <a name="inject-a-dsc-metaconfiguration-into-a-vhd"></a><span data-ttu-id="9182e-142">Inserir uma metaconfiguração DSC em um VHD</span><span class="sxs-lookup"><span data-stu-id="9182e-142">Inject a DSC metaconfiguration into a VHD</span></span>

<span data-ttu-id="9182e-143">Você também pode configurar um computador para efetuar pull de uma configuração na inicialização inicial, inserindo uma metaconfiguração (veja [Configurando o LCM [Configuration Manager Local]](../managing-nodes/metaConfig.md)) no VHD como seu arquivo `MetaConfig.mof`.</span><span class="sxs-lookup"><span data-stu-id="9182e-143">You can also configure a computer to pull a configuration at initial boot-up by injecting a metaconfiguration (see [Configuring the Local Configuration Manager (LCM)](../managing-nodes/metaConfig.md)) into the VHD as its `MetaConfig.mof` file.</span></span>
<span data-ttu-id="9182e-144">Se a chave do Registro **DSCAutomationHostEnabled** estiver definida como 2 (o valor padrão), o DSC aplicará a metaconfiguração definida por `MetaConfig.mof` ao LCM quando o computador for inicializado pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="9182e-144">If the **DSCAutomationHostEnabled** registry key is set to 2 (the default value),  DSC will apply the metaconfiguration defined by `MetaConfig.mof` to the LCM when the computer boots up for the first time.</span></span>
<span data-ttu-id="9182e-145">Se a metaconfiguração especificar que o LCM deve efetuar pull de configurações de um servidor de pull, o computador tentará efetuar pull de uma configuração do servidor de pull na inicialização inicial.</span><span class="sxs-lookup"><span data-stu-id="9182e-145">If the metaconfiguration specifies that the LCM should pull configurations from a pull server, the computer will attempt to pull a configuration from that pull server at initial boot-up.</span></span>
<span data-ttu-id="9182e-146">Para obter informações sobre a configuração de um servidor de pull de DSC, consulte [Configurando um servidor de pull da Web de DSC](../pull-server/pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="9182e-146">For information about setting up a DSC pull server, see [Setting up a DSC web pull server](../pull-server/pullServer.md).</span></span>

<span data-ttu-id="9182e-147">Neste exemplo, usaremos a configuração descrita na seção anterior (**SampleIISInstall**) e a metaconfiguração a seguir:</span><span class="sxs-lookup"><span data-stu-id="9182e-147">For this example, we will use both the configuration described in the previous section (**SampleIISInstall**), and the following metaconfiguration:</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientBootstrap
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
            ConfigurationNames = @('SampleIISInstall')
        }
    }
}
```

### <a name="to-inject-the-metaconfiguration-mof-document-on-the-vhd"></a><span data-ttu-id="9182e-148">Para inserir o documento MOF de metaconfiguração no VHD</span><span class="sxs-lookup"><span data-stu-id="9182e-148">To inject the metaconfiguration MOF document on the VHD</span></span>

1. <span data-ttu-id="9182e-149">Chamando o cmdlet [Mount-VHD](/powershell/module/hyper-v/mount-vhd), monte o VHD no qual você deseja inserir a metaconfiguração.</span><span class="sxs-lookup"><span data-stu-id="9182e-149">Mount the VHD into which you want to inject the metaconfiguration by calling the [Mount-VHD](/powershell/module/hyper-v/mount-vhd) cmdlet.</span></span> <span data-ttu-id="9182e-150">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9182e-150">For example:</span></span>

   ```powershell
   Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

2. <span data-ttu-id="9182e-151">[Configure um servidor de pull Web de DSC](../pull-server/pullServer.md) e salve a configuração **SampleIISInstall** na pasta apropriada.</span><span class="sxs-lookup"><span data-stu-id="9182e-151">[Set up a DSC web pull server](../pull-server/pullServer.md), and save the **SampleIISInstall** configuration to the appropriate folder.</span></span>

3. <span data-ttu-id="9182e-152">Em um computador executando o PowerShell 5.0 ou posterior, salve a metaconfiguração acima (**PullClientBootstrap**) como um arquivo de script do PowerShell (.ps1).</span><span class="sxs-lookup"><span data-stu-id="9182e-152">On a computer running PowerShell 5.0 or later, save the above metaconfiguration (**PullClientBootstrap**) as a PowerShell script (.ps1) file.</span></span>

4. <span data-ttu-id="9182e-153">No console do PowerShell, navegue até a pasta na qual você salvou o arquivo .ps1.</span><span class="sxs-lookup"><span data-stu-id="9182e-153">In a PowerShell console, navigate to the folder where you saved the .ps1 file.</span></span>

5. <span data-ttu-id="9182e-154">Execute os seguintes comandos do PowerShell para compilar o documento MOF de metaconfiguração (para obter informações sobre compilação de configurações DSC, consulte [Configurações DSC](../configurations/configurations.md)):</span><span class="sxs-lookup"><span data-stu-id="9182e-154">Run the following PowerShell commands to compile the  metaconfiguration MOF document (for information about compiling DSC configurations, see [DSC Configurations](../configurations/configurations.md):</span></span>

   ```powershell
   . .\PullClientBootstrap.ps1
   PullClientBootstrap
   ```

6. <span data-ttu-id="9182e-155">Isso criará um arquivo `localhost.meta.mof` em uma nova pasta chamada `PullClientBootstrap`.</span><span class="sxs-lookup"><span data-stu-id="9182e-155">This will create a `localhost.meta.mof` file in a new folder named `PullClientBootstrap`.</span></span>
   <span data-ttu-id="9182e-156">Renomear e mover esse arquivo para o local apropriado no VHD como `MetaConfig.mof`, usando o cmdlet [Move-Item](/powershell/module/microsoft.powershell.management/move-item).</span><span class="sxs-lookup"><span data-stu-id="9182e-156">Rename and move that file into the proper location on the VHD as `MetaConfig.mof` by using the [Move-Item](/powershell/module/microsoft.powershell.management/move-item) cmdlet.</span></span>

   ```powershell
   Move-Item -Path C:\DSCTest\PullClientBootstrap\localhost.meta.mof -Destination E:\Windows\System32\Configuration\MetaConfig.mof
   ```

7. <span data-ttu-id="9182e-157">Chamando o cmdlet [Dismount-VHD](/powershell/module/hyper-v/dismount-vhd), desmonte o VHD.</span><span class="sxs-lookup"><span data-stu-id="9182e-157">Dismount the VHD by calling the [Dismount-VHD](/powershell/module/hyper-v/dismount-vhd) cmdlet.</span></span> <span data-ttu-id="9182e-158">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9182e-158">For example:</span></span>

   ```powershell
   Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

8. <span data-ttu-id="9182e-159">Crie uma VM usando o VHD no qual você instalou o documento MOF do DSC.</span><span class="sxs-lookup"><span data-stu-id="9182e-159">Create a VM by using the VHD where you installed the DSC MOF document.</span></span>

<span data-ttu-id="9182e-160">Após a inicialização inicial e a instalação do sistema operacional, o DSC efetuará pull da configuração do servidor de pull e o IIS será instalado.</span><span class="sxs-lookup"><span data-stu-id="9182e-160">After initial boot-up and operating system installation, DSC will pull the configuration from the pull server, and IIS will be installed.</span></span>
<span data-ttu-id="9182e-161">Você pode verificar isso chamando o cmdlet [Get-WindowsFeature](/powershell/module/servermanager/get-windowsfeature).</span><span class="sxs-lookup"><span data-stu-id="9182e-161">You can verify this by calling the [Get-WindowsFeature](/powershell/module/servermanager/get-windowsfeature) cmdlet.</span></span>

## <a name="disable-dsc-at-boot-time"></a><span data-ttu-id="9182e-162">Desabilite a DSC no momento da inicialização</span><span class="sxs-lookup"><span data-stu-id="9182e-162">Disable DSC at boot time</span></span>

<span data-ttu-id="9182e-163">Por padrão, o valor da chave `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\DSCAutomationHostEnabled` é definido como 2, o que permite que uma configuração DSC seja executada se o computador estiver no estado pendente ou atual.</span><span class="sxs-lookup"><span data-stu-id="9182e-163">By default, the value of the `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\DSCAutomationHostEnabled` key is set to 2, which allows a DSC configuration to run if the computer is in pending or current state.</span></span> <span data-ttu-id="9182e-164">Se não desejar que uma configuração seja executada na inicialização inicial, você precisará definir o valor desta chave como 0:</span><span class="sxs-lookup"><span data-stu-id="9182e-164">If you do not want a configuration to run at initial boot-up, you need so set the value of this key to 0:</span></span>

1. <span data-ttu-id="9182e-165">Chamando o cmdlet [Mount-VHD](/powershell/module/hyper-v/mount-vhd), monte o VHD.</span><span class="sxs-lookup"><span data-stu-id="9182e-165">Mount the VHD by calling the [Mount-VHD](/powershell/module/hyper-v/mount-vhd) cmdlet.</span></span> <span data-ttu-id="9182e-166">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9182e-166">For example:</span></span>

   ```powershell
   Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

2. <span data-ttu-id="9182e-167">Carregue a subchave `HKLM\Software` do Registro do VHD chamando `reg load`.</span><span class="sxs-lookup"><span data-stu-id="9182e-167">Load the registry `HKLM\Software` subkey from the VHD by calling `reg load`.</span></span>

   ```powershell
   reg load HKLM\Vhd E:\Windows\System32\Config\Software`
   ```

3. <span data-ttu-id="9182e-168">Navegue até `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System` usando o provedor do Registro do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9182e-168">Navigate to the `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System` by using the PowerShell Registry provider.</span></span>

   ```powershell
   Set-Location HKLM:\Software\Microsoft\Windows\CurrentVersion\Policies\System`
   ```

4. <span data-ttu-id="9182e-169">Altere o valor de `DSCAutomationHostEnabled` para 0.</span><span class="sxs-lookup"><span data-stu-id="9182e-169">Change the value of `DSCAutomationHostEnabled` to 0.</span></span>

   ```powershell
   Set-ItemProperty -Path . -Name DSCAutomationHostEnabled -Value 0
   ```

5. <span data-ttu-id="9182e-170">Descarregue o Registro executando os comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9182e-170">Unload the registry by running the following commands:</span></span>

   ```powershell
   [gc]::Collect()
   reg unload HKLM\Vhd
   ```

## <a name="see-also"></a><span data-ttu-id="9182e-171">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="9182e-171">See Also</span></span>

[<span data-ttu-id="9182e-172">Configurações DSC</span><span class="sxs-lookup"><span data-stu-id="9182e-172">DSC Configurations</span></span>](../configurations/configurations.md)

[<span data-ttu-id="9182e-173">Chave do Registro de DSCAutomationHostEnabled</span><span class="sxs-lookup"><span data-stu-id="9182e-173">DSCAutomationHostEnabled registry key</span></span>](DSCAutomationHostEnabled.md)

[<span data-ttu-id="9182e-174">Configurando o LCM (Gerenciador de Configurações Local)</span><span class="sxs-lookup"><span data-stu-id="9182e-174">Configuring the Local Configuration Manager (LCM)</span></span>](../managing-nodes/metaConfig.md)

[<span data-ttu-id="9182e-175">Configurando um servidor de pull da Web de DSC</span><span class="sxs-lookup"><span data-stu-id="9182e-175">Setting up a DSC web pull server</span></span>](../pull-server/pullServer.md)
