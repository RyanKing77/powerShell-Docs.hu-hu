---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Beépített erőforrások Desired State Configuration linuxhoz
ms.openlocfilehash: ea700d24c7ff4377af671944184abb3f201852e8
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55689021"
---
# <a name="built-in-desired-state-configuration-resources-for-linux"></a><span data-ttu-id="45b2f-103">Beépített erőforrások Desired State Configuration linuxhoz</span><span class="sxs-lookup"><span data-stu-id="45b2f-103">Built-In Desired State Configuration Resources for Linux</span></span>

<span data-ttu-id="45b2f-104">Erőforrások építőelemei, amellyel a PowerShell Desired State Configuration (DSC) a parancsprogram írásához.</span><span class="sxs-lookup"><span data-stu-id="45b2f-104">Resources are building blocks that you can use to write a PowerShell Desired State Configuration (DSC) script.</span></span> <span data-ttu-id="45b2f-105">Linuxhoz készült DSC tartalmaz egy beépített funkciók konfigurálásához az erőforrások, például fájlok és mappák, csomagok, környezeti változókat, és a szolgáltatások és folyamatokat.</span><span class="sxs-lookup"><span data-stu-id="45b2f-105">DSC for Linux comes with a set of built-in functionality for configuring resources such as files and folders, packages, environment variables, and services and processes.</span></span>

## <a name="built-in-resources"></a><span data-ttu-id="45b2f-106">Beépített erőforrások</span><span class="sxs-lookup"><span data-stu-id="45b2f-106">Built-in resources</span></span>

<span data-ttu-id="45b2f-107">A következő táblázat felsorolja az erőforrások és mutató hivatkozásokat talál, amelyek részletesen ismertetik azokat.</span><span class="sxs-lookup"><span data-stu-id="45b2f-107">The following table provides a list of these resources and links to topics that describe them in detail.</span></span>

* <span data-ttu-id="45b2f-108">[nxArchive erőforrás](lnxArchiveResource.md)– archívum (.tar, .zip kiterjesztésű) fájlok egy adott elérési úton kicsomagolása mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="45b2f-108">[nxArchive Resource](lnxArchiveResource.md)--Provides a mechanism to unpack archive (.tar, .zip) files at a specific path.</span></span>
* <span data-ttu-id="45b2f-109">[nxEnvironment erőforrás](lnxEnvironmentResource.md)– környezeti változókat a célcsomópontokat kezeli.</span><span class="sxs-lookup"><span data-stu-id="45b2f-109">[nxEnvironment Resource](lnxEnvironmentResource.md)--Manages environment variables on target nodes.</span></span>
* <span data-ttu-id="45b2f-110">[nxFile erőforrás](lnxFileResource.md)--kezeli a Linux-fájlok és könyvtárak.</span><span class="sxs-lookup"><span data-stu-id="45b2f-110">[nxFile Resource](lnxFileResource.md)--Manages Linux files and directories.</span></span>
* <span data-ttu-id="45b2f-111">[nxFileLine erőforrás](lnxFileLineResource.md)– egy Linux-fájl az egyes sorok kezeli.</span><span class="sxs-lookup"><span data-stu-id="45b2f-111">[nxFileLine Resource](lnxFileLineResource.md)--Manages individual lines in a Linux file.</span></span>
* <span data-ttu-id="45b2f-112">[nxGroup erőforrás](lnxGroupResource.md)– helyi Linux kezeli.</span><span class="sxs-lookup"><span data-stu-id="45b2f-112">[nxGroup Resource](lnxGroupResource.md)--Manages local Linux groups.</span></span>
* <span data-ttu-id="45b2f-113">[nxPackage erőforrás](lnxPackageResource.md)--kezeli a csomagokat a Linux-csomópontokat.</span><span class="sxs-lookup"><span data-stu-id="45b2f-113">[nxPackage Resource](lnxPackageResource.md)--Manages packages on Linux nodes.</span></span>
* <span data-ttu-id="45b2f-114">[Erőforrás nxScript](lnxScriptResource.md)--futtat szkripteket a célcsomópontokat.</span><span class="sxs-lookup"><span data-stu-id="45b2f-114">[nxScript Resource](lnxScriptResource.md)--Runs scripts on target nodes.</span></span>
* <span data-ttu-id="45b2f-115">[nxService erőforrás](lnxServiceResource.md)--kezeli a Linux-szolgáltatás (démonok).</span><span class="sxs-lookup"><span data-stu-id="45b2f-115">[nxService Resource](lnxServiceResource.md)--Manages Linux services (daemons).</span></span>
* <span data-ttu-id="45b2f-116">[nxSshAuthorizedKeys erőforrás](lnxSshAuthorizedKeysResource.md)--kezeli a nyilvános ssh kulcsokat a Linux-felhasználók.</span><span class="sxs-lookup"><span data-stu-id="45b2f-116">[nxSshAuthorizedKeys Resource](lnxSshAuthorizedKeysResource.md)--Manages public ssh keys for a Linux user.</span></span>
* <span data-ttu-id="45b2f-117">[nxUser erőforrás](lnxUserResource.md)– helyi Linux-felhasználók kezeli.</span><span class="sxs-lookup"><span data-stu-id="45b2f-117">[nxUser Resource](lnxUserResource.md)--Manages local Linux users.</span></span>