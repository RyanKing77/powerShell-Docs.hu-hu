---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Nyomtatók használata
ms.assetid: 4f29ead3-f83b-4706-ac3e-f2154ff38dc5
ms.openlocfilehash: 5638629fdf79371c8eff9ee9194b642034250fff
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686956"
---
# <a name="working-with-printers"></a><span data-ttu-id="46578-103">Nyomtatók használata</span><span class="sxs-lookup"><span data-stu-id="46578-103">Working with Printers</span></span>

<span data-ttu-id="46578-104">Windows PowerShell segítségével nyomtatók kezelése a WMI és a WSH WScript.Network COM objektum használatával.</span><span class="sxs-lookup"><span data-stu-id="46578-104">You can use Windows PowerShell to manage printers by using WMI and the WScript.Network COM object from WSH.</span></span> <span data-ttu-id="46578-105">Mindkét eszköz kombinációját használjuk meghatározott feladatok bemutatásához.</span><span class="sxs-lookup"><span data-stu-id="46578-105">We will use a mix of both tools to demonstrate specific tasks.</span></span>

### <a name="listing-printer-connections"></a><span data-ttu-id="46578-106">Nyomtatókapcsolatok listázása</span><span class="sxs-lookup"><span data-stu-id="46578-106">Listing Printer Connections</span></span>

<span data-ttu-id="46578-107">A nyomtatókat, a számítógépen telepített listában legegyszerűbb módja az, hogy a WMI-vel **Win32_Printer** osztály:</span><span class="sxs-lookup"><span data-stu-id="46578-107">The simplest way to list the printers installed on a computer is to use the WMI **Win32_Printer** class:</span></span>

```powershell
Get-WmiObject -Class Win32_Printer -ComputerName
```

<span data-ttu-id="46578-108">A nyomtatók használatával is listázhatja a **WScript.Network** COM-objektum, általában használt WSH parancsfájlok:</span><span class="sxs-lookup"><span data-stu-id="46578-108">You can also list the printers by using the **WScript.Network** COM object that is typically used in WSH scripts:</span></span>

```powershell
(New-Object -ComObject WScript.Network).EnumPrinterConnections()
```

<span data-ttu-id="46578-109">Mivel ez a parancs a port és nyomtató eszköz nevének megkülönböztető címkék nélkül egyszerű karakterlánc gyűjteményét adja vissza, akkor sem könnyen értelmezni.</span><span class="sxs-lookup"><span data-stu-id="46578-109">Because this command returns a simple string collection of port names and printer device names without any distinguishing labels, it is not easy to interpret.</span></span>

### <a name="adding-a-network-printer"></a><span data-ttu-id="46578-110">A hálózati nyomtatók hozzáadása</span><span class="sxs-lookup"><span data-stu-id="46578-110">Adding a Network Printer</span></span>

<span data-ttu-id="46578-111">Segítségével adhat hozzá egy új hálózati nyomtató **WScript.Network**:</span><span class="sxs-lookup"><span data-stu-id="46578-111">To add a new network printer, use **WScript.Network**:</span></span>

```powershell
(New-Object -ComObject WScript.Network).AddWindowsPrinterConnection("\\Printserver01\Xerox5")
```

### <a name="setting-a-default-printer"></a><span data-ttu-id="46578-112">Alapértelmezett nyomtató beállítása</span><span class="sxs-lookup"><span data-stu-id="46578-112">Setting a Default Printer</span></span>

<span data-ttu-id="46578-113">Az alapértelmezett nyomtató beállítása a WMI használatával, keresse meg a nyomtatót a a **Win32_Printer** gyűjteményt, és ezután meghívja a **SetDefaultPrinter** módszer:</span><span class="sxs-lookup"><span data-stu-id="46578-113">To use WMI to set the default printer, find the printer in the **Win32_Printer** collection and then invoke the **SetDefaultPrinter** method:</span></span>

```powershell
(Get-WmiObject -ComputerName . -Class Win32_Printer -Filter "Name='HP LaserJet 5Si'").SetDefaultPrinter()
```

<span data-ttu-id="46578-114">**WScript.Network** kissé egyszerűbb használatához, mert egy **SetDefaultPrinter** metódus túlterhelését, amely csak a nyomtató neve argumentumként:</span><span class="sxs-lookup"><span data-stu-id="46578-114">**WScript.Network** is a little simpler to use, because it has a **SetDefaultPrinter** method that takes only the printer name as an argument:</span></span>

```powershell
(New-Object -ComObject WScript.Network).SetDefaultPrinter('HP LaserJet 5Si')
```

### <a name="removing-a-printer-connection"></a><span data-ttu-id="46578-115">A nyomtató-kapcsolat eltávolítása</span><span class="sxs-lookup"><span data-stu-id="46578-115">Removing a Printer Connection</span></span>

<span data-ttu-id="46578-116">Nyomtatási kapcsolat eltávolításához használja a **WScript.Network RemovePrinterConnection** módszer:</span><span class="sxs-lookup"><span data-stu-id="46578-116">To remove a printer connection, use the **WScript.Network RemovePrinterConnection** method:</span></span>

```powershell
(New-Object -ComObject WScript.Network).RemovePrinterConnection("\\Printserver01\Xerox5")
```