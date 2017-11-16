---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "gyűjtemény, a powershell, a parancsmag, a psget"
title: "Frissítés-parancsfájl"
ms.openlocfilehash: cae199636a3bb06099a07e3e0f9a17df2092cbab
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="update-script"></a><span data-ttu-id="05d93-103">Frissítés-parancsfájl</span><span class="sxs-lookup"><span data-stu-id="05d93-103">Update-Script</span></span>

<span data-ttu-id="05d93-104">Frissítés-parancsfájl parancsmag lehetővé teszi az helybeni frissítése a parancsfájlok, amelyek megtörtént-e telepítési parancsfájl-parancsmag használatával.</span><span class="sxs-lookup"><span data-stu-id="05d93-104">Update-Script cmdlet lets you to do in-place update of the script files which were installed using Install-Script cmdlet.</span></span>

## <a name="description"></a><span data-ttu-id="05d93-105">Leírás</span><span class="sxs-lookup"><span data-stu-id="05d93-105">Description</span></span>

<span data-ttu-id="05d93-106">A frissítés-parancsfájl parancsmag frissíti a megadott parancsfájl, amelyen korábban telepítették a tárházból.</span><span class="sxs-lookup"><span data-stu-id="05d93-106">The Update-Script cmdlet updates the specified script from the repository from which it was previously installed.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="05d93-107">A parancsmag szintaxisa</span><span class="sxs-lookup"><span data-stu-id="05d93-107">Cmdlet syntax</span></span>

```powershell
Get-Command -Name Update-Script -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="05d93-108">A parancsmag online Súgó-hivatkozás</span><span class="sxs-lookup"><span data-stu-id="05d93-108">Cmdlet online help reference</span></span>

[<span data-ttu-id="05d93-109">Frissítés-parancsfájl</span><span class="sxs-lookup"><span data-stu-id="05d93-109">Update-Script</span></span>](http://go.microsoft.com/fwlink/?LinkId=619787)

## <a name="example-commands"></a><span data-ttu-id="05d93-110">Példa parancsok</span><span class="sxs-lookup"><span data-stu-id="05d93-110">Example commands</span></span>
```powershell
Install-Script -Name Fabrikam-Script -RequiredVersion 1.0 -Repository GalleryINT -Scope
Get-InstalledScript -Name Fabrikam-Script
Version Name Type Repository Description
------- ---- ---- ---------- -----------
1.0 Fabrikam-Script Script GalleryINT Description for the Fabrikam-Script script

# Update a specific script to the required version
Update-Script -Name Fabrikam-Script -RequiredVersion 1.5
Get-InstalledScript -Name Fabrikam-Script
Version Name Type Repository Description
------- ---- ---- ---------- -----------
1.5 Fabrikam-Script Script GalleryINT Description for the Fabrikam-Script script

# Update all installed scripts
Install-Script -Name Fabrikam-ServerScript -RequiredVersion 1.0 -Repository GalleryINT -Scope CurrentUser
Get-InstalledScript
Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.0 Required-Script3 Script GalleryINT Description for the Required-Script3 script
1.0 Demo-Script Script LocalRepo1 Script file description goes here
1.5 Fabrikam-Script Script GalleryINT Description for the Fabrikam-Script script
1.0 Fabrikam-ServerScript Script GalleryINT Description for the Fabrikam-ServerScript script
2.5 Required-Script1 Script GalleryINT Description for the Required-Script1 script
2.5 Required-Script2 Script GalleryINT Description for the Required-Script2 script
2.0 Script-WithDependencies2 Script GalleryINT Description for the Script-WithDependencies2 script

Update-Script
Get-InstalledScript
Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.5 Required-Script3 Script GalleryINT Description for the Required-Script3 script
1.0 Demo-Script Script LocalRepo1 Script file description goes here
2.5 Fabrikam-Script Script GalleryINT Description for the Fabrikam-Script script
2.5 Fabrikam-ServerScript Script GalleryINT Description for the Fabrikam-ServerScript script
2.5 Required-Script1 Script GalleryINT Description for the Required-Script1 script
2.5 Required-Script2 Script GalleryINT Description for the Required-Script2 script
2.0 Script-WithDependencies2 Script GalleryINT Description for the Script-WithDependencies2 script
```

