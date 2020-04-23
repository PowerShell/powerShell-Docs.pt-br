---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,instalação
title: Melhorias da DSC no WMF 5.1
ms.openlocfilehash: 78c15f453977384ba437b0bd69cd620eb1a29fbd
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "80978280"
---
# <a name="improvements-in-desired-state-configuration-dsc-in-wmf-51"></a><span data-ttu-id="16205-103">Melhorias na DSC (Configuração de Estado Desejado) no WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="16205-103">Improvements in Desired State Configuration (DSC) in WMF 5.1</span></span>

## <a name="dsc-class-resource-improvements"></a><span data-ttu-id="16205-104">Melhorias de recursos de classe da DSC</span><span class="sxs-lookup"><span data-stu-id="16205-104">DSC class resource improvements</span></span>

<span data-ttu-id="16205-105">No 5.1 WMF, corrigimos os seguintes problemas conhecidos:</span><span class="sxs-lookup"><span data-stu-id="16205-105">In WMF 5.1, we have fixed the following known issues:</span></span>

- <span data-ttu-id="16205-106">O Get-DscConfiguration poderá retornar valores vazios (nulos) ou erros se um tipo complexo/de tabela de hash for retornado pela função Get() de um recurso DSC baseado em classe.</span><span class="sxs-lookup"><span data-stu-id="16205-106">Get-DscConfiguration may return empty values (null) or errors if a complex/hash table type is returned by Get() function of a class-based DSC resource.</span></span>
- <span data-ttu-id="16205-107">O Get-DscConfiguration retornará um erro se a credencial RunAs for usada na configuração DSC.</span><span class="sxs-lookup"><span data-stu-id="16205-107">Get-DscConfiguration returns error if RunAs credential is used in DSC configuration.</span></span>
- <span data-ttu-id="16205-108">Os recursos baseados em classe não podem ser usados em uma configuração de composição.</span><span class="sxs-lookup"><span data-stu-id="16205-108">Class-based resource cannot be used in a composite configuration.</span></span>
- <span data-ttu-id="16205-109">O Start-DscConfiguration será suspenso se o recurso baseado em classe tiver uma propriedade de seu próprio tipo.</span><span class="sxs-lookup"><span data-stu-id="16205-109">Start-DscConfiguration hangs if class-based resource has a property of its own type.</span></span>
- <span data-ttu-id="16205-110">O recurso baseado em classe não pode ser usado como um recurso exclusivo.</span><span class="sxs-lookup"><span data-stu-id="16205-110">Class-based resource cannot be used as an exclusive resource.</span></span>

## <a name="dsc-resource-debugging-improvements"></a><span data-ttu-id="16205-111">Melhorias de depuração de recursos da DSC</span><span class="sxs-lookup"><span data-stu-id="16205-111">DSC resource debugging improvements</span></span>

<span data-ttu-id="16205-112">No WMF 5.0, o depurador do PowerShell não interrompeu o método de recurso baseado em classe (Get/Set/Test) diretamente.</span><span class="sxs-lookup"><span data-stu-id="16205-112">In WMF 5.0, the PowerShell debugger did not stop at the class-based resource method (Get/Set/Test) directly.</span></span> <span data-ttu-id="16205-113">No WMF 5.1, o depurador interrompe o método de recurso baseado em classe da mesma forma que faz com os métodos de recursos baseados em MOF.</span><span class="sxs-lookup"><span data-stu-id="16205-113">In WMF 5.1, the debugger stops at the class-based resource method in the same way as for MOF-based resources methods.</span></span>

## <a name="dsc-pull-client-supports-tls-11-and-tls-12"></a><span data-ttu-id="16205-114">O cliente pull da DSC dá suporte para TLS 1.1 e para TLS 1.2</span><span class="sxs-lookup"><span data-stu-id="16205-114">DSC pull client supports TLS 1.1 and TLS 1.2</span></span>

<span data-ttu-id="16205-115">Anteriormente, o cliente pull da DSC dava suporte apenas para SSL3.0 e TLS1.0 por meio de conexões HTTPS.</span><span class="sxs-lookup"><span data-stu-id="16205-115">Previously, the DSC pull client only supported SSL3.0 and TLS1.0 over HTTPS connections.</span></span> <span data-ttu-id="16205-116">Se fosse forçado a usar protocolos mais seguros, o cliente pull pararia de funcionar.</span><span class="sxs-lookup"><span data-stu-id="16205-116">When forced to use more secure protocols, the pull client would stop functioning.</span></span> <span data-ttu-id="16205-117">No WMF 5.1, o cliente pull da DSC não dá mais suporte a SSL 3.0 e adiciona suporte a protocolos mais seguros TLS 1.1 e TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="16205-117">In WMF 5.1, the DSC pull client no longer supports SSL 3.0 and adds support for the more secure TLS 1.1 and TLS 1.2 protocols.</span></span>

## <a name="improved-pull-server-registration"></a><span data-ttu-id="16205-118">Registro do servidor de pull aprimorado</span><span class="sxs-lookup"><span data-stu-id="16205-118">Improved pull server registration</span></span>

<span data-ttu-id="16205-119">Nas versões anteriores do WMF, as solicitações simultâneas de registros/relatórios em um servidor de pull da DSC durante o uso do banco de dados ESENT provocavam uma falha de registro e/ou relatório do LCM.</span><span class="sxs-lookup"><span data-stu-id="16205-119">In the earlier versions of WMF, simultaneous registrations/reporting requests to a DSC pull server while using the ESENT database would lead to LCM failing to register and/or report.</span></span> <span data-ttu-id="16205-120">Nesses casos, os logs de eventos no servidor de pull têm o erro "O nome da instância já está em uso."</span><span class="sxs-lookup"><span data-stu-id="16205-120">In such cases, the event logs on the pull server has the error "Instance Name already in use."</span></span> <span data-ttu-id="16205-121">Isso ocorreu devido ao uso de um padrão incorreto para acessar o banco de dados ESENT em um cenário com multithread.</span><span class="sxs-lookup"><span data-stu-id="16205-121">This was caused by an incorrect pattern being used to access the ESENT database in a multi-threaded scenario.</span></span> <span data-ttu-id="16205-122">No WMF 5.1, esse problema foi corrigido.</span><span class="sxs-lookup"><span data-stu-id="16205-122">In WMF 5.1, this issue has been fixed.</span></span> <span data-ttu-id="16205-123">Os registros ou relatórios simultâneos (que envolvem o banco de dados ESENT) funcionam bem no WMF 5.1.</span><span class="sxs-lookup"><span data-stu-id="16205-123">Concurrent registrations or reporting (involving ESENT database) works fine in WMF 5.1.</span></span> <span data-ttu-id="16205-124">Esse problema é aplicável somente ao banco de dados ESENT e não se aplica ao banco de dados OLEDB.</span><span class="sxs-lookup"><span data-stu-id="16205-124">This issue is applicable only to the ESENT database and does not apply to the OLEDB database.</span></span>

## <a name="enable-circular-log-on-esent-database-instance"></a><span data-ttu-id="16205-125">Habilitar o log Circular na instância do banco de dados ESENT</span><span class="sxs-lookup"><span data-stu-id="16205-125">Enable Circular log on ESENT database instance</span></span>

<span data-ttu-id="16205-126">Na versão anterior da DSC-PullServer, os arquivos de log do banco de dados ESENT preenchiam o espaço em disco do pullserver porque a instância do banco de dados estava sendo criada sem log circular.</span><span class="sxs-lookup"><span data-stu-id="16205-126">In eariler version of DSC-PullServer, the ESENT database log files were filling up the disk space of the pullserver because the database instance was being created without circular logging.</span></span> <span data-ttu-id="16205-127">Nesta versão, você tem a opção de controlar o comportamento de log circular da instância usando o web.config do pullserver.</span><span class="sxs-lookup"><span data-stu-id="16205-127">In this release, you have the option to control the circular logging behavior of the instance using the web.config of the pullserver.</span></span> <span data-ttu-id="16205-128">Por padrão, o CircularLogging está definido como VERDADEIRO.</span><span class="sxs-lookup"><span data-stu-id="16205-128">By default CircularLogging is set to TRUE.</span></span>

```xml
<appSettings>
    <add key="dbprovider" value="ESENT" />
    <add key="dbconnectionstr" value="C:\Program Files\WindowsPowerShell\DscService\Devices.edb" />
    <add key="CheckpointDepthMaxKB" value="512" />
    <add key="UseCircularESENTLogs" value="TRUE" />
  </appSettings>
```

## <a name="wow64-support-for-configuration-keyword"></a><span data-ttu-id="16205-129">Suporte ao WOW64 para palavra-chave Configuration</span><span class="sxs-lookup"><span data-stu-id="16205-129">WOW64 support for Configuration Keyword</span></span>

<span data-ttu-id="16205-130">Agora há suporte para a palavra-chave `Configuration` no WOW64 em um computador de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="16205-130">The `Configuration` keyword is now supported in WOW64 on a 64-bit computer.</span></span> <span data-ttu-id="16205-131">Isso significa que uma configuração DSC pode ser definida e compilada dentro de um processo de 32 bits como o ISE do Windows PowerShell (x86) executado em um computador de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="16205-131">This means that a DSC configuration can be defined and compiled within a 32-bit process such as Windows PowerShell ISE (x86) running on a 64-bit computer.</span></span>

## <a name="pull-partial-configuration-naming-convention"></a><span data-ttu-id="16205-132">Convenção de nomenclatura de configuração parcial de pull</span><span class="sxs-lookup"><span data-stu-id="16205-132">Pull partial configuration naming convention</span></span>

<span data-ttu-id="16205-133">Na versão anterior, a convenção de nomenclatura para uma configuração parcial era que o nome do arquivo MOF no servidor de pull/serviço deveria ser compatível com o nome de configuração parcial especificado nas configurações do gerenciador de configuração local que, por sua vez, deve ser compatível com o nome de configuração inserido no arquivo MOF.</span><span class="sxs-lookup"><span data-stu-id="16205-133">In the previous release, the naming convention for a partial configuration was that the MOF file name in the pull server/service should match the partial configuration name specified in the local configuration manager settings that in turn must match the configuration name embedded in the MOF file.</span></span>

<span data-ttu-id="16205-134">Confira os instantâneos abaixo:</span><span class="sxs-lookup"><span data-stu-id="16205-134">See the snapshots below:</span></span>

- <span data-ttu-id="16205-135">Definições da configuração local, que determina uma configuração parcial que um nó está autorizado a receber.</span><span class="sxs-lookup"><span data-stu-id="16205-135">Local configuration settings which defines a partial configuration that a node is allowed to receive.</span></span>

  ![Metaconfiguração de exemplo](media/DSC-improvements/MetaConfigPartialOne.png)

- <span data-ttu-id="16205-137">Definição da configuração parcial de exemplo</span><span class="sxs-lookup"><span data-stu-id="16205-137">Sample partial configuration definition</span></span>

  ```powershell
  Configuration PartialOne
  {
      Node('localhost')
      {
          File test
          {
              DestinationPath = "$env:TEMP\partialconfigexample.txt"
              Contents = 'Partial Config Example'
          }
      }
  }
  PartialOne
  ```

- <span data-ttu-id="16205-138">"ConfigurationName" inserido no arquivo MOF gerado.</span><span class="sxs-lookup"><span data-stu-id="16205-138">'ConfigurationName' embedded in the generated MOF file.</span></span>

  ![Arquivo mof de exemplo gerado](media/DSC-improvements/PartialGeneratedMof.png)

- <span data-ttu-id="16205-140">FileName no repositório de configuração de pull</span><span class="sxs-lookup"><span data-stu-id="16205-140">FileName in the pull configuration repository</span></span>

  ![FileName no Repositório de Configuração](media/DSC-improvements/PartialInConfigRepository.png)

  <span data-ttu-id="16205-142">O nome do serviço da Automação do Azure gerou arquivos MOF como `<ConfigurationName>.<NodeName>.mof`.</span><span class="sxs-lookup"><span data-stu-id="16205-142">Azure Automation service name generated MOF files as `<ConfigurationName>.<NodeName>.mof`.</span></span> <span data-ttu-id="16205-143">Portanto, a configuração abaixo é compilada para PartialOne.localhost.mof.</span><span class="sxs-lookup"><span data-stu-id="16205-143">So the configuration below compiles to PartialOne.localhost.mof.</span></span>

  <span data-ttu-id="16205-144">Ela tornou impossível a extração de uma de suas configurações parciais do serviço da Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="16205-144">This made it impossible to pull one of your partial configuration from Azure Automation service.</span></span>

  ```powershell
  Configuration PartialOne
  {
      Node('localhost')
      {
          File test
          {
              DestinationPath = "$env:TEMP\partialconfigexample.txt"
              Contents = 'Partial Config Example'
          }
      }
  }
  PartialOne
  ```

  <span data-ttu-id="16205-145">No WMF 5.1, uma configuração parcial no servidor de pull/serviço pode ser nomeada `<ConfigurationName>.<NodeName>.mof`.</span><span class="sxs-lookup"><span data-stu-id="16205-145">In WMF 5.1, a partial configuration in the pull server/service can be named as `<ConfigurationName>.<NodeName>.mof`.</span></span> <span data-ttu-id="16205-146">Além disso, se um computador estiver extraindo uma única configuração de um servidor de pull/serviço, então, o arquivo de configuração no repositório de configuração do servidor de pull poderá ter qualquer nome de arquivo.</span><span class="sxs-lookup"><span data-stu-id="16205-146">Moreover, if a machine is pulling a single configuration from a pull server/service then the configuration file on the pull server configuration repository can have any file name.</span></span> <span data-ttu-id="16205-147">Esta flexibilidade de nomenclatura permite que você gerencie seus nós parcialmente pelo serviço da Automação do Azure, no qual algumas configurações do nó chegarão da DSC de Automação do Azure e uma configuração parcial gerenciada localmente.</span><span class="sxs-lookup"><span data-stu-id="16205-147">This naming flexibility allows you to manage your nodes partially by Azure Automation service, where some configuration for your node is coming from Azure Automation DSC and with a partial configuration that you manage locally.</span></span>

  <span data-ttu-id="16205-148">A metaconfiguração abaixo configura um nó para ser gerenciado tanto localmente quanto pelo serviço da Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="16205-148">The metaconfiguration below sets up a node to be managed both locally as well as by Azure Automation service.</span></span>

  ```powershell
  [DscLocalConfigurationManager()]
  Configuration RegistrationMetaConfig
  {
      Settings
      {
          RefreshFrequencyMins = 30
          RefreshMode = "PULL"
      }

      ConfigurationRepositoryWeb web
      {
          ServerURL =  $endPoint
          RegistrationKey = $registrationKey
          ConfigurationNames = $configurationName
      }

      # Partial configuration managed by Azure Automation service.
      PartialConfiguration PartialConfigurationManagedByAzureAutomation
      {
          ConfigurationSource = "[ConfigurationRepositoryWeb]Web"
      }

      # This partial configuration is managed locally.
      PartialConfiguration OnPremisesConfig
      {
          RefreshMode = "PUSH"
          ExclusiveResources = @("Script")
      }

  }

  RegistrationMetaConfig
  Set-DscLocalConfigurationManager -Path .\RegistrationMetaConfig -Verbose
  ```

## <a name="using-psdscrunascredential-with-dsc-composite-resources"></a><span data-ttu-id="16205-149">Usando a PsDscRunAsCredential com os recursos de composição da DSC</span><span class="sxs-lookup"><span data-stu-id="16205-149">Using PsDscRunAsCredential with DSC composite resources</span></span>

<span data-ttu-id="16205-150">Adicionamos suporte para usar [PsDscRunAsCredential](/powershell/scripting/dsc/configurations/runAsUser) com os recursos de [Composição](/powershell/scripting/dsc/resources/authoringresourcecomposite) da DSC.</span><span class="sxs-lookup"><span data-stu-id="16205-150">We have added support for using [PsDscRunAsCredential](/powershell/scripting/dsc/configurations/runAsUser) with DSC [Composite](/powershell/scripting/dsc/resources/authoringresourcecomposite) resources.</span></span>

<span data-ttu-id="16205-151">Agora é possível especificar o valor para **PsDscRunAsCredential** ao usar recursos de composição nas configurações.</span><span class="sxs-lookup"><span data-stu-id="16205-151">You can now specify a value for **PsDscRunAsCredential** when using composite resources inside configurations.</span></span> <span data-ttu-id="16205-152">Quando especificado, todos os recursos serão executados em um recurso de composição como um usuário RunAs.</span><span class="sxs-lookup"><span data-stu-id="16205-152">When specified, all resources run inside a composite resource as a RunAs user.</span></span> <span data-ttu-id="16205-153">Se o recurso de composição chamar outro recurso de composição, todos os seus recursos também serão executados como usuário RunAs.</span><span class="sxs-lookup"><span data-stu-id="16205-153">If a composite resource calls another composite resource, all those resources are also executed as RunAs user.</span></span> <span data-ttu-id="16205-154">As credenciais RunAs são propagadas para qualquer nível da hierarquia do recurso de composição.</span><span class="sxs-lookup"><span data-stu-id="16205-154">RunAs credentials are propagated to any level of the composite resource hierarchy.</span></span> <span data-ttu-id="16205-155">Se qualquer recurso dentro de um recurso de composição especificar seu próprio valor para **PsDscRunAsCredential**, ocorrerá um erro de mesclagem durante a compilação da configuração.</span><span class="sxs-lookup"><span data-stu-id="16205-155">If any resource inside a composite resource specifies its own value for **PsDscRunAsCredential**, a merge error results during configuration compilation.</span></span>

<span data-ttu-id="16205-156">Este exemplo mostra o uso com o recurso de composição [WindowsFeatureSet](/powershell/scripting/dsc/reference/resources/windows/windowsfeaturesetresource) incluso no módulo PSDesiredStateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="16205-156">This example shows usage with the [WindowsFeatureSet](/powershell/scripting/dsc/reference/resources/windows/windowsfeaturesetresource) composite resource included in PSDesiredStateConfiguration module.</span></span>

```powershell
Configuration InstallWindowsFeature
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node $AllNodes.NodeName
    {
        WindowsFeatureSet features
        {
            Name = @("Telnet-Client","SNMP-Service")
            Ensure = "Present"
            IncludeAllSubFeature = $true
            PsDscRunAsCredential = Get-Credential
        }
    }
}

$configData = @{
    AllNodes = @(
        @{
            NodeName             = 'localhost'
            PSDscAllowDomainUser = $true
            CertificateFile      = 'C:\publicKeys\targetNode.cer'
            Thumbprint           = '7ee7f09d-4be0-41aa-a47f-96b9e3bdec25'
        }
    )
}

InstallWindowsFeature -ConfigurationData $configData
```

## <a name="allowing-for-identical-duplicate-resources-in-a-configuration"></a><span data-ttu-id="16205-157">Permitindo recursos duplicados idênticos em uma configuração</span><span class="sxs-lookup"><span data-stu-id="16205-157">Allowing for Identical Duplicate Resources in a Configuration</span></span>

<span data-ttu-id="16205-158">O DSC não permite nem manipula definições de recursos conflitantes dentro de uma configuração.</span><span class="sxs-lookup"><span data-stu-id="16205-158">DSC does not allow or handle conflicting resource definitions within a configuration.</span></span> <span data-ttu-id="16205-159">Em vez de tentar resolver o conflito, ele simplesmente falha.</span><span class="sxs-lookup"><span data-stu-id="16205-159">Instead of trying to resolve the conflict, it simply fails.</span></span> <span data-ttu-id="16205-160">Como a reutilização de configuração é cada mais utilizada por meio de recursos de composição, etc., os conflitos ocorrerão com mais frequência.</span><span class="sxs-lookup"><span data-stu-id="16205-160">As configuration reuse becomes more utilized through composite resources, etc. conflicts will occur more often.</span></span> <span data-ttu-id="16205-161">Quando definições de recursos conflitantes forem idênticas, o DSC deverá ter inteligência para permiti-las.</span><span class="sxs-lookup"><span data-stu-id="16205-161">When conflicting resource definitions are identical, DSC should be smart and allow this.</span></span> <span data-ttu-id="16205-162">Com esta versão, damos suporte a várias instâncias de recursos com definições idênticas:</span><span class="sxs-lookup"><span data-stu-id="16205-162">With this release, we support having multiple resource instances that have identical definitions:</span></span>

```powershell
Configuration IIS_FrontEnd
{
    WindowsFeature FE_IIS         #Identical resource
    {
        Ensure = 'Present'
        Name = 'Web-Server'
    }

    WindowsFeature FTP
    {
        Ensure = 'Present'
        Name = 'Web-FTP-Server'
    }
}

Configuration IIS_Worker
{
    WindowsFeature Worker_IIS      #Identical resource
    {
        Ensure = 'Present'
        Name = 'Web-Server'
    }

    WindowsFeature ASP
    {
        Ensure = 'Present'
        Name = 'Web-ASP-Net45'
    }
}

Configuration WebApplication
{
    IIS_Frontend Web {}

    IIS_Worker ASP {}
}
```

<span data-ttu-id="16205-163">Em versões anteriores, o resultado seria uma compilação com falha devido a um conflito entre as instâncias de WindowsFeature FE_IIS e WindowsFeature Worker_IIS tentando garantir que a função “Web-Server” está instalada.</span><span class="sxs-lookup"><span data-stu-id="16205-163">In previous releases, the result would be a failed compilation due to a conflict between the WindowsFeature FE_IIS and WindowsFeature Worker_IIS instances trying to ensure the 'Web-Server' role is installed.</span></span> <span data-ttu-id="16205-164">Observe que *todas* as propriedades que estão sendo configuradas são idênticas nessas duas configurações.</span><span class="sxs-lookup"><span data-stu-id="16205-164">Notice that *all* of the properties that are being configured are identical in these two configurations.</span></span> <span data-ttu-id="16205-165">Uma vez que *todas* as propriedades nesses dois recursos são idênticas, agora isso resultará em uma compilação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="16205-165">Since *all* of the properties in these two resources are identical, this will result in a successful compilation now.</span></span>

<span data-ttu-id="16205-166">Se alguma das propriedades for diferente entre os dois recursos, elas não serão consideradas idênticas e a compilação falhará.</span><span class="sxs-lookup"><span data-stu-id="16205-166">If any of the properties are different between the two resources, they will not be considered identical and compilation will fail.</span></span>

## <a name="dsc-module-and-configuration-signing-validations"></a><span data-ttu-id="16205-167">Validações do módulo de DSC e da assinatura de configuração</span><span class="sxs-lookup"><span data-stu-id="16205-167">DSC module and configuration signing validations</span></span>

<span data-ttu-id="16205-168">Na DSC, as configurações e os módulos são distribuídos para computadores gerenciados do servidor de pull.</span><span class="sxs-lookup"><span data-stu-id="16205-168">In DSC, configurations and modules are distributed to managed computers from the pull server.</span></span> <span data-ttu-id="16205-169">Se o servidor de pull estiver comprometido, um invasor poderá possivelmente alterar as configurações e os módulos no servidor de pull e distribuí-los para todos os nós gerenciados.</span><span class="sxs-lookup"><span data-stu-id="16205-169">If the pull server is compromised, an attacker can potentially modify the configurations and modules on the pull server and have it distributed to all managed nodes.</span></span>

<span data-ttu-id="16205-170">No WMF 5.1, a DSC dá suporte para a validação de assinaturas digitais no catálogo e nos arquivos de configuração (.MOF).</span><span class="sxs-lookup"><span data-stu-id="16205-170">In WMF 5.1, DSC supports validating the digital signatures on catalog and configuration (.MOF) files.</span></span> <span data-ttu-id="16205-171">Este recurso evita que os nós executem as configurações ou os arquivos de módulo que não são assinados por um signatário confiável ou que foram violados depois de assinados por um signatário confiável.</span><span class="sxs-lookup"><span data-stu-id="16205-171">This feature prevents nodes from executing configurations or module files which are not signed by a trusted signer or which have been tampered with after they have been signed by trusted signer.</span></span>

### <a name="how-to-sign-configuration-and-module"></a><span data-ttu-id="16205-172">Como assinar a configuração e o módulo</span><span class="sxs-lookup"><span data-stu-id="16205-172">How to sign configuration and module</span></span>

- <span data-ttu-id="16205-173">Arquivos de Configuração (.MOFs): o cmdlet [Set-AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Set-AuthenticodeSignature) existente do PowerShell é estendido para dar suporte à assinatura de arquivos MOF.</span><span class="sxs-lookup"><span data-stu-id="16205-173">Configuration Files (.MOFs): The existing PowerShell cmdlet [Set-AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Set-AuthenticodeSignature) is extended to support signing of MOF files.</span></span>
- <span data-ttu-id="16205-174">Módulos: a assinatura dos módulos é feita com a assinatura do catálogo do módulo correspondente por meio das seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="16205-174">Modules: Signing of modules is done by signing the corresponding module catalog using the following steps:</span></span>
  1. <span data-ttu-id="16205-175">Crie um arquivo de catálogo: um arquivo de catálogo contém uma coleção de hashes criptográficos ou impressões digitais.</span><span class="sxs-lookup"><span data-stu-id="16205-175">Create a catalog file: A catalog file contains a collection of cryptographic hashes or thumbprints.</span></span> <span data-ttu-id="16205-176">Cada impressão digital corresponde a um arquivo que está incluído no módulo.</span><span class="sxs-lookup"><span data-stu-id="16205-176">Each thumbprint corresponds to a file that is included in the module.</span></span> <span data-ttu-id="16205-177">O novo cmdlet [New-FileCatalog](/powershell/module/microsoft.powershell.security/new-filecatalog) foi adicionado para permitir que os usuários criem um arquivo de catálogo para seu módulo.</span><span class="sxs-lookup"><span data-stu-id="16205-177">The new cmdlet [New-FileCatalog](/powershell/module/microsoft.powershell.security/new-filecatalog), has been added to enable users to create a catalog file for their module.</span></span>
  2. <span data-ttu-id="16205-178">Assine o arquivo de catálogo: use a [Set-AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Set-AuthenticodeSignature) para assinar o arquivo de catálogo.</span><span class="sxs-lookup"><span data-stu-id="16205-178">Sign the catalog file: Use [Set-AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Set-AuthenticodeSignature) to sign the catalog file.</span></span>
  3. <span data-ttu-id="16205-179">Coloque o arquivo de catálogo dentro da pasta do módulo.</span><span class="sxs-lookup"><span data-stu-id="16205-179">Place the catalog file inside the module folder.</span></span> <span data-ttu-id="16205-180">Por convenção, o arquivo de catálogo do módulo deve ser colocado na pasta do módulo, com o mesmo nome do módulo.</span><span class="sxs-lookup"><span data-stu-id="16205-180">By convention, module catalog file should be placed under the module folder with the same name as the module.</span></span>

### <a name="localconfigurationmanager-settings-to-enable-signing-validations"></a><span data-ttu-id="16205-181">Configurações de LocalConfigurationManager para habilitar as validações de assinatura</span><span class="sxs-lookup"><span data-stu-id="16205-181">LocalConfigurationManager settings to enable signing validations</span></span>

#### <a name="pull"></a><span data-ttu-id="16205-182">Recepção</span><span class="sxs-lookup"><span data-stu-id="16205-182">Pull</span></span>

<span data-ttu-id="16205-183">O LocalConfigurationManager de um nó executa a validação da assinatura dos módulos e das configurações com base em suas configurações atuais.</span><span class="sxs-lookup"><span data-stu-id="16205-183">The LocalConfigurationManager of a node performs signing validation of modules and configurations based on its current settings.</span></span> <span data-ttu-id="16205-184">Por padrão, a validação da assinatura está desabilitada.</span><span class="sxs-lookup"><span data-stu-id="16205-184">By default, signature validation is disabled.</span></span> <span data-ttu-id="16205-185">A validação da assinatura pode ser habilitada adicionando o bloco "SignatureValidation" à definição de metaconfiguração do nó, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="16205-185">Signature validation can enabled by adding the 'SignatureValidation' block to the meta-configuration definition of the node as shown below:</span></span>

```powershell
[DSCLocalConfigurationManager()]
Configuration EnableSignatureValidation
{
    Settings
    {
        RefreshMode = 'PULL'
    }

    ConfigurationRepositoryWeb pullserver{
      ConfigurationNames = 'sql'
      ServerURL = 'http://localhost:8080/PSDSCPullServer/PSDSCPullServer.svc'
      AllowUnsecureConnection = $true
      RegistrationKey = 'd6750ff1-d8dd-49f7-8caf-7471ea9793fc' # Replace this with correct registration key.
    }
    SignatureValidation validations{
        # If the TrustedStorePath property is provided then LCM will use the custom path. Otherwise, the LCM will use default trusted store path (Cert:\LocalMachine\DSCStore) to find the signing certificate.
        TrustedStorePath = 'Cert:\LocalMachine\DSCStore'
        SignedItemType = 'Configuration','Module'         # This is a list of DSC artifacts, for which LCM need to verify their digital signature before executing them on the node.
    }

}
EnableSignatureValidation
Set-DscLocalConfigurationManager -Path .\EnableSignatureValidation -Verbose
```

<span data-ttu-id="16205-186">A definição da metaconfiguração acima em um nó habilita a validação da assinatura nas configurações e nos módulos baixados.</span><span class="sxs-lookup"><span data-stu-id="16205-186">Setting the above metaconfiguration on a node enables signature validation on downloaded configurations and modules.</span></span> <span data-ttu-id="16205-187">O Gerenciador de Configurações Local executa as seguintes etapas para verificar as assinaturas digitais.</span><span class="sxs-lookup"><span data-stu-id="16205-187">The Local Configuration Manager performs the following steps to verify the digital signatures.</span></span>

1. <span data-ttu-id="16205-188">Verifique se a assinatura em um arquivo de configuração (.MOF) é válida usando o cmdlet `Get-AuthenticodeSignature`.</span><span class="sxs-lookup"><span data-stu-id="16205-188">Verify the signature on a configuration file (.MOF) is valid using the `Get-AuthenticodeSignature` cmdlet.</span></span>
2. <span data-ttu-id="16205-189">Verifique se a autoridade de certificação que autorizou o signatário é confiável.</span><span class="sxs-lookup"><span data-stu-id="16205-189">Verify the certificate authority that authorized the signer is trusted.</span></span>
3. <span data-ttu-id="16205-190">Baixe as dependências de módulo/recurso da configuração para uma localização temporária.</span><span class="sxs-lookup"><span data-stu-id="16205-190">Download module/resource dependencies of the configuration to a temp location.</span></span>
4. <span data-ttu-id="16205-191">Verifique se a assinatura do catálogo foi incluída dentro do módulo.</span><span class="sxs-lookup"><span data-stu-id="16205-191">Verify the signature of the catalog included inside the module.</span></span>
   - <span data-ttu-id="16205-192">Encontre um arquivo `<moduleName>.cat` e verifique sua assinatura usando `Get-AuthenticodeSignature`.</span><span class="sxs-lookup"><span data-stu-id="16205-192">Find a `<moduleName>.cat` file and verify its signature using `Get-AuthenticodeSignature`.</span></span>
   - <span data-ttu-id="16205-193">Verifique se a autoridade de certificação que autenticou o signatário é confiável.</span><span class="sxs-lookup"><span data-stu-id="16205-193">Verify the certification authority that authenticated the signer is trusted.</span></span>
   - <span data-ttu-id="16205-194">Verifique se o conteúdo dos módulos não foi violado usando o novo cmdlet `Test-FileCatalog`.</span><span class="sxs-lookup"><span data-stu-id="16205-194">Verify the content of the modules has not been tampered using the new cmdlet `Test-FileCatalog`.</span></span>
5. <span data-ttu-id="16205-195">`Install-Module` em `$env:ProgramFiles\WindowsPowerShell\Modules\`</span><span class="sxs-lookup"><span data-stu-id="16205-195">`Install-Module` to `$env:ProgramFiles\WindowsPowerShell\Modules\`</span></span>
6. <span data-ttu-id="16205-196">Configuração do processo</span><span class="sxs-lookup"><span data-stu-id="16205-196">Process configuration</span></span>

> [!NOTE]
> <span data-ttu-id="16205-197">a validação da assinatura no catálogo de módulo e na configuração é realizada somente quando a configuração é aplicada ao sistema pela primeira vez ou quando o módulo é baixado e instalado.</span><span class="sxs-lookup"><span data-stu-id="16205-197">Signature validation on module-catalog and configuration is only performed when the configuration is applied to the system for the first time or when the module is downloaded and installed.</span></span>
> <span data-ttu-id="16205-198">As execuções de consistência não validam a assinatura de Current.mof ou de suas dependências de módulo.</span><span class="sxs-lookup"><span data-stu-id="16205-198">Consistency runs do not validate the signature of Current.mof or its module dependencies.</span></span> <span data-ttu-id="16205-199">Se a verificação tiver falhado em qualquer estágio, por exemplo, se a configuração extraída do servidor de pull não estiver assinada, o processamento da configuração será encerrado com o erro mostrado abaixo e todos os arquivos temporários serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="16205-199">If verification has failed at any stage, for instance, if the configuration pulled from the pull server is unsigned, then processing of the configuration terminates with the error shown below and all temporary files are deleted.</span></span>

![Configuração de Saída de Erro de Exemplo](media/DSC-improvements/PullUnsignedConfigFail.png)

<span data-ttu-id="16205-201">Da mesma forma, a extração de um módulo cujo catálogo não está assinado resulta no seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="16205-201">Similarly, pulling a module whose catalog is not signed results in the following error:</span></span>

![Módulo de Saída de Erro de Exemplo](media/DSC-improvements/PullUnisgnedCatalog.png)

#### <a name="push"></a><span data-ttu-id="16205-203">Push</span><span class="sxs-lookup"><span data-stu-id="16205-203">Push</span></span>

<span data-ttu-id="16205-204">Uma configuração entregue com o uso de push pode ser violada em sua origem antes de ser entregue para o nó.</span><span class="sxs-lookup"><span data-stu-id="16205-204">A configuration delivered by using push might be tampered with at its source before it delivered to the node.</span></span> <span data-ttu-id="16205-205">O Gerenciador de Configurações Local executa etapas semelhantes de validação de assinatura para as configurações enviadas por push ou publicadas.</span><span class="sxs-lookup"><span data-stu-id="16205-205">The Local Configuration Manager performs similar signature validation steps for pushed or published configuration(s).</span></span> <span data-ttu-id="16205-206">Veja abaixo um exemplo completo de validação de assinatura para envio por push.</span><span class="sxs-lookup"><span data-stu-id="16205-206">Below is a complete example of signature validation for push.</span></span>

- <span data-ttu-id="16205-207">Habilite a validação da assinatura no nó.</span><span class="sxs-lookup"><span data-stu-id="16205-207">Enable signature validation on the node.</span></span>

  ```powershell
  [DSCLocalConfigurationManager()]
  Configuration EnableSignatureValidation
  {
      Settings
      {
          RefreshMode = 'PUSH'
      }
      SignatureValidation validations{
          TrustedStorePath = 'Cert:\LocalMachine\DSCStore'
          SignedItemType =  'Configuration','Module'
      }

  }
  EnableSignatureValidation
  Set-DscLocalConfigurationManager -Path .\EnableSignatureValidation -Verbose
  ```

- <span data-ttu-id="16205-208">Crie um arquivo de configuração de exemplo.</span><span class="sxs-lookup"><span data-stu-id="16205-208">Create a sample configuration file.</span></span>

  ```powershell
  # Sample configuration
  Configuration Test
  {

      File foo
      {
          DestinationPath =  "$env:TEMP\signingTest.txt"
          Contents = "ABC"
      }
  }
  Test
  ```

- <span data-ttu-id="16205-209">Tente enviar o arquivo de configuração não assinado por push para o nó.</span><span class="sxs-lookup"><span data-stu-id="16205-209">Try pushing the unsigned configuration file in to the node.</span></span>

  ```powershell
  Start-DscConfiguration -Path .\Test -Wait -Verbose -Force
  ```

  ![ErrorUnsignedMofPushed](media/DSC-improvements/PushUnsignedMof.png)

- <span data-ttu-id="16205-211">Assine o arquivo de configuração usando um certificado de assinatura de código.</span><span class="sxs-lookup"><span data-stu-id="16205-211">Sign the configuration file using code-signing certificate.</span></span>

  ![SignMofFile](media/DSC-improvements/SignMofFile.png)

- <span data-ttu-id="16205-213">Tente enviar o arquivo MOF assinado por push.</span><span class="sxs-lookup"><span data-stu-id="16205-213">Try pushing the signed MOF file.</span></span>

  ![PushSignedMofFile](media/DSC-improvements/PushSignedMof.png)
