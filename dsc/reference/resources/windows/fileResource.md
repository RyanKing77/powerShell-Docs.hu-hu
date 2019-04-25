---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-File erőforrás
ms.openlocfilehash: b5bc2c305b8cfccbd044274811df631264a24279
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62077330"
---
# <a name="dsc-file-resource"></a>DSC-File erőforrás

> A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

A fájl erőforrás a Windows PowerShell Desired State Configuration (DSC) lehetővé teszi a fájlok és mappák célcsomóponton kezeléséhez. A **DestinationPath** és **SourcePath** mindkét által elérhetőnek kell lennie a cél csomópont.

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

|Tulajdonság       |Leírás                                                                   |Szükséges|Alapértelmezett|
|---------------|------------------------------------------------------------------------------|--------|-------|
|DestinationPath|A helyre, a cél csomóponton szeretne biztosítani a `Present` vagy `Absent`.|Igen|Nem|
|Attribútumok     |A kívánt állapotra a célként megadott fájl vagy könyvtár attribútumait. Érvényes értékek a következők **archív**, **Hidden**, **ReadOnly**, és **rendszer**.|Nem|Egyik sem|
|Ellenőrzőösszeg      |Annak meghatározása,-e az azonos két fájlt használandó ellenőrzőösszeg típusa. Érvényes értékek a következők: Az SHA-1, SHA-256, SHA-512, createdDate, modifiedDate.|Nem|A rendszer összehasonlítja a csak a fájl vagy könyvtár nevét.|
|Tartalom       |Csak akkor érvényes, ha a használt `File` típusa. Azt jelzi, ellenőrizze, hogy a tartalom `Present` vagy `Absent` a célként megadott fájlból. |Nem|Egyik sem|
|Hitelesítő adatok     |A hitelesítő adatokat, amelyek szükségesek a hozzáférési erőforrások, például a forrásfájlok.|Nem|A célcsomópont számítógépfiókja. (*lásd a megjegyzést*)|
|Győződjön meg, hogy         |A célként megadott fájl vagy könyvtár a kívánt állapotra. |Nem|**Jelen van**|
|Force          |Felülbírálja a hozzáférés-műveletek (például fájl felülírása vagy egy nem üres könyvtár törlése) hibát eredményez.|Nem|`$false`|
|Parancs recurse kapcsolójának        |Csak akkor érvényes, ha a használt `Directory` típusa. Az állapot művelet rekurzív módon alkönyvtáraiban hajt végre.|Nem|`$false`|
|DependsOn      |Megadott erőforrás(ok) függőség beállítása. Ehhez az erőforráshoz csak akkor futnak, minden függő erőforrások sikeres végrehajtása után. Megadhatja a tőle függő erőforrások, a szintaxis használatával `"[ResourceType]ResourceName"`. Lásd: [about_DependsOn](../../../configurations/resource-depends-on.md)|Nem|Egyik sem|
|SourcePath     |Az elérési út, amelyről a fájl vagy mappa erőforrás másolásához.|Nem|Egyik sem|
|Típus           |A konfigurált erőforrás típusát. Érvényes értékek a következők `Directory` és `File`.|Nem|`File`|
|MatchSource    |Azt határozza meg, ha az erőforrás kell figyelnie a forráskönyvtár a kezdeti másolat után hozzáadott új fájlokat. Érték `$true` azt jelzi, hogy a kezdeti másolat után új forrásfájlokat kell másolni, hogy a célhelyen. Ha beállítása `$False`, az erőforrás gyorsítótárazza a forráskönyvtár tartalmát, és figyelmen kívül hagyja a kezdeti másolat után hozzáadott fájlokat.|Nem|`$false`|

> [!WARNING]
> Ha nem ad meg értéket `Credential` vagy `PSRunAsCredential` (PS még az V.5), az erőforrás eléréséhez fog használni a számítógépfiókot a célcsomópont a `SourcePath`.  Ha a `SourcePath` egy UNC-megosztásnevet, ez "Hozzáférés megtagadva" hibaüzenetet eredményezhet. Ellenőrizze, hogy az engedélyek megfelelően vannak beállítva, vagy használja a `Credential` vagy `PSRunAsCredential` tulajdonságokat adja meg a fiókot kell használni.

## <a name="present-vs-absent"></a>Jelenlegi vs. Nincs jelen

Az egyes DSC-erőforrások számára megadott érték alapján különböző műveleteket hajtja végre, a `Ensure` tulajdonság. Az értékeket adja meg a fenti tulajdonságokat határozza meg, az állapot műveletet végrehajtani.

### <a name="existence"></a>Létezik-e

Csak megadása egy `DestinationPath`, az erőforrás biztosítja, hogy létezik-e az elérési út (`Present`) vagy nem létezik (`Absent`).

### <a name="copy-operations"></a>Másolási műveletek

Beállítás megadása egy `SourcePath` és a egy `DestinationPath` együtt egy `Type` értékét **Directory**, az erőforrás-másolatok forrás elérési utat a könyvtár. A Tulajdonságok `Recurse`, `Force`, és `MatchSource` másolási művelet típusának módosítása hajtja végre, miközben `Credential` határozza meg, melyik fiókot szeretné használni a forrás-könyvtár eléréséhez.

### <a name="limitations"></a>Korlátozások

Ha a megadott érték `ReadOnly` a a `Attributes` tulajdonság mellett egy `DestinationPath`, `Ensure = "Present"` kell létrehoznia az elérési útvonal, közben `Contents` állíthatja be a fájl tartalmát.  Egy `Absent` állapotbetöltési művelet lenne figyelmen kívül a `Attributes` tulajdonság teljesen, és távolítsa el minden olyan fájlt a megadott elérési úton.

## <a name="example"></a>Példa

Az alábbi példa másol egy könyvtárat és annak almappáiba egy lekéréses kiszolgálót egy célcsomóponttal a fájl erőforrás használatával. Ha a művelet sikeres, a Log erőforrás egy megerősítő üzenetet ír az eseménynaplóba.

A forráskönyvtár egy UNC elérési út (`\\PullServer\DemoSource`) megosztott a lekérési kiszolgálóról. A `Recurse` tulajdonság biztosítja, hogy minden alkönyvtár másolása is megtörténik.

> [!IMPORTANT]
> Az LCM Konfigurálása a célként megadott csomópontban alapértelmezés szerint a helyi rendszerfiók környezetében hajtja végre. Hozzáférést kell biztosítani a **SourcePath**, adjon a célcsomópont számítógép fiókja megfelelő engedélyekkel. A **Credential** és **PSDSCRunAsCredential** (v5) is módosíthatja a összefüggésben LCM a által használt eléréséhez a **SourcePath**. Önnek kell elvégeznie a fiókhoz használandó a hozzáférést a hozzáférést a **SourcePath**.

```powershell
Configuration FileResourceDemo
{
    Node "localhost"
    {
        File DirectoryCopy
        {
            Ensure = "Present" # Ensure the directory is Present on the target node.
            Type = "Directory" # The default is File.
            Recurse = $true # Recursively copy all subdirectories.
            SourcePath = "\\PullServer\DemoSource"
            DestinationPath = "C:\Users\Public\Documents\DSCDemo\DemoDestination"
        }

        Log AfterDirectoryCopy
        {
            # The message below gets written to the Microsoft-Windows-Desired State Configuration/Analytic log
            Message = "Finished running the file resource with ID DirectoryCopy"
            DependsOn = "[File]DirectoryCopy" # Depends on successful execution of the File resource.
        }
    }
}
```

További on használatára vonatkozó **hitelesítő adatok** DSC itt talál: [futtatása felhasználóként](../../../configurations/runAsUser.md) vagy [Config tartozó hitelesítő adatok](../../../configurations/configDataCredentials.md).
