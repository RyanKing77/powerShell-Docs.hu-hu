---
ms.date: 06/12/2017
keywords: a jea, powershell, biztonsági
title: A JEA biztonsági szempontok
ms.openlocfilehash: 9526e141517601ae3b6d6932cd3536fdf49aa9a6
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62084776"
---
# <a name="jea-security-considerations"></a>A JEA biztonsági szempontok

> Érintett kiadások: Windows PowerShell 5.0

A JEA segítségével javíthatja biztonsági helyzetét a gépeken állandó rendszergazdák számának csökkentésével.
Így hozzon létre egy új belépési pont a felhasználók számára a rendszer (a PowerShell munkamenet-konfiguráció), amely szorosan zárolva van, a visszaélések megelőzése érdekében alapértelmezés szerint kezelheti hajtja végre.
Felhasználók, akiknek szükség van néhány, de nem korlátlan, a felügyeleti feladatokat hajthat végre a géphez való hozzáférés is hozzáférést kell biztosítani a JEA-végpont.
JEA lehetővé teszi, hogy azokat rendszergazdai parancsok futtatásához rendszergazdai hozzáférés nélkül közvetlenül, mert a magas jogosultsági szintű biztonsági csoportok (Ügyeljen rá, azokat az általános jogú felhasználók) majd eltávolíthatja a felhasználók.

Ez a témakör ismerteti a JEA biztonsági modell és ajánlott eljárások részletesebben.

## <a name="run-as-account"></a>Futtató fiók

Minden a JEA-végpont tartalmaz egy kijelölt "Futtatás mint" fiók, amely a fiók, amely alatt a csatlakozó felhasználó műveletek végrehajtására kerül sor.
Ez a fiók akkor lehet beállítani a [munkamenet konfigurációs fájl](session-configurations.md), és a választott fiók rendelkezik a jelentős hatással a végpont biztonságát.

**A virtuális fiókok** az ajánlott módszer az, hogy a futtató fiók konfigurálása.
A virtuális fiókok olyan egyszeri, ideiglenes helyi felhasználói fiókok a csatlakozó felhasználó JEA a munkamenet időtartama alatt használni létrehozott.
Amint azok a munkamenet meg lett szakítva, a virtuális fiók meg kell semmisíteni, és többé nem használható.
A kapcsolódó felhasználó nem tudja a virtuális fiók hitelesítő adatait, és a virtuális fiók nem használható a rendszer más eszközzel, például a távoli asztal vagy a PowerShell korlátozás végpont elérésére.

Alapértelmezés szerint a virtuális fiókok tartoznak a helyi Rendszergazdák csoportjában a számítógépen.
Ezáltal őket teljes jogosultságokkal kezelése semmit, a rendszer, de nincs jogosultsága a hálózaton lévő erőforrások kezelésére.
Más gépeken való hitelesítéskor a felhasználói környezet, amely a helyi számítógépfiók, nem a virtuális fiók lesz.

Mivel a helyi Rendszergazdák csoport fogalma nem létezik tartományvezérlők, nem egy különleges esetben.
Ehelyett a virtuális fiókok tartományi rendszergazdák inkább tartozik, és kezelheti a tartományvezérlő a címtárszolgáltatások.
A tartomány identitás korlátozódik továbbra is használni a tartományvezérlőn, ahol a JEA-munkamenet példányosítása volt, és minden olyan hálózati hozzáférési jelenik meg a tartományvezérlő számítógép-objektumot inkább származnak.

Mindkét esetben közvetlenül is definiálhat melyik biztonsági csoportok, a virtuális fiókhoz kell tartoznia.
Ez akkor célszerű, ha a helyi és tartományi rendszergazdai jogosultságok nélkül a feladat végez végezhető.
Ha már rendelkezik a rendszergazdák számára meghatározott biztonsági csoport, egyszerűen biztosíthat a virtuális fiók tagság, hogy a csoport adjon meg a szükséges engedélyekkel.
Virtuális fiók csoporttagság korlátozódik munkaállomás és a tagok a helyi biztonsági csoportoknak, de egy tartományvezérlőn csak lehet, hogy tartományi biztonsági csoportok tagjai.
Ha megad egy vagy több biztonsági csoportot a virtuális fiók tartozik, azt fogja már nem tartozik alapértelmezett csoportok (helyi vagy tartományi rendszergazdaként).

Az alábbi táblázat összefoglalja a lehetséges konfigurációs beállításokat és az eredményül kapott engedélyeket a virtuális fiókok

Számítógép típusa                | Virtuális fiók csoport konfigurálása | Helyi felhasználói környezet                                      | Hálózati felhasználói környezet
-----------------------------|-------------------------------------|---------------------------------------------------------|--------------------------------------------------
Tartományvezérlő            | Alapértelmezett                             | Tartományi felhasználó, tagja "*tartomány*\Domain rendszergazdák         | Számítógépfiók
Tartományvezérlő            | A és B tartományi csoportok               | Tartományi felhasználó, tagja "*tartomány*\A ','*tartomány*\B"       | Számítógépfiók
Tagkiszolgáló vagy munkaállomás | Alapértelmezett                             | Helyi felhasználói, tagja "*beépített*\Administrators'        | Számítógépfiók
Tagkiszolgáló vagy munkaállomás | C és a D helyi csoportok                | Helyi felhasználói, tagja "*számítógép*\C" és "*számítógép*\D" | Számítógépfiók

Ha biztonsági naplózási eseményeket és a alkalmazás eseménynaplóit, látni fogja, hogy minden egyes JEA felhasználói munkamenet egy egyedi virtuális fiók rendelkezik-e.
Ennek segítségével nyomon követheti a JEA-végpont felhasználói műveletek térjen vissza az eredeti felhasználó, aki a parancsot futtatta.
Virtuális fiók neve követi a "WinRM virtuális felhasználók\\WinRM\_sebezhetőség-Felmérési\_*ACCOUNTNUMBER*\_*tartomány* \_ *sAMAccountName*"például"Contoso"tartományban a" Alice "nevű felhasználó a JEA-végpont a szolgáltatás újraindul, ha a service control manager eseményeket társított felhasználónevet lenne" a WinRM virtuális felhasználók\\WinRM\_ Sebezhetőség-Felmérési\_1\_contoso\_alice ".


**A felügyelt szolgáltatásfiókok (csoportosan felügyelt szolgáltatásfiókokat) csoport** akkor hasznos, ha egy tagkiszolgálóra hozzáféréssel kell rendelkeznie a hálózati erőforrásokhoz a JEA-munkamenetben.
Egy példa a funkcióban a JEA-végpont egy másik gépen futó REST API-val való hozzáférés szabályozásához használt.
Ahhoz, hogy a kívánt indítások a REST API-t, de annak érdekében, hogy hitelesítéséhez az API-val függvények hálózati identitás kell írni könnyebbé vált.
Csoportosan felügyelt szolgáltatásfiók használata lehetővé teszi, a "második Ugrás" közben továbbra is fennáll a vezérlő, amelyen számítógépek fiókot is használhatja.
A csoportosan felügyelt szolgáltatásfiókot, a hatályos engedélyek határozzák meg a biztonsági csoportok (helyi vagy tartományi), amelyhez a csoportosan felügyelt szolgáltatásfiók tartozik.

A JEA-végpont a csoportosan felügyelt szolgáltatásfiók használatára van konfigurálva, amikor a felhasználók a JEA műveletek jelenik meg, ugyanabba a csoportba származniuk felügyelt szolgáltatásfiók.
Vissza az adott felhasználó a műveletek nyomon követhetők csak úgy, hogy azonosítsa azokat a parancsokat futtatni egy PowerShell-munkamenet átiratot.

**Hitelesítő adatok pass –** akkor használjuk, ha nem adja meg egy futtató fiókot, és nem szeretné a PowerShell-parancsok futtatásához a távoli kiszolgálón a csatlakozó felhasználó hitelesítő adatait használja.
Ez a konfiguráció *nem* JEA számára ajánlott, mivel a felület kéri, hogy a csatlakozó felhasználó közvetlen hozzáférést biztosítson a kiemelt jogosultságú felügyeleti csoportokhoz.
Ha a kapcsolódó felhasználó már rendelkezik rendszergazdai jogosultságokkal, JEA érvényesítette elkerülése, és keresztül más, korlátozás azt jelenti, hogy a rendszer kezelését.
Tekintse át az alábbi szakaszban [JEA nem nyújt védelmet a rendszergazdák](#jea-does-not-protect-against-admins) további információt.

**Standard szintű Futtatás mint fiókok** meg lehet adni egy felhasználói fiókot, amely alatt futni fog a teljes PowerShell-munkamenetben.
Ez fontos különbség, mivel egy munkamenet-konfiguráció beállítása használandó rögzített futtató fiókot (a a `-RunAsCredential` paraméter) még nem ismeri a JEA.
Ez azt jelenti, hogy a szerepkör-definíciók nem várt módon működik, és minden felhasználó jogosult a végpont elérésére rendeli ugyanarra a szerepkörre.

Nehézségekbe ütközik a nyomkövetés műveletek vissza a konkrét felhasználókat és a felhasználók leképezése szerepkörök támogatása hiánya miatt a JEA-végpont nem használjon egy RunAsCredential.

## <a name="winrm-endpoint-acl"></a>WinRM Endpoint ACL

Rendszeres PowerShell távoli eljáráshívás végpontokkal, minden a JEA-végpont egy külön hozzáférés-vezérlési lista (ACL) állíthat be a vezérlő a Rendszerfelügyeleti webszolgáltatások konfigurációs van, akik hitelesítheti a JEA-végponttal.
Ha nem megfelelően konfigurált, megbízható felhasználók nem lehet tudni hozzáférni a JEA-végpont, és/vagy nem megbízható felhasználók előfordulhat, hogy hozzáférést kapjanak.
A WinRM ACL nem, azonban befolyásolja a felhasználók JEA szerepkörökhöz a leképezést.
Szabályozza, amely a *RoleDefinitions* mezőt a rendszer regisztrált munkamenet konfigurációs fájlban.

Alapértelmezés szerint amikor regisztrál egy JEA-végpont használatával egy munkamenet-konfigurációs fájlban és a egy vagy több szerepkör-szolgáltatásait, a Rendszerfelügyeleti webszolgáltatások ACL lesz konfigurálva, hogy a végponthoz való hozzáférést egy vagy több szerepkörök hozzárendelése az összes felhasználó.
Például a JEA munkamenet konfigurálva, a következő parancsokkal, teljes hozzáférést biztosít *CONTOSO\JEA\_Lev1* és *CONTOSO\JEA\_Lev2*.

```powershell
$roles = @{ 'CONTOSO\JEA_Lev1' = 'Lev1Role'; 'CONTOSO\JEA_Lev2' = 'Lev2Role' }
New-PSSessionConfigurationFile -Path '.\jea.pssc' -SessionType RestrictedRemoteServer -RoleDefinitions $roles -RunAsVirtualAccount
Register-PSSessionConfiguration -Path '.\jea.pssc' -Name 'MyJEAEndpoint'
```

A felhasználói engedélyek naplózhatók a [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) parancsmagot.

```powershell
PS C:\> Get-PSSessionConfiguration -Name 'MyJEAEndpoint' | Select-Object Permission

Permission
----------
CONTOSO\JEA_Lev1 AccessAllowed
CONTOSO\JEA_Lev2 AccessAllowed
```

Szeretné módosítani, hogy mely felhasználók férhessenek, futtathatja az alábbiak `Set-PSSessionConfiguration -Name 'MyJEAEndpoint' -ShowSecurityDescriptorUI` számára egy interaktív kérdés vagy `Set-PSSessionConfiguration -Name 'MyJEAEndpoint' -SecurityDescriptorSddl <SDDL string>` engedélyeinek frissítését.
A felhasználóknak kell legalább *Invoke* jogok a JEA-végpont elérésére.

Ha további felhasználókat a JEA-végpont elérhető, de nem az a munkamenet-konfigurációs fájlban meghatározott szerepkörök valamelyikébe tartoznak, fogják tudni JEA munkamenetet, de csak az alapértelmezett parancsmagok hozzáférése.
A JEA-végpont a felhasználói engedélyek naplózhatók futtatásával `Get-PSSessionCapability`.
Tekintse meg a [naplózás és a JEA-jelentések](audit-and-report.md) cikk naplózásával kapcsolatos további információt, hogy milyen parancsokat egy felhasználó hozzáfér az a JEA-végpont.

## <a name="least-privilege-roles"></a>Legkisebb jogosultság szerepkörök

JEA szerepkörök tervezésekor fontos megjegyezni, hogy a virtuális vagy csoport felügyelt szolgáltatás fiók fut a háttérben gyakran rendelkezik korlátlan hozzáférést a helyi gépen.
JEA szerepköri funkciók segítségével korlátozhatja a mi fiók is használható, korlátozza a parancsok és az alkalmazásokat, amelyek használatával a privilegizált környezetben futtatható.
Nem megfelelően kialakított szerepköröket lehetővé tehetik a veszélyes parancsok futtatását, előfordulhat, hogy lehetővé teszi, hogy a JEA határain kívül break vagy férhet hozzá a bizalmas adatokat.

Vegyük példaként a következő szerepkör-képesség bejegyzés:

```powershell
@{
    VisibleCmdlets = 'Microsoft.PowerShell.Management\*-Process'
}
```

Ez a szerepkör funkció lehetővé teszi a felhasználóknak minden olyan PowerShell-parancsmaggal futtassa a főnév "Folyamat" a Microsoft.PowerShell.Management modulból.
Felhasználók valószínűleg eléréséhez, például a parancsmagok `Get-Process` megérteni, milyen alkalmazások vannak a rendszeren futó és `Stop-Process` le olyan alkalmazásokat, amelyek nem válaszolnak.
Azonban ez a bejegyzés is lehetővé teszi, hogy `Start-Process`, teljes körű rendszergazda engedélyekkel rendelkező egy tetszőleges program elindításához használható.
A program nem kell helyileg kell telepíteni a rendszerre, hogy egy támadó egyszerűen sikerült elindítani a program, amely lehetővé teszi a csatlakozó felhasználó helyi rendszergazdai jogosultságokat, futtatások kártevők és más fájlmegosztáson. "

A szerepkör funkció biztonságosabb verziója hasonlóan néz ki:

```powershell
@{
    VisibleCmdlets = 'Microsoft.PowerShell.Management\Get-Process', 'Microsoft.PowerShell.Management\Stop-Process'
}
```

Kerülje a helyettesítő karaktereket a szerepkörrel képességeket, és ügyeljen arra, hogy [hatékony felhasználói engedélyek naplózási](audit-and-report.md#check-effective-rights-for-a-specific-user) rendszeresen megértéséhez, amely parancsokat egy felhasználó hozzáfér.

## <a name="jea-does-not-protect-against-admins"></a>A JEA nem nyújt védelmet a rendszergazdák

A JEA core alapelveit egyik, mert így a nem rendszergazda jogosultságú végrehajtásához *néhány* rendszergazdai feladatok.
A JEA nem nyújt védelmet a azoknak, akik már rendelkezik rendszergazdai jogosultságokkal.
Felhasználók számára tartozik a "tartományi rendszergazdák", "helyi rendszergazdák," vagy egyéb magas jogosultsági szintű csoportokhoz a környezetben még fogja tudni megkerülésében JEA a védelmet, ehhez jelentkezzen be egy másik azt jelenti, hogy a gép.
Ezek sikerült, például jelentkezzen be az RDP, használjon távoli MMC-konzolt, vagy csatlakoztassa korlátozás PowerShell-végpontokra irányuló.
A rendszer a helyi rendszergazdák módosíthatja a további felhasználók kezelhetik a rendszert, vagy módosítsa a szerepkör képes kiterjeszteni a felhasználók mit tehetnek a JEA-munkamenetet a JEA-konfigurációk is.
Ezért fontos kiértékelni a JEA-felhasználók kiterjesztett engedéllyel vannak-e más módokon szerezhet, emelt szintű hozzáférést a rendszerhez.

Egy gyakori eljárás, ha a jea-t használnak rendszeres napi karbantartás, és "igény szerinti" emelt szintű hozzáférés-kezelési megoldást engedélyezése a felhasználók ideiglenesen a helyi rendszergazdák vészhelyzet válik.
Ez biztosítja, hogy, hogy a felhasználók nem állandó rendszergazdák, a rendszer, de ezeket a jogokat kaphat, ha, és csak akkor végezze el egy munkafolyamatot, amely a dokumentumok használata során ezeket az engedélyeket.