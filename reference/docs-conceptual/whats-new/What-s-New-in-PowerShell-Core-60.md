---
title: A PowerShell Core 6.0 újdonságai
description: Új szolgáltatásokat és módosításokat jelent meg a PowerShell Core 6.0
ms.date: 08/06/2018
ms.openlocfilehash: e1218a38398f4d86829cf2b4ba6a3a882675eaab
ms.sourcegitcommit: 09f02ccef56ef30e7a9ca901f8d3713724960c68
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843921"
---
# <a name="whats-new-in-powershell-core-60"></a>A PowerShell Core 6.0 újdonságai

[A PowerShell Core 6.0][github] van egy új PowerShell kiadása, amely cross-platform (Windows, macOS és Linux), nyílt forráskódú és a heterogén környezetek és a hibrid felhő tervezve.

## <a name="moved-from-net-framework-to-net-core"></a>A .NET-keretrendszer átkerülnek a .NET Core

Használja a PowerShell Core [.NET Core 2.0][] , a modul.
.NET core 2.0 lehetővé teszi, hogy a PowerShell Core (Windows, macOS és Linux), több platformon működik.
A PowerShell Core is elérhetővé teszi a .NET Core 2.0 használható a PowerShell-parancsmagok és parancsfájlok által nyújtott API-készlet.

Windows PowerShell a PowerShell motor használja a .NET-keretrendszer futtatókörnyezete.
Ez azt jelenti, hogy a Windows PowerShell elérhetővé teszi a .NET-keretrendszer által nyújtott API-készlet.

Az API-kat közösen kezelt .NET Core- és .NET-keretrendszer részeként meghatározott [.NET Standard][].

Hogyan befolyásolja ez a PowerShell Core és a Windows PowerShell modul parancsfájl kompatibilitási további információkért lásd: [Backwards kompatibilitás a Windows PowerShell-lel](#backwards-compatibility-with-windows-powershell).

## <a name="support-for-macos-and-linux"></a>MacOS és Linux-támogatása

PowerShell mostantól hivatalosan támogatja macOS és Linux rendszeren, többek között:

- Windows 7, 8.1 és 10
- Windows Server 2008 R2, 2012 R2, 2016
- [A Windows Server féléves csatorna][semi-annual]
- Ubuntu 14.04, 16.04 és 17.04
- Debian 8.7 + és 9
- CentOS 7
- Red Hat Enterprise Linux 7
- OpenSUSE 42.2
- Fedora 25, 26.
- macOS 10.12 +

Közösségünkhöz is hozzájárult a csomagok a következő platformokhoz, de ez nem hivatalosan támogatott:

- Arch Linux
- Kali Linux
- AppImage (több Linux platformon működik)

Kísérleti (nem támogatott) kiadások, az alábbi platformokon van:

- A ARM32/ARM64 Windows
- Raspbian (Stretch)

A módosítások számát történtek a PowerShell Core 6.0-s helyes működéséhez jobban nem Windows rendszereken.
Ezek közül néhányat a rendszer használhatatlanná tévő változásai, amely arra is hatással lehet a Windows.
Mások csak jelen vagy nem Windows-telepítés esetén a PowerShell Core a alkalmazni.

- Támogatás hozzáadva a UNIX rendszerű platformokon a natív parancs helyettesítés.
- A `more` funkció tiszteletben tartja a Linux `$PAGER` és az alapértelmezett `less`.
  Ez azt jelenti, hogy natív bináris/parancsokkal mostantól használhatja a helyettesítő karakterek (például `ls *.txt`). (#3463)
- Záró fordított perjel automatikusan escape-karakterrel megjelölve natív parancssori argumentumok esetén. (#4965)
- Hagyja figyelmen kívül a `-ExecutionPolicy` váltani, ha futtatja a Powershellt a nem Windows platformokon, mert a parancsfájl aláírása nem támogatott. (#3481)
- Tartsa tiszteletben ConsoleHost rögzített `NoEcho` Unix-platformokon. (#3801)
- Rögzített `Get-Help` megkülönbözteti a kis-és nagybetű nincs megkülönböztetve mintaegyeztetésre Unix platformokon támogatásához. (#3852)
- `powershell` csomag hozzáadott Man-lap

### <a name="logging"></a>Naplózás

MacOS-gépeken, a PowerShell használja a natív `os_log` API-k bejelentkezni az Apple [egyesített naplózási rendszer][os_log].
Linux rendszeren használja PowerShell [Syslog][], széles körben használt naplózási megoldást.

### <a name="filesystem"></a>Fájlrendszer

A változások száma hagyományosan nem támogatott a Windows fájlnévkarakterekkel támogatása macOS és Linux rendszeren végzett:

- Parancsmagok megadott utakat most perjel-független (egyaránt / és \ munkahelyi directory elválasztóként)
- Most is érvényesek és alapértelmezés szerint használt XDG alap könyvtár megadása:
  - A Linux/macOS-profil elérési útja a következő helyen található `~/.config/powershell/profile.ps1`
  - Az előzmények mentési útvonala a következő helyen található `~/.local/share/powershell/PSReadline/ConsoleHost_history.txt`
  - A felhasználói modul elérési út a következő helyen található: `~/.local/share/powershell/Modules`
- A kettőspont a Unix tartalmazó fájl- és mappanevek támogatása. (#4959)
- Támogatás a parancsfájl nevét vagy teljes elérési útját, amelyek vesszővel válassza el egymástól. (#4136) (Köszönhetően [ @TimCurwick ](https://github.com/TimCurwick)!)
- Észleli, ha `-LiteralPath` mellőzése a helyettesítő karakterekkel való navigáció parancsmagok segítségével. (#5038)
- Frissített `Get-ChildItem` működéséhez több hasonló a * nix `ls -R` és a Windows `DIR /S` natív parancsokat.
  `Get-ChildItem` most adja vissza a rekurzív a keresés során tapasztalt szimbolikus hivatkozásokat, és nem keres a könyvtárak, amelyek ezeket a hivatkozásokat cél. (#3780)

### <a name="case-sensitivity"></a>Kis-és nagybetűk

Linux és MacOS rendszeren általában kis-és nagybetűket pedig a Windows nem betűérzékeny eset megőrzése mellett.
Általánosságban véve a PowerShell az megkülönbözteti a kis-és nagybetű nincs megkülönböztetve.

Például a környezeti változók-és nagybetűk macOS és Linux rendszeren, ezért a kis-és nagybetűhasználatának a `PSModulePath` szabványosított környezeti változót. (#3255) `Import-Module` nem különbözteti meg meghatározni a modul nevét egy fájl elérési útját használata esetén. (#5097)

## <a name="support-for-side-by-side-installations"></a>Egymás melletti telepítések támogatása

A PowerShell Core telepített, konfigurált, és a Windows Powershellből külön-külön végrehajtva.
A PowerShell Core rendelkezik egy "hordozható" ZIP-csomagját.
A ZIP-csomagját használja, telepítheti tetszőleges számú verzióval bárhonnan, például egy alkalmazást, amely a PowerShell függőségként a helyi lemezen.
Egymás melletti telepítés megkönnyíti a PowerShell és a meglévő szkriptekre áttelepítése új verziói tesztelhetők az idő függvényében.
Egymás mellett is lehetővé teszi a visszamenőleges kompatibilitási, parancsprogramok is kitűzhetők az verzióját, amelyre szükségük.

> [!NOTE]
> Alapértelmezés szerint a Windows az MSI-alapú telepítő hajtja végre a helyben történő frissítés telepítését.
>

## <a name="renamed-powershellexe-to-pwshexe"></a>Átnevezett `powershell(.exe)` , `pwsh(.exe)`

A bináris fájl neve, a PowerShell Core elváltoztatják az `powershell(.exe)` való `pwsh(.exe)`.
Ez a változás lehetővé teszi determinisztikus a felhasználók számára a PowerShell Core gépeken fussanak egymás mellett Windows PowerShell és a PowerShell Core-telepítéseket támogatja.
`pwsh` sokkal rövidebb, és könnyebben írja be, akkor az is.

További módosítások `pwsh(.exe)` a `powershell.exe`:

- Az első Helyzetbeállító paramétere módosítva `-Command` való `-File`.
  Ez a változás javítja a használatát `#!` (más néven a shebangje határoz meg) a PowerShell-parancsfájlok, amelyek a nem Windows platformokon nem PowerShell ismertetése a végrehajtás alatt.
  Azt is jelenti, hogy hasonló parancsokat futtathat `pwsh foo.ps1` vagy `pwsh fooScript` megadása nélkül `-File`.
  Azonban ez a változás megköveteli, hogy Ön kifejezetten megad `-c` vagy `-Command` hasonló parancsok futtatására tett kísérlet során `pwsh.exe -Command Get-Command`. (#4019)
- A PowerShell Core elfogadja a `-i` (vagy `-Interactive`) kapcsoló interaktív shell jelzi. (#3558) Ez lehetővé teszi egy alapértelmezett rendszerhéját Unix platformon használható PowerShell-lel.
- Paraméterek eltávolítása `-importsystemmodules` és `-psconsoleFile` a `pwsh.exe`. (#4995)
- Módosított `pwsh -version` és a beépített súgója `pwsh.exe` igazodni más natív eszközökkel. (#4958 & #4931) (Köszönjük, hogy [ @iSazonov ](https://github.com/iSazonov))
- Érvénytelen argumentum üzenetei `-File` és `-Command` és a kilépési kódokat az Unix szabványok (#4573)
- Hozzáadott `-WindowStyle` Windows paraméterrel. (#4573) Ehhez hasonlóan a csomag-alapú telepítések frissítések nem Windows platformokon helybeni frissítéseket állnak.

## <a name="backwards-compatibility-with-windows-powershell"></a>Visszamenőleges kompatibilitás a Windows PowerShell-lel

A PowerShell Core célja, hogy továbbra is is kompatibilis, amennyire csak lehetséges, a Windows PowerShell-lel.
Használja a PowerShell Core [.NET Standard][] 2.0 meglévő .NET-szerelvények a bináris kompatibilitás érdekében.
Sok PowerShell-modul függenek ezekkel a szerelvényekkel (gyakran időpontokban DLL-ek), így a .NET Standard lehetővé teszi, hogy a .NET Core használatának folytatásához.
A PowerShell Core, nézze meg jól ismert mappák – például a globális szerelvény-gyorsítótár általában tartalmazó lemez – a keresendő függőségek .NET-keretrendszer DLL heurisztikát is tartalmaz.

További információ a .NET Standard az a [.NET Blog][], a jelen [YouTube][] video- és keresztül ez [GYAKORI KÉRDÉSEK][] a Githubon.

Ajánlott erőfeszítéseket annak érdekében, hogy a PowerShell nyelv és a "beépített" modulokat (például `Microsoft.PowerShell.Management`, `Microsoft.PowerShell.Utility`használatához és így tovább) azonos működik, mint a Windows PowerShellben.
Sok esetben a Közösség segítségével hozzáadtunk azok a parancsmagok új funkciókat és hibajavításokat tartalmaz.
Bizonyos esetekben az alapul szolgáló .NET-rétegek, egy hiányzó függőség miatt funkció el lett távolítva, vagy nem érhető el.

A legtöbb, a Windows részét képezi, amelyek (például `DnsClient`, `Hyper-V`, `NetTCPIP`, `Storage`használatához és így tovább) és más Microsoft-termékek, köztük az Azure és az Office nem lettek *explicit módon* már. NET Core még.
A PowerShell csapatának érvényesítéséhez és a meglévő modulokat a PowerShell Core port termék csoportok és csapatok dolgoznak.
A .NET Standard és a [CDXML][], számos, a hagyományos Windows PowerShell-modulok működik a Microsoft a PowerShell Core, de azok nem hivatalosan ellenőrzése és hivatalosan nem támogatják.

Telepítse a [ `WindowsPSModulePath` ][windowspsmodulepath] modult, a használható Windows PowerShell-modulok a Windows PowerShell hozzáfűzésével `PSModulePath` , a PowerShell Core `PSModulePath`.

Először telepítse a `WindowsPSModulePath` modul a PowerShell-galériából:

```powershell
# Add `-Scope CurrentUser` if you're installing as non-admin
Install-Module WindowsPSModulePath -Force
```

Ez a modul telepítése után futtassa a `Add-WindowsPSModulePath` adja hozzá a Windows PowerShell-parancsmagot `PSModulePath` a PowerShell Core:

```powershell
# Add this line to your profile if you always want Windows PowerShell PSModulePath
Add-WindowsPSModulePath
```

## <a name="docker-support"></a>Docker-támogatás

A PowerShell Core Docker-tárolók is nyújtunk támogatást (beleértve a több Linux-disztribúciók, Windows Server Core és a Nano Server) minden főbb platformhoz támogat.

Teljes listáját, tekintse meg a címkéket a [ `microsoft/powershell` a Docker hubon][docker-hub].
További információ a Docker és a PowerShell Core: [Docker][] a Githubon.

## <a name="ssh-based-powershell-remoting"></a>SSH-alapú PowerShell távoli eljáráshívás

A PowerShell távoli eljáráshívás protokoll (PSRP) most már együttműködik a Secure Shell (SSH) protokollt a hagyományos WinRM-alapú PSRP mellett.

Ez azt jelenti, hogy például a parancsmagokat használhatja `Enter-PSSession` és `New-PSSession` és hitelesítéséhez SSH-val.
Mindössze be kell PowerShell regisztrálásához egy alrendszer OpenSSH-alapú SSH-kiszolgálót, és használhatja a meglévő SSH-alapú hitelesítéséhez mechanizmus (például jelszavak vagy titkos kulcsok), a hagyományos `PSSession` szemantikáját.

Konfigurálása és használata a távoli eljáráshívás SSH-alapú további információkért lásd: [PowerShell távoli eljáráshívás ssh-n keresztül][ssh-remoting].

## <a name="default-encoding-is-utf-8-without-a-bom-except-for-new-modulemanifest"></a>Alapértelmezett kódolás az UTF-8, kivéve a New-ModuleManifest AJ nélkül

Múltbeli időpont, például Windows PowerShell-parancsmagok `Get-Content`, `Set-Content` használt különböző, például az ASCII és UTF-16 kódolásokat.
A kódolást alapértelmezés szerint az eltérés problémák létrehozásakor keverése parancsmagok egy kódolást megadása nélkül.

Nem-Windows platformok hagyományosan UTF-8 egy bájt rendelés Mark (AJ) nélkül használja szöveges fájlok alapértelmezett kódolást.
További Windows-alkalmazások és eszközök is távolabbi UTF-16 és AJ nélküli UTF-8 kódolást felé történő áthelyezésének.
A PowerShell Core módosítja az alapértelmezett kódolási megfelel a szélesebb körű rendszereit.

Ez azt jelenti, hogy minden beépített parancsmag, amely használja a `-Encoding` paraméterrel használja a `UTF8NoBOM` az érték alapértelmezés szerint.
A következő parancsmagokat érinti a változás:

- Add-Content
- Export-Clixml
- Export-Csv
- Export-PSSession
- Format-Hex
- Get-Content
- Import-Csv
- Out-File
- SELECT-karakterlánc
- Send-MailMessage
- Set-Content

Ezek a parancsmagok is frissültek, hogy a `-Encoding` univerzálisan paraméterben `System.Text.Encoding`.

Az alapértelmezett érték `$OutputEncoding` UTF-8 is módosult.

Ajánlott eljárásként érdemes explicit módon állítsa be kódolásokat parancsfájlok használatával a `-Encoding` paraméter determinisztikus viselkedés előállításához a különböző platformokon.

`New-ModuleManifest` a parancsmag nem rendelkezik **kódolás** paraméter. A modul jegyzékfájlt (.psd1) fájl kódolási létrehozott `New-ModuleManifest` parancsmag környezettől függ: Ha a PowerShell Core a linuxon futó majd kódolás az UTF-8 (nincs AJ); ellenkező esetben kódolás az UTF-16 (a AJ). (#3940)

## <a name="support-backgrounding-of-pipelines-with-ampersand--3360"></a>Támogatja az és jel folyamatok backgrounding (`&`) (#3360)

Üzembe `&` folyamat végén okozza a folyamat futtatásához PowerShell feladatként.
Ha egy folyamat backgrounded van, egy feladatobjektumot ad vissza.
Ha a folyamat már fut egy feladat, mind a standard `*-Job` parancsmagok segítségével kezelheti a feladat.
Változók (figyelmen kívül hagyja a folyamat-specifikus változók) használt a folyamat automatikusan átmásolja a feladat így `Copy-Item $foo $bar &` ugyanúgy működik.
A feladatot is futtathat, a felhasználó kezdőkönyvtárának helyett az aktuális könyvtárban található.
PowerShell-feladatokkal kapcsolatos további információkért lásd: [about_Jobs](https://msdn.microsoft.com/powershell/reference/6/about/about_jobs).

## <a name="semantic-versioning"></a>Szemantikus verziószámozást

- Végrehajtott `SemanticVersion` kompatibilis `SemVer 2.0`. (#5037) (Köszönjük, hogy [ @iSazonov ](https://github.com/iSazonov)!)
- Módosította az alapértelmezett `ModuleVersion` a `New-ModuleManifest` való `0.0.1` SemVer igazodva. (#4842) (Köszönjük, hogy [ @LDSpits ](https://github.com/LDSpits))
- Hozzáadott `semver` , egy típus accelerator `System.Management.Automation.SemanticVersion`. (#4142) (Köszönhetően [ @oising ](https://github.com/oising)!)
- Kezelőfelületének összehasonlítása az engedélyezett egy `SemanticVersion` példány és a egy `Version` példányt, amely úgy van felépítve csak `Major` és `Minor` verzió értékeket.

## <a name="language-updates"></a>Nyelvi frissítések

- Bemutatjuk a Unicode escape-elemzés, hogy a felhasználók használhatják a Unicode-karaktereket argumentum, a karakterláncok vagy a változó neve. (#3958) (Köszönhetően [ @rkeithhill ](https://github.com/rkeithhill)!)
- A hozzáadott új escape-karakter az ESC Billentyűt: `` `e``
- Mostantól támogatott az átalakítás enumerálások (#4318) karakterláncot a (Köszönjük, hogy [ @KirkMunro ](https://github.com/KirkMunro))
- Rögzített leadó egyetlen elem tömb általános gyűjteményhez. (#3170)
- A hozzáadott karakter tartomány túlterhelési a `..` operátor, így `'a'..'z'` karaktereit adja eredményül. "a" z-ig. (#5026) (Köszönjük, hogy [ @IISResetMe ](https://github.com/IISResetMe)!)
- Rögzített változó-hozzárendelés nem felülírja az írásvédett változók
- Az automatikus változók Hívásiverem leküldése "DottedScopes", amikor szkriptparancsmagok dotting (#4709)
- A felosztási operátor "Egysoros, többsoros" beállítás engedélyezése (#4721) (Köszönjük, hogy [ @iSazonov ](https://github.com/iSazonov))

## <a name="engine-updates"></a>Frissítések

- `$PSVersionTable` négy új tulajdonságokkal rendelkezik:
  - `PSEdition`: A beállított érték `Core` PowerShell Core-on és `Desktop` a Windows PowerShell
  - `GitCommitId`: Ez az a Git-ágak vagy a kód Git véglegesítési Azonosítóját, a PowerShell lett létrehozva.
    A kiadott buildek esetében valószínűleg lesz azonos `PSVersion`.
  - `OS`: Ez az egy operációs rendszer verziója által visszaadott karakterlánc `[System.Runtime.InteropServices.RuntimeInformation]::OSDescription`
  - `Platform`: Ezt adja vissza `[System.Environment]::OSVersion.Platform` értékre van állítva `Win32NT` Windows, a `Unix` MacOS-gépeken, és `Unix` Linux rendszeren.
- Eltávolítja a `BuildVersion` tulajdonságot `$PSVersionTable`.
  Ez a tulajdonság lett szorosan kapcsolódnak a Windows build-verziószáma.
  Ehelyett azt javasoljuk, hogy használjon `GitCommitId` a PowerShell Core pontos buildverziója lekéréséhez. (#3877) (Köszönhetően [ @iSazonov ](https://github.com/iSazonov)!)
- Távolítsa el `ClrVersion` tulajdonságot `$PSVersionTable`.
  Ez a tulajdonság a .NET Core nem számít, és csak továbbra is fennáll, a .NET Core a PowerShell nem vonatkozik konkrét örökölt célokat.
- Három új automatikus változók meghatározni, hogy az egy adott operációs rendszer fut-e a PowerShell hozzáadva: `$IsWindows`, `$IsMacOs`, és `$IsLinux`.
- Adjon hozzá `GitCommitId` a PowerShell Core szalagcím.
  Most nem szükséges futtatni `$PSVersionTable` , amint, indítsa el a Powershellt a verzió beszerzéséhez! (#3916) (Köszönhetően [ @iSazonov ](https://github.com/iSazonov)!)
- Adjon hozzá egy JSON konfigurációs fájl nevű `powershell.config.json` a `$PSHome` indítási idő előtt meg kell adni bizonyos beállítások tárolására (pl. `ExecutionPolicy`).
- Folyamat nem blokkolja a Windows EXE futtatásakor
- COM-gyűjtemények engedélyezett enumerálása. (#4553)

## <a name="cmdlet-updates"></a>Parancsmag-frissítések

### <a name="new-cmdlets"></a>Új parancsmagok

- Adjon hozzá `Get-Uptime` való `Microsoft.PowerShell.Utility`.
- Adjon hozzá `Remove-Alias` parancsot. (#5143) (Köszönjük, hogy [ @PowershellNinja ](https://github.com/PowershellNinja)!)
- Adjon hozzá `Remove-Service` felügyeleti modul. (#4858) (Köszönjük, hogy [ @joandrsn ](https://github.com/joandrsn)!)

### <a name="web-cmdlets"></a>Webes parancsmagjai

- Adja hozzá a tanúsítvány-hitelesítési támogatás a web parancsmagok. (#4646) (Köszönjük, hogy [ @markekraus ](https://github.com/markekraus))
- Adja hozzá a tartalom fejlécek támogatása webes parancsmagok. (#4494 & #4640) (Köszönjük, hogy [ @markekraus ](https://github.com/markekraus))
- Adja hozzá több hivatkozás fejléc támogató webes parancsmagok. (#5265) (Köszönjük, hogy [ @markekraus ](https://github.com/markekraus)!)
- Webes parancsmagok hivatkozás-fej tördelés támogatása (#3828)
  - A `Invoke-WebRequest`, ha a válasz tartalmaz egy hivatkozást a fejlécet, RelationLink tulajdonság létrehozunk egy szótár, az URL-címeket jelölő, és `rel` attribútumok, valamint ellenőrizze, hogy a fejlesztő használandó könnyebben abszolút URL-címek.
  - A `Invoke-RestMethod`, ha a válasz tartalmaz egy hivatkozást a fejlécet, elérhetővé tesszük a `-FollowRelLink` kapcsolót, hogy automatikusan kövesse `next` `rel` hivatkozásokat, amíg azok már nem létezik vagy egyszer azt nyomja le az opcionális `-MaximumFollowRelLink` paraméter értéke.
- Adjon hozzá `-CustomMethod` webes parancsmagokhoz, hogy a nem szabványos módszerrel műveletek paramétert. (#3142) (Köszönhetően [ @Lee303 ](https://github.com/Lee303)!)
- Adjon hozzá `SslProtocol` webes parancsmagok támogatják. (#5329) (Köszönjük, hogy [ @markekraus ](https://github.com/markekraus)!)
- Adja hozzá a többrészes webes parancsmagok támogatása. (#4782) (Köszönjük, hogy [ @markekraus ](https://github.com/markekraus))
- Adjon hozzá `-NoProxy` webes parancsmagok, hogy azok figyelmen kívül hagyja a rendszerre kiterjedő proxy beállítása. (#3447) (Köszönhetően [ @TheFlyingCorpse ](https://github.com/TheFlyingCorpse)!)
- Webes parancsmagok ügynök felhasználói most már az operációs rendszer platform jelentések (#4937) (Köszönjük, hogy [ @LDSpits ](https://github.com/LDSpits))
- Adjon hozzá `-SkipHeaderValidation` váltson webes parancsmagok támogatják a fejlécek hozzáadása a fejléc értéke ellenőrzése nélkül. (#4085)
- Engedélyezze a webes parancsmagok nem érvényesíti a HTTPS-tanúsítvány a kiszolgáló, ha szükséges.
- Hitelesítési paraméterek hozzáadása a webes parancsmagok. (#5052) (Köszönjük, hogy [ @markekraus ](https://github.com/markekraus))
  - Adjon hozzá `-Authentication` , amely három lehetőséget kínál: Alapszintű, OAuth hitelesítéssel és tulajdonosi.
  - Adjon hozzá `-Token` beolvasni a tulajdonosi jogkivonatot OAuth és tulajdonosi beállításait.
  - Adjon hozzá `-AllowUnencryptedAuthentication` a HTTPS-től eltérő bármely átviteli séma biztosított authentication kihagyásához.
- Adjon hozzá `-ResponseHeadersVariable` való `Invoke-RestMethod` válaszfejlécek rögzítését engedélyezéséhez. (#4888) (Köszönjük, hogy [ @markekraus ](https://github.com/markekraus))
- Javítsa ki a webes parancsmagjai a HTTP-válasz szerepeljenek a kivétel, amikor a válaszként kapott állapotkód nem sikeres. (#3201)
- Módosítsa a webes parancsmagok `UserAgent` a `WindowsPowerShell` való `PowerShell`. (#4914) (Köszönjük, hogy [ @markekraus ](https://github.com/markekraus))
- Adjon hozzá kifejezett `ContentType` az észlelési `Invoke-RestMethod` (#4692)
- Javítsa ki a webes parancsmagok `-SkipHeaderValidation` nem szabványos felhasználói ügynök fejlécek dolgozhat. (#4479 & #4512) (Köszönjük, hogy [ @markekraus ](https://github.com/markekraus))

### <a name="json-cmdlets"></a>JSON-parancsmagok

- Adjon hozzá `-AsHashtable` való `ConvertFrom-Json` vissza egy `Hashtable` helyette. (#5043) (Köszönjük, hogy [ @bergmeister ](https://github.com/bergmeister)!)
- Használja a prettier formázó `ConvertTo-Json` kimeneti. (#2787) (Köszönhetően @kittholland!)
- Adjon hozzá `Jobject` szerializálási támogatási `ConvertTo-Json`. (#5141)
- Javítsa ki `ConvertFrom-Json` deszerializálni az adatcsatornából karakterláncok, amelyek együttesen hozhatnak létre a teljes JSON-karakterláncot.
  Ez a bizonyos esetekben, ahol a sortörésekből álló szóközöket tartalmazza megtörnék JSON-elemzési megoldása. (#3823)
- Távolítsa el a `AliasProperty "Count"` definiált `System.Array`.
  Ezzel eltávolítja a felesleges beolvasások `Count` néhány tulajdonság `ConvertFrom-Json` kimeneti. (#3231) (Köszönhetően [ @PetSerAl ](https://github.com/PetSerAl)!)

### <a name="csv-cmdlets"></a>CSV-parancsmagok

- `Import-Csv` most már támogatja a W3C bővített naplófájlformátum (#2482) (Köszönjük, hogy [ @iSazonov ](https://github.com/iSazonov)!)
- Adjon hozzá `PSTypeName` támogatása `Import-Csv` és `ConvertFrom-Csv`. (#5389) (Köszönjük, hogy [ @markekraus ](https://github.com/markekraus)!)
- Győződjön meg arról, `Import-Csv` támogatja `CR`, `LF`, és `CRLF` as sor elválasztó. (#5363) (Köszönjük, hogy [ @iSazonov ](https://github.com/iSazonov)!)
- Győződjön meg arról, `-NoTypeInformation` az alapértelmezett `Export-Csv` és `ConvertTo-Csv`. (#5164) (Köszönjük, hogy [ @markekraus ](https://github.com/markekraus)!)

### <a name="service-cmdlets"></a>Parancsmagok

- Adja hozzá tulajdonságokat `UserName`, `Description`, `DelayedAutoStart`, `BinaryPathName`, és `StartupType` , a `ServiceController` által visszaadott objektumokhoz `Get-Service`. (#4907) (Köszönjük, hogy [ @joandrsn ](https://github.com/joandrsn))
- Hitelesítő adatok beállítása a funkcionalitást `Set-Service` parancsot. (#4844) (Köszönjük, hogy [ @joandrsn ](https://github.com/joandrsn))

### <a name="other-cmdlets"></a>Egyéb parancsmagok

- Adjon hozzá egy paramétert a `Get-ChildItem` nevű `-FollowSymlink` symlinks áthaladó igény szerint, hurkokat hivatkozás ellenőrzése. (#4020)
- Frissítés `Add-Type` támogatásához `CSharpVersion7`. (#3933) (Köszönhetően [ @iSazonov ](https://github.com/iSazonov))
- Távolítsa el a `Microsoft.PowerShell.LocalAccounts` modul mindaddig, amíg talál egy jobb megoldás nem támogatott API-k használata miatt. (#4302)
- Távolítsa el a `*-Counter` parancsmagok a `Microsoft.PowerShell.Diagnostics` mindaddig, amíg talál egy jobb megoldás nem támogatott API-k használata miatt. (#4303)
- Támogatása `Invoke-Item -Path <folder>`. (#4262)
- Adjon hozzá `-Extension` és `-LeafBase` vált, amennyiben az `Split-Path` úgy, hogy akkor is feloszthatja az elérési utak a fájlnév kiterjesztése és a fájlnevet a többi között. (#2721) (Köszönhetően [ @powercode ](https://github.com/powercode)!)
- Paraméterek hozzáadása `-Top` és `-Bottom` való `Sort-Object` az alsó vagy felső N-rendezés
- Egy folyamat szülőfolyamata elérhetővé hozzáadásával a `CodeProperty "Parent"` való `System.Diagnostics.Process`. (#2850) (Köszönhetően [ @powercode ](https://github.com/powercode)!)
- MB memória oszlopait helyett KB-os használata `Get-Process`
- Adjon hozzá `-NoNewLine` a Váltás `Out-String`. (#5056) (Köszönjük, hogy [ @raghav710 ](https://github.com/raghav710))
- `Move-Item` a parancsmag figyelembe veszi `-Include`, `-Exclude`, és `-Filter` paramétereket. (#3878)
- Lehetővé teszi `*` beállításjegyzékbeli elérési út a használandó `Remove-Item`. (#4866)
- Adjon hozzá `-Title` való `Get-Credential` és az azonnali élmény több platformon használja őket egységes előtérrendszerként.
- Adja hozzá a `-TimeOut` paramétert `Test-Connection`. (#2492)
- `Get-AuthenticodeSignature` parancsmagok most már beszerezheti a fájl aláírása időbélyegző. (#4061)
- Távolítsa el a nem támogatott `-ShowWindow` átállás `Get-Help`. (#4903)
- Javítsa ki `Get-Content -Delimiter` nem tartalmazza a kivonni kívánt a tömbelemek rekordsémáját visszaadott a (#3706) (Köszönjük, hogy [ @mklement0 ](https://github.com/mklement0))
- Adjon hozzá `Meta`, `Charset`, és `Transitional` paraméterek `ConvertTo-HTML` (#4184) (Köszönjük, hogy [ @ergo3114 ](https://github.com/ergo3114))
- Adjon hozzá `WindowsUBR` és `WindowsVersion` tulajdonságok `Get-ComputerInfo` eredménye
- Adjon hozzá `-Group` paramétert `Get-Verb`
- Adjon hozzá `ShouldProcess` támogatása a `New-FileCatalog` és `Test-FileCatalog` (kijavítja `-WhatIf` és `-Confirm`). (#3074) (Köszönhetően [ @iSazonov ](https://github.com/iSazonov)!)
- Adjon hozzá `-WhatIf` váltson `Start-Process` parancsmag (#4735) (Köszönjük, hogy [ @sarithsutha ](https://github.com/sarithsutha))
- Adjon hozzá `ValidateNotNullOrEmpty` túl sok meglévő paraméterek.

## <a name="tab-completion"></a>Kiegészítés

- A továbbfejlesztett a típus következtetésekhez a kiegészítés futásidejű változó értékek alapján. (#2744) (Köszönhetően [ @powercode ](https://github.com/powercode)!) Ez lehetővé teszi az olyan helyzetekben, például a kiegészítés:

  ```powershell
  $p = Get-Process
  $p | Foreach-Object Prio<tab>
  ```

- Adja hozzá a kivonattábla kulcsa parancssori kiegészítési `-Property` , `Select-Object`. (#3625) (Köszönhetően [ @powercode ](https://github.com/powercode))
- Argument automatikus kiegészítését a engedélyezése `-ExcludeProperty` és `-ExpandProperty` , `Select-Object`. (#3443) (Köszönhetően [ @iSazonov ](https://github.com/iSazonov)!)
- Javításra került egy kiegészítés győződjön meg arról, hogy a `native.exe --<tab>` fejeznie natív könyvtárba. (#3633) (Köszönhetően [ @powercode ](https://github.com/powercode)!)

## <a name="breaking-changes"></a>Kompatibilitástörő változások

A PowerShell Core 6.0-s kompatibilitástörő változásokat számos jelentettük be.
További őket részletes információ: [használhatatlanná tévő változások a PowerShell Core 6.0-s][breaking-changes].

## <a name="debugging"></a>Hibakeresés

- Távoli step-in kapcsolatos hibakeresés támogatása `Invoke-Command -ComputerName`. (#3015)
- Engedélyezi a binder hibakeresési naplózás a PowerShell Core

## <a name="filesystem-updates"></a>Fájlrendszer-frissítések

- A fájlrendszer-szolgáltatót UNC elérési úton használatának engedélyezése. ($4998)
- `Split-Path` most már működik a UNC-gyökér
- `cd` argumentumok nélkül most úgy viselkedik, mint `cd ~`
- Kijavítva a PowerShell Core elérési utakat legfeljebb 260 karakter hosszú használatának engedélyezésére. (#3960)

## <a name="bug-fixes-and-performance-improvements"></a>Hibajavítások és teljesítménnyel kapcsolatos fejlesztések

Végeztünk *számos* között PowerShell-lel, beleértve az indítási idő, a különféle beépített parancsmagok és a natív bináris való interakció teljesítménnyel kapcsolatos fejlesztések.

Azt is orvosoltuk már számos hiba javítása a PowerShell Core belül.
Javításhoz és módosításhoz teljes listájáért tekintse meg a [változásnaplójában][] a Githubon.

## <a name="telemetry"></a>Telemetria

- A konzol a gazdagép számára a jelentés két PowerShell Core 6.0 hozzáadott telemetriai értékeket (#3620):
  - az operációsrendszer-platform (`$PSVersionTable.OSDescription`)
  - a pontos PowerShell-verzió (`$PSVersionTable.GitCommitId`)

Ha azt szeretné, a telemetria lemond, egyszerűen hozzon létre `POWERSHELL_TELEMETRY_OPTOUT` környezeti változót a következő értékek egyikét: `true`, `1` vagy `yes`.
A változó létrehozása megkerüli az összes telemetriai adat még a PowerShell első futtatása előtt.
Is tervezzük a telemetriai adatok és az elemzések, mi az a telemetriai adatokból glean is közzéteheti a [közösségi irányítópult][community-dashboard].
További információk a módját a jelen használjuk ezeket az adatokat annak [blogbejegyzés][telemetry-blog].

[github]: https://github.com/PowerShell/PowerShell
[.NET Core 2.0]: https://docs.microsoft.com/dotnet/core/
[.NET Standard]: https://docs.microsoft.com/dotnet/standard/net-standard
[os_log]: https://developer.apple.com/documentation/os/logging
[Syslog]: https://en.wikipedia.org/wiki/Syslog
[ssh-remoting]: ../core-powershell/SSH-Remoting-in-PowerShell-Core.md
[breaking-changes]: breaking-changes-ps6.md
[változásnaplójában]: https://github.com/PowerShell/PowerShell/tree/master/CHANGELOG.md
[community-dashboard]: https://aka.ms/PSGitHubBI
[telemetry-blog]: https://blogs.msdn.microsoft.com/powershell/2017/01/31/powershell-open-source-community-dashboard/
[.NET Standard]: https://docs.microsoft.com/dotnet/standard/net-standard
[.NET Blog]: https://blogs.msdn.microsoft.com/dotnet/2016/09/26/introducing-net-standard
[YouTube]: https://www.youtube.com/watch?v=YI4MurjfMn8&list=PLRAdsfhKI4OWx321A_pr-7HhRNk7wOLLY
[GYAKORI KÉRDÉSEK]: https://github.com/dotnet/standard/blob/master/docs/faq.md
[CDXML]: https://msdn.microsoft.com/library/jj542525(v=vs.85).aspx
[docker-hub]: https://hub.docker.com/r/microsoft/powershell/
[docker]: https://github.com/PowerShell/PowerShell/tree/master/docker
[windowspsmodulepath]: https://www.powershellgallery.com/packages/WindowsPSModulePath/
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
