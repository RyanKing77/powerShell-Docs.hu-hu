---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: Get-InstalledModule
ms.openlocfilehash: f82d8f3b6b6a9283deef44c2705b97d4717b634c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="get-installedmodule"></a>Get-InstalledModule

Lekérdezi a számítógépen telepített modulok.

## <a name="description"></a>Leírás

A Get-InstalledModule parancsmag lekéri a telepített PowerShell moduloknál számítógépen telepített Install-modul a parancsmag használatával.

Minden telepített modul Get-InstalledModule ad vissza egy nem kötelezően átirányítható PSRepositoryItemInfo objektum eltávolítás-modul a telepített modulok eltávolításához.

- Get-InstalledModule telepített modulokban neve, verziója paraméterek alapján szűrhetők.
- Get-InstalledModule verzió paraméterekkel szűrheti: MinimumVersion, MaximumVersion, RequiredVersion, AllVersions.
  - Ezek a paraméterek kölcsönösen kizárják egymást, kivéve a MinmimumVersion és MaximumVersion.
  - Ezen verzió paraméterek csak nevű egy modul nélkül a helyettesítő karakterek megengedettek.
  - Ha a RequiredVersion paraméter nincs megadva, a Get-InstalledModule egyenlő vagy nagyobb, mint a minimális verzió van megadva, vagy a legújabb verzióját a modul esetén nincs minimális verzió van megadva a telepített modul legújabb verzióját adja vissza.
  - A RequiredVersion paraméter van megadva, az Get-InstalledModule csak adja vissza a telepített modul, amely pontosan megegyezik a megadott version verzióját.

## <a name="cmdlet-syntax"></a>A parancsmag szintaxisa
```powershell
Get-Command -Name Get-InstalledModule -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>A parancsmag online Súgó-hivatkozás

[Get-InstalledModule](http://go.microsoft.com/fwlink/?LinkId=526863)

## <a name="example-commands"></a>Példa parancsok

```powershell

# Get all modules installed using PowerShellGet cmdlets
Get-InstalledModule

# Get a specific installed module
Get-InstalledModule DJoin

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.0        DJoin                               PSGallery            This is a PowerShell frontend to the DJOIN.exe c...

# Get installed module with wildcards
Get-InstalledModule -Name AzureRM*

# Get all versions of an installed module
Get-InstalledModule -Name AzureRM.Automation -AllVersions

# Get installed module with MinimumVersion
Get-InstalledModule -Name AzureRM.Automation -MinimumVersion 1.0.0

# Get installed module with MaximumVersion
Get-InstalledModule -Name AzureRM.Automation -MaximumVersion 1.0.8

# Get installed module with version range
Get-InstalledModule -Name AzureRM.Automation -MinimumVersion 1.0.0 -MaximumVersion 1.0.8

# Get installed module with RequiredVersion
Get-InstalledScript -Name AzureRM.Automation -RequiredVersion 1.0.3

# Properties of Get-InstalledModule returned object
Get-InstalledModule DJoin | Format-List * -Force

Name                       : DJoin
Version                    : 1.0
Type                       : Module
Description                : This is a PowerShell frontend to the DJOIN.exe command which provides better
                             discoverability and usability.
Author                     : Jeffrey Snover
CompanyName                : jsnover
Copyright                  : (C) Microsoft Corporation. All rights reserved.
PublishedDate              : 2/15/2016 7:12:37 PM
InstalledDate              : 4/5/2016 4:13:39 PM
UpdatedDate                :
LicenseUri                 :
ProjectUri                 :
IconUri                    :
Tags                       : {Nano, PSModule}
Includes                   : {Function, RoleCapability, Command, DscResource...}
PowerShellGetFormatVersion :
ReleaseNotes               :
Dependencies               : {}
RepositorySourceLocation   : https://www.powershellgallery.com/api/v2/
Repository                 : PSGallery
PackageManagementProvider  : NuGet
AdditionalMetadata         : {description, installeddate, tags, PackageManagementProvider...}
InstalledLocation          : C:\Program Files\WindowsPowerShell\Modules\DJoin\1.0

```



## <a name="installeddate-and-updateddate-properties-in-psgetrepositoryiteminfo-object"></a>InstalledDate és UpdatedDate PSGetRepositoryItemInfo objektum tulajdonságai

    During the install operation:
        InstalledDate: current DateTime (Get-Date) value
        UpdatedDate: null

    During the Update operation:
        InstalledDate: InstalledDate from the previous installation otherwise current DateTime (Get-Date) value
        UpdatedDate: current DateTime (Get-Date) value

```powershell
Install-Module -Name ContosoServer -RequiredVersion 1.0 -Repository INT
Get-InstalledModule -Name ContosoServer | Format-Table Name, InstalledDate, UpdatedDate

Name          InstalledDate         UpdatedDate
----          -------------         -----------
ContosoServer 2/29/2016 11:59:14 AM


\Update-Module -Name ContosoServer
Get-InstalledModule -Name ContosoServer | Format-Table Name, InstalledDate, UpdatedDate

Name          InstalledDate         UpdatedDate
----          -------------         -----------
ContosoServer 2/29/2016 11:59:14 AM 2/29/2016 12:00:15 PM
```