---
external help file: Microsoft.PowerShell.Commands.Management.dll-Help.xml
keywords: powershell, cmdlet
Locale: en-US
Module Name: Microsoft.PowerShell.Management
ms.date: 06/09/2017
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.management/join-path?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Join-Path
ms.openlocfilehash: bcba432fb52b327695b61a4475d4a93903a688a5
ms.sourcegitcommit: 9b28fb9a3d72655bb63f62af18b3a5af6a05cd3f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/07/2020
ms.locfileid: "93193983"
---
# Join-Path

## SINOPSE
Combina um caminho e um caminho filho em um único caminho.

## SYNTAX

```
Join-Path [-Path] <String[]> [-ChildPath] <String> [-Resolve] [-Credential <PSCredential>] [-UseTransaction]
 [<CommonParameters>]
```

## DESCRIPTION

O `Join-Path` cmdlet combina um caminho e um caminho filho em um único caminho.
O provedor fornece os delimitadores de caminho.

## EXEMPLOS

### Exemplo 1: combinar um caminho com um caminho filho

```powershell
PS C:\> Join-Path -Path "path" -ChildPath "childpath"
```

```output
path\childpath
```

Esse comando usa `Join-Path` para combinar um caminho com um ChildPath.

Como o comando é executado do `FileSystem` provedor, ele fornece o `\` delimitador para unir os caminhos.

### Exemplo 2: combinar caminhos que já contêm separadores de diretório

```powershell
PS C:\> Join-Path -Path "path\" -ChildPath "\childpath"
```

```output
path\childpath
```

Separadores de diretório existentes `\` e manipulados para que haja apenas um separador entre `Path` e `ChildPath`

### Exemplo 3: exibir arquivos e pastas unindo um caminho com um caminho filho

```powershell
Join-Path "C:\win*" "System*" -Resolve
```

Esse comando exibe os arquivos e pastas que são referenciados unindo o \* caminho C:\win e o \* caminho filho do sistema.
Ele exibe os mesmos arquivos e pastas que `Get-ChildItem` , mas exibe o caminho totalmente qualificado para cada item.
Nesse comando, os `Path` nomes de `ChildPath` parâmetro e opcionais são omitidos.

### Exemplo 4: usar Join-Path com o provedor de registro do PowerShell

```powershell
PS HKLM:\> Join-Path -Path System -ChildPath *ControlSet* -Resolve
```

```output
HKLM:\System\ControlSet001
HKLM:\System\CurrentControlSet
```

Esse comando exibe as chaves do registro na `HKLM\System` subchave do registro que incluem `ControlSet` .

O `Resolve` parâmetro, tenta resolver o caminho Unido, incluindo curingas do caminho do provedor atual `HKLM:\`

### Exemplo 5: combinar várias raízes de caminho com um caminho filho

```powershell
Join-Path -Path C:, D:, E:, F: -ChildPath New
```

```output
C:\New
D:\New
E:\New
F:\New
```

Esse comando usa `Join-Path` para combinar várias raízes de caminho com um caminho filho.

> [!NOTE]
> As unidades especificadas por `Path` devem existir ou haverá falha na junção dessa entrada.

### Exemplo 6: combinar as raízes de uma unidade do sistema de arquivos com um caminho filho

```powershell
Get-PSDrive -PSProvider filesystem | ForEach-Object {$_.root} | Join-Path -ChildPath "Subdir"
```

```output
C:\Subdir
D:\Subdir
```

Esse comando combina as raízes de cada unidade do sistema de arquivos do PowerShell no console do com o caminho filho subdir.

O comando usa o `Get-PSDrive` cmdlet para obter as unidades do PowerShell com suporte pelo provedor FileSystem.
A `ForEach-Object` instrução seleciona apenas a propriedade raiz dos `PSDriveInfo` objetos e a combina com o caminho filho especificado.

A saída mostra que as unidades do PowerShell no computador incluíram uma unidade mapeada para o diretório C:\Program Files.

## PARAMETERS

### -ChildPath

Especifica os elementos a serem acrescentados ao valor do `Path` parâmetro.
Caracteres curinga são permitidos.
O `ChildPath` parâmetro é necessário, embora o nome do parâmetro ("ChildPath") seja opcional.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: True
```

### -Credential

> [!NOTE]
> Não há suporte para esse parâmetro em nenhum provedor instalado com o PowerShell.
> Para representar outro usuário ou elevar suas credenciais ao executar esse cmdlet, use [Invoke-Command](../Microsoft.PowerShell.Core/Invoke-Command.md).

```yaml
Type: System.Management.Automation.PSCredential
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Path

Especifica o caminho principal (ou caminhos) ao qual o caminho filho é anexado.
Caracteres curinga são permitidos.

O valor de `Path` determina qual provedor une os caminhos e adiciona os delimitadores de caminho.
O `Path` parâmetro é necessário, embora o nome do parâmetro ("Path") seja opcional.

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases: PSPath

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName, ByValue)
Accept wildcard characters: True
```

### -Resolver

Indica que este cmdlet deve tentar resolver o caminho Unido do provedor atual.

- Se forem usados curingas, o cmdlet retornará todos os caminhos que correspondam ao caminho Unido.
- Se **nenhum** caractere curinga for usado, o cmdlet será um erro se o caminho não existir.

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

### -UseTransaction

Inclui o comando na transação ativa.
Este parâmetro é válido somente quando uma transação está em andamento.
Para obter mais informações, consulte [about_Transactions](../Microsoft.PowerShell.Core/About/about_Transactions.md).

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: usetx

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters

Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable. Para obter mais informações, confira [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## ENTRADAS

### System.String

É possível canalizar uma cadeia de caracteres que contém um caminho para esse cmdlet.

## SAÍDAS

### System.String

Esse cmdlet retorna uma cadeia de caracteres que contém o caminho resultante.

## OBSERVAÇÕES

Os cmdlets que contêm o substantivo de caminho (os cmdlets de caminho) manipulam nomes de caminho e retornam os nomes em um formato conciso que todos os provedores do PowerShell podem interpretar. Eles foram projetados para uso em programas e scripts onde você deseja exibir uma parte ou todo um nome de caminho em um formato específico. Use-os como usaria Dirname, Normpath, Realpath, Join ou outros manipuladores de caminho.

Você pode usar os cmdlets de caminho com vários provedores, incluindo `FileSystem` os `Registry` provedores, e `Certificate` .

Esse cmdlet foi projetado para trabalhar com os dados expostos por qualquer provedor.
Para listar os provedores disponíveis em sua sessão, digite `Get-PSProvider` .
Para obter mais informações, consulte [about_Providers](../Microsoft.PowerShell.Core/About/about_Providers.md).

## LINKS RELACIONADOS

[Convert-Path](Convert-Path.md)

[Resolve-Path](Resolve-Path.md)

[Split-Path](Split-Path.md)

[Test-Path](Test-Path.md)

[Get-PSProvider](Get-PSProvider.md)

[Get-ChildItem](Get-ChildItem.md)

[Get-PSDrive](Get-PSDrive.md)
