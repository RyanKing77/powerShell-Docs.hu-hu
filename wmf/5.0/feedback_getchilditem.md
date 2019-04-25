---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: cc5d2d799c1292f68de5fb2360fcba220c2c010b
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62085292"
---
# <a name="get-childitem-has--depth-parameter"></a>Get-ChildItem rendelkezik - Depth paraméterrel
**Get-ChildItem** most már rendelkezik egy **– mélysége** paraméter használata **– Recurse** a rekurzió korlátozása:

PS C:\\felhasználók\\slee\\letölti\\példa&gt; Get-ChildItem-Recurse - 0 mélysége

Könyvtár: C:\\felhasználók\\slee\\letölti\\példa

Mód LastWriteTime hosszúságú név

---- ------------- ------ ----

d---4/14/2015 17:36 közötti Depth0

-a---4/14/2015 1:19 PM 0 File1.txt

-a---4/14/2015 1:19 PM 0 fájl2.ref fájllal

-a---4/14/2015 1:19 PM 0 File3.txt

PS C:\\felhasználók\\slee\\letölti\\példa&gt; Get-ChildItem-Recurse - mélysége 1

Könyvtár: C:\\felhasználók\\slee\\letölti\\példa

Mód LastWriteTime hosszúságú név

---- ------------- ------ ----

d---4/14/2015 17:36 közötti Depth0

-a---4/14/2015 1:19 PM 0 File1.txt

-a---4/14/2015 1:19 PM 0 fájl2.ref fájllal

-a---4/14/2015 1:19 PM 0 File3.txt

Könyvtár: C:\\felhasználók\\slee\\letölti\\példa\\Depth0

Mód LastWriteTime hosszúságú név

---- ------------- ------ ----

d---4/14/2015 Délután 5:33 Depth1
