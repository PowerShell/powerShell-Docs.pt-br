---
ms.date: 09/13/2016
ms.topic: reference
title: Definir os conjuntos de membro padrão para objetos
description: Definir os conjuntos de membro padrão para objetos
ms.openlocfilehash: 919f7ba65322c6a56a27e046fb211bde151abf7d
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92653119"
---
# <a name="defining-default-member-sets-for-objects"></a>Definir os conjuntos de membro padrão para objetos

O conjunto de membros PSStandardMembers é usado pelo Windows PowerShell para definir os conjuntos de propriedades padrão para um objeto. Os conjuntos de propriedades padrão podem ser usados por comandos como os cmdlets de formatação para exibir somente as propriedades definidas pelo conjunto de propriedades. Os conjuntos de propriedades padrão incluem DefaultDisplayProperty, DefaultDisplayPropertySet e DefaultKeyPropertySet. O Windows PowerShell ignora todos os outros conjuntos de membros e quaisquer outros conjuntos de propriedades adicionados ao conjunto de membros PSStandardMembers.

## <a name="member-set-for-systemdiagnosticsprocess"></a>Conjunto de membros para System. Diagnostics. Process

No exemplo a seguir, o conjunto de membros PSStandardMembers define o conjunto de propriedades DefaultDisplayPropertySet para objetos [System. Diagnostics. Process](/dotnet/api/System.Diagnostics.Process) . Esse conjunto de propriedades é usado pelo cmdlet [Format-List](/powershell/module/Microsoft.PowerShell.Utility/Format-List) .

```xml
<Type>
  <Name>System.Diagnostics.Process</Name>
  <Members>
    <MemberSet>
     <Name>PSStandardMembers</Name>
     <Members>
       <PropertySet>
         <Name>DefaultDisplayPropertySet</Name>
         <ReferencedProperties>
           <Name>Id</Name>
           <Name>Handles</Name>
           <Name>CPU</Name>
           <Name>Name</Name>
         </ReferencedProperties>
      </PropertySet>
    </Members>
  </MemberSet>
```

A saída a seguir mostra as propriedades padrão retornadas pelo cmdlet [Format-List](/powershell/module/Microsoft.PowerShell.Utility/Format-List) . Somente as `Id` `Handles` Propriedades,, e `CPU` `Name` são retornadas para cada objeto de processo.

```powershell
Get-Process | format-list
```

```output
Id      : 2036
Handles : 27
CPU     :
Name    : AEADISRV

Id      : 272
Handles : 38
CPU     :
Name    : agrsmsvc
...
```

## <a name="see-also"></a>Consulte Também

[Escrevendo um Cmdlet do Windows PowerShell](./writing-a-windows-powershell-cmdlet.md)
