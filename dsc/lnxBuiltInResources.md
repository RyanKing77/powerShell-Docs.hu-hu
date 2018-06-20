---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Beépített konfiguráló erőforrások Linux szükséges.
ms.openlocfilehash: ea700d24c7ff4377af671944184abb3f201852e8
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34218501"
---
# <a name="built-in-desired-state-configuration-resources-for-linux"></a><span data-ttu-id="763de-103">Beépített konfiguráló erőforrások Linux szükséges.</span><span class="sxs-lookup"><span data-stu-id="763de-103">Built-In Desired State Configuration Resources for Linux</span></span>

<span data-ttu-id="763de-104">Erőforrások építőelemei, hogy PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) parancsfájlokat használhat.</span><span class="sxs-lookup"><span data-stu-id="763de-104">Resources are building blocks that you can use to write a PowerShell Desired State Configuration (DSC) script.</span></span> <span data-ttu-id="763de-105">Linux DSC tartalmaz egy beépített funkciók erőforrások, például a fájlok és mappák, csomagok, környezeti változókat és a szolgáltatások és folyamatok konfigurálásához.</span><span class="sxs-lookup"><span data-stu-id="763de-105">DSC for Linux comes with a set of built-in functionality for configuring resources such as files and folders, packages, environment variables, and services and processes.</span></span>

## <a name="built-in-resources"></a><span data-ttu-id="763de-106">Beépített erőforrások</span><span class="sxs-lookup"><span data-stu-id="763de-106">Built-in resources</span></span>

<span data-ttu-id="763de-107">A következő táblázat felsorolja a erőforrások és a hivatkozások témakörökre mutatnak, amelyek részletesen ismertetik azokat.</span><span class="sxs-lookup"><span data-stu-id="763de-107">The following table provides a list of these resources and links to topics that describe them in detail.</span></span>

* <span data-ttu-id="763de-108">[Erőforrás nxArchive](lnxArchiveResource.md)– egy adott elérési úton (.tar, .zip) archív fájlok kicsomagolása mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="763de-108">[nxArchive Resource](lnxArchiveResource.md)--Provides a mechanism to unpack archive (.tar, .zip) files at a specific path.</span></span>
* <span data-ttu-id="763de-109">[Erőforrás nxEnvironment](lnxEnvironmentResource.md)– környezeti változók a célcsomópontokat kezeli.</span><span class="sxs-lookup"><span data-stu-id="763de-109">[nxEnvironment Resource](lnxEnvironmentResource.md)--Manages environment variables on target nodes.</span></span>
* <span data-ttu-id="763de-110">[Erőforrás nxFile](lnxFileResource.md)--Linux kezeli a fájlok és könyvtárak.</span><span class="sxs-lookup"><span data-stu-id="763de-110">[nxFile Resource](lnxFileResource.md)--Manages Linux files and directories.</span></span>
* <span data-ttu-id="763de-111">[Erőforrás nxFileLine](lnxFileLineResource.md)--kezeli az egyes sorokban egy Linux-fájlban.</span><span class="sxs-lookup"><span data-stu-id="763de-111">[nxFileLine Resource](lnxFileLineResource.md)--Manages individual lines in a Linux file.</span></span>
* <span data-ttu-id="763de-112">[Erőforrás nxGroup](lnxGroupResource.md)--Linux helyi csoportok kezeli.</span><span class="sxs-lookup"><span data-stu-id="763de-112">[nxGroup Resource](lnxGroupResource.md)--Manages local Linux groups.</span></span>
* <span data-ttu-id="763de-113">[Erőforrás nxPackage](lnxPackageResource.md)--Linux csomópontján csomagok kezeli.</span><span class="sxs-lookup"><span data-stu-id="763de-113">[nxPackage Resource](lnxPackageResource.md)--Manages packages on Linux nodes.</span></span>
* <span data-ttu-id="763de-114">[Erőforrás nxScript](lnxScriptResource.md)--futtatja a parancsfájlokat a célcsomópontokat.</span><span class="sxs-lookup"><span data-stu-id="763de-114">[nxScript Resource](lnxScriptResource.md)--Runs scripts on target nodes.</span></span>
* <span data-ttu-id="763de-115">[Erőforrás nxService](lnxServiceResource.md)--Linux kezeli a szolgáltatások (démonok).</span><span class="sxs-lookup"><span data-stu-id="763de-115">[nxService Resource](lnxServiceResource.md)--Manages Linux services (daemons).</span></span>
* <span data-ttu-id="763de-116">[Erőforrás nxSshAuthorizedKeys](lnxSshAuthorizedKeysResource.md)--kezeli a nyilvános ssh kulcsokat a Linux-felhasználók számára.</span><span class="sxs-lookup"><span data-stu-id="763de-116">[nxSshAuthorizedKeys Resource](lnxSshAuthorizedKeysResource.md)--Manages public ssh keys for a Linux user.</span></span>
* <span data-ttu-id="763de-117">[Erőforrás nxUser](lnxUserResource.md)– helyi Linux-felhasználók kezeli.</span><span class="sxs-lookup"><span data-stu-id="763de-117">[nxUser Resource](lnxUserResource.md)--Manages local Linux users.</span></span>