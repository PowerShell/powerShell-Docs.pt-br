---
external help file: System.Management.Automation.dll-Help.xml
keywords: powershell, cmdlet
Locale: en-US
Module Name: Microsoft.PowerShell.Core
ms.date: 04/08/2020
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/start-job?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Start-Job
ms.openlocfilehash: 116e007cc28a91e3c97fd980cc27461932390b7c
ms.sourcegitcommit: 9b28fb9a3d72655bb63f62af18b3a5af6a05cd3f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/07/2020
ms.locfileid: "93193500"
---
# Start-Job

## SINOPSE
Inicia um trabalho em segundo plano do PowerShell.

## SYNTAX

### ComputerName (padrão)

```
Start-Job [-Name <String>] [-ScriptBlock] <ScriptBlock> [-Credential <PSCredential>]
 [-Authentication <AuthenticationMechanism>] [[-InitializationScript] <ScriptBlock>] [-RunAs32]
 [-PSVersion <Version>] [-InputObject <PSObject>] [-ArgumentList <Object[]>] [<CommonParameters>]
```

### Definitionname

```
Start-Job [-DefinitionName] <String> [[-DefinitionPath] <String>] [[-Type] <String>]
 [<CommonParameters>]
```

### FilePathComputerName

```
Start-Job [-Name <String>] [-Credential <PSCredential>] [-FilePath] <String>
 [-Authentication <AuthenticationMechanism>] [[-InitializationScript] <ScriptBlock>] [-RunAs32]
 [-PSVersion <Version>] [-InputObject <PSObject>] [-ArgumentList <Object[]>] [<CommonParameters>]
```

### LiteralFilePathComputerName

```
Start-Job [-Name <String>] [-Credential <PSCredential>] -LiteralPath <String>
 [-Authentication <AuthenticationMechanism>] [[-InitializationScript] <ScriptBlock>] [-RunAs32]
 [-PSVersion <Version>] [-InputObject <PSObject>] [-ArgumentList <Object[]>] [<CommonParameters>]
```

## DESCRIPTION

O `Start-Job` cmdlet inicia um trabalho em segundo plano do PowerShell no computador local.

Um trabalho em segundo plano do PowerShell executa um comando sem interagir com a sessão atual. Quando você inicia um trabalho em segundo plano, um objeto de trabalho retorna imediatamente, mesmo se o trabalho levar um tempo estendido para ser concluído. É possível continuar a trabalhar na sessão sem interrupção enquanto o trabalho é executado.

O objeto de trabalho contém informações úteis sobre o trabalho, mas não contém os resultados do trabalho.
Quando o trabalho for concluído, use o `Receive-Job` cmdlet para obter os resultados do trabalho. Para obter mais informações sobre trabalhos em segundo plano, consulte [about_Jobs](./About/about_Jobs.md).

Para executar um trabalho em segundo plano em um computador remoto, use o parâmetro **AsJob** que está disponível em muitos cmdlets ou use o `Invoke-Command` cmdlet para executar um `Start-Job` comando no computador remoto. Para obter mais informações, consulte [about_Remote_Jobs](./About/about_Remote_Jobs.md).

A partir do PowerShell 3,0, `Start-Job` o pode iniciar instâncias de tipos de trabalho personalizados, como trabalhos agendados. Para obter informações sobre como usar `Start-Job` o para iniciar trabalhos com tipos personalizados, consulte os documentos de ajuda para o recurso tipo de trabalho.

O diretório de trabalho padrão para trabalhos é codificado. O padrão do Windows é `$HOME\Documents` e no Linux ou MacOS o padrão é `$HOME` . O código de script em execução no trabalho em segundo plano precisa gerenciar o diretório de trabalho conforme necessário.

## EXEMPLOS

### Exemplo 1: iniciar um trabalho em segundo plano

Este exemplo inicia um trabalho em segundo plano que é executado no computador local.

```powershell
Start-Job -ScriptBlock { Get-Process -Name powershell }
```

```Output
Id  Name   PSJobTypeName   State     HasMoreData   Location    Command
--  ----   -------------   -----     -----------   --------    -------
1   Job1   BackgroundJob   Running   True          localhost   Get-Process -Name powershell
```

`Start-Job` usa o parâmetro **scriptblock** para executar `Get-Process` como um trabalho em segundo plano. O parâmetro **Name** especifica a localização de processos do PowerShell, `powershell` . As informações do trabalho são exibidas e o PowerShell retorna a um prompt enquanto o trabalho é executado em segundo plano.

Para exibir a saída do trabalho, use o `Receive-Job` cmdlet. Por exemplo, `Receive-Job -Id 1`.

### Exemplo 2: iniciar um trabalho usando Invoke-Command

Este exemplo executa um trabalho em vários computadores. O trabalho é armazenado em uma variável e é executado usando o nome da variável na linha de comando do PowerShell.

```powershell
$jobWRM = Invoke-Command -ComputerName (Get-Content -Path C:\Servers.txt) -ScriptBlock {
   Get-Service -Name WinRM } -JobName WinRM -ThrottleLimit 16 -AsJob
```

Um trabalho que usa `Invoke-Command` é criado e armazenado na `$jobWRM` variável. `Invoke-Command` usa o parâmetro **ComputerName** para especificar os computadores em que o trabalho é executado. `Get-Content` Obtém os nomes de servidor do `C:\Servers.txt` arquivo.

O parâmetro **scriptblock** especifica um comando que `Get-Service` Obtém o serviço **WinRM** . O parâmetro **JobName** especifica um nome amigável para o trabalho, **WinRM** . O parâmetro **ThrottleLimit** limita o número de comandos simultâneos a 16. O parâmetro **AsJob** inicia um trabalho em segundo plano que executa o comando nos servidores.

### Exemplo 3: obter informações do trabalho

Este exemplo obtém informações sobre um trabalho e exibe os resultados de um trabalho concluído que foi executado no computador local.

```powershell
$j = Start-Job -ScriptBlock { Get-WinEvent -Log System } -Credential Domain01\User01
$j | Select-Object -Property *
```

```Output
State         : Completed
HasMoreData   : True
StatusMessage :
Location      : localhost
Command       : Get-WinEvent -Log System
JobStateInfo  : Completed
Finished      : System.Threading.ManualResetEvent
InstanceId    : 27ce3fd9-40ed-488a-99e5-679cd91b9dd3
Id            : 18
Name          : Job18
ChildJobs     : {Job19}
PSBeginTime   : 8/8/2019 14:41:57
PSEndTime     : 8/8/2019 14:42:07
PSJobTypeName : BackgroundJob
Output        : {}
Error         : {}
Progress      : {}
Verbose       : {}
Debug         : {}
Warning       : {}
Information   : {}
```

`Start-Job` usa o parâmetro **scriptblock** para executar um comando que especifica `Get-WinEvent` para obter o log do **sistema** . O parâmetro **Credential** especifica uma conta de usuário de domínio com permissão para executar o trabalho no computador. O objeto de trabalho é armazenado na `$j` variável.

O objeto na `$j` variável é enviado ao pipeline para `Select-Object` . O parâmetro **Property** especifica um asterisco ( `*` ) para exibir todas as propriedades do objeto de trabalho.

### Exemplo 4: executar um script como um trabalho em segundo plano

Neste exemplo, um script no computador local é executado como um trabalho em segundo plano.

```powershell
Start-Job -FilePath C:\Scripts\Sample.ps1
```

`Start-Job` usa o parâmetro **FilePath** para especificar um arquivo de script armazenado no computador local.

### Exemplo 5: obter um processo usando um trabalho em segundo plano

Este exemplo usa um trabalho em segundo plano para obter um processo especificado por nome.

```powershell
Start-Job -Name PShellJob -ScriptBlock { Get-Process -Name PowerShell }
```

`Start-Job` usa o parâmetro **Name** para especificar um nome de trabalho amigável, **PShellJob** . O parâmetro **scriptblock** especifica `Get-Process` para obter processos com o nome **PowerShell** .

### Exemplo 6: coletar e salvar dados usando um trabalho em segundo plano

Este exemplo inicia um trabalho que coleta uma grande quantidade de dados de mapa e, em seguida, salva-o em um `.tif` arquivo.

```powershell
Start-Job -Name GetMappingFiles -InitializationScript {Import-Module MapFunctions} -ScriptBlock {
   Get-Map -Name * | Set-Content -Path D:\Maps.tif } -RunAs32
```

`Start-Job` usa o parâmetro **Name** para especificar um nome de trabalho amigável, **GetMappingFiles** . O parâmetro **initializationScript** executa um bloco de script que importa o módulo **MapFunctions** . O parâmetro **scriptblock** executa `Get-Map` e `Set-Content` salva os dados no local especificado pelo parâmetro **Path** . O parâmetro **RunAs32** executa o processo como 32 bits, mesmo em um sistema operacional de 64 bits.

### Exemplo 7: passar entrada para um trabalho em segundo plano

Este exemplo usa a `$input` variável automática para processar um objeto de entrada. Use `Receive-Job` para exibir a saída do trabalho.

```powershell
Start-Job -ScriptBlock { Get-Content $input } -InputObject "C:\Servers.txt"
Receive-Job -Name Job45 -Keep
```

```Output
Server01
Server02
Server03
Server04
```

`Start-Job` usa o parâmetro **scriptblock** para executar `Get-Content` com a `$input` variável automática. A `$input` variável obtém objetos do parâmetro **InputObject** . `Receive-Job` usa o parâmetro **Name** para especificar o trabalho e gera os resultados. O parâmetro **Keep** salva a saída do trabalho para que possa ser exibido novamente durante a sessão do PowerShell.

### Exemplo 8: usar o parâmetro ArgumentList para especificar uma matriz

Este exemplo usa o parâmetro **ArgumentList** para especificar uma matriz de argumentos. A matriz é uma lista separada por vírgulas de nomes de processo.

```powershell
Start-Job -ScriptBlock { Get-Process -Name $args } -ArgumentList powershell, pwsh, notepad
```

```Output
Id     Name      PSJobTypeName   State       HasMoreData     Location     Command
--     ----      -------------   -----       -----------     --------     -------
1      Job1      BackgroundJob   Running     True            localhost    Get-Process -Name $args
```

O `Start-Job` cmdlet usa o parâmetro **scriptblock** para executar um comando. `Get-Process` usa o parâmetro **Name** para especificar a variável automática `$args` . O parâmetro **ArgumentList** passa a matriz de nomes de processo para `$args` . Os nomes de processo PowerShell, pwsh e Notepad são processos em execução no computador local.

Para exibir a saída do trabalho, use o `Receive-Job` cmdlet. Por exemplo, `Receive-Job -Id 1`.

## PARAMETERS

### -ArgumentList

Especifica uma matriz de argumentos, ou valores de parâmetro, para o script que é especificado pelo parâmetro **FilePath** ou um comando especificado com o parâmetro **scriptblock** .

Os argumentos devem ser passados para **ArgumentList** como argumento de matriz de dimensão única. Por exemplo, uma lista separada por vírgulas. Para obter mais informações sobre o comportamento de **ArgumentList** , consulte [about_Splatting](about/about_Splatting.md#splatting-with-arrays).

```yaml
Type: System.Object[]
Parameter Sets: ComputerName, LiteralFilePathComputerName, FilePathComputerName
Aliases: Args

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Autenticação

Especifica o mecanismo usado para autenticar as credenciais do usuário.

Os valores aceitáveis para esse parâmetro são os seguintes:

- Padrão
- Básico
- CredSSP
- Digest
- Kerberos
- Negotiate
- NegotiateWithImplicitCredential

O valor padrão é Default.

A autenticação CredSSP está disponível somente no Windows Vista, no Windows Server 2008 e em versões posteriores do sistema operacional Windows.

Para obter mais informações sobre os valores desse parâmetro, consulte [AuthenticationMechanism](/dotnet/api/system.management.automation.runspaces.authenticationmechanism).

> [!CAUTION]
> A autenticação CredSSP (Credencial Security Support Provider), na qual as credenciais do usuário são passadas a um computador remoto para autenticação, foi projetada para comandos que exijam autenticação em mais de um recurso, como acessar um compartilhamento de rede remota. Esse mecanismo aumenta o risco de segurança da operação remota. Se o computador remoto estiver comprometido, as credenciais que são passadas a ele podem ser usadas para controlar a sessão de rede.

```yaml
Type: System.Management.Automation.Runspaces.AuthenticationMechanism
Parameter Sets: ComputerName, LiteralFilePathComputerName, FilePathComputerName
Aliases:
Accepted values: Default, Basic, Negotiate, NegotiateWithImplicitCredential, Credssp, Digest, Kerberos

Required: False
Position: Named
Default value: Default
Accept pipeline input: False
Accept wildcard characters: False
```

### -Credential

Especifica uma conta de usuário que tem permissão para executar esta ação. Se o parâmetro **Credential** não for especificado, o comando usará as credenciais do usuário atual.

Digite um nome de usuário, como **User01** ou **Domínio01 \ Usuário01** , ou insira um objeto **PSCredential** gerado pelo `Get-Credential` cmdlet. Se você digitar um nome de usuário, você será solicitado a inserir a senha.

As credenciais são armazenadas em um objeto [PSCredential](/dotnet/api/system.management.automation.pscredential) e a senha é armazenada como uma [SecureString](/dotnet/api/system.security.securestring).

> [!NOTE]
> Para obter mais informações sobre a proteção de dados **SecureString** , consulte [quão seguro é a SecureString?](/dotnet/api/system.security.securestring#how-secure-is-securestring).

```yaml
Type: System.Management.Automation.PSCredential
Parameter Sets: ComputerName, LiteralFilePathComputerName, FilePathComputerName
Aliases:

Required: False
Position: Named
Default value: Current user
Accept pipeline input: False
Accept wildcard characters: False
```

### -Definitionname

Especifica o nome da definição do trabalho que este cmdlet inicia. Use este parâmetro para iniciar tipos de trabalho personalizados que têm um nome de definição, como trabalhos agendados.

Quando você usa `Start-Job` o para iniciar uma instância de um trabalho agendado, o trabalho é iniciado imediatamente, independentemente dos gatilhos de trabalho ou das opções de trabalho. A instância de trabalho resultante é um trabalho agendado, mas não é salva em disco, como trabalhos agendados disparados. Você não pode usar o parâmetro **ArgumentList** de `Start-Job` para fornecer valores para parâmetros de scripts que são executados em um trabalho agendado. Para obter mais informações, consulte [about_Scheduled_Jobs](../PSScheduledJob/About/about_Scheduled_Jobs.md).

Esse parâmetro foi introduzido no PowerShell 3,0.

```yaml
Type: System.String
Parameter Sets: DefinitionName
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -DefinitionPath

Especifica o caminho da definição para o trabalho que este cmdlet inicia. Insira o caminho de definição. A concatenação dos valores dos parâmetros **DefinitionPath** e **definitionname** é o caminho totalmente qualificado da definição de trabalho. Use este parâmetro para iniciar tipos de trabalho personalizados que têm um caminho de definição, como trabalhos agendados.

Para trabalhos agendados, o valor do parâmetro **DefinitionPath** é `$home\AppData\Local\Windows\PowerShell\ScheduledJob` .

Esse parâmetro foi introduzido no PowerShell 3,0.

```yaml
Type: System.String
Parameter Sets: DefinitionName
Aliases:

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -FilePath

Especifica um script local que `Start-Job` é executado como um trabalho em segundo plano. Insira o caminho e o nome de arquivo do script ou use o pipeline para o qual enviar um caminho de script `Start-Job` . O script deve estar no computador local ou em uma pasta que o computador local possa acessar.

Quando você usa esse parâmetro, o PowerShell converte o conteúdo do arquivo de script especificado em um bloco de script e executa o bloco de script como um trabalho em segundo plano.

```yaml
Type: System.String
Parameter Sets: FilePathComputerName
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -InitializationScript

Especifica os comandos que são executados antes do trabalho ser iniciado. Para criar um bloco de script, coloque os comandos entre chaves ( `{}` ).

Use esse parâmetro para preparar a sessão na qual o trabalho é executado. Por exemplo, você pode usá-lo para adicionar funções, snap-ins e módulos à sessão.

```yaml
Type: System.Management.Automation.ScriptBlock
Parameter Sets: ComputerName, LiteralFilePathComputerName, FilePathComputerName
Aliases:

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -InputObject

Especifica a entrada para o comando. Insira uma variável que contenha os objetos ou digite um comando ou uma expressão que gere os objetos.

No valor do parâmetro **scriptblock** , use a `$input` variável automática para representar os objetos de entrada.

```yaml
Type: System.Management.Automation.PSObject
Parameter Sets: ComputerName, LiteralFilePathComputerName, FilePathComputerName
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -LiteralPath

Especifica um script local que este cmdlet executa como um trabalho em segundo plano. Insira o caminho de um script no computador local.

`Start-Job` usa o valor do parâmetro **LiteralPath** exatamente como ele é digitado. Nenhum caractere é interpretado como caractere curinga. Se o caminho incluir caracteres de escape, coloque-o entre aspas simples. Aspas simples instruem o PowerShell a não interpretar nenhum caractere como sequências de escape.

```yaml
Type: System.String
Parameter Sets: LiteralFilePathComputerName
Aliases: PSPath

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name

Especifica um nome amigável para o novo trabalho. Você pode usar o nome para identificar o trabalho para outros cmdlets de trabalho, como o `Stop-Job` cmdlet.

O nome amigável padrão é `Job#` , em que `#` é um número ordinal que é incrementado para cada trabalho.

```yaml
Type: System.String
Parameter Sets: ComputerName, LiteralFilePathComputerName, FilePathComputerName
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -PSVersion

Especifica uma versão. `Start-Job` executa o trabalho com a versão do PowerShell. Os valores aceitáveis para esse parâmetro são: `2.0` e `3.0` .

Esse parâmetro foi introduzido no PowerShell 3,0.

```yaml
Type: System.Version
Parameter Sets: ComputerName, LiteralFilePathComputerName, FilePathComputerName
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -RunAs32

Indica que `Start-Job` o executa o trabalho em um processo de 32 bits. **RunAs32** força o trabalho a ser executado em um processo de 32 bits, mesmo em um sistema operacional de 64 bits.

Nas versões de 64 bits do Windows 7 e do Windows Server 2008 R2, quando o `Start-Job` comando inclui o parâmetro **RunAs32** , você não pode usar o parâmetro **Credential** para especificar as credenciais de outro usuário.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: ComputerName, LiteralFilePathComputerName, FilePathComputerName
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -ScriptBlock

Especifica os comandos a executar no trabalho em segundo plano. Para criar um bloco de script, coloque os comandos entre chaves ( `{}` ). Use a `$input` variável automática para acessar o valor do parâmetro **InputObject** . Este parâmetro é necessário.

```yaml
Type: System.Management.Automation.ScriptBlock
Parameter Sets: ComputerName
Aliases: Command

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Type

Especifica o tipo personalizado para trabalhos iniciados por `Start-Job` . Insira um nome de tipo de trabalho personalizado como PSScheduledJob para trabalhos agendados, ou PSWorkflowJob para tarefas de fluxo de trabalho. Esse parâmetro não é válido para trabalhos em segundo plano padrão.

Esse parâmetro foi introduzido no PowerShell 3,0.

```yaml
Type: System.String
Parameter Sets: DefinitionName
Aliases:

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters

Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable. Para obter mais informações, confira [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## ENTRADAS

### System.String

Você pode usar o pipeline para enviar um objeto com a propriedade **Name** para o parâmetro **Name** . Por exemplo, você pode canalizar um objeto **FileInfo** de `Get-ChildItem` para `Start-Job` .

## SAÍDAS

### System. Management. Automation. PSRemotingJob

`Start-Job` Retorna um objeto **PSRemotingJob** que representa o trabalho que ele iniciou.

## OBSERVAÇÕES

Para ser executado em segundo plano, `Start-Job` o é executado em sua própria sessão na sessão atual. Quando você usa o `Invoke-Command` cmdlet para executar um `Start-Job` comando em uma sessão em um computador remoto, `Start-Job` o é executado em uma sessão na sessão remota.

## LINKS RELACIONADOS

[about_Arrays](./about/about_arrays.md)

[about_Automatic_Variables](./about/about_automatic_variables.md)

[about_Jobs](./About/about_Jobs.md)

[about_Job_Details](./About/about_Job_Details.md)

[about_Remote_Jobs](./About/about_Remote_Jobs.md)

[Get-Job](Get-Job.md)

[Invoke-Command](Invoke-Command.md)

[Receive-Job](Receive-Job.md)

[Remove-Job](Remove-Job.md)

[Resume-Job](Resume-Job.md)

[Stop-Job](Stop-Job.md)

[Suspend-Job](Suspend-Job.md)

[Wait-Job](Wait-Job.md)
