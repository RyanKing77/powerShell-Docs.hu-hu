---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSCAutomationHostEnabled beállításkulcs
ms.openlocfilehash: 2bccd2738b9f61efd656fdf0f98cf71affdbe781
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684800"
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
