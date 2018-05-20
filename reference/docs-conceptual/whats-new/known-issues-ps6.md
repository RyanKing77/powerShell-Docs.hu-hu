---
ms.date: 05/17/2018
keywords: PowerShell-core
title: PowerShell 6.0 kapcsolatos ismert problémák
ms.openlocfilehash: 6ad1bcaf1de06f204b57eb8ce23b3053ba4a5b38
ms.sourcegitcommit: 2d9cf1ccb9a653db7726a408ebcb65530dcb1522
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/19/2018
---
# <a name="known-issues-for-powershell-60"></a>PowerShell 6.0 kapcsolatos ismert problémák

## <a name="known-issues-for-powershell-on-non-windows-platforms"></a>A nem Windows platformokon PowerShell kapcsolatos ismert problémák

A Linux és macOS PowerShell alfa kiadásaiban többnyire működési, de néhány jelentős korlátozások és meghatározhatnak olyan használati problémákat rendelkezik. Linux PowerShell feloldja a béta és macOS működik, és alfa kiadások, mint stabil, de továbbra is lehetséges, hogy nem kell rendelkező egyes szolgáltatások készlete, és tartalmazhatnak hibák. Néhány esetben ezek a problémák egyszerűen a még nem lett még rögzített hibák. Más esetekben (például az alapértelmezett aliasok ls, cp, stb.), azt keres visszajelzés a Közösségtől kapcsolatban a választási lehetőségek biztosítjuk.

Megjegyzés: Több alapul szolgáló alrendszereket Hasonlóságok, mert a Linux és macOS PowerShell általában megosztani a lejárat, a szolgáltatások és a hibák azonos szinten. Kivéve az alábbi esetekben ebben a szakaszban a problémák mindkét típusú operációs rendszerekre vonatkozik.

### <a name="case-sensitivity-in-powershell"></a>A PowerShell Kisbetű/nagybetű megkülönböztetése

Hagyományosan PowerShell lett egységesen nem betűérzékeny, néhány kivétellel. A UNIX-operációs rendszerrel a fájlrendszer túlnyomórészt kis-és nagybetűket, és PowerShell megfelelő normál a fájlrendszer; Ez többféleképpen, nyilvánvaló, és nem egyértelmű keresztül kommunikál.

#### <a name="directly"></a>közvetlenül

- A fájl a PowerShellben megadásakor a kis-és nagybetűk kell használni.

#### <a name="indirectly"></a>Közvetve

- Ha a parancsfájl megpróbál egy modul betöltéséhez, és a modul neve nem cased megfelelően, akkor a modul betöltése sikertelen lesz. Ez meglévő parancsfájlok probléma okozhatja, ha a neve, amely szerint a modul hivatkozott nem egyezik a tényleges fájlnév.
- Kiegészítést rendszer nem automatikusan hajthat végre, ha a fájl neve eset nem megfelelő. A töredéke befejezéséhez cased megfelelően kell lennie. (A létrehozása után a típus neve és típusa tag befejezésekhez azonban nem.)

### <a name="ps1-file-extensions"></a>. PS1 Fájlkiterjesztések

PowerShell-parancsfájlok kell végződnie `.ps1` a értelmező hogyan tölthető be, és futtassa azokat az aktuális folyamat számára. A várt szokásos működése PowerShell parancsfájlok futtatásához a jelenlegi folyamatban. A `#!` varázsszáma fel az olyan parancsfájlt, amely nem rendelkezik egy `.ps1` bővítményt, de ez eredményezi a parancsfájl futtatásához megakadályozza a parancsfájl működő megfelelően Ha jelzések felcserélése objektumok új PowerShell-példányban. (Megjegyzés: Ez lehet a kívánt viselkedés, a PowerShell-parancsfájl végrehajtása közben `bash` vagy egy másik rendszerhéj.)

### <a name="missing-command-aliases"></a>Hiányzó parancs aliast

A Linux/macOS, az alapvető parancsok "kényelmi"-aliasok `ls`, `cp`, `mv`, `rm`, `cat`, `man`, `mount`, `ps` el lettek távolítva. A Windows PowerShell biztosít aliasok, amelyek a Linux parancs nevek felhasználó kényelmét szolgálja. Ezek aliasok a Linux/macOS azokat a terjesztéseket, így a natív végrehajtható fájl futtatását nélkül elérési út az alapértelmezett PowerShell el lettek távolítva.

Vannak előnyei és hátrányai ez tevékenységéhez. Az alias eltávolítása a PowerShell-felhasználó a natív parancs kezelését mutatja, de csökkenti a rendszerhéj funkciót, mert a natív parancsok visszaadnia az objektumok helyett.

> [!NOTE]
> Ez az egy olyan területre, ahol a PowerShell csapatának visszajelzés keres.
> Mi az az előnyben részesített megoldás? A Microsoft hagyja, vagy adja hozzá a kényelem aliasok vissza? Lásd: [#929 ki](https://github.com/PowerShell/PowerShell/issues/929).

### <a name="missing-wildcard-globbing-support"></a>Hiányzik a helyettesítő karakter (helyettesítés) támogatása

Jelenleg PowerShell csak nem helyettesítő bővítése (helyettesítés) beépített parancsmagok a Windows, és a külső parancsok vagy bináris fájljait és a Linux parancsmagok. Ez azt jelenti, hogy egy parancs hasonlóan `ls
*.txt` sikertelen lesz, mert a csillag a program nem bontja ki fájlnevek kereséséhez. Ön ezt úgy kerülheti ezzel `ls (gci *.txt | % name)` vagy egyszerűbb, `gci *.txt` a PowerShell beépített megfelelője használja `ls`.

Lásd: [#954](https://github.com/PowerShell/PowerShell/issues/954) visszajelzését a helyettesítés élmény, a Linux/macOS javítására.

### <a name="net-framework-vs-net-core-framework"></a>.NET-keretrendszer Visual Studio .NET Core-keretrendszer

A Linux/macOS PowerShell használja a .NET Core, amely a teljes .NET-keretrendszer Microsoft Windows részhalmaza. Ez azért fontos, mert a PowerShell közvetlen hozzáférést biztosít az alapul szolgáló keretrendszer típusok, módszerek, stb. Ennek eredményeképpen Windows rendszeren futó parancsfájlok futása nem nem Windows platformokon a keretrendszereket különbségek miatt. További információ a .NET Core-keretrendszer: <https://dotnetfoundation.org/net-core>

A megjelenésével [.NET-szabvány 2.0](https://blogs.msdn.microsoft.com/dotnet/2016/09/26/introducing-net-standard/), .NET Core 2.0 be fogja hozni a hagyományos típusok és módszerek a teljes .NET-keretrendszer jelen vissza. Ez azt jelenti, hogy PowerShell Core tudják betölteni sok hagyományos Windows PowerShell-modulok módosítás nélkül. A .NET szabványos 2.0 kapcsolódó munkaelem követésével [Itt](https://github.com/PowerShell/PowerShell/projects/4).

### <a name="redirection-issues"></a>Problémákat is

Bemeneti átirányítása bármilyen platformon nem támogatott a PowerShellben.
[A probléma #1629](https://github.com/PowerShell/PowerShell/issues/1629)

Használjon `Get-Content` fájl tartalmának írása bele a folyamatba.

Kimenet fogja tartalmazni az Unicode bájtsorrend (AJ), amikor az alapértelmezett UTF-8 kódolással szolgál. Az Anyagjegyzék problémákat okozhat, amelyek nem várt segédprogramok használatakor, vagy ha egy fájl hozzáfűzése. Használjon `-Encoding Ascii` (amelynek, nem lesznek Unicode, nem AJ) ASCII-szöveget írni. (Megjegyzés: lásd: [RFC0020](https://github.com/PowerShell/PowerShell-RFC/issues/71) visszajelzését a PowerShell Core minden platformon kódolási élményének javítása. Azt az UTF-8 támogatás nélkül AJ működik, és potenciálisan módosítása a különböző parancsmagok kódolási alapértelmezései különböző platformokon.)

### <a name="job-control"></a>Feladat-vezérlő

Nincs a PowerShellben Linux/macOS a feladat-vezérlő támogatás.
A `fg` és `bg` parancsok nem érhetők el.

Jelenleg, használhatja a [PowerShell feladatok](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_jobs) amelyek működnek a minden platformon.

### <a name="remoting-support"></a>Távelérésének jobb támogatása

Jelenleg PowerShell Core támogatja a PowerShell távoli eljáráshívás (PSRP) keresztül WSMan az egyszerű hitelesítéssel macOS és a Linux és a Linux NTLM-alapú hitelesítéssel. (Kerberos-alapú hitelesítés nem támogatott.)

A WSMan-alapú távoli eléréshez dolgozott a [psl-omi-szolgáltató](https://github.com/PowerShell/psl-omi-provider) tárházban.

PowerShell Core is támogatja a PowerShell távoli eljáráshívás (PSRP) SSH-n keresztül (a Windows, a macOS és a Linux) minden platformon. Amíg ez nem jelenleg támogatott éles környezetben, többet is megtudhat a beállításával kapcsolatos [Itt](../core-powershell/ssh-remoting-in-powershell-core.md).

### <a name="just-enough-administration-jea-support"></a>Most-elegendő-felügyeleti (JEA) támogatása

Korlátozott felügyelet (JEA) távoli eljáráshívási végpontok létrehozásának jelenleg nem áll rendelkezésre a Linux/macOS a PowerShellben. Ez a funkció jelenleg nem 6.0 hatókörébe, és valamit a Microsoft úgy tekinti, hogy post 6.0 mivel az jelentős tervezési munka.

### <a name="sudo-exec-and-powershell"></a>`sudo`, `exec`, és a PowerShell használatával

PowerShell használt parancsok többsége a memóriában fut (például a Python vagy Ruby), mert a sudo közvetlenül a PowerShell built-ins nem használhat. (Természetesen futtathatjuk `powershell` a sudo.) Ha a sudo, például a PowerShell belül egy PowerShell-parancsmag futtatásához szükséges `sudo Set-Date 8/18/2016`, akkor teheti meg `sudo powershell Set-Date 8/18/2016`. Hasonlóképpen nem lehet egy beépített PowerShell exec közvetlenül. Ehelyett kellene lennie ehhez `exec powershell item_to_exec`.

A probléma jelenleg követett #3232 részeként.

### <a name="missing-cmdlets"></a>Hiányzó parancsmagok

Nagyszámú általában használható a PowerShell parancsok (parancsmagok) a Linux/macOS nem érhetők el. Sok esetben ezek a parancsok célszerű nem ezek a rendszerek (például Windows-specifikus szolgáltatások, mint a beállításjegyzék). Egyéb parancsok, például a szolgáltatás parancsokat (Get/kezdő/Stop-Service) találhatók, de nem működik. Ezek a problémák kijavítása a nem működő parancsmagok és idővel újakat ad hozzá későbbi kiadásokban javíthatja ki.

### <a name="command-availability"></a>A parancs rendelkezésre állása

Az alábbi táblázat a parancsok, amelyek nem fog működni a Linux/macOS PowerShell ismert.

<table>
<th>Parancsok</th><th>Működési állapot</th><th>Megjegyzések</th>
<tr>
<td>Get-szolgáltatás, új szolgáltatás, indítsa újra a szolgáltatást, Resume-szolgáltatás, szolgáltatás beállítása, Start-Service, szolgáltatás leállítása, Suspend-szolgáltatás
<td>Nem érhető el.
<td>Ezek a parancsok nem azonosítható. Ez egy későbbi kiadásban javítani kell.
</tr>
<tr>
<td>Get-Acl, a Set-hozzáférés-vezérlési lista
<td>Nem érhető el.
<td>Ezek a parancsok nem azonosítható. Ez egy későbbi kiadásban javítani kell.
</tr>
<tr>
<td>Get-AuthenticodeSignature, a Set-AuthenticodeSignature
<td>Nem érhető el.
<td>Ezek a parancsok nem azonosítható. Ez egy későbbi kiadásban javítani kell.
</tr>
<tr>
<td>Várjon, amíg-folyamat
<td>Elérhető, nem működik megfelelően. <td>Például `Start-Process gvim -PassThru | Wait-Process` nem működik; várja meg a folyamat nem sikerül.
</tr>
<tr>
<td>Register-PSSessionConfiguration, Unregister-PSSessionConfiguration, Get-PSSessionConfiguration
<td>Rendelkezésre álló azonban nem működik.
<td>Ír egy hiba üzenet arról, hogy a parancsok nem működnek. Ezek az egy későbbi kiadásban javítani kell.
</tr>
<tr>
<td>Get-esemény, új esemény, a Register-EngineEvent, a Register-WmiEvent, Remove-esemény, Unregister-esemény
<td>Elérhető, de nincs eseményforrások érhetők el.
<td>A PowerShell esemény parancsok jelen van, de a parancsok (például System.Timers.Timer) használt eseményforrások többsége nem érhető el, így a parancsok a Alpha kiadásban használhatatlan Linux rendszeren.
</tr>
<tr>
<td>Set-ExecutionPolicy
<td>Rendelkezésre álló azonban nem működik.
<td>Visszaadja egy üzenetet megkapta ezen a platformon nem támogatott. Végrehajtási házirend a felhasználói tárgyalt "biztonsági", amely segítségével megakadályozhatja, hogy a felhasználó költséges vét. A biztonsági határ nincs.
</tr>
<tr>
<td>Új-PSSessionOption, új PSTransportOption
<td>Elérhető, de a New-PSSession nem működik.
<td>Új-PSSessionOption és a New-PSTransportOption jelenleg nem ellenőrzése működéséhez most, hogy a New-PSSession működik.
</tr>
</table>
