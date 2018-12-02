---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Erőforrás-készítési ellenőrzőlista
ms.openlocfilehash: 2b6e972776dba4ecc6fd1ab5c21361d653e1a469
ms.sourcegitcommit: e24525046dd37166b9d83eeecdc534726316f429
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/01/2018
ms.locfileid: "52742839"
---
# <a name="resource-authoring-checklist"></a>Erőforrás-készítési ellenőrzőlista

Ezzel az ellenőrzőlistával az ajánlott eljárások listája, amikor új DSC-erőforrások szerzői.

## <a name="resource-module-contains-psd1-file-and-schemamof-for-every-resource"></a>Resource modul .psd1 fájlban, és minden erőforráshoz schema.mof tartalmaz

Ellenőrizze, hogy az erőforrás megfelelő szerkezetéről, és minden szükséges fájlokat tartalmazza. Minden erőforrás modul esetleg tartalmaz egy .psd1 fájlban, és minden nem összetett erőforrás schema.mof fájlt kell rendelkeznie. Erőforrások, amelyek nem rendelkeznek a séma szerint nem lesznek felsorolva `Get-DscResource` és a felhasználók nem fognak tudni használni az intellisense ISE-ben ilyen modulokhoz elleni használt kód írásakor.
A könyvtárstruktúra xRemoteFile erőforrás, amely részét képezi, a [xPSDesiredStateConfiguration resource modul](https://github.com/PowerShell/xPSDesiredStateConfiguration), a következőképpen néz ki:

```
xPSDesiredStateConfiguration
    DSCResources
        MSFT_xRemoteFile
            MSFT_xRemoteFile.psm1
            MSFT_xRemoteFile.schema.mof
    Examples
        xRemoteFile_DownloadFile.ps1
    ResourceDesignerScripts
        GenerateXRemoteFileSchema.ps1
    Tests
        ResourceDesignerTests.ps1
    xPSDesiredStateConfiguration.psd1
```

## <a name="resource-and-schema-are-correct"></a>Erőforrás és a séma helyességét

Ellenőrizze az erőforrás-séma (*. schema.mof) fájlt. Használhatja a [DSC erőforrás Designer](https://www.powershellgallery.com/packages/xDSCResourceDesigner) fejlesztése és tesztelése a séma segítségével.
Győződjön meg arról, hogy:

- Tulajdonságtípusok megengedettek helyes-e (pl. ne használjon karakterlánc azokhoz a tulajdonságokhoz, amelyek elfogadják a numerikus értékek, akkor érdemes használni UInt32 más numerikus típusok)
- Tulajdonság attribútumok helyesen van megadva: ([kulcs], [kötelező], [írási], [olvasási])
- Legalább egy paramétert a sémában rendelkezik kell megjelölni, [key]
- [olvasható] tulajdonság nem létezhet együtt bármelyik: [kötelező], [key], [írási]
- Ha több minősítők meg van adva, [olvasási] kivételével, [key] lép érvénybe
- Ha [írási] és [kötelező] van megadva, majd [kötelező] elsőbbséget élvez
- ValueMap megadott adott esetben az a példában:

  ```
  [Read, ValueMap{"Present", "Absent"}, Values{"Present", "Absent"}, Description("Says whether DestinationPath exists on the machine")] String Ensure;
  ```

- Felhasználóbarát név van megadva, és megerősíti, hogy elnevezési konvencióinak DSC

  Példa: `[ClassVersion("1.0.0.0"), FriendlyName("xRemoteFile")]`

- Minden mező rendelkezik kifejező leírást. A PowerShell GitHub-adattár tartozik jó példa, például [a. a xRemoteFile schema.mof](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCResources/MSFT_xRemoteFile/MSFT_xRemoteFile.schema.mof)

Ezenkívül használjon **Test-xDscResource** és **Test-xDscSchema** parancsmagjait [DSC erőforrás Designer](https://www.powershellgallery.com/packages/xDSCResourceDesigner) automatikusan ellenőrizhető, hogy az erőforrások és a séma:

```
Test-xDscResource <Resource_folder>
Test-xDscSchema <Path_to_resource_schema_file>
```

Például:

```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof
```

## <a name="resource-loads-without-errors"></a>Hiba nélkül betölt erőforrás

Ellenőrizze, hogy az erőforrás-modul sikeresen tölthetők be.
Ez a érhető el manuálisan a futó `Import-Module <resource_module> -force` , hogy nem lépett megerősíti, a írása és automatizált tesztelést. Az utóbbi esetén ez a struktúra a Teszteset a követheti:

```powershell
$error = $null
Import-Module <resource_module> –force
If ($error.count –ne 0) {
    Throw “Module was not imported correctly. Errors returned: $error”
}
```

## <a name="resource-is-idempotent-in-the-positive-case"></a>Erőforrás áll a pozitív esetben idempotens

A DSC-erőforrások alapvető jellemzői egyik idempotencia. Ez azt jelenti, hogy egy adott erőforrást tartalmazó többször DSC-konfiguráció alkalmazása mindig éri el a ugyanazt az eredményt. Például, ha létrehozunk egy konfigurációt, amely tartalmazza a következő fájl erőforrás:

```powershell
File file {
    DestinationPath = "C:\test\test.txt"
    Contents = "Sample text"
}
```

Alkalmazás először, utáni fájl teszt.txt meg kell jelennie `C:\test` mappát. Utólagosan ugyanazt a konfigurációt, azonban ne módosítsa a gép állapota (pl. nincs másolatait a `test.txt` fájlt kell létrehozni).
Annak biztosítása érdekében erőforrás többször is meghívhat idempotens `Set-TargetResource` közvetlenül az erőforrás ellenőrzése, vagy hívja `Start-DscConfiguration` Ha ezt többször is feldolgozza, teljes körű tesztelés. Az eredmény azonosnak kell lennie minden futtatása után.

## <a name="test-user-modification-scenario"></a>Tesztkörnyezet felhasználói módosítása

A gép állapotát, és majd újbóli DSC, ellenőrizheti, hogy `Set-TargetResource` és `Test-TargetResource` megfelelő működéséhez. Az alábbiakban a lépéseket kell tennie:

1. Indítsa el az erőforrás nem a kívánt állapotban.
2. Futtassa az erőforrás-konfiguráció
3. Győződjön meg arról `Test-DscConfiguration` igaz értéket ad vissza
4. Módosítsa a kívánt állapotban a konfigurált cikk
5. Győződjön meg arról `Test-DscConfiguration` false értéket adja vissza

Íme egy beállításjegyzék-erőforrást használ több konkrét példa:

1. Indítsa el a rendszerleíró kulcsot nem a kívánt állapotban
2. Futtatás `Start-DscConfiguration` konfigurációval, a kívánt állapotban és ellenőrzi, hogy adja át.
3. Futtatás `Test-DscConfiguration` , és ellenőrizze, hogy igaz értéket ad vissza
4. A kulcsnak az értéke módosíthatja, hogy nem szerepel a kívánt állapot
5. Futtatás `Test-DscConfiguration` , és ellenőrizze a hamis értéket ad vissza
6. `Get-TargetResource` funkciók a rendszer ellenőrizte használatával `Get-DscConfiguration`

`Get-TargetResource` az aktuális állapotát az erőforrás részleteit adja vissza. Győződjön meg arról, hogy kipróbáljuk meghívásával `Get-DscConfiguration` a konfiguráció alkalmazásához, és a gép aktuális állapotát tükröző, amely a megfelelő kimeneti ellenőrzése után. Fontos, hogy külön-külön tesztelni, mivel ez a terület esetleg felmerülő problémákat többé nem jelenik meg, hívásakor `Start-DscConfiguration`.

## <a name="call-getsettest-targetresource-functions-directly"></a>Hívás **Get/Set/Test-TargetResource** közvetlenül függvények

Ellenőrizze, hogy tesztelje a **Get/Set/Test-TargetResource** közvetlen hívása és annak ellenőrzésére, hogy azok a várt módon működik az erőforrásban implementált függvények.

## <a name="verify-end-to-end-using-start-dscconfiguration"></a>Ellenőrizze a teljes körű használatával **Start-DscConfiguration**

Tesztelés **Get/Set/Test-TargetResource** őket közvetlenül meghívásával függvények azért fontos, de ezzel a módszerrel nem minden problémák lesz felderítve. Irányul, hogy a tesztelés használatával jelentős része `Start-DscConfiguration` vagy a lekéréses kiszolgálón. Sőt ez a felhasználók hogyan használja az erőforrást, ezért nem alábecsülni tesztet hajt végre ilyen típusú a jelentősége.
Problémák lehetséges típusait:

- Hitelesítő adat/munkamenet előfordulhat, hogy eltérően viselkednek, mivel szolgáltatásként fut a DSC-ügynök.  Mindenképp tesztelje a szolgáltatásokat itt teljes körű.
- Hibák kimenetét `Start-DscConfiguration` jelenik meg, ha a hívó eltérő lehet a `Set-TargetResource` függvényt közvetlenül.

## <a name="test-compatability-on-all-dsc-supported-platforms"></a>Teszt kompatibilitási minden DSC a támogatott platformok

Erőforrás működnie kell az összes DSC támogatott platformon (Windows Server 2008 R2 és újabb). Telepítse a WMF legújabb Verziójára (a Windows Management Framework) az operációs rendszer DSC legújabb verziójának beszerzéséhez. Ha az erőforrás nem működik egyes ezekről a platformokról elvárt, vissza kell egy adott hibaüzenetet. Ügyeljen arra, hogy az erőforrás ellenőrzi, hogy az adott gép jelen-e parancsmagok hívja meg. A Windows Server 2012 új parancsmagok, amelyek nem érhetők el a Windows Server 2008R2, a WMF telepítése mellett is nagy számú hozzá.

## <a name="verify-on-windows-client-if-applicable"></a>Ellenőrizze a Windows ügyfél (ha van)

Egy nagyon gyakori teszt gap ellenőrzi az erőforrás csak a Windows server verzióit. Sok erőforrást is tervezték, hogy működik az ügyfél SKU-k, ezért ha ez az Ön esetében igaz, ne felejtse el platformokhoz is tesztelni.

## <a name="get-dscresource-lists-the-resource"></a>Get-DSCResource listázza az erőforrás

A modul telepítése után hívása `Get-DscResource` többek között az erőforrás ezért felsorolásban szerepelnie kell. Ha az erőforrás nem található a listában, ellenőrizze, hogy a schema.mof fájlt a erőforrás létezik.

## <a name="resource-module-contains-examples"></a>Erőforrás-modul példákat tartalmaz

Mező segít másoknak létrehozása minőség példákat megtudhatja, hogyan használhatja azt. Ez különösen fontos, különösen, mivel sok felhasználó mintakód gyökérkönyvtárral dokumentációját.

- Először döntse el, hogy a modul – legalább tartalmazni fogja a bemutatott példákat, ki kell terjednie az erőforrás legfontosabb alkalmazási helyzetek:
- Ha a modul számos olyan erőforrásokat tartalmaz, egy végpontok közötti forgatókönyv működjön együtt van szükség, az alapszintű teljes körű ideális esetben lehet például első.
- Lehet, hogy a kezdeti példák nagyon egyszerű – az erőforrások (pl. létrehozásakor egy új virtuális merevlemez) kis méretű kezelhető tömbökben az első lépések
- További példák kell, ezek példák (például egy virtuális gép létrehozása virtuális merevlemezből, eltávolítja a virtuális gép, virtuális gép módosítása) buildet, és összetettebb funkciók (például egy virtuális gép létrehozása a dinamikus memória) megjelenítése
- Érdemes lehet paraméterezni, például konfigurációk (összes értéket kell átadni a konfigurációhoz meg paraméterként, és nincsenek nem változtatható értékek kell lennie):

  ```powershell
  configuration Sample_xRemoteFile_DownloadFile
  {
    param
    (
        [string[]] $nodeName = 'localhost',

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String] $destinationPath,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String] $uri,

        [String] $userAgent,

        [Hashtable] $headers
    )

    Import-DscResource -Name MSFT_xRemoteFile -ModuleName xPSDesiredStateConfiguration

    Node $nodeName
    {
        xRemoteFile DownloadFile
        {
            DestinationPath = $destinationPath
            Uri = $uri
            UserAgent = $userAgent
            Headers = $headers
        }
    }
  }
  ```

- Tanácsos hogyan hívhat meg a konfiguráció a példa parancsfájl végén található tényleges értékkel (megjegyzésekkel ki) példa tartalmazza.
  Ha például a fenti konfigurációban nem feltétlenül nyilvánvaló, hogy van-e a legjobb módszer UserAgent adja meg:

  `UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer` Ebben az esetben egy megjegyzést a konfiguráció a tervezett végrehajtási jól átláthatók:

  ```powershell
  <#
  Sample use (parameter values need to be changed according to your scenario):

  Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg"

  Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg" `
  -userAgent [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer -headers @{"Accept-Language" = "en-US"}
  #>
  ```

- Minden egyes például írjon egy rövid leírást, amely bemutatja, mire használható, és a paraméterek jelentése.
- Ellenőrizze, hogy az erőforrás fontos a legtöbb forgatókönyvre példákat, és ha semmit nem hiányzik, ellenőrizze, hogy az összes végrehajtás, és helyezze a gép a kívánt állapotban.

## <a name="error-messages-are-easy-to-understand-and-help-users-solve-problems"></a>Hibaüzenetek a következők így könnyen megismerhető és segítség a felhasználóknak a problémák megoldása

Lesz helyes hibaüzenetek:

- : A legnagyobb problémát hibaüzenetek, hogy azok milyen gyakran nem létezik, ezért ügyeljen arra, hogy vannak-e.
- Könnyen áttekinthető: emberi olvasható, nem homályos hibakódok
- Pontos: Mi az, hogy pontosan a probléma leírása
- Vélelmezett: Tanácsokat a probléma megoldása
- Udvarias: Nem blame felhasználói, vagy azt gondolja hibás

Győződjön meg arról, ellenőrizze, hogy a végpontok közötti forgatókönyvek hibákat (használatával `Start-DscConfiguration`), mert előfordulhat, hogy különböznek azoktól, akik közvetlenül erőforrásfüggvények futtatásakor kapott.

## <a name="log-messages-are-easy-to-understand-and-informative-including-verbose-debug-and-etw-logs"></a>Naplóüzenetek, könnyen érthető és informatív (beleértve a – részletes, – hibakeresési és ETW-naplók)

Győződjön meg arról, hogy az erőforrás által használt kimeneti adattípus naplók elsajátítása, és adjon meg értéket a felhasználóhoz. Erőforrások jeleníti meg minden olyan információt, amely a felhasználó számára hasznos lehet, de további naplók nem mindig jobb. Érdemes elkerülése érdekében a redundancia és a ad ki adatokat, amelyek nem adja meg a további értékek – ne valaki naplóbejegyzések több száz hajtania annak érdekében, hogy találja, amit keresnek. Természetesen nincs napló nem az elfogadható megoldás a probléma vagy.

Tesztelésekor, emellett részletes elemzését és hibakeresési naplók (futtatásával `Start-DscConfiguration` a `–Verbose` és `–Debug` vált megfelelően), illetve ETW-naplók formájában. DSC ETW-naplók megtekintéséhez nyissa meg az eseménynaplót, és nyissa meg a következő mappát: alkalmazások és szolgáltatások – Microsoft - Windows - Desired State Configuration.  Alapértelmezés szerint nincs fog műveleti csatorna lehet, de ellenőrizze, hogy engedélyezi a elemzési és hibakeresési csatornák a konfiguráció futtatása előtt.
Engedélyezi az elemzési és hibakeresési csatornák, hajtsa végre az alábbi parancsfájlt:

```powershell
$statusEnabled = $true
# Use "Analytic" to enable Analytic channel
$eventLogFullName = "Microsoft-Windows-Dsc/Debug"
$commandToExecute = "wevtutil set-log $eventLogFullName /e:$statusEnabled /q:$statusEnabled   "
$log = New-Object System.Diagnostics.Eventing.Reader.EventLogConfiguration $eventLogFullName
if($statusEnabled -eq $log.IsEnabled)
{
    Write-Host -Verbose "The channel event log is already enabled"
    return
}
Invoke-Expression $commandToExecute
```

## <a name="resource-implementation-does-not-contain-hardcoded-paths"></a>Erőforrás-implementáció nem tartalmaz szoftveresen kötött elérési utak

Győződjön meg, hogy nincsenek szoftveresen kötött elérési utak erőforrás végrehajtásában, különösen akkor, ha a nyelvi azt feltételezik (en-us), vagy ha rendszerváltozók használható.
Ha az erőforrás eléréséhez egyedi elérési utak, a környezeti változók használata helyett hardcoding kell az elérési út, ahogy más gépeken eltérő lehet.

Példa:

ahelyett, hogy:

```powershell
$tempPath = "C:\Users\kkaczma\AppData\Local\Temp\MyResource"
$programFilesPath = "C:\Program Files (x86)"
```

Írhat:

```powershell
$tempPath = Join-Path $env:temp "MyResource"
$programFilesPath = ${env:ProgramFiles(x86)}
```

## <a name="resource-implementation-does-not-contain-user-information"></a>Erőforrás-implementáció nem tartalmaz felhasználói adatokat

Ellenőrizze, hogy nincsenek e-mail neveket, fiók adatait, vagy a kódban személyek nevét.

## <a name="resource-was-tested-with-validinvalid-credentials"></a>Erőforrás teszteltük érvényes/érvénytelen hitelesítő adatok

Ha az erőforrás paraméterként vesz igénybe egy hitelesítő adatot:

- Ellenőrizze az erőforrás működését, amikor a helyi rendszer (vagy távoli erőforrásokhoz tartozó számítógépfiók) nem rendelkezik hozzáféréssel.
- Ellenőrizze az erőforrás működik a megadott hitelesítő adatok Get, Set és tesztelése
- Ha az erőforráshoz fér hozzá a megosztásokat, teszteléséhez szüksége támogatásra, mint például variantní hodnoty:
  - Szabványos windows-megosztásokat.
  - Elosztott fájlrendszer-megosztásokat.
  - SAMBA megosztások (Ha szeretne Linux támogatja.)

## <a name="resource-does-not-require-interactive-input"></a>Erőforrás nem igényel interaktív bemenet

**Get/Set/Test-TargetResource** függvények automatikusan hajtható végre, és nem kell megvárja, hogy felhasználói bevitel végrehajtási bármely szakaszában (pl. ne használjon `Get-Credential` ezek a függvények belül). Ha meg kell adnia a felhasználói bevitel, meg kell adja át azt a konfigurációs paraméterként a fordítási fázis során.

## <a name="resource-functionality-was-thoroughly-tested"></a>Erőforrás-funkciókat alaposan tesztelés

Ezzel az ellenőrzőlistával elemek, amelyek fontosak, tesztelését és/vagy gyakran vannak-e elmulasztott tartalmazza. Többféle teszteket, elsősorban olyan működési azokat, amely jellemző az erőforrás éppen tesztel, és nem szerepelnek itt lesz. Ne felejtse el kapcsolatos negatív vizsgálati eset.

## <a name="best-practice-resource-module-contains-tests-folder-with-resourcedesignertestsps1-script"></a>Ajánlott eljárás: Resource modul tesztek mappát ResourceDesignerTests.ps1 szkript tartalmaz

A mappa "teszt" resource modul belül létrehozásához hozzon létre egy célszerű `ResourceDesignerTests.ps1` fájlt, és adja hozzá a tesztek segítségével **Test-xDscResource** és **Test-xDscSchema** található összes erőforrást a megadott modul.
Így gyorsan ellenőrizheti az adott modulok és a megerősítést a közzététel előtt ellenőrizze az összes erőforrás sémák.
A xRemoteFile `ResourceTests.ps1` rákeresve beállítható:

```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof
```

## <a name="best-practice-resource-folder-contains-resource-designer-script-for-generating-schema"></a>Ajánlott eljárás: erőforrás mappa tartalmazza az erőforrás a Tervező parancsfájlját a séma generálásához

Az egyes erőforrások tartalmaznia kell egy erőforrás tervező parancsfájlt, amely az erőforrás mof sémát hoz létre. Ezt a fájlt kell elhelyezni a `<ResourceName>\ResourceDesignerScripts` Generate neve lehet, és `<ResourceName>Schema.ps1` xRemoteFile erőforrás ezt a fájlt hívható `GenerateXRemoteFileSchema.ps1` és tartalmaznak:

```powershell
$DestinationPath = New-xDscResourceProperty -Name DestinationPath -Type String -Attribute Key -Description 'Path under which downloaded or copied file should be accessible after operation.'
$Uri = New-xDscResourceProperty -Name Uri -Type String -Attribute Required -Description 'Uri of a file which should be copied or downloaded. This parameter supports HTTP and HTTPS values.'
$Headers = New-xDscResourceProperty -Name Headers -Type Hashtable[] -Attribute Write -Description 'Headers of the web request.'
$UserAgent = New-xDscResourceProperty -Name UserAgent -Type String -Attribute Write -Description 'User agent for the web request.'
$Ensure = New-xDscResourceProperty -Name Ensure -Type String -Attribute Read -ValidateSet "Present", "Absent" -Description 'Says whether DestinationPath exists on the machine'
$Credential = New-xDscResourceProperty -Name Credential -Type PSCredential -Attribute Write -Description 'Specifies a user account that has permission to send the request.'
$CertificateThumbprint = New-xDscResourceProperty -Name CertificateThumbprint -Type String -Attribute Write -Description 'Digital public key certificate that is used to send the request.'

New-xDscResource -Name MSFT_xRemoteFile -Property @($DestinationPath, $Uri, $Headers, $UserAgent, $Ensure, $Credential, $CertificateThumbprint) -ModuleName xPSDesiredStateConfiguration2 -FriendlyName xRemoteFile
```

## <a name="best-practice-resource-supports--whatif"></a>Ajánlott eljárás: erőforrás - WhatIf támogatja

Az erőforrás "veszélyes" műveleteket hajt végre, ha tanácsos megvalósítása `-WhatIf` funkciót. Miután elkészült, győződjön meg arról, hogy `-WhatIf` kimeneti megfelelően leírja a műveleteit, amely történne a parancs végrehajtása történt nélkül `-WhatIf` váltani.
Azt is ellenőrizze, hogy a művelet nem futtatható (nem az a csomópont állapota módosul) Ha `–WhatIf` kapcsoló használata.
Például tegyük fel, File erőforrás azt teszteli. Az alábbi, az egyszerű konfigurációs fájlt hoz létre, amely `test.txt` "test" tartalma:

```powershell
configuration config
{
    node localhost
    {
        File file
        {
            Contents="test"
            DestinationPath="C:\test\test.txt"
        }
    }
}
config
```

Ha azt fordítsa le és majd futtassa a konfiguráció a `-WhatIf` kapcsoló, a kimeneti eredménytelen pontosan mi lenne fordulhat elő, ha futtatjuk a konfigurációt. Maga a konfiguráció azonban nem lett végrehajtva (`test.txt` fájl nem jött létre).

```powershell
Start-DscConfiguration -Path .\config -ComputerName localhost -Wait -Verbose -WhatIf
```

```output
VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' =
SendConfigurationApply,'className' = MSFT_DSCLocalConfigurationManager,'namespaceName' =
root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer CHARLESX1 with user sid
S-1-5-21-397955417-626881126-188441444-5179871.
What if: [X]: LCM:  [ Start  Set      ]
What if: [X]: LCM:  [ Start  Resource ]  [[File]file]
What if: [X]: LCM:  [ Start  Test     ]  [[File]file]
What if: [X]:                            [[File]file] The system cannot find the file specified.
What if: [X]:                            [[File]file] The related file/directory is: C:\test\test.txt.
What if: [X]: LCM:  [ End    Test     ]  [[File]file]  in 0.0270 seconds.
What if: [X]: LCM:  [ Start  Set      ]  [[File]file]
What if: [X]:                            [[File]file] The system cannot find the file specified.
What if: [X]:                            [[File]file] The related file/directory is: C:\test\test.txt.
What if: [X]:                            [C:\test\test.txt] Creating and writing contents and setting attributes.
What if: [X]: LCM:  [ End    Set      ]  [[File]file]  in 0.0180 seconds.
What if: [X]: LCM:  [ End    Resource ]  [[File]file]
What if: [X]: LCM:  [ End    Set      ]
VERBOSE: [X]: LCM:  [ End    Set      ]    in  0.1050 seconds.
VERBOSE: Operation 'Invoke CimMethod' complete.
```

Ez a lista tehát nem tekinthető teljesnek, de számos fontos problémák megtervezése, fejlesztése és tesztelése a DSC-erőforrások is történt, amely lefedi.
