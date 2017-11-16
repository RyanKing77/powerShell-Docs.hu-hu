---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
contributor: ryanpu
title: "Éppen elég felügyelettel (JEA) fejlesztései"
ms.openlocfilehash: 2811b4deb3f4fca513791c7389ee5f9f877dbfe8
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="improvements-to-just-enough-administration-jea"></a><span data-ttu-id="d9205-103">Éppen elég felügyelettel (JEA) fejlesztései</span><span class="sxs-lookup"><span data-stu-id="d9205-103">Improvements to Just Enough Administration (JEA)</span></span>

## <a name="constrained-file-copy-tofrom-jea-endpoints"></a><span data-ttu-id="d9205-104">JEA végpontok és a korlátozott fájl másolása</span><span class="sxs-lookup"><span data-stu-id="d9205-104">Constrained file copy to/from JEA endpoints</span></span>

<span data-ttu-id="d9205-105">Mostantól távolról másolhatja a fájlokat/egy JEA a többi pedig a végpont biztosítva, hogy a csatlakozó felhasználó nem lehet másolni az imént *bármely* fájl a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="d9205-105">You can now remotely copy files to/from a JEA endpoint and rest assured that the connecting user can't copy just *any* file on your system.</span></span>
<span data-ttu-id="d9205-106">Ezen nem lehetséges a felhasználók csatlakozni felhasználói meghajtó csatlakoztatása FERB fájl konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="d9205-106">This is possible by configuring your PSSC file to mount a user drive for connecting users.</span></span>
<span data-ttu-id="d9205-107">A felhasználó egy új PSDrive, amely az egyes csatlakozó felhasználók egyedi, és továbbra is fennáll, munkamenetei között.</span><span class="sxs-lookup"><span data-stu-id="d9205-107">The user drive is a new PSDrive that is unique to each connecting user and persists across sessions.</span></span>
<span data-ttu-id="d9205-108">Amikor elem használatával másolja a fájlokat, vagy a JEA munkamenetből, hogy csak a felhasználó meghajtót által korlátozott.</span><span class="sxs-lookup"><span data-stu-id="d9205-108">When Copy-Item is used to copy files to or from a JEA session, it is constrained to only allow access to the user drive.</span></span>
<span data-ttu-id="d9205-109">Fájlok másolása bármely más PSDrive kísérletek sikertelenek lesznek.</span><span class="sxs-lookup"><span data-stu-id="d9205-109">Attempts to copy files to any other PSDrive will fail.</span></span>

<span data-ttu-id="d9205-110">A JEA munkamenet konfigurációs fájlban beállítása a felhasználó merevlemezén, használja a következő új mezők:</span><span class="sxs-lookup"><span data-stu-id="d9205-110">To set up the user drive in your JEA session configuration file, use the following new fields:</span></span>

```powershell
MountUserDrive = $true
UserDriveMaximumSize = 10485760    # 10 MB
```

<span data-ttu-id="d9205-111">A mappa biztonsági a felhasználó-meghajtó létrehozása`$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\DriveRoots\DOMAIN_USER`</span><span class="sxs-lookup"><span data-stu-id="d9205-111">The folder backing the user drive will be created at `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\DriveRoots\DOMAIN_USER`</span></span>

<span data-ttu-id="d9205-112">A felhasználó meghajtó használatára, és másolja a fájlokat, egy teszi közzé a felhasználó meghajtó beállított JEA végpont onnan, használja a `-ToSession` és `-FromSession` elem paraméterek.</span><span class="sxs-lookup"><span data-stu-id="d9205-112">To utilize the user drive and copy files to/from a JEA endpoint configured to expose the User drive, use the `-ToSession` and `-FromSession` parameters on Copy-Item.</span></span>

```powershell
# Connect to the JEA endpoint
$jeasession = New-PSSession -ComputerName 'srv01' -ConfigurationName 'UserDemo'

# Copy a file in the local folder to the remote machine.
# Note: you cannot specify the file name or subfolder on the remote machine. You must exactly type "User:"
Copy-Item -Path .\SampleFile.txt -Destination User: -ToSession $jeasession

# Copy the file back from the remote machine to your local machine
Copy-Item -Path User:\SampleFile.txt -Destination . -FromSession $jeasession
```

<span data-ttu-id="d9205-113">Majd írhat feldolgozni az adatokat, a felhasználó meghajtón tárolja, és elérhetővé a felhasználóknak a szerepkör funkció fájlban egyéni függvényekhez.</span><span class="sxs-lookup"><span data-stu-id="d9205-113">You can then write custom functions to process the data stored in the user drive and make those available to users in your Role Capability file.</span></span>

## <a name="support-for-group-managed-service-accounts"></a><span data-ttu-id="d9205-114">A felügyelt támogatási csoport fiókok</span><span class="sxs-lookup"><span data-stu-id="d9205-114">Support for Group Managed Service Accounts</span></span>

<span data-ttu-id="d9205-115">Bizonyos esetekben egy feladatot, a felhasználó számára szükséges-e a JEA-munkamenetben kell a helyi számítógép mögötti erőforrások eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="d9205-115">In some cases, a task a user needs to perform in a JEA session may need to access resources beyond the local machine.</span></span>
<span data-ttu-id="d9205-116">A JEA munkamenet virtuális fiók használatára van konfigurálva, amikor minden, az ilyen erőforrások eléréséhez az általa elérni a helyi gép identitása, nem a virtuális fiók vagy a csatlakoztatott felhasználói jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="d9205-116">When a JEA session is configured to use a virtual account, any attempt to reach such resources will appear to come from the local machine's identity, not the virtual account or connected user.</span></span>
<span data-ttu-id="d9205-117">A TP5 azt engedélyezte a JEA egy [csoportosan felügyelt szolgáltatásfiók] (https://technet.microsoft.com/en-us/library/jj128431(v=ws.11\).aspx), így sokkal könnyebben hálózati erőforrások eléréséhez a tartomány környezetében futó támogatása identitás.</span><span class="sxs-lookup"><span data-stu-id="d9205-117">In TP5, we have enabled support for running JEA under the context of a [Group Managed Service Account](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11\).aspx), making it much easier to access network resources by using a domain identity.</span></span>

<span data-ttu-id="d9205-118">A csoportosan felügyelt szolgáltatásfiók alatt fut JEA munkamenet konfigurálásához használja a következő új kulcsot a FERB fájlban:</span><span class="sxs-lookup"><span data-stu-id="d9205-118">To configure a JEA session to run under a gMSA account, use the following new key in your PSSC file:</span></span>

```powershell
# Provide the name of your gMSA account here (don't include a trailing $)
# The local machine must be privileged to use this gMSA in Active Directory
GroupManagedServiceAccount = 'myGMSAforJEA'

# You cannot configure a JEA endpoint to use both a gMSA and virtual account
# You can leave the RunAsVirtualAccount field commented out or explicitly set it to false
RunAsVirtualAccount = $false
```

> <span data-ttu-id="d9205-119">**Megjegyzés:** csoportosan felügyelt szolgáltatásfiókok nem biztosít a elkülönítés vagy a virtuális fiókokat korlátozott körét.</span><span class="sxs-lookup"><span data-stu-id="d9205-119">**Note:** Group Managed Service Accounts do not afford the isolation or limited scope of virtual accounts.</span></span>
> <span data-ttu-id="d9205-120">Minden csatlakozó felhasználó megosztja szükségszerűen rendelkezik engedéllyel a teljes vállalat azonos csoportosan felügyelt szolgáltatásfiók-identitást.</span><span class="sxs-lookup"><span data-stu-id="d9205-120">Every connecting user will share the same gMSA identity, which may have permissions across your entire enterprise.</span></span>
> <span data-ttu-id="d9205-121">Legyen körültekintő, lehetőséget választva a csoportosan felügyelt szolgáltatásfiókot, és mindig előnyben részesítik a virtuális fiókokat, amelyek csak a helyi számítógépen, ha lehetséges.</span><span class="sxs-lookup"><span data-stu-id="d9205-121">Be very careful when selecting to use a gMSA, and always prefer virtual accounts which are limited to the local machine when possible.</span></span>

## <a name="conditional-access-policies"></a><span data-ttu-id="d9205-122">Feltételes hozzáférési házirendek</span><span class="sxs-lookup"><span data-stu-id="d9205-122">Conditional access policies</span></span>

<span data-ttu-id="d9205-123">Nagyszerű, hogy milyen valaki lehet elvégezni, ha már kapcsolódik egy rendszer kezeléséhez, de milyen Ha akkor is korlátozni szeretné az JEA *amikor* JEA segítségével bárki?</span><span class="sxs-lookup"><span data-stu-id="d9205-123">JEA is great at limiting what someone can do when they've connected to a system to manage it, but what if you also want to limit *when* someone can use JEA?</span></span>
<span data-ttu-id="d9205-124">Lehetővé teszi, hogy a felhasználó kell tartozniuk ahhoz, hogy a JEA-munkamenetet létrehozni a biztonsági csoportokat adja meg a munkamenet-konfigurációs fájlok (.pssc) a konfigurációs beállítások jelentek meg.</span><span class="sxs-lookup"><span data-stu-id="d9205-124">We have added configuration options into the session configuration files (.pssc) to let you specify security groups to which a user must belong in order to establish a JEA session.</span></span>
<span data-ttu-id="d9205-125">Ez különösen hasznos lehet, ha egy csak az idő szerinti (JIT) rendszer környezetében, és szeretné, hogy a magas jogosultsági szintű JEA végpont elérése előtt függesztheti a felhasználót.</span><span class="sxs-lookup"><span data-stu-id="d9205-125">This can be particularly helpful if you have a Just In Time (JIT) system in your environment, and want to make your users elevate their privileges before accessing a highly-privileged JEA endpoint.</span></span>

<span data-ttu-id="d9205-126">Az új *RequiredGroups* a FERB mezőjének lehetővé teszi annak meghatározásához, ha egy felhasználó csatlakozhat JEA logikát.</span><span class="sxs-lookup"><span data-stu-id="d9205-126">The new *RequiredGroups* field in the PSSC file allows you to specify the logic to determine if a user can connect to JEA.</span></span>
<span data-ttu-id="d9205-127">Olyan karakterekből áll, egy kivonattáblát (ha szükséges a beágyazott) használó megadása a "És" és "Vagy" kulcsok készítse el szabályait.</span><span class="sxs-lookup"><span data-stu-id="d9205-127">It consists of specifying a hashtable (optionally nested) that uses the 'And' and 'Or' keys to construct your rules.</span></span>
<span data-ttu-id="d9205-128">Íme néhány példa bemutatja, hogyan használhatók ki ebben a mezőben:</span><span class="sxs-lookup"><span data-stu-id="d9205-128">Here are some examples of how to leverage this field:</span></span>

```powershell
# Example 1: Connecting users must belong to a security group called "elevated-jea"
RequiredGroups = @{ And = 'elevated-jea' }

# Example 2: Connecting users must have signed on with 2 factor authentication or a smart card
# The 2 factor authentication group name is "2FA-logon" and the smart card group name is "smartcard-logon"
RequiredGroups = @{ Or = '2FA-logon', 'smartcard-logon' }

# Example 3: Connecting users must elevate into "elevated-jea" with their JIT system and have logged on with 2FA or a smart card
RequiredGroups = @{ And = 'elevated-jea', @{ Or = '2FA-logon', 'smartcard-logon' }}
```

## <a name="fixed-virtual-accounts-are-now-supported-on-windows-server-2008-r2"></a><span data-ttu-id="d9205-129">Rögzített: Virtuális fiókok mostantól támogatja a Windows Server 2008 R2 rendszeren</span><span class="sxs-lookup"><span data-stu-id="d9205-129">Fixed: Virtual accounts are now supported on Windows Server 2008 R2</span></span>
<span data-ttu-id="d9205-130">A WMF 5.1 áll a virtuális fiókokat használhatják a Windows Server 2008 R2, engedélyezése konzisztens konfigurációk és szolgáltatásparitást keresztül Windows Server 2008 R2 – 2016.</span><span class="sxs-lookup"><span data-stu-id="d9205-130">In WMF 5.1, you are now able to use virtual accounts on Windows Server 2008 R2, enabling consistent configurations and feature parity across Windows Server 2008 R2 - 2016.</span></span>
<span data-ttu-id="d9205-131">Virtuális fiókok továbbra is nem támogatott, ha a Windows 7 JEA használatával.</span><span class="sxs-lookup"><span data-stu-id="d9205-131">Virtual accounts remain unsupported when using JEA on Windows 7.</span></span>

