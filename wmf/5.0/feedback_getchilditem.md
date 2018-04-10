---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 62cccabd7c63c6ba928fc2bf8addd3d11483e90f
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="get-childitem-has--depth-parameter"></a>Get-ChildItem - mélysége paraméterrel rendelkezik
**Get-ChildItem** most már rendelkezik egy **– mélysége** paraméter használata **– Recurse** a rekurzió korlátozása:

PS C:\\felhasználók\\slee\\letölti\\példa&gt; Get-ChildItem-Recurse - mélysége 0

Könyvtár: C:\\felhasználók\\slee\\letölti\\– példa

Mód LastWriteTime hossza név

---- ------------- ------ ----

d---4 14 / / 2015 5:36 du Depth0

-a---4/14/2015 1:19 PM 0 File1.txt

-a---4/14/2015 1:19 PM 0 fájl2.ref fájllal

-a---4/14/2015 1:19 PM 0 File3.txt

PS C:\\felhasználók\\slee\\letölti\\példa&gt; Get-ChildItem-Recurse - mélysége 1

Könyvtár: C:\\felhasználók\\slee\\letölti\\– példa

Mód LastWriteTime hossza név

---- ------------- ------ ----

d---4 14 / / 2015 5:36 du Depth0

-a---4/14/2015 1:19 PM 0 File1.txt

-a---4/14/2015 1:19 PM 0 fájl2.ref fájllal

-a---4/14/2015 1:19 PM 0 File3.txt

Könyvtár: C:\\felhasználók\\slee\\letölti\\példa\\Depth0

Mód LastWriteTime hossza név

---- ------------- ------ ----

d---4 14 / / 2015 5:33 PM Depth1