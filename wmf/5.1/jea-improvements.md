---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
contributor: ryanpu
title: Éppen elég felügyelettel (JEA) fejlesztései
ms.openlocfilehash: 47a58a6fae9f3a41ec527ec1f77ac1c196336669
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="improvements-to-just-enough-administration-jea"></a>Éppen elég felügyelettel (JEA) fejlesztései

## <a name="constrained-file-copy-tofrom-jea-endpoints"></a>JEA végpontok és a korlátozott fájl másolása

Mostantól távolról másolhatja a fájlokat/egy JEA a többi pedig a végpont biztosítva, hogy a csatlakozó felhasználó nem lehet másolni az imént *bármely* fájl a rendszeren.
Ezen nem lehetséges a felhasználók csatlakozni felhasználói meghajtó csatlakoztatása FERB fájl konfigurálása.
A felhasználó egy új PSDrive, amely az egyes csatlakozó felhasználók egyedi, és továbbra is fennáll, munkamenetei között.
Amikor elem használatával másolja a fájlokat, vagy a JEA munkamenetből, hogy csak a felhasználó meghajtót által korlátozott.
Fájlok másolása bármely más PSDrive kísérletek sikertelenek lesznek.

A JEA munkamenet konfigurációs fájlban beállítása a felhasználó merevlemezén, használja a következő új mezők:

```powershell
MountUserDrive = $true
UserDriveMaximumSize = 10485760    # 10 MB
```

A mappa biztonsági a felhasználó-meghajtó létrehozása `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\DriveRoots\DOMAIN_USER`

A felhasználó meghajtó használatára, és másolja a fájlokat, egy teszi közzé a felhasználó meghajtó beállított JEA végpont onnan, használja a `-ToSession` és `-FromSession` elem paraméterek.

```powershell
# Connect to the JEA endpoint
$jeasession = New-PSSession -ComputerName 'srv01' -ConfigurationName 'UserDemo'

# Copy a file in the local folder to the remote machine.
# Note: you cannot specify the file name or subfolder on the remote machine. You must exactly type "User:"
Copy-Item -Path .\SampleFile.txt -Destination User: -ToSession $jeasession

# Copy the file back from the remote machine to your local machine
Copy-Item -Path User:\SampleFile.txt -Destination . -FromSession $jeasession
```

Majd írhat feldolgozni az adatokat, a felhasználó meghajtón tárolja, és elérhetővé a felhasználóknak a szerepkör funkció fájlban egyéni függvényekhez.

## <a name="support-for-group-managed-service-accounts"></a>A felügyelt támogatási csoport fiókok

Bizonyos esetekben egy feladatot, a felhasználó számára szükséges-e a JEA-munkamenetben kell a helyi számítógép mögötti erőforrások eléréséhez.
A JEA munkamenet virtuális fiók használatára van konfigurálva, amikor minden, az ilyen erőforrások eléréséhez az általa elérni a helyi gép identitása, nem a virtuális fiók vagy a csatlakoztatott felhasználói jelenik meg.
A TP5, azt engedélyezte a JEA egy [csoportosan felügyelt szolgáltatásfiók](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11\).aspx) környezetében futó támogatása , így sokkal könnyebben hálózati erőforrások eléréséhez a tartomány identitásával.

A csoportosan felügyelt szolgáltatásfiók alatt fut JEA munkamenet konfigurálásához használja a következő új kulcsot a FERB fájlban:

```powershell
# Provide the name of your gMSA account here (don't include a trailing $)
# The local machine must be privileged to use this gMSA in Active Directory
GroupManagedServiceAccount = 'myGMSAforJEA'

# You cannot configure a JEA endpoint to use both a gMSA and virtual account
# You can leave the RunAsVirtualAccount field commented out or explicitly set it to false
RunAsVirtualAccount = $false
```

> **Megjegyzés:** csoportosan felügyelt szolgáltatásfiókok nem biztosít a elkülönítés vagy a virtuális fiókokat korlátozott körét.
> Minden csatlakozó felhasználó megosztja szükségszerűen rendelkezik engedéllyel a teljes vállalat azonos csoportosan felügyelt szolgáltatásfiók-identitást.
> Legyen körültekintő, lehetőséget választva a csoportosan felügyelt szolgáltatásfiókot, és mindig előnyben részesítik a virtuális fiókokat, amelyek csak a helyi számítógépen, ha lehetséges.

## <a name="conditional-access-policies"></a>Feltételes hozzáférési házirendek

Nagyszerű, hogy milyen valaki lehet elvégezni, ha már kapcsolódik egy rendszer kezeléséhez, de milyen Ha akkor is korlátozni szeretné az JEA *amikor* JEA segítségével bárki?
Lehetővé teszi, hogy a felhasználó kell tartozniuk ahhoz, hogy a JEA-munkamenetet létrehozni a biztonsági csoportokat adja meg a munkamenet-konfigurációs fájlok (.pssc) a konfigurációs beállítások jelentek meg.
Ez különösen hasznos lehet, ha egy csak az idő szerinti (JIT) rendszer környezetében, és szeretné, hogy a magas jogosultsági szintű JEA végpont elérése előtt függesztheti a felhasználót.

Az új *RequiredGroups* a FERB mezőjének lehetővé teszi annak meghatározásához, ha egy felhasználó csatlakozhat JEA logikát.
Olyan karakterekből áll, egy kivonattáblát (ha szükséges a beágyazott) használó megadása a "És" és "Vagy" kulcsok készítse el szabályait.
Íme néhány példa bemutatja, hogyan használhatók ki ebben a mezőben:

```powershell
# Example 1: Connecting users must belong to a security group called "elevated-jea"
RequiredGroups = @{ And = 'elevated-jea' }

# Example 2: Connecting users must have signed on with 2 factor authentication or a smart card
# The 2 factor authentication group name is "2FA-logon" and the smart card group name is "smartcard-logon"
RequiredGroups = @{ Or = '2FA-logon', 'smartcard-logon' }

# Example 3: Connecting users must elevate into "elevated-jea" with their JIT system and have logged on with 2FA or a smart card
RequiredGroups = @{ And = 'elevated-jea', @{ Or = '2FA-logon', 'smartcard-logon' }}
```

## <a name="fixed-virtual-accounts-are-now-supported-on-windows-server-2008-r2"></a>Rögzített: Virtuális fiókok mostantól támogatja a Windows Server 2008 R2 rendszeren
A WMF 5.1 áll a virtuális fiókokat használhatják a Windows Server 2008 R2, engedélyezése konzisztens konfigurációk és szolgáltatásparitást keresztül Windows Server 2008 R2 – 2016.
Virtuális fiókok továbbra is nem támogatott, ha a Windows 7 JEA használatával.
