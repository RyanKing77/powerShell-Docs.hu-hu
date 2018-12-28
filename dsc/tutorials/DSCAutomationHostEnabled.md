---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSCAutomationHostEnabled beállításkulcs
ms.openlocfilehash: 38e3189323c39a522b2ccad89f5cfcadf5e45616
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404155"
---
>Érintett kiadások: Windows PowerShell 5.0

# <a name="dscautomationhostenabled-registry-key"></a>DSCAutomationHostEnabled beállításkulcs

DSC használja a **DSCAutomationHostEnabled** beállításkulcs alatt **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** engedélyezéséhez az első, a gép konfigurációját.
DSCAutomationHostEnabled három módot támogat:

|  DSCAutomationHostEnabled érték  |  Leírás   |
|---|---|
0 | Tiltsa le a rendszerindítás, a gép konfigurálásával. |
1 | Engedélyezze a gép konfigurál a rendszerindítás. |
2 | Engedélyezze a konfigurálása a gép csak akkor, ha a DSC van függőben lévő vagy a jelenlegi állapotban. Ez az alapértelmezett érték. |

## <a name="see-also"></a>Lásd még:

Ez a funkció használata első konfigurációk futtatni egy példa: [konfigurálása a virtuális gépek első indításkor DSC használatával](bootstrapDsc.md).