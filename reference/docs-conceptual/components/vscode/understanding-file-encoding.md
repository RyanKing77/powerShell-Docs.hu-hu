---
title: A VSCode-ban és a PowerShellben történő fájlkódolás megértése
description: Fájlkódolás VSCode, a PowerShell konfigurálása
ms.date: 02/28/2019
ms.openlocfilehash: 6a00e45b3700f72f78e2fbcdf6e317f3a17b53c0
ms.sourcegitcommit: f4bd4e116e22c8b5bfcb61680a7c42e58b4da93e
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/22/2019
ms.locfileid: "59984119"
---
# <a name="understanding-file-encoding-in-vscode-and-powershell"></a><span data-ttu-id="9de13-103">A VSCode-ban és a PowerShellben történő fájlkódolás megértése</span><span class="sxs-lookup"><span data-stu-id="9de13-103">Understanding file encoding in VSCode and PowerShell</span></span>

<span data-ttu-id="9de13-104">A VS Code használatával létrehozása és szerkesztése a PowerShell-szkripteket, fontos, hogy menti a fájlokat a helyes karaktert a kódolási formátum használatával.</span><span class="sxs-lookup"><span data-stu-id="9de13-104">When using VS Code to create and edit PowerShell scripts, it is important that your files are saved using the correct character encoding format.</span></span>

## <a name="what-is-file-encoding-and-why-is-it-important"></a><span data-ttu-id="9de13-105">Mi a fájl kódolása, és miért fontos?</span><span class="sxs-lookup"><span data-stu-id="9de13-105">What is file encoding and why is it important?</span></span>

<span data-ttu-id="9de13-106">VSCode kezeli egy karaktert a pufferbe emberi belépés karakterláncok és olvasási/írási blokkok bájt, a fájlrendszer közötti illesztőfelületet.</span><span class="sxs-lookup"><span data-stu-id="9de13-106">VSCode manages the interface between a human entering strings of characters into a buffer and reading/writing blocks of bytes to the filesystem.</span></span> <span data-ttu-id="9de13-107">VSCode fájlba menti, amikor ehhez a szövegkódolás használ.</span><span class="sxs-lookup"><span data-stu-id="9de13-107">When VSCode saves a file, it uses a text encoding to do this.</span></span>

<span data-ttu-id="9de13-108">Ehhez hasonlóan PowerShell parancsfájl futtatásakor, konvertálni kell egy fájlt bájtok karakter hosszúságú lehet helyreállítani a fájlt egy PowerShell-programba.</span><span class="sxs-lookup"><span data-stu-id="9de13-108">Similarly, when PowerShell runs a script it must convert the bytes in a file to characters to reconstruct the file into a PowerShell program.</span></span> <span data-ttu-id="9de13-109">VSCode ír a fájlt, és a PowerShell beolvassa a fájlt, mert kell használniuk az adott kódolási rendszer.</span><span class="sxs-lookup"><span data-stu-id="9de13-109">Since VSCode writes the file and PowerShell reads the file, they need to use the same encoding system.</span></span> <span data-ttu-id="9de13-110">Ez a folyamat az elemzés egy PowerShell-parancsfájlt mutat: *bájt* -> *karakterek* -> *jogkivonatok*  ->   *Absztrakt szintaxis fa* -> *végrehajtási*.</span><span class="sxs-lookup"><span data-stu-id="9de13-110">This process of parsing a PowerShell script goes: *bytes* -> *characters* -> *tokens* -> *abstract syntax tree* -> *execution*.</span></span>

<span data-ttu-id="9de13-111">VSCode és a PowerShell telepített kódolási észszerű alapértelmezett konfigurációval.</span><span class="sxs-lookup"><span data-stu-id="9de13-111">Both VSCode and PowerShell are installed with a sensible default encoding configuration.</span></span> <span data-ttu-id="9de13-112">Ugyanakkor a PowerShell által használt alapértelmezett kódolást megváltozott a PowerShell Core (6.x-es) kiadása.</span><span class="sxs-lookup"><span data-stu-id="9de13-112">However, the default encoding used by PowerShell has changed with the release of PowerShell Core (v6.x).</span></span> <span data-ttu-id="9de13-113">Győződjön meg arról, hogy a PowerShell vagy a PowerShell-bővítmény használatával a vscode-ban nincs probléma, a VSCode- és PowerShell-beállítások konfigurálásához kell megfelelően.</span><span class="sxs-lookup"><span data-stu-id="9de13-113">To ensure you have no problems using PowerShell or the PowerShell extension in VSCode, you need to configure your VSCode and PowerShell settings properly.</span></span>

## <a name="common-causes-of-encoding-issues"></a><span data-ttu-id="9de13-114">A kódolási hibák gyakori okai</span><span class="sxs-lookup"><span data-stu-id="9de13-114">Common causes of encoding issues</span></span>

<span data-ttu-id="9de13-115">Kódolási problémák lépnek fel, amikor a VSCode vagy a szkript kódolása nem egyezik a várt kódolást PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9de13-115">Encoding problems occur when the encoding of VSCode or your script file does not match the expected encoding of PowerShell.</span></span> <span data-ttu-id="9de13-116">Nincs lehetőség a PowerShell automatikusan meghatározni a fájl kódolása.</span><span class="sxs-lookup"><span data-stu-id="9de13-116">There is no way for PowerShell to automatically determine the file encoding.</span></span>

<span data-ttu-id="9de13-117">Ön valószínűséggel problémák kódolást, ha nincs a karakterek használata esetén a [7 bites ASCII karakterkészlet](https://ascii.cl/).</span><span class="sxs-lookup"><span data-stu-id="9de13-117">You're more likely to have encoding problems when you're using characters not in the [7-bit ASCII character set](https://ascii.cl/).</span></span> <span data-ttu-id="9de13-118">Például:</span><span class="sxs-lookup"><span data-stu-id="9de13-118">For example:</span></span>

- <span data-ttu-id="9de13-119">Latin karaktereket ékezetes (`É`, `ü`)</span><span class="sxs-lookup"><span data-stu-id="9de13-119">Accented latin characters (`É`, `ü`)</span></span>
- <span data-ttu-id="9de13-120">A nem latin karaktereket, például cirill (`Д`, `Ц`)</span><span class="sxs-lookup"><span data-stu-id="9de13-120">Non-latin characters like Cyrillic (`Д`, `Ц`)</span></span>
- <span data-ttu-id="9de13-121">Han kínai (`脚`, `本`)</span><span class="sxs-lookup"><span data-stu-id="9de13-121">Han Chinese (`脚`, `本`)</span></span>

<span data-ttu-id="9de13-122">A kódolási problémák leggyakoribb okai a következők:</span><span class="sxs-lookup"><span data-stu-id="9de13-122">Common reasons for encoding issues are:</span></span>

- <span data-ttu-id="9de13-123">Kódolásai a VSCode és a PowerShell nem módosult a beállításokat alapértelmezett értékükön.</span><span class="sxs-lookup"><span data-stu-id="9de13-123">The encodings of VSCode and PowerShell have not been changed from their defaults.</span></span> <span data-ttu-id="9de13-124">A PowerShell 5.1, és alapértelmezés szerint az alábbi kódolás nem azonos a VSCode-a.</span><span class="sxs-lookup"><span data-stu-id="9de13-124">For PowerShell 5.1 and below, the default encoding is different from VSCode's.</span></span>
- <span data-ttu-id="9de13-125">Más szerkesztővel megnyitotta, és írja felül a fájlt egy új kódolást.</span><span class="sxs-lookup"><span data-stu-id="9de13-125">Another editor has opened and overwritten the file in a new encoding.</span></span> <span data-ttu-id="9de13-126">Ez gyakran az ISE használatával történik.</span><span class="sxs-lookup"><span data-stu-id="9de13-126">This often happens with the ISE.</span></span>
- <span data-ttu-id="9de13-127">A fájl be verziókövetés a kódolást, amely eltér a rendszer ellenőrzi, milyen VSCode-vagy PowerShell vár.</span><span class="sxs-lookup"><span data-stu-id="9de13-127">The file is checked into source control in an encoding that is different from what VSCode or PowerShell expects.</span></span> <span data-ttu-id="9de13-128">Ez akkor fordulhat elő, amikor a közreműködők szerkesztők használata a különböző kódolási konfigurációk.</span><span class="sxs-lookup"><span data-stu-id="9de13-128">This can happen when collaborators use editors with different encoding configurations.</span></span>

### <a name="how-to-tell-when-you-have-encoding-issues"></a><span data-ttu-id="9de13-129">Hogyan állapítható meg, ha rendelkezik a kódolási problémák</span><span class="sxs-lookup"><span data-stu-id="9de13-129">How to tell when you have encoding issues</span></span>

<span data-ttu-id="9de13-130">Gyakran kódolási hibák találhatók maguk módon használhatóak a szkriptek hibák elemzése.</span><span class="sxs-lookup"><span data-stu-id="9de13-130">Often encoding errors present themselves as parse errors in scripts.</span></span> <span data-ttu-id="9de13-131">Furcsa karaktersorozatok a parancsfájlban keresse meg, ha ez a probléma lehet.</span><span class="sxs-lookup"><span data-stu-id="9de13-131">If you find strange character sequences in your script, this can be the problem.</span></span> <span data-ttu-id="9de13-132">Gondolatjelet – az alábbi példában (`–`) jelenik meg a karakterek `â€“`:</span><span class="sxs-lookup"><span data-stu-id="9de13-132">In the example below, an en-dash (`–`) appears as the characters `â€“`:</span></span>

```Output
Send-MailMessage : A positional parameter cannot be found that accepts argument 'Testing FuseMail SMTP...'.
At C:\Users\<User>\<OneDrive>\Development\PowerShell\Scripts\Send-EmailUsingSmtpRelay.ps1:6 char:1
+ Send-MailMessage â€“From $from â€“To $recipient1 â€“Subject $subject  ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (:) [Send-MailMessage], ParameterBindingException
    + FullyQualifiedErrorId : PositionalParameterNotFound,Microsoft.PowerShell.Commands.SendMailMessage
```

<span data-ttu-id="9de13-133">Ez a probléma oka, hogy a VSCode kódolja a karakter `–` UTF-8 a bájtok formájában `0xE2 0x80 0x93`.</span><span class="sxs-lookup"><span data-stu-id="9de13-133">This problem occurs because VSCode encodes the character `–` in UTF-8 as the bytes `0xE2 0x80 0x93`.</span></span>
<span data-ttu-id="9de13-134">Ezek bájt, a Windows-1252 vannak dekódolni, amikor azok a karakterek értelmez `â€“`.</span><span class="sxs-lookup"><span data-stu-id="9de13-134">When these bytes are decoded as Windows-1252, they are interpreted as the characters `â€“`.</span></span>

<span data-ttu-id="9de13-135">Néhány furcsa karaktersorozatok által is látható a következők:</span><span class="sxs-lookup"><span data-stu-id="9de13-135">Some strange character sequences that you might see include:</span></span>

<!-- markdownlint-disable MD038 -->
- <span data-ttu-id="9de13-136">`â€“` ahelyett, hogy `–`</span><span class="sxs-lookup"><span data-stu-id="9de13-136">`â€“` instead of `–`</span></span>
- <span data-ttu-id="9de13-137">`â€”` ahelyett, hogy `—`</span><span class="sxs-lookup"><span data-stu-id="9de13-137">`â€”` instead of `—`</span></span>
- <span data-ttu-id="9de13-138">`Ã„2` ahelyett, hogy `Ä`</span><span class="sxs-lookup"><span data-stu-id="9de13-138">`Ã„2` instead of `Ä`</span></span>
- <span data-ttu-id="9de13-139">`Â` helyett ` ` (nem törhető szóköz)</span><span class="sxs-lookup"><span data-stu-id="9de13-139">`Â` instead of ` `  (a non-breaking space)</span></span>
- <span data-ttu-id="9de13-140">`Ã©` ahelyett, hogy `é`</span><span class="sxs-lookup"><span data-stu-id="9de13-140">`Ã©` instead of `é`</span></span>
<!-- markdownlint-enable MD038 -->

<span data-ttu-id="9de13-141">Ez praktikus [referencia](https://www.i18nqa.com/debug/utf8-debug.html) sorolja fel, hogy az UTF-8 vagy Windows-1252 kódolási általános mintákat.</span><span class="sxs-lookup"><span data-stu-id="9de13-141">This handy [reference](https://www.i18nqa.com/debug/utf8-debug.html) lists the common patterns that indicate a UTF-8/Windows-1252 encoding problem.</span></span>

## <a name="how-the-powershell-extension-in-vscode-interacts-with-encodings"></a><span data-ttu-id="9de13-142">Hogyan kommunikál az a vscode-ban a PowerShell-bővítmény kódolásokat</span><span class="sxs-lookup"><span data-stu-id="9de13-142">How the PowerShell extension in VSCode interacts with encodings</span></span>

<span data-ttu-id="9de13-143">A PowerShell-bővítmény parancsfájlok számos módon kommunikál:</span><span class="sxs-lookup"><span data-stu-id="9de13-143">The PowerShell extension interacts with scripts in a number of ways:</span></span>

1. <span data-ttu-id="9de13-144">Parancsfájlok szerkesztése a vscode-ban, a tartalma küldik VSCode a bővítményt.</span><span class="sxs-lookup"><span data-stu-id="9de13-144">When scripts are edited in VSCode, the contents are sent by VSCode to the extension.</span></span> <span data-ttu-id="9de13-145">A [nyelvi protokoll][] , hogy a tartalmak kerüljenek az UTF-8 építjük.</span><span class="sxs-lookup"><span data-stu-id="9de13-145">The [Language Server Protocol][] mandates that this content is transferred in UTF-8.</span></span> <span data-ttu-id="9de13-146">Ezért azt nem alkalmas a hibás kódolás beolvasni a bővítmény.</span><span class="sxs-lookup"><span data-stu-id="9de13-146">Therefore, it is not possible for the extension to get the wrong encoding.</span></span>
2. <span data-ttu-id="9de13-147">Parancsfájlok végrehajtása közvetlenül az integrált konzol az, ha azok még olvasni a fájlt PowerShell közvetlenül.</span><span class="sxs-lookup"><span data-stu-id="9de13-147">When scripts are executed directly in the Integrated Console, they're read from the file by PowerShell directly.</span></span> <span data-ttu-id="9de13-148">A VSCode eltér a PowerShell a kódolást, ha valami meg helytelen itt.</span><span class="sxs-lookup"><span data-stu-id="9de13-148">If PowerShell's encoding differs from VSCode's, something can go wrong here.</span></span>
3. <span data-ttu-id="9de13-149">Ha egy parancsfájl, amely meg van nyitva a vscode-ban hivatkozik, amely nem a vscode-ban nyissa meg egy másik parancsprogramra, a bővítmény visszavált a fájlrendszer a parancsprogram tartalmát betöltése.</span><span class="sxs-lookup"><span data-stu-id="9de13-149">When a script that is open in VSCode references another script that is not open in VSCode, the extension falls back to loading that script's content from the file system.</span></span> <span data-ttu-id="9de13-150">A PowerShell-bővítmény alapértelmezett értéke UTF-8 kódolást, de használ [bájtsorrendjelző][], vagy AJ, válassza ki a megfelelő kódolást az észlelést.</span><span class="sxs-lookup"><span data-stu-id="9de13-150">The PowerShell extension defaults to UTF-8 encoding, but uses [byte-order mark][], or BOM, detection to select the correct encoding.</span></span>

<span data-ttu-id="9de13-151">A probléma akkor fordul elő, amikor feltéve, hogy a kódolás AJ nélküli formátumok (például [UTF-8][] Anyagjegyzék nem rendelkező és [Windows-1252][]).</span><span class="sxs-lookup"><span data-stu-id="9de13-151">The problem occurs when assuming the encoding of BOM-less formats (like [UTF-8][] with no BOM and [Windows-1252][]).</span></span>
<span data-ttu-id="9de13-152">A PowerShell-bővítmény alapértelmezés szerint az UTF-8.</span><span class="sxs-lookup"><span data-stu-id="9de13-152">The PowerShell extension defaults to UTF-8.</span></span> <span data-ttu-id="9de13-153">A bővítmény a VSCode kódolási beállítások nem módosíthatók.</span><span class="sxs-lookup"><span data-stu-id="9de13-153">The extension cannot change VSCode's encoding settings.</span></span>
<span data-ttu-id="9de13-154">További információkért lásd: [#824 kiadása](https://github.com/Microsoft/vscode/issues/824).</span><span class="sxs-lookup"><span data-stu-id="9de13-154">For more information, see [issue #824](https://github.com/Microsoft/vscode/issues/824).</span></span>

## <a name="choosing-the-right-encoding"></a><span data-ttu-id="9de13-155">A megfelelő kódolási kiválasztása</span><span class="sxs-lookup"><span data-stu-id="9de13-155">Choosing the right encoding</span></span>

<span data-ttu-id="9de13-156">A különböző rendszerek és alkalmazások különböző kódolásokat használhatja:</span><span class="sxs-lookup"><span data-stu-id="9de13-156">Different systems and applications can use different encodings:</span></span>

- <span data-ttu-id="9de13-157">.NET standardban a weben és Linux világában UTF-8 rendszer most már a domináns kódolást.</span><span class="sxs-lookup"><span data-stu-id="9de13-157">In .NET Standard, on the web, and in the Linux world, UTF-8 is now the dominant encoding.</span></span>
- <span data-ttu-id="9de13-158">.NET-keretrendszer számos alkalmazásban a [UTF-16][].</span><span class="sxs-lookup"><span data-stu-id="9de13-158">Many .NET Framework applications use [UTF-16][].</span></span> <span data-ttu-id="9de13-159">Korábbi okokból "Unicode" is nevezik, egy adott most kifejezés pedig széles körű [standard](https://en.wikipedia.org/wiki/Unicode) , amely tartalmazza az UTF-8 és UTF-16 is.</span><span class="sxs-lookup"><span data-stu-id="9de13-159">For historical reasons, this is sometimes called "Unicode", a term that now refers to a broad [standard](https://en.wikipedia.org/wiki/Unicode) that includes both UTF-8 and UTF-16.</span></span>
- <span data-ttu-id="9de13-160">A Windows Unicode előtti számos natív alkalmazások továbbra is használhatja a Windows-1252 alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="9de13-160">On Windows, many native applications that predate Unicode continue to use Windows-1252 by default.</span></span>

<span data-ttu-id="9de13-161">Unicode kódolású is (AJ) megjelölni egy bájtsorrendjelző fogalma.</span><span class="sxs-lookup"><span data-stu-id="9de13-161">Unicode encodings also have the concept of a byte-order mark (BOM).</span></span> <span data-ttu-id="9de13-162">AJ szöveget kell tudniuk a dekóder milyen kódolást használ a szöveg elején történik.</span><span class="sxs-lookup"><span data-stu-id="9de13-162">BOMs occur at the beginning of text to tell a decoder which encoding the text is using.</span></span> <span data-ttu-id="9de13-163">Több-bájtos kódolást, a AJ is megadja, hogy [bájtsorrend](https://en.wikipedia.org/wiki/Endianness) a kódolást.</span><span class="sxs-lookup"><span data-stu-id="9de13-163">For multi-byte encodings, the BOM also indicates [endianness](https://en.wikipedia.org/wiki/Endianness) of the encoding.</span></span> <span data-ttu-id="9de13-164">AJ célja nem Unicode szöveg, lehetővé téve, hogy a szöveg AJ megléte esetén az Unicode-ésszerű találgatásos ritkán előforduló bájt lehet.</span><span class="sxs-lookup"><span data-stu-id="9de13-164">BOMs are designed to be bytes that rarely occur in non-Unicode text, allowing a reasonable guess that text is Unicode when a BOM is present.</span></span>

<span data-ttu-id="9de13-165">AJ megadása nem kötelező, és azok elfogadását nem, népszerű Linux világ, mert egy megbízható egyezmény UTF-8 mindenhol használja.</span><span class="sxs-lookup"><span data-stu-id="9de13-165">BOMs are optional and their adoption isn't as popular in the Linux world because a dependable convention of UTF-8 is used everywhere.</span></span> <span data-ttu-id="9de13-166">A legtöbb Linux-alkalmazások feltételezik, hogy szövegbevitel UTF-8 kódolása.</span><span class="sxs-lookup"><span data-stu-id="9de13-166">Most Linux applications presume that text input is encoded in UTF-8.</span></span> <span data-ttu-id="9de13-167">Míg számos Linux-alkalmazás ismeri fel, és a egy AJ megfelelően kezeli, számos viszont nem, és kezelhetők az ilyen alkalmazások szöveges összetevők.</span><span class="sxs-lookup"><span data-stu-id="9de13-167">While many Linux applications will recognize and correctly handle a BOM, a number do not, leading to artifacts in text manipulated with those applications.</span></span>

<span data-ttu-id="9de13-168">**Ezért**:</span><span class="sxs-lookup"><span data-stu-id="9de13-168">**Therefore**:</span></span>

- <span data-ttu-id="9de13-169">Ha elsősorban a Windows-alkalmazások és a Windows PowerShell dolgozik, a részesítsék előnyben, például az UTF-8 AJ vagy UTF-16 kódolást.</span><span class="sxs-lookup"><span data-stu-id="9de13-169">If you work primarily with Windows applications and Windows PowerShell, you should prefer an encoding like UTF-8 with BOM or UTF-16.</span></span>
- <span data-ttu-id="9de13-170">Platformok közötti használathoz, az UTF-8 AJ-kell használni.</span><span class="sxs-lookup"><span data-stu-id="9de13-170">If you work across platforms, you should prefer UTF-8 with BOM.</span></span>
- <span data-ttu-id="9de13-171">Ha Linux-kapcsolódó környezeteket főleg a dolgozik, az UTF-8 AJ nélkül kell inkább.</span><span class="sxs-lookup"><span data-stu-id="9de13-171">If you work mainly in Linux-associated contexts, you should prefer UTF-8 without BOM.</span></span>
- <span data-ttu-id="9de13-172">Latin-1 és a Windows-1252-es rendszer lehetőség szerint kerülendő lényegében örökölt kódolásokat.</span><span class="sxs-lookup"><span data-stu-id="9de13-172">Windows-1252 and latin-1 are essentially legacy encodings that you should avoid if possible.</span></span>
  <span data-ttu-id="9de13-173">Előfordulhat, hogy néhány régebbi Windows-alkalmazások azonban rajtuk függ.</span><span class="sxs-lookup"><span data-stu-id="9de13-173">However, some older Windows applications may depend on them.</span></span>
- <span data-ttu-id="9de13-174">Célszerű is érdemes megjegyezni, hogy a parancsfájl aláírása, [kódolás függő](https://github.com/PowerShell/PowerShell/issues/3466), egy aláírt parancsfájl kódolás módosítását jelenti számára lesz szükség.</span><span class="sxs-lookup"><span data-stu-id="9de13-174">It's also worth noting that script signing is [encoding-dependent](https://github.com/PowerShell/PowerShell/issues/3466), meaning a change of encoding on a signed script will require resigning.</span></span>

## <a name="configuring-vscode"></a><span data-ttu-id="9de13-175">VSCode konfigurálása</span><span class="sxs-lookup"><span data-stu-id="9de13-175">Configuring VSCode</span></span>

<span data-ttu-id="9de13-176">VSCode az alapértelmezett kódolás az UTF-8 AJ nélkül.</span><span class="sxs-lookup"><span data-stu-id="9de13-176">VSCode's default encoding is UTF-8 without BOM.</span></span>

<span data-ttu-id="9de13-177">Beállítása [A VSCode-kódolás][], nyissa meg a VSCode-beállításokat (<kbd>Ctrl</kbd>+<kbd>,</kbd>) és állítsa be a `"files.encoding"` beállítást:</span><span class="sxs-lookup"><span data-stu-id="9de13-177">To set [VSCode's encoding][], go to the VSCode settings (<kbd>Ctrl</kbd>+<kbd>,</kbd>) and set the `"files.encoding"` setting:</span></span>

```json
"files.encoding": "utf8bom"
```

<span data-ttu-id="9de13-178">Néhány lehetséges értékei a következők:</span><span class="sxs-lookup"><span data-stu-id="9de13-178">Some possible values are:</span></span>

- <span data-ttu-id="9de13-179">`utf8`: [UTF-8] AJ nélkül</span><span class="sxs-lookup"><span data-stu-id="9de13-179">`utf8`: [UTF-8] without BOM</span></span>
- <span data-ttu-id="9de13-180">`utf8bom`: [UTF-8] az Anyagjegyzék</span><span class="sxs-lookup"><span data-stu-id="9de13-180">`utf8bom`: [UTF-8] with BOM</span></span>
- <span data-ttu-id="9de13-181">`utf16le`: Little endian [UTF-16]</span><span class="sxs-lookup"><span data-stu-id="9de13-181">`utf16le`: Little endian [UTF-16]</span></span>
- <span data-ttu-id="9de13-182">`utf16be`: A big endian [UTF-16]</span><span class="sxs-lookup"><span data-stu-id="9de13-182">`utf16be`: Big endian [UTF-16]</span></span>
- <span data-ttu-id="9de13-183">`windows1252`: [Windows-1252]</span><span class="sxs-lookup"><span data-stu-id="9de13-183">`windows1252`: [Windows-1252]</span></span>

<span data-ttu-id="9de13-184">A grafikus felhasználói Felülettel nézetben a legördülő lista kell kap, vagy kiegészítése, a JSON-fájlban megtekintheti.</span><span class="sxs-lookup"><span data-stu-id="9de13-184">You should get a dropdown for this in the GUI view, or completions for it in the JSON view.</span></span>

<span data-ttu-id="9de13-185">Emellett a kapcsolatok automatikus észleléssel kódolást, ha lehetséges, adja hozzá a következő:</span><span class="sxs-lookup"><span data-stu-id="9de13-185">You can also add the following to autodetect encoding when possible:</span></span>

```json
"files.autoGuessEncoding": true
```

<span data-ttu-id="9de13-186">Ha nem szeretné ezeket a beállításokat az összes fájltípus hatással, VSCode is lehetővé teszi, hogy nyelvenkénti konfigurációkat.</span><span class="sxs-lookup"><span data-stu-id="9de13-186">If you don't want these settings to affect all files types, VSCode also allows per-language configurations.</span></span> <span data-ttu-id="9de13-187">Hozzon létre egy nyelvspecifikus beállítás beállításait írja a `[<language-name>]` mező.</span><span class="sxs-lookup"><span data-stu-id="9de13-187">Create a language-specific setting by putting settings in a `[<language-name>]` field.</span></span> <span data-ttu-id="9de13-188">Például:</span><span class="sxs-lookup"><span data-stu-id="9de13-188">For example:</span></span>

```json
"[powershell]": {
    "files.encoding": "utf8bom",
    "files.autoGuessEncoding": true
}
```

## <a name="configuring-powershell"></a><span data-ttu-id="9de13-189">PowerShell konfigurálása</span><span class="sxs-lookup"><span data-stu-id="9de13-189">Configuring PowerShell</span></span>

<span data-ttu-id="9de13-190">PowerShell az alapértelmezett kódolás verziójától függően változik:</span><span class="sxs-lookup"><span data-stu-id="9de13-190">PowerShell's default encoding varies depending on version:</span></span>

- <span data-ttu-id="9de13-191">A PowerShell 6, az alapértelmezett kódolás az UTF-8 nélkül AJ minden platformon.</span><span class="sxs-lookup"><span data-stu-id="9de13-191">In PowerShell 6+, the default encoding is UTF-8 without BOM on all platforms.</span></span>
- <span data-ttu-id="9de13-192">A Windows PowerShellben, az alapértelmezett kódolás az általában Windows-1252-es, bővítmény [latin 1][], más néven ISO 8859 – 1.</span><span class="sxs-lookup"><span data-stu-id="9de13-192">In Windows PowerShell, the default encoding is usually Windows-1252, an extension of [latin-1][], also known as ISO 8859-1.</span></span>

<span data-ttu-id="9de13-193">A PowerShell 5 + találja meg ez az alapértelmezett kódolást:</span><span class="sxs-lookup"><span data-stu-id="9de13-193">In PowerShell 5+ you can find your default encoding with this:</span></span>

```powershell
[psobject].Assembly.GetTypes() | Where-Object { $_.Name -eq 'ClrFacade'} |
  ForEach-Object {
    $_.GetMethod('GetDefaultEncoding', [System.Reflection.BindingFlags]'nonpublic,static').Invoke($null, @())
  }
```

<span data-ttu-id="9de13-194">A következő [parancsfájl](https://gist.github.com/rjmholt/3d8dd4849f718c914132ce3c5b278e0e) határozza meg, mi a PowerShell-munkamenetet kódolás nélkül AJ parancsfájl kikövetkezteti használható.</span><span class="sxs-lookup"><span data-stu-id="9de13-194">The following [script](https://gist.github.com/rjmholt/3d8dd4849f718c914132ce3c5b278e0e) can be used to determine what encoding your PowerShell session infers for a script without a BOM.</span></span>

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

<span data-ttu-id="9de13-195">Konfigurálása a PowerShell használata egy adott kódolási általában a profil beállításainak használatával lehetőség.</span><span class="sxs-lookup"><span data-stu-id="9de13-195">It's possible to configure PowerShell to use a given encoding more generally using profile settings.</span></span> <span data-ttu-id="9de13-196">Lásd az alábbi cikkeket:</span><span class="sxs-lookup"><span data-stu-id="9de13-196">See the following articles:</span></span>

- <span data-ttu-id="9de13-197">[@mklement0]a [PowerShell a StackOverflow-n kódolással kapcsolatos válasz](https://stackoverflow.com/a/40098904).</span><span class="sxs-lookup"><span data-stu-id="9de13-197">[@mklement0]'s [answer about PowerShell encoding on StackOverflow](https://stackoverflow.com/a/40098904).</span></span>
- <span data-ttu-id="9de13-198">[@rkeithhill]a [többé vesződnie a sérült a PowerShell AJ nélküli UTF-8 bemeneti szóló blogbejegyzést](https://rkeithhill.wordpress.com/2010/05/26/handling-native-exe-output-encoding-in-utf8-with-no-bom/).</span><span class="sxs-lookup"><span data-stu-id="9de13-198">[@rkeithhill]'s [blog post about dealing with BOM-less UTF-8 input in PowerShell](https://rkeithhill.wordpress.com/2010/05/26/handling-native-exe-output-encoding-in-utf8-with-no-bom/).</span></span>

<span data-ttu-id="9de13-199">Nem alkalmas kényszerítése a PowerShell használata az adott bemeneti kódolást.</span><span class="sxs-lookup"><span data-stu-id="9de13-199">It's not possible to force PowerShell to use a specific input encoding.</span></span> <span data-ttu-id="9de13-200">A PowerShell 5.1-es és Windows-1252 kódolást, ha ott nem Anyagjegyzék nem az alapértelmezett alatt.</span><span class="sxs-lookup"><span data-stu-id="9de13-200">PowerShell 5.1 and below default to Windows-1252 encoding when there's no BOM.</span></span> <span data-ttu-id="9de13-201">Együttműködési okokból célszerű menteni a parancsfájlok az Anyagjegyzék Unicode formátumú.</span><span class="sxs-lookup"><span data-stu-id="9de13-201">For interoperability reasons, it's best to save scripts in a Unicode format with a BOM.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9de13-202">Bármely eszközzel rendelkezik, hogy touch PowerShell parancsfájlok hatással lehet a kódolási beállításokat, vagy újra kódolása a parancsfájlokat egy másik kódolás.</span><span class="sxs-lookup"><span data-stu-id="9de13-202">Any other tools you have that touch PowerShell scripts may be affected by your encoding choices or re-encode your scripts to another encoding.</span></span>

### <a name="existing-scripts"></a><span data-ttu-id="9de13-203">Meglévő parancsfájlok</span><span class="sxs-lookup"><span data-stu-id="9de13-203">Existing scripts</span></span>

<span data-ttu-id="9de13-204">Már a fájlrendszerben parancsfájlok kell újra értéket kódolni kell az új választott kódolás.</span><span class="sxs-lookup"><span data-stu-id="9de13-204">Scripts already on the file system may need to be re-encoded to your new chosen encoding.</span></span> <span data-ttu-id="9de13-205">VSCode alsó sáv látni fogja a címkét az UTF-8.</span><span class="sxs-lookup"><span data-stu-id="9de13-205">In the bottom bar of VSCode, you'll see the label UTF-8.</span></span> <span data-ttu-id="9de13-206">A gombra kattintva nyissa meg a művelet sávon és **kódolással mentése**.</span><span class="sxs-lookup"><span data-stu-id="9de13-206">Click it to open the action bar and select **Save with encoding**.</span></span> <span data-ttu-id="9de13-207">Most kiválaszthatja, hogy a fájl egy új kódolást.</span><span class="sxs-lookup"><span data-stu-id="9de13-207">You can now pick a new encoding for that file.</span></span> <span data-ttu-id="9de13-208">Lásd: [A VSCode-kódolás][] teljes útmutatás.</span><span class="sxs-lookup"><span data-stu-id="9de13-208">See [VSCode's encoding][] for full instructions.</span></span>

<span data-ttu-id="9de13-209">Ha újra kódolása több fájl van szüksége, használhatja az alábbi parancsfájlt:</span><span class="sxs-lookup"><span data-stu-id="9de13-209">If you need to re-encode multiple files, you can use the following script:</span></span>

```powershell
Get-ChildItem *.ps1 -Recurse | ForEach-Object {
    $content = Get-Content -Path $_
    Set-Content -Path $_.Fullname -Value $content -Encoding UTF8 -PassThru -Force
}
```

### <a name="the-powershell-integrated-scripting-environment-ise"></a><span data-ttu-id="9de13-210">A PowerShell integrált parancsfájlkezelési környezet (ISE)</span><span class="sxs-lookup"><span data-stu-id="9de13-210">The PowerShell Integrated Scripting Environment (ISE)</span></span>

<span data-ttu-id="9de13-211">Ha a PowerShell ISE-alapú parancsprogramok is szerkeszti, kell szinkronizálhatja a kódolási beállításait.</span><span class="sxs-lookup"><span data-stu-id="9de13-211">If you also edit scripts using the PowerShell ISE, you need to synchronize your encoding settings there.</span></span>

<span data-ttu-id="9de13-212">A ISE kell figyelembe veszi a AJ, de azt is enumerálható reflexióval az [a kódolás](https://bensonxion.wordpress.com/2012/04/25/powershell-ise-default-saveas-encoding/).</span><span class="sxs-lookup"><span data-stu-id="9de13-212">The ISE should honor a BOM, but it's also possible to use reflection to [set the encoding](https://bensonxion.wordpress.com/2012/04/25/powershell-ise-default-saveas-encoding/).</span></span>
<span data-ttu-id="9de13-213">Vegye figyelembe, hogy ez nem őrizhető meg, induló cégek között.</span><span class="sxs-lookup"><span data-stu-id="9de13-213">Note that this wouldn't be persisted between startups.</span></span>

### <a name="source-control-software"></a><span data-ttu-id="9de13-214">Forrás felügyeleti szoftver</span><span class="sxs-lookup"><span data-stu-id="9de13-214">Source control software</span></span>

<span data-ttu-id="9de13-215">Egyes forrás ellenőrző eszközök, például a git, figyelmen kívül hagyása kódolásokat; a git csak a bájtok követi nyomon.</span><span class="sxs-lookup"><span data-stu-id="9de13-215">Some source control tools, such as git, ignore encodings; git just tracks the bytes.</span></span>
<span data-ttu-id="9de13-216">Mások, például az Azure DevOps- vagy Mercurial, előfordulhat, hogy nem.</span><span class="sxs-lookup"><span data-stu-id="9de13-216">Others, like Azure DevOps or Mercurial, may not.</span></span> <span data-ttu-id="9de13-217">Még néhány git-alapú eszközök válik a szöveg dekódolása.</span><span class="sxs-lookup"><span data-stu-id="9de13-217">Even some git-based tools rely on decoding text.</span></span>

<span data-ttu-id="9de13-218">Ha ez a helyzet, ellenőrizze, hogy:</span><span class="sxs-lookup"><span data-stu-id="9de13-218">When this is the case, make sure you:</span></span>

- <span data-ttu-id="9de13-219">Konfigurálja a szövegkódolás a VSCode-konfigurációnak megfelelően a verziókövetési rendszerben.</span><span class="sxs-lookup"><span data-stu-id="9de13-219">Configure the text encoding in your source control to match your VSCode configuration.</span></span>
- <span data-ttu-id="9de13-220">Győződjön meg róla, minden fájl a rendszer ellenőrzi a megfelelő kódolása forrásvezérlőben.</span><span class="sxs-lookup"><span data-stu-id="9de13-220">Ensure all your files are checked into source control in the relevant encoding.</span></span>
- <span data-ttu-id="9de13-221">Legyen óvatos az olyan módosításait a verziókövetés keresztül fogadott kódolást.</span><span class="sxs-lookup"><span data-stu-id="9de13-221">Be wary of changes to the encoding received through source control.</span></span> <span data-ttu-id="9de13-222">Ez a kulcs jele egy különbözeti utaló módosításokat, de ha semmit nem úgy tűnik, hogy megváltozott (mivel bájt rendelkeznek, de nem rendelkezik karakter).</span><span class="sxs-lookup"><span data-stu-id="9de13-222">A key sign of this is a diff indicating changes but where nothing seems to have changed (because bytes have but characters have not).</span></span>

### <a name="collaborators-environments"></a><span data-ttu-id="9de13-223">A közreműködők környezetek</span><span class="sxs-lookup"><span data-stu-id="9de13-223">Collaborators' environments</span></span>

<span data-ttu-id="9de13-224">Felett Verziókövetés beállítása, győződjön meg arról, a közreműködők, a megosztott fájlok nem rendelkezik, amelyek felülírják a kódolás szerint újrakódolása PowerShell fájlok beállításait.</span><span class="sxs-lookup"><span data-stu-id="9de13-224">On top of configuring source control, ensure that your collaborators on any files you share don't have settings that override your encoding by re-encoding PowerShell files.</span></span>

### <a name="other-programs"></a><span data-ttu-id="9de13-225">Más programok</span><span class="sxs-lookup"><span data-stu-id="9de13-225">Other programs</span></span>

<span data-ttu-id="9de13-226">Minden más programot, amelyet olvas vagy ír egy PowerShell-parancsprogram újra előfordulhat, hogy kódolja azokat.</span><span class="sxs-lookup"><span data-stu-id="9de13-226">Any other program that reads or writes a PowerShell script may re-encode it.</span></span>

<span data-ttu-id="9de13-227">Néhány példa a következők:</span><span class="sxs-lookup"><span data-stu-id="9de13-227">Some examples are:</span></span>

- <span data-ttu-id="9de13-228">A Vágólap használatával másolja és illessze be a parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="9de13-228">Using the clipboard to copy and paste a script.</span></span> <span data-ttu-id="9de13-229">Ez a gyakori helyzetek, például az:</span><span class="sxs-lookup"><span data-stu-id="9de13-229">This is common in scenarios like:</span></span>
  - <span data-ttu-id="9de13-230">A parancsfájl másolása virtuális gépre</span><span class="sxs-lookup"><span data-stu-id="9de13-230">Copying a script into a VM</span></span>
  - <span data-ttu-id="9de13-231">A parancsfájl egy e-mailben vagy weblap másolása</span><span class="sxs-lookup"><span data-stu-id="9de13-231">Copying a script out of an email or webpage</span></span>
  - <span data-ttu-id="9de13-232">A parancsfájl másolása vagy onnan máshová egy Microsoft Word és PowerPoint-dokumentum</span><span class="sxs-lookup"><span data-stu-id="9de13-232">Copying a script into or out of a Microsoft Word or PowerPoint document</span></span>
- <span data-ttu-id="9de13-233">Más szövegszerkesztők, például:</span><span class="sxs-lookup"><span data-stu-id="9de13-233">Other text editors, such as:</span></span>
  - <span data-ttu-id="9de13-234">A Jegyzettömb</span><span class="sxs-lookup"><span data-stu-id="9de13-234">Notepad</span></span>
  - <span data-ttu-id="9de13-235">vim</span><span class="sxs-lookup"><span data-stu-id="9de13-235">vim</span></span>
  - <span data-ttu-id="9de13-236">Bármely más PowerShell parancsprogram-szerkesztő</span><span class="sxs-lookup"><span data-stu-id="9de13-236">Any other PowerShell script editor</span></span>
- <span data-ttu-id="9de13-237">Segédprogramok, mint szerkesztő szövege:</span><span class="sxs-lookup"><span data-stu-id="9de13-237">Text editing utilities, like:</span></span>
  - `Get-Content`/`Set-Content`/`Out-File`
  - <span data-ttu-id="9de13-238">Például a PowerShell átirányítási operátorok `>` és `>>`</span><span class="sxs-lookup"><span data-stu-id="9de13-238">PowerShell redirection operators like `>` and `>>`</span></span>
  - `sed`/`awk`
- <span data-ttu-id="9de13-239">Fájl adatátviteli programok, például:</span><span class="sxs-lookup"><span data-stu-id="9de13-239">File transfer programs, like:</span></span>
  - <span data-ttu-id="9de13-240">A webböngészőben parancsprogramok letöltése esetén</span><span class="sxs-lookup"><span data-stu-id="9de13-240">A web browser, when downloading scripts</span></span>
  - <span data-ttu-id="9de13-241">Fájlmegosztás</span><span class="sxs-lookup"><span data-stu-id="9de13-241">A file share</span></span>

<span data-ttu-id="9de13-242">Egyes eszközök kezelésére bájt szöveg helyett, de más kódolási konfigurációk kínálnak.</span><span class="sxs-lookup"><span data-stu-id="9de13-242">Some of these tools deal in bytes rather than text, but others offer encoding configurations.</span></span> <span data-ttu-id="9de13-243">Ezekben az esetekben, ahol kell konfigurálnia a kódolást kell, hogy ugyanaz, mint a szerkesztő kódolási problémák megelőzése érdekében.</span><span class="sxs-lookup"><span data-stu-id="9de13-243">In those cases where you need to configure an encoding, you need to make it the same as your editor encoding to prevent problems.</span></span>

## <a name="other-resources-on-encoding-in-powershell"></a><span data-ttu-id="9de13-244">Kódolás a PowerShell egyéb erőforrásokhoz</span><span class="sxs-lookup"><span data-stu-id="9de13-244">Other resources on encoding in PowerShell</span></span>

<span data-ttu-id="9de13-245">Van néhány egyéb hasznos bejegyzések kódolás és a kódolás a PowerShell konfigurálása, amelyek olvasási érdemes:</span><span class="sxs-lookup"><span data-stu-id="9de13-245">There are a few other nice posts on encoding and configuring encoding in PowerShell that are worth a read:</span></span>

- <span data-ttu-id="9de13-246">[@mklement0]a [a PowerShell a StackOverflow-n kódolási összegzése](https://stackoverflow.com/questions/40098771/changing-powershells-default-output-encoding-to-utf-8)</span><span class="sxs-lookup"><span data-stu-id="9de13-246">[@mklement0]'s [summary of PowerShell encoding on StackOverflow](https://stackoverflow.com/questions/40098771/changing-powershells-default-output-encoding-to-utf-8)</span></span>
- <span data-ttu-id="9de13-247">Előző problémák vscode-PowerShell kódolási problémák megnyitása:</span><span class="sxs-lookup"><span data-stu-id="9de13-247">Previous issues opened on vscode-PowerShell for encoding problems:</span></span>
  - [<span data-ttu-id="9de13-248">#1308</span><span class="sxs-lookup"><span data-stu-id="9de13-248">#1308</span></span>](https://github.com/PowerShell/vscode-powershell/issues/1308)
  - [<span data-ttu-id="9de13-249">#1628</span><span class="sxs-lookup"><span data-stu-id="9de13-249">#1628</span></span>](https://github.com/PowerShell/vscode-powershell/issues/1628)
  - [<span data-ttu-id="9de13-250">#1680</span><span class="sxs-lookup"><span data-stu-id="9de13-250">#1680</span></span>](https://github.com/PowerShell/vscode-powershell/issues/1680)
  - [<span data-ttu-id="9de13-251">#1744</span><span class="sxs-lookup"><span data-stu-id="9de13-251">#1744</span></span>](https://github.com/PowerShell/vscode-powershell/issues/1744)
  - [<span data-ttu-id="9de13-252">#1751</span><span class="sxs-lookup"><span data-stu-id="9de13-252">#1751</span></span>](https://github.com/PowerShell/vscode-powershell/issues/1751)
- [<span data-ttu-id="9de13-253">A klasszikus *Joel szoftverfrissítési* Unicode kapcsolatos Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="9de13-253">The classic *Joel on Software* write up about Unicode</span></span>](https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/)
- [<span data-ttu-id="9de13-254">Kódolás a .NET Standard</span><span class="sxs-lookup"><span data-stu-id="9de13-254">Encoding in .NET Standard</span></span>](https://github.com/dotnet/standard/issues/260#issuecomment-289549508)


[@mklement0]: https://github.com/mklement0
[@rkeithhill]: https://github.com/rkeithhill
[Windows-1252]: https://wikipedia.org/wiki/Windows-1252
[Latin 1]: https://wikipedia.org/wiki/ISO/IEC_8859-1
[latin-1]: https://wikipedia.org/wiki/ISO/IEC_8859-1
[UTF-8]: https://wikipedia.org/wiki/UTF-8
[bájtsorrendjelző]: https://wikipedia.org/wiki/Byte_order_mark
[byte-order mark]: https://wikipedia.org/wiki/Byte_order_mark
[UTF-16]: https://wikipedia.org/wiki/UTF-16
[Nyelvi protokoll]: https://microsoft.github.io/language-server-protocol/
[Language Server Protocol]: https://microsoft.github.io/language-server-protocol/
[A VSCode-kódolás]: https://code.visualstudio.com/docs/editor/codebasics#_file-encoding-support
[VSCode's encoding]: https://code.visualstudio.com/docs/editor/codebasics#_file-encoding-support
