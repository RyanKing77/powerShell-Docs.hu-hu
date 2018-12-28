---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Egyéni Windows PowerShell Desired State Configuration erőforrások létrehozása
ms.openlocfilehash: 882b6efed4564d2354183d7472b301e1e1758335
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404165"
---
# <a name="build-custom-windows-powershell-desired-state-configuration-resources"></a>Egyéni Windows PowerShell Desired State Configuration erőforrások létrehozása

> Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

Windows PowerShell Desired State Configuration (DSC) rendelkezik beépített erőforrások, amelyek segítségével konfigurálja a környezetet. Ez a témakör áttekintést erőforrások és a konkrét információk és példák témakörökre mutató hivatkozásokat.

## <a name="dsc-resource-components"></a>DSC-erőforrás összetevők

A DSC-erőforrás egy Windows PowerShell-modul. A modul tartalmazza a séma (a Tulajdonságok gyűjteményével-definíció) és a (a kódot, amely a megadott konfiguráció szerint a tényleges munkát) végrehajtása az erőforrás. A DSC-erőforrás séma MOF-fájl lehet definiálni, és a egy szkriptmodulba végzi a megvalósítás. Verziótól kezdve a PowerShell-osztályok az 5-ös verzió támogatása, a séma és a megvalósítás is lehet definiálni egy osztályt. Az alábbi témakörök részletesen ismertetik a DSC-erőforrások létrehozása.

* [MOF-egyéni DSC-erőforrás írása](authoringResourceMOF.md)
* [A DSC erőforrás megvalósításaC#](authoringResourceMofCS.md)
* [A PowerShell-osztályok egyéni DSC-erőforrás írása](authoringResourceClass.md)
* [Összetett erőforrások: A DSC-konfiguráció használata erőforrásként](authoringResourceComposite.md)
* [Az erőforrás-tervező eszköz használata](../authoringResourceMofDesigner.md)
