---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Egyéni Windows PowerShell kívánt állapot konfigurációs erőforrások létrehozása"
ms.openlocfilehash: 4751bcaab1996ee3164bd2a2f430c3b188712860
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
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

