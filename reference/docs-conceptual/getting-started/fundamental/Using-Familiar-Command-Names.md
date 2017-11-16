---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Jól ismert parancs nevek használata"
ms.assetid: 021e2424-c64e-4fa5-aa98-aa6405758d5d
ms.openlocfilehash: 5e72e721bdb9d48684092344a0169907e7e25d40
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="using-familiar-command-names"></a>Jól ismert parancs nevek használata
Egy olyan mechanizmus használatával nevű *aliasképző*, a Windows PowerShell segítségével a felhasználók alternatív névvel parancsok hivatkozik. Aliasképző élmény a felhasználók közös parancs nevét, amely már ismerik a Windows PowerShell hasonló műveletek végrehajtásához újból más ismertetése lehetővé teszi. Bár nem ismertetjük részletesen Windows PowerShell-aliasokat, továbbra is használhatja őket, a Windows PowerShell-lel használatának első lépéseit.

Aliasképző beírt parancsnév társít egy másik parancsba is. Például a Windows PowerShell rendelkezik egy belső függvény **Clear-állomás** , amely törli a kimeneti ablakban. Ha akár a **cls** vagy **törölje** parancsot egy parancssorba, a Windows PowerShell parancs értelmezi, hogy ez az alias a **Clear-állomás** funkciót, és futtatja a  **Törölje az állomás** függvény.

Ez a szolgáltatás segít a felhasználóknak további Windows PowerShell. Első, a legtöbb Cmd.exe és a UNIX felhasználók rendelkeznek-e, hogy a felhasználók már tudja nevű parancsok nagy repertoire, és bár a Windows PowerShell alakokat nem lehet azonos eredményt adnak, elég közel használó felhasználók őket anélkül, hogy a munka formában először memorize a Windows PowerShell-neveket. Második a fő eljárás megzavarását az új felület esetén a felhasználó már ismeri a másik rendszerhéj forrása "ujját memória" által okozott hibákat. Ha a Cmd.exe használt évig, ha a kimenet teljes képernyős, és törölni szeretné azt, reflexively írja be a **cls** parancsot, és nyomja le az ENTER billentyűt. Az alias nélkül a **Clear-állomás** funkció a Windows PowerShellben, egyszerűen számíthat a hibaüzenet a következő "**"cls"nem ismerhető fel egy parancsmag, function, futtatható program vagy parancsfájl.**" és nem meghatározni, hogy mi a teendő, törölje a kimeneti kell hagyni.

A következő a közös Cmd.exe és UNIX-parancsok Windows PowerShell belül használható rövid listáját:

|||||
|-|-|-|-|
|cat|Dir|csatlakoztatása|erőforrás-kezelő|
|CD-ről|echo|Helyezze át|rmdir|
|chdir|tartalmának végleges törlése|popd|alvó állapot|
|Törölje a jelet|H|PS|Rendezés|
|CLS|Előzmények|pushd|TEE|
|Másolás|Kill|pwd|típus|
|del|LP|R|írási|
|diff|Ls|ren||

Ha ezek egyike segítségével reflexively parancsokat, és szeretné megtanulni a natív Windows PowerShell-paranccsal valódi nevét, használja a **Get-Alias** parancs:

```
PS> Get-Alias cls

CommandType     Name                            Definition
-----------     ----                            ----------
Alias           cls                             Clear-Host
```

Olvashatóbbá példák, a Windows PowerShell felhasználói útmutatója általában Ezzel elkerülheti alias. Azonban több tudomása aliasok ez korai továbbra is lehet hasznos, ha a Windows PowerShell-kód más forrásból származó tetszőleges kódtöredékek dolgozik, vagy saját aliasok meghatározhat. Ez a szakasz a többi szabványos aliasok és hogyan adhat meg a saját aliasok ismertetik.

### <a name="interpreting-standard-aliases"></a>Standard aliasok értelmezése
Ellentétben a fent említett aliasok tervezett egyéb felületek név-kompatibilisek, a Windows PowerShell épített aliasok általában tervezett kivonatosan mutatja. A rövidebb nevek gyorsan írható, de nem lehet olvasni, ha nem tudja, mit hivatkoznak.

A Windows PowerShell megpróbálja kedvezőtlenül között az érthetőség és kivonatosan mutatja, adja meg a standard aliasok rövid szintaxist nevek a gyakori műveletek és főnevek alapuló készlete. Ez lehetővé teszi, hogy egy közös parancsmagokat olvasható amikor tudja, hogy a rövid szintaxist nevek aliasok sor. Például a standard aliasok művelet **beolvasása** rövidítése **g**, a művelet **beállítása** rövidítése **s**, a főnév **Elem** rövidítése **i**, a főnév **hely** rövidítése **l**, és a parancs rövidítése főnév**cm**.

Ez a következő példa mutatja be, ennek működéséről. A Get-cikk szabványos aliasa származik egyesítő **g** a Get és **i** elem: **gi**. A Set-cikk szabványos aliasa származik egyesítő **s** készlet és **i** elem: **si**. A Get-hely normál alias származik egyesítő **g** a Get és **l** helyen **főkönyvi**. A hely beállítása a szabványos aliasa származik egyesítő **s** készlet és **l** helyen **l**. A Get-Command szabványos aliasa származik egyesítő **g** a Get és **cm** parancs, **gcm**. Nincs Set-Command parancsmaggal van, de ha vannak, azt tudná kitalálja, hogy a szabványos alias származik **s** készlet és **cm** parancshoz: **scm**. Ezenkívül a Windows PowerShell aliassal való ellátását, akik előforduló ismernie személyek **scm** tudná kitalálja, hogy az alias Set-parancs hivatkozik.

### <a name="creating-new-aliases"></a>Új aliasok létrehozása
A saját aliasok a Set-Alias parancsmaggal hozhat létre. A következő utasítás például a szabványos aliasok értelmezése ismertetett szabványos parancsmag-aliasok létrehozása:

```
Set-Alias -Name gi -Value Get-Item
Set-Alias -Name si -Value Set-Item
Set-Alias -Name gl -Value Get-Location
Set-Alias -Name sl -Value Set-Location
Set-Alias -Name gcm -Value Get-Command
```

Belső a Windows PowerShell parancsokat hasonló indításakor használja, de ezek aliasok a következők nem módosítható. Ha megpróbálja ténylegesen hajtható végre az alábbi parancsok egyikét, elérhetővé válik a arról tájékoztat, hogy az alias nem lehet módosítani. Például:

```
PS> Set-Alias -Name gi -Value Get-Item
Set-Alias : Alias is not writeable because alias gi is read-only or constant and cannot be written to.
At line:1 char:10
+ Set-Alias  <<<< -Name gi -Value Get-Item
```

