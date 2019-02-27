---
title: A hibajelentési fogalmak |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- non-terminating errors [PowerShell SDK]
- errors [PowerShell SDK], described
- terminating errors [PowerShell SDK]
- errors [PowerShell SDK]
ms.assetid: 0dce97c0-bd9a-4691-8ca3-e8d5dea902c5
caps.latest.revision: 11
ms.openlocfilehash: aac6b7b6ac8a0fad15194b6d3f92c434524fabdb
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846164"
---
# <a name="error-reporting-concepts"></a>Hibajelentés – Fogalmak

Windows PowerShell biztosít, két mechanizmusok hibákat jelentő: egy mechanizmusa *megszakítást okozó hibák* és a egy másik mechanizmust *okozó*. Fontos a parancsmag hibák jelentéséhez megfelelően, hogy a megfelelő módon reagálhat, amelyen fut a parancsmagokat a gazdaalkalmazást.

A parancsmag meg kell hívnia a [System.Management.Automation.Cmdlet.Throwterminatingerror*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) módszer, ha hiba történik, amely nem létezik, vagy nem teszi lehetővé a parancsmagot, hogy a bemeneti objektumok feldolgozásához. A parancsmag meg kell hívnia a [System.Management.Automation.Cmdlet.Writeerror*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) okozó jelentés küldése, ha a parancsmag továbbra is a bemeneti objektumok feldolgozása metódust. Mindkét módszer adjon meg egy hiba rekordot, amely a gazdaalkalmazást a hiba okának kivizsgálására használható.

Az alábbi irányelvek segítségével meghatározhatja, hogy hiba a megszakítást okozó vagy megszakítást nem okozó hiba.

- Hiba a megszakító hiba esetén megakadályozza, hogy a parancsmag az aktuális objektum feldolgozása továbbra is, illetve további bemeneti objektumokat, függetlenül attól, hogy a tartalmat sikerült feldolgozása.

- Hiba megszakító hibát, ha nem szeretné, a parancsmag folytatja az aktuális objektum vagy bármilyen további bemeneti objektumokhoz, függetlenül attól, hogy a tartalmat feldolgozása.

- Hiba egy hibát, amely nem fogadja el vagy egy objektumot ad vissza a parancsmag a esetén vagy akkor következik be, amely fogad el, vagy csak egy objektumot ad vissza a parancsmag.

- Hiba történt egy nem megszakító hiba esetén folytatja a parancsmag az aktuális objektum és minden további bemeneti objektumot feldolgozása.

- Hiba történt egy nem megszakító hiba esetén kapcsolatos, adott bemeneti objektum vagy bemeneti objektumok részét.

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Cmdlet.Throwterminatingerror*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError)

[System.Management.Automation.Cmdlet.Writeerror*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError)

[Windows PowerShell Hibarekordjainak](./windows-powershell-error-records.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
