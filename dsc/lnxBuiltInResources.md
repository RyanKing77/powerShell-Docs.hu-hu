---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Beépített konfiguráló erőforrások Linux szükséges."
ms.openlocfilehash: b85f32f7559d89bda566d35462cc613d73424c50
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
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
  
