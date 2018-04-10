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
# <a name="jea-session-configurations"></a>JEA Session Configurations

> A következőkre vonatkozik: a Windows PowerShell 5.0

A JEA végpont rendszerre hoz létre, és regisztrálja egy PowerShell-munkamenet konfigurációs fájl egy egyedi módon regisztrálva van.
Munkamenet-konfigurációk meghatározásához *ki* használhatja a JEA végpontot, és melyik szerepkör(ök) rendelkeznek hozzáféréssel.
Szintén definiálnia globális beállítások felhasználói szerepköröket a JEA-munkamenetben.

Ez a témakör ismerteti, hogyan hozzon létre egy PowerShell-munkamenet konfigurációs fájlt, és a JEA végpontjának regisztrálása.

## <a name="create-a-session-configuration-file"></a>Egy munkamenet-konfigurációs fájl létrehozása

Ahhoz, hogy a JEA végpontjának regisztrálása, meg kell adnia, hogyan kell konfigurálni, hogy a végpont.
Nincsenek a kell figyelembe venni, a legfontosabb mely, amely nem a JEA végpont hozzáféréssel rendelkező, mely szerepköröket fogják számos lehetőségük van hozzárendelve, mely identitás JEA használja a színfalak, és mi lesz a JEA végpont nevét.
Ezek az összes meghatározása a PowerShell munkamenetben konfigurációs fájlt, amely PowerShell adatfájlt befejezi .pssc kiterjesztéssel.

A JEA végpontokhoz üres munkamenet konfigurációs fájl létrehozásához futtassa a következő parancsot.

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\MyJEAEndpoint.pssc
```

> [!TIP]
> A leggyakoribb konfigurációs beállítások szerepelnek a üres fájl alapértelmezés szerint.
> Használja a `-Full` kapcsolót, hogy az összes alkalmazható beállításait adja meg a létrehozott FERB.

Szövegszerkesztőben nyissa meg a munkamenet-konfigurációs fájlt.
A `-SessionType RestrictedRemoteServer` mező jelzi, hogy a munkamenet-konfiguráció által használandó JEA biztonságos kezelésére.
Munkamenetet konfigurálta így fog működni [NoLanguage mód](https://technet.microsoft.com/library/dn433292.aspx) , és csak a következő 8 alapértelmezett parancsokat (és aliasok) érhető el:

- Törölje az állomás (cls, törölje a jelet)
- Kilépés-PSSession (exsn, kilépési)
- Get-Command (gcm)
- Get-FormatData
- Get-Help
- Mértékobjektumot (mérték)
- Kimenő alapértelmezett
- Select-Object (kijelölés)

Nincs PowerShell szolgáltató elérhető, sem pedig a bármely külső programokat (végrehajtható fájlok, parancsfájlok stb.).

A JEA munkamenet konfigurálása érdemes több más területen is.
Azok a következő szakaszok ismertetnek.

### <a name="choose-the-jea-identity"></a>Válassza ki a JEA identitás

A háttérben JEA kell a csatlakoztatott felhasználói parancsok futtatásakor identitás (fiók).
Eldöntheti, melyik identitás JEA fogja használni a munkamenet-konfigurációs fájlban.

#### <a name="local-virtual-account"></a>Helyi virtuális fiók

Ha a szerepköröket, a JEA végpont által támogatott összes használatával kezelheti a helyi számítógépen, és egy helyi rendszergazdai fiók elegendő ahhoz, hogy a parancsok sikeresen futtatni, konfigurálnia kell a JEA egy helyi virtuális fiók használatára.
A virtuális fiókok ideiglenes fiókot, amely egy adott felhasználónak egyedi és a PowerShell-munkamenetet időtartama csak az utolsó olyan.
Egy tagkiszolgáló vagy munkaállomás virtuális fiókok tartoznak a helyi számítógép **rendszergazdák** csoportot, és a legtöbb rendszer erőforrások elérésére.
Az Active Directory tartományvezérlőn lévő virtuális fiókokat a tartományhoz tartoznak **Tartománygazdák** csoport.

```powershell
# Setting the session to use a virtual account
RunAsVirtualAccount = $true
```

Ha a szerepköröket, a munkamenet-konfiguráció által támogatott nincs szükség ilyen széles körű jogosultsággal, opcionálisan megadhat a biztonsági csoportokat, amelyhez a virtuális fiók fog tartozni.
Egy olyan tagkiszolgáló vagy munkaállomáson a megadott biztonsági csoportokban helyi csoportok nem a tartományból kell lennie.

Ha meg van határozva egy vagy több biztonsági csoportot, a virtuális fiók már nem fog tartozni a helyi vagy tartományi rendszergazdák csoportnak.

```powershell
# Setting the session to use a virtual account that only belongs to the NetworkOperator and NetworkAuditor local groups
RunAsVirtualAccount = $true
RunAsVirtualAccountGroups = 'NetworkOperator', 'NetworkAuditor'
```

#### <a name="group-managed-service-account"></a>Csoportosan felügyelt szolgáltatásfiók


A JEA felhasználói hozzáférést hálózati erőforrások, például más gépek vagy webes szolgáltatásokból igénylő forgatókönyvek esetén a csoportosan felügyelt szolgáltatásfiókjait (gMSA) egy megfelelő identitás használatára.
csoportosan felügyelt szolgáltatásfiók fiókok biztosítják a tartomány identitása bármelyik olyan gépen a tartományon belüli erőforrásokon hitelesítéséhez használható.
A jogosultságok a csoportosan felügyelt szolgáltatásfiók biztosít azt határozza meg az erőforrások elérésére.
Nem automatikusan fog rendszergazdai jogosultságai a gépeket vagy szolgáltatásokat kivéve, ha a számítógép vagy szolgáltatás-rendszergazda explicit módon megadta a csoportosan felügyelt szolgáltatásfiókok rendszergazdai jogosultságokkal.

```powershell
# Configure JEA sessions to use the gMSA account in the local computer's domain with the sAMAccountName of 'MyJEAgMSA'
GroupManagedServiceAccount = 'Domain\MyJEAgMSA'
```

csoportosan felügyelt szolgáltatásfiók fiókok csak akkor használja, ha hálózati erőforrások eléréséhez szükség néhány lehetnek az okai:

- Nyomon követését műveletek egy felhasználó számára a csoportosan felügyelt szolgáltatásfiók használata, mivel minden felhasználó közösen használja az ugyanazon futtató identitás nehezebb. Szüksége lesz a további részleteket a PowerShell-munkamenethez ki és a naplók felhasználók összefüggéseket azok a műveletek.

- A csoportosan felügyelt szolgáltatásfiók hozzáférhetett számos hálózati erőforrások, amelyek a csatlakozó felhasználó nem kell a hozzáférést. Mindig próbálja hatályos engedélyek korlátozása egy JEA munkamenet hajtsa végre a legalacsonyabb jogosultsági szint elvét.

> [!NOTE]
> Csoportosan felügyelt szolgáltatásfiókok csak rendelkezésre állnak a Windows PowerShell 5.1 vagy újabb és a tartományhoz csatlakoztatott számítógépeken.


#### <a name="more-information-about-run-as-users"></a>További információ a futtató felhasználók

Identitások és hogyan azok tényező be a biztonsági munkamenet JEA futtató további információt megtalálhatók a [biztonsági szempontok](security-considerations.md) cikk.

### <a name="session-transcripts"></a>Munkamenet ki

Javasoljuk, hogy konfigurálja a felhasználói munkamenetek automatikus rögzítése átiratai JEA munkamenet konfigurációs fájlt.
PowerShell-munkamenethez ki a csatlakozó felhasználó, a hozzájuk tartozó identitás futtató információkat tartalmaznak, és a felhasználó által futtatott parancsok.
Akkor lehet hasznos, ha szeretné tudni végző felhasználók listáját egy adott módosítását a rendszer egy naplózási csoportnak.

Automatikus írjanak elő konfigurálása a munkamenet-konfigurációs fájlban, adja meg a mappa elérési útja a ki kell tárolásához.

```powershell
TranscriptDirectory = 'C:\ProgramData\JEAConfiguration\Transcripts'
```

A megadott mappába kell konfigurálni, hogy a felhasználók a módosítsa vagy törölje az összes adatot.
Ki a mappát a helyi rendszer fiók, amelyhez olvasási és írási hozzáféréssel a könyvtárhoz rögzíti.
Az általános jogú felhasználók nem hozzáféréssel kell rendelkeznie a mappához, és biztonsági rendszergazdák korlátozott számú naplózási a ki hozzáféréssel kell rendelkeznie.

### <a name="user-drive"></a>Felhasználói meghajtó

Ha a csatlakozó felhasználók kell másolnia a fájlokat a JEA végpont és a parancs futtatásához, engedélyezheti a felhasználói meghajtó a munkamenet-konfigurációs fájlban.
A felhasználó meghajtó egy [PSDrive](https://msdn.microsoft.com/powershell/scripting/getting-started/cookbooks/managing-windows-powershell-drives) , amely egy egyedi mappát az egyes csatlakozó felhasználó van leképezve.
Ez a mappa adhatja őket a rendszer, és a fájlok adjon hozzáférést a teljes fájlrendszer vagy a fájlrendszer szolgáltató kitettségének nélkül történő másolását funkcionál.
A felhasználó meghajtó tartalma állandó olyan helyzetekben, ahol lehet megszakítani hálózati kapcsolat munkamenetei között.

```powershell
MountUserDrive = $true
```

Alapértelmezés szerint a felhasználói meghajtó teszi legfeljebb 50MB / felhasználói adatok tárolásához.
A felhasználó felhasználhat az adatok mennyisége korlátozhatja a *UserDriveMaximumSize* mező.

```powershell
# Enables the user drive with a per-user limit of 500MB (524288000 bytes)
MountUserDrive = $true
UserDriveMaximumSize = 524288000
```

Ha nem szeretné, hogy a felhasználó meghajtó legyen állandó adatokat, konfigurálhatja egy ütemezett feladatot a rendszer automatikusan a mappa karbantartása éjszakánként.

> [!NOTE]
> A felhasználó meghajtó csak a Windows PowerShell 5.1-es vagy újabb.

### <a name="role-definitions"></a>Szerepkör-definíciók

A munkamenet-konfigurációs fájlban található szerepkör-definíciók megadása leképezése *felhasználók* való *szerepkörök*.
Minden felhasználó vagy csoport szerepel ebben a mezőben automatikusan engedélyt kap a JEA végponthoz való regisztrálásakor kerül.
Minden felhasználó vagy csoport is meg lehet adni a kivonattábla kulcsként csak egyszer, de több szerepkörhöz is hozzárendelhető.
A szerepkör funkció nevét kell lennie a szerepkör funkció .psrc kiterjesztés nélküli fájl nevét.

```powershell
RoleDefinitions = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}
```

Ha egy felhasználó több csoporthoz a szerepkör-definíció tartozik, az egyes szerepkörök elérésére fogja használni.
Ha két szerepkörök ugyanazon parancsmagok hozzáférést, a leghatékonyabb paraméterkészletet alakítanak kapnak a felhasználó számára.

Ha a szerepkör-definíciók mezőben adja meg a helyi felhasználókat és csoportokat, ügyeljen arra, hogy a számítógépnév (nem *localhost* vagy *.*) a fordított perjel előtt.
A számítógépnév vizsgálatával ellenőrizheti a `$env:computername` változó.

```powershell
RoleDefinitions = @{
    'MyComputerName\MyLocalGroup' = @{ RoleCapabilities = 'DnsAuditor' }
}
```

### <a name="role-capability-search-order"></a>Szerepkör funkció keresési sorrendje
Látható a fenti példában, szerepkör-képességek a szerepkör funkció fájl egyszerű név (fájlnév-kiterjesztés nélküli) által hivatkozott.
Ha több szerepkör képességek érhetők el a rendszer a strukturálatlan néven, a PowerShell használata a az implicit keresési sorrendje válassza ki a hatékony szerepkör funkció fájlt.
A következőket hajtja végre **nem** hozzáférést szerepkör funkció fájlokhoz ugyanazzal a névvel.

JEA használja a `$env:PSModulePath` környezeti változó határozza meg, mely elérési szerepkör funkció fájlok vizsgálatára.
Minden egyes adott elérési útján JEA keresni, amely tartalmaz egy "RoleCapabilities" almappát érvényes PowerShell-modulok.
Csakúgy, mint a modulok importálása, JEA inkább szerepkör képességeket kínál, amelyek a Windows ilyen nevű egyéni szerepkör-funkciókat.
Az összes többi mappaelnevezési ütközéseket sorrend Windows számba veszi a könyvtár (nem garantált betűrendben) sorrendje határozza meg.
Az első szerepkör funkció fájl található, amely megfelel a kívánt nevet fogja használni a csatlakozó felhasználó.

Mivel a szerepkör funkció keresési sorrendje nem determinisztikus, amikor két vagy több szerepkör képességek megosztása azonos nevű, **erősen ajánlott** szerepkör képességek egyedi nevük legyen a számítógépen biztosítása.

### <a name="conditional-access-rules"></a>Feltételes hozzáférési szabályai

Összes felhasználók és csoportok a RoleDefinitions mező automatikusan JEA végpontokkal való hozzáférést kapnak.
Feltételes hozzáférési szabályok lehetővé teszik finomíthatja a hozzáférés, és további biztonsági csoportokat, amelyek nem érintik a szerepkörök, amelyek a hozzárendelés tartozik, a felhasználóknak.
Ez akkor lehet hasznos, ha szeretné integrálni "csak az idő" emelt szintű hozzáférés felügyeleti megoldás, intelligens kártyás hitelesítés vagy más JEA többtényezős hitelesítés megoldást.

Feltételes hozzáférési szabályok vannak meghatározva, a RequiredGroups mezőben egy munkamenet-konfigurációs fájlban.
Itt megadhatja egy kivonattáblát (ha szükséges a beágyazott) használó "És" és "Vagy" kulcsok készítse el szabályait.
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

> [!NOTE]
> Feltételes hozzáférési szabályok csak olyan, a Windows PowerShell 5.1-es vagy újabb.

### <a name="other-properties"></a>Egyéb tulajdonságai
Munkamenet-konfigurációs fájlok is elérhető műveletek mindegyikét szerepkör funkció fájlt azonban csak a csatlakozó felhasználók hozzáférésének különböző parancsok képessége nélkül.
Ha azt szeretné, hogy engedélyezése minden felhasználó hozzáférést adott parancsmagok, függvények és szolgáltatók, ehhez jobbra a munkamenet-konfigurációs fájlban.
A támogatott tulajdonságok a munkamenet-konfigurációs fájl teljes listájának megtekintéséhez futtassa a `Get-Help New-PSSessionConfigurationFile -Full`.

## <a name="testing-a-session-configuration-file"></a>Egy munkamenet-konfigurációs fájl tesztelése

Egy munkamenet konfigurációs segítségével tesztelheti a [teszt-PSSessionConfigurationFile](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/test-pssessionconfigurationfile) parancsmag.
Erősen ajánlott, ha módosította a FERB fájlt egy szövegszerkesztő segítségével manuálisan annak érdekében, hogy a megfelelő-e szintaxisa tesztelje a munkamenet-konfigurációs fájlban.
Ha egy munkamenet-konfigurációs fájl nem felel meg a teszt, akkor nem fog hozzáférni a rendszer sikeresen regisztrálni kell.

## <a name="sample-session-configuration-file"></a>A minta munkamenet konfigurációs fájl

Alatt egy teljes példa bemutatja, hogyan hozzon létre és JEA egy munkamenet-konfiguráció érvényesítése.
Vegye figyelembe, hogy a szerepkör-definíciók létrehozva és tárolva a `$roles` változó a kényelem és olvashatóság érdekében.
A követelmény, hogy ehhez nincs.

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

Ha módosítania kell a JEA munkamenet-konfiguráció, beleértve a felhasználói szerepkör, a hozzárendelés tulajdonságait kell [regisztrációját](register-jea.md#unregistering-jea-configurations) és [újraregisztrálni](register-jea.md) JEA munkamenet-konfigurációt.
Regisztrálja újra a JEA munkamenet-konfiguráció, ha egy frissített PowerShell munkamenetben konfigurációs fájlt használja, amely tartalmazza a szükséges módosításokat.

## <a name="next-steps"></a>További lépések

- [A JEA konfigurációs regisztrálása](register-jea.md)
- [Szerző JEA szerepkörök](role-capabilities.md)