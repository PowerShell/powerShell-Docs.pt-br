---
ms.date: 09/13/2016
ms.topic: reference
title: AccessDBProviderSample02
description: AccessDBProviderSample02
ms.openlocfilehash: ebba2381370cf73f1e39015990f81dc4fd6dd937
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92667429"
---
# <a name="accessdbprovidersample02"></a>AccessDBProviderSample02

Este exemplo mostra como substituir os métodos [System. Management. Automation. Provider. Drivecmdletprovider. NewDrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) e [System. Management. Automation. Provider. Drivecmdletprovider. Removedrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) para dar suporte a chamadas para `New-PSDrive` os `Remove-PSDrive` cmdlets e. A classe de provedor neste exemplo deriva da classe [System. Management. Automation. Provider. Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) .

## <a name="demonstrates"></a>Demonstra

> [!IMPORTANT]
> Sua classe de provedor provavelmente derivará de uma das seguintes classes e, possivelmente, implementará outras interfaces de provedor:
>
> - Classe [System. Management. Automation. Provider. createcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) . Consulte [AccessDBProviderSample03](./accessdbprovidersample03.md).
> - Classe [System. Management. Automation. Provider. Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) . Consulte [AccessDBProviderSample04](./accessdbprovidersample04.md).
> - Classe [System. Management. Automation. Provider. Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) . Consulte [AccessDBProviderSample05](./accessdbprovidersample05.md).
>
> Para obter mais informações sobre como escolher qual classe de provedor deve ser derivada com base nos recursos do provedor, consulte [projetando seu provedor do Windows PowerShell](./provider-types.md).

Este exemplo demonstra o seguinte:

- Declarando o `CmdletProvider` atributo.

- Definição de uma classe de provedor que conduz da classe [System. Management. Automation. Provider. Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) .

- Substituindo o método [System. Management. Automation. Provider. Drivecmdletprovider. NewDrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) para dar suporte à criação de novas unidades. (Este exemplo não mostra como adicionar parâmetros dinâmicos ao `New-PSDrive` cmdlet.)

- Substituindo o método [System. Management. Automation. Provider. Drivecmdletprovider. Removedrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) para dar suporte à remoção de unidades existentes.

## <a name="example"></a>Exemplo

Este exemplo mostra como substituir os métodos [System. Management. Automation. Provider. Drivecmdletprovider. NewDrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) e [System. Management. Automation. Provider. Drivecmdletprovider. Removedrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) . Para este provedor de exemplo, quando uma unidade é criada, suas informações de conexão são armazenadas em um `AccessDBPsDriveInfo` objeto.

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample02/AccessDBProviderSample02.cs" range="11-154":::

## <a name="see-also"></a>Consulte Também

[System. Management. Automation. Provider. createcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider)

[System. Management. Automation. Provider. Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider)

[System. Management. Automation. Provider. Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)

[Projetar seu provedor do Windows PowerShell](./provider-types.md)
