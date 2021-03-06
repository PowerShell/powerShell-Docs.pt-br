---
ms.date: 12/31/2019
title: A hierarquia de modelo do objeto do ISE
description: Este artigo mostra a hierarquia de objetos que fazem parte do ISE do Windows PowerShell.
ms.openlocfilehash: 00980cda72f05bc6ccb398079b129de13a98f783
ms.sourcegitcommit: 488a940c7c828820b36a6ba56c119f64614afc29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92658331"
---
# <a name="the-ise-object-model-hierarchy"></a>A hierarquia de modelo do objeto do ISE

Este artigo mostra a hierarquia de objetos que fazem parte do ISE (Ambiente de Script Integrado) do Windows PowerShell. O ISE do Windows PowerShell está incluído no Windows PowerShell 3.0, 4.0 e 5.1. Clique um objeto para levá-lo até a documentação de referência da classe que define o objeto.

## <a name="psise-object"></a>Objeto $psISE

O objeto `$psISE` é o [objeto raiz](The-ObjectModelRoot-Object.md) da hierarquia de objeto ISE do Windows PowerShell. Localizado no nível superior, disponibiliza os seguintes objetos para script:

## <a name="psisecurrentfile"></a>[$psISE.CurrentFile](The-ISEFile-Object.md)

O objeto `$psISE.CurrentFile` é uma instância da classe [ISEFile](The-ISEFile-Object.md).

## <a name="psisecurrentpowershelltab"></a>[$psISE.CurrentPowerShellTab](The-PowerShellTab-Object.md)

O objeto `$psISE.CurrentPowerShellTab` é uma instância da classe [PowerShellTab](The-PowerShellTab-Object.md).

## <a name="psisecurrentvisiblehorizontaltool"></a>$psISE.CurrentVisibleHorizontalTool

O objeto `$psISE.CurrentVisibleHorizontalTool` é uma instância da classe [ISEAddOnTool](The-ISEAddOnTool-Object.md). Ele representa a ferramenta complementar instalada que está encaixada atualmente na borda superior da janela do ISE do Windows PowerShell.

## <a name="psisecurrentvisibleverticaltool"></a>$psISE.CurrentVisibleVerticalTool

O objeto `$psISE.CurrentVisibleHorizontalTool` é uma instância da classe [ISEAddOnTool](The-ISEAddOnTool-Object.md). Ele representa a ferramenta complementar instalada que está encaixada atualmente na borda superior direita da janela do ISE do Windows PowerShell.

## <a name="psiseoptions"></a>[$psISE.Options](The-ISEOptions-Object.md)

O objeto `$psISE.Options` é uma instância da classe [ISEOptions](The-ISEOptions-Object.md). O objeto ISEOptions representa várias configurações para o ISE do Windows PowerShell. Ele é uma instância da classe Microsoft.PowerShell.Host.ISE.ISEOptions.

## <a name="psisepowershelltabs"></a>[$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md)

O objeto `$psISE.PowerShellTabs` é uma instância da classe [PowerShellTabCollection](The-PowerShellTabCollection-Object.md). É uma coleção de todas as guias do PowerShell abertas no momento que representam os ambientes de execução disponíveis do Windows PowerShell no computador local ou em computadores remotos conectados. Cada membro da coleção é uma instância da classe [PowerShellTab](The-PowerShellTab-Object.md).

## <a name="see-also"></a>Consulte Também

- [Objetivo do modelo de objeto de script do ISE do Windows PowerShell](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [A hierarquia de modelo de objeto do ISE](The-ISE-Object-Model-Hierarchy.md)
