---
ms.date: 2017-06-27
keywords: PowerShell parancsmag
title: "A Webes Windows PowerShell-elérés engedélyezési szabályai és biztonsági funkciói"
ms.openlocfilehash: 19e4aa1bb55178ec2634af0771afe2db5db3423c
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="authorization-rules-and-security-features-of-windows-powershell-web-access"></a>A Webes Windows PowerShell-elérés engedélyezési szabályai és biztonsági funkciói

Frissített: Június 24 2013.

Vonatkozik: Windows Server 2012 R2, Windows Server 2012-ben

A Windows Server 2012 R2 és Windows Server 2012 a Windows PowerShell Web Access korlátozó biztonsági modellel rendelkezik.
Felhasználók kifejezetten hozzáférést kell rendelni ahhoz, hogy jelentkezzen be a Windows PowerShell Web Access-átjáró és a webes Windows PowerShell-konzolt használja.

## <a name="configuring-authorization-rules-and-site-security"></a>Az engedélyezési szabályok és a hely biztonságának konfigurálása

Miután a Windows PowerShell Web Access telepítve van, és az átjáró, felhasználó meg tudja nyitni a böngészőben a bejelentkezési oldal, de azok nem tud bejelentkezni, amíg a Windows PowerShell Web Access rendszergazdai hozzáférést biztosít a felhasználónak explicit módon.
"A Windows PowerShell Web Access" hozzáférés-vezérlés a következő táblázat ismerteti a Windows PowerShell-parancsmagok használatával kezeli.
Engedélyezési szabályok hozzáadásához és kezeléséhez nincs hasonló grafikus felhasználói felület.
Lásd: [Windows PowerShell Web Access parancsmagok](cmdlets/web-access-cmdlets.md).

Rendszergazdák meghatározhatnak 0 -*n* hitelesítési szabályokat Windows PowerShell Web Access.
Az alapértelmezett biztonság inkább korlátozóak, nem pedig engedélyezők; a nulla hitelesítési szabály azt jelenti, hogy egyetlen felhasználó sem férhet hozzá semmihez.

[Add-PswaAuthorizationRule](cmdlets/add-pswaauthorizationrule.md) és [Test-PswaAuthorizationRule](cmdlets/test-pswaauthorizationrule.md) a Windows Server 2012 R2 tartalmaznak egy Credential paramétert, amely lehetővé teszi a történő hozzáadását és tesztelését egy távoli Windows PowerShell Web Access engedélyezési szabályok számítógép, vagy egy aktív Windows PowerShell Web Access-munkameneten belül.
Mint a többi Windows PowerShell-parancsmaggal, amelyek tartalmaznak egy Credential paramétert is megadhat egy PSCredential objektumot a paraméter értékeként.
A távoli számítógépnek átadni kívánt hitelesítő adatokat tartalmazó PSCredential objektum létrehozásához futtassa a [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) parancsmag.

A Windows PowerShell Web Access hitelesítési szabályai engedélyezett szabályok vonatkoznak.
Minden egyes szabály a felhasználók, számítógépek és az adott Windows PowerShellÂ között engedélyezett kapcsolat definíciója [munkamenet-konfigurációk](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configurations) (más néven végpontok vagy _futási terek_) a a megadott célszámítógépeken.
Az előzetesben **futási terek** lásd [PowerShell futtatóterek használata kezdete](https://blogs.technet.microsoft.com/heyscriptingguy/2015/11/26/beginning-use-of-powershell-runspaces-part-1/)

> **Biztonsági Megjegyzés**
>
> A felhasználónak csak egy érvényes szabályra van szüksége a hozzáférés megszerzéséhez.
Ha a felhasználó kap hozzáférést egy számítógéphez teljes nyelvi hozzáféréssel vagy csak a Windows PowerShell-parancsmagok távoli felügyelet, a hozzáférés a webalapú konzolról a felhasználó jelentkezzen be (vagy átugorhat) más számítógépekre, amelyek az első célszámítógéphez csatlakoznak.
A legbiztonságosabb konfigurálása a Windows PowerShell Web Access módja csak korlátozott munkamenet-konfigurációkat, amelyek lehetővé teszik, hogy szokásos módon kell végrehajtani távolról konkrét feladatok elvégzését való felhasználói hozzáférést lehetővé.

A hivatkozott parancsmagok [Windows PowerShell Web Access parancsmagok](cmdlets/web-access-cmdlets.md) lehetővé teszi a Windows PowerShell Web Access-átjárón a felhasználó hitelesítéséhez használt hozzáférési szabályok hozzon létre.
A szabályok eltérnek a célszámítógépen található hozzáférés-vezérlési listáktól (ACL), és további biztonsági réteget biztosítanak a webes eléréshez.
A biztonsággal kapcsolatos további részleteket a következő szakasz tartalmazza.

Ha a felhasználók nem adható át az előző biztonsági rétegek bármelyikét, egy általános "hozzáférés megtagadva" üzenet megérkezése böngészőjük ablakában.
Habár az átjáró-kiszolgáló naplózza a biztonsági adatokat, a végfelhasználóknak nem jelenik meg információ arról, hogy hány biztonsági rétegnek feleltek meg, illetve melyik rétegnél nem sikerült a bejelentkezés vagy a hitelesítés.

Az engedélyezési szabályok konfigurálásával kapcsolatos további információkért lásd: [engedélyezési szabályok konfigurálásával](#configuring-authorization-rules-and-site-security) ebben a témakörben.

### <a name="security"></a>Biztonság

A Windows PowerShell Web Access biztonsági modellje négy réteget egy end user a webalapú konzol, és a célszámítógép között.
Windows PowerShell Web Access-rendszergazdák az IIS-kezelő konzolon kiegészítő konfigurálással további biztonsági rétegeket adhat hozzá.
Az IIS-kezelő konzolon webhelyek biztonságossá tétele kapcsolatos további információkért lásd: [webkiszolgáló biztonságának konfigurálása (IIS 7)](https://technet.microsoft.com/library/cc731278).
További információ az IIS ajánlott eljárások és -szolgáltatásmegtagadási támadások megelőzése, lásd: [gyakorlati tanácsok a megakadályozza a DoS/szolgáltatásmegtagadási támadások](https://technet.microsoft.com/library/cc750213).
A rendszergazda is vásárolhat és további kereskedelmi hitelesítési szoftvereket telepíteni.

Az alábbi táblázat a végfelhasználók és a célszámítógépek között lévő négy biztonsági réteget ismerteti.

|Szint|Réteg|
|-|-|
|1|[az IIS webkiszolgáló biztonsági szolgáltatásainak](#iis-web-server-security-features)|
|2|[a Windows powershell web access űrlapalapú átjáró hitelesítés](#windows-powershell-web-access-forms-based-gateway-authentication)|
|3|[a Windows powershell web access engedélyezési szabályok](#windows-powershell-web-access-authorization-rules)|
|4|[cél hitelesítési és engedélyezési szabályok](#target-authentication-and-authorization-rules)|

Minden egyes réteg kapcsolatos részletes információk a következő címszó alatt található:

#### <a name="iis-web-server-security-features"></a>IIS-webkiszolgáló biztonsági funkciói

A Windows PowerShell Web Access felhasználók mindig meg kell adniuk a felhasználónevet és jelszót a fiókjuk átjárón hitelesítéséhez.
Azonban a Windows PowerShell Web Access rendszergazdák is kapcsolhatja választható ügyféltanúsítvány-alapú hitelesítés be- és kikapcsolása, lásd: [telepítheti és használhatja a windows powershell web access](install-and-use-windows-powershell-web-access.md) teszttanúsítványt engedélyezése és újabb verziók, konfigurálása a eredeti tanúsítvánnyal).

A választható ügyféltanúsítvány-alapú szolgáltatás megköveteli, hogy a végfelhasználók felhasználónevükön és jelszavukon kívül érvényes ügyféltanúsítvánnyal rendelkezzenek, ami a webkiszolgáló (IIS) konfigurációjának részét képezi.
Ha az ügyféltanúsítvány rétege engedélyezve van, a Windows PowerShell Web Access bejelentkezési oldal kéri a felhasználóktól, érvényes tanúsítványok megadását, mielőtt a bejelentkezési hitelesítő adataikat.
Ügyféltanúsítvány-alapú hitelesítés automatikusan ellenőrzi az ügyfél tanúsítványát.
Ha nem található érvényes tanúsítvány, akkor a Windows PowerShell Web Access mindig tájékoztatnia a felhasználókat, így azok megadhatják a tanúsítványt.
Ha egy érvényes ügyféltanúsítványt talál, a Windows PowerShell Web Access megnyitja a bejelentkezési oldalt a felhasználók számára a felhasználói neveket és jelszavakat adjon meg.

Itt látható egy példa az IIS webkiszolgáló által felkínált kiegészítő biztonsági beállításokra.
Egyéb IIS biztonsági funkciókkal kapcsolatos további információkért lásd: [webkiszolgáló biztonságának konfigurálása (IIS 7)](https://technet.microsoft.com/library/cc731278)

#### <a name="windows-powershell-web-access-forms-based-gateway-authentication"></a>A Windows PowerShell Web Access űrlapalapú átjáró hitelesítése

A Windows PowerShell Web Access bejelentkezési oldal (felhasználónév és jelszó) hitelesítő adatokat igényel, és lehetővé teszi a felhasználók eltérő hitelesítő adatokat adjanak a célszámítógépen.
Ha a felhasználó nem ad meg más hitelesítő adatokat, az átjáróhoz való csatlakozáshoz használt elsődleges felhasználónév és jelszó használható a célszámítógéphez való csatlakozáshoz is.

A szükséges hitelesítő adatok hitelesítése a Windows PowerShell Web Access-átjárón.
Ezeket a hitelesítő adatokat kell érvényes felhasználói fiókkal vagy a helyi Windows PowerShell Web Access átjárókiszolgálón, vagy az Active Directoryban.

#### <a name="windows-powershell-web-access-authorization-rules"></a>A Windows PowerShell Web Access engedélyezési szabályok

A felhasználó hitelesítése az átjárón, a Windows PowerShell Web Access ellenőrzi engedélyezési szabályokat, hogy ellenőrizze, hogy a felhasználó rendelkezik-e a hozzáférést a kért célszámítógéphez.
Sikeres hitelesítést követően a felhasználó hitelesítő adatai továbbítódnak a célszámítógépre.

A rendszer a szabályok értékelését csak a felhasználó átjáró által történt hitelesítése után, és a felhasználó célszámítógépen történő hitelesítése előtt végzi el.

#### <a name="target-authentication-and-authorization-rules"></a>Cél hitelesítési és engedélyezési szabályok

A Windows PowerShell Web Access biztonságának végső rétegét a célként megadott számítógép saját biztonsági konfigurációja.
Felhasználónak rendelkeznie kell egy Windows PowerShell webalapú konzol, amely befolyásolja a célszámítógépet a Windows PowerShell Web Access futtatásához megfelelő hozzáférési jogosultságokkal a cél számítógépen, valamint a Windows PowerShell Web Access-engedélyezési szabályok konfigurálva.

Ez a réteg ugyanazt a biztonsági mechanizmust, amely a csatlakozási próbálkozásokat értékelné ki, ha a felhasználók megpróbálnának létrehozni egy távoli Windows PowerShell-munkamenetet a célszámítógéphez, a Windows PowerShell belül futó kínálja a [Enter-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Enter-PSSession) vagy [New-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/new-pssession) parancsmagok.

Alapértelmezés szerint a, az átjáró és a célszámítógép a Windows PowerShell Web Access használ az elsődleges felhasználónév és jelszó.
A webalapú bejelentkezési oldal, című **választható csatlakozási beállítások**, lehetővé teszi a felhasználók eltérő hitelesítő adatokat adjanak a célszámítógép, amennyiben azok szükségesek.
Ha a felhasználó nem ad meg más hitelesítő adatokat, az elsődleges felhasználó neve és az átjáró való csatlakozáshoz használt jelszót is használhatók a célszámítógéphez kapcsolódni.

Az engedélyezési szabályok segítségével engedélyezhető a felhasználók számára, hogy hozzáférjenek egy adott munkamenet-konfigurációhoz.
Létrehozhat _korlátozott futási terekben engedélyezze_ vagy munkamenet-konfigurációk Windows PowerShell Web Access, és meghatározott felhasználók csak a meghatározott munkamenet-konfigurációk csatlakozni, amikor bejelentkeznek a Windows PowerShell Web Access.
Hozzáférés-vezérlési listák (ACL) segítségével határozza meg, mely felhasználók férhessenek hozzá a meghatározott végpontokhoz, és további való hozzáférés korlátozása a felhasználók adott csoportja számára a végpont ebben a szakaszban ismertetett engedélyezési szabályok segítségével.
Korlátozott futtatóterek kapcsolatos további információkért lásd: [létrehozása egy korlátozott futási térrel](https://msdn.microsoft.com/en-us/library/dn614668).

### <a name="configuring-authorization-rules"></a>Az engedélyezési szabályok konfigurálása

Rendszergazdák valószínűleg az azonos engedélyezési szabály szeretné, hogy a Windows PowerShell Web Access felhasználók számára, amely a Windows PowerShell távoli kezelési környezetükben már definiálva van.
Ebben a szakaszban az első eljárás ismerteti egy olyan engedélyezési szabály, amely hozzáférést biztosít egy felhasználó bejelentkezik egy számítógépet kezelhet, és egy egyetlen munkamenet-konfiguráció belül adja hozzá.
A második eljárás egy olyan engedélyezési szabály eltávolítását ismerteti, amelyre már nincs szükség.

Ha tervezi olyan egyéni munkamenet-konfigurációk használatával meghatározott felhasználók számára csak a Windows PowerShell Web Access korlátozott futtatóterek belül működik, a rájuk hivatkozó engedélyezési szabályok hozzáadása előtt hozzon létre az egyéni munkamenet-konfigurációk.
A Windows PowerShell Web Access parancsmagok nem hozhat létre egyéni munkamenet-konfigurációk.
Egyéni munkamenet-konfigurációk létrehozásával kapcsolatos további információkért lásd: [about_Session_Configuration_Files](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configuration_files).

Windows PowerShell Web Access-parancsmagokat támogatja egy helyettesítő karaktert, a csillagot ( \* ).
A helyettesítő karakterek nem használhatók a karakterláncokon belül; tulajdonságonként (felhasználók, számítógépek vagy munkamenet-konfigurációk) egyetlen csillag használható.

> **Megjegyzés:**
>
> Az engedélyezési szabályok segítségével hozzáférés biztosítása a felhasználók és számítógépek biztonságossá tétele a Windows PowerShell Web Access környezet további részleteket lásd: [más engedélyezési szabály forgatókönyv példáit](#other-authorization-rule-scenario-examples) ebben a témakörben.

#### <a name="to-add-a-restrictive-authorization-rule"></a>Korlátozó engedélyezési szabály hozzáadása

1. Hajtsa végre az alábbi Windows PowerShell-munkamenetet emelt szintű felhasználói jogosultsággal nyissa meg.

    - A Windows asztalon kattintson a jobb gombbal **Windows PowerShell** a tálcán, és kattintson a **Futtatás rendszergazdaként**.

    - A Windows **Start** kattintson a jobb gombbal **Windows PowerShell** , és kattintson a **Futtatás rendszergazdaként**.

2. **Nem kötelező lépés** felhasználói hozzáférés korlátozására munkamenet-konfigurációk használatával:

    Győződjön meg arról, hogy a munkamenet-konfigurációk, szeretné használni, már léteznek a szabályokban.
Azok rendelkezik még nem jött létre, ha a munkamenet-konfigurációk létrehozásához használja utasításokat [about_Session_Configuration_Files](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configuration_files).

3. Ez az engedélyezési szabály lehetővé teszi, hogy a számítógépek egy adott felhasználó hozzáférését a hálózaton, amelyhez általában hozzáférhetnek, egy adott munkamenet-konfiguráció, ami a felhasználó hozzáférést "™ s szokásos parancsfájl-kezelési és parancsmag igényeinek. Írja be a következőt, és nyomja le az **Enter**.

```powershell
Add-PswaAuthorizationRule -UserName <domain\user | computer\user> -ComputerName <computer_name> -ConfigurationName <session_configuration_name>
```

  - A következő példában a felhasználó nevű _JSmith_ a a _Contoso_ tartományi hozzáférést kap a számítógép kezeléséhez _Contoso_214_, és egy munkamenet-konfiguráció használata _NewAdminsOnly_.

```powershell
Add-PswaAuthorizationRule -UserName 'Contoso\JSmith' -ComputerName Contoso_214 -ConfigurationName NewAdminsOnly
```

4. Győződjön meg arról, hogy létrejött-e a szabály futtatásával a **Get-PswaAuthorizationRule** parancsmagot, vagy **Test-PswaAuthorizationRule - UserName &lt;tartomány\\felhasználói |} számítógép\\ felhasználói&gt; - ComputerName** &lt;számítógép_neve&gt;. Például **Test-PswaAuthorizationRule - UserName Contoso\\JSmith - ComputerName Contoso_214**.

#### <a name="to-remove-an-authorization-rule"></a>Az engedélyezési szabály eltávolítása

1. Ha egy Windows PowerShell-munkamenetben még nincs megnyitva, tekintse meg az 1. lépésében [korlátozó engedélyezési szabály hozzáadása](#to-add-a-restrictive-authorization-rule) ebben a szakaszban.

2. Írja be a következőt, és nyomja le az **Enter**, ahol *szabályazonosító* eltávolítani kívánt szabály egyedi azonosító számot jelöli.

```powershell
Remove-PswaAuthorizationRule -ID <rule ID>
```

Azt is megteheti, ha nem ismeri a azonosítószámát, de tudja az eltávolítani kívánt szabály rövid nevét, a szabály nevét, és beállíthatja átadhatja azt a `Remove-PswaAuthorizationRule` parancsmagot, hogy a szabály eltávolításához az alábbi példában látható módon: `Get-PswaAuthorizationRule -RuleName <rule-name> | Remove-PswaAuthorizationRule`.

>**Megjegyzés:**:
>
>Nem kéri győződjön meg arról, hogy szeretné-e a megadott engedélyezési szabály; törlése a szabály törlődik, amikor lenyomja az **Enter**. A `Remove-PswaAuthorizationRule` parancsmagot csak akkor futtassa, ha biztosan el kívánja távolítani az engedélyezési szabályt.

#### <a name="other-authorization-rule-scenario-examples"></a>Példák az engedélyezési szabály egyéb eltávolítási módjaira

Minden Windows PowerShell-munkamenetet használ a munkamenet-konfiguráció; Ha egy munkamenethez nincs megadva, a Windows PowerShell használja az alapértelmezett, beépített Windows PowerShell munkamenet-konfiguráció, neve Microsoft.PowerShell. Az alapértelmezett munkamenet-konfiguráció a számítógépen elérhető összes parancsmagot tartalmazza. A rendszergazdák egy korlátozott futási teret (a parancsmagok és a végfelhasználóik által végrehajtható feladatok korlátozott tartománya) tartalmazó munkamenet-konfiguráció definiálásával korlátozhatják az összes számítógéphez való hozzáférést. Egy számítógép teljes nyelvi hozzáféréssel vagy csak a Windows PowerShell távfelügyeleti parancsmagjaihoz való hozzáféréssel rendelkező felhasználó az első számítógéphez csatlakoztatott más számítógépek is elérheti. Egy korlátozott futási térrel definiálása megakadályozhatja, hogy a felhasználók hozzáférhessenek más számítógépekhez az engedélyezett Windows PowerShell futási térben a, és javítja a Windows PowerShell Web Access-környezet biztonságát. A munkamenet-konfigurációt azokon a számítógépeken, amelyek a rendszergazdák elérhetővé kívánnak tenni a Windows PowerShell Web Access terjeszthető (a csoportházirend használatával). Munkamenet-konfigurációkkal kapcsolatos további információkért lásd: [about_session_configuration_files](https://technet.microsoft.com/library/dd819508.aspx).
Az alábbiakban bemutatunk néhány példát erre a témakörre.

- A rendszergazda létrehoz egy nevű végpontot, **PswaEndpoint**, korlátozott futási térrel. Ezt követően a rendszergazda létrehoz egy szabályt,  **\*,\*, PswaEndpoint**, és elosztja a végpontot a többi számítógép. A szabály lehetővé teszi, hogy az összes felhasználónak a végpont összes számítógép **PswaEndpoint**. Ha a szabálykészletben ez az egyetlen definiált engedélyezési szabály, az ezzel a végponttal nem rendelkező számítógépek nem lesznek elérhetők.

- A rendszergazda létrehozott egy korlátozott futási teret hívása **PswaEndpoint**, és az egyes felhasználók hozzáférését korlátozni kívánja. A rendszergazda nevű csoportot hoz létre **Level1Support**, és a következő szabályt definiálja: **Level1Support,\*, PswaEndpoint**. A szabály engedélyezi a csoportban lévő egyik felhasználóra sem **Level1Support** összes számítógép eléréséhez a **PswaEndpoint** konfigurációs. Hasonlóképpen, a hozzáférés korlátozható egy meghatározott számítógépcsoportra.

- Néhány rendszergazda bizonyos felhasználóknak több hozzáférést biztosít, mint a többieknek. Például a rendszergazda létrehoz két felhasználói csoportot **rendszergazdák** és **BasicSupport**. A rendszergazda létrehoz továbbá egy korlátozott futási térrel rendelkező **PswaEndpoint**, és a következő két szabályt definiálja: **rendszergazdák\*,\***  és  **BasicSupport,\*, PswaEndpoint**. Az első szabály lévő összes felhasználó számára biztosít a **Admin** az összes számítógép és a második szabály csoport hozzáférést biztosít a lévő összes felhasználó számára a **BasicSupport** csak hozzáféréssel rendelkező számítógépek csoport  **PswaEndpoint**.

- A rendszergazda beállított egy privát tesztkörnyezetet, és szeretné engedélyezni az összes jogosult hálózati felhasználó számára a hozzáférést a hálózaton található összes olyan számítógéphez, amelyhez általában hozzáférhetnek, az összes olyan munkamenet-konfigurációhoz való hozzáféréssel, amelyhez általában hozzáférhetnek. Mivel ez egy privát tesztkörnyezet, a rendszergazda egy nem biztonságos engedélyezési szabályt hoz létre.
  - A rendszergazda futtatja a parancsmagot `Add-PswaAuthorizationRule * * *`, amely használja, a helyettesítő karakter  **\***  minden felhasználó, az összes számítógép és az összes konfiguráció képviseletére.
  - Ez a szabály megegyezik a következővel: `Add-PswaAuthorizationRule -UserName * -ComputerName * -ConfigurationName *`.

  >**Megjegyzés:**:
  >
  >Ez a szabály biztonságos környezetben nem ajánlott, és nincs hatással az engedélyezési szabály nyújtott biztonsági rétegre vonatkozó Windows PowerShell Web Access.

- A rendszergazdának egy olyan környezetben kell engedélyeznie a felhasználók számára a célszámítógépekhez történő csatlakozást, amely egyaránt tartalmaz munkacsoportokat és tartományokat, ahol munkacsoportok számítógépeit alkalmanként a tartományokban lévő célszámítógépekhez való csatlakozáshoz használják, a tartományokban levő számítógépeket pedig alkalmanként a munkacsoportokban lévő célszámítógépekhez való csatlakozáshoz használják. A rendszergazda a átjárókiszolgáló *PswaServer*, munkacsoportban; és a célszámítógép *srv1.contoso.com* tartományban van. Felhasználói *Chris* jogosult helyi felhasználója a munkacsoport átjárókiszolgálónak és a célszámítógép is van. A felhasználónév a munkacsoport-kiszolgálón *chrisLocal*; és a felhasználónév, a célszámítógépen *contoso\\chris*. Ahhoz, hogy engedélyezze Chris számára a srv1.contoso.com célszámítógéphez való hozzáférést, rendszergazda a következő szabályt adja hozzá.

```powershell
Add-PswaAuthorizationRule -userName PswaServer\chrisLocal -computerName srv1.contoso.com -configurationName Microsoft.PowerShell
```

Az előző példában a szabály hitelesíti Christ az átjárókiszolgálón, és ezután engedélyezi a számára a hozzáférést a *srv1*. A bejelentkezési oldalon Chris egy második együttesét a hitelesítő adatokat kell megadnia a **választható csatlakozási beállítások** terület (*contoso\\chris*). Az átjárókiszolgáló használ a további hitelesítő adatok hitelesíti christ a célszámítógépen *srv1.contoso.com*.

Az előző esetben a Windows PowerShell Web Access a cél számítógéphez sikeres kapcsolatot létesít a csak után a következő volt sikeres, és legalább egy engedélyezési szabály engedélyezett.

1. Hitelesítés a munkacsoport átjárókiszolgálóján a felhasználónév formátuma való hozzáadásával *kiszolgáló_neve*\\*felhasználónév* az engedélyezési szabály

2. Hitelesítés a célszámítógépen a bejelentkezési oldal, a megadott másodlagos hitelesítő adatok használatával a **választható csatlakozási beállítások** terület

  >**Megjegyzés:**:
  >
  >Ha az átjáró-számítógép és a célszámítógép különböző munkacsoportokban vagy tartományokban vannak, megbízhatósági kapcsolatot kell létrehozni a két munkacsoport-számítógép, a két tartomány vagy a munkacsoport és a tartomány között. Ezt a kapcsolatot nem lehet konfigurálni a Windows PowerShell Web Access engedélyezési szabályokra vonatkozó parancsmagjainak használatával. Az engedélyezési szabályok nem határoznak meg megbízhatósági kapcsolatot a számítógépek között, csak a felhasználóknak engedélyezik, hogy az adott célszámítógépekhez és munkamenet-konfigurációkhoz csatlakozzanak. Különböző tartományok közötti megbízhatósági kapcsolat konfigurálásával kapcsolatos további információkért lásd: [létrehozása tartományi és erdőszintű megbízhatóság](https://technet.microsoft.com/library/cc794775.aspx"). További információ a munkacsoport-számítógépek felvétele a megbízható gazdagépek listájához: [távoli felügyelet a Kiszolgálókezelővel](https://technet.microsoft.com/library/dd759202.aspx)

### <a name="using-a-single-set-of-authorization-rules-for-multiple-sites"></a>Egyetlen engedélyezési szabálykészlet használata több helyhez

Az engedélyezési szabályok XML-fájlban tárolódnak. Alapértelmezés szerint az XML-fájl elérési útjának van _% windir %\\webes\\PowershellWebAccess\\adatok\\AuthorizationRules.xml_.

Az engedélyezési szabályok XML-fájl elérési útja tárolja a **powwa.config** fájl, amelyet az _% windir %\\webes\\PowershellWebAccess\\adatok_. A rendszergazda a rugalmasan módosíthatja az alapértelmezett elérési utat a hivatkozás **powwa.config** beállításoknak vagy követelményeknek megfelelően. Így a rendszergazdák a fájl helyének módosítása lehetővé teszi, hogy több Windows PowerShell Web Access-átjáró használja ugyanazokat az engedélyezési szabályokat, ha ilyen konfiguráció van szükség.

## <a name="session-management"></a>Munkamenet-kezelés

Alapértelmezés szerint a Windows PowerShell Web Access korlátozza a felhasználót, hogy egy adott időpontban legfeljebb három munkamenet. A webes alkalmazás szerkesztése **web.config** fájlt az IIS-kezelőben a felhasználói munkamenetek eltérő számú támogatásához.
Az elérési útját a **web.config** fájl _$Env: Windir\\webes\\PowerShellWebAccess\\wwwroot\\Web.config_.

Alapértelmezés szerint az IIS webkiszolgáló úgy van beállítva, az alkalmazáskészlet újraindítása, ha bármilyen beállítás szerkesztése. Az alkalmazáskészlet újraindul például, ha módosítás történik az **web.config** fájlt.
>Mivel **Windows PowerShell Web Access** használ memóriában tárolt munkamenet-állapotokat, bejelentkezett felhasználók **Windows PowerShell Web Access** munkamenetek munkameneteik az alkalmazáskészlet újraindításakor elveszítik.

### <a name="setting-default-parameters-on-the-sign-in-page"></a>A bejelentkezési oldalon megjelenő alapértelmezett paraméterek beállítása

Ha a Windows PowerShell Web Access-átjáró Windows Server 2012 R2 rendszeren fut, konfigurálhatja a Windows PowerShell Web Access bejelentkezési lapon megjelenő beállítások alapértelmezett értékeit. Beállíthatja, hogy az értékek a **web.config** az előző bekezdésben ismertetett fájlt. A bejelentkezési oldal beállításainak alapértelmezett értékek találhatók a **appSettings** szakasz a web.config fájl; az alábbiakban egy példát a **appSettings** szakasz. Számos beállítás érvényes értékei megegyeznek a megfelelő paraméterértékeivel a [New-PSSession](https://technet.microsoft.com/library/hh849717.aspx) a Windows PowerShell parancsmag.
Például a `defaultApplicationName` kulcs, a következő kódrészletet, ahogy az az érték a **$PSSessionApplicationName** preferenciaváltozót a célszámítógépen.

```xml
    <appSettings>
            <add key="maxSessionsAllowedPerUser" value="3"/>
            <add key="defaultPortNumber" value="5985"/>
            <add key="defaultSSLPortNumber" value="5986"/>
            <add key="defaultApplicationName" value="WSMAN"/>
            <add key="defaultUseSslSelection" value="0"/>
            <add key="defaultAuthenticationType" value="0"/>
            <add key="defaultAllowRedirection" value="0"/>
            <add key="defaultConfigurationName" value="Microsoft.PowerShell"/>
    </appSettings>
```

### <a name="time-outs-and-unplanned-disconnections"></a>Időtúllépések és nem tervezett szétkapcsolások

A Windows PowerShell Web Access munkamenetek időkorlátja lejárt. A Windows PowerShell Web Access Windows Server 2012 rendszeren fut egy időtúllépési üzenet jelenik meg, bejelentkezett felhasználók 15 perc munkamenet inaktivitás után. Ha a felhasználó az időtúllépési üzenet megjelenését követő 5 percen belül nem válaszol, a munkamenet véget ér, és a rendszer kijelentkezteti a felhasználót. Az IIS-kezelőben a webhely beállításainál módosíthatja a munkamenetekre vonatkozó időkorlátok időtartamát.

A Windows PowerShell Web Access futó Windows Server 2012 R2-ben munkamenetek időkorlátja lejárt, alapértelmezés szerint 20 perc inaktivitás után. Ha a felhasználók kapcsolódnak le a webalapú konzolon hálózati hibák vagy egyéb nem tervezett leállások vagy hibák miatt, és nem, mert azok bezárta a munkameneteket magukat, a Windows PowerShell Web Access munkamenetek folytatják a futtatja, csatlakozik célszámítógépekhez, amíg az időkorlátjuk az ügyfél oldali telik. A munkamenet leválasztása vagy az alapértelmezett 20 perc lejárata után, vagy az átjáró rendszergazdája által megadott időtartam lejárata után (amelyik rövidebb) történik meg.

Ha az átjárókiszolgáló fut a Windows Server 2012 R2, Windows PowerShell Web Access lehetővé teszi a felhasználók csatlakozni mentett munkamenetek egy későbbi időpontban, de a hálózati hibák, nem tervezett leállások vagy más hibák leválasztani a munkameneteket, amikor a felhasználók nem látják és kapcsolódjon újra mentése munkamenetekhez, amíg az átjáró által megadott időtartam lejárata után a rendszergazda lejárt.

## <a name="see-also"></a>Lásd még:

- [Telepítheti és használhatja a Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/hh831611(v=ws.11).aspx)
- [about_Session_Configurations](https://technet.microsoft.com/library/dd819508.aspx)
- [A Windows PowerShell webes elérés parancsmagjai](cmdlets/web-access-cmdlets.md)
