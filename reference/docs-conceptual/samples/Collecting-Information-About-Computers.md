---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Adatgyűjtés a számítógépekről
ms.assetid: 9e7b6a2d-34f7-4731-a92c-8b3382eb51bb
ms.openlocfilehash: d837684108656e17ebf26189bd4841c5de01051c
ms.sourcegitcommit: 806cf87488b80800b9f50a8af286e8379519a034
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59293163"
---
# <a name="collecting-information-about-computers"></a><span data-ttu-id="cbc51-103">Adatgyűjtés a számítógépekről</span><span class="sxs-lookup"><span data-stu-id="cbc51-103">Collecting Information About Computers</span></span>

<span data-ttu-id="cbc51-104">A parancsmagok **CimCmdlets** modul a legfontosabb parancsmagok általános felügyeleti feladatokhoz.</span><span class="sxs-lookup"><span data-stu-id="cbc51-104">Cmdlets from **CimCmdlets** module are the most important cmdlets for general system management tasks.</span></span>
<span data-ttu-id="cbc51-105">Az összes kritikus fontosságú alrendszert beállítások WMI-n keresztül érhetők el.</span><span class="sxs-lookup"><span data-stu-id="cbc51-105">All critical subsystem settings are exposed through WMI.</span></span>
<span data-ttu-id="cbc51-106">Ezenkívül WMI adatok, amelyek a gyűjtemények egy vagy több elem objektumként kezeli.</span><span class="sxs-lookup"><span data-stu-id="cbc51-106">Furthermore, WMI treats data as objects that are in collections of one or more items.</span></span>
<span data-ttu-id="cbc51-107">Windows PowerShell is működik együtt az objektumok és a egy folyamatot, amely lehetővé teszi, hogy ugyanolyan módon való kezelése egyetlen vagy több objektum van, mert általános WMI hozzáférés lehetővé teszi a nagyon kevés munkát speciális feladatok elvégzésére.</span><span class="sxs-lookup"><span data-stu-id="cbc51-107">Because Windows PowerShell also works with objects and has a pipeline that allows you to treat single or multiple objects in the same way, generic WMI access allows you to perform some advanced tasks with very little work.</span></span>

<span data-ttu-id="cbc51-108">Az alábbi példák bemutatják, hogyan lehet adott információk gyűjtése használatával `Get-CimInstance` egy tetszőleges számítógép ellen.</span><span class="sxs-lookup"><span data-stu-id="cbc51-108">The following examples demonstrate how to collect specific information by using `Get-CimInstance` against an arbitrary computer.</span></span>
<span data-ttu-id="cbc51-109">Adja meg, hogy a **ComputerName** pont értékű paraméter (**.**), amely jelöli, hogy a helyi számítógépen.</span><span class="sxs-lookup"><span data-stu-id="cbc51-109">We specify the **ComputerName** parameter with the dot value (**.**), which represents the local computer.</span></span>
<span data-ttu-id="cbc51-110">Megadhat egy nevet vagy a WMI-n keresztül érhető el minden olyan számítógéphez társított IP-cím.</span><span class="sxs-lookup"><span data-stu-id="cbc51-110">You can specify a name or IP address associated with any computer you can reach through WMI.</span></span>
<span data-ttu-id="cbc51-111">A helyi számítógép adatainak beolvasásához, sikerült kihagyja a **ComputerName** paraméter.</span><span class="sxs-lookup"><span data-stu-id="cbc51-111">To retrieve information about the local computer, you could omit the **ComputerName** parameter.</span></span>

## <a name="listing-desktop-settings"></a><span data-ttu-id="cbc51-112">Asztali beállítások listázása</span><span class="sxs-lookup"><span data-stu-id="cbc51-112">Listing Desktop Settings</span></span>

<span data-ttu-id="cbc51-113">Tudjuk, hogy az asztali adatokat gyűjt a helyi számítógépen paranccsal megkezdheti.</span><span class="sxs-lookup"><span data-stu-id="cbc51-113">We'll begin with a command that collects information about the desktops on the local computer.</span></span>

```powershell
Get-CimInstance -ClassName Win32_Desktop -ComputerName .
```

<span data-ttu-id="cbc51-114">Az összes asztali számítógép, információkat ezt adja vissza, akár használatban van-e.</span><span class="sxs-lookup"><span data-stu-id="cbc51-114">This returns information for all desktops, whether they are in use or not.</span></span>

> [!NOTE]
> <span data-ttu-id="cbc51-115">Bizonyos WMI-osztályok által visszaadott információk nagyon részletes lehetnek, és többek között általában a metaadatokat, a WMI-osztály.</span><span class="sxs-lookup"><span data-stu-id="cbc51-115">Information returned by some WMI classes can be very detailed, and often include metadata about the WMI class.</span></span>
<span data-ttu-id="cbc51-116">Mivel a metaadat-tulajdonságot a legtöbb kezdődő nevű **Cim**, szűrheti a tulajdonságok használatával `Select-Object`.</span><span class="sxs-lookup"><span data-stu-id="cbc51-116">Because most of these metadata properties have names that begin with **Cim**, you can filter the properties using `Select-Object`.</span></span>
<span data-ttu-id="cbc51-117">Adja meg a **- ExcludeProperty** paraméter "Cim \*" értéket.</span><span class="sxs-lookup"><span data-stu-id="cbc51-117">Specify the **-ExcludeProperty** parameter with "Cim\*" as the value.</span></span>
<span data-ttu-id="cbc51-118">Például:</span><span class="sxs-lookup"><span data-stu-id="cbc51-118">For example:</span></span>

```powershell
Get-CimInstance -ClassName Win32_Desktop -ComputerName . | Select-Object -ExcludeProperty "CIM*"
```

<span data-ttu-id="cbc51-119">Szűrje ki a metaadatokat, a csővezeték-kezelőt (|) használatával küldjön eredményeit a `Get-CimInstance` parancsot a `Select-Object -ExcludeProperty "CIM*"`.</span><span class="sxs-lookup"><span data-stu-id="cbc51-119">To filter out the metadata, use a pipeline operator (|) to send the results of the `Get-CimInstance` command to `Select-Object -ExcludeProperty "CIM*"`.</span></span>

## <a name="listing-bios-information"></a><span data-ttu-id="cbc51-120">BIOS adatainak listázása</span><span class="sxs-lookup"><span data-stu-id="cbc51-120">Listing BIOS Information</span></span>

<span data-ttu-id="cbc51-121">A WMI **Win32_BIOS** osztály adja vissza a rendszer BIOS viszonylag kompakt és teljes körű információkat a helyi számítógépen:</span><span class="sxs-lookup"><span data-stu-id="cbc51-121">The WMI **Win32_BIOS** class returns fairly compact and complete information about the system BIOS on the local computer:</span></span>

```powershell
Get-CimInstance -ClassName Win32_BIOS -ComputerName .
```

## <a name="listing-processor-information"></a><span data-ttu-id="cbc51-122">A processzor adatai listázása</span><span class="sxs-lookup"><span data-stu-id="cbc51-122">Listing Processor Information</span></span>

<span data-ttu-id="cbc51-123">A WMI használatával kérheti le általános processzoradatokat **Win32_Processor** osztályhoz, noha valószínűleg érdemes szűri az információkat:</span><span class="sxs-lookup"><span data-stu-id="cbc51-123">You can retrieve general processor information by using WMI's **Win32_Processor** class, although you will likely want to filter the information:</span></span>

```powershell
Get-CimInstance -ClassName Win32_Processor -ComputerName . | Select-Object -ExcludeProperty "CIM*"
```

<span data-ttu-id="cbc51-124">A processzorcsaládját. általános leírása karakterlánc, akkor csak visszatérhet a **SystemType** tulajdonság:</span><span class="sxs-lookup"><span data-stu-id="cbc51-124">For a generic description string of the processor family, you can just return the **SystemType** property:</span></span>

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem -ComputerName . | Select-Object -Property SystemType

SystemType
----------
X86-based PC
```

## <a name="listing-computer-manufacturer-and-model"></a><span data-ttu-id="cbc51-125">Számítógép gyártója és modellje listázása</span><span class="sxs-lookup"><span data-stu-id="cbc51-125">Listing Computer Manufacturer and Model</span></span>

<span data-ttu-id="cbc51-126">Számítógépadatok modell érhető el is **Win32_ComputerSystem**.</span><span class="sxs-lookup"><span data-stu-id="cbc51-126">Computer model information is also available from **Win32_ComputerSystem**.</span></span>
<span data-ttu-id="cbc51-127">A megjelenített normál a kimenetbe nem kell a megadott szűréseket OEM-adatok:</span><span class="sxs-lookup"><span data-stu-id="cbc51-127">The standard displayed output will not need any filtering to provide OEM data:</span></span>

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem
```

```output
Name PrimaryOwnerName Domain    TotalPhysicalMemory Model                   Manufacturer
---- ---------------- ------    ------------------- -----                   ------------
MyPC Jane Doe         WORKGROUP 804765696           DA243A-ABA 6415cl NA910 Compaq Presario 06
```

<span data-ttu-id="cbc51-128">Csak akkor megegyezik az adatokat, hogy a parancsok, amely információkat ad vissza közvetlenül az egyes hardverekről, a kimenete.</span><span class="sxs-lookup"><span data-stu-id="cbc51-128">Your output from commands such as this, which return information directly from some hardware, is only as good as the data you have.</span></span>
<span data-ttu-id="cbc51-129">Bizonyos adatok nem megfelelően van konfigurálva a hardvergyártók által, és ezért nem érhető el.</span><span class="sxs-lookup"><span data-stu-id="cbc51-129">Some information is not correctly configured by hardware manufacturers and may therefore be unavailable.</span></span>

## <a name="listing-installed-hotfixes"></a><span data-ttu-id="cbc51-130">A telepített gyorsjavítások listázása</span><span class="sxs-lookup"><span data-stu-id="cbc51-130">Listing Installed Hotfixes</span></span>

<span data-ttu-id="cbc51-131">Használatával listázhatja az összes telepített gyorsjavítások **Win32_QuickFixEngineering**:</span><span class="sxs-lookup"><span data-stu-id="cbc51-131">You can list all installed hotfixes by using **Win32_QuickFixEngineering**:</span></span>

```powershell
Get-CimInstance -ClassName Win32_QuickFixEngineering -ComputerName .
```

<span data-ttu-id="cbc51-132">Ez az osztály a következőhöz hasonló gyorsjavítások listáját adja vissza:</span><span class="sxs-lookup"><span data-stu-id="cbc51-132">This class returns a list of hotfixes that looks like this:</span></span>

```output
Source Description     HotFixID  InstalledBy   InstalledOn PSComputerName
------ -----------     --------  -----------   ----------- --------------
       Security Update KB4048951 Administrator 12/16/2017  .
```

<span data-ttu-id="cbc51-133">Több állapotára kimeneti érdemes kizárni néhány tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="cbc51-133">For more succinct output, you may want to exclude some properties.</span></span>
<span data-ttu-id="cbc51-134">Bár használhatja a `Get-CimInstance`a **tulajdonság** paramétert csak válassza a **HotFixID**, ezzel úgy fognak visszaküldeni további információkért, mert az összes metaadat alapértelmezés szerint megjelenik:</span><span class="sxs-lookup"><span data-stu-id="cbc51-134">Although you can use the `Get-CimInstance`'s **Property** parameter to choose only the **HotFixID**, doing so will actually return more information, because all the metadata is displayed by default:</span></span>

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

<span data-ttu-id="cbc51-135">A további adatokat ad vissza, mert a tulajdonság paramétert `Get-CimInstance` korlátozza a kapott a WMI-osztálypéldány tulajdonságainak az objektum nem adott vissza a Windows powershellt.</span><span class="sxs-lookup"><span data-stu-id="cbc51-135">The additional data is returned, because the Property parameter in `Get-CimInstance` restricts the properties returned from WMI class instances, not the object returned to Windows PowerShell.</span></span>
<span data-ttu-id="cbc51-136">A kimenet csökkentése érdekében használja `Select-Object`:</span><span class="sxs-lookup"><span data-stu-id="cbc51-136">To reduce the output, use `Select-Object`:</span></span>

```powershell
Get-CimInstance -ClassName Win32_QuickFixEngineering -ComputerName . -Property HotFixId | Select-Object -Property HotFixId
```

```output
HotFixId
--------
KB4048951
```

## <a name="listing-operating-system-version-information"></a><span data-ttu-id="cbc51-137">Operációsrendszer-Verziószámukat listázása</span><span class="sxs-lookup"><span data-stu-id="cbc51-137">Listing Operating System Version Information</span></span>

<span data-ttu-id="cbc51-138">A **Win32_OperatingSystem** osztálytulajdonságokat verziója és a service pack információval.</span><span class="sxs-lookup"><span data-stu-id="cbc51-138">The **Win32_OperatingSystem** class properties include version and service pack information.</span></span>
<span data-ttu-id="cbc51-139">Explicit módon kiválaszthatja a fájlverzió-információkat a összefoglalójának lekérése a tulajdonságok csak **Win32_OperatingSystem**:</span><span class="sxs-lookup"><span data-stu-id="cbc51-139">You can explicitly select only these properties to get a version information summary from **Win32_OperatingSystem**:</span></span>

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property BuildNumber,BuildType,OSType,ServicePackMajorVersion,ServicePackMinorVersion
```

<span data-ttu-id="cbc51-140">A helyettesítő karaktereket is használhatja a `Select-Object`a **tulajdonság** paraméter.</span><span class="sxs-lookup"><span data-stu-id="cbc51-140">You can also use wildcards with the `Select-Object`'s **Property** parameter.</span></span>
<span data-ttu-id="cbc51-141">Mivel verziótól kezdve, vagy az összes tulajdonság **hozhat létre** vagy **szervizcsomag** fontos használja itt, hogy lerövidítheti Ez a következő formában:</span><span class="sxs-lookup"><span data-stu-id="cbc51-141">Because all the properties beginning with either **Build** or **ServicePack** are important to use here, we can shorten this to the following form:</span></span>

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

## <a name="listing-local-users-and-owner"></a><span data-ttu-id="cbc51-142">A helyi felhasználók és a tulajdonos listázása</span><span class="sxs-lookup"><span data-stu-id="cbc51-142">Listing Local Users and Owner</span></span>

<span data-ttu-id="cbc51-143">Helyi általános információkat – licenccel rendelkező felhasználók száma, a felhasználók és a tulajdonos neve aktuális száma – között található egy kijelölt **Win32_OperatingSystem**' osztálytulajdonságokat.</span><span class="sxs-lookup"><span data-stu-id="cbc51-143">Local general user information — number of licensed users, current number of users, and owner name — can be found with a selection of **Win32_OperatingSystem** class' properties.</span></span>
<span data-ttu-id="cbc51-144">Explicit módon kiválaszthatja a tulajdonságok alapján a következőképpen jelenik meg:</span><span class="sxs-lookup"><span data-stu-id="cbc51-144">You can explicitly select the properties to display like this:</span></span>

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property NumberOfLicensedUsers,NumberOfUsers,RegisteredUser
```

<span data-ttu-id="cbc51-145">A helyettesítő karakterek használatával több állapotára verziója van:</span><span class="sxs-lookup"><span data-stu-id="cbc51-145">A more succinct version using wildcards is:</span></span>

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property *user*
```

## <a name="getting-available-disk-space"></a><span data-ttu-id="cbc51-146">Bevezetés a szabad lemezterület</span><span class="sxs-lookup"><span data-stu-id="cbc51-146">Getting Available Disk Space</span></span>

<span data-ttu-id="cbc51-147">Tekintse meg a lemezterület és a szabad terület a helyi meghajtókra, használhatja a Win32_LogicalDisk WMI-osztályt.</span><span class="sxs-lookup"><span data-stu-id="cbc51-147">To see the disk space and free space for local drives, you can use the Win32_LogicalDisk WMI class.</span></span>
<span data-ttu-id="cbc51-148">Meg kell tekintenie csak 3 és a egy DriveType példányok – WMI használja az érték rögzített merevlemez.</span><span class="sxs-lookup"><span data-stu-id="cbc51-148">You need to see only instances with a DriveType of 3 — the value WMI uses for fixed hard disks.</span></span>

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

## <a name="getting-logon-session-information"></a><span data-ttu-id="cbc51-149">Bejelentkezési munkamenet-információk lekérése</span><span class="sxs-lookup"><span data-stu-id="cbc51-149">Getting Logon Session Information</span></span>

<span data-ttu-id="cbc51-150">Társított keresztül a felhasználó bejelentkezési munkamenetek kapcsolatos általános információkat szerezhet a **Win32_LogonSession** WMI-osztály:</span><span class="sxs-lookup"><span data-stu-id="cbc51-150">You can get general information about logon sessions associated with users through the **Win32_LogonSession** WMI class:</span></span>

```powershell
Get-CimInstance -ClassName Win32_LogonSession -ComputerName .
```

## <a name="getting-the-user-logged-on-to-a-computer"></a><span data-ttu-id="cbc51-151">Bevezetés a számítógépre bejelentkezett felhasználó</span><span class="sxs-lookup"><span data-stu-id="cbc51-151">Getting the User Logged on to a Computer</span></span>

<span data-ttu-id="cbc51-152">A felhasználó jelentkezett be egy adott számítógép rendszer Win32_ComputerSystem használatával jeleníthet meg.</span><span class="sxs-lookup"><span data-stu-id="cbc51-152">You can display the user logged on to a particular computer system using Win32_ComputerSystem.</span></span>
<span data-ttu-id="cbc51-153">Ez a parancs csak a felhasználó bejelentkezett a rendszert asztal adja vissza:</span><span class="sxs-lookup"><span data-stu-id="cbc51-153">This command returns only the user logged on to the system desktop:</span></span>

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem -Property UserName -ComputerName .
```

## <a name="getting-local-time-from-a-computer"></a><span data-ttu-id="cbc51-154">Egy számítógép helyi ideje beolvasása</span><span class="sxs-lookup"><span data-stu-id="cbc51-154">Getting Local Time from a Computer</span></span>

<span data-ttu-id="cbc51-155">Egy adott számítógépen az aktuális helyi idő használatával lekérheti a **Win32_LocalTime** WMI-osztály.</span><span class="sxs-lookup"><span data-stu-id="cbc51-155">You can retrieve the current local time on a specific computer by using the **Win32_LocalTime** WMI class.</span></span>

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

## <a name="displaying-service-status"></a><span data-ttu-id="cbc51-156">Szolgáltatás állapotának megjelenítése</span><span class="sxs-lookup"><span data-stu-id="cbc51-156">Displaying Service Status</span></span>

<span data-ttu-id="cbc51-157">Az összes szolgáltatás állapotának megjelenítése egy adott számítógépen, helyben használhatja a `Get-Service` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="cbc51-157">To view the status of all services on a specific computer, you can locally use the `Get-Service` cmdlet.</span></span>
<span data-ttu-id="cbc51-158">Távoli rendszerek esetén használhatja a **Win32_Service** WMI-osztály.</span><span class="sxs-lookup"><span data-stu-id="cbc51-158">For remote systems, you can use the **Win32_Service** WMI class.</span></span>
<span data-ttu-id="cbc51-159">Ha is használja `Select-Object` , az eredmények szűréséhez **állapot**, **neve**, és **DisplayName**, kimeneti formátum a csaknem megegyezik-e a lesz`Get-Service`:</span><span class="sxs-lookup"><span data-stu-id="cbc51-159">If you also use `Select-Object` to filter the results to **Status**, **Name**, and **DisplayName**, the output format will be almost identical to that from `Get-Service`:</span></span>

```powershell
Get-CimInstance -ClassName Win32_Service -ComputerName . | Select-Object -Property Status,Name,DisplayName
```

<span data-ttu-id="cbc51-160">Ahhoz, hogy a teljes nevek a alkalmanként szolgáltatások rendkívül hosszú névvel rendelkező megjelenítését, előfordulhat, hogy használni kívánt `Format-Table` az a **AutoSize** és **burkolása** paraméterek oszlopszélesség optimalizálása és a hosszú nevek helyett a rendszer csonkolja burkolása engedélyezése:</span><span class="sxs-lookup"><span data-stu-id="cbc51-160">To allow the complete display of names for the occasional services with extremely long names, you may want to use `Format-Table` with the **AutoSize** and **Wrap** parameters, to optimize column width and allow long names to wrap instead of being truncated:</span></span>

```powershell
Get-CimInstance -ClassName Win32_Service -ComputerName . | Format-Table -Property Status,Name,DisplayName -AutoSize -Wrap
```
