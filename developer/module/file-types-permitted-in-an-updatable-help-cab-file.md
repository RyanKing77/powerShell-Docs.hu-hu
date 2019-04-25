---
title: Fájltípus esetében engedélyezett a egy frissíthető súgó CAB-fájl |} A Microsoft Docs
ms.custom: ''
ms.date: 03/22/2012
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Windows PowerShell 3.0
ms.assetid: acabdb93-c41a-4b8d-acbe-45cdab91e198
caps.latest.revision: 10
ms.openlocfilehash: 3562804157ebdfca561445a8671d726b55cc4efd
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62082447"
---
# <a name="file-types-permitted-in-an-updatable-help-cab-file"></a><span data-ttu-id="0589e-102">Frissíthető CAB-súgófájlok megengedett fájltípusai</span><span class="sxs-lookup"><span data-stu-id="0589e-102">File Types Permitted in an Updatable Help CAB File</span></span>

<span data-ttu-id="0589e-103">Ez a témakör felsorolja és ismerteti a tartalom frissíthető súgó CAB-fájlok.</span><span class="sxs-lookup"><span data-stu-id="0589e-103">This topics lists and describes the content requirements for Updatable Help CAB files.</span></span>

## <a name="updatable-help-cab-file-requirements"></a><span data-ttu-id="0589e-104">Frissíthető súgó CAB-fájl követelményei</span><span class="sxs-lookup"><span data-stu-id="0589e-104">Updatable Help CAB File Requirements</span></span>

<span data-ttu-id="0589e-105">Tömörítetlen CAB-fájl tartalmának alapértelmezés szerint 1 GB-os korlátozva.</span><span class="sxs-lookup"><span data-stu-id="0589e-105">Uncompressed CAB file content is limited to 1 GB by default.</span></span> <span data-ttu-id="0589e-106">Megkerülésére ezt a korlátot, a felhasználóknak meg kell használni a **kényszerített** paraméterében a [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) és [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="0589e-106">To bypass this limit, users have to use the **Force** parameter of the [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) and [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) cmdlets.</span></span>

<span data-ttu-id="0589e-107">Ahhoz, hogy biztosítsa a súgófájlokat, amelyek az internetről letöltött biztonságát, az frissíthető súgó CAB-fájl csak az alábbi fájltípusokat tartalmazhatnak.</span><span class="sxs-lookup"><span data-stu-id="0589e-107">To assure the security of help files that are downloaded from the Internet, an Updatable Help CAB file can include only the file types listed below.</span></span> <span data-ttu-id="0589e-108">A [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) parancsmag érvényesíti az összes fájlt a Súgó-témakör sémák alapján.</span><span class="sxs-lookup"><span data-stu-id="0589e-108">The [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) cmdlet validates all files against the help topic schemas.</span></span> <span data-ttu-id="0589e-109">Ha a `Update-Help` parancsmag egy fájlt, amely érvénytelen vagy nem engedélyezett típusú észlel, nem telepíti a érvénytelen fájlt, és leállítja a felhasználó számítógépén lévő fájlok telepítése.</span><span class="sxs-lookup"><span data-stu-id="0589e-109">If the `Update-Help` cmdlet encounters a file that is invalid or is not a permitted type, it does not install the invalid file and stops installing files from the CAB on the user's computer.</span></span>

- <span data-ttu-id="0589e-110">XML-alapú súgó-témaköröket parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="0589e-110">XML-based help topics for cmdlets.</span></span>

- <span data-ttu-id="0589e-111">XML-alapú súgó-témaköröket parancsfájlokban és függvényekben.</span><span class="sxs-lookup"><span data-stu-id="0589e-111">XML-based help topics for scripts and functions.</span></span>

- <span data-ttu-id="0589e-112">XML-alapú súgó-témaköröket Windows PowerShell-szolgáltatók.</span><span class="sxs-lookup"><span data-stu-id="0589e-112">XML-based help topics for Windows PowerShell providers.</span></span>

- <span data-ttu-id="0589e-113">Szöveges súgótémakörök, például a témákról.</span><span class="sxs-lookup"><span data-stu-id="0589e-113">Text-based help topics, such as About topics.</span></span>

<span data-ttu-id="0589e-114">A [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) amikor, kibontja a CAB ellenőrzi a cab-fájl tartalmát.</span><span class="sxs-lookup"><span data-stu-id="0589e-114">The [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) verifies the CAB contents when it unpacks the CAB.</span></span> <span data-ttu-id="0589e-115">Ha `Update-Help` megkeresi a nem megfelelő fájltípusok egy frissíthető súgó CAB-fájl, a leállítási hibát generál, és leállítja a műveletet.</span><span class="sxs-lookup"><span data-stu-id="0589e-115">If `Update-Help` finds non-compliant file types in an Updatable Help CAB file, it generates a terminating error and stops the operation.</span></span> <span data-ttu-id="0589e-116">Bármely súgófájlok nem telepít, a CAB, azokat is, az megfelelő típusú.</span><span class="sxs-lookup"><span data-stu-id="0589e-116">It does not install any help files from the CAB, even those of compliant file types.</span></span>