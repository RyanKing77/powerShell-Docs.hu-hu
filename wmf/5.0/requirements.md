---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: e4e5c6fff2eea12b9cfbba325d5519f6266218e8
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="system-requirements"></a>Rendszerkövetelmények

- Telepítse a legújabb Windows-frissítéseket WMF 5.0 RTM telepítése előtt.
- WMF 5.0 RTM csak a következő operációs rendszereken telepítheti:

    | Operációs rendszer       | Kiadás         | Előfeltételek        |  Csomag hivatkozások |
    |------------------------|--------------|------------------|----------------------| --------------|
    | Windows Server 2012 R2 |  |  | [Win8.1AndW2K12R2-KB3134758-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717507) |
    | Windows Server 2012    |  |  | [W2K12-KB3134759-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717506) |
    | Windows Server 2008 R2 SP1 | Összes IA64 kivételével | [WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855) és [.NET-keretrendszer 4.5 vagy újabb](https://msdn.microsoft.com/en-us/library/5a4x27ek.aspx) telepítve van| [Win7AndW2K8R2-KB3134760-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717504)|
    | A Windows 8.1 | Pro, Enterprise | | **x64:**[Win8.1AndW2K12R2-KB3134758-x64.msu  ](http://go.microsoft.com/fwlink/?LinkId=717507) </br> **x86:**[Win8.1-KB3134758-x86.msu  ](http://go.microsoft.com/fwlink/?LinkID=717963)|
    | Windows 7 SP1 | Összes | [WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855) és [.NET-keretrendszer 4.5 vagy újabb](https://msdn.microsoft.com/en-us/library/5a4x27ek.aspx) telepítve van | **x64:**[Win7AndW2K8R2-KB3134760-x64.msu  ](http://go.microsoft.com/fwlink/?LinkId=717504)  </br> **x86:**[Win7-KB3134760-x86.msu  ](http://go.microsoft.com/fwlink/?LinkID=717962)|

# <a name="installation-instructions"></a>Telepítési utasításokat

### <a name="to-install-wmf-50-from-windows-explorer-or-file-explorer"></a>WMF 5.0 telepítése a Windows Explorer (vagy a Fájlkezelőben):

1. Keresse meg a mappát, amelybe letöltötte a MSU fájlt.

2. Kattintson duplán az MSU futtatni.

### <a name="to-install-wmf-50-from-command-prompt"></a>WMF 5.0 telepítése a parancssorból:

1. Az a számítógép architektúrájának megfelelő csomag a letöltés után nyissa meg egy parancssori ablakot emelt szintű felhasználói jogosultságokkal (Futtatás rendszergazdaként). A Server Core telepítési lehetőségekkel, a Windows Server 2012 R2 vagy Windows Server 2012 vagy Windows Server 2008 R2 SP1, a parancssort emelt szintű felhasználói jogosultságokkal alapértelmezés szerint megnyílik.

2. Váltson át a mappát, amelybe korábban letöltött vagy másolja a WMF 5.0 telepítőcsomagját.

3. A következő parancsok egyikét futtatja:
    - Windows Server 2012 R2 vagy Windows 8.1 x64 futtató számítógépén futtassa az **Win8.1AndW2K12R2-KB3134758-x64.msu quiet**.
    - Futtassa a Windows Server 2012 rendszert futtató számítógépeken, **W2K12-KB3134759-x64.msu quiet**.
    - Az x 64 Windows Server 2008 R2 SP1 vagy Windows 7 SP1 futtató számítógépet, futtassa **Win7AndW2K8R2-KB3134760-x64.msu quiet**.
    - Windows 8.1 x86 futtató számítógépén futtassa az **Win8.1-KB3134758-x86.msu quiet**.
    - X 86 Windows 7 SP1 operációs rendszert futtató számítógépeken futtassa **Win7-KB3134760-x86.msu quiet**.

### <a name="additional-installation-notes-for-windows-server-2008-r2-sp1-and-windows-7-sp1"></a>További telepítési megjegyzések a Windows Server 2008 R2 SP1 és Windows 7 SP1:

Győződjön meg arról, hogy teljesülnek a következő előfeltételek teljesülését:
- Legfrissebb telepítve van.
- [WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855) telepítve van.
- [.NET-keretrendszer 4.5 vagy újabb](https://msdn.microsoft.com/en-us/library/5a4x27ek.aspx) telepítve van.

**WMF 4.0 függőség**

Windows Server 2008 R2 SP1 és a Windows 7 SP1 rendszer beépített PowerShell 2.0, WinRM és WMI rendelkezik. A WMF 3.0 és a WMF 4.0 csomagok, beépített összetevők frissül, a Windows Server 2008 R2 SP1 és Windows 7 SP1 kiadásában után kiadott. A WMF 3.0 telepítése/eltávolítása és WMF 4.0 csomagok nem sikerült felfedezni kapcsolatos néhány problémát ismertetünk, a következő frissítési elérési úton:

- Beépített WMF 4.0-->
- Beépített--> a WMF 3.0 WMF4.0-->. 

A WMF 4.0 csomagok azt rögzített ezeket a problémákat. Emiatt nincs WMF 4.0 előfeltétele a WMF 5.0 telepítése a Windows Server 2008 R2 SP1 és Windows 7 SP1. Az alábbiakban a konkrét problémák léphetnek fel, ha nem telepíti a WMF 4.0 WMF 5.0 való frissítés előtt:

- Továbbított események naplójában nem érhető el, és EventCollector napló nem jelenik meg az eseménynaplóban a WMF 3.0 vagy WMF 5.0 (nélkül az előfeltétel-ellenőrzési WMF 4.0-s verziójával) eltávolítása után Windows 7 SP1 és Windows Server 2008 R2 SP1 ([KB2809215](https://support.microsoft.com/en-us/kb/2809215)).
- A testreszabási *PSModulePath* környezeti változóval lekérdezi alapértelmezett értékre állnak vissza közvetlenül a PowerShell 2.0-s beépített történő frissítésekor WMF 5.0 ([KB2872035](https://support.microsoft.com/en-us/kb/2872035)) vagy a WMF 3.0 WMF 5.0. ([KB2872047](https://support.microsoft.com/en-us/kb/2872047)) Windows 7 SP1 és Windows Server 2008 R2 SP1.

**A WinRM-függőség**

Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) attól függ, hogy a Rendszerfelügyeleti webszolgáltatások. A Rendszerfelügyeleti webszolgáltatások a Windows Server 2008 R2 SP1 és Windows 7 SP1 alapértelmezés szerint nincs engedélyezve. Ahhoz, hogy a Rendszerfelügyeleti webszolgáltatások, egy Windows PowerShell az emelt szintű munkamenet, futtassa **Set-WSManQuickConfig**.

# <a name="uninstallation-instructions"></a>Az eltávolítás utasításokat

### <a name="using-command-prompt"></a>Parancssor használatával

1.  Nyissa meg **parancssort.**

2.  Futtassa a [Windows Update önálló indító](https://support.microsoft.com/en-us/kb/934307) alább látható módon:

A Windows Server 2012 R2 és Windows 8.1:
```powershell
wusa /uninstall /kb:3134758
```
A Windows Server 2012:
```powershell
wusa /uninstall /kb:3134759
```
A Windows Server 2008 R2 SP1 és Windows 7 SP1:
```powershell
wusa /uninstall /kb:3134760
```

### <a name="using-control-panel"></a>Vezérlőpult segítségével

1.  Nyissa meg **vezérlőpultot.**

2.  Nyissa meg a **programok**, majd nyissa meg **program eltávolítása.**

3.  Kattintson a **telepített frissítések megjelenítése.**

4.  Válassza ki **Windows Management Framework 5.0** telepített frissítések a listából. Ez megfelel *KB3134758*, *KB3134759*, vagy *KB3134760*. Kattintson a **eltávolítása.**

