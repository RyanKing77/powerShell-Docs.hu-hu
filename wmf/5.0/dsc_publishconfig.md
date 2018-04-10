---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 136e16ae74e54f3bc9d0623178257df1e9104aac
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="deliver-a-configuration-document-without-applying"></a>Egy konfigurációs dokumentum fájlmegosztásba alkalmazása nélkül

A [Publish-DscConfiguration](https://technet.microsoft.com/library/mt517875.aspx) parancsmag konfigurációs MOF-fájlt másolja a célcsomóponton, de nem alkalmazza a konfigurációt.
Ez a konfiguráció alkalmazása a következő konzisztencia fázis során, vagy ha futtatja a [frissítés-DscConfiguration](https://technet.microsoft.com/library/mt143541.aspx) parancsmag.