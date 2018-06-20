---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Konfigurációs adatok használata
ms.openlocfilehash: d42c43fddb54050adcbac949e7f67f3b41b540f1
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189686"
---
# <a name="using-configuration-data-in-dsc"></a>A DSC konfigurációs adatok használata

>Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A beépített DSC használatával **ConfigurationData** paraméter, használhatja a konfigurációs adatok definiálhat.
Ez lehetővé teszi több csomópont vagy különböző környezetekben használható egyetlen konfiguráció létrehozásához.
Például ha alkalmazást fejleszt, után egy konfigurációt használja a fejlesztési és éles környezetben is, is minden környezet adatainak megadása a konfigurációs adatok használatával.

Ez a témakör ismerteti a szerkezete a **ConfigurationData** hibás.
Konfigurációs adatok használatára, tekintse meg a [konfigurációs és környezeti adatok elválasztó](separatingEnvData.md).

## <a name="the-configurationdata-common-parameter"></a>A ConfigurationData általános paraméter

A DSC-konfiguráció egy közös paramétert fogad, **ConfigurationData**, meg kell adnia a konfiguráció-fordítási mikor.
További információ a konfiguráció fordítása: [a DSC-konfigurációk](configurations.md).

A **ConfigurationData** paraméter egy hasthtable, rendelkeznie kell legalább egy nevű kulcs **AllNodes**.
Egy vagy több kulcsot is rendelkezhet.

>**Megjegyzés:** ebben a témakörben szereplő példák egyetlen további kulcs használata (csak a megnevezett **AllNodes** kulcs) nevű `NonNodeData`, de további kulcsok tetszőleges számú, és nevezze függetlenül szeretné.

```powershell
$MyData =
@{
    AllNodes = @()
    NonNodeData = ""
}
```

Értékét a **AllNodes** kulcs egy tömb. A tömb egyes elemei egyben rendelkeznie kell legalább egy nevű kulcs kivonattáblát **csomópontnév**:

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

Más kulcsok minden egyes kivonattáblát is hozzáadhat:

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

Az összes csomópontra érvényes tulajdonság, tagja hozhat létre a **AllNodes** tömb, amely rendelkezik egy **csomópontnév** a `*`.
Például, hogy minden csomópont egy `LogPath` tulajdonság, sikerült ehhez:

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

Ez megfelel a nevű tulajdonság hozzáadása `LogPath` értékkel rendelkező `"C:\Logs"` minden más blokkok (`VM-1`, `VM-2`, és `VM-3`).

## <a name="defining-the-configurationdata-hashtable"></a>A ConfigurationData szórótáblájában meghatározása

Megadhat **ConfigurationData** vagy belül (ahogy az előző példák) egy konfigurációs parancsfájl fájlt változóként vagy külön `.psd1` fájlt.
Meghatározásához **ConfigurationData** a egy `.psd1` fájlt, hozzon létre egy fájlt, amely csak a kivonattábla a konfigurációs adatok jelölő tartalmazza.

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

## <a name="compiling-a-configuration-with-configuration-data"></a>A konfigurációs adatok konfiguráció fordítása

Egy konfigurációt, amely meghatározta a konfigurációs adatok lefordításához át a konfigurációs adatokat az értékeként a **ConfigurationData** paraméter.

Ezzel létrehoz minden bejegyzés esetében MOF-fájlt a **AllNodes** tömb.
Minden egyes MOF-fájlt nevű a `NodeName` a megfelelő tömb tétel tulajdonság.

Például, mint a konfigurációs adatok megadása a `MyData.psd1` fájl újabb, a konfiguráció fordítása hozna létre, mindkét `VM-1.mof` és `VM-2.mof` fájlokat.

### <a name="compiling-a-configuration-with-configuration-data-using-a-variable"></a>A konfiguráció fordítása és konfigurációs adatokat, a változó

Konfigurációs adatok azonos változóként definiált használandó `.ps1` fájl beállításként, adja meg a változó nevét az értékeként a **ConfigurationData** paraméter, a konfiguráció fordítása során:

```powershell
MyDscConfiguration -ConfigurationData $MyData
```

### <a name="compiling-a-configuration-with-configuration-data-using-a-data-file"></a>A konfiguráció fordítása és konfigurációs adatokat, egy adatfájlt

Egy .psd1 fájlban meghatározott konfigurációs adatok használatához adja meg az elérési útját és nevét, hogy a fájl értékeként a **ConfigurationData** paraméter, a konfiguráció fordítása során:

```powershell
MyDscConfiguration -ConfigurationData .\MyData.psd1
```

## <a name="using-configurationdata-variables-in-a-configuration"></a>Egy konfigurációs ConfigurationData változók használata

DSC nyújt három néhány speciális változó, amely egy konfigurációs parancsfájl használható: **$AllNodes**, **$Node**, és **$ConfigurationData**.

- **$AllNodes** hivatkozik a teljes gyűjteményt a meghatározott csomópontok **ConfigurationData**. Szűrheti a **AllNodes** gyűjtemény segítségével **. WHERE()** és **. ForEach()**.
- **Csomópont** egy adott bejegyzés hivatkozik a **AllNodes** gyűjtemény után a szűrt **. WHERE()** vagy **. ForEach()**.
- **ConfigurationData** hivatkozik a teljes kivonattábla a konfiguráció fordítása során átadott paraméterként.

## <a name="using-non-node-data"></a>Nem-csomópont adatok használata

Mivel az előző példákban is láttuk a **ConfigurationData** hashtable rendelkezhet egy vagy több kulcsot mellett a szükséges **AllNodes** kulcs.
Ebben a témakörben a példákban azt egyetlen további csomópont használja, és azt nevű `NonNodeData`.
Azonban minden további kulcsok számának megadása, és bármilyen kívánt nevet őket.

Például egy nem csomópont adatok használatával, lásd: [konfigurációs és környezeti adatok elválasztó](separatingEnvData.md).

## <a name="see-also"></a>Lásd még:
- [Konfigurációs adatokat a hitelesítő adatok beállításai](configDataCredentials.md)
- [A DSC-konfigurációk](configurations.md)