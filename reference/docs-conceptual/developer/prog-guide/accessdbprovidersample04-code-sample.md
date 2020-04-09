---
title: Exemplo de código AccessDbProviderSample04 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f9374c4a-e499-4516-9eb6-107c59df98d9
caps.latest.revision: 7
ms.openlocfilehash: 60f0ed4e3d39ee93ab63023161d09a6c7b914798
ms.sourcegitcommit: 7f2479edd329dfdc55726afff7019d45e45f9156
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80978569"
---
# <a name="accessdbprovidersample04-code-sample"></a><span data-ttu-id="a0fce-102">Exemplo de código AccessDbProviderSample04</span><span class="sxs-lookup"><span data-stu-id="a0fce-102">AccessDbProviderSample04 Code Sample</span></span>

<span data-ttu-id="a0fce-103">O código a seguir mostra a implementação do provedor do Windows PowerShell descrito em [criando um provedor de contêiner do Windows PowerShell](./creating-a-windows-powershell-container-provider.md).</span><span class="sxs-lookup"><span data-stu-id="a0fce-103">The following code shows the implementation of the Windows PowerShell provider described in [Creating a Windows PowerShell Container Provider](./creating-a-windows-powershell-container-provider.md).</span></span>
<span data-ttu-id="a0fce-104">Esse provedor funciona em armazenamentos de dados de várias camadas.</span><span class="sxs-lookup"><span data-stu-id="a0fce-104">This provider works on multi-layer data stores.</span></span> <span data-ttu-id="a0fce-105">Para esse tipo de armazenamento de dados, o nível superior do repositório contém os itens raiz e cada nível subsequente é referido como um nó de itens filho.</span><span class="sxs-lookup"><span data-stu-id="a0fce-105">For this type of data store, the top level of the store contains the root items and each subsequent level is referred to as a node of child items.</span></span> <span data-ttu-id="a0fce-106">Ao permitir que o usuário trabalhe nesses nós filho, um usuário pode interagir hierarquicamente por meio do armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="a0fce-106">By allowing the user to work on these child nodes, a user can interact hierarchically through the data store.</span></span>

## <a name="code-sample"></a><span data-ttu-id="a0fce-107">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="a0fce-107">Code Sample</span></span>

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample04/AccessDBProviderSample04.cs" range="11-1635":::

## <a name="see-also"></a><span data-ttu-id="a0fce-108">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="a0fce-108">See Also</span></span>

[<span data-ttu-id="a0fce-109">SDK do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0fce-109">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
