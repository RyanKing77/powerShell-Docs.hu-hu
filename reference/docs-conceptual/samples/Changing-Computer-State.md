---
ms.date: 06/05/2017
keywords: PowerShell, parancsmag
title: A számítógép állapotának módosítása
ms.openlocfilehash: de3e31e358548943a015b7bba275c4461202b20f
ms.sourcegitcommit: d1ba596f9e0d4df9565601a70687a126d535c917
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/05/2019
ms.locfileid: "70386284"
---
# <a name="changing-computer-state"></a>A számítógép állapotának módosítása

Ha a Windows PowerShellben szeretné visszaállítani a számítógépeket, használja a szabványos parancssori eszközt, a WMI-t vagy a CIM-osztályt. Bár a Windows PowerShellt csak az eszköz futtatására használja, megtudhatja, hogyan módosíthatja a számítógép energiagazdálkodási állapotát a Windows PowerShellben, és bemutatja a külső eszközök Windows PowerShellben való használatának fontos részleteit.

## <a name="locking-a-computer"></a>Számítógép zárolása

A számítógépek közvetlenül a szabványos elérhető eszközökkel való zárolásának egyetlen módja a **LockWorkstation ()** függvény meghívása a **user32. dll fájlban**:

```
rundll32.exe user32.dll,LockWorkStation
```

Ez a parancs azonnal zárolja a munkaállomást. A rendszer a *rundll32. exe fájlt*használja, amely Windows DLL-eket futtat (és a könyvtárakat ismételt használatra menti) a user32. dll futtatásához, a Windows Management functions könyvtárához.

Amikor zárol egy munkaállomást, miközben a gyors felhasználói váltás engedélyezve van, például Windows XP rendszeren, a számítógép a felhasználó bejelentkezési képernyőjét jeleníti meg, nem pedig az aktuális felhasználó képernyővédőjét.

A **tsshutdn. exe** parancssori eszköz segítségével leállíthatja az egyes munkameneteket a terminálkiszolgálón.

## <a name="logging-off-the-current-session"></a>Az aktuális munkamenet kijelentkezése

Számos különböző technikát használhat a helyi rendszerbeli munkamenetből való kijelentkezéshez. A legegyszerűbb módszer a Távoli asztal/Terminálszolgáltatások parancssori eszköz, a **kijelentkezés. exe** (a részletekért, a Windows PowerShell parancssorába írja be a következőt: **kijelentkezés/?** ). Az aktuális aktív munkamenet kijelentkezéséhez írja be a következőt argumentumok nélkül: **kijelentkezés** .

Használhatja a **shutdown. exe** eszközt is a kijelentkezési lehetőséggel:

```
shutdown.exe -l
```

Egy másik lehetőség a WMI használata. A Win32_OperatingSystem osztály Win32Shutdown metódussal rendelkezik. A metódus meghívása a 0 jelölővel kezdeményezi a kijelentkezést:

```powershell
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(0)
```

További információért és a Win32Shutdown metódus egyéb funkcióinak megkereséséhez tekintse meg az MSDN "Win32_OperatingSystem osztály Win32Shutdown metódusa" című részét.

Végül a CIM-t ugyanazzal a Win32_OperatingSystem osztállyal használhatja, mint a WMI-metódus fentebb leírtak szerint.

```powershell
Get-CIMInstance -Classname Win32_OperatingSystem | Invoke-CimMethod -MethodName Shutdown
```

## <a name="shutting-down-or-restarting-a-computer"></a>Számítógép leállítása vagy újraindítása

A számítógépek leállítása és újraindítása általában azonos típusú feladat. A számítógép leállítására szolgáló eszközök általában is újraindulnak, és fordítva. Két egyszerű lehetőség áll rendelkezésre a számítógép Windows PowerShellből való újraindításához. A megfelelő argumentumokkal használja a tsshutdn. exe vagy a shutdown. exe fájlt. Részletes használati adatokat a **tsshutdn. exe/?** címről kaphat. vagy a **shutdown. exe/?** .

Emellett közvetlenül a Windows PowerShellből is elvégezheti a leállítási és újraindítási műveleteket.

A számítógép leállításához használja a stop-Computer parancsot

```powershell
Stop-Computer
```

Az operációs rendszer újraindításához használja a restart-Computer parancsot.

```powershell
Restart-Computer
```

A számítógép azonnali újraindításának kényszerítéséhez használja a-Force paramétert.

```powershell
Restart-Computer -Force
```
