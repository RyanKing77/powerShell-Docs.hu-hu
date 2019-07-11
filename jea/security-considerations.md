---
ms.date: 07/10/2019
keywords: a jea, powershell, biztonsági
title: A JEA biztonsági szempontok
ms.openlocfilehash: befc24fec368c4f6d60477daf63bf17e9431133e
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726588"
---
# <a name="jea-security-considerations"></a>A JEA biztonsági szempontok

A JEA segítségével javíthatja biztonsági helyzetét a gépeken állandó rendszergazdák számának csökkentésével. A JEA PowerShell munkamenet-konfigurációt használ, hozzon létre egy új belépési pont a felhasználók számára a rendszer kezelését. Felhasználók, akiknek szükség van a felügyeleti feladatokat hajthat végre a gép emelt szintű, de nem korlátlan hozzáférés adható a JEA-végpont elérését. A JEA lehetővé teszi, hogy ezek a felhasználók rendszergazdai parancsok teljes rendszergazdai hozzáférés nélkül futtathat, mivel a magas jogosultsági szintű biztonsági csoportokból majd eltávolíthatja a felhasználók.

## <a name="run-as-account"></a>Futtató fiók

Minden a JEA-végpont tartalmaz egy kijelölt **futtató** fiókot. Ez az a fiók, amely alatt a rendszer végrehajtja a műveleteket a csatlakozó felhasználó. Ez a fiók akkor lehet beállítani a [munkamenet konfigurációs fájl](session-configurations.md), és a választott fiók rendelkezik a jelentős hatással a végpont biztonságát.

**A virtuális fiókok** konfigurálásának az ajánlott módszer a **futtató** fiókot. A virtuális fiókok olyan egyszeri, ideiglenes helyi felhasználói fiókok a csatlakozó felhasználó JEA a munkamenet időtartama alatt használni létrehozott. Amint azok a munkamenet meg lett szakítva, a virtuális fiók megsemmisül, és többé nem használható. A kapcsolódó felhasználó nem ismeri a virtuális fiók hitelesítő adatait. A virtuális fiók nem használható a rendszer keresztül más módon, például a távoli asztal és a egy korlátozás PowerShell-végpont elérésére.

Alapértelmezés szerint a virtuális fiókok tartoznak a helyi **rendszergazdák** csoport a számítógépen. Ezáltal őket teljes jogosultságokkal kezelése semmit, a rendszer, de nincs jogosultsága a hálózaton lévő erőforrások kezelésére.
Más gépekkel hitelesítésekor a felhasználói környezetet, hogy a helyi számítógépfiók, nem a virtuális fiók.

Tartományvezérlő el egy különleges esetben, mivel nincs helyi **rendszergazdák** csoport. Ehelyett a virtuális fiókok tartoznak **Tartománygazdák** és felügyelheti a tartományvezérlő a címtárszolgáltatások. A tartomány identitás továbbra is használatra korlátozva a tartományvezérlőn, ahol a JEA-munkamenet példányosítása volt. Bármely hálózati hozzáférés úgy tűnik, hogy a tartományvezérlő számítógép-objektumot inkább származnak.

Mindkét esetben előfordulhat, hogy explicit módon meghatározni melyik biztonsági csoportok, a virtuális fiók tartozik. Ez akkor célszerű, ha a helyi vagy tartományi rendszergazdai jogosultságok nélkül a feladat elvégezhető. Ha már rendelkezik a rendszergazdák számára meghatározott biztonsági csoport, adja meg a virtuális fiók tagság ehhez a csoporthoz. Virtuális fiók csoporttagság helyi biztonsági csoportokat a munkaállomáson és a tagkiszolgálók korlátozódik. A tartományvezérlőkön a virtuális fiókok tartományi biztonsági csoportok tagjának kell lennie.
Miután a virtuális fiók van adva egy vagy több biztonsági csoportot, már nem tartozik alapértelmezett csoportok (helyi vagy tartományi rendszergazdák).

A következő táblázat összefoglalja a lehetséges konfigurációs beállításokat és az eredményül kapott virtuális fiókok engedélyeit:

|        Számítógép típusa         | Virtuális fiók csoport konfigurálása |                   Helyi felhasználói környezet                    | Hálózati felhasználói környezet |
| ---------------------------- | ----------------------------------- | ------------------------------------------------------- | -------------------- |
| Tartományvezérlő            | Alapértelmezett                             | Tartományi felhasználó, tagja "*tartomány*\Domain rendszergazdák         | Számítógépfiók     |
| Tartományvezérlő            | A és B tartományi csoportok               | Tartományi felhasználó, tagja "*tartomány*\A ','*tartomány*\B"       | Számítógépfiók     |
| Tagkiszolgáló vagy munkaállomás | Alapértelmezett                             | Helyi felhasználói, tagja "*beépített*\Administrators'        | Számítógépfiók     |
| Tagkiszolgáló vagy munkaállomás | C és a D helyi csoportok                | Helyi felhasználói, tagja "*számítógép*\C" és "*számítógép*\D" | Számítógépfiók     |

Ha biztonsági naplózási eseményeket és a alkalmazás eseménynaplóit, láthatja, hogy minden egyes JEA felhasználói munkamenet egy egyedi virtuális fiók rendelkezik-e. Ez a fiók egyedi segítségével nyomon követheti a JEA-végpont felhasználói műveletek térjen vissza az eredeti felhasználó, aki a parancsot futtatta. Virtuális fiók neve követi a `WinRM Virtual Users\WinRM_VA_<ACCOUNTNUMBER>_<DOMAIN>_<sAMAccountName>` például, ha felhasználói **Alice** tartományban **Contoso** újraindítja a szolgáltatást a JEA-végpont, a bármely szolgáltatásvezérlő társított felhasználónevet események lenne `WinRM Virtual Users\WinRM_VA_1_contoso_alice`.

**Csoportosan felügyelt szolgáltatásfiókok (csoportosan felügyelt szolgáltatásfiókokat)** akkor hasznos, ha egy tagkiszolgálóra hozzáféréssel kell rendelkeznie a hálózati erőforrásokhoz a JEA-munkamenetben. Ha például a JEA-végpont használatakor egy másik gépen futó REST API-szolgáltatásban való hozzáférés szabályozásához. Egyszerűen írhat olyan funkciók, a REST API-k meghívásához, de egy hálózati azonosságát az API-hitelesítésre van szüksége. Csoportosan felügyelt szolgáltatásfiók használata lehetővé teszi, a második Ugrás irányítást, amelyen számítógépek fiókot is használhatja. A csoportosan felügyelt szolgáltatásfiókot, a hatályos engedélyek határozzák meg a biztonsági csoportok (helyi vagy tartományi), amelyhez a csoportosan felügyelt szolgáltatásfiók tartozik.

A JEA-végpont csoportosan felügyelt szolgáltatásfiók használatára van konfigurálva, amikor minden JEA felhasználók műveleteinek úgy tűnik, hogy az azonos gMSA származnak. Vissza a megadott felhasználó követési műveleteket csak úgy, hogy azonosítsa azokat a parancsokat futtatni egy PowerShell-munkamenet átiratot.

**Hitelesítő adatok pass-** akkor használjuk, ha nem ad meg egy **futtató** fiókot. PowerShell-parancsok futtatásához a távoli kiszolgálón a csatlakozó felhasználó hitelesítő adatait használja. Ez megköveteli, hogy a csatlakozó felhasználó közvetlen hozzáférést biztosítson a kiemelt jogosultságú felügyeleti csoportokhoz. Ez a konfiguráció **nem** JEA ajánlott. Ha a kapcsolódó felhasználó már rendelkezik rendszergazdai jogosultságokkal, JEA elkerülése érdekében, és kezelheti keresztül más, korlátozás azt jelenti, hogy a rendszer. További információkért tekintse meg az alábbi hogyan [JEA rendszergazdák ellen védelmet biztosító nem](#jea-doesnt-protect-against-admins).

**Standard szintű Futtatás mint fiók** meg lehet adni egy felhasználói fiókot, amely alatt a teljes PowerShell-munkamenetben futtatja. Munkamenet-konfigurációk használatával rögzített **futtató** fiókok (az a `-RunAsCredential` paraméter) nem a JEA-t támogató. Szerepkör-definíciók nem várt módon működik. Minden felhasználó jogosult a végpont elérésére ugyanarra a szerepkörre van hozzárendelve.

Ne használja a **RunAsCredential** a JEA-végpont mert nehéz nyomkövetési műveletek vissza az adott felhasználókat, és hiányzik támogatása felhasználók leképezése szerepkörök.

## <a name="winrm-endpoint-acl"></a>WinRM Endpoint ACL

PowerShell távoli eljáráshívás végpontokkal rendszeres, minden a JEA-végpont rendelkezik egy külön hozzáférés-vezérlési lista (ACL), amely szabályozza, akik hitelesítheti a JEA-végponttal. Ha nem megfelelően konfigurált, megbízható felhasználók nem lehet tudni hozzáférni a JEA-végpont, és nem megbízható felhasználók rendelkezhetnek hozzáféréssel. A WinRM ACL nem befolyásolja a felhasználók szerepkörökhöz JEA leképezés. Leképezés vezérli a **RoleDefinitions** mező a munkamenet-konfigurációs fájlban használt végpont.

Alapértelmezés szerint a JEA-végpont rendelkezik több szerepkör-szolgáltatásait, amikor a Rendszerfelügyeleti webszolgáltatások ACL van konfigurálva az összes hozzárendelt felhasználók férhessenek hozzá. Ha például konfigurált, a következő parancsokkal JEA munkamenet teljes hozzáférést biztosít `CONTOSO\JEA_Lev1` és `CONTOSO\JEA_Lev2`.

```powershell
$roles = @{ 'CONTOSO\JEA_Lev1' = 'Lev1Role'; 'CONTOSO\JEA_Lev2' = 'Lev2Role' }
New-PSSessionConfigurationFile -Path '.\jea.pssc' -SessionType RestrictedRemoteServer -RoleDefinitions $roles -RunAsVirtualAccount
Register-PSSessionConfiguration -Path '.\jea.pssc' -Name 'MyJEAEndpoint'
```

A felhasználói engedélyek naplózhatók a [Get-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/get-pssessionconfiguration) parancsmagot.

```powershell
Get-PSSessionConfiguration -Name 'MyJEAEndpoint' | Select-Object Permission
```

```Output
Permission
----------
CONTOSO\JEA_Lev1 AccessAllowed
CONTOSO\JEA_Lev2 AccessAllowed
```

Szeretné módosítani, hogy mely felhasználók férhessenek, futtathatja az alábbiak `Set-PSSessionConfiguration -Name 'MyJEAEndpoint' -ShowSecurityDescriptorUI` számára egy interaktív kérdés vagy `Set-PSSessionConfiguration -Name 'MyJEAEndpoint' -SecurityDescriptorSddl <SDDL string>` engedélyeinek frissítését. A felhasználóknak kell legalább *Invoke* jogok a JEA-végpont elérésére.

Akkor lehet, amely nem egy meghatározott szerepkör hozzárendelése minden hozzáféréssel rendelkező felhasználó JEA-végpont létrehozásához. Ezek a felhasználók JEA munkamenetet, de csak az alapértelmezett parancsmagok hozzáférése. A JEA-végpont a felhasználói engedélyek naplózhatók futtatásával `Get-PSSessionCapability`. További információkért lásd: [naplózás és a JEA-jelentések](audit-and-report.md).

## <a name="least-privilege-roles"></a>Legkisebb jogosultság szerepkörök

JEA szerepkörök tervezésekor fontos megjegyezni, hogy a háttérben futó virtuális és a csoportosan felügyelt szolgáltatásfiókokat is ugyanolyan korlátlan hozzáféréssel rendelkezik a helyi gépen. A JEA szerepköri funkciók segítségével korlátozhatja a parancsok és a kiemelt jogosultságú környezetben futó alkalmazásokhoz.
Nem megfelelően kialakított szerepköröket lehetővé tehetik a veszélyes parancsok, amelyek lehetővé tehetik a JEA határain kívül break, vagy bizalmas információk elérését.

Vegyük példaként a következő szerepkör-képesség bejegyzés:

```powershell
@{
    VisibleCmdlets = 'Microsoft.PowerShell.Management\*-Process'
}
```

Ez a szerepkör funkció lehetővé teszi a felhasználóknak minden olyan PowerShell-parancsmag futtatásához a főnév **folyamat** származó a **Microsoft.PowerShell.Management** modul. Felhasználók valószínűleg eléréséhez, például a parancsmagok `Get-Process` megtekintheti, milyen alkalmazások vannak a rendszeren futó és `Stop-Process` le alkalmazásokat, amelyek nem válaszol. Azonban ez a bejegyzés is lehetővé teszi, hogy `Start-Process`, teljes körű rendszergazda engedélyekkel rendelkező egy tetszőleges program elindításához használható. A program nem szükséges, a rendszer helyben telepítendő. Egy csatlakoztatott felhasználói indítható egy programot, amely lehetővé teszi a felhasználó helyi rendszergazdai jogosultságokat, futtatja a kártevők és más fájlmegosztásból.

A szerepkör funkció biztonságosabb verziója hasonlóan néz ki:

```powershell
@{
    VisibleCmdlets = 'Microsoft.PowerShell.Management\Get-Process', 'Microsoft.PowerShell.Management\Stop-Process'
}
```

Kerülje a helyettesítő karakterek használatával a szerepkörrel képességeket. Ügyeljen arra, hogy rendszeresen [hatékony felhasználói engedélyek naplózási](audit-and-report.md#check-effective-rights-for-a-specific-user) tudni, mely parancsok a felhasználó számára elérhető.

## <a name="jea-doesnt-protect-against-admins"></a>Jea-t nem védi a rendszergazdák ellen

A JEA core alapelveit egyike, hogy lehetővé teszi bizonyos felügyeleti feladatokat hajthat végre, nem rendszergazda. Jea-t rendszergazdai jogosultsággal rendelkező felhasználók nem ellen. Felhasználók, akik tartoznak **Tartománygazdák**, helyi **rendszergazdák**, vagy egyéb magas jogosultsági szintű csoportok megkerülheti a JEA a védelmet egy másik eszközzel. Például ezek sikerült RDP, távoli MMC-konzolt használja, vagy bejelentkeznie korlátozás PowerShell végpontok csatlakozni. Emellett a rendszer a helyi rendszergazdák módosíthatja a további felhasználók, vagy módosítani a szerepkör képes kiterjeszteni a felhasználók mit tehetnek a JEA-munkamenetet a JEA-konfigurációk. Fontos a JEA-felhasználók kiterjesztett engedéllyel vannak-e a rendszer az emelt szintű hozzáférés más módon kiértékeléséhez.

Általános gyakorlat, hogy rendszeres napi karbantartás jea-t használnak, és a just-in-time, emelt szintű hozzáférés-kezelési megoldása, amely lehetővé teszi a felhasználóknak ideiglenesen a helyi rendszergazdák vészhelyzet válnak. Ezzel biztosíthatja a felhasználók nincsenek állandó rendszergazdák, a rendszer, de ezeket a jogokat kaphat, ha, és csak akkor végezze el egy munkafolyamatot, amely a dokumentumok használata során ezeket az engedélyeket.
