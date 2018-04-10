---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
contributor: keithb
title: Telepítse és konfigurálja a WMF 5.1
ms.openlocfilehash: e747487873c7c15c2bea3fca7136630ab2b572f7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="install-and-configure-wmf-51"></a>Telepítse és konfigurálja a WMF 5.1 #


## <a name="download-and-install-the-wmf-51-package"></a>Töltse le és telepítse a WMF 5.1 csomag

A telepíteni kívánt operációs rendszer és architektúra a WMF 5.1-csomagjának letöltése:

| Operációs rendszer       | Előfeltételek           | Csomag hivatkozások                          |
|------------------------|-------------------------|----------------------------------------|
| Windows Server 2012 R2 |                         | [Win8.1AndW2K12R2-KB3191564-x64.msu][] |
| Windows Server 2012    |                         | [W2K12-KB3191565-x64.msu][]            |
| Windows Server 2008 R2 | [.NET-keretrendszer 4.5.2][]| [Win7AndW2K8R2-KB3191566-x64.ZIP][]    |
| A Windows 8.1            |                         | **x64:** [Win8.1AndW2K12R2-KB3191564-x64.msu][]</br>**x86:** [Win8.1-KB3191564-x86.msu][] |
| Windows 7 SP1          | [.NET-keretrendszer 4.5.2][]| **x64:** [Win7AndW2K8R2-KB3191566-x64.ZIP][]</br>**x86:** [Win7-KB3191566-x86.ZIP][] |

[.NET-keretrendszer 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42642
[W2K12-KB3191565-x64.msu]: https://go.microsoft.com/fwlink/?linkid=839513
[Win7-KB3191566-x86.ZIP]: https://go.microsoft.com/fwlink/?linkid=839522
[Win7AndW2K8R2-KB3191566-x64.ZIP]: https://go.microsoft.com/fwlink/?linkid=839523
[Win8.1-KB3191564-x86.msu]: https://go.microsoft.com/fwlink/?linkid=839521
[Win8.1AndW2K12R2-KB3191564-x64.msu]: https://go.microsoft.com/fwlink/?linkid=839516

## <a name="install-wmf-51-for-windows-server-2008-r2-and-windows-7"></a>5.1 a WMF telepítése Windows Server 2008 R2 és Windows 7

> **Megjegyzés:** telepítési utasításokat Windows 7 és Windows Server 2008 R2 megváltoztak, és eltér a többi csomagot az utasításokat. Telepítési utasításokat a Windows Server 2012 R2, Windows Server 2012 és Windows 8.1 rendszer alatt.

**5.1 a WMF telepítése a Windows Server 2008 R2 és Windows 7**

1. Keresse meg a mappát, amelybe letöltötte a ZIP-fájl.

2. Kattintson a jobb gombbal a ZIP-fájl, és válassza a "Bontsa ki az összes...". A Zip 2 fájlokat tartalmazza: az MSU és az Install-WMF5.1.PS1 parancsfájlt.
Miután a ZIP-fájl kicsomagolása, másolja a tartalmát a Windows 7 vagy Windows Server 2008 R2 rendszerű gépek.

3. Ezt követően a ZIP-fájl tartalmát, nyissa meg a Powershellt rendszergazdaként, majd keresse meg a mappát, amely tartalmazza a ZIP-fájl tartalmát.

4. A telepítés-Wmf5.1.ps1 parancsprogrammal abban a mappában, és kövesse az utasításokat. Ez a parancsfájl a helyi számítógépen az Előfeltételek ellenőrzése, és telepítse a WMF 5.1, ha az előfeltételek teljesülnek. Az Előfeltételek alább láthatók.

Install-WMF5.1.ps1 megkönnyítése érdekében a Windows Server 2008 R2 és Windows 7 a telepítés automatizálása a következő paramétereket fogadja:

- AcceptEula: Ha ez a paraméter tartalmazza, a végfelhasználói licencszerződés automatikusan el van fogadva és nem jelenik meg.
- AllowRestart: Ez a paraméter csak használható, ha AcceptEula szerepel. Ha ez a paraméter szerepel, és WMF 5.1 telepítése után szükség egy újraindítás, akkor az újraindítás a telepítés befejezése után azonnal értesítése nélkül történik.

**WMF 5.1 Windows Server 2008 R2 SP1 és Windows 7 SP1 előfeltételei**

A Windows Server 2008 R2 SP1 vagy a Windows 7 SP1, a WMF 5.1 telepítéséhez a következő:
- Telepítenie kell a legújabb szervizcsomaggal.
- A WMF 3.0 **nem kell** telepíthető. WMF 5.1 telepítése a WMF 3.0 protokollon keresztül a PSModulePath, más alkalmazások sikertelenségét okozó elvesztését eredményezi. WMF 5.1 a telepítés előtt vagy eltávolítási WMF 3.0 vagy mentse a PSModulePath és kell majd állítsa vissza azt manuálisan WMF 5.1 telepítésének befejezése után.
- WMF 5.1 felhasználó számára legalább [.NET-keretrendszer 4.5.2-es](https://www.microsoft.com/en-ca/download/details.aspx?id=42642).
A letöltési helyen cikk utasításait követve telepítheti a Microsoft .NET-keretrendszer 4.5.2-es.

**A WinRM-függőség**

Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) attól függ, hogy a Rendszerfelügyeleti webszolgáltatások.
Rendszerfelügyeleti webszolgáltatások a Windows Server 2008 R2 és Windows 7 alapértelmezés szerint nincs engedélyezve.
Futtatás `Set-WSManQuickConfig`, egy Windows PowerShell az emelt szintű ahhoz, hogy a WinRM-munkamenetben.


## <a name="install-wmf-51-for-windows-server-2012-r2-windows-server-2012-and-windows-81"></a>5.1 a WMF telepítése Windows Server 2012 R2, Windows Server 2012 és Windows 8.1
**Telepítse a Windows Explorer (vagy a Fájlkezelőben a Windows Server 2012 R2 vagy Windows 8.1)**

1. Keresse meg a mappát, amelybe letöltötte a MSU fájlt.
2. Kattintson duplán az MSU futtatni.

**A parancssorból történő telepítése**

1. Az a számítógép architektúrájának megfelelő csomag a letöltés után nyissa meg egy parancssori ablakot emelt szintű felhasználói jogosultságokkal (Futtatás rendszergazdaként). A Server Core telepítési lehetőségekkel, a Windows Server 2012 R2, Windows Server 2012 vagy Windows Server 2008 R2 SP1, a parancssort emelt szintű felhasználói jogosultságokkal alapértelmezés szerint megnyílik.
2. Váltson át a mappát, amelybe korábban letöltött vagy másolja a WMF 5.1 telepítőcsomagját.
3. A következő parancsok egyikét futtatja:
   - Windows Server 2012 R2 vagy Windows 8.1 x64 futtató számítógépén futtassa az `Win8.1AndW2K12R2-KB3191564-x64.msu /quiet`.
   - Futtassa a Windows Server 2012 rendszert futtató számítógépeken, `W2K12-KB3191565-x64.msu /quiet`.
   - Windows 8.1 x86 futtató számítógépén futtassa az `Win8.1-KB3191564-x86.msu /quiet`.

> [!NOTE]
> 5.1 a WMF telepítése újraindítást igényel. Használja a `/quiet` beállítás újraindul figyelmeztetés nélkül a rendszer.
> Használja a `/norestart` beállítás újraindítás elkerülése érdekében. Azonban a WMF 5.1 fog nem telepíthető, amíg a újra kell indítani.