---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A konfigurációs adatok hitelesítő adatok beállításai
ms.openlocfilehash: 2a326e45bbbad7bd2362b66b88bf61b98df7b02e
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62080152"
---
# <a name="credentials-options-in-configuration-data"></a>A konfigurációs adatok hitelesítő adatok beállításai

>A következőkre vonatkozik: Windows PowerShell 5.0

## <a name="plain-text-passwords-and-domain-users"></a>Egyszerű szöveges jelszavak és a tartományi felhasználók

DSC-konfigurációkat titkosítás nélküli hitelesítő adatot tartalmazó egyszerű szöveges jelszavak kapcsolatos hibaüzenet hoz létre.
DSC is generál egy figyelmeztetés, tartományi hitelesítő adatok használata esetén.
Le ezeket a hibaüzenetek és figyelmeztető üzenetek használata a DSC-konfigurációs adatok kulcsszavakat:

- **PsDscAllowPlainTextPassword**
- **PsDscAllowDomainUser**

> [!NOTE]
> Nem titkosított szöveges jelszavak tárolására és továbbítására használata általában nem biztonságos. Hitelesítő adatok védelme az ebben a témakörben ismertetett technikák használatával használata javasolt.
> Az Azure Automation DSC szolgáltatás lehetővé teszi, hogy központilag kezelheti a lefordított konfigurációk és biztonságosan tárolt hitelesítő adatokat.
> Információkért lásd: [DSC-konfigurációk fordítása / hitelesítő objektumai](/azure/automation/automation-dsc-compile#credential-assets)

## <a name="handling-credentials-in-dsc"></a>A DSC hitelesítő adatok kezelése

DSC-konfiguráció erőforrásokat futtató `Local System` alapértelmezés szerint.
Azonban bizonyos erőforrások szükséges hitelesítő adatokat, például amikor a `Package` erőforrás van szüksége egy adott felhasználói fiók alatt a szoftverek telepítését.

Korábbi erőforrást használja, a szokott `Credential` kezeléséhez, ez a tulajdonság neve.
A WMF 5.0 hozzáadva egy automatikus `PsDscRunAsCredential` tulajdonság minden erőforráshoz.
További információ `PsDscRunAsCredential`, lásd: [DSC futtatása felhasználói hitelesítő adatokkal](runAsUser.md).
Egyéni erőforrásokat és újabb tulajdonsággal a automatikus létrehozása a hitelesítő adatokat a saját tulajdonság helyett.

> [!NOTE]
> Bizonyos erőforrások kialakítása több hitelesítő adatok használata valamilyen konkrét érv amellett, és a saját hitelesítő adat tulajdonságainak rendelkeznek.

A rendelkezésre álló hitelesítő adat található erőforrás tulajdonságainak bármelyikkel `Get-DscResource -Name ResourceName -Syntax` vagy az ISE-ben az Intellisense (`CTRL+SPACE`).

```powershell
PS C:\> Get-DscResource -Name Group -Syntax
Group [String] #ResourceName
{
    GroupName = [string]
    [Credential = [PSCredential]]
    [DependsOn = [string[]]]
    [Description = [string]]
    [Ensure = [string]{ Absent | Present }]
    [Members = [string[]]]
    [MembersToExclude = [string[]]]
    [MembersToInclude = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
}
```

Ez a példa egy [csoport](../resources/resources.md) erőforrásban a `PSDesiredStateConfiguration` DSC-erőforrás beépített modul.
Azt is létre helyi csoportok és tagok hozzáadása vagy eltávolítása.
Mindkettő elfogadja a `Credential` tulajdonság és az automatikus `PsDscRunAsCredential` tulajdonság.
Azonban az erőforrás csak használja a `Credential` tulajdonság.

További információ a `PsDscRunAsCredential` tulajdonságot használja, lásd: [DSC futtatása felhasználói hitelesítő adatokkal](runAsUser.md).

## <a name="example-the-group-resource-credential-property"></a>Példa: A csoport erőforrás hitelesítő adatok a tulajdonság

DSC fut a `Local System`, így már rendelkezik a helyi felhasználók és csoportok módosításához.
Ha a tag hozzáadva egy helyi fiókot, akkor nem hitelesítő adatok nem szükséges.
Ha a `Group` erőforrás egy tartományi fiókot ad a helyi csoport, akkor szükség egy hitelesítő adatot.

Az Active Directory névtelen lekérdezések nem engedélyezettek.
A `Credential` tulajdonságát a `Group` erőforrás az Active Directory lekérdezéséhez használt tartományi fiókhoz.
A legtöbb célra ez lehet egy általános felhasználói fiókot, mert alapértelmezés szerint a felhasználók *olvasási* nagy része az objektumok az Active Directoryban.

## <a name="example-configuration"></a>Konfigurálása – példa

Az alábbi példakód egy tartományi felhasználót egy helyi csoport feltöltéséhez használja a DSC:

```powershell
Configuration DomainCredentialExample
{
    param
    (
        [PSCredential] $DomainCredential
    )
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    node localhost
    {
        Group DomainUserToLocalGroup
        {
            GroupName        = 'ApplicationAdmins'
            MembersToInclude = 'contoso\alice'
            Credential       = $DomainCredential
        }
    }
}

$cred = Get-Credential -UserName contoso\genericuser -Message "Password please"
DomainCredentialExample -DomainCredential $cred
```

Ez a kód egy hiba- és a figyelmeztető üzenetet hoz létre:

```
ConvertTo-MOFInstance : System.InvalidOperationException error processing property 'Credential' OF
TYPE 'Group': Converting and storing encrypted passwords as plain text is not recommended.
For more information on securing credentials in MOF file, please refer to MSDN blog:
https://go.microsoft.com/fwlink/?LinkId=393729

At line:11 char:9
+   Group
At line:341 char:16
+     $aliasId = ConvertTo-MOFInstance $keywordName $canonicalizedValue
+                ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Write-Error], InvalidOperationException
    + FullyQualifiedErrorId : FailToProcessProperty,ConvertTo-MOFInstance
WARNING: It is not recommended to use domain credential for node 'localhost'. In order to suppress
the warning, you can add a property named 'PSDscAllowDomainUser' with a value of $true to your DSC
configuration data for node 'localhost'.

Compilation errors occurred while processing configuration
'DomainCredentialExample'. Please review the errors reported in error stream and modify your
configuration code appropriately.
At C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateConfiguration\PSDesiredStateConfiguration.psm1:3917 char:5
+     throw $ErrorRecord
+     ~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (DomainCredentialExample:String) [], InvalidOperationException
    + FullyQualifiedErrorId : FailToProcessConfiguration
```

Ebben a példában két veti fel:

1. Hiba történt ismerteti, hogy egyszerű szöveges jelszavak használata nem ajánlott
2. Figyelmeztetés tanácsolja elleni tartományi hitelesítő adatok használatával

A jelzők **PSDSCAllowPlainTextPassword** és **PSDSCAllowDomainUser** mellőzése a hiba és figyelmeztetés, amely tájékoztatja a felhasználót az azzal járó kockázat.

## <a name="psdscallowplaintextpassword"></a>PSDSCAllowPlainTextPassword

Az első hibaüzenet-dokumentáció URL-címet tartalmaz.
Ez a hivatkozás ismerteti a jelszavak titkosítása egy [ConfigurationData](./configData.md) struktúra és a egy tanúsítványt.
További információ a tanúsítványok és a DSC [blogbejegyzésből](http://aka.ms/certs4dsc).

Egyszerű szöveges jelszó kényszerítése, a erőforrás igényel a `PsDscAllowPlainTextPassword` kulcsszót a konfigurációs adatokat a következő szakaszban:

```powershell
$password = "ThisIsAPlaintextPassword" | ConvertTo-SecureString -asPlainText -Force
$username = "contoso\Administrator"
[PSCredential] $credential = New-Object System.Management.Automation.PSCredential($username,$password)

Configuration DomainCredentialExample
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    node localhost
    {
        Group DomainUserToLocalGroup
        {
            GroupName        = 'ApplicationAdmins'
            MembersToInclude = 'contoso\alice'
            Credential       = $credential
        }
    }
}

$cd = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            PSDscAllowPlainTextPassword = $true
        }
    )
}

DomainCredentialExample -ConfigurationData $cd
```

### <a name="localhostmof"></a>localhost.mof

A **PSDSCAllowPlainTextPassword** jelző megköveteli, hogy a felhasználó elfogadja a MOF-fájlnak egyszerű szöveges jelszavak tárolására kockázatát. A létrehozott MOF-fájlnak annak ellenére, hogy egy **PSCredential** tulajdonságot tartalmazó objektumra egy **SecureString** lett megadva, a jelszavak továbbra is egyszerű szövegként jelenik meg. Ez az az egyetlen alkalom, a hitelesítő adatok érhetők el. Hozzáférjenek a MOF-fájl biztosít, bárki hozzáférhet a rendszergazdai fiókhoz.

```
/*
@TargetNode='localhost'
@GeneratedBy=Administrator
@GenerationDate=01/31/2019 06:43:13
@GenerationHost=Server01
*/

instance of MSFT_Credential as $MSFT_Credential1ref
{
Password = "ThisIsAPlaintextPassword";
 UserName = "Administrator";

};

instance of MSFT_GroupResource as $MSFT_GroupResource1ref
{
ResourceID = "[Group]DomainUserToLocalGroup";
 MembersToInclude = {
    "contoso\\alice"
};
 Credential = $MSFT_Credential1ref;
 SourceInfo = "::11::9::Group";
 GroupName = "ApplicationAdmins";
 ModuleName = "PSDesiredStateConfiguration";

ModuleVersion = "1.0";

 ConfigurationName = "DomainCredentialExample";

};
```

### <a name="credentials-in-transit-and-at-rest"></a>Hitelesítő adatok átvitel és inaktív

- A **PSDscAllowPlainTextPassword** jelző lehetővé teszi, hogy a tiszta szöveges jelszavak tartalmazó MOF-fájlok összeállítása.
  Intézkedésekre tiszta szöveges jelszavak tartalmazó MOF-fájlok tárolásakor.
- Ha a MOF-fájl kézbesíti a rendszer egy csomópontja **leküldéses** mód, a Rendszerfelügyeleti webszolgáltatások titkosítja a kommunikációt a tiszta szöveges jelszavak védelmére, kivéve, ha az alapértelmezés felülbírálása a **AllowUnencrypted** paraméter.
  - A MOF-fájlban található, aktívan titkosítása a MOF-tanúsítvánnyal védi, mielőtt egy csomópontjára telepítve van.
- A **lekéréses** mód, a Windows-lekérési kiszolgálójával, hogy a forgalom az Internet Information Server megadott protokoll használatával titkosítja a HTTPS használatával konfigurálhatja. További információkért tekintse meg a cikkeket [DSC lekérési ügyfél beállítása](../pull-server/pullclient.md) és [biztonságossá tétele MOF-fájlok tanúsítványokkal](../pull-server/secureMOF.md).
  - Az a [Azure Automation Állapotkonfiguráció](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview) szolgáltatás, lekéréses forgalmat a rendszer mindig titkosítja.
- Inaktív titkosított MOF-fájlok a csomóponton, a PowerShell 5.0-s verziójától.
  - A PowerShell 4.0-s MOF fájlokhoz nem titkosított inaktív, kivéve, ha azok van titkosítva, egy tanúsítványt, ha leküldött vagy lekérte a csomópontra.

**Egyszerű szöveges jelszavak miatt a jelentős biztonsági kockázat elkerülése érdekében a Microsoft azt ajánlja.**

## <a name="domain-credentials"></a>Tartományi hitelesítő adatok

A példa konfigurációs parancsprogram újra fut (a vagy titkosítás nélkül), továbbra is figyelmeztetést hoz létre, a használata egy tartományi fiók a hitelesítő adatait nem javasolt.
Helyi fiók használatával kiküszöböli a tartományi hitelesítő adatok, amelyek felhasználhatók a többi kiszolgáló lehetséges vannak kitéve.

**Hitelesítő adatok a DSC-erőforrások használatakor egy helyi fiók előnyben részesítése egy tartományi fiókot, amikor csak lehetséges.**

Ha van egy "\\"vagy"\@" az a `Username` tartományi fiókként tulajdonság a hitelesítő adatokat, majd a DSC-rendszer kezeli.
Nincs a kivételt a "localhost", "127.0.0.1", és a ":: 1 – az a felhasználó nevét tartomány része.

## <a name="psdscallowdomainuser"></a>PSDscAllowDomainUser

A DSC a `Group` erőforrás a fenti példában egy Active Directory-tartomány lekérdezése *igényel* egy tartományi fiókot.
Ebben az esetben adja hozzá a `PSDscAllowDomainUser` tulajdonságot a `ConfigurationData` letiltása az alábbiak szerint:

```powershell
$password = "ThisIsAPlaintextPassword" | ConvertTo-SecureString -asPlainText -Force
$username = "contoso\Administrator"
[PSCredential] $credential = New-Object System.Management.Automation.PSCredential($username,$password)

Configuration DomainCredentialExample
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    node localhost
    {
        Group DomainUserToLocalGroup
        {
            GroupName        = 'ApplicationAdmins'
            MembersToInclude = 'contoso\alice'
            Credential       = $credential
        }
    }
}

$cd = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            PSDscAllowDomainUser = $true
            PSDscAllowPlainTextPassword = $true
        }
    )
}

DomainCredentialExample -ConfigurationData $cd
```

Most már a konfigurációs parancsfájlt a MOF-fájlt, hibák és figyelmeztetések nélkül hoz létre.
