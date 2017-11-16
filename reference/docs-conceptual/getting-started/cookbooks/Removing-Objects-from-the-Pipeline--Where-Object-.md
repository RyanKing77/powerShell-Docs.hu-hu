---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Objektumok eltávolítása a feldolgozási sor az adott objektum"
ms.assetid: 01df8b22-2d22-4e2c-a18d-c004cd3cc284
ms.openlocfilehash: 4140c4c3ebb26223d03ca139992fedf6e184a38b
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="removing-objects-from-the-pipeline-where-object"></a>Objektumok eltávolítása a láncból (Where-Object)
A Windows PowerShellben Ön gyakran hozza létre és adják át a több objektumot egy folyamat szükségesnél. Megadhatja, hogy a megjelenített adott objektumoknak azon tulajdonságait a **formátum** parancsmagok, de ez nem segíthetnek a probléma által megjelenített teljes objektumokat eltávolításával. Érdemes lehet egy sorban, végéig-objektumok szűrése a így műveleteket tudják végrehajtani a kezdetben által létrehozott objektumok csak egy részét.

A Windows PowerShell tartalmaz egy **Where-Object** parancsmag, amely lehetővé teszi az egyes objektumok tesztelése a folyamat, és csak adja át a feldolgozási sor mentén ha megfelel-e egy adott feltétel. A teszt nem továbbítja objektumok el lesznek távolítva a folyamatot. A feltétel értékeként adja meg a **Where-ObjectFilterScript** paraméter.

### <a name="performing-simple-tests-with-where-object"></a>A Where-Object egyszerű tesztek végrehajtása
Értékének **FilterScript** van egy *parancsfájlblokkban* - egy vagy több Windows PowerShell-parancsok csúcsos zárójelek {} között -, amely kiértékelésének eredménye true vagy false. Lehet, hogy a parancsfájl-blokkokban nagyon egyszerű, de szükséges hozza létre őket egy másik Windows PowerShell koncepció összehasonlító operátorok tudomása. Egy összehasonlító operátor mindkét oldalán megjelenő elemek hasonlítja össze. Összehasonlító operátorok kezdődhet a "-" karakter, és van egy neve követ. Alapszintű összehasonlító operátorok működik a szinte bármilyen típusú objektumot. A speciális összehasonlító operátorok csak lehet, hogy működni szöveg vagy tömb.

> [!NOTE]
> Alapértelmezés szerint az szöveg használatakor a Windows PowerShell összehasonlító operátorok értékek azonban nem.

Szempontok elemzése, mert szimbólumok szerepelhetnek, például <>, és = összehasonlító operátorok nem használatosak. Ehelyett összehasonlító operátorok rétegből betűket. Az alapvető összehasonlító operátorok a következő táblázatban láthatók.

|Összehasonlító operátor|Jelentés|(Igaz) – Példa|
|-----------------------|-----------|--------------------------|
|-eq|egyenlő|1 - eq 1|
|-ne|Nem egyenlő|1 - ne 2|
|-lt|Értéke kisebb, mint|1 - lt 2|
|-le|Kisebb vagy egyenlő, mint|1 – le 2|
|-gt|Nagyobb, mint|2 - gt 1|
|-ge|Nagyobb vagy egyenlő|2 -ge 1|
|– például a|Olyan, mint (helyettesítő szöveg a összehasonlítását)|"file.doc" – például a "f\*.do?"|
|-notlike|Nincs (a szöveg helyettesítő összehasonlítását) például|"file.doc"-notlike "p\*.doc"|
|-tartalmaz|tartalmazza|1,2,3 - 1 tartalmazza|
|-notcontains|Nem tartalmaz|1,2,3 - notcontains 4|

Where-Object parancsfájlblokkokban a '$_' speciális változó segítségével tekintse meg a folyamat az aktuális objektum. Íme egy példa annak működéséről. Ha számokból álló listát, és csak a meglévők közül, amelyek kevesebb mint 3 vissza szeretné, Where-Object segítségével írja be a számok szűrése:

```
PS> 1,2,3,4 | Where-Object -FilterScript {$_ -lt 3}
1
2
```

### <a name="filtering-based-on-object-properties"></a>Szűrés alapján objektum tulajdonságai
Az aktuális folyamat objektum $_ hivatkozik, azt a tesztek érhessék el a tulajdonságai.

Tegyük fel azt is megtekinthetik a Win32_SystemDriver osztály a WMI-ben. Előfordulhat, hogy egy adott rendszer illesztőprogramja több száz, de csak érdekelheti a rendszer-illesztőprogramok, például azokkal, amely jelenleg fut egy adott készletét. Ha a Get-tag Win32_SystemDriver tagok megtekintéséhez használja (**Get-WmiObject – osztály Win32_SystemDriver |} Get-Member - MemberType tulajdonsága**) jelenik meg, hogy a megfelelő tulajdonság állapotát, és, hogy az illesztőprogram futtatásakor "Fut" értékkel rendelkezik. Szűrheti a rendszer illesztőprogramokat, írja be a csak a futó ők kiválasztása:

```
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"}
```

Ez továbbra is szolgáltat hosszú listáját. Előfordulhat, hogy szűrni kívánt csak jelölje be az illesztőprogramok által a StartMode értéket is vizsgálati automatikus indításra állítva:

```
PS> Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"} | Where-Object -FilterScript {$_.StartMode -eq "Auto"}

DisplayName : RAS Asynchronous Media Driver
Name        : AsyncMac
State       : Running
Status      : OK
Started     : True

DisplayName : Audio Stub Driver
Name        : audstub
State       : Running
Status      : OK
Started     : True
```

Ez biztosítja, nagy mennyiségű információt azt már nem szükséges, mert tudjuk, hogy fut-e az illesztőprogramok. Az egyetlen adat valószínűleg kell ezen a ponton, nevét és megjelenítendő nevét. A következő parancs csak két tulajdonságokhoz, így sokkal egyszerűbb kimeneti tartalmazza:

```
PS> Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"} | Where-Object -FilterScript {$_.StartMode -eq "Manual"} | Format-Table -Property Name,DisplayName

Name                                    DisplayName
----                                    -----------
AsyncMac                                RAS Asynchronous Media Driver
Fdc                                     Floppy Disk Controller Driver
Flpydisk                                Floppy Disk Driver
Gpc                                     Generic Packet Classifier
IpNat                                   IP Network Address Translator
mouhid                                  Mouse HID Driver
MRxDAV                                  WebDav Client Redirector
mssmbios                                Microsoft System Management BIOS Driver
```

A fenti parancsban két Where-Object-eleme van, de ezek lehetnek a Where-Object elemet használatával a - és logikai operátor, ehhez hasonló:

```
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript { ($_.State -eq "Running") -and ($_.StartMode -eq "Manual") } | Format-Table -Property Name,DisplayName
```

A szabványos logikai operátorok a következő táblázatban láthatók.

|Logikai operátor|Jelentés|(Igaz) – Példa|
|--------------------|-----------|--------------------------|
|- és|Logikai és; Igaz kétoldalas teljesülése esetén|(1 - eq 1.) - és (2 - eq 2).|
|- vagy|Logikai vagy; IGAZ, ha bármelyik oldal igaz|(1 - eq 1) – vagy (1 - eq 2).|
|-nem|Logikai nem; Megfordítja a true és false|-nem (1 - eq 2)|
|\!|Logikai nem; Megfordítja a true és false|\!(1 - eq 2)|

