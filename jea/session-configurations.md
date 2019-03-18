---
ms.date: 06/12/2017
keywords: a jea, powershell, biztonsági
title: Jea-t a munkamenet-konfigurációk
ms.openlocfilehash: b98726ea7ed3aabdfd05034c3b70118e327160cd
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58056590"
---
# <a name="jea-session-configurations"></a><span data-ttu-id="5c98f-103">Jea-t a munkamenet-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="5c98f-103">JEA Session Configurations</span></span>

> <span data-ttu-id="5c98f-104">Érintett kiadások: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="5c98f-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="5c98f-105">A JEA-végpont létrehozásával és a egy PowerShell-munkamenet konfigurációs fájl regisztrálása a meghatározott módon regisztrálva van a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="5c98f-105">A JEA endpoint is registered on a system by creating and registering a PowerShell session configuration file in a specific way.</span></span>
<span data-ttu-id="5c98f-106">A munkamenet-konfigurációk meghatározásához *akik* használhatja a JEA-végpont, és mely szerepkör(ök) fog hozzáféréssel rendelkeznek.</span><span class="sxs-lookup"><span data-stu-id="5c98f-106">Session configurations determine *who* can use the JEA endpoint, and which role(s) they will have access to.</span></span>
<span data-ttu-id="5c98f-107">A JEA-munkamenet bármely szerepkör felhasználókra vonatkozó globális beállítások is definiálják.</span><span class="sxs-lookup"><span data-stu-id="5c98f-107">They also define global settings that apply to users of any role in the JEA session.</span></span>

<span data-ttu-id="5c98f-108">Ez a témakör ismerteti, hogyan hozzon létre egy PowerShell-munkamenet konfigurációs fájlt, és a JEA-végpontjának regisztrálását.</span><span class="sxs-lookup"><span data-stu-id="5c98f-108">This topic describes how to create a PowerShell session configuration file and register a JEA endpoint.</span></span>

## <a name="create-a-session-configuration-file"></a><span data-ttu-id="5c98f-109">Egy munkamenet-konfigurációs fájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="5c98f-109">Create a session configuration file</span></span>

<span data-ttu-id="5c98f-110">A JEA-végpontjának regisztrálását, adja meg, hogyan kell konfigurálni, hogy a végpont kell.</span><span class="sxs-lookup"><span data-stu-id="5c98f-110">In order to register a JEA endpoint, you need to specify how that endpoint should be configured.</span></span>
<span data-ttu-id="5c98f-111">Számos lehetőség kell figyelembe venni, a legfontosabb, mely hogy ki férhet hozzá a JEA-végpont, mely szerepköröket fogják hozzárendelni, mely identitás jea-t használja a háttérben, és mi lesz a JEA-végpont nevét.</span><span class="sxs-lookup"><span data-stu-id="5c98f-111">There are many options to consider here, the most important of which being who should have access to the JEA endpoint, which roles will they be assigned, which identity will JEA use under the covers, and what will be the name of the JEA endpoint.</span></span>
<span data-ttu-id="5c98f-112">Ezek az összes meghatározása egy PowerShell munkamenetet konfigurációs fájlban, amely egy PowerShell-adatfájlt lezárta .pssc kiterjesztéssel.</span><span class="sxs-lookup"><span data-stu-id="5c98f-112">These are all defined in a PowerShell session configuration file, which is a PowerShell data file ending with a .pssc extension.</span></span>

<span data-ttu-id="5c98f-113">A JEA-végpont vázát munkamenet konfigurációs fájl létrehozásához futtassa az alábbi parancsot.</span><span class="sxs-lookup"><span data-stu-id="5c98f-113">To create a skeleton session configuration file for JEA endpoints, run the following command.</span></span>

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\MyJEAEndpoint.pssc
```

> [!TIP]
> <span data-ttu-id="5c98f-114">A leggyakoribb konfigurációs beállítások szerepelnek a vázát fájl alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="5c98f-114">Only the most common configuration options are included in the skeleton file by default.</span></span>
> <span data-ttu-id="5c98f-115">Használja a `-Full` kapcsolót, hogy a létrehozott FERB az összes alkalmazható beállítást tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="5c98f-115">Use the `-Full` switch to include all applicable settings in the generated PSSC.</span></span>

<span data-ttu-id="5c98f-116">Megnyithatja a munkamenet-konfigurációs fájlt bármilyen szövegszerkesztőben.</span><span class="sxs-lookup"><span data-stu-id="5c98f-116">You can open the session configuration file in any text editor.</span></span>
<span data-ttu-id="5c98f-117">A `-SessionType RestrictedRemoteServer` jelzi, hogy a munkamenet-konfiguráció által használandó JEA biztonságos kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="5c98f-117">The `-SessionType RestrictedRemoteServer` field indicates that the session configuration will be used by JEA for secure management.</span></span>
<span data-ttu-id="5c98f-118">Munkamenetek van ilyen módon fog működni a [NoLanguage mód](https://technet.microsoft.com/library/dn433292.aspx) , és csak a következő 8 alapértelmezett parancsokat (és aliasok) érhető el:</span><span class="sxs-lookup"><span data-stu-id="5c98f-118">Sessions configured this way will operate in [NoLanguage mode](https://technet.microsoft.com/library/dn433292.aspx) and only have the following 8 default commands (and aliases) available:</span></span>

- <span data-ttu-id="5c98f-119">CLEAR-gazdagép (cls, törlése)</span><span class="sxs-lookup"><span data-stu-id="5c98f-119">Clear-Host (cls, clear)</span></span>
- <span data-ttu-id="5c98f-120">Kilépés-PSSession (exsn, Kilépés)</span><span class="sxs-lookup"><span data-stu-id="5c98f-120">Exit-PSSession (exsn, exit)</span></span>
- <span data-ttu-id="5c98f-121">Get-Command (gcm)</span><span class="sxs-lookup"><span data-stu-id="5c98f-121">Get-Command (gcm)</span></span>
- <span data-ttu-id="5c98f-122">Get-FormatData</span><span class="sxs-lookup"><span data-stu-id="5c98f-122">Get-FormatData</span></span>
- <span data-ttu-id="5c98f-123">Get-Help</span><span class="sxs-lookup"><span data-stu-id="5c98f-123">Get-Help</span></span>
- <span data-ttu-id="5c98f-124">Measure-Object (measure)</span><span class="sxs-lookup"><span data-stu-id="5c98f-124">Measure-Object (measure)</span></span>
- <span data-ttu-id="5c98f-125">Out-Default</span><span class="sxs-lookup"><span data-stu-id="5c98f-125">Out-Default</span></span>
- <span data-ttu-id="5c98f-126">Select-Object (select)</span><span class="sxs-lookup"><span data-stu-id="5c98f-126">Select-Object (select)</span></span>

<span data-ttu-id="5c98f-127">Nincs PowerShell szolgáltató érhetők el, sem pedig bármilyen külső programok (végrehajtható fájlok, parancsfájlok stb.).</span><span class="sxs-lookup"><span data-stu-id="5c98f-127">No PowerShell providers are available, nor are any external programs (executables, scripts, etc.).</span></span>

<span data-ttu-id="5c98f-128">Nincsenek számos más mezők, célszerű a JEA-munkamenet konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="5c98f-128">There are several other fields you will want to configure for the JEA session.</span></span>
<span data-ttu-id="5c98f-129">Azok a következő szakaszokban ismertetett.</span><span class="sxs-lookup"><span data-stu-id="5c98f-129">They are covered in the following sections.</span></span>

### <a name="choose-the-jea-identity"></a><span data-ttu-id="5c98f-130">Válassza ki a JEA-identitás</span><span class="sxs-lookup"><span data-stu-id="5c98f-130">Choose the JEA identity</span></span>

<span data-ttu-id="5c98f-131">A színfalak mögött a JEA-identitás (fiók) egy csatlakoztatott felhasználói parancsok futtatása során használandó van szüksége.</span><span class="sxs-lookup"><span data-stu-id="5c98f-131">Behind the scenes, JEA needs an identity (account) to use when running a connected user's commands.</span></span>
<span data-ttu-id="5c98f-132">Eldöntheti, melyik identitás jea-t fogja használni a munkamenet-konfigurációs fájlban.</span><span class="sxs-lookup"><span data-stu-id="5c98f-132">You decide which identity JEA will use in the session configuration file.</span></span>

#### <a name="local-virtual-account"></a><span data-ttu-id="5c98f-133">Virtuális helyi fiók</span><span class="sxs-lookup"><span data-stu-id="5c98f-133">Local Virtual Account</span></span>

<span data-ttu-id="5c98f-134">Ha a szerepköröket a JEA-végpont által támogatott összes kezelésére használhatók a helyi gépen, és egy helyi rendszergazdai fiók elegendő ahhoz, hogy a parancsok sikeresen lefutott, konfigurálnia kell a jea-t a helyi virtuális fiók használata.</span><span class="sxs-lookup"><span data-stu-id="5c98f-134">If the roles supported by this JEA endpoint are all used to manage the local machine, and a local administrator account is sufficient to run the commands successfully, you should configure JEA to use a local virtual account.</span></span>
<span data-ttu-id="5c98f-135">A virtuális fiókok olyan ideiglenes fiókot, amely egy adott felhasználónak egyedi, és csak az utolsó idejére a PowerShell-munkamenetet.</span><span class="sxs-lookup"><span data-stu-id="5c98f-135">Virtual accounts are temporary accounts that are unique to a specific user and only last for the duration of their PowerShell session.</span></span>
<span data-ttu-id="5c98f-136">Egy olyan tagkiszolgáló vagy a munkaállomáson, a virtuális fiókok tartoznak a helyi számítógép **rendszergazdák** csoportból, és a legtöbb rendszer erőforrásait elérheti.</span><span class="sxs-lookup"><span data-stu-id="5c98f-136">On a member server or workstation, virtual accounts belong to the local computer's **Administrators** group, and have access to most system resources.</span></span>
<span data-ttu-id="5c98f-137">Az Active Directory-tartományvezérlő, a virtuális fiókok tartoznak a tartomány **Tartománygazdák** csoport.</span><span class="sxs-lookup"><span data-stu-id="5c98f-137">On an Active Directory Domain Controller, virtual accounts belong to the domain's **Domain Admins** group.</span></span>

```powershell
# Setting the session to use a virtual account
RunAsVirtualAccount = $true
```

<span data-ttu-id="5c98f-138">Ha a szerepköröket, a munkamenet-konfiguráció által támogatott nincs szükség ilyen széles körű jogosultságokat, igény szerint megadhatja a biztonsági csoportok, amelyhez a virtuális fiók fog tartozni.</span><span class="sxs-lookup"><span data-stu-id="5c98f-138">If the roles supported by the session configuration do not require such broad privileges, you can optionally specify the security groups to which the virtual account will belong.</span></span>
<span data-ttu-id="5c98f-139">Egy olyan tagkiszolgáló vagy a munkaállomáson a megadott biztonsági csoportokban helyi csoportok nem a tartományból kell lennie.</span><span class="sxs-lookup"><span data-stu-id="5c98f-139">On a member server or workstation, the specified security groups must be local groups, not groups from a domain.</span></span>

<span data-ttu-id="5c98f-140">Ha egy vagy több biztonsági csoport megadva, a virtuális fiók már nem fog tartozni a helyi vagy tartományi rendszergazdák csoportnak.</span><span class="sxs-lookup"><span data-stu-id="5c98f-140">When one or more security groups is specified, the virtual account will no longer belong to the local or domain administrators group.</span></span>

```powershell
# Setting the session to use a virtual account that only belongs to the NetworkOperator and NetworkAuditor local groups
RunAsVirtualAccount = $true
RunAsVirtualAccountGroups = 'NetworkOperator', 'NetworkAuditor'
```

> [!NOTE]
> <span data-ttu-id="5c98f-141">A virtuális fiókok ideiglenesen kapnak a bejelentkezés, a szolgáltatás közvetlenül a helyi kiszolgálói biztonsági házirendben.</span><span class="sxs-lookup"><span data-stu-id="5c98f-141">Virtual accounts are temporarily granted the Logon as a service right in the local server security policy.</span></span>  <span data-ttu-id="5c98f-142">Ha a megadott VirtualAccountGroups egyike már rendelkezik ezzel a jogosultsággal, a házirendben, az egyes virtuális fiók lesz többé nem hozzáadható és eltávolítható a szabályzat alól.</span><span class="sxs-lookup"><span data-stu-id="5c98f-142">If one of the VirtualAccountGroups specified has already been granted this right in the policy, the individual virtual account will no longer be added and removed from the policy.</span></span>  <span data-ttu-id="5c98f-143">Ez például tartományvezérlőkkel, ahol a tartományvezérlő biztonsági házirendjének felülvizsgálata szorosan naplóz esetekben hasznos lehet.</span><span class="sxs-lookup"><span data-stu-id="5c98f-143">This can be useful in scenarios such as domain controllers where revisions to the domain controller security policy are closely audited.</span></span>  <span data-ttu-id="5c98f-144">Ez a lehetőség csak a 2018 November rendelkező Windows Server 2016 vagy újabb kumulatív és a Windows Server 2019 a január 2019- vagy újabb kumulatív.</span><span class="sxs-lookup"><span data-stu-id="5c98f-144">This is only available in Windows Server 2016 with the November 2018 or later rollup and Windows Server 2019 with the January 2019 or later rollup.</span></span>

#### <a name="group-managed-service-account"></a><span data-ttu-id="5c98f-145">Csoportosan felügyelt szolgáltatásfiók</span><span class="sxs-lookup"><span data-stu-id="5c98f-145">Group Managed Service Account</span></span>


<span data-ttu-id="5c98f-146">A JEA-felhasználó, például a más webes szolgáltatásokat vagy hálózati erőforrások eléréséhez igénylő forgatókönyvek esetén a csoportosan felügyelt szolgáltatásfiók (gMSA) egy megfelelő identitás használatára.</span><span class="sxs-lookup"><span data-stu-id="5c98f-146">For scenarios requiring the JEA user to access network resources such as other machines or web services, a group managed service account (gMSA) is a more appropriate identity to use.</span></span>
<span data-ttu-id="5c98f-147">csoportosan felügyelt szolgáltatásfiók fiókok lehetővé teszik, egy tartományi identitás, amely hitelesíti a rendszer minden olyan gép, a tartományban lévő erőforrások használható.</span><span class="sxs-lookup"><span data-stu-id="5c98f-147">gMSA accounts give you a domain identity which can be used to authenticate against resources on any machine within the domain.</span></span>
<span data-ttu-id="5c98f-148">A jogosultságok a csoportosan felügyelt szolgáltatásfiók fiók lehetővé teszi azt határozza meg az erőforrások elérésére.</span><span class="sxs-lookup"><span data-stu-id="5c98f-148">The rights the gMSA account gives you is determined by the resources you are accessing.</span></span>
<span data-ttu-id="5c98f-149">Nem automatikusan fog rendszergazdai jogosultságok minden olyan gép vagy szolgáltatás, ha a gép vagy szolgáltatás-rendszergazda explicit módon megadta a csoportosan felügyelt szolgáltatásfiókok rendszergazdai jogosultságokat.</span><span class="sxs-lookup"><span data-stu-id="5c98f-149">You will not automatically have admin rights on any machines or services unless the machine/service administrator has explicitly granted the gMSA account admin privileges.</span></span>

```powershell
# Configure JEA sessions to use the gMSA account in the local computer's domain with the sAMAccountName of 'MyJEAgMSA'
GroupManagedServiceAccount = 'Domain\MyJEAgMSA'
```

<span data-ttu-id="5c98f-150">csoportosan felügyelt szolgáltatásfiók-fiókok csak használható amikor hálózati erőforrásokhoz való hozzáférés szükség néhány okok miatt:</span><span class="sxs-lookup"><span data-stu-id="5c98f-150">gMSA accounts should only be used when access to network resources are required for a few reasons:</span></span>

- <span data-ttu-id="5c98f-151">Ezért jóval nehezebb nyomon követését egy felhasználói műveletek csoportosan felügyelt szolgáltatásfiókok használatakor, mivel minden felhasználó megosztja a ugyanazon futtató identitását.</span><span class="sxs-lookup"><span data-stu-id="5c98f-151">It is harder to trace back actions to a user when using a gMSA account since every user shares the same run-as identity.</span></span> <span data-ttu-id="5c98f-152">Tekintse meg a PowerShell-munkamenet szövegekben és a naplók felhasználók korrelációját, ha azok a műveletek kell.</span><span class="sxs-lookup"><span data-stu-id="5c98f-152">You will need to consult PowerShell session transcripts and logs to correlate users with their actions.</span></span>

- <span data-ttu-id="5c98f-153">A csoportosan felügyelt szolgáltatásfiók férhetnek számos hálózati erőforrások, amelyek a kapcsolódó felhasználó nem kell a hozzáférést.</span><span class="sxs-lookup"><span data-stu-id="5c98f-153">The gMSA account may have access to many network resources which the connecting user does not need access to.</span></span> <span data-ttu-id="5c98f-154">Mindig próbálja hatályos engedélyek korlátozására, kövesse a legalacsonyabb jogosultsági szint elvének JEA munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="5c98f-154">Always try to limit effective permissions in a JEA session to follow the principle of least privilege.</span></span>

> [!NOTE]
> <span data-ttu-id="5c98f-155">A felügyelt szolgáltatásfiókok csoportot csak olyan elérhető Windows PowerShell 5.1-es vagy újabb és a tartományhoz csatlakoztatott gépeket.</span><span class="sxs-lookup"><span data-stu-id="5c98f-155">Group managed service accounts are only available in Windows PowerShell 5.1 or newer and on domain-joined machines.</span></span>

#### <a name="more-information-about-run-as-users"></a><span data-ttu-id="5c98f-156">További információ a futtató felhasználók</span><span class="sxs-lookup"><span data-stu-id="5c98f-156">More information about run as users</span></span>

<span data-ttu-id="5c98f-157">Az identitások, és hogyan azok többtényezős biztonsági állapotáról a JEA-munkamenet, futtassa kapcsolatos további információk találhatók a [biztonsági szempontok](security-considerations.md) cikk.</span><span class="sxs-lookup"><span data-stu-id="5c98f-157">Additional information about run as identities and how they factor into the security of a JEA session can be found in the [security considerations](security-considerations.md) article.</span></span>

### <a name="session-transcripts"></a><span data-ttu-id="5c98f-158">Munkamenet szövegekben</span><span class="sxs-lookup"><span data-stu-id="5c98f-158">Session transcripts</span></span>

<span data-ttu-id="5c98f-159">Javasoljuk, hogy konfigurálja-e a felhasználói munkamenetek automatikus rögzítése szövegekben JEA munkamenet konfigurációs fájlt.</span><span class="sxs-lookup"><span data-stu-id="5c98f-159">It is recommended that you configure a JEA session configuration file to automatically record transcripts of users' sessions.</span></span>
<span data-ttu-id="5c98f-160">PowerShell-munkamenet átiratok a csatlakozó felhasználó, a hozzájuk tartozó identitás futtató vonatkozó adatokat tartalmaznak, és a felhasználó által futtatott parancsok.</span><span class="sxs-lookup"><span data-stu-id="5c98f-160">PowerShell session transcripts contain information about the connecting user, the run as identity assigned to them, and the commands run by the user.</span></span>
<span data-ttu-id="5c98f-161">Egy naplózási csapat, akiknek meg kell ismernie, hogy ki hajtotta végre a rendszer egy adott módosítását hasznos lehet.</span><span class="sxs-lookup"><span data-stu-id="5c98f-161">They can be useful to an auditing team who needs to understand who performed a specific change to a system.</span></span>

<span data-ttu-id="5c98f-162">Automatikus beszédátírási konfigurálása a munkamenet-konfigurációs fájlban, hol szeretné tárolni az átiratok mappa elérési útjának megadását.</span><span class="sxs-lookup"><span data-stu-id="5c98f-162">To configure automatic transcription in the session configuration file, provide a path to a folder where the transcripts should be stored.</span></span>

```powershell
TranscriptDirectory = 'C:\ProgramData\JEAConfiguration\Transcripts'
```

<span data-ttu-id="5c98f-163">A megadott mappába kell konfigurálni, hogy a felhasználók módosítsák vagy töröljék a benne lévő adatokat.</span><span class="sxs-lookup"><span data-stu-id="5c98f-163">The specified folder should be configured to prevent users from modifying or deleting any data in it.</span></span>
<span data-ttu-id="5c98f-164">Szövegekben írja azt a mappát a helyi rendszer fiók, amelyhez szükség van az olvasási és írási hozzáférés a címtárhoz.</span><span class="sxs-lookup"><span data-stu-id="5c98f-164">Transcripts are written to the folder by the Local System account, which requires read and write access to the directory.</span></span>
<span data-ttu-id="5c98f-165">Általános jogú felhasználók nem rendelkezhetnek azt a mappát, és a egy korlátozott számú biztonsági rendszergazdák rendelkezhetnek hozzáféréssel az átiratok naplózása.</span><span class="sxs-lookup"><span data-stu-id="5c98f-165">Standard users should have no access to the folder, and a limited set of security administrators should have access to audit the transcripts.</span></span>

### <a name="user-drive"></a><span data-ttu-id="5c98f-166">Felhasználó-meghajtó</span><span class="sxs-lookup"><span data-stu-id="5c98f-166">User drive</span></span>

<span data-ttu-id="5c98f-167">Ha a csatlakozó felhasználók kell másolni a fájlok és-tárolókról a JEA-végpont annak érdekében, hogy a parancs futtatása, engedélyezheti a felhasználó meghajtó a munkamenet-konfigurációs fájlban.</span><span class="sxs-lookup"><span data-stu-id="5c98f-167">If your connecting users will need to copy files to/from the JEA endpoint in order to run a command, you can enable the user drive in the session configuration file.</span></span>
<span data-ttu-id="5c98f-168">A felhasználó meghajtó egy [PSDrive](https://msdn.microsoft.com/powershell/scripting/getting-started/cookbooks/managing-windows-powershell-drives) , amely az egyes csatlakozó felhasználók egyedi mappát van leképezve.</span><span class="sxs-lookup"><span data-stu-id="5c98f-168">The user drive is a [PSDrive](https://msdn.microsoft.com/powershell/scripting/getting-started/cookbooks/managing-windows-powershell-drives) that is mapped to a unique folder for each connecting user.</span></span>
<span data-ttu-id="5c98f-169">Ez a mappa szolgál egy szóközt, hogy másolja a fájlokat és-tárolókról a rendszer anélkül, hogy hozzáférést ad nekik a teljes fájlrendszerbe vagy a fájlrendszer-szolgáltatót is közzéteheti.</span><span class="sxs-lookup"><span data-stu-id="5c98f-169">This folder serves as a space for them to copy files to/from the system, without giving them access to the full file system or exposing the FileSystem provider.</span></span>
<span data-ttu-id="5c98f-170">A felhasználó meghajtó tartalma állandó befogadásához helyzetekben, ahol a hálózati kapcsolat megszakadhat a munkamenetek között.</span><span class="sxs-lookup"><span data-stu-id="5c98f-170">The user drive contents are persistent across sessions to accommodate situations where network connectivity may be interrupted.</span></span>

```powershell
MountUserDrive = $true
```

<span data-ttu-id="5c98f-171">Alapértelmezés szerint a felhasználó meghajtó lehetővé teszi felhasználónként 50 MB-ot legfeljebb tárolni.</span><span class="sxs-lookup"><span data-stu-id="5c98f-171">By default, the user drive allows you to store a maximum of 50MB of data per user.</span></span>
<span data-ttu-id="5c98f-172">Korlátozhatja a felhasználók használhatnak fel, az adatok mennyisége a *UserDriveMaximumSize* mező.</span><span class="sxs-lookup"><span data-stu-id="5c98f-172">You can limit the amount of data a user can consume with the *UserDriveMaximumSize* field.</span></span>

```powershell
# Enables the user drive with a per-user limit of 500MB (524288000 bytes)
MountUserDrive = $true
UserDriveMaximumSize = 524288000
```

<span data-ttu-id="5c98f-173">Ha nem szeretné, hogy a felhasználó meghajtón állandóként adatok, konfigurálhatja egy ütemezett feladatot a rendszer automatikusan törölni a mappát éjszakánként.</span><span class="sxs-lookup"><span data-stu-id="5c98f-173">If you do not want data in the user drive to be persistent, you can configure a scheduled task on the system to automatically clean up the folder every night.</span></span>

> [!NOTE]
> <span data-ttu-id="5c98f-174">A felhasználó meghajtó csak akkor érhető el a Windows PowerShell 5.1-es vagy újabb.</span><span class="sxs-lookup"><span data-stu-id="5c98f-174">The user drive is only available in Windows PowerShell 5.1 or newer.</span></span>

### <a name="role-definitions"></a><span data-ttu-id="5c98f-175">Szerepkör-definíciók</span><span class="sxs-lookup"><span data-stu-id="5c98f-175">Role definitions</span></span>

<span data-ttu-id="5c98f-176">A munkamenet-konfigurációs fájlban található szerepkör-definíciók megadása leképezése *felhasználók* való *szerepkörök*.</span><span class="sxs-lookup"><span data-stu-id="5c98f-176">Role definitions in a session configuration file define the mapping of *users* to *roles*.</span></span>
<span data-ttu-id="5c98f-177">Minden felhasználó vagy csoport szerepel ebben a mezőben automatikusan engedélyt kap a JEA-végpont, ha regisztrálva van.</span><span class="sxs-lookup"><span data-stu-id="5c98f-177">Every user or group included in this field will automatically be granted permission to the JEA endpoint when it is registered.</span></span>
<span data-ttu-id="5c98f-178">Minden felhasználó vagy csoport csak egyszer lehet része lesz a kulcs a kivonattábla kulcsa, de több szerepkört is rendelhető.</span><span class="sxs-lookup"><span data-stu-id="5c98f-178">Each user or group can be included as a key in the hashtable only once, but can be assigned multiple roles.</span></span>
<span data-ttu-id="5c98f-179">A szerepkör funkció a nevének kell lennie a szerepkör képesség .psrc fájlkiterjesztés nélkül fájl nevét.</span><span class="sxs-lookup"><span data-stu-id="5c98f-179">The name of the role capability should be the name of the role capability file, without the .psrc extension.</span></span>

```powershell
RoleDefinitions = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}
```

<span data-ttu-id="5c98f-180">Ha egy felhasználó tartozik a szerepkör-definíció egynél több csoportot, akkor az egyes szerepkörök hozzáférést fog kapni.</span><span class="sxs-lookup"><span data-stu-id="5c98f-180">If a user belongs to more than one group in the role definition, they will get access to the roles of each.</span></span>
<span data-ttu-id="5c98f-181">Ha két szerepkör ugyanazok a parancsmagok való hozzáférést, a legmegengedőbb paraméterkészletet a felhasználó fog kapni.</span><span class="sxs-lookup"><span data-stu-id="5c98f-181">If two roles grant access to the same cmdlets, the most permissive parameter set will be granted to the user.</span></span>

<span data-ttu-id="5c98f-182">Ha a szerepkör-definíciók mezőben adja meg a helyi felhasználókat és csoportokat, ügyeljen arra, hogy a számítógép nevét (nem *localhost* vagy *.*) a fordított perjel előtt.</span><span class="sxs-lookup"><span data-stu-id="5c98f-182">When specifying local users or groups in the role definitions field, be sure to use the computer name (not *localhost* or *.*) before the backslash.</span></span>
<span data-ttu-id="5c98f-183">A számítógépnév vizsgálatával ellenőrizheti a `$env:computername` változó.</span><span class="sxs-lookup"><span data-stu-id="5c98f-183">You can check the computer name by inspecting the `$env:computername` variable.</span></span>

```powershell
RoleDefinitions = @{
    'MyComputerName\MyLocalGroup' = @{ RoleCapabilities = 'DnsAuditor' }
}
```

### <a name="role-capability-search-order"></a><span data-ttu-id="5c98f-184">Szerepkör képesség keresési sorrendje</span><span class="sxs-lookup"><span data-stu-id="5c98f-184">Role capability search order</span></span>

<span data-ttu-id="5c98f-185">A fenti példa szerint szerepkörrel képességeket szerepkör képesség fájl egybesimított (fájlkiterjesztés nélkül fájlnév) nevére hivatkozik.</span><span class="sxs-lookup"><span data-stu-id="5c98f-185">As shown in the example above, role capabilities are referenced by the flat name (filename without the extension) of the role capability file.</span></span>
<span data-ttu-id="5c98f-186">A rendszer strukturálatlan ugyanazzal a névvel több szerepkörrel képességeket érhetők el, ha PowerShell használatával az implicit keresési sorrendje válassza ki a szerepkör hatékony képesség fájlt.</span><span class="sxs-lookup"><span data-stu-id="5c98f-186">If multiple role capabilities are available on the system with the same flat name, PowerShell will use its implicit search order to select the effective role capability file.</span></span>
<span data-ttu-id="5c98f-187">Akkor **nem** hozzáférést biztosít minden szerepkör képesség fájl ezzel a névvel.</span><span class="sxs-lookup"><span data-stu-id="5c98f-187">It will **not** give access to all role capability files with the same name.</span></span>

<span data-ttu-id="5c98f-188">Jea-t használ a `$env:PSModulePath` környezeti változót, mely szolgáltatást a szerepkör képesség fájlok elérési határozza meg.</span><span class="sxs-lookup"><span data-stu-id="5c98f-188">JEA uses the `$env:PSModulePath` environment variable to determine which paths to scan for role capability files.</span></span>
<span data-ttu-id="5c98f-189">Minden egyes adott elérési útján JEA keresni, amely tartalmaz egy "RoleCapabilities" almappát érvényes PowerShell-modulok.</span><span class="sxs-lookup"><span data-stu-id="5c98f-189">Within each of those paths, JEA will look for valid PowerShell modules that contain a "RoleCapabilities" subfolder.</span></span>
<span data-ttu-id="5c98f-190">Csakúgy, mint a modulok importálása a JEA szerepkörrel képességeket, az egyéni szerepkör képességekkel azonos nevű Windows-tal szállított részesíti előnyben.</span><span class="sxs-lookup"><span data-stu-id="5c98f-190">As with importing modules, JEA prefers role capabilities that are shipped with Windows to custom role capabilities with the same name.</span></span>
<span data-ttu-id="5c98f-191">Minden más elnevezési ütközések elsőbbséget Windows számba veszi a könyvtár (nem garantált, hogy betűrend) lévő fájlok sorrendje határozza meg.</span><span class="sxs-lookup"><span data-stu-id="5c98f-191">For all other naming conflicts, precedence is determined by the order in which Windows enumerates the files in the directory (not guaranteed to be alphabetically).</span></span>
<span data-ttu-id="5c98f-192">Az első szerepkör képesség fájl található, amely megfelel a kívánt név lesz a csatlakozó felhasználó.</span><span class="sxs-lookup"><span data-stu-id="5c98f-192">The first role capability file found that matches the desired name will be used for the connecting user.</span></span>

<span data-ttu-id="5c98f-193">Mivel a szerepkör képesség keresési sorrend nem determinisztikus, ha két vagy több szerepkörrel képességeket rendelkezik ugyanazzal a névvel, **erősen ajánlott** szerepkörrel képességeket egyedi nevük legyen a gépen biztosítása.</span><span class="sxs-lookup"><span data-stu-id="5c98f-193">Since the role capability search order is not deterministic when two or more role capabilities share the same name, it is **strongly recommended** that you ensure role capabilities have unique names on your machine.</span></span>

### <a name="conditional-access-rules"></a><span data-ttu-id="5c98f-194">Feltételes hozzáférési szabályok</span><span class="sxs-lookup"><span data-stu-id="5c98f-194">Conditional access rules</span></span>

<span data-ttu-id="5c98f-195">Minden felhasználó és csoport a RoleDefinitions mező automatikusan megkapja a JEA-végpont elérését.</span><span class="sxs-lookup"><span data-stu-id="5c98f-195">All users and groups included in the RoleDefinitions field are automatically granted access to JEA endpoints.</span></span>
<span data-ttu-id="5c98f-196">Feltételes hozzáférési szabályok lehetővé teszik, hogy finomíthatja a hozzáférést, és nincs hatással a szerepkörök, amelyek hozzá vannak rendelve, amely további biztonsági csoporthoz tartoznak, hogy a felhasználók.</span><span class="sxs-lookup"><span data-stu-id="5c98f-196">Conditional access rules allow you to refine this access and require users to belong to additional security groups which do not impact the roles which they are assigned.</span></span>
<span data-ttu-id="5c98f-197">Ez akkor lehet hasznos, ha szeretné integrálni "igény szerinti" emelt szintű hozzáférés felügyeleti megoldás, intelligens kártyás hitelesítés vagy más JEA többtényezős hitelesítési megoldást.</span><span class="sxs-lookup"><span data-stu-id="5c98f-197">This can be useful if you want to integrate a "just in time" privileged access management solution, smartcard authentication, or other multifactor authentication solution with JEA.</span></span>

<span data-ttu-id="5c98f-198">Feltételes hozzáférési szabályok a RequiredGroups mező egy munkamenet-konfigurációs fájlban vannak definiálva.</span><span class="sxs-lookup"><span data-stu-id="5c98f-198">Conditional access rules are defined in the RequiredGroups field in a session configuration file.</span></span>
<span data-ttu-id="5c98f-199">Itt adhat meg egy kivonattáblát (szükség esetén a beágyazott) használó "És" és "Vagy" kulcsok a szabályok létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="5c98f-199">There, you can provide a hashtable (optionally nested) that uses 'And' and 'Or' keys to construct your rules.</span></span>
<span data-ttu-id="5c98f-200">Íme néhány példa bemutatja, hogyan használhatja ezt a mezőt:</span><span class="sxs-lookup"><span data-stu-id="5c98f-200">Here are some examples of how to leverage this field:</span></span>

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
> <span data-ttu-id="5c98f-201">Feltételes hozzáférési szabályok csak olyan, a Windows PowerShell 5.1-es vagy újabb.</span><span class="sxs-lookup"><span data-stu-id="5c98f-201">Conditional access rules are only available in Windows PowerShell 5.1 or newer.</span></span>

### <a name="other-properties"></a><span data-ttu-id="5c98f-202">Egyéb tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="5c98f-202">Other properties</span></span>

<span data-ttu-id="5c98f-203">Munkamenet konfigurációs fájljainak minden szerepkör képesség fájl anélkül teheti meg, csak lehetővé teszi csatlakozó felhasználók hozzáférést biztosíthat más parancsok is megteheti.</span><span class="sxs-lookup"><span data-stu-id="5c98f-203">Session configuration files can also do everything a role capability file can do, just without the ability to give connecting users access to different commands.</span></span>
<span data-ttu-id="5c98f-204">Ha azt szeretné, hogy minden felhasználó hozzáférést adott parancsmagok, függvények és szolgáltatók, megteheti közvetlenül a a munkamenet-konfigurációs fájlt.</span><span class="sxs-lookup"><span data-stu-id="5c98f-204">If you want to allow all users access to specific cmdlets, functions, or providers, you can do so right in the session configuration file.</span></span>
<span data-ttu-id="5c98f-205">A támogatott tulajdonságok a munkamenet-konfigurációs fájl teljes listájának megtekintéséhez futtassa `Get-Help New-PSSessionConfigurationFile -Full`.</span><span class="sxs-lookup"><span data-stu-id="5c98f-205">For a full list of supported properties in the session configuration file, run `Get-Help New-PSSessionConfigurationFile -Full`.</span></span>

## <a name="testing-a-session-configuration-file"></a><span data-ttu-id="5c98f-206">Egy munkamenet-konfigurációs fájl tesztelése</span><span class="sxs-lookup"><span data-stu-id="5c98f-206">Testing a session configuration file</span></span>

<span data-ttu-id="5c98f-207">A munkamenet konfigurációja használatával tesztelhet a [Test-PSSessionConfigurationFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/test-pssessionconfigurationfile) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="5c98f-207">You can test a session configuration using the [Test-PSSessionConfigurationFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/test-pssessionconfigurationfile) cmdlet.</span></span>
<span data-ttu-id="5c98f-208">Erősen ajánlott, ha a manuális szövegszerkesztővel annak biztosítása érdekében, a szintaxis helyes FERB fájl szerkesztése tesztelje a munkamenet-konfigurációs fájlban.</span><span class="sxs-lookup"><span data-stu-id="5c98f-208">It is strongly recommended that you test your session configuration file if you have edited the pssc file manually using a text editor to ensure the syntax is correct.</span></span>
<span data-ttu-id="5c98f-209">Ha egy munkamenet-konfigurációs fájl nem felel meg a teszt, akkor nem fog hozzáférni sikerült regisztrálni a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="5c98f-209">If a session configuration file does not pass this test, it will not be able to be successfully registered on the system.</span></span>

## <a name="sample-session-configuration-file"></a><span data-ttu-id="5c98f-210">Minta munkamenet konfigurációs fájl</span><span class="sxs-lookup"><span data-stu-id="5c98f-210">Sample session configuration file</span></span>

<span data-ttu-id="5c98f-211">Alább egy teljes példát, hogyan hozhat létre, és a egy munkamenet-konfiguráció ellenőrzése a jea-t bemutató.</span><span class="sxs-lookup"><span data-stu-id="5c98f-211">Below is a complete example showing how to create and validate a session configuration for JEA.</span></span>
<span data-ttu-id="5c98f-212">Vegye figyelembe, hogy a szerepkör-definíciók létrehozása és tárolása a a `$roles` változó a kényelem és olvashatóság érdekében.</span><span class="sxs-lookup"><span data-stu-id="5c98f-212">Note that the role definitions are created and stored in the `$roles` variable for convenience and readability.</span></span>
<span data-ttu-id="5c98f-213">Már nem szükséges ehhez.</span><span class="sxs-lookup"><span data-stu-id="5c98f-213">It is not a requirement to do so.</span></span>

```powershell
$roles = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}

New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\JEAConfig.pssc -RunAsVirtualAccount -TranscriptDirectory 'C:\ProgramData\JEAConfiguration\Transcripts' -RoleDefinitions $roles -RequiredGroups @{ Or = '2FA-logon', 'smartcard-logon' }
Test-PSSessionConfigurationFile -Path .\JEAConfig.pssc # should yield True
```

## <a name="updating-session-configuration-files"></a><span data-ttu-id="5c98f-214">Munkamenet-konfigurációs fájlok frissítése</span><span class="sxs-lookup"><span data-stu-id="5c98f-214">Updating session configuration files</span></span>

<span data-ttu-id="5c98f-215">Ha szeretné módosítani egy JEA munkamenet-konfiguráció, beleértve a felhasználók szerepkörökhöz, a hozzárendelés tulajdonságait kell [regisztrációját](register-jea.md#unregistering-jea-configurations) és [újraregisztrálni](register-jea.md) a JEA munkamenet-konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="5c98f-215">If you need to change properties of a JEA session configuration, including the mapping of users to roles, you must [unregister](register-jea.md#unregistering-jea-configurations) and [re-register](register-jea.md) the JEA session configuration.</span></span>
<span data-ttu-id="5c98f-216">Regisztrálja újra a JEA munkamenet-konfigurációt, használja egy frissített PowerShell munkamenet konfigurációs fájlt, amely tartalmazza a szükséges módosításokat.</span><span class="sxs-lookup"><span data-stu-id="5c98f-216">When you re-register the JEA session configuration, use an updated PowerShell session configuration file that includes your desired changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c98f-217">További lépések</span><span class="sxs-lookup"><span data-stu-id="5c98f-217">Next steps</span></span>

- [<span data-ttu-id="5c98f-218">Regisztrálja a JEA-konfiguráció</span><span class="sxs-lookup"><span data-stu-id="5c98f-218">Register a JEA configuration</span></span>](register-jea.md)
- [<span data-ttu-id="5c98f-219">Szerző JEA szerepkörök</span><span class="sxs-lookup"><span data-stu-id="5c98f-219">Author JEA roles</span></span>](role-capabilities.md)
