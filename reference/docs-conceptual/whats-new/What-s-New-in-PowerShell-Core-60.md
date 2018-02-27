# <a name="whats-new-in-powershell-core-60"></a>What's New in PowerShell Core 6.0

[PowerShell Core 6.0] [ github] platformfüggetlen (a Windows, a macOS és a Linux), amely PowerShell új kiadását, nyílt forráskódú, és beépített heterogén környezetben és a hibrid felhő.

## <a name="moved-from-net-framework-to-net-core"></a>A .NET-keretrendszer átkerülnek a .NET Core

PowerShell Core használ [.NET Core 2.0][] , a futtatókörnyezet.
A .NET core 2.0 lehetővé teszi, hogy a PowerShell alapvető működéséhez a több platformon (a Windows, a macOS és a Linux).
PowerShell Core is elérhetővé teszi a .NET Core 2.0-s verzióját a PowerShell-parancsmagok és parancsfájlok által nyújtott API-készlet.

A Windows PowerShell a .NET-keretrendszer futtatókörnyezete a PowerShell-motor tárolására szolgálnak.
Ez azt jelenti, hogy a Windows PowerShell elérhetővé teszi a .NET-keretrendszer által nyújtott API-készlet.

A .NET Core és a .NET-keretrendszer között megosztott API-k részeként meghatározott [.NET-szabvány][].

Hogyan befolyásolja ez a modul, a parancsfájl kompatibilitási PowerShell Core és a Windows PowerShell között további információkért lásd: [Backwards kompatibilitás a Windows PowerShell-lel](#backwards-compatibility-with-windows-powershell).

## <a name="support-for-macos-and-linux"></a>MacOS és Linux támogatása

PowerShell mostantól hivatalosan támogatja macOS és a Linux, beleértve:

- Windows 7, 8.1 és 10
- Windows Server 2008 R2, 2012 R2, 2016
- [Windows Server pontosvesszővel éves csatorna][semi-annual]
- Ubuntu 14.04, 16.04 és 17.04
- Debian 8.7 + és 9
- CentOS 7
- Red Hat Enterprise Linux 7
- OpenSUSE 42.2
- Fedora 25, 26
- macOS 10.12 +

A Közösség emellett hozzájárult csomagok a következő platformokat, de hivatalosan nem támogatják:

- Linux architektúrája
- Kali Linux
- AppImage (működik a több Linux platformon)

A következő platformokat kísérleti (nem támogatott) kiadásokban is van:

- A Windows ARM32/ARM64
- Raspbian (Stretch)

Módosításokat végzett PowerShell Core 6.0 abba, hogy a nem Windows rendszerek együttműködését.
Néhány esetben bontja Windows is érintő módosítások.
Mások csak jelen, vagy a nem Windows PowerShell Core telepítései alkalmazható.

- A Unix rendszerek natív parancs helyettesítés támogatása.
- A `more` funkció tiszteletben tartja a Linux `$PAGER` , alapértelmezett `less`.
  Ez azt jelenti, használhatja a helyettesítő karakterek natív bináris-parancsok (például `ls *.txt`). (#3463)
- Záró perjelet automatikusan escape-karakterrel megjelölve a natív parancsargumentumok meghatározásakor. (#4965)
- Figyelmen kívül hagyja a `-ExecutionPolicy` váltani, ha a nem Windows platformokon futó PowerShell, mert parancsfájl aláíró jelenleg nem támogatott. (#3481)
- Rögzített ConsoleHost tiszteletben `NoEcho` Unix platformokon. (#3801)
- Rögzített `Get-Help` támogatja a kis-és nagybetűket mintaegyezéshez Unix platformokon. (#3852)
- `powershell` a csomaghoz adott Man-lap

### <a name="logging"></a>Naplózás

MacOS, a PowerShell szolgáltatás használ a natív `os_log` API-k bejelentkezni az Apple [egyesített naplózási rendszer][os_log].
Linux, PowerShell használ [Syslog][], a széles körű naplózás megoldást.

### <a name="filesystem"></a>Filesystem

Módosításokat végzett macOS és Linux hagyományosan nem támogatott a Windows fájlnévkarakterekkel támogatásához:

- Parancsmagok megadott elérési útvonalai most törtvonallal-független (mind / és \ munkahelyi directory elválasztójelként)
- Most tiszteletben és alapértelmezés szerint használt XDG Base könyvtár megadása:
  - A Linux/macOS profil elérési út található: `~/.config/powershell/profile.ps1`
  - Az előzmények elérési útvonalat mentéséhez itt található: `~/.local/share/powershell/PSReadline/ConsoleHost_history.txt`
  - A felhasználó a modul elérési út található: `~/.local/share/powershell/Modules`
- A kettőspont a Unix tartalmazó fájl- és mappanevek támogatása. (#4959)
- Támogatás a parancsfájl nevét vagy teljes elérési rendelkező vesszővel válassza el egymástól. (#4136) (Köszönet a következőknek @TimCurwick!)
- Észlelés, ha `-LiteralPath` arra, hogy letiltsa a helyettesítő karakterekkel való navigációs parancsmagok szolgál. (#5038)
- Frissített `Get-ChildItem` működéséhez további hasonló a * nix `ls -R` és a Windows `DIR /S` natív parancsok.
  `Get-ChildItem` most adja vissza a szimbolikus csatolást közben rekurzív keresését, és a könyvtárak nem keres, amely ezeket a hivatkozásokat cél. (#3780)

### <a name="case-sensitivity"></a>Nagybetűk

Linux- és macOS általában kis-és nagybetűket pedig a Windows nem betűérzékeny eset adatainak megőrzése mellett.
PowerShell általában kis-és nagybetűket.

Például a környezeti változók-és nagybetűk macOS és a Linux, ezért a használttól a `PSModulePath` szabványosított környezeti változó. (#3255) `Import-Module` rendszer-és nagybetűket, egy fájl elérési útját annak meghatározásához, a modul neve használata esetén. (#5097)

## <a name="support-for-side-by-side-installations"></a>Egymás melletti telepítések támogatása

PowerShell Core telepítve, konfigurálva, és a Windows PowerShell külön-külön végrehajtani.
PowerShell Core rendelkezik egy "hordozható" ZIP-csomagját.
Segítségével a ZIP-csomagját, telepíthet verziók tetszőleges számú bárhonnan, például egy alkalmazást, amely PowerShell függőségei a helyi lemezen.
Egymás melletti telepítés megkönnyíti a PowerShell és a meglévő parancsfájlok áttelepítése új verzióinak tesztelésére adott idő alatt.
Egymás melletti is lehetővé teszi a visszamenőleges kompatibilitás, parancsfájlok rögzíthet meghatározott verziója, amelyre szükségük van.

> [!NOTE]
> Alapértelmezés szerint a MSI-alapú telepítő Windows helybeni frissítés telepítését végzi.
>

## <a name="renamed-powershellexe-to-pwshexe"></a>Átnevezett `powershell(.exe)` számára `pwsh(.exe)`

A PowerShell Core bináris neve módosult `powershell(.exe)` való `pwsh(.exe)`.
Ez a változás determinisztikus módon biztosít a felhasználók gépen futtatandó PowerShell Core egymás mellett a Windows PowerShell és a PowerShell Core-telepítések támogatásához.
`pwsh` sokkal rövidebb, és írja be a könnyebben is.

A további módosításokat `pwsh(.exe)` a `powershell.exe`:

- Az első pozícióparaméter megváltozott `-Command` való `-File`.
  Ez a változás kijavítja az használatát `#!` (más néven a egy shebang) a PowerShell-parancsfájlok, amelyek hajtja végre a nem Windows platformokon nem PowerShell ismertetése.
  Azt is jelenti, hogy futtatható-e parancsok például `pwsh foo.ps1` vagy `pwsh fooScript` megadása nélkül `-File`.
  Azonban ez a változás megköveteli, hogy Ön kifejezetten megad `-c` vagy `-Command` például parancsok végrehajtásakor `pwsh.exe -Command Get-Command`. (#4019)
- PowerShell Core elfogadja a `-i` (vagy `-Interactive`) kapcsoló egy interaktív rendszerhéj jelzi. (#3558) Ez lehetővé teszi egy alapértelmezett rendszerhéját Unix platformokon használandó PowerShell.
- Eltávolítja a paraméterek `-importsystemmodules` és `-psconsoleFile` a `pwsh.exe`. (#4995)
- Módosított `pwsh -version` és beépített súgóját `pwsh.exe` való megfelelés érdekében natív eszközöket használhatja. (#4958 & #4931) (Köszönjük @iSazonov)
- Érvénytelen argumentum hibaüzenetekben `-File` és `-Command` és kilépési kódokat Unix szabványok konzisztens (#4573)
- Hozzáadott `-WindowStyle` Windows paraméter. (#4573) Hasonlóképpen csomag-alapú telepítések nem Windows platformokon frissítései helybeni frissítéseket.

## <a name="backwards-compatibility-with-windows-powershell"></a>Visszamenőleges kompatibilitás a Windows PowerShell használatával

PowerShell Core célja szerint kompatibilis, a lehető a Windows PowerShell maradjon.
PowerShell Core használ [.NET-szabvány][] 2.0-s verzióját adja meg a meglévő .NET-szerelvények bináris kompatibilisek.
Számos PowerShell-modult függenek e szerelvények (gyakran időpontokban DLL-ek), így a .NET-szabvány lehetővé teszi a .NET Core platformmal a munka folytatásához.
PowerShell központ is ebben a jól ismert mappák – például ha a globális szerelvény-gyorsítótárban általában lemezen található--található a .NET Framework függőségeit heurisztikát.

További információ a .NET-szabvány a a [.NET Blog][], ezen [YouTube][] video-, és ez keresztül [gyakran ismételt kérdések][] a Githubon.

Ajánlott erőfeszítéseket annak érdekében, hogy a PowerShell nyelvet és a "beépített" modulokat (például `Microsoft.PowerShell.Management`, `Microsoft.PowerShell.Utility`stb) azonos működik, mint a Windows PowerShellben.
Sok esetben a Közösség segítségével a Microsoft új funkcióit és hibajavításait javításokat való felvételét e parancsmagok.
Bizonyos esetekben az alapul szolgáló .NET rétegek, egy hiányzó függőség miatt funkció el lett távolítva, vagy nem érhető el.

Nagy része a Windows részét képezi modulok (például `DnsClient`, `Hyper-V`, `NetTCPIP`, `Storage`stb) és más Microsoft-termékek, köztük az Azure és az Office még nem lettek *explicit módon* használatát. NET Core még.
A PowerShell csoport ezen csoportok és a csoportok érvényesítése és porttal, a meglévő PowerShell Core-modulok dolgozik.
A .NET-szabvány és [CDXML][], a hagyományos Windows PowerShell-modulok többsége tűnik, hogy működik a PowerShell-Core, de azok nem hivatalosan érvényesítése és hivatalosan nem támogatják.

Telepítse a [ `WindowsPSModulePath` ] [ windowspsmodulepath] modul, használhatja a Windows PowerShell-modul a Windows PowerShell hozzáfűzésével `PSModulePath` a PowerShell képességének `PSModulePath`.

Először telepítse a `WindowsPSModulePath` a PowerShell-galériából modul:

```powershell
# Add `-Scope CurrentUser` if you're installing as non-admin 
Install-Module WindowsPSModulePath -Force
```

Ez a modul telepítése után futtassa a `Add-WindowsPSModulePath` parancsmaggal adja hozzá a Windows PowerShell `PSModulePath` képességének PowerShell:

```powershell
# Add this line to your profile if you always want Windows PowerShell PSModulePath
Add-WindowsPSModulePath
```

## <a name="docker-support"></a>Docker-támogatás

PowerShell Core támogatást biztosít a Docker-tárolók a fő platformokon támogatott (beleértve a több Linux disztribúciókkal, a Windows Server Core és a Nano Server).

Teljes listájáért tekintse meg a címkék a [ `microsoft/powershell` Docker hub][docker-hub].
A Docker és a PowerShell Core további információkért lásd: [Docker][] a Githubon.

## <a name="ssh-based-powershell-remoting"></a>SSH-alapú PowerShell távvezérlése

A PowerShell távelérése protokoll (PSRP) most már működik a Secure Shell (SSH) protokoll a hagyományos WinRM-alapú PSRP mellett.

Ez azt jelenti, hogy például parancsmagokat használhatja `Enter-PSSession` és `New-PSSession` és hitelesíti az SSH használatával.
Meg kell nyitnia az összes PowerShell regisztrálható az OpenSSH-alapú SSH-kiszolgálót egy alrendszer, és használhatja a meglévő SSH-alapú hitelesítés szerkezetek (például a jelszavak és a titkos kulcsok) a hagyományos `PSSession` szemantikáját.

Konfigurálásával és használatával SSH-alapú távelérési további információkért lásd: [PowerShell távvezérlése SSH-n keresztül][ssh-remoting].

## <a name="default-encoding-is-utf-8-without-a-bom"></a>Alapértelmezett kódolás az UTF-8 AJ nélkül

A múltban, például a Windows PowerShell-parancsmagok `Get-Content`, `Set-Content` használt eltérő, például az ASCII és UTF-16 kódolást.
A varianciája, akkor az alapértelmezett problémák létrehozásakor parancsmagok keverése kódolással megadása nélkül.

Nem Windows platformokon hagyományosan UTF-8 nélkül bájt rendelés be van jelölve (AJ) használja a használt alapértelmezett kódolást szövegfájlok.
További Windows-alkalmazások és eszközök olyan áthelyezése elhagyja az UTF-16 és felé AJ nélküli UTF-8 kódolást.
PowerShell Core felel meg a szélesebb körű ökoszisztéma a kódolást alapértelmezés szerint változik.

Ez azt jelenti, hogy az összes beépített parancsmag, amely használja a `-Encoding` paraméter használata a `UTF8NoBOM` értéke alapértelmezés szerint.
Ez a változás által érintett a következő parancsmagokat:

- Tartalom hozzáadása
- Export-Clixml
- Export-Csv
- Export-PSSession
- Hexadecimális formátumú
- Get-Content
- Import-Csv
- Új ModuleManifest
- Out-File
- SELECT-karakterlánc
- Send-MailMessage
- Set-Content

Ezeket a parancsmagokat is frissítve lett, hogy a `-Encoding` paraméter egységesen fogad el `System.Text.Encoding`.

Az alapértelmezett érték `$OutputEncoding` is UTF-8 megváltozott.

Ajánlott eljárásként, explicit módon célszerű kódolások a parancsfájlok használata a `-Encoding` paraméter a különböző platformokon kiszámíthatóbb viselkedést eredményez.

## <a name="support-backgrounding-of-pipelines-with-ampersand--3360"></a>Támogatja az adatcsatornák az és jel backgrounding (`&`) (#3360)

Ha `&` folyamat végén hatására a folyamat egy PowerShell feladat rendszergazdaként kell futtatni.
Ha egy folyamat backgrounded van, egy feladatobjektumot ad vissza.
Amennyiben az a folyamat fut, mint egy feladatot, az összes normál `*-Job` parancsmag is használható a feladat kezeléséhez.
A feldolgozási soros (figyelmen kívül hagyva folyamatokra vonatkozó változók) változók automatikusan kerülnek a feladatot úgy `Copy-Item $foo $bar &` megoldás.
A feladatot is végre az aktuális könyvtárban található helyett a felhasználó saját könyvtárához.
PowerShell feladatok kapcsolatos további információkért lásd: [about_Jobs](https://msdn.microsoft.com/powershell/reference/6/about/about_jobs).

## <a name="semantic-versioning"></a>A szemantikai versioning

- Végrehajtott `SemanticVersion` kompatibilis `SemVer 2.0`. (#5037) (Köszönjük @iSazonov!)
- Módosította az alapértelmezett `ModuleVersion` a `New-ModuleManifest` való `0.0.1` való megfelelés érdekében SemVer. (#4842) (Köszönjük @LDSpits)
- Hozzáadott `semver` , egy típus gyorsító a `System.Management.Automation.SemanticVersion`. (#4142) (Köszönet a következőknek @oising!)
- Engedélyezett összehasonlítása a `SemanticVersion` példány és egy `Version` csak a létrehozott példány `Major` és `Minor` verzióértékek.

## <a name="language-updates"></a>Nyelvi frissítések

- Valósítja meg, hogy a felhasználók használhatják a Unicode-karaktereket argumentumok, karakterláncok vagy változónevek elemzése Unicode karaktert. (#3958) (Köszönet a következőknek @rkeithhill!)
- A hozzáadott új escape-karakter az ESC Billentyűt: `` `e``
- Felsorolások számára (#4318) karakterlánc alakításának támogatása (Köszönjük @KirkMunro)
- Rögzített adattípusokról egyelemű tömböt az általános gyűjteményben. (#3170)
- A hozzáadott karakter tartomány túlterhelési a `..` operátor, így `'a'..'z'` karaktereit adja eredményül. "a" – "z". (#5026) (Köszönjük @IISResetMe!)
- Rögzített változó-hozzárendelés nem felülírja az írásvédett változók
- Automatikus változók lokális változó leküldése "DottedScopes", ha a parancsfájl parancsmagok dotting (#4709)
- Engedélyezze az "Singleline, többsoros" lehetőség a felosztási operátor (#4721) (Köszönjük @iSazonov)

## <a name="engine-updates"></a>Frissítések

- `$PSVersionTable` négy új tulajdonságokkal rendelkezik:
  - `PSEdition`: A beállított érték `Core` PowerShell alapvető és `Desktop` a Windows PowerShell
  - `GitCommitId`: Ez az a Git commit azonosítója a Git fiók vagy a címke ahol PowerShell lett létrehozva.
    A kiadott buildek, azt valószínűleg találkozik majd olyan azonos `PSVersion`.
  - `OS`: Ez az az operációs rendszer által visszaadott verzió-karakterlánca `[System.Runtime.InteropServices.RuntimeInformation]::OSDescription`
  - `Platform`: A rendszer által visszaadott `[System.Environment]::OSVersion.Platform` érték `Win32NT` Windows, a `MacOSX` a macOS, és `Unix` Linux.
- Eltávolítja a `BuildVersion` tulajdonságot `$PSVersionTable`.
  Ez a tulajdonság erősen volt kötve a Windows verzió buildszámával.
  Ehelyett azt javasoljuk, hogy használjon `GitCommitId` PowerShell Core pontos buildszámának beolvasása. (#3877) (Köszönet a következőknek @iSazonov!)
- Távolítsa el `ClrVersion` tulajdonságot `$PSVersionTable`.
  Ez a tulajdonság a .NET Core nem számít, és csak továbbra is fennáll, a .NET Core konkrét örökölt céljából, amelyek a PowerShell küldésével.
- Annak meghatározásához, hogy fut-e egy adott operációs rendszer PowerShell három új automatikus változók hozzáadott: `$IsWindows`, `$IsMacOs`, és `$IsLinux`.
- Adja hozzá `GitCommitId` PowerShell Core fejléc számára.
  Most futtatásához nincs `$PSVersionTable` , amint a verzióval PowerShell elindítása! (#3916) (Köszönet a következőknek @iSazonov!)
- Nevű JSON-konfigurációs fájl hozzáadása `powershell.config.json` a `$PSHome` néhány indítási idő előtt szükséges beállításokat tárolja (pl. `ExecutionPolicy`).
- Feldolgozási sor nincs blokkolás Windows EXE futtatásakor
- A COM-gyűjtemények engedélyezett számbavétele. (#4553)

## <a name="cmdlet-updates"></a>A parancsmag frissítések

### <a name="new-cmdlets"></a>Új parancsmagok

- Adja hozzá `Get-Uptime` való `Microsoft.PowerShell.Utility`.
- Adja hozzá `Remove-Alias` parancsot. (#5143) (Köszönjük @PowershellNinja!)
- Adja hozzá `Remove-Service` felügyeleti modulra. (#4858) (Köszönjük @joandrsn!)

### <a name="web-cmdlets"></a>Webes parancsmagjai

- Vegye fel a tanúsítvány-hitelesítési támogatás a webes parancsmagjai. (#4646) (Köszönjük @markekraus)
- Támogatja a tartalomfejléceket hozzá webes parancsmagjai. (#4494 & #4640) (Köszönjük @markekraus)
- Több hivatkozás fejléc támogatás hozzáadása a webes parancsmagjai. (#5265) (Köszönjük @markekraus!)
- Hivatkozás fejléc tördelési támogatja a web-parancsmagokban (#3828)
  - A `Invoke-WebRequest`, ha a válasz tartalmazza azt az URL-címek képviselő Dictionary RelationLink tulajdonság létrehozása hivatkozás fejléc és `rel` attribútumok közül, biztosítsa, hogy az URL-címek abszolút könnyebb a fejlesztő használatára.
  - A `Invoke-RestMethod`, ha a válasz tartalmaz egy hivatkozást a fejlécet, elérhetővé kell tenni egy `-FollowRelLink` kapcsolót, hogy automatikusan `next` `rel` hivatkozások, amíg nem létezik vagy egyszer azt elérte az opcionális `-MaximumFollowRelLink` paraméter értékét.
- Adja hozzá `-CustomMethod` webes parancsmagok segítségével lehetővé teszik a nem szabványos metódus műveletek paramétert. (#3142) (Köszönet a következőknek @Lee303!)
- Adja hozzá `SslProtocol` támogatja a Web parancsmagok. (#5329) (Köszönjük @markekraus!)
- Adja hozzá a többrészes webes parancsmagjai a támogatási szolgálathoz. (#4782) (Köszönjük @markekraus)
- Adja hozzá `-NoProxy` webes parancsmagjainak, így azok figyelmen kívül hagyni a rendszerszintű proxybeállítást. (#3447) (Köszönet a következőknek @TheFlyingCorpse!)
- Webes parancsmagjai ügynök felhasználói most jelenti az operációs rendszer platform (#4937) (Köszönjük @LDSpits)
- Adja hozzá `-SkipHeaderValidation` váltani a webalkalmazás-parancsmagokat támogatja a fejlécek hozzáadását a fejléc értékének ellenőrzése nélkül. (#4085)
- Engedélyezze a webes parancsmagok nem érvényesíti a HTTPS-tanúsítvány a kiszolgáló, ha szükséges.
- Hitelesítési paraméterek hozzáadása a webes parancsmagjai. (#5052) (Köszönjük @markekraus)
  - Adja hozzá `-Authentication` , amely három lehetőséget kínál: Basic, az OAuth és a tulajdonosi.
  - Adja hozzá `-Token` megszerezni a tulajdonosi jogkivonatot OAuth és a tulajdonosi beállításait.
  - Adja hozzá `-AllowUnencryptedAuthentication` bármely átviteli séma nem HTTPS biztosított hitelesítési kihagyásához.
- Adja hozzá `-ResponseHeadersVariable` való `Invoke-RestMethod` válaszfejlécek rögzítése engedélyezéséhez. (#4888) (Köszönjük @markekraus)
- Javítsa ki a webes parancsmagjai a HTTP-válasz szerepeljenek a kivételt, ha a válasz állapotkódja nem sikeres. (#3201)
- Módosítsa a webes parancsmagjai `UserAgent` a `WindowsPowerShell` való `PowerShell`. (#4914) (Köszönjük @markekraus)
- Adja hozzá a explicit `ContentType` az észlelési `Invoke-RestMethod` (#4692)
- Javítsa ki a webes parancsmagjai `-SkipHeaderValidation` nem szabványos felhasználói ügynök fejlécek együttműködni. (#4479 & #4512) (Köszönjük @markekraus)

### <a name="json-cmdlets"></a>JSON-parancsmagok

- Adja hozzá `-AsHashtable` való `ConvertFrom-Json` vissza egy `Hashtable` helyette. (#5043) (Köszönjük @bergmeister!)
- Használja a prettier formázó `ConvertTo-Json` kimeneti. (#2787) (Köszönet a következőknek @kittholland!)
- Adja hozzá `Jobject` szerializálási támogatási `ConvertTo-Json`. (#5141)
- Javítsa ki `ConvertFrom-Json` deszerializálni a láncból karakterláncok, amelyek együtt összeállításához teljes JSON karakterláncnak.
  Ez javítja az egyes esetekben, ahol ágyazódjanak elemzése JSON megszűnését. (#3823)
- Távolítsa el a `AliasProperty "Count"` definiált `System.Array`.
  Ezzel eltávolítja a felesleges `Count` egyes tulajdonság `ConvertFrom-Json` kimeneti. (#3231) (Köszönet a következőknek @PetSerAl!)

### <a name="csv-cmdlets"></a>CSV-parancsmagok

- Adja hozzá `PSTypeName` támogatása `Import-Csv` és `ConvertFrom-Csv`. (#5389) (Köszönjük @markekraus!)
- Ellenőrizze `Import-Csv` támogatja `CR`, `LF`, és `CRLF` regisztrációja, mivel sor elválasztó karaktert. (#5363) (Köszönjük @iSazonov!)
- Ellenőrizze `-NoTypeInformation` az alapértelmezett `Export-Csv` és `ConvertTo-Csv`. (#5164) (Köszönjük @markekraus)

### <a name="service-cmdlets"></a>Parancsmagok

- Adja hozzá a Tulajdonságok `UserName`, `Description`, `DelayedAutoStart`, `BinaryPathName`, és `StartupType` számára a `ServiceController` által visszaadott objektumokhoz `Get-Service`. (#4907) (Köszönjük @joandrsn)
- Adja hozzá a hitelesítő adatok beállíthat az `Set-Service` parancsot. (#4844) (Köszönjük @joandrsn)

### <a name="other-cmdlets"></a>Más parancsmagok

- A paraméter hozzáadása `Get-ChildItem` nevű `-FollowSymlink` symlinks áthaladó az igény szerinti kapcsolat hurkok keres. (#4020)
- Frissítés `Add-Type` támogatásához `CSharpVersion7`. (#3933) (Köszönet a következőknek @iSazonov)
- Távolítsa el a `Microsoft.PowerShell.LocalAccounts` modul, amíg meg nem találja egy jobb megoldás nem támogatott API-k használata miatt. (#4302)
- Távolítsa el a `*-Counter` parancsmagok a `Microsoft.PowerShell.Diagnostics` amíg meg nem találja egy jobb megoldás nem támogatott API-k használata miatt. (#4303)
- Támogatást `Invoke-Item -Path <folder>`. (#4262)
- Adja hozzá `-Extension` és `-LeafBase` vált `Split-Path` , hogy a fájlnév kiterjesztése és a fájlnevet a többi közötti útvonalak fel. (#2721) (Köszönet a következőknek @powercode!)
- Paraméterek hozzáadása `-Top` és `-Bottom` való `Sort-Object` a felső/alsó N rendezési
- Egy folyamat szülő folyamat elérhetővé hozzáadásával a `CodeProperty "Parent"` való `System.Diagnostics.Process`. (#2850) (Köszönet a következőknek @powercode!)
- MB használata helyett KB memória oszlopához `Get-Process`
- Adja hozzá `-NoNewLine` átkapcsolni a `Out-String`. (#5056) (Köszönjük @raghav710)
- `Move-Item` a parancsmag eleget tegyen `-Include`, `-Exclude`, és `-Filter` paraméterek. (#3878)
- Engedélyezése `*` beállításjegyzékbeli elérési út a használandó `Remove-Item`. (#4866)
- Adja hozzá `-Title` való `Get-Credential` és egyesítése, ezáltal a Rákérdezés a felhasználói élmény különböző platformokon.
- Adja hozzá a `-TimeOut` paramétert `Test-Connection`. (#2492)
- `Get-AuthenticodeSignature` parancsmagok most kérheti le a fájl aláírása időbélyegző. (#4061)
- Távolítsa el a nem támogatott `-ShowWindow` átállás `Get-Help`. (#4903)
- Javítsa ki `Get-Content -Delimiter` tartalmazza az elválasztó a tömb elemeinek vissza a (#3706) (Köszönjük @mklement0)
- Adja hozzá `Meta`, `Charset`, és `Transitional` paraméterek `ConvertTo-HTML` (#4184) (Köszönjük @ergo3114)
- Adja hozzá `WindowsUBR` és `WindowsVersion` tulajdonságok `Get-ComputerInfo` eredménye
- Adja hozzá `-Group` paraméterrel `Get-Verb`
- Adja hozzá `ShouldProcess` támogatni szeretné a `New-FileCatalog` és `Test-FileCatalog` (javítások `-WhatIf` és `-Confirm`). (#3074) (Köszönet a következőknek @iSazonov!)
- Adja hozzá `-WhatIf` váltani `Start-Process` parancsmag (#4735) (Köszönjük @sarithsutha)
- Adja hozzá `ValidateNotNullOrEmpty` túl sok meglévő paraméterek.

## <a name="tab-completion"></a>Kiegészítést

- A továbbfejlesztett a következtetésének a kiegészítést futásidejű változó értékek alapján. (#2744) (Köszönet a következőknek @powercode!) Ez lehetővé teszi a kiegészítést olyan esetekben, például:

  ```powershell
  $p = Get-Process
  $p | Foreach-Object Prio<tab>
  ```

- Adja hozzá a kivonattábla kiegészítést `-Property` a `Select-Object`. (#3625) (Köszönet a következőknek @powercode)
- Argumentum automatikus kiegészítéshez a engedélyezése `-ExcludeProperty` és `-ExpandProperty` a `Select-Object`. (#3443) (Köszönet a következőknek @iSazonov!)
- Hárítsa el a hiba a kiegészítést, hogy `native.exe --<tab>` fejeznie natív hívása. (#3633) (Köszönet a következőknek @powercode!)

## <a name="breaking-changes"></a>Módosítások megszakítása

Azt a már bevezetett jelentős változásokat PowerShell Core 6.0 számos.
További részletes őket, lásd: [PowerShell Core 6.0 Megtörje változásai][breaking-changes].

## <a name="debugging"></a>Hibakeresés

- Támogatja a távoli step-in hibakeresést `Invoke-Command -ComputerName`. (#3015)
- Kötő hibakeresési PowerShell Core naplózás engedélyezése

## <a name="filesystem-updates"></a>Fájlrendszer frissítések

- A fájlrendszer szolgáltató UNC-útvonalon használatának engedélyezése. ($4998)
- `Split-Path` UNC-gyökér most működik
- `cd` argumentum nélkül most úgy viselkedik, mint `cd ~`
- Rögzített méretű PowerShell-Core az elérési utak legfeljebb 260 karakter hosszú használatának engedélyezése. (#3960)

## <a name="bug-fixes-and-performance-improvements"></a>Hibajavításokat tartalmaz, és a teljesítménnyel kapcsolatos fejlesztések

Hajtottunk *sok* PowerShell, többek között a indítási idő, a különféle beépített parancsmagok és a natív bináris való együttműködéshez között teljesítmény fejlesztései.

Azt korábban rögzített egy PowerShell Core belül hibák száma is.
A fentebbi javításhoz és módosításhoz teljes listájáért tekintse meg a [változásnaplója][] a Githubon.

## <a name="telemetry"></a>Telemetria

- A jelentés a két konzol állomással PowerShell Core 6.0 hozzáadott telemetriai értékek (#3620):
  - az operációs rendszer platform (`$PSVersionTable.OSDescription`)
  - a PowerShell pontos verzióját (`$PSVersionTable.GitCommitId`)

Ha azt szeretné, hogy lemondja a telemetriai adatot, egyszerűen csak törölje `$PSHome\DELETE_ME_TO_DISABLE_CONSOLEHOST_TELEMETRY` , vagy hozzon létre `POWERSHELL_TELEMETRY_OPTOUT` környezeti változó a következő értékek egyikét: `true`, `1` vagy `yes`.
Törölni a fájlt, vagy hozzon létre a változót megkerüli az összes telemetriai adat azelőtt PowerShell első alkalommal történő futtatásakor.
A telemetriai adatok és az azt a telemetriai adatok a glean insights teszi ki a is tervezzük az [közösségi irányítópult][community-dashboard].
További információk a hogyan ezen az adatok felhasználási található [blogbejegyzés][telemetry-blog].

[github]: https://github.com/PowerShell/PowerShell
[.NET Core 2.0]: https://docs.microsoft.com/en-us/dotnet/core/
[.NET-szabvány]: https://docs.microsoft.com/en-us/dotnet/standard/net-standard
[os_log]: https://developer.apple.com/documentation/os/logging
[Syslog]: https://en.wikipedia.org/wiki/Syslog
[ssh-remoting]: ../core-powershell/SSH-Remoting-in-PowerShell-Core.md
[breaking-changes]: https://github.com/PowerShell/PowerShell/tree/master/docs/BREAKINGCHANGES.md
[változásnaplója]: https://github.com/PowerShell/PowerShell/tree/master/CHANGELOG.md
[community-dashboard]: https://aka.ms/PSGitHubBI
[telemetry-blog]: https://blogs.msdn.microsoft.com/powershell/2017/01/31/powershell-open-source-community-dashboard/
[.NET Standard]: https://docs.microsoft.com/dotnet/standard/net-standard
[.NET Blog]: https://blogs.msdn.microsoft.com/dotnet/2016/09/26/introducing-net-standard
[YouTube]: https://www.youtube.com/watch?v=YI4MurjfMn8&list=PLRAdsfhKI4OWx321A_pr-7HhRNk7wOLLY
[gyakran ismételt kérdések]: https://github.com/dotnet/standard/blob/master/docs/faq.md
[CDXML]: https://msdn.microsoft.com/en-us/library/jj542525(v=vs.85).aspx
[docker-hub]: https://hub.docker.com/r/microsoft/powershell/
[docker]: https://github.com/PowerShell/PowerShell/tree/master/docker
[windowspsmodulepath]: https://www.powershellgallery.com/packages/WindowsPSModulePath/
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
