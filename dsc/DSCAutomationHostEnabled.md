---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "DSCAutomationHostEnabled beállításkulcs"
ms.openlocfilehash: e47c929b366f93738343eabc431aab5a4428352d
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
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


