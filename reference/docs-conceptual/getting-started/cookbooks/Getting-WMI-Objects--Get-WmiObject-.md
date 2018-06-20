---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Első WMI-objektumok WmiObject beolvasása
ms.assetid: f0ddfc7d-6b5e-4832-82de-2283597ea70d
ms.openlocfilehash: 279e656b4affd27450be71015a5d6bd21af9f7ad
ms.sourcegitcommit: a9aa5e8d0fab0cbb3e4e6cff0e3ca8c0339ab4e6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/27/2018
ms.locfileid: "32018059"
---
# <a name="getting-wmi-objects-get-wmiobject"></a><span data-ttu-id="8e69d-103">WMI-objektumok (Get-WmiObject) beolvasása</span><span class="sxs-lookup"><span data-stu-id="8e69d-103">Getting WMI Objects (Get-WmiObject)</span></span>

## <a name="getting-wmi-objects-get-wmiobject"></a><span data-ttu-id="8e69d-104">WMI-objektumok (Get-WmiObject) beolvasása</span><span class="sxs-lookup"><span data-stu-id="8e69d-104">Getting WMI Objects (Get-WmiObject)</span></span>

<span data-ttu-id="8e69d-105">A Windows Management Instrumentation (WMI) egy alapvető technológiák a Windows rendszer-felügyeleti oka egységes módon adatok széles skáláját teszi elérhetővé.</span><span class="sxs-lookup"><span data-stu-id="8e69d-105">Windows Management Instrumentation (WMI) is a core technology for Windows system administration because it exposes a wide range of information in a uniform manner.</span></span> <span data-ttu-id="8e69d-106">Mennyi lehetővé teszi a WMI lehetséges, a Windows PowerShell-parancsmag WMI-objektumok eléréséhez miatt **Get-WmiObject**, a leghasznosabb egyike a valódi munkát.</span><span class="sxs-lookup"><span data-stu-id="8e69d-106">Because of how much WMI makes possible, the Windows PowerShell cmdlet for accessing WMI objects, **Get-WmiObject**, is one of the most useful for doing real work.</span></span> <span data-ttu-id="8e69d-107">Fogjuk megvitatni a Get-WmiObject használata a WMI-objektumok eléréséhez és WMI-objektumok használata elvégzésére.</span><span class="sxs-lookup"><span data-stu-id="8e69d-107">We are going to discuss how to use Get-WmiObject to access WMI objects and then how to use WMI objects to do specific things.</span></span>

### <a name="listing-wmi-classes"></a><span data-ttu-id="8e69d-108">WMI-osztályok listázása</span><span class="sxs-lookup"><span data-stu-id="8e69d-108">Listing WMI Classes</span></span>

<span data-ttu-id="8e69d-109">A legtöbb WMI felhasználóknál első problémát próbál megtudhatja, mi teheti a WMI-ben.</span><span class="sxs-lookup"><span data-stu-id="8e69d-109">The first problem most WMI users encounter is trying to find out what can be done with WMI.</span></span> <span data-ttu-id="8e69d-110">WMI-osztályokat, amelyek kezelhetők erőforrásokat leíró.</span><span class="sxs-lookup"><span data-stu-id="8e69d-110">WMI classes describe the resources that can be managed.</span></span> <span data-ttu-id="8e69d-111">WMI-osztályokat, tulajdonságok több tucatnyi tartalmaz, amelyek több száz van.</span><span class="sxs-lookup"><span data-stu-id="8e69d-111">There are hundreds of WMI classes, some of which contain dozens of properties.</span></span>

<span data-ttu-id="8e69d-112">**Get-WmiObject** kezeli ezt a problémát azáltal, hogy a WMI felderíthető.</span><span class="sxs-lookup"><span data-stu-id="8e69d-112">**Get-WmiObject** addresses this problem by making WMI discoverable.</span></span> <span data-ttu-id="8e69d-113">A rendelkezésre álló WMI-osztályok listáját kaphat a helyi számítógépen írja be:</span><span class="sxs-lookup"><span data-stu-id="8e69d-113">You can get a list of the WMI classes available on the local computer by typing:</span></span>

```
PS> Get-WmiObject -List

__SecurityRelatedClass                  __NTLMUser9X
__PARAMETERS                            __SystemSecurity
__NotifyStatus                          __ExtendedStatus
Win32_PrivilegesStatus                  Win32_TSNetworkAdapterSettingError
Win32_TSRemoteControlSettingError       Win32_TSEnvironmentSettingError
...
```

<span data-ttu-id="8e69d-114">Kérheti le ugyanazokat az információkat egy távoli számítógépről a ComputerName paraméterrel a számítógép nevét vagy IP-cím megadása:</span><span class="sxs-lookup"><span data-stu-id="8e69d-114">You can retrieve the same information from a remote computer by using the ComputerName parameter, specifying a computer name or IP address:</span></span>

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
__ProviderRegistration                  __ObjectProviderRegistration
...
```

<span data-ttu-id="8e69d-115">A távoli számítógépek által visszaadott osztály listát az adott operációs rendszerrel, a számítógép fut, és a telepített alkalmazások által hozzáadott adott WMI-bővítmények miatt eltérhetnek.</span><span class="sxs-lookup"><span data-stu-id="8e69d-115">The class listing returned by remote computers may vary due to the specific operating system the computer is running and the particular WMI extensions added by installed applications.</span></span>

> [!NOTE]
> <span data-ttu-id="8e69d-116">Get-WmiObject használata a távoli számítógéphez csatlakozni, a távoli számítógépen futnia kell az WMI, és az alapértelmezett konfiguráció használt fiók a helyi Rendszergazdák csoport, a távoli számítógépen kell lennie.</span><span class="sxs-lookup"><span data-stu-id="8e69d-116">When using Get-WmiObject to connect to a remote computer, the remote computer must be running WMI and, under the default configuration, the account you are using must be in the local administrators group on the remote computer.</span></span> <span data-ttu-id="8e69d-117">A távoli rendszer nem kell a Windows PowerShell telepítve van.</span><span class="sxs-lookup"><span data-stu-id="8e69d-117">The remote system does not need to have Windows PowerShell installed.</span></span> <span data-ttu-id="8e69d-118">Ez lehetővé teszi, hogy nem futnak Windows PowerShell, amelyek WMI rendelkezésre álló operációs rendszerek felügyeletét.</span><span class="sxs-lookup"><span data-stu-id="8e69d-118">This allows you to administer operating systems that are not running Windows PowerShell, but do have WMI available.</span></span>

<span data-ttu-id="8e69d-119">A számítógépnév is tartalmazhatnak, amikor csatlakozik a helyi rendszer.</span><span class="sxs-lookup"><span data-stu-id="8e69d-119">You can even include the ComputerName when connecting to the local system.</span></span> <span data-ttu-id="8e69d-120">Használhatja a helyi számítógép neve, az IP-címét (vagy a visszacsatolási cím 127.0.0.1), vagy a WMI-style "." karaktert a számítógép neveként.</span><span class="sxs-lookup"><span data-stu-id="8e69d-120">You can use the local computer's name, its IP address (or the loopback address 127.0.0.1), or the WMI-style '.' as the computer name.</span></span> <span data-ttu-id="8e69d-121">Ha futtatja a Windows PowerShell IP-cím 192.168.1.90 Rgazda01 nevű számítógépen, a következő parancsokat minden visszatér a WMI-osztály listázása az adott számítógépen:</span><span class="sxs-lookup"><span data-stu-id="8e69d-121">If you are running Windows PowerShell on a computer named Admin01 with IP address 192.168.1.90, the following commands will all return the WMI class listing for that computer:</span></span>

```powershell
Get-WmiObject -List
Get-WmiObject -List -ComputerName .
Get-WmiObject -List -ComputerName Admin01
Get-WmiObject -List -ComputerName 192.168.1.90
Get-WmiObject -List -ComputerName 127.0.0.1
Get-WmiObject -List -ComputerName localhost
```

<span data-ttu-id="8e69d-122">Get-WmiObject alapértelmezés szerint a legfelső szintű/cimv2 névteret használja.</span><span class="sxs-lookup"><span data-stu-id="8e69d-122">Get-WmiObject uses the root/cimv2 namespace by default.</span></span> <span data-ttu-id="8e69d-123">Ha szeretne megadni egy másik WMI-névteret, használja a **Namespace** paraméter, és adja meg a megfelelő névtér elérési útja:</span><span class="sxs-lookup"><span data-stu-id="8e69d-123">If you want to specify another WMI namespace, use the **Namespace** parameter and specify the corresponding namespace path:</span></span>

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29 -Namespace root

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
...
```

### <a name="displaying-wmi-class-details"></a><span data-ttu-id="8e69d-124">WMI-osztály részletek megjelenítése</span><span class="sxs-lookup"><span data-stu-id="8e69d-124">Displaying WMI Class Details</span></span>

<span data-ttu-id="8e69d-125">Ha már ismeri a nevét, a WMI-osztályok, azonnal lekérése használhatja.</span><span class="sxs-lookup"><span data-stu-id="8e69d-125">If you already know the name of a WMI class, you can use it to get information immediately.</span></span> <span data-ttu-id="8e69d-126">Például a WMI-osztályokat, gyakran használják a számítógép adatainak lekérése egyik **Win32_OperatingSystem**.</span><span class="sxs-lookup"><span data-stu-id="8e69d-126">For example, one of the WMI classes commonly used for retrieving information about a computer is **Win32_OperatingSystem**.</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName .

SystemDirectory : C:\WINDOWS\system32
Organization    : Global Network Solutions
BuildNumber     : 2600
RegisteredUser  : Oliver W. Jones
SerialNumber    : 12345-678-9012345-67890
Version         : 5.1.2600
```

<span data-ttu-id="8e69d-127">Bár azt összes paraméterének láthatók, a parancs több állapotára úgy lehet megadni.</span><span class="sxs-lookup"><span data-stu-id="8e69d-127">Although we are showing all of the parameters, the command can be expressed in a more succinct way.</span></span> <span data-ttu-id="8e69d-128">A **számítógépnév** paraméter nem szükséges a helyi rendszer történő csatlakozás során.</span><span class="sxs-lookup"><span data-stu-id="8e69d-128">The **ComputerName** parameter is not necessary when connecting to the local system.</span></span> <span data-ttu-id="8e69d-129">A legtöbb általános esetben bemutatása és jelezve, az paraméterrel kapcsolatos megmutatjuk.</span><span class="sxs-lookup"><span data-stu-id="8e69d-129">We show it to demonstrate the most general case and remind you about the parameter.</span></span> <span data-ttu-id="8e69d-130">A **Namespace** legfelső szintű/cimv2 az alapértelmezett, és is kihagyható.</span><span class="sxs-lookup"><span data-stu-id="8e69d-130">The **Namespace** defaults to root/cimv2, and can be omitted as well.</span></span> <span data-ttu-id="8e69d-131">Végezetül legtöbb parancsmagok lehetővé teszik az általános paraméterek neve nincs megadva.</span><span class="sxs-lookup"><span data-stu-id="8e69d-131">Finally, most cmdlets allow you to omit the name of common parameters.</span></span> <span data-ttu-id="8e69d-132">A Get-WmiObject, ha nem adott meg az első paraméter, a Windows PowerShell úgy kezeli, mint a **osztály** paraméter.</span><span class="sxs-lookup"><span data-stu-id="8e69d-132">With Get-WmiObject, if no name is specified for the first parameter, Windows PowerShell treats it as the **Class** parameter.</span></span> <span data-ttu-id="8e69d-133">Ez azt jelenti, hogy az utolsó parancs beírásával kiadott sikerült:</span><span class="sxs-lookup"><span data-stu-id="8e69d-133">This means the last command could have been issued by typing:</span></span>

```powershell
Get-WmiObject Win32_OperatingSystem
```

<span data-ttu-id="8e69d-134">A **Win32_OperatingSystem** osztály tulajdonságai sok több mint itt jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="8e69d-134">The **Win32_OperatingSystem** class has many more properties than those displayed here.</span></span> <span data-ttu-id="8e69d-135">Get-tag használhatja a tulajdonságok megtekintéséhez.</span><span class="sxs-lookup"><span data-stu-id="8e69d-135">You can use Get-Member to see all the properties.</span></span> <span data-ttu-id="8e69d-136">A tulajdonságok a WMI-osztályok automatikusan elérhetők például más objektum tulajdonságai:</span><span class="sxs-lookup"><span data-stu-id="8e69d-136">The properties of a WMI class are automatically available like other object properties:</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Get-Member -MemberType Property

   TypeName: System.Management.ManagementObject#root\cimv2\Win32_OperatingSyste
m

Name                                      MemberType Definition
----                                      ---------- ----------
__CLASS                                   Property   System.String __CLASS {...
...
BootDevice                                Property   System.String BootDevic...
BuildNumber                               Property   System.String BuildNumb...
...
```

#### <a name="displaying-non-default-properties-with-format-cmdlets"></a><span data-ttu-id="8e69d-137">A formátum-parancsmagokkal nem alapértelmezett tulajdonságok megjelenítése</span><span class="sxs-lookup"><span data-stu-id="8e69d-137">Displaying Non-Default Properties with Format Cmdlets</span></span>

<span data-ttu-id="8e69d-138">Ha azt szeretné, hogy a tárolt információ a **Win32_OperatingSystem** osztály, amely alapértelmezés szerint nem jelenik meg, meg lehet jeleníteni használatával a **formátum** parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="8e69d-138">If you want information contained in the **Win32_OperatingSystem** class that is not displayed by default, you can display it by using the **Format** cmdlets.</span></span> <span data-ttu-id="8e69d-139">Ha meg szeretné jeleníteni a rendelkezésre álló memória adatok, például:</span><span class="sxs-lookup"><span data-stu-id="8e69d-139">For example, if you want to display available memory data, type:</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-Table -Property TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize TotalVisibleMemory FreePhysicalMemory FreeVirtualMemory FreeSpaceInPagingFiles
---------------------- ---------------    ------------------ -==--------------------- ---------------
               2097024          785904                305808           2056724                1558232
```

> [!NOTE]
> <span data-ttu-id="8e69d-140">Helyettesítő karakterek használata a tulajdonságnevek **Format-Table**, így csökkenthető a végső csővezeték elem `Format-Table -Property Total,Free`</span><span class="sxs-lookup"><span data-stu-id="8e69d-140">Wildcards work with property names in **Format-Table**, so the final pipeline element can be reduced to `Format-Table -Property Total,Free`</span></span>

<span data-ttu-id="8e69d-141">Lehet, hogy a memória adatok olvashatóbb, ha azt listaként beírásával:</span><span class="sxs-lookup"><span data-stu-id="8e69d-141">The memory data might be more readable if you format it as a list by typing:</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-List TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize : 2097024
TotalVisibleMemorySize : 785904
FreePhysicalMemory     : 301876
FreeVirtualMemory      : 2056724
FreeSpaceInPagingFiles : 1556644
```
