---
title: A PowerShell Core 6.2 újdonságai
description: Új szolgáltatásaival és módosításaival, amely a PowerShell Core 6.2
ms.date: 03/28/2019
ms.openlocfilehash: 6a0da8a410e602ae3963e0bc7bace745317d7d4b
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058097"
---
# <a name="whats-new-in-powershell-core-62"></a><span data-ttu-id="68977-103">A PowerShell Core 6.2 újdonságai</span><span class="sxs-lookup"><span data-stu-id="68977-103">What's New in PowerShell Core 6.2</span></span>

<span data-ttu-id="68977-104">A PowerShell Core 6.2 kiadásban a teljesítménnyel kapcsolatos fejlesztések, a hibajavítások és a kisebb parancsmag és a nyelvi fejlesztések, hogy javíthassunk összpontosít.</span><span class="sxs-lookup"><span data-stu-id="68977-104">The PowerShell Core 6.2 release focused on performance improvements, bug fixes, and smaller cmdlet and language enhancements that improve the quality.</span></span> <span data-ttu-id="68977-105">Fejlesztések a teljes listájának megtekintéséhez, tekintse meg a részletes [changelogs](https://github.com/PowerShell/PowerShell/releases) a Githubon.</span><span class="sxs-lookup"><span data-stu-id="68977-105">To see a full list of improvements, check out our detailed [changelogs](https://github.com/PowerShell/PowerShell/releases) on GitHub.</span></span>

## <a name="experimental-features"></a><span data-ttu-id="68977-106">Kísérleti funkciók</span><span class="sxs-lookup"><span data-stu-id="68977-106">Experimental Features</span></span>

<span data-ttu-id="68977-107">Korábban a támogatása lehetővé tettük [kísérleti funkciók][].</span><span class="sxs-lookup"><span data-stu-id="68977-107">Previously, we enabled support for [Experimental Features][].</span></span> <span data-ttu-id="68977-108">A 6.2-es kiadásban rendelkezünk, négy kísérleti funkciók kipróbálására. Adja meg a visszajelzéseket, így folyamatosan fejlesztjük is, és eldönteni, hogy a funkciót érdemes elősegítő technikai állapotát.</span><span class="sxs-lookup"><span data-stu-id="68977-108">In the 6.2 release, we have four experimental features to try out. Please provide feedback so we can make improvements and to decide whether the feature is worth promoting to mainstream status.</span></span>

<span data-ttu-id="68977-109">Használat `Get-ExperimentalFeature` elérhető kísérleti funkciók listáját.</span><span class="sxs-lookup"><span data-stu-id="68977-109">Use `Get-ExperimentalFeature` to get a list of available experimental features.</span></span> <span data-ttu-id="68977-110">Engedélyezheti vagy letilthatja ezeket a funkciókat `Enable-ExperimentalFeature` és `Disable-ExperimentalFeature`.</span><span class="sxs-lookup"><span data-stu-id="68977-110">You can enable or disable these features with `Enable-ExperimentalFeature` and `Disable-ExperimentalFeature`.</span></span>

### <a name="command-not-found-suggestions"></a><span data-ttu-id="68977-111">A parancs nem található a javaslatok</span><span class="sxs-lookup"><span data-stu-id="68977-111">Command Not Found Suggestions</span></span>

<span data-ttu-id="68977-112">Ez a funkció használatával intelligens megfelelő elírta parancsokat vagy parancsmagjai javaslatok keresése.</span><span class="sxs-lookup"><span data-stu-id="68977-112">This feature uses fuzzy matching to find suggestions for commands or cmdlets you may have mistyped.</span></span>

```powershell
Enable-ExperimentalFeature -Name PSCommandNotFoundSuggestion
```

#### <a name="example"></a><span data-ttu-id="68977-113">Példa</span><span class="sxs-lookup"><span data-stu-id="68977-113">Example</span></span>

<span data-ttu-id="68977-114">Ebben a példában a hibásan írt parancsmag neve intelligens egyezteti több javaslatok nagy valószínűséggel a legkevésbé valószínű.</span><span class="sxs-lookup"><span data-stu-id="68977-114">In this example, the misspelled cmdlet name is fuzzy matched to several suggestions from most likely to least likely.</span></span>

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

### <a name="implicit-remoting-batching"></a><span data-ttu-id="68977-115">Implicit távelérési kötegelés</span><span class="sxs-lookup"><span data-stu-id="68977-115">Implicit Remoting Batching</span></span>

<span data-ttu-id="68977-116">Használata esetén [implicit távelérési](https://devblogs.microsoft.com/scripting/remoting-the-implicit-way/) egy folyamatot, a PowerShell kezeli a folyamatban lévő összes parancs egymástól függetlenül.</span><span class="sxs-lookup"><span data-stu-id="68977-116">When using [implicit remoting](https://devblogs.microsoft.com/scripting/remoting-the-implicit-way/) in a pipeline, PowerShell treats each command in the pipeline independently.</span></span> <span data-ttu-id="68977-117">-Objektumok szerializálva vannak ismételten és `de-serialized` az ügyfél és a folyamat végrehajtása a távoli rendszer között.</span><span class="sxs-lookup"><span data-stu-id="68977-117">Objects are repeatedly serialized and `de-serialized` between the client and remote system over the execution of the pipeline.</span></span>

<span data-ttu-id="68977-118">Ezzel a funkcióval a PowerShell a folyamatot, ha a parancs biztonságosan futtatható-e, és a célrendszeren létezik megállapítja elemzi.</span><span class="sxs-lookup"><span data-stu-id="68977-118">With this feature, PowerShell analyzes the pipeline to determine if the command is safe to run and it exists on the target system.</span></span> <span data-ttu-id="68977-119">TRUE érték esetén a PowerShell távoli végrehajtja a teljes folyamat, és csak szerializálja és `de-serializes` az ügyfél vissza az eredményeket.</span><span class="sxs-lookup"><span data-stu-id="68977-119">When true, PowerShell executes the entire pipeline remotely and only serializes and `de-serializes` the results back to the client.</span></span>

```powershell
Enable-ExperimentalFeature -Name PSImplicitRemotingBatching
```

<span data-ttu-id="68977-120">Egy való életből vett teszt `Get-Process | Sort-Object` localhost keresztül csökkenti a 20-30 10 – 15 másodperc **ezredmásodperc**.</span><span class="sxs-lookup"><span data-stu-id="68977-120">A real-world test of `Get-Process | Sort-Object` over localhost decreases from 10-15 seconds to 20-30 **milliseconds**.</span></span> <span data-ttu-id="68977-121">A funkció csak az ügyfélen engedélyezni kell.</span><span class="sxs-lookup"><span data-stu-id="68977-121">The feature only needs to be enabled on the client.</span></span> <span data-ttu-id="68977-122">Nincs szükség módosításokra a kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="68977-122">No changes are required on the server.</span></span>

### <a name="temp-drive"></a><span data-ttu-id="68977-123">Temp Drive</span><span class="sxs-lookup"><span data-stu-id="68977-123">Temp Drive</span></span>

```powershell
Enable-ExperimentalFeature -Name PSTempDrive
```

<span data-ttu-id="68977-124">Ha a PowerShell Core a különböző operációs rendszert használ, azt ismerheti meg, hogy a környezeti változó lehet megkeresni az ideiglenes könyvtár nem azonos a Windows, macOS és Linux!</span><span class="sxs-lookup"><span data-stu-id="68977-124">If you're using PowerShell Core on different operating systems, you'll discover that the environment variable for finding the temporary directory is different on Windows, macOS, and Linux!</span></span> <span data-ttu-id="68977-125">Ezzel a funkcióval kap egy [PSDrive][] nevű `Temp:` , amely automatikusan az operációs rendszerhez használja az ideiglenes mappában van leképezve.</span><span class="sxs-lookup"><span data-stu-id="68977-125">With this feature, you get a [PSDrive][] called `Temp:` that is automatically mapped to the temporary folder for the operating system you are using.</span></span>

#### <a name="example"></a><span data-ttu-id="68977-126">Példa</span><span class="sxs-lookup"><span data-stu-id="68977-126">Example</span></span>

```powershell
PS> "Hello World!" > Temp:/hello.txt
PS> `Get-Content` Temp:/hello.txt
Hello World!
```

<span data-ttu-id="68977-127">Vegye figyelembe, hogy natív parancsok (például `ls` Linux rendszeren) nem PSDrives tudomást, és nem jelenik meg ez `Temp:` meghajtót.</span><span class="sxs-lookup"><span data-stu-id="68977-127">Be aware that native file commands (like `ls` on Linux) are not aware of PSDrives and won't see this `Temp:` drive.</span></span>

### <a name="abbreviation-expansion"></a><span data-ttu-id="68977-128">Rövidítése bővítése</span><span class="sxs-lookup"><span data-stu-id="68977-128">Abbreviation Expansion</span></span>

<span data-ttu-id="68977-129">PowerShell-parancsmagok várhatóan leíró jellegű szavak.</span><span class="sxs-lookup"><span data-stu-id="68977-129">PowerShell cmdlets are expected to have descriptive nouns.</span></span> <span data-ttu-id="68977-130">Az eredmény, amelyek nehezen írja be a hosszú névvel.</span><span class="sxs-lookup"><span data-stu-id="68977-130">This results in long names that are more difficult to type.</span></span> <span data-ttu-id="68977-131">Ez a funkció lehetővé teszi, hogy csak a parancsmag a nagybetűs karaktereket, és -kiegészítés használata való.</span><span class="sxs-lookup"><span data-stu-id="68977-131">This feature allows you to just type the uppercase characters of the cmdlet and use tab-completion to find a match.</span></span>

```powershell
Enable-ExperimentalFeature -Name PSUseAbbreviationExpansion
```

#### <a name="example"></a><span data-ttu-id="68977-132">Példa</span><span class="sxs-lookup"><span data-stu-id="68977-132">Example</span></span>

```powershell
PS> i-arsavsf
```

<span data-ttu-id="68977-133">Ha eléri a lapon, és rendelkezik az Azure PowerShell [Az](https://www.powershellgallery.com/packages/Az) modul telepítve van, akkor az automatikus kiegészítés:</span><span class="sxs-lookup"><span data-stu-id="68977-133">If you hit tab, and have the Azure PowerShell [Az](https://www.powershellgallery.com/packages/Az) module installed, it will autocomplete to:</span></span>

```Output
PS> Import-AzRecoveryServicesAsrVaultSettingsFile
```

> [!NOTE]
> <span data-ttu-id="68977-134">Ez a funkció célja interaktív módon használható.</span><span class="sxs-lookup"><span data-stu-id="68977-134">This feature is intended to be used interactively.</span></span> <span data-ttu-id="68977-135">Parancsmagok rövidített formáját nem hajtható végre.</span><span class="sxs-lookup"><span data-stu-id="68977-135">Abbreviated forms of cmdlets can't be executed.</span></span>
> <span data-ttu-id="68977-136">Ez a funkció nem helyettesíti a aliasok áll.</span><span class="sxs-lookup"><span data-stu-id="68977-136">This feature is not a replacement for aliases.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="68977-137">Kompatibilitástörő változások</span><span class="sxs-lookup"><span data-stu-id="68977-137">Breaking Changes</span></span>

- <span data-ttu-id="68977-138">Javítsa ki `-NoEnumerate` viselkedés `Write-Output` konzisztens, a Windows PowerShell-lel.</span><span class="sxs-lookup"><span data-stu-id="68977-138">Fix `-NoEnumerate` behavior in `Write-Output` to be consistent with Windows PowerShell.</span></span> <span data-ttu-id="68977-139">(#9069)</span><span class="sxs-lookup"><span data-stu-id="68977-139">(#9069)</span></span>
- <span data-ttu-id="68977-140">Győződjön meg arról, `Join-String -InputObject 1,2,3` eredmény egyenlő `1,2,3 | Join-String` (#8611) eredménye (Köszönjük, hogy @sethvs!)</span><span class="sxs-lookup"><span data-stu-id="68977-140">Make `Join-String -InputObject 1,2,3` result equal to `1,2,3 | Join-String` result (#8611) (Thanks @sethvs!)</span></span>
- <span data-ttu-id="68977-141">Adjon hozzá `-Stable` való `Sort-Object` és a kapcsolódó tesztek (#7862) (Köszönjük, hogy @KirkMunro!)</span><span class="sxs-lookup"><span data-stu-id="68977-141">Add `-Stable` to `Sort-Object` and related tests (#7862) (Thanks @KirkMunro!)</span></span>
- <span data-ttu-id="68977-142">Javítása `Start-Sleep` parancsmagot, hogy fogadja el a másodperc törtrészével megadott (#8537) (Köszönjük, hogy @Prototyyppi!)</span><span class="sxs-lookup"><span data-stu-id="68977-142">Improve `Start-Sleep` cmdlet to accept fractional seconds (#8537) (Thanks @Prototyyppi!)</span></span>
- <span data-ttu-id="68977-143">Kivonattábla OrdinalIgnoreCase használatával kell módosítani `case-insensitive` minden kultúrában (#8566)</span><span class="sxs-lookup"><span data-stu-id="68977-143">Change hashtable to use OrdinalIgnoreCase to be `case-insensitive` in all Cultures (#8566)</span></span>
- <span data-ttu-id="68977-144">Javítsa ki **LiteralPath** a `Import-Csv` kötést létrehozni `Get-ChildItem` (#8277) kimeneti (Köszönjük, hogy @iSazonov!)</span><span class="sxs-lookup"><span data-stu-id="68977-144">Fix **LiteralPath** in `Import-Csv` to bind to `Get-ChildItem` output (#8277) (Thanks @iSazonov!)</span></span>
- <span data-ttu-id="68977-145">Dvojité vozovky elválasztó karakter használata a már nem kihagyja az oszlop neve nélkül `Import-Csv` (#7899) (Köszönjük, hogy @Topping!)</span><span class="sxs-lookup"><span data-stu-id="68977-145">No longer skips a column without name if double quote delimiter is used in `Import-Csv` (#7899) (Thanks @Topping!)</span></span>
- <span data-ttu-id="68977-146">`Get-ExperimentalFeature` már nem rendelkezik `-ListAvailable` váltson (#8318)</span><span class="sxs-lookup"><span data-stu-id="68977-146">`Get-ExperimentalFeature` no longer has `-ListAvailable` switch (#8318)</span></span>
- <span data-ttu-id="68977-147">Hibakeresés most paraméterkészlettel `$DebugPreference` való **Folytatás** helyett **Inquire** (#8195) (Köszönjük, hogy @KirkMunro!)</span><span class="sxs-lookup"><span data-stu-id="68977-147">Debug parameter now sets `$DebugPreference` to **Continue** instead of **Inquire** (#8195) (Thanks @KirkMunro!)</span></span>
- <span data-ttu-id="68977-148">Honor `-OutputFormat` Ha pwsh együttes nem interaktív, átirányított, a kódolt parancsban megadott (#8115)</span><span class="sxs-lookup"><span data-stu-id="68977-148">Honor `-OutputFormat` if specified in non-interactive, redirected, encoded command used with pwsh (#8115)</span></span>
- <span data-ttu-id="68977-149">Szerelvény betölthető modul alapútvonal a GAC betöltése előtt (#8073)</span><span class="sxs-lookup"><span data-stu-id="68977-149">Load assembly from module base path before trying to load from the GAC (#8073)</span></span>
- <span data-ttu-id="68977-150">Linux előzetes csomagok eltávolítása a hullámos vonallal (#8244)</span><span class="sxs-lookup"><span data-stu-id="68977-150">Remove tilde from Linux preview packages (#8244)</span></span>
- <span data-ttu-id="68977-151">Helyezze át a feldolgozást, `-WorkingDirectory` profiljának feldolgozása előtt (#8079)</span><span class="sxs-lookup"><span data-stu-id="68977-151">Move processing of `-WorkingDirectory` before processing of profiles (#8079)</span></span>
- <span data-ttu-id="68977-152">Ne adjon hozzá `PATHEXT` Unix környezeti változóba (#7697) (Köszönjük, hogy @iSazonov!)</span><span class="sxs-lookup"><span data-stu-id="68977-152">Do not add `PATHEXT` environment variable on Unix (#7697) (Thanks @iSazonov!)</span></span>

## <a name="known-issues"></a><span data-ttu-id="68977-153">Ismert problémák</span><span class="sxs-lookup"><span data-stu-id="68977-153">Known Issues</span></span>

- <span data-ttu-id="68977-154">A távelérés Windows IOT ARM platformon modulok betöltése közben probléma lépett rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="68977-154">Remoting on Windows IOT ARM platforms has an issue loading modules.</span></span> <span data-ttu-id="68977-155">See (#8053)</span><span class="sxs-lookup"><span data-stu-id="68977-155">See (#8053)</span></span>

## <a name="general-updates-and-fixes"></a><span data-ttu-id="68977-156">Általános frissítések és javítások</span><span class="sxs-lookup"><span data-stu-id="68977-156">General Updates and Fixes</span></span>

- <span data-ttu-id="68977-157">A fájlok és mappák, a kis-és nagybetűket fájlrendszer kis-és parancssori kiegészítés engedélyezése (#8128)</span><span class="sxs-lookup"><span data-stu-id="68977-157">Enable case-insensitive tab completion for files and folders on case-sensitive filesystem (#8128)</span></span>
- <span data-ttu-id="68977-158">Győződjön meg arról, PSVersionInfo.PSVersion és PSVersionInfo.PSEdition nyilvános (#8054) (Köszönjük, hogy @KirkMunro!)</span><span class="sxs-lookup"><span data-stu-id="68977-158">Make PSVersionInfo.PSVersion and PSVersionInfo.PSEdition public (#8054) (Thanks @KirkMunro!)</span></span>
- <span data-ttu-id="68977-159">Adja hozzá a típus következtetésekhez `$_`  /  `$PSItem` a `catch{ }` blokkol (#8020) (Köszönjük, hogy @vexx32!)</span><span class="sxs-lookup"><span data-stu-id="68977-159">Add Type Inference for `$_` / `$PSItem` in `catch{ }` blocks (#8020) (Thanks @vexx32!)</span></span>
- <span data-ttu-id="68977-160">Javítsa ki a statikus metódus meghívása típus következtetésekhez (#8018) (Köszönjük, hogy @SeeminglyScience!)</span><span class="sxs-lookup"><span data-stu-id="68977-160">Fix static method invocation type inference (#8018) (Thanks @SeeminglyScience!)</span></span>
- <span data-ttu-id="68977-161">Következtetett típusainak létrehozása `Select-Object`, `Group-Object`, **PSObject** és **kivonattábla** (#7231) (Köszönjük, hogy @powercode!)</span><span class="sxs-lookup"><span data-stu-id="68977-161">Create inferred types for `Select-Object`, `Group-Object`, **PSObject** and **Hashtable** (#7231) (Thanks @powercode!)</span></span>
- <span data-ttu-id="68977-162">A hívó módszerének támogatásához `ByRef-like` írja be a paramétereket (#7721)</span><span class="sxs-lookup"><span data-stu-id="68977-162">Support calling method with `ByRef-like` type parameters (#7721)</span></span>
- <span data-ttu-id="68977-163">Az eset, ahol a Windows PowerShell-modul elérési útja már szerepel a környezetben PSModulePath kezelése (#7727)</span><span class="sxs-lookup"><span data-stu-id="68977-163">Handle the case where the Windows PowerShell module path is already in the environment's PSModulePath (#7727)</span></span>
- <span data-ttu-id="68977-164">Engedélyezése `SecureString` parancsmagok a Windows tárolja az egyszerű szöveg (#9199)</span><span class="sxs-lookup"><span data-stu-id="68977-164">Enable `SecureString` cmdlets for non-Windows by storing the plain text (#9199)</span></span>
- <span data-ttu-id="68977-165">Hibaüzenet jelenik meg, nem Windows javíthatja a securestring clixml importálásakor (#7997)</span><span class="sxs-lookup"><span data-stu-id="68977-165">Improve error message on non-Windows when importing clixml with securestring (#7997)</span></span>
- <span data-ttu-id="68977-166">ReplyTo paraméter hozzáadása a `Send-MailMessage` (#8727) (Köszönjük, hogy @replicaJunction!)</span><span class="sxs-lookup"><span data-stu-id="68977-166">Adding parameter ReplyTo to `Send-MailMessage` (#8727) (Thanks @replicaJunction!)</span></span>
- <span data-ttu-id="68977-167">Adja hozzá az elavult üzenetet `Send-MailMessage` (#9178)</span><span class="sxs-lookup"><span data-stu-id="68977-167">Add Obsolete message to `Send-MailMessage` (#9178)</span></span>
- <span data-ttu-id="68977-168">Javítsa ki `Restart-Computer` dolgozhatnak `localhost` amikor a Rendszerfelügyeleti webszolgáltatások nincs jelen (#9160)</span><span class="sxs-lookup"><span data-stu-id="68977-168">Fix `Restart-Computer` to work on `localhost` when WinRM is not present (#9160)</span></span>
- <span data-ttu-id="68977-169">Győződjön meg arról, `Start-Job` throw megszakítást okozó hiba, ha folyamatban van a PowerShell üzemeltetett (#9128)</span><span class="sxs-lookup"><span data-stu-id="68977-169">Make `Start-Job` throw terminating error when PowerShell is being hosted (#9128)</span></span>
- <span data-ttu-id="68977-170">Adjon hozzá C# style típusú gyorsítók és ushort, uint, ulong és rövid literálok utótagok (#7813) (Köszönjük, hogy @vexx32!)</span><span class="sxs-lookup"><span data-stu-id="68977-170">Add C# style type accelerators and suffixes for ushort, uint, ulong, and short literals (#7813) (Thanks @vexx32!)</span></span>
- <span data-ttu-id="68977-171">Tekintse meg a hozzáadott új utótagok numerikus literálok - [about_Numeric_Literals][] (#7901) (Köszönjük, hogy @vexx32!)</span><span class="sxs-lookup"><span data-stu-id="68977-171">Added new suffixes for numeric literals - see [about_Numeric_Literals][] (#7901) (Thanks @vexx32!)</span></span>
- <span data-ttu-id="68977-172">Során Cmdletbinding értéke "true" (#8209), a hatás szintje megfelelően jelentést (Köszönjük, hogy @vexx32!)</span><span class="sxs-lookup"><span data-stu-id="68977-172">Correctly Report impact level when SupportsShouldProcess is not set to 'true' (#8209) (Thanks @vexx32!)</span></span>
- <span data-ttu-id="68977-173">Kérelem karakterkészlet problémák megoldása a weben parancsmagok (#8742) (Köszönjük, hogy @markekraus!)</span><span class="sxs-lookup"><span data-stu-id="68977-173">Fix Request Charset Issues in Web Cmdlets (#8742) (Thanks @markekraus!)</span></span>
- <span data-ttu-id="68977-174">Javítsa ki a várt `100-continue` webes parancsmagokban probléma (#8679) (Köszönjük, hogy @markekraus!)</span><span class="sxs-lookup"><span data-stu-id="68977-174">Fix Expect `100-continue` issue with Web Cmdlets (#8679) (Thanks @markekraus!)</span></span>
- <span data-ttu-id="68977-175">Javítsa ki a fájl blokkoló problémával webes parancsmagokban (#7676) (Köszönjük, hogy @Claustn!)</span><span class="sxs-lookup"><span data-stu-id="68977-175">Fix file blocking issue with web cmdlets (#7676) (Thanks @Claustn!)</span></span>
- <span data-ttu-id="68977-176">Hárítsa el a problémát elemzés znaková stránka `Invoke-RestMethod` (#8694) (Köszönjük, hogy @markekraus!)</span><span class="sxs-lookup"><span data-stu-id="68977-176">Fix code page parsing issue in `Invoke-RestMethod` (#8694) (Thanks @markekraus!)</span></span>
- <span data-ttu-id="68977-177">Refaktorovat `ConvertTo-Json` nyilvános API-ként JsonObject.ConvertToJson elérhetővé (#8682)</span><span class="sxs-lookup"><span data-stu-id="68977-177">Refactor `ConvertTo-Json` to expose JsonObject.ConvertToJson as a public API (#8682)</span></span>
- <span data-ttu-id="68977-178">Adja hozzá a konfigurálható maximális mélység `ConvertFrom-Json` az - mélysége (#8199) (Köszönjük, hogy @louistio!)</span><span class="sxs-lookup"><span data-stu-id="68977-178">Add configurable maximum depth in `ConvertFrom-Json` with -Depth (#8199) (Thanks @louistio!)</span></span>
- <span data-ttu-id="68977-179">Adja hozzá a EscapeHandling paraméter `ConvertTo-Json` parancsmag (#7775) (Köszönjük, hogy @iSazonov!)</span><span class="sxs-lookup"><span data-stu-id="68977-179">Add EscapeHandling parameter in `ConvertTo-Json` cmdlet (#7775) (Thanks @iSazonov!)</span></span>
- <span data-ttu-id="68977-180">Adjon hozzá `-CustomPipeName` pwsh, és `Enter-PSHostProcess` (#8889)</span><span class="sxs-lookup"><span data-stu-id="68977-180">Add `-CustomPipeName` to pwsh and `Enter-PSHostProcess` (#8889)</span></span>
- <span data-ttu-id="68977-181">Engedélyezze a relatív szimbolikus hivatkozások létrehozása a Windows- `New-Item` (#8783)</span><span class="sxs-lookup"><span data-stu-id="68977-181">Enable creating relative symbolic links on Windows with `New-Item` (#8783)</span></span>
- <span data-ttu-id="68977-182">Windows-felhasználók engedélyezése a jogosultságszint-emelés nélkül symlinks létrehozása fejlesztői módban (#8534)</span><span class="sxs-lookup"><span data-stu-id="68977-182">Allow Windows users in developer mode to create symlinks without elevation (#8534)</span></span>
- <span data-ttu-id="68977-183">Engedélyezése `Write-Information` fogadására `$null` (#8774)</span><span class="sxs-lookup"><span data-stu-id="68977-183">Enable `Write-Information` to accept `$null` (#8774)</span></span>
- <span data-ttu-id="68977-184">Javítsa ki `Get-Help` MAML speciális függvények biztosíthatja a tartalmak (#8353)</span><span class="sxs-lookup"><span data-stu-id="68977-184">Fix `Get-Help` for advanced functions with MAML help content (#8353)</span></span>
- <span data-ttu-id="68977-185">Javítsa ki `Get-Help` PSTypeName probléma - paramétert, ha csak egy paramétere van deklarálva (#8754) (Köszönjük, hogy @pougetat!)</span><span class="sxs-lookup"><span data-stu-id="68977-185">Fix `Get-Help` PSTypeName issue with -Parameter when only one parameter is declared (#8754) (Thanks @pougetat!)</span></span>
- <span data-ttu-id="68977-186">Token számítási javítása `Get-Help` ScriptBlock Megjegyzés segítséget hajtja végre.</span><span class="sxs-lookup"><span data-stu-id="68977-186">Token calculation fix for `Get-Help` executed on ScriptBlock for comment help.</span></span> <span data-ttu-id="68977-187">(#8238) (Köszönjük, hogy @hubuk!)</span><span class="sxs-lookup"><span data-stu-id="68977-187">(#8238) (Thanks @hubuk!)</span></span>
- <span data-ttu-id="68977-188">Változás `Get-Help` parancsmag-karakterláncot fogad el, ezért a paraméter paraméter Tárolótömböket (#8454) (Köszönjük, hogy @sethvs!)</span><span class="sxs-lookup"><span data-stu-id="68977-188">Change `Get-Help` cmdlet -Parameter parameter so it accepts string arrays (#8454) (Thanks @sethvs!)</span></span>
- <span data-ttu-id="68977-189">Oldja meg a tárolóhelyek szolgáltatással SZEMÉLYHÍVÓ, ha az elérési útját tartalmazza (#8571) (Köszönjük, hogy @pougetat!)</span><span class="sxs-lookup"><span data-stu-id="68977-189">Resolve PAGER if its path contains spaces (#8571) (Thanks @pougetat!)</span></span>
- <span data-ttu-id="68977-190">Kérdés hozzáadása használatát `less` a függvényben való kilépéssel (#7998) a felhasználó felkérése a "Súgó"</span><span class="sxs-lookup"><span data-stu-id="68977-190">Add prompt to the use of `less` in the function 'help' to instruct user how to quit (#7998)</span></span>
- <span data-ttu-id="68977-191">Adja hozzá a támogatási enum és char típusok a `Format-Hex` parancsmag (#8191) (Köszönjük, hogy @iSazonov!)</span><span class="sxs-lookup"><span data-stu-id="68977-191">Add support enum and char types in `Format-Hex` cmdlet (#8191) (Thanks @iSazonov!)</span></span>
- <span data-ttu-id="68977-192">Távolítsa el a ShouldProcess `Format-Hex` (#8178)</span><span class="sxs-lookup"><span data-stu-id="68977-192">Remove ShouldProcess from `Format-Hex` (#8178)</span></span>
- <span data-ttu-id="68977-193">Az eltolás és a számláló új paraméterek `Format-Hex` és bontani a parancsmag (#7877) (Köszönjük, hogy @iSazonov!)</span><span class="sxs-lookup"><span data-stu-id="68977-193">Add new Offset and Count parameters to `Format-Hex` and refactor the cmdlet (#7877) (Thanks @iSazonov!)</span></span>
- <span data-ttu-id="68977-194">Engedélyezi a "name" alias kulcsként "címke" `ConvertTo-Html`, az egész "width" bejegyzés engedélyezése (#8426) (Köszönjük, hogy @mklement0!)</span><span class="sxs-lookup"><span data-stu-id="68977-194">Allow 'name' as an alias key for 'label' in `ConvertTo-Html`, allow the 'width' entry to be an integer (#8426) (Thanks @mklement0!)</span></span>
- <span data-ttu-id="68977-195">Gyártmány scriptblock kulcsszó alapján számított tulajdonság működik újra `ConvertTo-Html` (#8427) (Köszönjük, hogy @mklement0!)</span><span class="sxs-lookup"><span data-stu-id="68977-195">Make scriptblock based calculated properties work again in `ConvertTo-Html` (#8427) (Thanks @mklement0!)</span></span>
- <span data-ttu-id="68977-196">Adja hozzá a parancsmag `Join-String` szöveg létrehozásához (#7660) bemeneti adatcsatornából (Köszönjük, hogy @powercode!)</span><span class="sxs-lookup"><span data-stu-id="68977-196">Add cmdlet `Join-String` for creating text from pipeline input (#7660) (Thanks @powercode!)</span></span>
- <span data-ttu-id="68977-197">Javítsa ki `Join-String` FormatString paraméter logikai parancsmag (#8449) (Köszönjük, hogy @sethvs!)</span><span class="sxs-lookup"><span data-stu-id="68977-197">Fix `Join-String` cmdlet FormatString parameter logic (#8449) (Thanks @sethvs!)</span></span>
- <span data-ttu-id="68977-198">Változás `Clear-Host` az `$RAWUI` , és törölje a távoli eljáráshívás munkára (#8609)</span><span class="sxs-lookup"><span data-stu-id="68977-198">Change `Clear-Host` back to using `$RAWUI` and clear to work over remoting (#8609)</span></span>
- <span data-ttu-id="68977-199">Változás `Clear-Host` egyszerűen volána `[console]::clear` és egyértelmű alias eltávolítása a Unix (#8603)</span><span class="sxs-lookup"><span data-stu-id="68977-199">Change `Clear-Host` to simply called `[console]::clear` and remove clear alias from Unix (#8603)</span></span>
- <span data-ttu-id="68977-200">Javítsa ki a LiteralPath `Import-Csv` kötést létrehozni `Get-ChildItem` (#8277) kimeneti (Köszönjük, hogy @iSazonov!)</span><span class="sxs-lookup"><span data-stu-id="68977-200">Fix LiteralPath in `Import-Csv` to bind to `Get-ChildItem` output (#8277) (Thanks @iSazonov!)</span></span>
- <span data-ttu-id="68977-201">Súgó funkciót nem szabad használni stránkování AliasHelpInfo (#8552)</span><span class="sxs-lookup"><span data-stu-id="68977-201">help function shouldn't use pager for AliasHelpInfo (#8552)</span></span>
- <span data-ttu-id="68977-202">Adjon hozzá `-UseMinimalHeader` való `Start-Transcript` átiratok fejléc minimalizálása érdekében (#8402) (Köszönjük, hogy @lukexjeremy!)</span><span class="sxs-lookup"><span data-stu-id="68977-202">Add `-UseMinimalHeader` to `Start-Transcript` to minimize transcript header (#8402) (Thanks @lukexjeremy!)</span></span>
- <span data-ttu-id="68977-203">Adjon hozzá `Enable-ExperimentalFeature` és `Disable-ExperimentalFeature` parancsmagok (#8318)</span><span class="sxs-lookup"><span data-stu-id="68977-203">Add `Enable-ExperimentalFeature` and `Disable-ExperimentalFeature` cmdlets (#8318)</span></span>
- <span data-ttu-id="68977-204">Tegye elérhetővé az összes parancsmag **PSDiagnostics** logman.exe esetén érhető el (#8366)</span><span class="sxs-lookup"><span data-stu-id="68977-204">Expose all cmdlets from **PSDiagnostics** if logman.exe is available (#8366)</span></span>
- <span data-ttu-id="68977-205">Távolítsa el **megőrzése** paramétert `New-PSDrive` a `non-Windows` platform (#8291) (Köszönjük, hogy @lukexjeremy!)</span><span class="sxs-lookup"><span data-stu-id="68977-205">Remove **Persist** parameter from `New-PSDrive` on `non-Windows` platform (#8291) (Thanks @lukexjeremy!)</span></span>
- <span data-ttu-id="68977-206">Támogatása `cd +` (#7206) (Köszönjük, hogy @bergmeister!)</span><span class="sxs-lookup"><span data-stu-id="68977-206">Add support for `cd +` (#7206) (Thanks @bergmeister!)</span></span>
- <span data-ttu-id="68977-207">Engedélyezése `Set-Location -LiteralPath` nevű - mappák dolgozhat és + (#8089)</span><span class="sxs-lookup"><span data-stu-id="68977-207">Enable `Set-Location -LiteralPath` to work with folders named - and + (#8089)</span></span>
- <span data-ttu-id="68977-208">`Test-Path` adja vissza `$false` Ha megadott egy üres vagy `$null` elérési útja (#8080) értéket (Köszönjük, hogy @vexx32!)</span><span class="sxs-lookup"><span data-stu-id="68977-208">`Test-Path` returns `$false` when given an empty or `$null` path value (#8080) (Thanks @vexx32!)</span></span>
- <span data-ttu-id="68977-209">Dinamikus paraméterek kell visszaadni, még akkor is, ha az elérési út nem egyezik meg a bármely szolgáltatónál engedélyezése (#7957)</span><span class="sxs-lookup"><span data-stu-id="68977-209">Allow dynamic parameter to be returned even if path does not match any provider (#7957)</span></span>
- <span data-ttu-id="68977-210">Támogatási `Get-PSHostProcessInfo` és `Enter-PSHostProcess` Unix platformokon (#8232)</span><span class="sxs-lookup"><span data-stu-id="68977-210">Support `Get-PSHostProcessInfo` and `Enter-PSHostProcess` on Unix platforms (#8232)</span></span>
- <span data-ttu-id="68977-211">Csökkentse a hozzárendelések `Get-Content` parancsmag (#8103) (Köszönjük, hogy @iSazonov!)</span><span class="sxs-lookup"><span data-stu-id="68977-211">Reduce allocations in `Get-Content` cmdlet (#8103) (Thanks @iSazonov!)</span></span>
- <span data-ttu-id="68977-212">Engedélyezése `Add-Content` olvasási hozzáférés megosztása más eszközökkel tartalom írása közben (#8091)</span><span class="sxs-lookup"><span data-stu-id="68977-212">Enable `Add-Content` to share read access with other tools while writing content (#8091)</span></span>
- <span data-ttu-id="68977-213">`Get/Add-Content` javult a hibajelentések jelez, ha egy tároló célzó (#7823) (Köszönjük, hogy @kvprasoon!)</span><span class="sxs-lookup"><span data-stu-id="68977-213">`Get/Add-Content` throws improved error when targeting a container (#7823) (Thanks @kvprasoon!)</span></span>
- <span data-ttu-id="68977-214">Adjon hozzá `-Name`, `-NoUserOverrides` és `-ListAvailable` paraméterek `Get-Culture` parancsmag (#7702) (Köszönjük, hogy @iSazonov!)</span><span class="sxs-lookup"><span data-stu-id="68977-214">Add `-Name`, `-NoUserOverrides` and `-ListAvailable` parameters to `Get-Culture` cmdlet (#7702) (Thanks @iSazonov!)</span></span>
- <span data-ttu-id="68977-215">Adja hozzá az egységes attribútum befejezésére vonatkozó **kódolás** paraméter.</span><span class="sxs-lookup"><span data-stu-id="68977-215">Add unified attribute for completion for **Encoding** parameter.</span></span> <span data-ttu-id="68977-216">(#7732) (Köszönjük, hogy @ThreeFive-O!)</span><span class="sxs-lookup"><span data-stu-id="68977-216">(#7732) (Thanks @ThreeFive-O!)</span></span>
- <span data-ttu-id="68977-217">Numerikus azonosítók és nevét, a regisztrált kódlapok **kódolás** paraméterek (#7636) (Köszönjük, hogy @iSazonov!)</span><span class="sxs-lookup"><span data-stu-id="68977-217">Allow numeric Ids and name of registered code pages in **Encoding** parameters (#7636) (Thanks @iSazonov!)</span></span>
- <span data-ttu-id="68977-218">Javítsa ki `Rename-Item -Path` a helyettesítő karakter (#7398) (Köszönjük, hogy @kwkam!)</span><span class="sxs-lookup"><span data-stu-id="68977-218">Fix `Rename-Item -Path` with wildcard char (#7398) (Thanks @kwkam!)</span></span>
- <span data-ttu-id="68977-219">Használata esetén `Start-Transcript` és a fájl létezik, nem üres fájl törlésekor (#8131) nál (Köszönjük, hogy @paalbra!)</span><span class="sxs-lookup"><span data-stu-id="68977-219">When using `Start-Transcript` and file exists, empty file rather than deleting (#8131) (Thanks @paalbra!)</span></span>
- <span data-ttu-id="68977-220">Győződjön meg arról, `Add-Type` nyissa meg a forrásfájlokat **FileAccess.Read** és **Funkce** explicit módon (#7915) (Köszönjük, hogy @IISResetMe!)</span><span class="sxs-lookup"><span data-stu-id="68977-220">Make `Add-Type` open source files with **FileAccess.Read** and **FileShare.Read** explicitly (#7915) (Thanks @IISResetMe!)</span></span>
- <span data-ttu-id="68977-221">Javítsa ki `Enter-PSSession -ContainerId` számára a legújabb Windows (#7883)</span><span class="sxs-lookup"><span data-stu-id="68977-221">Fix `Enter-PSSession -ContainerId` for the latest Windows (#7883)</span></span>
- <span data-ttu-id="68977-222">Győződjön meg, hogy **NestedModules** tulajdonság tölti fel a rendszer által `Test-ModuleManifest` (#7859)</span><span class="sxs-lookup"><span data-stu-id="68977-222">Ensure **NestedModules** property gets populated by `Test-ModuleManifest` (#7859)</span></span>
- <span data-ttu-id="68977-223">Adjon hozzá `%F` megkülönbözteti a kis, `Get-Date` - UFormat (#7630) (Köszönjük, hogy @britishben!)</span><span class="sxs-lookup"><span data-stu-id="68977-223">Add `%F` case to `Get-Date` -UFormat (#7630) (Thanks @britishben!)</span></span>
- <span data-ttu-id="68977-224">Javítsa ki `Set-Service -Status Stopped` függőségekkel rendelkező szolgáltatások leállítása (#5525) (Köszönjük, hogy @zhenggu!)</span><span class="sxs-lookup"><span data-stu-id="68977-224">Fix `Set-Service -Status Stopped` to stop services with dependencies (#5525) (Thanks @zhenggu!)</span></span>

<!-- Link references -->
[about_Numeric_Literals]: /powershell/module/Microsoft.PowerShell.Core/About/about_numeric_literals
[Kísérleti funkciók]: /powershell/module/Microsoft.PowerShell.Core/About/about_Experimental_Features
[Experimental Features]: /powershell/module/Microsoft.PowerShell.Core/About/about_Experimental_Features
[PSDrive]: /powershell/module/microsoft.powershell.management/new-psdrive
