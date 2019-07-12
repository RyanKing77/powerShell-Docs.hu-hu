---
ms.date: 05/17/2018
keywords: PowerShell, a core
title: PowerShell 6.0 használhatatlanná tévő változásai
ms.openlocfilehash: 186e55c1ac46ce3fc172df18995f8c15d9eeb8eb
ms.sourcegitcommit: 09f02ccef56ef30e7a9ca901f8d3713724960c68
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843941"
---
# <a name="breaking-changes-for-powershell-60"></a>PowerShell 6.0 használhatatlanná tévő változásai

## <a name="features-no-longer-available-in-powershell-core"></a>A funkciók már nem érhető el, a PowerShell Core

### <a name="powershell-workflow"></a>PowerShell-munkafolyamat

[PowerShell-munkafolyamat][workflow] is a feature in Windows PowerShell that builds on top of [Windows Workflow Foundation (WF)][workflow-foundation] , amely lehetővé teszi a hosszan futó vagy párhuzamos feladatok hatékony runbookok létrehozása.

A Windows Workflow Foundation a .NET Core támogatása hiánya miatt nem folytatjuk a PowerShell Core a PowerShell-munkafolyamat támogatásához.

A későbbiekben szeretnénk natív PowerShell-munkafolyamat nélkül PowerShell nyelven párhuzamosság/egyidejűségi engedélyezéséhez.

[workflow]: https://docs.microsoft.com/powershell/scripting/core-powershell/workflows-guide
[workflow-foundation]: https://docs.microsoft.com/dotnet/framework/windows-workflow-foundation/

### <a name="custom-snap-ins"></a>Egyéni beépülő modulok

[PowerShell beépülő modulok][snapin] vannak a megelőző, a PowerShell-modulokat, amelyek nem rendelkeznek széles körű bevezetési a PowerShell-Közösségben.

A beépülő modulok és használati hiánya miatt a közösségi összetettsége miatt már nem támogatott egyéni beépülő modulokat a PowerShell Core.

Jelenleg ez megszünteti a `ActiveDirectory` és `DnsClient` modulok a Windows és Windows Server.

[snapin]: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_pssnapins

### <a name="wmi-v1-cmdlets"></a>A WMI v1-parancsmagok

WMI-alapú modulok két csoportját támogató összetettsége miatt a WMI v1-parancsmagok a PowerShell Core eltávolítottuk:

- `Get-WmiObject`
- `Invoke-WmiMethod`
- `Register-WmiEvent`
- `Set-WmiInstance`

Ehelyett azt javasoljuk, hogy Ön a (más néven WMI v2) CIM-parancsmagok, amelyek ugyanazt a funkcionalitást biztosítják rendelkező új funkciókat és a egy áttervezett szintaxis használata:

- `Get-CimAssociatedInstance`
- `Get-CimClass`
- `Get-CimInstance`
- `Get-CimSession`
- `Invoke-CimMethod`
- `New-CimInstance`
- `New-CimSession`
- `New-CimSessionOption`
- `Register-CimIndicationEvent`
- `Remove-CimInstance`
- `Remove-CimSession`
- `Set-CimInstance`

### <a name="microsoftpowershelllocalaccounts"></a>Microsoft.PowerShell.LocalAccounts

Nem támogatott API-k használata miatt `Microsoft.PowerShell.LocalAccounts` el lett távolítva a PowerShell Core mindaddig, amíg egy jobb megoldás található.

### <a name="-computer-cmdlets"></a>`*-Computer` Parancsmagok

Nem támogatott API-k használatát, mert a következő parancsmagokat el lettek távolítva a PowerShell Core mindaddig, amíg egy jobb megoldás található.

- Add-Computer
- Checkpoint-Computer
- Remove-Computer
- Visszaállítás – számítógép

### <a name="-counter-cmdlets"></a>`*-Counter` Parancsmagok

Nem támogatott API-k használata miatt a `*-Counter` el lett távolítva a PowerShell Core mindaddig, amíg egy jobb megoldás található.

### <a name="-eventlog-cmdlets"></a>`*-EventLog` Parancsmagok

Nem támogatott API-k használata miatt a `*-EventLog` a PowerShell Core el lett távolítva. amíg nem jobb megoldás található. `Get-WinEvent` és `Create-WinEvent` érhetők el, és a Windows eseményeket létrehozásához.

## <a name="enginelanguage-changes"></a>Összetevő/nyelvi változások

### <a name="rename-powershellexe-to-pwshexe-5101httpsgithubcompowershellpowershellissues5101"></a>Nevezze át `powershell.exe` való `pwsh.exe` [#5101](https://github.com/PowerShell/PowerShell/issues/5101)

Annak érdekében, hogy a felhasználóknak engedélyezi a Windows (ellentétben a Windows PowerShell) a PowerShell Core meghívásához determinisztikus módon, a PowerShell Core bináris módosult a `pwsh.exe` a Windows és `pwsh` nem Windows platformokon.

Akkor használhatja rövidített nevét is – nem Windows platformokon ismertetése az elnevezési összhangban.

### <a name="dont-insert-line-breaks-to-output-except-for-tables-5193httpsgithubcompowershellpowershellissues5193"></a>Ne szúrjon be a sortörések (kivéve a táblák) kimeneti [#5193](https://github.com/PowerShell/PowerShell/issues/5193)

Korábban a szélességét, a konzol kimenete lett igazítva, és sortörések, azaz a kimenet nem get újraformázta várható, ha a terminálon lett méretezve, a konzol tartomány zárószélessége lettek hozzáadva. Ez a változás nem alkalmazták táblákat, a sortörések az oszlopokat, igazítva, szükség szerint.

### <a name="skip-null-element-check-for-collections-with-a-value-type-element-type-5432httpsgithubcompowershellpowershellissues5432"></a>Hagyja ki a gyűjteményeket, amelyek egy értéktípus elem típusa null-elem keresése [#5432](https://github.com/PowerShell/PowerShell/issues/5432)

Az a `Mandatory` paraméter és `ValidateNotNull` és `ValidateNotNullOrEmpty` attribútumok, az elemhez null-ellenőrzés kihagyása, ha a gyűjtemény elem típusa typ hodnoty.

### <a name="change-outputencoding-to-use-utf-8-nobom-encoding-rather-than-ascii-5369httpsgithubcompowershellpowershellissues5369"></a>Változás `$OutputEncoding` használandó `UTF-8 NoBOM` ASCII helyett kódolás [#5369](https://github.com/PowerShell/PowerShell/issues/5369)

Az előző kódolással, ASCII (7 bites), a kimenet bizonyos esetekben helytelen lapjával eredményez. Ez a változás, hogy `UTF-8 NoBOM` alapértelmezett, amely Unicode kimeneti megőrzi a legtöbb eszközöket és operációs rendszerek által támogatott kódolást.

### <a name="remove-allscope-from-most-default-aliases-5268httpsgithubcompowershellpowershellissues5268"></a>Távolítsa el `AllScope` a legtöbb alapértelmezett aliasok [#5268](https://github.com/PowerShell/PowerShell/issues/5268)

Hatókör létrehozása, felgyorsítása érdekében `AllScope` legtöbb alapértelmezett aliasok el lett távolítva. `AllScope` maradt néhány gyakran használt aliasok ahol a keresési gyorsabb lett.

### <a name="-verbose-and--debug-no-longer-overrides-erroractionpreference-5113httpsgithubcompowershellpowershellissues5113"></a>`-Verbose` és `-Debug` már nem felülbírálások `$ErrorActionPreference` [#5113](https://github.com/PowerShell/PowerShell/issues/5113)

Korábban Ha `-Verbose` vagy `-Debug` van megadva, akkor overrode viselkedését `$ErrorActionPreference`. Ezzel `-Verbose` és `-Debug` már nem befolyásolja a működését `$ErrorActionPreference`.

## <a name="cmdlet-changes"></a>Parancsmag módosításai

### <a name="invoke-restmethod-doesnt-return-useful-info-when-no-data-is-returned-5320httpsgithubcompowershellpowershellissues5320"></a>Meghívása RestMethod nem ad vissza hasznos információ, ha nem ad vissza. [#5320](https://github.com/PowerShell/PowerShell/issues/5320)

Ha egy API-t csak adja vissza `null`, Invoke-RestMethod szerializálása volt ez a karakterlánc `"null"` helyett `$null`. Ez a változás javítja a logika `Invoke-RestMethod` megfelelően szerializálni az egyetlen érvényes érték JSON `null` szöveges `$null`.

### <a name="remove--protocol-from--computer-cmdlets-5277httpsgithubcompowershellpowershellissues5277"></a>Távolítsa el `-Protocol` a `*-Computer` parancsmagok [#5277](https://github.com/PowerShell/PowerShell/issues/5277)

RPC-táveléréssel CoreFX (különösen a nem Windows platformokon) és a egy egységes távelérése a PowerShellben, biztosítva a problémák miatt a `-Protocol` paraméter el lett távolítva a `\*-Computer` parancsmagok. A DCOM már nem támogatott a távelérése. A következő parancsmagokat csak a wsman által használt távoli eljáráshívás támogatják:

- Rename-Computer
- Számítógép újraindítása
- Stop-Computer

### <a name="remove--computername-from--service-cmdlets-5090httpsgithubcompowershellpowershellissues5094"></a>Távolítsa el `-ComputerName` a `*-Service` parancsmagok [#5090](https://github.com/PowerShell/PowerShell/issues/5094)

Annak érdekében, hogy PSRP, konzisztens használatát javasoljuk a `-ComputerName` paraméter el lett távolítva `*-Service` parancsmagok.

### <a name="fix-get-item--literalpath-ab-if-ab-doesnt-actually-exist-to-return-error-5197httpsgithubcompowershellpowershellissues5197"></a>Javítsa ki `Get-Item -LiteralPath a*b` Ha `a*b` ténylegesen nem létezik, hibaüzenetet ad vissza [#5197](https://github.com/PowerShell/PowerShell/issues/5197)

Korábban a `-LiteralPath` helyettesítő karakter a megadott szeretné kezelni, azonos `-Path` , és ha a helyettesítő karakter található fájlokat, a lenne csendes kilép. Megfelelő viselkedését kell lennie, amely `-LiteralPath` egy egyszerű érték, ha a fájl nem létezik, hibát kell végrehajtania. Változás az, hogy kezelje a helyettesítő karakterek használják `-Literal` szerint szövegkonstans.

### <a name="import-csv-should-apply-pstypenames-upon-import-when-type-information-is-present-in-the-csv-5134httpsgithubcompowershellpowershellissues5134"></a>`Import-Csv` a alkalmazni kell `PSTypeNames` típussal kapcsolatos információk esetén a Megosztott fürtköteten importálását követően [#5134](https://github.com/PowerShell/PowerShell/issues/5134)

Korábban az exportált objektumokat használatával `Export-CSV` a `TypeInformation` együtt importálja `ConvertFrom-Csv` nem lett megőrizve a típussal kapcsolatos információk. Ez a módosítás hozzáadja a típussal kapcsolatos információk a `PSTypeNames` tag ha rendelkezésre áll a CSV-fájlból.

### <a name="-notypeinformation-should-be-default-on-export-csv-5131httpsgithubcompowershellpowershellissues5131"></a>`-NoTypeInformation` alapértelmezett kell lennie a `Export-Csv` [#5131](https://github.com/PowerShell/PowerShell/issues/5131)

Ezt a módosítást hajtottak végre a alapértelmezett viselkedését, az ügyfélvisszajelzésekre `Export-CSV` típus információval.

Korábban a parancsmag lenne a kimeneti megjegyzést, az első sor tartalmazza az objektum nevét. A módosítás, akkor nem tudja értelmezni a legtöbb eszközök letiltásához ez alapértelmezés szerint. Használat `-IncludeTypeInformation` megőrzi a korábbi működése.

### <a name="web-cmdlets-should-warn-when--credential-is-sent-over-unencrypted-connections-5112httpsgithubcompowershellpowershellissues5112"></a>Webes parancsmagok figyelmeztetnek, ha `-Credential` titkosítatlan kapcsolaton keresztül zajlik [#5112](https://github.com/PowerShell/PowerShell/issues/5112)

HTTP használata esetén a tartalmat, beleértve a jelszavak tiszta szövegként érkeznek. Ez a változás, hogy nem engedélyezze ez alapértelmezés szerint, és hibát adhat vissza, ha az nem biztonságos módon, hogy átadta a hitelesítő adatok. Felhasználók használatával elkerülheti ezt a `-AllowUnencryptedAuthentication` váltani.

## <a name="api-changes"></a>API-módosítás

### <a name="remove-addtypecommandbase-class-5407httpsgithubcompowershellpowershellissues5407"></a>Távolítsa el `AddTypeCommandBase` osztály [#5407](https://github.com/PowerShell/PowerShell/issues/5407)

A `AddTypeCommandBase` osztály el lett távolítva `Add-Type` teljesítmény javítása érdekében. Ez az osztály csak az Add-Type parancsmagot használja, és a felhasználók nem érinti.

### <a name="unify-cmdlets-with-parameter--encoding-to-be-of-type-systemtextencoding-5080httpsgithubcompowershellpowershellissues5080"></a>Használja őket egységes előtérrendszerként paraméterrel parancsmagok `-Encoding` típusú `System.Text.Encoding` [#5080](https://github.com/PowerShell/PowerShell/issues/5080)

A `-Encoding` érték `Byte` a fájlrendszer-szolgáltató parancsmagjai el lett távolítva. Egy új paraméter `-AsByteStream`, most azt adhatja meg, hogy egy bájt stream szükség, mint bemenet vagy az, hogy a kimenet a stream bájt.

### <a name="add-better-error-message-for-empty-and-null--uformat-parameter-5055httpsgithubcompowershellpowershellissues5055"></a>Jobb hibaüzenet üres és null hozzáadása `-UFormat` paraméter [#5055](https://github.com/PowerShell/PowerShell/issues/5055)

Korábban, ha átadja egy üres formázó karakterlánc `-UFormat`, unhelpful hibaüzenet jelent. A kifejezőbb hiba lett hozzáadva.

### <a name="clean-up-console-code-4995httpsgithubcompowershellpowershellissues4995"></a>Távolítsa el a konzol kód [#4995](https://github.com/PowerShell/PowerShell/issues/4995)

A következő szolgáltatások eltávolítása nem támogatott a PowerShell Core, és nem is léteznek régi okokból Windows PowerShell-támogatás hozzáadása tervezzük: `-psconsolefile` kapcsoló és a kódot, `-importsystemmodules` kapcsoló és a kódot, és a betűtípus módosítása a kódot.

### <a name="removed-runspaceconfiguration-support-4942httpsgithubcompowershellpowershellissues4942"></a>Eltávolított `RunspaceConfiguration` támogatja [#4942](https://github.com/PowerShell/PowerShell/issues/4942)

Korábban a programozott módon a PowerShell futási térben létrehozásakor az API-val is használhat a régebbi [ `RunspaceConfiguration` ][runspaceconfig] or the newer [`InitialSessionState`][iss]. Ez a változás nem támogatja az `RunspaceConfiguration` , és csak támogatja `InitialSessionState`.

[runspaceconfig]: https://docs.microsoft.com/dotnet/api/system.management.automation.runspaces.runspaceconfiguration
[iss]: https://docs.microsoft.com/dotnet/api/system.management.automation.runspaces.initialsessionstate

### <a name="commandinvocationintrinsicsinvokescript-bind-arguments-to-input-instead-of-args-4923httpsgithubcompowershellpowershellissues4923"></a>`CommandInvocationIntrinsics.InvokeScript` argumenty kötési `$input` helyett `$args` [#4923](https://github.com/PowerShell/PowerShell/issues/4923)

Egy paraméter helytelen pozícióját az átadott argumentum, helyett bemeneti argumentum eredményezett.

### <a name="remove-unsupported--showwindow-switch-from-get-help-4903httpsgithubcompowershellpowershellissues4903"></a>Távolítsa el a nem támogatott `-showwindow` átállás `Get-Help` [#4903](https://github.com/PowerShell/PowerShell/issues/4903)

`-showwindow` WPF-, amely nem támogatott coreclr-nek a támaszkodik.

### <a name="allow--to-be-used-in-registry-path-for-remove-item-4866httpsgithubcompowershellpowershellissues4866"></a>Lehetővé teszi * beállításjegyzékbeli elérési út a használandó `Remove-Item` [#4866](https://github.com/PowerShell/PowerShell/issues/4866)

Korábban a `-LiteralPath` helyettesítő karakter a megadott szeretné kezelni, azonos `-Path` , és ha a helyettesítő karakter található fájlokat, a lenne csendes kilép. Megfelelő viselkedését kell lennie, amely `-LiteralPath` egy egyszerű érték, ha a fájl nem létezik, hibát kell végrehajtania. Változás az, hogy kezelje a helyettesítő karakterek használják `-Literal` szerint szövegkonstans.

### <a name="fix-set-service-failing-test-4802httpsgithubcompowershellpowershellissues4802"></a>Javítsa ki `Set-Service` sikertelen teszt [#4802](https://github.com/PowerShell/PowerShell/issues/4802)

Korábban Ha `New-Service -StartupType foo` használták, `foo` figyelmen kívül lett hagyva, és a szolgáltatás néhány alapértelmezett indítási típus lett létrehozva. Ez a változás, hogy explicit módon throw egy érvénytelen indítási típus hiba.

### <a name="rename-isosx-to-ismacos-4700httpsgithubcompowershellpowershellissues4700"></a>Nevezze át `$IsOSX` való `$IsMacOS` [#4700](https://github.com/PowerShell/PowerShell/issues/4700)

A PowerShellben elnevezési kell konzisztensek legyenek a kiosztási és felelnek meg az Apple OSX helyett macOS használatát. Azonban az olvashatóság érdekében és következetesen azt tartózkodó Pascal a kis-és nagybetűhasználatot.

### <a name="make-error-message-consistent-when-invalid-script-is-passed-to--file-better-error-when-passed-ambiguous-argument-4573httpsgithubcompowershellpowershellissues4573"></a>Győződjön meg arról, hibaüzenet jelenik meg konzisztens amikor átadott érvénytelen parancsprogram-fájlt, a hiba, ha a nem egyértelmű argumentum jobb [#4573](https://github.com/PowerShell/PowerShell/issues/4573)

Módosítsa a kilépési kódot `pwsh.exe` igazodva Unix konvenciók

### <a name="removal-of-localaccount-and-cmdlets-from--diagnostics-modules-4302httpsgithubcompowershellpowershellissues4302-4303httpsgithubcompowershellpowershellissues4303"></a>Eltávolításának `LocalAccount` és parancsmagjait `Diagnostics` modulok. [#4302](https://github.com/PowerShell/PowerShell/issues/4302) [#4303](https://github.com/PowerShell/PowerShell/issues/4303)

Nem támogatott API-kat, mert a `LocalAccounts` modul és a `Counter` parancsmagok a a `Diagnostics` modul el lettek távolítva, amíg nem jobb megoldás található.

### <a name="executing-powershell-script-with-bool-parameter-does-not-work-4036httpsgithubcompowershellpowershellissues4036"></a>Logikai paraméter a PowerShell-parancsprogram futtatása nem működik [#4036](https://github.com/PowerShell/PowerShell/issues/4036)

Korábban, a **powershell.exe** (mostantól **pwsh.exe**) végrehajtásához egy PowerShell szkriptet az `-File` semmilyen módon nem lehet átadni megadott `$true` / `$false` paraméterként értékek. Támogatja a `$true` / `$false` elemzett értékeket a paraméterekhez hozzá lett adva. Kapcsoló értékeket is támogatottak, ahogy jelenleg dokumentált szintaxis nem működik.

### <a name="remove-clrversion-property-from-psversiontable-4027httpsgithubcompowershellpowershellissues4027"></a>Távolítsa el `ClrVersion` tulajdonságot `$PSVersionTable` [#4027](https://github.com/PowerShell/PowerShell/issues/4027)

A `ClrVersion` tulajdonságát `$PSVersionTable` van coreclr-nek nem használható, a végfelhasználók kell nem használja ezt az értéket a kompatibilitás meghatározása.

### <a name="change-positional-parameter-for-powershellexe-from--command-to--file-4019httpsgithubcompowershellpowershellissues4019"></a>Módosítsa a Helyzetbeállító paramétere `powershell.exe` a `-Command` való `-File` [#4019](https://github.com/PowerShell/PowerShell/issues/4019)

A nem Windows platformokon shebangje határoz meg PowerShell használatának engedélyezése. Ez azt jelenti, hogy a Unix-alapú rendszerek esetében szeretné meghívni a PowerShell parancsfájl végrehajtható teheti automatikusan ahelyett, hogy explicit módon meghívása `pwsh`. Ez azt is jelenti, hogy most már elvégezhető többek között `powershell foo.ps1` vagy `powershell fooScript` megadása nélkül `-File`. Azonban ez a változás most megköveteli, hogy Ön kifejezetten megad `-c` vagy `-Command` többek között a tett kísérlet során `powershell.exe Get-Command`.

### <a name="implement-unicode-escape-parsing-3958httpsgithubcompowershellpowershellissues3958"></a>Unicode escape-elemzés megvalósítása [#3958](https://github.com/PowerShell/PowerShell/issues/3958)

`` `u####`` vagy `` `u{####}`` megfelelő Unicode-karaktert alakítja át. A kimenetben szövegkonstans `` `u``, a használni kívánt szintaxiskiemelést escape: ``` ``u```.

### <a name="change-new-modulemanifest-encoding-to-utf8nobom-on-non-windows-platforms-3940httpsgithubcompowershellpowershellissues3940"></a>Változás `New-ModuleManifest` kódolási `UTF8NoBOM` nem Windows platformokon [#3940](https://github.com/PowerShell/PowerShell/issues/3940)

Korábban a `New-ModuleManifest` psd1 kiterjesztésű jegyzékek létrehoz az UTF-16-AJ, Linux rendszerű eszközök kerülni létrehozásával. Ez használhatatlanná tévő változás módosítja a kódolását `New-ModuleManifest` UTF (nincs AJ) kell a nem Windows platformokon.

### <a name="prevent-get-childitem-from-recursing-into-symlinks-1875-3780httpsgithubcompowershellpowershellissues3780"></a>Megakadályozása `Get-ChildItem` származó be symlinks recursing (#1875). [#3780](https://github.com/PowerShell/PowerShell/issues/3780)

Ez a változás csökkenti a `Get-ChildItem` Unix megfelelően további `ls -r` és a Windows `dir /s` natív parancsokat. Az említett parancsokat, mint például a parancsmag jeleníti meg a szimbolikus hivatkozásokat a rekurzió során találhatók címtárak, de nem recurse be őket.

### <a name="fix-get-content--delimiter-to-not-include-the-delimiter-in-the-returned-lines-3706httpsgithubcompowershellpowershellissues3706"></a>Javítsa ki `Get-Content -Delimiter` nem tartalmazza a kivonni kívánt a visszaadott sorok [#3706](https://github.com/PowerShell/PowerShell/issues/3706)

Korábban, a kimeneti használata során `Get-Content -Delimiter` inkonzisztens és kényelmetlen lehet, ahogy ez szükséges az elválasztó karakter eltávolítása az adatok további feldolgozás céljából. Ez a változás a elválasztó eltávolítja a visszaadott sorok.

### <a name="implement-format-hex-in-c-3320httpsgithubcompowershellpowershellissues3320"></a>Hexadecimális formátumban, a megvalósítása C# [#3320](https://github.com/PowerShell/PowerShell/issues/3320)

A `-Raw` paraméter már "műveletvégzés" (abban, hogy ezt nem semmi sem). Módosítástól minden, a kimenet jelenik meg, amely tartalmazza az összes ehhez a típushoz a bájtok számok igaz reprezentációját (Mi a `-Raw` paraméter hivatalosan ennek során ez a módosítás előtt).

### <a name="powershell-as-a-default-shell-doesnt-work-with-script-command-3319httpsgithubcompowershellpowershellissues3319"></a>Egy alapértelmezett rendszerhéját, PowerShell-parancsprogram-utasítás nem működik [#3319](https://github.com/PowerShell/PowerShell/issues/3319)

A Unix és a egy fogadására parancsikonja egyezmény `-i` az interaktív shell és a számos eszköz Ez a viselkedés várható (`script` például és beállítása a PowerShell, az alapértelmezett rendszerhéját) és a rendszerhéj-meghívja a `-i` váltson. Ez a változás, amely a megsérti `-i` korábban volt használható rövid aktuális megfelelően `-inputformat`, így kell lennie `-in`.

### <a name="typo-fix-in-get-computerinfo-property-name-3167httpsgithubcompowershellpowershellissues3167"></a>Elírta javítása a Get-ComputerInfo tulajdonságnév [#3167](https://github.com/PowerShell/PowerShell/issues/3167)

`BiosSerialNumber` lett írva `BiosSeralNumber` és helyesen van beállítva.

### <a name="add-get-stringhash-and-get-filehash-cmdlets-3024httpsgithubcompowershellpowershellissues3024"></a>Adjon hozzá `Get-StringHash` és `Get-FileHash` parancsmagok [#3024](https://github.com/PowerShell/PowerShell/issues/3024)

Ez a változás, hogy néhány kivonatoló algoritmusok CoreFX által nem támogatott, ezért azok már nem érhetők el:

- `MACTripleDES`
- `RIPEMD160`

### <a name="add-validation-on-get--cmdlets-where-passing-null-returns-all-objects-instead-of-error-2672httpsgithubcompowershellpowershellissues2672"></a>Ellenőrzés bekapcsolása `Get-*` parancsmagok, ahol passing $null adja vissza a hiba helyett az összes objektum [#2672](https://github.com/PowerShell/PowerShell/issues/2672)

Átmenő `$null` valamelyik a következő egyelőre hibát jelez:

- `Get-Credential -UserName`
- `Get-Event -SourceIdentifier`
- `Get-EventSubscriber -SourceIdentifier`
- `Get-Help -Name`
- `Get-PSBreakpoint -Script`
- `Get-PSProvider -PSProvider`
- `Get-PSSessionConfiguration -Name`
- `Get-PSSnapin -Name`
- `Get-Runspace -Name`
- `Get-RunspaceDebug -RunspaceName`
- `Get-Service -Name`
- `Get-TraceSource -Name`
- `Get-Variable -Name`
- `Get-WmiObject -Class`
- `Get-WmiObject -Property`

### <a name="add-support-w3c-extended-log-file-format-in-import-csv-2482httpsgithubcompowershellpowershellissues2482"></a>Adja hozzá a W3C bővített naplófájlformátum az támogatási `Import-Csv` [#2482](https://github.com/PowerShell/PowerShell/issues/2482)

Korábban a `Import-Csv` parancsmag nem használható közvetlenül importálhat a W3C bővített naplóformátumban naplófájlokat, és további művelet lenne szükséges. Ez a változás a W3C bővített naplóformátumban támogatott.

### <a name="parameter-binding-problem-with-valuefromremainingarguments-in-ps-functions-2035httpsgithubcompowershellpowershellissues2035"></a>Paraméter kötés problémájára `ValueFromRemainingArguments` a PS-függvények [#2035](https://github.com/PowerShell/PowerShell/issues/2035)

`ValueFromRemainingArguments` most adja vissza az értékeket egy tömbként helyett egy érték osztályon van egy tömb.

### <a name="buildversion-is-removed-from-psversiontable-1415httpsgithubcompowershellpowershellissues1415"></a>`BuildVersion` eltávolítják az `$PSVersionTable` [#1415](https://github.com/PowerShell/PowerShell/issues/1415)

Távolítsa el a `BuildVersion` tulajdonságot `$PSVersionTable`. Ez a tulajdonság a Windows build-verziószáma kötött. Ehelyett azt javasoljuk, hogy használjon `GitCommitId` a PowerShell Core pontos buildverziója lekéréséhez.

### <a name="changes-to-web-cmdlets"></a>Webes parancsmagok módosításai

Az alapul szolgáló .NET API a webes parancsmagok értékre változott `System.Net.Http.HttpClient`. Ez a változás üzenetcsere számos előnnyel jár. Azonban ezt a módosítást, és az Internet Explorer együttműködés hiánya belül több kompatibilitástörő változásokat eredményezték `Invoke-WebRequest` és `Invoke-RestMethod`.

- `Invoke-WebRequest` mostantól támogatja az alapszintű HTML elemzése csak. `Invoke-WebRequest` mindig adja vissza egy `BasicHtmlWebResponseObject` objektum. A `ParsedHtml` és `Forms` tulajdonságai el lettek távolítva.
- `BasicHtmlWebResponseObject.Headers` értékek: mostantól `String[]` helyett `String`.
- `BasicHtmlWebResponseObject.BaseResponse` mostantól egy `System.Net.Http.HttpResponseMessage` objektum.
- A `Response` webes parancsmag kivételek a tulajdonság már egy `System.Net.Http.HttpResponseMessage` objektum.
- Az alapértelmezett szigorú RFC fejléc elemzés már a `-Headers` és `-UserAgent` paraméter. Ez is művelet megkerülését eredményezte az `-SkipHeaderValidation`.
- `file://` és `ftp://` URI sémák nem támogatottak.
- `System.Net.ServicePointManager` beállítások a rendszer már nem figyelembe véve.
- Jelenleg nincs Tanúsítványalapú hitelesítés elérhető MacOS-gépeken.
- Felhasználása `-Credential` keresztül egy `http://` URI-t egy hibát eredményez. Használata egy `https://` URI-t, vagy adja meg a `-AllowUnencryptedAuthentication` paramétert a hibát.
- `-MaximumRedirection` most hoz létre egy hibát, átirányítás kísérletek-nál nagyobb a megadott korlátot, az utolsó átirányítás eredményeinek visszaadása helyett.
