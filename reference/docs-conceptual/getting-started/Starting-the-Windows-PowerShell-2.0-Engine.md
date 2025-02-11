---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: A Windows PowerShell 2.0 motor indítása
ms.openlocfilehash: 824077008d2dcfd707e977d2112f0882d07a8aca
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030443"
---
# <a name="starting-the-windows-powershell-20-engine"></a>A Windows PowerShell 2.0 motor indítása

Ez a szakasz azt ismerteti, hogyan indítsa el a Windows PowerShell 2.0 motor a Windows 8.1, Windows Server 2012 R2, Windows 8 és Windows Server 2012, többek között a Windows PowerShell 2.0 motor, és más rendszereken, mely Windows PowerShell 2.0, a Windows PowerShell 3.0 és a Windows PowerShell 4.0-s verzióját telepíti.

Visszafelé kompatibilis a Windows PowerShell 2.0-s Windows PowerShell 4.0-s és a Windows PowerShell 3.0 célja. Parancsmagok, szolgáltatók, beépülő modulok, modulok és a Windows PowerShell 2.0 írt szkriptekkel futtassa változatlan marad, a Windows PowerShell 4.0-s és a Windows PowerShell 3.0. Azonban a Microsoft .NET-keretrendszer 4 futásidejű aktiválási házirendben megváltozása miatt Windows PowerShell gazdagép programok készült Windows PowerShell 2.0-s és a közös nyelvi futtatókörnyezet (CLR) 2.0 lefordított nem futnak Windows a módosítás nélkül PowerShell 3.0 vagy 4.0-s CLR-beli ügyfélbeállításai Windows PowerShell 4.0. A Windows PowerShell 2.0 motor kívánják használni, ha egy meglévő parancsfájl vagy a gazdagép program nem futtatható, mert az nem kompatibilis a Windows PowerShell 4.0-s verzióját, a Windows PowerShell 3.0 vagy a Microsoft .NET-keretrendszer 4. Ezekben az esetekben várhatóan ritkán fordul elő.

Számos programok, amelyek a Windows PowerShell 2.0 motor igényelnek, automatikusan elindul. Ezek az utasítások a ritka esetekben kell manuálisan elindítani a motor számára is.

## <a name="installing-and-enabling-required-programs"></a>A szükséges programok telepítése és engedélyezése

A Windows PowerShell 2.0 motor indítása, mielőtt engedélyezi a Windows PowerShell 2.0 motor és a Microsoft .NET-keretrendszer 3.5 Service Pack 1. Útmutatásért lásd: [Windows PowerShell telepítése](../install/Installing-Windows-PowerShell.md).

Rendszerek mely Windows Management Framework 4.0 vagy a Windows Management Framework 3.0 telepítve van a szükséges összetevőket. További konfiguráció nélkül nem szükséges. További információ [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkID=293881) vagy a Windows Management Framework 3.0, lásd: [Windows PowerShell telepítése](../install/Installing-Windows-PowerShell.md).

## <a name="how-to-start-the-windows-powershell-20-engine"></a>A Windows PowerShell 2.0 motor indítása

Amikor hozzákezd a Windows PowerShell alapértelmezés szerint elindul a legújabb verzióra. A Windows PowerShell 2.0 motor a Windows PowerShell indításához használja a PowerShell.exe verzió paramétere. Parancssort, beleértve a Windows PowerShell és a Cmd.exe futtathatja a parancsot.

```
PowerShell.exe -Version 2
```

## <a name="how-to-start-a-remote-session-with-the-windows-powershell-20-engine"></a>A Windows PowerShell 2.0 motor a távoli munkamenet elindítása

A Windows PowerShell 2.0 motor futtatható a távoli munkamenetet, a távoli számítógépen, amely betölti a Windows PowerShell 2.0 motor hozzon létre egy munkamenet-konfiguráció (más néven "végpont"). A munkamenet-konfiguráció a távoli számítógépen mentett, és hozhat létre olyan munkamenetek, amelyek a Windows PowerShell 2.0 motor használata semmilyen engedéllyel rendelkező felhasználó használható.

Ez az egy speciális, általában a rendszergazdák által végrehajtandó feladat.

Az alábbi eljárást használ a **PSVersion** paraméterében a [Register-PSSessionConfiguration](https://technet.microsoft.com/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) parancsmaggal hozzon létre egy munkamenet-konfiguráció, amely a Windows PowerShell 2.0 motor használja. Is használhatja a **PowerShellVersion** paraméterében a [New-PSSessionConfigurationFile](https://technet.microsoft.com/library/5f3e3633-6e90-479c-aea9-ba45a1954866) parancsmaggal hozzon létre egy munkamenet-konfigurációs fájlt, amely betölti a Windows PowerShell 2.0 motor munkamenet és használhatja a **PSVersion** paraméterében a [Set-PSSessionConfiguration](https://technet.microsoft.com/library/b21fbad3-1759-4260-b206-dcb8431cd6ea) paraméter egy munkamenet-konfiguráció használata a Windows PowerShell 2.0 motor módosítása.

Munkamenet-konfiguráció fájlokkal kapcsolatos további információkért lásd: [about_Session_Configuration_Files](https://technet.microsoft.com/library/c7217447-1ebf-477b-a8ef-4dbe9a1473b8). További információ a munkamenet-konfigurációk, a telepítő és a biztonság, többek között: [about_Session_Configurations [v4]](https://technet.microsoft.com/library/a2fbe12a-350c-4d04-be50-24102824e3ab).

#### <a name="to-start-a-remote-windows-powershell-20-session"></a>A távoli Windows PowerShell 2.0-munkamenet indítása

1. Egy munkamenet-konfiguráció, amely megköveteli a Windows PowerShell 2.0 motor létrehozásához használja a **PSVersion** paraméterében a [Register-PSSessionConfiguration](https://technet.microsoft.com/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) parancsmag "2.0" értékkel. Futtassa ezt a parancsot a számítógépen, a "server side" vagy a kapcsolatot fogadó végén.

   A következő mintaparancs kiszolgalo01 számítógépen hoz létre a PS2 munkamenet-konfiguráció. A parancs futtatásához, indítsa el a Windows PowerShell 4.0-s vagy Windows PowerShell 3.0 a **Futtatás rendszergazdaként** lehetőséget.

   ```powershell
   Register-PSSessionConfiguration -Name PS2 -PSVersion 2.0
   ```

2. A munkamenet létrehozásához a PS2 munkamenet-konfigurációt használó kiszolgalo01 számítógépen használja a **ConfigurationName** paraméter parancsmag-hozzon létre egy távoli munkamenetet, mint például a [New-PSSession](https://technet.microsoft.com/library/76f6628c-054c-4eda-ba7a-a6f28daaa26f) parancsmagot.

   A munkamenet-konfigurációt használó a munkamenet akkor kezdődik, amikor a Windows PowerShell 2.0 motor automatikusan betöltődik a munkamenetbe.

   A következő parancsot egy munkamenet indítása a kiszolgalo01 számítógépen, amely a PS2 munkamenet-konfigurációt használ. A parancs a munkamenetben $s változóba menti.

   ```powershell
   $s = New-PSSession -ComputerName Server01 -ConfigurationName PS2
   ```

## <a name="how-to-start-a-background-job-with-the-windows-powershell-20-engine"></a>A háttérben történő feldolgozás a Windows PowerShell 2.0 motor használatának első lépéseiről

A Windows PowerShell 2.0 motor a háttérben futó feladat indításához használja a **PSVersion** paraméterében a [a Start-Job](https://technet.microsoft.com/library/2bc04935-0deb-4ec0-b856-d7290cca6442) parancsmagot.

A következő parancsot a Windows PowerShell 2.0 motor háttérfeladatként kezdődik

```powershell
Start-Job {Get-Process} -PSVersion 2.0
```

Háttér-feladatokkal kapcsolatos további információkért lásd: [about_Jobs](/powershell/module/microsoft.powershell.core/about/about_jobs).
