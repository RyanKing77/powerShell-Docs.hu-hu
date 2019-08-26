---
ms.date: 07/10/2019
keywords: jea, PowerShell, biztonság
title: JEA munkamenet-konfigurációk
ms.openlocfilehash: 650d0d11ef13605847d0822249e29e3491180629
ms.sourcegitcommit: e894ed833cef57967cdaf002f8c883f66864e836
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/25/2019
ms.locfileid: "70017880"
---
# <a name="jea-session-configurations"></a><span data-ttu-id="1227b-103">JEA munkamenet-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="1227b-103">JEA Session Configurations</span></span>

<span data-ttu-id="1227b-104">Egy JEA-végpont regisztrálva van egy rendszeren egy PowerShell-munkamenet konfigurációs fájljának létrehozásával és regisztrálásával.</span><span class="sxs-lookup"><span data-stu-id="1227b-104">A JEA endpoint is registered on a system by creating and registering a PowerShell session configuration file.</span></span> <span data-ttu-id="1227b-105">A munkamenet-konfigurációk határozzák meg, hogy kik használhatják a JEA-végpontot, és hogy mely szerepkörökhöz férhetnek hozzá.</span><span class="sxs-lookup"><span data-stu-id="1227b-105">Session configurations define who can use the JEA endpoint and which roles they have access to.</span></span> <span data-ttu-id="1227b-106">Emellett olyan globális beállításokat is definiálnak, amelyek a JEA-munkamenet összes felhasználójára érvényesek.</span><span class="sxs-lookup"><span data-stu-id="1227b-106">They also define global settings that apply to all users of the JEA session.</span></span>

## <a name="create-a-session-configuration-file"></a><span data-ttu-id="1227b-107">Munkamenet-konfigurációs fájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="1227b-107">Create a session configuration file</span></span>

<span data-ttu-id="1227b-108">JEA-végpont regisztrálásához meg kell adnia a végpont konfigurálásának módját.</span><span class="sxs-lookup"><span data-stu-id="1227b-108">To register a JEA endpoint, you must specify how that endpoint is configured.</span></span> <span data-ttu-id="1227b-109">Számos lehetőség van a megfontolásra.</span><span class="sxs-lookup"><span data-stu-id="1227b-109">There are many options to consider.</span></span> <span data-ttu-id="1227b-110">A legfontosabb lehetőségek a következők:</span><span class="sxs-lookup"><span data-stu-id="1227b-110">The most important options are:</span></span>

- <span data-ttu-id="1227b-111">Ki fér hozzá a JEA-végponthoz</span><span class="sxs-lookup"><span data-stu-id="1227b-111">Who has access to the JEA endpoint</span></span>
- <span data-ttu-id="1227b-112">A hozzárendelt szerepkörök</span><span class="sxs-lookup"><span data-stu-id="1227b-112">Which roles they be assigned</span></span>
- <span data-ttu-id="1227b-113">A borító alatt használt JEA</span><span class="sxs-lookup"><span data-stu-id="1227b-113">Which identity JEA uses under the covers</span></span>
- <span data-ttu-id="1227b-114">Az JEA-végpont neve</span><span class="sxs-lookup"><span data-stu-id="1227b-114">The name of the JEA endpoint</span></span>

<span data-ttu-id="1227b-115">Ezek a beállítások egy PowerShell-adatfájlban, egy `.pssc` PowerShell-munkamenet konfigurációs fájl néven ismert bővítménnyel vannak meghatározva.</span><span class="sxs-lookup"><span data-stu-id="1227b-115">These options are defined in a PowerShell data file with a `.pssc` extension known as a PowerShell session configuration file.</span></span> <span data-ttu-id="1227b-116">A munkamenet-konfigurációs fájl bármely szövegszerkesztővel szerkeszthető.</span><span class="sxs-lookup"><span data-stu-id="1227b-116">The session configuration file can be edited using any text editor.</span></span>

<span data-ttu-id="1227b-117">A következő parancs futtatásával hozzon létre egy üres sablon-konfigurációs fájlt.</span><span class="sxs-lookup"><span data-stu-id="1227b-117">Run the following command to create a blank template configuration file.</span></span>

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\MyJEAEndpoint.pssc
```

> [!TIP]
> <span data-ttu-id="1227b-118">Alapértelmezés szerint csak a leggyakoribb konfigurációs beállítások szerepelnek a sablonban.</span><span class="sxs-lookup"><span data-stu-id="1227b-118">Only the most common configuration options are included in the template file by default.</span></span> <span data-ttu-id="1227b-119">`-Full` A kapcsoló használatával adja meg az összes vonatkozó beállítást a generált Ferb.</span><span class="sxs-lookup"><span data-stu-id="1227b-119">Use the `-Full` switch to include all applicable settings in the generated PSSC.</span></span>

<span data-ttu-id="1227b-120">A `-SessionType RestrictedRemoteServer` mező azt jelzi, hogy a munkamenet-konfigurációt a JEA használja a biztonságos felügyelethez.</span><span class="sxs-lookup"><span data-stu-id="1227b-120">The `-SessionType RestrictedRemoteServer` field indicates that the session configuration is used by JEA for secure management.</span></span> <span data-ttu-id="1227b-121">Az ilyen típusú munkamenetek nem **nyelvi** módban működnek, és csak a következő alapértelmezett parancsokhoz (és aliasokhoz) férnek hozzá:</span><span class="sxs-lookup"><span data-stu-id="1227b-121">Sessions of this type operate in **NoLanguage** mode and only have access to the following default commands (and aliases):</span></span>

- <span data-ttu-id="1227b-122">Clear-Host (CLS, Clear)</span><span class="sxs-lookup"><span data-stu-id="1227b-122">Clear-Host (cls, clear)</span></span>
- <span data-ttu-id="1227b-123">Exit-PSSession (exsn, Kilépés)</span><span class="sxs-lookup"><span data-stu-id="1227b-123">Exit-PSSession (exsn, exit)</span></span>
- <span data-ttu-id="1227b-124">Get-Command (GCM)</span><span class="sxs-lookup"><span data-stu-id="1227b-124">Get-Command (gcm)</span></span>
- <span data-ttu-id="1227b-125">Get-FormatData</span><span class="sxs-lookup"><span data-stu-id="1227b-125">Get-FormatData</span></span>
- <span data-ttu-id="1227b-126">Get-Help</span><span class="sxs-lookup"><span data-stu-id="1227b-126">Get-Help</span></span>
- <span data-ttu-id="1227b-127">Mérték – objektum (mérték)</span><span class="sxs-lookup"><span data-stu-id="1227b-127">Measure-Object (measure)</span></span>
- <span data-ttu-id="1227b-128">Alapértelmezett</span><span class="sxs-lookup"><span data-stu-id="1227b-128">Out-Default</span></span>
- <span data-ttu-id="1227b-129">Select-Object (kiválasztás)</span><span class="sxs-lookup"><span data-stu-id="1227b-129">Select-Object (select)</span></span>

<span data-ttu-id="1227b-130">Nincsenek elérhető PowerShell-szolgáltatók, és nincsenek külső programok (végrehajtható fájlok vagy parancsfájlok).</span><span class="sxs-lookup"><span data-stu-id="1227b-130">No PowerShell providers are available, nor are any external programs (executables or scripts).</span></span>

<span data-ttu-id="1227b-131">A nyelvi módokról további információt a következő témakörben talál: [about_Language_modes](/powershell/module/microsoft.powershell.core/about/about_language_modes).</span><span class="sxs-lookup"><span data-stu-id="1227b-131">For more information about language modes, see [about_Language_modes](/powershell/module/microsoft.powershell.core/about/about_language_modes).</span></span>

### <a name="choose-the-jea-identity"></a><span data-ttu-id="1227b-132">JEA-identitás kiválasztása</span><span class="sxs-lookup"><span data-stu-id="1227b-132">Choose the JEA identity</span></span>

<span data-ttu-id="1227b-133">A háttérben a JEA szüksége van egy identitásra (fiókra), amelyet a rendszer a csatlakoztatott felhasználó parancsainak futtatásakor használ.</span><span class="sxs-lookup"><span data-stu-id="1227b-133">Behind the scenes, JEA needs an identity (account) to use when running a connected user's commands.</span></span>
<span data-ttu-id="1227b-134">Meghatározhatja, hogy melyik Identity JEA használja a munkamenet-konfigurációs fájlban.</span><span class="sxs-lookup"><span data-stu-id="1227b-134">You define which identity JEA uses in the session configuration file.</span></span>

#### <a name="local-virtual-account"></a><span data-ttu-id="1227b-135">Helyi virtuális fiók</span><span class="sxs-lookup"><span data-stu-id="1227b-135">Local Virtual Account</span></span>

<span data-ttu-id="1227b-136">A helyi virtuális fiókok akkor hasznosak, ha az JEA-végponthoz definiált összes szerepkör a helyi gép felügyeletére szolgál, és egy helyi rendszergazdai fiók elegendő a parancsok sikeres futtatásához.</span><span class="sxs-lookup"><span data-stu-id="1227b-136">Local virtual accounts are useful when all roles defined for the JEA endpoint are used to manage the local machine and a local administrator account is sufficient to run the commands successfully.</span></span>
<span data-ttu-id="1227b-137">A virtuális fiókok olyan ideiglenes fiókok, amelyek egyediek egy adott felhasználó számára, és csak a PowerShell-munkamenet időtartama alatt tartanak.</span><span class="sxs-lookup"><span data-stu-id="1227b-137">Virtual accounts are temporary accounts that are unique to a specific user and only last for the duration of their PowerShell session.</span></span> <span data-ttu-id="1227b-138">Egy tagkiszolgálón vagy munkaállomáson a virtuális fiókok a helyi számítógép **rendszergazdák** csoportjába tartoznak.</span><span class="sxs-lookup"><span data-stu-id="1227b-138">On a member server or workstation, virtual accounts belong to the local computer's **Administrators** group.</span></span> <span data-ttu-id="1227b-139">Active Directory-tartomány vezérlőn a virtuális fiókok a tartomány Tartománygazdák csoportjába tartoznak.</span><span class="sxs-lookup"><span data-stu-id="1227b-139">On an Active Directory Domain Controller, virtual accounts belong to the domain's **Domain Admins** group.</span></span>

```powershell
# Setting the session to use a virtual account
RunAsVirtualAccount = $true
```

<span data-ttu-id="1227b-140">Ha a munkamenet-konfiguráció által meghatározott szerepkörök nem igényelnek teljes rendszergazdai jogosultságot, megadhatja azokat a biztonsági csoportokat, amelyekhez a virtuális fiók tartozni fog.</span><span class="sxs-lookup"><span data-stu-id="1227b-140">If the roles defined by the session configuration don't require full administrative privilege, you can specify the security groups to which the virtual account will belong.</span></span> <span data-ttu-id="1227b-141">Egy tagkiszolgálón vagy munkaállomáson a megadott biztonsági csoportoknak helyi csoportoknak kell lenniük, és nem lehetnek tartományokból származó csoportok.</span><span class="sxs-lookup"><span data-stu-id="1227b-141">On a member server or workstation, the specified security groups must be local groups, not groups from a domain.</span></span>

<span data-ttu-id="1227b-142">Ha meg van adva egy vagy több biztonsági csoport, a virtuális fiók nincs hozzárendelve a helyi vagy a tartományi rendszergazdák csoporthoz.</span><span class="sxs-lookup"><span data-stu-id="1227b-142">When one or more security groups are specified, the virtual account isn't assigned to the local or domain administrators group.</span></span>

```powershell
# Setting the session to use a virtual account that only belongs to the NetworkOperator and NetworkAuditor local groups
RunAsVirtualAccount = $true
RunAsVirtualAccountGroups = 'NetworkOperator', 'NetworkAuditor'
```

> [!NOTE]
> <span data-ttu-id="1227b-143">A virtuális fiókok a helyi kiszolgáló biztonsági házirendjében ideiglenesen biztosítják a bejelentkezést szolgáltatásként.</span><span class="sxs-lookup"><span data-stu-id="1227b-143">Virtual accounts are temporarily granted the Logon as a service right in the local server security policy.</span></span> <span data-ttu-id="1227b-144">Ha a megadott VirtualAccountGroups egyike már megkapta ezt a jogot a szabályzatban, a rendszer már nem adja hozzá és nem távolítja el az egyes virtuális fiókokat a szabályzatból.</span><span class="sxs-lookup"><span data-stu-id="1227b-144">If one of the VirtualAccountGroups specified has already been granted this right in the policy, the individual virtual account will no longer be added and removed from the policy.</span></span> <span data-ttu-id="1227b-145">Ez olyan forgatókönyvekben lehet hasznos, mint például a tartományvezérlők, amelyekben a tartományvezérlő biztonsági házirendjének felülvizsgálata szigorúan naplózva van.</span><span class="sxs-lookup"><span data-stu-id="1227b-145">This can be useful in scenarios such as domain controllers where revisions to the domain controller security policy are closely audited.</span></span> <span data-ttu-id="1227b-146">Ez csak a Windows Server 2016-es verzióban érhető el, a januári 2018-es vagy újabb kumulatív és a Windows Server 2019-es verzióban pedig a január 2019-es vagy újabb kumulatív</span><span class="sxs-lookup"><span data-stu-id="1227b-146">This is only available in Windows Server 2016 with the November 2018 or later rollup and Windows Server 2019 with the January 2019 or later rollup.</span></span>

#### <a name="group-managed-service-account"></a><span data-ttu-id="1227b-147">Csoportosan felügyelt szolgáltatásfiók</span><span class="sxs-lookup"><span data-stu-id="1227b-147">Group-managed service account</span></span>

<span data-ttu-id="1227b-148">A csoportosan felügyelt szolgáltatásfiók (GMSA) az a megfelelő identitás, amelyet akkor kell használni, ha a JEA-felhasználóknak olyan hálózati erőforrásokhoz kell hozzáférnie, mint a fájlmegosztás és a webszolgáltatások.</span><span class="sxs-lookup"><span data-stu-id="1227b-148">A group-managed service account (GMSA) is the appropriate identity to use when JEA users need to access network resources such as file shares and web services.</span></span> <span data-ttu-id="1227b-149">A csoportosan felügyelt szolgáltatásfiókokat olyan tartományi identitást biztosít, amely a tartományon belüli bármely gépen lévő erőforrásokkal való hitelesítéshez használatos.</span><span class="sxs-lookup"><span data-stu-id="1227b-149">GMSAs give you a domain identity that is used to authenticate with resources on any machine within the domain.</span></span> <span data-ttu-id="1227b-150">A GMSA által biztosított jogosultságokat az elérni kívánt erőforrások határozzák meg.</span><span class="sxs-lookup"><span data-stu-id="1227b-150">The rights that a GMSA provides are determined by the resources you're accessing.</span></span> <span data-ttu-id="1227b-151">Nem rendelkezik rendszergazdai jogokkal semmilyen gépen vagy szolgáltatáson, kivéve, ha a gép vagy szolgáltatás rendszergazdája kifejezetten nem adta meg ezeket a jogokat a GMSA.</span><span class="sxs-lookup"><span data-stu-id="1227b-151">You don't have admin rights on any machines or services unless the machine or service administrator has explicitly granted those rights to the GMSA.</span></span>

```powershell
# Configure JEA sessions to use the GMSA in the local computer's domain
# with the sAMAccountName of 'MyJEAGMSA'
GroupManagedServiceAccount = 'Domain\MyJEAGMSA'
```

<span data-ttu-id="1227b-152">A csoportosan felügyelt szolgáltatásfiókokat csak akkor kell használni, ha szükséges:</span><span class="sxs-lookup"><span data-stu-id="1227b-152">GMSAs should only be used when necessary:</span></span>

- <span data-ttu-id="1227b-153">GMSA használata esetén nehéz nyomon követni a műveleteket a felhasználók számára.</span><span class="sxs-lookup"><span data-stu-id="1227b-153">It's difficult to trace back actions to a user when using a GMSA.</span></span> <span data-ttu-id="1227b-154">Minden felhasználó ugyanazt a futtató identitást osztja meg.</span><span class="sxs-lookup"><span data-stu-id="1227b-154">Every user shares the same run-as identity.</span></span> <span data-ttu-id="1227b-155">A PowerShell-munkamenetek átiratait és naplóit át kell tekintenie az egyes felhasználók műveletekkel való összekapcsolásához.</span><span class="sxs-lookup"><span data-stu-id="1227b-155">You must review PowerShell session transcripts and logs to correlate individual users with their actions.</span></span>

- <span data-ttu-id="1227b-156">Előfordulhat, hogy a GMSA számos olyan hálózati erőforráshoz férhet hozzá, amelyhez a csatlakozó felhasználónak nincs szüksége.</span><span class="sxs-lookup"><span data-stu-id="1227b-156">The GMSA may have access to many network resources that the connecting user doesn't need access to.</span></span> <span data-ttu-id="1227b-157">Mindig próbálja meg korlátozni a JEA-munkamenetek hatályos engedélyeit, hogy kövessék a legalacsonyabb jogosultsági szint elvét.</span><span class="sxs-lookup"><span data-stu-id="1227b-157">Always try to limit effective permissions in a JEA session to follow the principle of least privilege.</span></span>

> [!NOTE]
> <span data-ttu-id="1227b-158">A csoportosan felügyelt szolgáltatásfiókok csak a PowerShell 5,1-es vagy újabb verzióját használó tartományhoz csatlakoztatott gépeken érhetők el.</span><span class="sxs-lookup"><span data-stu-id="1227b-158">Group managed service accounts are only available on domain-joined machines using PowerShell 5.1 or newer.</span></span>

<span data-ttu-id="1227b-159">A JEA-munkamenetek biztonságossá tételéről a [biztonsági megfontolások](security-considerations.md) című cikkben olvashat bővebben.</span><span class="sxs-lookup"><span data-stu-id="1227b-159">For more information about securing a JEA session, see the [security considerations](security-considerations.md) article.</span></span>

### <a name="session-transcripts"></a><span data-ttu-id="1227b-160">Munkamenet-átiratok</span><span class="sxs-lookup"><span data-stu-id="1227b-160">Session transcripts</span></span>

<span data-ttu-id="1227b-161">Javasoljuk, hogy a JEA-végpontot úgy konfigurálja, hogy automatikusan jegyezze fel a felhasználói munkamenetek átiratait.</span><span class="sxs-lookup"><span data-stu-id="1227b-161">It's recommended that you configure a JEA endpoint to automatically record transcripts of users' sessions.</span></span> <span data-ttu-id="1227b-162">A PowerShell-munkamenetek átiratai a csatlakozó felhasználóval, a hozzájuk rendelt futtató identitással és a felhasználó által futtatott parancsokkal kapcsolatos információkat tartalmaznak.</span><span class="sxs-lookup"><span data-stu-id="1227b-162">PowerShell session transcripts contain information about the connecting user, the run as identity assigned to them, and the commands run by the user.</span></span> <span data-ttu-id="1227b-163">Hasznosak lehetnek a naplózási csapatoknak, akiknek meg kell érteniük, hogy ki hajtotta végre a rendszer adott változását.</span><span class="sxs-lookup"><span data-stu-id="1227b-163">They can be useful to an auditing team who needs to understand who made a specific change to a system.</span></span>

<span data-ttu-id="1227b-164">A munkamenet-konfigurációs fájl automatikus átírásának konfigurálásához adjon meg egy elérési utat ahhoz a mappához, ahová az átiratokat tárolni szeretné.</span><span class="sxs-lookup"><span data-stu-id="1227b-164">To configure automatic transcription in the session configuration file, provide a path to a folder where the transcripts should be stored.</span></span>

```powershell
TranscriptDirectory = 'C:\ProgramData\JEAConfiguration\Transcripts'
```

<span data-ttu-id="1227b-165">Az átiratokat a **helyi** rendszerfiók írja a mappába, amely olvasási és írási hozzáférést igényel a címtárhoz.</span><span class="sxs-lookup"><span data-stu-id="1227b-165">Transcripts are written to the folder by the **Local System** account, which requires read and write access to the directory.</span></span> <span data-ttu-id="1227b-166">Az általános jogú felhasználóknak nincs hozzáférésük a mappához.</span><span class="sxs-lookup"><span data-stu-id="1227b-166">Standard users should have no access to the folder.</span></span> <span data-ttu-id="1227b-167">Korlátozza azon biztonsági rendszergazdák számát, akik hozzáféréssel rendelkeznek a átiratok naplózásához.</span><span class="sxs-lookup"><span data-stu-id="1227b-167">Limit the number of security administrators that have access to audit the transcripts.</span></span>

### <a name="user-drive"></a><span data-ttu-id="1227b-168">Felhasználói meghajtó</span><span class="sxs-lookup"><span data-stu-id="1227b-168">User drive</span></span>

<span data-ttu-id="1227b-169">Ha a csatlakozó felhasználóknak fájlokat kell másolnia a JEA-végpontba vagy a-ból, akkor engedélyezheti a felhasználói meghajtót a munkamenet-konfigurációs fájlban.</span><span class="sxs-lookup"><span data-stu-id="1227b-169">If your connecting users need to copy files to or from the JEA endpoint, you can enable the user drive in the session configuration file.</span></span> <span data-ttu-id="1227b-170">A felhasználói meghajtó egy **PSDrive** , amely az egyes csatlakozó felhasználók egyedi mappájára van leképezve.</span><span class="sxs-lookup"><span data-stu-id="1227b-170">The user drive is a **PSDrive** that is mapped to a unique folder for each connecting user.</span></span> <span data-ttu-id="1227b-171">Ez a mappa lehetővé teszi a felhasználók számára a fájlok másolását a rendszerbe, és anélkül, hogy hozzáférést kellene adni a teljes fájlrendszerhez vagy a fájlrendszer-szolgáltatóhoz.</span><span class="sxs-lookup"><span data-stu-id="1227b-171">This folder allows users to copy files to or from the system without giving them access to the full file system or exposing the FileSystem provider.</span></span> <span data-ttu-id="1227b-172">A felhasználói meghajtó tartalma állandó a munkamenetek között olyan helyzetekben, amikor a hálózati kapcsolat megszakadhat.</span><span class="sxs-lookup"><span data-stu-id="1227b-172">The user drive contents are persistent across sessions to accommodate situations where network connectivity may be interrupted.</span></span>

```powershell
MountUserDrive = $true
```

<span data-ttu-id="1227b-173">Alapértelmezés szerint a felhasználói meghajtó legfeljebb 50 MB adatmennyiséget tárolhat felhasználónként.</span><span class="sxs-lookup"><span data-stu-id="1227b-173">By default, the user drive allows you to store a maximum of 50MB of data per user.</span></span> <span data-ttu-id="1227b-174">Korlátozhatja a felhasználók által felhasználható adatmennyiséget a *UserDriveMaximumSize* mező használatával.</span><span class="sxs-lookup"><span data-stu-id="1227b-174">You can limit the amount of data a user can consume with the *UserDriveMaximumSize* field.</span></span>

```powershell
# Enables the user drive with a per-user limit of 500MB (524288000 bytes)
MountUserDrive = $true
UserDriveMaximumSize = 524288000
```

<span data-ttu-id="1227b-175">Ha nem szeretné, hogy a felhasználói meghajtón lévő adatok állandók legyenek, egy ütemezett feladatot is beállíthat a rendszeren, hogy minden éjjel automatikusan törölje a mappát.</span><span class="sxs-lookup"><span data-stu-id="1227b-175">If you don't want data in the user drive to be persistent, you can configure a scheduled task on the system to automatically clean up the folder every night.</span></span>

> [!NOTE]
> <span data-ttu-id="1227b-176">A felhasználói meghajtó csak a PowerShell 5,1-es vagy újabb verzióiban érhető el.</span><span class="sxs-lookup"><span data-stu-id="1227b-176">The user drive is only available in PowerShell 5.1 or newer.</span></span>

<span data-ttu-id="1227b-177">További információ a PSDrives: PowerShell- [meghajtók kezelése](/powershell/scripting/samples/managing-windows-powershell-drives).</span><span class="sxs-lookup"><span data-stu-id="1227b-177">For more information about PSDrives, see [Managing PowerShell drives](/powershell/scripting/samples/managing-windows-powershell-drives).</span></span>

### <a name="role-definitions"></a><span data-ttu-id="1227b-178">Szerepkör-definíciók</span><span class="sxs-lookup"><span data-stu-id="1227b-178">Role definitions</span></span>

<span data-ttu-id="1227b-179">A munkamenet-konfigurációs fájlban lévő szerepkör-definíciók határozzák mega **felhasználók** szerepkörökhöz való hozzárendelését.</span><span class="sxs-lookup"><span data-stu-id="1227b-179">Role definitions in a session configuration file define the mapping of **users** to **roles**.</span></span> <span data-ttu-id="1227b-180">Az ebben a mezőben szereplő összes felhasználó vagy csoport engedélyt kap a JEA-végpontnak a regisztráláskor.</span><span class="sxs-lookup"><span data-stu-id="1227b-180">Every user or group included in this field is granted permission to the JEA endpoint when it's registered.</span></span>
<span data-ttu-id="1227b-181">Minden felhasználó vagy csoport csak egyszer szerepelhet kulcsként a szórótábla, de több szerepkörhöz is hozzárendelhető.</span><span class="sxs-lookup"><span data-stu-id="1227b-181">Each user or group can be included as a key in the hashtable only once, but can be assigned multiple roles.</span></span> <span data-ttu-id="1227b-182">A szerepkör-képesség neve legyen a szerepkör-képesség fájl neve, a `.psrc` kiterjesztés nélkül.</span><span class="sxs-lookup"><span data-stu-id="1227b-182">The name of the role capability should be the name of the role capability file, without the `.psrc` extension.</span></span>

```powershell
RoleDefinitions = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}
```

<span data-ttu-id="1227b-183">Ha egy felhasználó több csoporthoz is tartozik a szerepkör-definícióban, az egyes szerepkörökhöz hozzáférnek.</span><span class="sxs-lookup"><span data-stu-id="1227b-183">If a user belongs to more than one group in the role definition, they get access to the roles of each.</span></span> <span data-ttu-id="1227b-184">Ha két szerepkör engedélyezi a hozzáférést ugyanahhoz a parancsmagokhoz, a rendszer a legmegfelelőbb paramétert adja meg a felhasználó számára.</span><span class="sxs-lookup"><span data-stu-id="1227b-184">When two roles grant access to the same cmdlets, the most permissive parameter set is granted to the user.</span></span>

<span data-ttu-id="1227b-185">A szerepkör-definíciók mezőben a helyi felhasználók vagy csoportok megadásakor ügyeljen arra, hogy a számítógép nevét, a **localhost** vagy a helyettesítő karaktereket ne használja.</span><span class="sxs-lookup"><span data-stu-id="1227b-185">When specifying local users or groups in the role definitions field, be sure to use the computer name, not **localhost** or wildcards.</span></span> <span data-ttu-id="1227b-186">A számítógép nevét a `$env:COMPUTERNAME` változó vizsgálatával ellenőrizheti.</span><span class="sxs-lookup"><span data-stu-id="1227b-186">You can check the computer name by inspecting the `$env:COMPUTERNAME` variable.</span></span>

```powershell
RoleDefinitions = @{
    'MyComputerName\MyLocalGroup' = @{ RoleCapabilities = 'DnsAuditor' }
}
```

### <a name="role-capability-search-order"></a><span data-ttu-id="1227b-187">Szerepkör-képesség keresési sorrendje</span><span class="sxs-lookup"><span data-stu-id="1227b-187">Role capability search order</span></span>

<span data-ttu-id="1227b-188">Ahogy az a fenti példában is látható, a szerepkör-képességek a szerepkör-képesség fájljának alapneve szerint vannak hivatkozva.</span><span class="sxs-lookup"><span data-stu-id="1227b-188">As shown in the example above, role capabilities are referenced by the base name of the role capability file.</span></span> <span data-ttu-id="1227b-189">A fájl alapneve a kiterjesztés nélküli fájlnév.</span><span class="sxs-lookup"><span data-stu-id="1227b-189">The base name of a file is the filename without the extension.</span></span> <span data-ttu-id="1227b-190">Ha ugyanazon a néven több szerepkör-képesség is elérhető a rendszeren, a PowerShell az implicit keresési sorrendet használja az érvényes szerepkör-képességi fájl kiválasztásához.</span><span class="sxs-lookup"><span data-stu-id="1227b-190">If multiple role capabilities are available on the system with the same name, PowerShell uses its implicit search order to select the effective role capability file.</span></span> <span data-ttu-id="1227b-191">A JEA **nem** biztosít hozzáférést az összes szerepkör-képességű fájlhoz ugyanazzal a névvel.</span><span class="sxs-lookup"><span data-stu-id="1227b-191">JEA does **not** give access to all role capability files with the same name.</span></span>

<span data-ttu-id="1227b-192">A JEA a `$env:PSModulePath` környezeti változó használatával határozza meg, hogy mely elérési utakat kell keresni a szerepkör-képesség fájljaihoz.</span><span class="sxs-lookup"><span data-stu-id="1227b-192">JEA uses the `$env:PSModulePath` environment variable to determine which paths to scan for role capability files.</span></span> <span data-ttu-id="1227b-193">Az egyes elérési utakon belül a JEA a "RoleCapabilities" almappát tartalmazó érvényes PowerShell-modulokat keres.</span><span class="sxs-lookup"><span data-stu-id="1227b-193">Within each of those paths, JEA looks for valid PowerShell modules that contain a "RoleCapabilities" subfolder.</span></span> <span data-ttu-id="1227b-194">Csakúgy, mint a modulok importálásakor, a JEA a Windows által az azonos nevű egyéni szerepkör-képességekhez tartozó szerepkör-képességeket részesíti előnyben.</span><span class="sxs-lookup"><span data-stu-id="1227b-194">As with importing modules, JEA prefers role capabilities that are shipped with Windows to custom role capabilities with the same name.</span></span>

<span data-ttu-id="1227b-195">Minden más elnevezési ütközés esetén a sorrendet a Windows a címtárban található fájlokat felsoroló sorrend szerint határozza meg.</span><span class="sxs-lookup"><span data-stu-id="1227b-195">For all other naming conflicts, precedence is determined by the order in which Windows enumerates the files in the directory.</span></span> <span data-ttu-id="1227b-196">A sorrend nem biztosítható betűrendben.</span><span class="sxs-lookup"><span data-stu-id="1227b-196">The order isn't guaranteed to be alphabetical.</span></span> <span data-ttu-id="1227b-197">A rendszer az első szerepkör-képesség fájlját találta, amely megfelel a megadott névnek a csatlakozáshoz használt felhasználó számára.</span><span class="sxs-lookup"><span data-stu-id="1227b-197">The first role capability file found that matches the specified name is used for the connecting user.</span></span> <span data-ttu-id="1227b-198">Mivel a szerepkör-képesség keresési sorrendje nem determinisztikus, **erősen ajánlott** , hogy a szerepkör képességei egyedi fájlnevekkel rendelkezzenek.</span><span class="sxs-lookup"><span data-stu-id="1227b-198">Since the role capability search order isn't deterministic, it's **strongly recommended** that role capabilities have unique filenames.</span></span>

### <a name="conditional-access-rules"></a><span data-ttu-id="1227b-199">Feltételes hozzáférési szabályok</span><span class="sxs-lookup"><span data-stu-id="1227b-199">Conditional access rules</span></span>

<span data-ttu-id="1227b-200">A **RoleDefinitions** mezőben szereplő összes felhasználó és csoport automatikusan megkapja a JEA-végpontokhoz való hozzáférést.</span><span class="sxs-lookup"><span data-stu-id="1227b-200">All users and groups included in the **RoleDefinitions** field are automatically granted access to JEA endpoints.</span></span> <span data-ttu-id="1227b-201">A feltételes hozzáférési szabályok lehetővé teszik a hozzáférés pontosítását, és azt, hogy a felhasználók olyan további biztonsági csoportokhoz tartozzanak, amelyek nem érintik azokat a szerepköröket, amelyekhez hozzá van rendelve.</span><span class="sxs-lookup"><span data-stu-id="1227b-201">Conditional access rules allow you to refine this access and require users to belong to additional security groups that don't impact the roles to which they're assigned.</span></span> <span data-ttu-id="1227b-202">Ez akkor hasznos, ha integrálni szeretné az igény szerinti privilegizált hozzáférés-kezelési megoldást, az intelligens kártyás hitelesítést vagy más, a JEA-t használó többtényezős hitelesítési megoldást.</span><span class="sxs-lookup"><span data-stu-id="1227b-202">This is useful when you want to integrate a just-in-time privileged access management solution, smartcard authentication, or other multifactor authentication solution with JEA.</span></span>

<span data-ttu-id="1227b-203">A feltételes hozzáférési szabályok a munkamenet-konfigurációs fájl RequiredGroups mezőjében vannak meghatározva.</span><span class="sxs-lookup"><span data-stu-id="1227b-203">Conditional access rules are defined in the RequiredGroups field in a session configuration file.</span></span>
<span data-ttu-id="1227b-204">Itt megadhat egy szórótábla (opcionálisan beágyazott), amely "és" és "vagy" kulcsot használ a szabályok létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="1227b-204">There, you can provide a hashtable (optionally nested) that uses 'And' and 'Or' keys to construct your rules.</span></span> <span data-ttu-id="1227b-205">Íme néhány példa a mező használatára:</span><span class="sxs-lookup"><span data-stu-id="1227b-205">Here are some examples of how to use this field:</span></span>

```powershell
# Example 1: Connecting users must belong to a security group called "elevated-jea"
RequiredGroups = @{ And = 'elevated-jea' }

# Example 2: Connecting users must have signed on with 2 factor authentication or a smart card
# The 2 factor authentication group name is "2FA-logon" and the smart card group name is "smartcard-logon"
RequiredGroups = @{ Or = '2FA-logon', 'smartcard-logon' }

# Example 3: Connecting users must elevate into "elevated-jea" with their JIT system and have logged on with 2FA or a smart card
RequiredGroups = @{ And = 'elevated-jea', @{ Or = '2FA-logon', 'smartcard-logon' }}
```

> [!NOTE]
> <span data-ttu-id="1227b-206">A feltételes hozzáférési szabályok csak a PowerShell 5,1-es vagy újabb verzióiban érhetők el.</span><span class="sxs-lookup"><span data-stu-id="1227b-206">Conditional access rules are only available in PowerShell 5.1 or newer.</span></span>

### <a name="other-properties"></a><span data-ttu-id="1227b-207">Egyéb tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="1227b-207">Other properties</span></span>

<span data-ttu-id="1227b-208">A munkamenet-konfigurációs fájlok is elvégezhetik az összes szerepkör-képességgel rendelkező fájlt, csak anélkül, hogy a felhasználókat különböző parancsokhoz kellene csatlakoztatni.</span><span class="sxs-lookup"><span data-stu-id="1227b-208">Session configuration files can also do everything a role capability file can do, just without the ability to give connecting users access to different commands.</span></span> <span data-ttu-id="1227b-209">Ha engedélyezni szeretné, hogy az összes felhasználó hozzáférjen bizonyos parancsmagokhoz, függvényekhez vagy szolgáltatóhoz, a munkamenet-konfigurációs fájlban is megteheti a jogot.</span><span class="sxs-lookup"><span data-stu-id="1227b-209">If you want to allow all users access to specific cmdlets, functions, or providers, you can do so right in the session configuration file.</span></span>
<span data-ttu-id="1227b-210">A munkamenet-konfigurációs fájl támogatott tulajdonságainak teljes listájához futtassa a parancsot `Get-Help New-PSSessionConfigurationFile -Full`.</span><span class="sxs-lookup"><span data-stu-id="1227b-210">For a full list of supported properties in the session configuration file, run `Get-Help New-PSSessionConfigurationFile -Full`.</span></span>

## <a name="testing-a-session-configuration-file"></a><span data-ttu-id="1227b-211">Munkamenet-konfigurációs fájl tesztelése</span><span class="sxs-lookup"><span data-stu-id="1227b-211">Testing a session configuration file</span></span>

<span data-ttu-id="1227b-212">A [test-PSSessionConfigurationFile](/powershell/module/microsoft.powershell.core/test-pssessionconfigurationfile) parancsmag használatával tesztelheti a munkamenetek konfigurációját.</span><span class="sxs-lookup"><span data-stu-id="1227b-212">You can test a session configuration using the [Test-PSSessionConfigurationFile](/powershell/module/microsoft.powershell.core/test-pssessionconfigurationfile) cmdlet.</span></span> <span data-ttu-id="1227b-213">Ha manuálisan szerkeszti a `.pssc` fájlt, javasoljuk, hogy tesztelje a munkamenet-konfigurációs fájlt.</span><span class="sxs-lookup"><span data-stu-id="1227b-213">It's recommended that you test your session configuration file if you've manually edited the `.pssc` file.</span></span> <span data-ttu-id="1227b-214">A tesztelés biztosítja a szintaxis helyességét.</span><span class="sxs-lookup"><span data-stu-id="1227b-214">Testing ensures the syntax is correct.</span></span> <span data-ttu-id="1227b-215">Ha egy munkamenet-konfigurációs fájl nem tudja végrehajtani ezt a tesztet, nem regisztrálható a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="1227b-215">If a session configuration file fails this test, it can't be registered on the system.</span></span>

## <a name="sample-session-configuration-file"></a><span data-ttu-id="1227b-216">Példa a munkamenet konfigurációs fájljára</span><span class="sxs-lookup"><span data-stu-id="1227b-216">Sample session configuration file</span></span>

<span data-ttu-id="1227b-217">Az alábbi példa bemutatja, hogyan hozhat létre és érvényesítheti a JEA munkamenet-konfigurációját.</span><span class="sxs-lookup"><span data-stu-id="1227b-217">The following example shows how to create and validate a session configuration for JEA.</span></span> <span data-ttu-id="1227b-218">A szerepkör-definíciók létrehozása és tárolása a `$roles` változóban a kényelem és az olvashatóság érdekében történik.</span><span class="sxs-lookup"><span data-stu-id="1227b-218">The role definitions are created and stored in the `$roles` variable for convenience and readability.</span></span> <span data-ttu-id="1227b-219">Erre nincs szükség.</span><span class="sxs-lookup"><span data-stu-id="1227b-219">It isn't a requirement to do so.</span></span>

```powershell
$roles = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}

New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\JEAConfig.pssc -RunAsVirtualAccount -TranscriptDirectory 'C:\ProgramData\JEAConfiguration\Transcripts' -RoleDefinitions $roles -RequiredGroups @{ Or = '2FA-logon', 'smartcard-logon' }
Test-PSSessionConfigurationFile -Path .\JEAConfig.pssc # should yield True
```

## <a name="updating-session-configuration-files"></a><span data-ttu-id="1227b-220">Munkamenet-konfigurációs fájlok frissítése</span><span class="sxs-lookup"><span data-stu-id="1227b-220">Updating session configuration files</span></span>

<span data-ttu-id="1227b-221">Ha módosítani szeretné egy JEA-munkamenet konfigurációjának tulajdonságait, beleértve a felhasználók szerepkörökhöz való hozzárendelését, [](register-jea.md#unregistering-jea-configurations)akkor meg kell szüntetnie a regisztrációt.</span><span class="sxs-lookup"><span data-stu-id="1227b-221">To change the properties of a JEA session configuration, including the mapping of users to roles, you must [unregister](register-jea.md#unregistering-jea-configurations).</span></span> <span data-ttu-id="1227b-222">Ezután [regisztrálja újra](register-jea.md) a JEA munkamenet-konfigurációt egy frissített munkamenet-konfigurációs fájllal.</span><span class="sxs-lookup"><span data-stu-id="1227b-222">Then, [re-register](register-jea.md) the JEA session configuration using an updated session configuration file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1227b-223">További lépések</span><span class="sxs-lookup"><span data-stu-id="1227b-223">Next steps</span></span>

- [<span data-ttu-id="1227b-224">JEA-konfiguráció regisztrálása</span><span class="sxs-lookup"><span data-stu-id="1227b-224">Register a JEA configuration</span></span>](register-jea.md)
- [<span data-ttu-id="1227b-225">JEA szerepköreinek szerzője</span><span class="sxs-lookup"><span data-stu-id="1227b-225">Author JEA roles</span></span>](role-capabilities.md)
