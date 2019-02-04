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
# <a name="getting-wmi-objects-get-wmiobject"></a>WMI-objektumok lékérése (Get-WmiObject)

## <a name="getting-wmi-objects-get-wmiobject"></a>WMI-objektumok lékérése (Get-WmiObject)

Windows Management Instrumentation (WMI) egy alapvető technológia a Windows Rendszerfelügyeleti azért számos különféle információkat egységes módon teszi elérhetővé. IP-címek fenntartási lehetővé teszi a WMI lehetséges, a Windows PowerShell-parancsmaggal WMI-objektumok elérése miatt **Get-WmiObject**, a leghasznosabb egyike a valódi munkát végző. Arról, hogyan használhatja a Get-WmiObject eléréséhez a WMI-objektumok és WMI-objektumok használata a konkrét feladatok fogjuk.

### <a name="listing-wmi-classes"></a>WMI-osztályok listázása

Ismerje meg, milyen teheti meg a WMI-WMI a felhasználók többsége lép fel az első probléma próbál. WMI-osztályok ismertetik az erőforrásokat, amelyek kezelhetők. Nincsenek WMI-osztályokat, amelyek tartalmazzák a Tulajdonságok tucat több száz.

**Get-WmiObject** azáltal, hogy a WMI észlelhető probléma címek. Elérhető a WMI-osztályok listáját a helyi számítógépen beírásával lekérése:

```
PS> Get-WmiObject -List

__SecurityRelatedClass                  __NTLMUser9X
__PARAMETERS                            __SystemSecurity
__NotifyStatus                          __ExtendedStatus
Win32_PrivilegesStatus                  Win32_TSNetworkAdapterSettingError
Win32_TSRemoteControlSettingError       Win32_TSEnvironmentSettingError
...
```

Lekérheti ugyanazt az információt egy távoli számítógépről a ComputerName paraméter használatával a számítógép nevét vagy IP-cím megadása:

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
__ProviderRegistration                  __ObjectProviderRegistration
...
```

A távoli számítógépek által visszaadott osztály listaelem eltérőek lehetnek a számítógép, amelyen fut az adott operációs rendszerrel és a telepített alkalmazások által hozzáadott adott WMI-bővítmények miatt.

> [!NOTE]
> Ha egy távoli számítógéphez való kapcsolódáshoz használja a Get-WmiObject, a távoli számítógépen kell futnia a WMI, és az alapértelmezett konfiguráció szerint a használt fiók a távoli számítógépen a helyi Rendszergazdák csoportban kell lennie. A távoli rendszer nem kell rendelkeznie a Windows PowerShell telepítve van. Ez lehetővé teszi, hogy operációs rendszereket, amelyeket nem futtatja a Windows Powershellt, de elérhető WMI kell felügyelni.

A számítógépnév is tartalmazhatnak, a helyi rendszer való csatlakozáskor. Használhatja a helyi számítógép neve, az IP-címét (vagy a visszacsatolási cím 127.0.0.1), vagy a WMI-stílusú "." a számítógép neve. Ha Rgazda01 nevű 192.168.1.90 IP-címmel rendelkező számítógépen futtatja a Windows Powershellt, a következő parancsokat az összes adja vissza a WMI-osztály, listázás, az adott számítógépen:

```powershell
Get-WmiObject -List
Get-WmiObject -List -ComputerName .
Get-WmiObject -List -ComputerName Admin01
Get-WmiObject -List -ComputerName 192.168.1.90
Get-WmiObject -List -ComputerName 127.0.0.1
Get-WmiObject -List -ComputerName localhost
```

Get-WmiObject alapértelmezés szerint a root/cimv2 névteret használja. Ha meg szeretné határozni a WMI-névteret, használja a **Namespace** paramétert, és adja meg a megfelelő névtér elérési útja:

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29 -Namespace root

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
...
```

### <a name="displaying-wmi-class-details"></a>A WMI-osztály részletek megjelenítése

Ha már ismeri a WMI-osztály neve, információt webszerveren, és használhatja. Például a gyakran használt számítógépre vonatkozó információk lekérését WMI-osztályok egyike **Win32_OperatingSystem**.

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName .

SystemDirectory : C:\WINDOWS\system32
Organization    : Global Network Solutions
BuildNumber     : 2600
RegisteredUser  : Oliver W. Jones
SerialNumber    : 12345-678-9012345-67890
Version         : 5.1.2600
```

Bár a Microsoft összes paraméterének láthatók, a parancs több állapotára úgy lehet kifejezni. A **ComputerName** paraméter esetén nem szükséges a helyi rendszer csatlakozik. Bemutatjuk, ez a legtöbb általános helyzet demonstrálására, illetve emlékeztesse a paraméterrel kapcsolatban. A **Namespace** alapértelmezés szerint a root/cimv2 és is elhagyható. Végül legtöbb parancsmag lehetővé teszi az általános paraméterek neve nincs megadva. A Get-WmiObject, ha nem ad meg nevet az első paraméterként a Windows PowerShell úgy kezeli, mintha a **osztály** paraméter. Ez azt jelenti, hogy az utolsó parancs beírásával kiadva sikerült:

```powershell
Get-WmiObject Win32_OperatingSystem
```

A **Win32_OperatingSystem** osztály itt jelenik meg, mint számos további tulajdonságokkal rendelkezik. Az összes tulajdonság megtekintéséhez használhatja a Get-Member. A WMI-osztályok tulajdonságainak automatikusan elérhetők például a többi objektum tulajdonságai:

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

#### <a name="displaying-non-default-properties-with-format-cmdlets"></a>A formátum parancsmagok nem alapértelmezett tulajdonságainak megjelenítése

Ha azt szeretné, hogy foglalt információk a **Win32_OperatingSystem** osztály, amely alapértelmezés szerint nem jelenik meg, a megjelenítéséhez használatával a **formátum** parancsmagok. Például ha meg szeretné jeleníteni a rendelkezésre álló memória adatok, írja be:

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-Table -Property TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize TotalVisibleMemory FreePhysicalMemory FreeVirtualMemory FreeSpaceInPagingFiles
---------------------- ---------------    ------------------ -==--------------------- ---------------
               2097024          785904                305808           2056724                1558232
```

> [!NOTE]
> A helyettesítő karakterek használata a tulajdonságnevek **Format-Table**, ezért az utolsó folyamat elem lehet szűkíteni `Format-Table -Property Total,Free`

Lehet, hogy a memória adatok jobban olvashatóbbak legyenek, ha formázza azt listaként beírásával:

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-List TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize : 2097024
TotalVisibleMemorySize : 785904
FreePhysicalMemory     : 301876
FreeVirtualMemory      : 2056724
FreeSpaceInPagingFiles : 1556644
```
