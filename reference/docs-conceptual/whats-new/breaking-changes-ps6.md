---
ms.date: 05/17/2018
keywords: PowerShell-core
title: Módosítások megtörje PowerShell 6.0
ms.openlocfilehash: 60ce7a1676403bb08b57bf852ba725acde86a30c
ms.sourcegitcommit: 2d9cf1ccb9a653db7726a408ebcb65530dcb1522
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/19/2018
---
# <a name="breaking-changes-for-powershell-60"></a>Módosítások megtörje PowerShell 6.0

## <a name="features-no-longer-available-in-powershell-core"></a>A PowerShell központ már nem elérhető szolgáltatások

### <a name="powershell-workflow"></a>PowerShell-munkafolyamat

[PowerShell-munkafolyamati] [ workflow] a Windows PowerShell, a épülő szolgáltatása [Windows Workflow Foundation (WF)] [ workflow-foundation] létrehozását lehetővé tévő hosszan futó vagy párhuzamos működésű feladatok hatékony runbookokat.

Támogatja a Windows Workflow Foundation a .NET Core hiánya miatt nem folytatjuk PowerShell Core PowerShell munkafolyamat támogatásához.

A jövőben szeretnénk natív párhuzamossági/feldolgozási a PowerShell-munkafolyamati nélkül PowerShell nyelven engedélyezése.

[workflow]: https://docs.microsoft.com/powershell/scripting/core-powershell/workflows-guide
[workflow-foundation]: https://docs.microsoft.com/dotnet/framework/windows-workflow-foundation/

### <a name="custom-snap-ins"></a>Egyéni beépülő modulok

[PowerShell beépülő modulok] [ snapin] a PowerShell-modulok széles körű bevezetési nem rendelkeznek a PowerShell közösségi megelőző vannak.

Beépülő modulok és azok még támogató közösségi összetettsége miatt már nem támogatjuk egyéni beépülő modulok a PowerShell Core.

Jelenleg ez megszünteti a `ActiveDirectory` és `DnsClient` Windows és Windows Server modulok.

[snapin]: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_pssnapins

### <a name="wmi-v1-cmdlets"></a>A WMI v1-parancsmagok

WMI-alapú modulok két csoportja támogató összetettsége miatt a WMI v1-parancsmagok a PowerShell Core eltávolítása:

- `Get-WmiObject`
- `Invoke-WmiMethod`
- `Register-WmiEvent`
- `Set-WmiInstance`

Ehelyett azt javasoljuk, hogy Ön a (más néven WMI v2) CIM parancsmagok, amely biztosítja ezt a szolgáltatást új funkciókkal és újratervezett szintaxis használata:

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

Nem támogatott API-k használata miatt `Microsoft.PowerShell.LocalAccounts` el lett távolítva PowerShell Core amíg meg nem találja egy jobb megoldás.

### <a name="-counter-cmdlets"></a>`*-Counter` parancsmagjai

Nem támogatott API-k használata miatt a `*-Counter` el lett távolítva PowerShell Core amíg meg nem találja egy jobb megoldás.

## <a name="enginelanguage-changes"></a>Motor/nyelvi változások

### <a name="rename-powershellexe-to-pwshexe-5101httpsgithubcompowershellpowershellissues5101"></a>Nevezze át `powershell.exe` való `pwsh.exe` [#5101](https://github.com/PowerShell/PowerShell/issues/5101)

Annak érdekében, hogy a felhasználók (nem Windows PowerShell) a Windows PowerShell Core hívni determinisztikus módon, a PowerShell Core bináris változott az `pwsh.exe` Windows és `pwsh` nem Windows platformokon.

A rövidített neve egyben a nem Windows platformokon ismertetése elnevezése konzisztens.

### <a name="dont-insert-line-breaks-to-output-except-for-tables-5193httpsgithubcompowershellpowershellissues5193"></a>Ne jelölje be a sortörések (kivéve a táblák) kimeneti [#5193](https://github.com/PowerShell/PowerShell/issues/5193)

Korábban szélessége a konzol kimeneti lett igazítva, valamint sortörést hozzáadták az end szélességgel a konzol, ami azt jelenti, a kimenet nem get újraformázza átméretezze-e a Terminálszolgáltatások volt annak megfelelően. Ez a változás nem lett alkalmazva az táblák,, a sortörések szükség az oszlopok igazítását.

### <a name="skip-null-element-check-for-collections-with-a-value-type-element-type-5432httpsgithubcompowershellpowershellissues5432"></a>Hagyja ki a null-elem keresése egy értéktípus elemtípussal gyűjtemények [#5432](https://github.com/PowerShell/PowerShell/issues/5432)

Az a `Mandatory` paraméter és `ValidateNotNull` és `ValidateNotNullOrEmpty` attribútumok, a null-elem ellenőrzés kihagyására, amennyiben a gyűjtemény elemtípus értéktípus.

### <a name="change-outputencoding-to-use-utf-8-nobom-encoding-rather-than-ascii-5369httpsgithubcompowershellpowershellissues5369"></a>Változás `$OutputEncoding` használandó `UTF-8 NoBOM` helyett ASCII kódolás [#5369](https://github.com/PowerShell/PowerShell/issues/5369)

Az előző kódolás, ASCII (7 bites), egyes esetekben a kimeneti helytelen módosítása eredményezne. Ez a változás, hogy `UTF-8 NoBOM` alapértelmezett, amely a legtöbb eszközök és operációs rendszerek által támogatott kódolással rendelkező Unicode kimeneti megőrzi.

### <a name="remove-allscope-from-most-default-aliases-5268httpsgithubcompowershellpowershellissues5268"></a>Távolítsa el `AllScope` a legtöbb alapértelmezett aliasok [#5268](https://github.com/PowerShell/PowerShell/issues/5268)

Hatókör-létrehozás gyorsabb `AllScope` legtöbb alapértelmezett aliasnevek el lett távolítva. `AllScope` lett maradt néhány gyakran használt aliasok ahol a keresési gyorsabb lett.

### <a name="-verbose-and--debug-no-longer-overrides-erroractionpreference-5113httpsgithubcompowershellpowershellissues5113"></a>`-Verbose` és `-Debug` már nem felülbírálások `$ErrorActionPreference` [#5113](https://github.com/PowerShell/PowerShell/issues/5113)

Korábban Ha `-Verbose` vagy `-Debug` volt megadva, akkor overrode viselkedését `$ErrorActionPreference`. Ez a változás a `-Verbose` és `-Debug` már nem viselkedését `$ErrorActionPreference`.

## <a name="cmdlet-changes"></a>A parancsmag változások

### <a name="invoke-restmethod-doesnt-return-useful-info-when-no-data-is-returned-5320httpsgithubcompowershellpowershellissues5320"></a>Invoke-RestMethod nem ad visszatérési hasznos adatait, amikor nincs adat. [#5320](https://github.com/PowerShell/PowerShell/issues/5320)

Ha az API-k csak adja vissza `null`, Invoke-RestMethod lett szerializálása során ez a karakterlánc `"null"` helyett `$null`. Ez a változás javítások lévő logika `Invoke-RestMethod` megfelelően szerializálni érvényes szimpla típusú érték JSON `null` szöveges `$null`.

### <a name="remove--computername-from--computer-cmdlets-5277httpsgithubcompowershellpowershellissues5277"></a>Távolítsa el `-ComputerName` a `*-Computer` parancsmagok [#5277](https://github.com/PowerShell/PowerShell/issues/5277)

RPC távelérése CoreFX (nem Windows platformokon különösen) és a PowerShell-ablakba konzisztens távelérése biztosítása problémái miatt a `-ComputerName` paraméter el lett távolítva a `\*-Computer` parancsmagok. Használjon `Invoke-Command` inkább a parancsmagok végrehajtása távolról módját.

### <a name="remove--computername-from--service-cmdlets-5090httpsgithubcompowershellpowershellissues5094"></a>Távolítsa el `-ComputerName` a `*-Service` parancsmagok [#5090](https://github.com/PowerShell/PowerShell/issues/5094)

Ahhoz, hogy PSRP, egységes használata a `-ComputerName` paraméter el lett távolítva `*-Service` parancsmagok.

### <a name="fix-get-item--literalpath-ab-if-ab-doesnt-actually-exist-to-return-error-5197httpsgithubcompowershellpowershellissues5197"></a>Javítsa ki `Get-Item -LiteralPath a*b` Ha `a*b` ténylegesen nem létezik a hibaüzenetet [#5197](https://github.com/PowerShell/PowerShell/issues/5197)

Korábban `-LiteralPath` megadott helyettesítő karakteres volna tekinti az azonos `-Path` és a helyettesítő karakter található fájlokat, ha azt szeretné csendes való kilépéshez. Helyes viselkedés kell lennie, amely `-LiteralPath` literális, így ha a fájl nem létezik, kell-e hiba. Módosítsa az, hogy helyettesítő karakterrel együtt kezelni `-Literal` szerint szövegkonstans.

### <a name="import-csv-should-apply-pstypenames-upon-import-when-type-information-is-present-in-the-csv-5134httpsgithubcompowershellpowershellissues5134"></a>`Import-Csv` vonatkozzon `PSTypeNames` amikor típusinformációt megtalálható a CSV import alapján [#5134](https://github.com/PowerShell/PowerShell/issues/5134)

Korábban, az objektumok exportált használatával `Export-CSV` rendelkező `TypeInformation` az importált `ConvertFrom-Csv` nem volt a következő a típus adatainak megőrzése. Ez a változás a típus adatainak a ad hozzá `PSTypeNames` tag Ha elérhető a CSV-fájlból.

### <a name="-notypeinformation-should-be-default-on-export-csv-5131httpsgithubcompowershellpowershellissues5131"></a>`-NoTypeInformation` az alapértelmezett kell `Export-Csv` [#5131](https://github.com/PowerShell/PowerShell/issues/5131)

A módosítás az alapértelmezett viselkedés alapján cím-ügyfelek visszajelzéseire `Export-CSV` típus információval.

Korábban a parancsmag volna a kimeneti megjegyzést, az első sor tartalmazza az objektum nevét. A módosításnak a célja, hogy nem tudja értelmezni a legtöbb eszközök mellőzése Ez alapértelmezés szerint. Használjon `-IncludeTypeInformation` az előző megőrzése érdekében.

### <a name="web-cmdlets-should-warn-when--credential-is-sent-over-unencrypted-connections-5112httpsgithubcompowershellpowershellissues5112"></a>Webes parancsmagjai figyelmeztetnek, mikor `-Credential` titkosítatlan kapcsolaton keresztül zajlik [#5112](https://github.com/PowerShell/PowerShell/issues/5112)

A HTTP használata esetén például a jelszavak küldése a tiszta szöveges. Ez a változás nem engedélyezze ez alapértelmezés szerint, és hibát ad vissza, ha a hitelesítő adatok nem biztonságos módon átadta-hoz. Felhasználók jogosultak ennek segítségével a `-AllowUnencryptedAuthentication` váltani.

## <a name="api-changes"></a>API-változások

### <a name="remove-addtypecommandbase-class-5407httpsgithubcompowershellpowershellissues5407"></a>Távolítsa el `AddTypeCommandBase` osztály [#5407](https://github.com/PowerShell/PowerShell/issues/5407)

A `AddTypeCommandBase` osztály el lett távolítva `Add-Type` teljesítmény javítása érdekében. Ez az osztály csak az Add-típus a parancsmag által használt, és nem kell befolyásolja a felhasználók.

### <a name="unify-cmdlets-with-parameter--encoding-to-be-of-type-systemtextencoding-5080httpsgithubcompowershellpowershellissues5080"></a>Parancsmag-paraméterrel egységes `-Encoding` típusúnak kell lennie `System.Text.Encoding` [#5080](https://github.com/PowerShell/PowerShell/issues/5080)

A `-Encoding` érték `Byte` a fájlrendszer szolgáltató parancsmagjai el lett távolítva. Egy új paraméter `-AsByteStream`, most használatával adja meg, hogy egy bájtos adatfolyam szükséges bemeneti, vagy hogy a kimenet egy bájtos adatfolyam.

### <a name="add-better-error-message-for-empty-and-null--uformat-parameter-5055httpsgithubcompowershellpowershellissues5055"></a>Adja hozzá a jobb üres hibaüzenetet és null `-UFormat` paraméter [#5055](https://github.com/PowerShell/PowerShell/issues/5055)

Korábban, ha átadja egy üres formátumú karakterlánc-való `-UFormat`, unhelpful hibaüzenetet jelent. A leíró hiba hozzá lett adva.

### <a name="clean-up-console-code-4995httpsgithubcompowershellpowershellissues4995"></a>Konzol kód karbantartása [#4995](https://github.com/PowerShell/PowerShell/issues/4995)

A következő szolgáltatások nem támogatják a PowerShell-Core, és nem tervezik támogatásához a Windows PowerShell örökölt összetevők miatt léteznek eltávolítása: `-psconsolefile` kapcsoló és a kódot, `-importsystemmodules` kapcsoló és a kód és a betűtípus módosítása a kódot.

### <a name="removed-runspaceconfiguration-support-4942httpsgithubcompowershellpowershellissues4942"></a>Eltávolított `RunspaceConfiguration` támogatja [#4942](https://github.com/PowerShell/PowerShell/issues/4942)

Korábban, a PowerShell futási térben programozott módon létrehozása az API-val használata az örökölt [ `RunspaceConfiguration` ] [ runspaceconfig] vagy az újabb [ `InitialSessionState` ] [ iss]. Ez a változás eltávolított támogatása `RunspaceConfiguration` és csak akkor támogatja a `InitialSessionState`.

[runspaceconfig]: https://docs.microsoft.com/dotnet/api/system.management.automation.runspaces.runspaceconfiguration
[iss]: https://docs.microsoft.com/dotnet/api/system.management.automation.runspaces.initialsessionstate

### <a name="commandinvocationintrinsicsinvokescript-bind-arguments-to-input-instead-of-args-4923httpsgithubcompowershellpowershellissues4923"></a>`CommandInvocationIntrinsics.InvokeScript` kötési argumentumokat `$input` helyett `$args` [#4923](https://github.com/PowerShell/PowerShell/issues/4923)

A paraméter helytelen pontjának eredményezett az átadott argumentum, ahelyett, hogy bemeneti argumentum.

### <a name="remove-unsupported--showwindow-switch-from-get-help-4903httpsgithubcompowershellpowershellissues4903"></a>Távolítsa el a nem támogatott `-showwindow` átállás `Get-Help` [#4903](https://github.com/PowerShell/PowerShell/issues/4903)

`-showwindow` WPF, amely nem támogatott a következő CoreCLR támaszkodik.

### <a name="allow--to-be-used-in-registry-path-for-remove-item-4866httpsgithubcompowershellpowershellissues4866"></a>Engedélyezése * beállításjegyzékbeli elérési út a használandó `Remove-Item` [#4866](https://github.com/PowerShell/PowerShell/issues/4866)

Korábban `-LiteralPath` megadott helyettesítő karakteres volna tekinti az azonos `-Path` és a helyettesítő karakter található fájlokat, ha azt szeretné csendes való kilépéshez. Helyes viselkedés kell lennie, amely `-LiteralPath` literális, így ha a fájl nem létezik, kell-e hiba. Módosítsa az, hogy helyettesítő karakterrel együtt kezelni `-Literal` szerint szövegkonstans.

### <a name="fix-set-service-failing-test-4802httpsgithubcompowershellpowershellissues4802"></a>Javítsa ki `Set-Service` teszt sikertelen [#4802](https://github.com/PowerShell/PowerShell/issues/4802)

Korábban Ha `New-Service -StartupType foo` lett megadva, `foo` figyelmen kívül lett hagyva, és a szolgáltatás egyes alapértelmezett indítási típus hozták létre. Ez a változás, hogy explicit módon throw hiba, ha egy érvénytelen indítási típus.

### <a name="rename-isosx-to-ismacos-4700httpsgithubcompowershellpowershellissues4700"></a>Nevezze át `$IsOSX` való `$IsMacOS` [#4700](https://github.com/PowerShell/PowerShell/issues/4700)

A PowerShell elnevezési konzisztensek legyenek az elnevezési legyen, és macOS OSX helyett az Apple felhasználási felelnek meg. Azonban az olvashatóság és következetesen azt tartózkodó Pascal a kis-és nagybetűhasználatot.

### <a name="make-error-message-consistent-when-invalid-script-is-passed-to--file-better-error-when-passed-ambiguous-argument-4573httpsgithubcompowershellpowershellissues4573"></a>Üzenet hiba konzisztens ellenőrizze Ha érvénytelen parancsfájl - fájl, a hiba, ha a nem egyértelmű argumentum jobb [#4573](https://github.com/PowerShell/PowerShell/issues/4573)

A kilépési kód módosítása `pwsh.exe` való megfelelés érdekében Unix konvenciók

### <a name="removal-of-localaccount-and-cmdlets-from--diagnostics-modules-4302httpsgithubcompowershellpowershellissues4302-4303httpsgithubcompowershellpowershellissues4303"></a>Az Eltávolítás `LocalAccount` és parancsmagjait `Diagnostics` modulok. [#4302](https://github.com/PowerShell/PowerShell/issues/4302) [#4303](https://github.com/PowerShell/PowerShell/issues/4303)

Nem támogatott API-kat, mert a `LocalAccounts` modul és a `Counter` parancsmagok a a `Diagnostics` modul eltávolítva, amíg meg nem találja egy jobb megoldás.

### <a name="executing-powershell-script-with-bool-parameter-does-not-work-4036httpsgithubcompowershellpowershellissues4036"></a>Logikai paraméterrel powershell-parancsprogram végrehajtása nem működik [#4036](https://github.com/PowerShell/PowerShell/issues/4036)

Korábban, a powershell.exe használatával (most `pwsh.exe`) végrehajtására, a PowerShell parancsfájl használatával `-File` megadott semmilyen módon nem felelt meg a $true vagy $false paraméter értékeként. $True támogatása/$false paraméterekhez elemzett értékként lett hozzáadva. Kapcsoló értékek használata is támogatott jelenleg dokumentált szintaxis nem működik.

### <a name="remove-clrversion-property-from-psversiontable-4027httpsgithubcompowershellpowershellissues4027"></a>Távolítsa el `ClrVersion` tulajdonságot `$PSVersionTable` [#4027](https://github.com/PowerShell/PowerShell/issues/4027)

A `ClrVersion` tulajdonsága `$PSVersionTable` van CoreCLR nem használható, a végfelhasználók kell nem használja ezt az értéket kompatibilitási meghatározásához.

### <a name="change-positional-parameter-for-powershellexe-from--command-to--file-4019httpsgithubcompowershellpowershellissues4019"></a>Módosítsa a pozícióparaméter `powershell.exe` a `-Command` való `-File` [#4019](https://github.com/PowerShell/PowerShell/issues/4019)

A nem Windows platformokon shebang PowerShell használatának engedélyezése. Ez azt jelenti, Unix-alapú rendszereken volna meghívása a PowerShell parancsfájl végrehajtható hogy automatikusan ahelyett, hogy explicit módon hívja `pwsh`. Ez azt is jelenti, hogy teheti többek között a `powershell foo.ps1` vagy `powershell fooScript` megadása nélkül `-File`. Azonban ez a változás megköveteli, hogy Ön kifejezetten megad `-c` vagy `-Command` amikor többek között a végrehajtását megkísérlő `powershell.exe Get-Command`.

### <a name="implement-unicode-escape-parsing-3958httpsgithubcompowershellpowershellissues3958"></a>Unicode karaktert elemzés végrehajtása [#3958](https://github.com/PowerShell/PowerShell/issues/3958)

`` `u#### `` vagy `` `u{####} `` alakítja át a megfelelő Unicode-karakter. Kimeneti szövegkonstans `` `u ``, a backtick karaktert: ``` ``u ```.

### <a name="change-new-modulemanifest-encoding-to-utf8nobom-on-non-windows-platforms-3940httpsgithubcompowershellpowershellissues3940"></a>Változás `New-ModuleManifest` kódolása `UTF8NoBOM` nem Windows platformokon [#3940](https://github.com/PowerShell/PowerShell/issues/3940)

Korábban `New-ModuleManifest` psd1 kiterjesztésű jegyzékfájlokban létrehozza az UTF-16 az Anyagjegyzék, a Linux rendszerű eszközök probléma létrehozása. Ez használhatatlanná tévő változást módosítja a kódolását `New-ModuleManifest` nem Windows platformokon UTF (nincs AJ) lehet.

### <a name="prevent-get-childitem-from-recursing-into-symlinks-1875-3780httpsgithubcompowershellpowershellissues3780"></a>Megakadályozása `Get-ChildItem` a symlinks történő recursing (#1875). [#3780](https://github.com/PowerShell/PowerShell/issues/3780)

Ez a változás számos lehetőséget kínál `Get-ChildItem` összhangban a Unix további `ls -r` és a Windows `dir /s` natív parancsok. Az említett parancsok, például a parancsmag megjeleníti a szimbolikus csatolást rekurzió alatt található könyvtárak, de nem alkönyvtárakban őket.

### <a name="fix-get-content--delimiter-to-not-include-the-delimiter-in-the-returned-lines-3706httpsgithubcompowershellpowershellissues3706"></a>Javítsa ki `Get-Content -Delimiter` nem tartalmazza az elválasztó a visszaadott sorok [#3706](https://github.com/PowerShell/PowerShell/issues/3706)

Korábban, a kimeneti `Get-Content -Delimiter` inkonzisztens és kényelmetlen, az adatok eltávolítása az elválasztó további feldolgozás szükség volt. Ez a változás az elválasztó eltávolítja a visszaadott sorok.

### <a name="implement-format-hex-in-c-3320httpsgithubcompowershellpowershellissues3320"></a>Hexadecimális formátumú megvalósítását a C# [#3320](https://github.com/PowerShell/PowerShell/issues/3320)

A `-Raw` paraméter most "műveletvégzés" (abban, hogy nincs semmi hatása). Továbbítja összes jelenik meg, amely tartalmazza az összes ehhez a típushoz a bájtok számok jelentik (Mi a `-Raw` paraméter hivatalosan műveletet végzett ezen).

### <a name="powershell-as-a-default-shell-doesnt-work-with-script-command-3319httpsgithubcompowershellpowershellissues3319"></a>Egy alapértelmezett rendszerhéját, PowerShell parancsprogram-utasítás nem működik [#3319](https://github.com/PowerShell/PowerShell/issues/3319)

UNIX ismertetése elfogadására vonatkozó `-i` az egy interaktív rendszerhéjat, és számos eszközt Ez a viselkedés várható (`script` például és beállítását PowerShell alapértelmezett rendszerhéját), és a rendszerhéj a `-i` váltani. Ezt a módosítást, amely a megsérti `-i` korábban volt használható rövid aktuális megfelelően `-inputformat`, mely most kell lennie `-in`.

### <a name="typo-fix-in-get-computerinfo-property-name-3167httpsgithubcompowershellpowershellissues3167"></a>A Get-ComputerInfo tulajdonságnév elgépelte javítás [#3167](https://github.com/PowerShell/PowerShell/issues/3167)

`BiosSerialNumber` lett írva `BiosSeralNumber` és helyesen van beállítva.

### <a name="add-get-stringhash-and-get-filehash-cmdlets-3024httpsgithubcompowershellpowershellissues3024"></a>Adja hozzá `Get-StringHash` és `Get-FileHash` parancsmagok [#3024](https://github.com/PowerShell/PowerShell/issues/3024)

Ez a változás az, hogy néhány kivonatoló algoritmusok nem támogatottak az CoreFX, ezért azok már nem érhető el:

- `MACTripleDES`
- `RIPEMD160`

### <a name="add-validation-on-get--cmdlets-where-passing-null-returns-all-objects-instead-of-error-2672httpsgithubcompowershellpowershellissues2672"></a>Adja hozzá az érvényesítés a `Get-*` parancsmagok, ahol sikeres $null adja vissza a hiba helyett minden objektumot [#2672](https://github.com/PowerShell/PowerShell/issues/2672)

Sikeres `$null` sem a következő most hibát jelez:

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

### <a name="add-support-w3c-extended-log-file-format-in-import-csv-2482httpsgithubcompowershellpowershellissues2482"></a>Adja hozzá a W3C bővített naplófájlformátum a támogatja `Import-Csv` [#2482](https://github.com/PowerShell/PowerShell/issues/2482)

Korábban a `Import-Csv` parancsmag nem használható közvetlenül a W3C bővített naplóformátumban naplófájlok importálása, és további művelet lenne szükséges. Ez a változás a W3C bővített naplóformátumban támogatott.

### <a name="parameter-binding-problem-with-valuefromremainingarguments-in-ps-functions-2035httpsgithubcompowershellpowershellissues2035"></a>A paraméter kötési hiba `ValueFromRemainingArguments` PS funkciókkal [#2035](https://github.com/PowerShell/PowerShell/issues/2035)

`ValueFromRemainingArguments` most adja vissza az értékeket egy tömbként helyett egyetlen érték pedig van egy tömb.

### <a name="buildversion-is-removed-from-psversiontable-1415httpsgithubcompowershellpowershellissues1415"></a>`BuildVersion` a rendszer eltávolítja a `$PSVersionTable` [#1415](https://github.com/PowerShell/PowerShell/issues/1415)

Távolítsa el a `BuildVersion` tulajdonságot `$PSVersionTable`. Ez a tulajdonság lett kötve a Windows verzió buildszámával. Ehelyett azt javasoljuk, hogy használjon `GitCommitId` PowerShell Core pontos buildszámának beolvasása.

### <a name="changes-to-web-cmdlets"></a>Webes parancsmagjai módosításai

Az alapul szolgáló .NET API-t a webes parancsmagok változott a `System.Net.Http.HttpClient`. Ez a változás számos előnyt kínál. Azonban ezt a módosítást és az Internet Explorer való hiánya belül több jelentős változásokat eredményezték `Invoke-WebRequest` és `Invoke-RestMethod`.

- `Invoke-WebRequest` mostantól támogatja az egyszerű HTML-elemzési csak. `Invoke-WebRequest` mindig adja meg a `BasicHtmlWebResponseObject` objektum. A `ParsedHtml` és `Forms` tulajdonságok el lettek távolítva.
- `BasicHtmlWebResponseObject.Headers` értékek: most `String[]` helyett `String`.
- `BasicHtmlWebResponseObject.BaseResponse` most már egy `System.Net.Http.HttpResponseMessage` objektum.
- A `Response` webes parancsmag kivételek tulajdonsága most egy `System.Net.Http.HttpResponseMessage` objektum.
- Az alapértelmezett szigorú RFC fejlécének elemzésekor mostantól a `-Headers` és `-UserAgent` paraméter. Ez a mellőzhető `-SkipHeaderValidation`.
- `file://` és `ftp://` URI-séma már nem támogatott.
- `System.Net.ServicePointManager` beállítások a rendszer már nem figyelembe véve.
- Jelenleg nincs a Tanúsítványalapú hitelesítés érhető el a macOS.
- A használatára `-Credential` keresztül egy `http://` URI hibát eredményez. Használjon egy `https://` URI, vagy adjon a `-AllowUnencryptedAuthentication` paramétert a hibát.
