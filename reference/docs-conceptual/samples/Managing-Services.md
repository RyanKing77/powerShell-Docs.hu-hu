---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Szolgáltatások kezelése
ms.assetid: 7a410e4d-514b-4813-ba0c-0d8cef88df31
ms.openlocfilehash: 81fd8802215da80ce22fa3fd4750b1df6efe8206
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687012"
---
# <a name="managing-services"></a>Szolgáltatások kezelése

Nincsenek nyolc core parancsmagok, számos szolgáltatás feladatai tervezve. Csak az ajánlati és módosítása a futó állapotú szolgáltatások tekintsük meg, de használatával megtekintheti a parancsmagok listáját `Get-Help \*-Service`, és annak minden egyes szolgáltatás parancsmaggal kapcsolatos információkat a `Get-Help <Cmdlet-Name>`, mint például `Get-Help New-Service`.

## <a name="getting-services"></a>Szolgáltatás beolvasása

A helyi vagy távoli számítógépen a szolgáltatások is kap a `Get-Service` parancsmagot. A `Get-Process`révén a `Get-Service` paraméterek nélkül parancs visszaadja az összes szolgáltatás. Név, szűrheti, még akkor is használatával helyettesítő karakterként csillagot:

```powershell
PS> Get-Service -Name se*

Status   Name               DisplayName
------   ----               -----------
Running  seclogon           Secondary Logon
Running  SENS               System Event Notification
Stopped  ServiceLayer       ServiceLayer
```

Mert nem mindig nyilvánvaló Mi az a szolgáltatás valódi neve, azt tapasztalhatja, meg kell keresnie a szolgáltatások által megjelenített neve. Ezt megteheti is egyedi neve, helyettesítő karakterek használatával, vagy a megjelenített nevek listája segítségével:

```powershell
PS> Get-Service -DisplayName se*

Status   Name               DisplayName
------   ----               -----------
Running  lanmanserver       Server
Running  SamSs              Security Accounts Manager
Running  seclogon           Secondary Logon
Stopped  ServiceLayer       ServiceLayer
Running  wscsvc             Security Center

PS> Get-Service -DisplayName ServiceLayer,Server

Status   Name               DisplayName
------   ----               -----------
Running  lanmanserver       Server
Stopped  ServiceLayer       ServiceLayer
```

A ComputerName paramétert a Get-Service-parancsmag használatával a szolgáltatások beolvasása a távoli számítógépeken. A ComputerName paraméter több értéket és helyettesítő karaktereket, fogad el, így a szolgáltatásokat több számítógépen egyetlen paranccsal. Például a következő parancsot a szolgáltatások beolvassa a kiszolgalo01 távoli számítógépen.

```powershell
Get-Service -ComputerName Server01
```

## <a name="getting-required-and-dependent-services"></a>Első szükséges, és a függő szolgáltatások

A Get-Service parancsmag rendelkezik, amelyek rendkívül hasznosak lehetnek a szolgáltatás felügyeleti két paramétert. A DependentServices paraméter szerzi meg szolgáltatás, amely a szolgáltatás függ. A RequiredServices paraméter szerzi meg szolgáltatásokat, amelyektől Ez a szolgáltatás függ.

Ezek a paraméterek csak a DependentServices és ServicesDependedOn értékeinek megjelenítése (alias = RequiredServices), amelyek megkönnyítik a Get-Service értéket ad vissza, de System.ServiceProcess.ServiceController objektum tulajdonságainak parancsokat, és győződjön meg arról, az első Ezt az információt sokkal egyszerűbbek.

Az alábbi parancs lekéri a szolgáltatásokat, amelyek a LanmanWorkstation szolgáltatás megköveteli.

```powershell
PS> Get-Service -Name LanmanWorkstation -RequiredServices

Status   Name               DisplayName
------   ----               -----------
Running  MRxSmb20           SMB 2.0 MiniRedirector
Running  bowser             Bowser
Running  MRxSmb10           SMB 1.x MiniRedirector
Running  NSI                Network Store Interface Service
```

Az alábbi parancs lekéri a szolgáltatások igénylik a LanmanWorkstation szolgáltatás.

```powershell
PS> Get-Service -Name LanmanWorkstation -DependentServices

Status   Name               DisplayName
------   ----               -----------
Running  SessionEnv         Terminal Services Configuration
Running  Netlogon           Netlogon
Stopped  Browser            Computer Browser
Running  BITS               Background Intelligent Transfer Ser...
```

Minden függőségeket tartalmazó szolgáltatásokat is kaphat. A következő parancs nem éppen ezt, és majd a Format-Table parancsmagot használja a szolgáltatások állapotát, a neve, a RequiredServices és DependentServices tulajdonságainak megjelenítéséhez a számítógépen.

```powershell
Get-Service -Name * | Where-Object {$_.RequiredServices -or $_.DependentServices} | Format-Table -Property Status, Name, RequiredServices, DependentServices -auto
```

## <a name="stopping-starting-suspending-and-restarting-services"></a>Leállítása, indítása, felfüggesztése és szolgáltatások újraindítása

Az összes parancsmagok általános a vezetéknévhez rendelkezik. Szolgáltatások köznapi név vagy a megjelenített név alapján adható meg, és listák és értékekként helyettesítő karaktereket. A nyomtatási várólista leállításához használja:

```powershell
Stop-Service -Name spooler
```

Miután leállt a nyomtatási várólista indításához használja:

```powershell
Start-Service -Name spooler
```

A nyomtatási várólista felfüggesztéséhez használja:

```powershell
Suspend-Service -Name spooler
```

A `Restart-Service` parancsmag a Service egyéb parancsmagokhoz hasonlóan azonos módon működik, de, majd bemutatunk néhány összetettebb példa. A legegyszerűbb használja adja meg a szolgáltatás neve:

```powershell
PS> Restart-Service -Name spooler

WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
PS>
```

Megfigyelheti, hogy a nyomtatási sorkezelő kapcsolatos ismétlődő figyelmeztető üzenetet kap: indul el. Amikor egy műveletet, bizonyos idő elteltével végez, a Windows PowerShell értesíti Önt, hogy továbbra is megpróbálja elvégezni a feladatot.

Ha azt szeretné, több szolgáltatás újraindítását, szolgáltatások listáját, szűrheti őket, és végezze el az újraindítást:

```powershell
PS> Get-Service | Where-Object -FilterScript {$_.CanStop} | Restart-Service

WARNING: Waiting for service 'Computer Browser (Browser)' to finish stopping...
WARNING: Waiting for service 'Computer Browser (Browser)' to finish stopping...
Restart-Service : Cannot stop service 'Logical Disk Manager (dmserver)' because
 it has dependent services. It can only be stopped if the Force flag is set.
At line:1 char:57
+ Get-Service | Where-Object -FilterScript {$_.CanStop} | Restart-Service <<<<
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
```

Ezen parancsmagok nem rendelkezik a ComputerName paraméter, de futtathatja őket egy távoli számítógépen az Invoke-Command parancsmaggal. Például az a következő parancsot a kiszolgalo01 távoli számítógépen a nyomtatásisor-kezelő szolgáltatás újraindul.

```powershell
Invoke-Command -ComputerName Server01 {Restart-Service Spooler}
```

## <a name="setting-service-properties"></a>A beállítás szolgáltatás tulajdonságai

A `Set-Service` parancsmag módosítja egy helyi vagy távoli számítógépen valamelyik szolgáltatás tulajdonságait. Mivel a szolgáltatás állapotát a tulajdonsággal, ez a parancsmag segítségével indítása, leállítása és a egy szolgáltatást.
A Set-Service parancsmag paramétere egy indítási típusa, amely lehetővé teszi a szolgáltatás indítási típusának módosítását.

Használandó `Set-Service` a Windows Vista és Windows újabb verziói, nyissa meg a Windows Powershellt a "Futtatás rendszergazdaként" lehetőséggel.

További információkért lásd: [Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)

## <a name="see-also"></a>Lásd még:

- [Get-Service [m2]](https://technet.microsoft.com/en-us/library/0a09cb22-0a1c-4a79-9851-4e53075f9cf6)
- [Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)
- [Restart-Service [m2]](https://technet.microsoft.com/en-us/library/45acf50d-2277-4523-baf7-ce7ced977d0f)
- [Suspend-Service [m2]](https://technet.microsoft.com/en-us/library/c8492b87-0e21-4faf-8054-3c83c2ec2826)