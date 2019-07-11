---
ms.date: 07/10/2019
keywords: a jea, powershell, biztonsági
title: Jea-t a munkamenet-konfigurációk
ms.openlocfilehash: 650d0d11ef13605847d0822249e29e3491180629
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726551"
---
# <a name="jea-session-configurations"></a><span data-ttu-id="a9dde-103">Jea-t a munkamenet-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="a9dde-103">JEA Session Configurations</span></span>

<span data-ttu-id="a9dde-104">A JEA-végpont létrehozásával és a egy PowerShell-munkamenet konfigurációs fájl regisztrálása regisztrálva van a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="a9dde-104">A JEA endpoint is registered on a system by creating and registering a PowerShell session configuration file.</span></span> <span data-ttu-id="a9dde-105">A munkamenet-konfigurációk határozza meg, ki használhatja a JEA-végpont, és mely szerepkörök rendelkeznek hozzáféréssel.</span><span class="sxs-lookup"><span data-stu-id="a9dde-105">Session configurations define who can use the JEA endpoint and which roles they have access to.</span></span> <span data-ttu-id="a9dde-106">A JEA-munkamenet az összes felhasználóra érvényes globális beállítások is definiálják.</span><span class="sxs-lookup"><span data-stu-id="a9dde-106">They also define global settings that apply to all users of the JEA session.</span></span>

## <a name="create-a-session-configuration-file"></a><span data-ttu-id="a9dde-107">Egy munkamenet-konfigurációs fájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="a9dde-107">Create a session configuration file</span></span>

<span data-ttu-id="a9dde-108">A JEA-végpontjának regisztrálását, meg kell adnia, hogy a végpont konfigurálását.</span><span class="sxs-lookup"><span data-stu-id="a9dde-108">To register a JEA endpoint, you must specify how that endpoint is configured.</span></span> <span data-ttu-id="a9dde-109">Számos módon kell figyelembe venni.</span><span class="sxs-lookup"><span data-stu-id="a9dde-109">There are many options to consider.</span></span> <span data-ttu-id="a9dde-110">A legfontosabb választási lehetőségek a következők:</span><span class="sxs-lookup"><span data-stu-id="a9dde-110">The most important options are:</span></span>

- <span data-ttu-id="a9dde-111">Kik férhetnek hozzá a JEA-végpont</span><span class="sxs-lookup"><span data-stu-id="a9dde-111">Who has access to the JEA endpoint</span></span>
- <span data-ttu-id="a9dde-112">Melyik szerepkört kell hozzárendelni</span><span class="sxs-lookup"><span data-stu-id="a9dde-112">Which roles they be assigned</span></span>
- <span data-ttu-id="a9dde-113">Melyik identitás jea-t használja a háttérben</span><span class="sxs-lookup"><span data-stu-id="a9dde-113">Which identity JEA uses under the covers</span></span>
- <span data-ttu-id="a9dde-114">A JEA-végpont neve</span><span class="sxs-lookup"><span data-stu-id="a9dde-114">The name of the JEA endpoint</span></span>

<span data-ttu-id="a9dde-115">Ezek a beállítások határozzák meg egy PowerShell-adatokat tartalmazó fájl egy `.pssc` bővítmény ismert PowerShell munkamenet konfigurációs fájlt.</span><span class="sxs-lookup"><span data-stu-id="a9dde-115">These options are defined in a PowerShell data file with a `.pssc` extension known as a PowerShell session configuration file.</span></span> <span data-ttu-id="a9dde-116">A munkamenet-konfigurációs fájlt bármilyen szövegszerkesztőben szerkeszthető.</span><span class="sxs-lookup"><span data-stu-id="a9dde-116">The session configuration file can be edited using any text editor.</span></span>

<span data-ttu-id="a9dde-117">A következő paranccsal hozzon létre egy üres sablon konfigurációs fájlt.</span><span class="sxs-lookup"><span data-stu-id="a9dde-117">Run the following command to create a blank template configuration file.</span></span>

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\MyJEAEndpoint.pssc
```

> [!TIP]
> <span data-ttu-id="a9dde-118">A leggyakoribb konfigurációs beállítások szerepelnek a sablonfájlt alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="a9dde-118">Only the most common configuration options are included in the template file by default.</span></span> <span data-ttu-id="a9dde-119">Használja a `-Full` kapcsolót, hogy a létrehozott FERB az összes alkalmazható beállítást tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="a9dde-119">Use the `-Full` switch to include all applicable settings in the generated PSSC.</span></span>

<span data-ttu-id="a9dde-120">A `-SessionType RestrictedRemoteServer` jelzi, hogy a munkamenet-konfiguráció szerint a JEA biztonságos felügyeletére használható.</span><span class="sxs-lookup"><span data-stu-id="a9dde-120">The `-SessionType RestrictedRemoteServer` field indicates that the session configuration is used by JEA for secure management.</span></span> <span data-ttu-id="a9dde-121">Az ilyen típusú munkamenetek működtetés **NoLanguage** mód, és csak a hozzáférést a következő alapértelmezett parancsokat (és aliasok):</span><span class="sxs-lookup"><span data-stu-id="a9dde-121">Sessions of this type operate in **NoLanguage** mode and only have access to the following default commands (and aliases):</span></span>

- <span data-ttu-id="a9dde-122">CLEAR-gazdagép (cls, törlése)</span><span class="sxs-lookup"><span data-stu-id="a9dde-122">Clear-Host (cls, clear)</span></span>
- <span data-ttu-id="a9dde-123">Kilépés-PSSession (exsn, Kilépés)</span><span class="sxs-lookup"><span data-stu-id="a9dde-123">Exit-PSSession (exsn, exit)</span></span>
- <span data-ttu-id="a9dde-124">Get-Command (gcm)</span><span class="sxs-lookup"><span data-stu-id="a9dde-124">Get-Command (gcm)</span></span>
- <span data-ttu-id="a9dde-125">Get-FormatData</span><span class="sxs-lookup"><span data-stu-id="a9dde-125">Get-FormatData</span></span>
- <span data-ttu-id="a9dde-126">Get-Help</span><span class="sxs-lookup"><span data-stu-id="a9dde-126">Get-Help</span></span>
- <span data-ttu-id="a9dde-127">Measure-Object (measure)</span><span class="sxs-lookup"><span data-stu-id="a9dde-127">Measure-Object (measure)</span></span>
- <span data-ttu-id="a9dde-128">Out-Default</span><span class="sxs-lookup"><span data-stu-id="a9dde-128">Out-Default</span></span>
- <span data-ttu-id="a9dde-129">Select-Object (select)</span><span class="sxs-lookup"><span data-stu-id="a9dde-129">Select-Object (select)</span></span>

<span data-ttu-id="a9dde-130">Nincs PowerShell szolgáltató érhetők el, sem pedig bármilyen külső programok (végrehajtható fájlok vagy parancsprogramok).</span><span class="sxs-lookup"><span data-stu-id="a9dde-130">No PowerShell providers are available, nor are any external programs (executables or scripts).</span></span>

<span data-ttu-id="a9dde-131">Nyelvi módokkal kapcsolatos további információkért lásd: [about_Language_modes](/powershell/module/microsoft.powershell.core/about/about_language_modes).</span><span class="sxs-lookup"><span data-stu-id="a9dde-131">For more information about language modes, see [about_Language_modes](/powershell/module/microsoft.powershell.core/about/about_language_modes).</span></span>

### <a name="choose-the-jea-identity"></a><span data-ttu-id="a9dde-132">Válassza ki a JEA-identitás</span><span class="sxs-lookup"><span data-stu-id="a9dde-132">Choose the JEA identity</span></span>

<span data-ttu-id="a9dde-133">A színfalak mögött a JEA-identitás (fiók) egy csatlakoztatott felhasználói parancsok futtatása során használandó van szüksége.</span><span class="sxs-lookup"><span data-stu-id="a9dde-133">Behind the scenes, JEA needs an identity (account) to use when running a connected user's commands.</span></span>
<span data-ttu-id="a9dde-134">Meghatározhatja, melyik identitás jea-t használ a munkamenet-konfigurációs fájlban.</span><span class="sxs-lookup"><span data-stu-id="a9dde-134">You define which identity JEA uses in the session configuration file.</span></span>

#### <a name="local-virtual-account"></a><span data-ttu-id="a9dde-135">Virtuális helyi fiók</span><span class="sxs-lookup"><span data-stu-id="a9dde-135">Local Virtual Account</span></span>

<span data-ttu-id="a9dde-136">A virtuális helyi fiókok akkor hasznos, ha a JEA-végpont definiált összes szerepkör segítségével felügyelhető a helyi gépen, és egy helyi rendszergazdai fiók elegendő ahhoz, hogy a parancsok sikeresen lefutott.</span><span class="sxs-lookup"><span data-stu-id="a9dde-136">Local virtual accounts are useful when all roles defined for the JEA endpoint are used to manage the local machine and a local administrator account is sufficient to run the commands successfully.</span></span>
<span data-ttu-id="a9dde-137">A virtuális fiókok olyan ideiglenes fiókot, amely egy adott felhasználónak egyedi, és csak az utolsó idejére a PowerShell-munkamenetet.</span><span class="sxs-lookup"><span data-stu-id="a9dde-137">Virtual accounts are temporary accounts that are unique to a specific user and only last for the duration of their PowerShell session.</span></span> <span data-ttu-id="a9dde-138">Egy olyan tagkiszolgáló vagy a munkaállomáson, a virtuális fiókok tartoznak a helyi számítógép **rendszergazdák** csoport.</span><span class="sxs-lookup"><span data-stu-id="a9dde-138">On a member server or workstation, virtual accounts belong to the local computer's **Administrators** group.</span></span> <span data-ttu-id="a9dde-139">Az Active Directory-tartományvezérlő, a virtuális fiókok tartoznak a tartomány **Tartománygazdák** csoport.</span><span class="sxs-lookup"><span data-stu-id="a9dde-139">On an Active Directory Domain Controller, virtual accounts belong to the domain's **Domain Admins** group.</span></span>

```powershell
# Setting the session to use a virtual account
RunAsVirtualAccount = $true
```

<span data-ttu-id="a9dde-140">Ha a szerepköröket, a munkamenet-konfiguráció által meghatározott nincs szükségük teljes körű rendszergazdai jogosultság, megadhatja a biztonsági csoportok, amelyhez a virtuális fiók fog tartozni.</span><span class="sxs-lookup"><span data-stu-id="a9dde-140">If the roles defined by the session configuration don't require full administrative privilege, you can specify the security groups to which the virtual account will belong.</span></span> <span data-ttu-id="a9dde-141">Egy olyan tagkiszolgáló vagy a munkaállomáson a megadott biztonsági csoportokban helyi csoportok nem a tartományból kell lennie.</span><span class="sxs-lookup"><span data-stu-id="a9dde-141">On a member server or workstation, the specified security groups must be local groups, not groups from a domain.</span></span>

<span data-ttu-id="a9dde-142">Ha egy vagy több biztonsági csoportokat is meg van adva, a virtuális fiók nincs hozzárendelve a helyi vagy tartományi rendszergazdák csoportba.</span><span class="sxs-lookup"><span data-stu-id="a9dde-142">When one or more security groups are specified, the virtual account isn't assigned to the local or domain administrators group.</span></span>

```powershell
# Setting the session to use a virtual account that only belongs to the NetworkOperator and NetworkAuditor local groups
RunAsVirtualAccount = $true
RunAsVirtualAccountGroups = 'NetworkOperator', 'NetworkAuditor'
```

> [!NOTE]
> <span data-ttu-id="a9dde-143">A virtuális fiókok ideiglenesen kapnak a bejelentkezés, a szolgáltatás közvetlenül a helyi kiszolgálói biztonsági házirendben.</span><span class="sxs-lookup"><span data-stu-id="a9dde-143">Virtual accounts are temporarily granted the Logon as a service right in the local server security policy.</span></span> <span data-ttu-id="a9dde-144">Ha a megadott VirtualAccountGroups egyike már rendelkezik ezzel a jogosultsággal, a házirendben, az egyes virtuális fiók lesz többé nem hozzáadható és eltávolítható a szabályzat alól.</span><span class="sxs-lookup"><span data-stu-id="a9dde-144">If one of the VirtualAccountGroups specified has already been granted this right in the policy, the individual virtual account will no longer be added and removed from the policy.</span></span> <span data-ttu-id="a9dde-145">Ez például tartományvezérlőkkel, ahol a tartományvezérlő biztonsági házirendjének felülvizsgálata szorosan naplóz esetekben hasznos lehet.</span><span class="sxs-lookup"><span data-stu-id="a9dde-145">This can be useful in scenarios such as domain controllers where revisions to the domain controller security policy are closely audited.</span></span> <span data-ttu-id="a9dde-146">Ez a lehetőség csak a 2018 November rendelkező Windows Server 2016 vagy újabb kumulatív és a Windows Server 2019 a január 2019- vagy újabb kumulatív.</span><span class="sxs-lookup"><span data-stu-id="a9dde-146">This is only available in Windows Server 2016 with the November 2018 or later rollup and Windows Server 2019 with the January 2019 or later rollup.</span></span>

#### <a name="group-managed-service-account"></a><span data-ttu-id="a9dde-147">Csoportosan felügyelt szolgáltatásfiók</span><span class="sxs-lookup"><span data-stu-id="a9dde-147">Group-managed service account</span></span>

<span data-ttu-id="a9dde-148">Csoportosan felügyelt szolgáltatásfiók (GMSA) a megfelelő identitással fussanak JEA felhasználók hozzáférjenek a hálózati erőforrásokhoz, például fájlmegosztásokat és a webszolgáltatások kell használni.</span><span class="sxs-lookup"><span data-stu-id="a9dde-148">A group-managed service account (GMSA) is the appropriate identity to use when JEA users need to access network resources such as file shares and web services.</span></span> <span data-ttu-id="a9dde-149">Csoportosan felügyelt szolgáltatásfiókokat adjon egy tartományi identitás, amely minden olyan gép, a tartományon belül található erőforrásokkal hitelesítésére szolgál.</span><span class="sxs-lookup"><span data-stu-id="a9dde-149">GMSAs give you a domain identity that is used to authenticate with resources on any machine within the domain.</span></span> <span data-ttu-id="a9dde-150">A jogosultságokat, amelyeket a csoportosan felügyelt Szolgáltatásfiók biztosít határozza meg az erőforrásokat ér el.</span><span class="sxs-lookup"><span data-stu-id="a9dde-150">The rights that a GMSA provides are determined by the resources you're accessing.</span></span> <span data-ttu-id="a9dde-151">Rendszergazdai jogosultságok minden olyan gép vagy szolgáltatás nem rendelkezik, kivéve, ha a gép vagy szolgáltatás-rendszergazda explicit módon megadta ezeket a jogokat a csoportosan felügyelt Szolgáltatásfiókot.</span><span class="sxs-lookup"><span data-stu-id="a9dde-151">You don't have admin rights on any machines or services unless the machine or service administrator has explicitly granted those rights to the GMSA.</span></span>

```powershell
# Configure JEA sessions to use the GMSA in the local computer's domain
# with the sAMAccountName of 'MyJEAGMSA'
GroupManagedServiceAccount = 'Domain\MyJEAGMSA'
```

<span data-ttu-id="a9dde-152">Csoportosan felügyelt szolgáltatásfiókokat csak szükség esetén használható:</span><span class="sxs-lookup"><span data-stu-id="a9dde-152">GMSAs should only be used when necessary:</span></span>

- <span data-ttu-id="a9dde-153">Meglehetősen nehéz nyomon követését egy felhasználói műveletek csoportosan felügyelt Szolgáltatásfiók használata esetén.</span><span class="sxs-lookup"><span data-stu-id="a9dde-153">It's difficult to trace back actions to a user when using a GMSA.</span></span> <span data-ttu-id="a9dde-154">Minden felhasználói fájlmegosztások azonos futtató identitását.</span><span class="sxs-lookup"><span data-stu-id="a9dde-154">Every user shares the same run-as identity.</span></span> <span data-ttu-id="a9dde-155">Nézze át PowerShell-munkamenet szövegekben és naplók korrelációját, ha azok a műveletek az egyéni felhasználók számára.</span><span class="sxs-lookup"><span data-stu-id="a9dde-155">You must review PowerShell session transcripts and logs to correlate individual users with their actions.</span></span>

- <span data-ttu-id="a9dde-156">A csoportosan felügyelt Szolgáltatásfiók lehet számos olyan hálózati erőforrásokra, amely a kapcsolódó felhasználó nem kell a hozzáférést.</span><span class="sxs-lookup"><span data-stu-id="a9dde-156">The GMSA may have access to many network resources that the connecting user doesn't need access to.</span></span> <span data-ttu-id="a9dde-157">Mindig próbálja hatályos engedélyek korlátozására, kövesse a legalacsonyabb jogosultsági szint elvének JEA munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="a9dde-157">Always try to limit effective permissions in a JEA session to follow the principle of least privilege.</span></span>

> [!NOTE]
> <span data-ttu-id="a9dde-158">A felügyelt szolgáltatásfiókok csoportot csak olyan elérhető a tartományhoz csatlakoztatott gépeket használ a PowerShell 5.1-es vagy újabb.</span><span class="sxs-lookup"><span data-stu-id="a9dde-158">Group managed service accounts are only available on domain-joined machines using PowerShell 5.1 or newer.</span></span>

<span data-ttu-id="a9dde-159">A JEA-munkamenet védelmével kapcsolatos további információkért lásd: a [biztonsági szempontok](security-considerations.md) cikk.</span><span class="sxs-lookup"><span data-stu-id="a9dde-159">For more information about securing a JEA session, see the [security considerations](security-considerations.md) article.</span></span>

### <a name="session-transcripts"></a><span data-ttu-id="a9dde-160">Munkamenet szövegekben</span><span class="sxs-lookup"><span data-stu-id="a9dde-160">Session transcripts</span></span>

<span data-ttu-id="a9dde-161">Javasoljuk, hogy konfigurálja-e a JEA végpontot a felhasználói munkamenetek automatikus rögzítése szövegekben.</span><span class="sxs-lookup"><span data-stu-id="a9dde-161">It's recommended that you configure a JEA endpoint to automatically record transcripts of users' sessions.</span></span> <span data-ttu-id="a9dde-162">PowerShell-munkamenet átiratok a csatlakozó felhasználó, a hozzájuk tartozó identitás futtató vonatkozó adatokat tartalmaznak, és a felhasználó által futtatott parancsok.</span><span class="sxs-lookup"><span data-stu-id="a9dde-162">PowerShell session transcripts contain information about the connecting user, the run as identity assigned to them, and the commands run by the user.</span></span> <span data-ttu-id="a9dde-163">Meg kell ismernie, akik által végrehajtott konkrét egy rendszer-naplózási csoport hasznos lehet.</span><span class="sxs-lookup"><span data-stu-id="a9dde-163">They can be useful to an auditing team who needs to understand who made a specific change to a system.</span></span>

<span data-ttu-id="a9dde-164">Automatikus beszédátírási konfigurálása a munkamenet-konfigurációs fájlban, hol szeretné tárolni az átiratok mappa elérési útjának megadását.</span><span class="sxs-lookup"><span data-stu-id="a9dde-164">To configure automatic transcription in the session configuration file, provide a path to a folder where the transcripts should be stored.</span></span>

```powershell
TranscriptDirectory = 'C:\ProgramData\JEAConfiguration\Transcripts'
```

<span data-ttu-id="a9dde-165">A mappa által írt átiratok a **helyi rendszer** fiókot, amelyhez szükség van az olvasási és írási hozzáférés a címtárhoz.</span><span class="sxs-lookup"><span data-stu-id="a9dde-165">Transcripts are written to the folder by the **Local System** account, which requires read and write access to the directory.</span></span> <span data-ttu-id="a9dde-166">Az általános jogú felhasználók nem hozzáféréssel kell rendelkeznie a mappában.</span><span class="sxs-lookup"><span data-stu-id="a9dde-166">Standard users should have no access to the folder.</span></span> <span data-ttu-id="a9dde-167">Az átiratok naplózási hozzáféréssel rendelkező rendszergazdák számának korlátozása.</span><span class="sxs-lookup"><span data-stu-id="a9dde-167">Limit the number of security administrators that have access to audit the transcripts.</span></span>

### <a name="user-drive"></a><span data-ttu-id="a9dde-168">Felhasználó-meghajtó</span><span class="sxs-lookup"><span data-stu-id="a9dde-168">User drive</span></span>

<span data-ttu-id="a9dde-169">Ha a csatlakozó felhasználók másolja a fájlokat, vagy a JEA-végpont szükséges, engedélyezheti a felhasználói meghajtó a munkamenet-konfigurációs fájlban.</span><span class="sxs-lookup"><span data-stu-id="a9dde-169">If your connecting users need to copy files to or from the JEA endpoint, you can enable the user drive in the session configuration file.</span></span> <span data-ttu-id="a9dde-170">A felhasználó meghajtó egy **PSDrive** , amely az egyes csatlakozó felhasználók egyedi mappát van leképezve.</span><span class="sxs-lookup"><span data-stu-id="a9dde-170">The user drive is a **PSDrive** that is mapped to a unique folder for each connecting user.</span></span> <span data-ttu-id="a9dde-171">Ez a mappa lehetővé teszi, hogy a felhasználók másolhatják a fájlokat, illetve a rendszer a hozzáférés engedélyezése a teljes fájlrendszer vagy a fájlrendszer-szolgáltatót is közzéteheti nélkül.</span><span class="sxs-lookup"><span data-stu-id="a9dde-171">This folder allows users to copy files to or from the system without giving them access to the full file system or exposing the FileSystem provider.</span></span> <span data-ttu-id="a9dde-172">A felhasználó meghajtó tartalma állandó befogadásához helyzetekben, ahol a hálózati kapcsolat megszakadhat a munkamenetek között.</span><span class="sxs-lookup"><span data-stu-id="a9dde-172">The user drive contents are persistent across sessions to accommodate situations where network connectivity may be interrupted.</span></span>

```powershell
MountUserDrive = $true
```

<span data-ttu-id="a9dde-173">Alapértelmezés szerint a felhasználó meghajtó lehetővé teszi felhasználónként 50 MB-ot legfeljebb tárolni.</span><span class="sxs-lookup"><span data-stu-id="a9dde-173">By default, the user drive allows you to store a maximum of 50MB of data per user.</span></span> <span data-ttu-id="a9dde-174">Korlátozhatja a felhasználók használhatnak fel, az adatok mennyisége a *UserDriveMaximumSize* mező.</span><span class="sxs-lookup"><span data-stu-id="a9dde-174">You can limit the amount of data a user can consume with the *UserDriveMaximumSize* field.</span></span>

```powershell
# Enables the user drive with a per-user limit of 500MB (524288000 bytes)
MountUserDrive = $true
UserDriveMaximumSize = 524288000
```

<span data-ttu-id="a9dde-175">Ha a felhasználó meghajtón állandóként adatokat nem szeretné, konfigurálhatja egy ütemezett feladatot a rendszer automatikusan törölni a mappát éjszakánként.</span><span class="sxs-lookup"><span data-stu-id="a9dde-175">If you don't want data in the user drive to be persistent, you can configure a scheduled task on the system to automatically clean up the folder every night.</span></span>

> [!NOTE]
> <span data-ttu-id="a9dde-176">A felhasználó meghajtó csak akkor érhető el a PowerShell 5.1-es vagy újabb.</span><span class="sxs-lookup"><span data-stu-id="a9dde-176">The user drive is only available in PowerShell 5.1 or newer.</span></span>

<span data-ttu-id="a9dde-177">PSDrives kapcsolatos további információkért lásd: [kezelése PowerShell-meghajtók](/powershell/scripting/samples/managing-windows-powershell-drives).</span><span class="sxs-lookup"><span data-stu-id="a9dde-177">For more information about PSDrives, see [Managing PowerShell drives](/powershell/scripting/samples/managing-windows-powershell-drives).</span></span>

### <a name="role-definitions"></a><span data-ttu-id="a9dde-178">Szerepkör-definíciók</span><span class="sxs-lookup"><span data-stu-id="a9dde-178">Role definitions</span></span>

<span data-ttu-id="a9dde-179">A munkamenet-konfigurációs fájlban található szerepkör-definíciók megadása leképezése **felhasználók** való **szerepkörök**.</span><span class="sxs-lookup"><span data-stu-id="a9dde-179">Role definitions in a session configuration file define the mapping of **users** to **roles**.</span></span> <span data-ttu-id="a9dde-180">Minden felhasználó vagy csoport szerepel ebben a mezőben a JEA-végpont engedélyt kap, ha regisztrálva van.</span><span class="sxs-lookup"><span data-stu-id="a9dde-180">Every user or group included in this field is granted permission to the JEA endpoint when it's registered.</span></span>
<span data-ttu-id="a9dde-181">Minden felhasználó vagy csoport csak egyszer lehet része lesz a kulcs a kivonattábla kulcsa, de több szerepkört is rendelhető.</span><span class="sxs-lookup"><span data-stu-id="a9dde-181">Each user or group can be included as a key in the hashtable only once, but can be assigned multiple roles.</span></span> <span data-ttu-id="a9dde-182">A név a szerepkör funkció nélkül legyen a szerepkör képesség fájl neve a `.psrc` bővítmény.</span><span class="sxs-lookup"><span data-stu-id="a9dde-182">The name of the role capability should be the name of the role capability file, without the `.psrc` extension.</span></span>

```powershell
RoleDefinitions = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}
```

<span data-ttu-id="a9dde-183">Ha egy felhasználó tartozik a szerepkör-definíció egynél több csoportot, akkor az egyes szerepkörök hozzáférést kap.</span><span class="sxs-lookup"><span data-stu-id="a9dde-183">If a user belongs to more than one group in the role definition, they get access to the roles of each.</span></span> <span data-ttu-id="a9dde-184">Ha két szerepkörnek hozzáférést ugyanazok a parancsmagok, a legmegengedőbb paraméterkészletet kapnak a felhasználó számára.</span><span class="sxs-lookup"><span data-stu-id="a9dde-184">When two roles grant access to the same cmdlets, the most permissive parameter set is granted to the user.</span></span>

<span data-ttu-id="a9dde-185">Ha a szerepkör-definíciók mezőben adja meg a helyi felhasználókat és csoportokat, ügyeljen arra, hogy a számítógép neve, nem **localhost** vagy helyettesítő karaktereket.</span><span class="sxs-lookup"><span data-stu-id="a9dde-185">When specifying local users or groups in the role definitions field, be sure to use the computer name, not **localhost** or wildcards.</span></span> <span data-ttu-id="a9dde-186">A számítógépnév vizsgálatával ellenőrizheti a `$env:COMPUTERNAME` változó.</span><span class="sxs-lookup"><span data-stu-id="a9dde-186">You can check the computer name by inspecting the `$env:COMPUTERNAME` variable.</span></span>

```powershell
RoleDefinitions = @{
    'MyComputerName\MyLocalGroup' = @{ RoleCapabilities = 'DnsAuditor' }
}
```

### <a name="role-capability-search-order"></a><span data-ttu-id="a9dde-187">Szerepkör képesség keresési sorrendje</span><span class="sxs-lookup"><span data-stu-id="a9dde-187">Role capability search order</span></span>

<span data-ttu-id="a9dde-188">A fenti példa szerint szerepkörrel képességeket a szerepkör képesség fájl alapneveként hivatkozik.</span><span class="sxs-lookup"><span data-stu-id="a9dde-188">As shown in the example above, role capabilities are referenced by the base name of the role capability file.</span></span> <span data-ttu-id="a9dde-189">A fájl alap név nélkül a kiterjesztést a fájlnév.</span><span class="sxs-lookup"><span data-stu-id="a9dde-189">The base name of a file is the filename without the extension.</span></span> <span data-ttu-id="a9dde-190">A rendszer ezzel a névvel több szerepköri funkciók érhetők el, ha a PowerShell az implicit keresési sorrendje válassza ki a szerepkör hatékony képesség fájlt használ.</span><span class="sxs-lookup"><span data-stu-id="a9dde-190">If multiple role capabilities are available on the system with the same name, PowerShell uses its implicit search order to select the effective role capability file.</span></span> <span data-ttu-id="a9dde-191">A JEA does **nem** hozzáférést biztosít minden szerepkör képesség fájl ezzel a névvel.</span><span class="sxs-lookup"><span data-stu-id="a9dde-191">JEA does **not** give access to all role capability files with the same name.</span></span>

<span data-ttu-id="a9dde-192">Jea-t használ a `$env:PSModulePath` környezeti változót, mely szolgáltatást a szerepkör képesség fájlok elérési határozza meg.</span><span class="sxs-lookup"><span data-stu-id="a9dde-192">JEA uses the `$env:PSModulePath` environment variable to determine which paths to scan for role capability files.</span></span> <span data-ttu-id="a9dde-193">Adott elérési útján belül JEA keres, amely tartalmaz egy "RoleCapabilities" almappát érvényes PowerShell-modulok.</span><span class="sxs-lookup"><span data-stu-id="a9dde-193">Within each of those paths, JEA looks for valid PowerShell modules that contain a "RoleCapabilities" subfolder.</span></span> <span data-ttu-id="a9dde-194">Csakúgy, mint a modulok importálása a JEA szerepkörrel képességeket, az egyéni szerepkör képességekkel azonos nevű Windows-tal szállított részesíti előnyben.</span><span class="sxs-lookup"><span data-stu-id="a9dde-194">As with importing modules, JEA prefers role capabilities that are shipped with Windows to custom role capabilities with the same name.</span></span>

<span data-ttu-id="a9dde-195">Minden más elnevezési ütközések elsőbbséget Windows számba veszi a könyvtárban található fájlok sorrendje határozza meg.</span><span class="sxs-lookup"><span data-stu-id="a9dde-195">For all other naming conflicts, precedence is determined by the order in which Windows enumerates the files in the directory.</span></span> <span data-ttu-id="a9dde-196">A rendelés betűrend szerinti rendezés nem garantált.</span><span class="sxs-lookup"><span data-stu-id="a9dde-196">The order isn't guaranteed to be alphabetical.</span></span> <span data-ttu-id="a9dde-197">Az első szerepkör képesség fájl található, amely megfelel a megadott nevet használja a csatlakozó felhasználó.</span><span class="sxs-lookup"><span data-stu-id="a9dde-197">The first role capability file found that matches the specified name is used for the connecting user.</span></span> <span data-ttu-id="a9dde-198">A szerepkör képesség keresés óta sorrendje nem determinisztikus, **erősen ajánlott** , szerepkörrel képességeket rendelkezik-e egyedi fájlnevet.</span><span class="sxs-lookup"><span data-stu-id="a9dde-198">Since the role capability search order isn't deterministic, it's **strongly recommended** that role capabilities have unique filenames.</span></span>

### <a name="conditional-access-rules"></a><span data-ttu-id="a9dde-199">Feltételes hozzáférési szabályok</span><span class="sxs-lookup"><span data-stu-id="a9dde-199">Conditional access rules</span></span>

<span data-ttu-id="a9dde-200">Minden felhasználó és csoport tartalmazza a **RoleDefinitions** mező automatikusan megkapja a JEA-végpont elérését.</span><span class="sxs-lookup"><span data-stu-id="a9dde-200">All users and groups included in the **RoleDefinitions** field are automatically granted access to JEA endpoints.</span></span> <span data-ttu-id="a9dde-201">Feltételes hozzáférési szabályok lehetővé teszik, hogy finomíthatja a hozzáférést, és ne befolyásolják a szerepköröket, amelyhez hozzá van rendelve, további biztonsági csoporthoz tartoznak, hogy a felhasználók.</span><span class="sxs-lookup"><span data-stu-id="a9dde-201">Conditional access rules allow you to refine this access and require users to belong to additional security groups that don't impact the roles to which they're assigned.</span></span> <span data-ttu-id="a9dde-202">Ez akkor hasznos, ha szeretné integrálni a just-in-time emelt szintű hozzáférés-kezelési megoldása, intelligens kártyás hitelesítés vagy más többtényezős hitelesítési megoldást a jea-t.</span><span class="sxs-lookup"><span data-stu-id="a9dde-202">This is useful when you want to integrate a just-in-time privileged access management solution, smartcard authentication, or other multifactor authentication solution with JEA.</span></span>

<span data-ttu-id="a9dde-203">Feltételes hozzáférési szabályok a RequiredGroups mező egy munkamenet-konfigurációs fájlban vannak definiálva.</span><span class="sxs-lookup"><span data-stu-id="a9dde-203">Conditional access rules are defined in the RequiredGroups field in a session configuration file.</span></span>
<span data-ttu-id="a9dde-204">Itt adhat meg egy kivonattáblát (szükség esetén a beágyazott) használó "És" és "Vagy" kulcsok a szabályok létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="a9dde-204">There, you can provide a hashtable (optionally nested) that uses 'And' and 'Or' keys to construct your rules.</span></span> <span data-ttu-id="a9dde-205">Íme néhány példa bemutatja, hogyan használja ezt a mezőt:</span><span class="sxs-lookup"><span data-stu-id="a9dde-205">Here are some examples of how to use this field:</span></span>

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
> <span data-ttu-id="a9dde-206">Feltételes hozzáférési szabályok csak olyan, a PowerShell 5.1-es vagy újabb.</span><span class="sxs-lookup"><span data-stu-id="a9dde-206">Conditional access rules are only available in PowerShell 5.1 or newer.</span></span>

### <a name="other-properties"></a><span data-ttu-id="a9dde-207">Egyéb tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="a9dde-207">Other properties</span></span>

<span data-ttu-id="a9dde-208">Munkamenet konfigurációs fájljainak minden szerepkör képesség fájl anélkül teheti meg, csak lehetővé teszi csatlakozó felhasználók hozzáférést biztosíthat más parancsok is megteheti.</span><span class="sxs-lookup"><span data-stu-id="a9dde-208">Session configuration files can also do everything a role capability file can do, just without the ability to give connecting users access to different commands.</span></span> <span data-ttu-id="a9dde-209">Ha azt szeretné, hogy minden felhasználó hozzáférést adott parancsmagok, függvények és szolgáltatók, megteheti közvetlenül a a munkamenet-konfigurációs fájlt.</span><span class="sxs-lookup"><span data-stu-id="a9dde-209">If you want to allow all users access to specific cmdlets, functions, or providers, you can do so right in the session configuration file.</span></span>
<span data-ttu-id="a9dde-210">A támogatott tulajdonságok a munkamenet-konfigurációs fájl teljes listájának megtekintéséhez futtassa `Get-Help New-PSSessionConfigurationFile -Full`.</span><span class="sxs-lookup"><span data-stu-id="a9dde-210">For a full list of supported properties in the session configuration file, run `Get-Help New-PSSessionConfigurationFile -Full`.</span></span>

## <a name="testing-a-session-configuration-file"></a><span data-ttu-id="a9dde-211">Egy munkamenet-konfigurációs fájl tesztelése</span><span class="sxs-lookup"><span data-stu-id="a9dde-211">Testing a session configuration file</span></span>

<span data-ttu-id="a9dde-212">A munkamenet konfigurációja használatával tesztelhet a [Test-PSSessionConfigurationFile](/powershell/module/microsoft.powershell.core/test-pssessionconfigurationfile) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="a9dde-212">You can test a session configuration using the [Test-PSSessionConfigurationFile](/powershell/module/microsoft.powershell.core/test-pssessionconfigurationfile) cmdlet.</span></span> <span data-ttu-id="a9dde-213">Javasoljuk, hogy a munkamenet-konfigurációs fájl teszteléséhez, ha manuálisan módosította a `.pssc` fájlt.</span><span class="sxs-lookup"><span data-stu-id="a9dde-213">It's recommended that you test your session configuration file if you've manually edited the `.pssc` file.</span></span> <span data-ttu-id="a9dde-214">Tesztelés biztosítja a szintaxisa helyes.</span><span class="sxs-lookup"><span data-stu-id="a9dde-214">Testing ensures the syntax is correct.</span></span> <span data-ttu-id="a9dde-215">Ha egy munkamenet-konfigurációs fájl a teszt meghiúsul, azt a rendszer nem regisztrálható.</span><span class="sxs-lookup"><span data-stu-id="a9dde-215">If a session configuration file fails this test, it can't be registered on the system.</span></span>

## <a name="sample-session-configuration-file"></a><span data-ttu-id="a9dde-216">Minta munkamenet konfigurációs fájl</span><span class="sxs-lookup"><span data-stu-id="a9dde-216">Sample session configuration file</span></span>

<span data-ttu-id="a9dde-217">Az alábbi példa bemutatja, hogyan hozhat létre, és a egy munkamenet-konfiguráció ellenőrzése a jea-t.</span><span class="sxs-lookup"><span data-stu-id="a9dde-217">The following example shows how to create and validate a session configuration for JEA.</span></span> <span data-ttu-id="a9dde-218">A szerepkör-definíciók létrehozása és tárolása a a `$roles` változó a kényelem és olvashatóság érdekében.</span><span class="sxs-lookup"><span data-stu-id="a9dde-218">The role definitions are created and stored in the `$roles` variable for convenience and readability.</span></span> <span data-ttu-id="a9dde-219">Nem követelmény ennek a végrehajtására.</span><span class="sxs-lookup"><span data-stu-id="a9dde-219">It isn't a requirement to do so.</span></span>

```powershell
$roles = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}

New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\JEAConfig.pssc -RunAsVirtualAccount -TranscriptDirectory 'C:\ProgramData\JEAConfiguration\Transcripts' -RoleDefinitions $roles -RequiredGroups @{ Or = '2FA-logon', 'smartcard-logon' }
Test-PSSessionConfigurationFile -Path .\JEAConfig.pssc # should yield True
```

## <a name="updating-session-configuration-files"></a><span data-ttu-id="a9dde-220">Munkamenet-konfigurációs fájlok frissítése</span><span class="sxs-lookup"><span data-stu-id="a9dde-220">Updating session configuration files</span></span>

<span data-ttu-id="a9dde-221">A JEA munkamenet-konfiguráció, többek között a felhasználók szerepkörökhöz leképezése tulajdonságainak módosítása kell [regisztrációját](register-jea.md#unregistering-jea-configurations).</span><span class="sxs-lookup"><span data-stu-id="a9dde-221">To change the properties of a JEA session configuration, including the mapping of users to roles, you must [unregister](register-jea.md#unregistering-jea-configurations).</span></span> <span data-ttu-id="a9dde-222">Ezt követően [újraregisztrálni](register-jea.md) a JEA munkamenet-konfiguráció frissített munkamenet konfigurációs fájl segítségével.</span><span class="sxs-lookup"><span data-stu-id="a9dde-222">Then, [re-register](register-jea.md) the JEA session configuration using an updated session configuration file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9dde-223">További lépések</span><span class="sxs-lookup"><span data-stu-id="a9dde-223">Next steps</span></span>

- [<span data-ttu-id="a9dde-224">Regisztrálja a JEA-konfiguráció</span><span class="sxs-lookup"><span data-stu-id="a9dde-224">Register a JEA configuration</span></span>](register-jea.md)
- [<span data-ttu-id="a9dde-225">Szerző JEA szerepkörök</span><span class="sxs-lookup"><span data-stu-id="a9dde-225">Author JEA roles</span></span>](role-capabilities.md)
