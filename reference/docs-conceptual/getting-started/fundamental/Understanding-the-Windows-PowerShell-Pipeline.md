---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A Windows PowerShell kimenetátirányítási mechanizmusával ismertetése"
ms.assetid: 6be50926-7943-4ef7-9499-4490d72a63fb
ms.openlocfilehash: 6d152e52d2fcfb9dd592eb9ac40500615f2186cb
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="understanding-the-windows-powershell-pipeline"></a>A Windows PowerShell kimenetátirányítási mechanizmusával ismertetése
Átirányítás gyakorlatilag tetszőleges helyszínről a Windows PowerShell működik. Bár a képernyőn látható szöveg, a Windows PowerShell a szöveges parancsok között nem csövön keresztüli. Ehelyett azt kiszolgálókészletéhez objektumok.

A notation szállítására hasonlít más ismertetése a használt, így első ránézésre nem lehet nyilvánvaló, hogy a Windows PowerShell bevezet egy új. Például, ha használja a **kimenő gazdagép** lap-lap megjeleníti a kimeneti csak egy másik parancsba is, a kimeneti keresi a force parancsmagot, például a normál szöveget a képernyőn látható, lapok lebontva:

```
PS> Get-ChildItem -Path C:\WINDOWS\System32 | Out-Host -Paging

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS\system32

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2005-10-22  11:04 PM        315 $winnt$.inf
-a---        2004-08-04   8:00 AM      68608 access.cpl
-a---        2004-08-04   8:00 AM      64512 acctres.dll
-a---        2004-08-04   8:00 AM     183808 accwiz.exe
-a---        2004-08-04   8:00 AM      61952 acelpdec.ax
-a---        2004-08-04   8:00 AM     129536 acledit.dll
-a---        2004-08-04   8:00 AM     114688 aclui.dll
-a---        2004-08-04   8:00 AM     194048 activeds.dll
-a---        2004-08-04   8:00 AM     111104 activeds.tlb
-a---        2004-08-04   8:00 AM       4096 actmovie.exe
-a---        2004-08-04   8:00 AM     101888 actxprxy.dll
-a---        2003-02-21   6:50 PM     143150 admgmt.msc
-a---        2006-01-25   3:35 PM      53760 admparse.dll
<SPACE> next page; <CR> next line; Q quit
...
```

A Out-Host-lapozást parancs esetén hasznos csővezeték tényező, valahányszor lassan megjeleníteni kívánt hosszadalmas kimenet van. Akkor különösen hasznos, ha a művelet nagyon processzorigényes. Mivel feldolgozási átkerül a kimenő futtatni a parancsmagot akkor is rendelkezik teljes készen áll a megjelenítése, ha azt megelőző az adatcsatorna parancsmagok halt művelet mindaddig, amíg a kimenet a következő oldalon érhető el. Erre úgy tekinthet, a Windows Feladatkezelő figyelése Processzor- és használja a Windows PowerShell használatakor.

A következő parancsot: **Get-ChildItem C:\\Windows-Recurse**. Hasonlítsa össze a parancs a Processzor- és memóriahasználatról: **Get-ChildItem C:\\Windows-Recurse |} Kimenő gazdagép-lapozást**. Mi a képernyőn látható szöveg, de, mert a szükséges objektumokat képviseli a konzolablakban szövegként. Ez az imént a megjelenítése, hogy mit valóban abba az írást, a Windows PowerShell belül. Vegye figyelembe például a Get-hely parancsmagot. Ha **Get-hely** amíg tartózkodási helyéhez a C meghajtó gyökérkönyvtárában, akkor jelenik meg a következő kimeneti:

```
PS> Get-Location

Path
----
C:\
```

A Windows PowerShell futószalagos szöveg, ha a parancs kiadása például **Get-hely |} Kimenő gazdagép**, átadása akkor **Get-hely** való **kimenő gazdagép** karakterek képernyőn megjelenésük sorrendjében. Más szóval, amelyeket a rendszer figyelmen kívül hagyja a fejlécadatokat **kimenő gazdagép** először kapja a karakter "**C"**, majd a karakter "**:"**, majd a karakter " **\\'**. A **kimenő gazdagép** parancsmag nem tudta megállapítani, mely tehát a karakterek kimenete társítandó a **Get-hely** parancsmag.

Ahhoz, hogy egy folyamat parancsok szöveg helyett kommunikálnak, a Windows PowerShell-objektumokat használ. A felhasználók szempontjából az objektumok kapcsolódó információkat, amelyek segítségével könnyebben egységként adatok kezelésére formába csomagot, majd bontsa ki a kívánt elemeket.

A **Get-hely** parancs nem ad vissza, amely tartalmazza az aktuális útvonalon szöveg. Nevű ismeretek adja vissza egy **PathInfo** objektum, amely tartalmazza az aktuális útvonalon néhány egyéb információk mellett. A **kimenő gazdagép** parancsmag ezután elküldi a **PathInfo** a képernyő, és a Windows PowerShell-objektum úgy dönt, hogy mi megjelenítendő adatok és hogyan kell megjelenítenie a formázási szabályok alapján.

Valójában a fejlécadatokat kimenetét az a **Get-hely** parancsmag csak a folyamat végén a képernyőn megjelenő megjelenített adatok formázási folyamat részeként kerül. Megjelenő képernyőn van információk összegzését, és a kimeneti objektum nem a teljes megjelenítése.

Fényében, hogy előfordulhat, hogy egy parancs, mint mi látható ablakban jelenik meg a konzolon, hogyan lehet Windows PowerShell kimenete további információk lekérése az nem látható elemek? Miként jelenjenek meg a további adatokat? És mi történik, ha azt szeretné, az adatok megtekintéséhez eltér a egy Windows PowerShell formátuma általában?

A többi Ez a fejezet ismerteti, hogyan felderítené az adott Windows PowerShell objektumok szerkezete meghatározott elemek kijelölése és formázási azokat könnyebben megjelenítési, és ezek az információk küldése az alternatív kimeneti helyekre, mint a fájlok és nyomtatók.

