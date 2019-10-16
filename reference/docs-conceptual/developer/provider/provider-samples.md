---
title: Exemplos de provedor | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c4933dad-fec9-4337-a1a9-9dc16ee87cc3
caps.latest.revision: 9
ms.openlocfilehash: 1e7aeb5bcb6bd5a2845648c3327e2245e6c428ba
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72366295"
---
# <a name="provider-samples"></a>Amostras de provedor

Esta seção inclui exemplos de provedores que acessam um banco de dados do Microsoft Access. Esses exemplos incluem classes de provedor que derivam de todas as classes de provedor base.

## <a name="in-this-section"></a>Nesta seção

Esta seção inclui os seguintes tópicos:

[Exemplo de AccessDBProviderSample01](./accessdbprovidersample01.md) Este exemplo mostra como declarar a classe de provedor que deriva diretamente da classe [System. Management. Automation. Provider. cmdletprovider](/dotnet/api/System.Management.Automation.Provider.CmdletProvider) . Ele é incluído aqui apenas para fins de integridade.

[AccessDBProviderSample02](./accessdbprovidersample02.md) Este exemplo mostra como substituir os métodos [System. Management. Automation. Provider. Drivecmdletprovider. NewDrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) e [System. Management. Automation. Provider. Drivecmdletprovider. Removedrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) para dar suporte a chamadas para o `New-PSDrive` e cmdlets `Remove-PSDrive`. A classe de provedor neste exemplo deriva da classe [System. Management. Automation. Provider. Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) .

[AccessDBProviderSample03](./accessdbprovidersample03.md) Este exemplo mostra como substituir os métodos [System. Management. Automation. Provider. docmdletprovider. GetItem *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) e [System. Management. Automation. Provider. docmdletprovider. SetItem *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) para dar suporte a chamadas para o `Get-Item` e @no__ cmdlets t-4. A classe de provedor neste exemplo deriva da classe [System. Management. Automation. Provider. createcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) .

[AccessDBProviderSample04](./accessdbprovidersample04.md) Este exemplo mostra como substituir métodos de contêiner para dar suporte a chamadas para os cmdlets `Copy-Item`, `Get-ChildItem`, `New-Item` e `Remove-Item`. Esses métodos devem ser implementados quando o armazenamento de dados contiver itens que são contêineres. Um contêiner é um grupo de itens filho em um item pai comum. A classe de provedor neste exemplo deriva da classe [System. Management. Automation. Provider. Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) .

[AccessDBProviderSample05](./accessdbprovidersample05.md) Este exemplo mostra como substituir métodos de contêiner para dar suporte a chamadas para os cmdlets `Move-Item` e `Join-Path`. Esses métodos deverão ser implementados quando o usuário precisar mover itens dentro de um contêiner e se o armazenamento de dados contiver contêineres aninhados. A classe de provedor neste exemplo deriva da classe [System. Management. Automation. Provider. Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) .

[AccessDBProviderSample06](./accessdbprovidersample06.md) Este exemplo mostra como substituir os métodos de conteúdo para dar suporte a chamadas para os cmdlets `Clear-Content`, `Get-Content` e `Set-Content`. Esses métodos devem ser implementados quando o usuário precisa gerenciar o conteúdo dos itens no armazenamento de dados. A classe de provedor neste exemplo deriva da classe [System. Management. Automation. Provider. Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) e implementa a interface [System. Management. Automation. Provider. Icontentcmdletprovider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider) .

## <a name="see-also"></a>Consulte Também

[Escrevendo um provedor do Windows PowerShell](./writing-a-windows-powershell-provider.md)