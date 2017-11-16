---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 668a5b20add58ff5e23f35d6cebddc39c64ce926
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="installation-instructions"></a>Telepítési utasításokat

Töltse le az operációs rendszer és az architektúra a megfelelő csomag:

| Operációs rendszer       | Architektúra | Csomag neve              | 
|------------------------|--------------|---------------------------| 
| Windows Server 2012 R2 | x64      | [Win8.1AndW2K12R2-KB3134758-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717507) | 
| Windows Server 2012    | x64      | [W2K12-KB3134759-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717506) | 
| Windows Server 2008 R2 | x64      | [Win7AndW2K8R2-KB3134760-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717504) |
| A Windows 8.1            | x64          | [Win8.1AndW2K12R2-KB3134758-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717507) |
| A Windows 8.1            | x86          | [Win8.1-KB3134758-x86.msu](http://go.microsoft.com/fwlink/?LinkID=717963) |
| Windows 7 SP1          | x64          | [Win7AndW2K8R2-KB3134760-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717504) |
| Windows 7 SP1          | x86          | [Win7-KB3134760-x86.msu](http://go.microsoft.com/fwlink/?LinkID=717962) |


**WMF 5.0 telepítése a Windows Explorer (vagy a Fájlkezelőben a Windows Server 2012 R2 és Windows 8.1):**

1. Keresse meg a mappát, amelybe letöltötte a MSU fájlt.

2. Kattintson duplán az MSU futtatni.

**WMF 5.0 telepítése a parancssorból:** 

1. Az a számítógép architektúrájának megfelelő csomag a letöltés után nyissa meg egy parancssori ablakot emelt szintű felhasználói jogosultságokkal (Futtatás rendszergazdaként). A Server Core telepítési lehetőségekkel, a Windows Server 2012 R2 vagy Windows Server 2012 vagy Windows Server 2008 R2 SP1, a parancssort emelt szintű felhasználói jogosultságokkal alapértelmezés szerint megnyílik.

2. Váltson át a mappát, amelybe korábban letöltött vagy másolja a WMF 5.0 telepítőcsomagját.

3. A következő parancsok egyikét futtatja:
    - Windows Server 2012 R2 vagy Windows 8.1 x64 futtató számítógépén futtassa az **Win8.1AndW2K12R2-KB3134758-x64.msu quiet**.
    - Futtassa a Windows Server 2012 rendszert futtató számítógépeken, **W2K12-KB3134759-x64.msu quiet**.
    - Az x 64 Windows Server 2008 R2 SP1 vagy Windows 7 SP1 futtató számítógépet, futtassa **Win7AndW2K8R2-KB3134760-x64.msu quiet**.
    - Windows 8.1 x86 futtató számítógépén futtassa az **Win8.1-KB3134758-x86.msu quiet**.
    - X 86 Windows 7 SP1 operációs rendszert futtató számítógépeken futtassa **Win7-KB3134760-x86.msu quiet**.

**További telepítési megjegyzések a Windows Server 2008 SP1 és Windows 7 SP1:**

Győződjön meg arról, hogy teljesülnek a következő előfeltételek teljesülését:
- Legfrissebb telepítve van.
- [WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855) telepítve van

*A Rendszerfelügyeleti webszolgáltatások függőségi:* Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) WinRM függ. Rendszerfelügyeleti webszolgáltatások a Windows Server 2008 R2 és Windows 7 alapértelmezés szerint nincs engedélyezve. Ahhoz, hogy a Rendszerfelügyeleti webszolgáltatások, egy Windows PowerShell az emelt szintű munkamenet, futtassa **Set-WSManQuickConfig**.


