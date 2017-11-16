---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Lekéréses kiszolgáló ajánlott eljárások"
ms.openlocfilehash: 66b97f4edb43926866b39731d720a2dc8c91eb2e
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="pull-server-best-practices"></a>Lekéréses kiszolgáló ajánlott eljárások

>Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

Összefoglalás: Ez a dokumentum célja, hogy folyamata, és segít a mérnökök számára készül a megoldás bővítési tartalmazza. Részletek kell ajánlott eljárások nyújtása a felhasználók által meghatározott, és a termék csapatától javaslatok jövőbeli számára is elérhető, és figyelembe veendő stabil majd érvényesíteni.

| |DOC adatai|
|:---|:---|
Szerző | Michael Greene  
Lektorok | Ben Gelens, Ravikanth Chaganti Aleksandar Nikolic  
Közzétett | 2015. április

## <a name="abstract"></a>Absztrakt

Jelen dokumentum célja, hogy bárki a Windows PowerShell célállapot-konfiguráció lekéréses kiszolgáló megvalósításának tervezési hivatalos útmutatást. A lekérési kiszolgálójával egy olyan egyszerű szolgáltatás, hajtson végre központi telepítéséhez csak perc. Bár ez a dokumentum műszaki útmutató útmutatást, amelyek a központi telepítés is használható lesz kínálnak, ez a dokumentum értéke az ajánlott eljárásokat, és milyen üzembe helyezése előtt gondolja hivatkozásként.
Olvasók kell rendelkeznie a DSC alapszintű ismeretét, és az összetevők leíró feltételeket, amelyek központi telepítésben lévő egy DSC. További információkért lásd: a [Windows PowerShell kívánt állapot beállítása – áttekintés](https://technet.microsoft.com/en-us/library/dn249912.aspx) témakör.
DSC elvárt azt fejleszteni a felhő ütemben történik az alapul szolgáló technológiát, beleértve a lekérési kiszolgálón is várt fejlődnek, és amelyek új lehetőségeket biztosítanak. Ez a dokumentum egy verzió táblázatot, amely korábbi kiadásokban mutató hivatkozásokat és előretekintő tervek bátorítva jövőbeli kinézetű megoldások mutató hivatkozásokat biztosít a függelékben tartalmaz.

A két fő szakasz ebben a dokumentumban:

 - Konfiguráció tervezése
 - A telepítési útmutató
 
### <a name="versions-of-the-windows-management-framework"></a>Windows Management Framework verziói 
A jelen dokumentumban szereplő információk alkalmazása a Windows Management Framework 5.0-ra készült. WMF 5.0 nincs szükség, telepítéséhez és működtetéséhez egy lekérési kiszolgálójával, amíg a 5.0-s verziója a fókusz ezen dokumentum.

### <a name="windows-powershell-desired-state-configuration"></a>A Windows PowerShell célállapot konfiguráló
A keresett konfiguráló (DSC) az olyan felügyeleti platform, amely lehetővé teszi a konfigurációs adatok telepítését és kezelését ismertetik a Common Information Model (CIM) egy iparági szintaxis a Managed Object Format (MOF) nevű használatával. Ezeknek a szabványoknak fejlesztésének tovább a különböző platformokon, beleértve a Linux és a hálózati hardver operációs rendszerek van nyílt forráskódú projektként, nyissa meg a Management Infrastructure (OMI). További információkért lásd: a [MOF specifikációk csatolása DMTF lap](http://dmtf.org/standards/cim), és [OMI dokumentumokat és a forrás](https://collaboration.opengroup.org/omi/documents.php).

A Windows PowerShell célállapot-konfiguráció, amely hozhat létre és kezelhet deklaratív konfigurációk biztosít a a nyelvi kiterjesztés-készlet.

### <a name="pull-server-role"></a>Lekéréses kiszolgálói szerepkör  
A lekérési kiszolgálójával hozzáférhető a célcsomópontokat konfigurációk tárolásához egy központosított szolgáltatást biztosít.
 
A lekéréses kiszolgálói szerepkör vagy a Web Server-példányt, vagy SMB-fájlmegosztásra is telepíthető. A webes képesség OData illesztőfelület tartalmazza, és visszaküldi megerősítése sikeres vagy sikertelen volt, a konfiguráció alkalmazása a célcsomópontokat képességeket választhatóan is. Ez a funkció olyan környezetben hasznos, ahol nagyszámú célcsomópontokat. Egy célcsomóponttal (más néven ügyfél) konfigurálását, hogy a lekéréses kiszolgálóra mutasson a legfrissebb konfigurációt követő adatok és a szükséges parancsfájlokat vannak letöltésére és alkalmazására. Ez akkor fordulhat elő, egy egyszeri központi telepítést, vagy egy újra előforduló is lehetővé teszi a lekérési kiszolgálójával lényeges módosítása a méretezés kezelésére szolgáló feladat. További információkért lásd: [Windows PowerShell kívánt állapot konfigurációs lekéréses kiszolgálók](https://technet.microsoft.com/en-us/library/dn249913.aspx) és [leküldéses és lekéréses konfigurációs módjai](https://technet.microsoft.com/en-us/library/dn249913.aspx).

## <a name="configuration-planning"></a>Konfiguráció tervezése

Az összes vállalati szoftver központi telepítése nincs információ előre gyűjtendő megtervezheti a megfelelő architektúra és elő kell készíteni a központi telepítés befejezéséhez szükséges lépéseket a. A következő szakaszokban előkészítése és a szervezeti kapcsolatok, valószínűleg létre fordulhat elő, előre kell vonatkozó információk.

### <a name="software-requirements"></a>Szoftverkövetelmények

A lekéréses kiszolgáló telepítéséhez a DSC szolgáltatás a Windows Server szükséges. Ez a funkció a Windows Server 2012-ben bevezetett, és folyamatban lévő kiadásokban Windows Management Framework (WMF) keresztül frissítve lett.

### <a name="software-downloads"></a>Szoftver letöltése

Telepíti a legújabb tartalom a Windows Update-ről, kívül ajánlott eljárás a DSC lekérési kiszolgálójával telepítése két letöltések: A legújabb Windows Management Framework, és a DSC-modulok lekéréses kiszolgáló kiépítés automatizálásához.

### <a name="wmf"></a>WMF

Windows Server 2012 R2 magában foglalja a DSC szolgáltatás nevű szolgáltatás. A DSC szolgáltatás lekéréses kiszolgáló funkciókat, beleértve a bináris fájlok, amelyek támogatják az OData-végpont biztosítja. WMF része a Windows Server, és egy, a Windows Server között gyors ütemben történik frissül. [WMF 5.0 új verzióit](http://aka.ms/wmf5latest) tartalmazhatják a DSC szolgáltatás számára. Ezért ajánlott letölteni a WMF legújabb kiadása, és tekintse át a kibocsátási megjegyzéseket határozza meg, ha a kiadás egy frissítést adunk ki a DSC szolgáltatás is. Emellett tekintse át a kibocsátási megjegyzéseket, amely jelzi, hogy a frissítés vagy forgatókönyv tervezési állapottal jelenik meg stabil vagy kísérleti szakasza. Szeretné engedélyezni az Agilis kiadási ciklus egyes szolgáltatások stabil deklarálható, ami azt jelenti, hogy a szolgáltatás készen áll a WMF felszabadul Preview közben is az éles környezetben használható.
Egyéb szolgáltatások hagyományosan frissített által WMF kiadások (lásd a további részletek a WMF kibocsátási megjegyzései):

 - A Windows PowerShell Windows PowerShell integrált parancsfájlkezelési
 - Környezet (ISE) a Windows PowerShell webszolgáltatások (felügyeleti OData
 - IIS-bővítmény) a Windows PowerShell célállapot konfiguráló (DSC)
 - Windows Rendszerfelügyeleti (webszolgáltatások WinRM) a Windows Management Instrumentation (WMI)

### <a name="dsc-resource"></a>A DSC-erőforrás

A lekéréses kiszolgálói telepítése által DSC konfigurációs parancsfájl használata a szolgáltatás kiépítését egyszerűsíthető. Ez a dokumentum tartalmaz, amelyek segítségével központi telepítése az üzemi kiszolgáló készen áll a csomópont konfigurációs parancsfájlokat. A konfigurációs parancsfájlok használatához egy DSC modulra lenne szükség, amely nem a Windows Serverben megtalálható. A szükséges modulnév **xPSDesiredStateConfiguration**, mely tartalmazza a DSC-erőforrás **xDscWebService**. A xPSDesiredStateConfiguration modul letölthető [Itt](https://gallery.technet.microsoft.com/xPSDesiredStateConfiguratio-417dc71d).

Használja a **Install-modul** parancsmag a **PowerShellGet** modul.

```powershell
Install-Module xPSDesiredStateConfiguration
```

A **PowerShellGet** modul modul tölti le: 

`C:\Program Files\Windows PowerShell\Modules`

A tervezési feladat|
---|
Rendelkezik hozzáféréssel a telepítési fájlok a Windows Server 2012 R2 rendszerben?|
A telepítési környezet kell WMF és a modul letöltése az online katalógusból Internet-hozzáférés?|
Hogyan telepíti az operációs rendszer telepítése után a legújabb biztonsági frissítéseket?|
A frissítések letöltése érdekében Internet-hozzáféréssel kell a környezetben, vagy fog rendelkezni a helyi Windows Server Update Services (WSUS) kiszolgáló?|
Rendelkezik hozzáféréssel, amely már tartalmazza az offline injektálási a frissítéseket a Windows Server telepítési fájlok?|

### <a name="hardware-requirements"></a>Hardverkövetelmények

Lekérési telepítések támogatottak a virtuális és fizikai kiszolgálón. A méretezési követelmények lekérési kiszolgálójával összhangba kerüljenek a Windows Server 2012 R2 követelményei.

CPU: 1,4 GHz-es 64 bites processzor  
Memória: 512 MB  
Szabad lemezterület: 32 GB  
Hálózati: Gigabit Ethernet-Adapter  

A tervezési feladat|
---|
Telepíti a fizikai hardverek vagy olyan virtualizációs platformon?|
Mi az a folyamatot követve kérjen a a célkörnyezet új kiszolgálót?|
Mi az a kiszolgáló elérhető legyen, az átlagos válaszidő?|
Milyen mérete server kérés?|

### <a name="accounts"></a>Fiókok

Nincsenek service fiókot egy lekéréses server-példány telepítése. Vannak azonban forgatókönyvek, ahol a webhely egy helyi felhasználói fiók kontextusában futtathat. Például ha egy szükséges hozzáférését a storage-megosztásban webhelytartalmat és a Windows Server vagy az eszköz a storage-megosztás üzemeltetési nincsenek tartományhoz.

### <a name="dns-records"></a>DNS-rekordok

Szüksége lesz a kiszolgáló nevét használja, ha az ügyfelek egy lekéréses kiszolgálói környezetben használható. Tesztelési környezetben jellemzően akkor alkalmazzák a kiszolgáló állomásneve, vagy a kiszolgáló IP-címe használható, ha a DNS-név feloldása nem érhető el. Éles környezetben, amely az éles környezet jelöl laborkörnyezetben, az ajánlott eljárás akkor DNS CNAME rekordot kell létrehozni.

DNS CNAME rekord lehet hivatkozni az állomás (A) rekordot alias létrehozását teszi lehetővé. A további rekordhoz célja rugalmasabb kell változás szükség lehet a jövőben. Egy olyan CNAME REKORDOT segít elkülöníteni az ügyfél-konfigurációt, hogy a kiszolgáló környezet, például egy lekéréses kiszolgáló cseréje vagy lekéréses további kiszolgálók hozzáadásával módosításai nem kell az ügyfél-konfigurációhoz megfelelő megváltoztatása.

A DNS-rekord nevét kiválasztásakor tartsa szem előtt a megoldás architektúrája. Ha használatával terheléselosztás, a tanúsítvány használatával teszi biztonságossá a HTTPS-KAPCSOLATON keresztül a forgalom kell neve megegyezik a DNS-rekord. 

Forgatókönyv |Ajánlott eljárás
:---|:---
Tesztkörnyezet |Ha lehetséges Reprodukálja a tervezett éles környezetben. A kiszolgáló állomásneve egyszerű konfigurációk alkalmas. Ha a DNS nem érhető el, IP-címet az állomásnév helyett használható.|
Egyetlen csomópont telepítése |A kiszolgáló állomásneve mutató DNS CNAME rekordot kell létrehozni.|

További információkért lásd: [DNS ciklikus multiplexelés konfigurálása a Windows Server](https://technet.microsoft.com/en-us/library/cc787484(v=ws.10).aspx).

A tervezési feladat|
---|
Tudja Megadja annak a személynek a DNS-rekordok létrehozott és módosított?|
Újdonságok a DNS-rekord a kérelmek átlagos esetenként?|
Meg kell igényelnie a kiszolgálók statikus állomásnév (A) rekordot?|
Mit fog kér, egy olyan CNAME REKORDOT?|
Ha szükséges, terheléselosztás megoldás fog használhatja a? (című terheléselosztás részletekért lásd:)|

### <a name="public-key-infrastructure"></a>Nyilvános kulcsokra épülő infrastruktúra

A legtöbb szervezet ma igényelnek, hálózati forgalom, különösen az, hogy a kiszolgálók konfigurálva vannak, például bizalmas adatokat tartalmazó forgalom ellenőrizni kell, illetve átvitel során titkosítva. Bár a lekéréses kiszolgáló, amely elősegíti a HTTP-n keresztül telepítéséhez az ügyfélkérelmek törölje a szöveget, a HTTPS protokoll használatával biztonságos forgalom ajánlott. A szolgáltatás beállítható úgy, hogy használja a HTTPS-kapcsolaton paraméterek a DSC-erőforrás **xPSDesiredStateConfiguration**.

A tanúsítványokkal szemben támasztott követelmények biztonságossá a HTTPS-forgalmat a lekérési kiszolgálójával nincsenek különböző, mint bármely más HTTPS webhely biztonságossá tételéhez. A **webkiszolgáló** egy Windows Server tanúsítványszolgáltatási sablon megfelel a szükséges képességek.

A tervezési feladat|
---|
Ha tanúsítványkérelmek nem automatizált, ki kell a kérelmekre, forduljon a tanúsítványt?|
Mi az a kérelem esetenként átlagosan?|
Hogyan a Tanúsítványfájl használatával lesz áthelyezve meg?|
Hogyan a tanúsítvány titkos kulcsa használatával lesz áthelyezve meg?|
Milyen hosszú legyen az alapértelmezett lejárati idő?|
Rendelkezik elszámolása meg egy DNS-nevet az lekéréses kiszolgáló környezetben, használhatja a tanúsítvány neve?|

### <a name="choosing-an-architecture"></a>Az architektúrát kiválasztása

A lekérési kiszolgálójával vagy webszolgáltatás IIS vagy SMB-fájlmegosztásra is telepíthető. A legtöbb esetben a webes szolgáltatás lehetőség nagyobb rugalmasságot biztosítja. Nincs ritka, hogy HTTPS-forgalom haladnak át a hálózati határok, mivel SMB-forgalom gyakran szűrt vagy letiltott hálózatok között. A webszolgáltatás is biztosít, a megfelelési kiszolgáló vagy a webes Reporting Manager (mindkét figyelembe venni a jelen dokumentum egy jövőbeli verziójában témakörök), amely egy olyan mechanizmus biztosítása az ügyfelek egy kiszolgálóra a központi látható az állapot jelentése érdekében lehetősége. SMB környezetekben, ahol házirend szerint, hogy a webkiszolgáló nem állítható be, és más környezeti követelmények, amelyek a webkiszolgálói szerepkör nemkívánatos lehetőséget biztosít. Mindkét esetben ne felejtse el az aláíráshoz és a forgalom titkosításának követelmények kiértékeléséhez. IPSEC-házirendek, HTTPS és SMB-aláírást érdemes fontolóra veheti, hogy minden opció.

#### <a name="load-balancing"></a>Terheléselosztás  
A webszolgáltatáshoz való interakció ügyfelek egyetlen válaszként visszaküldött adatokat kérhet. Szekvenciális kérelmek nem szükségesek, így nincs szükség a terheléselosztási platform munkamenetek karbantartása bármikor egy kiszolgálón az idő biztosításához.

A tervezési feladat|
---|
Melyik megoldás a kiszolgálók közötti terheléselosztás forgalom fog használni?|
Ha használja a hardveres terheléselosztót, aki a kérést vegyen fel új konfigurációt az eszközön érvénybe?|
Mi az, hogy egy új terheléselosztási konfigurálja a kérelmek átlagos esetenként elosztott terhelésű webszolgáltatás?|
Milyen információkat kell a kérelem?|
Meg kell kérnie olyan további IP-címet, vagy a terheléselosztás felelős csapat kezelnek, amelyek?|
Rendelkezik a szükséges DNS-rekordokat, és ez szükség lesz a terheléselosztási megoldás konfigurálása felelős csapat?|
A betöltési terheléselosztási megoldást igényel, hogy a nyilvános kulcsokra épülő infrastruktúra elvégezhető-e az eszköz vagy is azt a terhelést HTTPS forgalmat, mindaddig, amíg nincsenek munkamenet követelmények?|

### <a name="staging-configurations-and-modules-on-the-pull-server"></a>Átmeneti konfigurációk és a modulok a lekérési kiszolgálón

A konfiguráció tervezése részeként szüksége lesz gondolja, hogy melyik DSC kapcsolatos modulok és konfigurációk tárolható a lekérési kiszolgálójával. Céljából konfigurációs tervezési fontos, hogy alapszinten megértse, hogyan lehet előkészíteni és telepítse központilag a tartalmakat egy lekérési kiszolgálójával. 

A jövőben ez a szakasz kibontva lesz, és az üzemeltetési útmutatóban DSC lekéréses kiszolgáló tartalmazza.  Az útmutatóban modulok és konfigurációk kezelése az Automation szolgáltatásban, időbeli napi folyamatát ismertetik. 

#### <a name="dsc-modules"></a>A DSC-modulok  
Egy konfigurációs kérő ügyfelek kell a szükséges DSC-modulokat. A lekéréses kiszolgáló egy funkciójának automatizálhatja a DSC-modulokat az ügyfelek számára az igény szerinti terjesztési. Ha telepít egy lekérési kiszolgálójával először, lehet, hogy egy laboratóriumi vagy a koncepció igazolása, valószínűleg fog függ, például a PowerShell-galériában nyilvános adattárak vagy a DSC-modulok PowerShell.org GitHub-adattárak rendelkezésre álló DSC-modulok .

Nagyon fontos megjegyezni, hogy még a megbízható online források, például a PowerShell-galériában, bármely modul, egy nyilvános tárházból letöltött felül kell vizsgálni valaki PowerShell élmény és a környezetben, ahol a modulok fog ismerete éles környezetben használt előtt használt. Ez a feladat végrehajtása közben, akkor egy időben semmilyen további hasznos a modul, például a dokumentáció és például parancsfájlok eltávolítható kereséséhez. Ez csökkenti a hálózati sávszélesség az első kérelem ügyfelenként, amikor modulok letölti az ügyfél-kiszolgálóról a hálózaton keresztül.

Minden modul be kell csomagolni, egy meghatározott formátumban, nevű ModuleName_Version.zip, a modul forgalma tartalmazó ZIP-fájl. Miután a rendszer átmásolja a fájlt a kiszolgálóra egy ellenőrzőösszeg-fájl jön létre. Ha az ügyfelek csatlakoznak a kiszolgálóhoz, győződjön meg arról közzététele óta a DSC-modul tartalma nem módosult. az ellenőrzőösszeg szolgál.

```powershell
New-DscCheckSum -ConfigurationPath .\ -OutPath .\
```

A tervezési feladat|
---|
Ha azt tervezi, a vizsgálat vagy a laboratóriumi környezet változatok kulcsával ellenőrzi?|
Vannak-e nyilvánosan elérhető, amelyek minden szükséges erőforrásokat tartalmazó modulok, vagy meg kell ahhoz, hogy saját erőforrásokat?|
A környezet lesz nyilvános modulok beolvasása Internet-hozzáférést?|
Ki kell konfigurálnia a DSC-modulok áttekintése?|
Ha azt tervezi, éles környezetben mi fog használni, a helyi tárház DSC modulok tárolása?|
Egy központi munkacsoport elfogadja a DSC-modulok az alkalmazásokat fejlesztő csapatoknak együtt? Mi lesz a folyamatot?|
Csomagolására, másolása és éles használatra kész DSC modulok ellenőrzőösszeg létrehozása a kiszolgálón, a forrás tárházból fog automatizálni?|
A csapat felelős kezelése, valamint az automatizálási platform?|

#### <a name="dsc-configurations"></a>A DSC-konfigurációk

A lekérési kiszolgálójával célja ügyfél csomópontokhoz DSC-konfigurációk kiosztása során egy olyan központi mechanizmus biztosítása. A konfigurációk MOF-dokumentumokként tárolása a kiszolgálón. Egyes dokumentumok egyedi GUID azonosítója lesznek elnevezve. Ha az ügyfelek csatlakozhatnak a lekérési kiszolgálójával vannak beállítva, is számukra a globálisan egyedi Azonosítót a konfiguráció kérelmeznie kell. A rendszer a konfigurációk GUID alapján hivatkozik biztosítja, hogy a globális egyediségi és rugalmas úgy, hogy egy konfiguráció alkalmazható lépésköz csomópontonként, vagy egy szerepkör-konfigurációja is sok kiszolgálók, amelyek azonos beállításokkal kell rendelkeznie.

#### <a name="guids"></a>GUID azonosítók

Konfigurációs GUID tervezése ér további figyelmet egy lekéréses server központi végezni. Nincs olyan GUID kezelését az adott követelmény, és a folyamat valószínű környezetben egyedinek kell lennie. A folyamat egyszerű és közötti összetett: központilag tárolt CSV-fájl, egyszerű SQL táblázat, a CMDB vagy egy másik eszközt vagy a szoftver megoldással való integráció igénylő összetett megoldás. Kétféleképpen általános:

 - **GUID azonosítók hozzárendelése kiszolgálónként** – biztosítása, hogy minden kiszolgáló konfigurációs egyénileg szabályozott biztosítékot nyújt. Ez biztosít, a pontosság frissítések körül, és néhány kiszolgálókkal környezetekben is használhatók.
 - **GUID azonosítók hozzárendelése egy kiszolgálói szerepkör** – minden kiszolgálón, amely ugyanazt a funkciót, például a webkiszolgálók, ugyanaz a GUID segítségével a szükséges konfigurációs adatokra hivatkoztak.  Vegye figyelembe, hogy sok kiszolgálók megosztják a ugyanaz a GUID azonosítója, ha az összes kellene frissítésekor egyidejűleg a konfiguráció módosításait.

A GUID-azonosító, amelyet érdemes figyelembe venni bizalmas adatokat, mert valaki rosszindulatú ahhoz, hogy a kiszolgálók telepítve és konfigurálva a környezetben az eszközintelligencia sikerült javítható. További információkért lásd: [biztonságosan a PowerShell kívánt állapot konfigurációs módban lekéréses GUID azonosítók lefoglalásával](http://blogs.msdn.com/b/powershell/archive/2014/12/31/securely-allocating-guids-in-powershell-desired-state-configuration-pull-mode.aspx).

A tervezési feladat|
---|
Ki kell konfigurálnia a konfigurációk másolása a lekérési kiszolgálón mappába, amikor azok készen állnak?|
Ha egy alkalmazás csapat konfigurációk hoztak létre, mely a folyamat kell kiosztják azokat a?|
Kihasználhatja a tárház konfigurációk tárolja az azok alatt hoztak létre, csapatok?|
Automatizálható a folyamat-konfigurációk másolása a kiszolgálóra, és ellenőrzőösszeg létrehozása, amikor azok készen állnak?|
Hogyan fogja leképez GUID kiszolgálók vagy szerepkörök, és ez tárolására szolgáló?|
Mi használatával folyamatként ügyfél gépet állíthat be, és hogyan fogja azt integrálása a folyamat létrehozása és tárolása konfigurációs GUID?|

## <a name="installation-guide"></a>A telepítési útmutató

*Ebben a dokumentumban megadott parancsfájlok példák stabil. Mindig parancsfájlok célszerű gondosan felülvizsgálni őket éles környezetben végrehajtása előtt.*

### <a name="prerequisites"></a>Előfeltételek

Győződjön meg arról, hogy a PowerShell verzióját a kiszolgálón a következő paranccsal.

```powershell
$PSVersionTable.PSVersion
```

Ha lehetséges frissítsen a legújabb Windows Management Framework.
Ezt követően töltse le a `xPsDesiredStateConfiguration` modul a következő parancsot.


```powershell
Install-Module xPSDesiredStateConfiguration
```

A parancs a modul letöltése előtt jóváhagyásra fogja kérni.

### <a name="installation-and-configuration-scripts"></a>Telepítési és konfigurációs parancsfájlokat
-

A legjobb módszere a DSC lekérési kiszolgálójával, hogy a DSC-konfigurációs parancsprogram használja. Ez a dokumentum bemutatja a parancsfájlok mindkét alapszintű beállításokat, amelyek csak a DSC-webszolgáltatás kell konfigurálni, és speciális kell konfigurálni a Windows Server-végpontok közötti többek között a következőket DSC webszolgáltatás beállításokat is beleértve.

Megjegyzés: Jelenleg a `xPSDesiredStateConfiguation` DSC module használatához a kiszolgálónak EN-US területi beállítás.

### <a name="basic-configuration-for-windows-server-2012"></a>A Windows Server 2012 alapvető konfiguráció
-------------------------------------------
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

### <a name="advanced-configuration-for-windows-server-2012-r2"></a>A Windows Server 2012 R2 rendszerben speciális konfiguráció

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
    ([xml](invoke-webrequest "https://$($fqdn):8080/psdscpullserver.svc" | % Content)).service.workspace.collection.href
}
Verify-DSCPullServer 'INSERT SERVER FQDN' 

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


## <a name="additional-references-snippets-and-examples"></a>További hivatkozások kódtöredékek és példák

Ez a példa bemutatja, hogyan manuálisan (WMF5 igényel) ügyfél kapcsolatot kezdeményez teszteléshez. 

```powershell
Update-DSCConfiguration –Wait -Verbose
```

A [Add-DnsServerResourceRecordName](http://bit.ly/1G1H31L) parancsmag segítségével egy típus CNAME rekord hozzáadása a DNS-zónából. 

A PowerShell függvényt [hozzon létre egy ellenőrzőösszeg és DSC MOF közzététele a SMB lekérési kiszolgálójával](http://bit.ly/1E46BhI) , és automatikusan létrehozza a szükséges ellenőrzőösszeg, majd másolja az SMB-lekérési kiszolgálójával MOF-konfigurációt és ellenőrzőösszeg-fájlok.

## <a name="appendix---understanding-odata-service-data-file-types"></a>Függelék – ismertetése ODATA szolgáltatás adatainak fájltípusok

Egy adatfájlt létrehozása, amely tartalmazza az OData webszolgáltatást lekéréses kiszolgáló üzembe helyezése során információkat tárolja. A fájl típusát attól függ, az operációs rendszer az alább ismertetett.

 - **Windows Server 2012-ben**  
A fájl típusa mindig lesz .mdb
 - **Windows Server 2012 R2 rendszerben**  
A fájl típusa alapértelmezett .edb egy .mdb Ha nincs megadva a konfigurációban

Az a [példa parancsfájl speciális](https://github.com/mgreenegit/Whitepapers/blob/Dev/PullServerCPIG.md#installation-and-configuration-scripts) egy lekéréses kiszolgáló telepítésekor is talál arról, hogyan automatikusan vezérlőket a web.config fájl bármely fájltípus által okozott hiba esélyét megelőzése érdekében.

