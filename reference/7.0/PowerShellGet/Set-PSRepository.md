---
external help file: PSModule-help.xml
keywords: powershell, cmdlet
Locale: en-US
Module Name: PowerShellGet
ms.date: 04/22/2020
online version: https://docs.microsoft.com/powershell/module/powershellget/set-psrepository?view=powershell-7&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Set-PSRepository
ms.openlocfilehash: 95289839fc491cc90def6df7b7ef6bbbdf9ea014
ms.sourcegitcommit: 22c93550c87af30c4895fcb9e9dd65e30d60ada0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2020
ms.locfileid: "94892596"
---
# Set-PSRepository

## SINOPSE
Define valores para um repositório registrado.

## SYNTAX

```
Set-PSRepository [-Name] <String> [[-SourceLocation] <Uri>] [-PublishLocation <Uri>]
 [-ScriptSourceLocation <Uri>] [-ScriptPublishLocation <Uri>] [-Credential <PSCredential>]
 [-InstallationPolicy <String>] [-Proxy <Uri>] [-ProxyCredential <PSCredential>]
 [-PackageManagementProvider <String>] [<CommonParameters>]
```

## DESCRIPTION

O `Set-PSRepository` cmdlet define valores para um repositório de módulo registrado. As configurações são persistentes para o usuário atual e se aplicam a todas as versões do PowerShell instaladas para esse usuário.

## EXEMPLOS

### Exemplo 1: definir a política de instalação para um repositório

```powershell
Set-PSRepository -Name "myInternalSource" -InstallationPolicy Trusted
```

Esse comando define a política de instalação para o repositório **Myinternalname** como **confiável**, para que você não seja solicitado antes de instalar os módulos dessa fonte.

### Exemplo 2: definir a origem e os locais de publicação para um repositório

```powershell
Set-PSRepository -Name "myInternalSource" -SourceLocation 'https://someNuGetUrl.com/api/v2' -PublishLocation 'https://someNuGetUrl.com/api/v2/packages'
```

Esse comando define o local de origem e o local de publicação para **Myinternalname** para os URIs especificados.

## PARAMETERS

### -Credential

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

### -InstallationPolicy

Especifica a política de instalação. Os valores válidos são: **confiável**, **não confiável**.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:
Accepted values: Trusted, Untrusted

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name

Especifica o nome do repositório.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -PackageManagementProvider

Especifica o provedor de gerenciamento de pacotes.

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

### -Proxy

Especifica um servidor proxy para a solicitação, em vez de conectar-se diretamente ao recurso da Internet.

```yaml
Type: System.Uri
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -ProxyCredential

Especifica uma conta de usuário com permissão para conectar-se aos computadores especificados pelo parâmetro **Proxy**.

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

### -PublishLocation

Especifica o URI do local de publicação. Por exemplo, para repositórios baseados em NuGet, o local de publicação é semelhante a `https://someNuGetUrl.com/api/v2/Packages` .

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

### -ScriptPublishLocation

Especifica o local de publicação do script.

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

### -ScriptSourceLocation

Especifica o local de origem do script.

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

### -SourceLocation

Especifica o URI para descobrir e instalar os módulos deste repositório. Por exemplo, para repositórios baseados em NuGet, o local de origem é semelhante a `https://someNuGetUrl.com/api/v2` .

```yaml
Type: System.Uri
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters

Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable. Para obter mais informações, confira [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## ENTRADAS

### System.String

### System. Management. Automation. PSCredential

### System.Uri

## SAÍDAS

### System.Object

## OBSERVAÇÕES

> [!IMPORTANT]
> A partir de abril de 2020, o Galeria do PowerShell não dá mais suporte às versões 1,0 e 1,1 da segurança da camada de transporte (TLS). Se você não estiver usando o TLS 1,2 ou superior, receberá um erro ao tentar acessar o Galeria do PowerShell. Use o comando a seguir para garantir que você esteja usando o TLS 1,2:
>
> `[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12`
>
> Para obter mais informações, consulte o [comunicado](https://devblogs.microsoft.com/powershell/powershell-gallery-tls-support/) no blog do PowerShell.

## LINKS RELACIONADOS

[Get-PSRepository](Get-PSRepository.md)

[Register-PSRepository](Register-PSRepository.md)

[Unregister-PSRepository](Unregister-PSRepository.md)
