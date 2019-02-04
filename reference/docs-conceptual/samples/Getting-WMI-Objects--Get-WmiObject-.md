---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: WMI-objektumok lékérése Get-WmiObject
ms.assetid: f0ddfc7d-6b5e-4832-82de-2283597ea70d
ms.openlocfilehash: 522822ac3ea6f08b20fa5af6c9accb48b01035d3
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688461"
---
# <a name="getting-wmi-objects-get-wmiobject"></a><span data-ttu-id="86488-103">WMI-objektumok lékérése (Get-WmiObject)</span><span class="sxs-lookup"><span data-stu-id="86488-103">Getting WMI Objects (Get-WmiObject)</span></span>

## <a name="getting-wmi-objects-get-wmiobject"></a><span data-ttu-id="86488-104">WMI-objektumok lékérése (Get-WmiObject)</span><span class="sxs-lookup"><span data-stu-id="86488-104">Getting WMI Objects (Get-WmiObject)</span></span>

<span data-ttu-id="86488-105">Windows Management Instrumentation (WMI) egy alapvető technológia a Windows Rendszerfelügyeleti azért számos különféle információkat egységes módon teszi elérhetővé.</span><span class="sxs-lookup"><span data-stu-id="86488-105">Windows Management Instrumentation (WMI) is a core technology for Windows system administration because it exposes a wide range of information in a uniform manner.</span></span> <span data-ttu-id="86488-106">IP-címek fenntartási lehetővé teszi a WMI lehetséges, a Windows PowerShell-parancsmaggal WMI-objektumok elérése miatt **Get-WmiObject**, a leghasznosabb egyike a valódi munkát végző.</span><span class="sxs-lookup"><span data-stu-id="86488-106">Because of how much WMI makes possible, the Windows PowerShell cmdlet for accessing WMI objects, **Get-WmiObject**, is one of the most useful for doing real work.</span></span> <span data-ttu-id="86488-107">Arról, hogyan használhatja a Get-WmiObject eléréséhez a WMI-objektumok és WMI-objektumok használata a konkrét feladatok fogjuk.</span><span class="sxs-lookup"><span data-stu-id="86488-107">We are going to discuss how to use Get-WmiObject to access WMI objects and then how to use WMI objects to do specific things.</span></span>

### <a name="listing-wmi-classes"></a><span data-ttu-id="86488-108">WMI-osztályok listázása</span><span class="sxs-lookup"><span data-stu-id="86488-108">Listing WMI Classes</span></span>

<span data-ttu-id="86488-109">Ismerje meg, milyen teheti meg a WMI-WMI a felhasználók többsége lép fel az első probléma próbál.</span><span class="sxs-lookup"><span data-stu-id="86488-109">The first problem most WMI users encounter is trying to find out what can be done with WMI.</span></span> <span data-ttu-id="86488-110">WMI-osztályok ismertetik az erőforrásokat, amelyek kezelhetők.</span><span class="sxs-lookup"><span data-stu-id="86488-110">WMI classes describe the resources that can be managed.</span></span> <span data-ttu-id="86488-111">Nincsenek WMI-osztályokat, amelyek tartalmazzák a Tulajdonságok tucat több száz.</span><span class="sxs-lookup"><span data-stu-id="86488-111">There are hundreds of WMI classes, some of which contain dozens of properties.</span></span>

<span data-ttu-id="86488-112">**Get-WmiObject** azáltal, hogy a WMI észlelhető probléma címek.</span><span class="sxs-lookup"><span data-stu-id="86488-112">**Get-WmiObject** addresses this problem by making WMI discoverable.</span></span> <span data-ttu-id="86488-113">Elérhető a WMI-osztályok listáját a helyi számítógépen beírásával lekérése:</span><span class="sxs-lookup"><span data-stu-id="86488-113">You can get a list of the WMI classes available on the local computer by typing:</span></span>

```
PS> Get-WmiObject -List

__SecurityRelatedClass                  __NTLMUser9X
__PARAMETERS                            __SystemSecurity
__NotifyStatus                          __ExtendedStatus
Win32_PrivilegesStatus                  Win32_TSNetworkAdapterSettingError
Win32_TSRemoteControlSettingError       Win32_TSEnvironmentSettingError
...
```

<span data-ttu-id="86488-114">Lekérheti ugyanazt az információt egy távoli számítógépről a ComputerName paraméter használatával a számítógép nevét vagy IP-cím megadása:</span><span class="sxs-lookup"><span data-stu-id="86488-114">You can retrieve the same information from a remote computer by using the ComputerName parameter, specifying a computer name or IP address:</span></span>

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
__ProviderRegistration                  __ObjectProviderRegistration
...
```

<span data-ttu-id="86488-115">A távoli számítógépek által visszaadott osztály listaelem eltérőek lehetnek a számítógép, amelyen fut az adott operációs rendszerrel és a telepített alkalmazások által hozzáadott adott WMI-bővítmények miatt.</span><span class="sxs-lookup"><span data-stu-id="86488-115">The class listing returned by remote computers may vary due to the specific operating system the computer is running and the particular WMI extensions added by installed applications.</span></span>

> [!NOTE]
> <span data-ttu-id="86488-116">Ha egy távoli számítógéphez való kapcsolódáshoz használja a Get-WmiObject, a távoli számítógépen kell futnia a WMI, és az alapértelmezett konfiguráció szerint a használt fiók a távoli számítógépen a helyi Rendszergazdák csoportban kell lennie.</span><span class="sxs-lookup"><span data-stu-id="86488-116">When using Get-WmiObject to connect to a remote computer, the remote computer must be running WMI and, under the default configuration, the account you are using must be in the local administrators group on the remote computer.</span></span> <span data-ttu-id="86488-117">A távoli rendszer nem kell rendelkeznie a Windows PowerShell telepítve van.</span><span class="sxs-lookup"><span data-stu-id="86488-117">The remote system does not need to have Windows PowerShell installed.</span></span> <span data-ttu-id="86488-118">Ez lehetővé teszi, hogy operációs rendszereket, amelyeket nem futtatja a Windows Powershellt, de elérhető WMI kell felügyelni.</span><span class="sxs-lookup"><span data-stu-id="86488-118">This allows you to administer operating systems that are not running Windows PowerShell, but do have WMI available.</span></span>

<span data-ttu-id="86488-119">A számítógépnév is tartalmazhatnak, a helyi rendszer való csatlakozáskor.</span><span class="sxs-lookup"><span data-stu-id="86488-119">You can even include the ComputerName when connecting to the local system.</span></span> <span data-ttu-id="86488-120">Használhatja a helyi számítógép neve, az IP-címét (vagy a visszacsatolási cím 127.0.0.1), vagy a WMI-stílusú "." a számítógép neve.</span><span class="sxs-lookup"><span data-stu-id="86488-120">You can use the local computer's name, its IP address (or the loopback address 127.0.0.1), or the WMI-style '.' as the computer name.</span></span> <span data-ttu-id="86488-121">Ha Rgazda01 nevű 192.168.1.90 IP-címmel rendelkező számítógépen futtatja a Windows Powershellt, a következő parancsokat az összes adja vissza a WMI-osztály, listázás, az adott számítógépen:</span><span class="sxs-lookup"><span data-stu-id="86488-121">If you are running Windows PowerShell on a computer named Admin01 with IP address 192.168.1.90, the following commands will all return the WMI class listing for that computer:</span></span>

```powershell
Get-WmiObject -List
Get-WmiObject -List -ComputerName .
Get-WmiObject -List -ComputerName Admin01
Get-WmiObject -List -ComputerName 192.168.1.90
Get-WmiObject -List -ComputerName 127.0.0.1
Get-WmiObject -List -ComputerName localhost
```

<span data-ttu-id="86488-122">Get-WmiObject alapértelmezés szerint a root/cimv2 névteret használja.</span><span class="sxs-lookup"><span data-stu-id="86488-122">Get-WmiObject uses the root/cimv2 namespace by default.</span></span> <span data-ttu-id="86488-123">Ha meg szeretné határozni a WMI-névteret, használja a **Namespace** paramétert, és adja meg a megfelelő névtér elérési útja:</span><span class="sxs-lookup"><span data-stu-id="86488-123">If you want to specify another WMI namespace, use the **Namespace** parameter and specify the corresponding namespace path:</span></span>

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29 -Namespace root

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
...
```

### <a name="displaying-wmi-class-details"></a><span data-ttu-id="86488-124">A WMI-osztály részletek megjelenítése</span><span class="sxs-lookup"><span data-stu-id="86488-124">Displaying WMI Class Details</span></span>

<span data-ttu-id="86488-125">Ha már ismeri a WMI-osztály neve, információt webszerveren, és használhatja.</span><span class="sxs-lookup"><span data-stu-id="86488-125">If you already know the name of a WMI class, you can use it to get information immediately.</span></span> <span data-ttu-id="86488-126">Például a gyakran használt számítógépre vonatkozó információk lekérését WMI-osztályok egyike **Win32_OperatingSystem**.</span><span class="sxs-lookup"><span data-stu-id="86488-126">For example, one of the WMI classes commonly used for retrieving information about a computer is **Win32_OperatingSystem**.</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName .

SystemDirectory : C:\WINDOWS\system32
Organization    : Global Network Solutions
BuildNumber     : 2600
RegisteredUser  : Oliver W. Jones
SerialNumber    : 12345-678-9012345-67890
Version         : 5.1.2600
```

<span data-ttu-id="86488-127">Bár a Microsoft összes paraméterének láthatók, a parancs több állapotára úgy lehet kifejezni.</span><span class="sxs-lookup"><span data-stu-id="86488-127">Although we are showing all of the parameters, the command can be expressed in a more succinct way.</span></span> <span data-ttu-id="86488-128">A **ComputerName** paraméter esetén nem szükséges a helyi rendszer csatlakozik.</span><span class="sxs-lookup"><span data-stu-id="86488-128">The **ComputerName** parameter is not necessary when connecting to the local system.</span></span> <span data-ttu-id="86488-129">Bemutatjuk, ez a legtöbb általános helyzet demonstrálására, illetve emlékeztesse a paraméterrel kapcsolatban.</span><span class="sxs-lookup"><span data-stu-id="86488-129">We show it to demonstrate the most general case and remind you about the parameter.</span></span> <span data-ttu-id="86488-130">A **Namespace** alapértelmezés szerint a root/cimv2 és is elhagyható.</span><span class="sxs-lookup"><span data-stu-id="86488-130">The **Namespace** defaults to root/cimv2, and can be omitted as well.</span></span> <span data-ttu-id="86488-131">Végül legtöbb parancsmag lehetővé teszi az általános paraméterek neve nincs megadva.</span><span class="sxs-lookup"><span data-stu-id="86488-131">Finally, most cmdlets allow you to omit the name of common parameters.</span></span> <span data-ttu-id="86488-132">A Get-WmiObject, ha nem ad meg nevet az első paraméterként a Windows PowerShell úgy kezeli, mintha a **osztály** paraméter.</span><span class="sxs-lookup"><span data-stu-id="86488-132">With Get-WmiObject, if no name is specified for the first parameter, Windows PowerShell treats it as the **Class** parameter.</span></span> <span data-ttu-id="86488-133">Ez azt jelenti, hogy az utolsó parancs beírásával kiadva sikerült:</span><span class="sxs-lookup"><span data-stu-id="86488-133">This means the last command could have been issued by typing:</span></span>

```powershell
Get-WmiObject Win32_OperatingSystem
```

<span data-ttu-id="86488-134">A **Win32_OperatingSystem** osztály itt jelenik meg, mint számos további tulajdonságokkal rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="86488-134">The **Win32_OperatingSystem** class has many more properties than those displayed here.</span></span> <span data-ttu-id="86488-135">Az összes tulajdonság megtekintéséhez használhatja a Get-Member.</span><span class="sxs-lookup"><span data-stu-id="86488-135">You can use Get-Member to see all the properties.</span></span> <span data-ttu-id="86488-136">A WMI-osztályok tulajdonságainak automatikusan elérhetők például a többi objektum tulajdonságai:</span><span class="sxs-lookup"><span data-stu-id="86488-136">The properties of a WMI class are automatically available like other object properties:</span></span>

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

#### <a name="displaying-non-default-properties-with-format-cmdlets"></a><span data-ttu-id="86488-137">A formátum parancsmagok nem alapértelmezett tulajdonságainak megjelenítése</span><span class="sxs-lookup"><span data-stu-id="86488-137">Displaying Non-Default Properties with Format Cmdlets</span></span>

<span data-ttu-id="86488-138">Ha azt szeretné, hogy foglalt információk a **Win32_OperatingSystem** osztály, amely alapértelmezés szerint nem jelenik meg, a megjelenítéséhez használatával a **formátum** parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="86488-138">If you want information contained in the **Win32_OperatingSystem** class that is not displayed by default, you can display it by using the **Format** cmdlets.</span></span> <span data-ttu-id="86488-139">Például ha meg szeretné jeleníteni a rendelkezésre álló memória adatok, írja be:</span><span class="sxs-lookup"><span data-stu-id="86488-139">For example, if you want to display available memory data, type:</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-Table -Property TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize TotalVisibleMemory FreePhysicalMemory FreeVirtualMemory FreeSpaceInPagingFiles
---------------------- ---------------    ------------------ -==--------------------- ---------------
               2097024          785904                305808           2056724                1558232
```

> [!NOTE]
> <span data-ttu-id="86488-140">A helyettesítő karakterek használata a tulajdonságnevek **Format-Table**, ezért az utolsó folyamat elem lehet szűkíteni `Format-Table -Property Total,Free`</span><span class="sxs-lookup"><span data-stu-id="86488-140">Wildcards work with property names in **Format-Table**, so the final pipeline element can be reduced to `Format-Table -Property Total,Free`</span></span>

<span data-ttu-id="86488-141">Lehet, hogy a memória adatok jobban olvashatóbbak legyenek, ha formázza azt listaként beírásával:</span><span class="sxs-lookup"><span data-stu-id="86488-141">The memory data might be more readable if you format it as a list by typing:</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-List TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize : 2097024
TotalVisibleMemorySize : 785904
FreePhysicalMemory     : 301876
FreeVirtualMemory      : 2056724
FreeSpaceInPagingFiles : 1556644
```
