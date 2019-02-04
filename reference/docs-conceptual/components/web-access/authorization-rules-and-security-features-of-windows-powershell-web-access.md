---
ms.date: 06/27/2017
keywords: PowerShell, a parancsmag
title: A Webes Windows PowerShell-elérés engedélyezési szabályai és biztonsági funkciói
ms.openlocfilehash: c426b8cfb10829241ba244a5d840c91e1de9f66e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686417"
---
# <a name="authorization-rules-and-security-features-of-windows-powershell-web-access"></a>A Webes Windows PowerShell-elérés engedélyezési szabályai és biztonsági funkciói

Frissítve: 2013. június 24-én

Érvényes: Windows Server 2012 R2, Windows Server 2012

Windows PowerShell-elérés a Windows Server 2012 R2 és Windows Server 2012-alkalmazásban korlátozó biztonsági modellel rendelkezik. Felhasználók kifejezetten hozzáférést kell biztosítani ahhoz, hogy jelentkezzen be a Windows PowerShell-elérés átjáró és a webes Windows PowerShell-konzolt használja.

## <a name="configuring-authorization-rules-and-site-security"></a>Az engedélyezési szabályok és a hely biztonságának konfigurálása

Után a Windows PowerShell-elérés telepítése és az átjáró van konfigurálva, a felhasználó meg tudja nyitni a böngészőben a bejelentkezési oldal, de nem tudnak bejelentkezni mindaddig, amíg a Windows PowerShell-elérés rendszergazdai hozzáférést biztosít a felhasználónak explicit módon. "Windows PowerShell-elérés" hozzáférés-vezérlés kezeli az alábbi táblázatban ismertetett Windows PowerShell-parancsmagok használatával. Engedélyezési szabályok hozzáadásához és kezeléséhez nincs hasonló grafikus felhasználói felület.
Lásd: [Windows PowerShell webes elérés parancsmagjai](/powershell/module/powershellwebaccess/?view=winserver2012r2-ps).

Rendszergazdák meghatározhatnak `{0-n}` hitelesítési szabályokat Windows PowerShell-elérés. Az alapértelmezett biztonság inkább korlátozóak, nem pedig engedélyezők; a nulla hitelesítési szabály azt jelenti, hogy egyetlen felhasználó sem férhet hozzá semmihez.

[Add-PswaAuthorizationRule](/powershell/module/powershellwebaccess/add-pswaauthorizationrule?view=winserver2012r2-ps) és [Test-PswaAuthorizationRule](/powershell/module/powershellwebaccess/test-pswaauthorizationrule?view=winserver2012r2-ps) a Windows Server 2012 R2 tartalmaznak egy Credential paramétert, amely lehetővé teszi, hogy hozzáadását és tesztelését egy távoli Windows PowerShell-elérés engedélyezési szabályai számítógép, vagy a Windows PowerShell-elérés aktív munkamenet belül. Igény szerint a többi Windows PowerShell-parancsmagok, amelyek tartalmaznak egy Credential paramétert, megadhat egy PSCredential objektumot a paraméter értékeként. A távoli számítógépnek átadni kívánt hitelesítő adatokat tartalmazó PSCredential objektum létrehozásához futtassa a [Get-Credential](/powershell/module/microsoft.powershell.security/Get-Credential) parancsmagot.

Windows PowerShell-elérés hitelesítési szabályai engedélyezett szabályok. Minden egyes szabály egy adott Windows PowerShell, felhasználók és célszámítógépek között engedélyezett kapcsolat definíciója [munkamenet-konfigurációk](/powershell/module/microsoft.powershell.core/about/about_session_configurations?view=powershell-5.1) (más néven végpontok vagy _futási terek_) a a megadott célszámítógépeken.
A magyarázatot **futási terek** lásd [PowerShell futtatóterek használata kezdete](https://blogs.technet.microsoft.com/heyscriptingguy/2015/11/26/beginning-use-of-powershell-runspaces-part-1/)

> [!IMPORTANT]
> A felhasználónak csak egy érvényes szabályra van szüksége a hozzáférés megszerzéséhez. Ha a felhasználó kap hozzáférést egy számítógéphez a teljes nyelvi hozzáféréssel vagy csak Windows PowerShell távfelügyeleti parancsmagjaihoz való hozzáférés a webalapú konzol, a felhasználó jelentkezzen be (vagy Ugrás) más számítógépekre, amelyek az első célszámítógéphez csatlakoznak. A legbiztonságosabb módja Windows PowerShell-elérés konfigurálása, hogy csak korlátozott munkamenet-konfigurációk, amelyek lehetővé teszik, hogy szokásos módon kell távolról végrehajtani konkrét feladatok elvégzését való hozzáférés engedélyezése a felhasználóknak.

A hivatkozott parancsmagok [Windows PowerShell webes elérés parancsmagjai](/powershell/module/powershellwebaccess/?view=winserver2012r2-ps) lehetővé teszik hozzáférési szabályok engedélyezik a Windows PowerShell-elérés átjáró felhasználója használt készlet létrehozásához. A szabályok eltérnek a célszámítógépen található hozzáférés-vezérlési listáktól (ACL), és további biztonsági réteget biztosítanak a webes eléréshez. A biztonsággal kapcsolatos további részleteket a következő szakasz tartalmazza.

Ha a felhasználók nem felelnek meg az előző biztonsági rétegek bármelyikét, a böngészőjük kapott egy általános "hozzáférés megtagadva" üzenet. Habár az átjáró-kiszolgáló naplózza a biztonsági adatokat, a végfelhasználóknak nem jelenik meg információ arról, hogy hány biztonsági rétegnek feleltek meg, illetve melyik rétegnél nem sikerült a bejelentkezés vagy a hitelesítés.

Az engedélyezési szabályok konfigurálásával kapcsolatos további információkért lásd: [engedélyezési szabályok beállításával](#configuring-authorization-rules-and-site-security) ebben a témakörben.

### <a name="security"></a>Biztonság

A Windows PowerShell-elérés biztonsági modellje négy réteget egy end user a webalapú konzol, és a célszámítógép között. A rendszergazdák Windows PowerShell-elérés az IIS-kezelő konzolon kiegészítő konfigurálással további biztonsági rétegeket adhat hozzá. Az IIS-kezelő konzolon webhelyek védelmével kapcsolatos további információkért lásd: [webkiszolgáló biztonságának konfigurálása (IIS7)](https://technet.microsoft.com/library/cc731278).

További információ az IIS ajánlott eljárásokat és -szolgáltatásmegtagadásos támadások megelőzése, lásd: [ajánlott eljárások a megakadályozza, hogy DoS/szolgáltatásmegtagadási támadások ellen](https://technet.microsoft.com/library/cc750213).
A rendszergazdák is vásárol, és további kiskereskedelmi hitelesítési szoftver telepítése.

Az alábbi táblázat a végfelhasználók és a célszámítógépek között lévő négy biztonsági réteget ismerteti.

|Szint|Réteg|
|-|-|
|1|[az IIS webkiszolgáló biztonsági szolgáltatásairól](#iis-web-server-security-features)|
|2|[a Windows powershell webes hozzáférés űrlapalapú átjáró hitelesítése](#windows-powershell-web-access-forms-based-gateway-authentication)|
|3|[a Windows powershell web access engedélyezési szabályok](#windows-powershell-web-access-authorization-rules)|
|4|[cél hitelesítési és engedélyezési szabályok](#target-authentication-and-authorization-rules)|

Az egyes rétegek részletes információkat találhat a következő kategóriákban:

#### <a name="iis-web-server-security-features"></a>IIS-webkiszolgáló biztonsági funkciók

Windows PowerShell-elérés felhasználók mindig adjon meg egy felhasználónevet és jelszót a fiókjuk az átjáró hitelesítése. Azonban a rendszergazdák Windows PowerShell-elérés is is választható ügyféltanúsítvány-alapú hitelesítés ki- vagy bekapcsolja, lásd: [telepítése és használata a windows powershell-elérés](install-and-use-windows-powershell-web-access.md) teszttanúsítványt engedélyezéséhez és újabb verziók, konfigurálása egy eredeti tanúsítvánnyal).

A választható ügyféltanúsítvány-alapú szolgáltatás megköveteli, hogy a végfelhasználók felhasználónevükön és jelszavukon kívül érvényes ügyféltanúsítvánnyal rendelkezzenek, ami a webkiszolgáló (IIS) konfigurációjának részét képezi. Ha az ügyféltanúsítvány rétege engedélyezve van, akkor a Windows PowerShell-elérés bejelentkezési oldal kéri a felhasználóktól, érvényes tanúsítványok megadását, mielőtt értékeli ki a bejelentkezési hitelesítő adataikat. Ügyféltanúsítvány-alapú hitelesítés automatikusan ellenőrzi az ügyfél tanúsítványát. Ha nem található érvényes tanúsítvány, a Windows PowerShell-elérés a így azok megadhatják a tanúsítványt tájékoztatja a felhasználókat. Ha érvényes ügyféltanúsítványt talál, a Windows PowerShell-elérés megnyitja a bejelentkezési oldalt a felhasználók számára adja meg a felhasználóneveket és jelszavakat.

Itt látható egy példa az IIS webkiszolgáló által felkínált kiegészítő biztonsági beállításokra. Egyéb IIS biztonsági funkciókkal kapcsolatos további információkért lásd: [webkiszolgáló biztonságának konfigurálása (IIS 7)](https://technet.microsoft.com/library/cc731278).

#### <a name="windows-powershell-web-access-forms-based-gateway-authentication"></a>Windows PowerShell-elérés űrlapalapú átjáró hitelesítése

A Windows PowerShell-elérés bejelentkezési oldal hitelesítő adatait (felhasználónév és jelszó) szükséges, és lehetővé teszi a felhasználók a, a célszámítógéphez eltérő hitelesítő adatokat adjanak.
Ha a felhasználó nem ad meg más hitelesítő adatokat, az átjáróhoz való csatlakozáshoz használt elsődleges felhasználónév és jelszó használható a célszámítógéphez való csatlakozáshoz is.

A szükséges hitelesítő adatok hitelesítése, a Windows PowerShell Web Access-átjárón. Ezeket a hitelesítő adatokat kell érvényes felhasználói fiókkal, vagy a helyi Windows PowerShell-elérés átjárókiszolgálón, vagy az Active Directoryban.

#### <a name="windows-powershell-web-access-authorization-rules"></a>Windows PowerShell-elérés engedélyezési szabályai

Az átjáró a felhasználó hitelesítése után a Windows PowerShell-elérés engedélyezési szabályokat, győződjön meg arról, ha a felhasználó rendelkezik-e a kért célszámítógéphez való hozzáférést ellenőrzi. A sikeres hitelesítést követően a felhasználó hitelesítő adatai továbbítódnak a célszámítógépre.

A rendszer a szabályok értékelését csak a felhasználó átjáró által történt hitelesítése után, és a felhasználó célszámítógépen történő hitelesítése előtt végzi el.

#### <a name="target-authentication-and-authorization-rules"></a>Cél hitelesítési és engedélyezési szabályok

A Windows PowerShell-elérés biztonságának végső rétegét a célként megadott számítógép saját biztonsági konfigurációs. Felhasználók kell rendelkeznie a konfigurált a cél számítógépen és a Windows PowerShell-elérés engedélyezési szabályokat, a megfelelő hozzáférési jogosultságokkal futtatásához egy Windows PowerShell webalapú konzol, amely befolyásolja a célszámítógépet a Windows PowerShell-elérés keresztül.

Ez a réteg ugyanazt a biztonsági mechanizmust, amely a csatlakozási próbálkozásokat értékelné ki, ha a felhasználók megpróbálnának létrehozni egy távoli Windows PowerShell-munkamenetet a Windows Powershellen belülről a célszámítógéphez futtatásával kínálja a [Enter-PSSession](/powershell/module/microsoft.powershell.core/Enter-PSSession) vagy [New-PSSession](/powershell/module/microsoft.powershell.core/new-pssession) parancsmagok.

Alapértelmezés szerint a az átjáró és a cél számítógépen is, a Windows PowerShell-elérés használ az elsődleges felhasználónevet és jelszót. A webalapú bejelentkezési oldal, szakaszban található **választható csatlakozási beállítások**, lehetővé teszi a felhasználók a, eltérő hitelesítő adatokat adjanak a célszámítógéphez, amennyiben azok szükségesek. Ha a felhasználó nem ad meg más hitelesítő adatokat, az átjáróhoz való csatlakozáshoz használt elsődleges felhasználónév és jelszó használható a célszámítógéphez való csatlakozáshoz is.

Az engedélyezési szabályok segítségével engedélyezhető a felhasználók számára, hogy hozzáférjenek egy adott munkamenet-konfigurációhoz. Létrehozhat _korlátozott futási terek_ vagy a Windows PowerShell-elérés, a munkamenet-konfigurációk és meghatározott felhasználók számára, hogy csak meghatározott munkamenet-konfigurációk csatlakozás Windows PowerShell-elérés való bejelentkezéskor. A hozzáférés-vezérlési listák (ACL) segítségével meghatározhatja, hogy mely felhasználók férhessenek hozzá a meghatározott végpontokhoz, és a jelen szakaszban ismertetett engedélyezési szabályok használatával a felhasználók adott csoportja számára tovább korlátozhatja a végponthoz való hozzáférést. Korlátozott futtatóterek kapcsolatos további információkért lásd: [létrehozása egy korlátozott futási térrel](https://msdn.microsoft.com/library/dn614668).

### <a name="configuring-authorization-rules"></a>Az engedélyezési szabályok konfigurálása

Rendszergazdák valószínűleg szeretné azonos engedélyezési szabály a Windows PowerShell-elérés felhasználók számára, amely a Windows PowerShell távoli kezelési környezetükben már definiálva van. A jelen szakaszban található első eljárás ismerteti, hogyan adható hozzá egy olyan engedélyezési szabály, amely egy felhasználó számára biztosít hozzáférést, aki a bejelentkezés után egy számítógépet kezelhet, és csak egyetlen munkamenet-konfigurációban. A második eljárás egy olyan engedélyezési szabály eltávolítását ismerteti, amelyre már nincs szükség.

Ha azt tervezi, egyéni munkamenet-konfigurációk használatával meghatározott felhasználók számára csak a Windows PowerShell-elérés korlátozott futtatóterek belül működik, a rájuk hivatkozó engedélyezési szabályok hozzáadása előtt hozzon létre az egyéni munkamenet-konfigurációk. A Windows PowerShell-elérés parancsmagjai nem hozhat létre egyéni munkamenet-konfigurációk. Egyéni munkamenet-konfigurációk létrehozásával kapcsolatos további információkért lásd: [about_Session_Configuration_Files](/powershell/module/microsoft.powershell.core/about/about_session_configuration_files).

Windows PowerShell-elérés parancsmagjai támogatja egy helyettesítő karaktert, a csillag ( \* ). A helyettesítő karakterek nem használhatók a sztringeken belül; tulajdonságonként (felhasználók, számítógépek vagy munkamenet-konfigurációk) egyetlen csillag használható.

> [!NOTE]
> A témakör a további lehetőségek az engedélyezési szabályok segítségével felhasználók hozzáférésének megadásához és a Windows PowerShell-elérés környezet biztonságának [más engedélyezési szabály forgatókönyv példáit](#other-authorization-rule-scenario-examples) ebben a témakörben.

#### <a name="to-add-a-restrictive-authorization-rule"></a>Korlátozó engedélyezési szabály hozzáadása

1. Hajtsa végre az alábbi lépéseket egy Windows PowerShell-munkamenetet emelt szintű felhasználói jogosultsággal nyissa meg.

   - A Windows asztalon kattintson a jobb gombbal **Windows PowerShell** a tálcán, és kattintson a **Futtatás rendszergazdaként**.

   - A Windows a **Start** kattintson a jobb gombbal **Windows PowerShell**, és kattintson a **Futtatás rendszergazdaként**.

2. **Nem kötelező lépés** felhasználói hozzáférés korlátozására munkamenet-konfigurációk használatával:

   Győződjön meg arról, hogy a munkamenet-konfigurációk, amelyeket szeretne használni, már léteznek a szabályokban.

   Ha azok még nem lett hozott, alkalmaznia munkamenet-konfigurációk létrehozására vonatkozó [about_Session_Configuration_Files](/powershell/module/microsoft.powershell.core/about/about_session_configuration_files).

3. Ez az engedélyezési szabály lehetővé teszi egy adott felhasználó hozzáférését egy adott számítógépre a hálózaton, amelyhez általában van hozzáférése egy adott munkamenet-konfiguráció, ami a felhasználói hozzáférést a(z)™ s tipikus parancsfájl-kezelési és parancsmag-igényeihez. Írja be a következőt, majd nyomja le **Enter**.

   ```
   Add-PswaAuthorizationRule -UserName <domain\user | computer\user> `
      -ComputerName <computer_name> -ConfigurationName <session_configuration_name>
   ```

   - A következő példában egy felhasználó nevű _JSmith_ a a _Contoso_ tartományi hozzáférést kap a számítógép felügyeletéhez _Contoso_214_, és a egy munkamenet-konfiguráció használata _NewAdminsOnly_.

   ```powershell
   Add-PswaAuthorizationRule -UserName 'Contoso\JSmith' `
      -ComputerName Contoso_214 -ConfigurationName NewAdminsOnly
   ```

4. Győződjön meg arról, hogy az a szabály futtatásával hozták-e a **Get-PswaAuthorizationRule** parancsmagot, vagy `Test-PswaAuthorizationRule -UserName <domain\user | computer\user> -ComputerName** <computer_name>`.
   Például: `Test-PswaAuthorizationRule -UserName Contoso\\JSmith -ComputerName Contoso_214`.

#### <a name="to-remove-an-authorization-rule"></a>Az engedélyezési szabály eltávolítása

1. Ha egy Windows PowerShell-munkamenetben még nem nyitott, tekintse meg az 1. lépés a [korlátozó engedélyezési szabály hozzáadása](#to-add-a-restrictive-authorization-rule) ebben a szakaszban.

2. Írja be a következőt, majd nyomja le **Enter**, ahol *szabályazonosítóval* jelöli, hogy el kívánja távolítani a szabály az egyedi azonosító szám.

   ```
   Remove-PswaAuthorizationRule -ID <rule ID>
   ```

   Másik lehetőségként, ha nem ismeri a azonosítószámát, de tudja az eltávolítani kívánt szabály rövid nevét, is a szabály nevét, és átadhatja azt a `Remove-PswaAuthorizationRule` parancsmagot, hogy a szabály eltávolításához az alábbi példában látható módon:

   ```
   Get-PswaAuthorizationRule `
      -RuleName <rule-name> | Remove-PswaAuthorizationRule
   ```

> [!NOTE]
> A rendszer nem kéri, erősítse meg, hogy szeretné-e a megadott engedélyezési szabály; törlése a szabály törlődik, amikor lenyomja **Enter**. A `Remove-PswaAuthorizationRule` parancsmagot csak akkor futtassa, ha biztosan el kívánja távolítani az engedélyezési szabályt.

#### <a name="other-authorization-rule-scenario-examples"></a>Példák az engedélyezési szabály egyéb eltávolítási módjaira

Minden Windows PowerShell-munkamenetben; munkamenet-konfigurációt használ Ha az egyik egy munkamenethez nincs megadva, a Windows PowerShell az alapértelmezett, beépített Windows PowerShell munkamenet-konfiguráció, neve Microsoft.PowerShell használja. Az alapértelmezett munkamenet-konfiguráció a számítógépen elérhető összes parancsmagot tartalmazza. A rendszergazdák egy korlátozott futási teret (a parancsmagok és a végfelhasználóik által végrehajtható feladatok korlátozott tartománya) tartalmazó munkamenet-konfiguráció definiálásával korlátozhatják az összes számítógéphez való hozzáférést. A felhasználó, aki egy számítógép teljes nyelvi hozzáféréssel vagy csak a Windows PowerShell távfelügyeleti parancsmagjaihoz való hozzáféréssel csatlakozhat más számítógépek, amelyek az első számítógéphez csatlakoznak. Korlátozott futási térrel definiálása megakadályozhatja, hogy a felhasználók a saját engedélyezett Windows PowerShell futási térben más számítógépek elérése, és biztonságosabbá teszi a Windows PowerShell-elérés környezetében. A munkamenet-konfigurációt azokon a számítógépeken, amelyek a rendszergazdák elérhetővé kívánnak tenni keresztül a Windows PowerShell-elérés terjeszthetők ki (a csoportházirend használatával). Munkamenet-konfigurációkkal kapcsolatos további információkért lásd: [about_Session_Configurations](https://technet.microsoft.com/library/dd819508.aspx). Az alábbiakban bemutatunk néhány példát erre a témakörre.

- A rendszergazda létrehoz egy végpontot, nevű **PswaEndpoint**, korlátozott futási térrel. Ezt követően a rendszergazda létrehoz egy szabályt `*,*,PswaEndpoint`, és elosztja a végpontot a többi számítógéphez. A szabály lehetővé teszi, hogy minden felhasználó számára a végponttal rendelkező minden számítógép **PswaEndpoint**.
  Ha a szabálykészletben ez az egyetlen definiált engedélyezési szabály, az ezzel a végponttal nem rendelkező számítógépek nem lesznek elérhetők.

- A rendszergazda létrehozott egy végpontot egy korlátozott futási térrel rendelkező nevű **PswaEndpoint**, és bizonyos felhasználók hozzáférését korlátozni kívánja. A rendszergazda létrehoz egy csoport nevű **Level1Support**, és a következő szabályt definiálja: **Level1Support,\*, PswaEndpoint**. A szabály engedélyezi a csoportban lévő egyik felhasználóra sem **Level1Support** összes számítógépet, amelynél a hozzáférést a **PswaEndpoint** konfigurációja. Hasonlóképpen, a hozzáférés korlátozható egy meghatározott számítógépcsoportra.

- Néhány rendszergazda bizonyos felhasználóknak több hozzáférést biztosít, mint a többieknek. Ha például a rendszergazda létrehoz két felhasználói csoportot, **rendszergazdák** és **BasicSupport**. A rendszergazda létrehoz továbbá egy végpontot egy korlátozott futási teret nevű **PswaEndpoint**, és a következő két szabályt definiálja: **A rendszergazdák,\*,\***  és **BasicSupport,\*, PswaEndpoint**. Az első szabály lévő összes felhasználó számára biztosít a **rendszergazdai** az összes számítógép és a második szabály a csoport hozzáférést biztosít az összes felhasználó a **BasicSupport** csoporthoz hozzáféréssel rendelkező számítógépekhez csak  **PswaEndpoint**.

- A rendszergazda beállított egy privát tesztkörnyezetet, és szeretné engedélyezni az összes jogosult hálózati felhasználó számára a hozzáférést a hálózaton található összes olyan számítógéphez, amelyhez általában hozzáférhetnek, az összes olyan munkamenet-konfigurációhoz való hozzáféréssel, amelyhez általában hozzáférhetnek. Mivel ez egy privát tesztkörnyezet, a rendszergazda egy nem biztonságos engedélyezési szabályt hoz létre. – A rendszergazda futtatja a parancsmagot `Add-PswaAuthorizationRule * * *`, helyettesítő karaktert használja, amely **\*** minden felhasználó, az összes számítógép és az összes konfiguráció képviseletére. – Ez a szabály megegyezik a következők közül: `Add-PswaAuthorizationRule -UserName * -ComputerName * -ConfigurationName *`.

  > [!NOTE]
  > Ez a szabály biztonságos környezetben nem ajánlott, és figyelmen kívül hagyja a rétegre vonatkozó engedélyezési szabályt Windows PowerShell-elérés által biztosított biztonsági.

- A rendszergazdának egy olyan környezetben kell engedélyeznie a felhasználók számára a célszámítógépekhez történő csatlakozást, amely egyaránt tartalmaz munkacsoportokat és tartományokat, ahol munkacsoportok számítógépeit alkalmanként a tartományokban lévő célszámítógépekhez való csatlakozáshoz használják, a tartományokban levő számítógépeket pedig alkalmanként a munkacsoportokban lévő célszámítógépekhez való csatlakozáshoz használják. A rendszergazda egy átjárókiszolgáló *PswaServer*, munkacsoportban; és a célszámítógép *srv1.contoso.com* tartományban van. Felhasználói *Chris* jogosult helyi felhasználója a munkacsoport átjárókiszolgálónak és a cél számítógépen is van. A munkacsoport-kiszolgálón a felhasználónév *chrisLocal*; a felhasználó neve, a célszámítógépen pedig *contoso\\chris*. Ahhoz, hogy engedélyezze Chris számára a srv1.contoso.com célszámítógéphez való hozzáférést, rendszergazda a következő szabályt adja hozzá.

```powershell
Add-PswaAuthorizationRule -userName PswaServer\chrisLocal `
   -computerName srv1.contoso.com -configurationName Microsoft.PowerShell
```

Az előző példában a szabály hitelesíti Christ az átjárókiszolgálón, majd engedélyezi számára a hozzáférést a *srv1*. A bejelentkezési oldalon Chrisnek meg kell adnia a hitelesítő adatokat egy második együttesét a **választható csatlakozási beállítások** területen (*contoso\\chris*). Az átjáró-kiszolgálót a további hitelesítő adatokat használja a cél számítógépen hitelesíti *srv1.contoso.com*.

Az előző esetben a Windows PowerShell-elérés a cél számítógéphez sikeres kapcsolatot létesít a csak után a következő volt sikeres, és legalább egy engedélyezési szabály által engedélyezett.

1. Hitelesítés a munkacsoport átjárókiszolgálónak egy felhasználónevet a következő formátumban hozzáadásával *kiszolgáló_neve*\\*felhasználónév* az engedélyezési szabály

2. Hitelesítés a célszámítógépen a bejelentkezési oldalon a megadott másodlagos hitelesítő adatok használatával a **választható csatlakozási beállítások** terület

   > [!NOTE]
   > Ha az átjáró-számítógép és a célszámítógép különböző munkacsoportokban vagy tartományokban vannak, megbízhatósági kapcsolatot kell létrehozni a két munkacsoport-számítógép, a két tartomány vagy a munkacsoport és a tartomány között. Ez a kapcsolat nem konfigurálható a Windows PowerShell-elérés engedélyezési szabályokra vonatkozó parancsmagjainak használatával. Az engedélyezési szabályok nem határoznak meg megbízhatósági kapcsolatot a számítógépek között, csak a felhasználóknak engedélyezik, hogy az adott célszámítógépekhez és munkamenet-konfigurációkhoz csatlakozzanak. Különböző tartományok közötti megbízhatósági kapcsolat konfigurálásával kapcsolatos további információkért lásd: [létrehozása tartományi és erdőszintű Megbízhatóságok](https://technet.microsoft.com/library/cc794775.aspx).
   > További információ a munkacsoport-számítógépek hozzáadása a megbízható gazdagépek listájához: [távoli felügyelet a Kiszolgálókezelővel](https://technet.microsoft.com/library/dd759202.aspx).

### <a name="using-a-single-set-of-authorization-rules-for-multiple-sites"></a>Egyetlen engedélyezési szabálykészlet használata több helyhez

Az engedélyezési szabályok XML-fájlban tárolódnak. Alapértelmezés szerint az XML-fájl elérési útja a `$env:windir\Web\PowershellWebAccess\data\AuthorizationRules.xml`.

Az engedélyezési szabályok XML-fájl elérési útját tárolja a **powwa.config** fájlt, amely megtalálható a `$env:windir\Web\PowershellWebAccess\data`. A rendszergazda rugalmasan módosíthatja az alapértelmezett elérési utat mutató hivatkozás **powwa.config** vagy követelményeknek megfelelően. Lehetővé teszi a rendszergazda módosíthatja a fájl helyét lehetővé teszi, hogy több Windows PowerShell-elérés átjáró használja ugyanazokat az engedélyezési szabályokat, ha ilyen konfiguráció van szükség.

## <a name="session-management"></a>Munkamenet-kezelés

Alapértelmezés szerint a Windows PowerShell-elérés egy felhasználó egy adott időpontban legfeljebb három munkamenet használatára korlátozza. Szerkesztheti a webalkalmazás **web.config** fájlt az IIS-kezelő felhasználói munkamenetek különböző számú támogatásához. Az elérési útját a **web.config** fájl `$env:windir\Web\PowerShellWebAccess\wwwroot\Web.config`.

Alapértelmezés szerint az IIS webkiszolgáló úgy van beállítva, az alkalmazáskészlet újraindítása, ha bármilyen beállítás szerkesztése. Az alkalmazáskészlet újraindul például, ha a módosítások a **web.config** fájlt. > mert **Windows PowerShell-elérés** használ a memórián belüli munkamenet-állapotok, > bejelentkezett felhasználók **Windows PowerShell-elérés** munkamenetek elveszítik munkameneteiket, amikor az alkalmazáskészlet újraindul.

### <a name="setting-default-parameters-on-the-sign-in-page"></a>A bejelentkezési oldalon megjelenő alapértelmezett paraméterek beállítása

Ha a Windows PowerShell-elérés átjáró Windows Server 2012 R2 rendszeren fut, konfigurálhatja a Windows PowerShell-elérés bejelentkezési lapon megjelenő beállítások alapértelmezett értékeit. Beállíthatja, hogy az értékek a **web.config** fájlt, amely az előző bekezdésben leírt. A bejelentkezési oldal beállításainak alapértelmezett értékek találhatók a **appSettings** szakasz a web.config fájl; az alábbiakban egy példát a a **appSettings** szakaszban. Számos beállítás érvényes értékei a következők ugyanazok, mint a megfelelő paraméterértékeivel a [New-PSSession](https://technet.microsoft.com/library/hh849717.aspx) parancsmagot a Windows PowerShellben.

Ha például a `defaultApplicationName` kulcs, ahogyan az az alábbi kódblokkot az az érték a **$PSSessionApplicationName** preferenciaváltozó a célszámítógépen.

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

Windows PowerShell-elérés munkamenetek időkorlátja lejárt. A Windows PowerShell-elérés Windows Server 2012 rendszeren fut egy időtúllépési üzenet jelenik meg a bejelentkezett felhasználók számára 15 perc a munkamenet inaktivitás után. Ha a felhasználó az időtúllépési üzenet megjelenését követő 5 percen belül nem válaszol, a munkamenet véget ér, és a rendszer kijelentkezteti a felhasználót. Az IIS-kezelőben a webhely beállításainál módosíthatja a munkamenetekre vonatkozó időkorlátok időtartamát.

A Windows PowerShell-elérés futó Windows Server 2012 R2, a munkamenetek időkorlátja lejárt, alapértelmezés szerint 20 perc inaktivitás után. Ha a felhasználók közül a webalapú konzolon hálózati hibák vagy egyéb nem tervezett leállások vagy hibák miatt, és nem azért, mert azok bezárta a munkameneteket magukat, a Windows PowerShell-elérés munkamenetek folytatják a futást, csatlakoztatva célszámítógépekhez, amíg az ügyfél oldalán le nem telik időkorlát. A munkamenet leválasztása vagy az alapértelmezett 20 perc lejárata után, vagy az átjáró rendszergazdája által megadott időtartam lejárata után (amelyik rövidebb) történik meg.

Ha az átjáró-kiszolgálót futtat Windows Server 2012 R2, Windows PowerShell-elérés lehetővé teszi a felhasználók mentett munkamenetek egy későbbi időpontban, de a hálózati hibák, nem tervezett leállások vagy más hibák leválasztani a munkameneteket, amikor a felhasználók nem látják és újból menteni mindaddig, amíg az átjáró által meghatározott időkorlát időtartama után a rendszergazda lejárt munkamenet.

## <a name="see-also"></a>Lásd még:

[Telepítheti és használhatja a Windows PowerShell-Elérésbe](https://technet.microsoft.com/library/hh831611(v=ws.11).aspx)

[about_Session_Configurations](https://technet.microsoft.com/library/dd819508.aspx)

[Windows PowerShell webes elérés parancsmagjai](/powershell/module/powershellwebaccess/?view=winserver2012r2-ps)
