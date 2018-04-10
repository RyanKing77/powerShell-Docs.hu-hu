---
ms.date: 10/17/2017
contributor: keithb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: Save-Script
ms.openlocfilehash: 67697fc0e70fb31cad9ad5ae7ce01debef160b81
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="save-script"></a><span data-ttu-id="4d08e-103">Save-Script</span><span class="sxs-lookup"><span data-stu-id="4d08e-103">Save-Script</span></span>

<span data-ttu-id="4d08e-104">Mentés-parancsfájl parancsmag lehetővé teszi, hogy tekintse át a parancsfájl által megadott helyre való mentése.</span><span class="sxs-lookup"><span data-stu-id="4d08e-104">Save-Script cmdlet lets you to review the script file by saving it to a specified location.</span></span>

## <a name="description"></a><span data-ttu-id="4d08e-105">Leírás</span><span class="sxs-lookup"><span data-stu-id="4d08e-105">Description</span></span>

<span data-ttu-id="4d08e-106">A Save-parancsfájl parancsmag menti a rendszer a megadott parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="4d08e-106">The Save-Script cmdlet saves the specified script.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="4d08e-107">A parancsmag szintaxisa</span><span class="sxs-lookup"><span data-stu-id="4d08e-107">Cmdlet syntax</span></span>

```powershell
Get-Command -Name Save-Script -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="4d08e-108">A parancsmag online Súgó-hivatkozás</span><span class="sxs-lookup"><span data-stu-id="4d08e-108">Cmdlet online help reference</span></span>

[<span data-ttu-id="4d08e-109">Save-Script</span><span class="sxs-lookup"><span data-stu-id="4d08e-109">Save-Script</span></span>](http://go.microsoft.com/fwlink/?LinkId=619786)

## <a name="example-commands"></a><span data-ttu-id="4d08e-110">Példa parancsok</span><span class="sxs-lookup"><span data-stu-id="4d08e-110">Example commands</span></span>

### <a name="example-1-save-a-script-from-a-repository"></a><span data-ttu-id="4d08e-111">1. példa: Mentse a parancsfájlt a tárházból</span><span class="sxs-lookup"><span data-stu-id="4d08e-111">Example 1: Save a script from a repository</span></span>
<span data-ttu-id="4d08e-112">Ez a parancs menti a parancsfájl Fabrikam-ClientScript GalleryINT tárházból a helyi mappába C:\ScriptSharingDemo legújabb verzióját</span><span class="sxs-lookup"><span data-stu-id="4d08e-112">This command saves the latest version of the script Fabrikam-ClientScript from GalleryINT repository to the local folder C:\ScriptSharingDemo</span></span>

```powershell
Save-Script -Name Fabrikam-ClientScript -Repository GalleryINT -Path C:\ScriptSharingDemo
```

### <a name="example-2-save-a-version-of-a-script-by-piping-from-the-find-script-cmdlet"></a><span data-ttu-id="4d08e-113">2. példa: Egy parancsfájl verziója takaríthat meg a keresés-parancsfájl parancsmag átirányítás</span><span class="sxs-lookup"><span data-stu-id="4d08e-113">Example 2: Save a version of a script by piping from the Find-Script cmdlet</span></span>

<span data-ttu-id="4d08e-114">Az első parancs megkeresi a Fabrikam-ClientScript a tárházból GalleryINT 1.5-ös verzióját, és menti a mappa C:\ScriptSharingDemo</span><span class="sxs-lookup"><span data-stu-id="4d08e-114">The first command finds version 1.5 of Fabrikam-ClientScript from the repository GalleryINT and saves it to the folder C:\ScriptSharingDemo</span></span>

<span data-ttu-id="4d08e-115">A második parancs ellenőrzi a mentett parancsprogram-metaadatait.</span><span class="sxs-lookup"><span data-stu-id="4d08e-115">The second command validates the saved script metadata.</span></span>

```powershell
Find-Script -Name Fabrikam-ClientScript -Repository GalleryINT -RequiredVersion 1.5 | Save-Script -Path C:\\ScriptSharingDemo
Test-ScriptFileInfo C:\\ScriptSharingDemo\\Fabrikam-ClientScript.ps1

Version Name Author Description
------- ---- ------ -----------
1.5 Fabrikam-ClientScript manikb Description for the Fabrikam-ClientScript script
```

### <a name="example-3-save-a-prerelease-version-of-a-script-from-a-repository"></a><span data-ttu-id="4d08e-116">3. példa: A tárházban lévő parancsfájl előzetes verziójának mentése</span><span class="sxs-lookup"><span data-stu-id="4d08e-116">Example 3: Save a prerelease version of a script from a repository</span></span>
<span data-ttu-id="4d08e-117">Ez a parancs menti a parancsfájl Fabrikam-ClientScript GalleryINT tárházból a helyi mappába C:\ScriptSharingDemo legújabb verzióját</span><span class="sxs-lookup"><span data-stu-id="4d08e-117">This command saves the latest version of the script Fabrikam-ClientScript from GalleryINT repository to the local folder C:\ScriptSharingDemo</span></span>

```powershell
Save-Script -Name Fabrikam-ClientScript -Path C:\ScriptSharingDemo -AllowPrerelease
```