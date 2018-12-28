---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A DSC folyamatos integrációt és folyamatos üzembe helyezési folyamat felépítésével bajlódnia
ms.openlocfilehash: c305d9bc7e0f8c659129b5a20d0b7e8b34d09ba8
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404376"
---
# <a name="building-a-continuous-integration-and-continuous-deployment-pipeline-with-dsc"></a>A DSC folyamatos integrációt és folyamatos üzembe helyezési folyamat felépítésével bajlódnia

Ez a példa bemutatja, hogyan hozhat létre egy folyamatos integráció/folyamatos üzembe helyezés (CI/CD) folyamatot a PowerShell, DSC, a Pester és a Visual Studio Team Foundation Server (TFS) használatával.

Miután a folyamat beépített és konfigurálva van, ennek segítségével teljes mértékben központi telepítése, konfigurálása és tesztelése a DNS-kiszolgáló, és állomásrekordokat kapcsolódó.
Ez a folyamat egy fejlesztési környezetben használni kívánt folyamat első részének szimulálja.

Egy automatizált CI/CD-folyamat segítségével gyorsabban szoftverek frissítése és megbízhatóan, biztosítva, hogy az összes kód lett tesztelve, és hogy a kód aktuális build mindenkor.

## <a name="prerequisites"></a>Előfeltételek

Ebben a példában használatához ismernie kell a következőkkel:

- CI-CD fogalmakat. Útmutatással található [a kiadási adatfolyamat-modell](http://aka.ms/thereleasepipelinemodelpdf).
- [A Git](https://git-scm.com/) verziókövetés
- A [Pester](https://github.com/pester/Pester) tesztelési keretrendszerének
- [A Team Foundation Server](https://www.visualstudio.com/tfs/)

## <a name="what-you-will-need"></a>Mit kell

Hozza létre, és futtassa az ebben a példában, szüksége lesz számos számítógépek és/vagy virtuális gépek környezet.

### <a name="client"></a>Ügyfél

Ez az a számítógépen, ahol teheti meg az összes beállíthatja és futtathatja a példa a munkahelyi.

Az ügyfélszámítógépen kell telepíteni az alábbi Windows számítógép:

- [a git](https://git-scm.com/)
- klónozza a helyi git-adattár https://github.com/PowerShell/Demo_CI
- egy szövegszerkesztőben, például [Visual Studio Code](https://code.visualstudio.com/)

### <a name="tfssrv1"></a>TFSSrv1

A számítógép, amelyen a TFS-kiszolgálónak, ahol a build meghatározzuk és kiadása.
Ezen a számítógépen telepítve kell [Team Foundation Server 2017](https://www.visualstudio.com/tfs/) telepítve.

### <a name="buildagent"></a>BuildAgent

A számítógépen, amelyen a Windows ügynök, amely összeállítja a projekt létrehozása.
Ez a számítógép rendelkeznie kell egy telepített és futó ügynök hozhat létre Windows.
Lásd: [a Windows-ügynök telepítése](/azure/devops/pipelines/agents/v2-windows) való telepítése és futtatása egy Windows hozhat létre az ügynök számára.

Alkalmazást is telepíteni kell a `xDnsServer` és `xNetworking` DSC-modulok ezen a számítógépen.

### <a name="testagent1"></a>TestAgent1

Ez az a számítógép, amely szerint ebben a példában a DSC-konfiguráció DNS-kiszolgálóként van konfigurálva.
A számítógépen kell futnia [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).

### <a name="testagent2"></a>TestAgent2

Ez az a számítógép, amelyen a webhely, ez a példa konfigurálja.
A számítógépen kell futnia [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).

## <a name="add-the-code-to-tfs"></a>Adja hozzá a kódot a TFS

Hozunk egy Git-tárház létrehozása a TFS-ben, és a kód importálja a helyi tárház az ügyfélszámítógépen.
Ha nem rendelkezik már klónozta a Demo_CI tárházat az ügyfélszámítógépre tegye most a következő git-parancs futtatásával:

`git clone https://github.com/PowerShell/Demo_CI`

1. Az ügyfélszámítógépen navigáljon a TFS-kiszolgáló egy webböngészőben.
1. A TFS rendszerben [hozzon létre egy új csoportprojektet](/azure/devops/organizations/projects/create-project) Demo_CI nevű.

   Győződjön meg arról, hogy **verziókövetés** értékre van állítva **Git**.
1. Az ügyfélszámítógépen adjon hozzá egy távoli a tárházban létrehozott a TFS-ben a következő paranccsal:

   `git remote add tfs <YourTFSRepoURL>`

   Ahol `<YourTFSRepoURL>` a TFS-tárházba az előző lépésben létrehozott klón URL-címe.

   Ha nem tudja, hol találja az URL-címet, tekintse meg [egy meglévő Git-adattár klónozása](/azure/devops/repos/git/clone).
1. A kód a helyi adattárból leküldése a TFS-tárunkat, ahol a következő parancsot:

   `git push tfs --all`
1. A TFS-tárház tölti fel a Demo_CI kódot.

> [!NOTE]
> Ez a példa lévő kódot az `ci-cd-example` a Git-adattár ágában.
> Ügyeljen arra, hogy ez az ág az alapértelmezett ágon, a TFS-projektben adja meg, és a CI/CD-eseményindítók létrehozásához.

## <a name="understanding-the-code"></a>A kód ismertetése

A buildelési és üzembe helyezési folyamatok hozunk létre, mielőtt tekintsük át néhány a kódot, és ismerje meg, mi is történik.
Az ügyfélszámítógépen nyissa meg a kedvenc szövegszerkesztőjével, és keresse meg a Demo_CI Git-tárház gyökérkönyvtárában.

### <a name="the-dsc-configuration"></a>A DSC-konfiguráció

Nyissa meg a fájlt `DNSServer.ps1` (a helyi Demo_CI tárház gyökérkönyvtárából `./InfraDNS/Configs/DNSServer.ps1`).

Ez a fájl tartalmazza a DSC-konfiguráció, amely beállítja a DNS-kiszolgálót. Itt van ebben az esetben:

```powershell
configuration DNSServer
{
    Import-DscResource -module 'xDnsServer','xNetworking', 'PSDesiredStateConfiguration'

    Node $AllNodes.Where{$_.Role -eq 'DNSServer'}.NodeName
    {
        WindowsFeature DNS
        {
            Ensure  = 'Present'
            Name    = 'DNS'
        }

        xDnsServerPrimaryZone $Node.zone
        {
            Ensure    = 'Present'
            Name      = $Node.Zone
            DependsOn = '[WindowsFeature]DNS'
        }

        foreach ($ARec in $Node.ARecords.keys) {
            xDnsRecord $ARec
            {
                Ensure    = 'Present'
                Name      = $ARec
                Zone      = $Node.Zone
                Type      = 'ARecord'
                Target    = $Node.ARecords[$ARec]
                DependsOn = '[WindowsFeature]DNS'
            }
        }

        foreach ($CName in $Node.CNameRecords.keys) {
            xDnsRecord $CName
            {
                Ensure    = 'Present'
                Name      = $CName
                Zone      = $Node.Zone
                Type      = 'CName'
                Target    = $Node.CNameRecords[$CName]
                DependsOn = '[WindowsFeature]DNS'
            }
        }
    }
}
```

Figyelje meg a `Node` utasítást:

```powershell
Node $AllNodes.Where{$_.Role -eq 'DNSServer'}.NodeName
```

Ez olyan csomópontokat, hogy az egyik szerepköre, definiált megkeresi `DNSServer` a a [konfigurációs adatok](../configurations/configData.md), által létrehozott a `DevEnv.ps1` parancsfájlt.

További információ a `Where` metódus az [about_arrays](/powershell/reference/3.0/Microsoft.PowerShell.Core/About/about_Arrays.md)

Konfigurációs adatok segítségével határozza meg a csomópontok akkor fontos, ha ezzel a CI, mivel a csomópont-információk valószínűleg változni fognak a környezetek között, és a konfigurációs adatok használata lehetővé teszi, hogy egyszerűen módosításokat csomópontjának adatait a konfigurációs programkód módosítása nélkül.

Az első resource blokkban, a konfiguráció meghívja a **WindowsFeature** annak érdekében, hogy a DNS szolgáltatás engedélyezve van-e.
Az erőforrás blokkokat hívás erőforrásokat, kövesse a [xDnsServer](https://github.com/PowerShell/xDnsServer) modul elsődleges zóna és a DNS-rekordok konfigurálása.

Figyelje meg, hogy a két `xDnsRecord` blokkok burkolja `foreach` , amely a konfigurációs adatokat a tömbök iterálódnak hurkokat.
A konfigurációs adatok létre újra, a `DevEnv.ps1` szkriptet, amely áttekintjük a Tovább gombra.

### <a name="configuration-data"></a>Konfigurációs adatok

A `DevEnv.ps1` fájlt (a helyi Demo_CI tárház gyökérkönyvtárából `./InfraDNS/DevEnv.ps1`) egy kivonattáblát határozza meg az adott környezetre vonatkozó konfigurációs adatokat, és ezután továbbítja a kivonattábla kulcsa hívása a `New-DscConfigurationDataDocument` függvény, amelyet a `DscPipelineTools.psm` (`./Assets/DscPipelineTools/DscPipelineTools.psm1`).

A `DevEnv.ps1` fájlt:

```powershell
param(
    [parameter(Mandatory=$true)]
    [string]
    $OutputPath
)

Import-Module $PSScriptRoot\..\Assets\DscPipelineTools\DscPipelineTools.psd1 -Force

# Define Unit Test Environment
$DevEnvironment = @{
    Name                        = 'DevEnv';
    Roles = @(
        @{  Role                = 'DNSServer';
            VMName              = 'TestAgent1';
            Zone                = 'Contoso.com';
            ARecords            = @{'TFSSrv1'= '10.0.0.10';'Client'='10.0.0.15';'BuildAgent'='10.0.0.30';'TestAgent1'='10.0.0.40';'TestAgent2'='10.0.0.50'};
            CNameRecords        = @{'DNS' = 'TestAgent1.contoso.com'};
        }
    )
}

Return New-DscConfigurationDataDocument -RawEnvData $DevEnvironment -OutputPath $OutputPath
```

A `New-DscConfigurationDataDocument` függvény (meghatározott `\Assets\DscPipelineTools\DscPipelineTools.psm1`) programozott módon hoz létre a konfigurációs adatok dokumentum a kivonattábla (csomópont adatait) és a tömb (nem csomópont adatait), amely adhatók be a `RawEnvData` és `OtherEnvData` paramétereket.

Ebben az esetben csak a `RawEnvData` paramétert használja.

### <a name="the-psake-build-script"></a>A psake felépítési szkriptjének

A [psake](https://github.com/psake/psake) felépítési szkript meghatározott `Build.ps1` (a Demo_CI tárház gyökérkönyvtárából `./InfraDNS/Build.ps1`) a build részét képező tevékenységek meghatározása.
Minden tevékenység más tevékenységek is meghatározza.
Meghívva, ha a psake parancsfájl biztosítja, hogy a megadott feladat (vagy nevű feladatot `Default` Ha nincs megadva) fut, és az összes függőséget is futtathat (Ez azért szükséges, a rekurzív függőségek függőségeinek futtatása, és így tovább).

Ebben a példában a `Default` feladat típusúként van definiálva:

```powershell
Task Default -depends UnitTests
```

A `Default` feladat nem magát végrehajtására van, de maga a `CompileConfigs` feladat.
Az eredményül kapott láncában tevékenységfüggőségek biztosítja, hogy a felépítési szkriptjének található összes feladat futtatása.

Ebben a példában a psake parancsfájl hívása hív `Invoke-PSake` a a `Initiate.ps1` fájlt (a Demo_CI tárház gyökérkönyvtárában található):

```powershell
param(
    [parameter()]
    [ValidateSet('Build','Deploy')]
    [string]
    $fileName
)

#$Error.Clear()

Invoke-PSake $PSScriptRoot\InfraDNS\$fileName.ps1

<#if($Error.count)
{
    Throw "$fileName script failed. Check logs for failure details."
}
#>
```

Ha a builddefiníció hozunk létre a példa a TFS-ben, azt fogja adni a psake parancsfájlt, a `fileName` Ez a szkript paramétere.

A felépítési szkriptjének határozza meg a következő feladatokat:

#### <a name="generateenvironmentfiles"></a>GenerateEnvironmentFiles

Futtatások `DevEnv.ps1`, amely állít elő, hogy a konfigurációs adatfájl.

#### <a name="installmodules"></a>InstallModules

Telepíti a modulokat, a konfiguráció szükséges `DNSServer.ps1`.

#### <a name="scriptanalysis"></a>ScriptAnalysis

Hívások a [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer).

#### <a name="unittests"></a>UnitTests

Futtatás a [Pester](https://github.com/pester/Pester/wiki) egységteszteket.

#### <a name="compileconfigs"></a>CompileConfigs

Lefordítja a konfigurációt (`DNSServer.ps1`) által létrehozott konfigurációs adatok használatával MOF-fájlba a `GenerateEnvironmentFiles` feladat.

#### <a name="clean"></a>Clean

A például szolgáló mappákat hoz létre, és eltávolítja a korábbi közvetítésekből származó terhelésiteszt-eredményei, konfigurációs adatfájllal, és modulok.

### <a name="the-psake-deploy-script"></a>A psake parancsfájl központi telepítése

A [psake](https://github.com/psake/psake) meghatározott telepítési parancsfájl `Deploy.ps1` (a Demo_CI tárház gyökérkönyvtárából `./InfraDNS/Deploy.ps1`) határozza meg, amely üzembe helyezése és futtatása a konfigurációs feladatok.

`Deploy.ps1` határozza meg a következő feladatokat:

#### <a name="deploymodules"></a>DeployModules

Elindít egy PowerShell-munkamenetet a `TestAgent1` , és telepíti a modulokat tartalmazó a DSC-erőforrások, a konfigurációhoz szükséges.

#### <a name="deployconfigs"></a>DeployConfigs

Hívások a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmag futtatása a konfiguráció `TestAgent1`.

#### <a name="integrationtests"></a>IntegrationTests

Futtatás a [Pester](https://github.com/pester/Pester/wiki) integráció az egységteszteket.

#### <a name="acceptancetests"></a>AcceptanceTests

Futtatás a [Pester](https://github.com/pester/Pester/wiki) minőségellenőrzési tesztelésben vesznek részt.

#### <a name="clean"></a>Clean

Eltávolítja a modulokat az előző futtatásokat telepítve, és biztosítja, hogy a teszt eredménye mappa létezik-e.

### <a name="test-scripts"></a>Parancsfájlok tesztelése

Elfogadó, integráció, és az egységteszteket definiált szkriptekben a `Tests` mappát (a Demo_CI tárház gyökérkönyvtárából `./InfraDNS/Tests`), mindegyik nevű fájlt a `DNSServer.tests.ps1` megfelelő mappáiban.

A teszt-szkriptek használata [Pester](https://github.com/pester/Pester/wiki) és [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) szintaxist.

#### <a name="unit-tests"></a>Egységteszteket

Az egység teszteli magukat, hogy győződjön meg arról, hogy a konfigurációk elvégzi az alkalmazás futtatásakor várt tesztelési a DSC-konfigurációkat.
A parancsfájlt használja vetünk [Pester](https://github.com/pester/Pester/wiki).

#### <a name="integration-tests"></a>Integráció az egységteszteket

Az integrációs tesztek a konfiguráció teszteléséhez vagy a rendszer bizonyosodjon meg arról, hogy más összetevők integrálva, amikor a rendszer elvárt módon. Ezek a tesztek futtatása célcsomóponton után a DSC lett konfigurálva.
Az integrációs teszt szkriptjét használ vegyesen [Pester](https://github.com/pester/Pester/wiki) és [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) szintaxist.

#### <a name="acceptance-tests"></a>Minőségellenőrzési tesztelésben vesznek részt

Minőségellenőrzési tesztelésben vesznek részt teszteléséhez győződjön meg arról, hogy a várt módon működnek-e, a rendszer.
Például azt teszteli, annak érdekében, hogy egy weblap történő lekérdezéskor a megfelelő információt ad vissza.
Ezek a tesztek távolról futtatni a célcsomópont a valós életből vett teszteléséhez.
Az integrációs teszt szkriptjét használ vegyesen [Pester](https://github.com/pester/Pester/wiki) és [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) szintaxist.

## <a name="define-the-build"></a>A build megadása

Most, hogy mi feltöltötte a kódban, TFS és tekintett meg, mire, határozzon meg a build.

Itt csak a fogja hozzáadni a buildre létrehozási lépések lesz szó. Builddefiníció létrehozása a TFS-ben, lásd: [létrehozása és a várólista builddefiníció](/azure/devops/pipelines/get-started-designer).

Hozzon létre egy új builddefiníció (válassza ki a **üres** sablon) "InfraDNS" nevű.
Adja hozzá az alábbi lépések végrehajtásával, build definíciója:

- PowerShell-parancsfájl
- Vizsgálati eredmények közzététele
- Fájlok másolása
- Összetevők közzététele

Ezek lépések, a következő az egyes lépések tulajdonságainak szerkesztéséhez hozzáadása után:

### <a name="powershell-script"></a>PowerShell-parancsfájl

1. Állítsa be a **típus** tulajdonságot `File Path`.
1. Állítsa be a **parancsfájl elérési útján** tulajdonságot `initiate.ps1`.
1. Adjon hozzá `-fileName build` , a **argumentumok** tulajdonság.

Ez a létrehozási lépés fut a `initiate.ps1` fájlt, amely meghívja a psake felépítési szkriptet.

### <a name="publish-test-results"></a>Vizsgálati eredmények közzététele

1. Állítsa be **Eredményformátum tesztelése** , `NUnit`
1. Állítsa be **fájlokat a vizsgálati eredmények** , `InfraDNS/Tests/Results/*.xml`
1. Állítsa be **futtatási cím tesztelése** való `Unit`.
1. Győződjön meg arról, hogy **verziókövetési lehetőségek állnak rendelkezésre** **engedélyezve** és **mindig fusson** azok mind kiválasztva.

A létrehozási lépés fut, a Pester parancsfájl megvizsgáltunk, korábban az egységteszteket, és tárolja az eredményeket a `InfraDNS/Tests/Results/*.xml` mappát.

### <a name="copy-files"></a>Fájlok másolása

1. Adja hozzá a következő sorokat **tartalma**:

   ```
   initiate.ps1
   **\deploy.ps1
   **\Acceptance\**
   **\Integration\**
   ```

1. Állítsa be **TargetFolder** , `$(Build.ArtifactStagingDirectory)\`

Ebben a lépésben másolja át a build és a teszt parancsfájlok, az átmeneti könyvtárhoz úgy, hogy a build-összetevőket, által közzétehető a következő lépéssel.

### <a name="publish-artifact"></a>Összetevők közzététele

1. Állítsa be **közzététele elérési út** , `$(Build.ArtifactStagingDirectory)\`
1. Állítsa be **összetevőnév** , `Deploy`
1. Állítsa be **Összetevőtípussal** , `Server`
1. Válassza ki `Enabled` a **beállítások**

## <a name="enable-continuous-integration"></a>Folyamatos integráció engedélyezése

Most beállítjuk egy eseményindítót, amely miatt a projekt felépítéséhez bármikor egy módosítást a rendszer ellenőrzi, a `ci-cd-example` a git-adattár ágában.

1. A TFS-ben, kattintson a **Build & Release** lap
1. Válassza ki a `DNS Infra` builddefiníció, majd kattintson az **szerkesztése**
1. Kattintson a **eseményindítók** lap
1. Válassza ki **folyamatos integrációs (CI)**, és válassza ki `refs/heads/ci-cd-example` a fiókiroda legördülő lista
1. Kattintson a **mentése** , majd **OK**

Most már minden változása a TFS git-tárház eseményindítók egy automatizált összeállítási.

## <a name="create-the-release-definition"></a>A kiadási definíció létrehozása

Kiadási definíció hozzunk létre úgy, hogy a projekt rendszerbe minden kód bejelentkezés a fejlesztői környezetben.

Ehhez adja hozzá társított új kiadási definíciót a `InfraDNS` hozhat létre a korábban létrehozott builddefiníciót.
Ügyeljen arra, hogy válasszon **folyamatos üzembe helyezés** úgy, hogy az új kiadás akkor aktiválódik, amikor elkészül egy új build.
([Hogyan: Kiadási definíciók együttműködve](https://www.visualstudio.com/en-us/docs/build/actions/work-with-release-definitions)) és a következőképpen konfigurálja:

Adja hozzá a kiadási definíció az alábbi lépéseket:

- PowerShell-parancsfájl
- Vizsgálati eredmények közzététele
- Vizsgálati eredmények közzététele

Szerkesztése a következő lépéseket:

### <a name="powershell-script"></a>PowerShell-parancsfájl

1. Állítsa be a **parancsfájl elérési útján** mezőt `$(Build.DefinitionName)\Deploy\initiate.ps1"`
1. Állítsa be a **argumentumok** mezőt `-fileName Deploy`

### <a name="first-publish-test-results"></a>Először a vizsgálati eredmények közzététele

1. Válassza ki `NUnit` számára a **teszt Eredményformátum** mező
1. Állítsa be a **eredmény Tesztfájlok** mezőt `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Integration*.xml`
1. Állítsa be a **futtatási cím tesztelése** , `Integration`
1. A **verziókövetési lehetőségek állnak rendelkezésre**, ellenőrizze **mindig futtatja**

### <a name="second-publish-test-results"></a>A második a vizsgálati eredmények közzététele

1. Válassza ki `NUnit` számára a **teszt Eredményformátum** mező
1. Állítsa be a **eredmény Tesztfájlok** mezőt `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Acceptance*.xml`
1. Állítsa be a **futtatási cím tesztelése** , `Acceptance`
1. A **verziókövetési lehetőségek állnak rendelkezésre**, ellenőrizze **mindig futtatja**

## <a name="verify-your-results"></a>Az eredmények ellenőrzése

Most bármikor, küldje le változások a `ci-cd-example` ágra a TFS-ben, egy új létrehozást indul el.
Ha a létrehozás sikeresen befejeződik, akkor aktiválódik, új központi telepítést.

Az eredmény az üzembe helyezés ellenőrzéséhez nyissa meg egy böngészőt, az ügyfélszámítógépen, és ellenőrizheti, hogy `www.contoso.com`.

## <a name="next-steps"></a>További lépések

Ez a példa konfigurálja a DNS-kiszolgáló `TestAgent1` úgy, hogy az URL-cím `www.contoso.com` mutat `TestAgent2`, de azt nem ténylegesen telepíti egy webhely.
Ennek a vázat a tárház alatt megtalálható a `WebApp` mappát.
A psake parancsfájlok, a Pester tesztek és a DSC-konfigurációk létrehozása a megadott fájl segítségével telepítheti a saját webhelyen.
