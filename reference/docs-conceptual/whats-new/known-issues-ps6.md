---
ms.date: 05/17/2018
keywords: PowerShell, a core
title: PowerShell 6.0 kapcsolatos ismert problémák
ms.openlocfilehash: e3e718be903ff2223064d5790d3d0fe554ef04cd
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268002"
---
# <a name="known-issues-for-powershell-60"></a>PowerShell 6.0 kapcsolatos ismert problémák

## <a name="known-issues-for-powershell-on-non-windows-platforms"></a>Ismert problémák PowerShell nem Windows platformokon

PowerShell a Linux és MacOS rendszeren alfa kiadásaiban többnyire működési, de rendelkezik néhány jelentős korlátozások és a használati problémákkal kapcsolatban. Béta verzióinak PowerShell Linux és macOS működési és alfa kiadások, mint stabil azonban továbbra is kell, hiányoznak bizonyos funkciók készletét, és a hibák is tartalmazhat. Bizonyos esetekben ezek olyan problémák, egyszerűen, amelyek még nem javított hibák. Más esetekben (mint az alapértelmezett aliasok ls, cp, stb.), a Microsoft által keresett visszajelzést kapcsolatban a választási lehetőségek arra a Közösségtől.

Megjegyzés: Miatt számos mögöttes alrendszerek Hasonlóságok, Linux és macOS PowerShell általában azonos szintű szolgáltatásai és a hibákat a lejárat megosztása. Kivéve az alábbi esetekben ebben a szakaszban a problémák mindkét típusú operációs rendszerekre vonatkozik.

### <a name="case-sensitivity-in-powershell"></a>Kisbetű/nagybetű megkülönböztetése a PowerShellben

PowerShell hagyományosan le lett egységesen kis-és nagybetűket, néhány kivétellel. A UNIX-hoz hasonló operációs rendszerek esetében a fájlrendszer az túlnyomórészt kis-és nagybetűket, és a PowerShell betartja a szabványt, a fájlrendszer; Ez számos módon, nyilvánvaló, és nem nyilvánvaló-n keresztül teszi közzé.

#### <a name="directly"></a>Közvetlenül

- Adjon meg egy fájlt a PowerShell, ha az megfelelő esetben kell használni.

#### <a name="indirectly"></a>Közvetett módon

- Ha a parancsfájl megpróbál betölt egy modult, és a modul neve nem kisbetűsek megfelelően, akkor a modul betöltése sikertelen lesz. Emiatt előfordulhat, hogy meglévő parancsfájlok probléma, ha a neve, amely hivatkozik a modul nem felel meg a tényleges fájlnév.
- Kiegészítés – a rendszer nem automatikus kiegészítés, ha a fájl neve szerepel. Fejezze be a kódrészletet megfelelően kell lennie kisbetűsek. (A befejezési a kis-és a típus neve és típusa tag befejezésekhez.)

### <a name="ps1-file-extensions"></a>. PS1 Fájlkiterjesztések

PowerShell-parancsfájlok végződése `.ps1` a értelmezője számára készült, megtudhatja, hogyan tölthet be és futtassa őket az aktuális folyamat számára. A várt szokásos működése PowerShell parancsfájlok futtatásához a jelenlegi folyamatban. A `#!` Magic Quadrant szám adható hozzá egy szkript, amely nem rendelkezik egy `.ps1` bővítményt, de ez a parancsfájl futtatásához egy új PowerShell-példányban meggátolja, hogy a parancsfájl működő megfelelően Ha objektumok felcserélésének okoz. (Megjegyzés: Ez lehet a kívánatos viselkedését, egy PowerShell-szkript végrehajtása közben `bash` vagy egy másik rendszerhéj.)

### <a name="missing-command-aliases"></a>Hiányzó parancsaliasok

Linux/MacOS-gépeken, az alapszintű parancsokat "csoportosított"-aliasok `ls`, `cp`, `mv`, `rm`, `cat`, `man`, `mount`, `ps` el lettek távolítva. Windows, a PowerShell biztosít aliasról, amelyek leképezése Linux parancsnevek felhasználói kényelmi célokat szolgál. Ezek az aliasok el lettek távolítva az alapértelmezett PowerShell Linux/MacOS rendszeren disztribúciókon, lehetővé téve a natív végrehajtható fájl futtatásához egy elérési út megadása nélkül.

Vannak, és ennek a hátrányai. Az aliasok tesz elérhetővé a natív parancs kezelését a PowerShell-felhasználó, de csökkenti a funkció a rendszerhéj, mert a natív parancsok karakterláncok helyett objektumokat adja vissza.

> [!NOTE]
> Ez az egy adott területre, ahol a PowerShell csapatának visszajelzést keres.
> Mi az az előnyben részesített megoldás? Hagyja, hogy azt, vagy adja hozzá a felhasználók kényelme érdekében aliasok vissza? Lásd: [#929 kiadása](https://github.com/PowerShell/PowerShell/issues/929).

### <a name="missing-wildcard-globbing-support"></a>Hiányzik a helyettesítő karakter (helyettesítés) támogatása

Jelenleg PowerShell csak hajtja végre helyettesítő bővítése (helyettesítés) a Windows beépített parancsmagokra, valamint a külső parancsok vagy bináris fájljainak, valamint parancsmagok Linux rendszeren. Ez azt jelenti, hogy egy parancs hasonlóan `ls
*.txt` sikertelen lesz, mert a csillag megfelelően fájlnevek nem lesznek kibontva. Megkerülheti a foglalkozások `ls (gci *.txt | % name)` vagy egyszerűbben `gci *.txt` használata a PowerShell beépített megfelelője `ls`.

Lásd: [#954](https://github.com/PowerShell/PowerShell/issues/954) visszajelzését Linux/MacOS rendszeren a helyettesítés élmény fejlesztéséhez.

### <a name="net-framework-vs-net-core-framework"></a>.NET-keretrendszer vagy Core .NET-keretrendszer

PowerShell a Linux/MacOS rendszeren használja a .NET Core, amely a teljes .NET-keretrendszer Microsoft Windows részhalmaza. Ez azért fontos, mert a PowerShell közvetlen hozzáférést biztosít az alapul szolgáló keretrendszer típusok, módszerekkel, stb. Ennek eredményeképpen Windows futtatott parancsfájlok, előfordulhat, hogy fut a nem Windows platformokon a keretrendszereket különbségek miatt. További információ a .NET Core-keretrendszer: <https://dotnetfoundation.org/net-core>

Létrejöttével [.NET Standard2.0](https://blogs.msdn.microsoft.com/dotnet/2016/09/26/introducing-net-standard/), .NET Core 2.0 tartalomtérkép vissza számos hagyományos típusok és módszerek a teljes .NET-keretrendszer szerepelnek. Ez azt jelenti, hogy a PowerShell Core tudják betölteni a sok hagyományos Windows PowerShell-modul módosítás nélkül. Kövesse a .NET Standard 2.0-s kapcsolódó munkahelyi [Itt](https://github.com/PowerShell/PowerShell/projects/4).

### <a name="redirection-issues"></a>Átirányítási hibáinak

A bemeneti átirányítás nem támogatott a PowerShellben bármilyen platformon.
[#1629 probléma](https://github.com/PowerShell/PowerShell/issues/1629)

Használat `Get-Content` egy fájl tartalmának írása a folyamatba.

Kimenet fogja tartalmazni a Unicode bájtsorrendjelző (AJ), amikor az alapértelmezett UTF-8 kódolást szolgál. Az Anyagjegyzék problémákat okozhat az nem várt segédprogramok használatakor, vagy ha egy fájl hozzáfűzése. Használat `-Encoding Ascii` ASCII szöveget (amely, nem a Unicode használatát, hogy nem kell AJ) írására.

> [!Note]
> Lásd: [RFC0020](https://github.com/PowerShell/PowerShell-RFC/issues/71) visszajelzését minden platformon a PowerShell Core a kódolási élmény javításáról. Hogy dolgozunk azon, hogy támogatja az UTF-8 AJ nélkül és potenciálisan módosítása a különböző parancsmagok kódolási alapértelmezései különböző platformokon.

### <a name="job-control"></a>Ellenőrzési feladat

A rendszer nem feladat-vezérlő támogatja, a Linux/MacOS rendszeren a PowerShellben.
A `fg` és `bg` parancsok nem érhetők el.

Jelenleg használhatja [PowerShell-feladatok](/powershell/module/microsoft.powershell.core/about/about_jobs) amely minden platformon működnek.

### <a name="remoting-support"></a>Távelérésének jobb támogatása

Jelenleg a PowerShell Core támogatja a PowerShell távoli eljáráshívás (PSRP) WSMan keresztül az alapszintű hitelesítés, macOS és Linux rendszeren és Linux rendszeren az NTLM-alapú hitelesítéssel. (A Kerberos-alapú hitelesítés nem támogatott.)

A WSMan-alapú távelérése alatt végezhető el a [psl omi-szolgáltató](https://github.com/PowerShell/psl-omi-provider) adattárat.

A PowerShell Core is támogatja a PowerShell távoli eljáráshívás (PSRP) ssh-n keresztül minden platformon (Windows, macOS és Linux). Miközben jelenleg nem támogatott éles környezetben, ez további információ a beállításra [Itt](../core-powershell/ssh-remoting-in-powershell-core.md).

### <a name="just-enough-administration-jea-support"></a>Csak-elegendő-felügyelet (JEA) támogatása

Korlátozott felügyelet (JEA) távoli eljáráshívás végpontok létrehozása jelenleg nem áll rendelkezésre a PowerShellben a Linux/MacOS rendszeren. Ez a funkció jelenleg nem terjed ki 6.0-s és valami azt fogja megfontolnia a post 6.0 kialakítása jelentős munkát igényel.

### <a name="sudo-exec-and-powershell"></a>`sudo`, `exec`, és a PowerShell használatával

Mivel a PowerShell parancsok többsége a memóriában (például Python vagy Ruby), a sudo közvetlenül a PowerShell built-ins nem használhat. (Természetesen futtathatjuk `powershell` a sudo.) Sudo, például a Powershellen belülről egy PowerShell-parancsmag futtatásához szükség esetén `sudo `Set-Date` 8/18/2016`, majd kellene tennie `sudo powershell `Set-Date` 8/18/2016`. Hasonlóképpen nem egy beépített PowerShell exec közvetlenül. Ehelyett meg kell tegye `exec powershell item_to_exec`.

A probléma jelenleg követett #3232 részeként.

### <a name="missing-cmdlets"></a>Hiányzó parancsmagok

Nagy számú rendszerint elérhető PowerShell parancsai (parancsmagok) a Linux/MacOS rendszeren nem érhetők el. Sok esetben ezek a parancsok van értelme nincs ezeken a platformokon (például Windows-specifikus szolgáltatások, mint például a beállításjegyzék). Egyéb parancsok, például a szolgáltatás parancsok (Get/Start/Stop-Service) találhatók, de nem működik. Jövőbeli kiadások fog kijavítani a hibákat, a nem működő parancsmagok javítása, és idővel újakat ad hozzá.

### <a name="command-availability"></a>A parancs rendelkezésre állása

A következő táblázat felsorolja az ismert, hogy nem működik a Linux/MacOS-gépeken a PowerShell-parancsok.

|Parancsok|Működési állapot|Megjegyzések|
|--------|-----------------|-----|
|`Get-Service`, `New-Service`, `Restart-Service`, `Resume-Service`, `Set-Service`, `Start-Service`, `Stop-Service`, `Suspend-Service`|Nem érhető el.|Ezeket a parancsokat a rendszer nem ismeri. Ez egy későbbi kiadásban rögzíteni kell.|
|`Get-Acl` és `Set-Acl` esetén|Nem érhető el.|Ezeket a parancsokat a rendszer nem ismeri. Ez egy későbbi kiadásban rögzíteni kell.|
|`Get-AuthenticodeSignature` és `Set-AuthenticodeSignature` esetén|Nem érhető el.|Ezeket a parancsokat a rendszer nem ismeri. Ez egy későbbi kiadásban rögzíteni kell.|
|`Wait-Process`|Elérhető, nem működik megfelelően. |Például "folyamatának elindítása gvim - PassThru | Nem működik a wait-Process'; Várjon, amíg a folyamat nem.|
|`Register-PSSessionConfiguration`, `Unregister-PSSessionConfiguration`, `Get-PSSessionConfiguration`|Elérhető, de nem működik.|Ír, egy üzenet, miszerint a parancsok nem működnek. Ezek egy későbbi kiadásban rögzíteni kell.|
|`Get-Event`, `New-Event`, `Register-EngineEvent`, `Register-WmiEvent`, `Remove-Event`, `Unregister-Event`|Elérhető, de nincs eseményforrások érhetők el.|A PowerShell-parancsok eseménykezelési jelen van, de a parancsok (például System.Timers.Timer) együttes eseményforrások többsége nem érhetők el Linux rendszerre, így a parancsok a Alpha kiadásban használhatatlan.|
|`Set-ExecutionPolicy`|Elérhető, de nem működik.|Ezen a platformon nem támogatott üzenetnek adja vissza. Végrehajtási házirend egy felhasználó témájú "biztonsági", amely segítségével megakadályozható, hogy a felhasználó költséges hibák. Akkor sem biztonsági határként.|
|`New-PSSessionOption` és `New-PSTransportOption` esetén|Rendelkezésre álló de `New-PSSession` nem működik.|`New-PSSessionOption` és `New-PSTransportOption` jelenleg nem ellenőrzi, hogy már működik `New-PSSession` működik.|