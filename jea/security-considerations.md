---
ms.date: 06/12/2017
keywords: jea, a powershell, a biztonsági
title: JEA biztonsági megfontolások
ms.openlocfilehash: 46ea5cc3e9bc7b6759524aa466e900950a6dee26
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="jea-security-considerations"></a>JEA biztonsági megfontolások

> A következőkre vonatkozik: a Windows PowerShell 5.0

JEA segít csökkenteni a gépeken állandó rendszergazdák számát javítják a biztonságot.
Igen, hozzon létre egy új belépési pont a felhasználók kezeléséhez a rendszerben (a PowerShell munkamenet-konfiguráció), ami szorosan zárolta alapértelmezett való visszaélés megakadályozására.
Felhasználók, akik néhány, de nem korlátlan hozzáférést a felügyeleti feladatok a számítógéphez is hozzáférést kell biztosítani a JEA végpont.
Mivel JEA lehetővé teszi őket anélkül, hogy közvetlenül a rendszergazdai hozzáférés admin parancsok futtatásához, majd eltávolíthat azoknak a felhasználóknak kiemelt jogosultságokkal rendelkező biztonsági csoportok (ügyeljen azokat az általános jogú felhasználók).

Ez a témakör ismerteti a JEA biztonsági modellt és ajánlott eljárások részletesebben.

## <a name="run-as-account"></a>Futtató fiók

Minden egyes JEA végpont rendelkezik a kijelölt "Futtatás mint" fiók, amely az a fiók, amely alatt a csatlakozó felhasználó végrehajt.
Ez a fiók akkor szeretné tenni a konfigurálását a [munkamenet konfigurációs fájl](session-configurations.md), és úgy dönt, a fiók biztonsága érdekében a végpont rendelkezik a jelentős hatással.

**A virtuális fiókok** az ajánlott módszer az, hogy a futtató fiók konfigurálása.
A virtuális fiókok egyszeri, ideiglenes helyi fiók, a kapcsolódó felhasználó a munkamenet időtartama alatt a JEA közbeni létrehozott is.
Amint a munkamenet megszakadt, a virtuális fiók meg kell semmisíteni, és többé már nem használható.
A csatlakozó felhasználó nem tudja a virtuális fiók hitelesítő adatait, és nem a virtuális fiókot használja a rendszer egyéb eszközzel, például a távoli asztal vagy a korlátozás nélküli PowerShell végpontot eléréséhez.

Alapértelmezés szerint a virtuális fiókok a helyi rendszergazdák csoporthoz tartozik.
Így azok teljes körű jogosultságot kezelése semmit a rendszeren, de nincs jogosultsága a hálózaton lévő erőforrások kezelésére.
Más gépekkel hitelesítésekor a felhasználói környezet, amely a helyi számítógépfiók, nem a virtuális fiók lesz.

Tartományvezérlők egy különleges esetben, mivel nincs a helyi rendszergazdák csoporthoz.
Ehelyett virtuális fiókok tartományi rendszergazdák inkább tartozik, és kezelheti a tartományvezérlő a címtárszolgáltatások.
A tartomány identitása korlátozódik továbbra is a tartományvezérlőről, ahol a JEA munkamenet példánya létre lett hozva, és a hálózati hozzáférés jelennek származnia inkább a tartományvezérlő számítógép-objektumot.

Mindkét esetben közvetlenül is definiálhat melyik biztonsági csoportokat, a virtuális fiók kell tartoznia.
Ez akkor célszerű, ha a helyi vagy tartományi rendszergazdai jogosultságok nélkül a feladat végez végezhető.
Ha már van definiálva a rendszergazdák biztonsági csoport, egyszerűen biztosíthat a virtuális fiók tagságát a engedélyt kell adnia azt a csoportot.
Virtuális fiók csoporttagság korlátozódik munkaállomás és a tagkiszolgálók helyi biztonsági csoport, de egy olyan tartományvezérlő csak lehet, hogy tartományi biztonsági csoportok tagjai.
Ha megad egy vagy több biztonsági csoportot a virtuális fiók tartozik, azt fogja már nem tartozik alapértelmezett csoportok (a helyi rendszergazda vagy a tartományi rendszergazda).

Az alábbi táblázat összefoglalja a konfigurációs beállítások és az eredményül kapott virtuális fiókok engedélyeit

Számítógép típusa                | Virtuális fiók csoport konfigurálása | Helyi felhasználói környezet                                      | Hálózati felhasználói környezet
-----------------------------|-------------------------------------|---------------------------------------------------------|--------------------------------------------------
Tartományvezérlő            | Alapértelmezett                             | Tartományi felhasználó, tagja "*tartomány*\Domain'         | Számítógépfiók
Tartományvezérlő            | A és B tartományi csoportok               | Tartományi felhasználó, tagja "*tartomány*\A ','*tartomány*\B"       | Számítógépfiók
Tagkiszolgáló vagy munkaállomás | Alapértelmezett                             | Helyi felhasználói, tagja "*beépített*\Administrators'        | Számítógépfiók
Tagkiszolgáló vagy munkaállomás | Helyi csoportok C és D                | Helyi felhasználói, tagja "*számítógép*\C" és "*számítógép*\D" | Számítógépfiók

Ha megnézzük biztonsági naplózási eseményeket és az alkalmazás eseménynaplóiban, látni fogja, hogy minden JEA felhasználói munkamenet egy egyedi virtuális fiók rendelkezik-e.
Ezzel a megoldással követi nyomon a műveleteket a JEA végpont vissza az eredeti felhasználó futtatta a parancsot.
Virtuális fiók nevét a formátumot követi "a Rendszerfelügyeleti webszolgáltatások virtuális felhasználók\\WinRM\_VA\_*ACCOUNTNUMBER*\_*tartomány* \_ *sAMAccountName*"például, ha a felhasználói tartományban"Contoso"a" Alice"JEA-végpont szolgáltatás újraindul, a service control manager eseményeket társított felhasználónevet lenne" Rendszerfelügyeleti webszolgáltatások virtuális felhasználók\\WinRM\_ VA\_1\_contoso\_alice ".


**A felügyelt szolgáltatásfiókok (gmsa-k) csoport** hasznosak, ha tagkiszolgálóra kell biztosítani a hálózati erőforrások eléréséhez a JEA-munkamenetben.
Ez egy példa használati eset egy JEA végpont, amellyel egy másik gépre tárolt REST API való hozzáférés szabályozása.
Akkor is könnyen funkciók adja meg a kívánt indítások a REST API-t, de hitelesítéséhez az API-hoz, egy hálózati azonosító kell írni.
A csoportosan felügyelt szolgáltatásfiók használata lehetővé teszi, az "Ugrás" közben továbbra is fennáll a vezérlő, amelyben a számítógépek használni tudják a fiókot.
A csoportosan felügyelt szolgáltatásfiók a hatályos engedélyek határozzák meg a biztonsági csoportok (helyi vagy tartományi), amelyhez a csoportosan felügyelt szolgáltatásfiók tartozik.

A JEA végpont a csoportosan felügyelt szolgáltatásfiók használatára van konfigurálva, JEA felhasználók műveletek után megjelenik ugyanabban a csoportban származnia felügyelt szolgáltatásfiók.
A csak vezethető vissza az adott felhasználó műveletek, azonosításához futtassa a PowerShell-munkamenet Beszélgetés szövegének parancsok készlete.

**Pass-hitelesítő adatok** akkor használatosak, ha nem adja meg a futtató fiókot, és szeretné, hogy PowerShell-parancsokat futtatnak majd a távoli kiszolgáló a csatlakozó felhasználó hitelesítő adatai segítségével.
Ez a konfiguráció *nem* JEA az ajánlott, mivel azt igényel a csatlakozó felhasználó közvetlen hozzáférést adhat, a kiemelt felügyeleti csoportokhoz.
Ha a kapcsolódó felhasználó már rendszergazdai jogosultságokkal rendelkezik, ugyanakkor JEA teljesen elkerülése és kezelhetik az keresztül más, korlátozás nélküli azt jelenti, hogy a rendszer.
Az alábbi részben meg, hogyan [JEA nem véd a rendszergazdák](#jea-does-not-protect-against-admins) további információt.

**Standard futtató fiókok** adhatók meg egy felhasználói fiókot, amely alatt a teljes PowerShell-munkamenet futni fog.
Ez fontos különbség, mivel a munkamenet-konfiguráció beállítása rögzített futtató fiók használata (a a `-RunAsCredential` paraméter) nincs JEA-kompatibilis.
Ez azt jelenti, hogy a szerepkör-definíciók nem várt módon működik, és minden felhasználói férhetnek hozzá a végpont rendeli ugyanarra a szerepkörre.

Egy RunAsCredential JEA-végponton műveletek vissza az adott felhasználó és a felhasználók hozzárendelése szerepkörök támogatásának hiányát a nyomkövetés nehézsége miatt ne használjon.

## <a name="winrm-endpoint-acl"></a>A Rendszerfelügyeleti webszolgáltatások végponti ACL-t

Rendszeres PowerShell távoli eljáráshívás végpontokon, JEA végpontok rendelkezik egy különálló hozzáférési szabálygyűjtemény (ACL) állíthat be a Rendszerfelügyeleti webszolgáltatások konfigurációs, amely meghatározza, akik hitelesítheti a JEA-végponthoz.
Ha helytelenül van konfigurálva, nem lehet tudni elérni a JEA végpont megbízható felhasználók és/vagy nem megbízható felhasználók is hozzáférhetnek.
A Rendszerfelügyeleti webszolgáltatások ACL, azonban hatással a a felhasználók hozzárendelése JEA szerepkörök.
Amely vezérli a *RoleDefinitions* mezőjét a rendszer a regisztrált munkamenet konfigurációs fájlban.

Alapértelmezés szerint amikor regisztrál egy JEA végpont egy munkamenet-konfigurációs fájlban és egy vagy több szerepkör képességeit, a Rendszerfelügyeleti webszolgáltatások ACL teszi engedélyezése minden felhasználó hozzárendelése egy vagy több szerepkört a hozzáférést a végpont.
Például az alábbi parancsok használatával konfigurált JEA munkamenet teljes hozzáférést adni *CONTOSO\JEA\_Lev1* és *CONTOSO\JEA\_Lev2*.

```powershell
$roles = @{ 'CONTOSO\JEA_Lev1' = 'Lev1Role'; 'CONTOSO\JEA_Lev2' = 'Lev2Role' }
New-PSSessionConfigurationFile -Path '.\jea.pssc' -SessionType RestrictedRemoteServer -RoleDefinitions $roles -RunAsVirtualAccount
Register-PSSessionConfiguration -Path '.\jea.pssc' -Name 'MyJEAEndpoint'
```

A felhasználói engedélyek naplózhatja a [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) parancsmag.

```powershell
PS C:\> Get-PSSessionConfiguration -Name 'MyJEAEndpoint' | Select-Object Permission

Permission
----------
CONTOSO\JEA_Lev1 AccessAllowed
CONTOSO\JEA_Lev2 AccessAllowed
```

Mely felhasználók férhessenek módosításához futtassa vagy `Set-PSSessionConfiguration -Name 'MyJEAEndpoint' -ShowSecurityDescriptorUI` a egy interaktív kérdés vagy `Set-PSSessionConfiguration -Name 'MyJEAEndpoint' -SecurityDescriptorSddl <SDDL string>` engedélyek frissítése.
Legalább a felhasználóknak kell *Invoke* jogok a JEA-végpont elérésére.

Ha további felhasználók férhetnek hozzá a JEA végpont, de nem sorolhatók be a munkamenet konfigurációs fájljában definiált szerepköröket, akkor nem képes elindítani a JEA-munkamenetet, de az alapértelmezett parancsmagok csak már.
Felhasználói engedélyek egy JEA végpont naplózható futtatásával `Get-PSSessionCapability`.
Tekintse meg a [naplózási és jelentéskészítési összetevője JEA](audit-and-report.md) cikk további információt a naplózás, amelyet a felhasználó parancsok hozzáféréssel rendelkezik a JEA végpont.

## <a name="least-privilege-roles"></a>Legalacsonyabb jogosultsági szerepkörök

JEA szerepkörök tervezésekor fontos megjegyezni, hogy a virtuális vagy csoport felügyelt fiók, amelyen a háttérben gyakran rendelkezik teljes hozzáférést a helyi számítógép kezeléséhez.
JEA szerepkör képességek segítségével korlátozhatja a mi fiók is használható, ha a parancsok és az alkalmazások, amelyek használatával a privilegizált környezetben futtathatók korlátozza.
Nem tervezett szerepkörök lehetővé tehetik a veszélyes parancsok futtatásához, amelyek a JEA határain kívül break, vagy bizalmas információk elérését tehetik lehetővé.

Vegyük példaként a következő szerepkör funkció bejegyzést:

```powershell
@{
    VisibleCmdlets = 'Microsoft.PowerShell.Management\*-Process'
}
```

Ez a szerepkör funkció lehetővé teszi a felhasználóknak a főnév "Folyamat" PowerShell-parancsmag futtatásához a Microsoft.PowerShell.Management modulból.
Felhasználók valószínűleg például parancsmagok eléréséhez `Get-Process` megérteni, hogy milyen alkalmazások vannak a rendszeren futó és `Stop-Process` leállítani az összes lefagyott alkalmazások.
Azonban ez a bejegyzés is lehetővé teszi, hogy `Start-Process`, teljes körű rendszergazdai jogosultságokkal rendelkező egy tetszőleges program elindításához használható.
A program nem szükséges helyileg kell telepíteni a rendszerre, az ellenfél sikerült egyszerűen indítsa el a program egy fájlmegosztáson, amely a kapcsolódó felhasználói helyi rendszergazdai jogosultságokat, fut kártevő és további. "

A szerepkör funkció biztonságosabb verziója alábbihoz hasonlóan fog kinézni:

```powershell
@{
    VisibleCmdlets = 'Microsoft.PowerShell.Management\Get-Process', 'Microsoft.PowerShell.Management\Stop-Process'
}
```

Kerülje a helyettesítő karaktereket a szerepkör képességeit, és ügyeljen arra, hogy [hatékony felhasználói engedélyek naplózási](audit-and-report.md#check-effective-rights-for-a-specific-user) rendszeresen megértéséhez, amely a parancsokat egy felhasználó hozzáfér.

## <a name="jea-does-not-protect-against-admins"></a>JEA nem véd a rendszergazdák

A JEA core alapelvek egyik, hogy lehetővé teszi a nem rendszergazda végrehajtásához *néhány* rendszergazdai feladatok elvégzéséhez.
JEA nem véd azok, akik már rendelkezik rendszergazdai jogosultságokkal.
Felhasználók tartozó "tartományi rendszergazdák", "helyi rendszergazdák,", vagy más kiemelt jogosultságokkal rendelkező csoportok a környezetben is elkerülése érdekében JEA a védelmet a gépet egy másik eszközzel való aláírásával.
Azok volt, például jelentkezzen be az RDP, használjon távoli MMC-konzolt, vagy csatlakoztassa korlátozás nélküli PowerShell végpontokhoz.
A rendszer a helyi rendszergazdák módosíthatja a rendszer felügyelheti vagy módosíthatja a szerepkör képes kiterjeszteni a a felhasználók mit tehetnek a JEA-munkamenetet a további felhasználók JEA konfigurációk is.
Ezért fontos a JEA felhasználók kiterjesztett engedéllyel, ha van-e más módon, a rendszer privilegizált hozzáférést kapnak sikerült kiértékeléséhez.

Egy általános gyakorlat az, hogy rendszeres napi karbantartás JEA használnak, és egy "csak az idő" emelt szintű hozzáférés-kezelési megoldás engedélyezése a felhasználók ideiglenesen a helyi rendszergazdák vészhelyzetben válik.
Ez biztosítja a felhasználók nem állandó rendszergazdák, a rendszer, de ezeket a jogokat kaphat, ha, és csak olyan munkafolyamatot, amely ezeket az engedélyeket a használatukat dokumentumok művelet befejeződik.