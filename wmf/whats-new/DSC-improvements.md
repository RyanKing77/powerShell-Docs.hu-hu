---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: A WMF 5.1 DSC fejlesztései
ms.openlocfilehash: e7f20bfa865777aeac8f083959782317cfdf6cde
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65856230"
---
# <a name="improvements-in-desired-state-configuration-dsc-in-wmf-51"></a>A Desired State Configuration (DSC) a WMF 5.1 fejlesztései

## <a name="dsc-class-resource-improvements"></a>DSC osztály erőforrás fejlesztései

A WMF 5.1 hogy kijavítása az alábbi ismert problémák:

- Ha egy összetett/kivonat táblatípus osztályalapú DSC-erőforrás Get() függvény által visszaadott Get-DscConfiguration üres (null) értékeket, vagy hibát adhat vissza.
- Get-DscConfiguration hibát ad vissza, ha a RunAs hitelesítő adatok a DSC-konfiguráció használatban van.
- Osztályalapú erőforrás összetett konfigurációban nem használható.
- Start-DscConfiguration lefagy, ha a osztályalapú erőforrás rendelkezik egy tulajdonságot a saját típusú.
- Osztály-alapú erőforrás-kizárólagos erőforrásként nem használható.

## <a name="dsc-resource-debugging-improvements"></a>DSC-erőforrás hibakeresési javításai

A WMF 5.0-a PowerShell-hibakereső nem állt le, az osztály-alapú erőforrás metódus (Get/Set/Test) közvetlenül. A WMF 5.1-es a hibakereső megáll az osztály-alapú erőforrás módszer ugyanúgy, mint a MOF-alapú erőforrások módszerek az.

## <a name="dsc-pull-client-supports-tls-11-and-tls-12"></a>DSC lekérési ügyfél támogatja a TLS 1.1 és TLS 1.2

Korábban a DSC lekérési ügyfél csak támogatott SSL3.0 és TLS1.0 HTTPS-kapcsolaton keresztül. Kényszerített biztonságosabb protokollokra, ha a lekérési ügyfél lenne működni. A WMF 5.1-es a DSC lekérési ügyfél már nem támogatja az SSL 3.0 és a biztonságosabb a TLS 1.1 és TLS 1.2 protokoll támogatása.

## <a name="improved-pull-server-registration"></a>Továbbfejlesztett lekéréses kiszolgáló regisztrálása

A WMF korábbi verzióiban egyidejű regisztrációk/reporting kéréseket a ESENT adatbázis használatakor DSC lekéréses kiszolgálóra LCM regisztrálása és/vagy a jelentés sikertelen vezetne. Ezekben az esetekben az Eseménynapló bejegyzéseit, a lekérési kiszolgálón rendelkezik a hiba "Példány neve már használatban van." Ez a okozta több szálon futó forgatókönyvekben ESENT-adatbázisának eléréséhez használt helytelen mintát. A WMF 5.1 Ez a hiba elhárítása. Egyidejű vagy a reporting (ESENT adatbázist érintő) jól működik, a WMF 5.1-es. Ez a probléma csak a ESENT adatbázis használható, és nem vonatkozik az OLEDB-adatbázishoz.

## <a name="enable-circular-log-on-esent-database-instance"></a>A ESENT adatbázispéldány körkörös napló engedélyezése

DSC-PullServer eariler verziójában a ESENT adatbázis-naplófájlokat is betelik a pullserver becouse az adatbázis-példány létrehozása nélkül a körkörös naplózást, a lemezterület. Ebben a kiadásban lehetősége van a körkörös naplózás viselkedése a példányon a pullserver web.config szabályozására. Alapértelmezés szerint CircularLogging TRUE értékre van állítva.

```xml
<appSettings>
    <add key="dbprovider" value="ESENT" />
    <add key="dbconnectionstr" value="C:\Program Files\WindowsPowerShell\DscService\Devices.edb" />
    <add key="CheckpointDepthMaxKB" value="512" />
    <add key="UseCircularESENTLogs" value="TRUE" />
  </appSettings>
```

## <a name="wow64-support-for-configuration-keyword"></a>A konfigurációs kulcsszó WOW64-támogatása

A `Configuration` kulcsszó mostantól támogatott a WOW64 egy 64 bites számítógépen. Ez azt jelenti, hogy a DSC-konfiguráció definiálhatók és egy 32 bites folyamatként például a Windows PowerShell ISE-ben (x 86) futtat egy 64 bites számítógépen van lefordítva.

## <a name="pull-partial-configuration-naming-convention"></a>Kérje le a részleges konfigurációs elnevezési egyezmény

A korábbi kiadásában egy részleges konfigurációs elnevezési lett, hogy a MOF-fájl neve, a lekéréses/szolgáltatás egyeznie kell a helyi configuration manager elkerülését, amelyek ezután meg kell egyeznie a megadott részben konfiguráció nevével a konfiguráció neve beágyazza a MOF-fájlt.

Az alábbi-pillanatképek megtekintéséhez:

- Helyi konfigurációs beállításokat, amely meghatározza egy részleges konfigurációs csomópont fogadására van engedélyezve.

  ![Minta metaconfiguration](../images/MetaConfigPartialOne.png)

- Minta részleges konfiguráció definíciója

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

- A létrehozott MOF-fájl (ConfigurationName) beágyazott.

  ![Minta létrehozott mof-fájl](../images/PartialGeneratedMof.png)

- A konfigurációs lekérési tárházban fájlnév

  ![A konfigurációs adattárhoz fájlnév](../images/PartialInConfigRepository.png)

  Az Azure Automation szolgáltatás neve MOF-fájlok használata a létrehozott `<ConfigurationName>.<NodeName>.mof`. Ezért az alábbi konfigurációval való PartialOne.localhost.mof lefordítja.

  Ez lehetetlenné lekéréses egy részleges konfigurálásakor az Azure Automation szolgáltatás.

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

  A WMF 5.1-es, a lekéréses/szolgáltatás egy részleges konfigurációt is előtereként `<ConfigurationName>.<NodeName>.mof`. Ezen felül egy gép van lehetőség a lekérési egyetlen konfigurációval kiszolgálók/szolgáltatások a lekéréses kiszolgálón konfigurációs adattárhoz majd a konfigurációs fájlt minden olyan fájlnevet rendelkezhet. E elnevezési rugalmasság lehetővé teszi a csomópontok részlegesen kezelése az Azure Automation szolgáltatás, néhány beállítást a csomópont a az Azure Automation DSC és a egy részleges konfigurációval helyileg kezelt forrását.

  Az alábbi állítja be egy csomópont lehet metaconfiguration felügyelt is helyileg, valamint az Azure Automation által szolgáltatás.

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

## <a name="using-psdscrunascredential-with-dsc-composite-resources"></a>Összetett erőforrások DSC PsDscRunAsCredential használata

Mostantól támogatjuk a [PsDscRunAsCredential](/powershell/dsc/configurations/runAsUser) DSC- [összetett](https://msdn.microsoft.com/powershell/dsc/authoringresourcecomposite) erőforrásokat.

Mostantól megadhatja a egy értéke **PsDscRunAsCredential** összetett erőforrások belül konfigurációk használata esetén. Megadása esetén az összes erőforrás belül futó összetett erőforrás futtató felhasználóként. Ha egy összetett erőforrást egy másik összetett erőforrás, ezeket az erőforrásokat is végrehajtása futtató felhasználóként. RunAs hitelesítő adatokat a rendszer propagálja a webhelyre az összetett erőforrás hierarchia minden szintjére. Ha egy összetett erőforrás belül bármely erőforrás megadja a saját értékét **PsDscRunAsCredential**, egy merge hibát eredményez a konfiguráció fordításakor.

Ez a példa bemutatja a használatot a a [WindowsFeatureSet](/powershell/dsc/reference/resources/windows/windowsfeaturesetresource) PSDesiredStateConfiguration modulban található összetett erőforrást.

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

## <a name="allowing-for-identical-duplicate-resources-in-a-configuration"></a>Azonos ismétlődő erőforrások engedélyezése

Nem engedélyezi a DSC, vagy ütköző erőforrás-definíciókban belül a konfiguráció kezelésére. Az ütközés feloldása helyett egyszerűen meghiúsul. Konfiguráció újbóli több összetett erőforrások révén válik fel, mert ütközés stb. fogja gyakrabban fordulnak elő. Amikor az ütköző erőforrás-definíciókban azonosak, DSC legyen intelligens és ez lehetővé teszi. Ebben a kiadásban támogatott több, azonos definíciókkal rendelkező erőforrás példánnyal rendelkező:

```powershell
Configuration IIS_FrontEnd
{
    WindowsFeature FE_IIS         #Identical resource
    {
        Ensure = 'Present'
        Name = 'Web-Server'
    }

    WindowsFeature FTP
    {
        Ensure = 'Present'
        Name = 'Web-FTP-Server'
    }
}

Configuration IIS_Worker
{
    WindowsFeature Worker_IIS      #Identical resource
    {
        Ensure = 'Present'
        Name = 'Web-Server'
    }

    WindowsFeature ASP
    {
        Ensure = 'Present'
        Name = 'Web-ASP-Net45'
    }
}

Configuration WebApplication
{
    IIS_Frontend Web {}

    IIS_Worker ASP {}
}
```

A korábbi kiadásokban az eredmény lehet a WindowsFeature FE_IIS és annak biztosítása érdekében a webalkalmazás-kiszolgáló szerepkört próbált WindowsFeature Worker_IIS példányok közötti ütközés miatt nem sikerült rendszerezve van telepítve. Figyelje meg, hogy *összes* a folyamatban konfigurált tulajdonságok megegyeznek az alábbi két konfigurációk. Mivel *összes* Ez a két tulajdonság azonos erőforrásokat, emiatt most a sikeres fordítás.

Ha bármely tulajdonsága eltérő a két erőforrás között, nem minősülnek azonos, és a fordítás sikertelen lesz.

## <a name="dsc-module-and-configuration-signing-validations"></a>DSC-modul és a konfigurációs ellenőrzések aláírása

A DSC konfigurációkat és a modulok oszlanak meg a felügyelt számítógépekre a lekérési kiszolgálóról. Ha a pull-kiszolgáló sérül, a támadó potenciálisan módosíthatja a konfigurációkat és a modulok a lekérési kiszolgálón és kell terjeszteni az összes felügyelt csomópont.

A WMF 5.1, DSC támogatja a katalógus és a konfiguráció a digitális aláírások ellenőrzése (. MOF) formátumú fájlok. Ez a funkció meggátolja, hogy a csomópontok konfigurációk vagy amely nem egy megbízható aláíró által aláírt, vagy amelyek illetéktelenül után megbízható aláíró által aláírt modul fájlok végrehajtása.

### <a name="how-to-sign-configuration-and-module"></a>Csatlakozás a konfigurációs és modul

- Konfigurációs fájlok (. MOF-fájlok): A meglévő PowerShell-parancsmag [Set-AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Set-AuthenticodeSignature) ki van bővítve a MOF-fájlok-aláírás támogatásához.
- Modulok: Aláírás-modulok végzi el a megfelelő modul katalógus az alábbi lépéseket követve aláíró:
  1. Hozzon létre egy katalógus fájlt: A katalógus kriptográfiai kivonatokat vagy ujjlenyomat gyűjteményét tartalmazza. Minden egyes ujjlenyomat felel meg egy fájlt, amely a modul része. Új parancsmag [New-FileCatalog](/powershell/module/microsoft.powershell.security/new-filecatalog), engedélyezze a felhasználók számára, hogy a modul olyan katalógusfájlt bővült.
  2. A katalógus-fájl aláírásához: Használat [Set-AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Set-AuthenticodeSignature) a katalógus-fájl aláírásához.
  3. Helyezze a katalógus-fájlt a modul mappán belül. Szabályok szerint modul katalógus fájl neve megegyezik a modul az a modul mappában kell elhelyezni.

### <a name="localconfigurationmanager-settings-to-enable-signing-validations"></a>Aláírás-ellenőrzés engedélyezése LocalConfigurationManager beállításai

#### <a name="pull"></a>A lekéréses

A csomópont a LocalConfigurationManager aláíró érvényesítési modulok és konfigurációk a jelenlegi beállításai alapján hajt végre. Aláírás-ellenőrzése alapértelmezés szerint le van tiltva. Aláírás-ellenőrzése a "SignatureValidation" blokk hozzáadásával a csomópont látható az alábbi meta-konfiguráció definíciójának engedélyezhető:

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
        # If the TrustedStorePath property is provided then LCM will use the custom path. Otherwise, the LCM will use default trusted store path (Cert:\LocalMachine\DSCStore) to find the signing certificate.
        TrustedStorePath = 'Cert:\LocalMachine\DSCStore'
        SignedItemType = 'Configuration','Module'         # This is a list of DSC artifacts, for which LCM need to verify their digital signature before executing them on the node.
    }

}
EnableSignatureValidation
Set-DscLocalConfigurationManager -Path .\EnableSignatureValidation -Verbose
```

A csomópont a fenti metaconfiguration beállítás lehetővé teszi, hogy a letöltött konfigurációkat és a modulok az aláírás-ellenőrzése. A Local Configuration Manager végrehajtja a következő lépéseket a digitális aláírások ellenőrzése.

1. A konfigurációs fájl aláírásának ellenőrzése (. Érvénytelen MOF) használatával a `Get-AuthenticodeSignature` parancsmagot.
2. Ellenőrizze, hogy jogosult az aláíró hitelesítésszolgáltató megbízható-e.
3. Töltse le a konfigurációs modul és az erőforrások függőségeinek egy ideiglenes helyre.
4. A katalógus tartalmazza a modulban aláírásának ellenőrzésére.
   - Keresse meg a `<moduleName>.cat` fájlt, és ellenőrizze az aláírás használatával `Get-AuthenticodeSignature`.
   - Ellenőrizze, hogy a hitelesített az aláíró hitelesítésszolgáltatót megbízható-e.
   - Ellenőrizze, hogy a modul tartalma nem módosították az új parancsmaggal `Test-FileCatalog`.
5. `Install-Module` A `$env:ProgramFiles\WindowsPowerShell\Modules\`
6. A konfigurációs folyamat

> [!NOTE]
> A modul-katalógus és konfigurációs aláírás-ellenőrzése csak akkor hajtható végre, ha a konfigurációt alkalmazza a rendszer először, vagy ha a modul letöltését és telepítését.
> Konzisztencia-futtatások nem ellenőrzik az aláírás Current.mof vagy a modul függőségeit. Ellenőrzése nem sikerült minden fázisban, ha például ha a konfiguráció az abból lekért a lekéréses kiszolgálón nincs aláírva, majd az alábbi hiba miatt leállítja a konfiguráció feldolgozása és az ideiglenes fájlok törlése.

![Példa hiba kimeneti konfigurációja](../images/PullUnsignedConfigFail.png)

Hasonlóképpen egy modult, amelynek a katalógus nincs lehetőség aláírt a következő hibaüzenetet eredményezi:

![Minta hiba kimeneti modul](../images/PullUnisgnedCatalog.png)

#### <a name="push"></a>Leküldéses

Ügyfélleküldés használatával kommunikálásra előfordulhat, hogy lehessen illetéktelenül módosítani a forrásban mielőtt megkapná a csomópont azt. A Local Configuration Manager leküldött vagy közzétett beállítás(ok) aláírás-ellenőrzés hasonló lépéseket hajtja végre. Alább az aláírás-ellenőrzése leküldés teljes példát.

- Engedélyezze az aláírás-ellenőrzése a csomóponton.

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

- Hozzon létre egy minta konfigurációs fájlt.

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

- Próbálja ki a nem aláírt konfigurációs fájlt leküldése a csomópontot.

  ```powershell
  Start-DscConfiguration -Path .\Test -Wait -Verbose -Force
  ```

  ![ErrorUnsignedMofPushed](../images/PushUnsignedMof.png)

- A konfigurációs fájl használatával kódaláíró tanúsítvány aláírására.

  ![SignMofFile](../images/SignMofFile.png)

- Próbálja ki, hogyan lehet továbbítani rá az aláírt MOF-fájlt.

  ![SignMofFile](../images/PushSignedMof.png)
