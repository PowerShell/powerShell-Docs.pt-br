---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,instalação
title: Melhorias da DSC no WMF 5.1
ms.openlocfilehash: 445d0f7bb54c6b21b6af26c4174f3d6422caf6dd
ms.sourcegitcommit: 0907b8c6322d2c7c61b17f8168d53452c8964b41
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/05/2020
ms.locfileid: "87771542"
---
# <a name="improvements-in-desired-state-configuration-dsc-in-wmf-51"></a>Melhorias na DSC (Configuração de Estado Desejado) no WMF 5.1

## <a name="dsc-class-resource-improvements"></a>Melhorias de recursos de classe da DSC

No 5.1 WMF, corrigimos os seguintes problemas conhecidos:

- O Get-DscConfiguration poderá retornar valores vazios (nulos) ou erros se um tipo complexo/de tabela de hash for retornado pela função Get() de um recurso DSC baseado em classe.
- O Get-DscConfiguration retornará um erro se a credencial RunAs for usada na configuração DSC.
- Os recursos baseados em classe não podem ser usados em uma configuração de composição.
- O Start-DscConfiguration será suspenso se o recurso baseado em classe tiver uma propriedade de seu próprio tipo.
- O recurso baseado em classe não pode ser usado como um recurso exclusivo.

## <a name="dsc-resource-debugging-improvements"></a>Melhorias de depuração de recursos da DSC

No WMF 5.0, o depurador do PowerShell não interrompeu o método de recurso baseado em classe (Get/Set/Test) diretamente. No WMF 5.1, o depurador interrompe o método de recurso baseado em classe da mesma forma que faz com os métodos de recursos baseados em MOF.

## <a name="dsc-pull-client-supports-tls-11-and-tls-12"></a>O cliente pull da DSC dá suporte para TLS 1.1 e para TLS 1.2

Anteriormente, o cliente pull da DSC dava suporte apenas para SSL3.0 e TLS1.0 por meio de conexões HTTPS. Se fosse forçado a usar protocolos mais seguros, o cliente pull pararia de funcionar. No WMF 5.1, o cliente pull da DSC não dá mais suporte a SSL 3.0 e adiciona suporte a protocolos mais seguros TLS 1.1 e TLS 1.2.

## <a name="improved-pull-server-registration"></a>Registro do servidor de pull aprimorado

Nas versões anteriores do WMF, as solicitações simultâneas de registros/relatórios em um servidor de pull da DSC durante o uso do banco de dados ESENT provocavam uma falha de registro e/ou relatório do LCM. Nesses casos, os logs de eventos no servidor de pull têm o erro "O nome da instância já está em uso." Isso ocorreu devido ao uso de um padrão incorreto para acessar o banco de dados ESENT em um cenário com multithread. No WMF 5.1, esse problema foi corrigido. Os registros ou relatórios simultâneos (que envolvem o banco de dados ESENT) funcionam bem no WMF 5.1. Esse problema é aplicável somente ao banco de dados ESENT e não se aplica ao banco de dados OLEDB.

## <a name="enable-circular-log-on-esent-database-instance"></a>Habilitar o log Circular na instância do banco de dados ESENT

Na versão anterior da DSC-PullServer, os arquivos de log do banco de dados ESENT preenchiam o espaço em disco do pullserver porque a instância do banco de dados estava sendo criada sem log circular. Nesta versão, você tem a opção de controlar o comportamento de log circular da instância usando o web.config do pullserver. Por padrão, o CircularLogging está definido como VERDADEIRO.

```xml
<appSettings>
    <add key="dbprovider" value="ESENT" />
    <add key="dbconnectionstr" value="C:\Program Files\WindowsPowerShell\DscService\Devices.edb" />
    <add key="CheckpointDepthMaxKB" value="512" />
    <add key="UseCircularESENTLogs" value="TRUE" />
  </appSettings>
```

## <a name="wow64-support-for-configuration-keyword"></a>Suporte ao WOW64 para palavra-chave Configuration

Agora há suporte para a palavra-chave `Configuration` no WOW64 em um computador de 64 bits. Isso significa que uma configuração DSC pode ser definida e compilada dentro de um processo de 32 bits como o ISE do Windows PowerShell (x86) executado em um computador de 64 bits.

## <a name="pull-partial-configuration-naming-convention"></a>Convenção de nomenclatura de configuração parcial de pull

Na versão anterior, a convenção de nomenclatura para uma configuração parcial era que o nome do arquivo MOF no servidor de pull/serviço deveria ser compatível com o nome de configuração parcial especificado nas configurações do gerenciador de configuração local que, por sua vez, deve ser compatível com o nome de configuração inserido no arquivo MOF.

Confira os instantâneos abaixo:

- Definições da configuração local, que determina uma configuração parcial que um nó está autorizado a receber.

  ![Metaconfiguração de exemplo](media/DSC-improvements/MetaConfigPartialOne.png)

- Definição da configuração parcial de exemplo

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

- "ConfigurationName" inserido no arquivo MOF gerado.

  ![Arquivo MOF de exemplo gerado](media/DSC-improvements/PartialGeneratedMof.png)

- FileName no repositório de configuração de pull

  ![FileName no Repositório de Configuração](media/DSC-improvements/PartialInConfigRepository.png)

  O nome do serviço da Automação do Azure gerou arquivos MOF como `<ConfigurationName>.<NodeName>.mof`. Portanto, a configuração abaixo é compilada para PartialOne.localhost.mof.

  Ela tornou impossível a extração de uma de suas configurações parciais do serviço da Automação do Azure.

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

  No WMF 5.1, uma configuração parcial no servidor de pull/serviço pode ser nomeada `<ConfigurationName>.<NodeName>.mof`. Além disso, se um computador estiver extraindo uma única configuração de um servidor de pull/serviço, então, o arquivo de configuração no repositório de configuração do servidor de pull poderá ter qualquer nome de arquivo. Esta flexibilidade de nomenclatura permite que você gerencie seus nós parcialmente pelo serviço da Automação do Azure, no qual algumas configurações do nó chegarão da DSC de Automação do Azure e uma configuração parcial gerenciada localmente.

  A metaconfiguração abaixo configura um nó para ser gerenciado tanto localmente quanto pelo serviço da Automação do Azure.

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

## <a name="using-psdscrunascredential-with-dsc-composite-resources"></a>Usando a PsDscRunAsCredential com os recursos de composição da DSC

Adicionamos suporte para usar [PsDscRunAsCredential](/powershell/scripting/dsc/configurations/runAsUser) com os recursos de [Composição](/powershell/scripting/dsc/resources/authoringresourcecomposite) da DSC.

Agora é possível especificar o valor para **PsDscRunAsCredential** ao usar recursos de composição nas configurações. Quando especificado, todos os recursos serão executados em um recurso de composição como um usuário RunAs. Se o recurso de composição chamar outro recurso de composição, todos os seus recursos também serão executados como usuário RunAs. As credenciais RunAs são propagadas para qualquer nível da hierarquia do recurso de composição. Se qualquer recurso dentro de um recurso de composição especificar seu próprio valor para **PsDscRunAsCredential**, ocorrerá um erro de mesclagem durante a compilação da configuração.

Este exemplo mostra o uso com o recurso de composição [WindowsFeatureSet](/powershell/scripting/dsc/reference/resources/windows/windowsfeaturesetresource) incluso no módulo PSDesiredStateConfiguration.

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

## <a name="allowing-for-identical-duplicate-resources-in-a-configuration"></a>Permitindo recursos duplicados idênticos em uma configuração

O DSC não permite nem manipula definições de recursos conflitantes dentro de uma configuração. Em vez de tentar resolver o conflito, ele simplesmente falha. Como a reutilização de configuração é cada mais utilizada por meio de recursos de composição, etc., os conflitos ocorrerão com mais frequência. Quando definições de recursos conflitantes forem idênticas, o DSC deverá ter inteligência para permiti-las. Com esta versão, damos suporte a várias instâncias de recursos com definições idênticas:

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

Em versões anteriores, o resultado seria uma compilação com falha devido a um conflito entre as instâncias de WindowsFeature FE_IIS e WindowsFeature Worker_IIS tentando garantir que a função “Web-Server” está instalada. Observe que *todas* as propriedades que estão sendo configuradas são idênticas nessas duas configurações. Uma vez que *todas* as propriedades nesses dois recursos são idênticas, agora isso resultará em uma compilação bem-sucedida.

Se alguma das propriedades for diferente entre os dois recursos, elas não serão consideradas idênticas e a compilação falhará.

## <a name="dsc-module-and-configuration-signing-validations"></a>Validações do módulo de DSC e da assinatura de configuração

Na DSC, as configurações e os módulos são distribuídos para computadores gerenciados do servidor de pull. Se o servidor de pull estiver comprometido, um invasor poderá possivelmente alterar as configurações e os módulos no servidor de pull e distribuí-los para todos os nós gerenciados.

No WMF 5.1, a DSC dá suporte para a validação de assinaturas digitais no catálogo e nos arquivos de configuração (.MOF). Este recurso evita que os nós executem as configurações ou os arquivos de módulo que não são assinados por um signatário confiável ou que foram violados depois de assinados por um signatário confiável.

### <a name="how-to-sign-configuration-and-module"></a>Como assinar a configuração e o módulo

- Arquivos de Configuração (.MOFs): o cmdlet [Set-AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Set-AuthenticodeSignature) existente do PowerShell é estendido para dar suporte à assinatura de arquivos MOF.
- Módulos: a assinatura dos módulos é feita com a assinatura do catálogo do módulo correspondente por meio das seguintes etapas:
  1. Crie um arquivo de catálogo: um arquivo de catálogo contém uma coleção de hashes criptográficos ou impressões digitais. Cada impressão digital corresponde a um arquivo que está incluído no módulo. O novo cmdlet [New-FileCatalog](/powershell/module/microsoft.powershell.security/new-filecatalog) foi adicionado para permitir que os usuários criem um arquivo de catálogo para seu módulo.
  2. Assine o arquivo de catálogo: use a [Set-AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Set-AuthenticodeSignature) para assinar o arquivo de catálogo.
  3. Coloque o arquivo de catálogo dentro da pasta do módulo. Por convenção, o arquivo de catálogo do módulo deve ser colocado na pasta do módulo, com o mesmo nome do módulo.

### <a name="localconfigurationmanager-settings-to-enable-signing-validations"></a>Configurações de LocalConfigurationManager para habilitar as validações de assinatura

#### <a name="pull"></a>Recepção

O LocalConfigurationManager de um nó executa a validação da assinatura dos módulos e das configurações com base em suas configurações atuais. Por padrão, a validação da assinatura está desabilitada. A validação da assinatura pode ser habilitada adicionando o bloco "SignatureValidation" à definição de metaconfiguração do nó, conforme mostrado abaixo:

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

A definição da metaconfiguração acima em um nó habilita a validação da assinatura nas configurações e nos módulos baixados. O Gerenciador de Configurações Local executa as seguintes etapas para verificar as assinaturas digitais.

1. Verifique se a assinatura em um arquivo de configuração (.MOF) é válida usando o cmdlet `Get-AuthenticodeSignature`.
2. Verifique se a autoridade de certificação que autorizou o signatário é confiável.
3. Baixe as dependências de módulo/recurso da configuração para uma localização temporária.
4. Verifique se a assinatura do catálogo foi incluída dentro do módulo.
   - Encontre um arquivo `<moduleName>.cat` e verifique sua assinatura usando `Get-AuthenticodeSignature`.
   - Verifique se a autoridade de certificação que autenticou o signatário é confiável.
   - Verifique se o conteúdo dos módulos não foi violado usando o novo cmdlet `Test-FileCatalog`.
5. `Install-Module` em `$env:ProgramFiles\WindowsPowerShell\Modules\`
6. Configuração do processo

> [!NOTE]
> a validação da assinatura no catálogo de módulo e na configuração é realizada somente quando a configuração é aplicada ao sistema pela primeira vez ou quando o módulo é baixado e instalado.
> As execuções de consistência não validam a assinatura de Current.mof ou de suas dependências de módulo. Se a verificação tiver falhado em qualquer estágio, por exemplo, se a configuração extraída do servidor de pull não estiver assinada, o processamento da configuração será encerrado com o erro mostrado abaixo e todos os arquivos temporários serão excluídos.

![Configuração de Saída de Erro de Exemplo](media/DSC-improvements/PullUnsignedConfigFail.png)

Da mesma forma, a extração de um módulo cujo catálogo não está assinado resulta no seguinte erro:

![Módulo de Saída de Erro de Exemplo](media/DSC-improvements/PullUnisgnedCatalog.png)

#### <a name="push"></a>Push

Uma configuração entregue com o uso de push pode ser violada em sua origem antes de ser entregue para o nó. O Gerenciador de Configurações Local executa etapas semelhantes de validação de assinatura para as configurações enviadas por push ou publicadas. Veja abaixo um exemplo completo de validação de assinatura para envio por push.

- Habilite a validação da assinatura no nó.

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

- Crie um arquivo de configuração de exemplo.

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

- Tente enviar o arquivo de configuração não assinado por push para o nó.

  ```powershell
  Start-DscConfiguration -Path .\Test -Wait -Verbose -Force
  ```

  ![Erro – arquivo MOF não assinado enviado por push](media/DSC-improvements/PushUnsignedMof.png)

- Assine o arquivo de configuração usando um certificado de assinatura de código.

  ![Assinar o arquivo MOF](media/DSC-improvements/SignMofFile.png)

- Tente enviar o arquivo MOF assinado por push.

  ![Enviar por push o arquivo MOF assinado](media/DSC-improvements/PushSignedMof.png)
