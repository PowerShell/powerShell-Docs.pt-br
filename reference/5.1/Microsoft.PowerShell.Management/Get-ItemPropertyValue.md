---
external help file: Microsoft.PowerShell.Commands.Management.dll-Help.xml
keywords: powershell, cmdlet
Locale: en-US
Module Name: Microsoft.PowerShell.Management
ms.date: 10/18/2018
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.management/get-itempropertyvalue?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Get-ItemPropertyValue
ms.openlocfilehash: 2dbbbfeac3810f79b976b6a68ab3089e91707fb3
ms.sourcegitcommit: 9b28fb9a3d72655bb63f62af18b3a5af6a05cd3f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/07/2020
ms.locfileid: "93194170"
---
# Get-ItemPropertyValue

## SINOPSE
Obtém o valor de uma ou mais propriedades de um item especificado.

## SYNTAX

### Caminho (padrão)

```
Get-ItemPropertyValue [[-Path] <String[]>] [-Name] <String[]> [-Filter <String>] [-Include <String[]>]
 [-Exclude <String[]>] [-Credential <PSCredential>] [-UseTransaction] [<CommonParameters>]
```

### LiteralPath

```
Get-ItemPropertyValue -LiteralPath <String[]> [-Name] <String[]> [-Filter <String>] [-Include <String[]>]
 [-Exclude <String[]>] [-Credential <PSCredential>] [-UseTransaction] [<CommonParameters>]
```

## DESCRIPTION

O `Get-ItemPropertyValue` Obtém o valor atual para uma propriedade que você especifica quando usa o parâmetro *Name* , localizado em um caminho que você especifica com os parâmetros *Path* ou *LiteralPath* .

## EXEMPLOS

### Exemplo 1: obter o valor da propriedade ProductID

Esse comando obtém o valor da propriedade **ProductID** do objeto "\SOFTWARE\Microsoft\Windows NT\CurrentVersion" no provedor de registro do Windows.

```powershell
Get-ItemPropertyValue 'HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion' -Name ProductID
```

```output
94253-50000-11141-AA785
```

### Exemplo 2: obter a hora da última gravação de um arquivo ou pasta

Esse comando obtém o valor da propriedade **LastWriteTime** , ou a última vez que um arquivo ou pasta foi alterado, da pasta "C:\Users\Test\Documents\ModuleToAssembly", trabalhando no provedor FileSystem.

```powershell
Get-ItemPropertyValue -Path C:\Users\Test\Documents\ModuleToAssembly -Name LastWriteTime
```

```output
Wednesday, September 3, 2014 2:53:22 PM
```

### Exemplo 3: obter vários valores de propriedade de um arquivo ou pasta

Esse comando obtém os valores das propriedades **LastWriteTime** , **CreationTime** e **root** de uma pasta.
Os valores de propriedade são retornados na ordem em que você especificou os nomes de propriedade.

```powershell
Get-ItemPropertyValue -Path C:\Users\Test\Documents\ModuleToAssembly -Name LastWriteTime,CreationTime,Root
```

```output
Wednesday, September 3, 2014 2:53:22 PM
Wednesday, September 3, 2014 2:53:10 PM

Name              : C:\
Parent            :
Exists            : True
Root              : C:\
FullName          : C:\
Extension         :
CreationTime      : 9/1/2014 4:59:45 AM
CreationTimeUtc   : 9/1/2014 11:59:45 AM
LastAccessTime    : 9/27/2014 5:22:02 PM
LastAccessTimeUtc : 9/28/2014 12:22:02 AM
LastWriteTime     : 9/27/2014 5:22:02 PM
LastWriteTimeUtc  : 9/28/2014 12:22:02 AM
Attributes        : Hidden, System, Directory
BaseName          : C:\
Target            :
LinkType          :
Mode              : d--hs-
```

## PARAMETERS

### -Credential

Especifica uma conta de usuário que tem permissão para executar esta ação.
O padrão é o usuário atual.

Digite um nome de usuário, como "User01" ou "Domínio01 \ Usuário01", ou insira um objeto **PSCredential** , como um gerado pelo `Get-Credential` cmdlet.
Se você digitar um nome de usuário, uma senha será solicitada.

> [!WARNING]
> Nenhum provedor instalado com o Windows PowerShell dá suporte a esse parâmetro.

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

### -Excluir

Especifica, como uma matriz de cadeia de caracteres, um item ou itens que esse cmdlet exclui da operação.
O valor deste parâmetro qualifica o parâmetro **Path** .
Insira um padrão ou elemento de caminho, como "*.txt".
Caracteres curinga são permitidos.

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: True
```

### -Filter

Especifica um filtro no formato ou idioma do provedor.
O valor deste parâmetro qualifica o parâmetro **Path** .

A sintaxe do filtro, incluindo o uso de caracteres curinga, depende do provedor.
Os filtros são mais eficientes do que outros parâmetros, porque o provedor os aplica quando o cmdlet obtém os objetos em vez de fazer com que o PowerShell filtre os objetos depois que eles são recuperados.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: True
```

### -Incluir

Especifica, como uma matriz de cadeia de caracteres, um item ou itens que esse cmdlet inclui na operação.
O valor deste parâmetro qualifica o parâmetro **Path** .
Insira um padrão ou elemento de caminho, como "*.txt".
Caracteres curinga são permitidos.

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: True
```

### -LiteralPath

Especifica o caminho para o local atual da propriedade.
Ao contrário do parâmetro **Path** , o valor de **LiteralPath** é usado exatamente como digitado.
Nenhum caractere é interpretado como caractere curinga.
Se o caminho incluir caracteres de escape, coloque-o entre aspas simples.
Aspas simples instruem o PowerShell a não interpretar nenhum caractere como sequências de escape.

```yaml
Type: System.String[]
Parameter Sets: LiteralPath
Aliases: PSPath

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Name

Especifica o nome da propriedade ou propriedades para recuperar.

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases: PSProperty

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path

Especifica o caminho para o(s) item(ns).

```yaml
Type: System.String[]
Parameter Sets: Path
Aliases:

Required: False
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName, ByValue)
Accept wildcard characters: False
```

### -UseTransaction

Inclui o comando na transação ativa.
Este parâmetro é válido somente quando uma transação está em andamento.
Para obter mais informações, consulte about_Transactions.

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

Esse cmdlet oferece suporte aos parâmetros comuns:,,,,,, `-Debug` `-ErrorAction` `-ErrorVariable` `-InformationAction` `-InformationVariable` `-OutVariable` `-OutBuffer` , `-PipelineVariable` , `-Verbose` , `-WarningAction` e `-WarningVariable` . Para obter mais informações, confira [about_CommonParameters](../Microsoft.PowerShell.Core/About/about_CommonParameters.md).

## ENTRADAS

### System.String

É possível canalizar uma cadeia de caracteres que contém um caminho para esse cmdlet.

## SAÍDAS

### System. booliano, System. String, System. DateTime

Esse cmdlet retorna um objeto para cada valor de propriedade de item que obtém.
O tipo de objeto depende do valor da propriedade que é recuperado.
Por exemplo, em uma unidade do sistema de arquivos, o cmdlet pode retornar um arquivo ou uma pasta.

## OBSERVAÇÕES

Esse cmdlet foi projetado para trabalhar com os dados expostos por qualquer provedor. Para listar os provedores disponíveis em sua sessão, execute o `Get-PSProvider` cmdlet. Para obter mais informações, consulte about_Providers.

## LINKS RELACIONADOS

[Get-ItemProperty](Get-ItemProperty.md)

[Clear-ItemProperty](Clear-ItemProperty.md)

[Copy-ItemProperty](Copy-ItemProperty.md)

[Move-ItemProperty](Move-ItemProperty.md)

[New-ItemProperty](New-ItemProperty.md)

[Remove-ItemProperty](Remove-ItemProperty.md)

[Rename-ItemProperty](Rename-ItemProperty.md)

[Set-ItemProperty](Set-ItemProperty.md)

[Get-PSProvider](Get-PSProvider.md)