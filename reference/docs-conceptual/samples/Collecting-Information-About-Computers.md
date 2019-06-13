---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Adatgyűjtés a számítógépekről
ms.openlocfilehash: 5dc8fcc5f12fdf9e3fc8151d3e50b8b660262c62
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030850"
---
# <a name="collecting-information-about-computers"></a>Adatgyűjtés a számítógépekről

A parancsmagok **CimCmdlets** modul a legfontosabb parancsmagok általános felügyeleti feladatokhoz.
Az összes kritikus fontosságú alrendszert beállítások WMI-n keresztül érhetők el.
Ezenkívül WMI adatok, amelyek a gyűjtemények egy vagy több elem objektumként kezeli.
Windows PowerShell is működik együtt az objektumok és a egy folyamatot, amely lehetővé teszi, hogy ugyanolyan módon való kezelése egyetlen vagy több objektum van, mert általános WMI hozzáférés lehetővé teszi a nagyon kevés munkát speciális feladatok elvégzésére.

Az alábbi példák bemutatják, hogyan lehet adott információk gyűjtése használatával `Get-CimInstance` egy tetszőleges számítógép ellen.
Adja meg, hogy a **ComputerName** pont értékű paraméter ( **.** ), amely jelöli, hogy a helyi számítógépen.
Megadhat egy nevet vagy a WMI-n keresztül érhető el minden olyan számítógéphez társított IP-cím.
A helyi számítógép adatainak beolvasásához, sikerült kihagyja a **ComputerName** paraméter.

## <a name="listing-desktop-settings"></a>Asztali beállítások listázása

Tudjuk, hogy az asztali adatokat gyűjt a helyi számítógépen paranccsal megkezdheti.

```powershell
Get-CimInstance -ClassName Win32_Desktop -ComputerName .
```

Az összes asztali számítógép, információkat ezt adja vissza, akár használatban van-e.

> [!NOTE]
> Bizonyos WMI-osztályok által visszaadott információk nagyon részletes lehetnek, és többek között általában a metaadatokat, a WMI-osztály.
Mivel a metaadat-tulajdonságot a legtöbb kezdődő nevű **Cim**, szűrheti a tulajdonságok használatával `Select-Object`.
Adja meg a **- ExcludeProperty** paraméter "Cim *" értéket.
Például:

```powershell
Get-CimInstance -ClassName Win32_Desktop -ComputerName . | Select-Object -ExcludeProperty "CIM*"
```

Szűrje ki a metaadatokat, a csővezeték-kezelőt (|) használatával küldjön eredményeit a `Get-CimInstance` parancsot a `Select-Object -ExcludeProperty "CIM*"`.

## <a name="listing-bios-information"></a>BIOS adatainak listázása

A WMI **Win32_BIOS** osztály adja vissza a rendszer BIOS viszonylag kompakt és teljes körű információkat a helyi számítógépen:

```powershell
Get-CimInstance -ClassName Win32_BIOS -ComputerName .
```

## <a name="listing-processor-information"></a>A processzor adatai listázása

A WMI használatával kérheti le általános processzoradatokat **Win32_Processor** osztályhoz, noha valószínűleg érdemes szűri az információkat:

```powershell
Get-CimInstance -ClassName Win32_Processor -ComputerName . | Select-Object -ExcludeProperty "CIM*"
```

A processzorcsaládját. általános leírása karakterlánc, akkor csak visszatérhet a **SystemType** tulajdonság:

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem -ComputerName . | Select-Object -Property SystemType

SystemType
----------
X86-based PC
```

## <a name="listing-computer-manufacturer-and-model"></a>Számítógép gyártója és modellje listázása

Számítógépadatok modell érhető el is **Win32_ComputerSystem**.
A megjelenített normál a kimenetbe nem kell a megadott szűréseket OEM-adatok:

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem
```

```output
Name PrimaryOwnerName Domain    TotalPhysicalMemory Model                   Manufacturer
---- ---------------- ------    ------------------- -----                   ------------
MyPC Jane Doe         WORKGROUP 804765696           DA243A-ABA 6415cl NA910 Compaq Presario 06
```

Csak akkor megegyezik az adatokat, hogy a parancsok, amely információkat ad vissza közvetlenül az egyes hardverekről, a kimenete.
Bizonyos adatok nem megfelelően van konfigurálva a hardvergyártók által, és ezért nem érhető el.

## <a name="listing-installed-hotfixes"></a>A telepített gyorsjavítások listázása

Használatával listázhatja az összes telepített gyorsjavítások **Win32_QuickFixEngineering**:

```powershell
Get-CimInstance -ClassName Win32_QuickFixEngineering -ComputerName .
```

Ez az osztály a következőhöz hasonló gyorsjavítások listáját adja vissza:

```output
Source Description     HotFixID  InstalledBy   InstalledOn PSComputerName
------ -----------     --------  -----------   ----------- --------------
       Security Update KB4048951 Administrator 12/16/2017  .
```

Több állapotára kimeneti érdemes kizárni néhány tulajdonság.
Bár használhatja a `Get-CimInstance`a **tulajdonság** paramétert csak válassza a **HotFixID**, ezzel úgy fognak visszaküldeni további információkért, mert az összes metaadat alapértelmezés szerint megjelenik:

```powershell
Get-CimInstance -ClassName Win32_QuickFixEngineering -ComputerName . -Property HotFixID
```

```output
PSShowComputerName    : True
InstalledOn           :
Caption               :
Description           :
InstallDate           :
Name                  :
Status                :
CSName                :
FixComments           :
HotFixID              : KB4048951
InstalledBy           :
ServicePackInEffect   :
PSComputerName        : .
CimClass              : root/cimv2:Win32_QuickFixEngineering
CimInstanceProperties : {Caption, Description, InstallDate, Name...}
CimSystemProperties   : Microsoft.Management.Infrastructure.CimSystemProperties
```

A további adatokat ad vissza, mert a tulajdonság paramétert `Get-CimInstance` korlátozza a kapott a WMI-osztálypéldány tulajdonságainak az objektum nem adott vissza a Windows powershellt.
A kimenet csökkentése érdekében használja `Select-Object`:

```powershell
Get-CimInstance -ClassName Win32_QuickFixEngineering -ComputerName . -Property HotFixId | Select-Object -Property HotFixId
```

```output
HotFixId
--------
KB4048951
```

## <a name="listing-operating-system-version-information"></a>Operációsrendszer-Verziószámukat listázása

A **Win32_OperatingSystem** osztálytulajdonságokat verziója és a service pack információval.
Explicit módon kiválaszthatja a fájlverzió-információkat a összefoglalójának lekérése a tulajdonságok csak **Win32_OperatingSystem**:

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property BuildNumber,BuildType,OSType,ServicePackMajorVersion,ServicePackMinorVersion
```

A helyettesítő karaktereket is használhatja a `Select-Object`a **tulajdonság** paraméter.
Mivel verziótól kezdve, vagy az összes tulajdonság **hozhat létre** vagy **szervizcsomag** fontos használja itt, hogy lerövidítheti Ez a következő formában:

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property Build*,OSType,ServicePack*
```

```output
BuildNumber             : 16299
BuildType               : Multiprocessor Free
OSType                  : 18
ServicePackMajorVersion : 0
ServicePackMinorVersion : 0
```

## <a name="listing-local-users-and-owner"></a>A helyi felhasználók és a tulajdonos listázása

Helyi általános információkat – licenccel rendelkező felhasználók száma, a felhasználók és a tulajdonos neve aktuális száma – között található egy kijelölt **Win32_OperatingSystem**' osztálytulajdonságokat.
Explicit módon kiválaszthatja a tulajdonságok alapján a következőképpen jelenik meg:

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property NumberOfLicensedUsers,NumberOfUsers,RegisteredUser
```

A helyettesítő karakterek használatával több állapotára verziója van:

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property *user*
```

## <a name="getting-available-disk-space"></a>Bevezetés a szabad lemezterület

Tekintse meg a lemezterület és a szabad terület a helyi meghajtókra, használhatja a Win32_LogicalDisk WMI-osztályt.
Meg kell tekintenie csak 3 és a egy DriveType példányok – WMI használja az érték rögzített merevlemez.

```powershell
Get-CimInstance -ClassName Win32_LogicalDisk -Filter "DriveType=3" -ComputerName .

DeviceID DriveType ProviderName VolumeName Size         FreeSpace   PSComputerName
-------- --------- ------------ ---------- ----         ---------   --------------
C:       3                      Local Disk 203912880128 65541357568 .
Q:       3                      New Volume 122934034432 44298250240 .

Get-CimInstance -ClassName Win32_LogicalDisk -Filter "DriveType=3" -ComputerName . | Measure-Object -Property FreeSpace,Size -Sum | Select-Object -Property Property,Sum

Property           Sum
--------           ---
FreeSpace 109839607808
Size      326846914560
```

## <a name="getting-logon-session-information"></a>Bejelentkezési munkamenet-információk lekérése

Társított keresztül a felhasználó bejelentkezési munkamenetek kapcsolatos általános információkat szerezhet a **Win32_LogonSession** WMI-osztály:

```powershell
Get-CimInstance -ClassName Win32_LogonSession -ComputerName .
```

## <a name="getting-the-user-logged-on-to-a-computer"></a>Bevezetés a számítógépre bejelentkezett felhasználó

A felhasználó jelentkezett be egy adott számítógép rendszer Win32_ComputerSystem használatával jeleníthet meg.
Ez a parancs csak a felhasználó bejelentkezett a rendszert asztal adja vissza:

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem -Property UserName -ComputerName .
```

## <a name="getting-local-time-from-a-computer"></a>Egy számítógép helyi ideje beolvasása

Egy adott számítógépen az aktuális helyi idő használatával lekérheti a **Win32_LocalTime** WMI-osztály.

```powershell
Get-CimInstance -ClassName Win32_LocalTime -ComputerName .

Day          : 15
DayOfWeek    : 4
Hour         : 12
Milliseconds :
Minute       : 11
Month        : 6
Quarter      : 2
Second       : 52
WeekInMonth  : 3
Year         : 2017
PSComputerName : .
```

## <a name="displaying-service-status"></a>Szolgáltatás állapotának megjelenítése

Az összes szolgáltatás állapotának megjelenítése egy adott számítógépen, helyben használhatja a `Get-Service` parancsmagot.
Távoli rendszerek esetén használhatja a **Win32_Service** WMI-osztály.
Ha is használja `Select-Object` , az eredmények szűréséhez **állapot**, **neve**, és **DisplayName**, kimeneti formátum a csaknem megegyezik-e a lesz`Get-Service`:

```powershell
Get-CimInstance -ClassName Win32_Service -ComputerName . | Select-Object -Property Status,Name,DisplayName
```

Ahhoz, hogy a teljes nevek a alkalmanként szolgáltatások rendkívül hosszú névvel rendelkező megjelenítését, előfordulhat, hogy használni kívánt `Format-Table` az a **AutoSize** és **burkolása** paraméterek oszlopszélesség optimalizálása és a hosszú nevek helyett a rendszer csonkolja burkolása engedélyezése:

```powershell
Get-CimInstance -ClassName Win32_Service -ComputerName . | Format-Table -Property Status,Name,DisplayName -AutoSize -Wrap
```
