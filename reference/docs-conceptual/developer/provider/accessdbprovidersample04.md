---
title: AccessDBProviderSample04 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ee3a7e56-7331-4f71-9ecb-7a59b8021c68
caps.latest.revision: 10
ms.openlocfilehash: 7096f8066568c214a5902f6943a2c093932d3b56
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72366335"
---
# <a name="accessdbprovidersample04"></a><span data-ttu-id="9bba0-102">AccessDBProviderSample04</span><span class="sxs-lookup"><span data-stu-id="9bba0-102">AccessDBProviderSample04</span></span>

<span data-ttu-id="9bba0-103">Este exemplo mostra como substituir métodos de contêiner para dar suporte a chamadas para os cmdlets `Copy-Item`, `Get-ChildItem`, `New-Item` e `Remove-Item`.</span><span class="sxs-lookup"><span data-stu-id="9bba0-103">This sample shows how to overwrite container methods to support calls to the `Copy-Item`, `Get-ChildItem`, `New-Item`, and `Remove-Item` cmdlets.</span></span> <span data-ttu-id="9bba0-104">Esses métodos devem ser implementados quando o armazenamento de dados contiver itens que são contêineres.</span><span class="sxs-lookup"><span data-stu-id="9bba0-104">These methods should be implemented when the data store contains items that are containers.</span></span> <span data-ttu-id="9bba0-105">Um contêiner é um grupo de itens filho em um item pai comum.</span><span class="sxs-lookup"><span data-stu-id="9bba0-105">A container is a group of child items under a common parent item.</span></span> <span data-ttu-id="9bba0-106">A classe de provedor neste exemplo deriva da classe [System. Management. Automation. Provider. Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) .</span><span class="sxs-lookup"><span data-stu-id="9bba0-106">The provider class in this sample derives from the [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) class.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="9bba0-107">Demonstrar</span><span class="sxs-lookup"><span data-stu-id="9bba0-107">Demonstrates</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9bba0-108">Sua classe de provedor provavelmente será derivada do [System. Management. Automation. Provider. Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)</span><span class="sxs-lookup"><span data-stu-id="9bba0-108">Your provider class will most likely derive from the [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)</span></span>

<span data-ttu-id="9bba0-109">Este exemplo demonstra o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9bba0-109">This sample demonstrates the following:</span></span>

- <span data-ttu-id="9bba0-110">Declarando o atributo `CmdletProvider`.</span><span class="sxs-lookup"><span data-stu-id="9bba0-110">Declaring the `CmdletProvider` attribute.</span></span>

- <span data-ttu-id="9bba0-111">Definindo uma classe de provedor que deriva da classe [System. Management. Automation. Provider. Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) .</span><span class="sxs-lookup"><span data-stu-id="9bba0-111">Defining a provider class that derives from the [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) class.</span></span>

- <span data-ttu-id="9bba0-112">Substituindo o método [System. Management. Automation. Provider. ContainerCmdletProvider. CopyItem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) para alterar o comportamento do cmdlet `Copy-Item`, que permite ao usuário copiar itens de um local para outro.</span><span class="sxs-lookup"><span data-stu-id="9bba0-112">Overwriting the [System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) method to change the behavior of the `Copy-Item` cmdlet which allows the user to copy items from one location to another.</span></span> <span data-ttu-id="9bba0-113">(Este exemplo não mostra como adicionar parâmetros dinâmicos ao cmdlet `Copy-Item`.)</span><span class="sxs-lookup"><span data-stu-id="9bba0-113">(This sample does not show how to add dynamic parameters to the `Copy-Item` cmdlet.)</span></span>

- <span data-ttu-id="9bba0-114">Substituindo o método [System. Management. Automation. Provider. Containercmdletprovider. GetChildItems \*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) para alterar o comportamento do cmdlet Get-ChildItems, que permite ao usuário recuperar os itens filho do item pai.</span><span class="sxs-lookup"><span data-stu-id="9bba0-114">Overwriting the [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) method to change the behavior of the Get-ChildItems cmdlet, which allows the user to retrieve the child items of the parent item.</span></span> <span data-ttu-id="9bba0-115">(Este exemplo não mostra como adicionar parâmetros dinâmicos ao cmdlet Get-ChildItems.)</span><span class="sxs-lookup"><span data-stu-id="9bba0-115">(This sample does not show how to add dynamic parameters to the Get-ChildItems cmdlet.)</span></span>

- <span data-ttu-id="9bba0-116">Substituindo o método [System. Management. Automation. Provider. Containercmdletprovider. getchildnames \*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNames) para alterar o comportamento do cmdlet Get-ChildItems quando o parâmetro `Name` do cmdlet é especificado.</span><span class="sxs-lookup"><span data-stu-id="9bba0-116">Overwriting the [System.Management.Automation.Provider.Containercmdletprovider.Getchildnames\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNames) method to change the behavior of the Get-ChildItems cmdlet when the `Name` parameter of the cmdlet is specified.</span></span>

- <span data-ttu-id="9bba0-117">Substituindo o método [System. Management. Automation. Provider. Containercmdletprovider. NewItem \*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) para alterar o comportamento do cmdlet `New-Item`, que permite ao usuário adicionar itens ao armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="9bba0-117">Overwriting the [System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) method to change the behavior of the `New-Item` cmdlet, which allows the user to add items to the data store.</span></span> <span data-ttu-id="9bba0-118">(Este exemplo não mostra como adicionar parâmetros dinâmicos ao cmdlet `New-Item`.)</span><span class="sxs-lookup"><span data-stu-id="9bba0-118">(This sample does not show how to add dynamic parameters to the `New-Item` cmdlet.)</span></span>

- <span data-ttu-id="9bba0-119">Substituindo o método [System. Management. Automation. Provider. Containercmdletprovider. RemoveItem \*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem) para alterar o comportamento do cmdlet `Remove-Item`.</span><span class="sxs-lookup"><span data-stu-id="9bba0-119">Overwriting the [System.Management.Automation.Provider.Containercmdletprovider.Removeitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem) method to change the behavior of the `Remove-Item` cmdlet.</span></span> <span data-ttu-id="9bba0-120">(Este exemplo não mostra como adicionar parâmetros dinâmicos ao cmdlet `Remove-Item`.)</span><span class="sxs-lookup"><span data-stu-id="9bba0-120">(This sample does not show how to add dynamic parameters to the `Remove-Item` cmdlet.)</span></span>

## <a name="example"></a><span data-ttu-id="9bba0-121">Exemplo</span><span class="sxs-lookup"><span data-stu-id="9bba0-121">Example</span></span>

<span data-ttu-id="9bba0-122">Este exemplo mostra como substituir os métodos necessários para copiar, criar e remover itens, bem como métodos para obter os itens filho de um item pai.</span><span class="sxs-lookup"><span data-stu-id="9bba0-122">This sample shows how to overwrite the methods needed to copy, create, and remove items, as well as methods for getting the child items of a parent item.</span></span>

[!code-csharp[AccessDBProviderSample04.cs](../../../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L11-L1635 "AccessDBProviderSample04.cs")]

## <a name="see-also"></a><span data-ttu-id="9bba0-123">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="9bba0-123">See Also</span></span>

[<span data-ttu-id="9bba0-124">System. Management. Automation. Provider. createcmdletprovider</span><span class="sxs-lookup"><span data-stu-id="9bba0-124">System.Management.Automation.Provider.Itemcmdletprovider</span></span>](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider)

[<span data-ttu-id="9bba0-125">System. Management. Automation. Provider. Containercmdletprovider</span><span class="sxs-lookup"><span data-stu-id="9bba0-125">System.Management.Automation.Provider.Containercmdletprovider</span></span>](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider)

[<span data-ttu-id="9bba0-126">System. Management. Automation. Provider. Navigationcmdletprovider</span><span class="sxs-lookup"><span data-stu-id="9bba0-126">System.Management.Automation.Provider.Navigationcmdletprovider</span></span>](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)

[<span data-ttu-id="9bba0-127">Criando seu provedor do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bba0-127">Designing Your Windows PowerShell Provider</span></span>](./provider-types.md)