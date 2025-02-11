---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
title: Éppen elég felügyelettel (JEA) fejlesztései
ms.openlocfilehash: 847ae92a6225023bcd0ee3dfe7c7058bdc356836
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65856202"
---
# <a name="improvements-to-just-enough-administration-jea"></a>Éppen elég felügyelettel (JEA) fejlesztései

Just Enough Administration új funkciója a WMF 5.0-s, amely lehetővé teszi, hogy a szerepkör alapú felügyelet a PowerShell távoli eljáráshívás segítségével. Kibővíti a meglévő infrastruktúra korlátozott végpontot azáltal, hogy nem rendszergazdák számára a parancsok, parancsprogramok és végrehajtható fájlok futtassa rendszergazdaként. Ez lehetővé teszi, hogy a rendszergazdák a környezetében számának csökkentése és a biztonság növelése.

## <a name="constrained-file-copy-tofrom-jea-endpoints"></a>Korlátozott fájlmásolási és-tárolókról a JEA-végpont

Most már távolról fájlokat másolhat és- tárolókról a JEA-végpont, és biztos lehet abban, hogy a kapcsolódó felhasználó nem lehet másolni az imént *bármely* fájlt a rendszer. Ez akkor lehetséges, a felhasználók kapcsolódás felhasználói meghajtó csatlakoztatása FERB fájl konfigurálásával. A felhasználó meghajtó nem egy új PSDrive, amely minden csatlakozó felhasználó egyedi, és továbbra is fennáll, munkamenetek között. Amikor `Copy-Item` van segítségével másolja a fájlokat, vagy a JEA-munkamenetből, azt korlátozza a kizárólag a felhasználó meghajtót. Fájlok másolása a bármely más PSDrive tett kísérletek sikertelenek lesznek.

A felhasználó meghajtó a JEA munkamenet konfigurációs fájlban, használja a következő új mezőket:

```powershell
MountUserDrive = $true
UserDriveMaximumSize = 10485760    # 10 MB
```

A mappa, a felhasználó meghajtó biztonsági jön létre: `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\DriveRoots\DOMAIN_USER`

A felhasználó meghajtót, és a fájlok másolása és- tárolókról a JEA végpont elérhetővé a felhasználói meghajtót konfigurálni, használja a `-ToSession` és `-FromSession` paramétereket lévő `Copy-Item`.

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

Majd írhat fel az adatokat a felhasználó meghajtón tárolja, és azokat a szerepkör képesség fájlt a felhasználók számára elérhetővé tenni az egyéni függvényekhez.

## <a name="support-for-group-managed-service-accounts"></a>Támogatási csoport számára a felügyelt fiókok

Bizonyos esetekben a JEA munkamenet egy felhasználó számára szükséges feladat kell előfordulhat, hogy a helyi gép erőforrások eléréséhez. A JEA-munkamenet virtuális fiók használatára van konfigurálva, amikor eléri az ilyen erőforrások tett bármilyen kísérlet kell meghatároznia a helyi gép identitása, nem a virtuális vagy csatlakoztatott felhasználói fiókot fog megjelenni. A TP5, engedélyeztük a jea-t futtató környezetében támogatása egy [csoportosan felügyelt szolgáltatásfiók](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj128431\(v=ws.11\)), ami nagyban megkönnyíti a tartomány identitás használatával hálózati erőforrások eléréséhez.

A JEA-munkamenet futtatásához a csoportosan felügyelt szolgáltatásfiókok konfigurálásához használja a következő új kulcs a FERB fájlban:

```powershell
# Provide the name of your gMSA account here (don't include a trailing $)
# The local machine must be privileged to use this gMSA in Active Directory
GroupManagedServiceAccount = 'myGMSAforJEA'

# You cannot configure a JEA endpoint to use both a gMSA and virtual account
# You can leave the RunAsVirtualAccount field commented out or explicitly set it to false
RunAsVirtualAccount = $false
```

> [!NOTE]
> Csoportosan felügyelt szolgáltatásfiókok nem elfogadható, az elkülönítés vagy a virtuális fiókok korlátozott körét.
> Minden csatlakozó felhasználó megosztja szükségszerűen rendelkezik engedéllyel a teljes vállalaton belül azonos csoportosan felügyelt szolgáltatásfiók-identitást. Legyen körültekintő, amikor kiválasztja a csoportosan felügyelt szolgáltatásfiók használatára, és mindig igény szerint virtuális fiók, amely csak a helyi számítógépre, amikor csak lehetséges.

## <a name="conditional-access-policies"></a>Feltételes hozzáférési szabályzatok

A JEA kiválóan korlátozza, hogy valaki mire képes, ha már kapcsolódik egy rendszerhez való, de Lehetőségelemzési meg is szeretné korlátozni, *amikor* valaki használhatja a JEA? Hozzáadtuk a konfigurációs beállításokat, a munkamenet-konfigurációs fájlok (.pssc) lehetővé teszi, hogy adja meg a felhasználó kell tartozniuk ahhoz, hogy a JEA-munkamenetet létrehozni a biztonsági csoportokat. Ez akkor hasznos, ha csak az idő szerinti (JIT) rendszert a környezetben, és győződjön meg a felhasználók jogosultságai kibővítésére a magas jogosultsági szintű JEA-végpont elérése előtt.

Az új *RequiredGroups* a FERB fájlban mező lehetővé teszi a logikát meghatározni, ha egy felhasználó csatlakozhat a JEA megadását. Adjon meg egy kivonattáblát (szükség esetén a beágyazott) használó áll a "És" és "Vagy" kulcsok a szabályok létrehozásához. Íme néhány példa bemutatja, hogyan használja ezt a mezőt:

```powershell
# Example 1: Connecting users must belong to a security group called "elevated-jea"
RequiredGroups = @{ And = 'elevated-jea' }

# Example 2: Connecting users must have signed on with 2 factor authentication or a smart card
# The 2 factor authentication group name is "2FA-logon" and the smart card group name is "smartcard-logon"
RequiredGroups = @{ Or = '2FA-logon', 'smartcard-logon' }

# Example 3: Connecting users must elevate into "elevated-jea" with their JIT system and have logged on with 2FA or a smart card
RequiredGroups = @{ And = 'elevated-jea', @{ Or = '2FA-logon', 'smartcard-logon' }}
```

## <a name="fixed-virtual-accounts-are-now-supported-on-windows-server-2008-r2"></a>Kijavítva: A virtuális fiókok mostantól támogatja a Windows Server 2008 R2 rendszeren

A WMF 5.1 áll a virtuális fiókok használhatják a Windows Server 2008 R2, teszi lehetővé a konzisztens konfigurációk és funkcióparitás Windows Server 2008 R2 – 2016. A JEA használata a Windows 7-es virtuális fiókok továbbra is nem támogatott.