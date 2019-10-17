---
title: Arquivo de exemplo XML HelpInfo | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6544070f-5549-407f-8603-5df60fe9e013
caps.latest.revision: 7
ms.openlocfilehash: 11804db56ec47554e82f04fe6954920ad9577370
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72360805"
---
# <a name="helpinfo-xml-sample-file"></a><span data-ttu-id="c84ff-102">Arquivo de exemplo XML HelpInfo</span><span class="sxs-lookup"><span data-stu-id="c84ff-102">HelpInfo XML Sample File</span></span>

<span data-ttu-id="c84ff-103">Este tópico exibe um exemplo de um arquivo de informações de ajuda atualizável bem formado, normalmente conhecido como "arquivo XML HelpInfo".</span><span class="sxs-lookup"><span data-stu-id="c84ff-103">This topic displays a sample of a well-formed Updatable Help Information file, commonly known as "HelpInfo XML file."</span></span> <span data-ttu-id="c84ff-104">Neste arquivo de exemplo, os elementos de cultura da interface do usuário são organizados em ordem alfabética pelo nome de cultura da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="c84ff-104">In this sample file, the UI culture elements are arranged in alphabetical order by UI culture name.</span></span> <span data-ttu-id="c84ff-105">A ordenação alfabética é uma prática recomendada, mas não é necessária.</span><span class="sxs-lookup"><span data-stu-id="c84ff-105">Alphabetical ordering is a best practice, but it is not required.</span></span>

## <a name="helpinfo-xml-sample-file"></a><span data-ttu-id="c84ff-106">Arquivo de exemplo XML HelpInfo</span><span class="sxs-lookup"><span data-stu-id="c84ff-106">HelpInfo XML Sample File</span></span>

```xml

<?xml version="1.0" encoding="utf-8"?>
<HelpInfo xmlns="http://schemas.microsoft.com/powershell/help/2010/05">
   <HelpContentURI>http://go.microsoft.com/fwlink/?LinkID=141553</HelpContentURI>
   <SupportedUICultures>
    <UICulture>
      <UICultureName>de-DE</UICultureName>
      <UICultureVersion>2.15.0.10</UICultureVersion>
    </UICulture>
    <UICulture>
      <UICultureName>en-US</UICultureName>
      <UICultureVersion>3.2.0.7</UICultureVersion>
    </UICulture>
    <UICulture>
      <UICultureName>it-IT</UICultureName>
      <UICultureVersion>1.1.0.5</UICultureVersion>
    </UICulture>
    <UICulture>
      <UICultureName>ja-JP</UICultureName>
      <UICultureVersion>3.2.0.4</UICultureVersion>
    </UICulture>
   </SupportedUICultures>
</HelpInfo>

```