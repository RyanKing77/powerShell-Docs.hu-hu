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
---
# <a name="getting-wmi-objects-get-wmiobject"></a>WMI-objektumok (Get-WmiObject) beolvasása

## <a name="getting-wmi-objects-get-wmiobject"></a>WMI-objektumok (Get-WmiObject) beolvasása

A Windows Management Instrumentation (WMI) egy alapvető technológiák a Windows rendszer-felügyeleti oka egységes módon adatok széles skáláját teszi elérhetővé. Mennyi lehetővé teszi a WMI lehetséges, a Windows PowerShell-parancsmag WMI-objektumok eléréséhez miatt **Get-WmiObject**, a leghasznosabb egyike a valódi munkát. Fogjuk megvitatni a Get-WmiObject használata a WMI-objektumok eléréséhez és WMI-objektumok használata elvégzésére.

### <a name="listing-wmi-classes"></a>WMI-osztályok listázása

A legtöbb WMI felhasználóknál első problémát próbál megtudhatja, mi teheti a WMI-ben. WMI-osztályokat, amelyek kezelhetők erőforrásokat leíró. WMI-osztályokat, tulajdonságok több tucatnyi tartalmaz, amelyek több száz van.

**Get-WmiObject** kezeli ezt a problémát azáltal, hogy a WMI felderíthető. A rendelkezésre álló WMI-osztályok listáját kaphat a helyi számítógépen írja be:

```
PS> Get-WmiObject -List

__SecurityRelatedClass                  __NTLMUser9X
__PARAMETERS                            __SystemSecurity
__NotifyStatus                          __ExtendedStatus
Win32_PrivilegesStatus                  Win32_TSNetworkAdapterSettingError
Win32_TSRemoteControlSettingError       Win32_TSEnvironmentSettingError
...
```

Kérheti le ugyanazokat az információkat egy távoli számítógépről a ComputerName paraméterrel a számítógép nevét vagy IP-cím megadása:

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
__ProviderRegistration                  __ObjectProviderRegistration
...
```

A távoli számítógépek által visszaadott osztály listát az adott operációs rendszerrel, a számítógép fut, és a telepített alkalmazások által hozzáadott adott WMI-bővítmények miatt eltérhetnek.

> [!NOTE]
> Get-WmiObject használata a távoli számítógéphez csatlakozni, a távoli számítógépen futnia kell az WMI, és az alapértelmezett konfiguráció használt fiók a helyi Rendszergazdák csoport, a távoli számítógépen kell lennie. A távoli rendszer nem kell a Windows PowerShell telepítve van. Ez lehetővé teszi, hogy nem futnak Windows PowerShell, amelyek WMI rendelkezésre álló operációs rendszerek felügyeletét.

A számítógépnév is tartalmazhatnak, amikor csatlakozik a helyi rendszer. Használhatja a helyi számítógép neve, az IP-címét (vagy a visszacsatolási cím 127.0.0.1), vagy a WMI-style "." karaktert a számítógép neveként. Ha futtatja a Windows PowerShell IP-cím 192.168.1.90 Rgazda01 nevű számítógépen, a következő parancsokat minden visszatér a WMI-osztály listázása az adott számítógépen:

```powershell
Get-WmiObject -List
Get-WmiObject -List -ComputerName .
Get-WmiObject -List -ComputerName Admin01
Get-WmiObject -List -ComputerName 192.168.1.90
Get-WmiObject -List -ComputerName 127.0.0.1
Get-WmiObject -List -ComputerName localhost
```

Get-WmiObject alapértelmezés szerint a legfelső szintű/cimv2 névteret használja. Ha szeretne megadni egy másik WMI-névteret, használja a **Namespace** paraméter, és adja meg a megfelelő névtér elérési útja:

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29 -Namespace root

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
...
```

### <a name="displaying-wmi-class-details"></a>WMI-osztály részletek megjelenítése

Ha már ismeri a nevét, a WMI-osztályok, azonnal lekérése használhatja. Például a WMI-osztályokat, gyakran használják a számítógép adatainak lekérése egyik **Win32_OperatingSystem**.

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName .

SystemDirectory : C:\WINDOWS\system32
Organization    : Global Network Solutions
BuildNumber     : 2600
RegisteredUser  : Oliver W. Jones
SerialNumber    : 12345-678-9012345-67890
Version         : 5.1.2600
```

Bár azt összes paraméterének láthatók, a parancs több állapotára úgy lehet megadni. A **számítógépnév** paraméter nem szükséges a helyi rendszer történő csatlakozás során. A legtöbb általános esetben bemutatása és jelezve, az paraméterrel kapcsolatos megmutatjuk. A **Namespace** legfelső szintű/cimv2 az alapértelmezett, és is kihagyható. Végezetül legtöbb parancsmagok lehetővé teszik az általános paraméterek neve nincs megadva. A Get-WmiObject, ha nem adott meg az első paraméter, a Windows PowerShell úgy kezeli, mint a **osztály** paraméter. Ez azt jelenti, hogy az utolsó parancs beírásával kiadott sikerült:

```powershell
Get-WmiObject Win32_OperatingSystem
```

A **Win32_OperatingSystem** osztály tulajdonságai sok több mint itt jelenik meg. Get-tag használhatja a tulajdonságok megtekintéséhez. A tulajdonságok a WMI-osztályok automatikusan elérhetők például más objektum tulajdonságai:

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

#### <a name="displaying-non-default-properties-with-format-cmdlets"></a>A formátum-parancsmagokkal nem alapértelmezett tulajdonságok megjelenítése

Ha azt szeretné, hogy a tárolt információ a **Win32_OperatingSystem** osztály, amely alapértelmezés szerint nem jelenik meg, meg lehet jeleníteni használatával a **formátum** parancsmagok. Ha meg szeretné jeleníteni a rendelkezésre álló memória adatok, például:

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-Table -Property TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize TotalVisibleMemory FreePhysicalMemory FreeVirtualMemory FreeSpaceInPagingFiles
---------------------- ---------------    ------------------ -==--------------------- ---------------
               2097024          785904                305808           2056724                1558232
```

> [!NOTE]
> Helyettesítő karakterek használata a tulajdonságnevek **Format-Table**, így csökkenthető a végső csővezeték elem `Format-Table -Property Total,Free`

Lehet, hogy a memória adatok olvashatóbb, ha azt listaként beírásával:

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-List TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize : 2097024
TotalVisibleMemorySize : 785904
FreePhysicalMemory     : 301876
FreeVirtualMemory      : 2056724
FreeSpaceInPagingFiles : 1556644
```
