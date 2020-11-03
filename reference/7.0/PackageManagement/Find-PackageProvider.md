---
external help file: Microsoft.PowerShell.PackageManagement.dll-Help.xml
keywords: powershell, cmdlet
Locale: en-US
Module Name: PackageManagement
ms.date: 06/09/2017
online version: https://docs.microsoft.com/powershell/module/packagemanagement/find-packageprovider?view=powershell-7&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Find-PackageProvider
ms.openlocfilehash: 96e8829b6939c40c85fb924ae65d73f48d2e475b
ms.sourcegitcommit: de63e9481cf8024883060aae61fb02c59c2de662
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2020
ms.locfileid: "93192935"
---
# Find-PackageProvider

## SINOPSE
Retorna uma lista de provedores de pacote Gerenciamento de Pacotes disponíveis para instalação.

## SYNTAX

```
Find-PackageProvider [[-Name] <String[]>] [-AllVersions] [-Source <String[]>] [-IncludeDependencies]
 [-Credential <PSCredential>] [-Proxy <Uri>] [-ProxyCredential <PSCredential>] [-RequiredVersion <String>]
 [-MinimumVersion <String>] [-MaximumVersion <String>] [-Force] [-ForceBootstrap] [<CommonParameters>]
```

## DESCRIPTION

O cmdlet **Find-packageprovider** localiza provedores de PackageManagement correspondentes que estão disponíveis em fontes de pacote registradas com PowerShellGet.
Esses são os provedores de pacote disponíveis para instalação com o cmdlet Install-PackageProvider.
Por padrão, isso inclui módulos disponíveis no Galeria do PowerShell com as marcas **PackageManagement** e **Provider** .

**Find-packageprovider** também localiza provedores de gerenciamento de pacotes correspondentes que estão disponíveis no repositório de Blob do gerenciamento de pacotes Azure.
Use o provedor de bootstrapper para localizá-los e instalá-los.

## EXEMPLOS

### Exemplo 1: localizar todos os provedores de pacote disponíveis

```
PS C:\> Find-PackageProvider
```

Esse comando obtém uma lista de todos os provedores de pacote que estão disponíveis nos repositórios com suporte pelo Gerenciamento de Pacotes.
Por padrão, esses provedores de pacotes estão disponíveis no Galeria do PowerShell e usando o aplicativo de inicialização Gerenciamento de Pacotes.

### Exemplo 2: localizar todas as versões de um provedor

```
PS C:\> Find-PackageProvider -Name "Nuget" -AllVersions
```

Esse comando localiza todas as versões do provedor de pacote chamado NuGet.

### Exemplo 3: localizar um provedor de uma fonte especificada

```
PS C:\> Find-PackageProvider -Name "Gistprovider" -Source "PSGallery"
```

Esse comando localiza um provedor de pacote disponível usando uma origem de pacote especificada.

## PARAMETERS

### -Próprias versões

Indica que esse cmdlet retorna todas as versões disponíveis do provedor de pacote.
Por padrão, **Find-packageprovider** retorna apenas a versão mais recente disponível.

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

### -Credential

Especifica uma conta de usuário que tem permissão para pesquisar provedores de pacote.

```yaml
Type: System.Management.Automation.PSCredential
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Force

Força o comando a ser executado sem solicitar a confirmação do usuário.
Atualmente, isso é equivalente ao parâmetro *ForceBootstrap* .

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

### -ForceBootstrap

Indica que esse cmdlet força Gerenciamento de Pacotes a instalar automaticamente o provedor de pacote.

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

### -IncludeDependencies

Indica que esse cmdlet inclui dependências.

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

### -MaximumVersion

Especifica a versão máxima permitida do provedor de pacote que você deseja localizar.
Se você não adicionar esse parâmetro, **Find-packageprovider** encontrará a versão mais alta disponível do provedor.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -MinimumVersion

Especifica a versão mínima permitida do provedor de pacote que você deseja localizar.
Se você não adicionar esse parâmetro, **Find-packageprovider** encontrará a versão mais alta disponível do pacote que também atende a qualquer versão especificada máxima especificada pelo parâmetro *MaximumVersion* .

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name

Especifica um ou mais nomes de módulo de provedor de pacote ou nomes de provedor com caracteres curinga.
Separe vários nomes de pacote com vírgulas.

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: True
```

### -Proxy

Especifica um servidor proxy para a solicitação, em vez de conectar-se diretamente ao recurso da Internet.

```yaml
Type: System.Uri
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ProxyCredential

Especifica uma conta de usuário com permissão para conectar-se aos computadores especificados pelo parâmetro **Proxy** .

```yaml
Type: System.Management.Automation.PSCredential
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -RequiredVersion

Especifica a versão exata permitida do provedor de pacote que você deseja localizar.
Se você não adicionar esse parâmetro, **Find-packageprovider** encontrará a versão mais alta disponível do provedor que também atende a qualquer versão máxima especificada pelo parâmetro *MaximumVersion* .

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Source

Especifica uma ou mais origens de pacote.
Você pode obter uma lista de fontes de pacote disponíveis usando o cmdlet Get-PackageSource.

```yaml
Type: System.String[]
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

## SAÍDAS

### Microsoft. PackageManagement. Packaging. SoftwareIdentity

Esse cmdlet retorna um objeto **SoftwareIdentity** .
Um objeto **SoftwareIdentity** pode ser canalizado para **install-packageprovider** para instalar os resultados de **Find-packageprovider** .

## OBSERVAÇÕES

## LINKS RELACIONADOS

[about_PackageManagement](../Microsoft.PowerShell.Core/About/about_PackageManagement.md)

[Unregister-PackageSource](Unregister-PackageSource.md)

[Get-PackageSource](Get-PackageSource.md)

[Register-PackageSource](Register-PackageSource.md)

[Install-PackageProvider](Install-PackageProvider.md)