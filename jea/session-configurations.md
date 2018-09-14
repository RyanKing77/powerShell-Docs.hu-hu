---
ms.date: 06/12/2017
keywords: a jea, powershell, biztonsági
title: Jea-t a munkamenet-konfigurációk
ms.openlocfilehash: bdf3659357045203d90e8083613e51cce657da1a
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/13/2018
ms.locfileid: "45522959"
---
# <a name="jea-session-configurations"></a>Jea-t a munkamenet-konfigurációk

> A következőkre vonatkozik: Windows PowerShell 5.0

A JEA-végpont létrehozásával és a egy PowerShell-munkamenet konfigurációs fájl regisztrálása a meghatározott módon regisztrálva van a rendszeren.
A munkamenet-konfigurációk meghatározásához *akik* használhatja a JEA-végpont, és mely szerepkör(ök) fog hozzáféréssel rendelkeznek.
A JEA-munkamenet bármely szerepkör felhasználókra vonatkozó globális beállítások is definiálják.

Ez a témakör ismerteti, hogyan hozzon létre egy PowerShell-munkamenet konfigurációs fájlt, és a JEA-végpontjának regisztrálását.

## <a name="create-a-session-configuration-file"></a>Egy munkamenet-konfigurációs fájl létrehozása

A JEA-végpontjának regisztrálását, adja meg, hogyan kell konfigurálni, hogy a végpont kell.
Számos lehetőség kell figyelembe venni, a legfontosabb, mely hogy ki férhet hozzá a JEA-végpont, mely szerepköröket fogják hozzárendelni, mely identitás jea-t használja a háttérben, és mi lesz a JEA-végpont nevét.
Ezek az összes meghatározása egy PowerShell munkamenetet konfigurációs fájlban, amely egy PowerShell-adatfájlt lezárta .pssc kiterjesztéssel.

A JEA-végpont vázát munkamenet konfigurációs fájl létrehozásához futtassa az alábbi parancsot.

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\MyJEAEndpoint.pssc
```

> [!TIP]
> A leggyakoribb konfigurációs beállítások szerepelnek a vázát fájl alapértelmezés szerint.
> Használja a `-Full` kapcsolót, hogy a létrehozott FERB az összes alkalmazható beállítást tartalmazza.

Megnyithatja a munkamenet-konfigurációs fájlt bármilyen szövegszerkesztőben.
A `-SessionType RestrictedRemoteServer` jelzi, hogy a munkamenet-konfiguráció által használandó JEA biztonságos kezeléséhez.
Munkamenetek van ilyen módon fog működni a [NoLanguage mód](https://technet.microsoft.com/library/dn433292.aspx) , és csak a következő 8 alapértelmezett parancsokat (és aliasok) érhető el:

- CLEAR-gazdagép (cls, törlése)
- Kilépés-PSSession (exsn, Kilépés)
- Get-Command (gcm)
- Get-FormatData
- Get-Help
- Mérték-objektum (mérték)
- Kimenő irányú alapértelmezett
- Select-Object (kijelölés)

Nincs PowerShell szolgáltató érhetők el, sem pedig bármilyen külső programok (végrehajtható fájlok, parancsfájlok stb.).

Nincsenek számos más mezők, célszerű a JEA-munkamenet konfigurálása.
Azok a következő szakaszokban ismertetett.

### <a name="choose-the-jea-identity"></a>Válassza ki a JEA-identitás

A színfalak mögött a JEA-identitás (fiók) egy csatlakoztatott felhasználói parancsok futtatása során használandó van szüksége.
Eldöntheti, melyik identitás jea-t fogja használni a munkamenet-konfigurációs fájlban.

#### <a name="local-virtual-account"></a>Virtuális helyi fiók

Ha a szerepköröket a JEA-végpont által támogatott összes kezelésére használhatók a helyi gépen, és egy helyi rendszergazdai fiók elegendő ahhoz, hogy a parancsok sikeresen futtatni, konfigurálnia kell a jea-t a helyi virtuális fiók használata.
A virtuális fiókok olyan ideiglenes fiókot, amely egy adott felhasználónak egyedi, és csak az utolsó idejére a PowerShell-munkamenetet.
Egy olyan tagkiszolgáló vagy a munkaállomáson, a virtuális fiókok tartoznak a helyi számítógép **rendszergazdák** csoportból, és a legtöbb rendszer erőforrásait elérheti.
Az Active Directory-tartományvezérlő, a virtuális fiókok tartoznak a tartomány **Tartománygazdák** csoport.

```powershell
# Setting the session to use a virtual account
RunAsVirtualAccount = $true
```

Ha a szerepköröket, a munkamenet-konfiguráció által támogatott nincs szükség ilyen széles körű jogosultságokat, igény szerint megadhatja a biztonsági csoportok, amelyhez a virtuális fiók fog tartozni.
Egy olyan tagkiszolgáló vagy a munkaállomáson a megadott biztonsági csoportokban helyi csoportok nem a tartományból kell lennie.

Ha egy vagy több biztonsági csoport megadva, a virtuális fiók már nem fog tartozni a helyi vagy tartományi rendszergazdák csoportnak.

```powershell
# Setting the session to use a virtual account that only belongs to the NetworkOperator and NetworkAuditor local groups
RunAsVirtualAccount = $true
RunAsVirtualAccountGroups = 'NetworkOperator', 'NetworkAuditor'
```

#### <a name="group-managed-service-account"></a>Csoportosan felügyelt szolgáltatásfiók


A JEA-felhasználó, például a más webes szolgáltatásokat vagy hálózati erőforrások eléréséhez igénylő forgatókönyvek esetén a csoportosan felügyelt szolgáltatásfiók (gMSA) egy megfelelő identitás használatára.
csoportosan felügyelt szolgáltatásfiók fiókok lehetővé teszik, egy tartományi identitás, amely hitelesíti a rendszer minden olyan gép, a tartományban lévő erőforrások használható.
A jogosultságok a csoportosan felügyelt szolgáltatásfiók fiók lehetővé teszi azt határozza meg az erőforrások elérésére.
Nem automatikusan fog rendszergazdai jogosultságok minden olyan gép vagy szolgáltatás, ha a gép vagy szolgáltatás-rendszergazda explicit módon megadta a csoportosan felügyelt szolgáltatásfiókok rendszergazdai jogosultságokat.

```powershell
# Configure JEA sessions to use the gMSA account in the local computer's domain with the sAMAccountName of 'MyJEAgMSA'
GroupManagedServiceAccount = 'Domain\MyJEAgMSA'
```

csoportosan felügyelt szolgáltatásfiók-fiókok csak használható amikor hálózati erőforrásokhoz való hozzáférés szükség néhány okok miatt:

- Ezért jóval nehezebb nyomon követését egy felhasználói műveletek csoportosan felügyelt szolgáltatásfiókok használatakor, mivel minden felhasználó megosztja a ugyanazon futtató identitását. Tekintse meg a PowerShell-munkamenet szövegekben és a naplók felhasználók korrelációját, ha azok a műveletek kell.

- A csoportosan felügyelt szolgáltatásfiók férhetnek számos hálózati erőforrások, amelyek a kapcsolódó felhasználó nem kell a hozzáférést. Mindig próbálja hatályos engedélyek korlátozására, kövesse a legalacsonyabb jogosultsági szint elvének JEA munkamenetben.

> [!NOTE]
> A felügyelt szolgáltatásfiókok csoportot csak olyan elérhető Windows PowerShell 5.1-es vagy újabb és a tartományhoz csatlakoztatott gépeket.


#### <a name="more-information-about-run-as-users"></a>További információ a futtató felhasználók

Az identitások, és hogyan azok többtényezős biztonsági állapotáról a JEA-munkamenet, futtassa kapcsolatos további információk találhatók a [biztonsági szempontok](security-considerations.md) cikk.

### <a name="session-transcripts"></a>Munkamenet szövegekben

Javasoljuk, hogy konfigurálja-e a felhasználói munkamenetek automatikus rögzítése szövegekben JEA munkamenet konfigurációs fájlt.
PowerShell-munkamenet átiratok a csatlakozó felhasználó, a hozzájuk tartozó identitás futtató vonatkozó adatokat tartalmaznak, és a felhasználó által futtatott parancsok.
Egy naplózási csapat, akiknek meg kell ismernie, hogy ki hajtotta végre a rendszer egy adott módosítását hasznos lehet.

Automatikus beszédátírási konfigurálása a munkamenet-konfigurációs fájlban, hol szeretné tárolni az átiratok mappa elérési útjának megadását.

```powershell
TranscriptDirectory = 'C:\ProgramData\JEAConfiguration\Transcripts'
```

A megadott mappába kell konfigurálni, hogy a felhasználók módosítsák vagy töröljék a benne lévő adatokat.
Szövegekben írja azt a mappát a helyi rendszer fiók, amelyhez szükség van az olvasási és írási hozzáférés a címtárhoz.
Általános jogú felhasználók nem rendelkezhetnek azt a mappát, és a egy korlátozott számú biztonsági rendszergazdák rendelkezhetnek hozzáféréssel az átiratok naplózása.

### <a name="user-drive"></a>Felhasználó-meghajtó

Ha a csatlakozó felhasználók kell másolni a fájlok és-tárolókról a JEA-végpont annak érdekében, hogy a parancs futtatása, engedélyezheti a felhasználó meghajtó a munkamenet-konfigurációs fájlban.
A felhasználó meghajtó egy [PSDrive](https://msdn.microsoft.com/powershell/scripting/getting-started/cookbooks/managing-windows-powershell-drives) , amely az egyes csatlakozó felhasználók egyedi mappát van leképezve.
Ez a mappa szolgál egy szóközt, hogy másolja a fájlokat és-tárolókról a rendszer anélkül, hogy hozzáférést ad nekik a teljes fájlrendszerbe vagy a fájlrendszer-szolgáltatót is közzéteheti.
A felhasználó meghajtó tartalma állandó befogadásához helyzetekben, ahol a hálózati kapcsolat megszakadhat a munkamenetek között.

```powershell
MountUserDrive = $true
```

Alapértelmezés szerint a felhasználó meghajtó lehetővé teszi felhasználónként 50 MB-ot legfeljebb tárolni.
Korlátozhatja a felhasználók használhatnak fel, az adatok mennyisége a *UserDriveMaximumSize* mező.

```powershell
# Enables the user drive with a per-user limit of 500MB (524288000 bytes)
MountUserDrive = $true
UserDriveMaximumSize = 524288000
```

Ha nem szeretné, hogy a felhasználó meghajtón állandóként adatok, konfigurálhatja egy ütemezett feladatot a rendszer automatikusan törölni a mappát éjszakánként.

> [!NOTE]
> A felhasználó meghajtó csak akkor érhető el a Windows PowerShell 5.1-es vagy újabb.

### <a name="role-definitions"></a>Szerepkör-definíciók

A munkamenet-konfigurációs fájlban található szerepkör-definíciók megadása leképezése *felhasználók* való *szerepkörök*.
Minden felhasználó vagy csoport szerepel ebben a mezőben automatikusan engedélyt kap a JEA-végpont, ha regisztrálva van.
Minden felhasználó vagy csoport csak egyszer lehet része lesz a kulcs a kivonattábla kulcsa, de több szerepkört is rendelhető.
A szerepkör funkció a nevének kell lennie a szerepkör képesség .psrc fájlkiterjesztés nélkül fájl nevét.

```powershell
RoleDefinitions = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}
```

Ha egy felhasználó tartozik a szerepkör-definíció egynél több csoportot, akkor az egyes szerepkörök hozzáférést fog kapni.
Ha két szerepkör ugyanazok a parancsmagok való hozzáférést, a legmegengedőbb paraméterkészletet a felhasználó fog kapni.

Ha a szerepkör-definíciók mezőben adja meg a helyi felhasználókat és csoportokat, ügyeljen arra, hogy a számítógép nevét (nem *localhost* vagy *.*) a fordított perjel előtt.
A számítógépnév vizsgálatával ellenőrizheti a `$env:computername` változó.

```powershell
RoleDefinitions = @{
    'MyComputerName\MyLocalGroup' = @{ RoleCapabilities = 'DnsAuditor' }
}
```

### <a name="role-capability-search-order"></a>Szerepkör képesség keresési sorrendje
A fenti példa szerint szerepkörrel képességeket szerepkör képesség fájl egybesimított (fájlkiterjesztés nélkül fájlnév) nevére hivatkozik.
A rendszer strukturálatlan ugyanazzal a névvel több szerepkörrel képességeket érhetők el, ha PowerShell használatával az implicit keresési sorrendje válassza ki a szerepkör hatékony képesség fájlt.
Akkor **nem** hozzáférést biztosít minden szerepkör képesség fájl ezzel a névvel.

Jea-t használ a `$env:PSModulePath` környezeti változót, mely szolgáltatást a szerepkör képesség fájlok elérési határozza meg.
Minden egyes adott elérési útján JEA keresni, amely tartalmaz egy "RoleCapabilities" almappát érvényes PowerShell-modulok.
Csakúgy, mint a modulok importálása a JEA szerepkörrel képességeket, az egyéni szerepkör képességekkel azonos nevű Windows-tal szállított részesíti előnyben.
Minden más elnevezési ütközések elsőbbséget Windows számba veszi a könyvtár (nem garantált, hogy betűrend) lévő fájlok sorrendje határozza meg.
Az első szerepkör képesség fájl található, amely megfelel a kívánt név lesz a csatlakozó felhasználó.

Mivel a szerepkör képesség keresési sorrend nem determinisztikus, ha két vagy több szerepkörrel képességeket rendelkezik ugyanazzal a névvel, **erősen ajánlott** szerepkörrel képességeket egyedi nevük legyen a gépen biztosítása.

### <a name="conditional-access-rules"></a>Feltételes hozzáférési szabályok

Minden felhasználó és csoport a RoleDefinitions mező automatikusan megkapja a JEA-végpont elérését.
Feltételes hozzáférési szabályok lehetővé teszik, hogy finomíthatja a hozzáférést, és nincs hatással a szerepkörök, amelyek hozzá vannak rendelve, amely további biztonsági csoporthoz tartoznak, hogy a felhasználók.
Ez akkor lehet hasznos, ha szeretné integrálni "igény szerinti" emelt szintű hozzáférés felügyeleti megoldás, intelligens kártyás hitelesítés vagy más JEA többtényezős hitelesítési megoldást.

Feltételes hozzáférési szabályok a RequiredGroups mező egy munkamenet-konfigurációs fájlban vannak definiálva.
Itt adhat meg egy kivonattáblát (szükség esetén a beágyazott) használó "És" és "Vagy" kulcsok a szabályok létrehozásához.
Íme néhány példa bemutatja, hogyan használhatja ezt a mezőt:

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
> Feltételes hozzáférési szabályok csak olyan, a Windows PowerShell 5.1-es vagy újabb.

### <a name="other-properties"></a>Egyéb tulajdonságok
Munkamenet konfigurációs fájljainak minden szerepkör képesség fájl anélkül teheti meg, csak lehetővé teszi csatlakozó felhasználók hozzáférést biztosíthat más parancsok is megteheti.
Ha azt szeretné, hogy minden felhasználó hozzáférést adott parancsmagok, függvények és szolgáltatók, megteheti közvetlenül a a munkamenet-konfigurációs fájlt.
A támogatott tulajdonságok a munkamenet-konfigurációs fájl teljes listájának megtekintéséhez futtassa `Get-Help New-PSSessionConfigurationFile -Full`.

## <a name="testing-a-session-configuration-file"></a>Egy munkamenet-konfigurációs fájl tesztelése

A munkamenet konfigurációja használatával tesztelhet a [Test-PSSessionConfigurationFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/test-pssessionconfigurationfile) parancsmagot.
Erősen ajánlott, ha a manuális szövegszerkesztővel annak biztosítása érdekében, a szintaxis helyes FERB fájl szerkesztése tesztelje a munkamenet-konfigurációs fájlban.
Ha egy munkamenet-konfigurációs fájl nem felel meg a teszt, akkor nem fog hozzáférni sikerült regisztrálni a rendszeren.

## <a name="sample-session-configuration-file"></a>Minta munkamenet konfigurációs fájl

Alább egy teljes példát, hogyan hozhat létre, és a egy munkamenet-konfiguráció ellenőrzése a jea-t bemutató.
Vegye figyelembe, hogy a szerepkör-definíciók létrehozása és tárolása a a `$roles` változó a kényelem és olvashatóság érdekében.
Már nem szükséges ehhez.

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

Ha szeretné módosítani egy JEA munkamenet-konfiguráció, beleértve a felhasználók szerepkörökhöz, a hozzárendelés tulajdonságait kell [regisztrációját](register-jea.md#unregistering-jea-configurations) és [újraregisztrálni](register-jea.md) a JEA munkamenet-konfiguráció.
Regisztrálja újra a JEA munkamenet-konfigurációt, használja egy frissített PowerShell munkamenet konfigurációs fájlt, amely tartalmazza a szükséges módosításokat.

## <a name="next-steps"></a>További lépések

- [Regisztrálja a JEA-konfiguráció](register-jea.md)
- [Szerző JEA szerepkörök](role-capabilities.md)