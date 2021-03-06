---
external help file: PSDesiredStateConfiguration-help.xml
keywords: powershell, cmdlet
Locale: en-US
Module Name: PSDesiredStateConfiguration
ms.date: 06/09/2017
online version: https://docs.microsoft.com/powershell/module/psdesiredstateconfiguration/new-dscchecksum?view=powershell-7&WT.mc_id=ps-gethelp
schema: 2.0.0
title: New-DscChecksum
ms.openlocfilehash: 2a66f906025f7a25609080e0b8da7f01755cd2fa
ms.sourcegitcommit: de63e9481cf8024883060aae61fb02c59c2de662
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2020
ms.locfileid: "93192836"
---
# New-DscChecksum

## SINOPSE
Cria arquivos de soma de verificação para documentos DSC e recursos DSC.

## SYNTAX

```
New-DscChecksum [-Path] <String[]> [[-OutPath] <String>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION

O cmdlet **New-DSCCheckSum** gera arquivos de soma de verificação para documentos de DSC (configuração de estado desejado) do PowerShell e recursos de DSC compactados.
Esse cmdlet gera um arquivo de soma de verificação para cada configuração e recurso a ser usado no modo de pull.
O serviço DSC usa as somas de verificação para verificar se a configuração e os recursos corretos existem no nó de destino.
Coloque as somas de verificação junto com os documentos DSC associados e os recursos de DSC compactados no armazenamento do serviço DSC.

## EXEMPLOS

### Exemplo 1: criar arquivos de soma de verificação para todas as configurações em um caminho específico

```
PS C:\> New-DscCheckSum -Path "C:\DSC\Configurations\"
```

Este comando cria arquivos de soma de verificação para todas as configurações no caminho C:\DSC\Configurations.
Todos os arquivos de soma de verificação que já existem são ignorados.

### Exemplo 2: criar arquivos de soma de verificação para todas as configurações em um caminho específico e substituir os arquivos de soma de verificação existentes

```
PS C:\> New-DscCheckSum -Path "C:\DSC\Configurations\" -Force
```

Este comando cria novos arquivos de soma de verificação para todas as configurações no caminho C:\DSC\Configurations.
A especificação do parâmetro *Force* faz com que o comando Substitua todos os arquivos de soma de verificação que já existem.

## PARAMETERS

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

### -Force

Indica que o cmdlet substitui o arquivo de saída especificado se ele já existir.

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

### -OutPath

Especifica o caminho e o nome do arquivo de soma de verificação de saída.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path

Especifica o caminho do arquivo de entrada.

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases: ConfigurationPath

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf

Mostra o que aconteceria se o cmdlet fosse executado.
O cmdlet não é executado.

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

### Nenhum

## SAÍDAS

### System.Object

## OBSERVAÇÕES

## LINKS RELACIONADOS

[Visão geral da Desired State Configuration do Windows PowerShell](/powershell/scripting/dsc/overview/dscforengineers)
