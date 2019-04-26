---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Konfigurációs adatok használatával
ms.openlocfilehash: f2d25b9ced805fb4c91378ebfe840104eb6ce52a
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62080220"
---
# <a name="using-configuration-data-in-dsc"></a>A DSC használata a konfigurációs adatok

> A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

A beépített DSC használatával **ConfigurationData** paraméterrel határozhatja meg belül a konfigurációs adatokat.
Ez lehetővé teszi, hogy hozzon létre egy egyetlen konfigurációs több csomópont, vagy különböző környezetekben használható.
Például ha egy olyan alkalmazást fejleszt, is egy konfigurációs fejlesztési és éles környezetben is használja, és adja meg az adatokat az egyes környezetekhez a konfigurációs adatok használatával.

Ez a témakör ismerteti a szerkezete a **ConfigurationData** kivonattábla.
Konfigurációs adatok használatát bemutató példákért lásd [konfigurációs és környezeti adatok szétválasztása](separatingEnvData.md).

## <a name="the-configurationdata-common-parameter"></a>A gyakori ConfigurationData-paraméter

A DSC-konfiguráció paramétert egy közös, **ConfigurationData**, adjon meg mikor lefordítja a konfigurációt.
További információ a konfiguráció fordítása: [DSC-konfigurációk](configurations.md).

A **ConfigurationData** paraméter nevű legalább egy kulccsal kell rendelkeznie a szórótábla **AllNodes**.
Egy vagy több kulcsot is rendelkezhet.

> [!NOTE]
> Ebben a témakörben szereplő példák egy további kulcs használata (a megnevezett eltérő **AllNodes** kulcs) nevű `NonNodeData`, de tetszőleges számú további kulcsokat, és adja nekik bármilyen kívánt.

```powershell
$MyData =
@{
    AllNodes = @()
    NonNodeData = ""
}
```

Értékét a **AllNodes** kulcs egy tömb. A tömb egyes elemei is, hogy az legalább egy kulcsot egy kivonattáblát **csomópontnév**:

```powershell
$MyData =
@{
    AllNodes =
    @(
        @{
            NodeName = "VM-1"
        },


        @{
            NodeName = "VM-2"
        },


        @{
            NodeName = "VM-3"
        }
    );

    NonNodeData = ""
}
```

Más kulcsok minden egyes kivonattábla is hozzáadhat:

```powershell
$MyData =
@{
    AllNodes =
    @(
        @{
            NodeName = "VM-1"
            Role     = "WebServer"
        },


        @{
            NodeName = "VM-2"
            Role     = "SQLServer"
        },


        @{
            NodeName = "VM-3"
            Role     = "WebServer"
        }
    );

    NonNodeData = ""
}
```

Vlastnost összes csomópontjára érvényesek, tagja hozhat létre a **AllNodes** tömb, amely rendelkezik egy **csomópontnév** , `*`.
Például, hogy minden csomópont egy `LogPath` tulajdonságot használja, ezt megteheti:

```powershell
$MyData =
@{
    AllNodes =
    @(
        @{
            NodeName     = "*"
            LogPath      = "C:\Logs"
        },


        @{
            NodeName     = "VM-1"
            Role         = "WebServer"
            SiteContents = "C:\Site1"
            SiteName     = "Website1"
        },


        @{
            NodeName     = "VM-2"
            Role         = "SQLServer"
        },


        @{
            NodeName     = "VM-3"
            Role         = "WebServer"
            SiteContents = "C:\Site2"
            SiteName     = "Website3"
        }
    );
}
```

Ez megegyezik a hozzáad egy tulajdonságot nevű `LogPath` értékkel `"C:\Logs"` minden más blokkok (`VM-1`, `VM-2`, és `VM-3`).

## <a name="defining-the-configurationdata-hashtable"></a>A ConfigurationData kivonattábla meghatározása

Definiálhat **ConfigurationData** vagy változóként belül (ahogy az előző példákban) egy konfigurációs parancsfájl fájlt vagy egy különálló `.psd1` fájlt.
Meghatározásához **ConfigurationData** a egy `.psd1` hozzon létre egy fájlt, amely csak a kivonattábla kulcsa, amely a konfigurációs adatokat tartalmazza.

Például létrehozhat egy fájlt `MyData.psd1` a következő tartalommal:

```powershell
@{
    AllNodes =
    @(
        @{
            NodeName    = 'VM-1'
            FeatureName = 'Web-Server'
        },

        @{
            NodeName    = 'VM-2'
            FeatureName = 'Hyper-V'
        }
    )
}
```

## <a name="compiling-a-configuration-with-configuration-data"></a>A konfigurációs adatok-konfiguráció fordítása

Amely meghatározta a konfigurációs adatok konfiguráció fordítása, át kell adnia a konfigurációs adatok értékeként a **ConfigurationData** paraméter.

Ezzel létrehoz egy MOF-fájl minden bejegyzés esetében a **AllNodes** tömb.
Az egyes MOF-fájl neve lesz a `NodeName` a megfelelő tömb tétel tulajdonság.

Például, mint a konfigurációs adatok megadása a `MyData.psd1` fájlban a fenti fordításáról hozna létre a mindkét `VM-1.mof` és `VM-2.mof` fájlokat.

### <a name="compiling-a-configuration-with-configuration-data-using-a-variable"></a>A konfigurációs adatok változóval fordításáról

Konfigurációs adatok azonos változóként definiált használandó `.ps1` fájlt, a konfigurációt, át kell adnia a változó nevét értékeként a **ConfigurationData** paramétert, ha a konfiguráció fordítása:

```powershell
MyDscConfiguration -ConfigurationData $MyData
```

### <a name="compiling-a-configuration-with-configuration-data-using-a-data-file"></a>A konfigurációs adatok adatfájlt fordításáról

Egy .psd1 fájlban meghatározott konfigurációs adatokat használja, át kell adnia az elérési útját és nevét, hogy a fájl értékeként a **ConfigurationData** paramétert, ha a konfiguráció fordítása:

```powershell
MyDscConfiguration -ConfigurationData .\MyData.psd1
```

## <a name="using-configurationdata-variables-in-a-configuration"></a>Egy konfigurációs ConfigurationData változók használata

DSC biztosít a következő különleges változók konfigurációs parancsfájl használható:

- **$AllNodes** hivatkozik a teljes gyűjteményt a meghatározott csomópontok **ConfigurationData**. Szűrheti a **AllNodes** gyűjtemény használatával **. WHERE()** és **. ForEach()**.
- **ConfigurationData** hivatkozik a teljes kivonattáblában, amikor fordításáról átadott paraméterként.
- **MyTypeName** tartalmazza a [konfigurációs](configurations.md) használt változó neve. Például a konfigurációban `MyDscConfiguration`, a `$MyTypeName` fog rendelkezni a egy értéke `MyDscConfiguration`.
- **Csomópont** hivatkozik egy adott bejegyzést a **AllNodes** gyűjtemény után az szűrve van **. WHERE()** vagy **. ForEach()**.
  - Tudjon meg többet ezekről az eljárásokról a [about_arrays](/powershell/reference/3.0/Microsoft.PowerShell.Core/About/about_Arrays.md)

## <a name="using-non-node-data"></a>Nem csomópont adatait használatával

Ahogy megtudtuk, a korábbi példákban a **ConfigurationData** kivonattábla rendelkezhet egy vagy több kulcsot mellett a szükséges **AllNodes** kulcsot.
Ebben a témakörben a példákban azt egyetlen további csomópont használt, és azt nevű `NonNodeData`.
Azonban tetszőleges számú további kulcsok definiálása, és adja nekik bármit.

Nem csomópont adatait használatának példájáért lásd [konfigurációs és környezeti adatok szétválasztása](separatingEnvData.md).

## <a name="see-also"></a>Lásd még:

- [A konfigurációs adatok hitelesítő adatok beállításai](configDataCredentials.md)
- [DSC-konfigurációk](configurations.md)