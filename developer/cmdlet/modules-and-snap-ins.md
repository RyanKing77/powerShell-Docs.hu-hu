---
title: Modulok és beépülő modulok |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2d342f91-23e0-467f-8de2-f9657d820693
caps.latest.revision: 6
ms.openlocfilehash: 157cd64e286392f3fd770e1e34542682b1e63625
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067620"
---
# <a name="modules-and-snap-ins"></a>Modulok és beépülő modulok

Parancsmagok modulok (bevezetett Windows PowerShell 2.0-s) vagy a beépülő modulok használata a munkamenet lehet hozzáadni. Miután hozzáadta a parancsmag futtatása programozott módon egy fogadó alkalmazás vagy a parancssorból interaktív módon a munkamenet.

Javasoljuk, hogy a modulok parancsmagok hozzáadása a munkamenet a következő okok miatt a kézbesítési módszerként használja:

- Modulok adhat hozzá parancsmagok által a szerelvény betöltése során, a parancsmag van definiálva. Hiba esetén nem kell egy beépülő modul osztály megvalósításához.

- Modulok adhat hozzá más erőforrások, például a változókat, függvények, parancsfájlok, típusok és formázási fájlok és több.

- Beépülő modulok segítségével csak parancsmagok és szolgáltatók hozzáadása a munkamenethez.

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-modul írása](../module/writing-a-windows-powershell-module.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
