---
title: Como criar um snap-in do Windows PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snap-ins [PowerShell SDK], examples
ms.assetid: 71bd9b2c-5f2e-4aa8-b5fe-08c956540d37
caps.latest.revision: 10
ms.openlocfilehash: 43199544dc02ccae4b61053c30d6ed36576adfcf
ms.sourcegitcommit: 2aec310ad0c0b048400cb56f6fa64c1e554c812a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2020
ms.locfileid: "83811325"
---
# <a name="how-to-create-a-windows-powershell-snap-in"></a>Como criar um snap-in do Windows PowerShell

Um snap-in do Windows PowerShell fornece um mecanismo para registrar conjuntos de cmdlets e outro provedor do Windows PowerShell com o Shell, estendendo assim a funcionalidade do Shell. Um snap-in do Windows PowerShell pode registrar todos os cmdlets e provedores em um único assembly ou pode registrar uma lista específica de cmdlets e provedores.

Os assemblies de snap-in devem ser instalados em um diretório protegido, assim como seriam com outros sistemas operacionais. Caso contrário, os usuários mal-intencionados podem substituir um assembly por código não seguro.

## <a name="windows-powershell-snap-in-classes"></a>Classes de snap-in do Windows PowerShell

Todas as classes de snap-in do Windows PowerShell derivam das classes [System. Management. Automation. PSSnapin](/dotnet/api/System.Management.Automation.PSSnapIn) ou [System. Management. Automation. CustomPSSnapIn](/dotnet/api/System.Management.Automation.CustomPSSnapIn) .

## <a name="examples"></a>Exemplos

[Escrevendo um snap-in do Windows PowerShell](./writing-a-windows-powershell-snap-in.md): Este exemplo mostra como criar um snap-in que é usado para registrar todos os cmdlets e provedores em um assembly.

[Escrevendo um snap-in personalizado do Windows PowerShell](./writing-a-custom-windows-powershell-snap-in.md): Este exemplo mostra como criar um snap-in personalizado que é usado para registrar um conjunto específico de cmdlets e provedores que podem ou não existir em um único assembly.

## <a name="see-also"></a>Consulte Também

[System. Management. Automation. PSSnapIn](/dotnet/api/System.Management.Automation.PSSnapIn)

[System. Management. Automation. CustomPSSnapIn](/dotnet/api/System.Management.Automation.CustomPSSnapIn)

[Registrar cmdlets](./registering-cmdlets.md)

[SDK do shell do Windows PowerShell](../windows-powershell-reference.md)