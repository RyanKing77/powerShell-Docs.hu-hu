---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
contributor: keithb
title: Telepítse és konfigurálja a WMF 5.1
ms.openlocfilehash: e5c7968744a442b4be9f1e43a45e91429a6d6165
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685059"
---
# <a name="install-and-configure-wmf-51"></a>Telepítse és konfigurálja a WMF 5.1 #


## <a name="download-and-install-the-wmf-51-package"></a>Töltse le és telepítse a WMF 5.1-csomagot

Töltse le a WMF 5.1 csomagot a telepíteni kívánt operációs rendszer és architektúra:

| Operációs rendszer       | Előfeltételek           | Csomag hivatkozások                          |
|------------------------|-------------------------|----------------------------------------|
| Windows Server 2012 R2 |                         | [Win8.1AndW2K12R2-KB3191564-x64.msu][] |
| Windows Server 2012    |                         | [W2K12-KB3191565-x64.msu][]            |
| Windows Server 2008 R2 | [.NET-keretrendszer 4.5.2-es verziója][]| [Win7AndW2K8R2-KB3191566-x64.ZIP][]    |
| Windows 8.1            |                         | **x64:** [Win8.1AndW2K12R2-KB3191564-x64.msu][]</br>**x86:** [Win8.1-KB3191564-x86.msu][] |
| Windows 7 SP1          | [.NET-keretrendszer 4.5.2-es verziója][]| **x64:** [Win7AndW2K8R2-KB3191566-x64.ZIP][]</br>**x86:** [Win7-KB3191566-x86.ZIP][] |

[.NET-keretrendszer 4.5.2-es verziója]: https://www.microsoft.com/download/details.aspx?id=42642
[W2K12-KB3191565-x64.msu]: https://go.microsoft.com/fwlink/?linkid=839513
[Win7-KB3191566-x86.ZIP]: https://go.microsoft.com/fwlink/?linkid=839522
[Win7AndW2K8R2-KB3191566-x64.ZIP]: https://go.microsoft.com/fwlink/?linkid=839523
[Win8.1-KB3191564-x86.msu]: https://go.microsoft.com/fwlink/?linkid=839521
[Win8.1AndW2K12R2-KB3191564-x64.msu]: https://go.microsoft.com/fwlink/?linkid=839516

## <a name="install-wmf-51-for-windows-server-2008-r2-and-windows-7"></a>Telepítse a WMF 5.1 Windows Server 2008 R2 és Windows 7

> **Megjegyzés:** Telepítési utasítások Windows 7 és Windows Server 2008 R2 változtak, és eltér a többi csomagot vonatkozó utasításokat. Az alábbiakban a Windows Server 2012 R2, Windows Server 2012 és Windows 8.1 telepítési utasításokat.

**A WMF 5.1 Windows Server 2008 R2 és Windows 7 telepítése**

1. Keresse meg a mappát, amelybe a letöltött ZIP-fájl.

2. Kattintson a jobb gombbal a ZIP-fájlt, és válassza a "Bontsa ki az összes...". A zip-fájl 2 fájlokat tartalmazza: az MSU és az Install-WMF5.1.PS1-parancsfájl tárolásához.
Miután a ZIP-fájl kicsomagolása, másolja bele a bármely Windows 7 vagy Windows Server 2008 R2 rendszerű géphez.

3. Ezt követően a ZIP-fájl tartalmát, nyissa meg a Powershellt rendszergazdaként, majd nyissa meg a mappát, amely tartalmazza a ZIP-fájl tartalmát.

4. A telepítés-Wmf5.1.ps1 parancsprogrammal abban a mappában, és kövesse az utasításokat. Ez a szkript ellenőrizze az előfeltételeket a helyi gépen, és telepítse a WMF 5.1, ha az előfeltételek teljesülnek. Az előfeltételek az alábbiakban láthatók.

Install-WMF5.1.ps1 megkönnyítése érdekében automatizálása a Windows 7 és Windows Server 2008 R2 telepítését a következő paramétereket fogadja:

- AcceptEula: Ha ezt a paramétert tartalmaz, a végfelhasználói licencszerződés automatikusan elfogadja a rendszer, és nem jelenik meg.
- AllowRestart: Ez a paraméter csak használható, ha AcceptEula van megadva. Ha ez a paraméter szerepel, és újraindításra szükség a WMF 5.1 telepítése után, az újraindítás a telepítés befejezése után azonnal rákérdezés nélkül történik meg.

**A WMF 5.1 Windows Server 2008 R2 SP1, Windows 7 SP1 és előfeltételei**

A Windows Server 2008 R2 SP1 vagy Windows 7 SP1, a WMF 5.1 telepítéséhez a következőket:
- Legfrissebb szervizcsomag telepítve kell lennie.
- WMF 3.0 **nem kell** telepíthető. A WMF 5.1 telepítése a WMF 3.0 protokollon keresztül a PSModulePath, ami okozhat más alkalmazások sikertelen elvesztését eredményezi. A WMF 5.1 a telepítés előtt vagy eltávolítási WMF 3.0-s vagy mentse a PSModulePath és kell majd annak visszaállítására manuálisan a WMF 5.1 telepítésének befejezése után.
- A WMF 5.1-es vagy újabb szükséges [.NET-keretrendszer 4.5.2-es](https://www.microsoft.com/en-ca/download/details.aspx?id=42642).
A letöltési helyen található utasításokat követve telepítheti a Microsoft .NET-keretrendszer 4.5.2-es verzióját.

**A WinRM-függőség**

Windows PowerShell Desired State Configuration (DSC) attól függ, hogy a Rendszerfelügyeleti webszolgáltatások.
A Rendszerfelügyeleti webszolgáltatások a Windows Server 2008 R2 és Windows 7 alapértelmezés szerint nincs engedélyezve.
Futtatás `Set-WSManQuickConfig`, egy Windows PowerShell az emelt szintű ahhoz, hogy a WinRM-munkamenetben.


## <a name="install-wmf-51-for-windows-server-2012-r2-windows-server-2012-and-windows-81"></a>Telepítse a WMF 5.1 Windows Server 2012 R2, Windows Server 2012 és Windows 8.1
**Telepítse a Windows Explorer (vagy a Fájlkezelővel, a Windows Server 2012 R2 vagy Windows 8.1)**

1. Lépjen abba a mappába, amelybe letöltötte a MSU-fájlt.
2. Kattintson duplán az MSU a futtatáshoz.

**Telepítése a parancssorból**

1. Az a számítógép architektúrájának megfelelő csomagot a letöltés után nyissa meg egy parancssori ablakot emelt szintű felhasználói jogosultságokkal (Futtatás rendszergazdaként). A Server Core telepítési lehetőségekkel, a Windows Server 2012 R2, Windows Server 2012 vagy Windows Server 2008 R2 SP1, a parancssort emelt szintű felhasználói jogosultságokkal alapértelmezés szerint megnyílik.
2. Módosítsa a könyvtárakat a mappát, amelybe korábban letöltött vagy másolja a WMF 5.1-telepítési csomagot.
3. Futtassa a következő parancsok egyikét:
   - Windows Server 2012 R2 vagy Windows 8.1 x64 rendszert futtató számítógépeken futtassa `Win8.1AndW2K12R2-KB3191564-x64.msu /quiet`.
   - A Windows Server 2012 rendszert futtató számítógépeken futtassa `W2K12-KB3191565-x64.msu /quiet`.
   - X86 Windows 8.1 rendszert futtató számítógépeken futtassa `Win8.1-KB3191564-x86.msu /quiet`.

> [!NOTE]
> A WMF 5.1 telepítéséhez újraindítás szükséges. Használatával a `/quiet` beállítás újraindul figyelmeztetés nélkül a rendszer.
> Használja a `/norestart` azzal elkerülheti a beállítást. Azonban a WMF 5.1-es nem lesz telepítve csak rendelkezik újraindítása.
