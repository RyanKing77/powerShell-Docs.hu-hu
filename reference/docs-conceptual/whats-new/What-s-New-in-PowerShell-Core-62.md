---
title: A PowerShell Core 6.2 újdonságai
description: Új szolgáltatásaival és módosításaival, amely a PowerShell Core 6.2
ms.date: 03/28/2019
ms.openlocfilehash: 2224d23a244175059a705c07001e8ad8d6ab3aa0
ms.sourcegitcommit: 8dd4394cf867005a8b9ef0bb74b744c964fbc332
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/30/2019
ms.locfileid: "58750033"
---
# <a name="whats-new-in-powershell-core-62"></a>A PowerShell Core 6.2 újdonságai

Alább néhány fontos új szolgáltatásokat és módosításokat vezettek be a PowerShell Core 6.2 egy kijelölt van.

Is **tonna** "unalmas szolgáltatáshasználatot", amelyek gyorsabb és stabilabb (és sok és számos hibajavítás) PowerShell!
Változások teljes listájához tekintse meg a [a Githubon változásnaplójában](https://github.com/PowerShell/PowerShell/blob/master/CHANGELOG.md).

És közben ki az alábbi néhány nevet nevezzük, Köszönjük, hogy [összes a közösségi közreműködők](https://github.com/PowerShell/PowerShell/graphs/contributors) , amely ebben a kiadásban lehetővé tenni.

## <a name="engine-updates-and-fixes"></a>A motor-frissítések és javítások

- Adja hozzá a PowerShell távoli eljáráshívás engedélyezését vagy letiltását a parancsmag a figyelmeztető üzenetek ([#9203][])
- Javítás a `FormatTable` távoli deszerializálás regressziós ([#9116][])
- Frissítse a feladatalapú `async` PowerShell-lel közvetlenül egy feladat objektumot ad vissza hozzáadott API-k ([#9079][])
- Adja hozzá az 5 `InvokeAsync` túlterheléssel és `StopAsync` , a `PowerShell` típusa ([#8056][]) (Köszönjük, hogy @KirkMunro!)

## <a name="general-cmdlet-updates-and-fixes"></a>Általános parancsmag frissítések és javítások

- Engedélyezése `SecureString` parancsmagok a Windows tárolja az egyszerű szöveg ([#9199][])
- Adja hozzá az elavult üzenetet `Send-MailMessage` ([#9178][])
- Javítsa ki `Restart-Computer` dolgozhatnak `localhost` amikor a Rendszerfelügyeleti webszolgáltatások nem szerepel ([#9160][])
- Győződjön meg arról, `Start-Job` throw hibát, ha a PowerShell üzemeltetési ([#9128][])
- -Es frissítési verziója `PowerShell.Native` és tesztek üzemeltetésére ([#8983][])

## <a name="breaking-changes"></a>Kompatibilitástörő változások

Javítsa ki a - NoEnumerate viselkedése konzisztens, a Windows PowerShell Write-Output ([#9069][]) (Köszönjük, hogy @vexx32!)

<!-- Link references -->
[#8056]: https://github.com/PowerShell/PowerShell/pull/8056
[#8983]: https://github.com/PowerShell/PowerShell/pull/8983
[#9069]: https://github.com/PowerShell/PowerShell/pull/9069
[#9079]: https://github.com/PowerShell/PowerShell/pull/9079
[#9116]: https://github.com/PowerShell/PowerShell/pull/9116
[#9128]: https://github.com/PowerShell/PowerShell/pull/9128
[#9160]: https://github.com/PowerShell/PowerShell/pull/9160
[#9178]: https://github.com/PowerShell/PowerShell/pull/9178
[#9199]: https://github.com/PowerShell/PowerShell/pull/9199
[#9203]: https://github.com/PowerShell/PowerShell/pull/9203
