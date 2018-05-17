---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: d9f1ca10c948b06b234e17f688b8f899ed41c5d6
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
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
