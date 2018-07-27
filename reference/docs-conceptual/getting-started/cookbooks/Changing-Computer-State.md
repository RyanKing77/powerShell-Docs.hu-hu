---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: A számítógép állapotának módosítása
ms.assetid: 8093268b-27f8-4a49-8871-142c5cc33f01
ms.openlocfilehash: 4b5b4adb349dd8036117c364ed2ebb1ffaf8c88f
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/26/2018
ms.locfileid: "39267885"
---
# <a name="changing-computer-state"></a>A számítógép állapotának módosítása

Alaphelyzetbe állítani a számítógépet a Windows PowerShellben, használhatja a szabványos parancssori eszköz vagy egy WMI-osztály. Windows PowerShell csak az eszköz futtatásához használ, bár egyes külső eszközök a Windows PowerShell használatával kapcsolatos fontos részleteket megtudhatja, hogyan kell módosítani a Windows PowerShellben a számítógép energiaállapotát szemlélteti.

### <a name="locking-a-computer"></a>A számítógép zárolása

Közvetlenül a szabványos elérhető eszközöket a számítógép zárolása csak úgy, hogy hívja a **LockWorkstation()** függvényével **user32.dll**:

```
rundll32.exe user32.dll,LockWorkStation
```

Ez a parancs azonnal zárolja a munkaállomáson. Használ *rundll32.exe*, amely futtatja a Windows DLL-fájlok (és a szalagtárak ismételt használatra menti) user32.dll, egy könyvtár Windows-felügyeleti funkciók végrehajtásához.

Ha zárolja munkaállomás gyors felhasználóváltás engedélyezve van, például a Windows XP, a számítógép megjeleníti az aktuális felhasználó képernyőkímélő indítása helyett a felhasználó bejelentkezési képernyő.

Állítsa le a Terminálszolgáltatások kiszolgáló adott munkamenetek, használja a **tsshutdn.exe** parancssori eszköz.

### <a name="logging-off-the-current-session"></a>Az aktuális munkamenet kijelentkeztetése

Számos különböző módszer használatával a helyi rendszer egy munkamenetet kijelentkeztetni. A legegyszerűbb módja, ha a távoli asztal/Terminálszolgáltatások parancssori eszköz **logoff.exe** (részletek, a Windows PowerShell parancssorába írja be a következőt **kijelentkezési /?**). Kijelentkezés az aktuális aktív munkamenet, írja be a **kijelentkezési** argumentumok nélkül.

Is használhatja a **shutdown.exe** eszközben a kijelentkezési lehetőséget:

```
shutdown.exe -l
```

Egy harmadik lehetőség, hogy a WMI használható. A Win32_OperatingSystem osztály egy Win32Shutdown metoda má. A metódus hívása a 0 jelző kezdeményezi a kijelentkezési:

```powershell
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(0)
```

További információt, és egyéb funkciók Win32Shutdown metody található tekintse meg a "Win32Shutdown metódus, a Win32_OperatingSystem osztály" az MSDN webhelyen.

### <a name="shutting-down-or-restarting-a-computer"></a>Leállítás vagy a számítógép újraindítása

Leállítása vagy újraindítása a számítógépek olyan általánosan feladat azonos típusú. Eszközök, amelyek a számítógép leállítása általában újraindul, valamint – és fordítva. A Windows PowerShell a számítógép újraindítása két egyszerű lehetőség van. Használhatja a Tsshutdn.exe vagy Shutdown.exe megfelelő argumentumokkal. A részletes használati információkat szerezhet a **tsshutdn.exe /?** vagy **shutdown.exe /?**.

Hajtsa végre a leállítási is, és indítsa újra közvetlenül a Windows PowerShell, valamint a műveletek.

A számítógép leállítása, használja a stop-computer parancs

```powershell
stop-computer
```

Indítsa újra az operációs rendszer, a paranccsal a számítógép újraindítása

```powershell
restart-computer
```
