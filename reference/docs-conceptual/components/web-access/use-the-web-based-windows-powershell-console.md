---
ms.date: 08/23/2017
keywords: PowerShell, a parancsmag
title: a webes alapú windows powershell-konzol használata
ms.openlocfilehash: 2bb9c6ef486ef32012a15f9890997cf2fa6a3a0b
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404448"
---
# <a name="use-the-web-based-windows-powershell-console"></a>A webalapú Windows PowerShell konzol használata

Frissítve: 2013. június 24-én

Érvényes: A Windows Server 2012 R2, Windows Server 2012-ben

Windows PowerShell-elérés lehetővé teszi a felhasználóknak, jelentkezzen be a biztonságos webhelyek; annak érdekében, hogy a Windows PowerShell-munkamenetek, a parancsmagok és parancsfájlok segítségével egy távoli számítógép kezeléséhez.

Mivel a Windows PowerShell-konzol webböngészőben fut, akkor is megnyithatók számos különféle ügyféleszközről; egy webböngészővel rendelkező szinte minden eszköz működik.

A webes Windows PowerShell-konzol egy távoli számítógépen, amely a bejelentkezési folyamat részeként a felhasználó által megadott célja.

Ez a témakör ismerteti, hogyan jelentkezzen be, és a Windows PowerShell-elérés webalapú konzol használatának megkezdéséhez.

Ez a témakör ismerteti a Windows PowerShell-lel vagy a parancsmagok vagy parancsfájlok futtatásának.
Windows PowerShell és programozási erőforrások használatával kapcsolatos információkért lásd: a [lásd még](#see-also) szakaszban Ez a témakör végén található.

## <a name="supported-browsers-and-client-devices"></a>Támogatott böngészők és ügyféleszközök

Windows PowerShell-elérés a következő webböngészőket támogatja.
Bár a mobilböngészők hivatalosan nem támogatottak, számos lehet képes a webalapú Windows PowerShell-konzol futtatásához.
Egyéb, cookie-kat elfogadó, JavaScriptet és HTTPS-webhelyeket futtató böngészők valószínűleg képesek a konzol használatára, de hivatalosan még nem lettek tesztelve.

### <a name="supported-desktop-computer-browsers"></a>Támogatott asztali számítógépes böngészők

- Windows Internet Explorer alkalmazás Microsoft Windows 8.0, 9.0, 10.0 és 11.0
- Mozilla Firefox 10.0.2
- Google Chrome-17.0.963.56m Windows esetében
- Apple Safari® 5.1.2 Windows
- Apple Safari® 5.1.2 Mac OS

### <a name="minimally-tested-mobile-devices-or-browsers"></a>Minimális tesztelésen átesett mobileszközök és böngészők

- Windows Phone 7 és 7.5
- Google Android WebKit 3.1 böngésző Android 2.2.1-en (Kernel 2.6)
- Apple Safari 5.0.1-es iPhone operációs rendszerhez
- Apple Safari 5.0.1-es iPad 2 operációs rendszerhez

### <a name="browser-requirements"></a>Böngészőkre vonatkozó követelmények

A Windows PowerShell-elérés webalapú konzol használatához böngészők a következőket kell tennie.

- Cookie-k a Windows PowerShell-elérés átjáró webhelyéről.
- HTTPS-lapok megnyitása és olvasása.
- JavaScriptet használó webhelyek megnyitása és futtatása.

## <a name="signing-in-to-windows-powershell-web-access"></a>Bejelentkezés a webes Windows PowerShell-elérésbe

A Windows PowerShell-elérés rendszergazdájától kaphatja meg azt a szervezet Windows PowerShell-elérés átjáró webhelyének címe URL-címet.
Alapértelmezés szerint ez a cím a *https://\<kiszolgáló_neve\>/pswa*.

Amikor bejelentkezik a Windows PowerShell-elérés, lehet, hogy rendelkezik-e a neve vagy a felügyelni kívánt távoli számítógép IP-címét.
Jogosult felhasználónak kell lennie a távoli számítógépen, amelyet úgy kell konfigurálni, hogy engedélyezze a távoli felügyeletet.
A számítógép a távoli felügyelet engedélyezésére konfigurálásával kapcsolatos további információkért lásd: [a Windows PowerShell használata a távoli parancsok engedélyezése és](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enable-psremoting).

A számítógép a távoli felügyelet engedélyezésére konfigurálásának legegyszerűbb módja az, hogy futtassa a **Enable-PSRemoting - force** parancsmagot a számítógépen egy megnyitott Windows PowerShell-munkamenetet emelt szintű felhasználói jogosultságokkal (**Futtatás rendszergazdaként**).

### <a name="to-sign-in-to-windows-powershell-web-access"></a>Bejelentkezés a webes Windows PowerShell-elérésbe

1. Nyissa meg a Windows PowerShell-elérés webhely egy böngészőablakban vagy lapon.

1. A bejelentkezési lapon Windows PowerShell-elérés adja meg a hálózati felhasználónevet, jelszót és a neve, amely a kezelni kívánt számítógép (és a, melyek egy jogosult felhasználó). Ha a Windows PowerShell-elérés rendszergazdájának utasítása szerint egy egyéni webhely vagy a proxykiszolgáló mutató URI-t használhatja a számítógép neve helyett, jelölje be **kapcsolati URI** a a **kapcsolattípus** mezőben, majd Adja meg az URI-t.

    > ![Megjegyzés:](images/Note.jpeg) **Megjegyzés**:
    >
    > - Ha a célszámítógép egy munkacsoportban, használja a következő szintaxist a felhasználónév megadásához és a számítógépre történő bejelentkezéshez: `<workgroup_name>\<user_name>`
    > - Ha a célként megadott számítógéphez az átjárókiszolgáló, megadhatja `localhost` a számítógép neve mezőben
    > - Ha a célszámítógép az átjárókiszolgáló, és az átjárókiszolgáló egy munkacsoporthoz tartozik van, akkor kell használnia `<workgroup name>\<user_name>` mezőjénél a felhasználó nevében. Használhat `localhost` a számítógép neve mezőben.

1. A **választható kapcsolati beállítások** szakasz a felügyelni kívánt távoli számítógép engedélyezési követelményeihez kapcsolódik. Választható kapcsolati beállításokkal egyenértékű paraméterekre vonatkozó további információkért lásd: a [Enter-PSSession](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enter-pssession) parancsmag súgóját.

    Általában a Windows PowerShell-elérés átjárón keresztül használt hitelesítő adatok megegyeznek a felügyelni kívánt távoli számítógép által elfogadottakkal. Azonban ha eltérő hitelesítő adatok használata a távoli számítógép kezeléséhez, amely a 2. lépésben megadott, bontsa ki a **választható kapcsolati beállítások** szakaszt, és adja meg a másodlagos hitelesítő adatokat. Egyéb esetben folytassa a 6. lépéssel.

1. Ha a Windows PowerShell-elérés rendszergazda hozott létre egy egyéni munkamenet-konfiguráció a Windows PowerShell-elérés felhasználók számára, írja be a munkamenet-konfiguráció nevét a nevét a **konfiguráció neve** mező. Munkamenet-konfigurációkkal kapcsolatos további információkért lásd: [about_Session_Configurations](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_session_configurations).

1. Tartsa a **hitelesítési típus** beállítása **alapértelmezett** , ha, hogy ne így tegyen a Windows PowerShell-elérés rendszergazdája által kapott utasítást.

1. Kattintson a **jelentkezzen be a**.

## <a name="signing-out-and-timing-out"></a>Kijelentkezés és időtúllépés

Az alábbi kijelentkezik, a webes Windows PowerShell-munkamenetben.

- Kattintson a **Kijelentkezés** a konzol jobb alsó sarkában található. (Csak Windows Server 2012)

- Kattintson a **mentése** vagy **kilépési** a (csak Windows Server 2012 R2) konzol jobb alsó sarkában található. Kattintson a **mentése** ezzel menti és bezárja a Windows PowerShell-elérés munkamenet; a munkamenethez később újra. Amikor bejelentkezik a Windows PowerShell-elérés újra, a Windows PowerShell-elérés a mentett munkamenetek listáját jeleníti meg akkor válassza ki, és az egy mentett munkamenetet csatlakozni, vagy új munkamenet indításához. Az egyes felhasználók számára engedélyezett mentett és aktív munkamenetek maximális számát az átjáró rendszergazdája határozza meg.

    Kattintson a **kilépési** kijelentkezik, a Windows PowerShell-elérés munkamenet, mentés nélkül.

- Megpróbálhat bejelentkezni egy másik távoli számítógép kezeléséhez ugyanazon a böngészői munkameneten belül, vagy a böngészői munkamenet egy új lapjáról. (Ez nem érvényes, ha az átjáró-kiszolgálót futtató Windows Server 2012 R2; Windows a Windows Server 2012 R2 rendszeren futó PowerShell-elérés engedélyezése több felhasználói munkamenet új lapjain az ugyanazon böngésző-munkamenet.) Ugyanazon a számítógépen egynél több aktív munkamenet használatával kapcsolatos további információkért lásd: csatlakozás több célszámítógéphez egyszerre a a [a webalapú konzol korlátozásai](#limitations-of-the-web-based-console) című szakaszát.

- 20 percig ne végezzen semmilyen tevékenységet a munkameneten belül. Az átjáró rendszergazdája testreszabhatja az inaktivitás időkorlátját További információkért lásd: [munkamenet-kezelés](authorization-rules-and-security-features-of-windows-powershell-web-access.md#session-management).

    - Ha hálózati hiba vagy egyéb nem tervezett leállás vagy hiba miatt kapcsolata egy munkamenettel a webalapú konzol a, és nem azért, mert a munkamenet bezárása saját maga is a Windows PowerShell-elérés továbbra is fut, csatlakoztatja a cél számítógép, amíg az ügyfél oldalán le nem telik időkorlát. Alapértelmezés szerint ez az időkorlát 20 perc, amelyet az átjáró rendszergazdája konfigurál. A munkamenet leválasztása vagy az alapértelmezett 20 perc lejárata után, vagy az átjáró rendszergazdája által megadott időtartam lejárata után (amelyik rövidebb) történik meg.

        Ha az átjáró-kiszolgálót futtat Windows Server 2012 R2, Windows PowerShell-elérés lehetővé teszi a felhasználóknak a mentett munkamenetekhez, egy későbbi időpontban újra csatlakozni, de nem látható vagy mentett munkamenetekhez, amíg az átjáró által meghatározott időkorlát időtartama után a rendszergazda lejárt.

- Zárja be a böngészőablakot vagy -lapot.

- Kapcsolja ki azt az ügyféleszközt, amelyen a böngésző fut, vagy válassza le a hálózatról.

- Fut a **kilépési** parancsot a webkonzolon. Ez a parancs nem működik, ha a munkamenet-konfiguráció, amelyhez csatlakozik, támogatására van konfigurálva [NoLanguage](https://msdn.microsoft.com/library/windows/desktop/system.management.automation.pslanguagemode.aspx) módban, vagy korlátozott futási térben van.

Ha azt szeretné, újra be kell jelentkezni, nyissa meg újra a Windows PowerShell-elérés weblap, és a lépéseket követve jelentkezzen be [bejelentkezés a Windows PowerShell-elérés](#signing-in-to-windows-powershell-web-access) ebben a témakörben.

## <a name="differences-in-the-web-based-windows-powershell-console"></a>A webalapú Windows PowerShell konzolok közötti különbségek

Miután bejelentkezett a Windows PowerShell-elérés, a webes Windows PowerShell-konzolt a böngészőablakban vagy lapon nyílik meg. Mivel a konzol a bejelentkezési folyamat során megadott távoli számítógép csatlakoztatva van, csak ezeket a Windows PowerShell-parancsmagok vagy parancsfájlok, amelyek elérhetők a távoli számítógépen is használható a konzolon. Ez a szakasz ismerteti a Windows PowerShell-elérés konzolok és a telepített és a Windows PowerShell-elérés konzolok közötti különbségek más korlátozásai **PowerShell.exe** konzolon.

### <a name="functional-disparity-with-powershellexe"></a>Funkcióbeli eltérések a PowerShell.exe konzolhoz képest

Windows PowerShell gazdagép funkciók legnagyobb részét a webes Windows PowerShell-elérés konzolon érhető el, de néhány szolgáltatás, amely nem érhetők el.

- Megjeleníti a beágyazott folyamatban van.

  Windows PowerShell-elérés jeleníti meg a parancsmagok egy folyamatban van grafikus felhasználói Felülettel, hogy a jelentés folyamatban van, de csak a legfelső szintű állapotinformációk jelennek meg.

- Bemeneti szín módosítása.

  A bemeneti színt (az előtér és a háttér színét) nem lehet módosítani. A kimenet, a figyelmeztetés, a részletes és a hibaüzenetek stílusát egy parancsfájl futtatásával lehet módosítani.

- PSHostRawUserInterface.

  Windows PowerShell-elérés Windows PowerShell távoli felügyeletének van megvalósítva, és a egy távoli futási teret használ. Windows PowerShell-elérés nem implementálja az ezen a felületen egyes metódusok Ha például olyan parancsokat, amelyek a Windows konzol ír. Parancsok, mint **PowerTab** nem működnek a Windows PowerShell-elérés.

- Funkcióbillentyűk.

  Windows PowerShell-elérés nepodporuje egyes funkcióbillentyűket sok esetben, mivel a parancsok a böngésző számára van fenntartva.

### <a name="unsupported-shortcut-keys"></a>Nem támogatott a gyorsbillentyűk

Billentyűt | Művelet
-- | --
Ctrl+C | A Windows PowerShell-elérés **Ctrl + C** másolhatják a tartalmat a böngészőben használják. A konzolon egy **Mégse** gomb, valamint a felhasználók is használhatja **Ctrl + Q** parancsok visszavonásához.
Alt+szóköz, e, l | A képernyőpuffer görgetése
Alt+szóköz, e, f | Szöveg keresése a képernyőpufferen
Alt+szóköz, e, k | Szöveg kijelölése másolásra a képernyőpufferen
Alt+szóköz, e, p | A vágólap tartalmának illessze be a Windows PowerShell-konzol
Alt+szóköz, c | Zárja be a Windows PowerShell-konzol
Ctrl+Break | A Windows PowerShell ablak bezárásához kényszerítése
Ctrl+Home | Törlés az aktuális parancssor elejétől
Ctrl+End | Törlés a parancssor végéig
F1 | A kurzor mozgatása egy karakterrel jobbra a parancssorban
F2 | Új parancs létrehozása az utolsó parancs másolásával az éppen gépelt karakterig
F3 | A parancssor kiegészítése az utolsó parancssorból származó tartalommal
F4 | Karakterek törlése a kurzor helyétől kezdve
F5 | Keresés a parancselőzményekben. Parancsok a parancselőzményekben szereplő Windows PowerShell-elérés az eléréséhez kattintson a **előzmények** görgetőgombokra a webalapú konzolon.
F7 | Parancs interaktív kiválasztása a parancselőzményekben
F8 | Keresés az előzményekben az aktuális szöveggel egyező parancsok megjelenítéséhez
F9 | Adott számozású parancs futtatása az előzményekből
Page Up | Az előzményekben található első parancs futtatása
Page Down | Az előzményekben található utolsó parancs futtatása
Alt+F7 | A parancselőzmények listájának törlése

### <a name="limitations-of-the-web-based-console"></a>A webalapú konzol korlátozásai

- Két ugrásos

    Akkor találkozhat a két Ugrás (vagy csatlakozás egy második számítógéphez az első kapcsolatról) korlátozásával, próbál létrehozni munkamenetet vagy dolgozni rajta egy új Windows PowerShell-elérés használatával. Windows PowerShell-elérés egy távoli futási teret használ, és jelenleg **PowerShell.exe** nem támogatja a távoli kapcsolat létrehozása egy második számítógéphez egy távoli futási térből. Ha egy második távoli számítógéphez való csatlakozás meglévő kapcsolat használatával kísérli meg a **Enter-PSSession** parancsmagot, például akkor különböző hibákat kaphat, például a "œCannot beolvasása a hálózati erőforrásokhoz.

    Két ugrásos hibák elkerülése érdekében a rendszergazdának konfigurálnia kell a CredSSP-hitelesítést a szervezet hálózati környezetében. A CredSSP-hitelesítés konfigurálásával kapcsolatos további információkért lásd: [CredSSP for second-hop remoting](https://blogs.msdn.com/b/powershell/archive/2008/06/05/credssp-for-second-hop-remoting-part-i-domain-account.aspx) a Microsoft webhelyén. Ha egy második távoli számítógépet is szeretne felügyelni, érdemes explicit módon megadott hitelesítő adatokat használni; az implicit módon megadott hitelesítő adatok általában nem engedélyezik a kétugrásos kapcsolatot.

- Távoli eljáráshívás

    Windows PowerShell-elérés használja, és a egy távoli Windows PowerShell-munkamenetet, ugyanazokkal a korlátozásokkal rendelkezik. A Windows-konzol API-jait közvetlenül hívó parancsok – például a konzolalapú szerkesztők vagy szöveges menüprogramok parancsai – nem működnek, mert a parancsok nem olvasnak vagy írnak szabványos bemeneti, kimeneti és hibafolyamatokba. Ezért egy végrehajtható fájl elindító parancsok fájlt, mint például **notepad.exe**, vagy a grafikus felhasználói Felülettel, például a megjelenítendő `OpenGridView` vagy `ogv`, nem működnek. Ez a viselkedés; hatással van a felhasználói élmény Ön úgy tűnik, hogy a Windows PowerShell-elérés nem válaszol a parancshoz.

- Kiegészítés

    Kiegészítés funkció nem működik a munkamenet-konfigurációban, vagy egy korlátozott futási térrel, amely a **NoLanguage** mód. Bár a rendszergazdák konfigurálhatnak úgy egy munkamenetet, hogy az támogassa a parancssori kiegészítést, ez biztonsági okokból nem javasolt, mivel a következő információkat jogosulatlan felhasználók számára is elérhetővé teheti.

    - Belső fájlrendszeri elérési utak

    - Belső számítógépeken található megosztott mappák

    - A futási térben található változók

    - Betöltött típusok vagy a .NET-keretrendszer névterei

    - Környezeti változók

- **NoLanguage** munkamenet vagy korlátozott futási térrel

    Bejelentkezett felhasználók egy **NoLanguage** munkamenet-konfiguráció vagy a Windows PowerShell-elérés korlátozott futási térrel nem futtatható a **kilépési** parancsot a munkamenet befejezéséhez. Jelentkezzen ki, hogy a felhasználók kattintanak kell **Kijelentkezés** a konzol oldalon.

- Egyidejű csatlakozás több célszámítógéphez.

    Ha az átjáró-kiszolgálót futtat Windows Server 2012, Windows PowerShell-elérés lehetővé teszi a böngésző-munkamenetenként csak egy távoli számítógép csatlakoztatását nem teszi lehetővé a felhasználók bejelentkezés után, és több távoli számítógéphez csatlakozni külön böngészőlapokon. Amikor megnyit egy új lapot vagy böngészőablakot, Windows PowerShell-elérés felszólítja, hogy az aktuális munkamenet leválasztása és a egy új munkamenetet úgy, hogy csatlakozhat az új (vagy ugyanazon) távoli számítógépen. Legalább két külön munkameneteket szüksége különböző távoli számítógépekhez igény szerint azonban az Internet Explorer egyik funkciója lehetővé teszi új munkamenetet létrehozni. Új böngésző-munkamenet indítása az Internet Explorerben, nyomja le az ENTER **ALT**, nyissa meg a **fájl** menüt, és válassza ki **új munkamenet**. Ezután nyissa meg a Windows PowerShell-elérés webhely az új munkamenetben, és jelentkezzen be egy másik távoli számítógép eléréséhez.

    A Windows PowerShell-elérés átjáró Windows Server 2012 R2 rendszeren fut, amikor a felhasználók nyithatják több kapcsolat távoli számítógépekkel különböző böngészőlapokon. Ha azt szeretné, egynél több kapcsolatot egy távoli számítógépen megnyitása a webes Windows PowerShell-konzol használatával, akkor egyeztessen a Windows PowerShell-elérés átjáró rendszergazdájához annak ellenőrzéséhez, hogy ez a funkció az átjárókiszolgáló által támogatott.

- Állandó Windows PowerShell-munkamenetek (újracsatlakozás).

    A távoli kapcsolat az átjárón és a célszámítógép között, időtúllépésekor a Windows PowerShell-elérés átjáró után le van zárva. Ilyenkor az éppen futó parancsmagok és parancsfájlok leállnak. Javasoljuk, hogy a Windows PowerShell-lel Ön **-feladat** infrastruktúra végrehajtásakor hosszan futó feladatokat, így a feladatok indításához, válassza le a számítógépről, később újracsatlakozzon, és a feladatok Mindeközben megmaradjanak. Használatának másik előnye **-feladat** parancsmagok, hogy meg tudja elindítani ezeket a Windows PowerShell-elérés, jelentkezzen ki, és majd később újra futó Windows PowerShell-elérés vagy egy másik gazdagépre (például a Windows PowerShell Integrált parancsfájl-kezelési környezet (ISE)).

- Konzol átméretezése.

    A **PowerShell.exe** konzolablakot is a következő három módszerrel lehet átméretezni.

    - Húzza és módosítsa a konzolablak méretét az egérrel

    - Módosítsa a magassági és szélességi tulajdonságot a konzol tulajdonságainak grafikus felhasználói felületén

    - Módosítsa a konzolablak magasságát és szélességét egy parancsmaggal

        A konzolablakban a Windows PowerShell-elérés a következő parancsmagok segítségével konfigurálhatók. A következő példában a felhasználó módosítja a Windows PowerShell-elérés konzol szélessége **20**.

            $newSize = $Host.UI.RawUI.WindowSize
            $newSize.Width = $newSize.Width - 20

            $oldSize = $Host.UI.RawUI.WindowSize

            $Host.UI.RawUI.WindowSize = $newSize

        A konzol magassága hasonló módon változtatható.

        A konzol Nézet testreszabására vonatkozó további példákat érhetők el a [Windows PowerShell csapatának blogját](https://blogs.msdn.com/b/powershell/).

## <a name="see-also"></a>Lásd még:

- [Windows PowerShell-parancsmagok leírása](https://technet.microsoft.com/library/ee407531(ws.10).aspx)
- [Windows PowerShell a Microsoft TechNet webhelyen](https://technet.microsoft.com/library/bb978526.aspx)
- [TechNet Script Center-tár](https://gallery.technet.microsoft.com/scriptcenter)
- [Script Center – Hey, Scripting Guy!](https://technet.microsoft.com/scriptcenter)
- [Windows PowerShell Csapatblog](https://blogs.msdn.com/b/powershell/)