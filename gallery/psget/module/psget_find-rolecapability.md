---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: Keresés – RoleCapability
ms.openlocfilehash: 89aacd604d54f6a5e9752790be65cc3bcc77c8e1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="find-rolecapability"></a>Keresés – RoleCapability

Megkeresi a szerepkör képességek modulban.

## <a name="description"></a>Leírás
A keresés-RoleCapability parancsmag PowerShell szerepkör képességek modulok talál. Keresés – RoleCapability modulok regisztrált adattárak keresi.
Az egyes szerepkör képesség, ez a parancsmag által megtalált egy PSGetRoleCapabilityInfo objektum beállítása/beolvasása. A modul, amely tartalmazza a szerepkör funkció telepítése a telepítés-modul a parancsmag egy PSGetRoleCapabilityInfo objektumot tud átadni.
PowerShell szerepkör képességek határozza meg, amely parancsokat, alkalmazásokat, és így tovább egy felhasználó egy csak elég adminisztrációs (JEA) végpont elérhető. Szerepkör képességek .psrc kiterjesztésű fájlok határozzák meg.

- Keresés-RoleCapability verzió paraméterekkel szűrheti: MinimumVersion, RequiredVersion, AllVersions.
  - Ezek a paraméterek kölcsönösen kizárják egymást.
  - Ezen verzió paraméterek csak nevű egy modul nélkül a helyettesítő karakterek megengedettek.
  - A RequiredVersion paraméter nincs megadva, ha a keresés-RoleCapability a modult, amely egyenlő vagy nagyobb, mint a minimális verzió van megadva, vagy a legújabb verzióját a modul esetén nincs minimális verzió van megadva a legújabb verzióját adja vissza.
  - A RequiredVersion paraméter van megadva, ha keresés-RoleCapability, az csak a modult, amely pontosan megegyezik a megadott version verzióját adja vissza.
- Keresés – RoleCapability szűrést végezhet a modul metaadatai paraméterrel - címke
- Keresés – RoleCapability szűrést végezhet a tárház vonatkozó keresést nyelvi paraméterrel - szűrő.
- Keresés – RoleCapability modulok vagy kevés a regisztrált adattárak végezhet.

## <a name="cmdlet-syntax"></a>A parancsmag szintaxisa
```powershell
Get-Command -Name Find-RoleCapability -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>A parancsmag online Súgó-hivatkozás

[Find-RoleCapability](http://go.microsoft.com/fwlink/?LinkId=718029)

## <a name="example-commands"></a>Példa parancsok
```powershell

# Find a specific role capability
Find-RoleCapability -Name Maintenance

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
Maintenance                         1.5.0      RoleCapModule                       PrivatePSGallery

# Find multiple role capabilities
Find-RoleCapability -Name MyJeaRole, Maintenance

# Find all available role capabilities from all registered repositories
Find-RoleCapability

# Find available role capabilities from few registered repositories
Find-RoleCapability -Repository PSGallery,PrivatePSGallery

# Find all role capabilities in a specified repository
Find-RoleCapability -Repository PSGallery

# Find a role capability defined in a specific module
Find-RoleCapability -Name Maintenance -ModuleName RoleCapModule

# Find role capabilities from all versions of a module
Find-RoleCapability -ModuleName RoleCapModule -AllVersions

# Find role capabilities with module name and MinimumVersion.
Find-RoleCapability -ModuleName RoleCapModule -MinimumVersion 1.1

# Find role capabilities with module name and exact version
Find-RoleCapability -ModuleName RoleCapModule -RequiredVersion 1.4.0

# Find role capabilities defined modules with -Filter based search. -Filter searches in description and module names
Find-RoleCapability -Filter Cookbook
Find-RoleCapability -Filter RBAC

# Find all role capabilities with tags Azure or DSC in module metadata
Find-RoleCapability -Tag Azure, DSC

```