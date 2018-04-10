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
# <a name="unregister-psrepository"></a><span data-ttu-id="ecb7c-103">PSRepository regisztrációjának törlése</span><span class="sxs-lookup"><span data-stu-id="ecb7c-103">Unregister-PSRepository</span></span>

<span data-ttu-id="ecb7c-104">A tárház regisztrációjának törlése.</span><span class="sxs-lookup"><span data-stu-id="ecb7c-104">Unregisters a repository.</span></span>

## <a name="description"></a><span data-ttu-id="ecb7c-105">Leírás</span><span class="sxs-lookup"><span data-stu-id="ecb7c-105">Description</span></span>

<span data-ttu-id="ecb7c-106">A Unregister-PSRepository parancsmag az aktuális felhasználó tára regisztrációjának törlése.</span><span class="sxs-lookup"><span data-stu-id="ecb7c-106">The Unregister-PSRepository cmdlet unregisters a repository for the current user.</span></span>
- <span data-ttu-id="ecb7c-107">Regisztrációjának megszüntetése és az Újraregisztrálás PSGallery tárház vállalati számára engedélyezve van, és forgatókönyvek leválasztása.</span><span class="sxs-lookup"><span data-stu-id="ecb7c-107">Unregistration and re-registration of the PSGallery repository is allowed for an enterprise and disconnected scenarios.</span></span>
- <span data-ttu-id="ecb7c-108">A felhasználók újra regisztrálhatják a PSGallery egyszerűen futtatásával `Register-PSRepository -Default`</span><span class="sxs-lookup"><span data-stu-id="ecb7c-108">Users can re-register the PSGallery by simply running `Register-PSRepository -Default`</span></span>
- <span data-ttu-id="ecb7c-109">Mivel PSGallery az alapértelmezett tárház közzététele a Publish-modul és a közzététel-parancsfájl-parancsmagok, hibát fog jelezni, ha PSGallery regisztrált tárház listájában nem érhető el.</span><span class="sxs-lookup"><span data-stu-id="ecb7c-109">Since PSGallery is the default publish repository in Publish-Module and Publish-Script cmdlets, an error will be thrown if PSGallery is not available in the registered repository list.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="ecb7c-110">A parancsmag szintaxisa</span><span class="sxs-lookup"><span data-stu-id="ecb7c-110">Cmdlet syntax</span></span>

```powershell
Get-Command -Name Unregister-PSRepository -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="ecb7c-111">A parancsmag online Súgó-hivatkozás</span><span class="sxs-lookup"><span data-stu-id="ecb7c-111">Cmdlet online help reference</span></span>

[<span data-ttu-id="ecb7c-112">PSRepository regisztrációjának törlése</span><span class="sxs-lookup"><span data-stu-id="ecb7c-112">Unregister-PSRepository</span></span>](http://go.microsoft.com/fwlink/?LinkID=517130)

## <a name="example-commands"></a><span data-ttu-id="ecb7c-113">Példa parancsok</span><span class="sxs-lookup"><span data-stu-id="ecb7c-113">Example commands</span></span>

```powershell
Unregister-PSRepository -Name "MyPrivateGallery"

Get-PSRepository exp | Unregister-PSRepository
```

### <a name="unregistration-and-re-registration-of-the-psgallery-repository-is-allowed-for-an-enterprise-and-disconnected-scenarios"></a><span data-ttu-id="ecb7c-114">Regisztrációjának megszüntetése és az Újraregisztrálás PSGallery tárház vállalati számára engedélyezve van, és forgatókönyvek leválasztása.</span><span class="sxs-lookup"><span data-stu-id="ecb7c-114">Unregistration and re-registration of the PSGallery repository is allowed for an enterprise and disconnected scenarios.</span></span>
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