---
ms.date: 2017-10-17
contributor: keithb
ms.topic: reference
keywords: "gyűjtemény, a powershell, a parancsmag, a psget"
title: "Mentés-parancsfájl"
ms.openlocfilehash: b54e8ba074b7cadd52df781c9021332ccc90f9fd
ms.sourcegitcommit: 58371abe9db4b9a0e4e1eb82d39a9f9e187355f9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/05/2017
---
# <a name="save-script"></a><span data-ttu-id="3d696-103">Mentés-parancsfájl</span><span class="sxs-lookup"><span data-stu-id="3d696-103">Save-Script</span></span>

<span data-ttu-id="3d696-104">Mentés-parancsfájl parancsmag lehetővé teszi, hogy tekintse át a parancsfájl által megadott helyre való mentése.</span><span class="sxs-lookup"><span data-stu-id="3d696-104">Save-Script cmdlet lets you to review the script file by saving it to a specified location.</span></span>

## <a name="description"></a><span data-ttu-id="3d696-105">Leírás</span><span class="sxs-lookup"><span data-stu-id="3d696-105">Description</span></span>

<span data-ttu-id="3d696-106">A Save-parancsfájl parancsmag menti a rendszer a megadott parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="3d696-106">The Save-Script cmdlet saves the specified script.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="3d696-107">A parancsmag szintaxisa</span><span class="sxs-lookup"><span data-stu-id="3d696-107">Cmdlet syntax</span></span>

```powershell
Get-Command -Name Save-Script -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="3d696-108">A parancsmag online Súgó-hivatkozás</span><span class="sxs-lookup"><span data-stu-id="3d696-108">Cmdlet online help reference</span></span>

[<span data-ttu-id="3d696-109">Mentés-parancsfájl</span><span class="sxs-lookup"><span data-stu-id="3d696-109">Save-Script</span></span>](http://go.microsoft.com/fwlink/?LinkId=619786)

## <a name="example-commands"></a><span data-ttu-id="3d696-110">Példa parancsok</span><span class="sxs-lookup"><span data-stu-id="3d696-110">Example commands</span></span>

### <a name="example-1-save-a-script-from-a-repository"></a><span data-ttu-id="3d696-111">1. példa: Mentse a parancsfájlt a tárházból</span><span class="sxs-lookup"><span data-stu-id="3d696-111">Example 1: Save a script from a repository</span></span>
<span data-ttu-id="3d696-112">Ez a parancs menti a parancsfájl Fabrikam-ClientScript GalleryINT tárházból a helyi mappába C:\ScriptSharingDemo legújabb verzióját</span><span class="sxs-lookup"><span data-stu-id="3d696-112">This command saves the latest version of the script Fabrikam-ClientScript from GalleryINT repository to the local folder C:\ScriptSharingDemo</span></span>

```powershell
Save-Script -Name Fabrikam-ClientScript -Repository GalleryINT -Path C:\ScriptSharingDemo
```

### <a name="example-2-save-a-version-of-a-script-by-piping-from-the-find-script-cmdlet"></a><span data-ttu-id="3d696-113">2. példa: Egy parancsfájl verziója takaríthat meg a keresés-parancsfájl parancsmag átirányítás</span><span class="sxs-lookup"><span data-stu-id="3d696-113">Example 2: Save a version of a script by piping from the Find-Script cmdlet</span></span>

<span data-ttu-id="3d696-114">Az első parancs megkeresi a Fabrikam-ClientScript a tárházból GalleryINT 1.5-ös verzióját, és menti a mappa C:\ScriptSharingDemo</span><span class="sxs-lookup"><span data-stu-id="3d696-114">The first command finds version 1.5 of Fabrikam-ClientScript from the repository GalleryINT and saves it to the folder C:\ScriptSharingDemo</span></span>

<span data-ttu-id="3d696-115">A második parancs ellenőrzi a mentett parancsprogram-metaadatait.</span><span class="sxs-lookup"><span data-stu-id="3d696-115">The second command validates the saved script metadata.</span></span>

```powershell
Find-Script -Name Fabrikam-ClientScript -Repository GalleryINT -RequiredVersion 1.5 | Save-Script -Path C:\\ScriptSharingDemo
Test-ScriptFileInfo C:\\ScriptSharingDemo\\Fabrikam-ClientScript.ps1

Version Name Author Description
------- ---- ------ -----------
1.5 Fabrikam-ClientScript manikb Description for the Fabrikam-ClientScript script
```

### <a name="example-3-save-a-prerelease-version-of-a-script-from-a-repository"></a><span data-ttu-id="3d696-116">3. példa: A tárházban lévő parancsfájl előzetes verziójának mentése</span><span class="sxs-lookup"><span data-stu-id="3d696-116">Example 3: Save a prerelease version of a script from a repository</span></span>
<span data-ttu-id="3d696-117">Ez a parancs menti a parancsfájl Fabrikam-ClientScript GalleryINT tárházból a helyi mappába C:\ScriptSharingDemo legújabb verzióját</span><span class="sxs-lookup"><span data-stu-id="3d696-117">This command saves the latest version of the script Fabrikam-ClientScript from GalleryINT repository to the local folder C:\ScriptSharingDemo</span></span>

```powershell
Save-Script -Name Fabrikam-ClientScript -Path C:\ScriptSharingDemo -AllowPrerelease
```

