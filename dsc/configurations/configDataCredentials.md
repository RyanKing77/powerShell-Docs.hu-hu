---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Konfigurációs adatokat a hitelesítő adatok beállításai
ms.openlocfilehash: 2a326e45bbbad7bd2362b66b88bf61b98df7b02e
ms.sourcegitcommit: 6ae5b50a4b3ffcd649de1525c3ce6f15d3669082
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/18/2019
ms.locfileid: "55686375"
---
# <a name="credentials-options-in-configuration-data"></a>Konfigurációs adatokat a hitelesítő adatok beállításai

>Érvényes: Windows PowerShell 5.0

## <a name="plain-text-passwords-and-domain-users"></a>Egyszerű szöveges jelszavak és a tartományi felhasználók

A DSC-konfigurációk titkosítás nélkül hitelesítő adatokat tartalmazó hoz létre egy egyszerű szöveges jelszavak hibaüzenet.
Is DSC állít elő egy figyelmeztetés, ha a tartományi hitelesítő adatok használatával.
Ne jelenjen meg többé a hibaüzenetek és figyelmeztető üzenetek használja a DSC-konfigurációs adatok kulcsszavak:

- **PsDscAllowPlainTextPassword**
- **PsDscAllowDomainUser**

> [!NOTE]
> Egyszerű szöveges jelszavak titkosítás nélkül tárolja/továbbítása általában nem biztonságos. Ebben a témakörben ismertetett módszerek használatával biztonságossá tétele a hitelesítő adatok használata ajánlott.
> Az Azure Automation DSC szolgáltatás konfigurációk fordítása és biztonságosan tárolt hitelesítő adatok központi kezelését teszi lehetővé.
> Információkért lásd: [A DSC-konfigurációk fordítása / hitelesítőadat-eszközök](/azure/automation/automation-dsc-compile#credential-assets)

## <a name="handling-credentials-in-dsc"></a>A DSC hitelesítő adatok kezelése

A DSC-konfiguráció erőforrások futtató `Local System` alapértelmezés szerint.
Azonban bizonyos erőforrások szükséges hitelesítő adatokat, például amikor a `Package` egy adott felhasználói fiókhoz tartozó szoftver telepítéséhez szükséges erőforrás.

Korábbi erőforrást használja a kódolt `Credential` kezeléséhez, ez a tulajdonság neve.
WMF 5.0 hozzáadott automatikus `PsDscRunAsCredential` összes erőforrás tulajdonság.
További információ `PsDscRunAsCredential`, lásd: [felhasználói hitelesítő adatokkal rendelkező futtató DSC](runAsUser.md).
Egyéni erőforrásokat és újabb tulajdonsággal Ez automatikus létrehozása a hitelesítő adatokat a saját tulajdonság helyett.

> [!NOTE]
> Az egyes erőforrások terv bizonyos okból többféle hitelesítő adatot használnak, és saját hitelesítő adat tulajdonságokkal rendelkeznek.

A rendelkezésre álló hitelesítő adat található erőforrás tulajdonságainak bármelyikével `Get-DscResource -Name ResourceName -Syntax` vagy az Intellisense a ISE (`CTRL+SPACE`).

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

Ez a példa egy [csoport](../resources/resources.md) erőforrást a `PSDesiredStateConfiguration` DSC beépített erőforrás-modul.
Ez lehet helyi csoportok létrehozása és tagok hozzáadása vagy eltávolítása.
Mindkét fogadja el a `Credential` tulajdonság és az automatikus `PsDscRunAsCredential` tulajdonság.
Azonban, hogy az erőforrás használja-e csak a `Credential` tulajdonság.

További információ a `PsDscRunAsCredential` tulajdonság, lásd: [felhasználói hitelesítő adatokkal rendelkező futtató DSC](runAsUser.md).

## <a name="example-the-group-resource-credential-property"></a>Példa: A Credential tulajdonság csoporterőforrás

A DSC fut a `Local System`, így az engedélyek módosítása a helyi felhasználók és csoportok már rendelkezik.
Ha a hozzáadott tagja a helyi fiók, akkor nem hitelesítő adatok szükségesek.
Ha a `Group` erőforrás egy olyan tartományi fiók hozzáadása a helyi csoport, akkor szükség a hitelesítő adatokat.

Az Active Directory névtelen lekérdezések nem engedélyezettek.
A `Credential` tulajdonsága a `Group` erőforrás lekérdezés Active Directory tartományi fiók.
A legtöbb célra ez lehet egy általános felhasználói fiókot, mert alapértelmezés szerint a felhasználók *olvasási* nagy része a objektumok az Active Directoryban.

## <a name="example-configuration"></a>Példa konfiguráció

Az alábbi példakód egy helyi csoport számára a tartományi felhasználók feltöltéséhez DSC használja:

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

Ezt a kódot állít elő, egy hibaüzenet és a figyelmeztető üzenet:

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

Ebben a példában két problémákkal rendelkezik:

1. Hiba ismerteti, hogy a jelszavakat egyszerű szöveges formában nem támogatottak
2. Figyelmeztetés tesz elérhetővé a tartományi hitelesítő adatokkal szemben

A jelzők **PSDSCAllowPlainTextPassword** és **PSDSCAllowDomainUser** hiba és figyelmeztetés, amely tájékoztatja a felhasználót a járulékos kockázatok, elhagyása.

## <a name="psdscallowplaintextpassword"></a>PSDSCAllowPlainTextPassword

Az első hibaüzenet rendelkezik olyan dokumentáció URL-címe.
Ez a hivatkozás a jelszavak titkosítása ismerteti egy [ConfigurationData](./configData.md) struktúra és a tanúsítvány.
További információ a tanúsítványok és DSC [olvassa el a feladás egy vagy több](http://aka.ms/certs4dsc).

Az erőforrás megköveteli, hogy egy egyszerű szöveges jelszó, a `PsDscAllowPlainTextPassword` kulcsszó a konfigurációs adatokat a következő szakaszban:

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

A **PSDSCAllowPlainTextPassword** jelző megköveteli, hogy a felhasználó megerősíti a jelszavakat egyszerű szöveges formában tárolja a MOF-fájlban kockázatát. A generált MOF-fájlban annak ellenére, hogy egy **PSCredential** objektumot tartalmazó egy **SecureString** lett megadva, a jelszavak továbbra is egyszerű szövegként jelenik meg. Ez az az egyetlen alkalom érhetők el a hitelesítő adatokat. A MOF fájl által biztosított mindenki számára hozzáférést a rendszergazdai fiók hozzáférjenek.

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

### <a name="credentials-in-transit-and-at-rest"></a>Az átvitel során, és a hitelesítő adatok

- A **PSDscAllowPlainTextPassword** jelző lehetővé teszi, hogy a jelszavakat egyszerű szöveges tartalmazó MOF-fájlok összeállítása.
  Intézkedésekre tiszta szöveges jelszavak tartalmazó MOF-fájlok tárolásakor.
- Ha a a MOF-fájlt egy csomópontot a rendszer **leküldéses** módban, a Rendszerfelügyeleti webszolgáltatások titkosítja a kommunikációt a tiszta szöveges jelszavak védelmére, kivéve, ha felülírja az alapértelmezett a **AllowUnencrypted** paraméter.
  - A MOF-fájlban található, aktívan tanúsítvánnyal MOF titkosított védi, mielőtt telepítve van a csomópont.
- A **lekéréses** módban Windows lekérési kiszolgálójával, hogy HTTPS használatával titkosítja a forgalmat az Internet Information Server megadott protokoll használatával konfigurálható. További információkért lásd: a cikkek [ügyféltelepítéshez DSC lekérési](../pull-server/pullclient.md) és [biztonságossá tétele MOF-fájlok tanúsítványokkal](../pull-server/secureMOF.md).
  - Az a [Azure Automation Állapotkonfiguráció](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview) szolgáltatás, lekéréses mindig titkosítja a forgalmat.
- A csomópont MOF-fájlok titkosított aktívan PowerShell 5.0 kezdve.
  - A PowerShell 4.0 MOF fájlok titkosítatlan aktívan kivéve, ha azok titkosíthatók a tanúsítvánnyal leküldött, vagy le kell a csomópontot.

**A Microsoft tesz elérhetővé elkerülése formázatlan szöveges jelszavak miatt a jelentős biztonsági kockázatot jelent.**

## <a name="domain-credentials"></a>Tartományi hitelesítő adatok

A példa konfigurációs parancsprogram újra fut (a vagy titkosítás nélkül), továbbra is a figyelmeztetést, hogy egy tartomány használata nem ajánlott a fiókhoz tartozó hitelesítő adatokat állít elő.
Helyi fiók használatával nem tartományi hitelesítő adatok, amelyek felhasználhatók a többi kiszolgáló azok elérhetővé tegyék.

**Hitelesítő adatok használata a DSC-erőforrásokkal, inkább egy helyi fiók alatt egy olyan tartományi fiók, amikor lehetséges.**

Ha van egy "\\"vagy"\@" a a `Username` tartományi fiókként tulajdonság a hitelesítő adat, akkor a DSC fogják kezelni.
A "localhost", "127.0.0.1", kivétel és a ":: 1" a felhasználónév, a tartomány része.

## <a name="psdscallowdomainuser"></a>PSDscAllowDomainUser

A DSC a `Group` erőforrás a fenti példában egy Active Directory-tartomány lekérdezése *szükséges* egy olyan tartományi fiók.
Ebben az esetben vegye fel a `PSDscAllowDomainUser` tulajdonságot a `ConfigurationData` blokkolja az alábbiak szerint:

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

A konfigurációs parancsfájl most hibák és figyelmeztetések nélkül a MOF-fájlt hoz létre.
