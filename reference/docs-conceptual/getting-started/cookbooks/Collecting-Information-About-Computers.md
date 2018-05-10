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
# <a name="collecting-information-about-computers"></a><span data-ttu-id="3ec4e-103">Adatgyűjtés a számítógépekről</span><span class="sxs-lookup"><span data-stu-id="3ec4e-103">Collecting Information About Computers</span></span>

<span data-ttu-id="3ec4e-104">A parancsmagok **CimCmdlets** modul a legfontosabb parancsmagok az általános rendszer-felügyeleti feladatok elvégzésére.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-104">Cmdlets from **CimCmdlets** module are the most important cmdlets for general system management tasks.</span></span>
<span data-ttu-id="3ec4e-105">Minden kritikus alrendszer beállítás WMI-n keresztül érhetők el.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-105">All critical subsystem settings are exposed through WMI.</span></span>
<span data-ttu-id="3ec4e-106">Továbbá WMI adatok, amelyek egy vagy több elem gyűjteményeiben objektumként kezeli.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-106">Furthermore, WMI treats data as objects that are in collections of one or more items.</span></span>
<span data-ttu-id="3ec4e-107">Windows PowerShell is objektumok működik, és van egy folyamatot, amely lehetővé teszi, hogy egy vagy több objektum ugyanúgy kezelheti, mert az általános WMI-hozzáférését lehetővé teszi, nagyon kevés munkát néhány speciális feladatok elvégzéséhez.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-107">Because Windows PowerShell also works with objects and has a pipeline that allows you to treat single or multiple objects in the same way, generic WMI access allows you to perform some advanced tasks with very little work.</span></span>

<span data-ttu-id="3ec4e-108">Az alábbi példák bemutatják, hogyan lehet adott információgyűjtés használatával `Get-CimInstance` egy tetszőleges számítógép ellen.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-108">The following examples demonstrate how to collect specific information by using `Get-CimInstance` against an arbitrary computer.</span></span>
<span data-ttu-id="3ec4e-109">Azt adja meg a **számítógépnév** pont értékű paraméter (**.**), amely jelenti, hogy a helyi számítógépen.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-109">We specify the **ComputerName** parameter with the dot value (**.**), which represents the local computer.</span></span>
<span data-ttu-id="3ec4e-110">Megadhat egy nevet vagy a WMI-n keresztül érhető el a számítógéphez társított IP-címet.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-110">You can specify a name or IP address associated with any computer you can reach through WMI.</span></span>
<span data-ttu-id="3ec4e-111">A helyi számítógép adatainak lekérésére, nincs volt megadva a **számítógépnév** paraméter.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-111">To retrieve information about the local computer, you could omit the **ComputerName** parameter.</span></span>

### <a name="listing-desktop-settings"></a><span data-ttu-id="3ec4e-112">Asztali beállítások listázása</span><span class="sxs-lookup"><span data-stu-id="3ec4e-112">Listing Desktop Settings</span></span>

<span data-ttu-id="3ec4e-113">Egy parancs, amely az asztalok információt gyűjt a helyi számítógépen fogjuk első lépések.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-113">We'll begin with a command that collects information about the desktops on the local computer.</span></span>

```powershell
Get-CimInstance -ClassName Win32_Desktop -ComputerName .
```

<span data-ttu-id="3ec4e-114">Ez információt adhatja vissza az összes asztali számítógép, hogy használatban van-e.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-114">This returns information for all desktops, whether they are in use or not.</span></span>

> [!NOTE]
> <span data-ttu-id="3ec4e-115">Egyes WMI-osztályok által visszaadott adatok nagyon részletes kell, és többek között általában a WMI-osztály metaadatok.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-115">Information returned by some WMI classes can be very detailed, and often include metadata about the WMI class.</span></span>
<span data-ttu-id="3ec4e-116">Mivel a metaadatok tulajdonságok a többsége a karakterlánccal kezdődő **Cim**, szűrheti a Tulajdonságok `Select-Object`.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-116">Because most of these metadata properties have names that begin with **Cim**, you can filter the properties using `Select-Object`.</span></span>
<span data-ttu-id="3ec4e-117">Adja meg a **- ExcludeProperty** paraméter "Cim \*" értékeként.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-117">Specify the **-ExcludeProperty** parameter with "Cim\*" as the value.</span></span>
<span data-ttu-id="3ec4e-118">Például:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-118">For example:</span></span>

```powershell
Get-CimInstance -ClassName Win32_Desktop -ComputerName . | Select-Object -ExcludeProperty "CIM*"
```

<span data-ttu-id="3ec4e-119">A metaadatok kiszűrésére küldhet csővezeték-kezelőt (|) eredményeit a `Get-CimInstance` parancsot `Select-Object -ExcludeProperty "CIM*"`.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-119">To filter out the metadata, use a pipeline operator (|) to send the results of the `Get-CimInstance` command to `Select-Object -ExcludeProperty "CIM*"`.</span></span>

### <a name="listing-bios-information"></a><span data-ttu-id="3ec4e-120">BIOS-információkat listázása</span><span class="sxs-lookup"><span data-stu-id="3ec4e-120">Listing BIOS Information</span></span>

<span data-ttu-id="3ec4e-121">A WMI **Win32_BIOS** osztály a BIOS viszonylag kompakt és teljes információt nyújt a helyi számítógépen:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-121">The WMI **Win32_BIOS** class returns fairly compact and complete information about the system BIOS on the local computer:</span></span>

```powershell
Get-CimInstance -ClassName Win32_BIOS -ComputerName .
```

### <a name="listing-processor-information"></a><span data-ttu-id="3ec4e-122">A processzor adatai listázása</span><span class="sxs-lookup"><span data-stu-id="3ec4e-122">Listing Processor Information</span></span>

<span data-ttu-id="3ec4e-123">Általános adatok WMI segítségével kérheti le **Win32_Processor** osztály, de érdemes a megjelenített információkat szűrheti:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-123">You can retrieve general processor information by using WMI's **Win32_Processor** class, although you will likely want to filter the information:</span></span>

```powershell
Get-CimInstance -ClassName Win32_Processor -ComputerName . | Select-Object -ExcludeProperty "CIM*"
```

<span data-ttu-id="3ec4e-124">Általános leírás karakterlánc processzorcsaládját, most lépjen vissza a **SystemType** tulajdonság:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-124">For a generic description string of the processor family, you can just return the **SystemType** property:</span></span>

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem -ComputerName . | Select-Object -Property SystemType

SystemType
----------
X86-based PC
```

### <a name="listing-computer-manufacturer-and-model"></a><span data-ttu-id="3ec4e-125">Számítógép gyártója és modellje listázása</span><span class="sxs-lookup"><span data-stu-id="3ec4e-125">Listing Computer Manufacturer and Model</span></span>

<span data-ttu-id="3ec4e-126">Számítógép típusra vonatkozó adatokat is rendelkezésre áll, a **Win32_ComputerSystem**.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-126">Computer model information is also available from **Win32_ComputerSystem**.</span></span>
<span data-ttu-id="3ec4e-127">A standard megjelenített kimenete nem lesz szükség a szűrés OEM adatokat:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-127">The standard displayed output will not need any filtering to provide OEM data:</span></span>

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem
```

```output
Name PrimaryOwnerName Domain    TotalPhysicalMemory Model                   Manufacturer
---- ---------------- ------    ------------------- -----                   ------------
MyPC Jane Doe         WORKGROUP 804765696           DA243A-ABA 6415cl NA910 Compaq Presario 06
```

<span data-ttu-id="3ec4e-128">A parancsok, amely vissza az adatokat közvetlenül a hardver, eredménye csak az adatokat, hogy megegyezik.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-128">Your output from commands such as this, which return information directly from some hardware, is only as good as the data you have.</span></span>
<span data-ttu-id="3ec4e-129">Néhány információt által hardvergyártók nincs megfelelően beállítva, és ezért nem érhető el.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-129">Some information is not correctly configured by hardware manufacturers and may therefore be unavailable.</span></span>

### <a name="listing-installed-hotfixes"></a><span data-ttu-id="3ec4e-130">A telepített gyorsjavítások listázása</span><span class="sxs-lookup"><span data-stu-id="3ec4e-130">Listing Installed Hotfixes</span></span>

<span data-ttu-id="3ec4e-131">Minden telepített gyorsjavítások segítségével listázhatja **Win32_QuickFixEngineering**:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-131">You can list all installed hotfixes by using **Win32_QuickFixEngineering**:</span></span>

```powershell
Get-CimInstance -ClassName Win32_QuickFixEngineering -ComputerName .
```

<span data-ttu-id="3ec4e-132">Ez az osztály a gyorsjavítást, amely a következőképpen néz ki listáját adja vissza:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-132">This class returns a list of hotfixes that looks like this:</span></span>

```output
Source Description     HotFixID  InstalledBy   InstalledOn PSComputerName
------ -----------     --------  -----------   ----------- --------------
       Security Update KB4048951 Administrator 12/16/2017  .
```

<span data-ttu-id="3ec4e-133">A kimenet több állapotára előfordulhat, hogy kizárni kívánt néhány tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-133">For more succinct output, you may want to exclude some properties.</span></span>
<span data-ttu-id="3ec4e-134">Bár a `Get-CimInstance`tartozó **tulajdonság** paraméter csak kiválasztása a **HotFixID**, ezzel úgy ténylegesen ad meg további információkat, mert alapértelmezés szerint megjelenik a metaadatok:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-134">Although you can use the `Get-CimInstance`'s **Property** parameter to choose only the **HotFixID**, doing so will actually return more information, because all the metadata is displayed by default:</span></span>

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

<span data-ttu-id="3ec4e-135">A további adat, mert a tulajdonság paraméterének `Get-CimInstance` korlátozza a WMI-osztálypéldány visszakapott tulajdonságok a objektum nem adott vissza a Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-135">The additional data is returned, because the Property parameter in `Get-CimInstance` restricts the properties returned from WMI class instances, not the object returned to Windows PowerShell.</span></span>
<span data-ttu-id="3ec4e-136">A kimeneti csökkentése érdekében használjon `Select-Object`:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-136">To reduce the output, use `Select-Object`:</span></span>

```powershell
Get-CimInstance -ClassName Win32_QuickFixEngineering -ComputerName . -Property HotFixId | Select-Object -Property HotFixId
```

```output
HotFixId
--------
KB4048951
```

### <a name="listing-operating-system-version-information"></a><span data-ttu-id="3ec4e-137">Operációs rendszer verzióinformációja listázása</span><span class="sxs-lookup"><span data-stu-id="3ec4e-137">Listing Operating System Version Information</span></span>

<span data-ttu-id="3ec4e-138">A **Win32_OperatingSystem** osztálytulajdonságokat verziója és a service pack információval.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-138">The **Win32_OperatingSystem** class properties include version and service pack information.</span></span>
<span data-ttu-id="3ec4e-139">Kifejezetten választhatja csak ezeket a tulajdonságokat a fájlverzió-információkat az összefoglaló lekérése **Win32_OperatingSystem**:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-139">You can explicitly select only these properties to get a version information summary from **Win32_OperatingSystem**:</span></span>

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property BuildNumber,BuildType,OSType,ServicePackMajorVersion,ServicePackMinorVersion
```

<span data-ttu-id="3ec4e-140">A helyettesítő karakterek is használhatja a `Select-Object`tartozó **tulajdonság** paraméter.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-140">You can also use wildcards with the `Select-Object`'s **Property** parameter.</span></span>
<span data-ttu-id="3ec4e-141">Mivel vagy kezdve található összes tulajdonság **Build** vagy **szervizcsomag** fontos használandó itt, azt is Rövidítse le ez a következő űrlapon:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-141">Because all the properties beginning with either **Build** or **ServicePack** are important to use here, we can shorten this to the following form:</span></span>

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

### <a name="listing-local-users-and-owner"></a><span data-ttu-id="3ec4e-142">Helyi felhasználók és a tulajdonos listázása</span><span class="sxs-lookup"><span data-stu-id="3ec4e-142">Listing Local Users and Owner</span></span>

<span data-ttu-id="3ec4e-143">Helyi általános információkat – licenccel rendelkező felhasználók száma, a felhasználók és a tulajdonos neve aktuális száma – a kijelölt található **Win32_OperatingSystem**' osztálytulajdonságokat.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-143">Local general user information — number of licensed users, current number of users, and owner name — can be found with a selection of **Win32_OperatingSystem** class' properties.</span></span>
<span data-ttu-id="3ec4e-144">Explicit módon kiválaszthatja a megjelenítendő tulajdonságokat:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-144">You can explicitly select the properties to display like this:</span></span>

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property NumberOfLicensedUsers,NumberOfUsers,RegisteredUser
```

<span data-ttu-id="3ec4e-145">A helyettesítő karakterek használatával több állapotára verziója van:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-145">A more succinct version using wildcards is:</span></span>

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property *user*
```

### <a name="getting-available-disk-space"></a><span data-ttu-id="3ec4e-146">Első rendelkezésre álló szabad lemezterület</span><span class="sxs-lookup"><span data-stu-id="3ec4e-146">Getting Available Disk Space</span></span>

<span data-ttu-id="3ec4e-147">Olvassa el a lemezterület és a szabad terület a helyi meghajtókra, használhatja a Win32_LogicalDisk WMI-osztályt.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-147">To see the disk space and free space for local drives, you can use the Win32_LogicalDisk WMI class.</span></span>
<span data-ttu-id="3ec4e-148">Csak a 3-ból a DriveType rendelkező példányai látni – WMI használ az érték rögzített merevlemez.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-148">You need to see only instances with a DriveType of 3 — the value WMI uses for fixed hard disks.</span></span>

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

### <a name="getting-logon-session-information"></a><span data-ttu-id="3ec4e-149">Bejelentkezési munkamenet adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="3ec4e-149">Getting Logon Session Information</span></span>

<span data-ttu-id="3ec4e-150">Bejelentkezési munkamenetek, felhasználókon társított kapcsolatos általános információkat kaphat a **Win32_LogonSession** WMI-osztály:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-150">You can get general information about logon sessions associated with users through the **Win32_LogonSession** WMI class:</span></span>

```powershell
Get-CimInstance -ClassName Win32_LogonSession -ComputerName .
```

### <a name="getting-the-user-logged-on-to-a-computer"></a><span data-ttu-id="3ec4e-151">A számítógépre bejelentkezett felhasználó beolvasása</span><span class="sxs-lookup"><span data-stu-id="3ec4e-151">Getting the User Logged on to a Computer</span></span>

<span data-ttu-id="3ec4e-152">A felhasználó jelentkezik be egy adott számítógép rendszer Win32_ComputerSystem használatával jelenítheti meg.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-152">You can display the user logged on to a particular computer system using Win32_ComputerSystem.</span></span>
<span data-ttu-id="3ec4e-153">A parancs csak a rendszer asztali bejelentkezett felhasználó adja vissza:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-153">This command returns only the user logged on to the system desktop:</span></span>

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem -Property UserName -ComputerName .
```

### <a name="getting-local-time-from-a-computer"></a><span data-ttu-id="3ec4e-154">Egy számítógép helyi ideje lekérése</span><span class="sxs-lookup"><span data-stu-id="3ec4e-154">Getting Local Time from a Computer</span></span>

<span data-ttu-id="3ec4e-155">Az aktuális helyi idő az adott számítógépre használatával kérheti le a **Win32_LocalTime** WMI-osztályt.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-155">You can retrieve the current local time on a specific computer by using the **Win32_LocalTime** WMI class.</span></span>

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

### <a name="displaying-service-status"></a><span data-ttu-id="3ec4e-156">Szolgáltatás állapotának megjelenítése</span><span class="sxs-lookup"><span data-stu-id="3ec4e-156">Displaying Service Status</span></span>

<span data-ttu-id="3ec4e-157">Egy adott számítógép összes szolgáltatás állapotának megtekintéséhez helyileg használhatja a `Get-Service` parancsmag.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-157">To view the status of all services on a specific computer, you can locally use the `Get-Service` cmdlet.</span></span>
<span data-ttu-id="3ec4e-158">A távoli rendszerek esetében is használhatja a **Win32_Service** WMI-osztályt.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-158">For remote systems, you can use the **Win32_Service** WMI class.</span></span>
<span data-ttu-id="3ec4e-159">Ha is a `Select-Object` az eredmények szűréséhez **állapot**, **neve**, és **DisplayName**, a kimeneti formátum lesz majdnem megegyezik-e, a `Get-Service`:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-159">If you also use `Select-Object` to filter the results to **Status**, **Name**, and **DisplayName**, the output format will be almost identical to that from `Get-Service`:</span></span>

```powershell
Get-CimInstance -ClassName Win32_Service -ComputerName . | Select-Object -Property Status,Name,DisplayName
```

<span data-ttu-id="3ec4e-160">Ahhoz, hogy a teljes képernyőt az alkalmi szolgáltatások névváltozásai rendkívül hosszú névvel rendelkező, előfordulhat, hogy használni kívánt `Format-Table` rendelkező a **AutoSize** és **burkolása** paraméterek oszlopszélesség optimalizálása és hosszú nevek helyett csonkolva lesz csomagolásához engedélyezése:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-160">To allow the complete display of names for the occasional services with extremely long names, you may want to use `Format-Table` with the **AutoSize** and **Wrap** parameters, to optimize column width and allow long names to wrap instead of being truncated:</span></span>

```powershell
Get-CimInstance -ClassName Win32_Service -ComputerName . | Format-Table -Property Status,Name,DisplayName -AutoSize -Wrap
```
