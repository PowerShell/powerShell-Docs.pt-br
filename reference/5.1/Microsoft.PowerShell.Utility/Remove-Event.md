---
external help file: Microsoft.PowerShell.Commands.Utility.dll-Help.xml
keywords: powershell, cmdlet
Locale: en-US
Module Name: Microsoft.PowerShell.Utility
ms.date: 06/09/2017
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/remove-event?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Remove-Event
ms.openlocfilehash: 35d5d75cad2855753504549262abd2e14af200c0
ms.sourcegitcommit: 177ae45034b58ead716853096b2e72e4864e6df6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2020
ms.locfileid: "94344483"
---
# Remove-Event

## SINOPSE
Exclui eventos da fila de eventos.

## SYNTAX

### BySource (padrão)

```
Remove-Event [-SourceIdentifier] <String> [-WhatIf] [-Confirm] [<CommonParameters>]
```

### ByIdentifier

```
Remove-Event [-EventIdentifier] <Int32> [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION

O `Remove-Event` cmdlet exclui eventos da fila de eventos na sessão atual.

Este cmdlet exclui somente os eventos atualmente na fila. Para cancelar os registros de eventos ou cancelar a assinatura, use o `Unregister-Event` cmdlet.

## EXEMPLOS

### Exemplo 1: remover um evento por identificador de origem

```
PS C:\> Remove-Event -SourceIdentifier "ProcessStarted"
```

Esse comando exclui eventos com um identificador de origem do processo iniciado na fila de eventos.

### Exemplo 2: remover um evento por identificador de evento

```
PS C:\> Remove-Event -EventIdentifier 30
```

Esse comando exclui o evento com uma ID de evento 30 da fila de eventos.

### Exemplo 3: remover todos os eventos

```
PS C:\> Get-Event | Remove-Event
```

Esse comando exclui todos os eventos da fila de eventos.

## PARAMETERS

### -EventIdentifier

Especifica o identificador de evento para o qual o cmdlet exclui. Um parâmetro **EventIdentifier** ou **SourceIdentifier** é necessário em todos os comandos.

```yaml
Type: System.Int32
Parameter Sets: ByIdentifier
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -SourceIdentifier

Especifica o identificador de origem para o qual este cmdlet exclui eventos. Caracteres curinga não são permitidos. Um parâmetro **EventIdentifier** ou **SourceIdentifier** é necessário em todos os comandos.

```yaml
Type: System.String
Parameter Sets: BySource
Aliases:

Required: True
Position: 0
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

### System. Management. Automation. PSEventArgs

Você pode canalizar eventos de `Get-Event` para `Remove-Event` .

## SAÍDAS

### Nenhum

O cmdlet não gera nenhuma saída.

## OBSERVAÇÕES

Eventos, assinaturas de evento e a fila de eventos existem apenas na sessão atual. Se você fechar a sessão atual, a fila de eventos será descartada e a inscrição do evento será cancelada.

## LINKS RELACIONADOS

[Get-Event](Get-Event.md)

[New-Event](New-Event.md)

[Register-EngineEvent](Register-EngineEvent.md)

[Register-ObjectEvent](Register-ObjectEvent.md)

[Remove-Event](Remove-Event.md)

[Unregister-Event](Unregister-Event.md)

[Wait-Event](Wait-Event.md)
