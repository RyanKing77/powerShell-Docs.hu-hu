---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: Keresés – parancs
ms.openlocfilehash: 26ddf4824816db245131a0fc95b7d2a88bef8f4c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="find-command"></a>Keresés – parancs

Megkeresi a PowerShell-parancsok modulban.

## <a name="description"></a>Leírás
A keresés-Command parancsmaggal megkeresi a PowerShell-parancsok, például a parancsmagok, aliasok, függvények és munkafolyamatok. Keresés – parancs modulok regisztrált adattárak keresi.
Az egyes parancsok, ez a parancsmag által megtalált egy PSGetCommandInfo objektum beállítása/beolvasása. Az Install-modul parancsmag telepíti a modult, amely tartalmazza a parancsot egy PSGetCommandInfo objektumot tud átadni.

- Keresés-parancs verzió paraméterekkel szűrheti: MinimumVersion, RequiredVersion, AllVersions.
  - Ezek a paraméterek kölcsönösen kizárják egymást.
  - Ezen verzió paraméterek csak nevű egy modul nélkül a helyettesítő karakterek megengedettek.
  - A RequiredVersion paraméter nincs megadva, ha a Keresés-parancs a modult, amely egyenlő vagy nagyobb, mint a minimális verzió van megadva, vagy a legújabb verzióját a modul esetén nincs minimális verzió van megadva a legújabb verzióját adja vissza.
  - A RequiredVersion paraméter van megadva, ha Keresés-parancs, az csak a modult, amely pontosan megegyezik a megadott version verzióját adja vissza.
- Keresés – parancs szűrést végezhet a modul metaadatai paraméterrel - címke
- Keresés – parancs szűrést végezhet a tárház vonatkozó keresést nyelvi paraméterrel - szűrő.
- Keresés – parancs modulok vagy kevés a regisztrált adattárak végezhet.

## <a name="cmdlet-syntax"></a>A parancsmag szintaxisa
```powershell
Get-Command -Name Find-Command -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>A parancsmag online Súgó-hivatkozás

[Keresés – parancs](http://go.microsoft.com/fwlink/?LinkId=733636)

## <a name="example-commands"></a>Példa parancsok
```powershell

# Find a specific command
Find-Command -Name Get-ScriptAnalyzerRule

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
Get-ScriptAnalyzerRule              1.5.0      PSScriptAnalyzer                    PSGallery

# Find multiple commands
Find-Command -Name Get-ScriptAnalyzerRule, Invoke-ScriptAnalyzer

# Find all available commands from all registered repositories
Find-Command

# Find available commands from few registered repositories
Find-Command -Repository PSGallery,PrivatePSGallery

# Find all commands in a specified repository
Find-Command -Repository PSGallery

# Find a command defined in a specific module
Find-Command -Name Get-ScriptAnalyzerRule -Module PSScriptAnalyzer

# Find commands from all versions of a module
Find-Command -ModuleName PSReadline -AllVersions

# Find commands with module name and MinimumVersion.
Find-Command -ModuleName PSReadline -MinimumVersion 1.1

# Find commands with module name and exact version
Find-Command -ModuleName AzureRM -RequiredVersion 1.4.0

# Find commands defined modules with -Filter based search. -Filter searches in description and module names
Find-Command -Filter Cookbook
Find-Command -Filter RBAC

# Find all commands with tags Azure or DSC in module metadata
Find-Command -Tag Azure, DSC

```