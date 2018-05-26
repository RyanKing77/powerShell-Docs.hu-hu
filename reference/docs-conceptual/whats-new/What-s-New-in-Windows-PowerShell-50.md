---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: A Windows PowerShell 5.0 újdonságai
ms.openlocfilehash: f5a27c0541e21b379f88b318cbe09a0344c1b372
ms.sourcegitcommit: 735ccab3fb3834ccd8559fab6700b798e8e5ffbf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/25/2018
---
# <a name="whats-new-in-windows-powershell-50"></a>A Windows PowerShell 5.0 újdonságai
A Windows PowerShell 5.0 jelentős új szolgáltatásokkal, amelyek kibővítik annak használati, javítják használhatóságát, és felügyelete és kezelése Windows-alapú környezetek egyszerűbb és átfogóbb.

A Windows PowerShell 5.0 visszamenőlegesen kompatibilis. Parancsmagok, szolgáltatók, modulok, beépülő modulok, parancsfájlok, Funkciók, és a profilok a Windows PowerShell 4.0-s verzióját, a Windows PowerShell 3.0 és a Windows PowerShell 2.0 általában tervezett működnek a Windows PowerShell 5.0 változtatás nélkül.

# <a name="installing-windows-powershell"></a>A Windows PowerShell telepítése
Windows Server 2016 Technical Preview és a Windows 10 rendszeren alapértelmezés szerint telepítve van a Windows PowerShell 5.0.

A Windows PowerShell 5.0 telepítése a Windows Server 2012 R2, Windows 8.1 Enterprise vagy Windows 8.1 Pro, töltse le és telepítse [Windows Management Framework 5.0](http://aka.ms/wmf5download). Mindenképpen olvassa el a letöltési részletes adatait, és rendszerkövetelményeknek minden, a Windows Management Framework 5.0 telepítése előtt.

## <a name="in-this-topic"></a>A témakör tartalma

- [A KB 3000850 Windows PowerShell 4.0 DSC frissítések](#windows-powershell-40-updates-in-november-2014-update-rollup-kb-3000850)
- [A Windows PowerShell 5.0 újdonságai](#new-features-in-windows-powershell-50)
- [A Windows PowerShell 4.0 új szolgáltatásai](#new-features-in-windows-powershell-40)
- [Új szolgáltatások a Windows PowerShell 3.0](#new-features-in-windows-powershell-30)

## <a name="windows-powershell-40-updates-in-november-2014-update-rollup-kb-3000850"></a>A Windows PowerShell 4.0 frissítések a 2014. novemberben kiadott kumulatív (KB 3000850)
Sok frissítések és fejlesztések a Windows PowerShell szükséges konfiguráló (DSC) a Windows PowerShell 4.0 rendelkezésre állnak a [2014. novemberben kiadott kumulatív frissítés a Windows RT 8.1, Windows 8.1 és Windows Server 2012 R2](https://support.microsoft.com/kb/3000850/) (KB 3000850 ). Segítségével meghatározhatja, hogy ha KB 3000850 telepítve van a rendszeren futó `Get-Hotfix -Id KB3000850` a Windows PowerShellben.

- Meglévő parancsmagok a frissítéseket a [PSDesiredStateConfiguration](https://technet.microsoft.com/library/dn391651(v=wps.640).aspx) modul

    -   [Get-DscResource](http://technet.microsoft.com/library/dn521625.aspx) gyorsabb (különösen az ISE).

    -   [Start-DscConfiguration](http://technet.microsoft.com/library/dn521623.aspx) egy új paraméter - UseExisting, amely újra alkalmazza a legutolsó alkalmazott konfiguráció tartozik.

    -   [Start-DscConfiguration](http://technet.microsoft.com/library/dn521623.aspx) -Force kijavítása.

    -   [Get-DscLocalConfigurationManager](http://technet.microsoft.com/library/dn407378.aspx) a motor állapota hasznosabb információkat jelenít meg.

    -   [Teszt-DscConfiguration](http://technet.microsoft.com/library/dn407382.aspx) most adja vissza a számítógép nevét, és IGAZ vagy HAMIS eredményt ad.

    -   [Új DscChecksum](http://technet.microsoft.com/library/dn521622.aspx) mostantól támogatja az UNC elérési útvonalakat.

- Az új parancsmagok a [PSDesiredStateConfiguration](http://technet.microsoft.com/library/dn391651(v=wps.640).aspx) modul

    -   [Frissítés-DscConfiguration](http://technet.microsoft.com/library/mt143541(v=wps.630).aspx): igény szerinti lekéréses kiszolgáló-ellenőrzést végez.

    -   [STOP-DscConfiguration](http://technet.microsoft.com/library/mt143542(v=wps.630).aspx): leállítja a konfigurációkat, amelyek már jelenleg is fut.

    -   [Remove-DscConfigurationDocument](http://technet.microsoft.com/library/mt143544(v=wps.630).aspx): lehetővé teszi, hogy távolítsa el a konfigurációs dokumentumok különböző szakaszaiban (folyamatban, aktuális vagy korábbi).

- Nyelvi fejlesztései

    -   DependsOn mostantól támogatja az összetett erőforrásokat.

    -   DependsOn számok mostantól támogatja az erőforrás-példány nevét.

    -   Csomópont-kifejezések kiértékelésének eredménye üres már nem throw hibák.

    -   Hiba, amely akkor fordul elő, ha egy csomópont kifejezés eredménye üres kijavítása.

    -   Most hívása konfigurációk konfigurációk működik a Windows PowerShell-konzolban.

- Lekéréses mód fejlesztései

    -   Lekéréses mód mostantól támogatja az összes ZIP-fájl.

    -   **AllowModuleOverwrite** most már megfelelően működik-e.

- Rugalmasság fejlesztései

    -   Új **DebugMode** lehetővé teszi, hogy töltse be újra az erőforrás-modulok.

    -   Konfigurációs hiba lép fel, ha a pending.mof fájl nem törlődik.

    -   A helyi Configuration Manager (LCM) mostantól rugalmasabb, amikor metakonfigurációját beállításai megsérültek.

- Diagnosztikai fejlesztései

    -   A figyelmeztetés akkor jelenik meg, amikor a LCM értékűre állítja be a időzítő különböző beállítások, mint a megadott.

    -   Hiba naplófájlok mostantól tartalmazza a Windows PowerShell-erőforrások a hívási veremben.

- Rugalmasság fejlesztései

    -   A LocalConfigurationManager erőforrás tulajdonsága egy új, **ActionAfterReboot**.

        -   ContinueConfiguration (alapértelmezett érték): a konfiguráció automatikusan folytatja a cél csomópont újraindítása után.

        -   StopConfiguration: Automatikusan folytatódik a konfigurációs csomópont újraindítása után.

    -   Konzisztencia Futtatás most fordulhat gyakrabban egy LEKÉRÉSES műveletet, vagy fordítva.

    -   Versioning támogatási: DSC most felismerje a dokumentum lett létrehozva, egy újabb ügyfél (mellékelt [WMF 5.0](http://aka.ms/wmf5download)).

- Hiba megelőzéséhez fejlesztései

    -   Modul verziója most kényszerítése a konfiguráció alkalmazása előtt.

    -   **DebugPreference** most már megfelelően van beállítva a Get-, Set- vagy a teszt-TargetResource hívások.

- Hitelesítő adatok kezelése fejlesztései

    -   A tanúsítvány most szolgál, ha mindkét **tanúsítvány** és **PSDscAllowPlainTextPassword** vannak megadva.

    -   Hitelesítő adatok lesznek visszafejtve, még a Get-TargetResource.

    -   Metakonfigurációját hitelesítő adatokat titkosítása és visszafejtése.

    -   PSCredentials most lesznek visszafejtve, amikor a beágyazott objektum.

- Beépített erőforrás fejlesztései

    -   A csomag erőforrás

        -   Már nem telepíti a megfelelő (vagy a helyi vagy webes adatforrások).

        -   Most már támogatja a HTTPS PROTOKOLLT.

    -   Most már támogatja a HTTPS-hez a [erőforrás csomag](http://technet.microsoft.com/library/dn282132.aspx).

    -   [Erőforrás archiválására](http://technet.microsoft.com/library/dn249917.aspx) mostantól támogatja a hitelesítő adatokat.

## <a name="new-features-in-windows-powershell-50"></a>A Windows PowerShell 5.0 újdonságai

- [A Windows PowerShell újdonságai](#new-features-in-windows-powershell)
- [Új szolgáltatások a Windows PowerShell célállapot-konfiguráció](#new-features-in-windows-powershell-desired-state-configuration)
- [Új szolgáltatások a Windows PowerShell ISE](#new-features-in-windows-powershell-ise)
- [Új szolgáltatások a Windows PowerShell webszolgáltatások](#new-features-in-windows-powershell-web-services-management-odata-iis-extension)
- [A Windows PowerShell 5.0 figyelmet a jelentősebb hibajavítások](#notable-bug-fixes-in-windows-powershell-50)

### <a name="new-features-in-windows-powershell"></a>A Windows PowerShell újdonságai

- A Windows PowerShell 5.0-től kezdődően fejleszthet osztályok, a formális szintaxisát és egyéb objektumorientált programozási nyelvek hasonló szemantika használatával. **Osztály**, **Enum**, és a Windows PowerShell-nyelv az új szolgáltatást támogató más kulcsszavak lettek hozzáadva. Osztályok kezelésével kapcsolatos további információkért lásd: about_Classes.

- A Windows PowerShell 5.0 vezet be egy új, strukturált adatfolyamot, melyekkel küldött strukturált adatok parancsfájlt és a hívók (vagy közötti üzemeltetési környezet). Write-Host hozható létre az adatfolyamot kimenet most már használhatja. Információk adatfolyamokat is működnek az PowerShell.Streams, feladatok, ütemezett feladatok és munkafolyamatok. A következő funkciókat támogatja az adatfolyamot.

    -   Új írási-információkat a parancsmag, amely lehetővé teszi, hogy adja meg, hogyan kezeli a Windows PowerShell a információkat adatfolyam adatait parancsot. Write-Host egy burkoló írási-információt. Írási-információkat is egy támogatott munkafolyamat-tevékenységet.

    -   Két új közös paraméterek, InformationVariable és InformationAction, segítségével meghatározhatja, hogyan jelennek meg információk adatfolyamokat a parancs. InformationAction érvényes értékei Folytatáscsendben, Stop, folytatás, Inquire, figyelmen kívül hagyása vagy felfüggesztése, az alapértelmezett alatt Folytatáscsendben. InformationVariable egy karakterlánc, amely egy mentett parancs Write-Host adatait szeretné változó nevét adja meg.

    -   Egy új felhasználói beállítási változót, InformationPreference, egy Windows PowerShell-munkamenetben adja meg az adatfolyam adatok alapértelmezett beállításait. Az alapértelmezett érték: Folytatáscsendben.

    -   Két új munkafolyamat általános paramétereit, PSInformation és InformationAction, hozzá lett adva.

    -   A Format-Table parancs használatakor a táblázat oszlopaihoz mostantól automatikusan formázott haladnak keresztül az adatfolyam adatok első 300ms kiértékelésével.

- Együttműködve [Microsoft Research](http://research.microsoft.com/), egy új parancsmagot, ConvertFrom-karakterlánc, hozzá lett adva. ConvertFrom-karakterlánc bontsa ki, és elemezni a szöveges karakterláncok tartalmából strukturált objektumok teszi lehetővé. További információkért lásd: ConvertFrom-karakterlánc.

- Új Convert-karakterlánc parancsmag automatikusan formátumú szöveg, amelyhez - például paraméter biztosító példa alapján.

- Új modul Microsoft.PowerShell.Archive, amelyek lehetővé teszik a fájlok tömörítésével-parancsmagokat tartalmaz, és (más néven ZIP) archív fájlok, mappák fájlok kibontása ZIP-fájloknak a, és rajtuk tömörített fájlok újabb verzióival ZIP fájlt frissíteni.

- Új modul PackageManagement, lehetővé teszi a felderítése, és szoftvercsomagok telepítése az interneten. A PackageManagement (korábbi nevén OneGet) modul-hoz a kezelő vagy a meglévő csomag kezelők (más néven csomag szolgáltatók) multiplexer egységes Windows csomag kezelése egyetlen Windows PowerShell felületet.

- Új modul PowerShellGet, lehetővé teszi, hogy keresse meg, telepítse, közzététele, és frissítse modulok és a DSC-erőforrások a a [PowerShell-galériában](http://www.powershellgallery.com/), vagy egy belső modul tárházban, amely a Register-PSRepository parancsmag futtatásával állíthat be.

- Egy új nyelvi kulcsszó **rejtett**, adja meg, hogy a Get-tag eredményeket alapértelmezés szerint nem jelenik meg (tulajdonság vagy metódus) tag hozzá lett adva (Ha nem a - Force paraméterrel). Tulajdonságok vagy jelölt rejtett módszerek is nem jelennek meg az IntelliSense eredmények csak olyan környezetben, ahol a tagnak kell látható; például az automatikus változók $ez meg kell jelennie az osztály adott metódusát rejtett tagokat.

- Új elem, a Remove-cikk és a Get-ChildItem létrehozásának és kezelésének támogatása továbbfejlesztett [szimbolikus csatolások](http://en.wikipedia.org/wiki/Symbolic_link). A **- ItemType** paramétert a New-elem egy új értéket fogad el **SymbolicLink**. Most már külön sorba szimbolikus hivatkozásokat is létrehozhat, ha a parancsmagot a New-cikk.

- Get-ChildItem is rendelkezik egy új - mélysége paraméter, amely a rekurzió korlátozni a - Recurse paraméterrel együtt használni. Például Get-ChildItem-Recurse - mélysége 2 eredményeket ad vissza az aktuális mappában, a gyermek mappák, az aktuális mappában, és az összes a mappának a gyermek mappák.

- Most már megadható, hogy másol fájlokat vagy mappákat egy Windows PowerShell-munkamenetet a másikra, ami azt jelenti, hogy tud-e fájlokat másolni a távoli számítógépnek csatlakoztatott munkameneteket elem (beleértve futtató számítógépek [Nano Server](http://blogs.technet.com/b/windowsserver/archive/2015/04/08/microsoft-announces-nano-server-for-modern-apps-and-cloud.aspx), és így vannak más felület nélküli). Másolja a fájlokat, az új - FromSession és - ToSession paraméter értékeként adja meg a PSSession azonosítókat, és adjon hozzá - elérési út és - célt adjon meg a forrás elérési útvonalának és cél, illetve. Például elem-elérési út c:\\Sajatfajl.txt - ToSession $s-cél d:\\DestinationFiles.

- A Windows PowerShell írjanak elő javítottuk alkalmazhatja az összes üzemeltetési alkalmazásra (például a Windows PowerShell ISE) mellett a konzol állomás (**powershell.exe**). (Beleértve az egy rendszerszintű Beszélgetés szövegének engedélyezése) írjanak elő beállításokat lehet megadni, mivel lehetővé teszi a **PowerShell írjanak elő bekapcsolása** található a felügyeleti sablonok/Windows összetevők és a Windows csoportházirend-beállítás PowerShell.

- Egy új részletes parancsfájl nyomkövetési szolgáltatás lehetővé teheti, hogy részletes nyomon követését és a Windows PowerShell parancsfájl-kezelési a rendszerben használt elemzését. Részletes parancsfájl nyomkövetésének engedélyezése után a Windows PowerShell összes parancsfájl-blokkokban naplózza az esemény nyomkövetése Windows (ETW) eseménynaplóba **Microsoft-Windows-PowerShell/műveleti**.

- A Windows PowerShell 5.0-től kezdődően új titkosított üzenetek szintaxisának parancsmagok használatával támogatják a titkosítási és visszafejtési tartalom az IETF szabványos formátumban kriptográfiai üzenetek védelmére, megfelelően [RFC5652](http://tools.ietf.org/html/rfc5652). A Get-CmsMessage Protect-CmsMessage és Unprotect-CmsMessage parancsmagokkal bővült a [Microsoft.PowerShell.Security](http://technet.microsoft.com/library/hh849807.aspx) modul.

- Az új parancsmagok a [Microsoft.PowerShell.Utility](http://technet.microsoft.com/library/hh849958.aspx) modul, a Get-futási térben, a hibakeresési-futási térben, a Get-RunspaceDebug, a Enable-RunspaceDebug és a Disable-RunspaceDebug, lehetővé teszik, hogy a futási térből, és a kezdési és befejezési a hibakeresési beállítások megadása a futási teret hibakeresést. Tetszőleges futási terek hibakereséshez "Ez azt jelenti, hogy futási terek, amelyek nem egy Windows PowerShell-konzolt vagy a Windows PowerShell ISE-munkamenet alapértelmezett futási térben" "Windows PowerShell lehetővé teszi a állítson be töréspontokat a parancsfájlt, és töréspontok leállítani a parancsfájl hozzáadása amíg a futási teret parancsfájl hibakeresési hibakereső csatolhat fut. Tetszőleges futási terek beágyazott hibakeresési támogatása a Windows PowerShell-parancsfájl hibakereső a futási terek bővült.

- Új formátumú hexadecimális parancsmag hozzá lett adva a [Microsoft.PowerShell.Utility](http://technet.microsoft.com/library/hh849958.aspx) modul. Hexadecimális formátumú leltárfunkcióját szövegek vagy bináris adatok hexadecimális formátumban.

- Get-Vágólap és a Set-vágólap parancsmagok lettek hozzáadva a [Microsoft.PowerShell.Utility](http://technet.microsoft.com/library/hh849958.aspx) modul; ezek megkönnyítik a tartalomátvitelt a és a Windows PowerShell-munkamenetben. A vágólap parancsmagok támogatja a képek, a hangfájlok, a fájl listák és a szöveg.

- Egy új parancsmagot, a Clear-RecycleBin, hozzá lett adva a [Microsoft.PowerShell.Management](http://technet.microsoft.com/library/hh849827(v=wps.640).aspx) modul; a parancsmag kiüríti az újrahasznosítás Bin rögzített meghajtót, beleértve a külső meghajtók esetében. Alapértelmezés szerint kéri a Clear-RecycleBin parancs, mert a parancsmag a Defaultparametersetname tulajdonság ConfirmImpact.High értékre van állítva.

- Egy új parancsmagot, a New-TemporaryFile, lehetővé teszi a parancsfájl-kezelési részeként ideiglenes fájlt létrehozni. Alapértelmezés szerint az új ideiglenes fájl létrehozása ```C:\Users\<user name>\AppData\Local\Temp```.

- A Out-File, az Add-tartalom és a Set-tartalom parancsmagok most már rendelkezik egy új - NoNewline paraméter, amely egy új sor kihagyja a kimenet után.

- A New-Guid-parancsmaggal hozzon létre egy GUID Azonosítót, akkor hasznos, ha a parancsfájlok vagy DSC erőforrások ír a .NET-keretrendszer Guid osztályt használja.

- Mivel a fájlverzió-információkat félrevezető, különösen, miután egy fájlt van telepítve, FileInfo objektumok új FileVersionRaw és ProductVersionRaw parancsfájl tulajdonságok érhetők el. Például futtathatja a következő parancsot az ezeket a tulajdonságokat a powershell.exe értékek megjelenítése ahol $pid tartalmaz egy futó Windows PowerShell-munkamenethez a Folyamatazonosító:  ```Get-Process -Id $pid -FileVersionInfo | Format-List *version* -Force```

- Új parancsmagok Enter-PSHostProcess és kilépési-PSHostProcess lehetővé teszik, hogy a folyamatok elkülönül az aktuális folyamat, amely a Windows PowerShell-konzolt futtatja a Windows PowerShell-parancsfájlok hibakeresése. Futtassa a Enter-PSHostProcess adja meg, vagy csatlakoztatása egy adott folyamat azonosítója, és futtassa a Get-futási térben vissza az aktív futási terek a folyamaton belül. Futtassa a kilépési-PSHostProcess leválasztása a a folyamat, amikor elkészült, a parancsfájl a folyamaton belüli hibakeresés.

- Várjon, amíg hibakereső új parancsmag hozzá lett adva a [Microsoft.PowerShell.Utility](http://technet.microsoft.com/library/hh849958.aspx) modul. Várjon, amíg hibakereső leállítása a hibakereső-parancsfájl a következő utasítás a parancsfájl futtatása előtt is futtathatja.

- A Windows PowerShell munkafolyamat hibakereső mostantól támogatja a utasítás vagy -lapon befejezését, és a beágyazott munkafolyamat funkciók is hibakeresése. Most lenyomhatja **Ctrl + Break** parancsfájl futtatását, helyi és távoli munkamenetek és egy munkafolyamat-parancsfájl a hibakereső megadását.

- Egy hibakeresési-Job parancsmagnak hozzá lett adva a [Microsoft.PowerShell.Core](http://technet.microsoft.com/library/hh849695.aspx) modul Windows PowerShell munkafolyamat, a háttér és a távoli munkamenetek futnak feladatok futó feladat parancsfájlok hibakeresése.

- Új állapot, AtBreakpoint, a Windows PowerShell-feladatok hozzá lett adva. A AtBreakpoint állapot vonatkozik, amikor olyan parancsfájlt, amely magában foglalja a készlet töréspontok fut egy feladat, és a parancsfájl elérte a töréspont. Ha egy feladat le van állítva, a hibakeresési töréspont, a hibakeresési-Job parancsmagot kell hibakeresést végeznie a feladatot.

- A Windows PowerShell 5.0 ugyanabban a mappában lévő $PSModulePath valósítja meg egy Windows PowerShell-modul több verzióinak támogatása. Egy RequiredVersion tulajdonság bővült a ModuleSpecification osztály segítségével kap egy modul; kívánt verziója Ez a tulajdonság értéke kölcsönösen kizárják egymást az ModuleVersion tulajdonság. A Get-modul, a FullyQualifiedName paraméter értékének részeként mostantól támogatott a RequiredVersion Import-Module és eltávolítása-modul parancsmagokkal.

- Modul verzió érvényesítése is képes lemezvizsgálatok elvégzésére, a teszt-ModuleManifest parancsmag futtatásával.

- A Get-Command parancsmag eredményeinek értékűnek egy Version oszlop; egy új Version tulajdonság a CommandInfo osztály bővült. Get-Command ugyanabban a modulban több verzióinak parancsait tartalmazza. A Version tulajdonság is része a CmdletInfo származtatott osztályait: CmdletInfo és ApplicationInfo.

- Get-Command paramétere egy új, - ShowCommandInfo, PSObjects ShowCommand információt ad vissza. Ez a különösen hasznos funkció a Show-parancs futtatásakor a Windows PowerShell ISE Windows PowerShell távoli eljáráshívás segítségével. A - ShowCommandInfo paraméter lecseréli a meglévő Get-SerializedCommand függvény a Microsoft.PowerShell.Utility modulban, de a Get-SerializedCommand parancsfájl továbbra is támogatja az alacsonyabb szintű scripting elérhető.

- Új Get-ItemPropertyValue parancsmag segítségével egy tulajdonság értékének pontjelöléssel nélkül. Például a régebbi kiadásokban a Windows PowerShell, futtathatja a következő parancs használatával beszerezheti az alkalmazás alapja tulajdonság PowerShellEngine beállításkulcs: **(Get-ItemProperty-elérési út HKLM:\\szoftver\\ Microsoft\\PowerShell\\3\\PowerShellEngine-ApplicationBase neve). ApplicationBase**. A Windows PowerShell 5.0-től kezdődően futtathatja **Get-ItemPropertyValue-elérési út HKLM:\\szoftver\\Microsoft\\PowerShell\\3\\PowerShellEngine-név ApplicationBase** .

- A Windows PowerShell-konzolban most szintaxissal színátmenetekhez, hasonlóan a Windows PowerShell ISE.

- Új NetworkSwitch modul tartalmazza, amelyek lehetővé teszik a Windows Server 2012 R2 embléma hitelesített hálózati kapcsolók kapcsoló, a virtuális LAN (VLAN) és a 2. rétegbeli hálózati kapcsoló port alapkonfiguráció alkalmazandó parancsmagok.

- A FullyQualifiedName paraméter tárolása egy modul különböző verzióinak támogatása Import-Module és eltávolítása-modul parancsmagokkal bővült.

- Save-Help, a Update-Help, a Import-PSSession, a Export-PSSession és a Get-Command van egy új paraméter FullyQualifiedModule ModuleSpecification típusú. Adja hozzá ezt a paramétert adja meg a modul a teljesen minősített neve.

- Értékének **$PSVersionTable.PSVersion** 5.0 környezetébe.

### <a name="new-features-in-windows-powershell-desired-state-configuration"></a>Új szolgáltatások a Windows PowerShell célállapot-konfiguráció

- Windows PowerShell nyelvi fejlesztései lehetővé teszik, hogy adja meg a Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) erőforrások osztályok használatával. Importálás – DscResource már igaz dinamikus kulcsszó; A Windows PowerShell elemzi a megadott modul "™ s gyökérmodult osztályok, amelyek tartalmazzák a DscResource attribútumot keres. Osztályok segítségével mostantól megadhatja a DSC-erőforrások, amelyekre sem MOF-fájlt, sem a modul mappában DSCResource almappában szükség. A Windows PowerShell modul is tartalmazhatnak, több DSC erőforrás osztályok.

- A PSDesiredStateConfiguration modul az alábbi parancsmagok egy új paraméter ThrottleLimit, bővült. Adja hozzá a ThrottleLimit paraméter adható meg a cél számítógépeket és eszközöket, amelyeken a parancs működéséhez egy időben kívánja.

    -   Get-DscConfiguration

    -   Get-DscConfigurationStatus

    -   Get-DscLocalConfigurationManager

    -   Visszaállítás-DscConfiguration

    -   Teszt-DscConfiguration

    -   Hasonlítsa össze-DscConfiguration

    -   Közzététel DscConfiguration

    -   Set-DscLocalConfigurationManager

    -   Start-DscConfiguration

    -   Frissítés-DscConfiguration

- Központosított DSC hibajelentés, a hibával kapcsolatos részletes információk nem csak a rendszer naplózza abban az esetben, ha napló, de elküldhetők egy központi helyen újabb elemzés céljából. A központi hely hozhat tárolása bármely olyan kiszolgáló a környezetben bekövetkezett DSC konfigurációs hibák. Után a metaadat-konfiguráció a jelentéskészítő kiszolgáló megadva, az összes hiba esetén a jelentéskészítő kiszolgálón, majd adatbázisban tárolja, hogy. A lekérési kiszolgálójáról konfigurációk le tudja ezt a funkciót, függetlenül attól,-e a célcsomóponton van konfigurálva állíthat be.

- A Windows PowerShell ISE könnyű DSC erőforrás szerzői fejlesztései. Most tegye a következőket.

    -   Listán belül minden DSC erőforrás egy **konfigurációs** vagy **csomópont** blokk megadásával **Ctrl + szóköz** egy üres sor a blokkon belül.

    -   Az erőforrás-tulajdonságok automatikus kiegészítés a **számbavételi** típusa.

    -   Az automatikus kiegészítés a **DependsOn** tulajdonság DSC-erőforrások, más erőforrás-példánya a konfiguráció alapján.

    -   Továbbfejlesztett kiegészítést az erőforrás-tulajdonságok értékeit.

- A felhasználó most már futtathatja a hitelesítő adatok egy megadott készlet erőforrás hozzáadásával a **PSDscRunAsCredential** attribútum-csomópont címblokkhoz. Például PSDscRunAsCredential = Get-Credential Contoso\\DscUser. Ezt a funkciót érdemes beállítani, futtassa a Windows Installer és végrehajtható telepítők, a felhasználói beállításjegyzék-struktúrát elérésére, és a jelenlegi felhasználói környezetet kívül más feladatok végrehajtására létrehozni.

- 32 bites (x86-alapú) már támogatja az a **konfigurációs** kulcsszó.

- A Windows PowerShell mostantól tartalmazza a DSC-konfigurációk esetén hozzáadásával definiált egyéni segítségét \[CmdletBinding()] létrehozott konfiguráció függvény.

- Egy új **DscLocalConfigurationManager** attribútumot a konfigurációs blokk jelöli ki a metaadat-konfiguráció, a DSC helyi Configuration Manager konfigurálására szolgál. Ez az attribútum a konfigurációját, és csak olyan elemek, amelyek a DSC helyi Configuration Manager beállítása tartalmazó korlátozza. A feldolgozás során ez a konfiguráció hoz létre egy \*. meta.mof fájl a megfelelő célcsomópontokat majd küldött a Set-DscLocalConfigurationManager parancsmag futtatásával.

- Windows PowerShell 5.0 most engedélyezettek részleges konfigurációkat. Konfigurációs dokumentumok biztosíthat töredékben csomóponthoz. A csomópont konfigurációs dokumentum, a csomópont több töredék fogadásához "™ helyi Configuration Manager először meg kell adja meg a várt töredék s

- Kereszt-számítógép szinkronizációs egyik új Windows PowerShell 5.0 DSC. A beépített WaitFor használatával\* erőforrások (**WaitForAll**, **WaitForAny**, és **WaitForSome**), megadhat a függőségek a számítógépeken során konfiguráció futtatása nélkül külső álló üzenettípusok összehangolását. Ezeket az erőforrásokat csomópontok szinkronizálás a WS-Man protokollon keresztül CIM-kapcsolatok használatával adja meg. Egy konfigurációs várja meg, amíg egy másik számítógép "™ s adott erőforrás állapotának módosításához.

- Csak elég adminisztrációs (JEA), egy új delegálás biztonsági funkció, használja a DSC és Windows PowerShell korlátozott futási terek adatvesztés vagy a alkalmazottai, a biztonságos vállalatok érdekében, hogy szándékos vagy véletlen. További információ a JEA, ahonnan letöltheti a xJEA DSC erőforrás, például: [csak elég felügyeleti, lépésről lépésre](http://blogs.technet.com/b/privatecloud/archive/2014/05/14/just-enough-administration-step-by-step.aspx).

- A következő új parancsmagokkal bővült PSDesiredStateConfiguration modulhoz.

    -   Új Get-DscConfigurationStatus parancsmag lekérése egy célcsomóponttal konfigurációs állapotának magas szintű információkat. Ezt úgy szerezheti be a állapota az elmúlt, vagy az összes konfiguráció.

    -   Új összehasonlítása-DscConfiguration parancsmag hasonlítja össze a megadott konfigurációs és egy vagy több célcsomópontokat tényleges állapotának.

    -   Új Publish-DscConfiguration parancsmag konfigurációs MOF-fájlt másolja a célcsomóponton, de nem felel meg a konfigurációt. A konfiguráció alkalmazása a következő konzisztencia fázis során, vagy a frissítés-DscConfiguration parancsmag futtatásakor.

    -   Új vizsgálat-DscConfiguration parancsmag lehetővé teszi, hogy győződjön meg arról, hogy a létrejövő konfigurációt egyezik-e a kívánt konfiguráció, vagy igaz ad vissza, ha a konfiguráció megfelel a kívánt konfiguráció vagy hamis értéket, ha a tényleges konfigurációja nem felel meg a kívánt konfiguráció.

    -   Új frissítés-DscConfiguration parancsmag feldolgozandó konfiguráció kényszeríti. Ha a helyi Configuration Manager lekéréses módban van, a parancsmag a konfiguráció alkalmazása előtt a lekérési kiszolgálójáról kap.

### <a name="new-features-in-windows-powershell-ise"></a>Új szolgáltatások a Windows PowerShell ISE

- Most szerkesztéséhez távoli Windows PowerShell-parancsfájlok és a fájlok a Windows PowerShell ISE, helyi példányának Enter-PSSession távoli munkamenetet indítani a számítógépen fut, amely "™ s a szerkeszteni kívánt fájlok tárolására és majd futó **PSEdit <path and file name on the remote computer>**. Ez a funkció megkönnyíti a Server Core telepítési lehetőség a Windows Server, ahol nem tudja futtatni a Windows PowerShell ISE tárolt szerkesztési Windows PowerShell-fájlokat.

- A Start-Beszélgetés szövegének parancsmag mostantól támogatott a Windows PowerShell ISE.

- A Windows PowerShell ISE távoli parancsfájlok most megoldhassuk.

- Egy új parancsával **összes törés** (Ctrl + B) bontja a hibakereső helyi és távoli futó parancsfájlok.

### <a name="new-features-in-windows-powershell-web-services-management-odata-iis-extension"></a>Új szolgáltatások a Windows PowerShell webszolgáltatások (felügyeleti OData IIS kiterjesztés)

- A Windows PowerShell 5.0-től kezdődően a Windows PowerShell-parancsmagok jelennek meg, ha egy adott OData-végpont az Export-ODataEndpointProxy parancsmagot, az új található funkciókon alapulnak egy készletét hozhat létre [ Microsoft.PowerShell.OdataUtils](http://technet.microsoft.com/library/dn818507(v=wps.640).aspx) modul.

### <a name="notable-bug-fixes-in-windows-powershell-50"></a>A Windows PowerShell 5.0 figyelmet a jelentősebb hibajavítások

- A Windows PowerShell 5.0 tartalmaz egy új COM-megvalósításban kínál, amelyek jelentős teljesítményjavulást eredményezhet esetén COM-objektumok dolgozik. Videó az áttekintésről a hatás, lásd: [Com_Perf_Improvements](http://1drv.ms/1qu3UPZ).

- Jelentős teljesítménybeli fejlesztés első lap végrehajtása egy Windows PowerShell-munkamenetben lerövidíteni lapon befejezési idő szinte 500 ms által történt.

## <a name="new-features-in-windows-powershell-40"></a>A Windows PowerShell 4.0 új szolgáltatásai
A Windows PowerShell 4.0 a visszamenőlegesen kompatibilis. Parancsmagok, szolgáltatók, modulok, beépülő modulok, parancsfájlok, Funkciók, és a profilok a Windows PowerShell 3.0 és a Windows PowerShell 2.0 tervezett működnek a Windows PowerShell 4.0 változtatás nélkül.

A Windows 8.1 és Windows Server 2012 R2 alapértelmezés szerint telepítve van a Windows PowerShell 4.0-s verzióját. A Windows PowerShell 4.0-s verzióját telepíti a Windows 7 SP1 vagy Windows Server 2008 R2, töltse le és telepítse [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855). Mindenképpen olvassa el a letöltési részletes adatait, és rendszerkövetelményeknek minden, a Windows Management Framework 4.0 telepítése előtt.

- [A Windows PowerShell újdonságai](#new-features-in-windows-powershell-1)
- [Új funkciók a Windows PowerShell integrált parancsfájlkezelési környezet (ISE)](#new-features-in-windows-powershell-integrated-scripting-environment-ise)
- [Új szolgáltatások a Windows PowerShell munkafolyamat](#new-features-in-windows-powershell-workflow)
- [Új szolgáltatások a Windows PowerShell webszolgáltatások](#new-features-in-windows-powershell-web-services)
- [Új szolgáltatások a Windows PowerShell Web Access](#new-features-in-windows-powershell-web-access)
- [A Windows PowerShell 4.0 figyelmet a jelentősebb hibajavítások](#notable-bug-fixes-in-windows-powershell-40)

A Windows PowerShell 4.0 a következő új szolgáltatásokat tartalmazza.

### <a name="new-features-in-windows-powershell"></a>A Windows PowerShell újdonságai

- **A Windows PowerShell célállapot-konfiguráció** (DSC) egy olyan új felügyeleti rendszer, a Windows PowerShell 4.0-s verzióját, amely lehetővé teszi a központi telepítési és konfigurációs adatokat a szoftver szolgáltatások és a környezet, amelyben a szolgáltatások futnak kezelését. A DSC kapcsolatos további információkért lásd: [Ismerkedés a Windows PowerShell célállapot-konfiguráció](https://technet.microsoft.com/library/c134aa32-b085-4656-9a89-955d8ff768d0).

- **Save-Help** mostantól lehetővé teszi a távoli számítógépekre telepített modulok súgóját menti. Save-Help segítségével egy internethez csatlakozó ügyfél (amely nem az összes kívánt súgó modulok telepítve van a feltétlenül) modul súgó letöltését, és másolja egy távoli megosztott mappa vagy egy távoli számítógépen, amely nem rendelkezik Internet mentett Súgó a hozzáférés.

- A Windows PowerShell-hibakereső bővítésével lehetővé vált a Windows PowerShell-munkafolyamatok, valamint a távoli számítógépeken futó parancsfájlokat a hibakeresés engedélyezése. A Windows PowerShell-munkafolyamatok mostantól a Windows PowerShell-parancssorból vagy a Windows PowerShell ISE parancsfájl szinten indítja el. Windows PowerShell-parancsfájlok, beleértve a parancsfájl-munkafolyamatok, most keresztül működő távoli munkamenetek indítja el. Hibakeresési működő távoli munkamenetek megmaradnak a Windows PowerShell távoli munkamenet leválasztása és újból később.

- A **RunNow** paramétere **Register-ScheduledJob** és **Set-ScheduledJob** szükségtelenné teszi beállítása egy azonnali kezdési dátum és idő, a feladatok a használatával**Eseményindító** paraméter.

- **Invoke-RestMethod** és **Invoke-WebRequest** most lehetővé teszik, hogy az összes fejléc beállítása a fejlécek paraméter használatával. Bár ez a paraméter mindig megjelenése, volt a webes parancsmagokat, amelyek kivételek vagy hibák miatt több paraméterek egyikét.

- **Get-Module** új paramétereinek, **FullyQualifiedName**, típusú **ModuleSpecification\[]**. A **FullyQualifiedName** paramétert a Get-Module mostantól lehetővé teszi egy modult a modul nevét, verzióját, és szükség esetén a GUID azonosító használatával adja meg.

- Az alapértelmezett végrehajtási házirend-beállítás a Windows Server 2012 R2 **RemoteSigned**. A Windows 8.1 nincs változás az alapértelmezett beállítás.

- A Windows PowerShell 4.0-től kezdődően metódushívás dinamikus metódus-nevek használatával támogatott. Változók használata a metódus nevének megadása tárolja, és majd hívható meg dinamikusan metódus meghívásával beolvasott változó.

- Aszinkron munkafolyamat-feladatok nem lesznek törölve, ha által megadott időkorlát a **PSElapsedTimeoutSec** gyakori munkafolyamat-paraméter lejárt.

- Egy új paraméter **RepeatIndefinitely**, hozzá lett adva a **New-JobTrigger** és **Set-JobTrigger** parancsmagok. Ezzel a megoldással a szükségességét megadása egy **TimeSpan.MaxValue** értékét a **RepetitionDuration** futhat ismétlődően egy ütemezett feladatot határozatlan ideig paramétert.

- A **Passthru** paraméter hozzá lett adva a **Enable-JobTrigger** és **Disable-JobTrigger** parancsmagok. A Passthru paraméter létrehozott vagy a parancs által módosított objektumokat jeleníti meg.

- Adja meg a munkacsoporthoz tartozó paraméter nevek a **Add-Computer** és **Remove-Computer** parancsmagok most megegyeznek. Mindkét parancsmag most már használja a paraméter **Munkacsoport_neve**.

- Egy új közös paraméter **PipelineVariable**, hozzá lett adva. PipelineVariable változóként, is átadható a feldolgozási folyamat fennmaradó lehetővé teszi a menteni az eredményeket védőeszközön parancsot (vagy egy védőeszközön parancs része).

- Gyűjtemény szűrése egy metódus szintaxis használatával mostantól támogatott. Ez azt jelenti, hogy most már szűrhet objektumok gyűjteménye Where() vagy a Where-Object, metódushívások formázva, amely hasonló egyszerűsített szintaxist használja. Az alábbiakban egy példa: (Get-Process) .where ({$_. Name - felel meg a "powershell"})

- A **Get-Process** parancsmagja rendelkezik egy új kapcsolóparaméter **IncludeUserName**.

- Egy új parancsmagot **Get-FileHash**, hogy a fájl kivonatát adja vissza az adott fájlhoz több formátumok egyikében, hozzá lett adva.

- A Windows PowerShell 4.0-s verzióját, ha egy modul használja a **DefaultCommandPrefix** kulcs a jegyzékben, vagy ha a felhasználó importálja a modult a a **előtag** paraméter, a **ExportedCommands**modul tulajdonság mutatja a parancsok a modul előtagot. A modulhoz minősített szintaxissal ModuleName a parancsok futtatásakor\\CommandName, a parancs nevének tartalmaznia kell az előtagot.

- Értékének **$PSVersionTable.PSVersion** 4.0 környezetébe.

- **WHERE()** operátor viselkedés megváltozott. `Collection.Where('property -match name')` a formátumú karakterlánc-kifejezés elfogadása `"Property -CompareOperator Value"` már nem támogatott. Azonban a **Where()** operátor elfogadja a scriptblock kulcsszót, formátumú karakterlánc-kifejezés; ez továbbra is támogatott.

### <a name="new-features-in-windows-powershell-integrated-scripting-environment-ise"></a>Új funkciók a Windows PowerShell integrált parancsfájlkezelési környezet (ISE)

- A Windows PowerShell ISE Windows PowerShell munkafolyamat hibakeresési és a távoli parancsprogram-hibakeresés is támogatja.

- IntelliSense már támogatja a Windows PowerShell célállapot-konfiguráció szolgáltatókat és konfigurációkat.

### <a name="new-features-in-windows-powershell-workflow"></a>Új szolgáltatások a Windows PowerShell munkafolyamat

- Már támogatja az új **PipelineVariable** általános paraméter iteratív folyamatok, például a környezetben a System Center Orchestrator által használt; Ez azt jelenti, hogy folyamatok, futtassa a parancsokat egyszerűen balról jobbra, nem pedig elszórtan elhelyezett streaming használatával.

- Paraméterkötés történő együttműködésre kívül lapon befejezési forgatókönyvek, például parancsok, amelyek nem szerepelnek az aktuális futási térben jelentősen bővült.

- Egyéni tároló tevékenységek már támogatja a Windows PowerShell munkafolyamat. Ha egy tevékenység paraméter típusok **tevékenység**, **tevékenység\[]**""vagy tevékenységek általános gyűjteménye "és a felhasználó mellékelt parancsprogram-blokkot, amelynek argumentuma, majd a Windows PowerShell-munkafolyamat XAML-kódot, a parancsprogram-blokkot tartalmazzon, mint a szokásos Windows PowerShell parancsfájl-munkafolyamat fordítási alakítja.

- Egy összeomlás utáni Windows PowerShell-munkafolyamat automatikusan újracsatlakozik a felügyelt csomópontok.

- Most már képes szabályozni **Foreach-Parallel** tevékenység utasítás használatával a **ThrottleLimit** tulajdonság.

- A **ErrorAction** általános paraméter új érvényes értékkel, rendelkezik **Suspend**, vagyis kizárólag a munkafolyamatok.

- Egy munkafolyamat-végpont mostantól automatikusan bezárása nincs aktív munkamenetek, nincsenek folyamatban lévő feladatok, és nincsenek folyamatban lévő feladatok esetén. Ez a szolgáltatás takarít meg az automatikus megszüntetésre feltételek teljesülésekor a munkafolyamat-kiszolgálóként működő számítógép erőforrásait.

### <a name="new-features-in-windows-powershell-web-services"></a>Új szolgáltatások a Windows PowerShell webszolgáltatások

- Ha hiba lép fel Windows PowerShell webszolgáltatások (PSWS, is nevezett felügyeleti OData IIS kiterjesztés), miközben a parancsmag fut, részletes üzeneteket a rendszer visszairányítja a hívó hiba. Ezenkívül, hajtsa végre a hibakódok [Windows Azure REST API hiba kód irányelvek](http://msdn.microsoft.com/library/windowsazure/dd179357.aspx).

- A végpont is most az API verzió megadása, valamint az adott API-verzió használatát kényszerítéséhez. Verzió eltérést ügyfél és kiszolgáló közötti fordulhat elő, amikor az ügyfél és a kiszolgáló is hibák jelennek meg.

- A küldő séma felügyeleti egyszerűsített automatikusan létrehozott összes hiányzó mezők értékének a sémában. Létrehozás következik be, kiindulópontként hasznos, még akkor is, ha a küldő séma nem létezik.

- Típus kezelése, PSWS típusokat, amelyek úgy viselkedik, mint az alapértelmezett konstruktort, mint más konstruktort támogatásához javult a **PSTypeConverter** a Windows PowerShellben. Ez lehetővé teszi összetett típusok használata PSWS.

- PSWS mostantól lehetővé teszi, hogy a társított példány bővíteni a lekérdezés futtatása közben. A nagyobb bináris tartalma (például képek, illetve hang- vagy videó) az átviteli költsége jelentős, és jobb megoldás, ha továbbítani szeretné a bináris adatok kódolás nem. PSWS megnevezett adatfolyamok átvitelére kódolás nélkül használja. A nevesített erőforrás adatfolyama egy tulajdonság az entitás a **Edm.Stream** típusa. Minden elnevezett forrásadatfolyam a GET vagy az UPDATE művelet külön URI tartozik.

- Az OData-műveletek most már a nem CRUD (létrehozási, olvasási, frissítési és törlési) módszerek erőforráson meghívása egy olyan mechanizmus biztosítása. Egy művelet meghívásához HTTP POST-kérelmet küld az URI, amely a művelet van definiálva. A művelet paramétereinek a POST kérelem törzse vannak definiálva.

- A Windows Azure irányelveket következetes legyen, az URL-címet egyszerűsíteni kell. A szereplő módosítása **kulccsal mint szegmens** lehetővé teszi, hogy egyetlen kulcsok szegmensként magát. Vegye figyelembe, hogy hivatkozásokat, amelyek több kulcsértéket a szükséges vesszővel elválasztott értékeket tartalmazó zárójeles jelöléssel, mint korábban.

- Ebben a kiadásban a PSWS, mielőtt a csak a kétirányú végrehajtásához létrehozási, frissítési vagy törlési műveletek volt meghívni a feladás egy vagy több, Put, vagy törli a legfelső szintű erőforrás. Új PSWS ebben a kiadásban található erőforrás-műveletek segítségével a felhasználók ugyanaz az eredmény elérése ugyanaz az erőforrás kevesebb közvetlenül közeledik, mintha csak az ezekkel az erőforrásokkal tartalmazott elérése közben.

### <a name="new-features-in-windows-powershell-web-access"></a>Új szolgáltatások a Windows PowerShell Web Access

- Megszakítja a kapcsolatot, és csatlakozzon újra a webes Windows PowerShell Web Access konzolon meglévő munkamenetek. A **mentése** a webalapú konzolon gomb lehetővé teszi, hogy a munkamenet leválasztása törlés nélkül, és újra csatlakozhat a munkamenethez egy másik időt.

- Alapértelmezett paraméterek is megjeleníthetők a bejelentkezési oldal. Alapértelmezett paramétereinek megjelenítéséhez konfigurálása az összes megjelenített beállítások értékét a **választható kapcsolati beállítások** a bejelentkezési oldal nevű fájlba területe **web.config**. Használhatja a **web.config** fájl kivételével a hitelesítő adatok egy második vagy egy másik készlet minden választható csatlakozási beállítások konfigurálása.

- A Windows Server 2012 R2 távolról kezelheti az engedélyezési szabályok Windows PowerShell Web Access. A **Add-PswaAuthorizationRule** és **Test-PswaAuthorizationRule** parancsmagokat tartalmaz egy Credential paramétert, amely lehetővé teszi a rendszergazdák felügyelhetik-az engedélyezési szabályok távoli számítógépről vagy a egy A Windows PowerShell Web Access-munkamenet.

- A egyetlen böngésző-munkamenet több Windows PowerShell Web Access-munkamenetekben minden munkamenet egy új böngészőlapon használatával most már rendelkezik. Már nincs szüksége a webes Windows PowerShell-konzolján egy új munkamenethez való csatlakozáshoz új böngésző-munkamenet megnyitásához.

### <a name="notable-bug-fixes-in-windows-powershell-40"></a>A Windows PowerShell 4.0 figyelmet a jelentősebb hibajavítások

- **Get-Counter** számlálókat tartalmaz egy aposztróf karaktert Windows francia kiadása most adhat vissza.

- Most már megtekintheti a **GetType** deszerializált objektum metódust.

- **#Requires** utasítások most megadásakor a felhasználók rendszergazdai hozzáférési jogosultságokat, ha szükséges.

- A **importálás Csv** parancsmag most figyelmen kívül hagyja az üres sorok.

- Ha a Windows PowerShell ISE használja-e túl sok memóriát futtatása során probléma egy **Invoke-WebRequest** parancs kijavítása.

- **Get-Module** mostantól megjeleníti a modul verziója egy **verzió** oszlop.

- Elem eltávolítása - Recurse most eltávolítja az elemet almappák várt módon.

- A **felhasználónév** tulajdonság hozzá lett adva **Get-Process** kimeneti objektumok.

- A **Invoke-RestMethod** parancsmag most az összes rendelkezésre álló eredményeket ad vissza.

- **Tag hozzáadása** most lép életbe, szórótáblában, még akkor is, ha a szórótáblában még nem nyitottak.

- **Select-Object - bontsa ki a** többé nem meghiúsul és kivételt állít elő, ha a tulajdonság értéke null vagy üres.

- **Get-Process** most már megadható a folyamat más parancsokkal, amelyek már a **számítógépnév** objektumok-tulajdonságot.

- **ConvertTo-Json** és **ConvertFrom-Json** most már fogadhat idézőjelek közé foglalt kifejezések, és a hibaüzenetek honosítható kerülnek.

- **Get-Job** most már bármelyik befejeződött az ütemezett feladatok, még akkor is, új munkamenetek beolvasása.

- Csatlakoztatása és leválasztása a virtuális merevlemezek használatával kapcsolatos problémák a **fájlrendszer** a Windows PowerShell 4.0-s szolgáltató határoztak meg. A Windows PowerShell mostantól képes észlelni az új meghajtók, ha ugyanabban a munkamenetben csatlakoztatva vannak.

- Már nincs szüksége tölthető be explicit módon **ScheduledJob** vagy **munkafolyamat** modulok a feladattípusok használata.

- Teljesítménnyel kapcsolatos fejlesztések időpont óta történtek az importálás munkafolyamatok, amelyek meghatározzák a beágyazott munkafolyamatok; a folyamat Ez a folyamat már gyorsabb.

## <a name="new-features-in-windows-powershell-30"></a>Új szolgáltatások a Windows PowerShell 3.0
A Windows PowerShell 3.0 a következő új szolgáltatásokat tartalmazza.

- [A Windows PowerShell munkafolyamat](#windows-powershell-workflow)
- [A Windows PowerShell Web Access](#windows-powershell-web-access)
- [Új Windows PowerShell ISE-szolgáltatások](#new-windows-powershell-ise-features)
- [A Microsoft .NET-keretrendszer 4.0-s támogatása](#support-for-microsoft-net-framework-4)
- [A Windows előtelepítési környezet támogatása](#support-for-windows-preinstallation-environment)
- [Leválasztott munkamenetek](#disconnected-sessions)
- [Robusztus munkamenet-kapcsolatot](#robust-session-connectivity)
- [Frissíthető Súgó](#updatable-help-system)
- [Továbbfejlesztett Online súgó](#enhanced-online-help)
- [A CIM-integráció](#cim-integration)
- [Munkamenet-konfigurációs fájlok](#session-configuration-files)
- [Ütemezett feladatok és a feladat ütemezési integráció](#scheduled-jobs-and-task-scheduler-integration)
- [A Windows PowerShell nyelvi fejlesztései](#windows-powershell-language-enhancements)
- [Új fő parancsmagjainak](#new-core-cmdlets)
- [Meglévő Core parancsmagok és szolgáltatók fejlesztései](#improvements-to-existing-core-cmdlets-and-providers)
- [Távoli modul importálását és felderítés](#remote-module-import-and-discovery)
- [Továbbfejlesztett kiegészítést](#enhanced-tab-completion)
- [Automatikus telepítési modulja](#module-auto-loading)
- [A modul élmény fejlesztései](#module-experience-improvements)
- [Egyszerűsített parancs felderítése](#simplified-command-discovery)
- [Továbbfejlesztett naplózás, a diagnosztikát és a csoport csoportházirend támogatás](#improved-logging-diagnostics-and-group-policy-support)
- [Formázás és a kimeneti fejlesztései](#formatting-and-output-improvements)
- [Továbbfejlesztett konzol állomás élmény](#enhanced-console-host-experience)
- [Új parancsmag és az API-k üzemeltetéséhez](#new-cmdlet-and-hosting-apis)
- [Teljesítménnyel kapcsolatos fejlesztések](#performance-improvements)
- [A futtató és a megosztott Host támogatás](#runas-and-shared-host-support)
- [Speciális karakterek kezelési fejlesztések](#special-character-handling-improvements)

### <a name="windows-powershell-workflow"></a>A Windows PowerShell munkafolyamat
A Windows PowerShell munkafolyamat immár a Windows Workflow Foundation Windows PowerShell. Munkafolyamatok írása XAML vagy a Windows PowerShell nyelven, és futtatni azokat, mint egy parancsmaghoz kell futtatni. A [Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) parancsmag lekéri workflw parancsok és a [Get-Help](https://technet.microsoft.com/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a) parancsmag lekéri a munkafolyamatok súgóját.

Munkafolyamatok, amelyek hosszú futású, ismételhető, gyakori, párhuzamosítható, megszakítható, suspendable és újraindítható folyamatok multicomputer felügyeleti tevékenységek sorozatát. A munkafolyamatok a szándékos vagy véletlen megzavarná, például egy hálózati kimaradás, a Windows újraindítása vagy áramkimaradás folytathatók.

Munkafolyamatok is hordozhatók; akkor exportálható vagy XAML-fájlok importálására. Egyéni munkamenet-konfigurációkat, amelyek lehetővé teszik a munkafolyamatok vagy tevékenységek alárendelt vagy delegált felhasználók által futtatandó munkafolyamat írhat.

Az alábbiakban a Windows PowerShell munkafolyamat előnyei

- Az előkészített, hosszú ideig futó feladatok automatizálását.

- **A hosszú ideig futó feladatok távoli megfigyelési**. Állapot és a tevékenységek előrehaladásának felülvizsgálatára bármikor jelennek meg.

- **Multicomputer kezelése.** Egyidejűleg futtatható tevékenységek munkafolyamatként száz felügyeleti csomóponton. A Windows PowerShell munkafolyamat tartalmaz egy beépített könyvtárat az általános felügyeleti paraméterek, például **PSComputerName**, amelyek lehetővé teszik több számítógép felügyeleti forgatókönyveket.

- **Egy feladat végrehajtása is kiterjedő összetett folyamatokig.** Kapcsolódó parancsfájlokat, amelyek megvalósítják az egy teljes forgatókönyvön végpont egyetlen munkamenetben kombinálhatja.

- **Adatmegőrzési.** : egy munkafolyamat mentett (vagy az ellenőrzés jelölt) megadott pontjain a szerző által megadott, így folytathatja a munkafolyamatot az utolsó megőrzött feladat (vagy ellenőrzőpont), a munkafolyamatot az elejétől újraindítása helyett.

- **A szolgáltatás megbízhatóságára.** Automatikus hibaelhárítás. A munkafolyamatok tervezett és nem tervezett újraindítások képesek túlélni. A munkafolyamat végrehajtásának felfüggesztése, és ezután úgy folytatódik, a munkafolyamatot az utolsó adatmegőrzési pontot. A munkafolyamat-szerzők jelölhet ki egy vagy több felügyelt csomóponton sikertelenség esetén újra futtatható meghatározott tevékenységek.

- **Bontását, csatlakozzon újra, és a leválasztott-munkamenetekben futtathatják.** Felhasználók csatlakozhatnak, és válassza le a munkafolyamat-kiszolgálón, de a munkafolyamat futtatása folyamatosan. Jelentkezzen ki az ügyfélszámítógép vagy az ügyfélszámítógép újraindítása, és a munkafolyamat-végrehajtási egy másik számítógépről megszakítása nélkül felügyelheti tovább a munkafolyamat.

- **Az ütemezés.** Munkafolyamat-feladatok ütemezése például a Windows PowerShell-parancsmag vagy parancsfájl.

- **Munkafolyamat és a kapcsolat szabályozás.** Munkafolyamat-végrehajtási és kapcsolatok használatát a csomópontok is lehet szabályozva, így a méretezhetőséget és magas rendelkezésre állású forgatókönyvek.

### <a name="windows-powershell-web-access"></a>Webes Windows PowerShell-elérés
A Windows PowerShell Web Access egy Windows Server 2012 szolgáltatás, amely lehetővé teszi a felhasználóknak egy webalapú konzol Windows PowerShell-parancsokat és parancsfájlok futtatását. A webalapú konzol eszközök a Windows PowerShell, a távoli felügyeleti szoftver vagy a böngésző beépülő modul telepítése nem szükséges. Szükséges egy megfelelően konfigurált Windows PowerShell Web Access-átjáró és egy eszköz ügyfélböngésző, amely támogatja a JavaScript és elfogadja a cookie-kat.

További információkért lásd: [központi telepítése Windows PowerShell Web Access](http://go.microsoft.com/fwlink/p/?LinkID=221050).

### <a name="new-windows-powershell-ise-features"></a>Új Windows PowerShell ISE-szolgáltatások
A Windows PowerShell 3.0, a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) van számos új funkciója, beleértve az IntelliSense megjelenítése-parancsablakot, egy egységesített konzolpanelen kódtöredékek, zárójel egyező, bontsa ki összecsukása szakaszok, az automatikus mentés, a legutóbbi elemek lista, gazdag másolása, blokk másolása és teljes támogatást nyújt a Windows PowerShell parancsfájl-munkafolyamatok írása. További információkért lásd: [about_Windows_PowerShell_ISE [v3]](https://technet.microsoft.com/library/dfa54d47-60c6-4fff-8197-c747e8d411bb).

### <a name="support-for-microsoft-net-framework-4"></a>A Microsoft .NET-keretrendszer 4 támogatása
A Windows PowerShell buildje a közös nyelvi futtatókörnyezet 4.0-s verzióját. Parancsmag, parancsfájl és a munkafolyamat-szerzők használhatja az új Microsoft .NET-keretrendszer 4-osztályok a Windows PowerShellben, szolgáltatásokkal, amely tartalmazza az alkalmazáskompatibilitás és a központi telepítés, bővítési keretrendszer felügyelt, párhuzamos számítási, hálózati, a Windows Kommunikációs alaprendszer és a Windows folyamatkövető alaprendszer.

### <a name="support-for-windows-preinstallation-environment"></a>A Windows előtelepítési környezet támogatása
A Windows PowerShell 3.0 része egy nem kötelező Windows előtelepítési környezet (Windows PE) 4.0-s verzióját a Windows 8 rendszerhez készült. A Windows PE egy olyan minimális méretű operációs rendszer, hogy egy számítógép, amely nincs operációs rendszer, és felkészíti a Windows-telepítési elindul. Windows PE partíció használható és merevlemez-meghajtók formázása, lemezképek másolja át egy számítógépre, és a Windows telepítő kezdeményezheti egy hálózati megosztáson. A Windows PowerShell 3.0 a Windows PE telepítési, diagnosztikai és helyreállítási forgatókönyvek kezeléséhez használhatja.

### <a name="disconnected-sessions"></a>Leválasztott munkamenetek
A Windows PowerShell 3.0 verziótól kezdve állandó felhasználó által felügyelt munkamenetek ("PSSession"), amely a New-PSSession parancsmag használatával hoz létre a rendszer menti a távoli számítógépen. Már nem függenek a létrehozásuk, amelyben a munkamenet.

Most már leválaszthatja a munkamenetből a parancsok futnak a munkamenet megszakítása nélkül. Zárja be a munkamenetét, és állítsa le a számítógépet. Később akkor csatlakozhat a munkamenet egy másik munkamenetben ugyanazon vagy egy másik számítógépre.

A **számítógépnév** paramétere a [Get-PSSession](https://technet.microsoft.com/library/b2b10531-d0df-4746-b877-e75c09955cb6) parancsmag most lekérdezi az összes kapcsolódni a számítógéphez, a felhasználói munkamenetek akkor is, ha azok egy másik munkamenetben egy másik számítógépre lett elindítva. A munkamenetek kapcsolódni, parancsok eredményeinek lekérése, indítsa el az új parancsokat, és majd a munkamenet leválasztása.

Új parancsmagokkal bővült a munkamenet leválasztása szolgáltatást támogató beleértve [Disconnect-PSSession](https://technet.microsoft.com/library/f8f95111-612f-4cba-9098-77904b0473d8), [Connect-PSSession](https://technet.microsoft.com/library/b803dd29-f208-4079-80d4-db04d778f060), és a fogadási-PSSession, és új paraméterek lettek hozzáadva parancsmag-készlettel PSSession, például kezelheti a **InDisconnectedSession** paramétere a [Invoke-Command](https://technet.microsoft.com/library/906b4b41-7da8-4330-9363-e7164e5e6970) parancsmag.

A munkamenet leválasztása támogatja csak akkor, ha a számítógépen is származó ("ügyfél"), és leállítja a kapcsolat vége ("kiszolgáló") fut a Windows PowerShell 3.0.

### <a name="robust-session-connectivity"></a>Robusztus munkamenet-kapcsolatot
A Windows PowerShell 3.0 az ügyfél és kiszolgáló közötti kapcsolat váratlan veszteségeinek észleli, és megpróbálja helyreállítani a kapcsolatot, és végrehajtása automatikusan folytatódik. Ha az ügyfél-kiszolgáló közötti kapcsolat nem kell építeni őket a megadott időn belül, a felhasználó értesítést kap, és a munkamenetét. Újracsatlakozás közben a Windows PowerShell folyamatos visszajelzést biztosítanak a felhasználó számára.

Ha a kapcsolat nélküli munkamenet indítása a InvokeCommand, a Windows PowerShell létrehoz egy feladatot az könnyebb csatlakozzon újra, és folytathatja a végrehajtási leválasztott munkamenethez.

Ezek a funkciók megbízhatóbb és helyreállítható távoli eljáráshívási környezetet biztosítson, és engedélyezése a felhasználók hatékony munkamenetek, például a munkafolyamatok igénylő hosszú ideig futó feladatok elvégzéséhez.

### <a name="updatable-help-system"></a>Frissíthető Súgó
A modulok a parancsmagokhoz tartozó frissített Súgó-fájlok is letölthető. A [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) parancsmag azonosítja a legújabb súgófájlokat, letölti azokat az internetről, kicsomagolja őket, érvényesíti azokat, és telepíti azokat a megfelelő nyelvspecifikus könyvtárban, a modul.

A frissített Súgó-fájlokat használja, csak gépelje `Get-Help`. Nem kell újraindítania a Windows vagy a Windows PowerShell használatával. A modulok a $pshome könyvtárban súgójának frissítéséhez indítsa el a Windows PowerShell a "Futtatás rendszergazdaként" lehetőséggel.

Felhasználók, akik nem rendelkeznek Internet-hozzáférés és a tűzfal mögött elhelyezkedő felhasználók, az új támogatásához [Save-Help](https://technet.microsoft.com/library/aed94f90-b73f-4e25-a25d-7c18d9f161fa) parancsmag tölti le a súgófájlokat, a rendszer könyvtárába, például fájlmegosztáson. Felhasználók ezután használhatja a [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) parancsmag frissített súgófájlok lekérése a fájlmegosztáshoz.

Használhatja a [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) parancsmaggal frissítsen Súgó fájlok összes vagy adott modult az összes támogatott felhasználói felület honosítása. Akkor helyezheti egy [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) parancsot a Windows PowerShell-profilt. Alapértelmezés szerint a Windows PowerShell fájlokat tölti le a súgó egy modul legfeljebb naponta egyszer.

Windows 8 és Windows Server 2012 modulok nem tartalmazzák a súgófájlok. Töltse le a legújabb súgófájlokat, írja be a következőt `Update-Help`. További információért gépelje be `Get-Help` (paraméterek) nélkül, vagy keresse meg [about_Updatable_Help](https://technet.microsoft.com/library/10bba75c-f4ac-4ca1-bbf3-8f34dd521ffe).

Ha a parancsmag súgóját nincsenek telepítve a számítógépen a [Get-Help](https://technet.microsoft.com/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a) parancsmag mostantól automatikusan létrehozott súgó jeleníti meg. Az automatikusan létrehozott súgó a parancs szintaxisát és használatára vonatkozó utasításokat tartalmaz a [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) parancsmag Súgó-fájlok letöltéséhez.

Bármely modul Szerző támogathatja a frissített súgó a modulhoz. A modul olyan súgófájlok, és használja a frissíthető súgó frissítheti vagy hagyja ki ezt a súgófájlokat, illetve frissített súgó telepítéséhez használja azokat. Frissített súgó támogatásával kapcsolatos további információkért lásd: [frissíthető súgó támogatása](http://go.microsoft.com/FWLink/?LinkID=242129) az MSDN Webhelyén.

### <a name="enhanced-online-help"></a>Továbbfejlesztett Online súgó
A Windows PowerShell súgójában forrás az összes felhasználó számára, de különösen fontos, hogy a felhasználók, akik nem vagy frissített Súgó fájlokat nem lehet telepíteni.

A Windows PowerShell-parancsmag online súgójának megjelenítéséhez írja be:

```
Get-Help <cmdlet-name> -Online
```

A Windows PowerShell a Súgó-témakör online verzióját az alapértelmezett böngészőben nyílik meg.

A **Get-Help-Online** Windows PowerShell 3.0 szolgáltatásának még sokkal hatékonyabb miatt csak akkor működik, még ha a parancsmag súgóját nincsenek telepítve a számítógépen. A **Get-Help-Online** szolgáltatás URI-JÁNAK online súgó-témakörhöz lekérése parancsmagok és a speciális funkciók HelpUri tulajdonságát.

```
PS C:\>(Get-Command Get-ScheduledJob).HelpUri
http://go.microsoft.com/fwlink/?LinkID=223923
```

A Windows PowerShell 3.0 verziótól kezdve a C#-parancsmagok szerzők feltöltheti a **HelpUri** tulajdonság hozzon létre egy **HelpUri** a parancsmag osztály attribútuma. Speciális funkciók szerzők definiálhat egy **HelpUri** tulajdonságát a **CmdletBinding** attribútum. Értékét a **HelpUri** tulajdonság "http" vagy "https" kell kezdődnie.

Is hozzáadhat egy **HelpUri** érték egy XML-alapú parancsmag Súgó-fájl első kapcsolódó hivatkozás vagy a. Hivatkozás irányelv Megjegyzés-alapú súgó a függvényben.

További információ az online súgó támogatása: [Online súgó támogatása](http://go.microsoft.com/fwlink/?LinkId=242132) az MSDN Webhelyén.

### <a name="cim-integration"></a>A CIM-integráció
A Windows PowerShell 3.0 magában foglalja a a Common Information Model (CIM), biztosító közös definíciók felügyeleti információk rendszerek, hálózatok, alkalmazások és szolgáltatások, így azokat a felügyeleti közötti információcsere heterogén rendszerek. Parancsmag definíciójának XML-fájlok, támogatja a .NET-keretrendszer CIM alapján a Windows PowerShell 3.0, beleértve a Windows PowerShell-parancsmagok új vagy meglévő CIM osztályok, parancsok alapján készítésének képessége CIM támogatása. API-t, a CIM parancsmagokat és WMI 2.0-s szolgáltatók.

### <a name="session-configuration-files"></a>Munkamenet-konfigurációs fájlok
A Windows PowerShell 3.0 verziótól kezdve tervezhet egy egyéni munkamenet-konfiguráció fájl használatával. Az új munkamenet-konfigurációs fájl segítségével meghatározhatja, hogy a munkamenetek, amelyek a munkamenet-konfigurációt, mely modulokat, parancsfájlok, beleértve a környezet és formátumú fájlok töltődnek be a munkameneteket, mely parancsmagok és a nyelvi elemei felhasználók használhatják, melyik modulokat és mely változókat láthatják, és parancsprogramok is futtathatók.

Megtervezheti, amelyben felhasználók csak futtatni tudják a parancsmagok egy adott modulból munkamenet, vagy egy munkamenet, amelyben a felhasználók rendelkeznek teljes nyelvi összes modult a hozzáférést és speciális feladatokat elvégző parancsprogramok a hozzáférést.

Korábbi verzióiban a Windows PowerShell ezen a szinten vezérlő volt elérhető csak azok, akik egy C# programban vagy összetett indítási parancsfájl volt-e írási. Most bármely a számítógépen a Rendszergazdák csoport tagja, a munkamenet-konfiguráció a konfigurációs fájl segítségével szabhatja.

Egy munkamenet-konfigurációs fájl létrehozásához használja a [New-PSSessionConfigurationFile](https://technet.microsoft.com/library/5f3e3633-6e90-479c-aea9-ba45a1954866) parancsmag. A munkamenet-konfigurációs fájl egy munkamenet-konfigurációjához segítségével a [Register-PSSessionConfiguration](https://technet.microsoft.com/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) vagy [Set-PSSessionConfiguration](https://technet.microsoft.com/library/b21fbad3-1759-4260-b206-dcb8431cd6ea) parancsmagok.

További információkért lásd: [about_Session_Configuration_Files](https://technet.microsoft.com/library/c7217447-1ebf-477b-a8ef-4dbe9a1473b8) és [New-PSSessionConfigurationFile](https://technet.microsoft.com/library/5f3e3633-6e90-479c-aea9-ba45a1954866).

### <a name="scheduled-jobs-and-task-scheduler-integration"></a>Ütemezett feladatok és a feladat ütemezési integráció
Mostantól a Windows PowerShell háttér feladatok ütemezése és kezelheti azokat a Windows PowerShell és a Feladatütemező.

A Windows PowerShell ütemezett feladatok olyan hasznos hibrid feladatok a háttérben Windows PowerShell és a Feladatütemező feladatait.

Például a Windows PowerShell feladatok a háttérben, ütemezett feladatok aszinkron módon történik a háttérben futnak. A feladat parancsmagok használatával kezelheti ütemezett feladatokat elvégző példányai [indítási-feladat](https://technet.microsoft.com/library/2bc04935-0deb-4ec0-b856-d7290cca6442) és [Get-Job](https://technet.microsoft.com/library/1352c534-7193-46ca-9ab1-0c5219a661ad).

Például a Feladatütemező feladatait ütemezett feladatok egyszeri vagy ismétlődő ütemezés szerint, vagy művelet vagy esemény válaszul is futtathatja. Megtekintése és kezelése az ütemezett feladatok a Feladatütemezőben, engedélyezése és letiltása őket, igény szerint futtatni azokat vagy sablonként használhatja őket, és állítsa be a feltételeket, amelyek alapján a feladatok megkezdése.

Ütemezett feladatok továbbá azok kezelésére szolgáló parancsmagok csoportjának nyomtatásához rendelkeznek. A parancsmag lehetővé teszi a létrehozása, szerkesztése, kezelése, tiltsa le, és engedélyezze újra az ütemezett feladatok, ütemezett feladat eseményindítók létrehozása és ütemezett feladat beállítások megadása.

Ütemezett feladatok kapcsolatos további információkért lásd: [about_Scheduled_Jobs](https://technet.microsoft.com/library/3b546629-703c-4939-b44f-52dd567bce92).

### <a name="windows-powershell-language-enhancements"></a>A Windows PowerShell nyelvi fejlesztései
A Windows PowerShell 3.0 szolgáltatásai számos nyújtanak a nyelvi egyszerűbb és könnyebben használatára, és a gyakori hibák elkerülése érdekében. A fejlesztések közé tartoznak a tulajdonság számbavételi, count és adott hosszúságú tulajdonságok skaláris objektumok, új átirányító operátorok, a $Using hatókör-módosító, PSItem automatikus változó, rugalmas parancsfájl formázás, változókat, egyszerűsített attribútum attribútumai argumentumok, numerikus parancs nevét, a Stop-elemzés operátort, nagyobb a tömb a felosztás, új bit operátorok, rendezett szótárak, PSCustomObject adattípusokról és továbbfejlesztett Megjegyzés-alapú súgó.

### <a name="new-core-cmdlets"></a>Új fő parancsmagjainak
Új parancsmagok a Windows PowerShell Core, beleértve az ütemezett feladatok, kapcsolat nélküli munkamenetek, CIM-integráció és az frissíthető Súgó rendszer kezeléséhez parancsmagok hozzáadott.

|||
|-|-|
|-JobTrigger|Új-JobTrigger|
|Connect-PSSession|Új PSSessionConfigurationFile|
|ConvertFrom-Json|New-PSTransportOption|
|ConvertTo-Json|Új PSWorkflowExecutionOption|
|Disable-JobTrigger|Új PSWorkflowSession|
|Disable-ScheduledJob|Új ScheduledJobOption|
|Kapcsolat bontása-PSSession|Új WinEvent|
|Enable-JobTrigger|Fogadási-PSSession|
|Enable-ScheduledJob|Register-CimIndicationEvent|
|Get-CimAssociatedInstance|Register-ScheduledJob|
|Get-CimClass|Remove-CimInstance|
|Get-CimInstance|Remove-CimSession|
|Get-CimSession|Remove-TypeData|
|Get-ControlPanelItem|Számítógép átnevezése|
|Get-IseSnippet|RESUME-Job|
|Get-JobTrigger|Save-Help|
|Get-ScheduledJob|Set-CimInstance|
|Get-ScheduledJobOption|Set-JobTrigger|
|Get-TypeData|Set-ScheduledJob|
|Importálás – IseSnippet|Set-ScheduledJobOption|
|Invoke-AsWorkflow|A parancs megjelenítése|
|Invoke-CimMethod|Megjelenítése-ControlPanelItem|
|Invoke-RestMethod|Suspend-Job|
|Invoke-WebRequest|Teszt-PSSessionConfigurationFile|
|Új CimInstance|Fájl feloldása|
|Új-CimSession|Unregister-ScheduledJob|
|Új CimSessionOption|Update-Help|
|Új IseSnippet||

### <a name="improvements-to-existing-core-cmdlets-and-providers"></a>Meglévő Core parancsmagok és szolgáltatók fejlesztései
Windows PowerShell 3.0 meglévő parancsmagok, beleértve a egyszerűsített szintaxist használhat, és a következő parancsmag új paramétereinek új szolgáltatásokat tartalmazza: számítógép-parancsmagjai, a CSV-parancsmag, a Get-ChildItem, Get-Command, a Get-tartalmat, Get-előzmények Mértékobjektumot, biztonsági parancsmagok, Select-Object, válasszon-karakterlánc, megosztott elérési útja, folyamat, Tee-objektum, a Test-Connection, Add-tag, és a WMI-parancsmagokat.

A Windows PowerShell-szolgáltatókat is kifejlesztett jelentősen, többek között a tanúsítvány által támogatott szolgáltatók a webalkalmazás üzemeltetéséhez Secure Socket Layer (SSL) tanúsítványok kezeléséhez, támogatja a hitelesítő adatok, hálózati meghajtók és az alternatív adatfolyamok fájlrendszer meghajtók.

### <a name="remote-module-import-and-discovery"></a>Távoli modul importálását és felderítés
Windows PowerShell 3.0 kiterjeszti a felderítési modul importálása és implicit távoli eljáráshívási szolgáltatása a távoli számítógépek. A modul parancsmagjai modulok lekérni a távoli számítógépeken, és a modulok importálása a helyi vagy távoli számítógépen a Windows PowerShell távoli eljáráshívás segítségével. Új CIM munkamenet támogatása lehetővé teszi a CIM és a WMI használatát parancsok importálja a helyi számítógépen, amely implicit módon a távoli számítógépen futó-Windows számítógépek felügyeletére.

További információkért tekintse meg a Súgó-témaköröket a [Get-Module](https://technet.microsoft.com/library/2cccd4c4-9a21-4c77-b691-984ee57242e1) és [Import-Module](https://technet.microsoft.com/library/af616c24-e122-4098-930e-1e3ea2080ade) parancsmagok.

### <a name="enhanced-tab-completion"></a>Továbbfejlesztett kiegészítést
Kiegészítés a Windows PowerShell-konzolban most befejeződött parancsmagok, paraméterek, paraméterértékeket, enumerálások, .NET-keretrendszert típusok, COM objektumok, rejtett könyvtár, és több. A lap kiegészítési funkció teljesen van írni egy új elemzési és további forgatókönyvek, köztük a memórián belüli elemzési fák és középvonal kiegészítést támogatásához absztrakt szintaxis fa alapján.

### <a name="module-auto-loading"></a>Automatikus telepítési modulja
A [Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) parancsmag most lekérése az összes parancsmag és funkció a számítógépen telepített összes modul még akkor is, ha a modul nem importálta az aktuális munkamenet.

Amikor a parancsmag, amelyekre szüksége van, használhatja azonnal modul importálása nélkül. Windows PowerShell-modulok importálása mostantól automatikusan bármely parancsmag használatakor a modulban. Már nincs szüksége a modul keresheti ki és importálja azt a parancsmagok használatával.

Modulok automatikus importálása akkor váltódik ki, a parancsmag használatával a parancsban futó **Get-Command** nem helyettesítő karaktereket, illetve fut a parancsmag [Get-Help](https://technet.microsoft.com/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a) parancsmag helyettesítő karakterek nélkül.

Engedélyezése, letiltása, és automatikus importálása modulja segítségével konfigurálhatja a **$PSModuleAutoLoadingPreference** preferenciaváltozót.

További információkért lásd: [felügyelhető [v4]](https://technet.microsoft.com/library/94f57429-a539-4aee-bb0d-205cd7e801f9), [about_Preference_Variables [v4]](https://technet.microsoft.com/library/31344314-be29-4286-b039-afa5460cbe8b), és a Súgó-témaköröket a [Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) és [Import-Module ](https://technet.microsoft.com/library/af616c24-e122-4098-930e-1e3ea2080ade) parancsmagok.

### <a name="module-experience-improvements"></a>A modul élmény fejlesztései
Windows PowerShell 3.0 biztosítható a speciális szolgáltatások támogatásáról az modulok, többek között az alábbi új szolgáltatásokkal.

1. Az egyéni modulok (LogPipelineExecutionDetails) modul naplózásának és az új "A modul-naplózás a" csoportházirend-beállítás

2. Bővített teszi közzé a moduljegyzékben értékeinek modul objektumok

3. Új **ExportedCommands** tulajdonság modulokat, beleértve a beágyazott modulok, parancsok, bármilyen típusú kombináló

4. Továbbfejlesztett felderítése érhető el (nem importált) modult, beleértve, amely lehetővé teszi a **elérési** és **ListAvailable** ugyanaz a parancs paramétereit

5. Új **DefaultCommandPrefix** kulcs modul jegyzékfájlokban, amellyel elkerülhető a névütközések modul programkód módosítása nélkül.

6. Továbbfejlesztett modul követelményeket, ideértve a teljesen minősített szükséges modulokat a verziót és a GUID Azonosítót és a szükséges modulokat automatikus importálása

7. Csendesebb, zökkenőmentes működését a [New-ModuleManifest](https://technet.microsoft.com/library/512adced-f42f-4e88-ba7c-834fc9e5d047) parancsmag.

8. Új **modul** a(z) #Requires

9. Továbbfejlesztett [Import-Module](https://technet.microsoft.com/library/af616c24-e122-4098-930e-1e3ea2080ade) mindkét parancsmag **MinimumVersion** és **RequiredVersion** paraméterek.

### <a name="simplified-command-discovery"></a>Egyszerűsített parancs felderítése
Már nem szeretné felderíteni a parancsok a munkamenet számára elérhető összes modul importálása. A Windows PowerShell 3.0 a [Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) parancsmag minden parancs lekéri az összes telepített modulokban. És a paranccsal, ha a modul, a parancs által automatikusan importálja a munkamenetbe.

Az új [megjelenítése-parancs](https://technet.microsoft.com/library/65bba50b-91a8-49d5-80a2-a30fc684ba41) parancsmag kifejezetten a kezdők tervezték. Kereshet egy ablakban parancsokat. Minden parancs megtekintése vagy modul szűrés, modul importálása a gombra kattintva, szöveg- és legördülő listák segítségével hozható létre egy érvényes parancsot, és másolja, vagy futtassa a parancsot az ablak alkalmazáson.

### <a name="improved-logging-diagnostics-and-group-policy-support"></a>Továbbfejlesztett naplózás, a diagnosztikát és a csoport csoportházirend támogatás
Windows PowerShell 3.0 fokozza a naplózás és a nyomkövetési esemény-nyomkövetés Windows (ETW)-naplókban, egy szerkeszthető támogatása a parancsok és a modulok támogatását **LogPipelineExecutionDetails** modulok, és a "kapcsolja be a modul tulajdonsága Naplózás"csoport házirend-beállítást. Most már letölthető paraméterértékek napló részleteit a napló tulajdonságainak megjelenítésével jelzi ezt.

### <a name="formatting-and-output-improvements"></a>Formázás és a kimeneti fejlesztései
Új formázás és a kimeneti fejlesztései javítsa a Windows PowerShell az összes felhasználót. A fejlesztések közé tartoznak a kimenet átirányítása adatfolyamok összes, egy továbbfejlesztett Frissítéstípus parancsmag, amely dinamikusan Format.ps1xml fájlok, a kimenetben hosszú sorok tördelése nélküli típusok alapértelmezett egyéni objektumok formázási tulajdonságait a **PSCustomObject** szöveg, továbbfejlesztett WMI-objektumok és a heterogén objektumok és a támogatás metódus túlterhelések felderítéséhez formázás.

### <a name="enhanced-console-host-experience"></a>Továbbfejlesztett konzol állomás élmény
A Windows PowerShell-konzol gazdagép program Windows PowerShell 3.0 többek között az egyszálas apartmanszálaknak alapértelmezés szerint az új szolgáltatásokkal rendelkezik. Az új "Futtatás a PowerShell" lehetőséget a Fájlkezelőben lehetővé teszi a korlátozás nélküli munkamenet található parancsfájlok futtatásának csak kattint. Új konzol állomás indítási logika elindítja a Windows PowerShell gyorsabban, és új betűtípusok lehetővé teszik a megszokott konzol ablakának élmény személyre.

További információkért lásd: [about_Run_With_PowerShell](https://technet.microsoft.com/library/c9d9ca5f-eff9-4409-be9d-e43b5b4087eb).

### <a name="new-cmdlet-and-hosting-apis"></a>Új parancsmag és az API-k üzemeltetéséhez
Az új parancsmag API és üzemeltetési API tartalmazza a nyilvános speciális szintaktikai fa (AST-t) API-k és API-k csővezeték lapozás, beágyazott folyamatok, futási térben készletek kiegészítést, Windows RT, a elavult parancsmag attribútum és művelet és főnév FunctionInfo objektum tulajdonságainak.

### <a name="performance-improvements"></a>Teljesítménnyel kapcsolatos fejlesztések
Az új nyelvi elemző, a dinamikus futásidejű nyelvi (DLR) a .NET-keretrendszer 4 beépített származhat jelentős teljesítménybeli fejlesztések a Windows PowerShellben., futásidejű parancsfájl összeállítása, motor-megbízhatóság fejlesztései és módosításainak együtt a az algoritmus a [Get-ChildItem](https://technet.microsoft.com/library/75cf79bb-4db6-4a67-8c36-3d20754e2190) , hogy a teljesítmény javítása érdekében különösen akkor, ha a Keresés a hálózati megosztások.

### <a name="runas-and-shared-host-support"></a>A futtató és a megosztott Host támogatás
A Windows PowerShell 3.0 futtató és a gazdagép megosztott szolgáltatások támogatását is magában foglalja.

A *RunAs* készült Windows PowerShell munkafolyamat, a szolgáltatás lehetővé teszi, hogy a felhasználók egy munkamenet-konfiguráció egy megosztott felhasználói fiók engedéllyel rendelkező futó munkameneteket hozzon létre. Ez lehetővé teszi az adott parancsok és parancsfájlok futtatásához rendszergazdai jogosultságokkal rendelkező korlátozott engedélyekkel rendelkező felhasználók, és csökkenti a kevésbé tapasztalt felhasználóknak rendszergazdák csoportba való felvételekor szükség.

A **SharedHost** funkció lehetővé teszi, hogy a több felhasználó több számítógépen egyszerre egy munkafolyamat-munkamenet és a munkafolyamat előrehaladásának figyeléséhez. A felhasználók elindítsanak egy munkafolyamatot egy számítógépen, és csatlakozzon a munkafolyamat-munkamenetet egy másik számítógépen a munkamenet leválasztása az eredeti számítógép nélkül. A felhasználók ugyanazokkal az engedélyekkel kell rendelkeznie, és ugyanazt a munkamenet-konfigurációt használja. További információkért lásd: "Fut egy Windows PowerShell Workflow" első lépések a Windows PowerShell munkafolyamat.

### <a name="special-character-handling-improvements"></a>Speciális karakterek kezelési fejlesztések
A lehetőségét, a Windows PowerShell 3.0 értelmezi, és megfelelően kezeli a különleges karaktereket javításához a **LiteralPath** paraméter, amely kezeli a különleges karakterek az elérési utak, kulcsszó használható, amelyek szinte minden parancsmagok egy  **Elérési út** paramétert, beleértve az új [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) és [Save-Help](https://technet.microsoft.com/library/aed94f90-b73f-4e25-a25d-7c18d9f161fa) parancsmagok. Az elemző is magában foglalja a backtick karakter kezelésének javítása érdekében speciális logikát (\`) és a fájl neve és elérési utak szögletes zárójelben.

## <a name="see-also"></a>Lásd még:
- [about_Windows_PowerShell_5.0](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_windows_powershell_5.0?view=powershell-5.0)
- [A Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=107116)