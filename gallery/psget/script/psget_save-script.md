---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "gyűjtemény, a powershell, a parancsmag, a psget"
title: "Mentés-parancsfájl"
ms.openlocfilehash: 7b692d33e3f86a89505b8d37c0da4177f3dff2c2
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="save-script"></a><span data-ttu-id="bb67b-103">Mentés-parancsfájl</span><span class="sxs-lookup"><span data-stu-id="bb67b-103">Save-Script</span></span>

<span data-ttu-id="bb67b-104">Mentés-parancsfájl parancsmag lehetővé teszi, hogy tekintse át a parancsfájl által megadott helyre való mentése.</span><span class="sxs-lookup"><span data-stu-id="bb67b-104">Save-Script cmdlet lets you to review the script file by saving it to a specified location.</span></span>

## <a name="description"></a><span data-ttu-id="bb67b-105">Leírás</span><span class="sxs-lookup"><span data-stu-id="bb67b-105">Description</span></span>

<span data-ttu-id="bb67b-106">A Save-parancsfájl parancsmag menti a rendszer a megadott parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="bb67b-106">The Save-Script cmdlet saves the specified script.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="bb67b-107">A parancsmag szintaxisa</span><span class="sxs-lookup"><span data-stu-id="bb67b-107">Cmdlet syntax</span></span>

```powershell
Get-Command -Name Save-Script -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="bb67b-108">A parancsmag online Súgó-hivatkozás</span><span class="sxs-lookup"><span data-stu-id="bb67b-108">Cmdlet online help reference</span></span>

[<span data-ttu-id="bb67b-109">Mentés-parancsfájl</span><span class="sxs-lookup"><span data-stu-id="bb67b-109">Save-Script</span></span>](http://go.microsoft.com/fwlink/?LinkId=619786)

## <a name="example-commands"></a><span data-ttu-id="bb67b-110">Példa parancsok</span><span class="sxs-lookup"><span data-stu-id="bb67b-110">Example commands</span></span>

### <a name="example-1-save-a-script-from-a-repository"></a><span data-ttu-id="bb67b-111">1. példa: Mentse a parancsfájlt a tárházból</span><span class="sxs-lookup"><span data-stu-id="bb67b-111">Example 1: Save a script from a repository</span></span>
<span data-ttu-id="bb67b-112">Ez a parancs menti a parancsfájl Fabrikam-ClientScript GalleryINT tárházból a helyi mappába C:\ScriptSharingDemo legújabb verzióját</span><span class="sxs-lookup"><span data-stu-id="bb67b-112">This command saves the latest version of the script Fabrikam-ClientScript from GalleryINT repository to the local folder C:\ScriptSharingDemo</span></span>

```powershell
Save-Script -Name Fabrikam-ClientScript -Repository GalleryINT -Path C:\ScriptSharingDemo
```

### <a name="example-2-save-a-version-of-a-script-by-piping-from-the-find-script-cmdlet"></a><span data-ttu-id="bb67b-113">2. példa: Egy parancsfájl verziója takaríthat meg a keresés-parancsfájl parancsmag átirányítás</span><span class="sxs-lookup"><span data-stu-id="bb67b-113">Example 2: Save a version of a script by piping from the Find-Script cmdlet</span></span>

<span data-ttu-id="bb67b-114">Az első parancs megkeresi a Fabrikam-ClientScript a tárházból GalleryINT 1.5-ös verzióját, és menti a mappa C:\ScriptSharingDemo</span><span class="sxs-lookup"><span data-stu-id="bb67b-114">The first command finds version 1.5 of Fabrikam-ClientScript from the repository GalleryINT and saves it to the folder C:\ScriptSharingDemo</span></span>

<span data-ttu-id="bb67b-115">A második parancs ellenőrzi a mentett parancsprogram-metaadatait.</span><span class="sxs-lookup"><span data-stu-id="bb67b-115">The second command validates the saved script metadata.</span></span>

```powershell
Find-Script -Name Fabrikam-ClientScript -Repository GalleryINT -RequiredVersion 1.5 | Save-Script -Path C:\\ScriptSharingDemo
Test-ScriptFileInfo C:\\ScriptSharingDemo\\Fabrikam-ClientScript.ps1

Version Name Author Description
------- ---- ------ -----------
1.5 Fabrikam-ClientScript manikb Description for the Fabrikam-ClientScript script
```

