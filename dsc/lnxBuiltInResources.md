---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Beépített konfiguráló erőforrások Linux szükséges."
ms.openlocfilehash: e268cb2ee8a246f18216b34e5e2a6d512f15e18c
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="built-in-desired-state-configuration-resources-for-linux"></a>Beépített konfiguráló erőforrások Linux szükséges.

Erőforrások építőelemei, hogy PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) parancsfájlokat használhat. Linux DSC tartalmaz egy beépített funkciók erőforrások, például a fájlok és mappák, csomagok, környezeti változókat és a szolgáltatások és folyamatok konfigurálásához.

## <a name="built-in-resources"></a>Beépített erőforrások 

A következő táblázat felsorolja a erőforrások és a hivatkozások témakörökre mutatnak, amelyek részletesen ismertetik azokat.

* [Erőforrás nxArchive](lnxArchiveResource.md)– egy adott elérési úton (.tar, .zip) archív fájlok kicsomagolása mechanizmust biztosít.
* [Erőforrás nxEnvironment](lnxEnvironmentResource.md)– környezeti változók a célcsomópontokat kezeli. 
* [Erőforrás nxFile](lnxFileResource.md)--Linux kezeli a fájlok és könyvtárak. 
* [Erőforrás nxFileLine](lnxFileLineResource.md)--kezeli az egyes sorokban egy Linux-fájlban. 
* [Erőforrás nxGroup](lnxGroupResource.md)--Linux helyi csoportok kezeli. 
* [Erőforrás nxPackage](lnxPackageResource.md)--Linux csomópontján csomagok kezeli.
* [Erőforrás nxScript](lnxScriptResource.md)--futtatja a parancsfájlokat a célcsomópontokat.
* [Erőforrás nxService](lnxServiceResource.md)--Linux kezeli a szolgáltatások (démonok).
* [Erőforrás nxSshAuthorizedKeys](lnxSshAuthorizedKeysResource.md)--kezeli a nyilvános ssh kulcsokat a Linux-felhasználók számára. 
* [Erőforrás nxUser](lnxUserResource.md)– helyi Linux-felhasználók kezeli. 
  
