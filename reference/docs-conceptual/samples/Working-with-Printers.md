---
ms.date: 06/05/2017
keywords: powershell, cmdlet
title: Trabalhando com impressoras
ms.openlocfilehash: 816388325cc3155f1dbd1bc15fc1736155216092
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "67030668"
---
# <a name="working-with-printers"></a>Trabalhando com impressoras

Você pode usar o Windows PowerShell para gerenciar impressoras usando o WMI e o objeto COM WScript.Network do WSH. Usaremos uma combinação das duas ferramentas para demonstrar as tarefas específicas.

## <a name="listing-printer-connections"></a>Listar conexões de impressora

A maneira mais simples de listar as impressoras instaladas em um computador é usar o a classe do WMI **Win32_Printer**:

```powershell
Get-WmiObject -Class Win32_Printer
```

Você também pode listar as impressoras usando o objeto COM **WScript.Network** que normalmente é usado nos scripts do WSH:

```powershell
(New-Object -ComObject WScript.Network).EnumPrinterConnections()
```

Como esse comando retorna uma coleção simples de cadeia de caracteres de nomes de portas e nomes de dispositivo de impressora sem qualquer distinção rótulos, por isso não é fácil interpretar.

## <a name="adding-a-network-printer"></a>Adicionar uma impressora de rede

Para adicionar uma nova impressora de rede, use **WScript.Network**:

```powershell
(New-Object -ComObject WScript.Network).AddWindowsPrinterConnection("\\Printserver01\Xerox5")
```

## <a name="setting-a-default-printer"></a>Configurar uma impressora padrão

Para usar o WMI para definir a impressora padrão, localize a impressora na coleção **Win32_Printer** e, em seguida, invoque o método **SetDefaultPrinter**:

```powershell
(Get-WmiObject -ComputerName . -Class Win32_Printer -Filter "Name='HP LaserJet 5Si'").SetDefaultPrinter()
```

**WScript.Network** é um pouco mais simples de usar, pois ele tem um método **SetDefaultPrinter** que usa apenas o nome da impressora como um argumento:

```powershell
(New-Object -ComObject WScript.Network).SetDefaultPrinter('HP LaserJet 5Si')
```

## <a name="removing-a-printer-connection"></a>Remover a conexão da impressora

Para remover uma conexão de impressora, use o método **WScript.Network RemovePrinterConnection**:

```powershell
(New-Object -ComObject WScript.Network).RemovePrinterConnection("\\Printserver01\Xerox5")
```
