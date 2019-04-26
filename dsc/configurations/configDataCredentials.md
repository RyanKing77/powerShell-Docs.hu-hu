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
# <a name="credentials-options-in-configuration-data"></a><span data-ttu-id="7dccd-103">A konfigurációs adatok hitelesítő adatok beállításai</span><span class="sxs-lookup"><span data-stu-id="7dccd-103">Credentials Options in Configuration Data</span></span>

><span data-ttu-id="7dccd-104">A következőkre vonatkozik: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="7dccd-104">Applies To: Windows PowerShell 5.0</span></span>

## <a name="plain-text-passwords-and-domain-users"></a><span data-ttu-id="7dccd-105">Egyszerű szöveges jelszavak és a tartományi felhasználók</span><span class="sxs-lookup"><span data-stu-id="7dccd-105">Plain Text Passwords and Domain Users</span></span>

<span data-ttu-id="7dccd-106">DSC-konfigurációkat titkosítás nélküli hitelesítő adatot tartalmazó egyszerű szöveges jelszavak kapcsolatos hibaüzenet hoz létre.</span><span class="sxs-lookup"><span data-stu-id="7dccd-106">DSC configurations containing a credential without encryption will generate an error message about plain text passwords.</span></span>
<span data-ttu-id="7dccd-107">DSC is generál egy figyelmeztetés, tartományi hitelesítő adatok használata esetén.</span><span class="sxs-lookup"><span data-stu-id="7dccd-107">Also, DSC will generate a warning when using domain credentials.</span></span>
<span data-ttu-id="7dccd-108">Le ezeket a hibaüzenetek és figyelmeztető üzenetek használata a DSC-konfigurációs adatok kulcsszavakat:</span><span class="sxs-lookup"><span data-stu-id="7dccd-108">To suppress these error and warning messages use the DSC configuration data keywords:</span></span>

- <span data-ttu-id="7dccd-109">**PsDscAllowPlainTextPassword**</span><span class="sxs-lookup"><span data-stu-id="7dccd-109">**PsDscAllowPlainTextPassword**</span></span>
- <span data-ttu-id="7dccd-110">**PsDscAllowDomainUser**</span><span class="sxs-lookup"><span data-stu-id="7dccd-110">**PsDscAllowDomainUser**</span></span>

> [!NOTE]
> <span data-ttu-id="7dccd-111">Nem titkosított szöveges jelszavak tárolására és továbbítására használata általában nem biztonságos.</span><span class="sxs-lookup"><span data-stu-id="7dccd-111">Storing/transmitting plaintext passwords unencrypted is generally not secure.</span></span> <span data-ttu-id="7dccd-112">Hitelesítő adatok védelme az ebben a témakörben ismertetett technikák használatával használata javasolt.</span><span class="sxs-lookup"><span data-stu-id="7dccd-112">Securing credentials by using the techniques covered later in this topic is recommended.</span></span>
> <span data-ttu-id="7dccd-113">Az Azure Automation DSC szolgáltatás lehetővé teszi, hogy központilag kezelheti a lefordított konfigurációk és biztonságosan tárolt hitelesítő adatokat.</span><span class="sxs-lookup"><span data-stu-id="7dccd-113">The Azure Automation DSC service allows you to centrally manage credentials to be compiled in configurations and stored securely.</span></span>
> <span data-ttu-id="7dccd-114">Információkért lásd: [DSC-konfigurációk fordítása / hitelesítő objektumai](/azure/automation/automation-dsc-compile#credential-assets)</span><span class="sxs-lookup"><span data-stu-id="7dccd-114">For information, see: [Compiling DSC Configurations / Credential Assets](/azure/automation/automation-dsc-compile#credential-assets)</span></span>

## <a name="handling-credentials-in-dsc"></a><span data-ttu-id="7dccd-115">A DSC hitelesítő adatok kezelése</span><span class="sxs-lookup"><span data-stu-id="7dccd-115">Handling Credentials in DSC</span></span>

<span data-ttu-id="7dccd-116">DSC-konfiguráció erőforrásokat futtató `Local System` alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="7dccd-116">DSC configuration resources run as `Local System` by default.</span></span>
<span data-ttu-id="7dccd-117">Azonban bizonyos erőforrások szükséges hitelesítő adatokat, például amikor a `Package` erőforrás van szüksége egy adott felhasználói fiók alatt a szoftverek telepítését.</span><span class="sxs-lookup"><span data-stu-id="7dccd-117">However, some resources need a credential, for example when the `Package` resource needs to install software under a specific user account.</span></span>

<span data-ttu-id="7dccd-118">Korábbi erőforrást használja, a szokott `Credential` kezeléséhez, ez a tulajdonság neve.</span><span class="sxs-lookup"><span data-stu-id="7dccd-118">Earlier resources used a hard-coded `Credential` property name to handle this.</span></span>
<span data-ttu-id="7dccd-119">A WMF 5.0 hozzáadva egy automatikus `PsDscRunAsCredential` tulajdonság minden erőforráshoz.</span><span class="sxs-lookup"><span data-stu-id="7dccd-119">WMF 5.0 added an automatic `PsDscRunAsCredential` property for all resources.</span></span>
<span data-ttu-id="7dccd-120">További információ `PsDscRunAsCredential`, lásd: [DSC futtatása felhasználói hitelesítő adatokkal](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="7dccd-120">For information about using `PsDscRunAsCredential`, see [Running DSC with user credentials](runAsUser.md).</span></span>
<span data-ttu-id="7dccd-121">Egyéni erőforrásokat és újabb tulajdonsággal a automatikus létrehozása a hitelesítő adatokat a saját tulajdonság helyett.</span><span class="sxs-lookup"><span data-stu-id="7dccd-121">Newer resources and custom resources can use this automatic property instead of creating their own property for credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="7dccd-122">Bizonyos erőforrások kialakítása több hitelesítő adatok használata valamilyen konkrét érv amellett, és a saját hitelesítő adat tulajdonságainak rendelkeznek.</span><span class="sxs-lookup"><span data-stu-id="7dccd-122">The design of some resources are to use multiple credentials for a specific reason, and they will have their own credential properties.</span></span>

<span data-ttu-id="7dccd-123">A rendelkezésre álló hitelesítő adat található erőforrás tulajdonságainak bármelyikkel `Get-DscResource -Name ResourceName -Syntax` vagy az ISE-ben az Intellisense (`CTRL+SPACE`).</span><span class="sxs-lookup"><span data-stu-id="7dccd-123">To find the available credential properties on a resource use either `Get-DscResource -Name ResourceName -Syntax` or the Intellisense in the ISE (`CTRL+SPACE`).</span></span>

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

<span data-ttu-id="7dccd-124">Ez a példa egy [csoport](../resources/resources.md) erőforrásban a `PSDesiredStateConfiguration` DSC-erőforrás beépített modul.</span><span class="sxs-lookup"><span data-stu-id="7dccd-124">This example uses a [Group](../resources/resources.md) resource from the `PSDesiredStateConfiguration` built-in DSC resource module.</span></span>
<span data-ttu-id="7dccd-125">Azt is létre helyi csoportok és tagok hozzáadása vagy eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="7dccd-125">It can create local groups and add or remove members.</span></span>
<span data-ttu-id="7dccd-126">Mindkettő elfogadja a `Credential` tulajdonság és az automatikus `PsDscRunAsCredential` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="7dccd-126">It accepts both the `Credential` property and the automatic `PsDscRunAsCredential` property.</span></span>
<span data-ttu-id="7dccd-127">Azonban az erőforrás csak használja a `Credential` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="7dccd-127">However, the resource only uses the `Credential` property.</span></span>

<span data-ttu-id="7dccd-128">További információ a `PsDscRunAsCredential` tulajdonságot használja, lásd: [DSC futtatása felhasználói hitelesítő adatokkal](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="7dccd-128">For more information about the `PsDscRunAsCredential` property, see [Running DSC with user credentials](runAsUser.md).</span></span>

## <a name="example-the-group-resource-credential-property"></a><span data-ttu-id="7dccd-129">Példa: A csoport erőforrás hitelesítő adatok a tulajdonság</span><span class="sxs-lookup"><span data-stu-id="7dccd-129">Example: The Group resource Credential property</span></span>

<span data-ttu-id="7dccd-130">DSC fut a `Local System`, így már rendelkezik a helyi felhasználók és csoportok módosításához.</span><span class="sxs-lookup"><span data-stu-id="7dccd-130">DSC runs under `Local System`, so it already has permissions to change local users and groups.</span></span>
<span data-ttu-id="7dccd-131">Ha a tag hozzáadva egy helyi fiókot, akkor nem hitelesítő adatok nem szükséges.</span><span class="sxs-lookup"><span data-stu-id="7dccd-131">If the member added is a local account, then no credential is necessary.</span></span>
<span data-ttu-id="7dccd-132">Ha a `Group` erőforrás egy tartományi fiókot ad a helyi csoport, akkor szükség egy hitelesítő adatot.</span><span class="sxs-lookup"><span data-stu-id="7dccd-132">If the `Group` resource adds a domain account to the local group, then a credential is necessary.</span></span>

<span data-ttu-id="7dccd-133">Az Active Directory névtelen lekérdezések nem engedélyezettek.</span><span class="sxs-lookup"><span data-stu-id="7dccd-133">Anonymous queries to Active Directory are not allowed.</span></span>
<span data-ttu-id="7dccd-134">A `Credential` tulajdonságát a `Group` erőforrás az Active Directory lekérdezéséhez használt tartományi fiókhoz.</span><span class="sxs-lookup"><span data-stu-id="7dccd-134">The `Credential` property of the `Group` resource is the domain account used to query Active Directory.</span></span>
<span data-ttu-id="7dccd-135">A legtöbb célra ez lehet egy általános felhasználói fiókot, mert alapértelmezés szerint a felhasználók *olvasási* nagy része az objektumok az Active Directoryban.</span><span class="sxs-lookup"><span data-stu-id="7dccd-135">For most purposes this could be a generic user account, because by default users can *read* most of the objects in Active Directory.</span></span>

## <a name="example-configuration"></a><span data-ttu-id="7dccd-136">Konfigurálása – példa</span><span class="sxs-lookup"><span data-stu-id="7dccd-136">Example Configuration</span></span>

<span data-ttu-id="7dccd-137">Az alábbi példakód egy tartományi felhasználót egy helyi csoport feltöltéséhez használja a DSC:</span><span class="sxs-lookup"><span data-stu-id="7dccd-137">The following example code uses DSC to populate a local group with a domain user:</span></span>

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

<span data-ttu-id="7dccd-138">Ez a kód egy hiba- és a figyelmeztető üzenetet hoz létre:</span><span class="sxs-lookup"><span data-stu-id="7dccd-138">This code generates both an error and warning message:</span></span>

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

<span data-ttu-id="7dccd-139">Ebben a példában két veti fel:</span><span class="sxs-lookup"><span data-stu-id="7dccd-139">This example has two issues:</span></span>

1. <span data-ttu-id="7dccd-140">Hiba történt ismerteti, hogy egyszerű szöveges jelszavak használata nem ajánlott</span><span class="sxs-lookup"><span data-stu-id="7dccd-140">An error explains that plain text passwords are not recommended</span></span>
2. <span data-ttu-id="7dccd-141">Figyelmeztetés tanácsolja elleni tartományi hitelesítő adatok használatával</span><span class="sxs-lookup"><span data-stu-id="7dccd-141">A warning advises against using a domain credential</span></span>

<span data-ttu-id="7dccd-142">A jelzők **PSDSCAllowPlainTextPassword** és **PSDSCAllowDomainUser** mellőzése a hiba és figyelmeztetés, amely tájékoztatja a felhasználót az azzal járó kockázat.</span><span class="sxs-lookup"><span data-stu-id="7dccd-142">The flags **PSDSCAllowPlainTextPassword** and **PSDSCAllowDomainUser** suppress the error and warning informing the user of the risk involved.</span></span>

## <a name="psdscallowplaintextpassword"></a><span data-ttu-id="7dccd-143">PSDSCAllowPlainTextPassword</span><span class="sxs-lookup"><span data-stu-id="7dccd-143">PSDSCAllowPlainTextPassword</span></span>

<span data-ttu-id="7dccd-144">Az első hibaüzenet-dokumentáció URL-címet tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="7dccd-144">The first error message has a URL with documentation.</span></span>
<span data-ttu-id="7dccd-145">Ez a hivatkozás ismerteti a jelszavak titkosítása egy [ConfigurationData](./configData.md) struktúra és a egy tanúsítványt.</span><span class="sxs-lookup"><span data-stu-id="7dccd-145">This link explains how to encrypt passwords using a [ConfigurationData](./configData.md) structure and a certificate.</span></span>
<span data-ttu-id="7dccd-146">További információ a tanúsítványok és a DSC [blogbejegyzésből](http://aka.ms/certs4dsc).</span><span class="sxs-lookup"><span data-stu-id="7dccd-146">For more information on certificates and DSC [read this post](http://aka.ms/certs4dsc).</span></span>

<span data-ttu-id="7dccd-147">Egyszerű szöveges jelszó kényszerítése, a erőforrás igényel a `PsDscAllowPlainTextPassword` kulcsszót a konfigurációs adatokat a következő szakaszban:</span><span class="sxs-lookup"><span data-stu-id="7dccd-147">To force a plain text password, the resource requires the `PsDscAllowPlainTextPassword` keyword in the configuration data section as follows:</span></span>

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

### <a name="localhostmof"></a><span data-ttu-id="7dccd-148">localhost.mof</span><span class="sxs-lookup"><span data-stu-id="7dccd-148">localhost.mof</span></span>

<span data-ttu-id="7dccd-149">A **PSDSCAllowPlainTextPassword** jelző megköveteli, hogy a felhasználó elfogadja a MOF-fájlnak egyszerű szöveges jelszavak tárolására kockázatát.</span><span class="sxs-lookup"><span data-stu-id="7dccd-149">The **PSDSCAllowPlainTextPassword** flag requires that the user acknowledge the risk of storing plain text passwords in a MOF file.</span></span> <span data-ttu-id="7dccd-150">A létrehozott MOF-fájlnak annak ellenére, hogy egy **PSCredential** tulajdonságot tartalmazó objektumra egy **SecureString** lett megadva, a jelszavak továbbra is egyszerű szövegként jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="7dccd-150">In the generated MOF file, even though a **PSCredential** object containing a **SecureString** was used, the passwords still appear as plain text.</span></span> <span data-ttu-id="7dccd-151">Ez az az egyetlen alkalom, a hitelesítő adatok érhetők el.</span><span class="sxs-lookup"><span data-stu-id="7dccd-151">This is the only time the credentials are exposed.</span></span> <span data-ttu-id="7dccd-152">Hozzáférjenek a MOF-fájl biztosít, bárki hozzáférhet a rendszergazdai fiókhoz.</span><span class="sxs-lookup"><span data-stu-id="7dccd-152">Gaining access to this MOF file gives anyone access to the Administrator account.</span></span>

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

### <a name="credentials-in-transit-and-at-rest"></a><span data-ttu-id="7dccd-153">Hitelesítő adatok átvitel és inaktív</span><span class="sxs-lookup"><span data-stu-id="7dccd-153">Credentials in transit and at rest</span></span>

- <span data-ttu-id="7dccd-154">A **PSDscAllowPlainTextPassword** jelző lehetővé teszi, hogy a tiszta szöveges jelszavak tartalmazó MOF-fájlok összeállítása.</span><span class="sxs-lookup"><span data-stu-id="7dccd-154">The **PSDscAllowPlainTextPassword** flag allows the compilation of MOF files that contain passwords in clear text.</span></span>
  <span data-ttu-id="7dccd-155">Intézkedésekre tiszta szöveges jelszavak tartalmazó MOF-fájlok tárolásakor.</span><span class="sxs-lookup"><span data-stu-id="7dccd-155">Take precautions when storing MOF files containing clear text passwords.</span></span>
- <span data-ttu-id="7dccd-156">Ha a MOF-fájl kézbesíti a rendszer egy csomópontja **leküldéses** mód, a Rendszerfelügyeleti webszolgáltatások titkosítja a kommunikációt a tiszta szöveges jelszavak védelmére, kivéve, ha az alapértelmezés felülbírálása a **AllowUnencrypted** paraméter.</span><span class="sxs-lookup"><span data-stu-id="7dccd-156">When the MOF file is delivered to a Node in **Push** mode, WinRM encrypts the communication to protect the clear text password unless you override the default with the **AllowUnencrypted** parameter.</span></span>
  - <span data-ttu-id="7dccd-157">A MOF-fájlban található, aktívan titkosítása a MOF-tanúsítvánnyal védi, mielőtt egy csomópontjára telepítve van.</span><span class="sxs-lookup"><span data-stu-id="7dccd-157">Encrypting the MOF with a certificate protects the MOF file at rest before it has been applied to a node.</span></span>
- <span data-ttu-id="7dccd-158">A **lekéréses** mód, a Windows-lekérési kiszolgálójával, hogy a forgalom az Internet Information Server megadott protokoll használatával titkosítja a HTTPS használatával konfigurálhatja.</span><span class="sxs-lookup"><span data-stu-id="7dccd-158">In **Pull** mode, you can configure Windows pull server to use HTTPS to encrypt traffic using the protocol specified in Internet Information Server.</span></span> <span data-ttu-id="7dccd-159">További információkért tekintse meg a cikkeket [DSC lekérési ügyfél beállítása](../pull-server/pullclient.md) és [biztonságossá tétele MOF-fájlok tanúsítványokkal](../pull-server/secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="7dccd-159">For more information, see the articles [Setting up a DSC pull client](../pull-server/pullclient.md) and [Securing MOF files with Certificates](../pull-server/secureMOF.md).</span></span>
  - <span data-ttu-id="7dccd-160">Az a [Azure Automation Állapotkonfiguráció](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview) szolgáltatás, lekéréses forgalmat a rendszer mindig titkosítja.</span><span class="sxs-lookup"><span data-stu-id="7dccd-160">In the [Azure Automation State Configuration](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview) service, Pull traffic is always encrypted.</span></span>
- <span data-ttu-id="7dccd-161">Inaktív titkosított MOF-fájlok a csomóponton, a PowerShell 5.0-s verziójától.</span><span class="sxs-lookup"><span data-stu-id="7dccd-161">On the Node, MOF files are encrypted at rest Beginning in PowerShell 5.0.</span></span>
  - <span data-ttu-id="7dccd-162">A PowerShell 4.0-s MOF fájlokhoz nem titkosított inaktív, kivéve, ha azok van titkosítva, egy tanúsítványt, ha leküldött vagy lekérte a csomópontra.</span><span class="sxs-lookup"><span data-stu-id="7dccd-162">In PowerShell 4.0 MOF files are unencrypted at rest unless they are encrypted with a certificate when they pushed or pulled to the Node.</span></span>

<span data-ttu-id="7dccd-163">**Egyszerű szöveges jelszavak miatt a jelentős biztonsági kockázat elkerülése érdekében a Microsoft azt ajánlja.**</span><span class="sxs-lookup"><span data-stu-id="7dccd-163">**Microsoft advises to avoid plain text passwords due to the significant security risk.**</span></span>

## <a name="domain-credentials"></a><span data-ttu-id="7dccd-164">Tartományi hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="7dccd-164">Domain Credentials</span></span>

<span data-ttu-id="7dccd-165">A példa konfigurációs parancsprogram újra fut (a vagy titkosítás nélkül), továbbra is figyelmeztetést hoz létre, a használata egy tartományi fiók a hitelesítő adatait nem javasolt.</span><span class="sxs-lookup"><span data-stu-id="7dccd-165">Running the example configuration script again (with or without encryption), still generates the warning that using a domain account for a credential is not recommended.</span></span>
<span data-ttu-id="7dccd-166">Helyi fiók használatával kiküszöböli a tartományi hitelesítő adatok, amelyek felhasználhatók a többi kiszolgáló lehetséges vannak kitéve.</span><span class="sxs-lookup"><span data-stu-id="7dccd-166">Using a local account eliminates potential exposure of domain credentials that could be used on other servers.</span></span>

<span data-ttu-id="7dccd-167">**Hitelesítő adatok a DSC-erőforrások használatakor egy helyi fiók előnyben részesítése egy tartományi fiókot, amikor csak lehetséges.**</span><span class="sxs-lookup"><span data-stu-id="7dccd-167">**When using credentials with DSC resources, prefer a local account over a domain account when possible.**</span></span>

<span data-ttu-id="7dccd-168">Ha van egy "\\"vagy"\@" az a `Username` tartományi fiókként tulajdonság a hitelesítő adatokat, majd a DSC-rendszer kezeli.</span><span class="sxs-lookup"><span data-stu-id="7dccd-168">If there is a '\\' or '\@' in the `Username` property of the credential, then DSC will treat it as a domain account.</span></span>
<span data-ttu-id="7dccd-169">Nincs a kivételt a "localhost", "127.0.0.1", és a ":: 1 – az a felhasználó nevét tartomány része.</span><span class="sxs-lookup"><span data-stu-id="7dccd-169">There is an exception for "localhost", "127.0.0.1", and "::1" in the domain portion of the user name.</span></span>

## <a name="psdscallowdomainuser"></a><span data-ttu-id="7dccd-170">PSDscAllowDomainUser</span><span class="sxs-lookup"><span data-stu-id="7dccd-170">PSDscAllowDomainUser</span></span>

<span data-ttu-id="7dccd-171">A DSC a `Group` erőforrás a fenti példában egy Active Directory-tartomány lekérdezése *igényel* egy tartományi fiókot.</span><span class="sxs-lookup"><span data-stu-id="7dccd-171">In the DSC `Group` resource example above, querying an Active Directory domain *requires* a domain account.</span></span>
<span data-ttu-id="7dccd-172">Ebben az esetben adja hozzá a `PSDscAllowDomainUser` tulajdonságot a `ConfigurationData` letiltása az alábbiak szerint:</span><span class="sxs-lookup"><span data-stu-id="7dccd-172">In this case add the `PSDscAllowDomainUser` property to the `ConfigurationData` block as follows:</span></span>

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

<span data-ttu-id="7dccd-173">Most már a konfigurációs parancsfájlt a MOF-fájlt, hibák és figyelmeztetések nélkül hoz létre.</span><span class="sxs-lookup"><span data-stu-id="7dccd-173">Now the configuration script will generate the MOF file with no errors or warnings.</span></span>
