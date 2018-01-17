---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: DSCAutomationHostEnabled registry key
ms.openlocfilehash: c58b7a8f2485ff02f09763749a3de8a75f882d19
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
>A következőkre vonatkozik: a Windows PowerShell 5.0

# <a name="dscautomationhostenabled-registry-key"></a>DSCAutomationHostEnabled registry key

DSC használja a **DSCAutomationHostEnabled** kulcs alatt **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** ahhoz, hogy a kezdeti állítja a gép konfigurációját.
DSCAutomationHostEnabled három módot támogat:

|  DSCAutomationHostEnabled Value  |  Leírás   | 
|---|---| 
0 | Tiltsa le a gép konfigurál állítja. |
1 | Engedélyezze a gép konfigurál állítja. |
2 | A gép konfigurálása, csak ha DSC engedélyezése folyamatban lévő vagy a jelenlegi állapot. Ez az alapértelmezett érték. |

## <a name="see-also"></a>Lásd még:

A példa bemutatja, hogyan futtathat konfigurációk kezdeti állítja a szolgáltatás használatához, tekintse meg a [DSC segítségével konfigurálhatja a virtuális gépek kezdeti állítja](bootstrapDsc.md).


