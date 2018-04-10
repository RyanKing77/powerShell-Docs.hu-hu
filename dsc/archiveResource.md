---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC-archívum erőforrás
ms.openlocfilehash: 1accd48f3862ee09b88d2792f9b7e5a7324bcf17
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-archive-resource"></a>A DSC-archívum erőforrás

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

Az archív erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a kicsomagolásához (.zip) archív fájlok egy adott elérési úton.

## <a name="syntax"></a>Szintaxis
```MOF
Archive [string] #ResourceName
{
    Destination = [string]
    Path = [string]
    [ Checksum = [string] { CreatedDate | ModifiedDate | SHA-1 | SHA-256 | SHA-512 } ]
    [ DependsOn = [string[]] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Force = [bool] ]
    [ Validate = [bool] ]
}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   |
|---|---|
| Cél| Adja meg a helyét az archív tartalom kibontása biztosításához.|
| Elérési út| Az archív fájl a forrás elérési útját adja meg.|
| __Ellenőrzőösszeg__| Annak meghatározása, hogy két fájlok megegyeznek használandó típust határozza meg. Ha __ellenőrzőösszeg__ nincs megadva, csak a fájl vagy könyvtár neve Összehasonlításképpen szolgál. Érvényes értékek a következők: SHA-1, SHA-256, SHA-512, createdDate, modifiedDate, nincs (alapértelmezett). Ha megad __ellenőrzőösszeg__ nélkül __ellenőrzése__, a konfiguráció sikertelen lesz.|
| Győződjön meg arról| Meghatározza, hogy ellenőrizze, hogy létezik-e a tartalom az archívum a __cél__. Ez a tulajdonság beállítása __jelen__ annak érdekében, hogy a tartalom található. Állítsa az értékét __távol__ annak érdekében, hogy azok nem léteznek. Az alapértelmezett érték __jelen__.|
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például ha erőforrás konfigurációs parancsprogram-blokk futtatni kívánt azonosító először ResourceName és annak típusára is __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.|
| Ellenőrzése| Az ellenőrzőösszeg-tulajdonság segítségével határozza meg, ha az archívum megfelel-e az aláírás. Ha megadja az ellenőrzőösszeg-érvényesítés nélkül, a konfiguráció sikertelen lesz. Ha megad nélkül ellenőrzőösszegének ellenőrzése, SHA-256 ellenőrzőösszeg alapértelmezett használja.|
| Force| Egyes fájl műveletek (például a fájl felülírása vagy egy nem üres könyvtár törlése) hibát eredményez. A kényszerített tulajdonság használatával felülbírálja az ilyen hibák. Az alapértelmezett értéke False.|

## <a name="example"></a>Példa

A következő példa bemutatja, hogyan használható az archív erőforrás győződjön meg arról, hogy egy Test.zip nevű archív fájl létezik-e, és ki kell olvasni a megadott célhelyen.

```
Archive ArchiveExample {
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Path = "C:\Users\Public\Documents\Test.zip"
    Destination = "C:\Users\Public\Documents\ExtractionPath"
}
```