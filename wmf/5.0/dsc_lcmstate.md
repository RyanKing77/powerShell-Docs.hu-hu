---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 4fc146f84588d368ac3eb819e3acb4cb8c5d8793
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="detailed-information-about-lcm-state"></a>LCM állapotával kapcsolatos részletes információk

Fejlesztéseket hajtottunk kitettségének LCM állapotára vonatkozó részletek. A Get-DscLocalConfigurationManager által visszaadott LCMState most már tartalmazza a következő értékeket:

* **Üresjárati**
* **elfoglalt**
* **PendingReboot**
* **PendingConfiguration**

Egy LCMStateDetail tulajdonság, amely tartalmazza a állapotával kapcsolatos további információk is jelentek meg.

