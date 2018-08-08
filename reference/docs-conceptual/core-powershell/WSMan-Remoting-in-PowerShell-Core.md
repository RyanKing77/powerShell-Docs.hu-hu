---
title: WS-Management (WSMan) távoli eljáráshívás a PowerShell Core-ban
description: Távoli eljáráshívás a PowerShell Core-t a wsman által használt
ms.date: 08/06/2018
ms.openlocfilehash: ce58ed88f59f32b0f83951e55de36e829f7fa3f4
ms.sourcegitcommit: 01ac77cd0b00e4e5e964504563a9212e8002e5e0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/07/2018
ms.locfileid: "39587346"
---
# <a name="ws-management-wsman-remoting-in-powershell-core"></a>WS-Management (WSMan) távoli eljáráshívás a PowerShell Core-ban

## <a name="instructions-to-create-a-remoting-endpoint"></a>A távoli eljáráshívás végpont létrehozására vonatkozó utasításokat

A Windows PowerShell Core csomag tartalmaz egy beépülő modul WinRM (`pwrshplugin.dll`) és a egy telepítési szkript (`Install-PowerShellRemoting.ps1`) a `$PSHome`.
Ezek a fájlok PowerShell bejövő távoli PowerShell-kapcsolatok fogadására, ha meg van adva a végpont engedélyezése.

### <a name="motivation"></a>Motiváció

Telepíteni kell a PowerShell távoli számítógépekről, amelyek a PowerShell-munkameneteket hozhat létre `New-PSSession` és `Enter-PSSession`.
A felhasználó engedélyezi a bejövő távoli PowerShell-kapcsolatok fogadására, egy WinRM távoli eljáráshívás végpontot kell létrehoznia.
Ez az egy explicit vehetnek részt a forgatókönyvben, a felhasználó futtatja a telepítés-PowerShellRemoting.ps1 a WinRM-végpont létrehozása.
A telepítési parancsfájl egy rövid távú megoldást, a további funkciók még nem `Enable-PSRemoting` ugyanaz a művelet végrehajtásához.
További részletekért tekintse meg a probléma [#1193](https://github.com/PowerShell/PowerShell/issues/1193).

### <a name="script-actions"></a>A Parancsfájlműveletek

A parancsfájl

1. Létrehoz egy könyvtárat a beépülő modulhoz %windir%\System32\PowerShell belül
1. Másolja át a pwrshplugin.dll adott helyhez
1. Egy konfigurációs fájlt hoz létre
1. Regisztrál, hogy beépülő modul a Rendszerfelügyeleti webszolgáltatások

### <a name="registration"></a>Regisztráció

A szkript egy rendszergazdai PowerShell-munkamenetet, és két módban fut belül kell végrehajtani.

#### <a name="executed-by-the-instance-of-powershell-that-it-will-register"></a>PowerShell parancsmag, amely, regisztrálja az példány által végrehajtott

```powershell
Install-PowerShellRemoting.ps1
```

#### <a name="executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register"></a>Egy másik példánya PowerShell nevében, regisztrálja az adott példány által végrehajtott

```powershell
<path to powershell>\Install-PowerShellRemoting.ps1 -PowerShellHome "<absolute path to the instance's $PSHOME>"
```

Példa:

```powershell
Set-Location -Path 'C:\Program Files\PowerShell\6.0.0\'
.\Install-PowerShellRemoting.ps1 -PowerShellHome "C:\Program Files\PowerShell\6.0.0\"
```

**Megjegyzés:** a távoli eljáráshívás regisztrációs parancsfájl újraindul a Rendszerfelügyeleti webszolgáltatások, így az összes meglévő PSRP munkamenet befejeződik, azonnal a szkript futtatása után. Ha egy távoli munkamenet közben fut, ez a kapcsolat le fog állni.

## <a name="how-to-connect-to-the-new-endpoint"></a>Hogyan lehet csatlakozni az új végpont

Hozzon létre egy PowerShell-munkamenetet az új PowerShell-végpont megadásával `-ConfigurationName "some endpoint name"`. Ha csatlakozni szeretne a PowerShell-példány a fenti példában, vagy használja:

```powershell
New-PSSession ... -ConfigurationName "powershell.6.0.0"
Enter-PSSession ... -ConfigurationName "powershell.6.0.0"
```

Vegye figyelembe, hogy `New-PSSession` és `Enter-PSSession` meghívásához, amely nem ad meg `-ConfigurationName` az alapértelmezett PowerShell végpont által megcélzott `microsoft.powershell`.