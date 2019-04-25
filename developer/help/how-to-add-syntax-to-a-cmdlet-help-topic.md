---
title: Szintaxis egy parancsmag Súgó-témakör hozzáadása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d0c6d03f-1c1a-43d8-928e-e3290e90e0bc
caps.latest.revision: 5
ms.openlocfilehash: 2e9dbc9ff8f9507f2008cd6e114ba6fec36b10bf
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083382"
---
# <a name="how-to-add-syntax-to-a-cmdlet-help-topic"></a>Szintaxis hozzáadása egy parancsmagokkal kapcsolatos súgótémakörhöz

- [A paraméter-attribútumok](#Parameter-Attributes)

- [A paraméter értéke attribútumok](#Parameter-Value-Attributes)

- [Szintaxis-információk gyűjtése](#Gathering-Syntax-Information)

- [Kódolási Szintaxisdiagramja XML](#Coding-the-Syntax-Diagram-XML)

## <a name="things-to-know-about-the-syntax-diagram-in-cmdlet-help"></a>Tudnivaló a parancsmag súgóját Szintaxisdiagramja kapcsolatban

Olvassa el ezt a szakaszt, hogy milyen típusú adatok törlése képet kapjon a parancsmag súgójában szintaxisdiagramja XML-kód megkezdése előtt meg kell adnia, például a paraméter-attribútumok és hogyan jelenjen meg az adatokat a szintaxisdiagramja...

### <a name="parameter-attributes"></a>A paraméter-attribútumok

- Szükséges

  - Igaz értéke esetén a paraméter szerepelnie kell minden parancs, amely a paraméterkészletet használja.

  - Ha FALSE (hamis), a paraméter nem kötelező minden parancs, amely a paraméterkészletet használja.

- Beosztás

  - Ha a neve, a paraméter nevének megadása kötelező.

  - A Helyzetbeállító, ha a paraméter neve nem kötelező. Ha ki van hagyva, a paraméter értéke a parancsban megadott helyen kell lennie. Például ha az érték pozíció = "1", a paraméter értékét kell lennie az első vagy csak névtelen paraméter értéke a parancsban.

- Adatcsatorna bemenetének

  - Ha az értéke igaz (ByValue), akkor is lehet adatcsatornán bemenetet átadni a paramétert. A bemeneti társítva ("köthető az") az a paraméter, akkor is, ha a tulajdonság nevét és az objektum típusa nem egyezik a várt típus. A Windows PowerShell? a paraméter kötelező összetevők próbálja meg a megfelelő típusú a bemenet átalakítása és a parancs csak akkor, amikor a típus nem konvertálható. A paraméterkészlet csak egy paraméter értéke hozzá lehet rendelni.

  - Ha az értéke igaz (ByPropertyName), akkor is lehet adatcsatornán bemenetet átadni a paramétert. Azonban a bemeneti társítva a paraméter csak akkor, ha a paraméter neve megegyezik-e a bemeneti objektum olyan osztályát. Például, ha a paraméter neve `Path`, irányíthatja át a parancsmag objektum arra a paraméterre társítva, csak akkor, amikor az objektum elérési útja nevű tulajdonsággal rendelkezik.

  - Ha a bemeneti paraméteréhez adatcsatornán keresztül tulajdonság neve vagy értéke igaz (ByValue, ByPropertyName). A paraméterkészlet csak egy paraméter értéke hozzá lehet rendelni.

  - Ha hamis, akkor a paraméter bemenete nem kanálu.

- Helyettesítés

  - Ha az értéke igaz, a felhasználó beír a paraméter értékeként a szöveg tartalmazhat helyettesítő karaktereket is.

  - Ha nem, a felhasználó beír a paraméter értékeként a szöveg nem tartalmazhat helyettesítő karaktereket.

### <a name="parameter-value-attributes"></a>A paraméter értéke attribútumok

- Szükséges

  - Amennyiben az értéke igaz, a megadott értéket kell használni, amikor egy paraméter használatával.

  - Ha nem, a paraméter értéke nem kötelező. Általában egy értéket nem kötelező, csak akkor, ha egyike több érvényes értékei a paramétert, mint például a sorszámozott típus.

Hodnota parametru szükséges attribútuma eltér a paraméter kötelező attribútum.

A paraméter kötelező attribútum jelzi-e a paraméter (és annak értékét) kell foglalni a parancsmag meghívásakor. Ezzel szemben a paraméter értéke a kötelező attribútum csak akkor, ha a paraméter tartalmazza a parancs szolgál. Azt jelzi, hogy adott értékkel a paraméterrel együtt kell használni.

Általában, hogy a rendszer a helyőrzők paraméterértékek szükségesek, és szövegkonstans paraméterértékeket nem szükségesek, mivel azok, amelyeket lehet, hogy a paraméter együtt több érték egyikét.

### <a name="gathering-syntax-information"></a>Szintaxis-információk gyűjtése

1. Indítsa el a parancsmag neve.

   ```
   SYNTAX
       Get-Tech
   ```

2. A parancsmag a paraméterek listája. Írja be a kötőjel (más néven "kötőjel" vagy "mínusz" (ASCII 45) előtt minden paraméter neve. A paraméterek szét paraméterkészlettel (egyes parancsmagok beállítása csak egyetlen paraméterrel rendelkezhet). A Get, csúcskategóriás műszaki példánkban ez a parancsmag két paraméterkészlettel rendelkezik.

   ```
   SYNTAX
       Get-Tech -name -type
       Get-Tech -ID -list -type
   ```

   Indítsa el az egyes parancsmag nevű paramétert.

   Az alapértelmezett paraméter első listája. Az alapértelmezett paraméter nincs megadva, a parancsmag osztály alapján.

   Minden egyes paraméterkészletet listázza egyedi paramétereként először, kivéve ha pozícióparaméterek kell elsőként jelennek meg. Az előző példában a neve és azonosítója paraméterei a két paraméterkészlettel egyedi paramétereket (a minden egyes paraméterkészletet musí mít jeden parametr, amely egyedi az adott paraméter). Így megkönnyítheti a felhasználók azonosítására, hogy milyen paramétert, akkor meg kell adnia a paraméter beállítása.

   A megadott sorrendben szerepelniük kell a parancs a paraméterek listája. Sorrendje nem számít, ha a kapcsolódó paraméterekkel együtt listában, vagy először lista a leggyakrabban használt paraméterek.

   Győződjön meg arról, a WhatIf és Confirm paraméter listázásához, ha a parancsmag támogatja a ShouldProcess.

   A következő általános paramétereket (például a Verbose, a hibakeresési és ErrorAction) a szintaxis diagramon nem szerepelhet. A `Get-Help` parancsmag hozzáadja ezt az információt, amikor megjeleníti a Súgó-témakör.

3. Adja hozzá a paraméterértékeket. A Windows PowerShell?, a .NET-típus paraméter értékét képviseli. Azonban a típusnév rövidíthető, például a "string" System.String.

   ```
   SYNTAX
       Get-Tech -name string -type basic advanced
       Get-Tech -ID int -list -type basic advanced
   ```

   Mindaddig, amíg azok jelentését nincs bejelölve, például "string" System.String és "int" System.Int32, rövidítése típusokat.

   A listában szereplő összes enumerálások, például az "alapszintű" vagy "speciális" való beállítása az előző példában a - típusú paramétert.

   Váltson a paraméterek, például - lista az előző példában szereplő, nem rendelkezik az értékekkel.

4. Adja hozzá a csúcsos zárójeleket helyőrző, mint a korábban megszokott literálok paraméterértékeket paraméterek értékeket.

   ```
   SYNTAX
       Get-Tech -name <string> -type basic advanced
       Get-Tech -ID <int> -list -type basic advanced
   ```

5. Nem kötelező paraméterek és azok értékeket foglaljuk szögletes zárójelek közé.

   ```
   SYNTAX
       Get-Tech -name <string> [-type basic advanced]
       Get-Tech -ID <int> [-list] [-type basic advanced]
   ```

6. Választható paraméterek nevei (a pozicionális paramétereknél) foglaljuk szögletes zárójelek közé. A name paraméterek csak pozíciórekord, például a következő példában a Name paraméter esetében nem kell a parancsban benne lennie.

   ```
   SYNTAX
       Get-Tech [-name] <string> [-type basic advanced]
       Get-Tech -ID <int> [-list] [-type basic advanced]
   ```

7. Ha egy paraméterérték tartalmazhat több érték a Name paraméter, a nevek listája például szögletes zárójelek között, a paraméter értéke a következő két hozzáadása.

   ```
   SYNTAX
       Get-Tech [-name] <string[]> [-type basic advanced]
       Get-Tech -ID <int[]> [-list] [-type basic advanced]
   ```

8. Ha a felhasználó kiválaszthat a paraméterek vagy a paraméterértékeket, például a típus paraméternél tegye a választási lehetőségek kapcsos zárójelek közé, és válassza el őket a kizárólagos vagy symbol(;).

   ```
   SYNTAX
       Get-Tech [-name] <string[]> [-type {basic | advanced}]
       Get-Tech -ID <int[]> [-list] [-type {basic | advanced}]
   ```

9. Ha a paraméter értékét kell használnia adott formázás, idézőjelek vagy zárójelben, például a szintaxis megjelenítése formátumban.

   ```
   SYNTAX
       Get-Tech [-name] <"string[]"> [-type {basic | advanced}]
       Get-Tech -ID <int[]> [-list] [-type {basic | advanced}]
   ```

## <a name="coding-the-syntax-diagram-xml"></a>Kódolási Szintaxisdiagramja XML

A leírás csomópont vége után azonnal megkezdődik a szintaxis csomópont XML-kód a \</maml:description > címke. Szintaxisdiagramja használja az adatok összegyűjtésével kapcsolatban lásd: [szintaxis információk összegyűjtéséhez](#Gathering-Syntax-Information).

### <a name="adding-a-syntax-node"></a>Szintaxis csomópont hozzáadása

Az adatokból az XML-fájl szintaktikai csomópontjában jelenik meg a parancsmag súgó-témakörének szintaxisdiagramja jön létre. A szintaxis csomópont idézőjelek között egy pár, ha \<parancsszintaxist: > címkéket. Az egyes paraméterkészletet, a parancsmag egy idézőjelbe foglalt \<parancs: syntaxitem > címkéket. Nem korlátozott számú \<parancs: syntaxitem > címkéket adhat hozzá.

Az alábbi példa bemutatja egy szintaxis csomópont, amely szintaxis elem csomópontok két paraméterkészlettel rendelkezik.

```xml
<command:syntax>
  <command:syntaxItem>
    ...
    <!--Parameter Set 1 (default parameter set) parameters go here-->
    ...
  </command:syntaxItem>
  <command:syntaxItem>
    ...
    <!--Parameter Set 2 parameters go here-->
    ...
  </command:syntaxItem>
</command:syntax>
```

### <a name="adding-the-cmdlet-name-to-the-parameter-set-data"></a>Adatok hozzáadása a parancsmag Name paraméteréhez beállítása

Minden egyes paraméterkészletet, a parancsmag szintaxisa elem csomópont van megadva. Minden egyes szintaxis elem csomópont párjai kezdődik \<maml:name > címkék, amely tartalmazza annak a parancsmagnak a nevét.

Az alábbi példában megtalálhatja, amely rendelkezik a szintaxis-elem csomópont két paraméterkészlettel szintaxis csomópont.

```xml
<command:syntax>
  <command:syntaxItem>
    <maml:name>Cmdlet-Name</maml:name>
  </command:syntaxItem>
  <command:syntaxItem>
    <maml:name>Cmdlet-Name</maml:name>
  </command:syntaxItem>
</command:syntax>
```

### <a name="adding-parameters"></a>Paraméterek hozzáadása

Minden egyes paraméter, a szintaxis elem csomópont van megadva egy \<parancsparaméter: > címkéket. Egy kulcspárra van szüksége \<parancsparaméter: > címke szerepel a paraméterkészletet, a következő általános paramétereket, amelyek a Windows PowerShell által biztosított kivételével minden paraméter?.

A nyitó attribútumai \<parancsparaméter: > címke határozza meg, hogyan jelenjen meg a paraméter szintaxisdiagramja. A paraméter-attribútumok kapcsolatos információkért lásd: [paraméter-attribútumok](#Parameter-Attributes).

> [!NOTE]
> A \<parancsparaméter: > címke támogatja a gyermekelem \<maml:description > tartalmú soha nem jelenik meg. A paraméterek leírásait meg van adva a paraméter csomópont XML-kód. A szintaxis elem található információk közötti inkonzisztencia elkerülése érdekében bodes és a paraméter csomópont, hagyja ki a (\<maml:description >, vagy hagyja üresen.

Az alábbi példa egy két paraméterrel rendelkező paraméter szintaxisa elem csomópont tartalmaz.

```xml
<command:syntaxItem>
  <maml:name>Cmdlet-Name</maml:name>
  <command:parameter required="true" globbing="true"
    pipelineInput="true (ByValue)" position="1">
    <maml:name>ParameterName1</maml:name>
    <command:parameterValue required="true">
      string[]
    </command:parameterValue>
  </command:parameter>
  <command:parameter required="true" globbing="true"
    pipelineInput="true (ByPropertyName)">
    <maml:name>ParameterName2</maml:name>
    <command:parameterValue required="true">
      int32[]
    </command:parameterValue>
  </command:parameter>
</command:syntaxItem>
```
