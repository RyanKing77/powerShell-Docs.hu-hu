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
# <a name="jea-session-configurations"></a>Jea-t a munkamenet-konfigurációk

A JEA-végpont létrehozásával és a egy PowerShell-munkamenet konfigurációs fájl regisztrálása regisztrálva van a rendszeren. A munkamenet-konfigurációk határozza meg, ki használhatja a JEA-végpont, és mely szerepkörök rendelkeznek hozzáféréssel. A JEA-munkamenet az összes felhasználóra érvényes globális beállítások is definiálják.

## <a name="create-a-session-configuration-file"></a>Egy munkamenet-konfigurációs fájl létrehozása

A JEA-végpontjának regisztrálását, meg kell adnia, hogy a végpont konfigurálását. Számos módon kell figyelembe venni. A legfontosabb választási lehetőségek a következők:

- Kik férhetnek hozzá a JEA-végpont
- Melyik szerepkört kell hozzárendelni
- Melyik identitás jea-t használja a háttérben
- A JEA-végpont neve

Ezek a beállítások határozzák meg egy PowerShell-adatokat tartalmazó fájl egy `.pssc` bővítmény ismert PowerShell munkamenet konfigurációs fájlt. A munkamenet-konfigurációs fájlt bármilyen szövegszerkesztőben szerkeszthető.

A következő paranccsal hozzon létre egy üres sablon konfigurációs fájlt.

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\MyJEAEndpoint.pssc
```

> [!TIP]
> A leggyakoribb konfigurációs beállítások szerepelnek a sablonfájlt alapértelmezés szerint. Használja a `-Full` kapcsolót, hogy a létrehozott FERB az összes alkalmazható beállítást tartalmazza.

A `-SessionType RestrictedRemoteServer` jelzi, hogy a munkamenet-konfiguráció szerint a JEA biztonságos felügyeletére használható. Az ilyen típusú munkamenetek működtetés **NoLanguage** mód, és csak a hozzáférést a következő alapértelmezett parancsokat (és aliasok):

- CLEAR-gazdagép (cls, törlése)
- Kilépés-PSSession (exsn, Kilépés)
- Get-Command (gcm)
- Get-FormatData
- Get-Help
- Measure-Object (measure)
- Out-Default
- Select-Object (select)

Nincs PowerShell szolgáltató érhetők el, sem pedig bármilyen külső programok (végrehajtható fájlok vagy parancsprogramok).

Nyelvi módokkal kapcsolatos további információkért lásd: [about_Language_modes](/powershell/module/microsoft.powershell.core/about/about_language_modes).

### <a name="choose-the-jea-identity"></a>Válassza ki a JEA-identitás

A színfalak mögött a JEA-identitás (fiók) egy csatlakoztatott felhasználói parancsok futtatása során használandó van szüksége.
Meghatározhatja, melyik identitás jea-t használ a munkamenet-konfigurációs fájlban.

#### <a name="local-virtual-account"></a>Virtuális helyi fiók

A virtuális helyi fiókok akkor hasznos, ha a JEA-végpont definiált összes szerepkör segítségével felügyelhető a helyi gépen, és egy helyi rendszergazdai fiók elegendő ahhoz, hogy a parancsok sikeresen lefutott.
A virtuális fiókok olyan ideiglenes fiókot, amely egy adott felhasználónak egyedi, és csak az utolsó idejére a PowerShell-munkamenetet. Egy olyan tagkiszolgáló vagy a munkaállomáson, a virtuális fiókok tartoznak a helyi számítógép **rendszergazdák** csoport. Az Active Directory-tartományvezérlő, a virtuális fiókok tartoznak a tartomány **Tartománygazdák** csoport.

```powershell
# Setting the session to use a virtual account
RunAsVirtualAccount = $true
```

Ha a szerepköröket, a munkamenet-konfiguráció által meghatározott nincs szükségük teljes körű rendszergazdai jogosultság, megadhatja a biztonsági csoportok, amelyhez a virtuális fiók fog tartozni. Egy olyan tagkiszolgáló vagy a munkaállomáson a megadott biztonsági csoportokban helyi csoportok nem a tartományból kell lennie.

Ha egy vagy több biztonsági csoportokat is meg van adva, a virtuális fiók nincs hozzárendelve a helyi vagy tartományi rendszergazdák csoportba.

```powershell
# Setting the session to use a virtual account that only belongs to the NetworkOperator and NetworkAuditor local groups
RunAsVirtualAccount = $true
RunAsVirtualAccountGroups = 'NetworkOperator', 'NetworkAuditor'
```

> [!NOTE]
> A virtuális fiókok ideiglenesen kapnak a bejelentkezés, a szolgáltatás közvetlenül a helyi kiszolgálói biztonsági házirendben. Ha a megadott VirtualAccountGroups egyike már rendelkezik ezzel a jogosultsággal, a házirendben, az egyes virtuális fiók lesz többé nem hozzáadható és eltávolítható a szabályzat alól. Ez például tartományvezérlőkkel, ahol a tartományvezérlő biztonsági házirendjének felülvizsgálata szorosan naplóz esetekben hasznos lehet. Ez a lehetőség csak a 2018 November rendelkező Windows Server 2016 vagy újabb kumulatív és a Windows Server 2019 a január 2019- vagy újabb kumulatív.

#### <a name="group-managed-service-account"></a>Csoportosan felügyelt szolgáltatásfiók

Csoportosan felügyelt szolgáltatásfiók (GMSA) a megfelelő identitással fussanak JEA felhasználók hozzáférjenek a hálózati erőforrásokhoz, például fájlmegosztásokat és a webszolgáltatások kell használni. Csoportosan felügyelt szolgáltatásfiókokat adjon egy tartományi identitás, amely minden olyan gép, a tartományon belül található erőforrásokkal hitelesítésére szolgál. A jogosultságokat, amelyeket a csoportosan felügyelt Szolgáltatásfiók biztosít határozza meg az erőforrásokat ér el. Rendszergazdai jogosultságok minden olyan gép vagy szolgáltatás nem rendelkezik, kivéve, ha a gép vagy szolgáltatás-rendszergazda explicit módon megadta ezeket a jogokat a csoportosan felügyelt Szolgáltatásfiókot.

```powershell
# Configure JEA sessions to use the GMSA in the local computer's domain
# with the sAMAccountName of 'MyJEAGMSA'
GroupManagedServiceAccount = 'Domain\MyJEAGMSA'
```

Csoportosan felügyelt szolgáltatásfiókokat csak szükség esetén használható:

- Meglehetősen nehéz nyomon követését egy felhasználói műveletek csoportosan felügyelt Szolgáltatásfiók használata esetén. Minden felhasználói fájlmegosztások azonos futtató identitását. Nézze át PowerShell-munkamenet szövegekben és naplók korrelációját, ha azok a műveletek az egyéni felhasználók számára.

- A csoportosan felügyelt Szolgáltatásfiók lehet számos olyan hálózati erőforrásokra, amely a kapcsolódó felhasználó nem kell a hozzáférést. Mindig próbálja hatályos engedélyek korlátozására, kövesse a legalacsonyabb jogosultsági szint elvének JEA munkamenetben.

> [!NOTE]
> A felügyelt szolgáltatásfiókok csoportot csak olyan elérhető a tartományhoz csatlakoztatott gépeket használ a PowerShell 5.1-es vagy újabb.

A JEA-munkamenet védelmével kapcsolatos további információkért lásd: a [biztonsági szempontok](security-considerations.md) cikk.

### <a name="session-transcripts"></a>Munkamenet szövegekben

Javasoljuk, hogy konfigurálja-e a JEA végpontot a felhasználói munkamenetek automatikus rögzítése szövegekben. PowerShell-munkamenet átiratok a csatlakozó felhasználó, a hozzájuk tartozó identitás futtató vonatkozó adatokat tartalmaznak, és a felhasználó által futtatott parancsok. Meg kell ismernie, akik által végrehajtott konkrét egy rendszer-naplózási csoport hasznos lehet.

Automatikus beszédátírási konfigurálása a munkamenet-konfigurációs fájlban, hol szeretné tárolni az átiratok mappa elérési útjának megadását.

```powershell
TranscriptDirectory = 'C:\ProgramData\JEAConfiguration\Transcripts'
```

A mappa által írt átiratok a **helyi rendszer** fiókot, amelyhez szükség van az olvasási és írási hozzáférés a címtárhoz. Az általános jogú felhasználók nem hozzáféréssel kell rendelkeznie a mappában. Az átiratok naplózási hozzáféréssel rendelkező rendszergazdák számának korlátozása.

### <a name="user-drive"></a>Felhasználó-meghajtó

Ha a csatlakozó felhasználók másolja a fájlokat, vagy a JEA-végpont szükséges, engedélyezheti a felhasználói meghajtó a munkamenet-konfigurációs fájlban. A felhasználó meghajtó egy **PSDrive** , amely az egyes csatlakozó felhasználók egyedi mappát van leképezve. Ez a mappa lehetővé teszi, hogy a felhasználók másolhatják a fájlokat, illetve a rendszer a hozzáférés engedélyezése a teljes fájlrendszer vagy a fájlrendszer-szolgáltatót is közzéteheti nélkül. A felhasználó meghajtó tartalma állandó befogadásához helyzetekben, ahol a hálózati kapcsolat megszakadhat a munkamenetek között.

```powershell
MountUserDrive = $true
```

Alapértelmezés szerint a felhasználó meghajtó lehetővé teszi felhasználónként 50 MB-ot legfeljebb tárolni. Korlátozhatja a felhasználók használhatnak fel, az adatok mennyisége a *UserDriveMaximumSize* mező.

```powershell
# Enables the user drive with a per-user limit of 500MB (524288000 bytes)
MountUserDrive = $true
UserDriveMaximumSize = 524288000
```

Ha a felhasználó meghajtón állandóként adatokat nem szeretné, konfigurálhatja egy ütemezett feladatot a rendszer automatikusan törölni a mappát éjszakánként.

> [!NOTE]
> A felhasználó meghajtó csak akkor érhető el a PowerShell 5.1-es vagy újabb.

PSDrives kapcsolatos további információkért lásd: [kezelése PowerShell-meghajtók](/powershell/scripting/samples/managing-windows-powershell-drives).

### <a name="role-definitions"></a>Szerepkör-definíciók

A munkamenet-konfigurációs fájlban található szerepkör-definíciók megadása leképezése **felhasználók** való **szerepkörök**. Minden felhasználó vagy csoport szerepel ebben a mezőben a JEA-végpont engedélyt kap, ha regisztrálva van.
Minden felhasználó vagy csoport csak egyszer lehet része lesz a kulcs a kivonattábla kulcsa, de több szerepkört is rendelhető. A név a szerepkör funkció nélkül legyen a szerepkör képesség fájl neve a `.psrc` bővítmény.

```powershell
RoleDefinitions = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}
```

Ha egy felhasználó tartozik a szerepkör-definíció egynél több csoportot, akkor az egyes szerepkörök hozzáférést kap. Ha két szerepkörnek hozzáférést ugyanazok a parancsmagok, a legmegengedőbb paraméterkészletet kapnak a felhasználó számára.

Ha a szerepkör-definíciók mezőben adja meg a helyi felhasználókat és csoportokat, ügyeljen arra, hogy a számítógép neve, nem **localhost** vagy helyettesítő karaktereket. A számítógépnév vizsgálatával ellenőrizheti a `$env:COMPUTERNAME` változó.

```powershell
RoleDefinitions = @{
    'MyComputerName\MyLocalGroup' = @{ RoleCapabilities = 'DnsAuditor' }
}
```

### <a name="role-capability-search-order"></a>Szerepkör képesség keresési sorrendje

A fenti példa szerint szerepkörrel képességeket a szerepkör képesség fájl alapneveként hivatkozik. A fájl alap név nélkül a kiterjesztést a fájlnév. A rendszer ezzel a névvel több szerepköri funkciók érhetők el, ha a PowerShell az implicit keresési sorrendje válassza ki a szerepkör hatékony képesség fájlt használ. A JEA does **nem** hozzáférést biztosít minden szerepkör képesség fájl ezzel a névvel.

Jea-t használ a `$env:PSModulePath` környezeti változót, mely szolgáltatást a szerepkör képesség fájlok elérési határozza meg. Adott elérési útján belül JEA keres, amely tartalmaz egy "RoleCapabilities" almappát érvényes PowerShell-modulok. Csakúgy, mint a modulok importálása a JEA szerepkörrel képességeket, az egyéni szerepkör képességekkel azonos nevű Windows-tal szállított részesíti előnyben.

Minden más elnevezési ütközések elsőbbséget Windows számba veszi a könyvtárban található fájlok sorrendje határozza meg. A rendelés betűrend szerinti rendezés nem garantált. Az első szerepkör képesség fájl található, amely megfelel a megadott nevet használja a csatlakozó felhasználó. A szerepkör képesség keresés óta sorrendje nem determinisztikus, **erősen ajánlott** , szerepkörrel képességeket rendelkezik-e egyedi fájlnevet.

### <a name="conditional-access-rules"></a>Feltételes hozzáférési szabályok

Minden felhasználó és csoport tartalmazza a **RoleDefinitions** mező automatikusan megkapja a JEA-végpont elérését. Feltételes hozzáférési szabályok lehetővé teszik, hogy finomíthatja a hozzáférést, és ne befolyásolják a szerepköröket, amelyhez hozzá van rendelve, további biztonsági csoporthoz tartoznak, hogy a felhasználók. Ez akkor hasznos, ha szeretné integrálni a just-in-time emelt szintű hozzáférés-kezelési megoldása, intelligens kártyás hitelesítés vagy más többtényezős hitelesítési megoldást a jea-t.

Feltételes hozzáférési szabályok a RequiredGroups mező egy munkamenet-konfigurációs fájlban vannak definiálva.
Itt adhat meg egy kivonattáblát (szükség esetén a beágyazott) használó "És" és "Vagy" kulcsok a szabályok létrehozásához. Íme néhány példa bemutatja, hogyan használja ezt a mezőt:

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
> Feltételes hozzáférési szabályok csak olyan, a PowerShell 5.1-es vagy újabb.

### <a name="other-properties"></a>Egyéb tulajdonságok

Munkamenet konfigurációs fájljainak minden szerepkör képesség fájl anélkül teheti meg, csak lehetővé teszi csatlakozó felhasználók hozzáférést biztosíthat más parancsok is megteheti. Ha azt szeretné, hogy minden felhasználó hozzáférést adott parancsmagok, függvények és szolgáltatók, megteheti közvetlenül a a munkamenet-konfigurációs fájlt.
A támogatott tulajdonságok a munkamenet-konfigurációs fájl teljes listájának megtekintéséhez futtassa `Get-Help New-PSSessionConfigurationFile -Full`.

## <a name="testing-a-session-configuration-file"></a>Egy munkamenet-konfigurációs fájl tesztelése

A munkamenet konfigurációja használatával tesztelhet a [Test-PSSessionConfigurationFile](/powershell/module/microsoft.powershell.core/test-pssessionconfigurationfile) parancsmagot. Javasoljuk, hogy a munkamenet-konfigurációs fájl teszteléséhez, ha manuálisan módosította a `.pssc` fájlt. Tesztelés biztosítja a szintaxisa helyes. Ha egy munkamenet-konfigurációs fájl a teszt meghiúsul, azt a rendszer nem regisztrálható.

## <a name="sample-session-configuration-file"></a>Minta munkamenet konfigurációs fájl

Az alábbi példa bemutatja, hogyan hozhat létre, és a egy munkamenet-konfiguráció ellenőrzése a jea-t. A szerepkör-definíciók létrehozása és tárolása a a `$roles` változó a kényelem és olvashatóság érdekében. Nem követelmény ennek a végrehajtására.

```powershell
$roles = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}

New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\JEAConfig.pssc -RunAsVirtualAccount -TranscriptDirectory 'C:\ProgramData\JEAConfiguration\Transcripts' -RoleDefinitions $roles -RequiredGroups @{ Or = '2FA-logon', 'smartcard-logon' }
Test-PSSessionConfigurationFile -Path .\JEAConfig.pssc # should yield True
```

## <a name="updating-session-configuration-files"></a>Munkamenet-konfigurációs fájlok frissítése

A JEA munkamenet-konfiguráció, többek között a felhasználók szerepkörökhöz leképezése tulajdonságainak módosítása kell [regisztrációját](register-jea.md#unregistering-jea-configurations). Ezt követően [újraregisztrálni](register-jea.md) a JEA munkamenet-konfiguráció frissített munkamenet konfigurációs fájl segítségével.

## <a name="next-steps"></a>További lépések

- [Regisztrálja a JEA-konfiguráció](register-jea.md)
- [Szerző JEA szerepkörök](role-capabilities.md)
