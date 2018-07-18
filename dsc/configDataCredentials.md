---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A konfigurációs adatok hitelesítő adatok beállításai
ms.openlocfilehash: 12bb8d8ce5fc4685e583e74d411b098320ac4fd4
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093677"
---
# <a name="credentials-options-in-configuration-data"></a>A konfigurációs adatok hitelesítő adatok beállításai
>A következőkre vonatkozik: Windows PowerShell 5.0

## <a name="plain-text-passwords-and-domain-users"></a>Egyszerű szöveges jelszavak és a tartományi felhasználók

DSC-konfigurációkat titkosítás nélküli hitelesítő adatot tartalmazó egyszerű szöveges jelszavak kapcsolatos hibaüzenet hoz létre.
DSC is generál egy figyelmeztetés, tartományi hitelesítő adatok használata esetén.
Le ezeket a hibaüzenetek és figyelmeztető üzenetek használata a DSC-konfigurációs adatok kulcsszavakat:
* **PsDscAllowPlainTextPassword**
* **PsDscAllowDomainUser**

> [!NOTE]
> Nem titkosított szöveges jelszavak tárolására és továbbítására használata általában nem biztonságos. Hitelesítő adatok védelme az ebben a témakörben ismertetett technikák használatával használata javasolt.
> Az Azure Automation DSC szolgáltatás lehetővé teszi, hogy központilag kezelheti a lefordított konfigurációk és biztonságosan tárolt hitelesítő adatokat.
> Információkért lásd: [DSC-konfigurációk fordítása / hitelesítő eszközök](/azure/automation/automation-dsc-compile#credential-assets)

Az alábbiakban látható egy példa egyszerű szöveges hitelesítő adatok:

```powershell
#Prompt user for their credentials
#credentials will be unencrypted in the MOF
$promptedCreds = get-credential -Message "Please enter your credentials to generate a DSC MOF:"

# Store passwords in plaintext, in the document itself
# will also be stored in plaintext in the mof
$password = "ThisIsAPlaintextPassword" | ConvertTo-SecureString -asPlainText -Force
$username = "User1"
[PSCredential] $credential = New-Object System.Management.Automation.PSCredential($username,$password)

# DSC requires explicit confirmation before storing passwords insecurely
$ConfigurationData = @{
    AllNodes = @(
        @{
            # The "*" means "all nodes named in ConfigData" so we don't have to repeat ourselves
            NodeName="*"
            PSDscAllowPlainTextPassword = $true
        },
        #however, each node still needs to be explicitly defined for "*" to have meaning
        @{
            NodeName = "TestMachine1"
        },
        #we can also use a property to define node-specific passwords, although this is no more secure
        @{
            NodeName = "TestMachine2";
            UserName = "User2"
            LocalPassword = "ThisIsYetAnotherPlaintextPassword"
        }
        )
}
configuration unencryptedPasswordDemo
{
    Node "TestMachine1"
    {
        # We use the plaintext password to generate a new account
        User User1
        {
            UserName = $username
            Password = $credential
            Description = "local account"
            Ensure = "Present"
            Disabled = $false
            PasswordNeverExpires = $true
            PasswordChangeRequired = $false
        }
        # We use the prompted password to add this account to the local admins group
        Group addToAdmin
        {
            # Ensure the user exists before we add the user to a group
            DependsOn = "[User]User1"
            Credential = $promptedCreds
            GroupName = "Administrators"
            Ensure = "Present"
            MembersToInclude = "User1"
        }
    }

    Node "TestMachine2"
    {
        # Now we'll use a node-specific password to this machine
        $password = $Node.LocalPass | ConvertTo-SecureString -asPlainText -Force
        $username = $node.UserName
        [PSCredential] $nodeCred = New-Object System.Management.Automation.PSCredential($username,$password)

        User User2
        {
            UserName = $username
            Password = $nodeCred
            Description = "local account"
            Ensure = "Present"
            Disabled = $false
            PasswordNeverExpires = $true
            PasswordChangeRequired = $false
        }

        Group addToAdmin
        {
            Credential = $domain
            GroupName = "Administrators"
            DependsOn = "[User]User2"
            Ensure = "Present"
            MembersToInclude = "User2"
        }
    }

}
# We declared the ConfigurationData in a local variable, but we need to pass it in to our configuration function
# We need to invoke the configuration function we created to generate a MOF
unencryptedPasswordDemo -ConfigurationData $ConfigurationData
# We need to pass the MOF to the machines we named.
#-wait: doesn't use jobs so we get blocked at the prompt until the configuration is done
#-verbose: so we can see what's going on and catch any errors
#-force: for testing purposes, I run start-dscconfiguration frequently + want to make sure i'm
#        not blocked by previous configurations that are still running
Start-DscConfiguration ./unencryptedPasswordDemo -verbose -wait -force
```

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

Ez a példa egy [csoport](https://msdn.microsoft.com/powershell/dsc/groupresource) erőforrásban a `PSDesiredStateConfiguration` DSC-erőforrás beépített modul.
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
ConvertTo-MOFInstance : System.InvalidOperationException error processing
property 'Credential' OF TYPE 'Group': Converting and storing encrypted
passwords as plain text is not recommended. For more information on securing
credentials in MOF file, please refer to MSDN blog:
http://go.microsoft.com/fwlink/?LinkId=393729

At line:11 char:9
+   Group
At line:297 char:16
+     $aliasId = ConvertTo-MOFInstance $keywordName $canonicalizedValue
+                ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Write-Error], InvalidOperationException
    + FullyQualifiedErrorId : FailToProcessProperty,ConvertTo-MOFInstance

WARNING: It is not recommended to use domain credential for node 'localhost'.
In order to suppress the warning, you can add a property named
'PSDscAllowDomainUser' with a value of $true to your DSC configuration data
for node 'localhost'.
```

Ebben a példában két veti fel:
1. Hiba történt ismerteti, hogy egyszerű szöveges jelszavak használata nem ajánlott
2. Figyelmeztetés tanácsolja elleni tartományi hitelesítő adatok használatával

## <a name="psdscallowplaintextpassword"></a>PsDscAllowPlainTextPassword

Az első hibaüzenet-dokumentáció URL-címet tartalmaz.
Ez a hivatkozás ismerteti a jelszavak titkosítása egy [ConfigurationData](https://msdn.microsoft.com/powershell/dsc/configdata) struktúra és a egy tanúsítványt.
További információ a tanúsítványok és a DSC [blogbejegyzésből](http://aka.ms/certs4dsc).

Egyszerű szöveges jelszó kényszerítése, a erőforrás igényel a `PsDscAllowPlainTextPassword` kulcsszót a konfigurációs adatokat a következő szakaszban:

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

$cd = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            PSDscAllowPlainTextPassword = $true
        }
    )
}

$cred = Get-Credential -UserName contoso\genericuser -Message "Password please"
DomainCredentialExample -DomainCredential $cred -ConfigurationData $cd
```

> [!NOTE]
> `NodeName` nem lehet egyenlő csillag, egy adott csomópont nevének megadása kötelező.

**Egyszerű szöveges jelszavak miatt a jelentős biztonsági kockázat elkerülése érdekében a Microsoft azt ajánlja.**

## <a name="domain-credentials"></a>Tartományi hitelesítő adatok

A példa konfigurációs parancsprogram újra fut (a vagy titkosítás nélkül), továbbra is figyelmeztetést hoz létre, a használata egy tartományi fiók a hitelesítő adatait nem javasolt.
Helyi fiók használatával kiküszöböli a tartományi hitelesítő adatok, amelyek felhasználhatók a többi kiszolgáló lehetséges vannak kitéve.

**Hitelesítő adatok a DSC-erőforrások használatakor egy helyi fiók előnyben részesítése egy tartományi fiókot, amikor csak lehetséges.**

Ha egy "\' vagy" @ "az a `Username` tartományi fiókként tulajdonság a hitelesítő adatokat, majd a DSC-rendszer kezeli.
Nincs a kivételt a "localhost", "127.0.0.1", és a ":: 1 – az a felhasználó nevét tartomány része.

## <a name="psdscallowdomainuser"></a>PSDscAllowDomainUser

A DSC a `Group` erőforrás a fenti példában egy Active Directory-tartomány lekérdezése *igényel* egy tartományi fiókot.
Ebben az esetben adja hozzá a `PSDscAllowDomainUser` tulajdonságot a `ConfigurationData` letiltása az alábbiak szerint:

```powershell
$cd = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            PSDscAllowDomainUser = $true
            # PSDscAllowPlainTextPassword = $true
            CertificateFile = "C:\PublicKeys\server1.cer"
        }
    )
}
```

Most már a konfigurációs parancsfájlt a MOF-fájlt, hibák és figyelmeztetések nélkül hoz létre.
