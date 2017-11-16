---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 4185d9395f2f3e5ba1c8daa0c365cb2bf322936b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
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

