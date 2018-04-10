---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: Get-PSRepository
ms.openlocfilehash: 97279a8ed0087c835fb924991484959cd7237016
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="get-psrepository"></a>Get-PSRepository

Lekérdezi a regisztrált tárházak találhatók a számítógépen.

## <a name="description"></a>Leírás

A Get-PSRepository parancsmag PowerShell modul adattárak regisztrált lekérdezi az aktuális felhasználó a számítógépen.

Minden egyes regisztrált tárház Get-PSRepository ad vissza egy PSRepository objektumon, amelynek opcionálisan átirányítható Unregister-PSRepository a beállításjegyzékből való törlésekor egy regisztrált tárházat.

## <a name="cmdlet-syntax"></a>A parancsmag szintaxisa
```powershell
Get-Command -Name Get-PSRepository -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>A parancsmag online Súgó-hivatkozás

[Get-PSRepository](http://go.microsoft.com/fwlink/?LinkID=517127)

## <a name="example-commands"></a>Példa parancsok

```powershell

# Properties of Get-PSRepository returned object
Get-PSRepository PSGallery | Format-List * -Force

Name                      : PSGallery
SourceLocation            : https://www.powershellgallery.com/api/v2/
Trusted                   : False
Registered                : True
InstallationPolicy        : Untrusted
PackageManagementProvider : NuGet
PublishLocation           : https://www.powershellgallery.com/api/v2/package/
ScriptSourceLocation      : https://www.powershellgallery.com/api/v2/items/psscript/
ScriptPublishLocation     : https://www.powershellgallery.com/api/v2/package/
ProviderOptions           : {}

# Get all registered repositories
Get-PSRepository

# Get a specific registered repository
Get-PSRepository PSGallery

Name                      InstallationPolicy   SourceLocation
----                      ------------------   --------------
PSGallery                 Untrusted            https://www.powershellgallery.com/api/v2/

# Get registered repository with wildcards
Get-PSRepository *Gallery*

```