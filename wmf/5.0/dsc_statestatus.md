---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 0e8d0cb1e4afa7bc791d45bfb0b981654cb09ed5
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892569"
---
# <a name="unified-and-consistent-state-and-status-representation"></a>Egyesített és konzisztens állapotreprezentáció

Ebben a kiadásban az LCM állapotának és a DSC-állapot automatizálását a fejlesztésen került sor. Ezek közé tartozik a egyesített és konzisztens állapot reprezentációinak, kezelhető dátum/idő tulajdonság által visszaadott állapot objektumok `Get-DscConfigurationStatus` parancsmag és a továbbfejlesztett LCM állapot részletei tulajdonság által visszaadott `Get-DscLocalConfigurationManager` parancsmagot.

Leképezése az LCM állapotának és a DSC műveleti állapotának javított változat, és a következő szabályok szerint egyesített:

1. Az LCM állapotának és a DSC-állapot Notprocessed erőforrás nincs hatással.
2. Az LCM stop további erőforrások feldolgozása, miután újraindítást kérő erőforrás tapasztal.
3. Egy újraindítást kérő erőforrás nem áll a szükséges állapotban, amíg újraindítást ténylegesen történik.
4. Hajt végre, amikor egy erőforrást, amelyet nem sikerül, LCM tartja a feldolgozás után további erőforrásokat, amíg azok nem függnek a hiba egyik.
5. A törlés összesített állapotát által visszaadott `Get-DscConfigurationStatus` parancsmag az összes erőforrás állapotának a felügyelői készlete.
6. A PendingReboot állapota felülbírálja a PendingConfiguration állapota.

   Az alábbi táblázatban látható a létrejövő állapot kapcsolódó tulajdonságok alapján néhány gyakori forgatókönyveket.

   | Forgatókönyv                    | LCMState       | Állapot | A kért újraindítási  | ResourcesInDesiredState  | ResourcesNotInDesiredState |
   |---------------------------------|----------------------|------------|---------------|------------------------------|--------------------------------|
   | S**^**                          | Inaktív                 | Siker    | $false        | S                            | $null                          |
   | F**^**                          | PendingConfiguration | Hiba    | $false        | $null                        | F                              |
   | S, F                             | PendingConfiguration | Hiba    | $false        | S                            | F                              |
   | F,S                             | PendingConfiguration | Hiba    | $false        | S                            | F                              |
   | S<sub>1</sub>, F, S<sub>2</sub> | PendingConfiguration | Hiba    | $false        | S<sub>1</sub>, S<sub>2</sub> | F                              |
   | F<sub>1</sub>, S, F<sub>2</sub> | PendingConfiguration | Hiba    | $false        | S                            | F<sub>1</sub>, F<sub>2</sub>   |
   | S-, r                            | PendingReboot        | Siker    | $true         | S                            | r                              |
   | F, r                            | PendingReboot        | Hiba    | $true         | $null                        | F, r                           |
   | r, S                            | PendingReboot        | Siker    | $true         | $null                        | r                              |
   | r, F                            | PendingReboot        | Siker    | $true         | $null                        | r                              |

   ^
   S<sub>i</sub>: erőforrások, amelyek sikeresen alkalmazva F sorozata<sub>i</sub>: egy sorozat erőforrásokat, amelyeket a alkalmazni sikertelenül r: egy erőforrás, amelyhez újraindítás szükséges \*

   ```powershell
   $LCMState = (Get-DscLocalConfigurationManager).LCMState
   $Status = (Get-DscConfigurationStatus).Status

   $RebootRequested = (Get-DscConfigurationStatus).RebootRequested

   $ResourcesInDesiredState = (Get-DscConfigurationStatus).ResourcesInDesiredState

   $ResourcesNotInDesiredState = (Get-DscConfigurationStatus).ResourcesNotInDesiredState
   ```

## <a name="enhancement-in-get-dscconfigurationstatus-cmdlet"></a>Fejlesztés a Get-DscConfigurationStatus parancsmagban

Néhány kiegészítésre került sor a `Get-DscConfigurationStatus` parancsmag ebben a kiadásban. Korábban a StartDate a parancsmag által visszaadott objektumok tulajdonság karakterlánc típusú. Eljött a Datetime típusú, amely lehetővé teszi az összetett kiválasztása és szűrése a belső tulajdonságok egy dátum és idő objektum egyszerűbb alapján.

```powershell
(Get-DscConfigurationStatus).StartDate | Format-List *
DateTime : Friday, November 13, 2015 1:39:44 PM
Date : 11/13/2015 12:00:00 AM
Day : 13
DayOfWeek : Friday
DayOfYear : 317
Hour : 13
Kind : Local
Millisecond : 886
Minute : 39
Month : 11
Second : 44
Ticks : 635830187848860000
TimeOfDay : 13:39:44.8860000
Year : 2015
```

Következő egy példa, amely visszaadja az összes DSC műveleti rekordok történt a hét ma is ugyanazon a napon.

```powershell
(Get-DscConfigurationStatus –All) | Where-Object { $_.startdate.dayofweek -eq (Get-Date).DayOfWeek }
```

Kiküszöbölhetők azok a rekordok műveletek, amelyek a csomópont-konfiguráció (azaz olvasási csak műveletek), ne módosítsa. Ezért `Test-DscConfiguration`, `Get-DscConfiguration` műveletek már nem a visszaadott objektumok a rendszer tiltott `Get-DscConfigurationStatus` parancsmagot.
Meta konfigurációs beállítás művelet rekordok kerül, a visszatérési `Get-DscConfigurationStatus` parancsmagot.

Az alábbiakban egy példát eredményt adott vissza a `Get-DscConfigurationStatus` – minden parancsmagot.

```output
All configuration operations:

Status StartDate Type RebootRequested
------ --------- ---- ---------------
Success 11/13/2015 11:38:16 AM Consistency False
Success 11/13/2015 11:23:16 AM Reboot False
Success 11/13/2015 11:21:43 AM Reboot True
Success 11/13/2015 11:20:44 AM Initial True
Success 11/13/2015 11:20:44 AM LocalConfigurationManager False
```

## <a name="enhancement-in-get-dsclocalconfigurationmanager-cmdlet"></a>A Get-DscLocalConfigurationManager parancsmag a fejlesztés

Egy új mezőt LCMStateDetail a visszaadott objektum hozzáadódik `Get-DscLocalConfigurationManager` parancsmagot. Ez a mező kitöltése LCMState "Foglalt" esetén. A következő parancsmaggal kérhető:

```powershell
(Get-DscLocalConfigurationManager).LCMStateDetail
```

Következő egy példa a kimenetre végzett folyamatos figyelés a olyan konfigurációt, amely a távoli csomóponton két újraindításra van szükség.

```output
Start a configuration that requires two reboots

Monitor LCM State:
LCM State: Busy, LCM is applying a new configuration.
LCM State: PendingReboot,
Machine is rebooting...
LCM State: Busy, LCM is continuing applying configuration after last reboot.
LCM State: PendingReboot,
Machine is rebooting...
LCM State: Busy, LCM is continuing applying configuration after last reboot.
LCM State: Idle,
LCM State: Busy, LCM is performing a consistency check.
LCM State: Idle,
```