---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Egyéni Windows PowerShell kívánt állapot konfigurációs erőforrások létrehozása
ms.openlocfilehash: 7da4741a773d40da75c6ef667c35f86e1bae74bf
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="build-custom-windows-powershell-desired-state-configuration-resources"></a>Egyéni Windows PowerShell kívánt állapot konfigurációs erőforrások létrehozása

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) rendelkezik, amelyek segítségével konfigurálhatja a környezetében beépített erőforrások. (További információkért lásd: [beépített Windows PowerShell kívánt állapot konfigurációs erőforrások](builtInResource.md).) Ez a témakör áttekintést a szükséges erőforrások és az adott útmutatást és példákat témakörökre mutató hivatkozásokat tartalmaz.

## <a name="dsc-resource-components"></a>A DSC-erőforrás összetevők

A DSC-erőforrás egy Windows PowerShell-modul. A modul az erőforrás a séma (a beállítható tulajdonságok definíciója) és a megvalósítás (a kódot, amely a tényleges munkát konfiguráció által meghatározott) is tartalmazza. A DSC-erőforrás séma meghatározása a MOF-fájlt, és végrehajtása egy szkriptmodulba hajtja végre. Kezdődő 5-ös verzió osztályokat PowerShell-támogatása, a séma és a megvalósítását is definiálható osztályban található. Az alábbi témakörök ismertetik részletesebben DSC erőforrások létrehozásához.

* [Egyéni DSC-erőforrás MOF írása](authoringResourceMOF.md)
* [A DSC-erőforrás végrehajtási C#](authoringResourceMofCS.md)
* [A PowerShell osztályok egyéni DSC-erőforrás írása](authoringResourceClass.md)
* [Összetett erőforrások: erőforrásként a DSC-konfiguráció használata](authoringResourceComposite.md)
* [Az erőforrás-tervező eszközzel](authoringResourceMofDesigner.md)