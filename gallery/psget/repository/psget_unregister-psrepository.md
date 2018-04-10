---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: PSRepository regisztrációjának törlése
ms.openlocfilehash: 7847e223ae7edd9ec2417d104e5e8130f92a59cf
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="unregister-psrepository"></a>PSRepository regisztrációjának törlése

A tárház regisztrációjának törlése.

## <a name="description"></a>Leírás

A Unregister-PSRepository parancsmag az aktuális felhasználó tára regisztrációjának törlése.
- Regisztrációjának megszüntetése és az Újraregisztrálás PSGallery tárház vállalati számára engedélyezve van, és forgatókönyvek leválasztása.
- A felhasználók újra regisztrálhatják a PSGallery egyszerűen futtatásával `Register-PSRepository -Default`
- Mivel PSGallery az alapértelmezett tárház közzététele a Publish-modul és a közzététel-parancsfájl-parancsmagok, hibát fog jelezni, ha PSGallery regisztrált tárház listájában nem érhető el.

## <a name="cmdlet-syntax"></a>A parancsmag szintaxisa

```powershell
Get-Command -Name Unregister-PSRepository -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a>A parancsmag online Súgó-hivatkozás

[PSRepository regisztrációjának törlése](http://go.microsoft.com/fwlink/?LinkID=517130)

## <a name="example-commands"></a>Példa parancsok

```powershell
Unregister-PSRepository -Name "MyPrivateGallery"

Get-PSRepository exp | Unregister-PSRepository
```

### <a name="unregistration-and-re-registration-of-the-psgallery-repository-is-allowed-for-an-enterprise-and-disconnected-scenarios"></a>Regisztrációjának megszüntetése és az Újraregisztrálás PSGallery tárház vállalati számára engedélyezve van, és forgatókönyvek leválasztása.
```powershell

# Unregister PSGallery repository
Unregister-PSRepository PSGallery

# Publish-Module throws an error when PSGallery is not a registered repository
Publish-Module -Name MyModule
publish-module : Unable to find repository 'PSGallery'. Use Get-PSRepository to see all available repositories. Try again after specifying a valid repository name. You can use 'Register-PSRepository -Default' to register the PSGallery repository.
At line:1 char:1
+ publish-module -name mymodule
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (PSGallery:String) [Publish-Module], ArgumentException
    + FullyQualifiedErrorId : PSGalleryNotFound,Publish-Module

# Re-register PSGallery repository
Register-PSRepository -Default
```