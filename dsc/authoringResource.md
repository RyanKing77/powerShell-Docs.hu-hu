---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Egyéni Windows PowerShell kívánt állapot konfigurációs erőforrások létrehozása"
ms.openlocfilehash: 75b494db4ee6e381491decb11d35b60105217a0f
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
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

