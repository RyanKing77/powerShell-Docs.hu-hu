---
ms.date: 07/10/2019
keywords: jea, PowerShell, biztonság
title: JEA biztonsági megfontolások
ms.openlocfilehash: befc24fec368c4f6d60477daf63bf17e9431133e
ms.sourcegitcommit: e894ed833cef57967cdaf002f8c883f66864e836
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/25/2019
ms.locfileid: "70017908"
---
# <a name="jea-security-considerations"></a>JEA biztonsági megfontolások

A JEA segít a biztonsági helyzet javításában azáltal, hogy csökkenti a gépek állandó rendszergazdáinak számát. A JEA egy PowerShell-munkamenet-konfigurációt használ egy új belépési pont létrehozásához a felhasználók számára a rendszer felügyeletéhez. Azok a felhasználók, akiknek emelt szintűnek, de nem korlátlannak kell lenniük, a gépen a rendszergazdai feladatok elvégzéséhez hozzáférést kaphatnak a JEA-végponthoz. Mivel a JEA lehetővé teszi, hogy ezek a felhasználók teljes rendszergazdai hozzáférés nélkül futtassák a rendszergazdai parancsokat, ezeket a felhasználókat a magas jogosultsági szintű biztonsági csoportokból is eltávolíthatja.

## <a name="run-as-account"></a>Futtató fiók

Minden JEA-végpont egy kijelölt **futtató** fiókkal rendelkezik. Ez az a fiók, amely alatt a rendszer végrehajtja a csatlakozó felhasználó műveleteit. Ez a fiók konfigurálható a [munkamenet konfigurációs fájljában](session-configurations.md), és a választott fiók jelentős hatással van a végpont biztonságára.

A **virtuális fiókok** a **futtató** fiók konfigurálásának ajánlott módja. A virtuális fiókok egyszeri, ideiglenes helyi fiókok, amelyeket a rendszer a JEA-munkamenet időtartama alatt a csatlakozásra használt felhasználó számára hoz létre. A munkamenet leállítása után a virtuális fiók megsemmisül, és többé nem használható. A csatlakozó felhasználó nem ismeri a virtuális fiók hitelesítő adatait. A virtuális fiók nem használható a rendszer más módon, például Távoli asztal vagy egy nem korlátozott PowerShell-végponton keresztüli eléréséhez.

Alapértelmezés szerint a virtuális fiókok a helyi **rendszergazdák** csoportjába tartoznak a gépen. Ez teljes körű jogosultságot biztosít a rendszer minden adatának kezeléséhez, de nincs jogosultsága a hálózaton lévő erőforrások felügyeletére.
Ha más gépekkel végzi a hitelesítést, a felhasználói környezet a helyi számítógépfiók, nem pedig a virtuális fiók.

A tartományvezérlők különleges esetek, mert nincs helyi **rendszergazdák** csoport. Ehelyett a virtuális fiókok **tartományi rendszergazdákhoz** tartoznak, és felügyelhetik a tartományvezérlőn a címtárszolgáltatások szolgáltatást. A tartományi identitás továbbra is korlátozva van azon a tartományvezérlőn, amelyen a JEA-munkamenet példánya létrejött. A hálózati hozzáférés úgy tűnik, hogy a tartományvezérlő számítógép-objektumból származik.

Mindkét esetben explicit módon meghatározhatja, hogy mely biztonsági csoportok tartoznak a virtuális fiókhoz. Ez jó megoldás, ha a feladat helyi vagy tartományi rendszergazdai jogosultságok nélkül is elvégezhető. Ha már van definiálva biztonsági csoport a rendszergazdák számára, adja meg a virtuális fiók tagságát a csoporthoz. A virtuális fiókok csoporttagság a munkaállomáson és a tagkiszolgálókon lévő helyi biztonsági csoportokra korlátozódik. Tartományvezérlőkön a virtuális fiókoknak tartományi biztonsági csoportok tagjainak kell lenniük.
Miután hozzáadta a virtuális fiókot egy vagy több biztonsági csoporthoz, az már nem tartozik az alapértelmezett csoportok közé (helyi vagy tartományi rendszergazdák).

A következő táblázat összefoglalja a lehetséges konfigurációs beállításokat és a virtuális fiókok eredményül kapott engedélyeit:

|        Számítógép típusa         | Virtuális fiók csoportjának konfigurációja |                   Helyi felhasználói környezet                    | Hálózati felhasználói környezet |
| ---------------------------- | ----------------------------------- | ------------------------------------------------------- | -------------------- |
| Tartományvezérlő            | Alapértelmezett                             | Tartományi felhasználó, a "*domain*\Domain admins" tagja         | Számítógépfiók     |
| Tartományvezérlő            | A és B tartományi csoportok               | Tartományi felhasználó, a "*tartomány*\A", "*domain*\b" tagja       | Számítógépfiók     |
| Tagkiszolgáló vagy munkaállomás | Alapértelmezett                             | Helyi felhasználó, a "*beépített*\Administrators" tagja        | Számítógépfiók     |
| Tagkiszolgáló vagy munkaállomás | C és D helyi csoportok                | Helyi felhasználó, a "*Computer*\C" és a "*Computer*\D" tagja | Számítógépfiók     |

Ha megtekinti a biztonsági naplózási eseményeket és az alkalmazás eseménynaplóit, láthatja, hogy minden JEA felhasználói munkamenetben egyedi virtuális fiók található. Ez az egyedi fiók segít nyomon követni a JEA-végpont felhasználói műveleteit arra az eredeti felhasználóra, aki futtatta a parancsot. A virtuális fiókok nevei például a `WinRM Virtual Users\WinRM_VA_<ACCOUNTNUMBER>_<DOMAIN>_<sAMAccountName>` következő formátumot követik: ha a **contoso** felhasználója egy JEA-végpontban újraindít egy szolgáltatást, a `WinRM Virtual Users\WinRM_VA_1_contoso_alice`Service Control Manager összes eseményéhez társított Felhasználónév a következő:.

A **csoportosan felügyelt szolgáltatásfiókok (csoportosan felügyelt szolgáltatásfiókokat-EK)** akkor hasznosak, ha egy TAGKISZOLGÁLÓN a JEA-munkamenetben lévő hálózati erőforrásokhoz kell hozzáférnie. Ha például egy JEA-végpont egy másik gépen üzemeltetett REST API szolgáltatás elérésének vezérlésére szolgál. Egyszerűen írhat függvényeket a REST API-k meghívásához, de szükség van egy hálózati identitásra az API-val való hitelesítéshez. A csoportosan felügyelt szolgáltatásfiók használatával a második ugrás lehetséges, és megtarthatja, hogy mely számítógépek használhatják a fiókot. A gMSA érvényes engedélyeit azok a biztonsági csoportok (helyi vagy tartományi) határozzák meg, amelyekhez a gMSA-fiók tartozik.

Ha egy JEA-végpont gMSA használatára van konfigurálva, úgy tűnik, hogy az összes JEA-felhasználó műveletei ugyanabból a gMSA származnak. A műveletek egy adott felhasználóhoz való visszakövetésének egyetlen módja a PowerShell-munkamenet átiratában futtatott parancsok meghatározása.

Ha nem ad meg **futtató** fiókot, a rendszer a **pass-Thru hitelesítő adatokat** használja. A PowerShell a felhasználó hitelesítő adatait használja a parancsok távoli kiszolgálón való futtatásához. Ehhez az szükséges, hogy a közvetlen csatlakozású felhasználó közvetlenül hozzáférhessen a Kiemelt felügyeleti csoportokhoz. Ez a konfiguráció **nem** ajánlott a JEA. Ha a csatlakozó felhasználónak már van rendszergazdai jogosultsága, akkor elkerülhető, hogy a rendszer más, nem korlátozott módon JEA és kezelhesse a rendszerét. További információkért tekintse meg az alábbi szakaszt a JEA és a [rendszergazdák elleni védelemben](#jea-doesnt-protect-against-admins).

A **standard szintű futtató fiókok** lehetővé teszik bármely olyan felhasználói fiók megadását, amely alatt a teljes PowerShell-munkamenet fut. A rögzített **futtató** fiókokat (a `-RunAsCredential` paraméterrel együtt) használó munkamenet-konfigurációk nem JEA-kompatibilisek. A szerepkör-definíciók már nem a várt módon működnek. Minden, a végponthoz való hozzáférésre jogosult felhasználó ugyanahhoz a szerepkörhöz van rendelve.

Nem használhat **RunAsCredential** egy JEA-végponton, mert nehéz nyomon követni a műveleteket adott felhasználók számára, és nem támogatja a felhasználók szerepkörökhöz rendelését.

## <a name="winrm-endpoint-acl"></a>WinRM Endpoint ACL

Ahogy a PowerShell távelérési végpontokhoz hasonlóan, minden JEA-végponthoz külön hozzáférés-vezérlési lista (ACL) tartozik, amely azt szabályozza, hogy ki végezhet hitelesítést a JEA-végponton. Ha nincs megfelelően konfigurálva, előfordulhat, hogy a megbízható felhasználók nem férhetnek hozzá a JEA-végponthoz, és előfordulhat, hogy a nem megbízható felhasználók hozzáférhetnek. A WinRM ACL-je nem befolyásolja a felhasználók JEA-szerepkörökhöz való hozzárendelését. A leképezést a **RoleDefinitions** mező szabályozza a végpont regisztrálásához használt munkamenet-konfigurációs fájlban.

Alapértelmezés szerint, ha egy JEA-végpont több szerepköri képességgel rendelkezik, a WinRM ACL úgy van konfigurálva, hogy engedélyezze a hozzáférést az összes leképezett felhasználóhoz. A következő parancsokkal konfigurált JEA-munkamenetek például teljes hozzáférést `CONTOSO\JEA_Lev1` biztosítanak a és `CONTOSO\JEA_Lev2`a szolgáltatáshoz.

```powershell
$roles = @{ 'CONTOSO\JEA_Lev1' = 'Lev1Role'; 'CONTOSO\JEA_Lev2' = 'Lev2Role' }
New-PSSessionConfigurationFile -Path '.\jea.pssc' -SessionType RestrictedRemoteServer -RoleDefinitions $roles -RunAsVirtualAccount
Register-PSSessionConfiguration -Path '.\jea.pssc' -Name 'MyJEAEndpoint'
```

A [Get-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/get-pssessionconfiguration) parancsmaggal is naplózhatja a felhasználói engedélyeket.

```powershell
Get-PSSessionConfiguration -Name 'MyJEAEndpoint' | Select-Object Permission
```

```Output
Permission
----------
CONTOSO\JEA_Lev1 AccessAllowed
CONTOSO\JEA_Lev2 AccessAllowed
```

Ha módosítani szeretné, hogy mely felhasználók férhetnek hozzá `Set-PSSessionConfiguration -Name 'MyJEAEndpoint' -ShowSecurityDescriptorUI` , futtassa a parancsot interaktív `Set-PSSessionConfiguration -Name 'MyJEAEndpoint' -SecurityDescriptorSddl <SDDL string>` üzenetként, vagy frissítse az engedélyeket. A felhasználóknak legalább a JEA-végpont eléréséhez meg kell hívniuk a jogosultságokat.

Létrehozhat egy olyan JEA-végpontot, amely nem rendel hozzá meghatározott szerepkört minden olyan felhasználóhoz, aki hozzáféréssel rendelkezik. Ezek a felhasználók JEA-munkamenetet indíthatnak, de csak az alapértelmezett parancsmagokhoz férhetnek hozzá. A JEA-végponton futó felhasználói engedélyeket a futtatásával `Get-PSSessionCapability`lehet naplózni. További információ: [naplózás és jelentéskészítés a JEA-on](audit-and-report.md).

## <a name="least-privilege-roles"></a>Legalacsonyabb jogosultsági szintű szerepkörök

JEA-szerepkörök tervezésekor fontos megjegyezni, hogy a színfalak mögött futó virtuális és csoportosan felügyelt szolgáltatásfiókok korlátlan hozzáférést biztosíthatnak a helyi géphez. A JEA szerepkör-funkciók segítenek korlátozni az abban a Kiemelt környezetben futtatható parancsokat és alkalmazásokat.
A nem megfelelően tervezett szerepkörök lehetővé teszik a veszélyes parancsok használatát, amelyek lehetővé tehetik a felhasználók számára a JEA-határok kitörését vagy a bizalmas adatokhoz való hozzáférést.

Vegyük például a következő szerepkör-képesség bejegyzést:

```powershell
@{
    VisibleCmdlets = 'Microsoft.PowerShell.Management\*-Process'
}
```

Ez a szerepkör-funkció lehetővé teszi, hogy a felhasználók bármilyen PowerShell -parancsmagot futtassanak a **Microsoft. PowerShell. Management** modul főnévi folyamatával. Előfordulhat, hogy a felhasználóknak el kell érniük a parancsmagokat `Get-Process` , hogy meglássák, milyen alkalmazások futnak a rendszeren, és `Stop-Process` hogy a nem válaszoló alkalmazásokat öljenek meg. Ez a bejegyzés azonban lehetővé teszi `Start-Process`, hogy a teljes körű rendszergazdai engedélyekkel elindítson egy tetszőleges programot. A programot nem kell helyileg telepíteni a rendszeren. Egy csatlakoztatott felhasználó elindíthat egy programot egy olyan fájlmegosztás segítségével, amely a felhasználó helyi rendszergazdai jogosultságait, kártevőket futtat, és így tovább.

Ennek a szerepkör-képességnek a biztonságosabb verziója az alábbihoz hasonló:

```powershell
@{
    VisibleCmdlets = 'Microsoft.PowerShell.Management\Get-Process', 'Microsoft.PowerShell.Management\Stop-Process'
}
```

Ne használjon helyettesítő karaktereket a szerepkör-funkciókban. Győződjön meg arról, hogy rendszeresen naplózza a [hatályos felhasználói engedélyeket](audit-and-report.md#check-effective-rights-for-a-specific-user) , hogy megtudja, mely parancsok férhetnek hozzá a felhasználóhoz.

## <a name="jea-doesnt-protect-against-admins"></a>A JEA nem véd a rendszergazdák ellen

A JEA egyik alapvető alapelve, hogy a nem rendszergazdák számára is lehetővé teszi a rendszergazdai feladatok elvégzését. A JEA nem biztosít védelmet olyan felhasználók ellen, akik már rendelkeznek rendszergazdai jogosultságokkal. Azok a felhasználók, akik **tartományi rendszergazdák**, helyi **rendszergazdák**vagy más magas jogosultsági szintű csoportokba tartoznak, a JEA védelmét más módon is megkerülhetik. Bejelentkezhetnek például RDP használatával, távoli MMC-konzolokkal, vagy nem korlátozott PowerShell-végpontokhoz csatlakozhatnak. Emellett a rendszer helyi rendszergazdái módosíthatják a JEA konfigurációit, hogy további felhasználók számára is engedélyezzék a szerepkört, és hogy a felhasználók milyen hatókört tudjanak kiterjeszteni a JEA-munkamenetben. Fontos, hogy kiértékelje a JEA-felhasználók kiterjesztett engedélyeit, és ellenőrizze, hogy van-e más mód a rendszerszintű hozzáférés megszerzéséhez.

Az általános gyakorlat az, hogy a JEA-t használja a napi karbantartáshoz, és van egy igény szerinti, privilegizált hozzáférés-kezelési megoldás, amely lehetővé teszi a felhasználók számára, hogy vészhelyzeti helyzetekben átmenetileg helyi rendszergazdák legyenek. Ezzel biztosíthatja, hogy a felhasználók ne legyenek állandó rendszergazdák a rendszeren, de csak akkor kaphatják meg ezeket a jogosultságokat, ha a és csak akkor, amikor egy munkafolyamatot végeznek az engedélyek használatára.
