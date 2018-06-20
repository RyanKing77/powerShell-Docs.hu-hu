---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: db9b48c188b3bfe2e20c06875606a285922f55a6
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219861"
---
# <a name="detailed-information-about-lcm-state"></a>LCM állapotával kapcsolatos részletes információk

Fejlesztéseket hajtottunk kitettségének LCM állapotára vonatkozó részletek. A Get-DscLocalConfigurationManager által visszaadott LCMState most már tartalmazza a következő értékeket:

* **Üresjárati**
* **elfoglalt**
* **PendingReboot**
* **PendingConfiguration**

Egy LCMStateDetail tulajdonság, amely tartalmazza a állapotával kapcsolatos további információk is jelentek meg.
