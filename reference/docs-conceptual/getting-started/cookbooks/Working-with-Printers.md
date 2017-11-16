---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Nyomtatók használata"
ms.assetid: 4f29ead3-f83b-4706-ac3e-f2154ff38dc5
ms.openlocfilehash: c8b4d728c9fddd39e1aeb56d6f9b8ffffe4c7292
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="working-with-printers"></a><span data-ttu-id="e24cb-103">Nyomtatók használata</span><span class="sxs-lookup"><span data-stu-id="e24cb-103">Working with Printers</span></span>
<span data-ttu-id="e24cb-104">A Windows PowerShell segítségével WMI és a WSH WScript.Network COM objektum segítségével.</span><span class="sxs-lookup"><span data-stu-id="e24cb-104">You can use Windows PowerShell to manage printers by using WMI and the WScript.Network COM object from WSH.</span></span> <span data-ttu-id="e24cb-105">Mindkét eszközök vegyesen segítségével meghatározott feladatok bemutatása.</span><span class="sxs-lookup"><span data-stu-id="e24cb-105">We will use a mix of both tools to demonstrate specific tasks.</span></span>

### <a name="listing-printer-connections"></a><span data-ttu-id="e24cb-106">Nyomtatókapcsolatok listázása</span><span class="sxs-lookup"><span data-stu-id="e24cb-106">Listing Printer Connections</span></span>
<span data-ttu-id="e24cb-107">A legegyszerűbben úgy, hogy a nyomtatókat, a számítógépre telepített listában, hogy a WMI-vel **Win32_Printer** osztály:</span><span class="sxs-lookup"><span data-stu-id="e24cb-107">The simplest way to list the printers installed on a computer is to use the WMI **Win32_Printer** class:</span></span>

```
Get-WmiObject -Class Win32_Printer -ComputerName
```

<span data-ttu-id="e24cb-108">A nyomtatók használatával is listázhatja a **WScript.Network** COM-objektum, amelyet főként a WSH parancsfájlban:</span><span class="sxs-lookup"><span data-stu-id="e24cb-108">You can also list the printers by using the **WScript.Network** COM object that is typically used in WSH scripts:</span></span>

```
(New-Object -ComObject WScript.Network).EnumPrinterConnections()
```

<span data-ttu-id="e24cb-109">Ez a parancs visszaadja a port és nyomtató eszköz nevét megkülönböztető címkék nélkül egyszerű karakterlánc gyűjteménye, mert nincs könnyen értelmezhetők.</span><span class="sxs-lookup"><span data-stu-id="e24cb-109">Because this command returns a simple string collection of port names and printer device names without any distinguishing labels, it is not easy to interpret.</span></span>

### <a name="adding-a-network-printer"></a><span data-ttu-id="e24cb-110">A hálózati nyomtató hozzáadása</span><span class="sxs-lookup"><span data-stu-id="e24cb-110">Adding a Network Printer</span></span>
<span data-ttu-id="e24cb-111">Új hálózati nyomtató hozzáadásához használja **WScript.Network**:</span><span class="sxs-lookup"><span data-stu-id="e24cb-111">To add a new network printer, use **WScript.Network**:</span></span>

```
(New-Object -ComObject WScript.Network).AddWindowsPrinterConnection("\\Printserver01\Xerox5")
```

### <a name="setting-a-default-printer"></a><span data-ttu-id="e24cb-112">Alapértelmezett nyomtató beállítása</span><span class="sxs-lookup"><span data-stu-id="e24cb-112">Setting a Default Printer</span></span>
<span data-ttu-id="e24cb-113">WMI segítségével az alapértelmezett nyomtató beállítása, a nyomtató található a **Win32_Printer** gyűjteményben, és ezután meghívja a **SetDefaultPrinter** módszer:</span><span class="sxs-lookup"><span data-stu-id="e24cb-113">To use WMI to set the default printer, find the printer in the **Win32_Printer** collection and then invoke the **SetDefaultPrinter** method:</span></span>

```
(Get-WmiObject -ComputerName . -Class Win32_Printer -Filter "Name='HP LaserJet 5Si'").SetDefaultPrinter()
```

<span data-ttu-id="e24cb-114">**WScript.Network** még egyszerűbb használni, mert egy **SetDefaultPrinter** metódus azon definícióváltozatát csak a nyomtató neve, amelynek argumentuma:</span><span class="sxs-lookup"><span data-stu-id="e24cb-114">**WScript.Network** is a little simpler to use, because it has a **SetDefaultPrinter** method that takes only the printer name as an argument:</span></span>

```
(New-Object -ComObject WScript.Network).SetDefaultPrinter('HP LaserJet 5Si')
```

### <a name="removing-a-printer-connection"></a><span data-ttu-id="e24cb-115">A nyomtató-kapcsolat eltávolítása</span><span class="sxs-lookup"><span data-stu-id="e24cb-115">Removing a Printer Connection</span></span>
<span data-ttu-id="e24cb-116">Egy kapcsolatot eltávolításához használja a **WScript.Network RemovePrinterConnection** módszert:</span><span class="sxs-lookup"><span data-stu-id="e24cb-116">To remove a printer connection, use the **WScript.Network RemovePrinterConnection** method:</span></span>

```
(New-Object -ComObject WScript.Network).RemovePrinterConnection("\\Printserver01\Xerox5")
```

