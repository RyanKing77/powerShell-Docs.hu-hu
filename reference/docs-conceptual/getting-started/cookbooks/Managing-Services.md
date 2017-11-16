---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Szolgáltatások kezelése"
ms.assetid: 7a410e4d-514b-4813-ba0c-0d8cef88df31
ms.openlocfilehash: 9fd6c8bcfecc99756188409629ddf94b880aab91
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="managing-services"></a>Szolgáltatások kezelése
Nincsenek nyolc core szolgáltatás parancsmagkészleteket, a szolgáltatás feladatok széles köre. Követően áttekintjük csak listázása, és válassza a szolgáltatások elindítva, de kaphat a parancsmagok listáját a **Get-Help \&#42;-szolgáltatás**, és minden egyes szolgáltatás parancsmag további információt talál a használatával**Get-Help < parancsmag neve >**, például a **Get-Help új szolgáltatás**.

## <a name="getting-services"></a>Első szolgáltatások
Kaphat a szolgáltatások helyi vagy távoli számítógépen használja a **Get-Service** parancsmag. A **Get-Process**használatával a **Get-Service** paraméterek nélkül parancs visszaadja az összes szolgáltatás. Név szerint szűrheti, még akkor is használja a csillag helyettesítő karakterként:

```
PS> Get-Service -Name se*
Status   Name               DisplayName
------   ----               -----------
Running  seclogon           Secondary Logon
Running  SENS               System Event Notification
Stopped  ServiceLayer       ServiceLayer
```

Mivel nem mindig nyilvánvaló a szolgáltatás valódi neve van, azt tapasztalhatja, meg kell találnia szolgáltatások megjelenített név alapján. Ehhez egyedi neve, helyettesítő karakterek használatával, vagy használja a megjelenített nevek listája:

```
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

A számítógépnév paramétert a Get-Service parancsmag segítségével távoli számítógépeken a szolgáltatások beolvasása. A ComputerName paraméterre fogad el helyettesítő karaktereket, és több értékek nézze meg a szolgáltatások egyetlen paranccsal több számítógépen. Például a következő parancsot a szolgáltatás lekérdezi a kiszolgalo01 távoli számítógépen.

```
Get-Service -ComputerName Server01
```

## <a name="getting-required-and-dependent-services"></a>Első szükséges, és a függő szolgáltatások
A Get-Service parancsmag, amelyek nagyon hasznos a szolgáltatás felügyeleti két paraméterrel rendelkezik. A DependentServices paraméter szerzi meg, hogy a szolgáltatástól függő szolgáltatások. A RequiredServices paraméter szerzi meg szolgáltatások, amelyektől Ez a szolgáltatás függ.

Ezek a paraméterek megjelenítése a DependentServices és ServicesDependedOn (alias = RequiredServices) a System.ServiceProcess.ServiceController objektum, amelyek megkönnyítik a Get-Service értéket ad vissza, de a tulajdonságok a parancsokat és első Ezt az információt jóval egyszerűbbé válik.

A következő parancsot a szolgáltatások a LanmanWorkstation szolgáltatást igénylő lekérdezi.

```
PS> Get-Service -Name LanmanWorkstation -RequiredServices
Status   Name               DisplayName
------   ----               -----------
Running  MRxSmb20           SMB 2.0 MiniRedirector
Running  bowser             Bowser
Running  MRxSmb10           SMB 1.x MiniRedirector
Running  NSI                Network Store Interface Service
```

A következő parancsot a szolgáltatások a LanmanWorkstation szolgáltatást igénylő lekérdezi.

```
PS> Get-Service -Name LanmanWorkstation -DependentServices
Status   Name               DisplayName
------   ----               -----------
Running  SessionEnv         Terminal Services Configuration
Running  Netlogon           Netlogon
Stopped  Browser            Computer Browser
Running  BITS               Background Intelligent Transfer Ser...
```

Minden szolgáltatás olyan függőségekkel rendelkeznek, még akkor is kaphat. A következő parancs nem éppen ez, és majd a Format-Table parancsmagot használja a számítógépen a szolgáltatások állapotát, a nevét, a RequiredServices és DependentServices tulajdonságainak megjelenítéséhez.

```
Get-Service -Name * | where {$_.RequiredServices -or $_.DependentServices} | Format-Table -Property Status, Name, RequiredServices, DependentServices -auto
```

## <a name="stopping-starting-suspending-and-restarting-services"></a>Leállítása, elindítása, felfüggesztésével, és a szolgáltatások újraindítása
Az összes parancsmagok rendelkezik az általános űrlapon. Szolgáltatások közös neve vagy a megjelenítési név is megadható, és listák és a helyettesítő karakterek értékként. A nyomtatási várólista leállításához használja:

```
Stop-Service -Name spooler
```

Miután leállt a nyomtatási várólista elindításához használja:

```
Start-Service -Name spooler
```

A nyomtatási várólista felfüggesztéséhez használja:

```
Suspend-Service -Name spooler
```

A **Restart-Service** parancsmag a más parancsmagok az azonos módon működik, de az bemutatjuk a összetettebb példákat. A legegyszerűbb használatban van adja meg a szolgáltatás neve:

```
PS> Restart-Service -Name spooler
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
PS>
```

Megfigyelheti, hogy kap egy ismételt figyelmeztető üzenet arról a nyomtatásisor indítása. Egy műveletet, bizonyos idő végrehajtásakor a Windows PowerShell értesíti Önt, hogy továbbra is megpróbálja elvégezni a feladatot.

Ha azt szeretné, több szolgáltatás újraindítását, a szolgáltatások listáját, ezek szűrésére, és végezze el az újraindítást:

```
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

Ezen parancsmagok nem rendelkezik a ComputerName paraméterre, de futtathatja őket egy távoli számítógépen az Invoke-Command parancsmaggal. A következő parancs például a kiszolgalo01 távoli számítógépen a nyomtatásisor-kezelő szolgáltatás újraindul.

```
Invoke-Command -ComputerName Server01 {Restart-Service Spooler}
```

## <a name="setting-service-properties"></a>A beállítás szolgáltatás tulajdonságai
A szolgáltatás beállítása parancsmag módosítja a tulajdonságait egy helyi vagy távoli számítógépen. A szolgáltatás állapota tulajdonság, mert ez a parancsmag segítségével indítása, leállítása és a szolgáltatás felfüggesztése. A szolgáltatás beállítása parancsmag, amely lehetővé teszi, hogy a szolgáltatás indítási típusának módosítása StartupType paraméterrel is rendelkezik.

A Set-szolgáltatás használata a Windows Vista és újabb verziók, Windows, Windows PowerShell megnyitása a "Futtatás rendszergazdaként" lehetőséggel.

További információkért lásd: [[m2] Set-szolgáltatás](https://technet.microsoft.com/en-us/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)

## <a name="see-also"></a>Lásd még:
- [Get-Service [m2]](https://technet.microsoft.com/en-us/library/0a09cb22-0a1c-4a79-9851-4e53075f9cf6)
- [[M2] SET-szolgáltatás](https://technet.microsoft.com/en-us/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)
- [Restart-Service [m2]](https://technet.microsoft.com/en-us/library/45acf50d-2277-4523-baf7-ce7ced977d0f)
- [[M2] suspend-szolgáltatás](https://technet.microsoft.com/en-us/library/c8492b87-0e21-4faf-8054-3c83c2ec2826)

