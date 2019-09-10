---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
contributor: keithb
title: A WMF 5.1 telepítése és konfigurálása
ms.openlocfilehash: 241f52be011e1afc87d25c9a934db0c1e0361b76
ms.sourcegitcommit: 00083f07b13c73b86936e7d7307397df27c63c04
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/10/2019
ms.locfileid: "70848128"
---
# <a name="install-and-configure-wmf-51"></a>A WMF 5,1 telepítése és konfigurálása

> [!IMPORTANT]
> A WMF 5,0-et a WMF 5,1 váltja fel. A WMF 5,0-es verziójával rendelkező felhasználóknak támogatást kell kapniuk a WMF 5,1-re.
> **A WMF 5,1 szükséges a .NET-keretrendszer 4.5.2-es verziójához** (vagy újabb). A telepítés sikeres lesz, de a fő funkciók sikertelenek lesznek, ha a .NET 4.5.2 (vagy újabb) nincs telepítve.

## <a name="download-and-install-the-wmf-51-package"></a>A WMF 5,1-csomag letöltése és telepítése

Töltse le a WMF 5,1-csomagot a telepíteni kívánt operációs rendszerhez és architektúrához:

| Operációs rendszer       | Előfeltételek           | Csomagok hivatkozásai                          |
|------------------------|-------------------------|----------------------------------------|
| Windows Server 2012 R2 |                         | [Win8.1AndW2K12R2-KB3191564-x64.msu][] |
| Windows Server 2012    |                         | [W2K12-KB3191565-x64.msu][]            |
| Windows Server 2008 R2 | [.NET-keretrendszer 4.5.2][]| [Win7AndW2K8R2-KB3191566-x64.ZIP][]    |
| Windows 8.1            |                         | **x64** [Win8.1AndW2K12R2-KB3191564-x64.msu][]</br>**x86** [Win8.1-KB3191564-x86.msu][] |
| Windows 7 SP1          | [.NET-keretrendszer 4.5.2][]| **x64** [Win7AndW2K8R2-KB3191566-x64.ZIP][]</br>**x86** [Win7-KB3191566-x86.ZIP][] |

[.NET-keretrendszer 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42642
[W2K12-KB3191565-x64.msu]: https://go.microsoft.com/fwlink/?linkid=839513
[Win7-KB3191566-x86.ZIP]: https://go.microsoft.com/fwlink/?linkid=839522
[Win7AndW2K8R2-KB3191566-x64.ZIP]: https://go.microsoft.com/fwlink/?linkid=839523
[Win8.1-KB3191564-x86.msu]: https://go.microsoft.com/fwlink/?linkid=839521
[Win8.1AndW2K12R2-KB3191564-x64.msu]: https://go.microsoft.com/fwlink/?linkid=839516

- A WMF 5,1 előzetes verzióját el kell távolítani a WMF 5,1 RTM telepítése előtt.
- A WMF 5,1 közvetlenül a WMF 5,0-es vagy WMF 4,0-en keresztül telepíthető.
- A WMF 5,1 telepítése előtt a Windows 7 és a Windows Server 2008 R2 rendszerre **nem szükséges** a WMF 4,0 telepítése.

## <a name="install-wmf-51-for-windows-server-2008-r2-and-windows-7"></a>A WMF 5,1 telepítése a Windows Server 2008 R2 és a Windows 7 rendszerhez

> [!NOTE]
> A Windows Server 2008 R2 és a Windows 7 telepítési utasításai megváltoztak, és eltérnek a többi csomag utasításainak. A Windows Server 2012 R2, a Windows Server 2012 és a Windows 8,1 telepítési utasításai alább találhatók.

### <a name="wmf-51-prerequisites-for-windows-server-2008-r2-sp1-and-windows-7-sp1"></a>WMF 5,1 előfeltételek a Windows Server 2008 R2 SP1 és a Windows 7 SP1 rendszerhez

A WMF 5,1 telepítése Windows Server 2008 R2 SP1 vagy Windows 7 SP1 rendszeren a következőkre van szükség:

- Telepíteni kell a legújabb szervizcsomagot.
- A WMF 3,0 **nem** telepíthető. A WMF 5,1-es WMF 3,0-es verziójának telepítése a **PSModulePath** (`$env:PSModulePath`) elvesztését eredményezi, ami más alkalmazások meghibásodását is okozhatja. A WMF 5,1 telepítése előtt távolítsa el a WMF 3,0-et, vagy mentse a **PSModulePath** , majd állítsa vissza manuálisan a WMF 5,1 telepítésének befejeződése után.
- A WMF 5,1-ben legalább a [.NET-keretrendszer 4.5.2](https://www.microsoft.com/download/details.aspx?id=42642)-es verzió szükséges.
  A Microsoft .NET-keretrendszer 4.5.2-es verziójára a letöltési hely utasításait követve lehet telepíteni.

### <a name="installing-wmf-51-on-windows-server-2008-r2-and-windows-7"></a>A WMF 5,1 telepítése Windows Server 2008 R2 és Windows 7 rendszeren

1. Navigáljon ahhoz a mappához, amelybe letöltötte a ZIP-fájlt.

2. Kattintson a jobb gombbal a ZIP-fájlra, és válassza az **összes kibontása...** lehetőséget. A zip-fájl két fájlt tartalmaz: egy msu- `Install-WMF5.1.ps1` t és egy parancsfájlt. A ZIP-fájl kicsomagolása után bármely Windows 7 vagy Windows Server 2008 R2 rendszerű gépre másolhatja a tartalmat.

3. A ZIP-fájl tartalmának kibontása után nyissa meg a PowerShellt rendszergazdaként, majd navigáljon a ZIP-fájl tartalmát tartalmazó mappához.

4. Futtassa a `Install-WMF5.1.ps1` szkriptet a mappában, és kövesse az utasításokat. Ez a szkript az előfeltételeket a helyi gépen fogja ellenőriznie, és a WMF 5,1-et telepíti, ha teljesülnek az előfeltételek. Az előfeltételek az alábbiakban láthatók.

   `Install-WMF5.1.ps1`a következő paraméterekkel könnyítheti meg a telepítést a Windows Server 2008 R2 és a Windows 7 rendszereken:

   - **AcceptEula**: Ha ezt a paramétert tartalmazza, a rendszer automatikusan elfogadja a végfelhasználói licencszerződést, és nem fog megjelenni.
   - **AllowRestart**: Ez a paraméter csak akkor használható, ha meg van adva a AcceptEula. Ha ez a paraméter szerepel, és a WMF 5,1 telepítése után újraindításra van szükség, akkor az újraindítás a telepítés befejeződése után azonnal megtörténik.

## <a name="winrm-dependency"></a>WinRM-függőség

A Windows PowerShell kívánt állapotának konfigurációja (DSC) a WinRM szolgáltatástól függ. A WinRM szolgáltatás alapértelmezés szerint nincs engedélyezve a Windows Server 2008 R2 és a Windows 7 rendszeren. Futtassa `Set-WSManQuickConfig`a parancsot egy Windows PowerShell emelt szintű munkamenetben a WinRM engedélyezéséhez.

## <a name="install-wmf-51-for-windows-server-2012-r2-windows-server-2012-and-windows-81"></a>A WMF 5,1 telepítése a Windows Server 2012 R2, a Windows Server 2012 és a Windows 8,1 rendszerhez

### <a name="install-from-windows-file-explorer"></a>Telepítés a Windows Fájlkezelőből

1. Navigáljon ahhoz a mappához, amelybe letöltötte az MSU-fájlt.
2. Kattintson duplán az MSU-re a futtatásához.

### <a name="installing-from-the-command-prompt"></a>Telepítés a parancssorból

1. A számítógép architektúrájának megfelelő csomag letöltése után nyisson meg egy parancssori ablakot emelt szintű felhasználói jogosultságokkal (Futtatás rendszergazdaként). A Windows Server 2012 R2, a Windows Server 2012 vagy a Windows Server 2008 R2 SP1 Server Core telepítési beállításainál a parancssor alapértelmezés szerint emelt szintű felhasználói jogosultságokkal nyílik meg.
2. Módosítsa a könyvtárakat arra a mappára, amelybe a WMF 5,1 telepítőcsomagot letöltötte vagy átmásolta.
3. Futtassa a következő parancsok egyikét:
   - Futtassa `Win8.1AndW2K12R2-KB3191564-x64.msu /quiet`a következőt a Windows Server 2012 R2 vagy Windows 8,1 x64 rendszert futtató számítógépeken:.
   - A Windows Server 2012 rendszert futtató számítógépeken futtassa `W2K12-KB3191565-x64.msu /quiet`a következőt:.
   - A Windows 8,1 x86 rendszert futtató számítógépeken futtassa a `Win8.1-KB3191564-x86.msu /quiet`parancsot.

> [!NOTE]
> A WMF 5,1 telepítéséhez újraindítás szükséges. A `/quiet` lehetőség használata figyelmeztetés nélkül újraindítja a rendszerét. Az újraindítás `/norestart` elkerüléséhez használja a lehetőséget. A WMF 5,1 azonban addig nem lesz telepítve, amíg újra nem indítja.
