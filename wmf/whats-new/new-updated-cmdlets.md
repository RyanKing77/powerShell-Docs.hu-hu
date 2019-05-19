---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
title: Új és frissített parancsmagok
ms.openlocfilehash: 9ec31c89c0bc4b111b40e2d4725fa0782a573204
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65856244"
---
# <a name="new-and-updated-cmdlets"></a><span data-ttu-id="917a1-103">Új és frissített parancsmagok</span><span class="sxs-lookup"><span data-stu-id="917a1-103">New and updated cmdlets</span></span>

<span data-ttu-id="917a1-104">A közösségi visszajelzések alapján megjelent új és frissített meglévő parancsmagok hozzáadtuk.</span><span class="sxs-lookup"><span data-stu-id="917a1-104">We have added new and updated existing cmdlets based on feedback from the community.</span></span>

## <a name="archive-cmdlets"></a><span data-ttu-id="917a1-105">Archív parancsmagok</span><span class="sxs-lookup"><span data-stu-id="917a1-105">Archive cmdlets</span></span>

<span data-ttu-id="917a1-106">Két új parancsmagot `Compress-Archive` és `Expand-Archive`, hagyjuk, hogy tömöríteni, és bontsa ki a ZIP-fájlokat.</span><span class="sxs-lookup"><span data-stu-id="917a1-106">Two new cmdlets, `Compress-Archive` and `Expand-Archive`, let you compress and expand ZIP files.</span></span>

<span data-ttu-id="917a1-107">További információkért lásd: a [Microsoft.Powershell.Archive](/powershell/module/microsoft.powershell.archive/) modul dokumentációjában talál.</span><span class="sxs-lookup"><span data-stu-id="917a1-107">For more information, see the [Microsoft.Powershell.Archive](/powershell/module/microsoft.powershell.archive/) module documentation.</span></span>

## <a name="catalog-cmdlets"></a><span data-ttu-id="917a1-108">Katalógusbeli parancsmagok</span><span class="sxs-lookup"><span data-stu-id="917a1-108">Catalog Cmdlets</span></span>

<span data-ttu-id="917a1-109">Két új parancsmag hozzáadva az Microsoft.PowerShell.Security modulban.</span><span class="sxs-lookup"><span data-stu-id="917a1-109">Two new cmdlets have been added in the Microsoft.PowerShell.Security module.</span></span>

- [<span data-ttu-id="917a1-110">New-FileCatalog</span><span class="sxs-lookup"><span data-stu-id="917a1-110">New-FileCatalog</span></span>](/powershell/module/microsoft.powershell.security/New-FileCatalog)
- [<span data-ttu-id="917a1-111">Test-FileCatalog</span><span class="sxs-lookup"><span data-stu-id="917a1-111">Test-FileCatalog</span></span>](/powershell/module/microsoft.powershell.security/Test-FileCatalog)

<span data-ttu-id="917a1-112">Ezek létrehozása és ellenőrzése Windows katalógusfájlok.</span><span class="sxs-lookup"><span data-stu-id="917a1-112">These generate and validate Windows catalog files.</span></span>

## <a name="clipboard-cmdlets"></a><span data-ttu-id="917a1-113">Vágólap-parancsmagok</span><span class="sxs-lookup"><span data-stu-id="917a1-113">Clipboard cmdlets</span></span>

<span data-ttu-id="917a1-114">`Get-Clipboard` és `Set-Clipboard` könnyebben, tartalom, és a egy Windows PowerShell-munkamenetből átvitelét.</span><span class="sxs-lookup"><span data-stu-id="917a1-114">`Get-Clipboard` and `Set-Clipboard` make it easier for you to transfer content to and from a Windows PowerShell session.</span></span> <span data-ttu-id="917a1-115">A vágólap-parancsmagok támogatják a lemezképek, a hangfájlok, a fájl listák és a szöveg.</span><span class="sxs-lookup"><span data-stu-id="917a1-115">The Clipboard cmdlets support images, audio files, file lists, and text.</span></span>

<span data-ttu-id="917a1-116">További információ:</span><span class="sxs-lookup"><span data-stu-id="917a1-116">For more information, see:</span></span>

- [<span data-ttu-id="917a1-117">Get-Clipboard</span><span class="sxs-lookup"><span data-stu-id="917a1-117">Get-Clipboard</span></span>](/powershell/module/Microsoft.PowerShell.Management/Get-Clipboard)
- [<span data-ttu-id="917a1-118">Set-Clipboard</span><span class="sxs-lookup"><span data-stu-id="917a1-118">Set-Clipboard</span></span>](/powershell/module/Microsoft.PowerShell.Management/Set-Clipboard)

## <a name="cryptographic-message-syntax-cms-cmdlets"></a><span data-ttu-id="917a1-119">Titkosítási üzenet szintaxis-(CMS-) parancsmagok</span><span class="sxs-lookup"><span data-stu-id="917a1-119">Cryptographic Message Syntax (CMS) cmdlets</span></span>

<span data-ttu-id="917a1-120">A titkosítási üzenet szintaxis parancsmagok támogatják a titkosítási és visszafejtési a IETF szabvány formátum használatával titkosítási szempontból védelme érdekében üzenetet megfelelően tartalom [RFC5652](https://tools.ietf.org/html/rfc5652).</span><span class="sxs-lookup"><span data-stu-id="917a1-120">The Cryptographic Message Syntax cmdlets support encryption and decryption of content using the IETF standard format for cryptographically protecting messages as documented by [RFC5652](https://tools.ietf.org/html/rfc5652).</span></span>

<span data-ttu-id="917a1-121">A standard szintű tartalomkezelő rendszer titkosítási valósítja meg a nyilvános kulcsú titkosítás, ahol a kulcsot használja a tartalom titkosításához (a *nyilvános kulcs*) és a kulcs használatával fejti vissza a tartalom (a *titkos kulcs*) jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="917a1-121">The CMS encryption standard implements public key cryptography, where the key used to encrypt content (the *public key*) and the key used to decrypt content (the *private key*) are separate.</span></span>

<span data-ttu-id="917a1-122">A nyilvános kulcs széles körben történő megosztásának, és nem érzékeny adatokat.</span><span class="sxs-lookup"><span data-stu-id="917a1-122">Your public key can be shared widely and is not sensitive data.</span></span> <span data-ttu-id="917a1-123">A nyilvános kulccsal titkosított tartalmat a titkos kulccsal csak visszafejteni.</span><span class="sxs-lookup"><span data-stu-id="917a1-123">Any content encrypted with the public key can only be decrypted using the private key.</span></span> <span data-ttu-id="917a1-124">További információkért lásd: [nyilvános kulcsú titkosítással](https://en.wikipedia.org/wiki/Public-key_cryptography).</span><span class="sxs-lookup"><span data-stu-id="917a1-124">For more information, see [Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography).</span></span>

<span data-ttu-id="917a1-125">További információk:</span><span class="sxs-lookup"><span data-stu-id="917a1-125">For more information see:</span></span>

- [<span data-ttu-id="917a1-126">Get-CmsMessage</span><span class="sxs-lookup"><span data-stu-id="917a1-126">Get-CmsMessage</span></span>](/powershell/module/Microsoft.PowerShell.Security/Get-CmsMessage.md)
- [<span data-ttu-id="917a1-127">Protect-CmsMessage</span><span class="sxs-lookup"><span data-stu-id="917a1-127">Protect-CmsMessage</span></span>](/powershell/module/Microsoft.PowerShell.Security/Protect-CmsMessage.md)
- [<span data-ttu-id="917a1-128">Unprotect-CmsMessage</span><span class="sxs-lookup"><span data-stu-id="917a1-128">Unprotect-CmsMessage</span></span>](/powershell/module/Microsoft.PowerShell.Security/rotect-CmsMessage.md)

<span data-ttu-id="917a1-129">Tanúsítványok egyedi kulcshasználat azonosítója (EKU), például a "Kód aláírása" vagy 'Titkosítva Mail', azonosításához azokat az adatokat titkosítási tanúsítványok a PowerShell szükséges.</span><span class="sxs-lookup"><span data-stu-id="917a1-129">Certificates require a unique key usage identifier (EKU), such as 'Code Signing' or 'Encrypted Mail', to identify them as data encryption certificates in PowerShell.</span></span> <span data-ttu-id="917a1-130">A tanúsítványszolgáltató dokumentum titkosítási tanúsítványok megtekintéséhez használja a **DocumentEncryptionCert** dinamikus paraméterét `Get-ChildItem`:</span><span class="sxs-lookup"><span data-stu-id="917a1-130">To view document encryption certificates in the certificate provider, you can use the **DocumentEncryptionCert** dynamic parameter of `Get-ChildItem`:</span></span>

```powershell
Get-ChildItem Cert:\CurrentUser -DocumentEncryptionCert -Recurse
```

## <a name="extract-and-parse-structured-objects-from-string-content"></a><span data-ttu-id="917a1-131">Strukturált objektumok karakterlánc tartalom kibontása és elemzése</span><span class="sxs-lookup"><span data-stu-id="917a1-131">Extract and parse structured objects from string content</span></span>

### <a name="convertfrom-string"></a><span data-ttu-id="917a1-132">ConvertFrom-karakterlánc</span><span class="sxs-lookup"><span data-stu-id="917a1-132">ConvertFrom-String</span></span>

<span data-ttu-id="917a1-133">Az új `ConvertFrom-String` parancsmag két módot támogat:</span><span class="sxs-lookup"><span data-stu-id="917a1-133">The new `ConvertFrom-String` cmdlet supports two modes:</span></span>

- <span data-ttu-id="917a1-134">Alapszintű tagolt-elemzés</span><span class="sxs-lookup"><span data-stu-id="917a1-134">Basic delimited parsing</span></span>
- <span data-ttu-id="917a1-135">Automatikusan létrehozott példa adatvezérelt-elemzés</span><span class="sxs-lookup"><span data-stu-id="917a1-135">Auto generated example-driven parsing</span></span>

<span data-ttu-id="917a1-136">Tagolt elemzés, alapértelmezés szerint bontja a bemenet üres helyet, és a tulajdonságnevek rendel az eredményül kapott csoportok.</span><span class="sxs-lookup"><span data-stu-id="917a1-136">Delimited parsing, by default, splits the input at white space, and assigns property names to the resulting groups.</span></span>

<span data-ttu-id="917a1-137">A **UpdateTemplate** paraméter menti a tanulási algoritmus eredményeit a sablonfájlt megjegyzést.</span><span class="sxs-lookup"><span data-stu-id="917a1-137">The **UpdateTemplate** parameter saves the results of the learning algorithm into a comment in the template file.</span></span> <span data-ttu-id="917a1-138">Ez lehetővé teszi a learning feldolgozásához (a leglassabb fázis) egy egyszeri költség.</span><span class="sxs-lookup"><span data-stu-id="917a1-138">This makes the learning process (the slowest stage) a one-time cost.</span></span> <span data-ttu-id="917a1-139">Futó `ConvertFrom-String` a kódolt tanulási algoritmus tartalmazó sablonnal történő jelenleg szinte azonnali.</span><span class="sxs-lookup"><span data-stu-id="917a1-139">Running `ConvertFrom-String` with a template that contains the encoded learning algorithm is now nearly instantaneous.</span></span>

<span data-ttu-id="917a1-140">További információkért lásd: [ConvertFrom-karakterlánc](/powershell/module/Microsoft.PowerShell.Utility/ConvertFrom-String).</span><span class="sxs-lookup"><span data-stu-id="917a1-140">For more information, see [ConvertFrom-String](/powershell/module/Microsoft.PowerShell.Utility/ConvertFrom-String).</span></span>

### <a name="convert-string"></a><span data-ttu-id="917a1-141">Convert-String</span><span class="sxs-lookup"><span data-stu-id="917a1-141">Convert-String</span></span>

<span data-ttu-id="917a1-142">`Convert-String` lehetővé teszi előtt és után keresse meg a szöveg kívánt példái.</span><span class="sxs-lookup"><span data-stu-id="917a1-142">`Convert-String` allows you to provide before and after examples of how you want text to look.</span></span> <span data-ttu-id="917a1-143">A parancsmag automatikusan formázza a szöveget.</span><span class="sxs-lookup"><span data-stu-id="917a1-143">The cmdlet formats your text automatically.</span></span>

<span data-ttu-id="917a1-144">További információkért lásd: [Convert-karakterlánc](/powershell/module/Microsoft.PowerShell.Utility/Convert-String).</span><span class="sxs-lookup"><span data-stu-id="917a1-144">For more information, see [Convert-String](/powershell/module/Microsoft.PowerShell.Utility/Convert-String).</span></span>

## <a name="updates-to-fileinfo-object"></a><span data-ttu-id="917a1-145">A FileInfo objektum frissítései</span><span class="sxs-lookup"><span data-stu-id="917a1-145">Updates to FileInfo object</span></span>

<span data-ttu-id="917a1-146">Fájlverzió-információkat is félrevezető lehet, különösen azokban az esetekben, ahol a fájl javítva lett.</span><span class="sxs-lookup"><span data-stu-id="917a1-146">File version information can be misleading, especially in cases where the file was patched.</span></span> <span data-ttu-id="917a1-147">A WMF 5.0 ad hozzá új **FileVersionRaw** és **ProductVersionRaw** parancsfájl-tulajdonságok **FileInfo** objektumokat.</span><span class="sxs-lookup"><span data-stu-id="917a1-147">WMF 5.0 adds new **FileVersionRaw** and **ProductVersionRaw** script properties to **FileInfo** objects.</span></span>
<span data-ttu-id="917a1-148">A powershell.exe (feltéve, hogy $pid a PowerShell-folyamat azonosítója) jelenik meg az alábbiakban a tulajdonságai:</span><span class="sxs-lookup"><span data-stu-id="917a1-148">Here are the properties as displayed for powershell.exe (assuming $pid is the ID of the PowerShell process):</span></span>

```powershell
Get-Process -Id $pid -FileVersionInfo | Format-List *version*
```

```Output
FileVersionRaw    : 10.0.17763.1
ProductVersionRaw : 10.0.17763.1
FileVersion       : 10.0.17763.1 (WinBuild.160101.0800)
ProductVersion    : 10.0.17763.1
```

## <a name="format-hex"></a><span data-ttu-id="917a1-149">Format-Hex</span><span class="sxs-lookup"><span data-stu-id="917a1-149">Format-Hex</span></span>

<span data-ttu-id="917a1-150">`Format-Hex` lehetővé teszi hexadecimális formátumú szöveg vagy bináris adatok megtekintését.</span><span class="sxs-lookup"><span data-stu-id="917a1-150">`Format-Hex` lets you view text or binary data in hexadecimal format.</span></span>

<span data-ttu-id="917a1-151">További információkért lásd: [hexadecimális formátumban](/powershell/module/microsoft.powershell.utility/format-hex).</span><span class="sxs-lookup"><span data-stu-id="917a1-151">For more information, see [Format-Hex](/powershell/module/microsoft.powershell.utility/format-hex).</span></span>

## <a name="get-childitem-has--depth-parameter"></a><span data-ttu-id="917a1-152">Get-ChildItem rendelkezik - Depth paraméterrel</span><span class="sxs-lookup"><span data-stu-id="917a1-152">Get-ChildItem has -Depth parameter</span></span>

<span data-ttu-id="917a1-153">`Get-ChildItem` most már rendelkezik egy **mélysége** paraméter való használatra **Recurse** a rekurzió korlátozása:</span><span class="sxs-lookup"><span data-stu-id="917a1-153">`Get-ChildItem` now has a **Depth** parameter for use with **Recurse** to limit the recursion:</span></span>

## <a name="modules-support-for-declaring-version-ranges-1-etc"></a><span data-ttu-id="917a1-154">Modultámogatás a deklaráló verzió tartományok (1.\* stb.)</span><span class="sxs-lookup"><span data-stu-id="917a1-154">Modules support for declaring version ranges (1.\*, etc)</span></span>

<span data-ttu-id="917a1-155">Most már kombinálhatja **MinimumVersion** és **MaximumVersion** adott tartományon belüli modul importálásához.</span><span class="sxs-lookup"><span data-stu-id="917a1-155">You can now combine **MinimumVersion** and **MaximumVersion** to import module within specific range.</span></span> <span data-ttu-id="917a1-156">A paraméterek is támogatja a helyettesítő karaktereket.</span><span class="sxs-lookup"><span data-stu-id="917a1-156">The parameters also support wildcards.</span></span>

```powershell
Import-Module psreadline -Verbose -MinimumVersion 1.0 -MaximumVersion 1.2.*
```

```Output
VERBOSE: Loading module from path 'C:\Program Files\WindowsPowerShell\Modules\psreadline\1.1\psreadline.psd1'.
VERBOSE: Importing cmdlet 'Get-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Get-PSReadlineOption'.
VERBOSE: Importing cmdlet 'Remove-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Set-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Set-PSReadlineOption'.
VERBOSE: Importing function 'PSConsoleHostReadline'.
```

## <a name="new-guid"></a><span data-ttu-id="917a1-157">New-Guid</span><span class="sxs-lookup"><span data-stu-id="917a1-157">New-Guid</span></span>

<span data-ttu-id="917a1-158">Számos olyan ahol youneed az egyedi azonosítója.</span><span class="sxs-lookup"><span data-stu-id="917a1-158">There are many scenarios where youneed for unique identifier.</span></span> <span data-ttu-id="917a1-159">A `New-GUID` parancsmaggal hozhat létre egy új GUID-ja egyszerű módszert kínál.</span><span class="sxs-lookup"><span data-stu-id="917a1-159">The `New-GUID` cmdlet provides a simple way to create a new GUID.</span></span>

```powershell
New-Guid
```

```Output
Guid
----
e19d6ea5-3cc2-4db9-8095-0cdaed5a703d
```

## <a name="nonewline-parameter"></a><span data-ttu-id="917a1-160">NoNewLine paraméter</span><span class="sxs-lookup"><span data-stu-id="917a1-160">NoNewLine parameter</span></span>

<span data-ttu-id="917a1-161">`Out-File`, `Add-Content`, és `Set-Content` most már rendelkezik egy új **NoNewline** kapcsolót, amely egy új sor kihagyása után a kimenet.</span><span class="sxs-lookup"><span data-stu-id="917a1-161">`Out-File`, `Add-Content`, and `Set-Content` now have a new **NoNewline** switch which omits a new line after the output.</span></span> <span data-ttu-id="917a1-162">Például:</span><span class="sxs-lookup"><span data-stu-id="917a1-162">For example:</span></span>

```powershell
"This is " | Out-File -FilePath Example.txt -NoNewline
"a single " | Add-Content -Path Example.txt -NoNewline
"sentence." | Add-Content -Path Example.txt -NoNewline
Get-Content .\Example.txt

```Output
This is a single sentence.
```

<span data-ttu-id="917a1-163">Nélkül **NoNewline** megadott, minden egyes töredék lenne külön sorban:</span><span class="sxs-lookup"><span data-stu-id="917a1-163">Without **NoNewline** specified, each fragment would be on a separate line:</span></span>

```powershell
"This is " | Out-File -FilePath Example.txt
"a single " | Add-Content -Path Example.txt
"sentence." | Add-Content -Path Example.txt
Get-Content .\Example.txt
```

```Output
This is
a single
sentence.
```

## <a name="interact-with-symbolic-links-using-improved-item-cmdlets"></a><span data-ttu-id="917a1-164">Szimbolikus hivatkozások használata az Item-parancsmagokkal továbbfejlesztett kezelése</span><span class="sxs-lookup"><span data-stu-id="917a1-164">Interact with Symbolic links using improved Item cmdlets</span></span>

<span data-ttu-id="917a1-165">Az elem, valamint néhány kapcsolódó parancsmaghoz támogatja a szimbolikus hivatkozásokat volna terjeszteni.</span><span class="sxs-lookup"><span data-stu-id="917a1-165">The Item cmdlet and a few related cmdlets have been extended to support symbolic links.</span></span>

### <a name="symbolic-link-files"></a><span data-ttu-id="917a1-166">Szimbolikus hivatkozás fájlok</span><span class="sxs-lookup"><span data-stu-id="917a1-166">Symbolic link files</span></span>

<span data-ttu-id="917a1-167">Ebben a példában létrehozunk egy új szimbolikus hivatkozást fájlt MySymLinkFile.txt $pshome\profile.ps1 hivatkozik, amely C:\Temp mappájában.</span><span class="sxs-lookup"><span data-stu-id="917a1-167">In this example, we create a new symbolic link file named MySymLinkFile.txt in C:\Temp which links to $pshome\profile.ps1.</span></span> <span data-ttu-id="917a1-168">Mindhárom példában ugyanazt az eredményt hozhat létre.</span><span class="sxs-lookup"><span data-stu-id="917a1-168">All three examples produce the same result.</span></span>

```powershell
New-Item -ItemType SymbolicLink -Path C:\Temp -Name MySymLinkFile.txt -Value $pshome\profile.ps1
New-Item -ItemType SymbolicLink -Path C:\Temp\MySymLinkFile.txt -Value $pshome\profile.ps1
New-Item -ItemType SymbolicLink -Name C:\Temp\MySymLinkFile.txt -Value $pshome\profile.ps1
```

### <a name="symbolic-link-directories"></a><span data-ttu-id="917a1-169">Szimbolikus hivatkozás könyvtárak</span><span class="sxs-lookup"><span data-stu-id="917a1-169">Symbolic link directories</span></span>

<span data-ttu-id="917a1-170">Ebben a példában a $pshome mappára hivatkozik, amely C:\Temp mappájában MySymLinkDir nevű új szimbolikus hivatkozást könyvtárat hozunk létre.</span><span class="sxs-lookup"><span data-stu-id="917a1-170">In this example, we create a new symbolic link directory named MySymLinkDir in C:\Temp which links to the $pshome folder.</span></span> <span data-ttu-id="917a1-171">Mindhárom példában ugyanazt az eredményt hozhat létre.</span><span class="sxs-lookup"><span data-stu-id="917a1-171">All three examples produce the same result.</span></span>

```powershell
New-Item -ItemType SymbolicLink -Path C:\Temp -Name MySymLinkDir -Value $pshome
New-Item -ItemType SymbolicLink -Path C:\Temp\MySymLinkDir -Value $pshome
New-Item -ItemType SymbolicLink -Name C:\Temp\MySymLinkDir -Value $pshome
```

### <a name="hard-links"></a><span data-ttu-id="917a1-172">A rögzített hivatkozások</span><span class="sxs-lookup"><span data-stu-id="917a1-172">Hard links</span></span>

<span data-ttu-id="917a1-173">Az azonos kombinációja **elérési** és **neve** engedélyezett a fent leírtak szerint.</span><span class="sxs-lookup"><span data-stu-id="917a1-173">The same combinations of **Path** and **Name** allowed as described above.</span></span>

```powershell
New-Item -ItemType HardLink -Path C:\Temp -Name MyHardLinkFile.txt -Value $pshome\profile.ps1
```

### <a name="directory-junctions"></a><span data-ttu-id="917a1-174">Directory elhelyezni pontokra</span><span class="sxs-lookup"><span data-stu-id="917a1-174">Directory junctions</span></span>

<span data-ttu-id="917a1-175">Az azonos kombinációja **elérési** és **neve** engedélyezett a fent leírtak szerint.</span><span class="sxs-lookup"><span data-stu-id="917a1-175">The same combinations of **Path** and **Name** allowed as described above.</span></span>

```powershell
New-Item -ItemType Junction -Path C:\Temp\MyJunctionDir -Value $pshome
```

### <a name="get-childitem"></a><span data-ttu-id="917a1-176">Get-ChildItem</span><span class="sxs-lookup"><span data-stu-id="917a1-176">Get-ChildItem</span></span>

<span data-ttu-id="917a1-177">`Get-ChildItem` most már jeleníti meg az "l" a **mód** tulajdonság, amely jelzi a szimbolikus hivatkozást fájl vagy könyvtár.</span><span class="sxs-lookup"><span data-stu-id="917a1-177">`Get-ChildItem` now displays an 'l' in the **Mode** property to indicate a symbolic link file or directory.</span></span>

```powershell
Get-ChildItem C:\Temp | sort LastWriteTime -Descending

Directory: C:\Temp

Mode       LastWriteTime Length Name
----       ------------- ------ ----
-a---- 6/13/2014 3:00 PM     16 File.txt
d----- 6/13/2014 3:00 PM        Directory
-a---l 6/13/2014 3:21 PM      0 MySymLinkFile.txt
d----l 6/13/2014 3:22 PM        MySymLinkDir
-a---l 6/13/2014 3:23 PM  23304 MyHardLinkFile.txt
d----l 6/13/2014 3:24 PM        MyJunctionDir
```

### <a name="remove-item"></a><span data-ttu-id="917a1-178">Remove-Item</span><span class="sxs-lookup"><span data-stu-id="917a1-178">Remove-Item</span></span>

<span data-ttu-id="917a1-179">Szimbolikus hivatkozások eltávolítása működik, mint bármely más elemtípus eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="917a1-179">Removing symbolic links works like removing any other item type.</span></span>

```powershell
Remove-Item C:\Temp\MySymLinkFile.txt
Remove-Item C:\Temp\MySymLinkDir
```

<span data-ttu-id="917a1-180">Használja a **kényszerített** paraméter segítségével távolítsa el a fájlokat a céloldali könyvtár és a szimbolikus hivatkozást.</span><span class="sxs-lookup"><span data-stu-id="917a1-180">Use the **Force** parameter to remove the files in the target directory and the symbolic link.</span></span>

```powershell
Remove-Item C:\Temp\MySymLinkDir -Force
```

## <a name="new-temporaryfile"></a><span data-ttu-id="917a1-181">New-TemporaryFile</span><span class="sxs-lookup"><span data-stu-id="917a1-181">New-TemporaryFile</span></span>

<span data-ttu-id="917a1-182">Egyes esetekben a parancsfájlok kell létrehoznia egy ideiglenes fájlt.</span><span class="sxs-lookup"><span data-stu-id="917a1-182">Sometimes in your scripts, you must create a temporary file.</span></span> <span data-ttu-id="917a1-183">Most már teheti ezt meg az `New-TemporaryFile` parancsmagot:</span><span class="sxs-lookup"><span data-stu-id="917a1-183">You can now do this with the `New-TemporaryFile` cmdlet:</span></span>

```powershell
$tempFile = New-TemporaryFile
$tempFile.FullName
```

```Output
C:\Users\user1\AppData\Local\Temp\tmp375.tmp
```

## <a name="network-switch-management-with-powershell"></a><span data-ttu-id="917a1-184">Hálózati kapcsolók kezelése a PowerShell-lel</span><span class="sxs-lookup"><span data-stu-id="917a1-184">Network Switch Management with PowerShell</span></span>

<span data-ttu-id="917a1-185">A hálózati kapcsoló, a WMF 5.0-s-ben bevezetett parancsmagjaival kapcsoló, a virtuális LAN (VLAN) és az alapszintű 2. rétegbeli hálózati kapcsoló port konfigurációja alkalmazhat a Windows Server 2012 R2-emblémával hitelesített hálózati kapcsolók.</span><span class="sxs-lookup"><span data-stu-id="917a1-185">The Network Switch cmdlets, introduced in WMF 5.0, enable you to apply switch, virtual LAN (VLAN), and basic Layer 2 network switch port configuration to Windows Server 2012 R2 logo-certified network switches.</span></span> <span data-ttu-id="917a1-186">Ezek a parancsmagok használatával hajthatja végre:</span><span class="sxs-lookup"><span data-stu-id="917a1-186">Using these cmdlets you can perform:</span></span>

- <span data-ttu-id="917a1-187">Globális váltson konfigurációs, például:</span><span class="sxs-lookup"><span data-stu-id="917a1-187">Global switch configuration, such as:</span></span>
  - <span data-ttu-id="917a1-188">Gazdagép nevének beállítása</span><span class="sxs-lookup"><span data-stu-id="917a1-188">Set host name</span></span>
  - <span data-ttu-id="917a1-189">Set kapcsoló szalagcím</span><span class="sxs-lookup"><span data-stu-id="917a1-189">Set switch banner</span></span>
  - <span data-ttu-id="917a1-190">Konfigurációs megőrzése</span><span class="sxs-lookup"><span data-stu-id="917a1-190">Persist configuration</span></span>
  - <span data-ttu-id="917a1-191">Engedélyezi vagy letiltja a szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="917a1-191">Enable or disable feature</span></span>

- <span data-ttu-id="917a1-192">VLAN-konfiguráció:</span><span class="sxs-lookup"><span data-stu-id="917a1-192">VLAN configuration:</span></span>
  - <span data-ttu-id="917a1-193">Hozzon létre vagy VLAN eltávolítása</span><span class="sxs-lookup"><span data-stu-id="917a1-193">Create or remove VLAN</span></span>
  - <span data-ttu-id="917a1-194">Engedélyezheti vagy tilthatja le a VLAN</span><span class="sxs-lookup"><span data-stu-id="917a1-194">Enable or disable VLAN</span></span>
  - <span data-ttu-id="917a1-195">VLAN számbavétele</span><span class="sxs-lookup"><span data-stu-id="917a1-195">Enumerate VLAN</span></span>
  - <span data-ttu-id="917a1-196">Rövid név beállítása egy VLAN-hoz</span><span class="sxs-lookup"><span data-stu-id="917a1-196">Set friendly name to a VLAN</span></span>

- <span data-ttu-id="917a1-197">2. rétegbeli port konfigurációja:</span><span class="sxs-lookup"><span data-stu-id="917a1-197">Layer 2 port configuration:</span></span>
  - <span data-ttu-id="917a1-198">Portok számbavétele</span><span class="sxs-lookup"><span data-stu-id="917a1-198">Enumerate ports</span></span>
  - <span data-ttu-id="917a1-199">Engedélyezheti vagy tilthatja le a portok</span><span class="sxs-lookup"><span data-stu-id="917a1-199">Enable or disable ports</span></span>
  - <span data-ttu-id="917a1-200">Beállított port módok és tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="917a1-200">Set port modes and properties</span></span>
  - <span data-ttu-id="917a1-201">Adja hozzá, vagy VLAN-Trönk vagy a hozzáférés a porton társítása</span><span class="sxs-lookup"><span data-stu-id="917a1-201">Add or associate VLAN to Trunk or Access on the port</span></span>

<span data-ttu-id="917a1-202">További információkért lásd: a [NetworkSwitchManager](/powershell/module/networkswitchmanager/) dokumentációját.</span><span class="sxs-lookup"><span data-stu-id="917a1-202">For more information, see the [NetworkSwitchManager](/powershell/module/networkswitchmanager/) documentation.</span></span>

## <a name="generate-powershell-cmdlets-based-on-an-odata-endpoint-with-odatautils"></a><span data-ttu-id="917a1-203">Az OData-végpont az ODataUtils alapján PowerShell-parancsmagok létrehozása</span><span class="sxs-lookup"><span data-stu-id="917a1-203">Generate PowerShell cmdlets based on an OData endpoint with ODataUtils</span></span>

<span data-ttu-id="917a1-204">A ODataUtils modul lehetővé teszi, hogy a PowerShell-parancsmagok a REST-végpontokat, amelyek támogatják az OData generációja.</span><span class="sxs-lookup"><span data-stu-id="917a1-204">The ODataUtils module allows generation of PowerShell cmdlets from REST endpoints that support OData.</span></span> <span data-ttu-id="917a1-205">A Microsoft.PowerShell.ODataUtils modul az alábbi szolgáltatásokat tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="917a1-205">The Microsoft.PowerShell.ODataUtils module includes the following features:</span></span>

- <span data-ttu-id="917a1-206">Csatorna ügyféloldali, kiszolgálóoldali végpontról további információt.</span><span class="sxs-lookup"><span data-stu-id="917a1-206">Channel additional information from server-side endpoint to client side.</span></span>
- <span data-ttu-id="917a1-207">Ügyféloldali lapozási támogatása</span><span class="sxs-lookup"><span data-stu-id="917a1-207">Client-side paging support</span></span>
- <span data-ttu-id="917a1-208">Kiszolgálóoldali szűrés használatával a – Select paraméter</span><span class="sxs-lookup"><span data-stu-id="917a1-208">Server-side filtering by using the -Select parameter</span></span>
- <span data-ttu-id="917a1-209">Webalkalmazás-kérelemfejlécek támogatása</span><span class="sxs-lookup"><span data-stu-id="917a1-209">Support for web request headers</span></span>

<span data-ttu-id="917a1-210">A webalkalmazásproxy-parancsmagok által létrehozott a `Export-ODataEndPointProxy` parancsmag a kiszolgálóoldali OData-végpont a kiegészítő információt nyújt a **információk** stream.</span><span class="sxs-lookup"><span data-stu-id="917a1-210">The proxy cmdlets generated by the `Export-ODataEndPointProxy` cmdlet provide additional information from the server-side OData endpoint on the **Information** stream.</span></span>

```powershell
Import-Module Microsoft.PowerShell.ODataUtils -Force
$generatedProxyModuleDir = Join-Path -Path $env:SystemDrive -ChildPath 'ODataDemoProxy'
$uri = "http://services.odata.org/V3/(S(fhleiief23wrm5a5nhf542q5))/OData/OData.svc/"
Export-ODataEndpointProxy -Uri $uri -OutputModule $generatedProxyModuleDir -Force -AllowUnSecureConnection -Verbose -AllowClobber
```

<span data-ttu-id="917a1-211">A következő példában azt termékére beolvasása és a kimenetet a rögzítés a `$infoStream` változó.</span><span class="sxs-lookup"><span data-stu-id="917a1-211">In the following example, we are retrieving top product and capturing the output in the `$infoStream` variable.</span></span>

<span data-ttu-id="917a1-212">Megadásával **IncludeTotalResponseCount** paramétert, a teljes száma az összes lekérjük a **termék** rekordok található a kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="917a1-212">By specifying **IncludeTotalResponseCount** parameter, we get the total count of all the **Product** records available on the server.</span></span>

```powershell
Import-Module $generatedProxyModuleDir -Force
$product = Get-Product -Top 1 -AllowUnsecureConnection -AllowAdditionalData -IncludeTotalResponseCount -InformationVariable infoStream
$additionalInfo = $infoStream.GetEnumerator() | % MessageData
$additionalInfo['odata.count']
```

<span data-ttu-id="917a1-213">A rekordok a kiszolgálóról az ügyféloldali lapozási támogatási használatával kaphat.</span><span class="sxs-lookup"><span data-stu-id="917a1-213">You can get the records from the server in batches using client-side paging support.</span></span> <span data-ttu-id="917a1-214">Ez akkor hasznos, ha be kell szereznie egy nagy mennyiségű adatot a kiszolgálóról a hálózaton keresztül.</span><span class="sxs-lookup"><span data-stu-id="917a1-214">This is useful when you must get a large amount of data from the server over the network.</span></span>

```powershell
$skipCount = 0
$batchSize = 3
while($skipCount -le $additionalInfo['odata.count'])
{
  Get-Product -AllowUnsecureConnection -AllowAdditionalData -Top $batchSize -Skip $skipCount
  $skipCount += $batchSize
}
```

<span data-ttu-id="917a1-215">A létrehozott webalkalmazásproxy-parancsmagok támogatják a **kiválasztása** paraméter csak a rekord tulajdonságokat, amelyeket az ügyfélnek kell fogadni egy szűrőt használt.</span><span class="sxs-lookup"><span data-stu-id="917a1-215">The generated proxy cmdlets support the **Select** parameter that is used as a filter to receive only the record properties that the client needs.</span></span> <span data-ttu-id="917a1-216">A szűrés történik a kiszolgálón, amely csökkenti a hálózaton keresztül továbbított adatok mennyisége.</span><span class="sxs-lookup"><span data-stu-id="917a1-216">The filtering occurs on the server, which reduces the amount of data that is transferred over the network.</span></span>

```powershell
Get-Product -Top 2 -AllowUnsecureConnection -AllowAdditionalData -Select Name
```

<span data-ttu-id="917a1-217">A `Export-ODataEndpointProxy` , valamint az általa létrehozott webalkalmazásproxy-parancsmagok mostantól támogatják a **fejlécek** paraméter.</span><span class="sxs-lookup"><span data-stu-id="917a1-217">The `Export-ODataEndpointProxy` cmdlet, and the proxy cmdlets generated by it, now support the **Headers** parameter.</span></span> <span data-ttu-id="917a1-218">A fejléc a további információt az OData-végpont által várt channel használható.</span><span class="sxs-lookup"><span data-stu-id="917a1-218">The header can be used to channel additional information expected by the OData endpoint.</span></span>

<span data-ttu-id="917a1-219">A következő példában egy előfizetési kulcsot tartalmazó kivonattáblát megadott a **fejlécek** paraméter.</span><span class="sxs-lookup"><span data-stu-id="917a1-219">In the following example, a hash table containing a Subscription key is provided to the **Headers** parameter.</span></span> <span data-ttu-id="917a1-220">Ez a jellemző példa, amely egy előfizetési kulcsot hitelesítéshez sebességhez szolgáltatásokhoz.</span><span class="sxs-lookup"><span data-stu-id="917a1-220">This is a typical example for services that are expecting a Subscription key for authentication.</span></span>

```powershell
Export-ODataEndpointProxy -Uri $endPointUri -OutputModule $generatedProxyModuleDir -Force -AllowUnSecureConnection -Verbose -Headers @{'subscription-key'='XXXX'}
```
