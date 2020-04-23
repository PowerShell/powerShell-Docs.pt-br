---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Introdução à Configuração de Estado Desejado (DSC) para Linux
ms.openlocfilehash: b1bc9b9fafd89a1af0f967de38a817bff1f3ffe3
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "73933845"
---
# <a name="get-started-with-desired-state-configuration-dsc-for-linux"></a><span data-ttu-id="cf163-103">Introdução à Configuração de Estado Desejado (DSC) para Linux</span><span class="sxs-lookup"><span data-stu-id="cf163-103">Get started with Desired State Configuration (DSC) for Linux</span></span>

<span data-ttu-id="cf163-104">Este tópico explica como começar a usar a Configuração de Estado Desejado (DSC) do PowerShell para Linux.</span><span class="sxs-lookup"><span data-stu-id="cf163-104">This topic explains how to get started using PowerShell Desired State Configuration (DSC) for Linux.</span></span> <span data-ttu-id="cf163-105">Para obter informações gerais sobre o DSC, consulte [Introdução à Configuração de Estado Desejado do Windows PowerShell](../overview/overview.md).</span><span class="sxs-lookup"><span data-stu-id="cf163-105">For general information about DSC, see [Get Started with Windows PowerShell Desired State Configuration](../overview/overview.md).</span></span>

## <a name="supported-linux-operation-system-versions"></a><span data-ttu-id="cf163-106">Versões do sistema operacional Linux com suporte</span><span class="sxs-lookup"><span data-stu-id="cf163-106">Supported Linux operation system versions</span></span>

<span data-ttu-id="cf163-107">Há suporte para as seguintes versões de sistema operacional do Linux para DSC para Linux.</span><span class="sxs-lookup"><span data-stu-id="cf163-107">The following Linux operating system versions are supported for DSC for Linux.</span></span>

- <span data-ttu-id="cf163-108">CentOS 5, 6 e 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="cf163-108">CentOS 5, 6, and 7 (x86/x64)</span></span>
- <span data-ttu-id="cf163-109">Debian GNU/Linux 6, 7 e 8 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="cf163-109">Debian GNU/Linux 6, 7 and 8 (x86/x64)</span></span>
- <span data-ttu-id="cf163-110">Oracle Linux 5, 6 e 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="cf163-110">Oracle Linux 5, 6 and 7 (x86/x64)</span></span>
- <span data-ttu-id="cf163-111">Red Hat Enterprise Linux Server 5, 6 e 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="cf163-111">Red Hat Enterprise Linux Server 5, 6 and 7 (x86/x64)</span></span>
- <span data-ttu-id="cf163-112">SUSE Linux Enterprise Server 10, 11 e 12 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="cf163-112">SUSE Linux Enterprise Server 10, 11 and 12 (x86/x64)</span></span>
- <span data-ttu-id="cf163-113">Ubuntu Server 12.04 LTS, 14.04 LTS e 16.04 LTS (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="cf163-113">Ubuntu Server 12.04 LTS, 14.04 LTS and 16.04 LTS (x86/x64)</span></span>

<span data-ttu-id="cf163-114">A tabela a seguir descreve as dependências de pacote necessárias para a DSC para Linux.</span><span class="sxs-lookup"><span data-stu-id="cf163-114">The following table describes the required package dependencies for DSC for Linux.</span></span>

|  <span data-ttu-id="cf163-115">Pacote necessário</span><span class="sxs-lookup"><span data-stu-id="cf163-115">Required package</span></span> |  <span data-ttu-id="cf163-116">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="cf163-116">Description</span></span> |  <span data-ttu-id="cf163-117">Versão mínima</span><span class="sxs-lookup"><span data-stu-id="cf163-117">Minimum version</span></span> |
|---|---|---|
| <span data-ttu-id="cf163-118">glibc</span><span class="sxs-lookup"><span data-stu-id="cf163-118">glibc</span></span>| <span data-ttu-id="cf163-119">Biblioteca do GNU</span><span class="sxs-lookup"><span data-stu-id="cf163-119">GNU Library</span></span>| <span data-ttu-id="cf163-120">2…4 – 31.30</span><span class="sxs-lookup"><span data-stu-id="cf163-120">2…4 – 31.30</span></span>|
| <span data-ttu-id="cf163-121">python</span><span class="sxs-lookup"><span data-stu-id="cf163-121">python</span></span>| <span data-ttu-id="cf163-122">Python</span><span class="sxs-lookup"><span data-stu-id="cf163-122">Python</span></span>| <span data-ttu-id="cf163-123">2.4 – 3.4</span><span class="sxs-lookup"><span data-stu-id="cf163-123">2.4 – 3.4</span></span>|
| <span data-ttu-id="cf163-124">omiserver</span><span class="sxs-lookup"><span data-stu-id="cf163-124">omiserver</span></span>| <span data-ttu-id="cf163-125">Infraestrutura de gerenciamento aberta</span><span class="sxs-lookup"><span data-stu-id="cf163-125">Open Management Infrastructure</span></span>| <span data-ttu-id="cf163-126">1.0.8.1</span><span class="sxs-lookup"><span data-stu-id="cf163-126">1.0.8.1</span></span>|
| <span data-ttu-id="cf163-127">openssl</span><span class="sxs-lookup"><span data-stu-id="cf163-127">openssl</span></span>| <span data-ttu-id="cf163-128">Bibliotecas OpenSSL</span><span class="sxs-lookup"><span data-stu-id="cf163-128">OpenSSL Libraries</span></span>| <span data-ttu-id="cf163-129">0.9.8 ou 1.0</span><span class="sxs-lookup"><span data-stu-id="cf163-129">0.9.8 or 1.0</span></span>|
| <span data-ttu-id="cf163-130">ctypes</span><span class="sxs-lookup"><span data-stu-id="cf163-130">ctypes</span></span>| <span data-ttu-id="cf163-131">Biblioteca do Python CTypes</span><span class="sxs-lookup"><span data-stu-id="cf163-131">Python CTypes library</span></span>| <span data-ttu-id="cf163-132">Deve coincidir com a versão do Python</span><span class="sxs-lookup"><span data-stu-id="cf163-132">Must match Python version</span></span>|
| <span data-ttu-id="cf163-133">libcurl</span><span class="sxs-lookup"><span data-stu-id="cf163-133">libcurl</span></span>| <span data-ttu-id="cf163-134">biblioteca de cliente http do cURL</span><span class="sxs-lookup"><span data-stu-id="cf163-134">cURL http client library</span></span>| <span data-ttu-id="cf163-135">7.15.1</span><span class="sxs-lookup"><span data-stu-id="cf163-135">7.15.1</span></span>|

## <a name="installing-dsc-for-linux"></a><span data-ttu-id="cf163-136">Instalando a DSC para Linux</span><span class="sxs-lookup"><span data-stu-id="cf163-136">Installing DSC for Linux</span></span>

<span data-ttu-id="cf163-137">É necessário instalar a [Infraestrutura de Gerenciamento Aberta (OMI)](https://github.com/Microsoft/omi) antes de instalar a DSC para Linux.</span><span class="sxs-lookup"><span data-stu-id="cf163-137">You must install the [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi) before installing DSC for Linux.</span></span>

### <a name="installing-omi"></a><span data-ttu-id="cf163-138">Instalando a OMI</span><span class="sxs-lookup"><span data-stu-id="cf163-138">Installing OMI</span></span>

<span data-ttu-id="cf163-139">A Desired State Configuration para Linux requer o servidor CIM da OMI (Infraestrutura de Gerenciamento Aberta), versão 1.0.8.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="cf163-139">Desired State Configuration for Linux requires the Open Management Infrastructure (OMI) CIM server, version 1.0.8.1 or later.</span></span> <span data-ttu-id="cf163-140">A OMI pode ser baixada do The Open Group: [Infraestrutura de Gerenciamento Aberta (OMI)](https://github.com/Microsoft/omi).</span><span class="sxs-lookup"><span data-stu-id="cf163-140">OMI can be downloaded from The Open Group: [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi).</span></span>

<span data-ttu-id="cf163-141">Para instalar a OMI, instale o pacote adequado para seu sistema Linux (.rpm ou .deb), a versão do OpenSSL (ssl_098 ou ssl_100) e a arquitetura (x64/x86).</span><span class="sxs-lookup"><span data-stu-id="cf163-141">To install OMI, install the package that is appropriate for your Linux system (.rpm or .deb) and OpenSSL version (ssl_098 or ssl_100), and architecture (x64/x86).</span></span> <span data-ttu-id="cf163-142">Pacotes de RPM são adequados para CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server e Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="cf163-142">RPM packages are appropriate for CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, and Oracle Linux.</span></span> <span data-ttu-id="cf163-143">Pacotes de DEB são adequados para Debian GNU/Linux e Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="cf163-143">DEB packages are appropriate for Debian GNU/Linux and Ubuntu Server.</span></span> <span data-ttu-id="cf163-144">Os pacotes ssl_098 são adequados para computadores com OpenSSL 0.9.8 instalado, enquanto os pacotes ssl_100 são adequados para computadores com OpenSSL 1.0 instalado.</span><span class="sxs-lookup"><span data-stu-id="cf163-144">The ssl_098 packages are appropriate for computers with OpenSSL 0.9.8 installed while the ssl_100 packages are appropriate for computers with OpenSSL 1.0 installed.</span></span>

> [!NOTE]
> <span data-ttu-id="cf163-145">Para determinar a versão instalada do OpenSSL, execute o comando `openssl version`.</span><span class="sxs-lookup"><span data-stu-id="cf163-145">To determine the installed OpenSSL version, run the command `openssl version`.</span></span>

<span data-ttu-id="cf163-146">Execute o seguinte comando para instalar a OMI em um sistema CentOS 7 x64.</span><span class="sxs-lookup"><span data-stu-id="cf163-146">Run the following command to install OMI on a CentOS 7 x64 system.</span></span>

`# sudo rpm -Uvh omiserver-1.0.8.ssl_100.rpm`

### <a name="installing-dsc"></a><span data-ttu-id="cf163-147">Instalando a DSC</span><span class="sxs-lookup"><span data-stu-id="cf163-147">Installing DSC</span></span>

<span data-ttu-id="cf163-148">DSC para Linux está disponível para download [aqui](https://github.com/Microsoft/PowerShell-DSC-for-Linux/releases/tag/v1.1.1-294).</span><span class="sxs-lookup"><span data-stu-id="cf163-148">DSC for Linux is available for download [here](https://github.com/Microsoft/PowerShell-DSC-for-Linux/releases/tag/v1.1.1-294).</span></span>

<span data-ttu-id="cf163-149">Para instalar a DSC, instale o pacote adequado para seu sistema Linux (.rpm ou .deb), a versão do OpenSSL (ssl_098 ou ssl_100) e a arquitetura (x64/x86).</span><span class="sxs-lookup"><span data-stu-id="cf163-149">To install DSC, install the package that is appropriate for your Linux system (.rpm or .deb) and OpenSSL version (ssl_098 or ssl_100), and architecture (x64/x86).</span></span> <span data-ttu-id="cf163-150">Pacotes de RPM são adequados para CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server e Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="cf163-150">RPM packages are appropriate for CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, and Oracle Linux.</span></span> <span data-ttu-id="cf163-151">Pacotes de DEB são adequados para Debian GNU/Linux e Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="cf163-151">DEB packages are appropriate for Debian GNU/Linux and Ubuntu Server.</span></span> <span data-ttu-id="cf163-152">Os pacotes ssl_098 são adequados para computadores com OpenSSL 0.9.8 instalado, enquanto os pacotes ssl_100 são adequados para computadores com OpenSSL 1.0 instalado.</span><span class="sxs-lookup"><span data-stu-id="cf163-152">The ssl_098 packages are appropriate for computers with OpenSSL 0.9.8 installed while the ssl_100 packages are appropriate for computers with OpenSSL 1.0 installed.</span></span>

> [!NOTE]
> <span data-ttu-id="cf163-153">Para determinar a versão instalada do OpenSSL, execute a versão do comando openssl.</span><span class="sxs-lookup"><span data-stu-id="cf163-153">To determine the installed OpenSSL version, run the command openssl version.</span></span>

<span data-ttu-id="cf163-154">Execute o seguinte comando para instalar a DSC em um sistema CentOS 7 x64.</span><span class="sxs-lookup"><span data-stu-id="cf163-154">Run the following command to install DSC on a CentOS 7 x64 system.</span></span>

`# sudo rpm -Uvh dsc-1.0.0-254.ssl_100.x64.rpm`

## <a name="using-dsc-for-linux"></a><span data-ttu-id="cf163-155">Usando a DSC para Linux</span><span class="sxs-lookup"><span data-stu-id="cf163-155">Using DSC for Linux</span></span>

<span data-ttu-id="cf163-156">As seções a seguir explicam como criar e executar configurações DSC em computadores Linux.</span><span class="sxs-lookup"><span data-stu-id="cf163-156">The following sections explain how to create and run DSC configurations on Linux computers.</span></span>

### <a name="creating-a-configuration-mof-document"></a><span data-ttu-id="cf163-157">Criando um documento MOF de configuração</span><span class="sxs-lookup"><span data-stu-id="cf163-157">Creating a configuration MOF document</span></span>

<span data-ttu-id="cf163-158">A palavra-chave Configuration do Windows PowerShell é usada para criar uma configuração para computadores Linux, assim como para computadores Windows.</span><span class="sxs-lookup"><span data-stu-id="cf163-158">The Windows PowerShell Configuration keyword is used to create a configuration for Linux computers, just like for Windows computers.</span></span> <span data-ttu-id="cf163-159">As etapas a seguir descrevem a criação de um documento de configuração para um computador Linux usando o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cf163-159">The following steps describe the creation of a configuration document for a Linux computer using Windows PowerShell.</span></span>

1. <span data-ttu-id="cf163-160">Importe o módulo nx.</span><span class="sxs-lookup"><span data-stu-id="cf163-160">Import the nx module.</span></span> <span data-ttu-id="cf163-161">O módulo nx do Windows PowerShell contém o esquema para recursos internos para DSC para Linux e deve ser instalado no seu computador local e importado na configuração.</span><span class="sxs-lookup"><span data-stu-id="cf163-161">The nx Windows PowerShell module contains the schema for Built-In resources for DSC for Linux, and must be installed to your local computer and imported in the configuration.</span></span>

   - <span data-ttu-id="cf163-162">Para instalar o módulo nx, copie o diretório do módulo nx para `$env:USERPROFILE\Documents\WindowsPowerShell\Modules\` ou `$PSHOME\Modules`.</span><span class="sxs-lookup"><span data-stu-id="cf163-162">To install the nx module, copy the nx module directory to either `$env:USERPROFILE\Documents\WindowsPowerShell\Modules\` or `$PSHOME\Modules`.</span></span> <span data-ttu-id="cf163-163">O módulo nx está incluído no pacote de instalação da DSC para Linux.</span><span class="sxs-lookup"><span data-stu-id="cf163-163">The nx module is included in the DSC for Linux installation package.</span></span> <span data-ttu-id="cf163-164">Para importar o módulo nx na sua configuração, use o comando `Import-DSCResource`:</span><span class="sxs-lookup"><span data-stu-id="cf163-164">To import the nx module in your configuration, use the `Import-DSCResource` command:</span></span>

   ```powershell
   Configuration ExampleConfiguration{

    Import-DSCResource -Module nx

   }
   ```

2. <span data-ttu-id="cf163-165">Definir uma configuração e gerar o documento de configuração:</span><span class="sxs-lookup"><span data-stu-id="cf163-165">Define a configuration and generate the configuration document:</span></span>

   ```powershell
   Configuration ExampleConfiguration
   {
        Import-DscResource -Module nx

        Node  "linuxhost.contoso.com"
        {
            nxFile ExampleFile 
            {
                DestinationPath = "/tmp/example"
                Contents = "hello world `n"
                Ensure = "Present"
                Type = "File"
            }
        }
   }

   ExampleConfiguration -OutputPath:"C:\temp"
   ```

### <a name="push-the-configuration-to-the-linux-computer"></a><span data-ttu-id="cf163-166">Envie a configuração por push para o computador Linux</span><span class="sxs-lookup"><span data-stu-id="cf163-166">Push the configuration to the Linux computer</span></span>

<span data-ttu-id="cf163-167">Documentos de configuração (arquivos MOF) podem ser enviados por push para o computador Linux usando o cmdlet [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration).</span><span class="sxs-lookup"><span data-stu-id="cf163-167">Configuration documents (MOF files) can be pushed to the Linux computer using the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet.</span></span> <span data-ttu-id="cf163-168">Para usar esse cmdlet, juntamente com os cmdlets [Get-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration) ou [Test-DscConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration), remotamente em um computador Linux, você deve utilizar uma CIMSession.</span><span class="sxs-lookup"><span data-stu-id="cf163-168">In order to use this cmdlet, along with the [Get-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration), or [Test-DscConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration) cmdlets, remotely to a Linux computer, you must use a CIMSession.</span></span> <span data-ttu-id="cf163-169">O cmdlet [New-CimSession](/powershell/module/CimCmdlets/New-CimSession) é usado para criar uma CIMSession para o computador Linux.</span><span class="sxs-lookup"><span data-stu-id="cf163-169">The [New-CimSession](/powershell/module/CimCmdlets/New-CimSession) cmdlet is used to create a CIMSession to the Linux computer.</span></span>

<span data-ttu-id="cf163-170">O código a seguir mostra como criar uma CIMSession para DSC para Linux.</span><span class="sxs-lookup"><span data-stu-id="cf163-170">The following code shows how to create a CIMSession for DSC for Linux.</span></span>

```powershell
$Node = "ostc-dsc-01"
$Credential = Get-Credential -UserName "root" -Message "Enter Password:"

#Ignore SSL certificate validation
#$opt = New-CimSessionOption -UseSsl $true -SkipCACheck $true -SkipCNCheck $true -SkipRevocationCheck $true

#Options for a trusted SSL certificate
$opt = New-CimSessionOption -UseSsl $true
$Sess=New-CimSession -Credential $credential -ComputerName $Node -Port 5986 -Authentication basic -SessionOption $opt -OperationTimeoutSec 90
```

> [!NOTE]
> <span data-ttu-id="cf163-171">No modo de "Push", a credencial do usuário precisa ser o usuário raiz no computador Linux.</span><span class="sxs-lookup"><span data-stu-id="cf163-171">For "Push" mode, the user credential must be the root user on the Linux computer.</span></span>
> <span data-ttu-id="cf163-172">Há suporte apenas para conexões SSL/TLS para DSC para Linux; a `New-CimSession` precisa ser usada com o parâmetro –UseSSL definido como $true.</span><span class="sxs-lookup"><span data-stu-id="cf163-172">Only SSL/TLS connections are supported for DSC for Linux, the `New-CimSession` must be used with the –UseSSL parameter set to $true.</span></span>
> <span data-ttu-id="cf163-173">O certificado SSL usado pela OMI (para DSC) é especificado no arquivo: `/etc/opt/omi/conf/omiserver.conf` com as propriedades: pemfile e keyfile.</span><span class="sxs-lookup"><span data-stu-id="cf163-173">The SSL certificate used by OMI (for DSC) is specified in the file: `/etc/opt/omi/conf/omiserver.conf` with the properties: pemfile and keyfile.</span></span>
> <span data-ttu-id="cf163-174">Se o computador Windows em que você está executando o cmdlet [New-CimSession](/powershell/module/CimCmdlets/New-CimSession) não confiar nesse certificado, será possível optar por ignorar a validação do certificado com as Opções de CIMSession: `-SkipCACheck $true -SkipCNCheck $true -SkipRevocationCheck $true`</span><span class="sxs-lookup"><span data-stu-id="cf163-174">If this certificate is not trusted by the Windows computer that you are running the [New-CimSession](/powershell/module/CimCmdlets/New-CimSession) cmdlet on, you can choose to ignore certificate validation with the CIMSession Options: `-SkipCACheck $true -SkipCNCheck $true -SkipRevocationCheck $true`</span></span>

<span data-ttu-id="cf163-175">Execute o seguinte comando para enviar a configuração DSC por push para o nó do Linux.</span><span class="sxs-lookup"><span data-stu-id="cf163-175">Run the following command to push the DSC configuration to the Linux node.</span></span>

`Start-DscConfiguration -Path:"C:\temp" -CimSession $Sess -Wait -Verbose`

### <a name="distribute-the-configuration-with-a-pull-server"></a><span data-ttu-id="cf163-176">Distribuir a configuração com um servidor de pull</span><span class="sxs-lookup"><span data-stu-id="cf163-176">Distribute the configuration with a pull server</span></span>

<span data-ttu-id="cf163-177">As configurações podem ser distribuídas para um computador Linux com um servidor de pull, assim como para computadores Windows.</span><span class="sxs-lookup"><span data-stu-id="cf163-177">Configurations can be distributed to a Linux computer with a pull server, just like for Windows computers.</span></span> <span data-ttu-id="cf163-178">Para obter orientações sobre como usar um servidor de pull, consulte [Servidores de Pull de Configuração de Estado Desejado do Windows PowerShell](../pull-server/pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="cf163-178">For guidance on using a pull server, see [Windows PowerShell Desired State Configuration Pull Servers](../pull-server/pullServer.md).</span></span> <span data-ttu-id="cf163-179">Para obter informações adicionais e se informar sobre as limitações relacionadas ao uso de computadores Linux com um servidor pull, consulte as Notas de versão para a configuração de estado desejado para Linux.</span><span class="sxs-lookup"><span data-stu-id="cf163-179">For additional information and limitations related to using Linux computers with a pull server, see the Release Notes for Desired State Configuration for Linux.</span></span>

### <a name="working-with-configurations-locally"></a><span data-ttu-id="cf163-180">Trabalhando com configurações localmente</span><span class="sxs-lookup"><span data-stu-id="cf163-180">Working with configurations locally</span></span>

<span data-ttu-id="cf163-181">A DSC para Linux inclui scripts para trabalhar com a configuração no computador Linux local.</span><span class="sxs-lookup"><span data-stu-id="cf163-181">DSC for Linux includes scripts to work with configuration from the local Linux computer.</span></span> <span data-ttu-id="cf163-182">Esses scripts estão localizados em `/opt/microsoft/dsc/Scripts` e incluem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="cf163-182">These scripts are locate in `/opt/microsoft/dsc/Scripts` and include the following:</span></span>

- <span data-ttu-id="cf163-183">GetDscConfiguration.py</span><span class="sxs-lookup"><span data-stu-id="cf163-183">GetDscConfiguration.py</span></span>

<span data-ttu-id="cf163-184">Gera a configuração atual aplicada ao computador.</span><span class="sxs-lookup"><span data-stu-id="cf163-184">Returns the current configuration applied to the computer.</span></span> <span data-ttu-id="cf163-185">Semelhante ao cmdlet `Get-DscConfiguration` do cmdlet do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cf163-185">Similar to the Windows PowerShell cmdlet `Get-DscConfiguration` cmdlet.</span></span>

`# sudo ./GetDscConfiguration.py`

- <span data-ttu-id="cf163-186">GetDscLocalConfigurationManager.py</span><span class="sxs-lookup"><span data-stu-id="cf163-186">GetDscLocalConfigurationManager.py</span></span>

<span data-ttu-id="cf163-187">Gera a metaconfiguração atual aplicada ao computador.</span><span class="sxs-lookup"><span data-stu-id="cf163-187">Returns the current meta-configuration applied to the computer.</span></span> <span data-ttu-id="cf163-188">Semelhante ao cmdlet [Get-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager).</span><span class="sxs-lookup"><span data-stu-id="cf163-188">Similar to the cmdlet [Get-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) cmdlet.</span></span>

`# sudo ./GetDscLocalConfigurationManager.py`

- <span data-ttu-id="cf163-189">InstallModule.py</span><span class="sxs-lookup"><span data-stu-id="cf163-189">InstallModule.py</span></span>

<span data-ttu-id="cf163-190">Instala um módulo personalizado de recurso de DSC.</span><span class="sxs-lookup"><span data-stu-id="cf163-190">Installs a custom DSC resource module.</span></span> <span data-ttu-id="cf163-191">Requer o caminho para um arquivo. zip que contém a biblioteca de objeto compartilhado do módulo e os arquivos MOF do esquema.</span><span class="sxs-lookup"><span data-stu-id="cf163-191">Requires the path to a .zip file containing the module shared object library and schema MOF files.</span></span>

`# sudo ./InstallModule.py /tmp/cnx_Resource.zip`

- <span data-ttu-id="cf163-192">RemoveModule.py</span><span class="sxs-lookup"><span data-stu-id="cf163-192">RemoveModule.py</span></span>

<span data-ttu-id="cf163-193">Remove um módulo personalizado de recurso de DSC.</span><span class="sxs-lookup"><span data-stu-id="cf163-193">Removes a custom DSC resource module.</span></span> <span data-ttu-id="cf163-194">Requer o nome do módulo que será removido.</span><span class="sxs-lookup"><span data-stu-id="cf163-194">Requires the name of the module to remove.</span></span>

`# sudo ./RemoveModule.py cnx_Resource`

- <span data-ttu-id="cf163-195">StartDscLocalConfigurationManager.py</span><span class="sxs-lookup"><span data-stu-id="cf163-195">StartDscLocalConfigurationManager.py</span></span>

<span data-ttu-id="cf163-196">Aplica um arquivo MOF de configuração ao computador.</span><span class="sxs-lookup"><span data-stu-id="cf163-196">Applies a configuration MOF file to the computer.</span></span> <span data-ttu-id="cf163-197">Semelhante ao cmdlet [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration).</span><span class="sxs-lookup"><span data-stu-id="cf163-197">Similar to the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet.</span></span> <span data-ttu-id="cf163-198">Exige o caminho até o MOF de configuração para aplicar.</span><span class="sxs-lookup"><span data-stu-id="cf163-198">Requires the path to the configuration MOF to apply.</span></span>

`# sudo ./StartDscLocalConfigurationManager.py –configurationmof /tmp/localhost.mof`

- <span data-ttu-id="cf163-199">SetDscLocalConfigurationManager.py</span><span class="sxs-lookup"><span data-stu-id="cf163-199">SetDscLocalConfigurationManager.py</span></span>

<span data-ttu-id="cf163-200">Aplica um arquivo MOF de metaconfiguração ao computador.</span><span class="sxs-lookup"><span data-stu-id="cf163-200">Applies a Meta Configuration MOF file to the computer.</span></span> <span data-ttu-id="cf163-201">Semelhante ao cmdlet [Set-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager).</span><span class="sxs-lookup"><span data-stu-id="cf163-201">Similar to the [Set-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager) cmdlet.</span></span> <span data-ttu-id="cf163-202">Exige o caminho até o MOF de metaconfiguração para aplicar.</span><span class="sxs-lookup"><span data-stu-id="cf163-202">Requires the path to the Meta Configuration MOF to apply.</span></span>

`# sudo ./SetDscLocalConfigurationManager.py –configurationmof /tmp/localhost.meta.mof`

## <a name="powershell-desired-state-configuration-for-linux-log-files"></a><span data-ttu-id="cf163-203">Arquivos de Log da Configuração de Estado Desejado do PowerShell para Linux</span><span class="sxs-lookup"><span data-stu-id="cf163-203">PowerShell Desired State Configuration for Linux Log Files</span></span>

<span data-ttu-id="cf163-204">Os seguintes arquivos de log são gerados para mensagens da DSC para Linux.</span><span class="sxs-lookup"><span data-stu-id="cf163-204">The following log files are generated for DSC for Linux messages.</span></span>

|<span data-ttu-id="cf163-205">Arquivo de log</span><span class="sxs-lookup"><span data-stu-id="cf163-205">Log file</span></span>|<span data-ttu-id="cf163-206">Diretório</span><span class="sxs-lookup"><span data-stu-id="cf163-206">Directory</span></span>|<span data-ttu-id="cf163-207">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="cf163-207">Description</span></span>|
|---|---|---|
|<span data-ttu-id="cf163-208">**omiserver.log**</span><span class="sxs-lookup"><span data-stu-id="cf163-208">**omiserver.log**</span></span>|`/var/opt/omi/log`|<span data-ttu-id="cf163-209">Mensagens relacionadas à operação do servidor CIM da OMI.</span><span class="sxs-lookup"><span data-stu-id="cf163-209">Messages relating to the operation of the OMI CIM server.</span></span>|
|<span data-ttu-id="cf163-210">**dsc.log**</span><span class="sxs-lookup"><span data-stu-id="cf163-210">**dsc.log**</span></span>|`/var/opt/omi/log`|<span data-ttu-id="cf163-211">Mensagens relacionadas à operação das operações de recurso do Gerenciador de Configurações Local (LCM) e da DSC.</span><span class="sxs-lookup"><span data-stu-id="cf163-211">Messages relating to the operation of the Local Configuration Manager (LCM) and DSC resource operations.</span></span>|
