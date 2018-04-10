---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: Set-PSRepository
ms.openlocfilehash: 0b555f31241bad15c5e99f3db0136d88ff7ab717
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="set-psrepository"></a><span data-ttu-id="1f591-103">Set-PSRepository</span><span class="sxs-lookup"><span data-stu-id="1f591-103">Set-PSRepository</span></span>

<span data-ttu-id="1f591-104">Set-PSRepository regisztrált tárház értékek beállítása.</span><span class="sxs-lookup"><span data-stu-id="1f591-104">Set-PSRepository sets values for a registered repository.</span></span>

## <a name="description"></a><span data-ttu-id="1f591-105">Leírás</span><span class="sxs-lookup"><span data-stu-id="1f591-105">Description</span></span>

<span data-ttu-id="1f591-106">A Set-PSRepository parancsmag egy regisztrált modul tárház értékek beállítása.</span><span class="sxs-lookup"><span data-stu-id="1f591-106">The Set-PSRepository cmdlet sets values for a registered module repository.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="1f591-107">A parancsmag szintaxisa</span><span class="sxs-lookup"><span data-stu-id="1f591-107">Cmdlet syntax</span></span>

```powershell
Get-Command -Name Set-PSRepository -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="1f591-108">A parancsmag online Súgó-hivatkozás</span><span class="sxs-lookup"><span data-stu-id="1f591-108">Cmdlet online help reference</span></span>

[<span data-ttu-id="1f591-109">Set-PSRepository</span><span class="sxs-lookup"><span data-stu-id="1f591-109">Set-PSRepository</span></span>](http://go.microsoft.com/fwlink/?LinkID=517128)

## <a name="example-commands"></a><span data-ttu-id="1f591-110">Példa parancsok</span><span class="sxs-lookup"><span data-stu-id="1f591-110">Example commands</span></span>

```powershell
PS C:\> Register-PSRepository -Name myRepository -SourceLocation "https://www.myget.org/F/powershellgetdemo/api/v2" -InstallationPolicy Trusted
PS C:\> Get-PSRepository
Name                      InstallationPolicy   SourceLocation
----                      ------------------   --------------
myRepository              Trusted              https://www.myget.org/F/powershellgetdemo/api/v2

# Set installation Policy for a repository
PS C:\> Set-PSRepository -Name myRepository -InstallationPolicy Untrusted
PS C:\> Get-PSRepository

Name                      InstallationPolicy   SourceLocation
----                      ------------------   --------------
myRepository              Untrusted            https://www.myget.org/F/powershellgetdemo/api/v2
```


### <a name="set-psrepository-cmdlet-with-script-sharing-support"></a><span data-ttu-id="1f591-111">Set-PSRepository parancsmag-parancsfájllal támogatási megosztása</span><span class="sxs-lookup"><span data-stu-id="1f591-111">Set-PSRepository cmdlet with script sharing support</span></span>

<span data-ttu-id="1f591-112">Set-PSRepository-parancsmagok használatával adja hozzá a **ScriptSourceLocation** és **ScriptPublishLocation** a PSRepository számára.</span><span class="sxs-lookup"><span data-stu-id="1f591-112">Use Set-PSRepository cmdlets to add the **ScriptSourceLocation** and **ScriptPublishLocation** to the PSRepository.</span></span>
```powershell
# Add script sharing locations to an existing PSRepository using Set-PSRepository object.
Set-PSRepository -Name MyGallery `
                 -ScriptSourceLocation https://MyGallery.com/api/v2/items/psscript/ `
                 -ScriptPublishLocation https://MyGallery.com/api/v2/package/

Get-PSRepository -Name GalleryINT | Format-List * -Force

Name : GalleryINT
SourceLocation : https://MyGallery.com/api/v2/
Trusted : True
Registered : True
InstallationPolicy : Trusted
PackageManagementProvider : NuGet
PublishLocation : https://MyGallery.com/api/v2/package/
ScriptSourceLocation : https://MyGallery.com/api/v2/items/psscript/
ScriptPublishLocation : https://MyGallery.com/api/v2/package/
ProviderOptions : {}

```