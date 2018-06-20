---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Erőforrás-készítési ellenőrzőlista
ms.openlocfilehash: 76d9fecca8618fcc178975465f45cda0d0e04064
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189958"
---
# <a name="resource-authoring-checklist"></a>Erőforrás-készítési ellenőrzőlista
Az alábbi ellenőrzőlista gyakorlati tanácsok listája esetén egy új DSC-erőforrások szerzői.
## <a name="resource-module-contains-psd1-file-and-schemamof-for-every-resource"></a>Erőforrás-modul .psd1 fájl és minden erőforráshoz schema.mof tartalmazza
Ellenőrizze, hogy az erőforrás helyes struktúrával rendelkezik-e, és minden szükséges fájlokat tartalmazza. Minden erőforrás modul tartalmaznia kell egy .psd1 fájlt, és minden nem összetett erőforrás schema.mof fájl kell rendelkeznie. Erőforrásokat, amelyek nem tartalmaznak a séma nem jelenik meg által **Get-DscResource** és a felhasználók nem fognak tudni használni az intellisense ilyen modulokhoz kódot ISE írásakor.
A könyvtárstruktúra xRemoteFile-erőforráshoz tartozik, a [xPSDesiredStateConfiguration erőforrásmodul](https://github.com/PowerShell/xPSDesiredStateConfiguration), a következőképpen néz ki:


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

## <a name="resource-and-schema-are-correct"></a>Erőforrás és a séma helyességéről ##
Ellenőrizze az erőforrás-séma (*. schema.mof) fájl. Használhatja a [DSC erőforrás Designer](https://www.powershellgallery.com/packages/xDSCResourceDesigner/) fejlesztéséhez és teszteléséhez a séma segítségével.
Győződjön meg arról, hogy:
- Helyesek a Tulajdonságok típusa (pl. nem karakterlánc azokhoz a tulajdonságokhoz, amelyek elfogadják a numerikus érték, kell használni: UInt32 vagy más numerikus helyette)
- Tulajdonság attribútumok vannak megadva megfelelően: ([kulcs], [szükséges], [írási], [olvasható])
- A séma legalább egy paramétert kell megjelölni a [kulcsként] rendelkezik
- [olvasható] tulajdonság nem használható együtt: [szükséges], [key], [írási]
- Ha több minősítők [olvasható] kivéve van adva, majd [kulcs] elsőbbséget
- Ha [írási] és [szükséges] van megadva, az elsőbbséget élvez [szükséges]
- ValueMap szükség van megadva.

Példa:
```
[Read, ValueMap{"Present", "Absent"}, Values{"Present", "Absent"}, Description("Says whether DestinationPath exists on the machine")] String Ensure;
```

- Felhasználóbarát név van megadva, és megerősíti, hogy a DSC-elnevezési konvenciók

Példa: ```[ClassVersion("1.0.0.0"), FriendlyName("xRemoteFile")]```

- Minden mezőnek van beszédes leírást. A PowerShell GitHub-tárházban rendelkezik jó példa, például a [a. a xRemoteFile schema.mof](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCResources/MSFT_xRemoteFile/MSFT_xRemoteFile.schema.mof)

Ezen felül kell használnia **teszt-xDscResource** és **teszt-xDscSchema** parancsmagjait [DSC erőforrás Designer](https://www.powershellgallery.com/packages/xDSCResourceDesigner/) erőforrás és séma automatikusan ellenőrzéséhez:
```
Test-xDscResource <Resource_folder>
Test-xDscSchema <Path_to_resource_schema_file>
```
Például:
```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof
```

## <a name="resource-loads-without-errors"></a>Erőforrás-terhelés hibák nélkül ##
Ellenőrizze, hogy az erőforrás-modul sikeresen betölthető legyen.
Ez elérhető manuálisan, futtatásával `Import-Module <resource_module> -force ` erősítse meg, hogy nincs hiba történt, az írása és tesztelési automation. Az utóbbi esetén hajtsa végre ezt a struktúrát a Teszteset a:
```powershell
$error = $null
Import-Module <resource_module> –force
If ($error.count –ne 0) {
    Throw “Module was not imported correctly. Errors returned: $error”
}
```
## <a name="resource-is-idempotent-in-the-positive-case"></a>Erőforrás idempotent pozitív esetben
A DSC-erőforrások alapvető jellemzői egyik azonosítója lesz. Azt jelenti, hogy egy adott erőforrás többször tartalmazó DSC-konfiguráció alkalmazása mindig érhető el ugyanazt az eredményt. Ha például azt, amely tartalmazza a következő fájl erőforrás-konfiguráció létrehozása:
```powershell
File file {
    DestinationPath = "C:\test\test.txt"
    Contents = "Sample text"
}
```
Alkalmazás első indításakor, utáni fájl teszt.txt C:\test mappában kell megjelennie. Azonban későbbi frissítési kísérletei során ugyanaz a konfiguráció nem szükséges módosítani a (pl. nincs másolatot készíteni a teszt.txt fájlról kell létrehozni) a gép állapotát.
Az idempotent ismételten hívása erőforrás biztosításához **Set-TargetResource** az erőforrás ellenőrzése közvetlenül, vagy hívja **Start-DscConfiguration** többször esetén a következőnek teljes körű tesztelés. Az eredmény azonosnak kell lennie minden futtatása után.


## <a name="test-user-modification-scenario"></a>Tesztkörnyezet felhasználó módosítása ##
A gép állapotának módosítása, majd ezután futtassa újból a DSC, ellenőrizheti, hogy **Set-TargetResource** és **teszt-TargetResource** működnek majd megfelelően. Az alábbiakban a lépéseket kell tennie:
1.  Az erőforrás nem a kívánt állapot kezdődik.
2.  Futtassa az erőforrás-konfiguráció
3.  Győződjön meg arról **teszt-DscConfiguration** igaz értéket ad vissza
4.  A konfigurált elem nem a kívánt állapot módosítása
5.  Győződjön meg arról **teszt-DscConfiguration** adja vissza hamis, a beállításjegyzék használata konkrétabb példa:
1.  Indítsa el a beállításkulcs nem található a kívánt állapot
2.  Futtatás **Start-DscConfiguration** elhelyezi a megfelelő állapotban, és győződjön meg arról, hogy a konfiguráció megfelel.
3.  Futtatás **teszt-DscConfiguration** , és ellenőrizze, hogy igaz értéket ad vissza
4.  A kulcs értékének módosítása, hogy nem a megfelelő állapotban van
5.  Futtatás **teszt-DscConfiguration** , és ellenőrizze a hamis értéket ad vissza
6.  Get-TargetResource funkciókat használja a Get-DscConfiguration ellenőrzés

Get-TargetResource térjen vissza az erőforrás jelenlegi állapotával részleteit. Ügyeljen arra, hogy kipróbálja a Get-DscConfiguration hívása után a konfiguráció alkalmazásához, és ellenőrzi, hogy a kimeneti megfelelően tükrözi a gép aktuális állapotát. Fontos, ha kipróbálja külön-külön, mivel ez a terület esetleg felmerülő problémákat nem jelenik meg, Start-DscConfiguration hívásakor.

## <a name="call-getsettest-targetresource-functions-directly"></a>Hívás **Get vagy Set/Test-TargetResource** közvetlenül működik ##

Győződjön meg arról, hogy tesztelje a **Get vagy Set/Test-TargetResource** funkciók valósítják meg az erőforrás őket közvetlenül hívó, valamint annak ellenőrzését, vártnak megfelelően működnek.

## <a name="verify-end-to-end-using-start-dscconfiguration"></a>Ellenőrizze a végpontok közötti használatával **Start-DscConfiguration** ##

Tesztelési **Get vagy Set/Test-TargetResource** azokat közvetlenül meghívásával funkciók azért fontos, de nem minden probléma így fog történni. A tesztelés használatával jelentős részét irányul **Start-DscConfiguration** vagy a lekérési kiszolgálójával. Ez valójában a felhasználók hogyan használják az erőforrás, így nem alulbecsülheti vizsgálatok az ilyen típusú jelentőségét.
Problémák lehetséges típusait:
- Hitelesítő adatok/munkamenet is eltérően viselkednek, mivel szolgáltatásként fut a DSC-ügynök.  Mindenképpen próbálja ki a szolgáltatásokat itt végpont.
- Hibák kimenetét az **Start-DscConfiguration** jelenik meg, ha hívása házirendektől eltérő lehet a **Set-TargetResource** közvetlenül működik.

## <a name="test-compatability-on-all-dsc-supported-platforms"></a>Teszt kompatibilitási összes DSC a támogatott platformok ##
Erőforrás kell működnie az összes DSC támogatott platformon (Windows Server 2008 R2 és újabb). A WMF legújabb Verziójára (a Windows Management Framework) telepítse az operációs rendszer DSC legújabb verziójának. Ha az erőforrás nem működik az egyes ezekről a platformokról úgy lett kialakítva, vissza kell egy specifikus hibaüzenet. Ellenőrizze azt is, az erőforrás ellenőrzi, hogy hívott parancsmagok megtalálható az adott számítógépet. Windows Server 2012 új parancsmagokat, amelyek nem állnak rendelkezésre a Windows Server 2008R2, még akkor is a WMF telepítése számos hozzá.

## <a name="verify-on-windows-client-if-applicable"></a>Ellenőrizze a Windows-ügyfelén (ha van ilyen) ##
Egy nagyon gyakori teszt résnek ellenőrzi az erőforrás csak a Windows server-verziók. Sok erőforrást is tervezték az ügyfél-SKU, így ha, abban az esetben, ha igaz, ne feledje, tesztelje azokat platformokon.
## <a name="get-dscresource-lists-the-resource"></a>Get-DSCResource sorolja fel az erőforrás ##
A modul való telepítése után hívja a Get-DscResource szerepelnie kell többek között az erőforrás eredményeképpen. Ha az erőforrás nem található a listában, győződjön meg arról, hogy schema.mof fájl erőforrás létezik.
## <a name="resource-module-contains-examples"></a>Erőforrás-modul példákat tartalmaz ##
Létrehozása, amely segíteni fog másoknak minőségi példák megtudhatja, hogyan használják. Ez különösen fontos, különösen, mivel számos felhasználó mintakód tekinti dokumentációját.
- Először azt kell meghatározni a példákat is fog szerepelni a modulja – minimum, ki kell terjednie az erőforrás legfontosabb használati esetek:
- Ha a modul több olyan erőforrásokat tartalmaz, működjön együtt egy végpont forgatókönyvhöz szükséges, az alapszintű végpont példa ideális esetben első.
- A kezdeti példák nagyon egyszerű--kell lennie az erőforrásokhoz (pl. a új virtuális merevlemez létrehozása) kis kezelhető csoportokká az első lépések
- További példák kell létrehozása az adott példák (pl. a virtuális gép létrehozása a virtuális Merevlemezek, virtuális gép, módosítja a virtuális gép eltávolításakor) kiszolgálón, és speciális funkciók (például egy virtuális gép létrehozása a dinamikus memória) megjelenítése
- Példa konfigurációk kell paraméteres (összes értéket kell átadni a konfigurációs paraméterek, és nem változtatható értékek lehetnek):
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
- Ajánlott (megjegyzésként, kimenő), hogyan hívhatja meg a konfigurációs folyamat végén a példaként megadott parancsfájlt a tényleges értékeket tartalmaznak.
Például a fenti konfigurációban nem feltétlenül nyilvánvaló, hogy a legjobb adja meg a felhasználói ügynök módja:

`UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer` Ebben az esetben a Megjegyzés szolgálhatnak a konfiguráció kívánt végrehajtása:
```
<#
Sample use (parameter values need to be changed according to your scenario):

Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg"

Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg" `
-userAgent [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer -headers @{"Accept-Language" = "en-US"}
#>
```
- Minden egyes például egy rövid leírást, amelyből megtudhatja, hogyan kezeli, és a paraméterek szerinti írni.
- Ellenőrizze, hogy példák az erőforrás legtöbb fontos forgatókönyvekhez, és ha nincs szükség hiányzik, ellenőrizze, hogy az összes hajtható végre, és a gép be a kívánt állapot.

## <a name="error-messages-are-easy-to-understand-and-help-users-solve-problems"></a>Hibaüzenetek a következők megismeréséhez és problémák megoldására felhasználók könnyen ##
Jó hibaüzenetek kell lennie:
- : A legnagyobb hibaüzenetek probléma, hogy azok gyakran nem létezik, ezért győződjön meg arról, hogy vannak-e.
- Megértse: emberi olvasható, nem homályos hibakódok
- Pontos: Mi az, hogy pontosan a hiba leírása
- Vélelmezett: A Tanácsot a probléma megoldásához
- Udvarias: Nem vétkesség felhasználói vagy azok érzi, hogy rossz gondoskodjon győződjön meg arról, ellenőrizze, hogy teljes körű forgatókönyvekben hibákat (használatával **Start-DscConfiguration**), mert közvetlenül erőforrás funkciók futtatásakor visszaadott azoktól eltérő lehet.

## <a name="log-messages-are-easy-to-understand-and-informative-including-verbose-debug-and-etw-logs"></a>Naplóüzenetek: megértse és informatív (beleértve – részletes, – hibakeresési és ETW-naplók) ##
Gondoskodjon arról, hogy az erőforrás által outputted naplók könnyen megértéséhez, és adjon meg értéket a felhasználóhoz. Erőforrások kell kimeneti minden információt, amely a felhasználó számára hasznos lehet, de további naplók nem mindig jobb. Inkább elkerülése érdekében a redundancia és szerint kiírta volna az adatokat, amelyek nem további értéket adjon meg – nem jelöl valaki halad át több száz naplóbejegyzések ahhoz, hogy mi keresnek található. Természetesen naplókat nincs az elfogadható megoldás a probléma vagy.

Vizsgálatakor kell is részletes elemzéséhez és hibakeresési naplókat (futtatásával **Start-DscConfiguration** a-verbose és – megfelelően debug kapcsolók), illetve mint ETW-naplók. DSC ETW naplók megtekintéséhez nyissa meg az eseménynaplót, és nyissa meg a következő mappát: alkalmazások és szolgáltatások - Microsoft - Windows - célállapot-konfiguráció.  Alapértelmezés szerint nem fog működési csatornát kell, de ellenőrizze, hogy engedélyezi a elemzési és hibakeresési csatornák a konfiguráció futtatása előtt.
Ahhoz, hogy az elemző/Debug csatornák, az alábbi parancsfájl hajthat végre:
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
## <a name="resource-implementation-does-not-contain-hardcoded-paths"></a>Erőforrás-implementáció nem tartalmaz szoftveresen kötött elérési utak ##
Ellenőrizze, hogy nincsenek nincsenek szoftveresen kötött elérési utak erőforrás végrehajtásában, különösen akkor, ha azok feltételezik, hogy nyelvi (en-us), vagy ha az rendszerváltozók használható.
Ha az erőforrás kell egyedi elérési utak, a környezeti változók hardcoding helyett a útvonalat használja, mivel más számítógépeken eltérőek lehetnek.

Példa:

ahelyett, hogy:
```
$tempPath = "C:\Users\kkaczma\AppData\Local\Temp\MyResource"
$programFilesPath = "C:\Program Files (x86)"
 ```
Írhat:
```
$tempPath = Join-Path $env:temp "MyResource"
$programFilesPath = ${env:ProgramFiles(x86)}
```
## <a name="resource-implementation-does-not-contain-user-information"></a>Erőforrás-implementáció nem tartalmaz felhasználói adatokat ##
Győződjön meg arról, hogy nincsenek e-mail nevek, fiók adatait, vagy a kód nevek.
## <a name="resource-was-tested-with-validinvalid-credentials"></a>Erőforrás teszteltük, érvényes érvénytelen hitelesítő adatokkal ##
Ha az erőforrás hitelesítő adatokat fogad paraméterként:
- Az erőforrás works ellenőrizze, ha a helyi rendszer (vagy a távoli erőforrásokhoz tartozó számítógépfiók) nem rendelkezik hozzáféréssel.
- Ellenőrizze az erőforrás működik a megadott hitelesítő adatok beszerzéséhez beállítva, és tesztelése
- Ha az erőforrás megosztások fér hozzá, tesztelése a támogatandó, például a Variant típusú adatok:
  - Szabványos windows-megosztásokat.
  - Elosztott fájlrendszer-megosztásokat.
  - SAMBA megosztások (Ha a támogatni kívánt Linux.)

## <a name="resource-does-not-require-interactive-input"></a>Az erőforrásnál nincs szükség interaktív bemeneti ##
**GET vagy Set/Test-TargetResource** funkciók automatikusan hajtható végre, és nem kell várnia, a felhasználó bármely szakaszában végrehajtási bemeneti (pl. ne használjon **Get-Credential** ezeket a funkciókat belül). Meg kell adnia a felhasználótól, ha meg kell adja át a konfigurációs paramétere a fordítási fázis során.
## <a name="resource-functionality-was-thoroughly-tested"></a>Erőforrás-funkcióit alaposan teszteltük. ##
Ezt az ellenőrző listát tartalmaz elemeket, amelyek fontosak, tesztelése és/vagy gyakran nem talált. Tesztet hajt végre, főleg működési néhányat a meglévők közül ez az éppen tesztel, és itt nem szerepelnek az erőforráshoz adott bunch lesz. Ne feledje kapcsolatos negatív teszteseteket is tartalmaz.
## <a name="best-practice-resource-module-contains-tests-folder-with-resourcedesignertestsps1-script"></a>Az ajánlott eljárás: erőforrásmodul tartalmaz tesztek mappát ResourceDesignerTests.ps1-parancsfájllal ##
Jó gyakorlat mappa "teszt" create erőforrásmodul hozzon létre ResourceDesignerTests.ps1 fájlt, és adja hozzá a teszteket **teszt-xDscResource** és **teszt-xDscSchema** lévő összes erőforrás a megadott a modul.
Ezzel a módszerrel gyorsan ellenőrizheti az adott modulok és egy megerősítést a közzététel előtt ellenőrizze az összes erőforrás sémák.
XRemoteFile ResourceTests.ps1 egyszerűen sikerült meg:
```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof
```
##<a name="best-practice-resource-folder-contains-resource-designer-script-for-generating-schema"></a>Az ajánlott eljárás: erőforrásmappa tartalmaz erőforrás-tervező parancsfájl létrehozásának séma ##
Az egyes erőforrások tartalmaznia kell egy erőforrás tervező parancsfájlt, amely állít elő, az erőforrás mof séma. Ezt a fájlt kell helyezni <ResourceName>\ResourceDesignerScripts és Generate neve lehet<ResourceName>xRemoteFile erőforrás Schema.ps1 esetében a fájl volna hívni GenerateXRemoteFileSchema.ps1 és tartalmaz:
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
## <a name="best-practice-resource-supports--whatif"></a>Az ajánlott eljárás: erőforrás - whatif támogatja ##
Az erőforrás "veszélyes" műveleteket hajt végre, ajánlott a - whatif funkcióinak végrehajtásához. Miután elkészült, győződjön meg arról, hogy whatif kimeneti műveleteket, amelyek történne a parancs végrehajtása történt whatif kapcsoló nélkül helyesen írja le.
Azt is ellenőrizze, hogy a művelet nem futtatható (nem a csomópont állapota módosul) Ha szerepel – whatif paraméter.
Például tételezzük fel, hogy azt fájl erőforrás teszteli. Alább hoz létre a fájl "teszt.txt" tartalom "teszt" egyszerű konfiguráció van:
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
Ha azt fordítási, majd futtassa a konfiguráció a – whatif kapcsolóval a kimeneti ezzel azt jelzi, pontosan mi történne azt a konfigurációs futtatásakor. Maga a konfiguráció azonban nem történt meg (teszt.txt fájl nem jött létre).
```powershell
Start-DscConfiguration -path .\config -ComputerName localhost -wait -verbose -whatif
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

A lista nem teljes körű, de számos fontos problémák tervezési, fejlesztés és tesztelés DSC erőforrások is történt, amely magában foglalja.