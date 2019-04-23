---
title: A PowerShell Core 6.2 újdonságai
description: Új szolgáltatásaival és módosításaival, amely a PowerShell Core 6.2
ms.date: 03/28/2019
ms.openlocfilehash: 6a0da8a410e602ae3963e0bc7bace745317d7d4b
ms.sourcegitcommit: f4bd4e116e22c8b5bfcb61680a7c42e58b4da93e
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/22/2019
ms.locfileid: "59984493"
---
# <a name="whats-new-in-powershell-core-62"></a>A PowerShell Core 6.2 újdonságai

A PowerShell Core 6.2 kiadásban a teljesítménnyel kapcsolatos fejlesztések, a hibajavítások és a kisebb parancsmag és a nyelvi fejlesztések, hogy javíthassunk összpontosít. Fejlesztések a teljes listájának megtekintéséhez, tekintse meg a részletes [changelogs](https://github.com/PowerShell/PowerShell/releases) a Githubon.

## <a name="experimental-features"></a>Kísérleti funkciók

Korábban a támogatása lehetővé tettük [kísérleti funkciók][]. A 6.2-es kiadásban rendelkezünk, négy kísérleti funkciók kipróbálására. Adja meg a visszajelzéseket, így folyamatosan fejlesztjük is, és eldönteni, hogy a funkciót érdemes elősegítő technikai állapotát.

Használat `Get-ExperimentalFeature` elérhető kísérleti funkciók listáját. Engedélyezheti vagy letilthatja ezeket a funkciókat `Enable-ExperimentalFeature` és `Disable-ExperimentalFeature`.

### <a name="command-not-found-suggestions"></a>A parancs nem található a javaslatok

Ez a funkció használatával intelligens megfelelő elírta parancsokat vagy parancsmagjai javaslatok keresése.

```powershell
Enable-ExperimentalFeature -Name PSCommandNotFoundSuggestion
```

#### <a name="example"></a>Példa

Ebben a példában a hibásan írt parancsmag neve intelligens egyezteti több javaslatok nagy valószínűséggel a legkevésbé valószínű.

```powershell
Get-Commnd
```

```Output
Get-Commnd : The term 'Get-Commnd' is not recognized as the name of a cmdlet, function, script file, or operable program.
Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
At line:1 char:1
+ Get-Commnd
+ ~~~~~~~~~~
+ CategoryInfo          : ObjectNotFound: (Get-Commnd:String) [], CommandNotFoundException
+ FullyQualifiedErrorId : CommandNotFoundException


Suggestion [4,General]: The most similar commands are: Get-Command, Get-Content, Get-Job, Get-Module, Get-Event, Get-Host, Get-Member, Get-Item, Set-Content.
```

### <a name="implicit-remoting-batching"></a>Implicit távelérési kötegelés

Használata esetén [implicit távelérési](https://devblogs.microsoft.com/scripting/remoting-the-implicit-way/) egy folyamatot, a PowerShell kezeli a folyamatban lévő összes parancs egymástól függetlenül. -Objektumok szerializálva vannak ismételten és `de-serialized` az ügyfél és a folyamat végrehajtása a távoli rendszer között.

Ezzel a funkcióval a PowerShell a folyamatot, ha a parancs biztonságosan futtatható-e, és a célrendszeren létezik megállapítja elemzi. TRUE érték esetén a PowerShell távoli végrehajtja a teljes folyamat, és csak szerializálja és `de-serializes` az ügyfél vissza az eredményeket.

```powershell
Enable-ExperimentalFeature -Name PSImplicitRemotingBatching
```

Egy való életből vett teszt `Get-Process | Sort-Object` localhost keresztül csökkenti a 20-30 10 – 15 másodperc **ezredmásodperc**. A funkció csak az ügyfélen engedélyezni kell. Nincs szükség módosításokra a kiszolgálón.

### <a name="temp-drive"></a>Temp Drive

```powershell
Enable-ExperimentalFeature -Name PSTempDrive
```

Ha a PowerShell Core a különböző operációs rendszert használ, azt ismerheti meg, hogy a környezeti változó lehet megkeresni az ideiglenes könyvtár nem azonos a Windows, macOS és Linux! Ezzel a funkcióval kap egy [PSDrive][] nevű `Temp:` , amely automatikusan az operációs rendszerhez használja az ideiglenes mappában van leképezve.

#### <a name="example"></a>Példa

```powershell
PS> "Hello World!" > Temp:/hello.txt
PS> `Get-Content` Temp:/hello.txt
Hello World!
```

Vegye figyelembe, hogy natív parancsok (például `ls` Linux rendszeren) nem PSDrives tudomást, és nem jelenik meg ez `Temp:` meghajtót.

### <a name="abbreviation-expansion"></a>Rövidítése bővítése

PowerShell-parancsmagok várhatóan leíró jellegű szavak. Az eredmény, amelyek nehezen írja be a hosszú névvel. Ez a funkció lehetővé teszi, hogy csak a parancsmag a nagybetűs karaktereket, és -kiegészítés használata való.

```powershell
Enable-ExperimentalFeature -Name PSUseAbbreviationExpansion
```

#### <a name="example"></a>Példa

```powershell
PS> i-arsavsf
```

Ha eléri a lapon, és rendelkezik az Azure PowerShell [Az](https://www.powershellgallery.com/packages/Az) modul telepítve van, akkor az automatikus kiegészítés:

```Output
PS> Import-AzRecoveryServicesAsrVaultSettingsFile
```

> [!NOTE]
> Ez a funkció célja interaktív módon használható. Parancsmagok rövidített formáját nem hajtható végre.
> Ez a funkció nem helyettesíti a aliasok áll.

## <a name="breaking-changes"></a>Kompatibilitástörő változások

- Javítsa ki `-NoEnumerate` viselkedés `Write-Output` konzisztens, a Windows PowerShell-lel. (#9069)
- Győződjön meg arról, `Join-String -InputObject 1,2,3` eredmény egyenlő `1,2,3 | Join-String` (#8611) eredménye (Köszönjük, hogy @sethvs!)
- Adjon hozzá `-Stable` való `Sort-Object` és a kapcsolódó tesztek (#7862) (Köszönjük, hogy @KirkMunro!)
- Javítása `Start-Sleep` parancsmagot, hogy fogadja el a másodperc törtrészével megadott (#8537) (Köszönjük, hogy @Prototyyppi!)
- Kivonattábla OrdinalIgnoreCase használatával kell módosítani `case-insensitive` minden kultúrában (#8566)
- Javítsa ki **LiteralPath** a `Import-Csv` kötést létrehozni `Get-ChildItem` (#8277) kimeneti (Köszönjük, hogy @iSazonov!)
- Dvojité vozovky elválasztó karakter használata a már nem kihagyja az oszlop neve nélkül `Import-Csv` (#7899) (Köszönjük, hogy @Topping!)
- `Get-ExperimentalFeature` már nem rendelkezik `-ListAvailable` váltson (#8318)
- Hibakeresés most paraméterkészlettel `$DebugPreference` való **Folytatás** helyett **Inquire** (#8195) (Köszönjük, hogy @KirkMunro!)
- Honor `-OutputFormat` Ha pwsh együttes nem interaktív, átirányított, a kódolt parancsban megadott (#8115)
- Szerelvény betölthető modul alapútvonal a GAC betöltése előtt (#8073)
- Linux előzetes csomagok eltávolítása a hullámos vonallal (#8244)
- Helyezze át a feldolgozást, `-WorkingDirectory` profiljának feldolgozása előtt (#8079)
- Ne adjon hozzá `PATHEXT` Unix környezeti változóba (#7697) (Köszönjük, hogy @iSazonov!)

## <a name="known-issues"></a>Ismert problémák

- A távelérés Windows IOT ARM platformon modulok betöltése közben probléma lépett rendelkezik. See (#8053)

## <a name="general-updates-and-fixes"></a>Általános frissítések és javítások

- A fájlok és mappák, a kis-és nagybetűket fájlrendszer kis-és parancssori kiegészítés engedélyezése (#8128)
- Győződjön meg arról, PSVersionInfo.PSVersion és PSVersionInfo.PSEdition nyilvános (#8054) (Köszönjük, hogy @KirkMunro!)
- Adja hozzá a típus következtetésekhez `$_`  /  `$PSItem` a `catch{ }` blokkol (#8020) (Köszönjük, hogy @vexx32!)
- Javítsa ki a statikus metódus meghívása típus következtetésekhez (#8018) (Köszönjük, hogy @SeeminglyScience!)
- Következtetett típusainak létrehozása `Select-Object`, `Group-Object`, **PSObject** és **kivonattábla** (#7231) (Köszönjük, hogy @powercode!)
- A hívó módszerének támogatásához `ByRef-like` írja be a paramétereket (#7721)
- Az eset, ahol a Windows PowerShell-modul elérési útja már szerepel a környezetben PSModulePath kezelése (#7727)
- Engedélyezése `SecureString` parancsmagok a Windows tárolja az egyszerű szöveg (#9199)
- Hibaüzenet jelenik meg, nem Windows javíthatja a securestring clixml importálásakor (#7997)
- ReplyTo paraméter hozzáadása a `Send-MailMessage` (#8727) (Köszönjük, hogy @replicaJunction!)
- Adja hozzá az elavult üzenetet `Send-MailMessage` (#9178)
- Javítsa ki `Restart-Computer` dolgozhatnak `localhost` amikor a Rendszerfelügyeleti webszolgáltatások nincs jelen (#9160)
- Győződjön meg arról, `Start-Job` throw megszakítást okozó hiba, ha folyamatban van a PowerShell üzemeltetett (#9128)
- Adjon hozzá C# style típusú gyorsítók és ushort, uint, ulong és rövid literálok utótagok (#7813) (Köszönjük, hogy @vexx32!)
- Tekintse meg a hozzáadott új utótagok numerikus literálok - [about_Numeric_Literals][] (#7901) (Köszönjük, hogy @vexx32!)
- Során Cmdletbinding értéke "true" (#8209), a hatás szintje megfelelően jelentést (Köszönjük, hogy @vexx32!)
- Kérelem karakterkészlet problémák megoldása a weben parancsmagok (#8742) (Köszönjük, hogy @markekraus!)
- Javítsa ki a várt `100-continue` webes parancsmagokban probléma (#8679) (Köszönjük, hogy @markekraus!)
- Javítsa ki a fájl blokkoló problémával webes parancsmagokban (#7676) (Köszönjük, hogy @Claustn!)
- Hárítsa el a problémát elemzés znaková stránka `Invoke-RestMethod` (#8694) (Köszönjük, hogy @markekraus!)
- Refaktorovat `ConvertTo-Json` nyilvános API-ként JsonObject.ConvertToJson elérhetővé (#8682)
- Adja hozzá a konfigurálható maximális mélység `ConvertFrom-Json` az - mélysége (#8199) (Köszönjük, hogy @louistio!)
- Adja hozzá a EscapeHandling paraméter `ConvertTo-Json` parancsmag (#7775) (Köszönjük, hogy @iSazonov!)
- Adjon hozzá `-CustomPipeName` pwsh, és `Enter-PSHostProcess` (#8889)
- Engedélyezze a relatív szimbolikus hivatkozások létrehozása a Windows- `New-Item` (#8783)
- Windows-felhasználók engedélyezése a jogosultságszint-emelés nélkül symlinks létrehozása fejlesztői módban (#8534)
- Engedélyezése `Write-Information` fogadására `$null` (#8774)
- Javítsa ki `Get-Help` MAML speciális függvények biztosíthatja a tartalmak (#8353)
- Javítsa ki `Get-Help` PSTypeName probléma - paramétert, ha csak egy paramétere van deklarálva (#8754) (Köszönjük, hogy @pougetat!)
- Token számítási javítása `Get-Help` ScriptBlock Megjegyzés segítséget hajtja végre. (#8238) (Köszönjük, hogy @hubuk!)
- Változás `Get-Help` parancsmag-karakterláncot fogad el, ezért a paraméter paraméter Tárolótömböket (#8454) (Köszönjük, hogy @sethvs!)
- Oldja meg a tárolóhelyek szolgáltatással SZEMÉLYHÍVÓ, ha az elérési útját tartalmazza (#8571) (Köszönjük, hogy @pougetat!)
- Kérdés hozzáadása használatát `less` a függvényben való kilépéssel (#7998) a felhasználó felkérése a "Súgó"
- Adja hozzá a támogatási enum és char típusok a `Format-Hex` parancsmag (#8191) (Köszönjük, hogy @iSazonov!)
- Távolítsa el a ShouldProcess `Format-Hex` (#8178)
- Az eltolás és a számláló új paraméterek `Format-Hex` és bontani a parancsmag (#7877) (Köszönjük, hogy @iSazonov!)
- Engedélyezi a "name" alias kulcsként "címke" `ConvertTo-Html`, az egész "width" bejegyzés engedélyezése (#8426) (Köszönjük, hogy @mklement0!)
- Gyártmány scriptblock kulcsszó alapján számított tulajdonság működik újra `ConvertTo-Html` (#8427) (Köszönjük, hogy @mklement0!)
- Adja hozzá a parancsmag `Join-String` szöveg létrehozásához (#7660) bemeneti adatcsatornából (Köszönjük, hogy @powercode!)
- Javítsa ki `Join-String` FormatString paraméter logikai parancsmag (#8449) (Köszönjük, hogy @sethvs!)
- Változás `Clear-Host` az `$RAWUI` , és törölje a távoli eljáráshívás munkára (#8609)
- Változás `Clear-Host` egyszerűen volána `[console]::clear` és egyértelmű alias eltávolítása a Unix (#8603)
- Javítsa ki a LiteralPath `Import-Csv` kötést létrehozni `Get-ChildItem` (#8277) kimeneti (Köszönjük, hogy @iSazonov!)
- Súgó funkciót nem szabad használni stránkování AliasHelpInfo (#8552)
- Adjon hozzá `-UseMinimalHeader` való `Start-Transcript` átiratok fejléc minimalizálása érdekében (#8402) (Köszönjük, hogy @lukexjeremy!)
- Adjon hozzá `Enable-ExperimentalFeature` és `Disable-ExperimentalFeature` parancsmagok (#8318)
- Tegye elérhetővé az összes parancsmag **PSDiagnostics** logman.exe esetén érhető el (#8366)
- Távolítsa el **megőrzése** paramétert `New-PSDrive` a `non-Windows` platform (#8291) (Köszönjük, hogy @lukexjeremy!)
- Támogatása `cd +` (#7206) (Köszönjük, hogy @bergmeister!)
- Engedélyezése `Set-Location -LiteralPath` nevű - mappák dolgozhat és + (#8089)
- `Test-Path` adja vissza `$false` Ha megadott egy üres vagy `$null` elérési útja (#8080) értéket (Köszönjük, hogy @vexx32!)
- Dinamikus paraméterek kell visszaadni, még akkor is, ha az elérési út nem egyezik meg a bármely szolgáltatónál engedélyezése (#7957)
- Támogatási `Get-PSHostProcessInfo` és `Enter-PSHostProcess` Unix platformokon (#8232)
- Csökkentse a hozzárendelések `Get-Content` parancsmag (#8103) (Köszönjük, hogy @iSazonov!)
- Engedélyezése `Add-Content` olvasási hozzáférés megosztása más eszközökkel tartalom írása közben (#8091)
- `Get/Add-Content` javult a hibajelentések jelez, ha egy tároló célzó (#7823) (Köszönjük, hogy @kvprasoon!)
- Adjon hozzá `-Name`, `-NoUserOverrides` és `-ListAvailable` paraméterek `Get-Culture` parancsmag (#7702) (Köszönjük, hogy @iSazonov!)
- Adja hozzá az egységes attribútum befejezésére vonatkozó **kódolás** paraméter. (#7732) (Köszönjük, hogy @ThreeFive-O!)
- Numerikus azonosítók és nevét, a regisztrált kódlapok **kódolás** paraméterek (#7636) (Köszönjük, hogy @iSazonov!)
- Javítsa ki `Rename-Item -Path` a helyettesítő karakter (#7398) (Köszönjük, hogy @kwkam!)
- Használata esetén `Start-Transcript` és a fájl létezik, nem üres fájl törlésekor (#8131) nál (Köszönjük, hogy @paalbra!)
- Győződjön meg arról, `Add-Type` nyissa meg a forrásfájlokat **FileAccess.Read** és **Funkce** explicit módon (#7915) (Köszönjük, hogy @IISResetMe!)
- Javítsa ki `Enter-PSSession -ContainerId` számára a legújabb Windows (#7883)
- Győződjön meg, hogy **NestedModules** tulajdonság tölti fel a rendszer által `Test-ModuleManifest` (#7859)
- Adjon hozzá `%F` megkülönbözteti a kis, `Get-Date` - UFormat (#7630) (Köszönjük, hogy @britishben!)
- Javítsa ki `Set-Service -Status Stopped` függőségekkel rendelkező szolgáltatások leállítása (#5525) (Köszönjük, hogy @zhenggu!)

<!-- Link references -->
[about_Numeric_Literals]: /powershell/module/Microsoft.PowerShell.Core/About/about_numeric_literals
[Kísérleti funkciók]: /powershell/module/Microsoft.PowerShell.Core/About/about_Experimental_Features
[PSDrive]: /powershell/module/microsoft.powershell.management/new-psdrive
