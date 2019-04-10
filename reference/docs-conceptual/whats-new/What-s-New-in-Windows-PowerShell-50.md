---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Windows PowerShell 5.0 újdonságai
ms.openlocfilehash: b2cb729948d4b53c5ea9a536dbeda04c7cb50997
ms.sourcegitcommit: 9194e603ac242ae733839eb773e4af7360fdd044
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59363530"
---
# <a name="whats-new-in-windows-powershell-50"></a>Windows PowerShell 5.0 újdonságai

Windows PowerShell 5.0 jelentős új szolgáltatásokat tartalmaz, amelyek kibővítik annak használati, javítják használhatóságát, és szabályozhatja, és kezelheti a Windows-alapú környezetek egyszerűbb és.

Windows PowerShell 5.0 visszamenőlegesen kompatibilis. Parancsmagok, szolgáltatók, modulok, beépülő modulok, parancsfájlok, funkciók és a Windows PowerShell 4.0-s verzióját, a Windows PowerShell 3.0 és a Windows PowerShell 2.0 általában tervezett profilok működik a Windows PowerShell 5.0 módosítása nélkül.

## <a name="installing-windows-powershell"></a>A Windows PowerShell telepítése

A Windows Server 2016 Technical Preview és a Windows 10 rendszeren alapértelmezés szerint telepítve van a Windows PowerShell 5.0-s.

A Windows Server 2012 R2, Windows 8.1 Enterprise vagy Windows 8.1 Pro Windows PowerShell 5.0 telepítéséhez töltse le és telepítse [Windows Management Framework 5.0](https://aka.ms/wmf5download). Mindenképpen olvassa el a letöltési részleteit, és rendszerkövetelményeknek összes, Windows Management Framework 5.0 telepítése előtt.

## <a name="in-this-topic"></a>A témakör tartalma

- [A KB 3000850 Windows PowerShell 4.0-s DSC-frissítések](#windows-powershell-40-updates-in-november-2014-update-rollup-kb-3000850)
- [Windows PowerShell 5.0 újdonságai](#new-features-in-windows-powershell-50)
- [Új szolgáltatások a Windows PowerShell 4.0](#new-features-in-windows-powershell-40)
- [Új szolgáltatások a Windows PowerShell 3.0](#new-features-in-windows-powershell-30)

## <a name="windows-powershell-40-updates-in-november-2014-update-rollup-kb-3000850"></a>Windows PowerShell 4.0-frissítések a 2014. novemberi kumulatív (KB 3000850)

Számos frissítéseket és fejlesztéseket a Windows PowerShell Desired State Configuration (DSC) a Windows PowerShell 4.0-s érhetők el a [2014. novemberi kumulatív frissítés a Windows RT 8.1, Windows 8.1 és Windows Server 2012 R2](https://support.microsoft.com/kb/3000850/) (KB 3000850 ). Megadhatja, hogy ha a KB 3000850 telepítve van a rendszeren futtatásával `Get-Hotfix -Id KB3000850` a Windows PowerShellben.

- Meglévő parancsmagok a frissítések a [PSDesiredStateConfiguration](https://technet.microsoft.com/library/dn391651(v=wps.640).aspx) modul
  - [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) gyorsabb (különösen az ISE-ben).
  - [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) olyan új paraméter - UseExisting, amely az utoljára alkalmazott konfiguráció újra alkalmazza.
  - [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) -Force megoldották a problémát.
  - [Get-DscLocalConfigurationManager](https://technet.microsoft.com/library/dn407378.aspx) motor állapotával kapcsolatos további hasznos információkat jelenít meg.
  - [A test-DscConfiguration](https://technet.microsoft.com/library/dn407382.aspx) mostantól az a számítógép nevét, és IGAZ vagy hamis értéket ad vissza.
  - [Új DscChecksum](https://technet.microsoft.com/library/dn521622.aspx) mostantól támogatja az UNC elérési útvonalat.

- Az új parancsmagok a [PSDesiredStateConfiguration](https://technet.microsoft.com/library/dn391651(v=wps.640).aspx) modul
  - [Update-DscConfiguration](https://technet.microsoft.com/library/mt143541(v=wps.630).aspx):  Egy igény szerinti lekérése kiszolgáló ellenőrzést végez.
  - [STOP-DscConfiguration](https://technet.microsoft.com/library/mt143542(v=wps.630).aspx):  Már fut egy konfigurációját leáll.
  - [Remove-DscConfigurationDocument](https://technet.microsoft.com/library/mt143544(v=wps.630).aspx):  Lehetővé teszi a különböző fázisaival (folyamatban, jelenlegi vagy korábbi) konfiguráció-dokumentumok eltávolítása.

- Nyelvi fejlesztések
  - DependsOn mostantól támogatja az összetett erőforrások.
  - DependsOn számok mostantól támogatja az erőforrás-példány nevét.
  - Csomópont-kifejezések, amelyek kiértékelik a üres már nem throw hibákat.
  - Megoldottuk a hiba akkor jelentkezik, ha egy csomópont kifejezés értéke üres.
  - A konfigurációk konfigurációk most munkahelyi hívja meg a Windows PowerShell-konzolon.

- Lekérési mód fejlesztései
  - Lekérési mód mostantól támogatja az összes ZIP-fájlt.
  - **AllowModuleOverwrite** most már megfelelően működik-e.

- Rugalmasság fejlesztései
  - Új **DebugMode** töltse be újra az erőforrás-modulok teszi lehetővé.
  - Konfigurációs hiba történik, ha a pending.mof fájl nem törlődik.
  - A helyi Configuration Manager (LCM) Konfigurálása már rugalmasabb, amikor metaconfiguration beállításait, hogy megsérült.

- Diagnosztikai továbbfejlesztései
  - A figyelmeztetés akkor jelenik meg, amikor az LCM állítja be az időzítő különböző beállításokkal, mint a megadott.
  - Hiba történt a naplófájlok mostantól tartalmazza a Windows PowerShell-erőforrásokat a hívási veremben.

- Rugalmassággal kapcsolatos fejlesztések
  - A LocalConfigurationManager erőforrás rendelkezik egy új tulajdonság **ActionAfterReboot**.
    - ContinueConfiguration (alapértelmezett érték): A konfiguráció automatikusan folytatja a cél csomópont újraindítása után.
    - StopConfiguration: Nem automatikusan folytatja a konfiguráció egy csomópont újraindítását követően.
  - Konzisztencia Futtatás most fordulhat elő többször a PULL művelet, vagy fordítva.
  - Verziószámozás támogatása:  DSC mostantól képes felismerni egy dokumentumot létrehozott egy újabb ügyfél (mellékelt [WMF 5.0](https://aka.ms/wmf5download)).

- Hiba történt a megelőzési fejlesztései
  - Modulverzió kényszerítése megtörtént a konfiguráció alkalmazása előtt.
  - **DebugPreference** most már megfelelően vannak beállítva az Get-, Set- vagy a Test-TargetResource hívások.

- Hitelesítő adatok kezelése fejlesztései
  - A tanúsítvány már használja, ha mindkét **tanúsítvány** és **PSDscAllowPlainTextPassword** vannak megadva.
  - Hitelesítő adatok lesznek visszafejtve, még a Get-TargetResource.
  - Metaconfiguration hitelesítő adatok titkosítása és visszafejtése.
  - PSCredentials most lesznek visszafejtve, amelyek a beágyazott objektum.

- Beépített erőforrás fejlesztései
  - A Package erőforrás
    - Már nem telepíti a megfelelő (helyi eszközből vagy webes források).
    - Most már támogatja a HTTPS.
  - Mostantól támogatott a HTTPS-hez a [erőforrás csomag](https://technet.microsoft.com/library/dn282132.aspx).
  - [Archív erőforrás](https://technet.microsoft.com/library/dn249917.aspx) mostantól támogatja a hitelesítő adatokat.

## <a name="new-features-in-windows-powershell-50"></a>Windows PowerShell 5.0 újdonságai

- [Új szolgáltatások a Windows PowerShellben](#new-features-in-windows-powershell)
- [Új szolgáltatások a Windows PowerShell Desired State Configuration](#new-features-in-windows-powershell-desired-state-configuration)
- [Új szolgáltatások a Windows PowerShell ISE-ben](#new-features-in-windows-powershell-ise)
- [Új szolgáltatások a Windows PowerShell webszolgáltatások](#new-features-in-windows-powershell-web-services-management-odata-iis-extension)
- [A Windows PowerShell 5.0 jelentős hibajavítások](#notable-bug-fixes-in-windows-powershell-50)

### <a name="new-features-in-windows-powershell"></a>Új szolgáltatások a Windows PowerShellben

- A Windows PowerShell 5.0-től kezdődően is fejleszthet osztályokkal formális szintaxist és a hasonló más objektumorientált programozási nyelveket szemantika használatával. **Osztály**, **Enum**, és más kulcsszavak lettek hozzáadva a Windows PowerShell nyelv támogatásához az új funkció. Osztályok kezelésével kapcsolatos további információkért lásd: about_Classes.

- Windows PowerShell 5.0 mutatja be egy új, strukturált információfolyam, amely strukturált adatok között egy parancsfájlt a hívó (vagy egy üzemeltetési környezet) használatával. Mostantól használhatja Write-Host kibocsátható a információfolyam kimenetet. Információk streameket is PowerShell.Streams, feladatok, az ütemezett feladatok és a munkafolyamatok esetében működik. A következő funkciók az adatokat a stream támogatja.
  - Új írási-információk parancsmag, amellyel megadhatja, hogy miként kezeli az Windows PowerShell a információk adatok streamelése a parancshoz. Write-Host egy burkoló írási-információkat. Írási-információkat is egy támogatott munkafolyamat-tevékenységet.
  - Két új általános tevékenységparaméterekkel, InformationVariable és InformationAction, segítségével meghatározhatja, hogyan jelennek meg információk adatfolyamok egy parancs. InformationAction érvényes értékei a következők: Folytatáscsendben, Leállítás, folytatás, Inquire, figyelmen kívül hagyása vagy felfüggesztése folyamatban van az alapértelmezett Folytatáscsendben együtt. InformationVariable egy karakterlánc, amely egy mentett parancs Write-Host adatait kívánja a változó nevét adja meg.
  - Egy új preferenciaváltozó, InformationPreference, információ-adatok streamelése az alapértelmezett beállításait a Windows PowerShell-munkamenetben adja meg. Az alapértelmezett érték: Folytatáscsendben.
  - Két új munkafolyamat általános paramétereit, PSInformation és InformationAction, lettek hozzáadva.
  - A Format-Table parancs használatakor a táblázat oszlopaihoz automatikusan formázása mostantól az adatok, amely áthalad a stream első 300ms kiértékelése.

- Együttműködve [a Microsoft Research](https://research.microsoft.com/), egy új parancsmag, ConvertFrom-karakterlánc, hozzá van adva. ConvertFrom-karakterlánc lehetővé teszi a szöveges karakterláncok tartalmának strukturált objektumok kibontása és elemzése. További információkért lásd: ConvertFrom-karakterlánc.
- Új parancsmag Convert-karakterlánc automatikusan formázza a szöveget egy példa, amely egy – példa a paraméter meg alapján.
- Microsoft.PowerShell.Archive, új modul, amelyek lehetővé teszik, hogy a fájlok tömörítése-parancsmagokat tartalmaz, és az archív (más néven ZIP) fájlok, mappák, bontsa ki a fájlokat a ZIP-fájlokat, és frissítse ZIP-fájlokat rajtuk tömörített fájl újabb verzióját.
- Új modul PackageManagement, lehetővé teszi és szoftvercsomagok telepítése az interneten. A PackageManagement (korábbi nevén OneGet) modul manager vagy a meglévő csomagkezelők (más néven csomag szolgáltatók) multiplexer az használja őket egységes előtérrendszerként Windows csomagkezelés egyetlen Windows PowerShell felületet.
- Egy új, a PowerShellGet modul lehetővé teszi, hogy keresse meg, telepítse, közzététele és frissítése modulok és a DSC-erőforrások a [PowerShell-galériából](https://www.powershellgallery.com/), vagy a belső modulban tárházból a Register-PSRepository parancsmag futtatásával beállíthatja.
- Egy új kulcsszava, **Hidden**, adja meg, hogy a tag (egy tulajdonságot vagy metódus) nem jelenik meg alapértelmezés szerint a Get-Member eredmények bővült (, amíg a - Force paraméterrel). Tulajdonságaival és metódusaival jelölt rejtett is nem jelennek meg az IntelliSense eredmények között, kivéve ha biztosan megfeleljen az olyan környezetben, ahol a tag meg fognak jelenni; például az automatikus változók $Ez az osztály módszer rejtett tagjainak kell megjelennie.
- Új elem, Remove-Item és Get-ChildItem létrehozásának és kezelésének támogatására továbbfejlesztett [szimbolikus hivatkozások](https://en.wikipedia.org/wiki/Symbolic_link). A **- ItemType** paraméter a New-cikk egy új értéket fogad el **SymbolicLink**. Mostantól létrehozhat szimbolikus hivatkozások egyetlen sorban a New-cikk parancsmag futtatásával.
- Get-ChildItem is rendelkezik egy új - mélysége paramétert, amely korlátozza a rekurzió használatával az a - Recurse paramétert. Ha például Get-ChildItem-Recurse - mélysége 2 eredményeket ad vissza az aktuális mappából, összes alárendelt mappára az aktuális mappán belül, és az összes, a gyermek belüli mappa mappákat.
- Most már lehetővé teszi, hogy másolja fájlokat vagy mappákat egy Windows PowerShell-munkamenetből a másikba, ami azt jelenti, hogy tud-e fájlokat másolni olyan munkamenetek, amelyek a távoli számítógépek csatlakoznak a Copy-Item (például futtató számítógépek [Nano Server](https://blogs.technet.com/b/windowsserver/archive/2015/04/08/microsoft-announces-nano-server-for-modern-apps-and-cloud.aspx), és Ily módon kell nincs más felület). Másolja a fájlokat, az új - FromSession és - ToSession paramétereit értékként adja meg a PSSession-azonosítókat, és adjon hozzá - elérési út és - célt adja meg a forrás elérési útvonala a és a cél, jelölik. Ha például Copy-Item-c: elérési út\\myFile.txt - ToSession $s-cél d:\\DestinationFiles.
- Windows PowerShell beszédátírási lett továbbfejlesztve, hogy érvényesek minden üzemeltetési alkalmazások (például a Windows PowerShell ISE-ben) mellett a konzol gazdakörnyezetét (**powershell.exe**). Átírási beállítások (beleértve az egy rendszerszintű átiratok engedélyezése) engedélyezésével konfigurálható a **kapcsolja be a PowerShell Beszédátírási** található a felügyeleti sablonok/Windows-összetevők/Windows csoportházirend-beállítás PowerShell.
- Egy új parancsfájl részletes nyomkövetési szolgáltatás engedélyezi a részletes nyomon követési és elemzési rendszerek a Windows PowerShell parancsfájl-kezelési használati teszi lehetővé. Miután engedélyezte a részletes parancsfájl nyomkövetés, Windows PowerShell az összes parancsfájl-blokkokban naplózza az esemény nyomkövetése for Windows (ETW) eseménynaplóba **Microsoft-Windows-PowerShell/műveleti**.
- A Windows PowerShell 5.0-től kezdődően új titkosítási üzenet szintaxis parancsmagok támogatják az tartalmak titkosítását és visszafejtését titkosítási szempontból védelme érdekében üzenetet megfelelően az IETF szabvány formátum használatával [RFC5652](https://tools.ietf.org/html/rfc5652). A Get-CmsMessage, a védelem-CmsMessage és Unprotect-CmsMessage parancsmagok hozzáadva a [Microsoft.PowerShell.Security](https://technet.microsoft.com/library/hh849807.aspx) modul.
- Az új parancsmagok a [Microsoft.PowerShell.Utility](https://technet.microsoft.com/library/hh849958.aspx) modul, Get-futási térrel, hibakeresési-futási térrel, Get-RunspaceDebug, Enable-RunspaceDebug és Disable-RunspaceDebug, lehetővé teszik egy futási térből, és az Indítás és leállítás a hibakeresési beállításainak megadása a futási térben hibakeresést. Hibakeresés tetszőleges futási terek (vagyis a futási terek, amelyek nem egy Windows PowerShell-konzol vagy a Windows PowerShell ISE-munkamenet alapértelmezett futási térben) Windows PowerShell lehetővé teszi, hogy állítson be töréspontokat a parancsfájlt, és hozzáadta töréspontok állítsa le a parancsfájlt amíg nem lehet hibakereső hibakeresése a futási térben parancsfájl futtatását. Tetszőleges futási terek beágyazott hibakeresési támogatása a Windows PowerShell parancsfájl hibakeresőt a futási terek bővült.
- Hexadecimális formátumú új parancsmag hozzáadva az [Microsoft.PowerShell.Utility](https://technet.microsoft.com/library/hh849958.aspx) modul. Hexadecimális formátumú szöveg vagy bináris adatok megtekintése az hexadecimális formátumban teszi lehetővé.
- Get-vágólapra és Set-vágólap-parancsmagok hozzáadva a [Microsoft.PowerShell.Utility](https://technet.microsoft.com/library/hh849958.aspx) modul; ezek megkönnyítik a tartalom, és a egy Windows PowerShell-munkamenetből átvitelét. A vágólap-parancsmagok támogatják a lemezképek, a hangfájlok, a fájl listák és a szöveg.
- Új parancsmag, Clear-RecycleBin, bővült a [Microsoft.PowerShell.Management](https://technet.microsoft.com/library/hh849827(v=wps.640).aspx) modulja; Ez a parancsmag kiüríti a Lomtár Bin rögzített meghajtót, amely tartalmazza a külső meghajtók esetében. Alapértelmezés szerint kéri megerősítését a Clear-RecycleBin parancsot, mert a parancsmag ConfirmImpact tulajdonsága ConfirmImpact.High értékre van állítva.
- Új parancsmag, New-TemporaryFile, parancsfájl-kezelési részeként ideiglenes fájl létrehozását teszi lehetővé. Alapértelmezés szerint az új ideiglenes fájl létrehozása ```C:\Users\<user name>\AppData\Local\Temp```.
- A Out-File, az Add-tartalom és a Set-tartalom parancsmagok most már rendelkezik egy új - NoNewline paraméter, amely egy új sor kihagyása után a kimenet.
- A New-Guid parancsmagot használja a .NET-keretrendszer Guid osztály egy GUID Azonosítót, akkor hasznos, ha ír parancsfájlokat vagy DSC-erőforrások létrehozásához.
- Mivel a fájlverzió-információkat félrevezető, különösen, ha egy fájl javítva van, a FileInfo objektum új FileVersionRaw és ProductVersionRaw parancsfájl tulajdonságai érhetők el. Például futtathatja a következő parancsot az ezeket a tulajdonságokat a powershell.exe értékek megjelenítése ahol $pid tartalmaz egy futó Windows PowerShell-munkamenetet a folyamat azonosítója:  ```Get-Process -Id $pid -FileVersionInfo | Format-List *version* -Force```
- Új parancsmagok Enter-PSHostProcess és kilépési-PSHostProcess lehetővé teszik Windows PowerShell-parancsfájlokat elkülönítve a jelenlegi folyamat, amely a Windows PowerShell-konzolt futtatja a folyamatokat a hibakeresés. Futtatás Enter-PSHostProcess adja meg, vagy csatolni, egy adott folyamat azonosítója, és futtassa a Get-futási térben való visszatéréshez az aktív futási terek a folyamaton belül. Futtassa a kilépési-PSHostProcess leválasztása a folyamat, amikor végzett, a folyamaton belül a parancsprogram-hibakeresés.
- Új parancsmag Wait-hibakereső van adva a [Microsoft.PowerShell.Utility](https://technet.microsoft.com/library/hh849958.aspx) modul. Wait-hibakereső leállítása a hibakeresőt a parancsfájl a következő utasítást a parancsfájl futtatása előtt futtathatók.
- A Windows PowerShell-munkafolyamat hibakereső mostantól támogatja a parancsot vagy a tab befejezését, és a beágyazott munkafolyamat-függvények hibakeresése is. Most már lenyomhatja **Ctrl + Break** , adja meg a hibakeresőt a parancsprogram futtatásához, a helyi és távoli munkamenetek során és a egy munkafolyamat-parancsprogram.
- A hibakeresési-Job parancsmagnak bővült a [Microsoft.PowerShell.Core](https://technet.microsoft.com/library/hh849695.aspx) modul parancsfájlokban való hibakeresés futó feladat Windows PowerShell-munkafolyamat, a háttér-információkért és a távoli munkamenetek a futó feladatokat.
- Windows PowerShell-feladatok AtBreakpoint, új állapot lett hozzáadva. A AtBreakpoint állapot vonatkozik, amikor egy feladat fut egy parancsfájl, amely tartalmazza a set-töréspontokat, és a parancsfájl eléri egy töréspontot. Ha a feladat hibakeresési töréspont jelenleg le van állítva, a Debug-Job parancsmag futtatásával kell hibakeresést végeznie a a feladatot.
- Windows PowerShell 5.0 ugyanabban a mappában lévő $PSModulePath valósít meg egyetlen Windows PowerShell-modul több verziójának támogatása. Egy RequiredVersion tulajdonsággal bővült a ModuleSpecification osztályhoz segítségével a kívánt verziót, a modul; kap Ez a tulajdonság nem kölcsönösen kizárják egymást az ModuleVersion tulajdonság. A Get-Module FullyQualifiedName paraméterének értéke részeként mostantól támogatott a RequiredVersion Import-Module és a Remove-modul parancsmagjaival.
- Most már elvégezheti a modul verzió érvényesítése a Test-ModuleManifest parancsmag futtatásával.
- A Get-Command parancsmagot eredményeit mostantól megjelenítik a verzió oszlopban; új verzió tulajdonsággal bővült a CommandInfo osztály. Get-Command több verzióját ugyanarra a parancsait mutatja. A verzió tulajdonság része is CmdletInfo származtatott osztályok: CmdletInfo és ApplicationInfo.
- Get-Command paramétere egy új, - ShowCommandInfo, amely PSObjects ShowCommand információkat ad vissza. Ez akkor különösen hasznos funkciókat Show-parancs futtatásakor a Windows PowerShell ISE-ben Windows PowerShell-távelérés használatával. A - ShowCommandInfo paraméter lecseréli a meglévő Get-SerializedCommand függvény a Microsoft.PowerShell.Utility modulban, de a Get-SerializedCommand parancsfájl támogatja az alacsonyabb szintű scripting továbbra is elérhető.
- Új Get-ItemPropertyValue parancsmag lehetővé teszi egy tulajdonság értékének lekérése pontjelöléssel nélkül. Például a régebbi kiadásokban a Windows PowerShell, futtathatja a következő parancsot az alkalmazás alapja tulajdonság PowerShellEngine beállításkulcs értékének beolvasásához: **(Get-ItemProperty-elérési út HKLM:\\szoftver\\Microsoft\\PowerShell\\3\\PowerShellEngine-ApplicationBase neve). ApplicationBase**. A Windows PowerShell 5.0-től kezdődően futtathatja **Get-ItemPropertyValue-elérési út HKLM:\\szoftver\\Microsoft\\PowerShell\\3\\PowerShellEngine-név ApplicationBase** .
- A Windows PowerShell-konzolt használja a szintaxisszínek hasonlóan a Windows PowerShell ISE-ben.
- Új NetworkSwitch modul tartalmazza a parancsmagok, amelyek lehetővé teszik, hogy a alkalmazni a Windows Server 2012 R2-emblémával hitelesített hálózati kapcsolók kapcsoló, a virtuális LAN (VLAN) és az alapszintű 2. rétegbeli hálózati kapcsoló port konfigurációja.
- A FullyQualifiedName paraméter van adva Import-Module és a Remove-Module-parancsmagok tárolása egy modul több verzióját támogatja.
- Save-Help, az Update-Help, a Import-PSSession, a Export-PSSession és a Get-Command rendelkezik egy új paraméter FullyQualifiedModule ModuleSpecification típusú. Adja hozzá ezt a paramétert, a modul adja meg a teljes nevet.
- Az érték **$PSVersionTable.PSVersion** 5.0 frissült.
- A WMF 5.0 (PowerShell 5.0-s) tartalmazza a **Pester** modul.  Pester tesztelési keretrendszerének PowerShell egység. Néhány egyszerű használható kulcsszót, amelyekkel hozzon létre teszteket, hogy a parancsfájlok biztosít.

### <a name="new-features-in-windows-powershell-desired-state-configuration"></a>Új szolgáltatások a Windows PowerShell Desired State Configuration

- Nyelvi fejlesztések Windows PowerShell segítségével meghatározhatja a Windows PowerShell Desired State Configuration (DSC) erőforrások osztályok használatával. Az import-DscResource már igaz dinamikus kulcsszó; Windows PowerShell elemzi a megadott modul legfelső szintű modul, a DscResource attribútumot tartalmazó osztályok kereséséhez. Mostantól használhatja osztályok meghatározásához a DSC-erőforrások, ahol nem MOF-fájlt, sem a modul mappában DSCResource almappa nem szükséges. Egy Windows PowerShell-modul fájlt tartalmazhat több DSC-erőforrás osztályok.
- Új paraméter, ThrottleLimit, bővült a PSDesiredStateConfiguration modulban a következő parancsmagokat. Adja hozzá a ThrottleLimit paraméter adható meg a cél számítógépeket és eszközöket, amelyen szeretné, a parancs egy időben működjön.
  - Get-DscConfiguration
  - Get-DscConfigurationStatus
  - Get-DscLocalConfigurationManager
  - Restore-DscConfiguration
  - Test-DscConfiguration
  - Compare-DscConfiguration
  - Publish-DscConfiguration
  - Set-DscLocalConfigurationManager
  - Start-DscConfiguration
  - Update-DscConfiguration
- Központi DSC hibajelentés, a hibával kapcsolatos részletes információk a program nem csak naplózza abban az esetben, ha naplófájl van, de elküldhetők egy központi helyen későbbi elemzés céljából. Ez a központi hely használatával minden olyan kiszolgáló a környezetben bekövetkezett DSC konfigurációs hibák tárolja. A jelentéskészítő kiszolgáló a metaadat-konfigurációs van definiálva, miután hibákat a jelentéskészítő kiszolgálónak küldött, és egy adatbázisban tárolja. Ez a funkció függetlenül e van konfigurálva egy célcsomóponttal állíthat egy lekéréses kiszolgálóról konfigurációk lekérni.
- Fejlesztések a Windows PowerShell ISE-ben a DSC-erőforrások szerzői megkönnyítése érdekében. Most már a következőket teheti.
  - Belül minden DSC-erőforrások listája egy **konfigurációs** vagy **csomópont** megadásával blokk **Ctrl + szóköz** egy üres sor a blokkon belül.
  - Az erőforrás-tulajdonságainak automatikus kiegészítés a **enumerálás** típusa.
  - Az automatikus kiegészítés a **DependsOn** tulajdonság DSC-erőforrások, a többi erőforrás-példány a konfiguráció alapján.
  - Továbbfejlesztett kiegészítés erőforrás tulajdonságértékek.
- A felhasználók most már futtathatja egy erőforrást egy meghatározott hitelesítő adatokat adja hozzá a **PSDscRunAsCredential** egy csomópont blokk attribútumot. For example, PSDscRunAsCredential = Get-Credential Contoso\\DscUser. Ez a funkció akkor hasznos, futtassa a Windows Installer és a végrehajtható telepítők, a felhasználónkénti beállításjegyzék-struktúrát eléréséhez, vagy az aktuális felhasználói környezetet kívül más feladatok elvégzéséhez konfigurációk létrehozásához.
- 32 bites (x86 alapú) támogatás lett hozzáadva a **konfigurációs** kulcsszót.
- Mostantól DSC-konfigurációk hozzáadása által definiált egyéni súgója támogatja a Windows PowerShell \[CmdletBinding()] a generált konfigurációt függvénynek.
- Egy új **DscLocalConfigurationManager** attribútumot jelöli meg a konfigurációs blokk egy metaadat-konfigurációt, így a DSC helyi Configuration Manager konfigurálására szolgál. Ez az attribútum csak olyan elemek, amelyek a DSC helyi Configuration Manager beállítása tartalmazó konfigurációt korlátozza. A feldolgozás során ezt a konfigurációt hoz létre egy \*. meta.mof fájlt, amely elküldi a megfelelő cél csomópontokhoz a Set-DscLocalConfigurationManager parancsmag futtatásával.
- Részleges konfigurációk mostantól engedélyezettek a Windows PowerShell 5.0-s. Konfigurációs dokumentumok egy csomópontjára töredék juttathat el. Egy csomópont fogadni a konfigurációs dokumentum több töredékkel a csomópont helyi Configuration Manager először állítsa adja meg a várt töredék
- Kereszt-számítógép szinkronizációs DSC Windows PowerShell 5.0 rendszerben jelent meg. A beépített WaitFor használatával\* erőforrások (**WaitForAll**, **WaitForAny**, és **WaitForSome**), most már megadhatja függőségek a számítógépeken során konfigurációs fut le, külső vezénylések nélkül. Ezeket az erőforrásokat biztosítanak a csomópontok közötti szinkronizálás CIM-kapcsolatok a WS-Man protokoll használatával. Egy konfigurációs megvárhatja egy másik számítógépet adott erőforrás állapotának módosítása.
- Csak Enough Administration (JEA), egy új delegálás biztonsági funkció, használja a DSC és Windows PowerShell korlátozott futási terek segítségével biztonságos vállalatok adatvesztés vagy biztonsági sérülés, az alkalmazottak által, hogy szándékos vagy véletlen. További információ a JEA, ahonnan letöltheti a xJEA DSC-erőforrás, beleértve: [Just Enough Administration, lépésről lépésre](https://blogs.technet.com/b/privatecloud/archive/2014/05/14/just-enough-administration-step-by-step.aspx).
- Az alábbi új parancsmagok hozzáadva a PSDesiredStateConfiguration modulnak.
  - Új Get-DscConfigurationStatus parancsmag egy célcsomóponttal konfigurációs állapot kapcsolatos áttekintő szintű adatokat olvas be. Az állapot szerezheti be az utolsó, vagy az összes konfigurációt.
  - Új Compare-DscConfiguration parancsmag egy megadott konfigurációt egy vagy több cél csomópontok tényleges állapotát a hasonlítja össze.
  - Új Publish-DscConfiguration parancsmag másolja át a konfigurációs MOF-fájlt, amely a cél-csomópontra, de nem vonatkozik a konfigurációt. A konfiguráció alkalmazása a következő konzisztencia fázis során, vagy az Update-DscConfiguration parancsmag futtatásakor.
  - Új Test-DscConfiguration parancsmag segítségével győződjön meg arról, hogy a létrejövő konfigurációt egyezik-e a szükséges konfiguráció, adatszolgáltató pedig IGAZ, ha a konfiguráció megfelel a kívánt konfiguráció vagy a False, ha a tényleges konfiguráció nem felel meg a kívánt konfiguráció.
  - Új Update-DscConfiguration parancsmag a konfigurációt a dolgozhatók kényszeríti. A Local Configuration Manager lekéréses módban van, ha a parancsmag a konfiguráció alkalmazása előtt a pull-kiszolgálóról beolvasása.

### <a name="new-features-in-windows-powershell-ise"></a>Új szolgáltatások a Windows PowerShell ISE-ben

- Most már szerkesztheti távoli Windows PowerShell-parancsfájlok és a Windows PowerShell ISE-ben, egy helyi példányát fájlok futtatásával Enter-PSSession távoli munkamenet elindításához azon a számítógépen, a szerkeszteni kívánt fájlokat tárolja, és futtassa **PSEdit \<elérési útját és nevét a távoli számítógépen\>**. Ez a funkció egyszerűsíti a szerkesztési a Server Core telepítési lehetőség Windows Server, ahol nem tudja futtatni a Windows PowerShell ISE-ben tárolt Windows PowerShell-fájlokat.
- A Start-átírási parancsmag mostantól támogatott a Windows PowerShell ISE-ben.
- Most már a Windows PowerShell ISE-ben a távoli parancsfájlokat is hibakeresési.
- Egy új parancsával **összes felosztása** (Ctrl + B) bontja a hibakeresőt a helyi és távoli futó parancsprogramok.

### <a name="new-features-in-windows-powershell-web-services-management-odata-iis-extension"></a>Új szolgáltatások a Windows PowerShell webszolgáltatások (felügyeleti OData IIS kiterjesztés)

- A Windows PowerShell 5.0-től kezdődően is létrehozhat a az Export-ODataEndpointProxy parancsmagot, az az új található a megadott OData-végpont által elérhetővé tett funkciók alapján Windows PowerShell-parancsmagok egy halmaza [ Microsoft.PowerShell.OdataUtils](https://technet.microsoft.com/library/dn818507(v=wps.640).aspx) modul.

### <a name="notable-bug-fixes-in-windows-powershell-50"></a>A Windows PowerShell 5.0 jelentős hibajavítások

- Windows PowerShell 5.0 tartalmaz egy új COM megvalósításában, kínál, amelyek teljesítményének jelentős növelése esetén COM-objektumok dolgozik. Ismertető videó az áttekintésről a hatás, lásd: [Com_Perf_Improvements](https://1drv.ms/1qu3UPZ).
- Jelentős teljesítménybeli fejlesztések történtek-e az első kiegészítés egy Windows PowerShell-munkamenetben lecsökkentik lapon befejezési idő szerint szinte 500 ms.

## <a name="new-features-in-windows-powershell-40"></a>Új szolgáltatások a Windows PowerShell 4.0

Windows PowerShell 4.0 a visszamenőlegesen kompatibilis. Parancsmagok, szolgáltatók, modulok, beépülő modulokat, parancsfájlok, funkciók és profilok a Windows PowerShell 3.0 és a Windows PowerShell 2.0 kifejlesztett működik a Windows PowerShell 4.0-s módosítása nélkül.

A Windows 8.1 és Windows Server 2012 R2 alapértelmezés szerint telepítve van a Windows PowerShell 4.0-s verzióját. Windows PowerShell 4.0-s verzióját telepíti a Windows 7 SP1 vagy Windows Server 2008 R2, töltse le és telepítse [Windows Management Framework 4.0](https://www.microsoft.com/download/details.aspx?id=40855). Mindenképpen olvassa el a letöltési részleteit, és rendszerkövetelményeknek összes, Windows Management Framework 4.0 telepítése előtt.

- [Új szolgáltatások a Windows PowerShellben](#new-features-in-windows-powershell-1)
- [Új szolgáltatások a Windows PowerShell integrált parancsfájlkezelési környezet (ISE)](#new-features-in-windows-powershell-integrated-scripting-environment-ise)
- [Új szolgáltatások a Windows PowerShell-munkafolyamat](#new-features-in-windows-powershell-workflow)
- [Új szolgáltatások a Windows PowerShell webszolgáltatások](#new-features-in-windows-powershell-web-services)
- [Új szolgáltatások a Windows PowerShell-elérés](#new-features-in-windows-powershell-web-access)
- [A Windows PowerShell 4.0-s jelentős hibajavítások](#notable-bug-fixes-in-windows-powershell-40)

Windows PowerShell 4.0 a következő új funkciókat tartalmaz.

### <a name="a-namenew-features-in-windows-powershell-1-new-features-in-windows-powershell"></a><a name="new-features-in-windows-powershell-1" />Új szolgáltatások a Windows PowerShellben

- **Windows PowerShell Desired State Configuration** (DSC) egy olyan új felügyeleti rendszer a Windows PowerShell 4.0-s verzióját, amely lehetővé teszi a központi telepítési és konfigurációs adatok szoftveres szolgáltatások és a környezetben, ahol ezek a szolgáltatások futnak a felügyeletét. DSC kapcsolatos további információkért lásd: [Ismerkedés a Windows PowerShell Desired State Configuration](https://technet.microsoft.com/library/c134aa32-b085-4656-9a89-955d8ff768d0).
- **Save-Help** mostantól lehetővé teszi a távoli számítógépekre telepített modulok súgója menti. Save-Help használatával töltse le a modul súgó az internethez csatlakozó ügyféltől (amelyen nem az összes, amelyhez segítségre van szüksége a modulok feltétlenül telepítve van), és másolja a mentett súgó egy távoli megosztott mappa vagy egy távoli számítógépen, amelyen nincs Internet a hozzáférés.
- A Windows PowerShell-hibakereső bővült a Windows PowerShell-munkafolyamatok, valamint a távoli számítógépeken futó parancsfájlokat a hibakeresés engedélyezése. Windows PowerShell-munkafolyamatok mostantól a Windows PowerShell-parancssorból vagy a Windows PowerShell ISE parancsfájl szintjén indítja el. Windows PowerShell-szkriptek, beleértve a parancsfájl-munkafolyamatok, most is hibakereséséhez távoli munkamenetek során. Távoli hibakeresési munkamenetek megmaradnak a Windows PowerShell távoli munkamenet leválasztása és újból később.
- A **RunNow** paramétere **Register-ScheduledJob** és **Set-ScheduledJob** nem egy azonnali kezdési dátum és idő feladatok beállítása a használatávalkell**Eseményindító** paraméter.
- **Invoke-RestMethod** és **Invoke-WebRequest** mostantól lehetővé teszik az összes fejléc a fejlécek paraméter használatával. Bár ez a paraméter mindig korábban már létezett, korábban egy webes parancsmagokhoz, amelyek kivételek vagy hibák eredményeként több paramétert.
- **Get-Module** olyan új paraméter **FullyQualifiedName**, a típus **ModuleSpecification\[]**. A **FullyQualifiedName** paramétert a Get-Module lehetővé teszi a modul adja meg, a modul neve, verziója, és szükség esetén GUID Azonosítóját.
- Az alapértelmezett végrehajtási házirend-beállítás a Windows Server 2012 R2 **RemoteSigned**. A Windows 8.1 nem történik változás az alapértelmezett beállítás.
- A Windows PowerShell 4.0-től kezdődően metódus meghívásának dinamikus módszer nevek használatával támogatott. Változók használata a metódus nevét tárolja, és ezután dinamikusan a metódus meghívása a változó meghívásával.
- Aszinkron munkafolyamat-feladatokat már nem törlődnek, amikor az által megadott időkorlát a **PSElapsedTimeoutSec** gyakori munkafolyamat-paraméter telt el.
- Egy új paraméter **RepeatIndefinitely**, bővült a **New-JobTrigger** és **Set-JobTrigger** parancsmagok. Ezzel elkerülhető, hogy a telemetriaadatokat megadása egy **TimeSpan.MaxValue** értékét a **RepetitionDuration** futhat ismétlődően egy ütemezett feladatot határozatlan időre szól paramétert.
- A **Passthru** paraméter hozzáadva a **Enable-JobTrigger** és **Disable-JobTrigger** parancsmagok. A Passthru paraméter létrehozása vagy módosítása a parancs minden olyan objektumokat jeleníti meg.
- A paraméter nevét adja meg a munkacsoportban a **Add-Computer** és **Remove-Computer** parancsmagok mostantól konzisztensek. Mindkét parancsmag most már használja a paraméterrel **Munkacsoport_neve**.
- Egy új közös paraméter **PipelineVariable**, hozzá van adva. PipelineVariable változóként, melyet a folyamat további részében is átadható lehetővé teszi egy védőeszközön parancs (vagy egy védőeszközön parancs része) eredményeinek mentésére.
- Mostantól támogatott a gyűjtemény szűrést egy metódus-szintaxis használatával. Ez azt jelenti, hogy most már szűrhet objektumok gyűjteményét Where() vagy Where-Object metódushívásokat formázott hasonló egyszerűsített szintaxis használatával. A következő egy példa: (Get-Process) .where ({$_. -Neve egyezik "powershell"})
- A **Get-Process** parancsmag rendelkezik egy új kapcsolóparaméter **IncludeUserName**.
- Új parancsmag, **Get-FileHash**, egy fájlkivonat adja vissza a megadott fájl több formátum, hozzá van adva.
- A Windows PowerShell 4.0-s, ha egy modul használja a **DefaultCommandPrefix** kulcs a jegyzékfájlban, vagy ha a felhasználó importál egy modult a következővel a **előtag** paramétert, a **ExportedCommands**tulajdonság a modul a parancsok láthatók a modul a előtaggal. A modulhoz minősített szintaxissal, modulename: a parancsok futtatásakor\\CommandName, a nevek tartalmaznia kell az előtagot.
- Az érték **$PSVersionTable.PSVersion** 4.0-s frissítve lett.
- **WHERE()** operátor viselkedése megváltozott. `Collection.Where('property -match name')` egy karakterlánc-kifejezés a következő formátumban elfogadásával `"Property -CompareOperator Value"` már nem támogatott. Azonban a **Where()** operátor elfogadja a scriptblock kulcsszót a formátumú karakterlánc kifejezések; ez továbbra is támogatott.

### <a name="new-features-in-windows-powershell-integrated-scripting-environment-ise"></a>Új szolgáltatások a Windows PowerShell integrált parancsfájlkezelési környezet (ISE)

- Windows PowerShell ISE-ben a Windows PowerShell-munkafolyamat Hibakeresés és a távoli erőforrásparancsfájlokban végzett hibakeresés is támogatja.
- Az IntelliSense már támogatja a Windows PowerShell Desired State Configuration szolgáltatók és konfigurációkat.

### <a name="new-features-in-windows-powershell-workflow"></a>Új szolgáltatások a Windows PowerShell-munkafolyamat

- Támogatás hozzáadva az új **PipelineVariable** általános paraméter iteratív folyamatok, például kontextusában a System Center Orchestrator által használt; azaz folyamatok, amelyek egyszerűen balról jobbra, nem pedig parancsok futtatásához összekeveredett streamelés segítségével futnak.
- Paraméterkötés dolgozhat kívül lapon befejezési forgatókönyvek, például parancsok, amelyek nem szerepelnek az aktuális futási térben jelentősen bővült.
- Egyéni tároló tevékenységek már támogatja a Windows PowerShell-munkafolyamat. Ha egy tevékenység-paraméter a típusú **tevékenység**, **tevékenység\[]** (vagy a tevékenységek általános gyűjteménye) és a felhasználó argumentumként, majd a Windows PowerShell parancsprogram-blokkot mellékelt A munkafolyamat XAML, mint a szokásos Windows PowerShell-parancsfájl-munkafolyamat összeállítása a parancsprogram-blokkot alakítja.
- Egy összeomlás utáni Windows PowerShell-munkafolyamat automatikusan újracsatlakozik a felügyelt csomópontok.
- Most már képes szabályozni **Foreach-Parallel** tevékenység-utasítások használatával a **ThrottleLimit** tulajdonság.
- A **ErrorAction** általános paraméter új érvényes értékkel, rendelkezik **Suspend**, amely pedig kizárólag a munkafolyamatok.
- A munkafolyamat végpontjának most már automatikusan lezárja a nem aktív munkamenetek, nincs folyamatban lévő feladatok és nincsenek folyamatban lévő feladatok esetén. Ez a funkció takarékoskodik az automatikus lezárás feltételek teljesülése esetén a munkafolyamat-kiszolgálóként működő számítógép erőforrásait.

### <a name="new-features-in-windows-powershell-web-services"></a>Új szolgáltatások a Windows PowerShell webszolgáltatások

- Ha hiba lép fel, a Windows PowerShell webszolgáltatások (PSWS, is nevű felügyeleti OData IIS kiterjesztés), miközben a parancsmag fut, részletes hibaüzenet üzenetek vannak vissza a hívónak. Ezenkívül, hajtsa végre a hibakódok [Windows Azure REST API-hiba kódja útmutatójának](https://msdn.microsoft.com/library/windowsazure/dd179357.aspx).
- A végpont is most az API-verzió megadása, valamint egy adott API-verzió használatának kényszerítése. Verzió eltérést ügyfél és kiszolgáló közötti fordulhat elő, amikor az ügyfél és a kiszolgáló jelenik meg hibaüzenet.
- A feladó séma felügyeleti egyszerűsítettük a sémában bármely hiányzó mezők értékei automatikus létrehozásával. Generáció történik, kiindulópontként hasznos, még akkor is, ha a küldő séma nem létezik.
- Kezelése, PSWS típus lett továbbfejlesztve, hogy által hasonlóan viselkedik, mint az alapértelmezett konstruktort, használjon más konstruktort használó típusok támogatása az **PSTypeConverter** a Windows PowerShellben. Ez lehetővé teszi összetett típusok használata PSWS.
- PSWS mostantól lehetővé teszi a társított példány kibontása egy lekérdezés futtatása közben. A nagyobb bináris tartalom (például képek, hang- vagy videofájl) az adatátviteli költségek jelentős, és jobb bináris adatok átviteléhez a kódolás nélkül. PSWS megnevezett adatfolyamok átvitelére kódolás nélkül használja. A nevesített forrásadatfolyam egy tulajdonságot egy entitás az a **Edm.Stream** típusa. Minden elnevezett forrásadatfolyam BEOLVASÁSÁHOZ vagy frissítéséhez műveletek külön URI tartozik.
- OData-műveleteket biztosít az meghívása nem CRUD (létrehozás, Olvasás, frissítés és törlés) módszerek erőforrás mechanizmusként. Egy műveletet hívhat meg egy HTTP POST kérést küld az URI-t a művelet van definiálva. A művelet paramétereit a POST-kérés törzse vannak definiálva.
- A Windows Azure irányelveket összhangban kell lennie, az összes URL-címek egyszerűsíteni kell. Szereplő változást **kulcs, szegmens** lehetővé teszi, hogy történetesen szegmensek egyetlen kulcsok. Vegye figyelembe, hogy hivatkozik, amely több kulcs értéket használja a szükséges vesszővel tagolt értékek zárójeles jelöléssel, mint korábban.
- Ebben a kiadásban az PSWS, mielőtt a csak egyirányú végrehajtásához létrehozási, frissítési vagy törlési műveletek volt Post meghívni, Put, vagy törölje a legfelsőbb szintű erőforráshoz. Új PSWS ebben a kiadásban található erőforrás-műveletek segítségével a felhasználók az azonos eredmények elérése ugyanarra az erőforrásra, kevesebb közvetlenül hamarosan eléri a úgy, mintha a tartalmazott, ezek az erőforrások elérése közben.

### <a name="new-features-in-windows-powershell-web-access"></a>Új szolgáltatások a Windows PowerShell-elérés

- Bontsa a kapcsolatot, és újból csatlakozik a webes Windows PowerShell-elérés konzolon meglévő munkameneteket. A **mentése** gomb a webalapú konzol lehetővé teszi a munkamenet leválasztása annak törlése nélkül, és csatlakozni egy másik időt.
- Alapértelmezett paramétereihez is megjeleníthetők a bejelentkezési oldalon. Alapértelmezett paraméterek megjelenítéséhez értékeket konfigurálja az összes beállítás jelenik meg a **választható kapcsolati beállítások** nevű fájlt a bejelentkezési oldal területéhez **web.config**. Használhatja a **web.config** fájl hitelesítő adatok egy második vagy egy másik készletét kivételével minden választható csatlakozási beállítások konfigurálása.
- A Windows Server 2012 R2 távolról kezelheti az engedélyezési szabályok a Windows PowerShell-elérés. A **Add-PswaAuthorizationRule** és **Test-PswaAuthorizationRule** parancsmagok mostantól tartalmaznak egy Credential paramétert, amely lehetővé teszi a rendszergazdák számára, hogy egy távoli számítógépről vagy az engedélyezési szabályok kezelése egy Windows PowerShell-elérés munkamenet.
- Minden munkamenet egy új böngészőlapon használatával most már egyetlen böngésző-munkamenet több Windows PowerShell-elérés előadások is rendelkezhet. Meg kell nyitnia egy új böngésző-munkamenetet szeretne csatlakozni a webes Windows PowerShell-konzolján egy új munkamenet már nem.

### <a name="notable-bug-fixes-in-windows-powershell-40"></a>A Windows PowerShell 4.0-s jelentős hibajavítások

- **Get-Counter** így visszakerülhet számlálókat, amely tartalmaz egy Windows francia kiadásai aposztróf karaktert.
- Most már megtekintheti a **GetType** deszerializált objektum metódust.
- **#Requires** utasítások mostantól engedélyezheti a felhasználóknak rendszergazdai hozzáférési jogosultsággal kell, szükség esetén.
- A **importálása Csv-** parancsmag mostantól figyelmen kívül hagyja az üres sorok.
- A probléma, amelyben Windows PowerShell ISE-t használ-e túl sok memóriát futtatása során egy **Invoke-WebRequest** parancs megoldották a problémát.
- **Get-Module** mostantól megjeleníti a modulverziók egy **verzió** oszlop.
- Remove-Item - Recurse most almappák elemek eltávolítja a várt módon.
- A **felhasználónév** tulajdonsággal bővült **Get-Process** kimeneti objektumok.
- A **Invoke-RestMethod** parancsmag mostantól az összes rendelkezésre álló eredményeket ad vissza.
- **Tag hozzáadása** most már életbe a kivonattáblák, még akkor is, ha a kivonattáblák még nem használtak.
- **Select-Object - bontsa ki a** már nem sikertelen vagy kivételt állít elő, ha a tulajdonság értéke null vagy üres.
- **Get-Process** más parancsokkal, amely egy adott folyamat ezután használható a **ComputerName** objektumok tulajdonságot.
- **ConvertTo-Json** és **ConvertFrom-Json** is mostantól fogadja el a használati feltételeket dupla idézőjelek között, és a hibaüzenetek immár honosítható.
- **Get-Job** most már minden befejeződött az ütemezett feladatok, még akkor is, az új munkamenetek beolvasása.
- Csatlakoztatása és leválasztása a VHD-k használatával kapcsolatos problémák a **fájlrendszer** a Windows PowerShell 4.0-s szolgáltató megoldódott. Windows PowerShell már képes észlelni az új meghajtókat, ha csatlakoztatva vannak ugyanabban a munkamenetben.
- Már nem kell explicit módon töltse be **ScheduledJob** vagy **munkafolyamat** modulok feladat adattípusukkal együtt működik.
- Teljesítménnyel kapcsolatos fejlesztések történtek-e azon a munkafolyamatok, amelyek meghatározzák a beágyazott munkafolyamatok; importálása Ez a folyamat már gyorsabb.

## <a name="new-features-in-windows-powershell-30"></a>Új szolgáltatások a Windows PowerShell 3.0

Windows PowerShell 3.0 a következő új funkciókat is tartalmaz.

- [Windows PowerShell-munkafolyamat](#windows-powershell-workflow)
- [Webes Windows PowerShell-elérés](#windows-powershell-web-access)
- [Új Windows PowerShell ISE-ben szolgáltatások](#new-windows-powershell-ise-features)
- [A Microsoft .NET-keretrendszer 4.0-s támogatása](#support-for-microsoft-net-framework-4)
- [Windows előtelepítési környezet támogatása](#support-for-windows-preinstallation-environment)
- [Leválasztott munkamenetek](#disconnected-sessions)
- [Robusztus munkamenet-kapcsolatot](#robust-session-connectivity)
- [Frissíthető Súgó](#updatable-help-system)
- [Továbbfejlesztett Online súgó](#enhanced-online-help)
- [A CIM-integráció](#cim-integration)
- [Munkamenet-konfigurációs fájlok](#session-configuration-files)
- [Ütemezett feladatok és a tevékenység Scheduler-integráció](#scheduled-jobs-and-task-scheduler-integration)
- [Windows PowerShell nyelvi fejlesztések](#windows-powershell-language-enhancements)
- [Új fő parancsmagjainak](#new-core-cmdlets)
- [Meglévő Core parancsmagok és szolgáltatók fejlesztései](#improvements-to-existing-core-cmdlets-and-providers)
- [Távoli modul importálásához és felderítés](#remote-module-import-and-discovery)
- [Továbbfejlesztett kiegészítés](#enhanced-tab-completion)
- [A modul automatikus telepítéséhez](#module-auto-loading)
- [A modul környezetet eredményez](#module-experience-improvements)
- [Egyszerűsített parancsot felderítése](#simplified-command-discovery)
- [A továbbfejlesztett naplózás, a diagnosztikai és a csoport házirend támogatása](#improved-logging-diagnostics-and-group-policy-support)
- [Formázás és a kimeneti fejlesztései](#formatting-and-output-improvements)
- [Továbbfejlesztett Konzolfelületet gazdagép](#enhanced-console-host-experience)
- [Új parancsmag és az API-k üzemeltetéséhez](#new-cmdlet-and-hosting-apis)
- [Teljesítménnyel kapcsolatos fejlesztések](#performance-improvements)
- [Futtató és a megosztott gazdagép támogatása](#runas-and-shared-host-support)
- [Speciális karakter kezelési fejlesztések](#special-character-handling-improvements)

### <a name="windows-powershell-workflow"></a>Windows PowerShell-munkafolyamat

Windows PowerShell-munkafolyamati Windows PowerShell biztosít a Windows Workflow Foundation hatékonyságát. Munkafolyamatokat ír XAML vagy a Windows PowerShell nyelven, és azokat ugyanúgy, mint a parancsmag futtatásakor szeretné futtatni. A [Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) parancsmag beolvassa a munkafolyamat-parancsok és a [Get-Help](https://technet.microsoft.com/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a) parancsmag Előhozza a munkafolyamatok súgóját.

Munkafolyamatok, amelyek hosszú futású, ismételhető, gyakori, párhuzamosítható, megszakítható, suspendable és újraindítható multicomputer felügyeleti tevékenységek sorrendje. A munkafolyamatok a szándékos vagy véletlen a működésében zavarokat tapasztalhat, például a hálózati leállások, a Windows újraindítása vagy áramkimaradás folytathatók.

A munkafolyamatok is hordozhatók; ezeket exportálva mint vagy importált XAML-fájlokból. Egyéni munkamenet-konfigurációk, amelyek lehetővé teszik a munkafolyamat-tevékenységek vagy a meghatalmazott vagy alárendelt felhasználók által futtatandó munkafolyamat írhat.

Az alábbiakban a Windows PowerShell munkafolyamat előnyei

- Az előkészített, hosszan futó feladatok automatizálását.
- **Hosszan futó feladatok távoli megfigyelés**. Állapot és a tevékenységek előrehaladásának bármikor jelennek meg.
- **Multicomputer kezelése.** Egyidejű feladatok futtatása munkafolyamatként száz felügyeleti csomóponton. Windows PowerShell-munkafolyamat általános felügyeleti paramétert, beépített kódtárat tartalmaz például **PSComputerName**, amelyek lehetővé teszik több számítógép-felügyeleti forgatókönyvek.
- **Egyetlen feladat a végrehajtás összetett folyamatokat.** Kapcsolódó parancsfájlokat, amely egy teljes, végpontok közötti forgatókönyv megvalósításához egyetlen munkamenetben kombinálhatja.
- **Adatmegőrzés.** : munkafolyamat mentése (vagy ellenőrzési mutatott) adott időpontokban, a szerző által megadott, folytathatja a munkafolyamatot az elejétől újraindítania a munkafolyamatot az utolsó megőrzött feladat (vagy ellenőrzőpontból), így.
- **Megbízhatóságára.** Automatikus hibaelhárítás. A munkafolyamatok tervezett és nem tervezett újraindítás stabilitást biztosít. Munkafolyamat futtatásának felfüggesztése, és ezután úgy folytatódik, a munkafolyamatot az utolsó adatmegőrzés pontot. A munkafolyamat-szerzők meghatározott tevékenységek ismételt futtatásának hiba esetén egy vagy több felügyelt csomópontokon is kijelölhet.
- **Bontását, csatlakoztassa újra, és futtassa a leválasztott munkamenethez.** A felhasználók csatlakoztatása és leválasztása a munkafolyamat-kiszolgálón, de a munkafolyamat futtatása folyamatosan. Jelentkezzen ki az ügyfélszámítógép vagy indítsa újra az ügyfélszámítógépen, és a munkafolyamat-végrehajtási egy másik számítógépről figyelheti a munkafolyamat megszakítása nélkül.
- **Az ütemezés.** Munkafolyamat-feladatokat, mint bármely Windows PowerShell-parancsmag vagy szkript ütemezhető.
- **Munkafolyamat és a kapcsolat szabályozás.** A munkafolyamat végrehajtása és a kapcsolatok használatát a csomópontok szabályozható, méretezhetőséget és magas rendelkezésre állású forgatókönyveket tesz lehetővé.

### <a name="windows-powershell-web-access"></a>Webes Windows PowerShell-elérés

Windows PowerShell-elérés Windows Server 2012 funkciója lehetővé teszi a felhasználóknak a Windows PowerShell-parancsok és szkriptek futtatását egy webalapú konzol. A webalapú konzol használó eszközöket nem szükséges Windows PowerShell, a távfelügyeleti szoftvereket vagy a böngésző beépülő modul telepítése. Szükséges a Windows PowerShell-elérés megfelelően konfigurált átjáró és a egy eszköz ügyfélböngészőnek, amely támogatja a JavaScript, és elfogadja a cookie-kat.

További információkért lásd: [Windows PowerShell-elérés telepítése](https://go.microsoft.com/fwlink/p/?LinkID=221050).

### <a name="new-windows-powershell-ise-features"></a>Új Windows PowerShell ISE-ben szolgáltatások

Windows PowerShell 3.0, a Windows PowerShell integrált parancsfájl-kezelési környezet (ISE) tartalmaz számos új funkciót, beleértve az IntelliSense, Show-parancsablakot, egy egységesített konzol ablaktáblában kódrészletek, kapcsos zárójel egyeztetéséhez, bontsa ki a összecsukása szakaszok, az automatikus mentés, a legutóbbi elemek lista, gazdag másolási, blokk másolása és teljes támogatása a Windows PowerShell parancsfájl-munkafolyamatok írása. További információkért lásd: [about_Windows_PowerShell_ISE [3]](https://technet.microsoft.com/library/dfa54d47-60c6-4fff-8197-c747e8d411bb).

### <a name="support-for-microsoft-net-framework-4"></a>A Microsoft .NET-keretrendszer 4 támogatása

Windows PowerShell van építve a közös nyelvi futtatókörnyezet 4.0 ellen. A parancsmag, szkripteket vagy a munkafolyamat-szerzők használhatja az új Microsoft .NET-keretrendszer 4-osztályok a Windows PowerShellben, funkciókat, beleértve az alkalmazáskompatibilitás és üzembe helyezés, a felügyelt bővíthetőségi keretrendszerét, párhuzamos számítási, hálózatkezelési, Windows Communication Foundation és a Windows Workflow Foundation.

### <a name="support-for-windows-preinstallation-environment"></a>Windows előtelepítési környezet támogatása

Windows PowerShell 3.0 része egy nem kötelező Windows előtelepítési környezet (Windows PE) 4.0-s verzióját a Windows 8 rendszerhez. Windows PE nem olyan minimális méretű operációs rendszer, amely elindítja a számítógép, amely nincs operációs rendszer, és felkészíti a Windows-telepítési. Windows PE partíció használható és merevlemez-meghajtók formázásához, lemezképek másolja át egy számítógépre, és egy hálózati megosztásban található Windows telepítő elindításához. Windows PowerShell 3.0-s Windows PE környezetben való üzembe helyezésére, diagnosztikai és helyreállítási forgatókönyvek lehet használni.

### <a name="disconnected-sessions"></a>Leválasztott munkamenetek

Állandó felhasználó által felügyelt munkamenetek ("PSSessions"), amely a New-PSSession parancsmag használatával hoz létre menti a Windows PowerShell 3.0-es verziótól kezdve a távoli számítógépen. Nem lesznek függ a munkamenethez, amelyben létrehozták őket.

Most már leválaszthatja a munkamenetből a parancsok a munkamenet-ban futó megszakítása nélkül. Zárja be a munkamenetet, és a számítógép leállítása. Később akkor újra tud csatlakozni a munkamenet egy másik munkamenetben ugyanazon vagy egy másik számítógépre.

A **ComputerName** paraméterében a [Get-PSSession](https://technet.microsoft.com/library/b2b10531-d0df-4746-b877-e75c09955cb6) parancsmag mostantól lekéri az összes olyan kapcsolódni a számítógéphez, a felhasználói munkamenetek akkor is, ha azok egy másik számítógépen egy másik munkamenet indításának. Csatlakozhat a munkamenetek, parancsok eredményeinek beolvasása, indítsa el az új parancsokat, és ezután bontsa a kapcsolatot a munkamenet.

Új parancsmagokkal bővült a munkamenetek leválasztása szolgáltatást támogató beleértve [Disconnect-PSSession](https://technet.microsoft.com/library/f8f95111-612f-4cba-9098-77904b0473d8), [Connect-PSSession](https://technet.microsoft.com/library/b803dd29-f208-4079-80d4-db04d778f060), és a Receive-PSSession, és az új paraméterek hozzáadva PSSessions, mint például kezelésére szolgáló parancsmagok a **InDisconnectedSession** paraméterében a [Invoke-Command](https://technet.microsoft.com/library/906b4b41-7da8-4330-9363-e7164e5e6970) parancsmagot.

A munkamenet leválasztása a funkció csak akkor, amikor a számítógépek egyaránt származó ("ügyfél"), és lezárja a kapcsolatot ("kiszolgáló") végén futnak Windows PowerShell 3.0 támogatott.

### <a name="robust-session-connectivity"></a>Robusztus munkamenet-kapcsolatot

Windows PowerShell 3.0 észleli az ügyfél és kiszolgáló közötti kapcsolat nem várt veszteségek, és megpróbálja helyreállítani a kapcsolatot, és végrehajtása automatikusan folytatódik. Ha az ügyfél-kiszolgáló közötti kapcsolat nem kell építeni őket a megengedett időn belül, a felhasználó értesítést kap, és a munkamenet megszakad. Újracsatlakozás közben a Windows PowerShell folyamatos visszajelzést biztosítanak a felhasználó.

Ha a kapcsolat nélküli munkamenet a InvokeCommand használatával lett elindítva, a Windows PowerShell létrehoz egy feladatot, a könnyebb újracsatlakozni, és folytathatja a végrehajtási leválasztott munkamenethez.

Ezeket a funkciókat egy megbízhatóbb és helyreállítható távelérése adja meg, és így a felhasználók hosszan futó feladatokat, amely szükséges hatékony előadásainkat, például a munkafolyamatok végrehajtásához.

### <a name="updatable-help-system"></a>Frissíthető Súgó

A modulok frissített Súgó-fájlokat a parancsmagok mostantól letölthető. A [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) parancsmag a legújabb súgófájlokat azonosítja, letölti azokat az internetről, kicsomagolja őket, ellenőrzi őket és telepíti őket a megfelelő nyelvspecifikus könyvtárban modul.

A frissített fájlokat használja, csak gépelje `Get-Help`. Nem kell újraindítani a Windows vagy a Windows PowerShell használatával. Súgó a modulok a $pshome címtárban frissítéséhez indítsa el a Windows PowerShell a "Futtatás rendszergazdaként" lehetőséggel.

Felhasználók, akik nem rendelkeznek Internet-hozzáférés és a tűzfal mögötti felhasználók, az új támogatásához [Save-Help](https://technet.microsoft.com/library/aed94f90-b73f-4e25-a25d-7c18d9f161fa) parancsmag Súgó fájlokat tölt le egy rendszer könyvtárat, például fájlmegosztáson. Felhasználók használhatja a [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) parancsmag lekérni frissített Súgó-fájlok a fájlmegosztásból.

Használhatja a [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) parancsmag súgójának frissítéséhez fájlok összes vagy bizonyos modulok az összes támogatott felhasználói felületi kulturális környezetek. Akkor is elhelyezhet egy [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) parancsot a Windows PowerShell-profilban. Alapértelmezés szerint Windows PowerShell letölti a súgót fájlokat egy modul legfeljebb naponta egyszer.

A Windows 8 és Windows Server 2012 modulok nem tartalmazzák a súgófájlok. Töltse le a legújabb súgófájlokat, írja be a következőt `Update-Help`. További információért gépelje be `Get-Help` (paraméterek) nélkül, vagy tekintse meg [about_Updatable_Help](https://technet.microsoft.com/library/10bba75c-f4ac-4ca1-bbf3-8f34dd521ffe).

Amikor a parancsmag Súgó-fájlok nincsenek telepítve a számítógépen, a [Get-Help](https://technet.microsoft.com/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a) parancsmag mostantól automatikusan generált súgó jeleníti meg. Az automatikusan létrehozott súgó a parancs szintaxisát és használatára vonatkozó utasításokat tartalmaz a [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) parancsmagot, hogy a súgófájlok letöltéséhez.

Minden modul Szerző támogathat frissíthető súgó a modul. A modul tartalmazza a súgófájlok, és frissíthető súgó használja őket, vagy hagyja ki a súgófájlok és használja frissíthető súgó a telepítésükre. Frissíthető súgó támogatásával kapcsolatos további információkért lásd: [frissíthető súgó támogatása](https://go.microsoft.com/FWLink/?LinkID=242129) az MSDN webhelyen.

### <a name="enhanced-online-help"></a>Továbbfejlesztett Online súgó

Windows PowerShell online súgó az összes felhasználó számára értékes erőforrás, de különösen fontos a felhasználók számára, akik jelenleg vagy a frissített fájlokat nem lehet telepíteni.

Minden olyan Windows PowerShell-parancsmag online súgójának, írja be:

```
Get-Help <cmdlet-name> -Online
```

Windows PowerShell a Súgó-témakör online verzióját az alapértelmezett böngészőben nyílik meg.

A **Get-Help-Online** funkció a Windows PowerShell 3.0 azért most még hatékonyabb működését, még ha a parancsmag súgóját nincsenek telepítve a számítógépen. A **Get-Help-Online** funkció beolvasása az online súgó-témakörhöz tartozó URI-parancsmagok és a speciális funkciók HelpUri tulajdonságát.

```
PS C:\>(Get-Command Get-ScheduledJob).HelpUri
http://go.microsoft.com/fwlink/?LinkID=223923
```

Windows PowerShell 3.0-s készítői kezdve C# parancsmagok fel lehet tölteni a **HelpUri** létrehozásával tulajdonság egy **HelpUri** a parancsmag osztály attribútumot. Speciális funkciók készítői definiálhat egy **HelpUri** tulajdonsága a **CmdletBinding** attribútum. Értékét a **HelpUri** tulajdonság "http" vagy "https" kell kezdődnie.

Is használható egy **HelpUri** értéket az első kapcsolódó hivatkozásra egy XML-alapú parancsmag Súgó-fájl vagy a. Hivatkozás irányelv Megjegyzés-alapú segíthetnek a függvényt.

Online súgó támogatásával kapcsolatos további információkért lásd: [Online súgó támogatása](/powershell/developer/module/supporting-online-help) az a Microsoft Docs.

### <a name="cim-integration"></a>A CIM-integráció

Windows PowerShell 3.0 része a a Common Information Model (CIM), közös definíciók felügyeleti információkat biztosít a rendszerek, hálózatok, alkalmazások és szolgáltatások, amelyek az exchange felügyeleti információk között működve támogatása heterogén rendszerek. Parancsmag definíciójának XML-fájlok, a .NET-keretrendszer CIM támogatása alapján a Windows PowerShell 3.0, beleértve a Windows PowerShell-parancsmagok új vagy meglévő CIM-osztályokat, parancsok alapján hozzon létre CIM támogatása. API-t, a CIM-parancsmagok felügyeleti és 2.0-s WMI-szolgáltatók.

### <a name="session-configuration-files"></a>Munkamenet-konfigurációs fájlok

A Windows PowerShell 3.0-es verziótól kezdve fájl használatával egyéni munkamenet-konfigurációt is tervezhet. Az új munkamenet konfigurációs fájl lehetővé teszi annak a munkamenetek, amelyek a munkamenet-konfiguráció, melyik modulokat, parancsfájlok, beleértve a környezet és formátumú fájlok töltődnek be a munkameneteket, mely parancsmagok és a nyelvi elemei felhasználók használhatják, mely modulokat és parancsfájlokat lehet futtatni, és mely változókat is megtekinthetik.

Tervezhet egy munkamenetet, amely a felhasználók csak futtatni tudják a parancsmagok egy adott modulból, vagy a munkamenet, amelyben a felhasználók rendelkeznek speciális feladatokat elvégző parancsprogramok a hozzáférést, teljes nyelvi és elérhető minden modulokat.

Korábbi verzióiban a Windows PowerShell ezen a szinten vezérlő nem érhető el, csak azok számára, akik sikerült írni egy C# program vagy parancsfájl komplex indítási. Most már a számítógépen a Rendszergazdák csoport bármely tagja testre szabható egy munkamenet-konfiguráció egy konfigurációs fájl használatával.

Egy munkamenet-konfigurációs fájl létrehozásához használja a [New-PSSessionConfigurationFile](https://technet.microsoft.com/library/5f3e3633-6e90-479c-aea9-ba45a1954866) parancsmagot. A munkamenet-konfigurációs fájl alkalmazni egy munkamenet-konfigurációt, használja a [Register-PSSessionConfiguration](https://technet.microsoft.com/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) vagy [Set-PSSessionConfiguration](https://technet.microsoft.com/library/b21fbad3-1759-4260-b206-dcb8431cd6ea) parancsmagok.

További információkért lásd: [about_Session_Configuration_Files](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_session_configuration_files?view=powershell-5.0) és [New-PSSessionConfigurationFile](https://technet.microsoft.com/library/5f3e3633-6e90-479c-aea9-ba45a1954866).

### <a name="scheduled-jobs-and-task-scheduler-integration"></a>Ütemezett feladatok és a tevékenység Scheduler-integráció

Mostantól Windows PowerShell-háttérfeladatokkal ütemezheti és kezelheti azokat a Windows PowerShell és a Feladatütemező.

Ütemezett Windows PowerShell-feladatok a Feladatütemező feladatait és a Windows PowerShell-háttérfeladatokkal hasznos hibrid.

Például a Windows PowerShell-háttérfeladatokkal, ütemezett feladat aszinkron módon történik a háttérben futnak. Ütemezett, Befejezett feladatok példányait kezelheti a feladat parancsmagok használatával [a Start-Job](https://technet.microsoft.com/library/2bc04935-0deb-4ec0-b856-d7290cca6442) és [Get-Job](https://technet.microsoft.com/library/1352c534-7193-46ca-9ab1-0c5219a661ad).

Feladatütemező feladatait, mint az ütemezett feladatok futtatásához egy egyszeri vagy ismétlődő ütemezés szerint vagy egy műveletet vagy eseményre adott válaszként. Megtekintheti és kezelheti az ütemezett feladatok a Feladatütemezőben, engedélyezését és letiltását őket szükség esetén futtathatja őket vagy sablonként használni őket, és állítsa be a feltételeket, amelyek alapján a feladatok megkezdése.

Ütemezett feladatok emellett egy testre szabott őket kezelésére szolgáló parancsmagok készlete kapható. A parancsmag lehetővé teszi a létrehozása, szerkesztése, kezelése, tiltsa le, és engedélyezze újra az ütemezett feladatok, ütemezett feladat eseményindítók létrehozása és az ütemezett feladat beállításainak megadása.

Ütemezett feladatokkal kapcsolatos további információkért lásd: [about_Scheduled_Jobs](https://technet.microsoft.com/library/3b546629-703c-4939-b44f-52dd567bce92).

### <a name="windows-powershell-language-enhancements"></a>Windows PowerShell nyelvi fejlesztések

Windows PowerShell 3.0, a célt szolgálják, hogy a nyelvi egyszerűbb, könnyebben használja, és a gyakori hibák elkerülése érdekében számos funkciót tartalmaz. A fejlesztések közé tartoznak a tulajdonság enumerálása, darabszám és hossza tulajdonságok skaláris objektumok, új átirányító operátorok, a $Using hatókör-módosítót, PSItem automatikus változó, rugalmas parancsfájl formázását, változókat, egyszerűsített attribútum attribútumai argumentumok, numerikus nevek, a Stop-elemzés operátor, továbbfejlesztett tömb a felosztás, új bit operátorok, rendezett szótárak, PSCustomObject döntő és továbbfejlesztett Megjegyzés-alapú súgó.

### <a name="new-core-cmdlets"></a>Új fő parancsmagjainak

Új parancsmagokkal bővült a Windows PowerShell Core, többek között a parancsmagok leválasztott munkamenethez, a CIM-integráció és a frissíthető Súgó rendszer ütemezett feladatok kezeléséhez.

|||
|-|-|
|-JobTrigger|Új-JobTrigger|
|Connect-PSSession|New-PSSessionConfigurationFile|
|ConvertFrom-Json|New-PSTransportOption|
|ConvertTo-Json|New-PSWorkflowExecutionOption|
|Disable-JobTrigger|Új PSWorkflowSession|
|Disable-ScheduledJob|New-ScheduledJobOption|
|Disconnect-PSSession|New-WinEvent|
|Enable-JobTrigger|Receive-PSSession|
|Enable-ScheduledJob|Register-CimIndicationEvent|
|Get-CimAssociatedInstance|Register-ScheduledJob|
|Get-CimClass|Remove-CimInstance|
|Get-CimInstance|Remove-CimSession|
|Get-CimSession|Remove-TypeData|
|Get-ControlPanelItem|Rename-Computer|
|Get-IseSnippet|RESUME-Job|
|Get-JobTrigger|Save-Help|
|Get-ScheduledJob|Set-CimInstance|
|Get-ScheduledJobOption|Set-JobTrigger|
|Get-TypeData|Set-ScheduledJob|
|Import-IseSnippet|Set-ScheduledJobOption|
|Invoke-AsWorkflow|A parancs show|
|Invoke-CimMethod|Show-ControlPanelItem|
|Invoke-RestMethod|Suspend-Job|
|Invoke-WebRequest|Test-PSSessionConfigurationFile|
|New-CimInstance|Fájl letiltásának feloldása|
|New-CimSession|Unregister-ScheduledJob|
|New-CimSessionOption|Update-Help|
|New-IseSnippet||

### <a name="improvements-to-existing-core-cmdlets-and-providers"></a>Meglévő Core parancsmagok és szolgáltatók fejlesztései

Windows PowerShell 3.0 meglévő parancsmagjaihoz, beleértve az egyszerűsített szintaxis és a következő parancsmagok új paraméterei új szolgáltatásokat tartalmazza: Számítógépes parancsmagok, a fürt megosztott kötetei szolgáltatás parancsmagok, a Get-ChildItem, Get-Command, Get-tartalom, a Get-előzmények mérték-objektum, hálózatbiztonsági parancsmagok, Select-Object, Select-karakterlánc, osztott-elérési út, folyamatának elindítása, Tee-objektum, a Test-Connection tag hozzáadása és a WMI-parancsmagokat.

A Windows PowerShell-szolgáltatókat is is érdekében jelentős mértékben, beleértve a tanúsítványt a támogatott szolgáltatók a webalkalmazás üzemeltetéséhez Secure Socket Layer (SSL)-tanúsítványok kezeléséhez, támogatja a hitelesítő adatok állandó hálózati meghajtók és az alternatív adatstreamek fájlrendszer meghajtók.

### <a name="remote-module-import-and-discovery"></a>Távoli modul importálásához és felderítés

Windows PowerShell 3.0-modulok felderítése, importálása és a távoli számítógépeken lévő implicit távelérési képességek kiterjesztése. A modul parancsmagjai-modulok beszerzése távoli számítógépeken, és a modulok importálásához a helyi vagy távoli számítógépen a Windows PowerShell-távelérés használatával. Új CIM munkamenet támogatása lehetővé teszi, hogy a CIM és a WMI parancsok importálja a helyi számítógépen, amely implicit módon fut a távoli számítógépen nem Windows-számítógépek felügyeletére.

További információkért tekintse meg a Súgó-témaköröket a [Get-Module](https://technet.microsoft.com/library/2cccd4c4-9a21-4c77-b691-984ee57242e1) és [Import-Module](https://technet.microsoft.com/library/af616c24-e122-4098-930e-1e3ea2080ade) parancsmagok.

### <a name="enhanced-tab-completion"></a>Továbbfejlesztett kiegészítés

Kiegészítés a Windows PowerShell-konzol most befejezi a parancsmagok, paraméterek, paraméterértékeket, enumerálások, a .NET-keretrendszerek típusok, COM objektumok, rejtett könyvtár és további nevei. A lap kiegészítési funkció van teljesen írni egy új elemző és további forgatókönyvek, beleértve a memóriabeli elemzési fák és középvonal kiegészítés támogatása absztrakt szintaxis fa alapján.

### <a name="module-auto-loading"></a>A modul automatikus telepítéséhez

A [Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) parancsmag most olvas be az összes parancsmag és funkció a számítógépen telepített összes modul akkor is, ha a modul nem importálja az aktuális munkamenet.

A parancsmag kap, amikor ezzel azonnal kapcsolt modulok importálása nélkül. Windows PowerShell-modulok importálása most már automatikusan bármely parancsmag használatakor a modulban. Már nincs szüksége a modul keresheti ki és importálja azt a parancsmagok használatával.

A modulok automatikus importálása akkor aktiválódik, a parancsmag használatával egy parancsot a futó **Get-Command** nélkül helyettesítő karaktereket vagy futó parancsmag [Get-Help](https://technet.microsoft.com/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a) parancsmag helyettesítő karakterek nélkül.

Engedélyezze a, tiltsa le, majd konfigurálja az automatikus importálás modulok használatával a **$PSModuleAutoLoadingPreference** preferenciaváltozót.

További információkért lásd: [felügyelhető](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_modules?view=powershell-5.0), [about_Preference_Variables [v4]](https://technet.microsoft.com/library/31344314-be29-4286-b039-afa5460cbe8b), és a Súgó-témaköröket a [Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) és [Import-Module](https://technet.microsoft.com/library/af616c24-e122-4098-930e-1e3ea2080ade) parancsmagok.

### <a name="module-experience-improvements"></a>A modul környezetet eredményez

Windows PowerShell 3.0 speciális funkciók támogatása referenciaanyaga, beleértve a következő új funkciókat biztosít.

1. Egyes modulok (LogPipelineExecutionDetails) modul naplózásának és az új "A modul-naplózás a" csoportházirend-beállítás
2. A modul objektumok, amelyek teszik közzé az értékeket a moduljegyzékben kiterjesztett
3. Új **ExportedCommands** tulajdonság-modulok, beleértve a beágyazott modulok, amely ötvözi az összes típusú parancsok
4. Továbbfejlesztett felderítése érhető el (nem importált) modult, többek között, amely lehetővé teszi a **elérési útja** és **ListAvailable** ugyanazt a parancsot a paraméterek
5. Új **DefaultCommandPrefix** kulcs elkerülhetők a névütközések modul kódmódosítás nélkül a modul manifestech.
6. Továbbfejlesztett modul követelményeket, ideértve az teljes szükséges modulokat a verzió és a GUID Azonosítót és a szükséges modulok automatikus importálása
7. Csendesebb, zökkenőmentes működését az [New-ModuleManifest](https://technet.microsoft.com/library/512adced-f42f-4e88-ba7c-834fc9e5d047) parancsmagot.
8. Új **modul** paramétere #Requires
9. Továbbfejlesztett [Import-Module](https://technet.microsoft.com/library/af616c24-e122-4098-930e-1e3ea2080ade) parancsmagot mindkét **MinimumVersion** és **RequiredVersion** paramétereket.

### <a name="simplified-command-discovery"></a>Egyszerűsített parancsot felderítése

Nem kell többé felderíteni a parancsok a munkamenet számára elérhető összes modulok importálásához. A Windows PowerShell 3.0-ban a [Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) parancsmag minden parancs lekéri az összes telepített modulok. És a egy parancsot használja, ha a modul, amely a parancs exportálja automatikusan importálja a munkamenetbe.

Az új [Show-parancs](https://technet.microsoft.com/library/65bba50b-91a8-49d5-80a2-a30fc684ba41) parancsmag különösen a kezdők számára tervezték. Kereshet egy ablakban parancsokat. Összes parancs megtekintéséhez vagy a modul szűrheti, modul importálása a gombra kattintva, szövegmezők és a legördülő listák segítségével hozhat létre egy érvényes parancsot, és másolja, vagy futtassa a parancsot az ablak alkalmazáson.

### <a name="improved-logging-diagnostics-and-group-policy-support"></a>A továbbfejlesztett naplózás, a diagnosztikai és a csoport házirend támogatása

A naplózási és nyomkövetési esemény-nyomkövetés Windows (ETW)-naplókban, egy szerkeszthető támogatása a parancsok és a modulok támogatása javítja a Windows PowerShell 3.0 **LogPipelineExecutionDetails** modulokat, és a "kapcsolja be a modul tulajdonsága Naplózás"csoport házirend-beállítást. A napló részleteinek most már beszerezheti paraméterértékeket a napló tulajdonságainak megjelenítésével.

### <a name="formatting-and-output-improvements"></a>Formázás és a kimeneti fejlesztései

Új formázás és a kimeneti fejlesztései az összes Windows PowerShell-felhasználók hatékonyságának növelésére. A fejlesztések közé tartoznak a kimenet átirányítása, adatfolyamok összes, egy továbbfejlesztett Frissítéstípus parancsmag, amely dinamikusan Format.ps1xml fájlok, a kimenetben, a sortörés nélkül típusok egyéni objektumok formázási tulajdonságainak alapértelmezett hozzáadja a **PSCustomObject** típusa, továbbfejlesztett WMI-objektumok és a heterogén objektumokat, és a támogatási metódus túlterheléssel felderítéséhez formázása.

### <a name="enhanced-console-host-experience"></a>Továbbfejlesztett Konzolfelületet gazdagép

A Windows PowerShell-konzol gazdagép program Windows PowerShell 3.0 alapértelmezés szerint egyetlen szálon futó apartman beleértve az új szolgáltatásokkal rendelkezik. Az új "Futtatás a PowerShell" lehetőséget a Fájlkezelőben lehetővé teszi a szkriptek futtatása a nem korlátozott munkamenet csak a jobb gombbal kattintva. Új konzol gazdagép indítása logikai Windows PowerShell gyorsabban indul, és új betűtípusok lehetővé teszik a jól ismert console ablakban környezetének testreszabása.

További információkért lásd: [about_Run_With_PowerShell](https://technet.microsoft.com/library/c9d9ca5f-eff9-4409-be9d-e43b5b4087eb).

### <a name="new-cmdlet-and-hosting-apis"></a>Új parancsmag és az API-k üzemeltetéséhez

Az új parancsmag API és API-t üzemeltető tartalmazza a nyilvános speciális szintaktikai fa (AST-t) API-k és API-k folyamat lapozási, beágyazott folyamatok, futási térben készletek kiegészítés, Windows RT, a elavult parancsmag attribútum és a FunctionInfo objektum ige és főnév tulajdonságait.

### <a name="performance-improvements"></a>Teljesítménnyel kapcsolatos fejlesztések

Az új nyelvi elemző, a dinamikus futásidejű nyelv (DLR) a .NET-keretrendszer 4 épülő származnak teljesítményének jelentős növelése a Windows PowerShellben., valamint a futásidejű parancsfájl összeállításához, motor megbízhatóság fejlesztései és módosítása a az algoritmus a [Get-ChildItem](https://technet.microsoft.com/library/75cf79bb-4db6-4a67-8c36-3d20754e2190) , amely a teljesítmény javítása érdekében különösen akkor, ha a Keresés hálózati megosztások.

### <a name="runas-and-shared-host-support"></a>Futtató és a megosztott gazdagép támogatása

Windows PowerShell 3.0 tartalmazza a futtató és a Gazdagépcsoport megosztott funkciók támogatását.

A *RunAs* készült Windows PowerShell-munkafolyamat, a szolgáltatás lehetővé teszi, hogy a felhasználók egy munkamenet-konfiguráció, amely egy megosztott felhasználói fiók engedéllyel rendelkező-munkamenetek létrehozását. Ez lehetővé teszi, hogy kevesebb jogosultsággal rendelkező felhasználók adott parancsok és szkriptek futtatásához rendszergazdai jogosultságokkal, és csökkenti a kevésbé tapasztalt felhasználókat ad hozzá a Rendszergazdák csoport szükségességét.

A **SharedHost** funkció lehetővé teszi, hogy a több felhasználó egyidejűleg egy munkafolyamat-munkamenet csatlakozhat, és nyomon követheti a munkafolyamat több számítógépen. A felhasználók indítani egy munkafolyamatot egy számítógépen, és kapcsolódjon egy másik számítógépen, a munkafolyamat-munkamenetet az eredeti számítógépet a munkamenet leválasztása nélkül. A felhasználók ugyanazokkal az engedélyekkel kell rendelkeznie, és ugyanazt a munkamenet-konfigurációt használja. További információkért lásd: "Fut a Windows PowerShell-munkafolyamat" a Windows PowerShell-munkafolyamat – első lépések.

### <a name="special-character-handling-improvements"></a>Speciális karakter kezelési fejlesztések

Azon képessége, amely értelmezi és megfelelően kezeli a különleges karaktereket, a Windows PowerShell 3.0 javítása érdekében a **LiteralPath** paramétert, amely kezeli az elérési utakat speciális karaktereket, érvényességét, amelyek szinte minden parancsmag a egy  **Elérési út** paramétert, beleértve az új [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) és [Save-Help](https://technet.microsoft.com/library/aed94f90-b73f-4e25-a25d-7c18d9f161fa) parancsmagok. Az elemző is tartalmazza a használni kívánt szintaxiskiemelést karakter kezelésének javítása érdekében speciális logikát (\`) és fájl nevét és elérési utak szögletes zárójelben.

## <a name="see-also"></a>Lásd még:

- [about_Windows_PowerShell_5.0](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_windows_powershell_5.0?view=powershell-5.0)
- [Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=107116)
