---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: e921a5ead21f52b7e0d9efd9335c44b99d7d6802
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="deliver-a-configuration-document-without-applying"></a>Egy konfigurációs dokumentum fájlmegosztásba alkalmazása nélkül

A [Publish-DscConfiguration](https://technet.microsoft.com/library/mt517875.aspx) parancsmag konfigurációs MOF-fájlt másolja a célcsomóponton, de nem alkalmazza a konfigurációt. Ez a konfiguráció alkalmazása a következő konzisztencia fázis során, vagy ha futtatja a [frissítés-DscConfiguration](https://technet.microsoft.com/library/mt143541.aspx) parancsmag.

