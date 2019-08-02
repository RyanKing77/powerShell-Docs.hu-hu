---
ms.date: 05/17/2018
keywords: PowerShell, mag
title: A PowerShell 6,0-es feltörésének változásai
ms.openlocfilehash: 186e55c1ac46ce3fc172df18995f8c15d9eeb8eb
ms.sourcegitcommit: 118eb294d5a84a772e6449d42a9d9324e18ef6b9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/26/2019
ms.locfileid: "67843941"
---
# <a name="breaking-changes-for-powershell-60"></a>A PowerShell 6,0-es feltörésének változásai

## <a name="features-no-longer-available-in-powershell-core"></a>A szolgáltatás már nem érhető el a PowerShell Core-ban

### <a name="powershell-workflow"></a>PowerShell-munkafolyamat

A [PowerShell-munkafolyamat][workflow] a Windows PowerShell egyik funkciója, amely [Windows Workflow Foundation (WF)][workflow-foundation] épül, amely lehetővé teszi robusztus runbookok létrehozását a hosszan futó vagy párhuzamos feladatokhoz.

A .NET Core-Windows Workflow Foundation támogatásának hiánya miatt a PowerShell Core-ban nem folytatjuk a PowerShell-munkafolyamat támogatását.

A jövőben azt szeretnénk, hogy a PowerShell-munkafolyamatok szükségessége nélkül engedélyezzük a natív párhuzamosságot/párhuzamosságot a PowerShell nyelvén.

[workflow]: https://docs.microsoft.com/powershell/scripting/core-powershell/workflows-guide
[workflow-foundation]: https://docs.microsoft.com/dotnet/framework/windows-workflow-foundation/

### <a name="custom-snap-ins"></a>Egyéni beépülő modulok

A PowerShell beépülő modulok olyan PowerShell [-][snapin] modulok elődje, amelyek nem rendelkeznek széleskörű bevezetéssel a PowerShell-Közösségben.

A beépülő modulok és a Közösségen belüli használat hiányának összetettsége miatt a PowerShell Core-ban már nem támogatottak az egyéni beépülő modulok.

Napjainkban ez megszakítja `DnsClient` a Windows és a `ActiveDirectory` Windows Server-modulokat.

[snapin]: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_pssnapins

### <a name="wmi-v1-cmdlets"></a>WMI v1-parancsmagok

A WMI-alapú modulok két csoportja támogatásának összetettsége miatt a PowerShell Core-ból eltávolította a WMI v1-parancsmagokat:

- `Get-WmiObject`
- `Invoke-WmiMethod`
- `Register-WmiEvent`
- `Set-WmiInstance`

Ehelyett azt javasoljuk, hogy használja a CIM (aka WMI v2) parancsmagokat, amelyek ugyanazt a funkciót biztosítják az új funkciókkal és az újratervezett szintaxissal:

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

### <a name="microsoftpowershelllocalaccounts"></a>Microsoft. PowerShell. LocalAccounts

A nem támogatott API-k használata miatt a rendszer `Microsoft.PowerShell.LocalAccounts` eltávolította a PowerShell Core-ból, amíg jobb megoldást nem talál.

### <a name="-computer-cmdlets"></a>`*-Computer`parancsmagok

A nem támogatott API-k használata miatt a következő parancsmagok el lettek távolítva a PowerShell Core-ból, amíg nem talál jobb megoldást.

- Számítógép hozzáadása
- Checkpoint-Computer
- Számítógép eltávolítása
- Visszaállítás – számítógép

### <a name="-counter-cmdlets"></a>`*-Counter`parancsmagok

A nem támogatott API-k használata miatt a `*-Counter` el lett távolítva a PowerShell Core-ból, amíg nem talál jobb megoldást.

### <a name="-eventlog-cmdlets"></a>`*-EventLog`parancsmagok

A nem támogatott API-k használata miatt a `*-EventLog` el lett távolítva a PowerShell Core-ból. egészen addig, amíg nem talál jobb megoldást. `Get-WinEvent`és `Create-WinEvent` elérhetők a Windows rendszerű események beszerzéséhez és létrehozásához.

## <a name="enginelanguage-changes"></a>Motor/nyelvi változások

### <a name="rename-powershellexe-to-pwshexe-5101httpsgithubcompowershellpowershellissues5101"></a>`powershell.exe`Átnevezés#5101 `pwsh.exe` [](https://github.com/PowerShell/PowerShell/issues/5101)

Ahhoz, hogy a felhasználók determinisztikus a PowerShell Core-t a Windowsban (a Windows PowerShell helyett), a PowerShell Core bináris fájl a Windows és `pwsh.exe` `pwsh` a nem Windows rendszerű platformokra változott.

A lerövidített név is konzisztens a nem Windows platformokon lévő rendszerhéjok elnevezésével.

### <a name="dont-insert-line-breaks-to-output-except-for-tables-5193httpsgithubcompowershellpowershellissues5193"></a>Ne szúrjon be sortörést a kimenetbe (táblák kivételével) [#5193](https://github.com/PowerShell/PowerShell/issues/5193)

A kimenetet korábban a konzol szélessége és a sortörések a konzol végéhez igazították, ami azt jelenti, hogy a kimenet átméretezése nem a várt módon történt, ha a terminál át lett méretezve. Ez a módosítás nem lett alkalmazva a táblákra, mivel a sortörések szükségesek ahhoz, hogy az oszlopok összhangban maradjanak.

### <a name="skip-null-element-check-for-collections-with-a-value-type-element-type-5432httpsgithubcompowershellpowershellissues5432"></a>NULL értékű elemek keresésének kihagyása az érték típusú elem típusával [#5432](https://github.com/PowerShell/PowerShell/issues/5432)

A paraméter `Mandatory` `ValidateNotNull`ésazattribútumokesetében hagyja ki a null értékű elemet, ha a gyűjtemény elemének típusa értéktípus. `ValidateNotNullOrEmpty`

### <a name="change-outputencoding-to-use-utf-8-nobom-encoding-rather-than-ascii-5369httpsgithubcompowershellpowershellissues5369"></a>Az ASCII- `UTF-8 NoBOM` #5369 helyett használja a kódolást [](https://github.com/PowerShell/PowerShell/issues/5369) `$OutputEncoding`

Az előző kódolás, az ASCII (7 bites) helytelenül változtatja meg a kimenetet bizonyos esetekben. Ez a módosítás az `UTF-8 NoBOM` alapértelmezett beállítás, amely a legtöbb eszköz és operációs rendszer által támogatott kódolással megőrzi a Unicode-kimenetet.

### <a name="remove-allscope-from-most-default-aliases-5268httpsgithubcompowershellpowershellissues5268"></a>A `AllScope` legtöbb alapértelmezett alias eltávolítása [#5268](https://github.com/PowerShell/PowerShell/issues/5268)

A hatókör-létrehozás `AllScope` felgyorsításához a legtöbb alapértelmezett alias el lett távolítva. `AllScope`néhány gyakran használt alias maradt, ahol a keresés gyorsabb volt.

### <a name="-verbose-and--debug-no-longer-overrides-erroractionpreference-5113httpsgithubcompowershellpowershellissues5113"></a>`-Verbose`és `-Debug` már nem `$ErrorActionPreference` felülbírálja [#5113](https://github.com/PowerShell/PowerShell/issues/5113)

Korábban, ha `-Verbose` vagy `-Debug` meg lett adva, a viselkedését `$ErrorActionPreference`átlovagolta. Ezzel a módosítással `-Verbose` `-Debug` a `$ErrorActionPreference`továbbiakban nem befolyásolja a viselkedését.

## <a name="cmdlet-changes"></a>Parancsmag módosításai

### <a name="invoke-restmethod-doesnt-return-useful-info-when-no-data-is-returned-5320httpsgithubcompowershellpowershellissues5320"></a>Meghívás – a RestMethod nem ad vissza hasznos információt, ha nem ad vissza adatokat. [#5320](https://github.com/PowerShell/PowerShell/issues/5320)

Ha egy API `null`-t ad vissza, a meghívó-RestMethod ezt a karakterláncot a `$null`helyett sztringként `"null"` szerializálja. Ez a változás javítja a logikát, hogy megfelelően szerializálja egy érvényes `Invoke-RestMethod` , `null` `$null`egyértékű JSON-literálot a következőként:.

### <a name="remove--protocol-from--computer-cmdlets-5277httpsgithubcompowershellpowershellissues5277"></a>Eltávolítás `-Protocol` a`*-Computer` parancsmagokból [#5277](https://github.com/PowerShell/PowerShell/issues/5277)

A CoreFX-alapú RPC távoli eljáráshívás (különösen a nem Windows platformokon) és a PowerShell konzisztens távelérési felületének biztosítása miatt a `-Protocol` paraméter el lett távolítva `\*-Computer` a parancsmagokból. A DCOM már nem támogatott a táveléréshez. A következő parancsmagok csak a WSMAN távelérését támogatják:

- Számítógép átnevezése
- Újraindítás – számítógép
- Számítógép leállítása

### <a name="remove--computername-from--service-cmdlets-5090httpsgithubcompowershellpowershellissues5094"></a>Eltávolítás `-ComputerName` a`*-Service` parancsmagokból [#5090](https://github.com/PowerShell/PowerShell/issues/5094)

A PSRP egységes használatának elősegítése érdekében a `-ComputerName` paraméter `*-Service` el lett távolítva a parancsmagokból.

### <a name="fix-get-item--literalpath-ab-if-ab-doesnt-actually-exist-to-return-error-5197httpsgithubcompowershellpowershellissues5197"></a>Javítsa `Get-Item -LiteralPath a*b` a `a*b` hibát, ha valójában nem létezik a hiba [#5197](https://github.com/PowerShell/PowerShell/issues/5197)

Korábban, `-LiteralPath` mivel a helyettesítő karakter ugyanúgy kezeli azt, mint `-Path` ha a helyettesítő karakter nem talált fájlt, a rendszer csendben kizárja. A helyes viselkedésnek konstansnak kell lennie `-LiteralPath` , tehát ha a fájl nem létezik, akkor hiba történik. A módosítás a literálként használt `-Literal` helyettesítő karakterek kezelése.

### <a name="import-csv-should-apply-pstypenames-upon-import-when-type-information-is-present-in-the-csv-5134httpsgithubcompowershellpowershellissues5134"></a>`Import-Csv`importáláskor `PSTypeNames` kell alkalmazni, ha a típus adatai szerepelnek a CSV- [#5134](https://github.com/PowerShell/PowerShell/issues/5134)

Korábban a használatával `Export-CSV` `TypeInformation` exportáltobjektumoknemőrzikmegatípusinformációit.`ConvertFrom-Csv` Ez a változás adja hozzá a típus `PSTypeNames` adatait a tagnak, ha elérhető a csv-fájlból.

### <a name="-notypeinformation-should-be-default-on-export-csv-5131httpsgithubcompowershellpowershellissues5131"></a>`-NoTypeInformation`alapértelmezett értéknek `Export-Csv` kell lennie [#5131](https://github.com/PowerShell/PowerShell/issues/5131)

Ez a módosítás történt a felhasználói visszajelzések megadására az alapértelmezett `Export-CSV` viselkedésével kapcsolatban, hogy tartalmazza a típussal kapcsolatos információkat.

Korábban a parancsmag az objektum típusának nevét tartalmazó első sorban kiírja a megjegyzést. A módosítás alapértelmezés szerint letiltja ezt a beállítást, mert a legtöbb eszköz nem értelmezi. A `-IncludeTypeInformation` használatával megtarthatja az előző viselkedést.

### <a name="web-cmdlets-should-warn-when--credential-is-sent-over-unencrypted-connections-5112httpsgithubcompowershellpowershellissues5112"></a>A webes parancsmagoknak figyelmeztetést `-Credential` kell kapniuk, ha titkosítatlan kapcsolaton keresztül küldenek [#5112](https://github.com/PowerShell/PowerShell/issues/5112)

HTTP használata esetén a tartalmat, beleértve a jelszavakat is, a rendszer tiszta szövegként továbbítja. Ez a módosítás nem engedélyezi ezt alapértelmezés szerint, és nem ad vissza hibát, ha a hitelesítő adatok nem biztonságos módon jutnak át. Ezt a kapcsoló használatával a `-AllowUnencryptedAuthentication` felhasználók kihagyhatják.

## <a name="api-changes"></a>API-változások

### <a name="remove-addtypecommandbase-class-5407httpsgithubcompowershellpowershellissues5407"></a>Osztály `AddTypeCommandBase` eltávolítása [#5407](https://github.com/PowerShell/PowerShell/issues/5407)

Az `AddTypeCommandBase` osztály`Add-Type` el lett távolítva a teljesítmény javítása érdekében. Ezt az osztályt csak az Add-Type parancsmag használja, és nem befolyásolhatja a felhasználókat.

### <a name="unify-cmdlets-with-parameter--encoding-to-be-of-type-systemtextencoding-5080httpsgithubcompowershellpowershellissues5080"></a>A (z) paraméterrel `-Encoding` `System.Text.Encoding` rendelkező parancsmagok egyesítése [#5080](https://github.com/PowerShell/PowerShell/issues/5080)

Az `-Encoding` érték`Byte` el lett távolítva a fájlrendszer-szolgáltatói parancsmagokból. A (z) `-AsByteStream`új paraméterrel megadható, hogy egy bájtos adatfolyam kötelező legyen bemenetként, vagy hogy a kimenet egy bájtos stream.

### <a name="add-better-error-message-for-empty-and-null--uformat-parameter-5055httpsgithubcompowershellpowershellissues5055"></a>Adjon hozzá jobb hibaüzenetet az üres és `-UFormat` a null paraméterhez [#5055](https://github.com/PowerShell/PowerShell/issues/5055)

Korábban, ha üres formázó karakterláncot adott `-UFormat`át a értékre, egy nem megfelelő hibaüzenet jelenik meg. További leíró hiba lett hozzáadva.

### <a name="clean-up-console-code-4995httpsgithubcompowershellpowershellissues4995"></a>A konzol kódjának tisztítása [#4995](https://github.com/PowerShell/PowerShell/issues/4995)

A következő szolgáltatások el lettek távolítva, mivel azok a PowerShell Core-ban nem támogatottak, és a Windows PowerShell `-psconsolefile` `-importsystemmodules` korábbi okaihoz nem biztosítunk támogatást

### <a name="removed-runspaceconfiguration-support-4942httpsgithubcompowershellpowershellissues4942"></a>A `RunspaceConfiguration` támogatási [#4942](https://github.com/PowerShell/PowerShell/issues/4942) eltávolítva

Korábban, ha az API-val programozott módon hoz létre egy PowerShell-RunSpace, használhatja az [`RunspaceConfiguration`][runspaceconfig] örökölt vagy [`InitialSessionState`][iss]az újabbt. Ez a módosítás eltávolítja a `RunspaceConfiguration` támogatást, és `InitialSessionState`csak a támogatott.

[runspaceconfig]: https://docs.microsoft.com/dotnet/api/system.management.automation.runspaces.runspaceconfiguration
[iss]: https://docs.microsoft.com/dotnet/api/system.management.automation.runspaces.initialsessionstate

### <a name="commandinvocationintrinsicsinvokescript-bind-arguments-to-input-instead-of-args-4923httpsgithubcompowershellpowershellissues4923"></a>`CommandInvocationIntrinsics.InvokeScript`argumentumok `$input` kötése [#4923](https://github.com/PowerShell/PowerShell/issues/4923) helyett `$args`

A paraméter helytelen pozíciója az argumentumként átadott argumentumokat eredményezett.

### <a name="remove-unsupported--showwindow-switch-from-get-help-4903httpsgithubcompowershellpowershellissues4903"></a>Nem támogatott `-showwindow` `Get-Help` kapcsoló eltávolítása [#4903](https://github.com/PowerShell/PowerShell/issues/4903)

`-showwindow`a WPF-re támaszkodik, amely nem támogatott a CoreCLR.

### <a name="allow--to-be-used-in-registry-path-for-remove-item-4866httpsgithubcompowershellpowershellissues4866"></a>A * `Remove-Item` [#4866](https://github.com/PowerShell/PowerShell/issues/4866) beállításjegyzékbeli elérési útján való használatának engedélyezése

Korábban, `-LiteralPath` mivel a helyettesítő karakter ugyanúgy kezeli azt, mint `-Path` ha a helyettesítő karakter nem talált fájlt, a rendszer csendben kizárja. A helyes viselkedésnek konstansnak kell lennie `-LiteralPath` , tehát ha a fájl nem létezik, akkor hiba történik. A módosítás a literálként használt `-Literal` helyettesítő karakterek kezelése.

### <a name="fix-set-service-failing-test-4802httpsgithubcompowershellpowershellissues4802"></a>Sikertelen `Set-Service` tesztelési [#4802](https://github.com/PowerShell/PowerShell/issues/4802) javítása

Korábban a használatakor a rendszer `foo` figyelmen kívül hagyta a szolgáltatást, és az alapértelmezett indítási típussal lett létrehozva. `New-Service -StartupType foo` Ez a változás egy érvénytelen indítási típus hibájának kifejezett eldobása.

### <a name="rename-isosx-to-ismacos-4700httpsgithubcompowershellpowershellissues4700"></a>`$IsOSX`Átnevezés#4700 `$IsMacOS` [](https://github.com/PowerShell/PowerShell/issues/4700)

A PowerShellben való elnevezésnek konzisztensnek kell lennie az elnevezéssel, és meg kell felelnie az Apple által az OSX helyett a macOS használatának. Azonban az olvashatóság és a következetesen a Pascal ház marad.

### <a name="make-error-message-consistent-when-invalid-script-is-passed-to--file-better-error-when-passed-ambiguous-argument-4573httpsgithubcompowershellpowershellissues4573"></a>A hibaüzenet akkor konzisztens, ha a rendszer érvénytelen parancsfájlt ad át a fájlnak, ami jobb, ha kétértelmű argumentumot adott át [#4573](https://github.com/PowerShell/PowerShell/issues/4573)

A kilépési kódok `pwsh.exe` módosítása a UNIX-egyezményekhez való igazításhoz

### <a name="removal-of-localaccount-and-cmdlets-from--diagnostics-modules-4302httpsgithubcompowershellpowershellissues4302-4303httpsgithubcompowershellpowershellissues4303"></a>A `LocalAccount` és a parancsmagok `Diagnostics` eltávolítása a modulokból. [#4302](https://github.com/PowerShell/PowerShell/issues/4302) [#4303](https://github.com/PowerShell/PowerShell/issues/4303)

A nem támogatott API-k miatt a `LocalAccounts` modul és a `Counter` `Diagnostics` modul parancsmagjai el lettek távolítva, amíg nem talál jobb megoldást.

### <a name="executing-powershell-script-with-bool-parameter-does-not-work-4036httpsgithubcompowershellpowershellissues4036"></a>A PowerShell-parancsfájl a bool paraméterrel való végrehajtása nem működik [#4036](https://github.com/PowerShell/PowerShell/issues/4036)

Korábban a **PowerShell. exe** (most **pwsh. exe**) használatával hajtson végre `-File` egy PowerShell-parancsfájlt a megadott módon `$true` / `$false` a paraméter értékének megadásával. A rendszer `$true` / hozzáadtaaparamétereketazelemzettértékekhez`$false` a paraméterekhez. A váltási értékek is támogatottak, mert a jelenleg dokumentált szintaxis nem működik.

### <a name="remove-clrversion-property-from-psversiontable-4027httpsgithubcompowershellpowershellissues4027"></a>Tulajdonság `ClrVersion` eltávolítása#4027`$PSVersionTable` [](https://github.com/PowerShell/PowerShell/issues/4027)

`ClrVersion` A`$PSVersionTable` tulajdonsága nem hasznos a CoreCLR, ezért a végfelhasználóknak nem szabad ezt az értéket használni a kompatibilitás megállapításához.

### <a name="change-positional-parameter-for-powershellexe-from--command-to--file-4019httpsgithubcompowershellpowershellissues4019"></a>Pozíciós paraméter `powershell.exe` módosítása a `-File` - `-Command` ből [#4019](https://github.com/PowerShell/PowerShell/issues/4019)

Engedélyezze a PowerShell shebangje használatát a nem Windows platformokon. Ez azt jelenti, hogy UNIX-alapú rendszereken olyan végrehajtható parancsfájl futtatható, amely nem explicit módon `pwsh`hívja meg a PowerShellt. Ez azt is jelenti, hogy mostantól hasonló `powershell foo.ps1` módon vagy `powershell fooScript` anélkül teheti meg `-File`a műveleteket. Ez a módosítás azonban azt igényli, hogy explicit módon megadhatja `-c` , vagy `-Command` ha olyan műveleteket `powershell.exe Get-Command`próbál végrehajtani, mint a.

### <a name="implement-unicode-escape-parsing-3958httpsgithubcompowershellpowershellissues3958"></a>Unicode Escape-elemzési [#3958](https://github.com/PowerShell/PowerShell/issues/3958) implementálása

`` `u####``vagy `` `u{####}`` a rendszer a megfelelő Unicode-karakterre konvertálja. Egy literál `` `u``kimenetének megmeneküléséhez a kezdő ``` ``u```:.

### <a name="change-new-modulemanifest-encoding-to-utf8nobom-on-non-windows-platforms-3940httpsgithubcompowershellpowershellissues3940"></a>A kódolás módosítása `New-ModuleManifest` a nem Windows platformokra [#3940](https://github.com/PowerShell/PowerShell/issues/3940) `UTF8NoBOM`

Korábban a psd1-jegyzékeket hozlétreUTF-16-banazAJ-vel,ésproblémátokozaLinux-eszközökhöz.`New-ModuleManifest` Ez a feltörési változás megváltoztatja `New-ModuleManifest` a kódolást, hogy UTF legyen (nincs AJ) a nem Windows platformokon.

### <a name="prevent-get-childitem-from-recursing-into-symlinks-1875-3780httpsgithubcompowershellpowershellissues3780"></a>A `Get-ChildItem` symlink-re való rekurzív (#1875) használatának megakadályozása. [#3780](https://github.com/PowerShell/PowerShell/issues/3780)

Ez a változás `Get-ChildItem` többek között a UNIX `ls -r` és a Windows `dir /s` natív parancsaival összhangban áll. Az említett parancsokhoz hasonlóan a parancsmag a rekurzió során talált címtárak szimbolikus hivatkozásait jeleníti meg, de nem veszi át őket.

### <a name="fix-get-content--delimiter-to-not-include-the-delimiter-in-the-returned-lines-3706httpsgithubcompowershellpowershellissues3706"></a>Javítsa `Get-Content -Delimiter` ki, hogy ne szerepeljen a visszaadott sorok elválasztója [#3706](https://github.com/PowerShell/PowerShell/issues/3706)

Korábban a használata `Get-Content -Delimiter` során a kimenet inkonzisztens és nem megfelelő volt, mivel az adatokat további feldolgozást igényel az elválasztó eltávolításához. Ez a módosítás eltávolítja a határolójeleket a visszaadott sorokban.

### <a name="implement-format-hex-in-c-3320httpsgithubcompowershellpowershellissues3320"></a>Format-HEX C# implementálása [#3320](https://github.com/PowerShell/PowerShell/issues/3320)

A `-Raw` paraméter most már "No-op" (nem pedig semmi). Az összes kimenet továbbítása olyan számok valódi ábrázolásával fog megjelenni, amelyek a típushoz tartozó összes bájtot tartalmazzák (amit a `-Raw` paraméter a módosítás előtt formálisan végzett).

### <a name="powershell-as-a-default-shell-doesnt-work-with-script-command-3319httpsgithubcompowershellpowershellissues3319"></a>A PowerShell alapértelmezett rendszerhéjként nem működik a parancsfájl-paranccsal [#3319](https://github.com/PowerShell/PowerShell/issues/3319)

UNIX rendszeren a rendszerhéjak egyezménye, amely egy interaktív `-i` rendszerhéj fogadására szolgál, és számos eszköz várja ezt a`script` viselkedést (például a PowerShell alapértelmezett rendszerhéjként való beállításakor), és a `-i` kapcsolóval hívja meg a rendszerhéjat. Ez a változás abban az esetben `-i` kerül betörésre, hogy a korábban a `-inputformat`lehető legrövidebb megegyezéssel `-in`használható.

### <a name="typo-fix-in-get-computerinfo-property-name-3167httpsgithubcompowershellpowershellissues3167"></a>Sajtóhiba-javítás a Get-ComputerInfo tulajdonság nevében [#3167](https://github.com/PowerShell/PowerShell/issues/3167)

`BiosSerialNumber`a helytelenül lett beírva, `BiosSeralNumber` és a helyes helyesírásra módosult.

### <a name="add-get-stringhash-and-get-filehash-cmdlets-3024httpsgithubcompowershellpowershellissues3024"></a>Hozzáadás `Get-StringHash` és`Get-FileHash` parancsmagok [#3024](https://github.com/PowerShell/PowerShell/issues/3024)

Ez a változás azt jelenti, hogy egyes kivonatoló algoritmusok nem támogatottak a CoreFX, ezért már nem érhetők el:

- `MACTripleDES`
- `RIPEMD160`

### <a name="add-validation-on-get--cmdlets-where-passing-null-returns-all-objects-instead-of-error-2672httpsgithubcompowershellpowershellissues2672"></a>Adja meg `Get-*` az érvényesítést olyan parancsmagokon, amelyeknél a $null a hiba helyett az összes objektumot visszaadja [#2672](https://github.com/PowerShell/PowerShell/issues/2672)

A `$null` következők valamelyikére való továbbításkor hiba történt:

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

### <a name="add-support-w3c-extended-log-file-format-in-import-csv-2482httpsgithubcompowershellpowershellissues2482"></a>A W3C bővített naplófájl-formátum hozzáadása a `Import-Csv` [#2482](https://github.com/PowerShell/PowerShell/issues/2482)

Korábban a `Import-Csv` parancsmag nem használható a naplófájlok közvetlen importálására a W3C bővített naplózási formátumában, és további műveletre lenne szükség. Ezzel a módosítással a W3C bővített naplózási formátuma támogatott.

### <a name="parameter-binding-problem-with-valuefromremainingarguments-in-ps-functions-2035httpsgithubcompowershellpowershellissues2035"></a>Paraméter kötési probléma a `ValueFromRemainingArguments` PS functions-ben [#2035](https://github.com/PowerShell/PowerShell/issues/2035)

`ValueFromRemainingArguments`a most egy tömbként adja vissza az értékeket tömbként, egyetlen érték helyett.

### <a name="buildversion-is-removed-from-psversiontable-1415httpsgithubcompowershellpowershellissues1415"></a>`BuildVersion`eltávolítva a `$PSVersionTable` következőből: [#1415](https://github.com/PowerShell/PowerShell/issues/1415)

Távolítsa `BuildVersion` el a `$PSVersionTable`tulajdonságot a következőből:. Ez a tulajdonság a Windows Build verziójához lett kötve. Ehelyett azt javasoljuk, hogy a paranccsal `GitCommitId` kérje le a PowerShell Core pontos Build verzióját.

### <a name="changes-to-web-cmdlets"></a>Webes parancsmagok módosításai

A webes parancsmagok mögöttes .NET API-t `System.Net.Http.HttpClient`módosították. Ez a változás számos előnyt biztosít. Azonban ez a változás, valamint az Internet Explorer együttműködésének hiánya miatt több megszakítási módosítást eredményezett a `Invoke-WebRequest` és `Invoke-RestMethod`a között.

- `Invoke-WebRequest`a mostantól csak az alapszintű HTML-elemzést támogatja. `Invoke-WebRequest`mindig egy `BasicHtmlWebResponseObject` objektumot ad vissza. A `ParsedHtml` és`Forms` a tulajdonságok el lettek távolítva.
- `BasicHtmlWebResponseObject.Headers`az értékek mostantól `String[]` a `String`helyett vannak.
- `BasicHtmlWebResponseObject.BaseResponse`most egy `System.Net.Http.HttpResponseMessage` objektum.
- A `Response` web cmdlet-kivételek tulajdonsága mostantól egy `System.Net.Http.HttpResponseMessage` objektum.
- Az RFC-fejléc szigorú elemzése mostantól alapértelmezett a `-Headers` és `-UserAgent` a paraméter esetében. Ezt kihagyhatja a `-SkipHeaderValidation`használatával.
- `file://`és `ftp://` az URI-sémák már nem támogatottak.
- `System.Net.ServicePointManager`a beállítások már nem teljesülnek.
- Jelenleg nem érhető el tanúsítvány alapú hitelesítés macOS rendszeren.
- Az URI-n `-Credential` `http://` keresztüli használat hibát eredményez. Használjon URI-t, vagy `-AllowUnencryptedAuthentication` adja meg a paramétert a hiba letiltásához. `https://`
- `-MaximumRedirection`a mostantól megszakítási hibát eredményez, ha az átirányítási kísérletek túllépik a megadott korlátot a legutóbbi átirányítás eredményeinek visszaadása helyett.
