---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: DSCAutomationHostEnabled beállításkulcs
ms.openlocfilehash: 0cecbadc6802938cadb4ffb9745a23e6b98544be
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34221969"
---
>A következőkre vonatkozik: a Windows PowerShell 5.0

# <a name="dscautomationhostenabled-registry-key"></a>DSCAutomationHostEnabled beállításkulcs

DSC használja a **DSCAutomationHostEnabled** kulcs alatt **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** ahhoz, hogy a kezdeti állítja a gép konfigurációját.
DSCAutomationHostEnabled három módot támogat:

|  DSCAutomationHostEnabled érték  |  Leírás   |
|---|---|
0 | Tiltsa le a gép konfigurál állítja. |
1 | Engedélyezze a gép konfigurál állítja. |
2 | A gép konfigurálása, csak ha DSC engedélyezése folyamatban lévő vagy a jelenlegi állapot. Ez az alapértelmezett érték. |

## <a name="see-also"></a>Lásd még:

A példa bemutatja, hogyan futtathat konfigurációk kezdeti állítja a szolgáltatás használatához, tekintse meg a [DSC segítségével konfigurálhatja a virtuális gépek kezdeti állítja](bootstrapDsc.md).