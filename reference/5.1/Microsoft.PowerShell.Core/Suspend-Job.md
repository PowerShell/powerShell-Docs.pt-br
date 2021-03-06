---
external help file: System.Management.Automation.dll-Help.xml
keywords: powershell, cmdlet
Locale: en-US
Module Name: Microsoft.PowerShell.Core
ms.date: 06/09/2017
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/suspend-job?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Suspend-Job
ms.openlocfilehash: 9b18782fae77fa0776aa2cfaa39b74a2292099d9
ms.sourcegitcommit: 2c311274ce721cd1072dcf2dc077226789e21868
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2020
ms.locfileid: "94388457"
---
# Suspend-Job

## SINOPSE
Interrompe temporariamente tarefas de fluxo de trabalho.

## SYNTAX

### SessionIdParameterSet (padrão)

```
Suspend-Job [-Force] [-Wait] [-Id] <Int32[]> [-WhatIf] [-Confirm] [<CommonParameters>]
```

### JobParameterSet

```
Suspend-Job [-Job] <Job[]> [-Force] [-Wait] [-WhatIf] [-Confirm] [<CommonParameters>]
```

### NameParameterSet

```
Suspend-Job [-Force] [-Wait] [-Name] <String[]> [-WhatIf] [-Confirm] [<CommonParameters>]
```

### InstanceIdParameterSet

```
Suspend-Job [-Force] [-Wait] [-InstanceId] <Guid[]> [-WhatIf] [-Confirm] [<CommonParameters>]
```

### FilterParameterSet

```
Suspend-Job [-Force] [-Wait] [-Filter] <Hashtable> [-WhatIf] [-Confirm] [<CommonParameters>]
```

### StateParameterSet

```
Suspend-Job [-Force] [-Wait] [-State] <JobState> [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION

O `Suspend-Job` cmdlet suspende trabalhos de fluxo de trabalho. Suspender significa interromper temporariamente ou pausar um trabalho de fluxo de trabalhos. Este cmdlet permite que os usuários que estão executando fluxos de trabalho suspendam o fluxo de trabalho. Ele complementa a atividade suspender fluxo de trabalho https://go.microsoft.com/fwlink/?LinkId=267141 , que é um comando no fluxo de trabalho que suspende o fluxo de trabalho.

O `Suspend-Job` cmdlet funciona apenas em trabalhos de fluxo de trabalho. Ele não funciona em trabalhos em segundo plano padrão, como os que são iniciados usando o `Start-Job` cmdlet.

Para identificar uma tarefa de fluxo de trabalho, procure um valor de PSWorkflowJob na propriedade **PSJobTypeName** do trabalho. Para determinar se um determinado tipo de trabalho personalizado dá suporte ao `Suspend-Job` cmdlet, consulte os tópicos da ajuda para o tipo de trabalho personalizado.

Quando você suspende uma tarefa de fluxo de trabalho, essa tarefa é executada até o próximo ponto de verificação, suspendida e então retorna imediatamente como resultado um objeto de tarefa de fluxo de trabalho. Para aguardar a suspensão ser concluída antes de obter o trabalho, use o parâmetro **Wait** do `Suspend-Job` ou o `Wait-Job` cmdlet. Quando a tarefa de fluxo de trabalho é suspensa, o valor da propriedade **State** do trabalho é suspenso.

Suspender corretamente o trabalho depende dos pontos de verificação. O estado, os metadados e a saída atuais do trabalho são salvos no ponto de verificação, de modo que o trabalho do Workflow possa ser retomado sem perda de estado ou dados. Se o trabalho do Workflow não tiver pontos de verificação, ele não poderá ser suspenso corretamente. Para adicionar pontos de verificação a um fluxo de trabalho em execução, use o parâmetro comum de fluxo de trabalho **PSPersist**. Você pode usar o parâmetro **Force** para suspender qualquer trabalho de workflow imediatamente e para suspender um trabalho de workflow que não tem pontos de verificação, mas a ação pode causar perda de estado e dados.

Antes de você usar um cmdlet de trabalho em um tipo de trabalho personalizado, como um trabalho de Workflow ( **PSWorkflowJob** ), importe o módulo que dá suporte ao tipo de trabalho personalizado, seja usando o `Import-Module` cmdlet ou usando um cmdlet no módulo.

Este cmdlet foi introduzido no Windows PowerShell 3.0.

## EXEMPLOS

### Exemplo 1: suspender uma tarefa de fluxo de trabalho por nome

Este exemplo mostra como suspender uma tarefa de fluxo de trabalho.

O primeiro comando cria o `Get-SystemLog` fluxo de trabalho. O fluxo de trabalho usa a `CheckPoint-Workflow` atividade para definir um ponto de verificação no fluxo de trabalho.

O segundo comando usa o parâmetro **AsJob** , que é comum a todos os fluxos de trabalho para executar o `Get-SystemLog` Workflow como uma tarefa em segundo plano. O comando usa o parâmetro comum de fluxo de trabalho **JobName** para especificar um nome amigável para a tarefa de fluxo de trabalho.

O terceiro comando usa o `Get-Job` cmdlet para obter o `Get-SystemLogJob` trabalho de Workflow. A saída mostra que o valor da propriedade **PSJobTypeName** é PSWorkflowJob.

O quarto comando usa o `Suspend-Job` cmdlet para suspender o `Get-SystemLogJob` trabalho. O trabalho é executado até o ponto de verificação e então é suspenso.

```
#Sample WorkflowWorkflow Get-SystemLog
{
    $Events = Get-WinEvent -LogName System
    CheckPoint-Workflow
    InlineScript {\\Server01\Scripts\Analyze-SystemEvents.ps1 -Events $Events}
}

PS C:\> Get-SystemLog -AsJob -JobName "Get-SystemLogJob"

PS C:\> Get-Job -Name Get-SystemLogJob
Id     Name              PSJobTypeName   State       HasMoreData     Location   Command
--     ----              -------------   -----       -----------     --------   -------
4      Get-SystemLogJob  PSWorkflowJob   Running     True            localhost   Get-SystemLog

PS C:\> Suspend-Job -Name Get-SystemLogJob
Id     Name              PSJobTypeName   State       HasMoreData     Location   Command
--     ----              -------------   -----       -----------     --------   -------
4      Get-SystemLogJob  PSWorkflowJob   Suspended   True            localhost   Get-SystemLog
```


### Exemplo 2: suspender e retomar um trabalho de Workflow

Este exemplo mostra como suspender e retomar uma tarefa de fluxo de trabalho.

O primeiro comando suspende o trabalho LogWorkflowJob. O comando retorna imediatamente. A saída mostra que a tarefa de fluxo de trabalho ainda está em execução, mesmo que esteja sendo suspensa.

O segundo comando usa o `Get-Job` cmdlet para obter o trabalho LogWorkflowJob. A saída mostra que a tarefa de fluxo de trabalho foi suspensa com êxito.

O terceiro comando usa o `Get-Job` cmdlet para obter o trabalho LogWorkflowJob e o `Resume-Job` cmdlet para retomá-lo. A saída mostra que a tarefa de fluxo de trabalho foi retomada com êxito e está agora sendo executada.

```
PS C:\> Suspend-Job -Name LogWorkflowJob
Id     Name          PSJobTypeName      State         HasMoreData     Location             Command
--     ----          -------------      -----         -----------     --------             -------
67     LogflowJob    PSWorkflowJob      Running       True            localhost            LogWorkflow

PS C:\> Get-Job -Name LogWorkflowJob
Id     Name          PSJobTypeName      State         HasMoreData     Location             Command
--     ----          -------------      -----         -----------     --------             -------
67     LogflowJob    PSWorkflowJob      Suspended     True            localhost            LogWorkflow

PS C:\> Get-Job -Name LogWorkflowJob | Resume-Job
Id     Name          PSJobTypeName      State         HasMoreData     Location             Command
--     ----          -------------      -----         -----------     --------             -------
67     LogflowJob    PSWorkflowJob      Running       True            localhost            LogWorkflow
```


### Exemplo 3: suspender uma tarefa de fluxo de trabalho em um computador remoto

```
PS C:\> Invoke-Command -ComputerName Srv01 -Scriptblock {Suspend-Job -Filter @{CustomID="031589"}
```

Esse comando usa o `Invoke-Command` cmdlet para suspender um trabalho de fluxo de trabalhos no computador remoto Srv01. O valor do parâmetro de **filtro** é uma tabela de hash que especifica um valor personalizado.
Este **CustomID** é composto de metadados do trabalho ( **PSPrivateMetadata** ).

### Exemplo 4: aguardar a suspensão do trabalho de fluxo

```
PS C:\> Suspend-Job VersionCheck -Wait
Id     Name          PSJobTypeName      State         HasMoreData     Location             Command
--     ----          -------------      -----         -----------     --------             -------
 5     VersionCheck  PSWorkflowJob      Suspended     True            localhost            LogWorkflow
```

Este comando suspende a tarefa de fluxo de trabalho VersionCheck. O comando usa o parâmetro **Wait** para aguardar até a tarefa de fluxo de trabalho ser suspensa. Quando a tarefa de fluxo de trabalho é executada no próximo ponto de verificação e é suspensa, o comando é concluído e retorna o objeto de trabalho.

### Exemplo 5: forçar uma tarefa de fluxo de trabalho a suspender

```
PS C:\> Suspend-Job Maintenance -Force
```

Este comando suspende à força a tarefa de fluxo de trabalho Maintenance. O trabalho de manutenção não tem pontos de verificação. Ele não pode ser suspenso corretamente e pode não ser retomado corretamente.

## PARAMETERS

### -Filter

Especifica uma tabela de hash de condições. Esse cmdlet suspende trabalhos que atendem a todas as condições.
Insira uma tabela de hash na qual as chaves são propriedades do trabalho e os valores são valores de propriedade do trabalho.

```yaml
Type: System.Collections.Hashtable
Parameter Sets: FilterParameterSet
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Force

Suspende a tarefa de fluxo de trabalho imediatamente. Essa ação pode causar perda de estado e dados.

Por padrão, `Suspend-Job` permite que o trabalho de workflow seja executado até o próximo ponto de verificação e, em seguida, o suspende.
Você também pode usar esse parâmetro para suspender tarefas de fluxo de trabalho que não têm pontos de verificação.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: F

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Id

Especifica as IDs de trabalhos que esse cmdlet suspende.

A ID é um inteiro que identifica exclusivamente o trabalho na sessão atual. É mais fácil lembrar e digitar do que a ID da instância, mas só é exclusiva na sessão atual. Você pode digitar uma ou mais IDs, separadas por vírgulas. Para localizar a ID de um trabalho, use o `Get-Job` cmdlet.

```yaml
Type: System.Int32[]
Parameter Sets: SessionIdParameterSet
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -InstanceId

Especifica as IDs de instância dos trabalhos que esse cmdlet suspende. O padrão é obter todos os trabalhos.

Uma ID de instância é um GUID que identifica exclusivamente o trabalho no computador. Para localizar a ID de instância de um trabalho, use `Get-Job` .

```yaml
Type: System.Guid[]
Parameter Sets: InstanceIdParameterSet
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Trabalho

Especifica os trabalhos de fluxo de trabalho que este cmdlet interrompe. Insira uma variável que contenha as tarefas de fluxo de trabalho ou um comando que as obtenha. Você também pode canalizar trabalhos de fluxo de trabalho para o `Suspend-Job` cmdlet.

```yaml
Type: System.Management.Automation.Job[]
Parameter Sets: JobParameterSet
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName, ByValue)
Accept wildcard characters: False
```

### -Name

Especifica nomes amigáveis de trabalhos que esse cmdlet suspende. Insira um ou mais nomes de tarefas de fluxo de trabalho.
Há suporte para caracteres curinga.

```yaml
Type: System.String[]
Parameter Sets: NameParameterSet
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Estado

Especifica um estado de trabalho. Este cmdlet interrompe apenas os trabalhos no estado especificado. Os valores aceitáveis para esse parâmetro são:

- NotStarted
- Executando
- Concluído
- Falhou
- Parado
- Bloqueado
- Suspenso
- Desconectado
- Suspensão
- Parando

`Suspend-Job` suspende somente trabalhos de fluxo de trabalho no estado **executando** .

Para obter mais informações sobre os Estados de trabalho, consulte [Enumeração JobState](/dotnet/api/system.management.automation.jobstate).

```yaml
Type: System.Management.Automation.JobState
Parameter Sets: StateParameterSet
Aliases:
Accepted values: NotStarted, Running, Completed, Failed, Stopped, Blocked, Suspended, Disconnected, Suspending, Stopping, AtBreakpoint

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Wait

Indica que esse cmdlet suprime o prompt de comando até que o trabalho de fluxo de trabalhos esteja no estado suspenso. Por padrão, `Suspend-Job` retorna imediatamente, mesmo que o trabalho de fluxo de trabalhos ainda não esteja no estado suspenso.

O parâmetro **Wait** é equivalente a canalizar um `Suspend-Job` comando para o `Wait-Job` cmdlet.

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

### -Confirm

Solicita sua confirmação antes de executar o cmdlet.

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

### -WhatIf

Mostra o que aconteceria se o cmdlet fosse executado. O cmdlet não é executado.

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

### CommonParameters

Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable. Para obter mais informações, confira [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## ENTRADAS

### System. Management. Automation. Job

Você pode canalizar todos os tipos de trabalhos para esse cmdlet. No entanto, se `Suspend-Job` o obtiver um trabalho de um tipo sem suporte, ele retornará um erro de encerramento.

## SAÍDAS

### System. Management. Automation. Job
Esse cmdlet retorna os trabalhos que ele suspendeu.

## OBSERVAÇÕES

- O mecanismo e o local para salvar um trabalho suspenso podem variar, dependendo do tipo do trabalho. Por exemplo, tarefas de fluxo de trabalho suspensas são salvas em um repositório de arquivo simples por padrão, mas também podem ser salvas em um banco de dados.
- Se você enviar um trabalho de workflow que não esteja no estado executando, `Suspend-Job` o exibirá uma mensagem de aviso. Para suprimir o aviso, use o parâmetro de **aviso** comum com um valor de SilentlyContinue.

  Se um trabalho não for de um tipo que dá suporte à suspensão, `Suspend-Job` o retornará um erro de encerramento.

- Para localizar os trabalhos de fluxo de trabalho que estão suspensos, incluindo aqueles que foram suspensos por esse cmdlet, use o parâmetro **State** do `Get-Job` cmdlet para obter trabalhos de fluxo de trabalho no estado suspenso.
- Alguns tipos de trabalho têm opções ou propriedades que impedem que o Windows PowerShell suspenda o trabalho em questão.
  Se as tentativas de suspender o trabalho falharem, verifique se as opções e as propriedades do trabalho permitem a suspensão.

## LINKS RELACIONADOS

[Get-Job](Get-Job.md)

[Receive-Job](Receive-Job.md)

[Remove-Job](Remove-Job.md)

[Resume-Job](Resume-Job.md)

[Start-Job](Start-Job.md)

[Stop-Job](Stop-Job.md)

[Suspend-Job](Suspend-Job.md)

[Wait-Job](Wait-Job.md)
