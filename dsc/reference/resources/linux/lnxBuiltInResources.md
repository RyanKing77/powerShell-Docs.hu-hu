---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Beépített erőforrások Desired State Configuration linuxhoz
ms.openlocfilehash: ea700d24c7ff4377af671944184abb3f201852e8
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048477"
---
# <a name="built-in-desired-state-configuration-resources-for-linux"></a>Beépített erőforrások Desired State Configuration linuxhoz

Erőforrások építőelemei, amellyel a PowerShell Desired State Configuration (DSC) a parancsprogram írásához. Linuxhoz készült DSC tartalmaz egy beépített funkciók konfigurálásához az erőforrások, például fájlok és mappák, csomagok, környezeti változókat, és a szolgáltatások és folyamatokat.

## <a name="built-in-resources"></a>Beépített erőforrások

A következő táblázat felsorolja az erőforrások és mutató hivatkozásokat talál, amelyek részletesen ismertetik azokat.

* [nxArchive erőforrás](lnxArchiveResource.md)– archívum (.tar, .zip kiterjesztésű) fájlok egy adott elérési úton kicsomagolása mechanizmust biztosít.
* [nxEnvironment erőforrás](lnxEnvironmentResource.md)– környezeti változókat a célcsomópontokat kezeli.
* [nxFile erőforrás](lnxFileResource.md)--kezeli a Linux-fájlok és könyvtárak.
* [nxFileLine erőforrás](lnxFileLineResource.md)– egy Linux-fájl az egyes sorok kezeli.
* [nxGroup erőforrás](lnxGroupResource.md)– helyi Linux kezeli.
* [nxPackage erőforrás](lnxPackageResource.md)--kezeli a csomagokat a Linux-csomópontokat.
* [Erőforrás nxScript](lnxScriptResource.md)--futtat szkripteket a célcsomópontokat.
* [nxService erőforrás](lnxServiceResource.md)--kezeli a Linux-szolgáltatás (démonok).
* [nxSshAuthorizedKeys erőforrás](lnxSshAuthorizedKeysResource.md)--kezeli a nyilvános ssh kulcsokat a Linux-felhasználók.
* [nxUser erőforrás](lnxUserResource.md)– helyi Linux-felhasználók kezeli.