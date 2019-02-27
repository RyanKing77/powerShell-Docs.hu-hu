---
title: A parancsmag aliasok |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d0d70864-33fb-49ce-8054-c41ba19fd554
caps.latest.revision: 11
ms.openlocfilehash: 32f45702cc0d28e6652ef61ebdbe085291013408
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849965"
---
# <a name="cmdlet-aliases"></a>Parancsmagaliasok

A parancsmag aliasok használatával a parancsmag felhasználói élmény javítása érdekében. A gyakran használt parancsmagok csökkentésére, írja be, és hogy egyszerűbb legyen teljes körű feladatok gyors aliasok is hozzáadhat. A parancsmagok beépített aliasok is felvehet, vagy a felhasználók megadhatják a saját egyéni aliasok.

Ha például a [Get-Command](/powershell/module/microsoft.powershell.core/get-command) parancsmag rendelkezik egy beépített `gcm` alias. Az aliasok adhat hozzá parancsnevek más nyelvekre, hogy a felhasználók nem rendelkeznek a további új parancsokat használhatja.

## <a name="alias-guidelines"></a>Alias irányelvek

A parancsmagok beépített aliasok létrehozásakor kövesse az alábbi irányelveket:

- Mielőtt aliasok rendeli, indítsa el a Windows Powershellt, és futtassa a [Get-Alias](/powershell/module/Microsoft.PowerShell.Utility/Get-Alias) parancsmaggal ellenőrizheti, az aliasokat, amely már használatban van.

- Például egy aliast előtagot, amely hivatkozik a műveletet, a parancsmag neve és a egy aliast utótaggal, amely hivatkozik a főnév, a parancsmag neve tartalmazza. Alias például a `Import-Module` parancsmag "ipmo". Minden művelet, és az aliasokat listáját lásd: [parancsmag-utasítások](./approved-verbs-for-windows-powershell-commands.md).

- Parancsmagok esetében, amelyek az ugyanazon művelet például alias ugyanazon előtaggal. Az aliasok minden a Windows PowerShell-parancsmagok, amelyek a "Get" műveletet a neve például a "g" előtagot használja.

- Parancsmagok esetében, amelyek az ugyanazon főnév tartalmazza az ugyanazon alias-utótagot. Például az összes Windows PowerShell-parancsmagok, amelyek rendelkeznek a neve a "Munkamenet" főnév aliasok használja a "sn" utótag.

- Parancsmagok esetében, egyenértékű parancsok más nyelven a parancs nevét használja.

- Általánosságban elmondható győződjön meg a lehető legrövidebb aliasok. Ellenőrizze, hogy az alias a művelethez legalább egy eltérő karaktert és a egy különálló karakter a főnév rendelkezik. Adja hozzá az alias egyediségének biztosítása érdekében szükség szerint több karaktert.

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
