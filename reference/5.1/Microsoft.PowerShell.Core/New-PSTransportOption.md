---
external help file: System.Management.Automation.dll-Help.xml
keywords: powershell, cmdlet
Locale: en-US
Module Name: Microsoft.PowerShell.Core
ms.date: 06/09/2017
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/new-pstransportoption?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: New-PSTransportOption
ms.openlocfilehash: 9257c0a1829cc9cc85029f7c6fdc8e61b0ed7e56
ms.sourcegitcommit: 37abf054ad9eda8813be8ff4487803b10e1842ef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "93194876"
---
# New-PSTransportOption

## SINOPSE

Cria um objeto que contém opções avançadas para uma configuração de sessão.

## SYNTAX

```
New-PSTransportOption [-MaxIdleTimeoutSec <Int32>] [-ProcessIdleTimeoutSec <Int32>] [-MaxSessions <Int32>]
 [-MaxConcurrentCommandsPerSession <Int32>] [-MaxSessionsPerUser <Int32>] [-MaxMemoryPerSessionMB <Int32>]
 [-MaxProcessesPerSession <Int32>] [-MaxConcurrentUsers <Int32>] [-IdleTimeoutSec <Int32>]
 [-OutputBufferingMode <OutputBufferingMode>] [<CommonParameters>]
```

## DESCRIPTION

O cmdlet **New-PSTransportOption** cria um objeto que contém opções de transporte para configurações de sessão.
Você pode usar o objeto como o valor do parâmetro *TransportOption* de cmdlets que criam ou alteram uma configuração de sessão, como os cmdlets Register-PSSessionConfiguration e Set-PSSessionConfiguration.

Você também pode alterar as configurações de opção de transporte editando os valores das propriedades de configuração de sessão na unidade WSMan:.
Para obter mais informações, consulte provedor WSMan.

As opções de configuração de sessão representam os valores de sessão definidos no lado do servidor ou a extremidade de recebimento de uma conexão remota.
O lado do cliente, ou o término do envio da conexão, pode definir valores de opção de sessão quando a sessão é criada ou quando o cliente se desconecta do ou se reconecta à sessão.
Salvo indicação em contrário, quando há conflito de valores na configuração, prevalecem os valores do lado do cliente.
No entanto, os valores do lado do cliente não podem violar valores máximos e as cotas definidas na configuração da sessão.

Sem parâmetros, **New-PSTransportOption** gera um objeto de opção de transporte que tem valores nulos para todas as opções.
Se um parâmetro for omitido, o objeto tem um valor nulo para a propriedade que representa o parâmetro.
Um valor nulo não afeta a configuração da sessão.

Para obter mais informações sobre as opções de sessão, consulte New-PSSessionOption.
Para obter mais informações sobre configurações de sessão, consulte [about_Session_Configurations](About/about_Session_Configurations.md).

Este cmdlet foi introduzido no Windows PowerShell 3.0.

## EXEMPLOS

### Exemplo 1: gerar uma opção de transporte padrão

```
PS C:\> New-PSTransportOption
ProcessIdleTimeoutSec           :
MaxIdleTimeoutSec               :
MaxSessions                     :
MaxConcurrentCommandsPerSession :
MaxSessionsPerUser              :
MaxMemoryPerSessionMB           :
MaxProcessesPerSession          :
MaxConcurrentUsers              :
IdleTimeoutSec                  :
OutputBufferingMode             :
```

Esse comando executa o **New-PSTransportOption** sem parâmetros.
A saída mostra que o cmdlet gera um objeto de opção de transporte que tem valores nulos para todas as propriedades.

### Exemplo 2: obter opções de configuração de sessão

```
The first command uses the **New-PSTransportOption** cmdlet to create a transport options object, which it saves in the $t variable. The command uses the *MaxSessions* parameter to increase the maximum number of sessions to 40.
PS C:\> $t = New-PSTransportOption -MaxSessions 40

The second command uses the **Register-PSSessionConfiguration** cmdlet create the ITTasks session configuration. The command uses the *TransportOption* parameter to specify the transport options object in the $t variable.
PS C:\> Register-PSSessionConfiguration -Name ITTasks -TransportOption $t

The third command uses the Get-PSSessionConfiguration cmdlet to get the ITTasks session configurations and the Format-List cmdlet to display all of the properties of the session configuration object in a list. The output shows that the value of the **MaxShells** property of the session configuration is 40.
PS C:\> Get-PSSessionConfiguration -Name ITTasks | Format-List -Property *
Architecture                  : 64
Filename                      : %windir%\system32\pwrshplugin.dll
ResourceUri                   : http://schemas.microsoft.com/powershell/ITTasks
MaxConcurrentCommandsPerShell : 1000
UseSharedProcess              : false
ProcessIdleTimeoutSec         : 0
xmlns                         : http://schemas.microsoft.com/wbem/wsman/1/config/PluginConfiguration
MaxConcurrentUsers            : 5
lang                          : en-US
SupportsOptions               : true
ExactMatch                    : true
RunAsUser                     :
IdleTimeoutms                 : 7200000
PSVersion                     : 3.0
OutputBufferingMode           : Block
AutoRestart                   : false
MaxShells                     : 40
MaxMemoryPerShellMB           : 1024
MaxIdleTimeoutms              : 43200000
SDKVersion                    : 2
Name                          : ITTasks
XmlRenderingType              : text
Capability                    : {Shell}
RunAsPassword                 :
MaxProcessesPerShell          : 15
Enabled                       : True
MaxShellsPerUser              : 25
Permission                    :
```

Este exemplo mostra como usar um objeto de opções de transporte para definir opções de configuração de sessão.

### Exemplo 3: definindo uma opção de transporte

```
The first command uses the **New-PSTransportOption** cmdlet to create a transport option object. The command uses the *IdleTimeoutSec* parameter to set the **IdleTimeoutSec** property value of the object to one hour (3600 seconds). The command saves the transport objects object in the $t variable.
PS C:\> $t = New-PSTransportOption -IdleTimeoutSec 3600

The second command uses the Set-PSSessionConfiguration cmdlet to change the transport options of the ITTasks session configuration. The command uses the *TransportOption* parameter to specify the transport options object in the $t variable.
PS C:\> Set-PSSessionConfiguration -Name ITTasks -TransportOption $t

The third command uses the New-PSSession cmdlet to create the MyITTasks session on the local computer. The command uses the **ConfigurationName** property to specify the ITTasks session configuration. The command saves the session in the $s variable.Notice that the command does not use the *SessionOption* parameter of **New-PSSession** to set a custom idle time-out for the session. If it did, the idle time-out value set in the session option would take precedence over the idle time-out set in the session configuration.
PS C:\> $s = New-PSSession -Name MyITTasks -ConfigurationName ITTasks

The fourth command uses the Format-List cmdlet to display all properties of the session in the $s variable in a list. The output shows that the session has an idle time-out of one hour (360,000 milliseconds).
PS C:\> $s | Format-List -Property *
State                  : Opened
IdleTimeout            : 3600000
OutputBufferingMode    : Block
ComputerName           : localhost
ConfigurationName      : ITTasks
InstanceId             : 4110c3f5-68ea-40fa-9bbf-04a433dbb02d
Id                     : 1
Name                   : MyITTasks
Availability           : Available
ApplicationPrivateData : {PSVersionTable}
Runspace               : System.Management.Automation.RemoteRunspace
```

Este comando mostra o efeito de definir uma opção de transporte em uma configuração de sessão nas sessões que usam a configuração de sessão.

## PARAMETERS

### -IdleTimeoutSec

Determina por quanto tempo cada sessão permanecerá aberta se o computador remoto não receber nenhuma comunicação do computador local.
Isso inclui o sinal de pulsação.
Quando o intervalo expira, a sessão é fechada.

O valor de tempo limite ocioso é de importância significativa quando o usuário pretende desconectar e reconectar-se a uma sessão.
O usuário poderá se reconectar somente se a sessão não tiver expirado.

O parâmetro *IdleTimeoutSec* corresponde à propriedade **IdleTimeoutMs** de uma configuração de sessão.

Insira um valor em segundos.
O valor padrão é 7200 (2 horas).
O valor mínimo é 60 (1 minuto).
O máximo é o valor da propriedade **IdleTimeout** dos objetos shell na configuração do WSMan ( `WSMan:\\\<ComputerName\>\Shell\IdleTimeout` ).
O valor padrão é 7200000 milissegundos (2 horas).

Se um valor de tempo limite ocioso for definido nas opções de sessão e na configuração de sessão, o valor definido nas opções de sessão terá precedência, mas não poderá exceder o valor da propriedade **MaxIdleTimeoutMs** da configuração de sessão.
Para definir o valor da propriedade **MaxIdleTimeoutMs** , use o parâmetro *MaxIdleTimeoutSec* .

```yaml
Type: System.Nullable`1[System.Int32]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -MaxConcurrentCommandsPerSession

Limita o número de comandos que podem ser executados ao mesmo tempo em cada sessão para o valor especificado.
O valor padrão é 1000.

O parâmetro *MaxConcurrentCommandsPerSession* corresponde à propriedade **MaxConcurrentCommandsPerShell** de uma configuração de sessão.

```yaml
Type: System.Nullable`1[System.Int32]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -MaxConcurrentUsers

Limita o número de usuários que podem executar comandos ao mesmo tempo em cada sessão para o valor especificado.
O valor padrão é 5.

```yaml
Type: System.Nullable`1[System.Int32]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -MaxIdleTimeoutSec

Limita o tempo limite de ociosidade definido para cada sessão ao valor especificado.
O valor padrão é \[ int \] :: MaxValue (aproximadamente 25 dias).

O valor de tempo limite ocioso é de importância significativa quando o usuário pretende desconectar e reconectar-se a uma sessão.
O usuário poderá se reconectar somente se a sessão não tiver expirado.

O parâmetro *MaxIdleTimeoutSec* corresponde à propriedade **MaxIdleTimeoutMs** de uma configuração de sessão.

```yaml
Type: System.Nullable`1[System.Int32]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -MaxMemoryPerSessionMB

Limita a memória usada por cada sessão para o valor especificado.
Insira um valor em megabytes.
O valor padrão é 1024 MB (1 GB).

O parâmetro *MaxMemoryPerSessionMB* corresponde à propriedade **MaxMemoryPerShellMB** de uma configuração de sessão.

```yaml
Type: System.Nullable`1[System.Int32]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -MaxProcessesPerSession

Limita o número de processos em execução em cada sessão para o valor especificado.
O valor padrão é 15.

O parâmetro *MaxProcessesPerSession* corresponde à propriedade **MaxProcessesPerShell** de uma configuração de sessão.

```yaml
Type: System.Nullable`1[System.Int32]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -MaxSessions

Especifica o número de sessões que usam a configuração de sessão.
O valor padrão é 25.

O parâmetro *MaxSessions* corresponde à propriedade **MaxShells** de uma configuração de sessão.

```yaml
Type: System.Nullable`1[System.Int32]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -MaxSessionsPerUser

Limita o número de sessões que usam a configuração de sessão e são executadas com as credenciais de um determinado usuário para o valor especificado.
O valor padrão é 25.

Ao especificar esse valor, considere que muitos usuários podem estar usando as credenciais de um usuário executar como.

O parâmetro *MaxSessionsPerUser* corresponde à propriedade **MaxShellsPerUser** de uma configuração de sessão.

```yaml
Type: System.Nullable`1[System.Int32]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -OutputBufferingMode

Determina como a saída do comando é gerenciada em sessões desconectadas quando o buffer de saída fica cheio.
Os valores aceitáveis para esse parâmetro são:

- Bloquear.
Quando o buffer de saída está cheio, a execução é suspensa até que o buffer esteja limpo.
- Drop.
Quando o buffer de saída está cheio, a execução continua.
Conforme uma nova saída é salva, a saída mais antiga é descartada.
- nenhuma.
Nenhum modo de buffering de saída é especificado.

O valor padrão da propriedade **OutputBufferingMode** de sessões é Block.

```yaml
Type: System.Nullable`1[System.Management.Automation.Runspaces.OutputBufferingMode]
Parameter Sets: (All)
Aliases:
Accepted values: None, Drop, Block

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -ProcessIdleTimeoutSec

Limita o tempo limite para cada processo de host para o valor especificado.
O valor padrão, 0, significa que não há nenhum valor de tempo limite para o processo.

Outras configurações de sessão têm valores de tempo limite por processo.
Por exemplo, a configuração de sessão do **Microsoft. PowerShell. Workflow** tem um valor de tempo limite por processo de 28800 segundos (8 horas).

```yaml
Type: System.Nullable`1[System.Int32]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### CommonParameters
Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable. Para obter mais informações, confira [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## ENTRADAS

### Nenhum

Não é possível redirecionar a entrada para este cmdlet.

## SAÍDAS

### Microsoft. PowerShell. Commands. WSManConfigurationOption

## OBSERVAÇÕES

- As propriedades de um objeto de configuração de sessão variam de acordo com as opções definidas para a configuração da sessão e os valores dessas opções. Além disso, as configurações de sessão que usam um arquivo de configuração de sessão têm propriedades adicionais.

## LINKS RELACIONADOS

[New-PSSession](New-PSSession.md)

[New-PSSessionOption](New-PSSessionOption.md)

[Register-PSSessionConfiguration](Register-PSSessionConfiguration.md)

[Set-PSSessionConfiguration](Set-PSSessionConfiguration.md)
