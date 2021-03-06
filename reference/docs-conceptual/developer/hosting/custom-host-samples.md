---
ms.date: 09/13/2016
ms.topic: reference
title: Amostras de host personalizadas
description: Amostras de host personalizadas
ms.openlocfilehash: 939b9f5d6bbc3ccf1ac95343e897ecffef0a2f42
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92649321"
---
# <a name="custom-host-samples"></a>Amostras de host personalizadas

Esta seção inclui um código de exemplo para a gravação de um host personalizado. Você pode usar Microsoft Visual Studio para criar um aplicativo de console e, em seguida, copiar o código dos tópicos nesta seção para seu aplicativo host.

## <a name="in-this-section"></a>Nesta seção

 [Exemplo de Host01](./host01-sample.md) Este exemplo mostra como implementar um aplicativo host que usa um host personalizado básico.

 [Exemplo de Host02](./host02-sample.md) Este exemplo mostra como gravar um aplicativo host que usa o tempo de execução do Windows PowerShell junto com uma implementação de host personalizada. O aplicativo host define a cultura do host como alemão, executa o cmdlet [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) e exibe os resultados como você os veria usando pwrsh.exe e, em seguida, imprime os dados e a hora atuais em alemão.

 [Exemplo de Host03](./host03-sample.md) Este exemplo mostra como criar um aplicativo de host baseado em console interativo que lê os comandos da linha de comando, executa os comandos e, em seguida, exibe os resultados para o console.

 [Exemplo de Host04](./host04-sample.md) Este exemplo mostra como criar um aplicativo de host baseado em console interativo que lê os comandos da linha de comando, executa os comandos e, em seguida, exibe os resultados para o console. Esse aplicativo host também dá suporte a exibições de avisos que permitem ao usuário especificar várias opções.

 [Exemplo de Host05](./host05-sample.md) Este exemplo mostra como criar um aplicativo de host baseado em console interativo que lê os comandos da linha de comando, executa os comandos e, em seguida, exibe os resultados para o console. Esse aplicativo host também dá suporte a chamadas para computadores remotos usando os cmdlets [Enter-PSSession](/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession) e [Exit-PSSession](/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession)

 [Exemplo de Host06](./host06-sample.md) Este exemplo mostra como criar um aplicativo de host baseado em console interativo que lê os comandos da linha de comando, executa os comandos e, em seguida, exibe os resultados para o console. Além disso, este exemplo usa as APIs do Criador de Token para especificar a cor do texto inserido pelo usuário.

## <a name="see-also"></a>Consulte Também
