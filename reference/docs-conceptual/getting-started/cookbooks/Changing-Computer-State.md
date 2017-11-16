---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Számítógép állapotának módosítása"
ms.assetid: 8093268b-27f8-4a49-8871-142c5cc33f01
ms.openlocfilehash: 636690c72b16bf19826b0a7e54ce00114ce30fb6
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="changing-computer-state"></a>Számítógép állapotának módosítása
A számítógép a Windows PowerShell alaphelyzetbe, használja a szabványos parancssori eszköz vagy a WMI-osztályt. Csak az eszköz futtatásához használ a Windows PowerShell, bár egyes külső eszközök a Windows PowerShell használatával kapcsolatos fontos részleteket a dokumentum a Windows PowerShell a számítógép energiaellátási állapot módosítására irányuló szemlélteti.

### <a name="locking-a-computer"></a>A számítógép zárolása
Csak a standard elérhető eszközök közvetlenül a számítógép zárolása, hívni a **LockWorkstation()** működni **user32.dll**:

```
rundll32.exe user32.dll,LockWorkStation
```

Ez a parancs azonnal zárolja a munkaállomást. Használja *rundll32.exe*, amely futtatja a Windows DLL-fájlok (és a szalagtárak ismételt használatra menti) user32.dll, a Windows felügyeleti funkciók a szalagtár futtatásához.

Ha akkor zárolja a munkaállomás gyors felhasználóváltás be van kapcsolva, például a Windows XP, a számítógép megjeleníti az aktuális felhasználó képernyőkímélő indítása helyett a bejelentkezési képernyő.

Állítsa le a Terminálszolgáltatások kiszolgáló munkameneten, használja a **tsshutdn.exe** parancssori eszközt.

### <a name="logging-off-the-current-session"></a>Az aktuális munkamenet kijelentkeztetése
Számos különböző módszert használhatja a helyi rendszer egy munkamenetet kijelentkeztetni. A legegyszerűbb módja, ha a távoli asztal/Terminálszolgáltatások parancssori eszközzel, **logoff.exe** (További részletek a Windows PowerShell parancssorába írja be a **kijelentkezési /?**). Az aktuális aktív munkamenetet kijelentkeztetni, írja be a **kijelentkezési** argumentum nélkül.

Használhatja a **shutdown.exe** a kijelentkezési kapcsolóval eszköz:

```
shutdown.exe -l
```

A harmadik lehetőség egy WMI-vel. A Win32_OperatingSystem osztály Win32Shutdown metódust tartalmaz. A metódus a 0 jelzővel kezdeményezi a kijelentkezési:

```
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(0)
```

További információt, és más szolgáltatások Win32Shutdown metódus kereséséhez tekintse meg a "Win32Shutdown metódus, a Win32_OperatingSystem osztály" az MSDN Webhelyén.

### <a name="shutting-down-or-restarting-a-computer"></a>A Leállítás fázisában vagy a számítógép újraindítása
Leállítása vagy újraindítása a számítógépek olyan általában feladat azonos típusú. Eszközök, amelyek a számítógép leállítása újra fog indulni általában azt is, és ez fordítva is igaz. A Windows PowerShell a számítógép újraindítása esetén két egyszerű lehetőség áll rendelkezésre. Használja a Tsshutdn.exe vagy Shutdown.exe megfelelő argumentumokkal. Részletes használati adatait kaphat **tsshutdn.exe /?** vagy **shutdown.exe /?**.

Is hajtsa végre a leállítási, és indítsa újra a műveletek segítségével **Win32_OperatingSystem** , valamint a Windows PowerShell-ről.

A számítógép leállítása, használja a Win32Shutdown metódus a **1** jelzőt.

```
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(1)
```

Újraindítja az operációs rendszert, használja a Win32Shutdown metódus a **2** jelzőt.

```
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(2)
```

