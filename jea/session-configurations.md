---
ms.date: 06/12/2017
author: rpsqrd
ms.topic: conceptual
keywords: jea, a powershell, a biztonsági
title: JEA Session Configurations
ms.openlocfilehash: 317a549ed20b5800d5bafdabd266e93ba7cd321c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="jea-session-configurations"></a><span data-ttu-id="0549b-103">JEA Session Configurations</span><span class="sxs-lookup"><span data-stu-id="0549b-103">JEA Session Configurations</span></span>

> <span data-ttu-id="0549b-104">A következőkre vonatkozik: a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="0549b-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="0549b-105">A JEA végpont rendszerre hoz létre, és regisztrálja egy PowerShell-munkamenet konfigurációs fájl egy egyedi módon regisztrálva van.</span><span class="sxs-lookup"><span data-stu-id="0549b-105">A JEA endpoint is registered on a system by creating and registering a PowerShell session configuration file in a specific way.</span></span>
<span data-ttu-id="0549b-106">Munkamenet-konfigurációk meghatározásához *ki* használhatja a JEA végpontot, és melyik szerepkör(ök) rendelkeznek hozzáféréssel.</span><span class="sxs-lookup"><span data-stu-id="0549b-106">Session configurations determine *who* can use the JEA endpoint, and which role(s) they will have access to.</span></span>
<span data-ttu-id="0549b-107">Szintén definiálnia globális beállítások felhasználói szerepköröket a JEA-munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="0549b-107">They also define global settings that apply to users of any role in the JEA session.</span></span>

<span data-ttu-id="0549b-108">Ez a témakör ismerteti, hogyan hozzon létre egy PowerShell-munkamenet konfigurációs fájlt, és a JEA végpontjának regisztrálása.</span><span class="sxs-lookup"><span data-stu-id="0549b-108">This topic describes how to create a PowerShell session configuration file and register a JEA endpoint.</span></span>

## <a name="create-a-session-configuration-file"></a><span data-ttu-id="0549b-109">Egy munkamenet-konfigurációs fájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="0549b-109">Create a session configuration file</span></span>

<span data-ttu-id="0549b-110">Ahhoz, hogy a JEA végpontjának regisztrálása, meg kell adnia, hogyan kell konfigurálni, hogy a végpont.</span><span class="sxs-lookup"><span data-stu-id="0549b-110">In order to register a JEA endpoint, you need to specify how that endpoint should be configured.</span></span>
<span data-ttu-id="0549b-111">Nincsenek a kell figyelembe venni, a legfontosabb mely, amely nem a JEA végpont hozzáféréssel rendelkező, mely szerepköröket fogják számos lehetőségük van hozzárendelve, mely identitás JEA használja a színfalak, és mi lesz a JEA végpont nevét.</span><span class="sxs-lookup"><span data-stu-id="0549b-111">There are many options to consider here, the most important of which being who should have access to the JEA endpoint, which roles will they be assigned, which identity will JEA use under the covers, and what will be the name of the JEA endpoint.</span></span>
<span data-ttu-id="0549b-112">Ezek az összes meghatározása a PowerShell munkamenetben konfigurációs fájlt, amely PowerShell adatfájlt befejezi .pssc kiterjesztéssel.</span><span class="sxs-lookup"><span data-stu-id="0549b-112">These are all defined in a PowerShell session configuration file, which is a PowerShell data file ending with a .pssc extension.</span></span>

<span data-ttu-id="0549b-113">A JEA végpontokhoz üres munkamenet konfigurációs fájl létrehozásához futtassa a következő parancsot.</span><span class="sxs-lookup"><span data-stu-id="0549b-113">To create a skeleton session configuration file for JEA endpoints, run the following command.</span></span>

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\MyJEAEndpoint.pssc
```

> [!TIP]
> <span data-ttu-id="0549b-114">A leggyakoribb konfigurációs beállítások szerepelnek a üres fájl alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="0549b-114">Only the most common configuration options are included in the skeleton file by default.</span></span>
> <span data-ttu-id="0549b-115">Használja a `-Full` kapcsolót, hogy az összes alkalmazható beállításait adja meg a létrehozott FERB.</span><span class="sxs-lookup"><span data-stu-id="0549b-115">Use the `-Full` switch to include all applicable settings in the generated PSSC.</span></span>

<span data-ttu-id="0549b-116">Szövegszerkesztőben nyissa meg a munkamenet-konfigurációs fájlt.</span><span class="sxs-lookup"><span data-stu-id="0549b-116">You can open the session configuration file in any text editor.</span></span>
<span data-ttu-id="0549b-117">A `-SessionType RestrictedRemoteServer` mező jelzi, hogy a munkamenet-konfiguráció által használandó JEA biztonságos kezelésére.</span><span class="sxs-lookup"><span data-stu-id="0549b-117">The `-SessionType RestrictedRemoteServer` field indicates that the session configuration will be used by JEA for secure management.</span></span>
<span data-ttu-id="0549b-118">Munkamenetet konfigurálta így fog működni [NoLanguage mód](https://technet.microsoft.com/library/dn433292.aspx) , és csak a következő 8 alapértelmezett parancsokat (és aliasok) érhető el:</span><span class="sxs-lookup"><span data-stu-id="0549b-118">Sessions configured this way will operate in [NoLanguage mode](https://technet.microsoft.com/library/dn433292.aspx) and only have the following 8 default commands (and aliases) available:</span></span>

- <span data-ttu-id="0549b-119">Törölje az állomás (cls, törölje a jelet)</span><span class="sxs-lookup"><span data-stu-id="0549b-119">Clear-Host (cls, clear)</span></span>
- <span data-ttu-id="0549b-120">Kilépés-PSSession (exsn, kilépési)</span><span class="sxs-lookup"><span data-stu-id="0549b-120">Exit-PSSession (exsn, exit)</span></span>
- <span data-ttu-id="0549b-121">Get-Command (gcm)</span><span class="sxs-lookup"><span data-stu-id="0549b-121">Get-Command (gcm)</span></span>
- <span data-ttu-id="0549b-122">Get-FormatData</span><span class="sxs-lookup"><span data-stu-id="0549b-122">Get-FormatData</span></span>
- <span data-ttu-id="0549b-123">Get-Help</span><span class="sxs-lookup"><span data-stu-id="0549b-123">Get-Help</span></span>
- <span data-ttu-id="0549b-124">Mértékobjektumot (mérték)</span><span class="sxs-lookup"><span data-stu-id="0549b-124">Measure-Object (measure)</span></span>
- <span data-ttu-id="0549b-125">Kimenő alapértelmezett</span><span class="sxs-lookup"><span data-stu-id="0549b-125">Out-Default</span></span>
- <span data-ttu-id="0549b-126">Select-Object (kijelölés)</span><span class="sxs-lookup"><span data-stu-id="0549b-126">Select-Object (select)</span></span>

<span data-ttu-id="0549b-127">Nincs PowerShell szolgáltató elérhető, sem pedig a bármely külső programokat (végrehajtható fájlok, parancsfájlok stb.).</span><span class="sxs-lookup"><span data-stu-id="0549b-127">No PowerShell providers are available, nor are any external programs (executables, scripts, etc.).</span></span>

<span data-ttu-id="0549b-128">A JEA munkamenet konfigurálása érdemes több más területen is.</span><span class="sxs-lookup"><span data-stu-id="0549b-128">There are several other fields you will want to configure for the JEA session.</span></span>
<span data-ttu-id="0549b-129">Azok a következő szakaszok ismertetnek.</span><span class="sxs-lookup"><span data-stu-id="0549b-129">They are covered in the following sections.</span></span>

### <a name="choose-the-jea-identity"></a><span data-ttu-id="0549b-130">Válassza ki a JEA identitás</span><span class="sxs-lookup"><span data-stu-id="0549b-130">Choose the JEA identity</span></span>

<span data-ttu-id="0549b-131">A háttérben JEA kell a csatlakoztatott felhasználói parancsok futtatásakor identitás (fiók).</span><span class="sxs-lookup"><span data-stu-id="0549b-131">Behind the scenes, JEA needs an identity (account) to use when running a connected user's commands.</span></span>
<span data-ttu-id="0549b-132">Eldöntheti, melyik identitás JEA fogja használni a munkamenet-konfigurációs fájlban.</span><span class="sxs-lookup"><span data-stu-id="0549b-132">You decide which identity JEA will use in the session configuration file.</span></span>

#### <a name="local-virtual-account"></a><span data-ttu-id="0549b-133">Helyi virtuális fiók</span><span class="sxs-lookup"><span data-stu-id="0549b-133">Local Virtual Account</span></span>

<span data-ttu-id="0549b-134">Ha a szerepköröket, a JEA végpont által támogatott összes használatával kezelheti a helyi számítógépen, és egy helyi rendszergazdai fiók elegendő ahhoz, hogy a parancsok sikeresen futtatni, konfigurálnia kell a JEA egy helyi virtuális fiók használatára.</span><span class="sxs-lookup"><span data-stu-id="0549b-134">If the roles supported by this JEA endpoint are all used to manage the local machine, and a local administrator account is sufficient to run the commands succesfully, you should configure JEA to use a local virtual account.</span></span>
<span data-ttu-id="0549b-135">A virtuális fiókok ideiglenes fiókot, amely egy adott felhasználónak egyedi és a PowerShell-munkamenetet időtartama csak az utolsó olyan.</span><span class="sxs-lookup"><span data-stu-id="0549b-135">Virtual accounts are temporary accounts that are unique to a specific user and only last for the duration of their PowerShell session.</span></span>
<span data-ttu-id="0549b-136">Egy tagkiszolgáló vagy munkaállomás virtuális fiókok tartoznak a helyi számítógép **rendszergazdák** csoportot, és a legtöbb rendszer erőforrások elérésére.</span><span class="sxs-lookup"><span data-stu-id="0549b-136">On a member server or workstation, virtual accounts belong to the local computer's **Administrators** group, and have access to most system resources.</span></span>
<span data-ttu-id="0549b-137">Az Active Directory tartományvezérlőn lévő virtuális fiókokat a tartományhoz tartoznak **Tartománygazdák** csoport.</span><span class="sxs-lookup"><span data-stu-id="0549b-137">On an Active Directory Domain Controller, virtual accounts belong to the domain's **Domain Admins** group.</span></span>

```powershell
# Setting the session to use a virtual account
RunAsVirtualAccount = $true
```

<span data-ttu-id="0549b-138">Ha a szerepköröket, a munkamenet-konfiguráció által támogatott nincs szükség ilyen széles körű jogosultsággal, opcionálisan megadhat a biztonsági csoportokat, amelyhez a virtuális fiók fog tartozni.</span><span class="sxs-lookup"><span data-stu-id="0549b-138">If the roles supported by the session configuration do not require such broad privileges, you can optionally specify the security groups to which the virtual account will belong.</span></span>
<span data-ttu-id="0549b-139">Egy olyan tagkiszolgáló vagy munkaállomáson a megadott biztonsági csoportokban helyi csoportok nem a tartományból kell lennie.</span><span class="sxs-lookup"><span data-stu-id="0549b-139">On a member server or workstation, the specified security groups must be local groups, not groups from a domain.</span></span>

<span data-ttu-id="0549b-140">Ha meg van határozva egy vagy több biztonsági csoportot, a virtuális fiók már nem fog tartozni a helyi vagy tartományi rendszergazdák csoportnak.</span><span class="sxs-lookup"><span data-stu-id="0549b-140">When one or more security groups is specified, the virtual account will no longer belong to the local or domain administrators group.</span></span>

```powershell
# Setting the session to use a virtual account that only belongs to the NetworkOperator and NetworkAuditor local groups
RunAsVirtualAccount = $true
RunAsVirtualAccountGroups = 'NetworkOperator', 'NetworkAuditor'
```

#### <a name="group-managed-service-account"></a><span data-ttu-id="0549b-141">Csoportosan felügyelt szolgáltatásfiók</span><span class="sxs-lookup"><span data-stu-id="0549b-141">Group Managed Service Account</span></span>


<span data-ttu-id="0549b-142">A JEA felhasználói hozzáférést hálózati erőforrások, például más gépek vagy webes szolgáltatásokból igénylő forgatókönyvek esetén a csoportosan felügyelt szolgáltatásfiókjait (gMSA) egy megfelelő identitás használatára.</span><span class="sxs-lookup"><span data-stu-id="0549b-142">For scenarios requiring the JEA user to access network resources such as other machines or web services, a group managed service account (gMSA) is a more appropriate identity to use.</span></span>
<span data-ttu-id="0549b-143">csoportosan felügyelt szolgáltatásfiók fiókok biztosítják a tartomány identitása bármelyik olyan gépen a tartományon belüli erőforrásokon hitelesítéséhez használható.</span><span class="sxs-lookup"><span data-stu-id="0549b-143">gMSA accounts give you a domain identity which can be used to authenticate against resources on any machine within the domain.</span></span>
<span data-ttu-id="0549b-144">A jogosultságok a csoportosan felügyelt szolgáltatásfiók biztosít azt határozza meg az erőforrások elérésére.</span><span class="sxs-lookup"><span data-stu-id="0549b-144">The rights the gMSA account gives you is determined by the resources you are accessing.</span></span>
<span data-ttu-id="0549b-145">Nem automatikusan fog rendszergazdai jogosultságai a gépeket vagy szolgáltatásokat kivéve, ha a számítógép vagy szolgáltatás-rendszergazda explicit módon megadta a csoportosan felügyelt szolgáltatásfiókok rendszergazdai jogosultságokkal.</span><span class="sxs-lookup"><span data-stu-id="0549b-145">You will not automatically have admin rights on any machines or services unless the machine/service administrator has explicitly granted the gMSA account admin privileges.</span></span>

```powershell
# Configure JEA sessions to use the gMSA account in the local computer's domain with the sAMAccountName of 'MyJEAgMSA'
GroupManagedServiceAccount = 'Domain\MyJEAgMSA'
```

<span data-ttu-id="0549b-146">csoportosan felügyelt szolgáltatásfiók fiókok csak akkor használja, ha hálózati erőforrások eléréséhez szükség néhány lehetnek az okai:</span><span class="sxs-lookup"><span data-stu-id="0549b-146">gMSA accounts should only be used when access to network resources are required for a few reasons:</span></span>

- <span data-ttu-id="0549b-147">Nyomon követését műveletek egy felhasználó számára a csoportosan felügyelt szolgáltatásfiók használata, mivel minden felhasználó közösen használja az ugyanazon futtató identitás nehezebb.</span><span class="sxs-lookup"><span data-stu-id="0549b-147">It is harder to trace back actions to a user when using a gMSA account since every user shares the same run-as identity.</span></span> <span data-ttu-id="0549b-148">Szüksége lesz a további részleteket a PowerShell-munkamenethez ki és a naplók felhasználók összefüggéseket azok a műveletek.</span><span class="sxs-lookup"><span data-stu-id="0549b-148">You will need to consult PowerShell session transcripts and logs to correlate users with their actions.</span></span>

- <span data-ttu-id="0549b-149">A csoportosan felügyelt szolgáltatásfiók hozzáférhetett számos hálózati erőforrások, amelyek a csatlakozó felhasználó nem kell a hozzáférést.</span><span class="sxs-lookup"><span data-stu-id="0549b-149">The gMSA account may have access to many network resources which the connecting user does not need access to.</span></span> <span data-ttu-id="0549b-150">Mindig próbálja hatályos engedélyek korlátozása egy JEA munkamenet hajtsa végre a legalacsonyabb jogosultsági szint elvét.</span><span class="sxs-lookup"><span data-stu-id="0549b-150">Always try to limit effective permissions in a JEA session to follow the principle of least privilege.</span></span>

> [!NOTE]
> <span data-ttu-id="0549b-151">Csoportosan felügyelt szolgáltatásfiókok csak rendelkezésre állnak a Windows PowerShell 5.1 vagy újabb és a tartományhoz csatlakoztatott számítógépeken.</span><span class="sxs-lookup"><span data-stu-id="0549b-151">Group managed service accounts are only available in Windows PowerShell 5.1 or newer and on domain-joined machines.</span></span>


#### <a name="more-information-about-run-as-users"></a><span data-ttu-id="0549b-152">További információ a futtató felhasználók</span><span class="sxs-lookup"><span data-stu-id="0549b-152">More information about run as users</span></span>

<span data-ttu-id="0549b-153">Identitások és hogyan azok tényező be a biztonsági munkamenet JEA futtató további információt megtalálhatók a [biztonsági szempontok](security-considerations.md) cikk.</span><span class="sxs-lookup"><span data-stu-id="0549b-153">Additional information about run as identities and how they factor into the security of a JEA session can be found in the [security considerations](security-considerations.md) article.</span></span>

### <a name="session-transcripts"></a><span data-ttu-id="0549b-154">Munkamenet ki</span><span class="sxs-lookup"><span data-stu-id="0549b-154">Session transcripts</span></span>

<span data-ttu-id="0549b-155">Javasoljuk, hogy konfigurálja a felhasználói munkamenetek automatikus rögzítése átiratai JEA munkamenet konfigurációs fájlt.</span><span class="sxs-lookup"><span data-stu-id="0549b-155">It is recommended that you configure a JEA session configuration file to automatically record transcripts of users' sessions.</span></span>
<span data-ttu-id="0549b-156">PowerShell-munkamenethez ki a csatlakozó felhasználó, a hozzájuk tartozó identitás futtató információkat tartalmaznak, és a felhasználó által futtatott parancsok.</span><span class="sxs-lookup"><span data-stu-id="0549b-156">PowerShell session transcripts contain information about the connecting user, the run as identity assigned to them, and the commands run by the user.</span></span>
<span data-ttu-id="0549b-157">Akkor lehet hasznos, ha szeretné tudni végző felhasználók listáját egy adott módosítását a rendszer egy naplózási csoportnak.</span><span class="sxs-lookup"><span data-stu-id="0549b-157">They can be useful to an auditing team who needs to understand who performed a specific change to a system.</span></span>

<span data-ttu-id="0549b-158">Automatikus írjanak elő konfigurálása a munkamenet-konfigurációs fájlban, adja meg a mappa elérési útja a ki kell tárolásához.</span><span class="sxs-lookup"><span data-stu-id="0549b-158">To configure automatic transcription in the session configuration file, provide a path to a folder where the transcripts should be stored.</span></span>

```powershell
TranscriptDirectory = 'C:\ProgramData\JEAConfiguration\Transcripts'
```

<span data-ttu-id="0549b-159">A megadott mappába kell konfigurálni, hogy a felhasználók a módosítsa vagy törölje az összes adatot.</span><span class="sxs-lookup"><span data-stu-id="0549b-159">The specified folder should be configured to prevent users from modifying or deleting any data in it.</span></span>
<span data-ttu-id="0549b-160">Ki a mappát a helyi rendszer fiók, amelyhez olvasási és írási hozzáféréssel a könyvtárhoz rögzíti.</span><span class="sxs-lookup"><span data-stu-id="0549b-160">Transcripts are written to the folder by the Local System account, which requires read and write access to the directory.</span></span>
<span data-ttu-id="0549b-161">Az általános jogú felhasználók nem hozzáféréssel kell rendelkeznie a mappához, és biztonsági rendszergazdák korlátozott számú naplózási a ki hozzáféréssel kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="0549b-161">Standard users should have no access to the folder, and a limited set of security administrators should have access to audit the transcripts.</span></span>

### <a name="user-drive"></a><span data-ttu-id="0549b-162">Felhasználói meghajtó</span><span class="sxs-lookup"><span data-stu-id="0549b-162">User drive</span></span>

<span data-ttu-id="0549b-163">Ha a csatlakozó felhasználók kell másolnia a fájlokat a JEA végpont és a parancs futtatásához, engedélyezheti a felhasználói meghajtó a munkamenet-konfigurációs fájlban.</span><span class="sxs-lookup"><span data-stu-id="0549b-163">If your connecting users will need to copy files to/from the JEA endpoint in order to run a command, you can enable the user drive in the session configuration file.</span></span>
<span data-ttu-id="0549b-164">A felhasználó meghajtó egy [PSDrive](https://msdn.microsoft.com/powershell/scripting/getting-started/cookbooks/managing-windows-powershell-drives) , amely egy egyedi mappát az egyes csatlakozó felhasználó van leképezve.</span><span class="sxs-lookup"><span data-stu-id="0549b-164">The user drive is a [PSDrive](https://msdn.microsoft.com/powershell/scripting/getting-started/cookbooks/managing-windows-powershell-drives) that is mapped to a unique folder for each connecting user.</span></span>
<span data-ttu-id="0549b-165">Ez a mappa adhatja őket a rendszer, és a fájlok adjon hozzáférést a teljes fájlrendszer vagy a fájlrendszer szolgáltató kitettségének nélkül történő másolását funkcionál.</span><span class="sxs-lookup"><span data-stu-id="0549b-165">This folder serves as a space for them to copy files to/from the system, without giving them access to the full file system or exposing the FileSystem provider.</span></span>
<span data-ttu-id="0549b-166">A felhasználó meghajtó tartalma állandó olyan helyzetekben, ahol lehet megszakítani hálózati kapcsolat munkamenetei között.</span><span class="sxs-lookup"><span data-stu-id="0549b-166">The user drive contents are persistent across sessions to accommodate situations where network connectivity may be interrupted.</span></span>

```powershell
MountUserDrive = $true
```

<span data-ttu-id="0549b-167">Alapértelmezés szerint a felhasználói meghajtó teszi legfeljebb 50MB / felhasználói adatok tárolásához.</span><span class="sxs-lookup"><span data-stu-id="0549b-167">By default, the user drive allows you to store a maximum of 50MB of data per user.</span></span>
<span data-ttu-id="0549b-168">A felhasználó felhasználhat az adatok mennyisége korlátozhatja a *UserDriveMaximumSize* mező.</span><span class="sxs-lookup"><span data-stu-id="0549b-168">You can limit the amount of data a user can consume with the *UserDriveMaximumSize* field.</span></span>

```powershell
# Enables the user drive with a per-user limit of 500MB (524288000 bytes)
MountUserDrive = $true
UserDriveMaximumSize = 524288000
```

<span data-ttu-id="0549b-169">Ha nem szeretné, hogy a felhasználó meghajtó legyen állandó adatokat, konfigurálhatja egy ütemezett feladatot a rendszer automatikusan a mappa karbantartása éjszakánként.</span><span class="sxs-lookup"><span data-stu-id="0549b-169">If you do not want data in the user drive to be persistent, you can configure a scheduled task on the system to automatically clean up the folder every night.</span></span>

> [!NOTE]
> <span data-ttu-id="0549b-170">A felhasználó meghajtó csak a Windows PowerShell 5.1-es vagy újabb.</span><span class="sxs-lookup"><span data-stu-id="0549b-170">The user drive is only available in Windows PowerShell 5.1 or newer.</span></span>

### <a name="role-definitions"></a><span data-ttu-id="0549b-171">Szerepkör-definíciók</span><span class="sxs-lookup"><span data-stu-id="0549b-171">Role definitions</span></span>

<span data-ttu-id="0549b-172">A munkamenet-konfigurációs fájlban található szerepkör-definíciók megadása leképezése *felhasználók* való *szerepkörök*.</span><span class="sxs-lookup"><span data-stu-id="0549b-172">Role definitions in a session configuration file define the mapping of *users* to *roles*.</span></span>
<span data-ttu-id="0549b-173">Minden felhasználó vagy csoport szerepel ebben a mezőben automatikusan engedélyt kap a JEA végponthoz való regisztrálásakor kerül.</span><span class="sxs-lookup"><span data-stu-id="0549b-173">Every user or group included in this field will automatically be granted permission to the JEA endpoint when it is registered.</span></span>
<span data-ttu-id="0549b-174">Minden felhasználó vagy csoport is meg lehet adni a kivonattábla kulcsként csak egyszer, de több szerepkörhöz is hozzárendelhető.</span><span class="sxs-lookup"><span data-stu-id="0549b-174">Each user or group can be included as a key in the hashtable only once, but can be assigned multiple roles.</span></span>
<span data-ttu-id="0549b-175">A szerepkör funkció nevét kell lennie a szerepkör funkció .psrc kiterjesztés nélküli fájl nevét.</span><span class="sxs-lookup"><span data-stu-id="0549b-175">The name of the role capability should be the name of the role capability file, without the .psrc extension.</span></span>

```powershell
RoleDefinitions = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}
```

<span data-ttu-id="0549b-176">Ha egy felhasználó több csoporthoz a szerepkör-definíció tartozik, az egyes szerepkörök elérésére fogja használni.</span><span class="sxs-lookup"><span data-stu-id="0549b-176">If a user belongs to more than one group in the role definition, they will get access to the roles of each.</span></span>
<span data-ttu-id="0549b-177">Ha két szerepkörök ugyanazon parancsmagok hozzáférést, a leghatékonyabb paraméterkészletet alakítanak kapnak a felhasználó számára.</span><span class="sxs-lookup"><span data-stu-id="0549b-177">If two roles grant access to the same cmdlets, the most permissive parameter set will be granted to the user.</span></span>

<span data-ttu-id="0549b-178">Ha a szerepkör-definíciók mezőben adja meg a helyi felhasználókat és csoportokat, ügyeljen arra, hogy a számítógépnév (nem *localhost* vagy *.*) a fordított perjel előtt.</span><span class="sxs-lookup"><span data-stu-id="0549b-178">When specifying local users or groups in the role definitions field, be sure to use the computer name (not *localhost* or *.*) before the backslash.</span></span>
<span data-ttu-id="0549b-179">A számítógépnév vizsgálatával ellenőrizheti a `$env:computername` változó.</span><span class="sxs-lookup"><span data-stu-id="0549b-179">You can check the computer name by inspecting the `$env:computername` variable.</span></span>

```powershell
RoleDefinitions = @{
    'MyComputerName\MyLocalGroup' = @{ RoleCapabilities = 'DnsAuditor' }
}
```

### <a name="role-capability-search-order"></a><span data-ttu-id="0549b-180">Szerepkör funkció keresési sorrendje</span><span class="sxs-lookup"><span data-stu-id="0549b-180">Role capability search order</span></span>
<span data-ttu-id="0549b-181">Látható a fenti példában, szerepkör-képességek a szerepkör funkció fájl egyszerű név (fájlnév-kiterjesztés nélküli) által hivatkozott.</span><span class="sxs-lookup"><span data-stu-id="0549b-181">As shown in the example above, role capabilities are referenced by the flat name (filename without the extension) of the role capability file.</span></span>
<span data-ttu-id="0549b-182">Ha több szerepkör képességek érhetők el a rendszer a strukturálatlan néven, a PowerShell használata a az implicit keresési sorrendje válassza ki a hatékony szerepkör funkció fájlt.</span><span class="sxs-lookup"><span data-stu-id="0549b-182">If multiple role capabilities are available on the system with the same flat name, PowerShell will use its implicit search order to select the effective role capability file.</span></span>
<span data-ttu-id="0549b-183">A következőket hajtja végre **nem** hozzáférést szerepkör funkció fájlokhoz ugyanazzal a névvel.</span><span class="sxs-lookup"><span data-stu-id="0549b-183">It will **not** give access to all role capability files with the same name.</span></span>

<span data-ttu-id="0549b-184">JEA használja a `$env:PSModulePath` környezeti változó határozza meg, mely elérési szerepkör funkció fájlok vizsgálatára.</span><span class="sxs-lookup"><span data-stu-id="0549b-184">JEA uses the `$env:PSModulePath` environment variable to determine which paths to scan for role capability files.</span></span>
<span data-ttu-id="0549b-185">Minden egyes adott elérési útján JEA keresni, amely tartalmaz egy "RoleCapabilities" almappát érvényes PowerShell-modulok.</span><span class="sxs-lookup"><span data-stu-id="0549b-185">Within each of those paths, JEA will look for valid PowerShell modules that contain a "RoleCapabilities" subfolder.</span></span>
<span data-ttu-id="0549b-186">Csakúgy, mint a modulok importálása, JEA inkább szerepkör képességeket kínál, amelyek a Windows ilyen nevű egyéni szerepkör-funkciókat.</span><span class="sxs-lookup"><span data-stu-id="0549b-186">As with importing modules, JEA prefers role capabilities that are shipped with Windows to custom role capabilities with the same name.</span></span>
<span data-ttu-id="0549b-187">Az összes többi mappaelnevezési ütközéseket sorrend Windows számba veszi a könyvtár (nem garantált betűrendben) sorrendje határozza meg.</span><span class="sxs-lookup"><span data-stu-id="0549b-187">For all other naming conflicts, precedence is determined by the order in which Windows enumerates the files in the directory (not guaranteed to be alphabetically).</span></span>
<span data-ttu-id="0549b-188">Az első szerepkör funkció fájl található, amely megfelel a kívánt nevet fogja használni a csatlakozó felhasználó.</span><span class="sxs-lookup"><span data-stu-id="0549b-188">The first role capability file found that matches the desired name will be used for the connecting user.</span></span>

<span data-ttu-id="0549b-189">Mivel a szerepkör funkció keresési sorrendje nem determinisztikus, amikor két vagy több szerepkör képességek megosztása azonos nevű, **erősen ajánlott** szerepkör képességek egyedi nevük legyen a számítógépen biztosítása.</span><span class="sxs-lookup"><span data-stu-id="0549b-189">Since the role capability search order is not deterministic when two or more role capabilities share the same name, it is **strongly recommended** that you ensure role capabilities have unique names on your machine.</span></span>

### <a name="conditional-access-rules"></a><span data-ttu-id="0549b-190">Feltételes hozzáférési szabályai</span><span class="sxs-lookup"><span data-stu-id="0549b-190">Conditional access rules</span></span>

<span data-ttu-id="0549b-191">Összes felhasználók és csoportok a RoleDefinitions mező automatikusan JEA végpontokkal való hozzáférést kapnak.</span><span class="sxs-lookup"><span data-stu-id="0549b-191">All users and groups included in the RoleDefinitions field are automatically granted access to JEA endpoints.</span></span>
<span data-ttu-id="0549b-192">Feltételes hozzáférési szabályok lehetővé teszik finomíthatja a hozzáférés, és további biztonsági csoportokat, amelyek nem érintik a szerepkörök, amelyek a hozzárendelés tartozik, a felhasználóknak.</span><span class="sxs-lookup"><span data-stu-id="0549b-192">Conditional access rules allow you to refine this access and require users to belong to additional security groups which do not impact the roles which they are assigned.</span></span>
<span data-ttu-id="0549b-193">Ez akkor lehet hasznos, ha szeretné integrálni "csak az idő" emelt szintű hozzáférés felügyeleti megoldás, intelligens kártyás hitelesítés vagy más JEA többtényezős hitelesítés megoldást.</span><span class="sxs-lookup"><span data-stu-id="0549b-193">This can be useful if you want to integrate a "just in time" privileged access management solution, smartcard authentication, or other multifactor authentication solution with JEA.</span></span>

<span data-ttu-id="0549b-194">Feltételes hozzáférési szabályok vannak meghatározva, a RequiredGroups mezőben egy munkamenet-konfigurációs fájlban.</span><span class="sxs-lookup"><span data-stu-id="0549b-194">Conditional access rules are defined in the RequiredGroups field in a session configuration file.</span></span>
<span data-ttu-id="0549b-195">Itt megadhatja egy kivonattáblát (ha szükséges a beágyazott) használó "És" és "Vagy" kulcsok készítse el szabályait.</span><span class="sxs-lookup"><span data-stu-id="0549b-195">There, you can provide a hashtable (optionally nested) that uses 'And' and 'Or' keys to construct your rules.</span></span>
<span data-ttu-id="0549b-196">Íme néhány példa bemutatja, hogyan használhatók ki ebben a mezőben:</span><span class="sxs-lookup"><span data-stu-id="0549b-196">Here are some examples of how to leverage this field:</span></span>

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
> <span data-ttu-id="0549b-197">Feltételes hozzáférési szabályok csak olyan, a Windows PowerShell 5.1-es vagy újabb.</span><span class="sxs-lookup"><span data-stu-id="0549b-197">Conditional access rules are only available in Windows PowerShell 5.1 or newer.</span></span>

### <a name="other-properties"></a><span data-ttu-id="0549b-198">Egyéb tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="0549b-198">Other properties</span></span>
<span data-ttu-id="0549b-199">Munkamenet-konfigurációs fájlok is elérhető műveletek mindegyikét szerepkör funkció fájlt azonban csak a csatlakozó felhasználók hozzáférésének különböző parancsok képessége nélkül.</span><span class="sxs-lookup"><span data-stu-id="0549b-199">Session configuration files can also do everything a role capability file can do, just without the ability to give connecting users access to different commands.</span></span>
<span data-ttu-id="0549b-200">Ha azt szeretné, hogy engedélyezése minden felhasználó hozzáférést adott parancsmagok, függvények és szolgáltatók, ehhez jobbra a munkamenet-konfigurációs fájlban.</span><span class="sxs-lookup"><span data-stu-id="0549b-200">If you want to allow all users access to specific cmdlets, functions, or providers, you can do so right in the session configuration file.</span></span>
<span data-ttu-id="0549b-201">A támogatott tulajdonságok a munkamenet-konfigurációs fájl teljes listájának megtekintéséhez futtassa a `Get-Help New-PSSessionConfigurationFile -Full`.</span><span class="sxs-lookup"><span data-stu-id="0549b-201">For a full list of supported properties in the session configuration file, run `Get-Help New-PSSessionConfigurationFile -Full`.</span></span>

## <a name="testing-a-session-configuration-file"></a><span data-ttu-id="0549b-202">Egy munkamenet-konfigurációs fájl tesztelése</span><span class="sxs-lookup"><span data-stu-id="0549b-202">Testing a session configuration file</span></span>

<span data-ttu-id="0549b-203">Egy munkamenet konfigurációs segítségével tesztelheti a [teszt-PSSessionConfigurationFile](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/test-pssessionconfigurationfile) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="0549b-203">You can test a session configuration using the [Test-PSSessionConfigurationFile](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/test-pssessionconfigurationfile) cmdlet.</span></span>
<span data-ttu-id="0549b-204">Erősen ajánlott, ha módosította a FERB fájlt egy szövegszerkesztő segítségével manuálisan annak érdekében, hogy a megfelelő-e szintaxisa tesztelje a munkamenet-konfigurációs fájlban.</span><span class="sxs-lookup"><span data-stu-id="0549b-204">It is strongly recommended that you test your session configuration file if you have edited the pssc file manually using a text editor to ensure the syntax is correct.</span></span>
<span data-ttu-id="0549b-205">Ha egy munkamenet-konfigurációs fájl nem felel meg a teszt, akkor nem fog hozzáférni a rendszer sikeresen regisztrálni kell.</span><span class="sxs-lookup"><span data-stu-id="0549b-205">If a session configuration file does not pass this test, it will not be able to be successfully registered on the system.</span></span>

## <a name="sample-session-configuration-file"></a><span data-ttu-id="0549b-206">A minta munkamenet konfigurációs fájl</span><span class="sxs-lookup"><span data-stu-id="0549b-206">Sample session configuration file</span></span>

<span data-ttu-id="0549b-207">Alatt egy teljes példa bemutatja, hogyan hozzon létre és JEA egy munkamenet-konfiguráció érvényesítése.</span><span class="sxs-lookup"><span data-stu-id="0549b-207">Below is a complete example showing how to create and validate a session configuration for JEA.</span></span>
<span data-ttu-id="0549b-208">Vegye figyelembe, hogy a szerepkör-definíciók létrehozva és tárolva a `$roles` változó a kényelem és olvashatóság érdekében.</span><span class="sxs-lookup"><span data-stu-id="0549b-208">Note that the role definitions are created and stored in the `$roles` variable for convenience and readability.</span></span>
<span data-ttu-id="0549b-209">A követelmény, hogy ehhez nincs.</span><span class="sxs-lookup"><span data-stu-id="0549b-209">It is not a requirement to do so.</span></span>

```powershell
$roles = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}

New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\JEAConfig.pssc -RunAsVirtualAccount -TranscriptDirectory 'C:\ProgramData\JEAConfiguration\Transcripts' -RoleDefinitions $roles -RequiredGroups @{ Or = '2FA-logon', 'smartcard-logon' }
Test-PSSessionConfigurationFile -Path .\JEAConfig.pssc # should yield True
```

## <a name="updating-session-configuration-files"></a><span data-ttu-id="0549b-210">Munkamenet-konfigurációs fájlok frissítése</span><span class="sxs-lookup"><span data-stu-id="0549b-210">Updating session configuration files</span></span>

<span data-ttu-id="0549b-211">Ha módosítania kell a JEA munkamenet-konfiguráció, beleértve a felhasználói szerepkör, a hozzárendelés tulajdonságait kell [regisztrációját](register-jea.md#unregistering-jea-configurations) és [újraregisztrálni](register-jea.md) JEA munkamenet-konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="0549b-211">If you need to change properties of a JEA session configuration, including the mapping of users to roles, you must [unregister](register-jea.md#unregistering-jea-configurations) and [re-register](register-jea.md) the JEA session configuration.</span></span>
<span data-ttu-id="0549b-212">Regisztrálja újra a JEA munkamenet-konfiguráció, ha egy frissített PowerShell munkamenetben konfigurációs fájlt használja, amely tartalmazza a szükséges módosításokat.</span><span class="sxs-lookup"><span data-stu-id="0549b-212">When you re-register the JEA session configuration, use an updated PowerShell session configuration file that includes your desired changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0549b-213">További lépések</span><span class="sxs-lookup"><span data-stu-id="0549b-213">Next steps</span></span>

- [<span data-ttu-id="0549b-214">A JEA konfigurációs regisztrálása</span><span class="sxs-lookup"><span data-stu-id="0549b-214">Register a JEA configuration</span></span>](register-jea.md)
- [<span data-ttu-id="0549b-215">Szerző JEA szerepkörök</span><span class="sxs-lookup"><span data-stu-id="0549b-215">Author JEA roles</span></span>](role-capabilities.md)