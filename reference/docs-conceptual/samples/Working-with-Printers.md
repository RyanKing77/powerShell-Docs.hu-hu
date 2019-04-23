---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Nyomtatók használata
ms.assetid: 4f29ead3-f83b-4706-ac3e-f2154ff38dc5
ms.openlocfilehash: 77ebb26369b6a40e9c8c7bbbc52347d614cbf083
ms.sourcegitcommit: f4bd4e116e22c8b5bfcb61680a7c42e58b4da93e
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/22/2019
ms.locfileid: "59984136"
---
# <a name="working-with-printers"></a>Nyomtatók használata

Windows PowerShell segítségével nyomtatók kezelése a WMI és a WSH WScript.Network COM objektum használatával. Mindkét eszköz kombinációját használjuk meghatározott feladatok bemutatásához.

## <a name="listing-printer-connections"></a>Nyomtatókapcsolatok listázása

A nyomtatókat, a számítógépen telepített listában legegyszerűbb módja az, hogy a WMI-vel **Win32_Printer** osztály:

```powershell
Get-WmiObject -Class Win32_Printer -ComputerName
```

A nyomtatók használatával is listázhatja a **WScript.Network** COM-objektum, általában használt WSH parancsfájlok:

```powershell
(New-Object -ComObject WScript.Network).EnumPrinterConnections()
```

Mivel ez a parancs a port és nyomtató eszköz nevének megkülönböztető címkék nélkül egyszerű karakterlánc gyűjteményét adja vissza, akkor sem könnyen értelmezni.

## <a name="adding-a-network-printer"></a>A hálózati nyomtatók hozzáadása

Segítségével adhat hozzá egy új hálózati nyomtató **WScript.Network**:

```powershell
(New-Object -ComObject WScript.Network).AddWindowsPrinterConnection("\\Printserver01\Xerox5")
```

## <a name="setting-a-default-printer"></a>Alapértelmezett nyomtató beállítása

Az alapértelmezett nyomtató beállítása a WMI használatával, keresse meg a nyomtatót a a **Win32_Printer** gyűjteményt, és ezután meghívja a **SetDefaultPrinter** módszer:

```powershell
(Get-WmiObject -ComputerName . -Class Win32_Printer -Filter "Name='HP LaserJet 5Si'").SetDefaultPrinter()
```

**WScript.Network** kissé egyszerűbb használatához, mert egy **SetDefaultPrinter** metódus túlterhelését, amely csak a nyomtató neve argumentumként:

```powershell
(New-Object -ComObject WScript.Network).SetDefaultPrinter('HP LaserJet 5Si')
```

## <a name="removing-a-printer-connection"></a>A nyomtató-kapcsolat eltávolítása

Nyomtatási kapcsolat eltávolításához használja a **WScript.Network RemovePrinterConnection** módszer:

```powershell
(New-Object -ComObject WScript.Network).RemovePrinterConnection("\\Printserver01\Xerox5")
```