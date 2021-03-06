---
external help file: System.Management.Automation.dll-Help.xml
Locale: en-US
Module Name: Microsoft.PowerShell.Core
ms.date: 11/06/2020
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/exit-pshostprocess?view=powershell-7.2&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Exit-PSHostProcess
ms.openlocfilehash: a1a8c6fcc16bcddc3bfcdade56cd75aadd179b74
ms.sourcegitcommit: 95d41698c7a2450eeb70ef2fb6507fe7e6eff3b6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "99596175"
---
# Exit-PSHostProcess

## SINOPSE
Fecha uma sessão interativa com um processo local.

## SYNTAX

```
Exit-PSHostProcess [<CommonParameters>]
```

## DESCRIPTION

O `Exit-PSHostProcess` cmdlet fecha uma sessão interativa com um processo local que você abriu executando o `Enter-PSHostProcess` cmdlet. Você executa o `Exit-PSHostProcess` cmdlet de dentro do processo, quando conclui a depuração ou a solução de problemas de um script que está sendo executado dentro de um processo. A partir do PowerShell 6,2, esse cmdlet tem suporte em plataformas que não são do Windows.

## EXEMPLOS

### Exemplo 1: sair de um processo

```
[Process:1520]: PS>  Exit-PSHostProcess
PS>
```

Neste exemplo, você esteve trabalhando em um processo ativo para depurar um script em execução em um runspace no processo, conforme descrito em `Enter-PSHostProcess` . Depois de digitar o `exit` comando para sair do depurador, execute o `Exit-PSHostProcess` cmdlet para fechar sua sessão interativa com o processo.
O cmdlet fecha a sessão no processo e retorna para o `PS C:\>` prompt.

## PARAMETERS

### CommonParameters

Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable. Para obter mais informações, confira [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## ENTRADAS

## SAÍDAS

## OBSERVAÇÕES

## LINKS RELACIONADOS

[Enter-PSHostProcess](Enter-PSHostProcess.md)

