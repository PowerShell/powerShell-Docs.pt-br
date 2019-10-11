---
ms.date: 10/30/2018
keywords: DSC,powershell,configuração,instalação
title: Solucionando problemas de DSC
ms.openlocfilehash: 2a0d2138f30573b9ae6cf52d8b106a05f1193407
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71954613"
---
# <a name="troubleshooting-dsc"></a>Solucionando problemas de DSC

_Aplica-se a: Windows PowerShell 4.0, Windows PowerShell 5.0_

Este tópico descreve maneiras de solucionar o DSC quando surgem problemas.

## <a name="winrm-dependency"></a>Dependência do WinRM

O DSC (Configuração de Estado Desejado) do Windows PowerShell depende do WinRM. O WinRM não é habilitado por padrão no Windows Server 2008 R2 nem no Windows 7. Execute `Set-WSManQuickConfig`, em uma sessão de privilégios elevados do Windows PowerShell, para habilitar o WinRM.

## <a name="using-get-dscconfigurationstatus"></a>Usando Get-DscConfigurationStatus

O cmdlet [Get-DscConfigurationStatus](/powershell/module/PSDesiredStateConfiguration/Get-DscConfigurationStatus) obtém informações sobre o status de configuração de um nó de destino. Será retornado um objeto avançado, que inclui informações de alto nível sobre se a execução da configuração foi bem-sucedida ou não. É possível examinar o objeto para descobrir detalhes sobre a execução da configuração como:

- Todos os recursos que falharam
- Qualquer recurso que solicitou uma reinicialização
- Definições de metaconfiguração em tempo de execução da configuração
- Etc.

O seguinte conjunto de parâmetros retorna as informações de status para a última execução de configuração:

```
Get-DscConfigurationStatus [-CimSession <CimSession[]>]
                           [-ThrottleLimit <int>]
                           [-AsJob]
                           [<CommonParameters>]
```
O seguinte conjunto de parâmetros retorna as informações de status para todas as execuções de configuração anteriores:

```
Get-DscConfigurationStatus -All
                           [-CimSession <CimSession[]>]
                           [-ThrottleLimit <int>]
                           [-AsJob]
                           [<CommonParameters>]
```

## <a name="example"></a>Exemplo

```powershell
PS C:\> $Status = Get-DscConfigurationStatus

PS C:\> $Status

Status         StartDate                Type            Mode    RebootRequested        NumberOfResources
------        ---------                ----            ----    ---------------        -----------------
Failure        11/24/2015  3:44:56     Consistency        Push    True                36

PS C:\> $Status.ResourcesNotInDesiredState

ConfigurationName     :    MyService
DependsOn             :
ModuleName            :    PSDesiredStateConfiguration
ModuleVersion         :    1.1
PsDscRunAsCredential  :
ResourceID            :    [File]ServiceDll
SourceInfo            :    c:\git\CustomerService\Configs\MyCustomService.ps1::5::34::File
DurationInSeconds     :    0.19
Error                 :    SourcePath must be accessible for current configuration. The related file/directory is:
                           \\Server93\Shared\contosoApp.dll. The related ResourceID is [File]ServiceDll
FinalState            :
InDesiredState        :    False
InitialState          :
InstanceName          :    ServiceDll
RebootRequested       :    False
ResourceName          :    File
StartDate             :    11/24/2015  3:44:56
PSComputerName        :
```

## <a name="my-script-wont-run-using-dsc-logs-to-diagnose-script-errors"></a>Meu script não funciona: usando logs de DSC para diagnosticar erros de script

Como todos os softwares do Windows, a DSC registra erros e eventos em [logs](/windows/desktop/EventLog/about-event-logging) que podem ser exibidos no [Visualizador de Eventos](https://support.microsoft.com/hub/4338813/windows-help).
Um exame desses logs pode ajudá-lo a entender por que uma determinada operação falhou e como evitar falhas no futuro. Escrever scripts de configuração pode ser complicado; portanto, para facilitar o rastreamento de erros durante a criação, use o recurso de Log de DSC para acompanhar o progresso da sua configuração no log de eventos Analítico de DSC.

## <a name="where-are-dsc-event-logs"></a>Onde estão os logs de eventos de DSC?

No Visualizador de Eventos, os eventos de DSC estão em: **Logs de Aplicativos e Serviços /Microsoft/Windows/Desired State Configuration**

O cmdlet do PowerShell correspondente, [Get-WinEvent](/powershell/module/Microsoft.PowerShell.Diagnostics/Get-WinEvent), também pode ser executado para exibir os logs de eventos:

```
PS C:\> Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"

   ProviderName: Microsoft-Windows-DSC

TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
11/17/2014 10:27:23 PM        4102 Information      Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} :
```

Como mostrado acima, o nome do log primário da DSC é **Microsoft->Windows->DSC** (outros nomes de logs no Windows não são mostrados aqui por uma questão de brevidade). O nome primário é anexado ao nome do canal para criar o nome completo do log. O mecanismo de DSC grava principalmente em três tipos de logs: [Logs Operacionais, Analíticos e de Depuração](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc722404(v=ws.11)). Como os logs analítico e de depuração permanecem desligados por padrão, devem ser habilitados no Visualizador de Eventos. Para fazer isso, abra o Visualizador de Eventos digitando Show-EventLog no Windows PowerShell; ou clique no botão **Iniciar**, clique em **Painel de Controle**, em **Ferramentas Administrativas** e, em seguida, clique em **Visualizador de Eventos**.
No menu **Exibir** no Visualizador de Eventos, clique em **Mostrar Logs Analítico e de Depuração**. O nome do log para o canal analítico **Microsoft-Windows-Dsc/Analytic**; para o canal de depuração é **Microsoft-Windows-Dsc/Debug**. Também é possível usar o utilitário [wevtutil](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc732848(v=ws.11)) para habilitar os logs, conforme mostrado no exemplo a seguir.

```powershell
wevtutil.exe set-log "Microsoft-Windows-Dsc/Analytic" /q:true /e:true
```

## <a name="what-do-dsc-logs-contain"></a>O que os logs de DSC contêm?

Os logs de DSC são divididos nos três canais de log com base na importância da mensagem. O log operacional na DSC contém todas as mensagens de erro e pode ser usado para identificar um problema. O log analítico tem um maior volume de eventos e pode identificar onde ocorreram erros. Esse canal também contém mensagens detalhadas (se houver). O log de depuração contém logs que podem ajudá-lo a entender como os erros ocorreram. As mensagens de eventos de DSC são estruturadas de modo que cada mensagem de evento comece com uma ID de trabalho que represente uma operação de DSC com exclusividade. O exemplo a seguir tenta obter a mensagem do primeiro evento registrado no log de DSC operacional.

```powershell
PS C:\> $AllDscOpEvents = Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"
PS C:\> $FirstOperationalEvent = $AllDscOpEvents[0]
PS C:\> $FirstOperationalEvent.Message
Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} :
Consistency engine was run successfully.
```

Os eventos de DSC são registrados em uma estrutura específica que permite que o usuário agregue eventos por meio de um trabalho de DSC. A estrutura é a seguinte:

```
Job ID : <Guid>
<Event Message>
```

## <a name="gathering-events-from-a-single-dsc-operation"></a>Coletando eventos de uma operação única de DSC

Os logs de eventos de DSC contêm os eventos gerados por várias operações de DSC. No entanto, você geralmente estará interessado nos detalhes sobre apenas uma operação específica. Todos os logs de DSC podem ser agrupados pela propriedade de ID do trabalho, que é exclusiva para cada operação de DSC. A ID do trabalho é exibida como o primeiro valor da propriedade em todos os eventos de DSC. As etapas a seguir explicam como acumular todos os eventos em uma estrutura de matriz agrupada.

```powershell
<##########################################################################
 Step 1 : Enable analytic and debug DSC channels (Operational channel is enabled by default)
###########################################################################>

wevtutil.exe set-log "Microsoft-Windows-Dsc/Analytic" /q:true /e:true
wevtutil.exe set-log "Microsoft-Windows-Dsc/Debug" /q:True /e:true

<##########################################################################
 Step 2 : Perform the required DSC operation (Below is an example, you could run any DSC operation instead)
###########################################################################>

Get-DscLocalConfigurationManager

<##########################################################################
Step 3 : Collect all DSC Logs, from the Analytic, Debug and Operational channels
###########################################################################>

$DscEvents=[System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Operational") `
         + [System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Analytic" -Oldest) `
         + [System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Debug" -Oldest)


<##########################################################################
 Step 4 : Group all logs based on the job ID
###########################################################################>
$SeparateDscOperations = $DscEvents | Group {$_.Properties[0].value}
```

Aqui, a variável `$SeparateDscOperations` contém logs agrupados pelas IDs de trabalho. Cada elemento da matriz dessa variável representa um grupo de eventos registrados por uma operação de DSC diferente, permitindo o acesso a mais informações sobre os logs.

```
PS C:\> $SeparateDscOperations

Count Name                      Group
----- ----                      -----
   48 {1A776B6A-5BAC-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
   40 {E557E999-5BA8-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....

PS C:\> $SeparateDscOperations[0].Group

   ProviderName: Microsoft-Windows-DSC

TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
12/2/2013 3:47:29 PM          4115 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4198 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4114 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4102 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4098 Warning          Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4098 Warning          Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4176 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
```

Você pode extrair os dados na variável `$SeparateDscOperations` usando [Where-Object](/powershell/module/microsoft.powershell.core/where-object). Seguem cinco cenários em que talvez você queira extrair dados para solucionar problemas de DSC:

### <a name="1-operations-failures"></a>1: Falhas em operações

Todos os eventos têm [níveis de gravidade](/windows/desktop/WES/defining-severity-levels). Essas informações podem ser usadas para identificar os eventos de erro:

```
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.LevelDisplayName -contains "Error"}

Count Name                      Group
----- ----                      -----
   38 {5BCA8BE7-5BB6-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
```

### <a name="2-details-of-operations-run-in-the-last-half-hour"></a>2: Detalhes das operações executadas na última meia hora

`TimeCreated`, uma propriedade de todos os eventos do Windows, indica o horário em que o evento foi criado. A comparação dessa propriedade com um objeto de data/hora específico pode ser usada para filtrar todos os eventos:

```powershell
PS C:\> $DateLatest = (Get-Date).AddMinutes(-30)
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.TimeCreated -gt $DateLatest}

Count Name                      Group
----- ----                      -----
    1 {6CEC5B09-5BB0-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord}
```

### <a name="3-messages-from-the-latest-operation"></a>3: Mensagens da operação mais recente

A operação mais recente é armazenada no primeiro índice do grupo de matriz `$SeparateDscOperations`.
Uma consulta às mensagens do grupo para o índice 0 gera todas as mensagens referentes à operação mais recente:

```powershell
PS C:\> $SeparateDscOperations[0].Group.Message
Job {5BCA8BE7-5BB6-11E3-BF41-00155D553612} :
Running consistency engine.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} :
Configuration is sent from computer NULL by user sid S-1-5-18.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} :
Displaying messages from built-in DSC resources:
 WMI channel 1
 ResourceID:
 Message : [INCH-VM]:                            [] Starting consistency engine.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} :
Displaying messages from built-in DSC resources:
 WMI channel 1
 ResourceID:
 Message : [INCH-VM]:                            [] Consistency check completed.
```

### <a name="4-error-messages-logged-for-recent-failed-operations"></a>4: Mensagens de erro registradas para falhas em operações recentes

`$SeparateDscOperations[0].Group` contém um conjunto de eventos para a operação mais recente. Execute o cmdlet `Where-Object` para filtrar os eventos com base em seu nome de exibição de nível. Os resultados são armazenados na variável `$myFailedEvent`, que ainda pode ser examinada para obter a mensagem de evento:

```powershell
PS C:\> $myFailedEvent = ($SeparateDscOperations[0].Group | Where-Object {$_.LevelDisplayName -eq "Error"})

PS C:\> $myFailedEvent.Message

Job {5BCA8BE7-5BB6-11E3-BF41-00155D553612} :
DSC Engine Error :
 Error Message Current configuration does not exist. Execute Start-DscConfiguration command with -Path pa
rameter to specify a configuration file and create a current configuration first.
Error Code : 1
```

### <a name="5-all-events-generated-for-a-particular-job-id"></a>5: Todos os eventos gerados para uma ID de trabalho específica.

`$SeparateDscOperations` é uma matriz de grupos, sendo que cada um deles tem o nome como a ID exclusiva do trabalho. Ao executar o cmdlet `Where-Object`, você pode extrair esses grupos de eventos que têm uma ID de trabalho específica:

```powershell
PS C:\> ($SeparateDscOperations | Where-Object {$_.Name -eq $jobX} ).Group

   ProviderName: Microsoft-Windows-DSC

TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
12/2/2013 4:33:24 PM          4102 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...
12/2/2013 4:33:24 PM          4168 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...
12/2/2013 4:33:24 PM          4146 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...
12/2/2013 4:33:24 PM          4120 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...
```

## <a name="using-xdscdiagnostics-to-analyze-dsc-logs"></a>Usando xDscDiagnostics para analisar logs de DSC

**xDscDiagnostics** é um módulo do PowerShell que consiste em várias funções que podem ajudar a analisar falhas de DSC em seu computador. Essas funções podem ajudá-lo a identificar todos os eventos locais de operações anteriores de DSC ou eventos de DSC em computadores remotos (com credenciais válidas). Aqui, o termo operação de DSC é usado para definir uma única execução de DSC desde o início até o fim. Por exemplo, `Test-DscConfiguration` seria uma operação de DSC separada. Da mesma forma, cada outro cmdlet na DSC (como `Get-DscConfiguration`, `Start-DscConfiguration`, etc.) pode ser identificado como operações de DSC separadas. As funções são explicadas em [xDscDiagnostics](https://github.com/PowerShell/xDscDiagnostics). A ajuda está disponível executando `Get-Help <cmdlet name>`.

### <a name="getting-details-of-dsc-operations"></a>Obtendo detalhes das operações de DSC

A função `Get-xDscOperation` permite encontrar os resultados das operações de DSC executadas em um ou vários computadores e retorna um objeto que contém a coleção de eventos produzidos por cada operação de DSC. Por exemplo, na seguinte saída, três comandos foram executados. O primeiro deles passou e os outros dois falharam. Esses resultados estão resumidos na saída de `Get-xDscOperation`.

```powershell
PS C:\DiagnosticsTest> Get-xDscOperation

ComputerName   SequenceId TimeCreated           Result   JobID                                 AllEvents
------------   ---------- -----------           ------   -----                                 ---------
SRV1   1          6/23/2016 9:37:52 AM  Failure  9701aadf-395e-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   2          6/23/2016 9:36:54 AM  Failure  7e8e2d6e-395c-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   3          6/23/2016 9:36:54 AM  Success  af72c6aa-3960-11e6-9165-00155d390509  {@{Message=Operati...
```

Você também pode especificar que deseja apenas obter resultados para as operações mais recentes usando o parâmetro `Newest`:

```powershell
PS C:\DiagnosticsTest> Get-xDscOperation -Newest 5
ComputerName   SequenceId TimeCreated           Result   JobID                                 AllEvents
------------   ---------- -----------           ------   -----                                 ---------
SRV1   1          6/23/2016 4:36:54 PM  Success                                        {@{Message=; TimeC...
SRV1   2          6/23/2016 4:36:54 PM  Success  5c06402b-399b-11e6-9165-00155d390509  {@{Message=Operati...
SRV1   3          6/23/2016 4:36:54 PM  Success                                        {@{Message=; TimeC...
SRV1   4          6/23/2016 4:36:54 PM  Success  5c06402a-399b-11e6-9165-00155d390509  {@{Message=Operati...
SRV1   5          6/23/2016 4:36:51 PM  Success                                        {@{Message=; TimeC...
```

### <a name="getting-details-of-dsc-events"></a>Obtendo detalhes de eventos de DSC

O cmdlet `Trace-xDscOperation` gera um objeto que contém uma coleção de eventos, os tipos de evento e a saída de mensagem gerada por meio de uma operação de DSC específica. Normalmente, quando uma falha é encontrada em qualquer uma das operações usando `Get-xDscOperation`, você rastrearia a operação para descobrir quais dos eventos causaram uma falha.

Use o parâmetro `SequenceID` para obter os eventos de uma operação específica referente a um computador específico.
Por exemplo, se você especificar um `SequenceID` de 9, `Trace-xDscOperaion` obterá o rastreamento para a operação de DSC que foi a 9ª da última operação:

```powershell
PS C:\DiagnosticsTest> Trace-xDscOperation -SequenceID 9

ComputerName   EventType    TimeCreated           Message
------------   ---------    -----------           -------
SRV1   OPERATIONAL  6/24/2016 10:51:52 AM Operation Consistency Check or Pull started by user sid S-1-5-20 from computer NULL.
SRV1   OPERATIONAL  6/24/2016 10:51:52 AM Running consistency engine.
SRV1   OPERATIONAL  6/24/2016 10:51:52 AM The local configuration manager is updating the PSModulePath to WindowsPowerShell\Modules;C:\Prog...
SRV1   OPERATIONAL  6/24/2016 10:51:53 AM  Resource execution sequence :: [WindowsFeature]DSCServiceFeature, [xDSCWebService]PSDSCPullServer.
SRV1   OPERATIONAL  6/24/2016 10:51:54 AM Consistency engine was run successfully.
SRV1   OPERATIONAL  6/24/2016 10:51:54 AM Job runs under the following LCM setting. ...
SRV1   OPERATIONAL  6/24/2016 10:51:54 AM Operation Consistency Check or Pull completed successfully.
```

Passe o **GUID** atribuído a uma operação de DSC específica (conforme retornado pelo cmdlet `Get-xDscOperation`) para obter os detalhes do evento para a operação de DSC:

```powershell
PS C:\DiagnosticsTest> Trace-xDscOperation -JobID 9e0bfb6b-3a3a-11e6-9165-00155d390509

ComputerName   EventType    TimeCreated           Message
------------   ---------    -----------           -------
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull started by user sid S-1-5-20 from computer NULL.
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCache.mof
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Running consistency engine.
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [] Starting consistency engine.
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Applying configuration from C:\Windows\System32\Configuration\Current.mof.
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Parsing the configuration to apply.
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM  Resource execution sequence :: [WindowsFeature]DSCServiceFeature, [xDSCWebService]PSDSCPullServer.
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Resource ]  [[WindowsFeature]DSCServiceFeature]
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_RoleResource with resource name [WindowsFeature]DSC...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Test     ]  [[WindowsFeature]DSCServiceFeature]
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[WindowsFeature]DSCServiceFeature] The operation 'Get...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[WindowsFeature]DSCServiceFeature] The operation 'Get...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Test     ]  [[WindowsFeature]DSCServiceFeature] True in 0.3130 sec...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Resource ]  [[WindowsFeature]DSCServiceFeature]
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Resource ]  [[xDSCWebService]PSDSCPullServer]
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_xDSCWebService with resource name [xDSCWebService]P...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Test     ]  [[xDSCWebService]PSDSCPullServer]
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check Ensure
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check Port
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check Physical Path ...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check State
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Get Full Path for We...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Test     ]  [[xDSCWebService]PSDSCPullServer] True in 0.0160 seconds.
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Resource ]  [[xDSCWebService]PSDSCPullServer]
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [] Consistency check completed.
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCache.mof
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Consistency engine was run successfully.
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Job runs under the following LCM setting. ...
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull completed successfully.
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCache.mof
```

Observe que, como `Trace-xDscOperation` agrega eventos dos logs Operacional, Analítico e de Depuração, ele solicitará a habilitação desses logs, conforme descrito acima.

Como alternativa, você pode reunir informações sobre os eventos salvando a saída de `Trace-xDscOperation` em uma variável. Pode-se usar o comando a seguir para exibir todos os eventos de determinada operação de DSC.

```powershell
PS C:\DiagnosticsTest> $Trace = Trace-xDscOperation -SequenceID 4

PS C:\DiagnosticsTest> $Trace.Event
```

Isso exibirá os mesmos resultados que o cmdlet `Get-WinEvent`, como a saída abaixo:

```output
   ProviderName: Microsoft-Windows-DSC

TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
6/23/2016 1:36:53 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 1:36:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 2:07:00 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 2:07:01 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 2:36:55 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 2:36:56 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 3:06:55 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 3:06:55 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 3:36:55 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 3:36:55 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 4:06:53 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 4:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 4:36:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 4:36:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 5:06:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 5:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 5:36:54 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 5:36:54 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 6:06:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 6:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 6:36:56 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 6:36:57 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 7:06:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 7:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 7:36:53 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 7:36:54 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 8:06:54 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
```

Idealmente, em primeiro lugar, use `Get-xDscOperation` para listar as últimas execuções da configuração DSC nos seus computadores. Depois disso, você pode examinar qualquer operação única (usando sua SequenceID ou JobID) com `Trace-xDscOperation` para descobrir o que ela fazia em segundo plano.

### <a name="getting-events-for-a-remote-computer"></a>Obtendo eventos de um computador remoto

Use o parâmetro `ComputerName` do cmdlet `Trace-xDscOperation` para obter os detalhes de evento em um computador remoto. Antes de poder fazer isso, é necessário criar uma regra de firewall para permitir a administração remota no computador remoto:

```powershell
New-NetFirewallRule -Name "Service RemoteAdmin" -DisplayName "Remote" -Action Allow
```

Agora você pode especificar o computador em sua chamada para `Trace-xDscOperation`:

```powershell
PS C:\DiagnosticsTest> Trace-xDscOperation -ComputerName SRV2 -Credential Get-Credential -SequenceID 5

ComputerName   EventType    TimeCreated           Message
------------   ---------    -----------           -------
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull started by user sid S-1-5-20 f...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCach...
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Running consistency engine.
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [] Starting consistency...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Applying configuration from C:\Windows\System32\Configuration\Curr...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Parsing the configuration to apply.
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM  Resource execution sequence :: [WindowsFeature]DSCServiceFeature,...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Resource ]  [[WindowsFeature]DSCSer...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_RoleResource with re...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Test     ]  [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Test     ]  [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Resource ]  [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Resource ]  [[xDSCWebService]PSDSCP...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_xDSCWebService with ...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Test     ]  [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Test     ]  [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Resource ]  [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [] Consistency check co...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCach...
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Consistency engine was run successfully.
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Job runs under the following LCM setting. ...
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull completed successfully.
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCach...
```

## <a name="my-resources-wont-update-how-to-reset-the-cache"></a>Meus recursos não são atualizados: como redefinir o cache

O mecanismo de DSC armazena em cache os recursos implementados como um módulo do PowerShell para fins de eficiência.
No entanto, isso pode causar problemas quando você está criando um recurso e testando-o simultaneamente, porque DSC carregará a versão armazenada em cache até o processo ser reiniciado. A única maneira de fazer a DSC carregar a versão mais recente é eliminar explicitamente o processo que hospeda o mecanismo de DSC.

Da mesma forma, quando você executa `Start-DscConfiguration`, depois de adicionar e modificar um recurso personalizado, a modificação pode não ser executada a menos que, ou até que, o computador seja reinicializado. Isso ocorre porque a DSC é executada no Processo de Host do provedor WMI (WmiPrvSE) e, geralmente, há muitas instâncias do WmiPrvSE em execução ao mesmo tempo. Quando você reinicializa, o processo de host é reiniciado e o cache é limpo.

Para conseguir reciclar a configuração e limpar o cache sem reinicialização, você deve parar e reiniciar o processo de host. Isso pode ser feito por instância, ou seja, você identifica o processo, interrompe-o e reinicia-o. Ou pode usar `DebugMode`, conforme demonstrado abaixo, para recarregar o recurso de DSC do PowerShell.

Para identificar o processo que está hospedando o mecanismo de DSC e interrompê-lo por instância, é possível listar a ID do processo do WmiPrvSE que está hospedando o mecanismo de DSC. Em seguida, para atualizar o provedor, interrompa o processo WmiPrvSE usando os comandos abaixo; depois, execute **Start-DscConfiguration** novamente.

```powershell
###
### find the process that is hosting the DSC engine
###
$dscProcessID = Get-WmiObject msft_providers |
Where-Object {$_.provider -like 'dsccore'} |
Select-Object -ExpandProperty HostProcessIdentifier

###
### Stop the process
###
Get-Process -Id $dscProcessID | Stop-Process
```

## <a name="using-debugmode"></a>Usando o DebugMode

Você pode configurar o Gerenciador de Configurações Local (LCM) de DSC para usar `DebugMode` para sempre limpar o cache quando o processo de host for reiniciado. Quando definido como **TRUE**, faz com que o mecanismo sempre recarregue o recurso de DSC do PowerShell. Depois de escrever seu recurso, você pode defini-lo como **FALSE** e o mecanismo será revertido para o comportamento de armazenamento em cache dos módulos.

Segue uma demonstração para mostrar como `DebugMode` pode atualizar o cache automaticamente. Primeiro, vamos examinar a configuração padrão:

```powershell
PS C:\> Get-DscLocalConfigurationManager
```

```output
AllowModuleOverwrite           : False
CertificateID                  :
ConfigurationID                :
ConfigurationMode              : ApplyAndMonitor
ConfigurationModeFrequencyMins : 30
Credential                     :
DebugMode                      : {None}
DownloadManagerCustomData      :
DownloadManagerName            :
LocalConfigurationManagerState : Ready
RebootNodeIfNeeded             : False
RefreshFrequencyMins           : 15
RefreshMode                    : PUSH
PSComputerName                 :
```

Pode-se ver que `DebugMode` foi definido como **"None"** .

Para configurar a demonstração `DebugMode`, use o seguinte recurso do PowerShell:

```powershell
function Get-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    return @{onlyProperty = Get-Content -Path "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"}
}
function Set-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    "1" | Out-File -PSPath "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"
}
function Test-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    return $false
}
```

Agora, crie uma configuração usando o recurso acima chamado `TestProviderDebugMode`:

```powershell
Configuration ConfigTestDebugMode
{
    Import-DscResource -Name TestProviderDebugMode
    Node localhost
    {
        TestProviderDebugMode test
        {
            onlyProperty = "blah"
        }
    }
}
ConfigTestDebugMode
```

Você verá que o conteúdo do arquivo: `$env:SystemDrive\OutputFromTestProviderDebugMode.txt` é **1**.

Agora, atualize o código do provedor usando o script a seguir:

```powershell
$newResourceOutput = Get-Random -Minimum 5 -Maximum 30
$content = @"
function Get-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    return @{onlyProperty = Get-Content -Path "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"}
}
function Set-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    "$newResourceOutput" | Out-File -PSPath C:\OutputFromTestProviderDebugMode.txt
}
function Test-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    return `$false
}
"@ | Out-File -FilePath "C:\Program Files\WindowsPowerShell\Modules\MyPowerShellModules\DSCResources\TestProviderDebugMode\TestProviderDebugMode.psm1
```

Esse script gera um número aleatório e atualiza o código do provedor correspondentemente. Com `DebugMode` definido como falso, o conteúdo do arquivo " **$env:SystemDrive\OutputFromTestProviderDebugMode.txt**" nunca é alterado.

Agora, defina `DebugMode` como **"ForceModuleImport"** no script de configuração:

```powershell
LocalConfigurationManager
{
    DebugMode = "ForceModuleImport"
}
```

Quando você executar novamente o script acima, verá que o conteúdo do arquivo é diferente em cada ocasião. (É possível executar `Get-DscConfiguration` para verificar). Abaixo está o resultado de duas execuções adicionais (os resultados podem ser diferentes quando você executar o script):

```powershell
PS C:\> Get-DscConfiguration -CimSession (New-CimSession localhost)

onlyProperty                            PSComputerName
------------                            --------------
20                                      localhost

PS C:\> Get-DscConfiguration -CimSession (New-CimSession localhost)

onlyProperty                            PSComputerName
------------                            --------------
14                                      localhost
```

## <a name="dsc-returns-unexpected-response-code-internalservererror-when-registering-with-windows-pull-server"></a>O DSC retorna "código de resposta InternalServerError inesperado" ao registrar com o Servidor de Pull do Windows

Ao aplicar uma metaconfiguração em um servidor para registrá-lo com uma instância do Servidor de Pull do Windows, você poderá encontrar o erro a seguir.

```PowerShell
Registration of the Dsc Agent with the server https://<serverfqdn>:8080/PSDSCPullServer.svc failed. The underlying error is: The attempt to register Dsc Agent with AgentId <ID> with the server 
https://<serverfqdn>:8080/PSDSCPullServer.svc/Nodes(AgentId='<ID>') returned unexpected response code InternalServerError. .
    + CategoryInfo          : InvalidResult: (root/Microsoft/...gurationManager:String) [], CimException
    + FullyQualifiedErrorId : RegisterDscAgentUnsuccessful,Microsoft.PowerShell.DesiredStateConfiguration.Commands.RegisterDscAgentCommand
    + PSComputerName        : <computername>
```

Isso pode ocorrer quando o certificado usado no servidor para criptografar o tráfego tem um CN (nome comum) diferente do nome DNS usado pelo nó para resolver a URL.
Atualize a instância do Servidor de Pull do Windows para usar um certificado com um nome corrigido.

## <a name="see-also"></a>Consulte Também

### <a name="concepts"></a>Conceitos

- [Criar recursos personalizados de configuração de estado desejado do Windows PowerShell](../resources/authoringResource.md)

### <a name="other-resources"></a>Outros recursos

- [Cmdlets de Configuração de Estado Desejado do Windows PowerShell](/powershell/module/psdesiredstateconfiguration/)
