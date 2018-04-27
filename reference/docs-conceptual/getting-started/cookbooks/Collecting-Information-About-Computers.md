---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Adatgyűjtés a számítógépekről
ms.assetid: 9e7b6a2d-34f7-4731-a92c-8b3382eb51bb
ms.openlocfilehash: 7f5a5f6accd57a84e2bcb3d20c14640a8e028791
ms.sourcegitcommit: a9aa5e8d0fab0cbb3e4e6cff0e3ca8c0339ab4e6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/27/2018
---
# <a name="collecting-information-about-computers"></a>Adatgyűjtés a számítógépekről

**Get-WmiObject** van az egyik legfontosabb parancsmagot, a rendszer általános kezelési feladatok. Minden kritikus alrendszer beállítás WMI-n keresztül érhetők el. Továbbá WMI adatok, amelyek egy vagy több elem gyűjteményeiben objektumként kezeli. Windows PowerShell is objektumok működik, és van egy folyamatot, amely lehetővé teszi, hogy egy vagy több objektum ugyanúgy kezelheti, mert az általános WMI-hozzáférését lehetővé teszi, nagyon kevés munkát néhány speciális feladatok elvégzéséhez.

Az alábbi példák bemutatják, hogyan lehet adott információgyűjtés használatával **Get-WmiObject** egy tetszőleges számítógép ellen. Azt adja meg a **számítógépnév** pont értékű paraméter (**.**), amely jelenti, hogy a helyi számítógépen. Megadhat egy nevet vagy a WMI-n keresztül érhető el a számítógéphez társított IP-címet. A helyi számítógép adatainak lekérésére, nincs volt megadva a **- ComputerName.**

### <a name="listing-desktop-settings"></a>Asztali beállítások listázása

Egy parancs, amely az asztalok információt gyűjt a helyi számítógépen fogjuk első lépések.

```powershell
Get-WmiObject -Class Win32_Desktop -ComputerName .
```

Ez információt adhatja vissza az összes asztali számítógép, hogy használatban van-e.

> [!NOTE]
> Egyes WMI-osztályok által visszaadott adatok nagyon részletes kell, és többek között általában a WMI-osztály metaadatok. A metaadat-tulajdonságainak többsége a neve, dupla aláhúzásjellel kezdődő, mert a Select-Object tulajdonságok jeleníthetők meg. Betűk karakterekkel kezdődő tulajdonságokat használatával adja meg **[a – z]*** tulajdonság értékeként. Például:

```powershell
Get-WmiObject -Class Win32_Desktop -ComputerName . | Select-Object -Property [a-z]*
```

A metaadatok kiszűrésére segítségével (|) csővezeték-kezelőt a Get-WmiObject parancs küldése `Select-Object -Property [a-z]*`.

### <a name="listing-bios-information"></a>BIOS-információkat listázása

A WMI Win32_BIOS osztály a BIOS viszonylag kompakt és teljes információt ad vissza a helyi számítógépen:

```powershell
Get-WmiObject -Class Win32_BIOS -ComputerName .
```

### <a name="listing-processor-information"></a>A processzor adatai listázása

Általános adatok WMI segítségével kérheti le **Win32_Processor** osztály, de érdemes a megjelenített információkat szűrheti:

```powershell
Get-WmiObject -Class Win32_Processor -ComputerName . | Select-Object -Property [a-z]*
```

Általános leírás karakterlánc processzorcsaládját, most lépjen vissza a **SystemType** tulajdonság:

```
PS> Get-WmiObject -Class Win32_ComputerSystem -ComputerName . | Select-Object -Property SystemType

SystemType
----------
X86-based PC
```

### <a name="listing-computer-manufacturer-and-model"></a>Számítógép gyártója és modellje listázása

Számítógép típusra vonatkozó adatokat is rendelkezésre áll, a **Win32_ComputerSystem**. A standard megjelenített kimenete nem lesz szükség a szűrés OEM adatokat:

```
PS> Get-WmiObject -Class Win32_ComputerSystem

Domain              : WORKGROUP
Manufacturer        : Compaq Presario 06
Model               : DA243A-ABA 6415cl NA910
Name                : MyPC
PrimaryOwnerName    : Jane Doe
TotalPhysicalMemory : 804765696
```

A parancsok, amely vissza az adatokat közvetlenül a hardver, eredménye csak az adatokat, hogy megegyezik. Néhány információt által hardvergyártók nincs megfelelően beállítva, és ezért nem érhető el.

### <a name="listing-installed-hotfixes"></a>A telepített gyorsjavítások listázása

Minden telepített gyorsjavítások segítségével listázhatja **Win32_QuickFixEngineering**:

```powershell
Get-WmiObject -Class Win32_QuickFixEngineering -ComputerName .
```

Ez az osztály a gyorsjavítást, amely a következőképpen néz ki listáját adja vissza:

```output
Description         : Update for Windows XP (KB910437)
FixComments         : Update
HotFixID            : KB910437
Install Date        :
InstalledBy         : Administrator
InstalledOn         : 12/16/2005
Name                :
ServicePackInEffect : SP3
Status              :
```

A kimenet több állapotára előfordulhat, hogy kizárni kívánt néhány tulajdonságát. Bár a **Get-WmiObject tulajdonság** paraméter csak kiválasztása a **HotFixID**, ezzel úgy ténylegesen ad meg további információkat, mert alapértelmezés szerint megjelenik a metaadatok:

```
PS> Get-WmiObject -Class Win32_QuickFixEngineering -ComputerName . -Property HotFixID

HotFixID         : KB910437
__GENUS          : 2
__CLASS          : Win32_QuickFixEngineering
__SUPERCLASS     :
__DYNASTY        :
__RELPATH        :
__PROPERTY_COUNT : 1
__DERIVATION     : {}
__SERVER         :
__NAMESPACE      :
__PATH           :
```

A további adat, mert a tulajdonság paraméterének **Get-WmiObject** korlátozza a WMI-osztálypéldány visszakapott tulajdonságok a objektum nem adott vissza a Windows PowerShell. A kimeneti csökkentése érdekében használjon **Select-Object**:

```
PS> Get-WmiObject -Class Win32_QuickFixEngineering -ComputerName . -Property HotFixId | Select-Object -Property HotFixId

HotFixId
--------
KB910437
```

### <a name="listing-operating-system-version-information"></a>Operációs rendszer verzióinformációja listázása

A **Win32_OperatingSystem** osztálytulajdonságokat verziója és a service pack információval. Kifejezetten választhatja csak ezeket a tulajdonságokat a fájlverzió-információkat az összefoglaló lekérése **Win32_OperatingSystem**:

```powershell
Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property BuildNumber,BuildType,OSType,ServicePackMajorVersion,ServicePackMinorVersion
```

A helyettesítő karakterek is használhatja a **Select-Object tulajdonság** paraméter. Mivel vagy kezdve található összes tulajdonság **Build** vagy **szervizcsomag** fontos használandó itt, azt is Rövidítse le ez a következő űrlapon:

```
PS> Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property Build*,OSType,ServicePack*

BuildNumber             : 2600
BuildType               : Uniprocessor Free
OSType                  : 18
ServicePackMajorVersion : 2
ServicePackMinorVersion : 0
```

### <a name="listing-local-users-and-owner"></a>Helyi felhasználók és a tulajdonos listázása

Helyi általános információkat – licenccel rendelkező felhasználók száma, a felhasználók és a tulajdonos neve aktuális száma – a kijelölt található **Win32_OperatingSystem** tulajdonságait. Explicit módon kiválaszthatja a megjelenítendő tulajdonságokat:

```powershell
Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property NumberOfLicensedUsers,NumberOfUsers,RegisteredUser
```

A helyettesítő karakterek használatával több állapotára verziója van:

```powershell
Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property *user*
```

### <a name="getting-available-disk-space"></a>Első rendelkezésre álló szabad lemezterület

Olvassa el a lemezterület és a szabad terület a helyi meghajtókra, a WMI Win32_LogicalDisk osztály is használhat. Csak a 3-ból a DriveType rendelkező példányai látni – WMI használ az érték rögzített merevlemez.

```
PS> Get-WmiObject -Class Win32_LogicalDisk -Filter "DriveType=3" -ComputerName .

DeviceID     : C:
DriveType    : 3
ProviderName :
FreeSpace    : 65541357568
Size         : 203912880128
VolumeName   : Local Disk

DeviceID     : Q:
DriveType    : 3
ProviderName :
FreeSpace    : 44298250240
Size         : 122934034432
VolumeName   : New Volume

PS> Get-WmiObject -Class Win32_LogicalDisk -Filter "DriveType=3" -ComputerName . | Measure-Object -Property FreeSpace,Size -Sum | Select-Object -Property Property,Sum

Property           Sum
--------           ---
FreeSpace 109839607808
Size      326846914560
```

### <a name="getting-logon-session-information"></a>Bejelentkezési munkamenet adatainak lekérése

A WMI Win32_LogonSession osztály végig a felhasználókat társított bejelentkezési munkamenetek kapcsolatos általános információkat kaphat:

```powershell
Get-WmiObject -Class Win32_LogonSession -ComputerName .
```

### <a name="getting-the-user-logged-on-to-a-computer"></a>A számítógépre bejelentkezett felhasználó beolvasása

A felhasználó jelentkezik be egy adott számítógép rendszer Win32_ComputerSystem használatával jelenítheti meg. A parancs csak a rendszer asztali bejelentkezett felhasználó adja vissza:

```powershell
Get-WmiObject -Class Win32_ComputerSystem -Property UserName -ComputerName .
```

### <a name="getting-local-time-from-a-computer"></a>Egy számítógép helyi ideje lekérése

Az aktuális helyi idő az adott számítógépre a WMI Win32_LocalTime osztály használatával kérheti le. Ez az osztály alapértelmezés szerint minden metaadat jeleníti meg, mert előfordulhat, hogy szűrni kívánt használatával **Select-Object**:

```
PS> Get-WmiObject -Class Win32_LocalTime -ComputerName . | Select-Object -Property [a-z]*

Day          : 15
DayOfWeek    : 4
Hour         : 12
Milliseconds :
Minute       : 11
Month        : 6
Quarter      : 2
Second       : 52
WeekInMonth  : 3
Year         : 2006
```

### <a name="displaying-service-status"></a>Szolgáltatás állapotának megjelenítése

Egy adott számítógép összes szolgáltatás állapotának megtekintéséhez helyileg használhatja a **Get-Service** parancsmag a korábban említett. A távoli rendszerek esetében a WMI Win32_Service osztály is használhatja. Ha is a **Select-Object** az eredmények szűréséhez **állapot**, **neve**, és **DisplayName**, a kimeneti formátum szinte lesz megegyezik-e a **Get-Service**:

```powershell
Get-WmiObject -Class Win32_Service -ComputerName . | Select-Object -Property Status,Name,DisplayName
```

Ahhoz, hogy a teljes képernyőt az alkalmi szolgáltatások névváltozásai rendkívül hosszú névvel rendelkező, előfordulhat, hogy használni kívánt **Format-Table** rendelkező a **AutoSize** és **burkolása** paraméterek , oszlopszélesség optimalizálása és a hosszú nevek helyett csonkolva lesz csomagolásához engedélyezése:

```powershell
Get-WmiObject -Class Win32_Service -ComputerName . | Format-Table -Property Status,Name,DisplayName -AutoSize -Wrap
```
