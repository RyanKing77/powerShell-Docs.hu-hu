---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Lekérési kiszolgáló – ajánlott eljárások
ms.openlocfilehash: fe483a487f85f2e4edb0928fccfe98746ae11231
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58057705"
---
# <a name="pull-server-best-practices"></a>Lekérési kiszolgáló – ajánlott eljárások

Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

> [!IMPORTANT]
> A lekéréses kiszolgálón (Windows-szolgáltatás *DSC-szolgáltatás*), a Windows Server támogatott összetevője létezik azonban tervekben sem funkciókat és képességeket kínálnak. Javasoljuk, hogy helyeződnek felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (beleértve a lekéréses kiszolgálón a Windows Server csomagban) vagy a közösségi megoldások felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).

Összegzés: Ez a dokumentum célja a folyamat és bővíthetőség felhőkarrierre készítik megoldás-mérnökök segítségét. Részletek ajánlott eljárásokat kell biztosítania, ügyfél által azonosított, és a termék csapatától javaslatok jövőbeli irányuló és stabil tekinthető majd érvényesíteni.

| |Dokumentum adatai|
|:---|:---|
Szerző | Michael Greene
Lektorok | Ben Gelens, Ravikanth Chaganti, Aleksandar Nikolic
Közzétett | 2015. április

## <a name="abstract"></a>Absztrakt

Jelen dokumentum célja, hogy mindenkinek, aki egy Windows PowerShell Desired State Configuration lekéréses kiszolgálón megvalósítás hivatalos útmutatást. Egy lekéréses kiszolgálót az egyszerű szolgáltatás csak perc alatt üzembe helyezéséhez. Bár ez a dokumentum műszaki útmutatókról, a központi telepítés használható tartalmazni fogja, ez a dokumentum értéke az ajánlott eljárásokat, és milyen üzembe helyezése előtt gondolja át hivatkozásként.
Olvasói rendelkeznie kell a DSC alapszintű ismeretét, és az összetevők leírására szolgáló a feltételeket, amelyek központi telepítésben lévő a DSC. További információkért lásd: a [Windows PowerShell Desired State Configuration áttekintése](/powershell/dsc/overview) témakör.
DSC elvárt való összpontosításnak köszönhetően felhőalapú kiadása ütemben történik, az alapul szolgáló technológiát, beleértve a lekéréses kiszolgálón is várható fejlődnek, és új lehetőségeket biztosítanak. Ez a dokumentum egy verzió tábla tartalmaz, amely a korábbi kiadásokban mutató hivatkozások és a jövőbeli akik megoldások előretekintő tervek ösztönzése mutató hivatkozásokat biztosít a függelékben.

A két fő szakasz ebben a dokumentumban:

- Konfiguráció tervezése
- Telepítési útmutató

### <a name="versions-of-the-windows-management-framework"></a>A Windows Management Framework verziói

A jelen dokumentumban lévő információk célja a alkalmazni a Windows Management Framework 5.0. Bár a WMF 5.0 nem kötelező központi telepítésére és a egy lekéréses kiszolgálót működő, a 5.0-s verzió a lépéseknek az ismertetése, ez a dokumentum.

### <a name="windows-powershell-desired-state-configuration"></a>Windows PowerShell Desired State Configuration

Desired State Configuration (DSC) egy felügyeleti platform, amely lehetővé teszi a konfigurációs adatokat, üzembe helyezése és felügyelete egy ipar szintaxisa a Managed Object Format (MOF) nevű leíró a Common Information Model (CIM) használatával. Egy nyílt forráskódú projekt, nyissa meg a Management Infrastructure (OMI) további ezeknek a szabványoknak a fejlesztés különböző platformokon, beleértve a Linux és a hálózati hardverek, operációs rendszerek létezik. További információkért lásd: a [összekapcsolása a MOF-specifikációk DMTF lap](https://www.dmtf.org/standards/cim), és [OMI a következő dokumentumok és a forrás](https://collaboration.opengroup.org/omi/documents.php).

Windows PowerShell egy nyelvet bővítménycsomag biztosít a Desired State Configuration, amellyel létrehozása és kezelése a deklaratív konfigurációkat.

### <a name="pull-server-role"></a>Kérje le a kiszolgálói szerepkör

Egy lekéréses kiszolgálót biztosít lesznek elérhetőek a célcsomópontokat konfigurációk tárolásához egy központosított szolgáltatásba.

A pull-kiszolgálói szerepkör egy Web Server-példányt vagy SMB-fájlmegosztásra is telepíthető. A web server funkció OData illesztőfelületet tartalmazza, és szükség esetén belefoglalhatja vissza erősítse meg a sikeres vagy sikertelen jelentés, mivel a beállítások vannak érvényben a célcsomópontokat képességeit. Ez a funkció olyan környezetben hasznos, ahol sok célcsomópontokat.
Egy célcsomóponttal (más néven ügyfél) konfigurálását, hogy a lekéréses kiszolgálóra mutasson a legújabb konfigurációt követő adatokat, és minden szükséges szkriptek vannak letöltésére és alkalmazására. Ez akkor fordulhat elő, egy egyszeri központi telepítést, vagy egy újra előforduló feladatot, amely is lehetővé teszi a lekéréses kiszolgálón fontos eszközt nagy mennyiségű módosítás kezeléséhez. További információkért lásd: [Windows PowerShell Desired State Configuration lekéréses kiszolgálók](/powershell/dsc/pullServer) és

[Leküldéses és lekéréses konfigurációs módjai](/powershell/dsc/pullServer).

## <a name="configuration-planning"></a>Konfiguráció tervezése

Minden vállalati szoftverek központi telepítéséhez nincs információ előre gyűjtött a megfelelő architektúra tervezésének segítéséhez és elő kell készíteni a a telepítés befejezéséhez szükséges lépéseket. A következő szakaszok előkészítése és a szervezeti kapcsolatokat, amelyek valószínűleg fordulhat elő, előre kell kapcsolatos információkat.

### <a name="software-requirements"></a>Szoftverkövetelmények

Egy lekéréses kiszolgálót telepítése a DSC szolgáltatás Windows Server igényel. Ez a funkció a Windows Server 2012-ben jelent meg, és folyamatban lévő verziók Windows Management Framework (WMF) keresztül frissítve lett.

### <a name="software-downloads"></a>Az ügyfélszoftver-letöltési

Telepíti a legújabb tartalom a Windows Update, kívül két letöltések üzembe helyezése egy DSC lekéréses kiszolgálót célszerű figyelembe venni: A Windows Management Framework, és a DSC-modul a pull-kiszolgáló üzembe helyezésének automatizálása legújabb verzióját.

### <a name="wmf"></a>WMF

A Windows Server 2012 R2 tartalmaz egy a DSC szolgáltatás nevű funkciót. A DSC szolgáltatás lekéréses server funkciókat, beleértve a bináris fájlokat, amelyek támogatják az OData-végpont biztosítja.
A WMF része a Windows Server, és a egy Agilis kiadása ütemben történik a Windows Server-kiadások között frissül. [A WMF 5.0 új verzióinak](https://www.microsoft.com/en-us/download/details.aspx?id=54616) a DSC szolgáltatás frissítéseket is tartalmaz. Emiatt tanácsos egy töltse le a WMF legújabb kiadását, és tekintse át a kibocsátási megjegyzéseket határozza meg, ha a kiadás a DSC szolgáltatás frissítését tartalmazza. Emellett tekintse át a kibocsátási megjegyzések a szakaszában, amely azt jelzi-e egy update vagy a forgatókönyv tervezési állapota stabil vagy kísérleti szerepel a listán.
Ahhoz, hogy egy Agilis kiadási ciklus egyes funkciókat is deklarálni stabil, ami azt jelenti, hogy a szolgáltatás készen áll az előzetes verzióban jelent meg a WMF közben is az éles környezetben használható.
Egyéb szolgáltatások hagyományosan frissítve lett-e a WMF-verziók (lásd a további részletek a WMF kibocsátási megjegyzései):

- Windows PowerShell Windows PowerShell integrált parancsfájlkezelési
- Környezet (ISE) Windows PowerShell webszolgáltatások (Management OData
- IIS-bővítmény) Windows PowerShell Desired State Configuration (DSC)
- Windows Rendszerfelügyeleti (webszolgáltatások WinRM) Windows Management Instrumentation (WMI)

### <a name="dsc-resource"></a>DSC-erőforrás

Egy lekéréses kiszolgálót üzembe helyezési is egyszerűbb legyen a létesítési DSC konfigurációs parancsfájl használata a szolgáltatás által. Ez a dokumentum tartalmaz egy éles készen áll a kiszolgáló-csomóponton üzembe helyezéséhez használható konfigurációs parancsfájlokat. A konfigurációs parancsfájlokat használ, a DSC-modul szükség, amely nem tartalmazza a Windows Server. A szükséges modulnév **xPSDesiredStateConfiguration**, amely tartalmazza a DSC-erőforrás **xDscWebService**. A xPSDesiredStateConfiguration modul letölthető [Itt](https://gallery.technet.microsoft.com/xPSDesiredStateConfiguratio-417dc71d).

Használja a `Install-Module` parancsmagot a **PowerShellGet** modul.

```powershell
Install-Module xPSDesiredStateConfiguration
```

A **PowerShellGet** modul tölti le a modult:

`C:\Program Files\Windows PowerShell\Modules`

A tervezési feladat|
---|
Rendelkezik hozzáféréssel a telepítési fájlok, Windows Server 2012 R2?|
Töltse le a WMF és a modul az online katalógusból internetes hozzáférést kap az üzembehelyezési környezetet?|
Hogyan telepíti az operációs rendszer telepítése után a legújabb biztonsági frissítéseket?|
A környezet van Internet-hozzáférés frissítések beszerzésére, vagy fog rendelkezni a helyi Windows Server Update Services (WSUS) kiszolgáló?|
Rendelkeznek hozzáféréssel a Windows Server telepítési fájlok, amelyek már tartalmazzák az offline injektálási frissítéseit?|

### <a name="hardware-requirements"></a>Hardverkövetelmények

Kérje le a telepítések támogatottak a fizikai és virtuális kiszolgáló. A lekéréses kiszolgálón méretezési követelményei összhangba kerüljenek a Windows Server 2012 R2 követelményei.

Processzor: 1,4 GHz-es 64 bites processzor, memória: 512 MB szabad lemezterület: 32 GB-os hálózati: Gigabit Ethernet Adapter

A tervezési feladat|
---|
Telepíti a fizikai hardver- vagy virtualizációs platformon?|
Mi az a folyamat egy új kiszolgálót a célkörnyezethez kéréséhez?|
Mi az a kiszolgáló elérhető legyen, az átlagos válaszidő?|
Milyen méretű server kérés?|

### <a name="accounts"></a>Fiókok

Nem vonatkoznak szolgáltatási fiók követelmények egy lekéréses kiszolgálót példány üzembe helyezéséhez.
Vannak azonban forgatókönyvek, ahol a webhely futhat egy helyi felhasználói fiók kontextusában.
Például ha egy szükséges hozzáférést egy storage-megosztásban webhely tartalmát, és a Windows Server vagy az eszköz, a storage-megosztás üzemeltetési nem lesznek tartományhoz.

### <a name="dns-records"></a>DNS records

Szüksége lesz a kívánt kiszolgáló nevét használja, ha az ügyfelek egy lekéréses kiszolgálót környezetben dolgozhat.
A tesztelési jellemzően a kiszolgáló állomásnevét vagy a kiszolgáló IP-címét is használható, ha a DNS-névfeloldás nem érhető el.
Az éles környezetben, vagy egy laborkörnyezetben, amelyek célja, hogy az éles környezet jelölik az ajánlott eljárás az hozzon létre egy DNS CNAME-rekordot.

Egy DNS CNAME rekord lehetővé teszi, hogy hozzon létre egy alias tekintse meg a gazdagép (A) rekordot.
A további rekordhoz célja egy módosítást kell kérni a jövőben rugalmasság növelésére.
Egy olyan CNAME REKORDOT segít elkülöníteni az ügyfél-konfiguráció, így, például kicserél egy lekéréses kiszolgálót, vagy további pull-kiszolgálók hozzáadása a kiszolgálói környezet módosításai nem követeli meg az ügyfél-konfiguráció megfelelő módosítása.

Egy nevet a DNS-rekord kiválasztásakor tartsa szem előtt a megoldásarchitektúra.
Ha használ terheléselosztási funkciók, a HTTPS-kapcsolaton keresztül a forgalom védelmére használt tanúsítvány neve megegyezik a DNS-rekord kell.

Forgatókönyv |Ajánlott eljárás
:---|:---
Tesztkörnyezet |Reprodukálja a tervezett éles környezetben, ha lehetséges. A kiszolgáló állomásnevét egyszerű konfigurációk esetén ideális választás. DNS nem érhető el, ha egy IP-címet egy állomásnév helyett használhatók.|
Egy csomópontos központi telepítés |Hozzon létre egy DNS CNAME-rekordot, amely a kiszolgáló állomásnevét.|

További információkért lásd: [DNS ciklikus időszeletelés konfigurálása a Windows Server](/previous-versions/windows/it-pro/windows-server-2003/cc787484(v=ws.10)).

A tervezési feladat|
---|
Tudta, hogy kihez kell fordulnia, hogy a DNS-rekordok létrehozott és módosított?|
Mi a DNS-rekordra vonatkozó kérelmek átlagos felülvizsgálatának?|
Szükséges a kiszolgálók statikus állomásnevet (A) rekordok kérelem?|
Mit fog kér, egy CNAME rekord?|
Ha szükséges, hogy milyen típusú terheléselosztási megoldás, felhasznál? (lásd a részre terheléselosztás részletekért)|

### <a name="public-key-infrastructure"></a>Nyilvános kulcsokra épülő infrastruktúra

A legtöbb szervezet ma szükséges, hogy hálózati forgalmat, különösen olyan forgalmat, hogy hogyan kiszolgálók konfigurálva vannak, például bizalmas adatokat tartalmazó ellenőrizni kell, illetve átvitel során titkosítva vannak.
Bár egy lekéréses kiszolgálót, amely elősegíti a HTTP-n keresztül telepíthető az ügyfélkérelmek törölje a szöveget, hogy az ajánlott eljárás a HTTPS PROTOKOLLT használó biztonságos forgalom. A szolgáltatás beállítható úgy, hogy a különböző paraméterek használatával a DSC-erőforrás a HTTPS használatára **xPSDesiredStateConfiguration**.

A tanúsítványokra vonatkozó követelményeket a biztonságos HTTPS-forgalmat a lekéréses kiszolgálón eltérése nem mint bármely más HTTPS webhely biztonságossá tételéhez. A **webkiszolgáló** egy Windows Server tanúsítványszolgáltatási sablon megfelel a szükséges képességek.

A tervezési feladat|
---|
Ha eszköztanúsítvány-kérelmeket a rendszer nem automatikus, akik szükség lesz egy tanúsítványt a kérelmekre kapcsolódni?|
Mi az a kérelem az átlagos válaszidejű, optimalizált?|
Hogyan fogja a tanúsítványfájl adni az Ön számára?|
Hogyan fogja a tanúsítvány titkos kulcsa adni az Ön számára?|
Mennyi ideig tart az alapértelmezett lejárati idő?|
Rendelkezik, a DNS-nevet a pull-kiszolgálói környezet, a tanúsítvány neve használható elszámolása?|

### <a name="choosing-an-architecture"></a>Az architektúra kiválasztása

Egy lekéréses kiszolgálót is telepíthető, vagy egy webes üzemeltetett szolgáltatás az IIS- vagy SMB-fájlmegosztás segítségével. A legtöbb esetben nagyobb rugalmasságot biztosít a web service lehetőséget. Már nem ritka, hogy HTTPS-forgalmat haladnak át a hálózati határok, mivel az SMB-forgalom gyakran szűrt vagy letiltott hálózatok között. A web service is lehetősége a megfelelési kiszolgáló vagy a webes Reporting Manager (mindkét ezeket egy jövőbeli verziójában ez a dokumentum az témakörök), amely az ügyfelek állapot jelentése egy központi látható-e a kiszolgálóra egy olyan mechanizmust kínál.
SMB környezetekben, ahol házirend előírja, hogy a webkiszolgáló nem használhatók fel, és az egyéb környezeti követelményeket, amelyek elérhetőbbé teszik a webkiszolgálói szerepkör nemkívánatos lehetőséget biztosít.
Mindkét esetben ne felejtse el a követelményeknek, az aláíráshoz és a forgalom titkosítása értékelheti ki. IPSEC-házirendek, HTTPS és SMB-aláírást mellett szóló érvek összes módon.

#### <a name="load-balancing"></a>Terheléselosztás

A web service kommunikáló ügyfelek indítson egy információt, amely egy választ adott vissza. Nem egymást követő kéréseket szükségesek, így nem szükséges a terheléselosztási platform munkamenetek karbantartása bármikor egyetlen kiszolgálón az idő biztosítása érdekében.

A tervezési feladat|
---|
Milyen megoldás elosztja a forgalmat kiszolgálók használható?|
Ha hardveres terheléselosztót, akik tart egy új konfiguráció hozzáadása az eszközre irányuló kérelem használatával?|
Mi az a konfigurálása egy új betöltés kérelmek átlagos felülvizsgálatának elosztott terhelésű webszolgáltatást?|
Milyen információt szükséges a kérelem lesz?|
Meg kell kérnie egy további IP-cím, vagy a terheléselosztás felelős csapat kezeli, amely?|
Rendelkezik a szükséges DNS-rekordokat, és ez szükség lesz a terheléselosztási megoldás konfigurálása felelős csapat?|
A teherelosztási szolgáltatás nem követeli meg, hogy a nyilvános kulcsokra épülő infrastruktúra kell kezelnie a az eszközt, vagy tudja azt terheléselosztása HTTPS-forgalmat, mindaddig, amíg nem vonatkoznak munkamenet követelmények?|

### <a name="staging-configurations-and-modules-on-the-pull-server"></a>Átmeneti konfigurációk és a modulok a lekérési kiszolgálón

A konfiguráció tervezése részeként szüksége lesz úgy gondolja, hogy mely DSC kapcsolatos modulok és konfigurációk üzemeltetett a lekéréses kiszolgálón. Konfiguráció tervezése szempontjából fontos alapfokon bemutatja, hogyan készítheti elő és a egy lekéréses kiszolgálót telepít tartalmat.

A jövőben ez a szakasz kiterjesztett lesz, és az DSC lekéréses kiszolgálón található az üzemeltetési útmutatóban.  Útmutató a modulok és konfigurációk kezelése az automation idővel napi folyamatát ismertetik.

#### <a name="dsc-modules"></a>DSC-modulok

Egy konfigurációs kérő ügyfelek kell a szükséges modulok DSC. A lekéréses kiszolgálón egy funkciója, automatizálhatja a DSC-modulok az ügyfelek igény szerinti eloszlása. Ha helyez üzembe egy lekéréses kiszolgálót az első alkalommal esetleg labor vagy a koncepció igazolása, valószínűleg fog függenek a DSC-modulok által biztosított nyilvános adattár, például a PowerShell-Galériával vagy a modulok DSC PowerShell.org GitHub-adattárak .

Fontos megjegyezni, hogy még a megbízható online forrásokból, például a PowerShell-galériából, egy nyilvános-tárházból letölti modulok át kell tekintenie valaki a PowerShell és a környezetben, ahol a modulok lesz ismerete éles környezetben használt előtt használt. Ez a feladat végrehajtása során, egy jó ideje a modul, amely például a dokumentáció és szkriptek eltávolítható minden olyan további hasznos kereséséhez. Ez csökkenti a hálózati sávszélesség, az első kérelem ügyfelenként amikor modulok letölti az ügyfél-kiszolgálóról a hálózaton keresztül.

Minden modul be kell csomagolni, egy meghatározott formátumban, egy ZIP-fájlt, amely tartalmazza a modul hasznos ModuleName_Version.zip nevű. Miután a kiszolgálóra, létre kell hozni egy ellenőrzőösszeg fájlt másolja a fájlt. Amikor az ügyfelek csatlakoznak a kiszolgálóhoz, ellenőrizze, hogy a tartalom a DSC-modul közzététele óta nem módosult az ellenőrzőösszeg szolgál.

```powershell
New-DscChecksum -ConfigurationPath .\ -OutPath .\
```

A tervezési feladat|
---|
Ha azt tervezi, milyen forgatókönyvekre kulcsával ellenőrzi egy teszt vagy a labor környezetben?|
Vannak-e, amit fedezésére erőforrásait tartalmazó nyilvánosan elérhető modulok vagy lesz szüksége ahhoz, hogy saját erőforrásokat?|
Nyilvános modulok beolvasása internetes hozzáférést kap a környezet?|
Ki legyen a felelős a DSC-modulok áttekintése?|
Ha azt tervezi, hogy éles környezetben mit fog használni mint egy helyi tárház tárolására a modulok DSC?|
A központi csapat elfogadja a alkalmazásfejlesztő csapatok dolgoznak a DSC-modulok? Mi lesz a folyamat?|
Csomagolás, a másolás és a egy éles használatra kész DSC modulok ellenőrzőösszeg létrehozása a kiszolgálóra, a forrás-adattárból fogja automatizálni?|
A csapat lesz az automatizálási platform, valamint kezeléséért?|

#### <a name="dsc-configurations"></a>DSC-konfigurációk

Egy lekéréses kiszolgálót az a célja, hogy központi DSC-konfigurációk ügyfél csomópontokra terjesztése mechanizmus biztosítására. A konfigurációk tárolása a kiszolgálón a MOF-dokumentumok formájában.
Egyes dokumentumok egyedi lesznek elnevezve **Guid**. Ha az ügyfelek csatlakozni egy lekérési kiszolgálóval van konfigurálva, akkor is kapnak a **Guid** kérelmeznie kell a konfiguráció. A rendszer konfigurációinak konfigurációk szerinti hivatkozó **Guid** garantálja a globális egyedi-e, és rugalmas, hogy egy konfiguráció alkalmazható granularitással csomópontonként, illetve a kiszolgálók számát, amely elvben kiterjedő szerepkör konfigurálása azonos konfigurációkat.

#### <a name="guids"></a>GUID-azonosítói

Konfiguráció tervezése **GUID** egy lekéréses kiszolgálót fejlesztésig fájlszerkesztés további figyelmet ér. Nem adott követelmény, hogy hogyan kezelje **GUID** és a folyamat valószínű oka az, hogy az egyes környezetekhez egyedi legyen. A folyamat között lehet egyszerű egészen az összetettekig: központilag tárolt CSV-fájlba, egy egyszerű SQL-táblára, a CMDB vagy egy másik eszköz vagy szoftver megoldás integrációt igénylő összetett megoldás. Kétféleképpen általános:

- **GUID-ok hozzárendelése kiszolgálónként** – mérhető, hogy minden kiszolgáló konfigurációs külön-külön szabályozott alkalmazunk. Ez pontosság körül frissítéseket biztosít, és jól néhány kiszolgálókkal környezetben is működik.
- **GUID-ok hozzárendelése egy kiszolgálói szerepkör** – minden kiszolgálón, amely ugyanazt a funkciót, például a webkiszolgálók, ugyanaz a GUID azonosító használatával a szükséges konfigurációs adatokra hivatkoznak.  Vegye figyelembe, hogy ha ugyanaz a GUID kiszolgálók számát, ezek mindegyike frissülnek egyszerre a konfiguráció módosításakor.

  A globálisan egyedi Azonosítót a bizalmas adatok tekintendők, mert sikerült adatbáziscsoportok próbál a jeggyel intelligencia kiszolgálók üzembe helyezve és konfigurálva a környezetben az illető ártó szándékkal rendelkező bármely személy. További információkért lásd: [biztonságosan lefoglalása a PowerShell Desired State Configuration lekéréses módban GUID](https://blogs.msdn.microsoft.com/powershell/2014/12/31/securely-allocating-guids-in-powershell-desired-state-configuration-pull-mode/).

A tervezési feladat|
---|
Ki legyen a felelős, amikor készen állnak a konfigurációk a másolási a lekéréses kiszolgálón mappát?|
Ha konfigurációk egy alkalmazás csapat munkafolyamatokba(n), mi a folyamat lesz kiosztják őket?|
Kihasználhatja a tárház konfigurációk tárolását azok alatt munkafolyamatokba(n), különböző csapatokkal?|
Automatizálhatja a folyamat konfigurációk másolása a kiszolgálóhoz és a egy ellenőrzőösszeg létrehozása, ha készen áll?|
Hogyan fogja leképez GUID szerverek és szerepkörök, és ez helyét?|
Mit fog használni egy folyamatot, az ügyfélgépek konfigurálása, és hogyan fogja azt integrálása a folyamat létrehozása és tárolása a konfigurációs GUID?|

## <a name="installation-guide"></a>Telepítési útmutató

*Ebben a dokumentumban megadott parancsfájlok használata a stabil példákat. Mindig tekintse át parancsfájl alaposan azokat éles környezetben a végrehajtása előtt.*

### <a name="prerequisites"></a>Előfeltételek

A következő parancs használatával ellenőrizze a PowerShell verzióját a kiszolgálón.

```powershell
$PSVersionTable.PSVersion
```

Ha lehetséges frissítse a legújabb Windows Management Framework.
Ezután töltse le a `xPsDesiredStateConfiguration` modul a következő paranccsal.

```powershell
Install-Module xPSDesiredStateConfiguration
```

A parancs a modul letöltése előtt a jóváhagyását kéri.

### <a name="installation-and-configuration-scripts"></a>Telepítés és konfigurálás parancsfájlok

A DSC lekéréses kiszolgálón telepítendő a legjobb módszer, hogy a DSC-konfigurációs parancsprogram használata. Ez a dokumentum bemutatja a parancsfájlok, beleértve a két alapszintű beállítás, amely csak a DSC-webszolgáltatás konfigurálására és a speciális beállításokat, amelyeket szeretne egy Windows Server teljes körű többek között DSC webszolgáltatás konfigurálása.

Megjegyzés:  Jelenleg a `xPSDesiredStateConfiguration` DSC modulnak szüksége van a kiszolgálóra, hogy EN-US területi beállítás.

### <a name="basic-configuration-for-windows-server-2012"></a>A Windows Server 2012 alapvető konfigurációs

```powershell
# This is a very basic Configuration to deploy a pull server instance in a lab environment on Windows Server 2012.

Configuration PullServer {
Import-DscResource -ModuleName xPSDesiredStateConfiguration

        # Load the Windows Server DSC Service feature
        WindowsFeature DSCServiceFeature
        {
          Ensure = 'Present'
          Name = 'DSC-Service'
        }

        # Use the DSC Resource to simplify deployment of the web service
        xDSCWebService PSDSCPullServer
        {
          Ensure = 'Present'
          EndpointName = 'PSDSCPullServer'
          Port = 8080
          PhysicalPath = "$env:SYSTEMDRIVE\inetpub\wwwroot\PSDSCPullServer"
          CertificateThumbPrint = 'AllowUnencryptedTraffic'
          ModulePath = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
          ConfigurationPath = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
          State = 'Started'
          DependsOn = '[WindowsFeature]DSCServiceFeature'
        }
}
PullServer -OutputPath 'C:\PullServerConfig\'
Start-DscConfiguration -Wait -Force -Verbose -Path 'C:\PullServerConfig\'
```

### <a name="advanced-configuration-for-windows-server-2012-r2"></a>A Windows Server 2012 R2 speciális konfiguráció

```powershell
# This is an advanced Configuration example for Pull Server production deployments on Windows Server 2012 R2.
# Many of the features demonstrated are optional and provided to demonstrate how to adapt the Configuration for multiple scenarios
# Select the needed resources based on the requirements for each environment.
# Optional scenarios include:
#      * Reduce footprint to Server Core
#      * Rename server and join domain
#      * Switch from SSL to TLS for HTTPS
#      * Automatically load certificate from Certificate Authority
#      * Locate Modules and Configuration data on remote SMB share
#      * Manage state of default websites in IIS

param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [System.String] $ServerName,
        [System.String] $DomainName,
        [System.String] $CARootName,
        [System.String] $CAServerFQDN,
        [System.String] $CertSubject,
        [System.String] $SMBShare,
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PsCredential] $Credential
    )

Configuration PullServer {
    Import-DscResource -ModuleName xPSDesiredStateConfiguration, xWebAdministration, xCertificate, xComputerManagement
    Node localhost
    {

        # Configure the server to automatically corret configuration drift including reboots if needed.
        LocalConfigurationManager
        {
            ConfigurationMode = 'ApplyAndAutoCorrect'
            RebootNodeifNeeded = $node.RebootNodeifNeeded
            CertificateId = $node.Thumbprint
        }

        # Remove all GUI interfaces so the server has minimum running footprint.
        WindowsFeature ServerCore
        {
            Ensure = 'Absent'
            Name = 'User-Interfaces-Infra'
        }

        # Set the server name and if needed, join a domain. If not joining a domain, remove the DomainName parameter.
        xComputer DomainJoin
        {
            Name = $Node.ServerName
            DomainName = $Node.DomainName
            Credential = $Node.Credential
        }

        # The next series of settings disable SSL and enable TLS, for environments where that is required by policy.
        Registry TLS1_2ServerEnabled
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server'
            ValueName = 'Enabled'
            ValueData = 1
            ValueType = 'Dword'
        }

        Registry TLS1_2ServerDisabledByDefault
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server'
            ValueName = 'DisabledByDefault'
            ValueData = 0
            ValueType = 'Dword'
        }

        Registry TLS1_2ClientEnabled
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client'
            ValueName = 'Enabled'
            ValueData = 1
            ValueType = 'Dword'
        }

        Registry TLS1_2ClientDisabledByDefault
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client'
            ValueName = 'DisabledByDefault'
            ValueData = 0
            ValueType = 'Dword'
        }

        Registry SSL2ServerDisabled
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server'
            ValueName = 'Enabled'
            ValueData = 0
            ValueType = 'Dword'
        }

        # Install the Windows Server DSC Service feature
        WindowsFeature DSCServiceFeature
        {
            Ensure = 'Present'
            Name = 'DSC-Service'
        }

        # If using a certificate from a local Active Directory Enterprise Root Certificate Authority, complete a request and install the certificate
        xCertReq SSLCert
        {
            CARootName = $Node.CARootName
            CAServerFQDN = $Node.CAServerFQDN
            Subject = $Node.CertSubject
            AutoRenew = $Node.AutoRenew
            Credential = $Node.Credential
        }

        # Use the DSC resource to simplify deployment of the web service.  You might also consider modifying the default port, possibly leveraging port 443 in environments where that is enforced as a standard.
        xDSCWebService PSDSCPullServer
        {
            Ensure = 'Present'
            EndpointName = 'PSDSCPullServer'
            Port = 8080
            PhysicalPath = "$env:SYSTEMDRIVE\inetpub\wwwroot\PSDSCPullServer"
            CertificateThumbPrint = 'CertificateSubject'
            CertificateSubject = $Node.CertSubject
            ModulePath = "$($Node.SMBShare)\DscService\Modules"
            ConfigurationPath = "$($Node.SMBShare)\DscService\Configuration"
            State = 'Started'
            DependsOn = '[WindowsFeature]DSCServiceFeature'
        }

        # Validate web config file contains current DB settings
        xWebConfigKeyValue CorrectDBProvider
        {
            ConfigSection = 'AppSettings'
            Key = 'dbprovider'
            Value = 'System.Data.OleDb'
            WebsitePath = 'IIS:\sites\PSDSCPullServer'
            DependsOn = '[xDSCWebService]PSDSCPullServer'
        }
        xWebConfigKeyValue CorrectDBConnectionStr
        {
            ConfigSection = 'AppSettings'
            Key = 'dbconnectionstr'
            Value = 'Provider=Microsoft.Jet.OLEDB.4.0;Data Source=C:\Program Files\WindowsPowerShell\DscService\Devices.mdb;'
            WebsitePath = 'IIS:\sites\PSDSCPullServer'
            DependsOn = '[xDSCWebService]PSDSCPullServer'
        }

        # Stop the default website
        xWebsite StopDefaultSite
        {
            Ensure = 'Present'
            Name = 'Default Web Site'
            State = 'Stopped'
            PhysicalPath = 'C:\inetpub\wwwroot'
            DependsOn = '[WindowsFeature]DSCServiceFeature'
        }
    }
}

$configData = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            ServerName = $ServerName
            DomainName = $DomainName
            CARootName = $CARootName
            CAServerFQDN = $CAServerFQDN
            CertSubject = $CertSubject
            AutoRenew = $true
            SMBShare = $SMBShare
            Credential = $Credential
            RebootNodeifNeeded = $true
            CertificateFile = 'c:\PullServerConfig\Cert.cer'
            Thumbprint = 'B9A39921918B466EB1ADF2509E00F5DECB2EFDA9'
            }
        )
    }

PullServer -ConfigurationData $configData -OutputPath 'C:\PullServerConfig\'
Set-DscLocalConfigurationManager -ComputerName localhost -Path 'C:\PullServerConfig\'
Start-DscConfiguration -Wait -Force -Verbose -Path 'C:\PullServerConfig\'

# .\Script.ps1 -ServerName web1 -domainname 'test.pha' -carootname 'test-dc01-ca' -caserverfqdn 'dc01.test.pha' -certsubject 'CN=service.test.pha' -smbshare '\\sofs1.test.pha\share'
```

### <a name="verify-pull-server-functionality"></a>Lekéréses kiszolgálói funkciók ellenőrzése

```powershell
# This function is meant to simplify a check against a DSC pull server. If you do not use the default service URL, you will need to adjust accordingly.
function Verify-DSCPullServer ($fqdn) {
    ([xml](Invoke-WebRequest "https://$($fqdn):8080/psdscpullserver.svc" | % Content)).service.workspace.collection.href
}

Verify-DSCPullServer 'INSERT SERVER FQDN'
```

```output
Expected Result:
Action
Module
StatusReport
Node
```

### <a name="configure-clients"></a>Ügyfelek konfigurálása

```powershell
Configuration PullClient {
    param(
    $ID,
    $Server
    )
        LocalConfigurationManager
                {
                    ConfigurationID = $ID;
                    RefreshMode = 'PULL';
                    DownloadManagerName = 'WebDownloadManager';
                    RebootNodeIfNeeded = $true;
                    RefreshFrequencyMins = 30;
                    ConfigurationModeFrequencyMins = 15;
                    ConfigurationMode = 'ApplyAndAutoCorrect';
                    DownloadManagerCustomData = @{ServerUrl = "http://"+$Server+":8080/PSDSCPullServer.svc"; AllowUnsecureConnection = $true}
                }
}

PullClient -ID 'INSERTGUID' -Server 'INSERTSERVER' -Output 'C:\DSCConfig\'
Set-DscLocalConfigurationManager -ComputerName 'Localhost' -Path 'C:\DSCConfig\' -Verbose
```

## <a name="additional-references-snippets-and-examples"></a>További hivatkozások kódrészletek és példák

Ez a példa bemutatja, hogyan manuálisan (WMF5 igényel) ügyfél kapcsolatot kezdeményez teszteléséhez.

```powershell
Update-DscConfiguration –Wait -Verbose
```

A [Add-DnsServerResourceRecordName](http://bit.ly/1G1H31L) parancsmag segítségével adjon hozzá egy CNAME-rekord típust a DNS-zónához.

A PowerShell-függvény, amely [ellenőrzőösszeg és DSC MOF közzététele az SMB-lekérési kiszolgálójának létrehozása](https://gallery.technet.microsoft.com/scriptcenter/PowerShell-Function-to-3bc4b7f0) automatikusan létrehozza a szükséges ellenőrzőösszeg, és ezután átmásolja az SMB-lekérési kiszolgálójának MOF-konfigurációt és ellenőrzőösszeg-fájlokat.

## <a name="appendix---understanding-odata-service-data-file-types"></a>A függelék – ismertetése ODATA szolgáltatás adatainak fájltípusok

Egy adatfájlt egy lekéréses kiszolgálót, amely tartalmazza az OData webszolgáltatást üzembe helyezése során az adatok létrehozásához tárolódik. A fájl típusa attól függ, az operációs rendszer, az alább ismertetett.

- **A Windows Server 2012** a fájl típusa mindig lesz .mdb
- **A Windows Server 2012 R2** a fájl típusa alapértelmezett .edb-.mdb Ha nincs megadva a konfigurációban

Az a [példa parancsfájl komplex](https://github.com/mgreenegit/Whitepapers/blob/Dev/PullServerCPIG.md#installation-and-configuration-scripts) egy lekéréses kiszolgálót telepíti, a is talál egy példát automatikusan kezelheti a web.config fájl beállításait, hogy bármilyen fájltípus által okozott hiba esélyét.
