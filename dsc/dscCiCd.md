---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC folyamatos integrációt és folyamatos üzembe helyezési folyamat létrehozása"
ms.openlocfilehash: baa56088d83fba56d3a19cff7954d3081f341f9a
ms.sourcegitcommit: 60c6f9d8cf316e6d5b285854e6e5641ac7648f3f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/17/2017
---
# <a name="building-a-continuous-integration-and-continuous-deployment-pipeline-with-dsc"></a>A DSC folyamatos integrációt és folyamatos üzembe helyezési folyamat létrehozása

Ez a példa bemutatja, hogyan folyamatos integráció/Continuous Deployment (CI/CD) folyamat létrehozása a PowerShell DSC, Pester és a Visual Studio Team Foundation Server (TFS) használatával.

A feldolgozási sor összeállítása és konfigurálva, után teljes telepítéséhez, konfigurálásához, és DNS-kiszolgáló tesztelése alkalmazhat, és állomásrekordokat társított. Ez a folyamat első része egy folyamatot, amely fejlesztői környezetben használni szimulálja.

Egy automatizált CI/CD folyamat segít a gyorsabb frissítse a szoftvert, és megbízhatóbb, győződjön meg arról, hogy az összes kód szolgáltatás tesztelése, és hogy a kód aktuális build mindenkor.

## <a name="prerequisites"></a>Előfeltételek

Ez a példa használatához ismernie kell a következőkkel:

- CI-CD fogalmakat. Egy jó hivatkozás található a [a kiadási csővezeték modell](http://aka.ms/thereleasepipelinemodelpdf).
- [Git](https://git-scm.com/) forrás-vezérlő
- A [Pester](https://github.com/pester/Pester) keretrendszer tesztelése
- [A Team Foundation Server](https://www.visualstudio.com/tfs/)

## <a name="what-you-will-need"></a>Mit kell

Építsenek, és ez a példa futtatásához, szüksége lesz a több számítógépek és/vagy a virtuális gépeket tartalmazó környezetben.

### <a name="client"></a>Ügyfél

Ez az a számítógépen, ahol el kell végeznie összes beállíthatja és futtathatja a példa a munkát.

Az ügyfélszámítógép kell lennie a Windows rendszerű számítógépeken telepítve a következőre:
- [Git](https://git-scm.com/)
- egy helyi git-tárház https://github.com/PowerShell/Demo_CI alapján klónozták
- egy szövegszerkesztőben, például a [Visual Studio Code](https://code.visualstudio.com/)

### <a name="tfssrv1"></a>TFSSrv1

A TFS-kiszolgálóhoz, amelyen határozza meg a build futtató számítógépen és felszabadítása.
A számítógépnek rendelkeznie kell [Team Foundation Server 2017](https://www.visualstudio.com/tfs/) telepítve.

### <a name="buildagent"></a>BuildAgent

A a Windows rendszerű számítógépre ügynök, amely létrehozza a projekt felépítéséhez.
Ezen a számítógépen telepített és futó ügynök összeállítása Windows kell rendelkeznie.
Lásd: [egy Windows-ügynök telepítéséhez](https://www.visualstudio.com/en-us/docs/build/actions/agents/v2-windows) vonatkozó útmutatást, telepítéséhez és futtatásához egy Windows-build ügynök.

Alkalmazást is telepíteni kell a `xDnsServer` és `xNetworking` DSC-modulok ezen a számítógépen.

### <a name="testagent1"></a>TestAgent1

Ez az a számítógép a DSC-konfiguráció ebben a példában a DNS-kiszolgálóként konfigurált.
A számítógépen futnia kell [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).

### <a name="testagent2"></a>TestAgent2

Ez az a számítógép, amelyen a webhely a példa.
A számítógépen futnia kell [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016). 

## <a name="add-the-code-to-tfs"></a>Adja hozzá a kódot TFS

Először foglalkozunk a Git-tárház létrehozása a TFS-ben, és importálja a helyi tárház az ügyfélszámítógépen a kódot.
Ha nem rendelkezik már klónozni a Demo_CI tárház az ügyfélszámítógépre tegye most a következő git parancs futtatásával:

`git clone https://github.com/PowerShell/Demo_CI`

1. Az ügyfélszámítógépen navigáljon a TFS-kiszolgáló egy webböngészőben.
1. A TFS rendszerben [hozzon létre egy új csapatprojektbe](https://www.visualstudio.com/en-us/docs/setup-admin/create-team-project) Demo_CI nevű.

    Győződjön meg arról, hogy **verziókezelést** értéke **Git**.
1. Az ügyfélszámítógépen a most létrehozott a TFS-ben a következő paranccsal tárház távoli hozzáadása:

    `git remote add tfs <YourTFSRepoURL>`

    Ha `<YourTFSRepoURL>` a klón URL-címét az előző lépésben létrehozott TFS-tárházba.

    Ha nem tudja, hol található az URL-cím, lásd: [egy meglévő Git-tárház klónozása](https://www.visualstudio.com/en-us/docs/git/tutorial/clone).
1. A kód a helyi tárházból a TFS tárház leküldése a következő paranccsal:

    `git push tfs --all`
1. A TFS-tárház tölti fel a Demo_CI kódot.

>**Megjegyzés:** ebben a példában a kódot használja a `ci-cd-example` a Git-tárház főágába.
>Ügyeljen arra, hogy az ág az alapértelmezett ágat a TFS-projekt adja meg, és a CI/CD eseményindítók hoz létre.

## <a name="understanding-the-code"></a>A kód ismertetése

A buildelés és üzembe helyezés folyamatok létrehozhatunk, mielőtt vizsgáljuk meg néhány, a kód folyamatainak megértése.
Az ügyfélszámítógépen nyissa meg a kedvenc szövegszerkesztőjével, és keresse meg a Demo_CI Git-tárház gyökérkönyvtárában.

### <a name="the-dsc-configuration"></a>A DSC-konfiguráció

Nyissa meg a fájlt `DNSServer.ps1` (a helyi Demo_CI tárház gyökérkönyvtárában `./InfraDNS/Configs/DNSServer.ps1`).

Ez a fájl tartalmazza a DSC-konfiguráció, amely beállítja a DNS-kiszolgáló. Itt van egészében:

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

Ez azoknak a fürtöknek, egyik szerepköre rendelkezőként meghatározott talál `DNSServer` a a [konfigurációs adatok](configData.md), által létrehozott a `DevEnv.ps1` parancsfájl.

Konfigurációs adatok segítségével határozza meg a csomópontok fontos CI során, mert a csomópont információk valószínűleg változik a különböző környezetek között, és a konfigurációs adatok használatával lehetővé teszi, könnyen módosíthatja csomópont adatokat a konfigurációs kódjának módosítása nélkül.

Az első erőforrás blokkban, a konfiguráció meghívja a [WindowsFeature](windowsFeatureResource.md) annak érdekében, hogy a DNS szolgáltatás engedélyezve van-e. A hívás erőforrások a következő erőforrás blokkolja a [xDnsServer](https://github.com/PowerShell/xDnsServer) modul elsődleges zóna és a DNS-rekordok konfigurálása.

Figyelje meg, hogy a két `xDnsRecord` blokkok csomagolni vannak `foreach` , amely a konfigurációs adatokat a tömbök iterációt hurkok.
Ebben az esetben a konfigurációs adatok hozta létre a `DevEnv.ps1` parancsfájl, amely megnézzük, a Tovább gombra.

### <a name="configuration-data"></a>Konfigurációs adatok

A `DevEnv.ps1` fájlt (a helyi Demo_CI tárház gyökérkönyvtárában `./InfraDNS/DevEnv.ps1`) megadja egy kivonattáblát a környezet konfigurációs adatait, és majd hívásakor adja át, hogy hibás a `New-DscConfigurationDataDocument` függvény, amelyet a `DscPipelineTools.psm` (`./Assets/DscPipelineTools/DscPipelineTools.psm1`).

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

A `New-DscConfigurationDataDocument` függvény (definiált `\Assets\DscPipelineTools\DscPipelineTools.psm1`) programozott módon a kivonattábla (adatai) és a tömb (nem csomópont adatait) szerint átadott a konfigurációs adatok dokumentum létrehozása a `RawEnvData` és `OtherEnvData` paraméterek.

Ebben az esetben csak a `RawEnvData` paraméterrel.

### <a name="the-psake-build-script"></a>A psake build script

A [psake](https://github.com/psake/psake) definiált parancsfájl összeállítása `Build.ps1` (Demo_CI tárház gyökérkönyvtárában `./InfraDNS/Build.ps1`) határozza meg a build feladatainak.
Minden tevékenység attól függ, milyen egyéb feladatokat is meghatározza. Meghívásakor, a psake parancsfájl biztosítja, hogy a megadott feladat (vagy nevű feladat `Default` Ha nincs megadva) fut, és, hogy az összes függősége is futtathatnak (rekurzív, azt, hogy a függőségek függőségek, és így tovább).

Ebben a példában a `Default` feladat típusúként van definiálva:

```powershell
Task Default -depends UnitTests
```

A `Default` feladat nem tartozik megvalósítás magát, de függ a `CompileConfigs` feladat.
Az eredményül kapott lánc feladat függőségi biztosítja, hogy futnak-e a build parancsfájlban szereplő összes feladatot.

Ebben a példában a psake parancsfájl hívásával meghívott `Invoke-PSake` a a `Initiate.ps1` fájlt (a Demo_CI tárház gyökérkönyvtárában található):

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

Létrehozásakor a build definícióját a fenti példában a TFS-ben, azt fogja adni a psake parancsfájlt, mint a `fileName` paraméter ehhez a parancsprogramhoz.

A build parancsfájl meghatározza, hogy a következő feladatokat:

#### <a name="generateenvironmentfiles"></a>GenerateEnvironmentFiles

Futtatása `DevEnv.ps1`, amely a konfigurációs adatok fájlt hoz létre.

#### <a name="installmodules"></a>InstallModules

Telepíti a modulok, a konfiguráció szükséges `DNSServer.ps1`.

#### <a name="scriptanalysis"></a>ScriptAnalysis

Hívások a [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer).

#### <a name="unittests"></a>UnitTests

Fut a [Pester](https://github.com/pester/Pester/wiki) egység teszteket.

#### <a name="compileconfigs"></a>CompileConfigs

Lefordítja a konfigurációs (`DNSServer.ps1`) által létrehozott konfigurációs adatok használatával MOF-fájlba, a `GenerateEnvironmentFiles` feladat.

#### <a name="clean"></a>Clean

A például szolgáló mappákat hoz létre, és a vizsgálati eredmények, a konfigurációs adatok fájlok és a modulok eltávolítja a korábbi futtatásakor.

### <a name="the-psake-deploy-script"></a>A psake parancsfájl központi telepítése

A [psake](https://github.com/psake/psake) meghatározott telepítési parancsfájl `Deploy.ps1` (Demo_CI tárház gyökérkönyvtárában `./InfraDNS/Deploy.ps1`) telepítése, és futtassa a konfigurációs feladatokat, határozza meg.

`Deploy.ps1`Meghatározza, hogy a következő feladatokat:

#### <a name="deploymodules"></a>DeployModules

A PowerShell-munkamenetben megkezdése `TestAgent1` és telepíti a konfiguráláshoz szükséges DSC erőforrásokat tartalmazó modult.

#### <a name="deployconfigs"></a>DeployConfigs

Hívások a [Start-DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration.md) parancsmag segítségével futtassa a konfigurációs `TestAgent1`.

#### <a name="integrationtests"></a>IntegrationTests

Fut a [Pester](https://github.com/pester/Pester/wiki) integrációs teszteket.

#### <a name="acceptancetests"></a>AcceptanceTests

Fut a [Pester](https://github.com/pester/Pester/wiki) elfogadási teszteket.

#### <a name="clean"></a>Clean

Eltávolítja a korábbi fut telepített modul, és biztosítja, hogy létezik-e a teszt eredménye mappa.

### <a name="test-scripts"></a>Parancsfájlok tesztelése

Elfogadási, integráció és egység tesztek határozzák meg a parancsfájlok a `Tests` mappa (Demo_CI tárház gyökérkönyvtárában `./InfraDNS/Tests`), a nevű fájlt minden egyes `DNSServer.tests.ps1` megfelelő mappáiban.

A vizsgálat a parancsfájlok használata [Pester](https://github.com/pester/Pester/wiki) és [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) szintaxist.

#### <a name="unit-tests"></a>Egység tesztek

Az egység magát győződjön meg arról, hogy a konfigurációk hajt végre a futtatásakor. várt teszt a DSC-konfigurációk teszteli.
Az egység tesztelése parancsfájl által használt [Pester](https://github.com/pester/Pester/wiki).

#### <a name="integration-tests"></a>Integráció tesztek

Az integráció tesztek tesztelje a konfigurációt a rendszer annak érdekében, hogy ha más összetevők integrálva, a rendszer elvártak szerint van konfigurálva. Ezek a tesztek futtatása célcsomóponton után a DSC lett konfigurálva.
Az integráció teszt parancsfájl keverékével [Pester](https://github.com/pester/Pester/wiki) és [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) szintaxist.

#### <a name="acceptance-tests"></a>Elfogadási tesztek

Elfogadási vizsgálatok tesztelje a rendszer annak érdekében, hogy úgy viselkedik a várt módon.
Például ezt megvizsgálja, győződjön meg arról, webes történő lekérdezéskor megfelelő információkat ad vissza.
Ezek a tesztek távolról futtatni a célcsomópont a valós életben előforduló helyzetek teszteléséhez.
Az integráció teszt parancsfájl keverékével [Pester](https://github.com/pester/Pester/wiki) és [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) szintaxist.

## <a name="define-the-build"></a>A build meghatározása

Most, hogy elvégeztük TFS kód feltölti és tekintett meg működés, is határozza meg a build.

Itt azt érintünk csak a fogja hozzáadni a buildre build lépéseket. Build definíció létrehozása a TFS-ben, lásd: [létrehozása és a várólista build definíció](https://www.visualstudio.com/en-us/docs/build/define/create).

Hozzon létre egy új build definition (válassza ki a **üres** sablon) "InfraDNS" nevű.
Adja hozzá az alábbi lépések végrehajtásával meg build definíciója:

- PowerShell-parancsfájl
- Vizsgálati eredmények közzététele
- Fájlok másolása
- Összetevő közzététele

Ezek lépések felépítéséhez, az alábbiak szerint minden lépés tulajdonságainak szerkesztése hozzáadása után:

### <a name="powershell-script"></a>PowerShell-parancsfájl

1. Állítsa be a **típus** tulajdonságot `File Path`.
1. Állítsa be a **parancsfájl elérési útján** tulajdonságot `initiate.ps1`.
1. Adja hozzá `-fileName build` számára a **argumentumok** tulajdonság.

Ez a lépés build a `initiate.ps1` fájlt, amely meghívja a psake build parancsfájlt.

### <a name="publish-test-results"></a>Vizsgálati eredmények közzététele

1. Állítsa be **Eredményformátum tesztelése** számára`NUnit`
1. Állítsa be **teszteredményei fájlok** számára`InfraDNS/Tests/Results/*.xml`
1. Állítsa be **futtatási cím tesztelése** való `Unit`.
1. Győződjön meg arról, hogy **beállítások** **engedélyezve** és **mindig fusson** biztosan mindkét kiválasztott.

A build lépés a egység tesztek fut a Microsoft megvizsgálta a korábbi Pester parancsfájl, és tárolja az eredményeket a `InfraDNS/Tests/Results/*.xml` mappát.

### <a name="copy-files"></a>Fájlok másolása

1. Adja hozzá a következő sorok **tartalma**:

    ```
    initiate.ps1
    **\deploy.ps1
    **\Acceptance\**
    **\Integration\**
    ```

1. Állítsa be **TargetFolder** számára`$(Build.ArtifactStagingDirectory)\`

Ezt a lépést, másolja át a összeállítása és tesztelése a parancsfájlok az átmeneti könyvtárhoz úgy, hogy a tehetők közzé, az összetevők létrehozása a következő lépésben.

### <a name="publish-artifact"></a>Összetevő közzététele

1. Állítsa be **közzététele elérési út** számára`$(Build.ArtifactStagingDirectory)\`
1. Állítsa be **Adatösszetevőt nevét** számára`Deploy`
1. Állítsa be **összetevő típus** számára`Server`
1. Válassza ki `Enabled` a **beállításokat**

## <a name="enable-continuous-integration"></a>Folyamatos integráció engedélyezése

Most egy eseményindítót, melynek következtében a projekt felépítéséhez bármikor be lesznek állítva a módosítása a beadása a `ci-cd-example` a git-tárház főágába.

1. A TFS rendszerben kattintson a **Build & kiadási** lap
1. Válassza ki a `DNS Infra` definíció létrehozása, és kattintson a **szerkesztése**
1. Kattintson a **eseményindítók** lap
1. Válassza ki **folyamatos integrációt (CI)**, és válassza ki `refs/heads/ci-cd-example` a fiókiroda legördülő lista
1. Kattintson a **mentése** , majd **OK**

Most már minden változása a TFS git-tárház eseményindítók egy automatizált build.

## <a name="create-the-release-definition"></a>A kiadási definíció létrehozása

Hozzon létre egy kiadási definícióját, hogy a projekt központi telepítése a fejlesztési környezet minden kód be.

Ehhez az szükséges, hozzáadása új kiadási társított a `InfraDNS` korábban létrehozott definíció létrehozása.
Ügyeljen arra, hogy válasszon **folyamatos üzembe helyezés** , hogy az új kiadási indul bármikor új buildverziót befejeződött.
([Hogyan: kiadás definíciók együttműködve](https://www.visualstudio.com/en-us/docs/build/actions/work-with-release-definitions)), és konfigurálja az alábbiak szerint:

A kiadási definition vegye fel az alábbi lépéseket:

- PowerShell-parancsfájl
- Vizsgálati eredmények közzététele
- Vizsgálati eredmények közzététele

A lépések az alábbiak szerint szerkesztése:

### <a name="powershell-script"></a>PowerShell-parancsfájl

1. Állítsa be a **parancsfájl elérési útján** mezőről`$(Build.DefinitionName)\Deploy\initiate.ps1"`
1. Állítsa be a **argumentumok** mezőről`-fileName Deploy`

### <a name="first-publish-test-results"></a>Először a vizsgálati eredmények közzététele

1. Válassza ki `NUnit` a a **teszt Eredményformátum** mező
1. Állítsa be a **vizsgálati eredményeket tartalmazó fájlokat** mezőről`$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Integration*.xml`
1. Állítsa be a **futtatási cím tesztelése** számára`Integration`
1. A **beállítások**, ellenőrizze **mindig futtatása**

### <a name="second-publish-test-results"></a>Vizsgálati eredmények második közzététele

1. Válassza ki `NUnit` a a **teszt Eredményformátum** mező
1. Állítsa be a **vizsgálati eredményeket tartalmazó fájlokat** mezőről`$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Acceptance*.xml`
1. Állítsa be a **futtatási cím tesztelése** számára`Acceptance`
1. A **beállítások**, ellenőrizze **mindig futtatása**

## <a name="verify-your-results"></a>Az eredmények ellenőrzése

Most, bármikor leküldéses módosítások a `ci-cd-example` TFS és az új buildverziót ág indul el.
A létrehozás sikeresen befejeződik, ha egy új központi telepítési elindul.

Ellenőrizheti a telepítés eredményét, nyisson meg egy böngészőt, az ügyfélszámítógépen, és navigáljon `www.contoso.com`.

## <a name="next-steps"></a>További lépések

Ebben a példában a DNS-kiszolgáló konfigurálása `TestAgent1` , hogy az URL-cím `www.contoso.com` oldja fel `TestAgent2`, de nem telepítheti valójában a webhely.
A vázat úgy valósul meg a tárházban alatt a `WebApp` mappát.
A kódcsonkok psake parancsfájlok, Pester a és a DSC-konfigurációk létrehozásához megadott segítségével telepítheti a saját webhelyén.







