---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC-fájl erőforrás
ms.openlocfilehash: 86a5dcd97b4163b3780038c815d3de5a523ce4bf
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34218943"
---
# <a name="dsc-file-resource"></a>A DSC-fájl erőforrás

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A fájl erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a célcsomóponton lévő fájlokat és mappákat kezeléséhez.

>**Megjegyzés:** Ha a **MatchSource** tulajdonsága **$false** (ez utóbbi érték az alapértelmezett érték), a tartalom másolása gyorsítótárba kerüljenek-e a konfiguráció alkalmazása először.
>A konfiguráció további alkalmazások nem fogják keresni az frissített fájlok és/vagy mappák által megadott útvonal **SourcePath**. Ha szeretné-e a fájlokat vagy mappákat a frissítések keresése **SourcePath** minden alkalommal, amikor a konfiguráció alkalmazása, állítsa be **MatchSource** való **$true**.

## <a name="syntax"></a>Szintaxis
```
File [string] #ResourceName
{
    DestinationPath = [string]
    [ Attributes = [string[]] { Archive | Hidden | ReadOnly | System }]
    [ Checksum = [string] { CreatedDate | ModifiedDate | SHA-1 | SHA-256 | SHA-512 } ]
    [ Contents = [string] ]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Force = [bool] ]
    [ Recurse = [bool] ]
    [ DependsOn = [string[]] ]
    [ SourcePath = [string] ]
    [ Type = [string] { Directory | File } ]
    [ MatchSource = [bool] ]
}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   |
|---|---|
| DestinationPath| Azt jelzi, hogy a hely hol szeretne biztosítani a fájlok vagy könyvtárak állapotát.|
| Attribútumok| Adja meg a kívánt állapot attribútumát a célként kijelölt fájl vagy könyvtár.|
| Ellenőrzőösszeg| Azt jelzi, hogy az ellenőrzőösszeg-típust használ annak meghatározása, hogy két fájlok megegyeznek. Ha __ellenőrzőösszeg__ nincs megadva, csak a fájl vagy könyvtár neve Összehasonlításképpen szolgál. Érvényes értékek a következők: SHA-1, SHA-256, SHA-512, createdDate, modifiedDate.|
| Tartalom| Adja meg a fájlt, például egy adott karakterláncot.|
| hitelesítő adatok| Azt jelzi, a hitelesítő adatokat, amelyek hozzáférését az erőforrásokhoz, például a forrásfájlokat, kötelező, ha ilyen hozzáférés szükséges.|
| Győződjön meg arról| Azt jelzi, hogy a fájl vagy könyvtár létezik-e. Állítsa be ezt a tulajdonságot "Hiányzik", annak érdekében, hogy a fájl vagy könyvtár nem létezik. Állítsa az értékét "Elérhető" Győződjön meg arról, hogy a fájl vagy könyvtár létezik. Az alapértelmezett érték az "Elérhető".|
| Force| Egyes fájl műveletek (például a fájl felülírása vagy egy nem üres könyvtár törlése) hibát eredményez. A kényszerített tulajdonság használatával felülbírálja az ilyen hibák. Az alapértelmezett érték __$false__.|
| Recurse| Azt jelzi, ha-e adva alkönyvtárak. Ez a tulajdonság beállítása __$true__ annak jelzésére, hogy szeretné-e alkönyvtárakat is meg lehet adni. Az alapértelmezett érték __$false__. **Megjegyzés:**: Ez a tulajdonság csak akkor érvényes, ha a Type tulajdonság beállítása könyvtárba.|
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.|
| SourcePath| Azt jelzi, hogy az elérési útja, amelyből a fájl vagy mappa erőforrás másolása.|
| Típus| Azt jelzi, hogy az erőforrás konfigurálva-e egy könyvtár vagy fájl. Ez azt jelzi, hogy az erőforrás egy könyvtár "Directory" tulajdonság értéke. Állítsa az értékét "File" azt jelzi, hogy az erőforrás egy fájlt. Az alapértelmezett érték: "File".|
| MatchSource| Ha az alapértelmezett érték beállítása __$false__, majd a forrás (azaz fájlokat A, B és C) lévő fájlok nem kerülnek be a cél a konfiguráció alkalmazása először. Ha egy új fájl (D) kerül a forrás-, az fog nem vehető fel a cél, akkor is, ha a konfiguráció alkalmazása újra később. Ha az érték __$true__, akkor minden alkalommal, amikor a konfiguráció alkalmazása, ezt követően a forrás (például D fájl ebben a példában) található új fájlokat vesznek fel a cél felé. Az alapértelmezett érték **$false**.|

## <a name="example"></a>Példa

A következő példa bemutatja, hogyan használja a fájl erőforrás annak érdekében, hogy egy könyvtárat az elérési úttal rendelkező `C:\Users\Public\Documents\DSCDemo\DemoSource` a forrás (például a "pull") a számítógépen megtalálható is (valamint minden alkönyvtár) célcsomóponton. Egy megerősítő üzenet naplóba írás, ha a teljes és a annak érdekében, hogy fut-e a fájl-ellenőrzés művelet előtt a naplózási művelet egy utasítást tartalmaz.

```powershell
Configuration FileResourceDemo
{
    Node "localhost"
    {
        File DirectoryCopy
        {
            Ensure = "Present"  # You can also set Ensure to "Absent"
            Type = "Directory" # Default is "File".
            Recurse = $true # Ensure presence of subdirectories, too
            SourcePath = "C:\Users\Public\Documents\DSCDemo\DemoSource"
            DestinationPath = "C:\Users\Public\Documents\DSCDemo\DemoDestination"
        }

        Log AfterDirectoryCopy
        {
            # The message below gets written to the Microsoft-Windows-Desired State Configuration/Analytic log
            Message = "Finished running the file resource with ID DirectoryCopy"
            DependsOn = "[File]DirectoryCopy" # This means run "DirectoryCopy" first.
        }
    }
}
```