---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-File erőforrás
ms.openlocfilehash: e5f7a91e5f19c8c7bbada090804d8f29a7cfedd5
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048523"
---
# <a name="dsc-file-resource"></a>DSC-File erőforrás

> Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

A fájl erőforrás a Windows PowerShell Desired State Configuration (DSC) lehetővé teszi a fájlok és mappák célcsomóponton kezeléséhez.

>**Megjegyzés:** Ha a **MatchSource** tulajdonsága **$false** (amely a az alapértelmezett érték), a tartalmát, másolja a gyorsítótárazza a rendszer először a konfiguráció alkalmazása.
>A konfiguráció további alkalmazásokat nem ellenőrzi a frissített fájlok és/vagy mappák által megadott útvonal **SourcePath**. Ha szeretné-e a fájlok és/vagy mappákat a frissítések keresése **SourcePath** minden alkalommal, amikor a konfigurációs van érvényben, állítsa be **MatchSource** való **$true**.

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
| DestinationPath| Azt jelzi, hogy a hely, ahol szeretne biztosítani egy fájl vagy könyvtár állapota.|
| Attribútumok| Itt adhatja meg a kívánt állapotra a célként megadott fájl vagy könyvtár attribútumait.|
| Ellenőrzőösszeg| Annak meghatározása,-e az azonos két fájlt használandó ellenőrzőösszeg típusát jelzi. Ha __ellenőrzőösszeg__ nincs megadva, csak a fájl vagy könyvtár nevét használja az összehasonlítást. Érvényes értékek a következők: Az SHA-1, SHA-256, SHA-512, createdDate, modifiedDate.|
| Tartalom| Itt adhatja meg, például egy adott karakterláncot egy fájl tartalmát.|
| Hitelesítő adatok| A hitelesítő adatokat, amelyek szükségesek a hozzáférési erőforrások, például a forrásfájlokat, azt jelzi, ha ilyen hozzáférésre szüksége.|
| Győződjön meg, hogy| Azt jelzi, hogy a fájl vagy könyvtár létezik-e. Állítsa be ezt a tulajdonságot a "Hiányzó" annak érdekében, hogy a fájl vagy könyvtár nem létezik. Állítsa a "E" Győződjön meg arról, hogy a fájl vagy könyvtár létezik. Az alapértelmezett érték "E".|
| Force| Bizonyos fájl műveletek (például fájl felülírása vagy egy nem üres könyvtár törlése) hibát eredményez. A kényszerített tulajdonságot felülbírálja az ilyen hibák. Az alapértelmezett érték __$false__.|
| Parancs recurse kapcsolójának| Azt jelzi, ha alkönyvtárakat tartalmaz. Ez a tulajdonság beállítása __$true__ jelzi, hogy szeretné-e alkönyvtárak fogja tartalmazni. Az alapértelmezett érték __$false__. **Megjegyzés:**: Ez a tulajdonság csak akkor érvényes, ha a tulajdonság beállítása könyvtárba.|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.|
| SourcePath| Azt jelzi, hogy az elérési utat, amelyről a fájl vagy mappa erőforrás másolásához.|
| Típus| Azt jelzi, hogy az erőforráshoz konfigurált egy könyvtárat vagy fájl. Ez azt jelzi, hogy az erőforrás egy könyvtárat a "Directory" tulajdonság értéke. Állítsa a "File" azt jelzi, hogy az erőforrás egy fájlt. Az alapértelmezett érték: "File".|
| MatchSource| Ha az alapértelmezett értékre állítva __$false__, majd a forrás (pl.: fájlok A, B és C) lévő fájlok az első alkalommal a konfiguráció alkalmazása hozzáadódik a célhelyen. (D) új fájl kerül, a forrás-, ha azt fogja nem vehető fel a cél, akkor is, ha a konfiguráció alkalmazása újra később. Ha az érték __$true__, akkor minden alkalommal, amikor a konfigurációs van érvényben, ezt követően a forrás (például D fájl ebben a példában) található új fájlokat adnak hozzá a célhelyen. Az alapértelmezett érték **$false**.|

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan használhatja a File resource annak érdekében, hogy egy könyvtárat az elérési útját `C:\Users\Public\Documents\DSCDemo\DemoSource` egy forrást a számítógépen (például a "PULL parancs" kiszolgáló) is jelen (együtt az összes alkönyvtár) célcsomóponton. Ez is egy megerősítő üzenetet írja a naplóba, amikor végzett és a egy nyilatkozatot, győződjön meg arról, hogy fut-e a fájl-ellenőrzés műveletet a naplózási művelet előtt.

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