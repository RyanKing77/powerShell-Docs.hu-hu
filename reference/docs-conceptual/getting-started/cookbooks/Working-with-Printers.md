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
# <a name="working-with-printers"></a>Nyomtatók használata
A Windows PowerShell segítségével WMI és a WSH WScript.Network COM objektum segítségével. Mindkét eszközök vegyesen segítségével meghatározott feladatok bemutatása.

### <a name="listing-printer-connections"></a>Nyomtatókapcsolatok listázása
A legegyszerűbben úgy, hogy a nyomtatókat, a számítógépre telepített listában, hogy a WMI-vel **Win32_Printer** osztály:

```
Get-WmiObject -Class Win32_Printer -ComputerName
```

A nyomtatók használatával is listázhatja a **WScript.Network** COM-objektum, amelyet főként a WSH parancsfájlban:

```
(New-Object -ComObject WScript.Network).EnumPrinterConnections()
```

Ez a parancs visszaadja a port és nyomtató eszköz nevét megkülönböztető címkék nélkül egyszerű karakterlánc gyűjteménye, mert nincs könnyen értelmezhetők.

### <a name="adding-a-network-printer"></a>A hálózati nyomtató hozzáadása
Új hálózati nyomtató hozzáadásához használja **WScript.Network**:

```
(New-Object -ComObject WScript.Network).AddWindowsPrinterConnection("\\Printserver01\Xerox5")
```

### <a name="setting-a-default-printer"></a>Alapértelmezett nyomtató beállítása
WMI segítségével az alapértelmezett nyomtató beállítása, a nyomtató található a **Win32_Printer** gyűjteményben, és ezután meghívja a **SetDefaultPrinter** módszer:

```
(Get-WmiObject -ComputerName . -Class Win32_Printer -Filter "Name='HP LaserJet 5Si'").SetDefaultPrinter()
```

**WScript.Network** még egyszerűbb használni, mert egy **SetDefaultPrinter** metódus azon definícióváltozatát csak a nyomtató neve, amelynek argumentuma:

```
(New-Object -ComObject WScript.Network).SetDefaultPrinter('HP LaserJet 5Si')
```

### <a name="removing-a-printer-connection"></a>A nyomtató-kapcsolat eltávolítása
Egy kapcsolatot eltávolításához használja a **WScript.Network RemovePrinterConnection** módszert:

```
(New-Object -ComObject WScript.Network).RemovePrinterConnection("\\Printserver01\Xerox5")
```

