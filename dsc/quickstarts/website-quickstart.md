---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Rövid útmutató – a DSC-s webhely létrehozása
ms.openlocfilehash: c62e2d8af46bf74c4dd13069ddff6cc39763a209
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684254"
---
> Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

# <a name="quickstart---create-a-website-with-dsc"></a>Rövid útmutató – a DSC-s webhely létrehozása

Ebben a gyakorlatban létrehozásával és alkalmazásával a Desired State Configuration (DSC) konfigurációs elejétől a végéig ismerteti.
A példában használunk biztosítja, hogy a kiszolgáló rendelkezik-e a `Web-Server` (IIS) szolgáltatás engedélyezve van, és egy egyszerű "Hello World" webhely tartalmának szerepel a `intepub\wwwroot` könyvtárat, az adott kiszolgáló.

DSC és működésének áttekintését lásd: [Desired State Configuration áttekintése döntéshozók számára](../overview/decisionMaker.md).

## <a name="requirements"></a>Követelmények

Ez a példa futtatásához szüksége lesz egy Windows Server 2012 vagy újabb verzió és a PowerShell 4.0-s vagy újabb rendszert futtató számítógép.

## <a name="write-and-place-the-indexhtm-file"></a>Írhat, és helyezze a index.HTML fájlt

Először a HTML-fájl, amely a webhely tartalmát, ezzel hozunk létre.

A legfelső szintű mappában hozza létre a `test`.

Egy szövegszerkesztőben írja be a következőket:

```html
<head></head>
<body>
<p>Hello World!</p>
</body>
```

Mentse ezt `index.htm` a a `test` korábban létrehozott mappába.

## <a name="write-the-configuration"></a>A konfiguráció írása

A [DSC-konfiguráció](../configurations/configurations.md) egy külön PowerShell-függvény, amely meghatározza, hogyan szeretné konfigurálni egy vagy több cél számítógépek (csomópontok).

A PowerShell ISE-ben írja be a következőt:

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

Mentse a fájlt az `WebsiteTest.ps1`.

Láthatja, hogy hasonlóan néz ki egy PowerShell-függvény, a kulcsszó azonban kiegészül **konfigurációs** előtt a függvény nevét használja.

A **csomópont** letiltása, adja meg a célcsomópont konfigurálását, ebben az esetben `localhost`.

A konfiguráció meghívja a két [erőforrások](../resources/resources.md), **WindowsFeature** és **fájl**.
Erőforrások teheti meg, hiszen a munkát, a célcsomópont a konfiguráció által meghatározott állapotban van.

## <a name="compile-the-configuration"></a>A konfiguráció fordítása

DSC csomópont alkalmazandó konfiguráció azt először kell összeállítani egy MOF-fájlba.
Ehhez futtassa a konfiguráció, például egy függvényt.
A PowerShell-konzolt ugyanabba a mappába, ahová mentette a konfiguráció keresse meg és futtassa a következő parancsokat egy MOF-fájlba konfiguráció fordítása:

```powershell
. .\WebsiteTest.ps1
WebsiteTest
```

Ez létrehozza a következő kimenet:

```
Directory: C:\ConfigurationTest\WebsiteTest


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/13/2017   5:20 PM           2746 localhost.mof
```

Az első sor elérhetővé teszi a konfigurációs funkció a konzolon.
A második sor fut, a konfigurációt.
Az eredménye, hogy egy új mappát nevű `WebsiteTest` jön létre, az aktuális mappa egy almappájában.
A `WebsiteTest` mappa tartalmaz egy fájlt `localhost.mof`.
Ezt a fájlt, majd alkalmazható a cél csomópontra.

## <a name="apply-the-configuration"></a>A konfiguráció alkalmazásához

Most, hogy a lefordított MOF, alkalmazhat a konfigurációt a célcsomópont (ebben az esetben az a helyi számítógép) meghívásával a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmagot.

A `Start-DscConfiguration` arra utasítja a parancsmag a [helyi Configuration Manager (LCM) Konfigurálása](../managing-nodes/metaConfig.md), azaz a a alkalmazni a konfigurációt a DSC motor.
Az LCM Konfigurálása a alkalmazni a konfigurációt a DSC-erőforrások hívása működik.

Az a PowerShell-konzolt keresse meg ugyanabba a mappába, ahová mentette a konfigurációt, és futtassa a következő parancsot:

```powershell
Start-DscConfiguration .\WebsiteTest
```

## <a name="test-the-configuration"></a>A konfiguráció tesztelése

Hívása a [Get-DscConfigurationStatus](/powershell/module/psdesiredstateconfiguration/get-dscconfigurationstatus) parancsmaggal ellenőrizheti, hogy sikerült-e a konfiguráció.

Is tesztelheti az eredményeket közvetlenül, ebben az esetben megkeresve `http://localhost/` egy webböngészőben.
Ez a példa első lépéseként kell megjelennie a "Hello World" HTML-lap hozott létre.

## <a name="next-steps"></a>További lépések

- További információk a DSC-konfigurációk [DSC-konfigurációk](../configurations/configurations.md).
- Megtudhatja, milyen DSC-erőforrás áll rendelkezésre, és hogyan hozhat létre egyéni DSC-erőforrásokat, [DSC-erőforrások](../resources/resources.md).
- DSC-konfigurációkat és erőforrásokat a [PowerShell-galériából](https://www.powershellgallery.com/).
