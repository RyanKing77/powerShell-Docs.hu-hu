---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Objektumok eltávolítása az adatcsatornából Where-Object
ms.assetid: 01df8b22-2d22-4e2c-a18d-c004cd3cc284
ms.openlocfilehash: c060b93a3823be26ad6c7757acc633bb4fc2fcfa
ms.sourcegitcommit: 01ac77cd0b00e4e5e964504563a9212e8002e5e0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/07/2018
ms.locfileid: "39587142"
---
# <a name="removing-objects-from-the-pipeline-where-object"></a>Objektumok eltávolítása az adatcsatornából (Where-Object)

A Windows PowerShellben Ön gyakran hozza létre és azt szeretné, hogy egy folyamat több objektum adják át. Adott lehetőségével szűkítheti a megjelenített objektumok tulajdonságait is megadhat a **formátum** parancsmagok, de ez nem segíthetnek a probléma, és a teljes objektumok eltávolítása. Érdemes a folyamat vége előtt-objektumok szűrése, így elvégezhető műveletek a kezdetben által létrehozott objektumok egy részhalmazára.

Windows PowerShell tartalmaz egy `Where-Object` parancsmagot, amely lehetővé teszi, hogy a folyamat minden egyes objektum tesztelése, és csak azt adják át a folyamat megfelel egy adott teszt feltételt. Objektumok, amelyek nem adnak át a vizsgálat a folyamat törlődnek. A feltétel értékeként adja meg a `Where-Object` **FilterScript** paraméter.

### <a name="performing-simple-tests-with-where-object"></a>A Where-Object egyszerű tesztek végrehajtása

Értékét **FilterScript** van egy *parancsfájlblokkban* – egy vagy több Windows PowerShell-parancsok csúcsos zárójelek között {} –, amely kiértékeli a true vagy FALSE (hamis). Lehet, hogy a parancsfájl-blokkokban nagyon egyszerű, de tudomása a másik a Windows PowerShell-fogalmat, összehasonlító operátorok hozza létre őket igényel. Egy összehasonlító operátor hasonlítja össze az egyes oldalán megjelenő elemek. Összehasonlító operátorok kezdődik a "-" karakter, és a egy neve követi. Alapszintű összehasonlító operátorok szinte bármilyen típusú objektumot működik. A speciális összehasonlító operátorok csak a szöveges vagy tömbök előfordulhat, hogy működik.

> [!NOTE]
> Alapesetben, amikor szöveg dolgozik a Windows PowerShell összehasonlító operátorok nincsenek megkülönböztetve.

Megfontolandó szempontok elemzés, mert szimbólumokat <>, például és = összehasonlító operátorok nem képeznek. Ehelyett összehasonlító operátorok rétegből betűt. Az alapszintű összehasonlító operátorok az alábbi táblázatban láthatók.

|Összehasonlító operátor|Jelentés|Példa (igaz értéket ad vissza)|
|-----------------------|-----------|--------------------------|
|-eq|egyenlő|1 - eq 1|
|-ne|Nem egyenlő|1 - ne 2|
|-lt|a kisebb, mint|1 – lt 2|
|-le|Kisebb vagy egyenlő|1 – le 2|
|-gt|nagyobb, mint|2 – gt 1|
|-ge|Nagyobb vagy egyenlő|2 -ge 1|
|– például a|Hasonló (helyettesítő összehasonlítás szöveg)|"file.doc" – például "f\*.do?"|
|-notlike|Nem hasonló (helyettesítő összehasonlítás szöveg)|"file.doc"-notlike "p\*.doc"|
|-tartalmaz|tartalmaz|1,2,3 – 1 tartalmaz|
|-notcontains|nem tartalmazza|1,2,3 - notcontains 4|

Where-Object parancsfájl-blokkokban használja a speciális változó `$_` , tekintse meg a folyamat az aktuális objektum. Íme egy példa annak működését. Ha rendelkezik egy számokból álló listát, és csak be szeretné olvasni azokat, amelyek kevesebb mint 3, használhatja a Where-Object számok szűréséhez írja be:

```
PS> 1,2,3,4 | Where-Object -FilterScript {$_ -lt 3}
1
2
```

### <a name="filtering-based-on-object-properties"></a>Szűrés alapján objektum tulajdonságai

Mivel `$_` hivatkozik a jelenlegi folyamat objektumba, elérheti a tulajdonságait a tesztek.

Például hogy megtekinthessük WMI Win32_SystemDriver osztályt. Előfordulhat, hogy a rendszer-illesztőprogramok egy adott rendszer több száz, de Ön csak hasznos lehet egy adott készletét a rendszer-illesztőprogramok, például azok, amelyek jelenleg futnak. Ha a Get-Member Win32_SystemDriver tagok megtekintéséhez használja (**Get-WmiObject – osztály Win32_SystemDriver |} Get-Member - MemberType tulajdonság**) látni fogja, hogy a megfelelő tulajdonság állapotát, és, hogy az illesztőprogram futtatásakor az "Fut" értékkel rendelkezik. A rendszer-illesztőprogramok, jelölje ki a kívánt csak futó beírásával szűrheti:

```powershell
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq 'Running'}
```

Ez egy hosszú listában továbbra is hoz létre. Előfordulhat, hogy szeretné szűrni, csak az illesztőprogramokat a StartMode értéket is tesztelésével automatikus indításra állítva:

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

Ez olyan biztosít, amely nagy mennyiségű információt, hogy már nincs szüksége, mivel tudjuk, hogy, hogy futnak-e az illesztőprogramok. Sőt valószínűleg kell ezen a ponton csak annyi információ a nevét és megjelenítendő nevét. A következő parancs csak két tulajdonságot, ami sokkal egyszerűbb kimeneti tartalmazza:

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

Két Where-Object-elemek a fenti parancsban, de azok kifejezhető egyetlen Where-Object elem használatával a - és logikai operátor szerinti szűrése, ehhez hasonló:

```powershell
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript { ($_.State -eq 'Running') -and ($_.StartMode -eq 'Manual') } | Format-Table -Property Name,DisplayName
```

A standard szintű logikai operátorokat az alábbi táblázatban láthatók.

|Logikai operátor|Jelentés|Példa (igaz értéket ad vissza)|
|--------------------|-----------|--------------------------|
|- és|Logikai és; IGAZ, ha mindkét oldal igaz|(1 - eq (1.) - és (2 - eq 2).|
|- vagy|Logikai vagy; IGAZ, ha bármelyik oldal igaz|(1 - eq 1) – vagy (1 - eq 2).|
|-nem|Logikai not; Megfordítja a true és false|-nem (1 - eq 2)|
|\!|Logikai not; Megfordítja a true és false|\!(1 - eq 2)|
