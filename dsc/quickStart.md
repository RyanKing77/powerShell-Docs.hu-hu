---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Szükségeskonfiguráció-State Configuration – első lépések"
ms.openlocfilehash: 295a78f3fd85464239d51d7be0defa04d2344689
ms.sourcegitcommit: f069ff0689006fece768f178c10e3e3eeaee09f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/13/2017
---
> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

# <a name="desired-state-configuration-quick-start"></a>Szükségeskonfiguráció-State Configuration – első lépések

Ebben a gyakorlatban végigvezeti a létrehozásával és alkalmazásával a kívánt állapot konfigurációs szolgáltatása (DSC) konfigurációs kezdetétől a végéig.
A példában használjuk biztosítja, hogy a kiszolgáló rendelkezik-e a `Web-Server` (IIS) engedélyezve van, és egy egyszerű "Hello, World" webhely tartalmának megtalálható-e a `intepub\wwwroot` mappában található a kiszolgálón.

A DSC-ből és annak működéséről áttekintését lásd: [kívánt állapot konfigurációs áttekintése döntéshozók](decisionMaker.md).

## <a name="requirements"></a>Követelmények

A példa futtatásához, szüksége lesz egy Windows Server 2012 vagy újabb és PowerShell 4.0-s vagy újabb rendszert futtató számítógép.

## <a name="write-and-place-the-indexhtm-file"></a>Írása, és helyezze a index.HTML fájlt

Először létrehozunk fogjuk használni, a webhely tartalmát a HTML-fájlba.

A legfelső szintű mappában hozza létre a `test`.

Egy szövegszerkesztőben írja be a következőket:

```html
<head></head>
<body>
<p>Hello World!</p>
</body>
```

Mentse ezt `index.htm` a a `test` korábban létrehozott mappába. 

## <a name="write-the-configuration"></a>A konfiguráció írásakor

A [DSC-konfiguráció](configurations.md) különleges PowerShell függvény, amely meghatározza, hogyan szeretné konfigurálni egy vagy több cél számítógépek (csomópontok).

A PowerShell ISE írja be a következőt:

```powershell
Configuration WebsiteTest {

    # Import the module that contains the resources we're using.
    Import-DscResource -ModuleName PsDesiredStateConfiguration

    # The Node statement specifies which targets this configuration will be applied to.
    Node 'localhost' {

        # The first resource block ensures that the Web-Server (IIS) feature is enabled.
        WindowsFeature WebServer {
            Ensure = "Present"
            Name   = "Web-Server"
        }

        # The second resource block ensures that the website content copied to the website root folder.
        File WebsiteContent {
            Ensure = 'Present'
            SourcePath = 'c:\test\index.htm'
            DestinationPath = 'c:\inetpub\wwwroot'
        }
    }
}
```

Mentse a fájlt `WebsiteTest.ps1`.

Láthatja, hogy úgy tűnik, a kulcsszó azonban kiegészül a PowerShell függvény **konfigurációs** a függvény neve előtt használt.

A **csomópont** blokk megadja a célcsomópont konfigurálását, ebben az esetben `localhost`.

A konfigurációs meghívja a két [erőforrások](resources.md), [WindowsFeature](windowsFeatureResource.md) és [fájl](fileResource.md).
Erőforrások munkájuk a annak biztosítására, hogy, hogy a célcsomópont a konfiguráció által meghatározott állapotban van.

## <a name="compile-the-configuration"></a>A konfiguráció-fordítási

A DSC-konfiguráció egy csomópont alkalmazandó azt kell először fordítható MOF-fájlt.
Ehhez futtassa a konfiguráció, például egy olyan függvényt.
PowerShell-konzolban navigáljon a ugyanabba a mappába, ahová menteni szeretné a konfigurációt, és futtassa az alábbi parancsokat a MOF-fájlba konfiguráció-fordítási:

```powershell
. .\WebsiteTest.ps1
WebsiteTest
```

Ezt követően a következő az alábbiakat:

```
Directory: C:\ConfigurationTest\WebsiteTest


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/13/2017   5:20 PM           2746 localhost.mof
```

Az első sor elérhetővé teszi a konfigurációs függvény a konzolon.
A második sor fut, a konfiguráció.
Az eredménye, hogy egy új mappát nevű `WebsiteTest` megegyezik az aktuális mappában jön létre.
A `WebsiteTest` mappa tartalmaz egy nevű fájlt `localhost.mof`.
Ezt a fájlt, majd a célcsomópont alkalmazhatja.

## <a name="apply-the-configuration"></a>A konfiguráció alkalmazásához

Most, hogy a lefordított MOF, alkalmazhat a konfiguráció célcsomóponton (ebben az esetben, a helyi számítógép) meghívásával a [Start-DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration) parancsmag.

A `Start-DscConfiguration` parancsmag közli a [helyi Configuration Manager (LCM)](metaConfig.md), vagyis a DSC-ből, a beállítások-motor.
A LCM e történt a DSC-erőforrások, a beállítások a munkáját.

PowerShell-konzolban navigáljon a ugyanabba a mappába, ahová menteni szeretné a konfigurációt, és futtassa a következő parancsot:

```powershell
Start-DscConfiguration .\WebsiteTest
```

## <a name="test-the-configuration"></a>Tesztelje a konfigurációt

Hívása a [Get-DscConfigurationStatus](/reference/5.1/PSDesiredStateConfiguration/Get-DscConfigurationStatus) parancsmag használatával ellenőrizheti, hogy a konfiguráció sikeres volt. 

Is tesztelheti az eredmények közvetlenül, ebben az esetben tallózással `http://localhost/` egy webböngészőben.
Ez a példa első lépéseként meg kell jelennie a létrehozott "Hello World" HTML-lapon.

## <a name="next-steps"></a>További lépések

- További információk a DSC-konfigurációk [a DSC-konfigurációk](configurations.md).
- Milyen DSC erőforrások elérhetők, és egyéni DSC erőforrások létrehozása [DSC erőforrások](resources.md).
- A DSC-konfigurációk és az erőforrások megkeresése a [PowerShell-galériában](https://www.powershellgallery.com/).



