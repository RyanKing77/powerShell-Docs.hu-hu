---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Adatgyűjtés a számítógépekről
ms.assetid: 9e7b6a2d-34f7-4731-a92c-8b3382eb51bb
ms.openlocfilehash: ca92474eaf6fa546c3d6450f5a282e45157018a8
ms.sourcegitcommit: 4a841ebda3339ae2477e0f5f5be8c01740221232
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/07/2018
---
# <a name="collecting-information-about-computers"></a>Adatgyűjtés a számítógépekről

A parancsmagok **CimCmdlets** modul a legfontosabb parancsmagok az általános rendszer-felügyeleti feladatok elvégzésére.
Minden kritikus alrendszer beállítás WMI-n keresztül érhetők el.
Továbbá WMI adatok, amelyek egy vagy több elem gyűjteményeiben objektumként kezeli.
Windows PowerShell is objektumok működik, és van egy folyamatot, amely lehetővé teszi, hogy egy vagy több objektum ugyanúgy kezelheti, mert az általános WMI-hozzáférését lehetővé teszi, nagyon kevés munkát néhány speciális feladatok elvégzéséhez.

Az alábbi példák bemutatják, hogyan lehet adott információgyűjtés használatával `Get-CimInstance` egy tetszőleges számítógép ellen.
Azt adja meg a **számítógépnév** pont értékű paraméter (**.**), amely jelenti, hogy a helyi számítógépen.
Megadhat egy nevet vagy a WMI-n keresztül érhető el a számítógéphez társított IP-címet.
A helyi számítógép adatainak lekérésére, nincs volt megadva a **számítógépnév** paraméter.

### <a name="listing-desktop-settings"></a>Asztali beállítások listázása

Egy parancs, amely az asztalok információt gyűjt a helyi számítógépen fogjuk első lépések.

```powershell
Get-CimInstance -ClassName Win32_Desktop -ComputerName .
```

Ez információt adhatja vissza az összes asztali számítógép, hogy használatban van-e.

> [!NOTE]
> Egyes WMI-osztályok által visszaadott adatok nagyon részletes kell, és többek között általában a WMI-osztály metaadatok.
Mivel a metaadatok tulajdonságok a többsége a karakterlánccal kezdődő **Cim**, szűrheti a Tulajdonságok `Select-Object`.
Adja meg a **- ExcludeProperty** paraméter "Cim *" értékeként.
Például:

```powershell
Get-CimInstance -ClassName Win32_Desktop -ComputerName . | Select-Object -ExcludeProperty "CIM*"
```

A metaadatok kiszűrésére küldhet csővezeték-kezelőt (|) eredményeit a `Get-CimInstance` parancsot `Select-Object -ExcludeProperty "CIM*"`.

### <a name="listing-bios-information"></a>BIOS-információkat listázása

A WMI **Win32_BIOS** osztály a BIOS viszonylag kompakt és teljes információt nyújt a helyi számítógépen:

```powershell
Get-CimInstance -ClassName Win32_BIOS -ComputerName .
```

### <a name="listing-processor-information"></a>A processzor adatai listázása

Általános adatok WMI segítségével kérheti le **Win32_Processor** osztály, de érdemes a megjelenített információkat szűrheti:

```powershell
Get-CimInstance -ClassName Win32_Processor -ComputerName . | Select-Object -ExcludeProperty "CIM*"
```

Általános leírás karakterlánc processzorcsaládját, most lépjen vissza a **SystemType** tulajdonság:

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem -ComputerName . | Select-Object -Property SystemType

SystemType
----------
X86-based PC
```

### <a name="listing-computer-manufacturer-and-model"></a>Számítógép gyártója és modellje listázása

Számítógép típusra vonatkozó adatokat is rendelkezésre áll, a **Win32_ComputerSystem**.
A standard megjelenített kimenete nem lesz szükség a szűrés OEM adatokat:

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem
```

```output
Name PrimaryOwnerName Domain    TotalPhysicalMemory Model                   Manufacturer
---- ---------------- ------    ------------------- -----                   ------------
MyPC Jane Doe         WORKGROUP 804765696           DA243A-ABA 6415cl NA910 Compaq Presario 06
```

A parancsok, amely vissza az adatokat közvetlenül a hardver, eredménye csak az adatokat, hogy megegyezik.
Néhány információt által hardvergyártók nincs megfelelően beállítva, és ezért nem érhető el.

### <a name="listing-installed-hotfixes"></a>A telepített gyorsjavítások listázása

Minden telepített gyorsjavítások segítségével listázhatja **Win32_QuickFixEngineering**:

```powershell
Get-CimInstance -ClassName Win32_QuickFixEngineering -ComputerName .
```

Ez az osztály a gyorsjavítást, amely a következőképpen néz ki listáját adja vissza:

```output
Source Description     HotFixID  InstalledBy   InstalledOn PSComputerName
------ -----------     --------  -----------   ----------- --------------
       Security Update KB4048951 Administrator 12/16/2017  .
```

A kimenet több állapotára előfordulhat, hogy kizárni kívánt néhány tulajdonságát.
Bár a `Get-CimInstance`tartozó **tulajdonság** paraméter csak kiválasztása a **HotFixID**, ezzel úgy ténylegesen ad meg további információkat, mert alapértelmezés szerint megjelenik a metaadatok:

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

A további adat, mert a tulajdonság paraméterének `Get-CimInstance` korlátozza a WMI-osztálypéldány visszakapott tulajdonságok a objektum nem adott vissza a Windows PowerShell.
A kimeneti csökkentése érdekében használjon `Select-Object`:

```powershell
Get-CimInstance -ClassName Win32_QuickFixEngineering -ComputerName . -Property HotFixId | Select-Object -Property HotFixId
```

```output
HotFixId
--------
KB4048951
```

### <a name="listing-operating-system-version-information"></a>Operációs rendszer verzióinformációja listázása

A **Win32_OperatingSystem** osztálytulajdonságokat verziója és a service pack információval.
Kifejezetten választhatja csak ezeket a tulajdonságokat a fájlverzió-információkat az összefoglaló lekérése **Win32_OperatingSystem**:

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property BuildNumber,BuildType,OSType,ServicePackMajorVersion,ServicePackMinorVersion
```

A helyettesítő karakterek is használhatja a `Select-Object`tartozó **tulajdonság** paraméter.
Mivel vagy kezdve található összes tulajdonság **Build** vagy **szervizcsomag** fontos használandó itt, azt is Rövidítse le ez a következő űrlapon:

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

### <a name="listing-local-users-and-owner"></a>Helyi felhasználók és a tulajdonos listázása

Helyi általános információkat – licenccel rendelkező felhasználók száma, a felhasználók és a tulajdonos neve aktuális száma – a kijelölt található **Win32_OperatingSystem**' osztálytulajdonságokat.
Explicit módon kiválaszthatja a megjelenítendő tulajdonságokat:

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property NumberOfLicensedUsers,NumberOfUsers,RegisteredUser
```

A helyettesítő karakterek használatával több állapotára verziója van:

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property *user*
```

### <a name="getting-available-disk-space"></a>Első rendelkezésre álló szabad lemezterület

Olvassa el a lemezterület és a szabad terület a helyi meghajtókra, használhatja a Win32_LogicalDisk WMI-osztályt.
Csak a 3-ból a DriveType rendelkező példányai látni – WMI használ az érték rögzített merevlemez.

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

### <a name="getting-logon-session-information"></a>Bejelentkezési munkamenet adatainak lekérése

Bejelentkezési munkamenetek, felhasználókon társított kapcsolatos általános információkat kaphat a **Win32_LogonSession** WMI-osztály:

```powershell
Get-CimInstance -ClassName Win32_LogonSession -ComputerName .
```

### <a name="getting-the-user-logged-on-to-a-computer"></a>A számítógépre bejelentkezett felhasználó beolvasása

A felhasználó jelentkezik be egy adott számítógép rendszer Win32_ComputerSystem használatával jelenítheti meg.
A parancs csak a rendszer asztali bejelentkezett felhasználó adja vissza:

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem -Property UserName -ComputerName .
```

### <a name="getting-local-time-from-a-computer"></a>Egy számítógép helyi ideje lekérése

Az aktuális helyi idő az adott számítógépre használatával kérheti le a **Win32_LocalTime** WMI-osztályt.

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

### <a name="displaying-service-status"></a>Szolgáltatás állapotának megjelenítése

Egy adott számítógép összes szolgáltatás állapotának megtekintéséhez helyileg használhatja a `Get-Service` parancsmag.
A távoli rendszerek esetében is használhatja a **Win32_Service** WMI-osztályt.
Ha is a `Select-Object` az eredmények szűréséhez **állapot**, **neve**, és **DisplayName**, a kimeneti formátum lesz majdnem megegyezik-e, a `Get-Service`:

```powershell
Get-CimInstance -ClassName Win32_Service -ComputerName . | Select-Object -Property Status,Name,DisplayName
```

Ahhoz, hogy a teljes képernyőt az alkalmi szolgáltatások névváltozásai rendkívül hosszú névvel rendelkező, előfordulhat, hogy használni kívánt `Format-Table` rendelkező a **AutoSize** és **burkolása** paraméterek oszlopszélesség optimalizálása és hosszú nevek helyett csonkolva lesz csomagolásához engedélyezése:

```powershell
Get-CimInstance -ClassName Win32_Service -ComputerName . | Format-Table -Property Status,Name,DisplayName -AutoSize -Wrap
```
