---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Introdução à Configuração de Estado Desejado (DSC) para Linux
ms.openlocfilehash: b1bc9b9fafd89a1af0f967de38a817bff1f3ffe3
ms.sourcegitcommit: 14b50e5446f69729f72231f5dc6f536cdd1084c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2019
ms.locfileid: "73933845"
---
# <a name="get-started-with-desired-state-configuration-dsc-for-linux"></a>Introdução à Configuração de Estado Desejado (DSC) para Linux

Este tópico explica como começar a usar a Configuração de Estado Desejado (DSC) do PowerShell para Linux. Para obter informações gerais sobre o DSC, consulte [Introdução à Configuração de Estado Desejado do Windows PowerShell](../overview/overview.md).

## <a name="supported-linux-operation-system-versions"></a>Versões do sistema operacional Linux com suporte

Há suporte para as seguintes versões de sistema operacional do Linux para DSC para Linux.

- CentOS 5, 6 e 7 (x86/x64)
- Debian GNU/Linux 6, 7 e 8 (x86/x64)
- Oracle Linux 5, 6 e 7 (x86/x64)
- Red Hat Enterprise Linux Server 5, 6 e 7 (x86/x64)
- SUSE Linux Enterprise Server 10, 11 e 12 (x86/x64)
- Ubuntu Server 12.04 LTS, 14.04 LTS e 16.04 LTS (x86/x64)

A tabela a seguir descreve as dependências de pacote necessárias para a DSC para Linux.

|  Pacote necessário |  Descrição |  Versão mínima |
|---|---|---|
| glibc| Biblioteca do GNU| 2…4 – 31.30|
| python| Python| 2.4 – 3.4|
| omiserver| Infraestrutura de gerenciamento aberta| 1.0.8.1|
| openssl| Bibliotecas do OpenSSL| 0.9.8 ou 1.0|
| ctypes| Biblioteca do Python CTypes| Deve coincidir com a versão do Python|
| libcurl| biblioteca de cliente http do cURL| 7.15.1|

## <a name="installing-dsc-for-linux"></a>Instalando a DSC para Linux

É necessário instalar a [Infraestrutura de Gerenciamento Aberta (OMI)](https://github.com/Microsoft/omi) antes de instalar a DSC para Linux.

### <a name="installing-omi"></a>Instalando a OMI

A Desired State Configuration para Linux requer o servidor CIM da OMI (Infraestrutura de Gerenciamento Aberta), versão 1.0.8.1 ou posterior. A OMI pode ser baixada do The Open Group: [OMI (Infraestrutura de gerenciamento aberta)](https://github.com/Microsoft/omi).

Para instalar a OMI, instale o pacote adequado para seu sistema Linux (.rpm ou .deb), a versão do OpenSSL (ssl_098 ou ssl_100) e a arquitetura (x64/x86). Pacotes de RPM são adequados para CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server e Oracle Linux. Pacotes de DEB são adequados para Debian GNU/Linux e Ubuntu Server. Os pacotes ssl_098 são adequados para computadores com OpenSSL 0.9.8 instalado, enquanto os pacotes ssl_100 são adequados para computadores com OpenSSL 1.0 instalado.

> [!NOTE]
> Para determinar a versão instalada do OpenSSL, execute o comando `openssl version`.

Execute o seguinte comando para instalar a OMI em um sistema CentOS 7 x64.

`# sudo rpm -Uvh omiserver-1.0.8.ssl_100.rpm`

### <a name="installing-dsc"></a>Instalando a DSC

DSC para Linux está disponível para download [aqui](https://github.com/Microsoft/PowerShell-DSC-for-Linux/releases/tag/v1.1.1-294).

Para instalar a DSC, instale o pacote adequado para seu sistema Linux (.rpm ou .deb), a versão do OpenSSL (ssl_098 ou ssl_100) e a arquitetura (x64/x86). Pacotes de RPM são adequados para CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server e Oracle Linux. Pacotes de DEB são adequados para Debian GNU/Linux e Ubuntu Server. Os pacotes ssl_098 são adequados para computadores com OpenSSL 0.9.8 instalado, enquanto os pacotes ssl_100 são adequados para computadores com OpenSSL 1.0 instalado.

> [!NOTE]
> Para determinar a versão instalada do OpenSSL, execute a versão do comando openssl.

Execute o seguinte comando para instalar a DSC em um sistema CentOS 7 x64.

`# sudo rpm -Uvh dsc-1.0.0-254.ssl_100.x64.rpm`

## <a name="using-dsc-for-linux"></a>Usando a DSC para Linux

As seções a seguir explicam como criar e executar configurações DSC em computadores Linux.

### <a name="creating-a-configuration-mof-document"></a>Criando um documento MOF de configuração

A palavra-chave Configuration do Windows PowerShell é usada para criar uma configuração para computadores Linux, assim como para computadores Windows. As etapas a seguir descrevem a criação de um documento de configuração para um computador Linux usando o Windows PowerShell.

1. Importe o módulo nx. O módulo nx do Windows PowerShell contém o esquema para recursos internos para DSC para Linux e deve ser instalado no seu computador local e importado na configuração.

   - Para instalar o módulo nx, copie o diretório do módulo nx para `$env:USERPROFILE\Documents\WindowsPowerShell\Modules\` ou `$PSHOME\Modules`. O módulo nx está incluído no pacote de instalação da DSC para Linux. Para importar o módulo nx na sua configuração, use o comando `Import-DSCResource`:

   ```powershell
   Configuration ExampleConfiguration{

    Import-DSCResource -Module nx

   }
   ```

2. Definir uma configuração e gerar o documento de configuração:

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

### <a name="push-the-configuration-to-the-linux-computer"></a>Envie a configuração por push para o computador Linux

Documentos de configuração (arquivos MOF) podem ser enviados por push para o computador Linux usando o cmdlet [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration). Para usar esse cmdlet, juntamente com os cmdlets [Get-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration) ou [Test-DscConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration), remotamente em um computador Linux, você deve utilizar uma CIMSession. O cmdlet [New-CimSession](/powershell/module/CimCmdlets/New-CimSession) é usado para criar uma CIMSession para o computador Linux.

O código a seguir mostra como criar uma CIMSession para DSC para Linux.

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
> No modo de "Push", a credencial do usuário precisa ser o usuário raiz no computador Linux.
> Há suporte apenas para conexões SSL/TLS para DSC para Linux; a `New-CimSession` precisa ser usada com o parâmetro –UseSSL definido como $true.
> O certificado SSL usado pela OMI (para DSC) é especificado no arquivo: `/etc/opt/omi/conf/omiserver.conf` com as propriedades: pemfile e keyfile.
> Se o computador Windows em que você está executando o cmdlet [New-CimSession](/powershell/module/CimCmdlets/New-CimSession) não confiar nesse certificado, será possível optar por ignorar a validação do certificado com as Opções de CIMSession: `-SkipCACheck $true -SkipCNCheck $true -SkipRevocationCheck $true`

Execute o seguinte comando para enviar a configuração DSC por push para o nó do Linux.

`Start-DscConfiguration -Path:"C:\temp" -CimSession $Sess -Wait -Verbose`

### <a name="distribute-the-configuration-with-a-pull-server"></a>Distribuir a configuração com um servidor de pull

As configurações podem ser distribuídas para um computador Linux com um servidor de pull, assim como para computadores Windows. Para obter orientações sobre como usar um servidor de pull, consulte [Servidores de Pull de Configuração de Estado Desejado do Windows PowerShell](../pull-server/pullServer.md). Para obter informações adicionais e se informar sobre as limitações relacionadas ao uso de computadores Linux com um servidor pull, consulte as Notas de versão para a configuração de estado desejado para Linux.

### <a name="working-with-configurations-locally"></a>Trabalhando com configurações localmente

A DSC para Linux inclui scripts para trabalhar com a configuração no computador Linux local. Esses scripts estão localizados em `/opt/microsoft/dsc/Scripts` e incluem o seguinte:

- GetDscConfiguration.py

Gera a configuração atual aplicada ao computador. Semelhante ao cmdlet `Get-DscConfiguration` do cmdlet do Windows PowerShell.

`# sudo ./GetDscConfiguration.py`

- GetDscLocalConfigurationManager.py

Gera a metaconfiguração atual aplicada ao computador. Semelhante ao cmdlet [Get-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager).

`# sudo ./GetDscLocalConfigurationManager.py`

- InstallModule.py

Instala um módulo personalizado de recurso de DSC. Requer o caminho para um arquivo. zip que contém a biblioteca de objeto compartilhado do módulo e os arquivos MOF do esquema.

`# sudo ./InstallModule.py /tmp/cnx_Resource.zip`

- RemoveModule.py

Remove um módulo personalizado de recurso de DSC. Requer o nome do módulo que será removido.

`# sudo ./RemoveModule.py cnx_Resource`

- StartDscLocalConfigurationManager.py

Aplica um arquivo MOF de configuração ao computador. Semelhante ao cmdlet [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration). Exige o caminho até o MOF de configuração para aplicar.

`# sudo ./StartDscLocalConfigurationManager.py –configurationmof /tmp/localhost.mof`

- SetDscLocalConfigurationManager.py

Aplica um arquivo MOF de metaconfiguração ao computador. Semelhante ao cmdlet [Set-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager). Exige o caminho até o MOF de metaconfiguração para aplicar.

`# sudo ./SetDscLocalConfigurationManager.py –configurationmof /tmp/localhost.meta.mof`

## <a name="powershell-desired-state-configuration-for-linux-log-files"></a>Arquivos de Log da Configuração de Estado Desejado do PowerShell para Linux

Os seguintes arquivos de log são gerados para mensagens da DSC para Linux.

|Arquivo de log|Directory|Descrição|
|---|---|---|
|**omiserver.log**|`/var/opt/omi/log`|Mensagens relacionadas à operação do servidor CIM da OMI.|
|**dsc.log**|`/var/opt/omi/log`|Mensagens relacionadas à operação das operações de recurso do Gerenciador de Configurações Local (LCM) e da DSC.|
