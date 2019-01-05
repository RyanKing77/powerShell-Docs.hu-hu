---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC archív erőforrás
ms.openlocfilehash: d5ccd242d000a0907c6768f30923764be6bf20a3
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048432"
---
# <a name="dsc-archive-resource"></a>DSC archív erőforrás

> Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

Az archív erőforrás a Windows PowerShell Desired State Configuration (DSC), csomagolja ki az archív (.zip kiterjesztésű) fájlok egy adott elérési úton mechanizmust biztosít.

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
| Cél| Itt adhatja meg a helyet, ahol szeretne biztosítani, ki kell olvasni az archívum tartalmát.|
| Elérési út| Forrás elérési utat határozza meg az archív fájl.|
| __Ellenőrzőösszeg__| Határozza meg, amely meghatározza, hogy-e az azonos két fájlt használni kívánt típusát. Ha __ellenőrzőösszeg__ nincs megadva, csak a fájl vagy könyvtár nevét használja az összehasonlítást. Érvényes értékek a következők: Az SHA-1, SHA-256, SHA-512, createdDate, modifiedDate, egyik sem (alapértelmezett). Ha megad __ellenőrzőösszeg__ nélkül __ellenőrzése__, a konfigurálása sikertelen lesz.|
| Győződjön meg, hogy| Határozza meg, ellenőrizze, hogy az archívum tartalmát a __cél__. Ez a tulajdonság beállítása __jelen__ annak érdekében, hogy a tartalom létezik. Állítsa be __távol__ annak érdekében, még nem léteznek. Az alapértelmezett érték __jelen__.|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például, ha az erőforrás konfigurációs parancsprogram-blokkot, amelyet futtatni szeretne azonosítója először ResourceName és a típus azt __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.|
| Ellenőrzése| Az ellenőrzőösszeg-tulajdonság segítségével határozza meg, ha az archívum megfelel-e az aláírás. Az ellenőrzőösszeg érvényesítése nélkül adja meg, ha a konfiguráció sikertelen lesz. Ha ellenőrzése ellenőrzőösszeg nélkül adja meg, SHA-256 ellenőrzőösszeg alapértelmezett használják.|
| Force| Bizonyos fájl műveletek (például fájl felülírása vagy egy nem üres könyvtár törlése) hibát eredményez. A kényszerített tulajdonságot felülbírálja az ilyen hibák. Az alapértelmezett érték: False.|

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan biztosíthatja, hogy létezik Test.zip nevű archív fájl tartalmát, és egy adott célhelyen ki kell olvasni az archív erőforrás használatára.

```
Archive ArchiveExample {
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Path = "C:\Users\Public\Documents\Test.zip"
    Destination = "C:\Users\Public\Documents\ExtractionPath"
}
```