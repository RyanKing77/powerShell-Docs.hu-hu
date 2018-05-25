---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 7b4e4dbeaf9c3c48e7b2dfc74435dfa2cd9c7ea7
ms.sourcegitcommit: 735ccab3fb3834ccd8559fab6700b798e8e5ffbf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/25/2018
---
# <a name="unified-and-consistent-state-and-status-representation"></a>Egyesített és konzisztens állapotreprezentáció

Fejlesztésen végzett ebben a kiadásban a beépített LCM állapotát és DSC állapot automatizálása. Ezek közé tartozik a egyesített és konzisztens állapotban és állapot formátumban, az állapot objektumok kezelhető dátum/idő tulajdonság Get-DscConfigurationStatus parancsmag által visszaadott és fokozott LCM állapot részletei tulajdonság Get-DscLocalConfigurationManager által visszaadott parancsmag.

LCM állapot és a DSC műveleti állapotának ábrázolása javított változat, és a következő szabályok szerint egyesített:
1.  Notprocessed erőforrás nem befolyásolja a LCM állapotot és a DSC-állapota.
2.  További erőforrások feldolgozásának, miután újraindítást kérő erőforrás ütközik LCM leállítása.
3.  Egy erőforrás újraindítást kérő nincs megfelelő állapotban amíg újraindítást ténylegesen történik.
4.  Amikor egy erőforrást, amely nem sikerül, LCM tartja a feldolgozás után további erőforrások mindaddig, amíg azok nem függ a hiba egyik.
5.  A Get-DscConfigurationStatus parancsmag által visszaadott összesített állapotát az összes erőforrás állapotának super összessége.
6.  A PendingReboot állapota felülbírálja a PendingConfiguration állapotát.

Az alábbi táblázat szemlélteti a eredő állapot kapcsolódó tulajdonságok néhány jellemző forgatókönyvek alapján.

| Forgatókönyv                    | LCMState       | Állapot | A kért újraindítás  | ResourcesInDesiredState  | ResourcesNotInDesiredState |
|---------------------------------|----------------------|------------|---------------|------------------------------|--------------------------------|
| S**^**                          | Üresjárati                 | Siker    | $false        | S                            | $null                          |
| F**^**                          | PendingConfiguration | Hiba    | $false        | $null                        | F                              |
| S, F                             | PendingConfiguration | Hiba    | $false        | S                            | F                              |
| F,S                             | PendingConfiguration | Hiba    | $false        | S                            | F                              |
| S<sub>1</sub>, F, S<sub>2</sub> | PendingConfiguration | Hiba    | $false        | S<sub>1</sub>, S<sub>2</sub> | F                              |
| F<sub>1</sub>, S, F<sub>2</sub> | PendingConfiguration | Hiba    | $false        | S                            | F<sub>1</sub>, F<sub>2</sub>   |
| S, r                            | PendingReboot        | Siker    | $true         | S                            | r                              |
| F, r                            | PendingReboot        | Hiba    | $true         | $null                        | F, r                           |
| r, S                            | PendingReboot        | Siker    | $true         | $null                        | r                              |
| r, F                            | PendingReboot        | Siker    | $true         | $null                        | r                              |

^ S<sub>i</sub>: erőforrásokat, a rendszer sikeresen alkalmazta F sorozata<sub>i</sub>: a rendszer újraindítását igénylő r: A erőforrás sikertelenül telepített erőforrások több \*

```powershell
$LCMState = (Get-DscLocalConfigurationManager).LCMState
$Status = (Get-DscConfigurationStatus).Status

$RebootRequested = (Get-DscConfigurationStatus).RebootRequested

$ResourcesInDesiredState = (Get-DscConfigurationStatus).ResourcesInDesiredState

$ResourcesNotInDesiredState = (Get-DscConfigurationStatus).ResourcesNotInDesiredState
```

## <a name="enhancement-in-get-dscconfigurationstatus-cmdlet"></a>A Get-DscConfigurationStatus parancsmag továbbfejlesztése

Ebben a kiadásban a Get-DscConfigurationStatus parancsmagnak néhány kiegészítésre került sor. Korábban a Kezdődátum a parancsmag által visszaadott objektumok tulajdonsága karakterlánc típusú. Most már dátum/idő típusú, amely lehetővé teszi összetett, válassza ki, majd a szűrési beállítások könnyebb a belső tulajdonságok egy DateTime típusú objektum.

```powershell
(Get-DscConfigurationStatus).StartDate | fl *
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

Az alábbiakban látható egy példa, amely ugyanarra a napra esnek ennek ma hét történt a DSC-művelet az összes rekord visszaadása.

```powershell
(Get-DscConfigurationStatus –All) | where { $_.startdate.dayofweek -eq (Get-Date).DayOfWeek }
```

Ne módosítsa a csomópont konfigurációs (vagyis olvasási csak műveletek) műveletkészlet rekordok szűrni. Ezért teszt-DscConfiguration, Get-DscConfiguration műveletek vannak már nem tiltott a Get-DscConfigurationStatus parancsmag objektumot sem adott vissza.
Meta konfigurációs beállítás művelet rögzíti a Get-DscConfigurationStatus parancsmag visszatérési kerül.

Az alábbiakban látható egy példa a Get-DscConfigurationStatus visszaadott eredmény – az összes parancsmag.

```powershell
All configuration operations:

Status StartDate Type RebootRequested
------ --------- ---- ---------------
Success 11/13/2015 11:38:16 AM Consistency False
Success 11/13/2015 11:23:16 AM Reboot False
Success 11/13/2015 11:21:43 AM Reboot True
Success 11/13/2015 11:20:44 AM Initial True
Success 11/13/2015 11:20:44 AM LocalConfigurationManager False
```

## <a name="enhancement-in-get-dsclocalconfigurationmanager-cmdlet"></a>A Get-DscLocalConfigurationManager parancsmag továbbfejlesztése

Egy új mezőt a LCMStateDetail hozzáadódik a Get-DscLocalConfigurationManager parancsmag által visszaadott objektum. Ebben a mezőben van feltöltve, ha LCMState "Foglalt". Lekérhető által a következő parancsmagot:

```powershell
(Get-DscLocalConfigurationManager).LCMStateDetail
```

Az alábbiakban látható egy példa a kimenetre végzett folyamatos figyelés a olyan konfigurációt, amely a távoli csomóponton levő két újraindításra van szükség.

```powershell
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
