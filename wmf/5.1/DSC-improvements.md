---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
title: A WMF 5.1 DSC fejlesztései
ms.openlocfilehash: 04bf8ed820d24f1062e05d19c8f3b0c041298979
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="improvements-in-desired-state-configuration-dsc-in-wmf-51"></a>A célállapot-konfiguráció (DSC) a WMF 5.1 fejlesztései

## <a name="dsc-class-resource-improvements"></a>A DSC osztály erőforrás fejlesztései

A WMF 5.1 rögzített azt az alábbi ismert problémák:
* Ha egy osztály-alapú DSC erőforrás Get() függvény által visszaadott komplex/kivonat táblatípust Get-DscConfiguration üres értékek (null) vagy hibákat adhat vissza.
* Get-DscConfiguration RunAs hitelesítő adatok használata a DSC-konfiguráció hibaüzenetet adja vissza.
* Az osztály-alapú erőforrás összetett konfigurációban nem használható.
* Start-DscConfiguration lefagy, ha az osztály-alapú erőforrás rendelkezik saját típusú tulajdonság.
* Az osztály-alapú erőforrás kizárólagos erőforrásként nem használható.


## <a name="dsc-resource-debugging-improvements"></a>A DSC erőforrás hibakeresési fejlesztései
A WMF 5.0-s a PowerShell hibakereső nem állt le a erőforrás osztály-alapú módszer (Get és Set/tesztelési célú) közvetlenül.
WMF 5.1 a hibakereső nem osztály-alapú erőforrás metódust. a MOF-alapú erőforrások módszerek ugyanúgy.

## <a name="dsc-pull-client-supports-tls-11-and-tls-12"></a>DSC lekérési ügyfél támogatja a TLS 1.1 és TLS 1.2-es
Korábban a DSC lekérési ügyfél csak támogatott SSL3.0 és TLS1.0 HTTPS-kapcsolatokon keresztül.
Kényszerítetten biztonságosabb protokollt használják, amikor a leküldéses ügyfél volna működését.
WMF 5.1 a DSC lekérési ügyfél már nem támogatja az SSL 3.0, és a biztonságosabb a TLS 1.1 és TLS 1.2 protokoll támogatása.

## <a name="improved-pull-server-registration"></a>Továbbfejlesztett lekéréses kiszolgáló regisztrálása ##

WMF korábbi verzióiban egyidejű regisztrációk/reporting kérelmek egy DSC lekérési kiszolgálójával a ESENT adatbázis használatakor regisztrálni és/vagy a jelentést sikerült LCM vezetne.
Ezekben az esetekben az eseménynaplók a lekérési kiszolgálón hibát a "Példány neve már használatban van."
A többszálas forgatókönyvek ESENT-adatbázisának eléréséhez használt helytelen mintát miatt volt.
A WMF 5.1 a probléma kijavítása.
Egyidejű regisztrációk vagy reporting (ESENT adatbázist érintő) szolgáltatás megfelelően működik az WMF 5.1.
A probléma csak a ESENT adatbázis használható, és nem vonatkozik az OLEDB-adatbázisban.

## <a name="enable-circular-log-on-esent-database-instance"></a>Körkörös napló ESENT adatbázispéldányhoz engedélyezése
A DSC-PullServer eariler verzióban ESENT adatbázis naplófájlokat a szabad lemezterület a körkörös naplózás nélkül létrehozásakor az adatbázispéldány fölött pullserver becouse volt betelőben. Ebben a kiadásban lehetősége van a körkörös naplózás működését a példányhoz, a pullserver web.config használatával. Alapértelmezés szerint CircularLogging igaz értékre van beállítva.
```
<appSettings>
    <add key="dbprovider" value="ESENT" />
    <add key="dbconnectionstr" value="C:\Program Files\WindowsPowerShell\DscService\Devices.edb" />
    <add key="CheckpointDepthMaxKB" value="512" />
    <add key="UseCircularESENTLogs" value="TRUE" />
  </appSettings>
```
## <a name="pull-partial-configuration-naming-convention"></a>Lekéréses részleges konfigurációs elnevezési egyezmény
A korábbi változatban az elnevezési részleges-konfiguráció lett, hogy a MOF-fájl neve, a lekéréses/szolgáltatás meg kell felelnie a helyi configuration manager-beállításait, amely pedig meg kell egyeznie a részleges konfiguráció nevét a a beágyazott konfiguráció neve a MOF-fájlban.

Tekintse meg az alábbi pillanatképeket:

• Helyi konfigurációs beállításokat, hogy egy csomópont kap részleges konfiguráció meghatározó.

![A minta metakonfigurációját](../images/MetaConfigPartialOne.png)

• A minta részleges konfiguráció definíciója

```powershell
Configuration PartialOne
{
    Node('localhost')
    {
        File test
        {
            DestinationPath = "$env:TEMP\partialconfigexample.txt"
            Contents = 'Partial Config Example'
        }
    }
}
PartialOne
```

• A (ConfigurationName) beágyazott a generált MOF-fájlban.

![A minta létrehozott mof-fájlt](../images/PartialGeneratedMof.png)

• A lekéréses konfigurációs tárházban fájlnév

![A konfigurációs tárházban fájlnév](../images/PartialInConfigRepository.png)

Azure Automation szolgáltatás neve MOF-fájlok használata a generált `<ConfigurationName>.<NodeName>.mof`.
Az alábbi konfigurációs így PartialOne.localhost.mof lefordítja.

Ez lehetetlenné a részleges konfigurációs egyik lekéréses az Azure Automation szolgáltatás.

```powershell
Configuration PartialOne
{
    Node('localhost')
    {
        File test
        {
            DestinationPath = "$env:TEMP\partialconfigexample.txt"
            Contents = 'Partial Config Example'
        }
    }
}
PartialOne
```

A WMF 5.1, a lekéréses/szolgáltatás egy részleges konfigurációs nevű `<ConfigurationName>.<NodeName>.mof`.
Továbbá a gép van húzza a lekérési egyetlen konfigurációja majd a konfigurációs fájl a lekérési kiszolgálón konfigurációs tárházban kiszolgálószolgáltatás minden olyan fájlnevet rendelkezhet.
Erre a rugalmasságra elnevezési kezelését teszi a csomópontok részben Azure Automation szolgáltatás, ahol egyes a csomópont konfigurációs várható az Azure Automation DSC és helyileg kezelt részleges konfigurációjával.

Alább állítja be egy csomópont lehet metakonfigurációját felügyelt mindkét helyileg, valamint által az Azure Automation szolgáltatás.

```powershell
  [DscLocalConfigurationManager()]
   Configuration RegistrationMetaConfig
   {
        Settings
        {
            RefreshFrequencyMins = 30
            RefreshMode = "PULL"
        }

        ConfigurationRepositoryWeb web
        {
            ServerURL =  $endPoint
            RegistrationKey = $registrationKey
            ConfigurationNames = $configurationName
        }

        # Partial configuration managed by Azure Automation service.
        PartialConfiguration PartialConfigurationManagedByAzureAutomation
        {
            ConfigurationSource = "[ConfigurationRepositoryWeb]Web"
        }

        # This partial configuration is managed locally.
        PartialConfiguration OnPremisesConfig
        {
            RefreshMode = "PUSH"
            ExclusiveResources = @("Script")
        }

   }

   RegistrationMetaConfig
   Set-DscLocalConfigurationManager -Path .\RegistrationMetaConfig -Verbose
 ```

# <a name="using-psdscrunascredential-with-dsc-composite-resources"></a>PsDscRunAsCredential használata DSC összetett erőforrások

Támogatja az [ *PsDscRunAsCredential* ](https://msdn.microsoft.com/cs-cz/powershell/dsc/runasuser) a DSC [összetett](https://msdn.microsoft.com/en-us/powershell/dsc/authoringresourcecomposite) erőforrásokat.

Megadhat egy értéket a PsDscRunAsCredential összetett erőforráshoz, konfigurációk használata esetén.
Megadása esetén összes erőforrás futhat egy összetett erőforrás RunAs felhasználóként.
Ha egy összetett erőforrást egy másik összetett erőforrás, az összes erőforrást is végrehajtása RunAs felhasználóként.
RunAs hitelesítő adatok rendszer nem propagál minden összetett erőforrás hierarchia szintje.
Ha bármilyen olyan erőforrás összetett erőforrás belül PsDscRunAsCredential saját érték Megadja, egy merge hiba eredménye, konfiguráció fordításakor.

Ez a példa bemutatja a használati [WindowsFeatureSet](https://msdn.microsoft.com/en-us/powershell/wmf/dsc_newresources) összetett erőforrás PSDesiredStateConfiguration modulban.



```powershell

Configuration InstallWindowsFeature
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node $AllNodes.NodeName
    {
        WindowsFeatureSet features
        {
            Name = @("Telnet-Client","SNMP-Service")
            Ensure = "Present"
            IncludeAllSubFeature = $true
            PsDscRunAsCredential = Get-Credential
        }
    }

}

$configData = @{
    AllNodes = @(
        @{
            NodeName             = 'localhost'
            PSDscAllowDomainUser = $true
            CertificateFile      = 'C:\publicKeys\targetNode.cer'
            Thumbprint           = '7ee7f09d-4be0-41aa-a47f-96b9e3bdec25'
        }
    )
}


InstallWindowsFeature -ConfigurationData $configData

```

##<a name="dsc-module-and-configuration-signing-validations"></a>DSC modul és a konfigurációs ellenőrzések aláírása
A DSC konfiguráció és a modulok terjesztése a kezelt számítógépek számára a lekérési kiszolgálójáról.
Ha a lekérési kiszolgálójával biztonsága sérül, a támadó potenciálisan módosíthatja a konfigurációkat és a modulok a lekérési kiszolgálón és kell terjeszteni az összes felügyelt csomóponthoz, az összes veszélyeztetése.

 A WMF 5.1 DSC támogatja a katalógus és konfigurációs digitális aláírások ellenőrzése (. MOF) formátumú fájlok.
Ez a szolgáltatás megakadályozza, hogy a csomópontok a konfigurációk vagy fájlok modul, amely nem egy megbízható aláíró aláírásával, vagy amely illetéktelenül után megbízható aláíró által aláírt végrehajtása.



###<a name="how-to-sign-configuration-and-module"></a>Csatlakozás a konfigurációs és modul
***
* Konfigurációs fájlok (. MOF-ot): A meglévő PowerShell-parancsmag [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) ki van bővítve a MOF-fájlok aláírása támogatásához.
* Modulok: Ha bejelentkezik a megfelelő modul katalógus az alábbi lépéseket követve modulok aláírása történik:
    1. Hozzon létre egy katalógusfájlt: egy katalógusfájlt kriptográfiai kivonatokat vagy ujjlenyomatok gyűjteményét tartalmazza.
       Minden egyes ujjlenyomat felel meg egy fájlt, amely a moduljában található.
       A következő új parancsmagját [New-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx), engedélyezése a felhasználók számára hozzon létre egy katalógusfájlt az a modul hozzá lett adva.
    2. A katalógus-fájl aláírásához: használata [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) a katalógus-fájl aláírásához.
    3. Helyezze a katalógus fájlt a modul mappában található.
Szabály szerint modul katalógusfájlt a modul neve megegyezik a modul a mappában kell helyezni.

###<a name="localconfigurationmanager-settings-to-enable-signing-validations"></a>LocalConfigurationManager beállítások aláíró érvényesítést engedélyezése

####<a name="pull"></a>Lekéréses
A csomópont LocalConfigurationManager modulok és a jelenlegi beállításai alapján a konfigurációk aláírási érvényesítést végez.
Az aláírás érvényesítése alapértelmezés szerint le van tiltva.
Az aláírás érvényesítése a "SignatureValidation" blokk hozzáadásával a csomópont látható az alábbi meta-konfiguráció definíciójának engedélyezhető:

```powershell
[DSCLocalConfigurationManager()]
Configuration EnableSignatureValidation
{
    Settings
    {
        RefreshMode = 'PULL'
    }

    ConfigurationRepositoryWeb pullserver{
      ConfigurationNames = 'sql'
      ServerURL = 'http://localhost:8080/PSDSCPullServer/PSDSCPullServer.svc'
      AllowUnsecureConnection = $true
      RegistrationKey = 'd6750ff1-d8dd-49f7-8caf-7471ea9793fc' # Replace this with correct registration key.
    }
    SignatureValidation validations{
        # By default, LCM uses the default Windows trusted publisher store to validate the certificate chain. If TrustedStorePath property is specified, LCM uses this custom store for retrieving the trusted publishers to validate the content.
        TrustedStorePath = 'Cert:\LocalMachine\DSCStore'
        SignedItemType = 'Configuration','Module'         # This is a list of DSC artifacts, for which LCM need to verify their digital signature before executing them on the node.
    }

}
EnableSignatureValidation
Set-DscLocalConfigurationManager -Path .\EnableSignatureValidation -Verbose
 ```

A fenti metakonfigurációját beállítása a csomópont lehetővé teszi, hogy a letöltött konfigurációk és a modulok aláírás érvényesítése.
A helyi Configuration Manager végrehajtja a következő lépéseket a digitális aláírások ellenőrzése.

1. Ellenőrizze a konfigurációs fájl aláírását (. MOF) érvénytelen.
   A PowerShell-parancsmagot használja [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx), amely ki van bővítve 5.1 MOF aláírás érvényesítése támogatásához.
2. Ellenőrizze, hogy a hitelesítésszolgáltató, amely jogosult az aláíró megbízható-e.
3. A konfiguráció modul/erőforrás-függőségek letöltése egy ideiglenes helyre.
4. A katalógus, a modul bekerüljön aláírásának ellenőrzése.
    * Keresés a `<moduleName>.cat` fájlt, és ellenőrizze a parancsmaggal aláírásának [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx).
    * Ellenőrizze, hogy a hitelesített az aláíró hitelesítésszolgáltatót megbízható-e.
    * Ellenőrizze, hogy a modul tartalma nem változott az új parancsmaggal [teszt-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx).
5. Install-modul $env: ProgramFiles\WindowsPowerShell\Modules\
6. A konfigurációs folyamat

> Megjegyzés: Az aláírás érvényesítése modul-katalógus és konfigurációs csak hajtható végre, ha a konfigurációs alkalmazza a rendszer először, vagy ha a modul letöltése és telepítése.
Konzisztencia futtatása nem ellenőrzik az aláírás Current.mof vagy modul függőségeit.
Ellenőrzése nem sikerült fel, ha például ha a konfigurációs lekért a lekérési kiszolgálójával nincs aláírva, majd a konfiguráció feldolgozása leáll, a hiba alább látható és az ideiglenes fájlok törlődnek.

![Minta kimenet Hibakonfigurációját](../images/PullUnsignedConfigFail.png)

Hasonlóképpen húzza egy modult, amelynek a katalógus nem aláírt eredménye a következő hiba:

![A minta hiba kimenetigyorsítótár-modul](../images/PullUnisgnedCatalog.png)

####<a name="push"></a>Leküldéses
Egy leküldéses keresztül konfigurációs előfordulhat, hogy lehessen illetéktelenül módosítani a forrásnál, mielőtt azt a csomópont.
A helyi Configuration Manager hasonló aláírás érvényesítése lépéseket megnyomott vagy közzétett beállítás(ok) hajt végre.
Alább van az aláírás érvényesítése leküldéses átfogó példát.

* A csomópont aláírás-ellenőrzés engedélyezése.

```powershell
[DSCLocalConfigurationManager()]
Configuration EnableSignatureValidation
{
    Settings
    {
        RefreshMode = 'PUSH'
    }
    SignatureValidation validations{
        TrustedStorePath = 'Cert:\LocalMachine\DSCStore'
        SignedItemType =  'Configuration','Module'
    }

}
EnableSignatureValidation
Set-DscLocalConfigurationManager -Path .\EnableSignatureValidation -Verbose
```
* Hozzon létre egy minta konfigurációs fájlt.

```powershell
# Sample configuration
Configuration Test
{

    File foo
    {
        DestinationPath =  "$env:TEMP\signingTest.txt"
        Contents = "ABC"
    }
}
Test
```

* Próbálja meg a nem aláírt konfigurációs fájl küldését csomóponthoz.

```powershell
Start-DscConfiguration -Path .\Test -Wait -Verbose -Force
```
![ErrorUnsignedMofPushed](../images/PushUnsignedMof.png)

* A konfigurációs fájl kódaláíró tanúsítvánnyal aláírásához.

![SignMofFile](../images/SignMofFile.png)

* Próbálja küldését a MOF-fájlját.

![SignMofFile](../images/PushSignedMof.png)