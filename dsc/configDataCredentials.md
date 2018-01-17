---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Konfigurációs adatokat a hitelesítő adatok beállításai"
ms.openlocfilehash: 15cdb29127d9774c58e1d6518bbba56273e7defd
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="credentials-options-in-configuration-data"></a>Konfigurációs adatokat a hitelesítő adatok beállításai
>Vonatkozik: A Windows PowerShell 5.0

## <a name="plain-text-passwords-and-domain-users"></a>Egyszerű szöveges jelszavak és a tartományi felhasználók

A DSC-konfigurációk titkosítás nélkül hitelesítő adatokat tartalmazó hoz létre egy egyszerű szöveges jelszavak hibaüzenet.
Is DSC állít elő egy figyelmeztetés, ha a tartományi hitelesítő adatok használatával.
Ne jelenjen meg többé a hibaüzenetek és figyelmeztető üzenetek használja a DSC-konfigurációs adatok kulcsszavak:
* **PsDscAllowPlainTextPassword**
* **PsDscAllowDomainUser**

> [!NOTE]
> Egyszerű szöveges jelszavak titkosítás nélkül tárolja/továbbítása általában nem biztonságos. Ebben a témakörben ismertetett módszerek használatával biztonságossá tétele a hitelesítő adatok használata ajánlott.
> Az Azure Automation DSC szolgáltatás konfigurációk fordítása és biztonságosan tárolt hitelesítő adatok központi kezelését teszi lehetővé.
> További információ:: [DSC-konfigurációk fordítása / hitelesítő eszközök](/azure/automation/automation-dsc-compile#credential-assets)

A következő egy példa az egyszerű szöveges hitelesítő adatokat áthaladó:

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

Ez a példa egy [csoport](https://msdn.microsoft.com/en-us/powershell/dsc/groupresource) erőforrást a `PSDesiredStateConfiguration` DSC beépített erőforrás-modul.
Ez lehet helyi csoportok létrehozása és tagok hozzáadása vagy eltávolítása.
Mindkét fogadja el a `Credential` tulajdonság és az automatikus `PsDscRunAsCredential` tulajdonság.
Azonban, hogy az erőforrás használja-e csak a `Credential` tulajdonság.

További információ a `PsDscRunAsCredential` tulajdonság, lásd: [felhasználói hitelesítő adatokkal rendelkező futtató DSC](runAsUser.md).

## <a name="example-the-group-resource-credential-property"></a>Példa: A csoport erőforrás Credential tulajdonság

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

Ebben a példában két problémákkal rendelkezik:
1. Hiba ismerteti, hogy a jelszavakat egyszerű szöveges formában nem támogatottak
2. Figyelmeztetés tesz elérhetővé a tartományi hitelesítő adatokkal szemben

## <a name="psdscallowplaintextpassword"></a>PsDscAllowPlainTextPassword

Az első hibaüzenet rendelkezik olyan dokumentáció URL-címe.
Ez a hivatkozás a jelszavak titkosítása ismerteti egy [ConfigurationData](https://msdn.microsoft.com/en-us/powershell/dsc/configdata) struktúra és a tanúsítvány.
További információ a tanúsítványok és DSC [olvassa el a feladás egy vagy több](http://aka.ms/certs4dsc).

Az erőforrás megköveteli, hogy egy egyszerű szöveges jelszó, a `PsDscAllowPlainTextPassword` kulcsszó a konfigurációs adatokat a következő szakaszban:

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
> `NodeName`nem lehet egyenlő csillag, egy adott csomópont nevének megadása kötelező.

**A Microsoft tesz elérhetővé elkerülése formázatlan szöveges jelszavak miatt a jelentős biztonsági kockázatot jelent.**

Kivétel lenne az Azure Automation DSC szolgáltatással, ha csak, mivel az adatokat a rendszer mindig titkosítva tárolja (az átvitel során, a szolgáltatás aktívan, és a csomóponton aktívan).

## <a name="domain-credentials"></a>Domain Credentials

A példa konfigurációs parancsprogram újra fut (a vagy titkosítás nélkül), továbbra is a figyelmeztetést, hogy egy tartomány használata nem ajánlott a fiókhoz tartozó hitelesítő adatokat állít elő.
Helyi fiók használatával nem tartományi hitelesítő adatok, amelyek felhasználhatók a többi kiszolgáló azok elérhetővé tegyék.

**Hitelesítő adatok használata a DSC-erőforrásokkal, inkább egy helyi fiók alatt egy olyan tartományi fiók, amikor lehetséges.**

Ha van egy "\' vagy" @ "a a `Username` tartományi fiókként tulajdonság a hitelesítő adat, akkor a DSC fogják kezelni.
A "localhost", "127.0.0.1", kivétel és a ":: 1" a felhasználónév, a tartomány része.

## <a name="psdscallowdomainuser"></a>PSDscAllowDomainUser

A DSC a `Group` erőforrás a fenti példában egy Active Directory-tartomány lekérdezése *szükséges* egy olyan tartományi fiók.
Ebben az esetben vegye fel a `PSDscAllowDomainUser` tulajdonságot a `ConfigurationData` blokkolja az alábbiak szerint:

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

A konfigurációs parancsfájl most hibák és figyelmeztetések nélkül a MOF-fájlt hoz létre.
