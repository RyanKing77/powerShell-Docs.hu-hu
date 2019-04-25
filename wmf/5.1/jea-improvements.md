---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
contributor: ryanpu
title: Éppen elég felügyelettel (JEA) fejlesztései
ms.openlocfilehash: 66cbacb78f8a365e9c8556c7c56b3c3525de7395
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62055632"
---
# <a name="improvements-to-just-enough-administration-jea"></a><span data-ttu-id="0d897-103">Éppen elég felügyelettel (JEA) fejlesztései</span><span class="sxs-lookup"><span data-stu-id="0d897-103">Improvements to Just Enough Administration (JEA)</span></span>

## <a name="constrained-file-copy-tofrom-jea-endpoints"></a><span data-ttu-id="0d897-104">Korlátozott fájlmásolási és-tárolókról a JEA-végpont</span><span class="sxs-lookup"><span data-stu-id="0d897-104">Constrained file copy to/from JEA endpoints</span></span>

<span data-ttu-id="0d897-105">Most már távolról másolhat fájlokat/a JEA-végpont és a rest biztosítani, hogy a kapcsolódó felhasználó nem lehet másolni az imént *bármely* fájlt a rendszer.</span><span class="sxs-lookup"><span data-stu-id="0d897-105">You can now remotely copy files to/from a JEA endpoint and rest assured that the connecting user can't copy just *any* file on your system.</span></span> <span data-ttu-id="0d897-106">Ez akkor lehetséges, a felhasználók kapcsolódás felhasználói meghajtó csatlakoztatása FERB fájl konfigurálásával.</span><span class="sxs-lookup"><span data-stu-id="0d897-106">This is possible by configuring your PSSC file to mount a user drive for connecting users.</span></span> <span data-ttu-id="0d897-107">A felhasználó meghajtó nem egy új PSDrive, amely minden csatlakozó felhasználó egyedi, és továbbra is fennáll, munkamenetek között.</span><span class="sxs-lookup"><span data-stu-id="0d897-107">The user drive is a new PSDrive that is unique to each connecting user and persists across sessions.</span></span> <span data-ttu-id="0d897-108">Amikor `Copy-Item` van segítségével másolja a fájlokat, vagy a JEA-munkamenetből, azt korlátozza a kizárólag a felhasználó meghajtót.</span><span class="sxs-lookup"><span data-stu-id="0d897-108">When `Copy-Item` is used to copy files to or from a JEA session, it is constrained to only allow access to the user drive.</span></span> <span data-ttu-id="0d897-109">Fájlok másolása a bármely más PSDrive tett kísérletek sikertelenek lesznek.</span><span class="sxs-lookup"><span data-stu-id="0d897-109">Attempts to copy files to any other PSDrive will fail.</span></span>

<span data-ttu-id="0d897-110">A felhasználó meghajtó a JEA munkamenet konfigurációs fájlban, használja a következő új mezőket:</span><span class="sxs-lookup"><span data-stu-id="0d897-110">To set up the user drive in your JEA session configuration file, use the following new fields:</span></span>

```powershell
MountUserDrive = $true
UserDriveMaximumSize = 10485760    # 10 MB
```

<span data-ttu-id="0d897-111">A mappa, a felhasználó meghajtó biztonsági jön létre: `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\DriveRoots\DOMAIN_USER`</span><span class="sxs-lookup"><span data-stu-id="0d897-111">The folder backing the user drive will be created at `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\DriveRoots\DOMAIN_USER`</span></span>

<span data-ttu-id="0d897-112">A felhasználó meghajtót, és a fájlok másolása és- tárolókról a JEA végpont elérhetővé a felhasználói meghajtót konfigurálni, használja a `-ToSession` és `-FromSession` paramétereket lévő `Copy-Item`.</span><span class="sxs-lookup"><span data-stu-id="0d897-112">To utilize the user drive and copy files to/from a JEA endpoint configured to expose the User drive, use the `-ToSession` and `-FromSession` parameters on `Copy-Item`.</span></span>

```powershell
# Connect to the JEA endpoint
$jeasession = New-PSSession -ComputerName 'srv01' -ConfigurationName 'UserDemo'

# Copy a file in the local folder to the remote machine.
# Note: you cannot specify the file name or subfolder on the remote machine.
# You must exactly type "User:"
Copy-Item -Path .\SampleFile.txt -Destination User: -ToSession $jeasession

# Copy the file back from the remote machine to your local machine
Copy-Item -Path User:\SampleFile.txt -Destination . -FromSession $jeasession
```

<span data-ttu-id="0d897-113">Majd írhat fel az adatokat a felhasználó meghajtón tárolja, és azokat a szerepkör képesség fájlt a felhasználók számára elérhetővé tenni az egyéni függvényekhez.</span><span class="sxs-lookup"><span data-stu-id="0d897-113">You can then write custom functions to process the data stored in the user drive and make those available to users in your Role Capability file.</span></span>

## <a name="support-for-group-managed-service-accounts"></a><span data-ttu-id="0d897-114">Támogatási csoport számára a felügyelt fiókok</span><span class="sxs-lookup"><span data-stu-id="0d897-114">Support for Group Managed Service Accounts</span></span>

<span data-ttu-id="0d897-115">Bizonyos esetekben a JEA munkamenet egy felhasználó számára szükséges feladat kell előfordulhat, hogy a helyi gép erőforrások eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="0d897-115">In some cases, a task a user needs to perform in a JEA session may need to access resources beyond the local machine.</span></span> <span data-ttu-id="0d897-116">A JEA-munkamenet virtuális fiók használatára van konfigurálva, amikor eléri az ilyen erőforrások tett bármilyen kísérlet kell meghatároznia a helyi gép identitása, nem a virtuális vagy csatlakoztatott felhasználói fiókot fog megjelenni.</span><span class="sxs-lookup"><span data-stu-id="0d897-116">When a JEA session is configured to use a virtual account, any attempt to reach such resources will appear to come from the local machine's identity, not the virtual account or connected user.</span></span> <span data-ttu-id="0d897-117">A TP5, engedélyeztük a jea-t futtató környezetében támogatása egy [csoportosan felügyelt szolgáltatásfiók](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj128431\(v=ws.11\)), ami nagyban megkönnyíti a tartomány identitás használatával hálózati erőforrások eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="0d897-117">In TP5, we have enabled support for running JEA under the context of a [Group Managed Service Account](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj128431\(v=ws.11\)), making it much easier to access network resources by using a domain identity.</span></span>

<span data-ttu-id="0d897-118">A JEA-munkamenet futtatásához a csoportosan felügyelt szolgáltatásfiókok konfigurálásához használja a következő új kulcs a FERB fájlban:</span><span class="sxs-lookup"><span data-stu-id="0d897-118">To configure a JEA session to run under a gMSA account, use the following new key in your PSSC file:</span></span>

```powershell
# Provide the name of your gMSA account here (don't include a trailing $)
# The local machine must be privileged to use this gMSA in Active Directory
GroupManagedServiceAccount = 'myGMSAforJEA'

# You cannot configure a JEA endpoint to use both a gMSA and virtual account
# You can leave the RunAsVirtualAccount field commented out or explicitly set it to false
RunAsVirtualAccount = $false
```

> [!NOTE]
> <span data-ttu-id="0d897-119">Csoportosan felügyelt szolgáltatásfiókok nem elfogadható, az elkülönítés vagy a virtuális fiókok korlátozott körét.</span><span class="sxs-lookup"><span data-stu-id="0d897-119">Group Managed Service Accounts do not afford the isolation or limited scope of virtual accounts.</span></span>
> <span data-ttu-id="0d897-120">Minden csatlakozó felhasználó megosztja szükségszerűen rendelkezik engedéllyel a teljes vállalaton belül azonos csoportosan felügyelt szolgáltatásfiók-identitást.</span><span class="sxs-lookup"><span data-stu-id="0d897-120">Every connecting user will share the same gMSA identity, which may have permissions across your entire enterprise.</span></span> <span data-ttu-id="0d897-121">Legyen körültekintő, amikor kiválasztja a csoportosan felügyelt szolgáltatásfiók használatára, és mindig igény szerint virtuális fiók, amely csak a helyi számítógépre, amikor csak lehetséges.</span><span class="sxs-lookup"><span data-stu-id="0d897-121">Be very careful when selecting to use a gMSA, and always prefer virtual accounts which are limited to the local machine when possible.</span></span>

## <a name="conditional-access-policies"></a><span data-ttu-id="0d897-122">Feltételes hozzáférési szabályzatok</span><span class="sxs-lookup"><span data-stu-id="0d897-122">Conditional access policies</span></span>

<span data-ttu-id="0d897-123">A JEA kiválóan korlátozza, hogy valaki mire képes, ha már kapcsolódik egy rendszerhez való, de Lehetőségelemzési meg is szeretné korlátozni, *amikor* valaki használhatja a JEA?</span><span class="sxs-lookup"><span data-stu-id="0d897-123">JEA is great at limiting what someone can do when they've connected to a system to manage it, but what if you also want to limit *when* someone can use JEA?</span></span> <span data-ttu-id="0d897-124">Hozzáadtuk a konfigurációs beállításokat, a munkamenet-konfigurációs fájlok (.pssc) lehetővé teszi, hogy adja meg a felhasználó kell tartozniuk ahhoz, hogy a JEA-munkamenetet létrehozni a biztonsági csoportokat.</span><span class="sxs-lookup"><span data-stu-id="0d897-124">We have added configuration options into the session configuration files (.pssc) to let you specify security groups to which a user must belong in order to establish a JEA session.</span></span> <span data-ttu-id="0d897-125">Ez különösen hasznos lehet, ha csak az idő szerinti (JIT) rendszert a környezetben, és győződjön meg a felhasználók jogosultságai kibővítésére a magas jogosultsági szintű JEA-végpont elérése előtt.</span><span class="sxs-lookup"><span data-stu-id="0d897-125">This can be particularly helpful if you have a Just In Time (JIT) system in your environment, and want to make your users elevate their privileges before accessing a highly-privileged JEA endpoint.</span></span>

<span data-ttu-id="0d897-126">Az új *RequiredGroups* a FERB fájlban mező lehetővé teszi a logikát meghatározni, ha egy felhasználó csatlakozhat a JEA megadását.</span><span class="sxs-lookup"><span data-stu-id="0d897-126">The new *RequiredGroups* field in the PSSC file allows you to specify the logic to determine if a user can connect to JEA.</span></span> <span data-ttu-id="0d897-127">Adjon meg egy kivonattáblát (szükség esetén a beágyazott) használó áll a "És" és "Vagy" kulcsok a szabályok létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="0d897-127">It consists of specifying a hashtable (optionally nested) that uses the 'And' and 'Or' keys to construct your rules.</span></span> <span data-ttu-id="0d897-128">Íme néhány példa bemutatja, hogyan használhatja ezt a mezőt:</span><span class="sxs-lookup"><span data-stu-id="0d897-128">Here are some examples of how to leverage this field:</span></span>

```powershell
# Example 1: Connecting users must belong to a security group called "elevated-jea"
RequiredGroups = @{ And = 'elevated-jea' }

# Example 2: Connecting users must have signed on with 2 factor authentication or a smart card
# The 2 factor authentication group name is "2FA-logon" and the smart card group name is "smartcard-logon"
RequiredGroups = @{ Or = '2FA-logon', 'smartcard-logon' }

# Example 3: Connecting users must elevate into "elevated-jea" with their JIT system and have logged on with 2FA or a smart card
RequiredGroups = @{ And = 'elevated-jea', @{ Or = '2FA-logon', 'smartcard-logon' }}
```

## <a name="fixed-virtual-accounts-are-now-supported-on-windows-server-2008-r2"></a><span data-ttu-id="0d897-129">Kijavítva: A virtuális fiókok mostantól támogatja a Windows Server 2008 R2 rendszeren</span><span class="sxs-lookup"><span data-stu-id="0d897-129">Fixed: Virtual accounts are now supported on Windows Server 2008 R2</span></span>

<span data-ttu-id="0d897-130">A WMF 5.1 áll a virtuális fiókok használhatják a Windows Server 2008 R2, teszi lehetővé a konzisztens konfigurációk és funkcióparitás Windows Server 2008 R2 – 2016.</span><span class="sxs-lookup"><span data-stu-id="0d897-130">In WMF 5.1, you are now able to use virtual accounts on Windows Server 2008 R2, enabling consistent configurations and feature parity across Windows Server 2008 R2 - 2016.</span></span> <span data-ttu-id="0d897-131">A JEA használata a Windows 7-es virtuális fiókok továbbra is nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="0d897-131">Virtual accounts remain unsupported when using JEA on Windows 7.</span></span>