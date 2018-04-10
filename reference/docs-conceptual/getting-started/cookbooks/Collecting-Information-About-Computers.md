---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Adatgyűjtés a számítógépekről
ms.assetid: 9e7b6a2d-34f7-4731-a92c-8b3382eb51bb
ms.openlocfilehash: c914a7133a1ac0a05346233db802175f7f29c6b2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="collecting-information-about-computers"></a><span data-ttu-id="f6c00-103">Adatgyűjtés a számítógépekről</span><span class="sxs-lookup"><span data-stu-id="f6c00-103">Collecting Information About Computers</span></span>

<span data-ttu-id="f6c00-104">**Get-WmiObject** van az egyik legfontosabb parancsmagot, a rendszer általános kezelési feladatok.</span><span class="sxs-lookup"><span data-stu-id="f6c00-104">**Get-WmiObject** is the most important cmdlet for general system management tasks.</span></span> <span data-ttu-id="f6c00-105">Minden kritikus alrendszer beállítás WMI-n keresztül érhetők el.</span><span class="sxs-lookup"><span data-stu-id="f6c00-105">All critical subsystem settings are exposed through WMI.</span></span> <span data-ttu-id="f6c00-106">Továbbá WMI adatok, amelyek egy vagy több elem gyűjteményeiben objektumként kezeli.</span><span class="sxs-lookup"><span data-stu-id="f6c00-106">Furthermore, WMI treats data as objects that are in collections of one or more items.</span></span> <span data-ttu-id="f6c00-107">Windows PowerShell is objektumok működik, és van egy folyamatot, amely lehetővé teszi, hogy egy vagy több objektum ugyanúgy kezelheti, mert az általános WMI-hozzáférését lehetővé teszi, nagyon kevés munkát néhány speciális feladatok elvégzéséhez.</span><span class="sxs-lookup"><span data-stu-id="f6c00-107">Because Windows PowerShell also works with objects and has a pipeline that allows you to treat single or multiple objects in the same way, generic WMI access allows you to perform some advanced tasks with very little work.</span></span>

<span data-ttu-id="f6c00-108">Az alábbi példák bemutatják, hogyan lehet adott információgyűjtés használatával **Get-WmiObject** egy tetszőleges számítógép ellen.</span><span class="sxs-lookup"><span data-stu-id="f6c00-108">The following examples demonstrate how to collect specific information by using **Get-WmiObject** against an arbitrary computer.</span></span> <span data-ttu-id="f6c00-109">Azt adja meg a **számítógépnév** pont értékű paraméter (**.**), amely jelenti, hogy a helyi számítógépen.</span><span class="sxs-lookup"><span data-stu-id="f6c00-109">We specify the **ComputerName** parameter with the dot value (**.**), which represents the local computer.</span></span> <span data-ttu-id="f6c00-110">Megadhat egy nevet vagy a WMI-n keresztül érhető el a számítógéphez társított IP-címet.</span><span class="sxs-lookup"><span data-stu-id="f6c00-110">You can specify a name or IP address associated with any computer you can reach through WMI.</span></span> <span data-ttu-id="f6c00-111">A helyi számítógép adatainak lekérésére, nincs volt megadva a **- ComputerName.**</span><span class="sxs-lookup"><span data-stu-id="f6c00-111">To retrieve information about the local computer, you could omit the **-ComputerName.**</span></span>

### <a name="listing-desktop-settings"></a><span data-ttu-id="f6c00-112">Asztali beállítások listázása</span><span class="sxs-lookup"><span data-stu-id="f6c00-112">Listing Desktop Settings</span></span>

<span data-ttu-id="f6c00-113">Egy parancs, amely az asztalok információt gyűjt a helyi számítógépen fogjuk első lépések.</span><span class="sxs-lookup"><span data-stu-id="f6c00-113">We'll begin with a command that collects information about the desktops on the local computer.</span></span>

```powershell
Get-WmiObject -Class Win32_Desktop -ComputerName .
```

<span data-ttu-id="f6c00-114">Ez információt adhatja vissza az összes asztali számítógép, hogy használatban van-e.</span><span class="sxs-lookup"><span data-stu-id="f6c00-114">This returns information for all desktops, whether they are in use or not.</span></span>

> [!NOTE]
> <span data-ttu-id="f6c00-115">Egyes WMI-osztályok által visszaadott adatok nagyon részletes kell, és többek között általában a WMI-osztály metaadatok.</span><span class="sxs-lookup"><span data-stu-id="f6c00-115">Information returned by some WMI classes can be very detailed, and often include metadata about the WMI class.</span></span> <span data-ttu-id="f6c00-116">A metaadat-tulajdonságainak többsége a neve, dupla aláhúzásjellel kezdődő, mert a Select-Object tulajdonságok jeleníthetők meg.</span><span class="sxs-lookup"><span data-stu-id="f6c00-116">Because most of these metadata properties have names that begin with a double underscore, you can filter the properties using Select-Object.</span></span> <span data-ttu-id="f6c00-117">Betűk karakterekkel kezdődő tulajdonságokat használatával adja meg **[a – z]**\* tulajdonság értékeként.</span><span class="sxs-lookup"><span data-stu-id="f6c00-117">Specify only properties that begin with alphabetic characters by using **[a-z]**\* as the Property value.</span></span> <span data-ttu-id="f6c00-118">Például:</span><span class="sxs-lookup"><span data-stu-id="f6c00-118">For example:</span></span>

```powershell
Get-WmiObject -Class Win32_Desktop -ComputerName . | Select-Object -Property [a-z]*
```

<span data-ttu-id="f6c00-119">A metaadatok kiszűrésére segítségével (|) csővezeték-kezelőt a Get-WmiObject parancs küldése ** Select-Object - tulajdonság [a – z] x.</span><span class="sxs-lookup"><span data-stu-id="f6c00-119">To filter out the metadata, use a pipeline operator (|) to send the results of the Get-WmiObject command to \*\*Select-Object -Property [a-z]\*\*\*.</span></span>

### <a name="listing-bios-information"></a><span data-ttu-id="f6c00-120">BIOS-információkat listázása</span><span class="sxs-lookup"><span data-stu-id="f6c00-120">Listing BIOS Information</span></span>

<span data-ttu-id="f6c00-121">A WMI Win32_BIOS osztály a BIOS viszonylag kompakt és teljes információt ad vissza a helyi számítógépen:</span><span class="sxs-lookup"><span data-stu-id="f6c00-121">The WMI Win32_BIOS class returns fairly compact and complete information about the system BIOS on the local computer:</span></span>

```powershell
Get-WmiObject -Class Win32_BIOS -ComputerName .
```

### <a name="listing-processor-information"></a><span data-ttu-id="f6c00-122">A processzor adatai listázása</span><span class="sxs-lookup"><span data-stu-id="f6c00-122">Listing Processor Information</span></span>

<span data-ttu-id="f6c00-123">Általános adatok WMI segítségével kérheti le **Win32_Processor** osztály, de érdemes a megjelenített információkat szűrheti:</span><span class="sxs-lookup"><span data-stu-id="f6c00-123">You can retrieve general processor information by using WMI's **Win32_Processor** class, although you will likely want to filter the information:</span></span>

```powershell
Get-WmiObject -Class Win32_Processor -ComputerName . | Select-Object -Property [a-z]*
```

<span data-ttu-id="f6c00-124">Általános leírás karakterlánc processzorcsaládját, most lépjen vissza a **SystemType** tulajdonság:</span><span class="sxs-lookup"><span data-stu-id="f6c00-124">For a generic description string of the processor family, you can just return the **SystemType** property:</span></span>

```
PS> Get-WmiObject -Class Win32_ComputerSystem -ComputerName . | Select-Object -Property SystemType

SystemType
----------
X86-based PC
```

### <a name="listing-computer-manufacturer-and-model"></a><span data-ttu-id="f6c00-125">Számítógép gyártója és modellje listázása</span><span class="sxs-lookup"><span data-stu-id="f6c00-125">Listing Computer Manufacturer and Model</span></span>

<span data-ttu-id="f6c00-126">Számítógép típusra vonatkozó adatokat is rendelkezésre áll, a **Win32_ComputerSystem**.</span><span class="sxs-lookup"><span data-stu-id="f6c00-126">Computer model information is also available from **Win32_ComputerSystem**.</span></span> <span data-ttu-id="f6c00-127">A standard megjelenített kimenete nem lesz szükség a szűrés OEM adatokat:</span><span class="sxs-lookup"><span data-stu-id="f6c00-127">The standard displayed output will not need any filtering to provide OEM data:</span></span>

```
PS> Get-WmiObject -Class Win32_ComputerSystem

Domain              : WORKGROUP
Manufacturer        : Compaq Presario 06
Model               : DA243A-ABA 6415cl NA910
Name                : MyPC
PrimaryOwnerName    : Jane Doe
TotalPhysicalMemory : 804765696
```

<span data-ttu-id="f6c00-128">A parancsok, amely vissza az adatokat közvetlenül a hardver, eredménye csak az adatokat, hogy megegyezik.</span><span class="sxs-lookup"><span data-stu-id="f6c00-128">Your output from commands such as this, which return information directly from some hardware, is only as good as the data you have.</span></span> <span data-ttu-id="f6c00-129">Néhány információt által hardvergyártók nincs megfelelően beállítva, és ezért nem érhető el.</span><span class="sxs-lookup"><span data-stu-id="f6c00-129">Some information is not correctly configured by hardware manufacturers and may therefore be unavailable.</span></span>

### <a name="listing-installed-hotfixes"></a><span data-ttu-id="f6c00-130">A telepített gyorsjavítások listázása</span><span class="sxs-lookup"><span data-stu-id="f6c00-130">Listing Installed Hotfixes</span></span>

<span data-ttu-id="f6c00-131">Minden telepített gyorsjavítások segítségével listázhatja **Win32_QuickFixEngineering**:</span><span class="sxs-lookup"><span data-stu-id="f6c00-131">You can list all installed hotfixes by using **Win32_QuickFixEngineering**:</span></span>

```powershell
Get-WmiObject -Class Win32_QuickFixEngineering -ComputerName .
```

<span data-ttu-id="f6c00-132">Ez az osztály a gyorsjavítást, amely a következőképpen néz ki listáját adja vissza:</span><span class="sxs-lookup"><span data-stu-id="f6c00-132">This class returns a list of hotfixes that looks like this:</span></span>

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

<span data-ttu-id="f6c00-133">A kimenet több állapotára előfordulhat, hogy kizárni kívánt néhány tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="f6c00-133">For more succinct output, you may want to exclude some properties.</span></span> <span data-ttu-id="f6c00-134">Bár a **Get-WmiObject tulajdonság** paraméter csak kiválasztása a **HotFixID**, ezzel úgy ténylegesen ad meg további információkat, mert alapértelmezés szerint megjelenik a metaadatok:</span><span class="sxs-lookup"><span data-stu-id="f6c00-134">Although you can use the **Get-WmiObject's Property** parameter to choose only the **HotFixID**, doing so will actually return more information, because all the metadata is displayed by default:</span></span>

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

<span data-ttu-id="f6c00-135">A további adat, mert a tulajdonság paraméterének **Get-WmiObject** korlátozza a WMI-osztálypéldány visszakapott tulajdonságok a objektum nem adott vissza a Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6c00-135">The additional data is returned, because the Property parameter in **Get-WmiObject** restricts the properties returned from WMI class instances, not the object returned to Windows PowerShell.</span></span> <span data-ttu-id="f6c00-136">A kimeneti csökkentése érdekében használjon **Select-Object**:</span><span class="sxs-lookup"><span data-stu-id="f6c00-136">To reduce the output, use **Select-Object**:</span></span>

```
PS> Get-WmiObject -Class Win32_QuickFixEngineering -ComputerName . -Property HotFixId | Select-Object -Property HotFixId

HotFixId
--------
KB910437
```

### <a name="listing-operating-system-version-information"></a><span data-ttu-id="f6c00-137">Operációs rendszer verzióinformációja listázása</span><span class="sxs-lookup"><span data-stu-id="f6c00-137">Listing Operating System Version Information</span></span>

<span data-ttu-id="f6c00-138">A **Win32_OperatingSystem** osztálytulajdonságokat verziója és a service pack információval.</span><span class="sxs-lookup"><span data-stu-id="f6c00-138">The **Win32_OperatingSystem** class properties include version and service pack information.</span></span> <span data-ttu-id="f6c00-139">Kifejezetten választhatja csak ezeket a tulajdonságokat a fájlverzió-információkat az összefoglaló lekérése **Win32_OperatingSystem**:</span><span class="sxs-lookup"><span data-stu-id="f6c00-139">You can explicitly select only these properties to get a version information summary from **Win32_OperatingSystem**:</span></span>

```powershell
Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property BuildNumber,BuildType,OSType,ServicePackMajorVersion,ServicePackMinorVersion
```

<span data-ttu-id="f6c00-140">A helyettesítő karakterek is használhatja a **Select-Object tulajdonság** paraméter.</span><span class="sxs-lookup"><span data-stu-id="f6c00-140">You can also use wildcards with the **Select-Object's Property** parameter.</span></span> <span data-ttu-id="f6c00-141">Mivel vagy kezdve található összes tulajdonság **Build** vagy **szervizcsomag** fontos használandó itt, azt is Rövidítse le ez a következő űrlapon:</span><span class="sxs-lookup"><span data-stu-id="f6c00-141">Because all the properties beginning with either **Build** or **ServicePack** are important to use here, we can shorten this to the following form:</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property Build*,OSType,ServicePack*

BuildNumber             : 2600
BuildType               : Uniprocessor Free
OSType                  : 18
ServicePackMajorVersion : 2
ServicePackMinorVersion : 0
```

### <a name="listing-local-users-and-owner"></a><span data-ttu-id="f6c00-142">Helyi felhasználók és a tulajdonos listázása</span><span class="sxs-lookup"><span data-stu-id="f6c00-142">Listing Local Users and Owner</span></span>

<span data-ttu-id="f6c00-143">Helyi általános információkat – licenccel rendelkező felhasználók száma, a felhasználók és a tulajdonos neve aktuális száma – a kijelölt található **Win32_OperatingSystem** tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="f6c00-143">Local general user information—number of licensed users, current number of users, and owner name—can be found with a selection of **Win32_OperatingSystem** properties.</span></span> <span data-ttu-id="f6c00-144">Explicit módon kiválaszthatja a megjelenítendő tulajdonságokat:</span><span class="sxs-lookup"><span data-stu-id="f6c00-144">You can explicitly select the properties to display like this:</span></span>

```powershell
Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property NumberOfLicensedUsers,NumberOfUsers,RegisteredUser
```

<span data-ttu-id="f6c00-145">A helyettesítő karakterek használatával több állapotára verziója van:</span><span class="sxs-lookup"><span data-stu-id="f6c00-145">A more succinct version using wildcards is:</span></span>

```powershell
Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property *user*
```

### <a name="getting-available-disk-space"></a><span data-ttu-id="f6c00-146">Első rendelkezésre álló szabad lemezterület</span><span class="sxs-lookup"><span data-stu-id="f6c00-146">Getting Available Disk Space</span></span>

<span data-ttu-id="f6c00-147">Olvassa el a lemezterület és a szabad terület a helyi meghajtókra, a WMI Win32_LogicalDisk osztály is használhat.</span><span class="sxs-lookup"><span data-stu-id="f6c00-147">To see the disk space and free space for local drives, you can use the WMI Win32_LogicalDisk class.</span></span> <span data-ttu-id="f6c00-148">Csak a 3-ból a DriveType rendelkező példányai látni – WMI használ az érték rögzített merevlemez.</span><span class="sxs-lookup"><span data-stu-id="f6c00-148">You need to see only instances with a DriveType of 3—the value WMI uses for fixed hard disks.</span></span>

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

### <a name="getting-logon-session-information"></a><span data-ttu-id="f6c00-149">Bejelentkezési munkamenet adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="f6c00-149">Getting Logon Session Information</span></span>

<span data-ttu-id="f6c00-150">A WMI Win32_LogonSession osztály végig a felhasználókat társított bejelentkezési munkamenetek kapcsolatos általános információkat kaphat:</span><span class="sxs-lookup"><span data-stu-id="f6c00-150">You can get general information about logon sessions associated with users through the WMI Win32_LogonSession class:</span></span>

```powershell
Get-WmiObject -Class Win32_LogonSession -ComputerName .
```

### <a name="getting-the-user-logged-on-to-a-computer"></a><span data-ttu-id="f6c00-151">A számítógépre bejelentkezett felhasználó beolvasása</span><span class="sxs-lookup"><span data-stu-id="f6c00-151">Getting the User Logged on to a Computer</span></span>

<span data-ttu-id="f6c00-152">A felhasználó jelentkezik be egy adott számítógép rendszer Win32_ComputerSystem használatával jelenítheti meg.</span><span class="sxs-lookup"><span data-stu-id="f6c00-152">You can display the user logged on to a particular computer system using Win32_ComputerSystem.</span></span> <span data-ttu-id="f6c00-153">A parancs csak a rendszer asztali bejelentkezett felhasználó adja vissza:</span><span class="sxs-lookup"><span data-stu-id="f6c00-153">This command returns only the user logged on to the system desktop:</span></span>

```powershell
Get-WmiObject -Class Win32_ComputerSystem -Property UserName -ComputerName .
```

### <a name="getting-local-time-from-a-computer"></a><span data-ttu-id="f6c00-154">Egy számítógép helyi ideje lekérése</span><span class="sxs-lookup"><span data-stu-id="f6c00-154">Getting Local Time from a Computer</span></span>

<span data-ttu-id="f6c00-155">Az aktuális helyi idő az adott számítógépre a WMI Win32_LocalTime osztály használatával kérheti le.</span><span class="sxs-lookup"><span data-stu-id="f6c00-155">You can retrieve the current local time on a specific computer by using the WMI Win32_LocalTime class.</span></span> <span data-ttu-id="f6c00-156">Ez az osztály alapértelmezés szerint minden metaadat jeleníti meg, mert előfordulhat, hogy szűrni kívánt használatával **Select-Object**:</span><span class="sxs-lookup"><span data-stu-id="f6c00-156">Because this class by default displays all metadata, you may want to filter it using **Select-Object**:</span></span>

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

### <a name="displaying-service-status"></a><span data-ttu-id="f6c00-157">Szolgáltatás állapotának megjelenítése</span><span class="sxs-lookup"><span data-stu-id="f6c00-157">Displaying Service Status</span></span>

<span data-ttu-id="f6c00-158">Egy adott számítógép összes szolgáltatás állapotának megtekintéséhez helyileg használhatja a **Get-Service** parancsmag a korábban említett.</span><span class="sxs-lookup"><span data-stu-id="f6c00-158">To view the status of all services on a specific computer, you can locally use the **Get-Service** cmdlet as mentioned earlier.</span></span> <span data-ttu-id="f6c00-159">A távoli rendszerek esetében a WMI Win32_Service osztály is használhatja.</span><span class="sxs-lookup"><span data-stu-id="f6c00-159">For remote systems, you can use the WMI Win32_Service class.</span></span> <span data-ttu-id="f6c00-160">Ha is a **Select-Object** az eredmények szűréséhez **állapot**, **neve**, és **DisplayName**, a kimeneti formátum szinte lesz megegyezik-e a **Get-Service**:</span><span class="sxs-lookup"><span data-stu-id="f6c00-160">If you also use **Select-Object** to filter the results to **Status**, **Name**, and **DisplayName**, the output format will be almost identical to that from **Get-Service**:</span></span>

```powershell
Get-WmiObject -Class Win32_Service -ComputerName . | Select-Object -Property Status,Name,DisplayName
```

<span data-ttu-id="f6c00-161">Ahhoz, hogy a teljes képernyőt az alkalmi szolgáltatások névváltozásai rendkívül hosszú névvel rendelkező, előfordulhat, hogy használni kívánt **Format-Table** rendelkező a **AutoSize** és **burkolása** paraméterek , oszlopszélesség optimalizálása és a hosszú nevek helyett csonkolva lesz csomagolásához engedélyezése:</span><span class="sxs-lookup"><span data-stu-id="f6c00-161">To allow the complete display of names for the occasional services with extremely long names, you may want to use **Format-Table** with the **AutoSize** and **Wrap** parameters, to optimize column width and allow long names to wrap instead of being truncated:</span></span>

```powershell
Get-WmiObject -Class Win32_Service -ComputerName . | Format-Table -Property Status,Name,DisplayName -AutoSize -Wrap
```