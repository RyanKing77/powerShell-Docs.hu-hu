---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: Keresés – DscResource
ms.openlocfilehash: 522a44e25c57a7dd75a098a1f34e53e74d96f4a6
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="find-dscresource"></a>Keresés – DscResource

A DSC-erőforrásokat keresi az modulok.

## <a name="description"></a>Leírás

A keresés-DscResource parancsmagot talál [kívánt állapot konfigurációs szolgáltatása (DSC)](https://msdn.microsoft.com/PowerShell/dsc/overview) regisztrált tárházak találhatók a megadott feltételeknek megfelelő modulban található erőforrást.
Minden modul a parancsmag által megtalált keresés-DscResource telepítés-modulhoz, amely a parancsmag visszaadja erőforrásokat tartalmazó moduljainak telepítése egy átadható PSGetDscResourceInfo objektum beállítása/beolvasása.

A DSC-ből egy olyan új felügyeleti platformot, amely lehetővé teszi a telepítésével és konfigurációs adatokat a szoftver szolgáltatások kezelése és a környezet, amelyben a szolgáltatások futnak kezelése a Windows PowerShell.

A kívánt állapot konfigurációs szolgáltatása (DSC) forrásokban a építőelemeket DSC-konfiguráció. Egy erőforrás konfigurált (séma), valamint a PowerShell parancsfájl olyan függvényeket tartalmaz, hogy "," meghívja a helyi Configuration Manager (LCM) tulajdonságok közzététele.

Egy erőforrás modellezhető valamilyen általános fájlként, vagy egy olyan IIS-kiszolgálói beállítást legpontosabb. Például erőforrások csoportja, amelyek rendszerezi az összes szükséges fájlt a hordozható, és a metaadatok azonosítására, hogyan a az erőforrásokhoz való használatra készült tartalmazó struktúrára DSC modulra van összevonva.

- Keresés-DscResource verzió paraméterekkel szűrheti: MinimumVersion, RequiredVersion, AllVersions.
  - Ezek a paraméterek kölcsönösen kizárják egymást.
  - Ezen verzió paraméterek csak nevű egy modul nélkül a helyettesítő karakterek megengedettek.
  - A RequiredVersion paraméter nincs megadva, ha a keresés-DscResource a modult, amely egyenlő vagy nagyobb, mint a minimális verzió van megadva, vagy a legújabb verzióját a modul esetén nincs minimális verzió van megadva a legújabb verzióját adja vissza.
  - A RequiredVersion paraméter van megadva, ha keresés-DscResource, az csak a modult, amely pontosan megegyezik a megadott version verzióját adja vissza.
- Keresés – DscResource szűrést végezhet a modul metaadatai paraméterrel - címke
- Keresés – DscResource szűrést végezhet a tárház vonatkozó keresést nyelvi paraméterrel - szűrő.
- Keresés – DscResource modulok vagy kevés a regisztrált adattárak végezhet.

## <a name="cmdlet-syntax"></a>A parancsmag szintaxisa
```powershell
Get-Command -Name Find-DscResource -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>A parancsmag online Súgó-hivatkozás

[Keresés – DscResource](http://go.microsoft.com/fwlink/?LinkId=517196)

## <a name="example-commands"></a>Példa parancsok
```powershell

# Find a specific DSC Resource
Find-DscResource -Name xIisFeatureDelegation

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
xIisFeatureDelegation               1.10.0.0   xWebAdministration                  PSGallery

# Find all available DSC Resources from all registered repositories
Find-DscResource

# Find a DSC resource by name
Find-DscResource -Name xWebsite

# Find multiple DSC Resources
Find-DscResource -Name xIisHandler, xFirewall

# Find all DSC resources contained within a specific module
Find-DscResource -ModuleName xNetworking
Find-DscResource -ModuleName xWebAdministration

# Find all DSC resources in modules with DSCResourceKit or DesiredStateConfiguration
Find-DscResource -Tag DesiredStateConfiguration, DSCResourceKit

# Find available DSC Resources from few registered repositories
Find-DscResource -Repository PSGallery,PrivatePSGallery

# Find all DSC Resources in a specified repository
Find-DscResource -Repository PSGallery

# Find DSC Resources from all versions of a module
Find-DscResource -ModuleName xNetworking -AllVersions

# Find DSC Resources with module name and MinimumVersion.
Find-DscResource -ModuleName xNetworking -MinimumVersion 1.1

# Find DSC Resources with module name and exact version
Find-DscResource -ModuleName xNetworking -RequiredVersion 2.1.1

# Find DSC Resources defined modules with -Filter based search. -Filter searches in description and module names
Find-DscResource -Filter Domain

# Find all DSC Resources with tags Azure or DSC in module metadata
Find-DscResource -Tag Azure, DSC

```