---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: f929ce4684bb53c3039238ecd465f1c0e432f741
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34225674"
---
# <a name="deliver-a-configuration-document-without-applying"></a>Egy konfigurációs dokumentum fájlmegosztásba alkalmazása nélkül

A [Publish-DscConfiguration](https://technet.microsoft.com/library/mt517875.aspx) parancsmag konfigurációs MOF-fájlt másolja a célcsomóponton, de nem alkalmazza a konfigurációt.
Ez a konfiguráció alkalmazása a következő konzisztencia fázis során, vagy ha futtatja a [frissítés-DscConfiguration](https://technet.microsoft.com/library/mt143541.aspx) parancsmag.
