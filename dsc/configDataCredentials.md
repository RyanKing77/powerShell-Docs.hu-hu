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
# <a name="credentials-options-in-configuration-data"></a><span data-ttu-id="98b9b-103">Konfigurációs adatokat a hitelesítő adatok beállításai</span><span class="sxs-lookup"><span data-stu-id="98b9b-103">Credentials Options in Configuration Data</span></span>
><span data-ttu-id="98b9b-104">Vonatkozik: A Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="98b9b-104">Applies To: Windows PowerShell 5.0</span></span>

## <a name="plain-text-passwords-and-domain-users"></a><span data-ttu-id="98b9b-105">Egyszerű szöveges jelszavak és a tartományi felhasználók</span><span class="sxs-lookup"><span data-stu-id="98b9b-105">Plain Text Passwords and Domain Users</span></span>

<span data-ttu-id="98b9b-106">A DSC-konfigurációk titkosítás nélkül hitelesítő adatokat tartalmazó hoz létre egy egyszerű szöveges jelszavak hibaüzenet.</span><span class="sxs-lookup"><span data-stu-id="98b9b-106">DSC configurations containing a credential without encryption will generate an error message about plain text passwords.</span></span>
<span data-ttu-id="98b9b-107">Is DSC állít elő egy figyelmeztetés, ha a tartományi hitelesítő adatok használatával.</span><span class="sxs-lookup"><span data-stu-id="98b9b-107">Also, DSC will generate a warning when using domain credentials.</span></span>
<span data-ttu-id="98b9b-108">Ne jelenjen meg többé a hibaüzenetek és figyelmeztető üzenetek használja a DSC-konfigurációs adatok kulcsszavak:</span><span class="sxs-lookup"><span data-stu-id="98b9b-108">To suppress these error and warning messages use the DSC configuration data keywords:</span></span>
* <span data-ttu-id="98b9b-109">**PsDscAllowPlainTextPassword**</span><span class="sxs-lookup"><span data-stu-id="98b9b-109">**PsDscAllowPlainTextPassword**</span></span>
* <span data-ttu-id="98b9b-110">**PsDscAllowDomainUser**</span><span class="sxs-lookup"><span data-stu-id="98b9b-110">**PsDscAllowDomainUser**</span></span>

> [!NOTE]
> <span data-ttu-id="98b9b-111">Egyszerű szöveges jelszavak titkosítás nélkül tárolja/továbbítása általában nem biztonságos.</span><span class="sxs-lookup"><span data-stu-id="98b9b-111">Storing/transmitting plaintext passwords unencrypted is generally not secure.</span></span> <span data-ttu-id="98b9b-112">Ebben a témakörben ismertetett módszerek használatával biztonságossá tétele a hitelesítő adatok használata ajánlott.</span><span class="sxs-lookup"><span data-stu-id="98b9b-112">Securing credentials by using the techniques covered later in this topic is recommended.</span></span>
> <span data-ttu-id="98b9b-113">Az Azure Automation DSC szolgáltatás konfigurációk fordítása és biztonságosan tárolt hitelesítő adatok központi kezelését teszi lehetővé.</span><span class="sxs-lookup"><span data-stu-id="98b9b-113">The Azure Automation DSC service allows you to centrally manage credentials to be compiled in configurations and stored securely.</span></span>
> <span data-ttu-id="98b9b-114">További információ:: [DSC-konfigurációk fordítása / hitelesítő eszközök](/azure/automation/automation-dsc-compile#credential-assets)</span><span class="sxs-lookup"><span data-stu-id="98b9b-114">For information, see: [Compiling DSC Configurations / Credential Assets](/azure/automation/automation-dsc-compile#credential-assets)</span></span>

<span data-ttu-id="98b9b-115">A következő egy példa az egyszerű szöveges hitelesítő adatokat áthaladó:</span><span class="sxs-lookup"><span data-stu-id="98b9b-115">The following is an example of passing plain text credentials:</span></span>

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

## <a name="handling-credentials-in-dsc"></a><span data-ttu-id="98b9b-116">A DSC hitelesítő adatok kezelése</span><span class="sxs-lookup"><span data-stu-id="98b9b-116">Handling Credentials in DSC</span></span>

<span data-ttu-id="98b9b-117">A DSC-konfiguráció erőforrások futtató `Local System` alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="98b9b-117">DSC configuration resources run as `Local System` by default.</span></span>
<span data-ttu-id="98b9b-118">Azonban bizonyos erőforrások szükséges hitelesítő adatokat, például amikor a `Package` egy adott felhasználói fiókhoz tartozó szoftver telepítéséhez szükséges erőforrás.</span><span class="sxs-lookup"><span data-stu-id="98b9b-118">However, some resources need a credential, for example when the `Package` resource needs to install software under a specific user account.</span></span>

<span data-ttu-id="98b9b-119">Korábbi erőforrást használja a kódolt `Credential` kezeléséhez, ez a tulajdonság neve.</span><span class="sxs-lookup"><span data-stu-id="98b9b-119">Earlier resources used a hard-coded `Credential` property name to handle this.</span></span>
<span data-ttu-id="98b9b-120">WMF 5.0 hozzáadott automatikus `PsDscRunAsCredential` összes erőforrás tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="98b9b-120">WMF 5.0 added an automatic `PsDscRunAsCredential` property for all resources.</span></span>
<span data-ttu-id="98b9b-121">További információ `PsDscRunAsCredential`, lásd: [felhasználói hitelesítő adatokkal rendelkező futtató DSC](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="98b9b-121">For information about using `PsDscRunAsCredential`, see [Running DSC with user credentials](runAsUser.md).</span></span>
<span data-ttu-id="98b9b-122">Egyéni erőforrásokat és újabb tulajdonsággal Ez automatikus létrehozása a hitelesítő adatokat a saját tulajdonság helyett.</span><span class="sxs-lookup"><span data-stu-id="98b9b-122">Newer resources and custom resources can use this automatic property instead of creating their own property for credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="98b9b-123">Az egyes erőforrások terv bizonyos okból többféle hitelesítő adatot használnak, és saját hitelesítő adat tulajdonságokkal rendelkeznek.</span><span class="sxs-lookup"><span data-stu-id="98b9b-123">The design of some resources are to use multiple credentials for a specific reason, and they will have their own credential properties.</span></span>

<span data-ttu-id="98b9b-124">A rendelkezésre álló hitelesítő adat található erőforrás tulajdonságainak bármelyikével `Get-DscResource -Name ResourceName -Syntax` vagy az Intellisense a ISE (`CTRL+SPACE`).</span><span class="sxs-lookup"><span data-stu-id="98b9b-124">To find the available credential properties on a resource use either `Get-DscResource -Name ResourceName -Syntax` or the Intellisense in the ISE (`CTRL+SPACE`).</span></span>

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

<span data-ttu-id="98b9b-125">Ez a példa egy [csoport](https://msdn.microsoft.com/en-us/powershell/dsc/groupresource) erőforrást a `PSDesiredStateConfiguration` DSC beépített erőforrás-modul.</span><span class="sxs-lookup"><span data-stu-id="98b9b-125">This example uses a [Group](https://msdn.microsoft.com/en-us/powershell/dsc/groupresource) resource from the `PSDesiredStateConfiguration` built-in DSC resource module.</span></span>
<span data-ttu-id="98b9b-126">Ez lehet helyi csoportok létrehozása és tagok hozzáadása vagy eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="98b9b-126">It can create local groups and add or remove members.</span></span>
<span data-ttu-id="98b9b-127">Mindkét fogadja el a `Credential` tulajdonság és az automatikus `PsDscRunAsCredential` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="98b9b-127">It accepts both the `Credential` property and the automatic `PsDscRunAsCredential` property.</span></span>
<span data-ttu-id="98b9b-128">Azonban, hogy az erőforrás használja-e csak a `Credential` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="98b9b-128">However, the resource only uses the `Credential` property.</span></span>

<span data-ttu-id="98b9b-129">További információ a `PsDscRunAsCredential` tulajdonság, lásd: [felhasználói hitelesítő adatokkal rendelkező futtató DSC](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="98b9b-129">For more information about the `PsDscRunAsCredential` property, see [Running DSC with user credentials](runAsUser.md).</span></span>

## <a name="example-the-group-resource-credential-property"></a><span data-ttu-id="98b9b-130">Példa: A csoport erőforrás Credential tulajdonság</span><span class="sxs-lookup"><span data-stu-id="98b9b-130">Example: The Group resource Credential property</span></span>

<span data-ttu-id="98b9b-131">A DSC fut a `Local System`, így az engedélyek módosítása a helyi felhasználók és csoportok már rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="98b9b-131">DSC runs under `Local System`, so it already has permissions to change local users and groups.</span></span>
<span data-ttu-id="98b9b-132">Ha a hozzáadott tagja a helyi fiók, akkor nem hitelesítő adatok szükségesek.</span><span class="sxs-lookup"><span data-stu-id="98b9b-132">If the member added is a local account, then no credential is necessary.</span></span>
<span data-ttu-id="98b9b-133">Ha a `Group` erőforrás egy olyan tartományi fiók hozzáadása a helyi csoport, akkor szükség a hitelesítő adatokat.</span><span class="sxs-lookup"><span data-stu-id="98b9b-133">If the `Group` resource adds a domain account to the local group, then a credential is necessary.</span></span>

<span data-ttu-id="98b9b-134">Az Active Directory névtelen lekérdezések nem engedélyezettek.</span><span class="sxs-lookup"><span data-stu-id="98b9b-134">Anonymous queries to Active Directory are not allowed.</span></span>
<span data-ttu-id="98b9b-135">A `Credential` tulajdonsága a `Group` erőforrás lekérdezés Active Directory tartományi fiók.</span><span class="sxs-lookup"><span data-stu-id="98b9b-135">The `Credential` property of the `Group` resource is the domain account used to query Active Directory.</span></span>
<span data-ttu-id="98b9b-136">A legtöbb célra ez lehet egy általános felhasználói fiókot, mert alapértelmezés szerint a felhasználók *olvasási* nagy része a objektumok az Active Directoryban.</span><span class="sxs-lookup"><span data-stu-id="98b9b-136">For most purposes this could be a generic user account, because by default users can *read* most of the objects in Active Directory.</span></span>

## <a name="example-configuration"></a><span data-ttu-id="98b9b-137">Példa konfiguráció</span><span class="sxs-lookup"><span data-stu-id="98b9b-137">Example Configuration</span></span>

<span data-ttu-id="98b9b-138">Az alábbi példakód egy helyi csoport számára a tartományi felhasználók feltöltéséhez DSC használja:</span><span class="sxs-lookup"><span data-stu-id="98b9b-138">The following example code uses DSC to populate a local group with a domain user:</span></span>

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

<span data-ttu-id="98b9b-139">Ezt a kódot állít elő, egy hibaüzenet és a figyelmeztető üzenet:</span><span class="sxs-lookup"><span data-stu-id="98b9b-139">This code generates both an error and warning message:</span></span>

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

<span data-ttu-id="98b9b-140">Ebben a példában két problémákkal rendelkezik:</span><span class="sxs-lookup"><span data-stu-id="98b9b-140">This example has two issues:</span></span>
1. <span data-ttu-id="98b9b-141">Hiba ismerteti, hogy a jelszavakat egyszerű szöveges formában nem támogatottak</span><span class="sxs-lookup"><span data-stu-id="98b9b-141">An error explains that plain text passwords are not recommended</span></span>
2. <span data-ttu-id="98b9b-142">Figyelmeztetés tesz elérhetővé a tartományi hitelesítő adatokkal szemben</span><span class="sxs-lookup"><span data-stu-id="98b9b-142">A warning advises against using a domain credential</span></span>

## <a name="psdscallowplaintextpassword"></a><span data-ttu-id="98b9b-143">PsDscAllowPlainTextPassword</span><span class="sxs-lookup"><span data-stu-id="98b9b-143">PsDscAllowPlainTextPassword</span></span>

<span data-ttu-id="98b9b-144">Az első hibaüzenet rendelkezik olyan dokumentáció URL-címe.</span><span class="sxs-lookup"><span data-stu-id="98b9b-144">The first error message has a URL with documentation.</span></span>
<span data-ttu-id="98b9b-145">Ez a hivatkozás a jelszavak titkosítása ismerteti egy [ConfigurationData](https://msdn.microsoft.com/en-us/powershell/dsc/configdata) struktúra és a tanúsítvány.</span><span class="sxs-lookup"><span data-stu-id="98b9b-145">This link explains how to encrypt passwords using a [ConfigurationData](https://msdn.microsoft.com/en-us/powershell/dsc/configdata) structure and a certificate.</span></span>
<span data-ttu-id="98b9b-146">További információ a tanúsítványok és DSC [olvassa el a feladás egy vagy több](http://aka.ms/certs4dsc).</span><span class="sxs-lookup"><span data-stu-id="98b9b-146">For more information on certificates and DSC [read this post](http://aka.ms/certs4dsc).</span></span>

<span data-ttu-id="98b9b-147">Az erőforrás megköveteli, hogy egy egyszerű szöveges jelszó, a `PsDscAllowPlainTextPassword` kulcsszó a konfigurációs adatokat a következő szakaszban:</span><span class="sxs-lookup"><span data-stu-id="98b9b-147">To force a plain text password, the resource requires the `PsDscAllowPlainTextPassword` keyword in the configuration data section as follows:</span></span>

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
> <span data-ttu-id="98b9b-148">`NodeName`nem lehet egyenlő csillag, egy adott csomópont nevének megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="98b9b-148">`NodeName` cannot equal asterisk, a specific node name is mandatory.</span></span>

<span data-ttu-id="98b9b-149">**A Microsoft tesz elérhetővé elkerülése formázatlan szöveges jelszavak miatt a jelentős biztonsági kockázatot jelent.**</span><span class="sxs-lookup"><span data-stu-id="98b9b-149">**Microsoft advises to avoid plain text passwords due to the significant security risk.**</span></span>

<span data-ttu-id="98b9b-150">Kivétel lenne az Azure Automation DSC szolgáltatással, ha csak, mivel az adatokat a rendszer mindig titkosítva tárolja (az átvitel során, a szolgáltatás aktívan, és a csomóponton aktívan).</span><span class="sxs-lookup"><span data-stu-id="98b9b-150">An exception would be when using the Azure Automation DSC service, only because the data is always stored encrypted (in transit, at rest in the service, and at rest on the node).</span></span>

## <a name="domain-credentials"></a><span data-ttu-id="98b9b-151">Domain Credentials</span><span class="sxs-lookup"><span data-stu-id="98b9b-151">Domain Credentials</span></span>

<span data-ttu-id="98b9b-152">A példa konfigurációs parancsprogram újra fut (a vagy titkosítás nélkül), továbbra is a figyelmeztetést, hogy egy tartomány használata nem ajánlott a fiókhoz tartozó hitelesítő adatokat állít elő.</span><span class="sxs-lookup"><span data-stu-id="98b9b-152">Running the example configuration script again (with or without encryption), still generates the warning that using a domain account for a credential is not recommended.</span></span>
<span data-ttu-id="98b9b-153">Helyi fiók használatával nem tartományi hitelesítő adatok, amelyek felhasználhatók a többi kiszolgáló azok elérhetővé tegyék.</span><span class="sxs-lookup"><span data-stu-id="98b9b-153">Using a local account eliminates potential exposure of domain credentials that could be used on other servers.</span></span>

<span data-ttu-id="98b9b-154">**Hitelesítő adatok használata a DSC-erőforrásokkal, inkább egy helyi fiók alatt egy olyan tartományi fiók, amikor lehetséges.**</span><span class="sxs-lookup"><span data-stu-id="98b9b-154">**When using credentials with DSC resources, prefer a local account over a domain account when possible.**</span></span>

<span data-ttu-id="98b9b-155">Ha van egy "\' vagy" @ "a a `Username` tartományi fiókként tulajdonság a hitelesítő adat, akkor a DSC fogják kezelni.</span><span class="sxs-lookup"><span data-stu-id="98b9b-155">If there is a '\' or '@' in the `Username` property of the credential, then DSC will treat it as a domain account.</span></span>
<span data-ttu-id="98b9b-156">A "localhost", "127.0.0.1", kivétel és a ":: 1" a felhasználónév, a tartomány része.</span><span class="sxs-lookup"><span data-stu-id="98b9b-156">There is an exception for "localhost", "127.0.0.1", and "::1" in the domain portion of the user name.</span></span>

## <a name="psdscallowdomainuser"></a><span data-ttu-id="98b9b-157">PSDscAllowDomainUser</span><span class="sxs-lookup"><span data-stu-id="98b9b-157">PSDscAllowDomainUser</span></span>

<span data-ttu-id="98b9b-158">A DSC a `Group` erőforrás a fenti példában egy Active Directory-tartomány lekérdezése *szükséges* egy olyan tartományi fiók.</span><span class="sxs-lookup"><span data-stu-id="98b9b-158">In the DSC `Group` resource example above, querying an Active Directory domain *requires* a domain account.</span></span>
<span data-ttu-id="98b9b-159">Ebben az esetben vegye fel a `PSDscAllowDomainUser` tulajdonságot a `ConfigurationData` blokkolja az alábbiak szerint:</span><span class="sxs-lookup"><span data-stu-id="98b9b-159">In this case add the `PSDscAllowDomainUser` property to the `ConfigurationData` block as follows:</span></span>

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

<span data-ttu-id="98b9b-160">A konfigurációs parancsfájl most hibák és figyelmeztetések nélkül a MOF-fájlt hoz létre.</span><span class="sxs-lookup"><span data-stu-id="98b9b-160">Now the configuration script will generate the MOF file with no errors or warnings.</span></span>
