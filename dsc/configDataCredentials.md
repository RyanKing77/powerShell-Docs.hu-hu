---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A konfigurációs adatok hitelesítő adatok beállításai
ms.openlocfilehash: 890dbd01ae37ca5834070961ffd693aa811dbaa2
ms.sourcegitcommit: 56b9be8503a5a1342c0b85b36f5ba6f57c281b63
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/21/2018
ms.locfileid: "43133843"
---
# <a name="credentials-options-in-configuration-data"></a><span data-ttu-id="b9bbf-103">A konfigurációs adatok hitelesítő adatok beállításai</span><span class="sxs-lookup"><span data-stu-id="b9bbf-103">Credentials Options in Configuration Data</span></span>
><span data-ttu-id="b9bbf-104">A következőkre vonatkozik: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="b9bbf-104">Applies To: Windows PowerShell 5.0</span></span>

## <a name="plain-text-passwords-and-domain-users"></a><span data-ttu-id="b9bbf-105">Egyszerű szöveges jelszavak és a tartományi felhasználók</span><span class="sxs-lookup"><span data-stu-id="b9bbf-105">Plain Text Passwords and Domain Users</span></span>

<span data-ttu-id="b9bbf-106">DSC-konfigurációkat titkosítás nélküli hitelesítő adatot tartalmazó egyszerű szöveges jelszavak kapcsolatos hibaüzenet hoz létre.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-106">DSC configurations containing a credential without encryption will generate an error message about plain text passwords.</span></span>
<span data-ttu-id="b9bbf-107">DSC is generál egy figyelmeztetés, tartományi hitelesítő adatok használata esetén.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-107">Also, DSC will generate a warning when using domain credentials.</span></span>
<span data-ttu-id="b9bbf-108">Le ezeket a hibaüzenetek és figyelmeztető üzenetek használata a DSC-konfigurációs adatok kulcsszavakat:</span><span class="sxs-lookup"><span data-stu-id="b9bbf-108">To suppress these error and warning messages use the DSC configuration data keywords:</span></span>
* <span data-ttu-id="b9bbf-109">**PsDscAllowPlainTextPassword**</span><span class="sxs-lookup"><span data-stu-id="b9bbf-109">**PsDscAllowPlainTextPassword**</span></span>
* <span data-ttu-id="b9bbf-110">**PsDscAllowDomainUser**</span><span class="sxs-lookup"><span data-stu-id="b9bbf-110">**PsDscAllowDomainUser**</span></span>

> [!NOTE]
> <span data-ttu-id="b9bbf-111">Nem titkosított szöveges jelszavak tárolására és továbbítására használata általában nem biztonságos.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-111">Storing/transmitting plaintext passwords unencrypted is generally not secure.</span></span> <span data-ttu-id="b9bbf-112">Hitelesítő adatok védelme az ebben a témakörben ismertetett technikák használatával használata javasolt.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-112">Securing credentials by using the techniques covered later in this topic is recommended.</span></span>
> <span data-ttu-id="b9bbf-113">Az Azure Automation DSC szolgáltatás lehetővé teszi, hogy központilag kezelheti a lefordított konfigurációk és biztonságosan tárolt hitelesítő adatokat.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-113">The Azure Automation DSC service allows you to centrally manage credentials to be compiled in configurations and stored securely.</span></span>
> <span data-ttu-id="b9bbf-114">Információkért lásd: [DSC-konfigurációk fordítása / hitelesítő eszközök](/azure/automation/automation-dsc-compile#credential-assets)</span><span class="sxs-lookup"><span data-stu-id="b9bbf-114">For information, see: [Compiling DSC Configurations / Credential Assets](/azure/automation/automation-dsc-compile#credential-assets)</span></span>

<span data-ttu-id="b9bbf-115">Az alábbiakban látható egy példa egyszerű szöveges hitelesítő adatok:</span><span class="sxs-lookup"><span data-stu-id="b9bbf-115">The following is an example of passing plain text credentials:</span></span>

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
        $password = $Node.LocalPassword | ConvertTo-SecureString -asPlainText -Force
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
            Credential = $promptedCreds
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

## <a name="handling-credentials-in-dsc"></a><span data-ttu-id="b9bbf-116">A DSC hitelesítő adatok kezelése</span><span class="sxs-lookup"><span data-stu-id="b9bbf-116">Handling Credentials in DSC</span></span>

<span data-ttu-id="b9bbf-117">DSC-konfiguráció erőforrásokat futtató `Local System` alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-117">DSC configuration resources run as `Local System` by default.</span></span>
<span data-ttu-id="b9bbf-118">Azonban bizonyos erőforrások szükséges hitelesítő adatokat, például amikor a `Package` erőforrás van szüksége egy adott felhasználói fiók alatt a szoftverek telepítését.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-118">However, some resources need a credential, for example when the `Package` resource needs to install software under a specific user account.</span></span>

<span data-ttu-id="b9bbf-119">Korábbi erőforrást használja, a szokott `Credential` kezeléséhez, ez a tulajdonság neve.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-119">Earlier resources used a hard-coded `Credential` property name to handle this.</span></span>
<span data-ttu-id="b9bbf-120">A WMF 5.0 hozzáadva egy automatikus `PsDscRunAsCredential` tulajdonság minden erőforráshoz.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-120">WMF 5.0 added an automatic `PsDscRunAsCredential` property for all resources.</span></span>
<span data-ttu-id="b9bbf-121">További információ `PsDscRunAsCredential`, lásd: [DSC futtatása felhasználói hitelesítő adatokkal](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="b9bbf-121">For information about using `PsDscRunAsCredential`, see [Running DSC with user credentials](runAsUser.md).</span></span>
<span data-ttu-id="b9bbf-122">Egyéni erőforrásokat és újabb tulajdonsággal a automatikus létrehozása a hitelesítő adatokat a saját tulajdonság helyett.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-122">Newer resources and custom resources can use this automatic property instead of creating their own property for credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="b9bbf-123">Bizonyos erőforrások kialakítása több hitelesítő adatok használata valamilyen konkrét érv amellett, és a saját hitelesítő adat tulajdonságainak rendelkeznek.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-123">The design of some resources are to use multiple credentials for a specific reason, and they will have their own credential properties.</span></span>

<span data-ttu-id="b9bbf-124">A rendelkezésre álló hitelesítő adat található erőforrás tulajdonságainak bármelyikkel `Get-DscResource -Name ResourceName -Syntax` vagy az ISE-ben az Intellisense (`CTRL+SPACE`).</span><span class="sxs-lookup"><span data-stu-id="b9bbf-124">To find the available credential properties on a resource use either `Get-DscResource -Name ResourceName -Syntax` or the Intellisense in the ISE (`CTRL+SPACE`).</span></span>

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

<span data-ttu-id="b9bbf-125">Ez a példa egy [csoport](https://msdn.microsoft.com/powershell/dsc/groupresource) erőforrásban a `PSDesiredStateConfiguration` DSC-erőforrás beépített modul.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-125">This example uses a [Group](https://msdn.microsoft.com/powershell/dsc/groupresource) resource from the `PSDesiredStateConfiguration` built-in DSC resource module.</span></span>
<span data-ttu-id="b9bbf-126">Azt is létre helyi csoportok és tagok hozzáadása vagy eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-126">It can create local groups and add or remove members.</span></span>
<span data-ttu-id="b9bbf-127">Mindkettő elfogadja a `Credential` tulajdonság és az automatikus `PsDscRunAsCredential` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-127">It accepts both the `Credential` property and the automatic `PsDscRunAsCredential` property.</span></span>
<span data-ttu-id="b9bbf-128">Azonban az erőforrás csak használja a `Credential` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-128">However, the resource only uses the `Credential` property.</span></span>

<span data-ttu-id="b9bbf-129">További információ a `PsDscRunAsCredential` tulajdonságot használja, lásd: [DSC futtatása felhasználói hitelesítő adatokkal](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="b9bbf-129">For more information about the `PsDscRunAsCredential` property, see [Running DSC with user credentials](runAsUser.md).</span></span>

## <a name="example-the-group-resource-credential-property"></a><span data-ttu-id="b9bbf-130">Példa: A csoport erőforrás hitelesítő adatok a tulajdonság</span><span class="sxs-lookup"><span data-stu-id="b9bbf-130">Example: The Group resource Credential property</span></span>

<span data-ttu-id="b9bbf-131">DSC fut a `Local System`, így már rendelkezik a helyi felhasználók és csoportok módosításához.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-131">DSC runs under `Local System`, so it already has permissions to change local users and groups.</span></span>
<span data-ttu-id="b9bbf-132">Ha a tag hozzáadva egy helyi fiókot, akkor nem hitelesítő adatok nem szükséges.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-132">If the member added is a local account, then no credential is necessary.</span></span>
<span data-ttu-id="b9bbf-133">Ha a `Group` erőforrás egy tartományi fiókot ad a helyi csoport, akkor szükség egy hitelesítő adatot.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-133">If the `Group` resource adds a domain account to the local group, then a credential is necessary.</span></span>

<span data-ttu-id="b9bbf-134">Az Active Directory névtelen lekérdezések nem engedélyezettek.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-134">Anonymous queries to Active Directory are not allowed.</span></span>
<span data-ttu-id="b9bbf-135">A `Credential` tulajdonságát a `Group` erőforrás az Active Directory lekérdezéséhez használt tartományi fiókhoz.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-135">The `Credential` property of the `Group` resource is the domain account used to query Active Directory.</span></span>
<span data-ttu-id="b9bbf-136">A legtöbb célra ez lehet egy általános felhasználói fiókot, mert alapértelmezés szerint a felhasználók *olvasási* nagy része az objektumok az Active Directoryban.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-136">For most purposes this could be a generic user account, because by default users can *read* most of the objects in Active Directory.</span></span>

## <a name="example-configuration"></a><span data-ttu-id="b9bbf-137">Konfigurálása – példa</span><span class="sxs-lookup"><span data-stu-id="b9bbf-137">Example Configuration</span></span>

<span data-ttu-id="b9bbf-138">Az alábbi példakód egy tartományi felhasználót egy helyi csoport feltöltéséhez használja a DSC:</span><span class="sxs-lookup"><span data-stu-id="b9bbf-138">The following example code uses DSC to populate a local group with a domain user:</span></span>

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

<span data-ttu-id="b9bbf-139">Ez a kód egy hiba- és a figyelmeztető üzenetet hoz létre:</span><span class="sxs-lookup"><span data-stu-id="b9bbf-139">This code generates both an error and warning message:</span></span>

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

<span data-ttu-id="b9bbf-140">Ebben a példában két veti fel:</span><span class="sxs-lookup"><span data-stu-id="b9bbf-140">This example has two issues:</span></span>
1. <span data-ttu-id="b9bbf-141">Hiba történt ismerteti, hogy egyszerű szöveges jelszavak használata nem ajánlott</span><span class="sxs-lookup"><span data-stu-id="b9bbf-141">An error explains that plain text passwords are not recommended</span></span>
2. <span data-ttu-id="b9bbf-142">Figyelmeztetés tanácsolja elleni tartományi hitelesítő adatok használatával</span><span class="sxs-lookup"><span data-stu-id="b9bbf-142">A warning advises against using a domain credential</span></span>

## <a name="psdscallowplaintextpassword"></a><span data-ttu-id="b9bbf-143">PsDscAllowPlainTextPassword</span><span class="sxs-lookup"><span data-stu-id="b9bbf-143">PsDscAllowPlainTextPassword</span></span>

<span data-ttu-id="b9bbf-144">Az első hibaüzenet-dokumentáció URL-címet tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-144">The first error message has a URL with documentation.</span></span>
<span data-ttu-id="b9bbf-145">Ez a hivatkozás ismerteti a jelszavak titkosítása egy [ConfigurationData](https://msdn.microsoft.com/powershell/dsc/configdata) struktúra és a egy tanúsítványt.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-145">This link explains how to encrypt passwords using a [ConfigurationData](https://msdn.microsoft.com/powershell/dsc/configdata) structure and a certificate.</span></span>
<span data-ttu-id="b9bbf-146">További információ a tanúsítványok és a DSC [blogbejegyzésből](http://aka.ms/certs4dsc).</span><span class="sxs-lookup"><span data-stu-id="b9bbf-146">For more information on certificates and DSC [read this post](http://aka.ms/certs4dsc).</span></span>

<span data-ttu-id="b9bbf-147">Egyszerű szöveges jelszó kényszerítése, a erőforrás igényel a `PsDscAllowPlainTextPassword` kulcsszót a konfigurációs adatokat a következő szakaszban:</span><span class="sxs-lookup"><span data-stu-id="b9bbf-147">To force a plain text password, the resource requires the `PsDscAllowPlainTextPassword` keyword in the configuration data section as follows:</span></span>

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
> <span data-ttu-id="b9bbf-148">`NodeName` nem lehet egyenlő csillag, egy adott csomópont nevének megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-148">`NodeName` cannot equal asterisk, a specific node name is mandatory.</span></span>

<span data-ttu-id="b9bbf-149">**Egyszerű szöveges jelszavak miatt a jelentős biztonsági kockázat elkerülése érdekében a Microsoft azt ajánlja.**</span><span class="sxs-lookup"><span data-stu-id="b9bbf-149">**Microsoft advises to avoid plain text passwords due to the significant security risk.**</span></span>

## <a name="domain-credentials"></a><span data-ttu-id="b9bbf-150">Tartományi hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="b9bbf-150">Domain Credentials</span></span>

<span data-ttu-id="b9bbf-151">A példa konfigurációs parancsprogram újra fut (a vagy titkosítás nélkül), továbbra is figyelmeztetést hoz létre, a használata egy tartományi fiók a hitelesítő adatait nem javasolt.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-151">Running the example configuration script again (with or without encryption), still generates the warning that using a domain account for a credential is not recommended.</span></span>
<span data-ttu-id="b9bbf-152">Helyi fiók használatával kiküszöböli a tartományi hitelesítő adatok, amelyek felhasználhatók a többi kiszolgáló lehetséges vannak kitéve.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-152">Using a local account eliminates potential exposure of domain credentials that could be used on other servers.</span></span>

<span data-ttu-id="b9bbf-153">**Hitelesítő adatok a DSC-erőforrások használatakor egy helyi fiók előnyben részesítése egy tartományi fiókot, amikor csak lehetséges.**</span><span class="sxs-lookup"><span data-stu-id="b9bbf-153">**When using credentials with DSC resources, prefer a local account over a domain account when possible.**</span></span>

<span data-ttu-id="b9bbf-154">Ha egy "\' vagy" @ "az a `Username` tartományi fiókként tulajdonság a hitelesítő adatokat, majd a DSC-rendszer kezeli.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-154">If there is a '\' or '@' in the `Username` property of the credential, then DSC will treat it as a domain account.</span></span>
<span data-ttu-id="b9bbf-155">Nincs a kivételt a "localhost", "127.0.0.1", és a ":: 1 – az a felhasználó nevét tartomány része.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-155">There is an exception for "localhost", "127.0.0.1", and "::1" in the domain portion of the user name.</span></span>

## <a name="psdscallowdomainuser"></a><span data-ttu-id="b9bbf-156">PSDscAllowDomainUser</span><span class="sxs-lookup"><span data-stu-id="b9bbf-156">PSDscAllowDomainUser</span></span>

<span data-ttu-id="b9bbf-157">A DSC a `Group` erőforrás a fenti példában egy Active Directory-tartomány lekérdezése *igényel* egy tartományi fiókot.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-157">In the DSC `Group` resource example above, querying an Active Directory domain *requires* a domain account.</span></span>
<span data-ttu-id="b9bbf-158">Ebben az esetben adja hozzá a `PSDscAllowDomainUser` tulajdonságot a `ConfigurationData` letiltása az alábbiak szerint:</span><span class="sxs-lookup"><span data-stu-id="b9bbf-158">In this case add the `PSDscAllowDomainUser` property to the `ConfigurationData` block as follows:</span></span>

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

<span data-ttu-id="b9bbf-159">Most már a konfigurációs parancsfájlt a MOF-fájlt, hibák és figyelmeztetések nélkül hoz létre.</span><span class="sxs-lookup"><span data-stu-id="b9bbf-159">Now the configuration script will generate the MOF file with no errors or warnings.</span></span>
