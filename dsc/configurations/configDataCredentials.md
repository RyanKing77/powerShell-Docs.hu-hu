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
# <a name="credentials-options-in-configuration-data"></a><span data-ttu-id="4da72-103">Konfigurációs adatokat a hitelesítő adatok beállításai</span><span class="sxs-lookup"><span data-stu-id="4da72-103">Credentials Options in Configuration Data</span></span>

><span data-ttu-id="4da72-104">Érvényes: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="4da72-104">Applies To: Windows PowerShell 5.0</span></span>

## <a name="plain-text-passwords-and-domain-users"></a><span data-ttu-id="4da72-105">Egyszerű szöveges jelszavak és a tartományi felhasználók</span><span class="sxs-lookup"><span data-stu-id="4da72-105">Plain Text Passwords and Domain Users</span></span>

<span data-ttu-id="4da72-106">A DSC-konfigurációk titkosítás nélkül hitelesítő adatokat tartalmazó hoz létre egy egyszerű szöveges jelszavak hibaüzenet.</span><span class="sxs-lookup"><span data-stu-id="4da72-106">DSC configurations containing a credential without encryption will generate an error message about plain text passwords.</span></span>
<span data-ttu-id="4da72-107">Is DSC állít elő egy figyelmeztetés, ha a tartományi hitelesítő adatok használatával.</span><span class="sxs-lookup"><span data-stu-id="4da72-107">Also, DSC will generate a warning when using domain credentials.</span></span>
<span data-ttu-id="4da72-108">Ne jelenjen meg többé a hibaüzenetek és figyelmeztető üzenetek használja a DSC-konfigurációs adatok kulcsszavak:</span><span class="sxs-lookup"><span data-stu-id="4da72-108">To suppress these error and warning messages use the DSC configuration data keywords:</span></span>

- <span data-ttu-id="4da72-109">**PsDscAllowPlainTextPassword**</span><span class="sxs-lookup"><span data-stu-id="4da72-109">**PsDscAllowPlainTextPassword**</span></span>
- <span data-ttu-id="4da72-110">**PsDscAllowDomainUser**</span><span class="sxs-lookup"><span data-stu-id="4da72-110">**PsDscAllowDomainUser**</span></span>

> [!NOTE]
> <span data-ttu-id="4da72-111">Egyszerű szöveges jelszavak titkosítás nélkül tárolja/továbbítása általában nem biztonságos.</span><span class="sxs-lookup"><span data-stu-id="4da72-111">Storing/transmitting plaintext passwords unencrypted is generally not secure.</span></span> <span data-ttu-id="4da72-112">Ebben a témakörben ismertetett módszerek használatával biztonságossá tétele a hitelesítő adatok használata ajánlott.</span><span class="sxs-lookup"><span data-stu-id="4da72-112">Securing credentials by using the techniques covered later in this topic is recommended.</span></span>
> <span data-ttu-id="4da72-113">Az Azure Automation DSC szolgáltatás konfigurációk fordítása és biztonságosan tárolt hitelesítő adatok központi kezelését teszi lehetővé.</span><span class="sxs-lookup"><span data-stu-id="4da72-113">The Azure Automation DSC service allows you to centrally manage credentials to be compiled in configurations and stored securely.</span></span>
> <span data-ttu-id="4da72-114">Információkért lásd: [A DSC-konfigurációk fordítása / hitelesítőadat-eszközök](/azure/automation/automation-dsc-compile#credential-assets)</span><span class="sxs-lookup"><span data-stu-id="4da72-114">For information, see: [Compiling DSC Configurations / Credential Assets](/azure/automation/automation-dsc-compile#credential-assets)</span></span>

## <a name="handling-credentials-in-dsc"></a><span data-ttu-id="4da72-115">A DSC hitelesítő adatok kezelése</span><span class="sxs-lookup"><span data-stu-id="4da72-115">Handling Credentials in DSC</span></span>

<span data-ttu-id="4da72-116">A DSC-konfiguráció erőforrások futtató `Local System` alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="4da72-116">DSC configuration resources run as `Local System` by default.</span></span>
<span data-ttu-id="4da72-117">Azonban bizonyos erőforrások szükséges hitelesítő adatokat, például amikor a `Package` egy adott felhasználói fiókhoz tartozó szoftver telepítéséhez szükséges erőforrás.</span><span class="sxs-lookup"><span data-stu-id="4da72-117">However, some resources need a credential, for example when the `Package` resource needs to install software under a specific user account.</span></span>

<span data-ttu-id="4da72-118">Korábbi erőforrást használja a kódolt `Credential` kezeléséhez, ez a tulajdonság neve.</span><span class="sxs-lookup"><span data-stu-id="4da72-118">Earlier resources used a hard-coded `Credential` property name to handle this.</span></span>
<span data-ttu-id="4da72-119">WMF 5.0 hozzáadott automatikus `PsDscRunAsCredential` összes erőforrás tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="4da72-119">WMF 5.0 added an automatic `PsDscRunAsCredential` property for all resources.</span></span>
<span data-ttu-id="4da72-120">További információ `PsDscRunAsCredential`, lásd: [felhasználói hitelesítő adatokkal rendelkező futtató DSC](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="4da72-120">For information about using `PsDscRunAsCredential`, see [Running DSC with user credentials](runAsUser.md).</span></span>
<span data-ttu-id="4da72-121">Egyéni erőforrásokat és újabb tulajdonsággal Ez automatikus létrehozása a hitelesítő adatokat a saját tulajdonság helyett.</span><span class="sxs-lookup"><span data-stu-id="4da72-121">Newer resources and custom resources can use this automatic property instead of creating their own property for credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="4da72-122">Az egyes erőforrások terv bizonyos okból többféle hitelesítő adatot használnak, és saját hitelesítő adat tulajdonságokkal rendelkeznek.</span><span class="sxs-lookup"><span data-stu-id="4da72-122">The design of some resources are to use multiple credentials for a specific reason, and they will have their own credential properties.</span></span>

<span data-ttu-id="4da72-123">A rendelkezésre álló hitelesítő adat található erőforrás tulajdonságainak bármelyikével `Get-DscResource -Name ResourceName -Syntax` vagy az Intellisense a ISE (`CTRL+SPACE`).</span><span class="sxs-lookup"><span data-stu-id="4da72-123">To find the available credential properties on a resource use either `Get-DscResource -Name ResourceName -Syntax` or the Intellisense in the ISE (`CTRL+SPACE`).</span></span>

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

<span data-ttu-id="4da72-124">Ez a példa egy [csoport](../resources/resources.md) erőforrást a `PSDesiredStateConfiguration` DSC beépített erőforrás-modul.</span><span class="sxs-lookup"><span data-stu-id="4da72-124">This example uses a [Group](../resources/resources.md) resource from the `PSDesiredStateConfiguration` built-in DSC resource module.</span></span>
<span data-ttu-id="4da72-125">Ez lehet helyi csoportok létrehozása és tagok hozzáadása vagy eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="4da72-125">It can create local groups and add or remove members.</span></span>
<span data-ttu-id="4da72-126">Mindkét fogadja el a `Credential` tulajdonság és az automatikus `PsDscRunAsCredential` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="4da72-126">It accepts both the `Credential` property and the automatic `PsDscRunAsCredential` property.</span></span>
<span data-ttu-id="4da72-127">Azonban, hogy az erőforrás használja-e csak a `Credential` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="4da72-127">However, the resource only uses the `Credential` property.</span></span>

<span data-ttu-id="4da72-128">További információ a `PsDscRunAsCredential` tulajdonság, lásd: [felhasználói hitelesítő adatokkal rendelkező futtató DSC](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="4da72-128">For more information about the `PsDscRunAsCredential` property, see [Running DSC with user credentials](runAsUser.md).</span></span>

## <a name="example-the-group-resource-credential-property"></a><span data-ttu-id="4da72-129">Példa: A Credential tulajdonság csoporterőforrás</span><span class="sxs-lookup"><span data-stu-id="4da72-129">Example: The Group resource Credential property</span></span>

<span data-ttu-id="4da72-130">A DSC fut a `Local System`, így az engedélyek módosítása a helyi felhasználók és csoportok már rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="4da72-130">DSC runs under `Local System`, so it already has permissions to change local users and groups.</span></span>
<span data-ttu-id="4da72-131">Ha a hozzáadott tagja a helyi fiók, akkor nem hitelesítő adatok szükségesek.</span><span class="sxs-lookup"><span data-stu-id="4da72-131">If the member added is a local account, then no credential is necessary.</span></span>
<span data-ttu-id="4da72-132">Ha a `Group` erőforrás egy olyan tartományi fiók hozzáadása a helyi csoport, akkor szükség a hitelesítő adatokat.</span><span class="sxs-lookup"><span data-stu-id="4da72-132">If the `Group` resource adds a domain account to the local group, then a credential is necessary.</span></span>

<span data-ttu-id="4da72-133">Az Active Directory névtelen lekérdezések nem engedélyezettek.</span><span class="sxs-lookup"><span data-stu-id="4da72-133">Anonymous queries to Active Directory are not allowed.</span></span>
<span data-ttu-id="4da72-134">A `Credential` tulajdonsága a `Group` erőforrás lekérdezés Active Directory tartományi fiók.</span><span class="sxs-lookup"><span data-stu-id="4da72-134">The `Credential` property of the `Group` resource is the domain account used to query Active Directory.</span></span>
<span data-ttu-id="4da72-135">A legtöbb célra ez lehet egy általános felhasználói fiókot, mert alapértelmezés szerint a felhasználók *olvasási* nagy része a objektumok az Active Directoryban.</span><span class="sxs-lookup"><span data-stu-id="4da72-135">For most purposes this could be a generic user account, because by default users can *read* most of the objects in Active Directory.</span></span>

## <a name="example-configuration"></a><span data-ttu-id="4da72-136">Példa konfiguráció</span><span class="sxs-lookup"><span data-stu-id="4da72-136">Example Configuration</span></span>

<span data-ttu-id="4da72-137">Az alábbi példakód egy helyi csoport számára a tartományi felhasználók feltöltéséhez DSC használja:</span><span class="sxs-lookup"><span data-stu-id="4da72-137">The following example code uses DSC to populate a local group with a domain user:</span></span>

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

<span data-ttu-id="4da72-138">Ezt a kódot állít elő, egy hibaüzenet és a figyelmeztető üzenet:</span><span class="sxs-lookup"><span data-stu-id="4da72-138">This code generates both an error and warning message:</span></span>

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

<span data-ttu-id="4da72-139">Ebben a példában két problémákkal rendelkezik:</span><span class="sxs-lookup"><span data-stu-id="4da72-139">This example has two issues:</span></span>

1. <span data-ttu-id="4da72-140">Hiba ismerteti, hogy a jelszavakat egyszerű szöveges formában nem támogatottak</span><span class="sxs-lookup"><span data-stu-id="4da72-140">An error explains that plain text passwords are not recommended</span></span>
2. <span data-ttu-id="4da72-141">Figyelmeztetés tesz elérhetővé a tartományi hitelesítő adatokkal szemben</span><span class="sxs-lookup"><span data-stu-id="4da72-141">A warning advises against using a domain credential</span></span>

<span data-ttu-id="4da72-142">A jelzők **PSDSCAllowPlainTextPassword** és **PSDSCAllowDomainUser** hiba és figyelmeztetés, amely tájékoztatja a felhasználót a járulékos kockázatok, elhagyása.</span><span class="sxs-lookup"><span data-stu-id="4da72-142">The flags **PSDSCAllowPlainTextPassword** and **PSDSCAllowDomainUser** suppress the error and warning informing the user of the risk involved.</span></span>

## <a name="psdscallowplaintextpassword"></a><span data-ttu-id="4da72-143">PSDSCAllowPlainTextPassword</span><span class="sxs-lookup"><span data-stu-id="4da72-143">PSDSCAllowPlainTextPassword</span></span>

<span data-ttu-id="4da72-144">Az első hibaüzenet rendelkezik olyan dokumentáció URL-címe.</span><span class="sxs-lookup"><span data-stu-id="4da72-144">The first error message has a URL with documentation.</span></span>
<span data-ttu-id="4da72-145">Ez a hivatkozás a jelszavak titkosítása ismerteti egy [ConfigurationData](./configData.md) struktúra és a tanúsítvány.</span><span class="sxs-lookup"><span data-stu-id="4da72-145">This link explains how to encrypt passwords using a [ConfigurationData](./configData.md) structure and a certificate.</span></span>
<span data-ttu-id="4da72-146">További információ a tanúsítványok és DSC [olvassa el a feladás egy vagy több](http://aka.ms/certs4dsc).</span><span class="sxs-lookup"><span data-stu-id="4da72-146">For more information on certificates and DSC [read this post](http://aka.ms/certs4dsc).</span></span>

<span data-ttu-id="4da72-147">Az erőforrás megköveteli, hogy egy egyszerű szöveges jelszó, a `PsDscAllowPlainTextPassword` kulcsszó a konfigurációs adatokat a következő szakaszban:</span><span class="sxs-lookup"><span data-stu-id="4da72-147">To force a plain text password, the resource requires the `PsDscAllowPlainTextPassword` keyword in the configuration data section as follows:</span></span>

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

### <a name="localhostmof"></a><span data-ttu-id="4da72-148">localhost.mof</span><span class="sxs-lookup"><span data-stu-id="4da72-148">localhost.mof</span></span>

<span data-ttu-id="4da72-149">A **PSDSCAllowPlainTextPassword** jelző megköveteli, hogy a felhasználó megerősíti a jelszavakat egyszerű szöveges formában tárolja a MOF-fájlban kockázatát.</span><span class="sxs-lookup"><span data-stu-id="4da72-149">The **PSDSCAllowPlainTextPassword** flag requires that the user acknowledge the risk of storing plain text passwords in a MOF file.</span></span> <span data-ttu-id="4da72-150">A generált MOF-fájlban annak ellenére, hogy egy **PSCredential** objektumot tartalmazó egy **SecureString** lett megadva, a jelszavak továbbra is egyszerű szövegként jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="4da72-150">In the generated MOF file, even though a **PSCredential** object containing a **SecureString** was used, the passwords still appear as plain text.</span></span> <span data-ttu-id="4da72-151">Ez az az egyetlen alkalom érhetők el a hitelesítő adatokat.</span><span class="sxs-lookup"><span data-stu-id="4da72-151">This is the only time the credentials are exposed.</span></span> <span data-ttu-id="4da72-152">A MOF fájl által biztosított mindenki számára hozzáférést a rendszergazdai fiók hozzáférjenek.</span><span class="sxs-lookup"><span data-stu-id="4da72-152">Gaining access to this MOF file gives anyone access to the Administrator account.</span></span>

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

### <a name="credentials-in-transit-and-at-rest"></a><span data-ttu-id="4da72-153">Az átvitel során, és a hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="4da72-153">Credentials in transit and at rest</span></span>

- <span data-ttu-id="4da72-154">A **PSDscAllowPlainTextPassword** jelző lehetővé teszi, hogy a jelszavakat egyszerű szöveges tartalmazó MOF-fájlok összeállítása.</span><span class="sxs-lookup"><span data-stu-id="4da72-154">The **PSDscAllowPlainTextPassword** flag allows the compilation of MOF files that contain passwords in clear text.</span></span>
  <span data-ttu-id="4da72-155">Intézkedésekre tiszta szöveges jelszavak tartalmazó MOF-fájlok tárolásakor.</span><span class="sxs-lookup"><span data-stu-id="4da72-155">Take precautions when storing MOF files containing clear text passwords.</span></span>
- <span data-ttu-id="4da72-156">Ha a a MOF-fájlt egy csomópontot a rendszer **leküldéses** módban, a Rendszerfelügyeleti webszolgáltatások titkosítja a kommunikációt a tiszta szöveges jelszavak védelmére, kivéve, ha felülírja az alapértelmezett a **AllowUnencrypted** paraméter.</span><span class="sxs-lookup"><span data-stu-id="4da72-156">When the MOF file is delivered to a Node in **Push** mode, WinRM encrypts the communication to protect the clear text password unless you override the default with the **AllowUnencrypted** parameter.</span></span>
  - <span data-ttu-id="4da72-157">A MOF-fájlban található, aktívan tanúsítvánnyal MOF titkosított védi, mielőtt telepítve van a csomópont.</span><span class="sxs-lookup"><span data-stu-id="4da72-157">Encrypting the MOF with a certificate protects the MOF file at rest before it has been applied to a node.</span></span>
- <span data-ttu-id="4da72-158">A **lekéréses** módban Windows lekérési kiszolgálójával, hogy HTTPS használatával titkosítja a forgalmat az Internet Information Server megadott protokoll használatával konfigurálható.</span><span class="sxs-lookup"><span data-stu-id="4da72-158">In **Pull** mode, you can configure Windows pull server to use HTTPS to encrypt traffic using the protocol specified in Internet Information Server.</span></span> <span data-ttu-id="4da72-159">További információkért lásd: a cikkek [ügyféltelepítéshez DSC lekérési](../pull-server/pullclient.md) és [biztonságossá tétele MOF-fájlok tanúsítványokkal](../pull-server/secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="4da72-159">For more information, see the articles [Setting up a DSC pull client](../pull-server/pullclient.md) and [Securing MOF files with Certificates](../pull-server/secureMOF.md).</span></span>
  - <span data-ttu-id="4da72-160">Az a [Azure Automation Állapotkonfiguráció](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview) szolgáltatás, lekéréses mindig titkosítja a forgalmat.</span><span class="sxs-lookup"><span data-stu-id="4da72-160">In the [Azure Automation State Configuration](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview) service, Pull traffic is always encrypted.</span></span>
- <span data-ttu-id="4da72-161">A csomópont MOF-fájlok titkosított aktívan PowerShell 5.0 kezdve.</span><span class="sxs-lookup"><span data-stu-id="4da72-161">On the Node, MOF files are encrypted at rest Beginning in PowerShell 5.0.</span></span>
  - <span data-ttu-id="4da72-162">A PowerShell 4.0 MOF fájlok titkosítatlan aktívan kivéve, ha azok titkosíthatók a tanúsítvánnyal leküldött, vagy le kell a csomópontot.</span><span class="sxs-lookup"><span data-stu-id="4da72-162">In PowerShell 4.0 MOF files are unencrypted at rest unless they are encrypted with a certificate when they pushed or pulled to the Node.</span></span>

<span data-ttu-id="4da72-163">**A Microsoft tesz elérhetővé elkerülése formázatlan szöveges jelszavak miatt a jelentős biztonsági kockázatot jelent.**</span><span class="sxs-lookup"><span data-stu-id="4da72-163">**Microsoft advises to avoid plain text passwords due to the significant security risk.**</span></span>

## <a name="domain-credentials"></a><span data-ttu-id="4da72-164">Tartományi hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="4da72-164">Domain Credentials</span></span>

<span data-ttu-id="4da72-165">A példa konfigurációs parancsprogram újra fut (a vagy titkosítás nélkül), továbbra is a figyelmeztetést, hogy egy tartomány használata nem ajánlott a fiókhoz tartozó hitelesítő adatokat állít elő.</span><span class="sxs-lookup"><span data-stu-id="4da72-165">Running the example configuration script again (with or without encryption), still generates the warning that using a domain account for a credential is not recommended.</span></span>
<span data-ttu-id="4da72-166">Helyi fiók használatával nem tartományi hitelesítő adatok, amelyek felhasználhatók a többi kiszolgáló azok elérhetővé tegyék.</span><span class="sxs-lookup"><span data-stu-id="4da72-166">Using a local account eliminates potential exposure of domain credentials that could be used on other servers.</span></span>

<span data-ttu-id="4da72-167">**Hitelesítő adatok használata a DSC-erőforrásokkal, inkább egy helyi fiók alatt egy olyan tartományi fiók, amikor lehetséges.**</span><span class="sxs-lookup"><span data-stu-id="4da72-167">**When using credentials with DSC resources, prefer a local account over a domain account when possible.**</span></span>

<span data-ttu-id="4da72-168">Ha van egy "\\"vagy"\@" a a `Username` tartományi fiókként tulajdonság a hitelesítő adat, akkor a DSC fogják kezelni.</span><span class="sxs-lookup"><span data-stu-id="4da72-168">If there is a '\\' or '\@' in the `Username` property of the credential, then DSC will treat it as a domain account.</span></span>
<span data-ttu-id="4da72-169">A "localhost", "127.0.0.1", kivétel és a ":: 1" a felhasználónév, a tartomány része.</span><span class="sxs-lookup"><span data-stu-id="4da72-169">There is an exception for "localhost", "127.0.0.1", and "::1" in the domain portion of the user name.</span></span>

## <a name="psdscallowdomainuser"></a><span data-ttu-id="4da72-170">PSDscAllowDomainUser</span><span class="sxs-lookup"><span data-stu-id="4da72-170">PSDscAllowDomainUser</span></span>

<span data-ttu-id="4da72-171">A DSC a `Group` erőforrás a fenti példában egy Active Directory-tartomány lekérdezése *szükséges* egy olyan tartományi fiók.</span><span class="sxs-lookup"><span data-stu-id="4da72-171">In the DSC `Group` resource example above, querying an Active Directory domain *requires* a domain account.</span></span>
<span data-ttu-id="4da72-172">Ebben az esetben vegye fel a `PSDscAllowDomainUser` tulajdonságot a `ConfigurationData` blokkolja az alábbiak szerint:</span><span class="sxs-lookup"><span data-stu-id="4da72-172">In this case add the `PSDscAllowDomainUser` property to the `ConfigurationData` block as follows:</span></span>

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

<span data-ttu-id="4da72-173">A konfigurációs parancsfájl most hibák és figyelmeztetések nélkül a MOF-fájlt hoz létre.</span><span class="sxs-lookup"><span data-stu-id="4da72-173">Now the configuration script will generate the MOF file with no errors or warnings.</span></span>
