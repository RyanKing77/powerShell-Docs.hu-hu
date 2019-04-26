---
title: A VSCode-ban és a PowerShellben történő fájlkódolás megértése
description: Fájlkódolás VSCode, a PowerShell konfigurálása
ms.date: 02/28/2019
ms.openlocfilehash: 6a00e45b3700f72f78e2fbcdf6e317f3a17b53c0
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058437"
---
# <a name="understanding-file-encoding-in-vscode-and-powershell"></a>A VSCode-ban és a PowerShellben történő fájlkódolás megértése

A VS Code használatával létrehozása és szerkesztése a PowerShell-szkripteket, fontos, hogy menti a fájlokat a helyes karaktert a kódolási formátum használatával.

## <a name="what-is-file-encoding-and-why-is-it-important"></a>Mi a fájl kódolása, és miért fontos?

VSCode kezeli egy karaktert a pufferbe emberi belépés karakterláncok és olvasási/írási blokkok bájt, a fájlrendszer közötti illesztőfelületet. VSCode fájlba menti, amikor ehhez a szövegkódolás használ.

Ehhez hasonlóan PowerShell parancsfájl futtatásakor, konvertálni kell egy fájlt bájtok karakter hosszúságú lehet helyreállítani a fájlt egy PowerShell-programba. VSCode ír a fájlt, és a PowerShell beolvassa a fájlt, mert kell használniuk az adott kódolási rendszer. Ez a folyamat az elemzés egy PowerShell-parancsfájlt mutat: *bájt* -> *karakterek* -> *jogkivonatok*  ->   *Absztrakt szintaxis fa* -> *végrehajtási*.

VSCode és a PowerShell telepített kódolási észszerű alapértelmezett konfigurációval. Ugyanakkor a PowerShell által használt alapértelmezett kódolást megváltozott a PowerShell Core (6.x-es) kiadása. Győződjön meg arról, hogy a PowerShell vagy a PowerShell-bővítmény használatával a vscode-ban nincs probléma, a VSCode- és PowerShell-beállítások konfigurálásához kell megfelelően.

## <a name="common-causes-of-encoding-issues"></a>A kódolási hibák gyakori okai

Kódolási problémák lépnek fel, amikor a VSCode vagy a szkript kódolása nem egyezik a várt kódolást PowerShell. Nincs lehetőség a PowerShell automatikusan meghatározni a fájl kódolása.

Ön valószínűséggel problémák kódolást, ha nincs a karakterek használata esetén a [7 bites ASCII karakterkészlet](https://ascii.cl/). Például:

- Latin karaktereket ékezetes (`É`, `ü`)
- A nem latin karaktereket, például cirill (`Д`, `Ц`)
- Han kínai (`脚`, `本`)

A kódolási problémák leggyakoribb okai a következők:

- Kódolásai a VSCode és a PowerShell nem módosult a beállításokat alapértelmezett értékükön. A PowerShell 5.1, és alapértelmezés szerint az alábbi kódolás nem azonos a VSCode-a.
- Más szerkesztővel megnyitotta, és írja felül a fájlt egy új kódolást. Ez gyakran az ISE használatával történik.
- A fájl be verziókövetés a kódolást, amely eltér a rendszer ellenőrzi, milyen VSCode-vagy PowerShell vár. Ez akkor fordulhat elő, amikor a közreműködők szerkesztők használata a különböző kódolási konfigurációk.

### <a name="how-to-tell-when-you-have-encoding-issues"></a>Hogyan állapítható meg, ha rendelkezik a kódolási problémák

Gyakran kódolási hibák találhatók maguk módon használhatóak a szkriptek hibák elemzése. Furcsa karaktersorozatok a parancsfájlban keresse meg, ha ez a probléma lehet. Gondolatjelet – az alábbi példában (`–`) jelenik meg a karakterek `â€“`:

```Output
Send-MailMessage : A positional parameter cannot be found that accepts argument 'Testing FuseMail SMTP...'.
At C:\Users\<User>\<OneDrive>\Development\PowerShell\Scripts\Send-EmailUsingSmtpRelay.ps1:6 char:1
+ Send-MailMessage â€“From $from â€“To $recipient1 â€“Subject $subject  ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (:) [Send-MailMessage], ParameterBindingException
    + FullyQualifiedErrorId : PositionalParameterNotFound,Microsoft.PowerShell.Commands.SendMailMessage
```

Ez a probléma oka, hogy a VSCode kódolja a karakter `–` UTF-8 a bájtok formájában `0xE2 0x80 0x93`.
Ezek bájt, a Windows-1252 vannak dekódolni, amikor azok a karakterek értelmez `â€“`.

Néhány furcsa karaktersorozatok által is látható a következők:

<!-- markdownlint-disable MD038 -->
- `â€“` ahelyett, hogy `–`
- `â€”` ahelyett, hogy `—`
- `Ã„2` ahelyett, hogy `Ä`
- `Â` helyett ` ` (nem törhető szóköz)
- `Ã©` ahelyett, hogy `é`
<!-- markdownlint-enable MD038 -->

Ez praktikus [referencia](https://www.i18nqa.com/debug/utf8-debug.html) sorolja fel, hogy az UTF-8 vagy Windows-1252 kódolási általános mintákat.

## <a name="how-the-powershell-extension-in-vscode-interacts-with-encodings"></a>Hogyan kommunikál az a vscode-ban a PowerShell-bővítmény kódolásokat

A PowerShell-bővítmény parancsfájlok számos módon kommunikál:

1. Parancsfájlok szerkesztése a vscode-ban, a tartalma küldik VSCode a bővítményt. A [nyelvi protokoll][] , hogy a tartalmak kerüljenek az UTF-8 építjük. Ezért azt nem alkalmas a hibás kódolás beolvasni a bővítmény.
2. Parancsfájlok végrehajtása közvetlenül az integrált konzol az, ha azok még olvasni a fájlt PowerShell közvetlenül. A VSCode eltér a PowerShell a kódolást, ha valami meg helytelen itt.
3. Ha egy parancsfájl, amely meg van nyitva a vscode-ban hivatkozik, amely nem a vscode-ban nyissa meg egy másik parancsprogramra, a bővítmény visszavált a fájlrendszer a parancsprogram tartalmát betöltése. A PowerShell-bővítmény alapértelmezett értéke UTF-8 kódolást, de használ [bájtsorrendjelző][], vagy AJ, válassza ki a megfelelő kódolást az észlelést.

A probléma akkor fordul elő, amikor feltéve, hogy a kódolás AJ nélküli formátumok (például [UTF-8][] Anyagjegyzék nem rendelkező és [Windows-1252][]).
A PowerShell-bővítmény alapértelmezés szerint az UTF-8. A bővítmény a VSCode kódolási beállítások nem módosíthatók.
További információkért lásd: [#824 kiadása](https://github.com/Microsoft/vscode/issues/824).

## <a name="choosing-the-right-encoding"></a>A megfelelő kódolási kiválasztása

A különböző rendszerek és alkalmazások különböző kódolásokat használhatja:

- .NET standardban a weben és Linux világában UTF-8 rendszer most már a domináns kódolást.
- .NET-keretrendszer számos alkalmazásban a [UTF-16][]. Korábbi okokból "Unicode" is nevezik, egy adott most kifejezés pedig széles körű [standard](https://en.wikipedia.org/wiki/Unicode) , amely tartalmazza az UTF-8 és UTF-16 is.
- A Windows Unicode előtti számos natív alkalmazások továbbra is használhatja a Windows-1252 alapértelmezés szerint.

Unicode kódolású is (AJ) megjelölni egy bájtsorrendjelző fogalma. AJ szöveget kell tudniuk a dekóder milyen kódolást használ a szöveg elején történik. Több-bájtos kódolást, a AJ is megadja, hogy [bájtsorrend](https://en.wikipedia.org/wiki/Endianness) a kódolást. AJ célja nem Unicode szöveg, lehetővé téve, hogy a szöveg AJ megléte esetén az Unicode-ésszerű találgatásos ritkán előforduló bájt lehet.

AJ megadása nem kötelező, és azok elfogadását nem, népszerű Linux világ, mert egy megbízható egyezmény UTF-8 mindenhol használja. A legtöbb Linux-alkalmazások feltételezik, hogy szövegbevitel UTF-8 kódolása. Míg számos Linux-alkalmazás ismeri fel, és a egy AJ megfelelően kezeli, számos viszont nem, és kezelhetők az ilyen alkalmazások szöveges összetevők.

**Ezért**:

- Ha elsősorban a Windows-alkalmazások és a Windows PowerShell dolgozik, a részesítsék előnyben, például az UTF-8 AJ vagy UTF-16 kódolást.
- Platformok közötti használathoz, az UTF-8 AJ-kell használni.
- Ha Linux-kapcsolódó környezeteket főleg a dolgozik, az UTF-8 AJ nélkül kell inkább.
- Latin-1 és a Windows-1252-es rendszer lehetőség szerint kerülendő lényegében örökölt kódolásokat.
  Előfordulhat, hogy néhány régebbi Windows-alkalmazások azonban rajtuk függ.
- Célszerű is érdemes megjegyezni, hogy a parancsfájl aláírása, [kódolás függő](https://github.com/PowerShell/PowerShell/issues/3466), egy aláírt parancsfájl kódolás módosítását jelenti számára lesz szükség.

## <a name="configuring-vscode"></a>VSCode konfigurálása

VSCode az alapértelmezett kódolás az UTF-8 AJ nélkül.

Beállítása [A VSCode-kódolás][], nyissa meg a VSCode-beállításokat (<kbd>Ctrl</kbd>+<kbd>,</kbd>) és állítsa be a `"files.encoding"` beállítást:

```json
"files.encoding": "utf8bom"
```

Néhány lehetséges értékei a következők:

- `utf8`: [UTF-8] AJ nélkül
- `utf8bom`: [UTF-8] az Anyagjegyzék
- `utf16le`: Little endian [UTF-16]
- `utf16be`: A big endian [UTF-16]
- `windows1252`: [Windows-1252]

A grafikus felhasználói Felülettel nézetben a legördülő lista kell kap, vagy kiegészítése, a JSON-fájlban megtekintheti.

Emellett a kapcsolatok automatikus észleléssel kódolást, ha lehetséges, adja hozzá a következő:

```json
"files.autoGuessEncoding": true
```

Ha nem szeretné ezeket a beállításokat az összes fájltípus hatással, VSCode is lehetővé teszi, hogy nyelvenkénti konfigurációkat. Hozzon létre egy nyelvspecifikus beállítás beállításait írja a `[<language-name>]` mező. Például:

```json
"[powershell]": {
    "files.encoding": "utf8bom",
    "files.autoGuessEncoding": true
}
```

## <a name="configuring-powershell"></a>PowerShell konfigurálása

PowerShell az alapértelmezett kódolás verziójától függően változik:

- A PowerShell 6, az alapértelmezett kódolás az UTF-8 nélkül AJ minden platformon.
- A Windows PowerShellben, az alapértelmezett kódolás az általában Windows-1252-es, bővítmény [latin 1][], más néven ISO 8859 – 1.

A PowerShell 5 + találja meg ez az alapértelmezett kódolást:

```powershell
[psobject].Assembly.GetTypes() | Where-Object { $_.Name -eq 'ClrFacade'} |
  ForEach-Object {
    $_.GetMethod('GetDefaultEncoding', [System.Reflection.BindingFlags]'nonpublic,static').Invoke($null, @())
  }
```

A következő [parancsfájl](https://gist.github.com/rjmholt/3d8dd4849f718c914132ce3c5b278e0e) határozza meg, mi a PowerShell-munkamenetet kódolás nélkül AJ parancsfájl kikövetkezteti használható.

```powershell
$badBytes = [byte[]]@(0xC3, 0x80)
$utf8Str = [System.Text.Encoding]::UTF8.GetString($badBytes)
$bytes = [System.Text.Encoding]::ASCII.GetBytes('Write-Output "') + [byte[]]@(0xC3, 0x80) + [byte[]]@(0x22)
$path = Join-Path ([System.IO.Path]::GetTempPath()) 'encodingtest.ps1'

try
{
    [System.IO.File]::WriteAllBytes($path, $bytes)

    switch (& $path)
    {
        $utf8Str
        {
            return 'UTF-8'
            break
        }

        default
        {
            return 'Windows-1252'
            break
        }
    }
}
finally
{
    Remove-Item $path
}
```

Konfigurálása a PowerShell használata egy adott kódolási általában a profil beállításainak használatával lehetőség. Lásd az alábbi cikkeket:

- [@mklement0]a [PowerShell a StackOverflow-n kódolással kapcsolatos válasz](https://stackoverflow.com/a/40098904).
- [@rkeithhill]a [többé vesződnie a sérült a PowerShell AJ nélküli UTF-8 bemeneti szóló blogbejegyzést](https://rkeithhill.wordpress.com/2010/05/26/handling-native-exe-output-encoding-in-utf8-with-no-bom/).

Nem alkalmas kényszerítése a PowerShell használata az adott bemeneti kódolást. A PowerShell 5.1-es és Windows-1252 kódolást, ha ott nem Anyagjegyzék nem az alapértelmezett alatt. Együttműködési okokból célszerű menteni a parancsfájlok az Anyagjegyzék Unicode formátumú.

> [!IMPORTANT]
> Bármely eszközzel rendelkezik, hogy touch PowerShell parancsfájlok hatással lehet a kódolási beállításokat, vagy újra kódolása a parancsfájlokat egy másik kódolás.

### <a name="existing-scripts"></a>Meglévő parancsfájlok

Már a fájlrendszerben parancsfájlok kell újra értéket kódolni kell az új választott kódolás. VSCode alsó sáv látni fogja a címkét az UTF-8. A gombra kattintva nyissa meg a művelet sávon és **kódolással mentése**. Most kiválaszthatja, hogy a fájl egy új kódolást. Lásd: [A VSCode-kódolás][] teljes útmutatás.

Ha újra kódolása több fájl van szüksége, használhatja az alábbi parancsfájlt:

```powershell
Get-ChildItem *.ps1 -Recurse | ForEach-Object {
    $content = Get-Content -Path $_
    Set-Content -Path $_.Fullname -Value $content -Encoding UTF8 -PassThru -Force
}
```

### <a name="the-powershell-integrated-scripting-environment-ise"></a>A PowerShell integrált parancsfájlkezelési környezet (ISE)

Ha a PowerShell ISE-alapú parancsprogramok is szerkeszti, kell szinkronizálhatja a kódolási beállításait.

A ISE kell figyelembe veszi a AJ, de azt is enumerálható reflexióval az [a kódolás](https://bensonxion.wordpress.com/2012/04/25/powershell-ise-default-saveas-encoding/).
Vegye figyelembe, hogy ez nem őrizhető meg, induló cégek között.

### <a name="source-control-software"></a>Forrás felügyeleti szoftver

Egyes forrás ellenőrző eszközök, például a git, figyelmen kívül hagyása kódolásokat; a git csak a bájtok követi nyomon.
Mások, például az Azure DevOps- vagy Mercurial, előfordulhat, hogy nem. Még néhány git-alapú eszközök válik a szöveg dekódolása.

Ha ez a helyzet, ellenőrizze, hogy:

- Konfigurálja a szövegkódolás a VSCode-konfigurációnak megfelelően a verziókövetési rendszerben.
- Győződjön meg róla, minden fájl a rendszer ellenőrzi a megfelelő kódolása forrásvezérlőben.
- Legyen óvatos az olyan módosításait a verziókövetés keresztül fogadott kódolást. Ez a kulcs jele egy különbözeti utaló módosításokat, de ha semmit nem úgy tűnik, hogy megváltozott (mivel bájt rendelkeznek, de nem rendelkezik karakter).

### <a name="collaborators-environments"></a>A közreműködők környezetek

Felett Verziókövetés beállítása, győződjön meg arról, a közreműködők, a megosztott fájlok nem rendelkezik, amelyek felülírják a kódolás szerint újrakódolása PowerShell fájlok beállításait.

### <a name="other-programs"></a>Más programok

Minden más programot, amelyet olvas vagy ír egy PowerShell-parancsprogram újra előfordulhat, hogy kódolja azokat.

Néhány példa a következők:

- A Vágólap használatával másolja és illessze be a parancsfájlt. Ez a gyakori helyzetek, például az:
  - A parancsfájl másolása virtuális gépre
  - A parancsfájl egy e-mailben vagy weblap másolása
  - A parancsfájl másolása vagy onnan máshová egy Microsoft Word és PowerPoint-dokumentum
- Más szövegszerkesztők, például:
  - A Jegyzettömb
  - vim
  - Bármely más PowerShell parancsprogram-szerkesztő
- Segédprogramok, mint szerkesztő szövege:
  - `Get-Content`/`Set-Content`/`Out-File`
  - Például a PowerShell átirányítási operátorok `>` és `>>`
  - `sed`/`awk`
- Fájl adatátviteli programok, például:
  - A webböngészőben parancsprogramok letöltése esetén
  - Fájlmegosztás

Egyes eszközök kezelésére bájt szöveg helyett, de más kódolási konfigurációk kínálnak. Ezekben az esetekben, ahol kell konfigurálnia a kódolást kell, hogy ugyanaz, mint a szerkesztő kódolási problémák megelőzése érdekében.

## <a name="other-resources-on-encoding-in-powershell"></a>Kódolás a PowerShell egyéb erőforrásokhoz

Van néhány egyéb hasznos bejegyzések kódolás és a kódolás a PowerShell konfigurálása, amelyek olvasási érdemes:

- [@mklement0]a [a PowerShell a StackOverflow-n kódolási összegzése](https://stackoverflow.com/questions/40098771/changing-powershells-default-output-encoding-to-utf-8)
- Előző problémák vscode-PowerShell kódolási problémák megnyitása:
  - [#1308](https://github.com/PowerShell/vscode-powershell/issues/1308)
  - [#1628](https://github.com/PowerShell/vscode-powershell/issues/1628)
  - [#1680](https://github.com/PowerShell/vscode-powershell/issues/1680)
  - [#1744](https://github.com/PowerShell/vscode-powershell/issues/1744)
  - [#1751](https://github.com/PowerShell/vscode-powershell/issues/1751)
- [A klasszikus *Joel szoftverfrissítési* Unicode kapcsolatos Microsoft Word](https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/)
- [Kódolás a .NET Standard](https://github.com/dotnet/standard/issues/260#issuecomment-289549508)


[@mklement0]: https://github.com/mklement0
[@rkeithhill]: https://github.com/rkeithhill
[Windows-1252]: https://wikipedia.org/wiki/Windows-1252
[Latin 1]: https://wikipedia.org/wiki/ISO/IEC_8859-1
[UTF-8]: https://wikipedia.org/wiki/UTF-8
[bájtsorrendjelző]: https://wikipedia.org/wiki/Byte_order_mark
[UTF-16]: https://wikipedia.org/wiki/UTF-16
[Nyelvi protokoll]: https://microsoft.github.io/language-server-protocol/
[A VSCode-kódolás]: https://code.visualstudio.com/docs/editor/codebasics#_file-encoding-support
