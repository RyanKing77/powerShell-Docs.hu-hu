---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: A Windows PowerShell-nevek elsajátítása
ms.assetid: b4d0fd22-8298-4ee6-82ae-9b6f2907c986
ms.openlocfilehash: 381aa619a41ccacb2ff3a4cdbc2b75b7f04282d1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30953473"
---
# <a name="learning-windows-powershell-names"></a>A Windows PowerShell-nevek elsajátítása
Learning nevek a parancsok és a parancs paraméterei a legtöbb parancssori felületen jelentős mennyiségű időt befektetés. A probléma oka, hogy nincsenek nagyon kevés kombinációját, így az egyetlen lehetőség további megjegyzésével minden parancs és az egyes paramétereket, amelyek rendszeresen szüksége van.

Új parancsot vagy paraméter használata esetén nem általában használható már tapasztalatai; ki kell található, és ismerje meg, egy új nevet. Hogyan felületek nő a növekményes kiegészítésekkel eszközök egy kis készletét a működést tekinti meg, akkor egyszerűen miért nem szabványos van-e a struktúra. Parancs nevű különösen ez lehetséges, hogy hangkártya logikai mivel minden parancs egy olyan önálló eszköz, de nincs a parancsnév kezelésére fejlettebb módszert.

A legtöbb parancsok kezelése az operációs rendszer vagy az alkalmazások, például a szolgáltatások és a folyamatok elemeinek épülnek. A parancsok, amely, vagy előfordulhat, hogy nem felelnek meg a csomagcsalád nevét számos rendelkeznek. Például a Windows rendszereken is használhatja a **net start** és **net stop** parancsokat a szolgáltatás elindítása és leállítása. Egy másik általánosabb szolgáltatás vezérlő eszköz, amely egy teljesen más neve van Windows **sc**, amelyek nem felelnek meg az elnevezési minta a **nettó** parancsok szolgáltatás. A folyamat management, Windows van a **tasklist** lista folyamatok parancsot és a **taskkill** folyamatok leállítási parancsot.

Parancsok, paraméterek specifikációk szabálytalan paraméterrel rendelkezik. Nem használhatja a **net start** parancs használatával indítsa el a szolgáltatást egy távoli számítógépen. A **sc** parancs szolgáltatás indítása a távoli számítógépen, de a távoli számítógép megadásához a neve, dupla perjellel kell írni. Például egy távoli számítógépen DC01 nevű a nyomtatásisor-kezelő szolgáltatás elindításához kell beírni **sc \\ \\DC01 indítsa el a nyomtatásisor-kezelő**. Listára DC01 futó feladatok kell használnia a **/S** (a "rendszer") paraméter, és adjon meg fordított perjeleket, ilyen nélkül DC01 nevét: **tasklist /S DC01**.

Bár a szolgáltatás és a folyamat fontos műszaki különbség van, akkor példák mindkét számítógép kezelhető, amely jól meghatározott életciklusuk elemek. Érdemes lehet egy szolgáltatás vagy folyamat leállítása, illetve az összes jelenleg futó szolgáltatások és a folyamatok listáját. Ez azt jelenti annak ellenére, hogy a szolgáltatás és a folyamat különböző fogalom, egy szolgáltatás vagy folyamat végezzük a műveletek megegyeznek gyakran hasonlóak. Ezenkívül lehetősége biztosítjuk előfordulhat, hogy a művelet paraméterek megadásával testre fogalmilag hasonló lehet is.

A Windows PowerShell kihasználja ezeket az Hasonlóságok megismeréséhez és használatához a parancsmagok tudnia kell különböző nevek számának csökkentése érdekében.

### <a name="cmdlets-use-verb-noun-names-to-reduce-command-memorization"></a>Parancs Memorization csökkentése érdekében ige-főnév-nevek parancsmagok használata
A Windows PowerShell egy "ige-főnév" elnevezési rendszert használ, ahol minden parancsmag neve áll, egy szabványos művelet a megadott főnév kötőjellel. A Windows PowerShell-műveletek nem mindig angol műveleteket, de azokat a konkrét műveletek a Windows PowerShell express. Főnevek az alábbiak nagyon hasonlít bármilyen nyelven főnevek, fontos a rendszer felügyeleti objektumtípusok leírják. Is könnyen bemutatják, hogyan ezen kétrészes nevek csökkentheti néhány példa a műveletek és főnevek megtekintésével tanulási beavatkozást.

Főnevek az alábbiak kevesebb korlátozott, de kell mindig leírják mi parancs műveleteket végez. A Windows PowerShell parancsok, mint rendelkezik **Get-Process**, **Stop-Process**, **Get-Service**, és **Stop-Service**.

Két parancsokat és két műveletek esetében konzisztencia nem egyszerűsítése érdekében, hogy jelentős tanulási. Azonban 10 műveletek és 10 főnevek szabványos készletét tekinti meg, ha csak 20 szavak tudni majd rendelkezik, de listázzák segítségével 100 különböző parancsnév alkotnak.

Gyakran felismerje a parancs funkciója ehhez beolvassa a nevét, és általában nyilvánvaló milyen nevet használja a rendszer új parancsot. Például lehet, hogy a számítógép leállítási parancs **Stop-Computer**. Lehet, hogy a hálózat összes számítógép listája parancsot **Get-számítógép**. A parancs, amely lekérdezi a rendszerdátum **Get-Date**.

Minden olyan parancsok, amelyek tartalmazzák az adott művelet listázhatja a **-művelet** paramétere **Get-Command** (ismertetik **Get-Command** a következő szakasz részletesen). Például, hogy, hogy a művelet használata az összes parancsmag **beolvasása**, típus:

```
PS> Get-Command -Verb Get
CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Get-Acl                         Get-Acl [[-Path] <String[]>]...
Cmdlet          Get-Alias                       Get-Alias [[-Name] <String[]...
Cmdlet          Get-AuthenticodeSignature       Get-AuthenticodeSignature [-...
Cmdlet          Get-ChildItem                   Get-ChildItem [[-Path] <Stri...
...
```

A **-főnév** paraméter akkor hasznos, mivel lehetővé teszi, hogy családba tartozó parancsok, amelyek hatással vannak az azonos típusú objektum. Például ha meg szeretné tekinteni rendelkezésre álló parancsokat a szolgáltatások, a következő parancs típusa kezeléséhez:

```
PS> Get-Command -Noun Service
CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Get-Service                     Get-Service [[-Name] <String...
Cmdlet          New-Service                     New-Service [-Name] <String>...
Cmdlet          Restart-Service                 Restart-Service [-Name] <Str...
Cmdlet          Resume-Service                  Resume-Service [-Name] <Stri...
Cmdlet          Set-Service                     Set-Service [-Name] <String>...
Cmdlet          Start-Service                   Start-Service [-Name] <Strin...
Cmdlet          Stop-Service                    Stop-Service [-Name] <String...
Cmdlet          Suspend-Service                 Suspend-Service [-Name] <Str...
...
```

A parancs nincs feltétlenül, a parancsmag csak, mert egy ige-főnév elnevezési sémát tartalmaz. A natív Windows PowerShell-parancsot, amely nem parancsmag, de egy ige-főnév nevet, például a parancs való törlése a Clear-állomás a konzolablakban. A Clear-állomás parancs ténylegesen egy belső függvény, ahogyan azt láthatja, ha a Get-Command futtatnia rajta:

```
PS> Get-Command -Name Clear-Host

CommandType     Name                            Definition
-----------     ----                            ----------
Function        Clear-Host                      $spaceType = [System.Managem...
```

### <a name="cmdlets-use-standard-parameters"></a>Szabványos paraméterek parancsmagok használata
Ahogy azt korábban említettük, a hagyományos parancssori felületen használt parancsok általában nincs összhangban paraméter neve. Egyes esetekben paraméterek nincs neve minden. Ha így tesznek, azok gyakran karakterek vagy szavak gyorsan írható, de az új felhasználók által nem könnyen érthető rövidítése.

Ellentétben a legtöbb más hagyományos parancssori felületen Windows PowerShell paraméterek közvetlenül feldolgozza, és a paraméterek – fejlesztői útmutatás és a közvetlen hozzáférést paraméterneveknek normalizálnia használ. Bár ez nem garantálja, hogy minden parancsmag mindig megfelel az előírásoknak, akkor ez ösztönözze.

> [!NOTE]
> Paraméterek nevei mindig rendelkezik egy "-" $a számukra használatakor, engedélyezi a Windows PowerShell egyértelműen paraméterekként azonosításához. Az a **Get-Command - Clear-állomás neve** a példában a paraméter értéke **neve**, de módon van megadva: -**neve**.

Az alábbiakban néhány általános jellemzői a tanúsítványalgoritmusok és használatuk szabványos paraméterek nevei.

#### <a name="the-help-parameter-"></a>A Súgó paramétert (?)
Ha a a **-?** paramétert a parancsmaghoz, a parancsmag nem hajtotta végre. Ehelyett Windows PowerShell jeleníti meg a parancsmag súgóját.

#### <a name="common-parameters"></a>Az általános paraméterek
A Windows PowerShell néven több paraméterrel rendelkezik *közös paraméterek*. Ezek a paraméterek a Windows PowerShell-motor által vezérelt amikor ezek a parancsmag által megvalósított, mert azok mindig ugyanúgy működik. A közös paraméterek **WhatIf**, **megerősítése**, **részletes**, **Debug**, **figyelmeztetés**, **ErrorAction**, **ErrorVariable**, **OutVariable**, és **OutBuffer**.

#### <a name="suggested-parameters"></a>Javasolt paraméterek
A Windows PowerShell fő parancsmagjainak hasonló paraméterek szabványos neveket használja. Bár a paraméterneveknek használatát nem kényszeríti ki, nincs explicit útmutatás szabványosítás bátorítva használat.

Például az útmutató azt javasolja, hogy egy paraméter megnevezés vonatkozik a számítógép neve, mint amelyet **számítógépnév**, ahelyett, hogy a kiszolgáló, Host, rendszer, csomópont vagy egyéb gyakori alternatív szavakat. A fontos javasolt paraméter között a következők **kényszerített**, **kizárása**, **Include**, **PassThru**, **elérésiútja**, és **CaseSensitive**.