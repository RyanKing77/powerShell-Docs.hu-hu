---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSCAutomationHostEnabled beállításkulcs
ms.openlocfilehash: 2bccd2738b9f61efd656fdf0f98cf71affdbe781
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62076485"
---
>Érintett kiadások: Windows PowerShell 5.0

# <a name="dscautomationhostenabled-registry-key"></a>DSCAutomationHostEnabled beállításkulcs

DSC használja a **DSCAutomationHostEnabled** beállításkulcs alatt **localaccounttokenfilterpolicy** ahhoz, hogy a gép kezdeti konfiguráció rendszerindítás.
**DSCAutomationHostEnabled** három módot támogat:

|  DSCAutomationHostEnabled érték  |  Leírás   |
|---|---|
0 | Tiltsa le a rendszerindítás, a gép konfigurálásával. |
1 | Engedélyezze a gép konfigurál a rendszerindítás. |
2 | Engedélyezze a konfigurálása a gép csak akkor, ha a DSC van függőben lévő vagy a jelenlegi állapotban. Ez az alapértelmezett érték. |

## <a name="see-also"></a>Lásd még:

Ez a funkció használata első konfigurációk futtatni egy példa: [konfigurálása a virtuális gépek első indításkor DSC használatával](bootstrapDsc.md).
