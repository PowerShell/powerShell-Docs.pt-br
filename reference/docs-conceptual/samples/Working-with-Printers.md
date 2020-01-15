---
ms.date: 12/23/2019
keywords: powershell, cmdlet
title: Trabalhando com impressoras
ms.openlocfilehash: 47c4f230d023ad93e2b65080feaa1dbfae803d08
ms.sourcegitcommit: 058a6e86eac1b27ca57a11687019df98709ed709
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2020
ms.locfileid: "75736855"
---
# <a name="working-with-printers-in-windows"></a><span data-ttu-id="997cc-103">Como trabalhar com impressoras no Windows</span><span class="sxs-lookup"><span data-stu-id="997cc-103">Working with Printers in Windows</span></span>

<span data-ttu-id="997cc-104">Você pode usar o PowerShell para gerenciar impressoras usando o WMI e o objeto COM **WScript.Network** do WSH.</span><span class="sxs-lookup"><span data-stu-id="997cc-104">You can use PowerShell to manage printers by using WMI and the **WScript.Network** COM object from WSH.</span></span> <span data-ttu-id="997cc-105">Usaremos uma combinação das duas ferramentas para demonstrar as tarefas específicas.</span><span class="sxs-lookup"><span data-stu-id="997cc-105">We will use a mix of both tools to demonstrate specific tasks.</span></span>

## <a name="listing-printer-connections"></a><span data-ttu-id="997cc-106">Listar conexões de impressora</span><span class="sxs-lookup"><span data-stu-id="997cc-106">Listing Printer Connections</span></span>

<span data-ttu-id="997cc-107">A maneira mais simples de listar as impressoras instaladas em um computador é usar o a classe do WMI **Win32_Printer**:</span><span class="sxs-lookup"><span data-stu-id="997cc-107">The simplest way to list the printers installed on a computer is to use the WMI **Win32_Printer** class:</span></span>

```powershell
Get-CimInstance -Class Win32_Printer
```

<span data-ttu-id="997cc-108">Você também pode listar as impressoras usando o objeto COM **WScript.Network** que normalmente é usado nos scripts do WSH:</span><span class="sxs-lookup"><span data-stu-id="997cc-108">You can also list the printers by using the **WScript.Network** COM object that is typically used in WSH scripts:</span></span>

```powershell
(New-Object -ComObject WScript.Network).EnumPrinterConnections()
```

<span data-ttu-id="997cc-109">Como esse comando retorna uma coleção simples de cadeia de caracteres de nomes de portas e nomes de dispositivo de impressora sem qualquer distinção rótulos, por isso não é fácil interpretar.</span><span class="sxs-lookup"><span data-stu-id="997cc-109">Because this command returns a simple string collection of port names and printer device names without any distinguishing labels, it is not easy to interpret.</span></span>

## <a name="adding-a-network-printer"></a><span data-ttu-id="997cc-110">Adicionar uma impressora de rede</span><span class="sxs-lookup"><span data-stu-id="997cc-110">Adding a Network Printer</span></span>

<span data-ttu-id="997cc-111">Para adicionar uma nova impressora de rede, use **WScript.Network**:</span><span class="sxs-lookup"><span data-stu-id="997cc-111">To add a new network printer, use **WScript.Network**:</span></span>

```powershell
(New-Object -ComObject WScript.Network).AddWindowsPrinterConnection("\\Printserver01\Xerox5")
```

## <a name="setting-a-default-printer"></a><span data-ttu-id="997cc-112">Configurar uma impressora padrão</span><span class="sxs-lookup"><span data-stu-id="997cc-112">Setting a Default Printer</span></span>

<span data-ttu-id="997cc-113">Para usar o WMI para definir a impressora padrão, localize a impressora na coleção **Win32_Printer** e, em seguida, invoque o método **SetDefaultPrinter**:</span><span class="sxs-lookup"><span data-stu-id="997cc-113">To use WMI to set the default printer, find the printer in the **Win32_Printer** collection and then invoke the **SetDefaultPrinter** method:</span></span>

```powershell
(Get-CimInstance -Class Win32_Printer -Filter "Name='HP LaserJet 5Si'").SetDefaultPrinter()
```

<span data-ttu-id="997cc-114">**WScript.Network** é um pouco mais simples de usar, pois ele tem um método **SetDefaultPrinter** que usa apenas o nome da impressora como um argumento:</span><span class="sxs-lookup"><span data-stu-id="997cc-114">**WScript.Network** is a little simpler to use, because it has a **SetDefaultPrinter** method that takes only the printer name as an argument:</span></span>

```powershell
(New-Object -ComObject WScript.Network).SetDefaultPrinter('HP LaserJet 5Si')
```

## <a name="removing-a-printer-connection"></a><span data-ttu-id="997cc-115">Remover a conexão da impressora</span><span class="sxs-lookup"><span data-stu-id="997cc-115">Removing a Printer Connection</span></span>

<span data-ttu-id="997cc-116">Para remover uma conexão de impressora, use o método **WScript.Network RemovePrinterConnection**:</span><span class="sxs-lookup"><span data-stu-id="997cc-116">To remove a printer connection, use the **WScript.Network RemovePrinterConnection** method:</span></span>

```powershell
(New-Object -ComObject WScript.Network).RemovePrinterConnection("\\Printserver01\Xerox5")
```
