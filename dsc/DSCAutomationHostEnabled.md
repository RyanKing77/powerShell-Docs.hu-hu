---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: DSCAutomationHostEnabled beállításkulcs
ms.openlocfilehash: 9fd71120b4959a7b14094922b453b05b217f3736
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
>A következőkre vonatkozik: a Windows PowerShell 5.0

# <a name="dscautomationhostenabled-registry-key"></a>DSCAutomationHostEnabled beállításkulcs

DSC használja a **DSCAutomationHostEnabled** kulcs alatt **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** ahhoz, hogy a kezdeti állítja a gép konfigurációját.
DSCAutomationHostEnabled három módot támogat:

|  DSCAutomationHostEnabled Value  |  Leírás   |
|---|---|
0 | Tiltsa le a gép konfigurál állítja. |
1 | Engedélyezze a gép konfigurál állítja. |
2 | A gép konfigurálása, csak ha DSC engedélyezése folyamatban lévő vagy a jelenlegi állapot. Ez az alapértelmezett érték. |

## <a name="see-also"></a>Lásd még:

A példa bemutatja, hogyan futtathat konfigurációk kezdeti állítja a szolgáltatás használatához, tekintse meg a [DSC segítségével konfigurálhatja a virtuális gépek kezdeti állítja](bootstrapDsc.md).