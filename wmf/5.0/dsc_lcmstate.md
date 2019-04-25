---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 57152e9f62c34600df63a2db8e9683928e825d93
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62085796"
---
# <a name="detailed-information-about-lcm-state"></a>Az LCM állapotának részletes adatai

Fejlesztéseket hajtottunk is közzéteheti az LCM állapotának részleteit. A Get-DscLocalConfigurationManager által visszaadott LCMState mostantól tartalmazza a következő értékeket:

* **Inaktív**
* **elfoglalt**
* **PendingReboot**
* **PendingConfiguration**

Bővítettük egy LCMStateDetail tulajdonsággal, amely tartalmazza az állam bővebben is.
