---
external help file: Microsoft.PowerShell.Commands.Utility.dll-Help.xml
keywords: powershell, cmdlet
Locale: en-US
Module Name: Microsoft.PowerShell.Utility
ms.date: 04/09/2020
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/trace-command?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Trace-Command
ms.openlocfilehash: 00c267b5db630944dbccd35a30ea614d13193af8
ms.sourcegitcommit: 9b28fb9a3d72655bb63f62af18b3a5af6a05cd3f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/07/2020
ms.locfileid: "93193729"
---
# Trace-Command

## SINOPSE
Configura e inicia um rastreamento da expressão ou comando especificado.

## SYNTAX

### expressionset (padrão)

```
Trace-Command [-InputObject <PSObject>] [-Name] <String[]> [[-Option] <PSTraceSourceOptions>]
 [-Expression] <ScriptBlock> [-ListenerOption <TraceOptions>] [-FilePath <String>] [-Force] [-Debugger]
 [-PSHost] [<CommonParameters>]
```

### commandSet

```
Trace-Command [-InputObject <PSObject>] [-Name] <String[]> [[-Option] <PSTraceSourceOptions>]
 [-Command] <String> [-ArgumentList <Object[]>] [-ListenerOption <TraceOptions>] [-FilePath <String>] [-Force]
 [-Debugger] [-PSHost] [<CommonParameters>]
```

## DESCRIPTION
O `Trace-Command` cmdlet configura e inicia um rastreamento da expressão ou do comando especificado.
Ele funciona como Set-TraceSource, exceto que se aplica apenas ao comando especificado.

## EXEMPLOS

### Exemplo 1: rastrear o processamento de metadados, a associação de parâmetro e uma expressão

Este exemplo inicia um rastreamento de processamento de metadados, associação de parâmetro e criação de cmdlet e destruição da `Get-Process Notepad` expressão.

```powershell
Trace-Command -Name metadata,parameterbinding,cmdlet -Expression {Get-Process Notepad} -PSHost
```

Ele usa o parâmetro **Name** para especificar as fontes de rastreamento, o parâmetro **expression** para especificar o comando e o parâmetro **PSHost** para enviar a saída para o console. Como não especifica nenhuma opção de rastreamento ou opções de ouvinte, o comando usa os padrões:

- Tudo para as opções de rastreamento
- Nenhuma para as opções de ouvinte

### Exemplo 2: rastrear as ações de operações de parâmetros

Este exemplo rastreia as ações das operações de **ParameterBinding** do PowerShell enquanto processa uma `Get-Alias` expressão que usa a entrada do pipeline.

```powershell
$A = "i*"
Trace-Command ParameterBinding {Get-Alias $Input} -PSHost -InputObject $A
```

No `Trace-Command` , o parâmetro **InputObject** passa um objeto para a expressão que está sendo processada durante o rastreamento.

O primeiro comando armazena a cadeia de caracteres `i*` na `$A` variável. O segundo comando usa o `Trace-Command` cmdlet com a origem de rastreamento de ParameterBinding. O parâmetro **PSHost** envia a saída para o console.

A expressão que está sendo processada é `Get-Alias $Input` , em que a `$Input` variável é associada ao parâmetro **InputObject** . O parâmetro **InputObject** passa a variável `$A` para a expressão. Na verdade, o comando que está sendo processado durante o rastreamento é `Get-Alias -InputObject $A" or "$A | Get-Alias` .

## PARAMETERS

### -ArgumentList

Especifica os parâmetros e valores de parâmetro para o comando que está sendo rastreado. O alias para **ArgumentList** é **Args** . Esse recurso é especialmente útil para depuração parâmetros dinâmicos.

Para obter mais informações sobre o comportamento de **ArgumentList** , consulte [about_Splatting](../Microsoft.PowerShell.Core/About/about_Splatting.md#splatting-with-arrays).

```yaml
Type: System.Object[]
Parameter Sets: commandSet
Aliases: Args

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Command

Especifica um comando que está sendo processado durante o rastreamento.

```yaml
Type: System.String
Parameter Sets: commandSet
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Depurador

Indica que o cmdlet envia a saída de rastreamento para o depurador. Você pode exibir a saída em qualquer modo de usuário ou depurador do modo kernel, ou ainda no Visual Studio. Esse parâmetro também seleciona o ouvinte de rastreamento padrão.

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

### -Expressão

Especifica a expressão que está sendo processada durante o rastreamento. Coloque a expressão entre chaves ( `{}` ).

```yaml
Type: System.Management.Automation.ScriptBlock
Parameter Sets: expressionSet
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -FilePath

Especifica um arquivo para o qual o cmdlet envia a saída de rastreamento. Esse parâmetro também seleciona o ouvinte de rastreamento do arquivo.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases: PSPath

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Force

Força o comando a ser executado sem solicitar a confirmação do usuário. Usado com o parâmetro **FilePath** . Mesmo usando o parâmetro **Force** , o cmdlet não pode substituir as restrições de segurança.

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

### -InputObject

Especifica a entrada para a expressão que está sendo processada durante o rastreamento. Você pode inserir uma variável que representa a entrada que aceita a expressão ou passar um objeto por meio do pipeline.

```yaml
Type: System.Management.Automation.PSObject
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -ListenerOption

Especifica dados opcionais para o prefixo de cada mensagem de rastreamento na saída. Os valores aceitáveis para esse parâmetro são:

- Nenhum
- LogicalOperationStack
- Datetime
- Timestamp
- ProcessId
- ThreadId
- Chamadas

**None** é o padrão.

Para especificar várias opções, separe-as com vírgulas, mas sem espaços, e coloque-as entre aspas, como "ProcessID ThreadID".

```yaml
Type: System.Diagnostics.TraceOptions
Parameter Sets: (All)
Aliases:
Accepted values: None, LogicalOperationStack, DateTime, Timestamp, ProcessId, ThreadId, Callstack

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name

Especifica uma matriz de componentes do PowerShell que são rastreados. Insira o nome da origem de rastreamento de cada componente. Caracteres curinga são permitidos. Para localizar as fontes de rastreamento no seu computador, digite `Get-TraceSource` .

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Opção

Determina o tipo de eventos que são rastreados. Os valores aceitáveis para esse parâmetro são:

- Nenhum
- Construtor
- Dispose
- Finalizer
- Método
- Propriedade
- Delegados
- Eventos
- Exceção
- Bloqueio
- Erro
- Errors
- Aviso
- Detalhado
- WriteLine
- Dados
- Escopo
- ExecutionFlow
- Assert
- Tudo

All é o padrão.

Os seguintes valores são combinações de outros valores:

- ExecutionFlow: (Construtor, descarte, finalizador, método, delegados, eventos e escopo)
- Dados: (constructor, Dispose, Finalizer, Property, Verbose e WriteLine)
- Erros: (erro e exceção).

Para especificar várias opções, separe-as com vírgulas, mas sem espaços, e coloque-as entre aspas, como "Constructor, Dispose".

```yaml
Type: System.Management.Automation.PSTraceSourceOptions
Parameter Sets: (All)
Aliases:
Accepted values: None, Constructor, Dispose, Finalizer, Method, Property, Delegates, Events, Exception, Lock, Error, Errors, Warning, Verbose, WriteLine, Data, Scope, ExecutionFlow, Assert, All

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -PSHost

Indica que o cmdlet envia a saída de rastreamento para o host do PowerShell. Esse parâmetro também seleciona o ouvinte de rastreamento PSHost.

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

### CommonParameters

Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable. Para obter mais informações, confira [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## ENTRADAS

### System. Management. Automation. PSObject

É possível canalizar objetos que representam a entrada para a expressão para `Trace-Command` .

## SAÍDAS

### System. Management. Automation. PSObject

Retorna o rastreamento de comando no fluxo de depuração.

## OBSERVAÇÕES

- O rastreamento é um método utilizado pelos desenvolvedores para depurar e aprimorar os programas. Ao realizar o rastreamento, o componente gera mensagens detalhadas sobre cada etapa no seu processamento interno.

- Os cmdlets de rastreamento do PowerShell são projetados para ajudar os desenvolvedores do PowerShell, mas estão disponíveis para todos os usuários. Eles permitem monitorar quase todos os aspectos da funcionalidade do shell.

- Para localizar os componentes do PowerShell que estão habilitados para rastreamento, digite `Get-Help Get-TraceSource` .

  Uma origem de rastreamento é a parte de cada componente do PowerShell que gerencia o rastreamento e gera mensagens de rastreamento para o componente. Para rastrear um componente, você deve identificar sua origem de rastreamento.

  Um ouvinte de rastreamento recebe a saída do rastreamento e o exibe para o usuário. Você pode optar por enviar os dados de rastreamento para um modo de usuário ou depurador de modo kernel, para o host ou console, para um arquivo ou para um ouvinte personalizado derivado da classe **System. Diagnostics. TraceListener** .

- Quando você usa o conjunto de parâmetros commandSet, o PowerShell processa o comando da mesma forma que seria processado em um pipeline. Por exemplo, a descoberta de comando não é repetida para cada objeto de entrada.

- Os nomes dos parâmetros **Name** , **expression** , **Option** e **Command** são opcionais. Se você omitir os nomes de parâmetro, os valores de parâmetro não nomeados deverão aparecer nesta ordem: **nome** , **expressão** , **opção** ou **nome** , **comando** , **opção** . Se você incluir os nomes dos parâmetros, os parâmetros podem aparecer em qualquer ordem.

## LINKS RELACIONADOS

[Get-TraceSource](Get-TraceSource.md)

[Measure-Command](Measure-Command.md)

[Set-TraceSource](Set-TraceSource.md)

[Show-Command](Show-Command.md)
