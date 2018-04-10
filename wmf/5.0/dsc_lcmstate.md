---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: baa35e9acd24d6f6155acf617a0d2c2210742af7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="detailed-information-about-lcm-state"></a>LCM állapotával kapcsolatos részletes információk

Fejlesztéseket hajtottunk kitettségének LCM állapotára vonatkozó részletek. A Get-DscLocalConfigurationManager által visszaadott LCMState most már tartalmazza a következő értékeket:

* **Üresjárati**
* **Busy**
* **PendingReboot**
* **PendingConfiguration**

Egy LCMStateDetail tulajdonság, amely tartalmazza a állapotával kapcsolatos további információk is jelentek meg.