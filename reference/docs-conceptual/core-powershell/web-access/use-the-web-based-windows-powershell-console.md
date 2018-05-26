---
ms.date: 08/23/2017
keywords: PowerShell parancsmag
title: a web alapú windows powershell konzol használata
ms.openlocfilehash: 5d29a6f97fddf4b329fcc7097cf7d40d47d22cca
ms.sourcegitcommit: 735ccab3fb3834ccd8559fab6700b798e8e5ffbf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/25/2018
---
# <a name="use-the-web-based-windows-powershell-console"></a>A webalapú Windows PowerShell konzol használata

Frissített: Június 24 2013.

Vonatkozik: Windows Server 2012 R2, Windows Server 2012-ben

A Windows PowerShell Web Access lehetővé teszi, hogy a felhasználók jelentkezzen be egy biztonságos webhely; Ahhoz, hogy a Windows PowerShell munkamenetek, -parancsmagok és parancsfájlok segítségével egy távoli számítógép kezeléséhez.

Mivel a Windows PowerShell konzol webböngészőben fut, akkor nyitható számos különféle ügyféleszközről; egy webböngészővel rendelkező szinte minden eszköz működik.

A webes Windows PowerShell-konzolban a távoli számítógép, amely a bejelentkezési folyamat részeként a felhasználó által megadott célja.

Ez a témakör ismerteti, hogyan jelentkezzen be, és a Windows PowerShell Web Access webalapú konzol használatának megkezdéséhez.

Ez a témakör nem ismerteti a Windows PowerShell használatával, vagy parancsmagok vagy parancsfájlok futtatásának.
Windows PowerShell és a parancsfájl-kezelési erőforrások használatával kapcsolatos információkért lásd: a [lásd még](#see-also) szakasz Ez a témakör végén.

## <a name="supported-browsers-and-client-devices"></a>Támogatott böngészők és ügyféleszközök

A Windows PowerShell Web Access a következő webböngészőket támogatja.
Bár a mobilböngészők hivatalosan nem támogatottak, számos mobilböngésző képes a webalapú Windows PowerShell konzol futtatásához.
Egyéb, cookie-kat elfogadó, JavaScriptet és HTTPS-webhelyeket futtató böngészők valószínűleg képesek a konzol használatára, de hivatalosan még nem lettek tesztelve.

### <a name="supported-desktop-computer-browsers"></a>Támogatott asztali számítógépes böngészők

- Windows Internet Explorer alkalmazás Microsoft Windows 8.0, 9.0, 10.0 és 11.0
- Mozilla Firefox 10.0.2
- Google Chrome-17.0.963.56m Windows
- Apple Safari 5.1.2 Windows rendszerhez
- Apple Safari 5.1.2 Mac OS

### <a name="minimally-tested-mobile-devices-or-browsers"></a>Minimális tesztelésen átesett mobileszközök és böngészők

- Windows Phone 7 és 7.5
- Google Android WebKit 3.1 böngésző Android 2.2.1-en (Kernel 2.6)
- Apple Safari 5.0.1-es iPhone operációs rendszerhez
- Apple Safari 5.0.1-es iPad 2 operációs rendszerhez

### <a name="browser-requirements"></a>Böngészőkre vonatkozó követelmények

A Windows PowerShell Web Access webalapú konzol használatához böngészők a következőket kell tennie.

- A Windows PowerShell Web Access-átjáró webhelyéről cookie-k engedélyezése.
- HTTPS-lapok megnyitása és olvasása.
- JavaScriptet használó webhelyek megnyitása és futtatása.

## <a name="signing-in-to-windows-powershell-web-access"></a>Bejelentkezés a webes Windows PowerShell-elérésbe

A Windows PowerShell Web Access rendszergazdájától kaphatja meg azt, hogy a szervezetek Windows PowerShell Web Access-átjáró webhelyének címe URL-címet.
Alapértelmezés szerint ez a cím van *https://\<kiszolgáló_neve\>/pswa*.

Mielőtt bejelentkezik a Windows PowerShell Web Access, lehet, hogy rendelkezik-e a neve vagy IP-cím segítségével felügyelni kívánt távoli számítógép.
Jogosult felhasználónak kell lennie a távoli számítógépen, amelyet úgy kell konfigurálni, hogy engedélyezze a távoli felügyeletet.
A számítógép távoli felügyelet engedélyezéséhez konfigurálásával kapcsolatos további információkért lásd: [használata a Windows PowerShell távoli parancsok engedélyezése és](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enable-psremoting).

A legegyszerűbben úgy konfigurálhatja a számítógép távoli felügyelet engedélyezéséhez, hogy futtassa a **Enable-PSRemoting - force** parancsmagot a számítógépen megnyitott Windows PowerShell-munkamenetet emelt szintű felhasználói jogosultságokkal (**Futtatás rendszergazdaként**).

### <a name="to-sign-in-to-windows-powershell-web-access"></a>Bejelentkezés a webes Windows PowerShell-elérésbe

1. Nyissa meg a Windows PowerShell Web Access webhely egy böngészőablakban vagy lapon.

1. A Windows PowerShell Web Access bejelentkezési lapján adja meg a hálózati felhasználónevet, jelszót és kezelni kívánt számítógép (és amely van jogosultsága) nevét. Ha a Windows PowerShell Web Access rendszergazdájának utasítása szerint egy URI-t egy egyéni webhely- vagy proxykiszolgáló használata a számítógép neve helyett, jelölje be **kapcsolati URI** a a **kapcsolattípus** mezőben, majd Adja meg az URI azonosító.

    > ![Megjegyzés:](images/Note.jpeg) **Megjegyzés**:
    >
    > - Ha a célszámítógép egy munkacsoport, használja a következő szintaxist a felhasználónév megadásához és a számítógépre történő bejelentkezéshez: `<workgroup_name>\<user_name>`
    > - Ha a célszámítógép az átjárókiszolgáló, megadhatja `localhost` a számítógép neve mezőbe
    > - Ha a célszámítógép az átjárókiszolgáló, pedig az átjárókiszolgáló egy munkacsoporthoz tartozik, akkor kell használnia `<workgroup name>\<user_name>` bejegyezve a felhasználó nevében. Használhat `localhost` a számítógép neve mezőben.

1. A **választható kapcsolati beállítások** szakasz segítségével felügyelni kívánt távoli számítógép engedélyezési követelményeihez kapcsolódik. A választható kapcsolati beállításokkal egyenértékű paraméterekre vonatkozó további információkért lásd: a [Enter-PSSession](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enter-pssession) a parancsmag súgójában talál.

    Általában a Windows PowerShell Web Access-átjárón keresztül használt hitelesítő adatok megegyeznek a kezelni kívánt távoli számítógép által elfogadottakkal. Azonban ha azt szeretné, hogy különböző hitelesítő adatot használnak a távoli számítógép kezeléséhez, amelyet a 2. lépés, bontsa ki a **választható kapcsolati beállítások** szakaszt, és adja meg a másodlagos hitelesítő adatokat. Egyéb esetben folytassa a 6. lépéssel.

1. Ha a Windows PowerShell Web Access rendszergazdája létrehozta a Windows PowerShell Web Access felhasználók egyéni munkamenet-konfigurációt, írja be a munkamenet-konfiguráció nevét a nevét a **konfigurációnévvel** mező. Munkamenet-konfigurációkkal kapcsolatos további információkért lásd: [about_session_configuration_files](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_session_configurations).

1. Tartsa a **hitelesítési típus** beállítása **alapértelmezett** kivéve, ha egyéb ehhez a Windows PowerShell Web Access-rendszergazda által kapott utasítást.

1. Kattintson a **bejelentkezés**.

## <a name="signing-out-and-timing-out"></a>Kijelentkezés és időtúllépés

Az alábbi kijelentkezik a webes Windows PowerShell-munkamenetben.

- Kattintson a **Kijelentkezés** a konzol jobb alsó sarkában található. (Csak Windows Server 2012)

- Kattintson a **mentése** vagy **kilépési** a (csak Windows Server 2012 R2) konzol jobb alsó sarkában található. Kattintson a **mentése** ezzel menti és bezárja a Windows PowerShell Web Access munkamenet; később csatlakozhat. Amikor bejelentkezik a Windows PowerShell Web Access újra, a Windows PowerShell Web Access a mentett munkamenetek; listáját jeleníti meg Válassza ki, és csatlakozzon újra egy mentett munkamenetet, vagy indítson egy újat. Az egyes felhasználók számára engedélyezett mentett és aktív munkamenetek maximális számát az átjáró rendszergazdája határozza meg.

    Kattintson a **kilépési** kijelentkezik a Windows PowerShell Web Access munkamenet mentés nélkül.

- Megpróbálhat bejelentkezni egy másik távoli számítógép kezeléséhez ugyanazon a böngészői munkameneten belül, vagy a böngészői munkamenet egy új lapjáról. (Ez alól kivételt képez az átjárókiszolgáló fut a Windows Server 2012 R2-t Windows PowerShell Web Access fut a Windows Server 2012 R2 lehetővé teszi több felhasználói munkamenet új lapokon az ugyanazon böngésző-munkamenet.) Ugyanazon a számítógépen egynél több aktív munkamenet használatával kapcsolatos további információkért lásd: csatlakozás több célszámítógéphez egyszerre szerepel a [a webalapú konzol korlátozásai](#limitations-of-the-web-based-console) című szakaszát.

- 20 percig ne végezzen semmilyen tevékenységet a munkameneten belül. Az átjáró rendszergazdája testreszabhatja az inaktivitás időkorlátját. További információkért lásd: [munkamenet-kezelés](authorization-rules-and-security-features-of-windows-powershell-web-access.md#session-management).

    - Ha a kapcsolat nélküli egy munkamenettel a webalapú konzol a hálózati hiba vagy egyéb nem tervezett leállás vagy hibája miatt, és nem, mert a munkamenet lezárta magát, a Windows PowerShell Web Access továbbra is fut, csatlakoztatja a cél számítógép, amíg az időkorlátjuk az ügyfél oldali telik. Alapértelmezés szerint ez az időkorlát 20 perc, amelyet az átjáró rendszergazdája konfigurál. A munkamenet leválasztása vagy az alapértelmezett 20 perc lejárata után, vagy az átjáró rendszergazdája által megadott időtartam lejárata után (amelyik rövidebb) történik meg.

        Ha az átjárókiszolgáló fut a Windows Server 2012 R2, Windows PowerShell Web Access lehetővé teszi, hogy a felhasználók újracsatlakozás a mentett munkamenetekhez egy későbbi időpontban, de nem látható, vagy nem kapcsolódhatnak a mentett munkamenetekhez, amíg az átjáró által megadott időtartam lejárata után a rendszergazda letelt.

- Zárja be a böngészőablakot vagy -lapot.

- Kapcsolja ki azt az ügyféleszközt, amelyen a böngésző fut, vagy válassza le a hálózatról.

- Fut a **kilépési** parancsot a webkonzolon. Ez a parancs nem használható, ha a munkamenet-konfiguráció, amelyhez csatlakozik, támogatására van konfigurálva [NoLanguage](https://msdn.microsoft.com/library/windows/desktop/system.management.automation.pslanguagemode.aspx) módban, vagy korlátozott futási térben van.

Ha azt szeretné, hogy jelentkezzen be újra, nyissa meg újra a Windows PowerShell Web Access weblapot, és jelentkezzen be a megfelelő lépéseket követve [bejelentkezés a Windows PowerShell Web Access](#signing-in-to-windows-powershell-web-access) ebben a témakörben.

## <a name="differences-in-the-web-based-windows-powershell-console"></a>A webalapú Windows PowerShell konzolok közötti különbségek

A webes Windows PowerShell-konzolban történő bejelentkezés után a Windows PowerShell Web Access a böngészőablakban vagy lapon nyílik meg. A konzol csatlakozik a távoli számítógépen, a bejelentkezési folyamat során adott meg, mert csak ezeket a Windows PowerShell-parancsmagok vagy parancsfájlok, amelyek elérhetők a távoli számítógépen is használható a konzolon. Ez a szakasz ismerteti a Windows PowerShell Web Access-konzolon, és a telepített és a Windows PowerShell Web Access konzolok közötti különbségek más korlátozásai **PowerShell.exe** konzol.

### <a name="functional-disparity-with-powershellexe"></a>Funkcióbeli eltérések a PowerShell.exe konzolhoz képest

A legtöbb Windows PowerShell állomás funkció érhető el a Windows PowerShell Web Access webalapú konzol, de bizonyos funkciók, amelyek nem érhető el.

- Megjeleníti a beágyazott folyamatban van.

  A Windows PowerShell Web Access megjelennek a grafikus felhasználói Felülettel a parancsmagok, hogy a jelentés folyamatban van, de csak a legfelső szintű állapotinformációk jelennek meg.

- Bemeneti szín módosítása.

  A bemeneti színt (az előtér és a háttér színét) nem lehet módosítani. A kimenet, a figyelmeztetés, a részletes és a hibaüzenetek stílusát egy parancsfájl futtatásával lehet módosítani.

- PSHostRawUserInterface.

  A Windows PowerShell Web Access Windows PowerShell távoli felügyeletének van megvalósítva, és egy távoli futási teret használ. A Windows PowerShell Web Access nem implementálja az egyes módszerek ezen a felületen; például olyan parancsokat, amelyek a Windows-konzol ír. Parancsok, mint **PowerTab** nem működik a Windows PowerShell Web Access.

- Funkcióbillentyűk.

  A Windows PowerShell Web Access nem támogatja egyes funkcióbillentyűket sok esetben a parancsok a böngésző által fenntartott mert.

### <a name="unsupported-shortcut-keys"></a>Nem támogatott a gyorsbillentyűk

Funkcióbillentyűk | Művelet
-- | --
Ctrl+C | A Windows PowerShell Web Access **Ctrl + C** másolhatják a tartalmat a böngésző használják. A konzolon található egy **Mégse** gombra, és a felhasználók is használhatja **Ctrl + Q** a parancsok visszavonásához.
Alt+szóköz, e, l | A képernyőpuffer görgetése
Alt+szóköz, e, f | Szöveg keresése a képernyőpufferen
Alt+szóköz, e, k | Szöveg kijelölése másolásra a képernyőpufferen
Alt+szóköz, e, p | A vágólap tartalmának beillesztése a Windows PowerShell-konzollal
Alt+szóköz, c | Zárja be a Windows PowerShell-konzollal
Ctrl+Break | A Windows PowerShell ablak bezárásához kényszerítése
Ctrl+Home | Törlés az aktuális parancssor elejétől
Ctrl+End | Törlés a parancssor végéig
F1 | A kurzor mozgatása egy karakterrel jobbra a parancssorban
F2 | Új parancs létrehozása az utolsó parancs másolásával az éppen gépelt karakterig
F3 | A parancssor kiegészítése az utolsó parancssorból származó tartalommal
F4 | Karakterek törlése a kurzor helyétől kezdve
F5 | Keresés a parancselőzményekben. A Windows PowerShell Web Access a parancselőzményekben szereplő parancsok eléréséhez kattintson a **előzmények** görgetőgombokra a webalapú konzol.
F7 | Parancs interaktív kiválasztása a parancselőzményekben
F8 | Keresés az előzményekben az aktuális szöveggel egyező parancsok megjelenítéséhez
F9 | Adott számozású parancs futtatása az előzményekből
Page Up | Az előzményekben található első parancs futtatása
Page Down | Az előzményekben található utolsó parancs futtatása
Alt+F7 | A parancselőzmények listájának törlése

### <a name="limitations-of-the-web-based-console"></a>A webalapú konzol korlátozásai

- Két ugrásos

    Akkor találkozhat a két Ugrás (vagy csatlakozó egy második számítógéphez az első kapcsolatról) korlátozásával, amikor megpróbál létrehozni, vagy új munkamenetet Windows PowerShell webes elérés használatával működik. A Windows PowerShell Web Access egy távoli futási teret használ, és jelenleg **PowerShell.exe** nem támogatja a távoli kapcsolat létrehozásához egy második számítógéppel egy távoli futási térből. Ha egy második távoli számítógéphez való csatlakozás meglévő kapcsolat használatával kísérli meg a **Enter-PSSession** parancsmag, például akkor különböző hibákat kaphat, például a "œCannot beolvasása a hálózati erőforrásokhoz.

    Két ugrásos hibák elkerülése érdekében a rendszergazdának a szervezet hálózati környezetben konfigurálnia a CredSSP-alapú hitelesítés kell. A CredSSP-hitelesítés konfigurálásával kapcsolatos további információkért lásd: [second-hop remoting a CredSSP](http://blogs.msdn.com/b/powershell/archive/2008/06/05/credssp-for-second-hop-remoting-part-i-domain-account.aspx) a Microsoft webhelyén. Ha egy második távoli számítógépet is szeretne felügyelni, érdemes explicit módon megadott hitelesítő adatokat használni; az implicit módon megadott hitelesítő adatok általában nem engedélyezik a kétugrásos kapcsolatot.

- Távoli eljáráshívás

    A Windows PowerShell Web Access használ, és egy távoli Windows PowerShell-munkamenetet, ugyanazokkal a korlátozásokkal rendelkezik. A Windows-konzol API-jait közvetlenül hívó parancsok – például a konzolalapú szerkesztők vagy szöveges menüprogramok parancsai – nem működnek, mert a parancsok nem olvasnak vagy írnak szabványos bemeneti, kimeneti és hibafolyamatokba. Ezért egy végrehajtható fájl elindító parancsok fájlba, például a **notepad.exe**, vagy egy grafikus felhasználói Felülettel, például a `OpenGridView` vagy `ogv`, nem működnek. Ez a viselkedés; hatással van a felhasználói élmény Önnek úgy tűnik, hogy a Windows PowerShell Web Access nem válaszol a parancsot.

- Kiegészítést

    Egy munkamenet-konfiguráció vagy annak egy korlátozott futási térrel rendelkező, amely nem működik kiegészítést **NoLanguage** mód. Bár a rendszergazdák konfigurálhatnak úgy egy munkamenetet, hogy az támogassa a parancssori kiegészítést, ez biztonsági okokból nem javasolt, mivel a következő információkat jogosulatlan felhasználók számára is elérhetővé teheti.

    - Belső fájlrendszeri elérési utak

    - Belső számítógépeken található megosztott mappák

    - A futási térben található változók

    - Betöltött típusok vagy a .NET-keretrendszer névterei

    - Környezeti változók

- **NoLanguage** munkamenet, vagy korlátozott futási térrel

    Felhasználók, akik jelentkezik be egy **NoLanguage** munkamenet-konfiguráció vagy a Windows PowerShell Web Access korlátozott futási térrel nem futtatható a **kilépési** parancsot a munkamenet befejezéséhez. Jelentkezzen ki, hogy a felhasználó kattint kell **Kijelentkezés** a konzollapon.

- Egyidejű csatlakozás több célszámítógéphez.

    Ha az átjárókiszolgáló fut a Windows Server 2012, Windows PowerShell Web Access lehetővé teszi, hogy csak egy távoli számítógép csatlakoztatását egy böngésző-munkamenet; nem teszi lehetővé a felhasználók bejelentkezés után, és több távoli számítógéphez csatlakozni külön-külön böngészőlapokon használatával. Amikor megnyit egy új lapot vagy böngészőablakot, Windows PowerShell Web Access kéri válassza le a jelenlegi munkamenethez, és indítson el egy új munkamenetet, így csatlakozni az új (vagy ugyanazon) távoli számítógépen. Két vagy több különböző távoli számítógépekhez külön munkamenetek igény szerint azonban az Internet Explorer egy szolgáltatása lehetővé teszi egy új munkamenetet létrehozni. Az Internet Explorer egy új böngésző-munkamenet elindításához nyomja le az **ALT**, nyissa meg a **fájl** menüben, majd válassza ki **új munkamenet**. Ezután nyissa meg a Windows PowerShell Web Access webhely az új munkamenetben, és jelentkezzen be egy másik távoli számítógép eléréséhez.

    A Windows PowerShell Web Access-átjáró Windows Server 2012 R2 rendszeren fut, ha felhasználók nyithatják meg több kapcsolatot távoli számítógépekkel különböző böngészőlapokon. Ha azt szeretné, egynél több kapcsolat egy távoli számítógéphez való megnyitásához a webes Windows PowerShell konzol használatával, kérje meg a Windows PowerShell Web Access-átjáró rendszergazdájánál, hogy ha ezt a szolgáltatást az átjáró kiszolgáló által támogatott.

- Állandó Windows PowerShell-munkamenetek (újracsatlakozás).

    Miután Ön túllépi az időkorlátot a Windows PowerShell Web Access-átjáró az átjáró és a célszámítógép között a távoli kapcsolat le van zárva. Ilyenkor az éppen futó parancsmagok és parancsfájlok leállnak. A Windows PowerShell hosszúan **-feladat** infrastruktúra végrehajtásakor hosszan futó feladatokat, hogy elindítson feladatokat, válassza le a számítógépről, később újracsatlakozzon, és feladatok Mindeközben megmaradjanak. Egy másik előnye, hogy használ **-feladat** parancsmagok, hogy a Windows PowerShell Web Access használatával indítsa el őket, jelentkezzen ki, és beállíthatja, majd később újra fut a Windows PowerShell Web Access vagy egy másik gazdagépre (például a Windows PowerShell Integrált parancsfájl-kezelési környezet (ISE)).

- Konzol átméretezése.

    A **PowerShell.exe** konzol lehet átméretezni a következő három módon.

    - Húzza és módosítsa a konzolablak méretét az egérrel

    - Módosítsa a magassági és szélességi tulajdonságot a konzol tulajdonságainak grafikus felhasználói felületén

    - Módosítsa a konzolablak magasságát és szélességét egy parancsmaggal

        A konzolablakban Windows PowerShell Web Access-parancsmagokkal a következőképpen konfigurálható. A következő példában a felhasználó módosítja a Windows PowerShell Web Access konzol szélességének **20**.

            $newSize = $Host.UI.RawUI.WindowSize
            $newSize.Width = $newSize.Width - 20

            $oldSize = $Host.UI.RawUI.WindowSize

            $Host.UI.RawUI.WindowSize = $newSize

        A konzol magassága hasonló módon változtatható.

        A konzolnézet testreszabására vonatkozó további példákat érhetők el a [Windows PowerShell csapatának blogját](http://blogs.msdn.com/b/powershell/).

## <a name="see-also"></a>Lásd még:

- [A Windows PowerShell parancsmag-referencia](https://technet.microsoft.com/library/ee407531(ws.10).aspx)
- [A Windows PowerShell a Microsoft TechNet webhelyen](https://technet.microsoft.com/library/bb978526.aspx)
- [TechNet Script Center-tár](http://gallery.technet.microsoft.com/scriptcenter)
- [Script Center – Hey, Scripting Guy!](https://technet.microsoft.com/scriptcenter)
- [A Windows PowerShell Csapatblog](http://blogs.msdn.com/b/powershell/)