---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: A PowerShell.exe parancssori súgója
ms.assetid: 1ab7b93b-6785-42c6-a1c9-35ff686a958f
ms.openlocfilehash: 60b6a7e310821a4092b0972b7abbdae0e2d5f738
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="powershellexe-command-line-help"></a><span data-ttu-id="e6e1c-103">PowerShell.exe parancssori súgó</span><span class="sxs-lookup"><span data-stu-id="e6e1c-103">PowerShell.exe Command-Line Help</span></span>

<span data-ttu-id="e6e1c-104">Egy PowerShell-munkamenet indítása egy másik eszköz, például a Cmd.exe, a parancssorban a PowerShell.exe segítségével, vagy használja a PowerShell-parancssorban egy új munkamenet indításához.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-104">You can use PowerShell.exe to start a PowerShell session from the command line of another tool, such as Cmd.exe, or use it at the PowerShell command line to start a new session.</span></span> <span data-ttu-id="e6e1c-105">A paraméterek segítségével testre szabhatja a munkamenet.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-105">Use the parameters to customize the session.</span></span>

## <a name="syntax"></a><span data-ttu-id="e6e1c-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="e6e1c-106">Syntax</span></span>

```syntax
PowerShell[.exe]
       [-Command { - | <script-block> [-args <arg-array>]
                     | <string> [<CommandParameters>] } ]
       [-EncodedCommand <Base64EncodedCommand>]
       [-ExecutionPolicy <ExecutionPolicy>]
       [-File <FilePath> [<Args>]]
       [-InputFormat {Text | XML}]
       [-Mta]
       [-NoExit]
       [-NoLogo]
       [-NonInteractive]
       [-NoProfile]
       [-OutputFormat {Text | XML}]
       [-PSConsoleFile <FilePath> | -Version <PowerShell version>]
       [-Sta]
       [-WindowStyle <style>]

PowerShell[.exe] -Help | -? | /?
```

## <a name="parameters"></a><span data-ttu-id="e6e1c-107">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="e6e1c-107">Parameters</span></span>

### <a name="-encodedcommand-base64encodedcommand"></a><span data-ttu-id="e6e1c-108">-EncodedCommand <Base64EncodedCommand></span><span class="sxs-lookup"><span data-stu-id="e6e1c-108">-EncodedCommand <Base64EncodedCommand></span></span>

<span data-ttu-id="e6e1c-109">Egy parancs egy base-64 kódolású karakterlánc verziója fogad el.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-109">Accepts a base-64-encoded string version of a command.</span></span> <span data-ttu-id="e6e1c-110">Ez a paraméter használatával küldje el a PowerShell vagy a komplex idézőjelek és a kapcsos zárójelek parancsokat.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-110">Use this parameter to submit commands to PowerShell that require complex quotation marks or curly braces.</span></span>

### <a name="-executionpolicy-executionpolicy"></a><span data-ttu-id="e6e1c-111">-ExecutionPolicy <ExecutionPolicy></span><span class="sxs-lookup"><span data-stu-id="e6e1c-111">-ExecutionPolicy <ExecutionPolicy></span></span>

<span data-ttu-id="e6e1c-112">Az alapértelmezett végrehajtási házirend beállítása a jelenlegi munkamenet, és menti a $env: PSExecutionPolicyPreference környezeti változó.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-112">Sets the default execution policy for the current session and saves it in the $env:PSExecutionPolicyPreference environment variable.</span></span> <span data-ttu-id="e6e1c-113">Ez a paraméter nem módosítja a PowerShell végrehajtási házirend, amely a beállításjegyzékben.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-113">This parameter does not change the PowerShell execution policy that is set in the registry.</span></span> <span data-ttu-id="e6e1c-114">PowerShell végrehajtási házirendet, beleértve az érvényes értékek listáját lásd: [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span><span class="sxs-lookup"><span data-stu-id="e6e1c-114">For information about PowerShell execution policies, including a list of valid values, see [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span></span>

### <a name="-file-filepath-parameters"></a><span data-ttu-id="e6e1c-115">-Fájl <FilePath> \[ <Parameters>]</span><span class="sxs-lookup"><span data-stu-id="e6e1c-115">-File <FilePath> \[<Parameters>]</span></span>

<span data-ttu-id="e6e1c-116">A megadott parancsfájlt futtatja a helyi hatókör ("pont-forrása"), hogy a funkciók és a változókat a parancsfájl hoz létre az aktuális munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-116">Runs the specified script in the local scope ("dot-sourced"), so that the functions and variables that the script creates are available in the current session.</span></span> <span data-ttu-id="e6e1c-117">Adja meg a parancsprogram-fájl elérési útját és bármely paraméterét.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-117">Enter the script file path and any parameters.</span></span> <span data-ttu-id="e6e1c-118">**Fájl** kell lennie az utolsó paramétert a parancsba, mert az összes karakter után adta-e a **fájl** paraméter neve, a parancsfájl fájl elérési útját a parancsfájl paramétereit és azok értékét követi értelmezi.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-118">**File** must be the last parameter in the command, because all characters typed after the **File** parameter name are interpreted as the script file path followed by the script parameters and their values.</span></span>

<span data-ttu-id="e6e1c-119">Egy parancsfájlt, és a paraméterértékek, a paraméterek értéke felvehető a **fájl** paraméter.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-119">You can include the parameters of a script, and parameter values, in the value of the **File** parameter.</span></span> <span data-ttu-id="e6e1c-120">Például: `-File .\Get-Script.ps1 -Domain Central` vegye figyelembe, hogy a parancsfájlnak átadott paraméterek át lettek adva a szöveges karakterláncok (után az aktuális rendszerhéj értelmezése).</span><span class="sxs-lookup"><span data-stu-id="e6e1c-120">For example: `-File .\Get-Script.ps1 -Domain Central` Note that parameters passed to the script are passed as literal strings (after interpretation by the current shell).</span></span>
<span data-ttu-id="e6e1c-121">Például, ha a cmd.exe, és hogy egy környezeti változó értékével, használhatja a cmd.exe Szintaxis: `powershell -File .\test.ps1 -Sample %windir%` Ha PowerShell-szintaxis távolítana el, akkor ebben a példában a parancsfájl kapja a szövegkonstans "$env: windir", és nem az adott érték környezeti változó: `powershell -File .\test.ps1 -Sample $env:windir`</span><span class="sxs-lookup"><span data-stu-id="e6e1c-121">For example, if you are in cmd.exe and want to pass an environment variable value, you would use the cmd.exe syntax: `powershell -File .\test.ps1 -Sample %windir%` If you were to use PowerShell syntax, then in this example your script would receive the literal "$env:windir" and not the value of that environmental variable: `powershell -File .\test.ps1 -Sample $env:windir`</span></span>

<span data-ttu-id="e6e1c-122">Általában egy parancsfájl kapcsoló paramétereinek található vagy nincs megadva.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-122">Typically, the switch parameters of a script are either included or omitted.</span></span> <span data-ttu-id="e6e1c-123">Például a következő parancsot használja a **összes** paramétert a Get-Script.ps1 parancsfájl: `-File .\Get-Script.ps1 -All`</span><span class="sxs-lookup"><span data-stu-id="e6e1c-123">For example, the following command uses the **All** parameter of the Get-Script.ps1 script file: `-File .\Get-Script.ps1 -All`</span></span>

### <a name="-inputformat-text--xml"></a><span data-ttu-id="e6e1c-124">\-InputFormat {szöveg |} XML}</span><span class="sxs-lookup"><span data-stu-id="e6e1c-124">\-InputFormat {Text | XML}</span></span>

<span data-ttu-id="e6e1c-125">PowerShell küldött adatok formátumát írja le.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-125">Describes the format of data sent to PowerShell.</span></span> <span data-ttu-id="e6e1c-126">Érvényes értékek: "Text" (karakterlánc) vagy az "XML" (szerializált CLIXML formátumban).</span><span class="sxs-lookup"><span data-stu-id="e6e1c-126">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-mta"></a><span data-ttu-id="e6e1c-127">-Mta</span><span class="sxs-lookup"><span data-stu-id="e6e1c-127">-Mta</span></span>

<span data-ttu-id="e6e1c-128">A PowerShell használatával a többszálas apartmanban kezdődik.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-128">Starts PowerShell using a multi-threaded apartment.</span></span> <span data-ttu-id="e6e1c-129">Ez a paraméter megjelent a PowerShell 3.0.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-129">This parameter is introduced in PowerShell 3.0.</span></span> <span data-ttu-id="e6e1c-130">A PowerShell 3.0 egyszálas apartman (STA) az alapértelmezett beállítás.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-130">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="e6e1c-131">A PowerShell 2.0-s többszálas apartmanban az alapértelmezett beállítás.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-131">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-noexit"></a><span data-ttu-id="e6e1c-132">-NoExit</span><span class="sxs-lookup"><span data-stu-id="e6e1c-132">-NoExit</span></span>

<span data-ttu-id="e6e1c-133">Indítási parancsok futtatása után nem létezik.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-133">Does not exit after running startup commands.</span></span>

### <a name="-nologo"></a><span data-ttu-id="e6e1c-134">-NoLogo</span><span class="sxs-lookup"><span data-stu-id="e6e1c-134">-NoLogo</span></span>

<span data-ttu-id="e6e1c-135">A szerzői jogi információ indításkor elrejti.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-135">Hides the copyright banner at startup.</span></span>

### <a name="-noninteractive"></a><span data-ttu-id="e6e1c-136">-NonInteractive</span><span class="sxs-lookup"><span data-stu-id="e6e1c-136">-NonInteractive</span></span>

<span data-ttu-id="e6e1c-137">Nem jelent-e egy interaktív kérdés jelenik a felhasználó számára.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-137">Does not present an interactive prompt to the user.</span></span>

### <a name="-noprofile"></a><span data-ttu-id="e6e1c-138">-NoProfile</span><span class="sxs-lookup"><span data-stu-id="e6e1c-138">-NoProfile</span></span>

<span data-ttu-id="e6e1c-139">Nem tölt be a PowerShell-profilt.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-139">Does not load the PowerShell profile.</span></span>

### <a name="-outputformat-text--xml"></a><span data-ttu-id="e6e1c-140">-OutputFormat {szöveg |} XML}</span><span class="sxs-lookup"><span data-stu-id="e6e1c-140">-OutputFormat {Text | XML}</span></span>

<span data-ttu-id="e6e1c-141">Meghatározza, hogy PowerShell kimenete formázását.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-141">Determines how output from PowerShell is formatted.</span></span> <span data-ttu-id="e6e1c-142">Érvényes értékek: "Text" (karakterlánc) vagy az "XML" (szerializált CLIXML formátumban).</span><span class="sxs-lookup"><span data-stu-id="e6e1c-142">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-psconsolefile-filepath"></a><span data-ttu-id="e6e1c-143">-PSConsoleFile <FilePath></span><span class="sxs-lookup"><span data-stu-id="e6e1c-143">-PSConsoleFile <FilePath></span></span>

<span data-ttu-id="e6e1c-144">Betölti a megadott PowerShell-konzol fájlt.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-144">Loads the specified PowerShell console file.</span></span> <span data-ttu-id="e6e1c-145">Adja meg az elérési útja és neve a konzol fájlt.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-145">Enter the path and name of the console file.</span></span> <span data-ttu-id="e6e1c-146">A konzol fájl létrehozásához használja a [ `Export-Console` ](/powershell/module/Microsoft.PowerShell.Core/Export-Console) PowerShell parancsmag.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-146">To create a console file, use the [`Export-Console`](/powershell/module/Microsoft.PowerShell.Core/Export-Console) cmdlet in PowerShell.</span></span>

### <a name="-sta"></a><span data-ttu-id="e6e1c-147">-Sta</span><span class="sxs-lookup"><span data-stu-id="e6e1c-147">-Sta</span></span>

<span data-ttu-id="e6e1c-148">Elindítja a PowerShell használatával egyszálas apartman.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-148">Starts PowerShell using a single-threaded apartment.</span></span> <span data-ttu-id="e6e1c-149">A PowerShell 3.0 egyszálas apartman (STA) az alapértelmezett beállítás.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-149">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="e6e1c-150">A PowerShell 2.0-s többszálas apartmanban az alapértelmezett beállítás.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-150">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-version-powershell-version"></a><span data-ttu-id="e6e1c-151">-Verzió <PowerShell Version></span><span class="sxs-lookup"><span data-stu-id="e6e1c-151">-Version <PowerShell Version></span></span>

<span data-ttu-id="e6e1c-152">Elindítja a megadott PowerShell-verzió.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-152">Starts the specified version of PowerShell.</span></span> <span data-ttu-id="e6e1c-153">A megadott verzió telepítenie kell a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-153">The version that you specify must be installed on the system.</span></span> <span data-ttu-id="e6e1c-154">Ha a számítógépen telepítve van a PowerShell 3.0-s, érvényes értékei a "2.0" és "3.0-s".</span><span class="sxs-lookup"><span data-stu-id="e6e1c-154">If PowerShell 3.0 is installed on the computer, valid values are "2.0" and "3.0".</span></span> <span data-ttu-id="e6e1c-155">Az alapértelmezett érték: "3.0-s".</span><span class="sxs-lookup"><span data-stu-id="e6e1c-155">The default value is "3.0".</span></span>

<span data-ttu-id="e6e1c-156">Ha a PowerShell 3.0 nincs telepítve, az egyetlen érvényes érték a "2.0".</span><span class="sxs-lookup"><span data-stu-id="e6e1c-156">If PowerShell 3.0 is not installed, the only valid value is "2.0".</span></span> <span data-ttu-id="e6e1c-157">Egyéb értékek figyelmen kívül lesznek hagyva.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-157">Other values are ignored.</span></span>

<span data-ttu-id="e6e1c-158">További információkért lásd: "[Windows PowerShell telepítése](../../setup/installing-windows-powershell.md)".</span><span class="sxs-lookup"><span data-stu-id="e6e1c-158">For more information, see "[Installing Windows PowerShell](../../setup/installing-windows-powershell.md)".</span></span>

### <a name="-windowstyle-window-style"></a><span data-ttu-id="e6e1c-159">-WindowStyle <Window style></span><span class="sxs-lookup"><span data-stu-id="e6e1c-159">-WindowStyle <Window style></span></span>

<span data-ttu-id="e6e1c-160">A munkamenet beállítja a az ablak stílusát.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-160">Sets the window style for the session.</span></span> <span data-ttu-id="e6e1c-161">Érvényes értékek: a normál, a kisméretű, a teljes méretű és a rejtett.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-161">Valid values are Normal, Minimized, Maximized and Hidden.</span></span>

### <a name="-command"></a><span data-ttu-id="e6e1c-162">-Parancs</span><span class="sxs-lookup"><span data-stu-id="e6e1c-162">-Command</span></span>

<span data-ttu-id="e6e1c-163">Végrehajtja a megadott parancsok (és bármilyen paraméterek), mintha a PowerShell-parancssorba írt volt, és majd kilép, ha a NoExit paraméter nincs megadva.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-163">Executes the specified commands (and any parameters) as though they were typed at the PowerShell command prompt, and then exits, unless the NoExit parameter is specified.</span></span>
<span data-ttu-id="e6e1c-164">Tulajdonképpen bármely szöveg után `-Command` ként legyen elküldve, egyetlen parancssori PowerShell (ez nem azonos a hogyan `-File` kezeli a parancsfájl küldött paramétereket).</span><span class="sxs-lookup"><span data-stu-id="e6e1c-164">Essentially, any text after `-Command` is sent as a single command line to PowerShell (this is different from how `-File` handles parameters sent to a script).</span></span>

<span data-ttu-id="e6e1c-165">A parancs értéke lehet "-", egy karakterláncot.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-165">The value of Command can be "-", a string.</span></span> <span data-ttu-id="e6e1c-166">vagy parancsprogram-blokkot tartalmazzon.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-166">or a script block.</span></span> <span data-ttu-id="e6e1c-167">Ha a parancs értéke "-", a parancs szövege szabványos bemeneti olvasható.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-167">If the value of Command is "-", the command text is read from standard input.</span></span>

<span data-ttu-id="e6e1c-168">Parancsfájl-blokkokban kapcsos zárójelek ({}) kell foglalni.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-168">Script blocks must be enclosed in braces ({}).</span></span> <span data-ttu-id="e6e1c-169">Parancsprogram-blokkot is megadhat, csak ha a PowerShell.exe PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-169">You can specify a script block only when running PowerShell.exe in PowerShell.</span></span> <span data-ttu-id="e6e1c-170">A parancsfájl eredményeinek a szülő rendszerhéj objektumokként deszerializált XML nem élő objektumokat.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-170">The results of the script are returned to the parent shell as deserialized XML objects, not live objects.</span></span>

<span data-ttu-id="e6e1c-171">Ha a parancs értéke egy karakterlánc **parancs** kell lennie az utolsó paramétert a parancsba, mert egyetlen karakter adta-e a parancs argumentumként értelmezi a parancs után.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-171">If the value of Command is a string, **Command** must be the last parameter in the command, because any characters typed after the command are interpreted as the command arguments.</span></span>

<span data-ttu-id="e6e1c-172">Karakterlánc, amely egy PowerShell-parancs futtatása, használja a formátumban:</span><span class="sxs-lookup"><span data-stu-id="e6e1c-172">To write a string that runs a PowerShell command, use the format:</span></span>

```powershell
"& {<command>}"
```

<span data-ttu-id="e6e1c-173">Ha az idézőjelek közötti jelzik, hogy egy karakterláncot, és az invoke operátor (&) hatására végrehajtani a parancsot.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-173">where the quotation marks indicate a string and the invoke operator (&) causes the command to be executed.</span></span>

### <a name="-help---"></a><span data-ttu-id="e6e1c-174">-Súgó-,?, /?</span><span class="sxs-lookup"><span data-stu-id="e6e1c-174">-Help, -?, /?</span></span>

<span data-ttu-id="e6e1c-175">Ezt az üzenetet jelenít meg.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-175">Shows this message.</span></span> <span data-ttu-id="e6e1c-176">Ha a PowerShell.exe parancsot a PowerShell beírt, illesztenie a parancs paraméterei a kötőjel (-), nem perjellel (/).</span><span class="sxs-lookup"><span data-stu-id="e6e1c-176">If you are typing a PowerShell.exe command in PowerShell, prepend the command parameters with a hyphen (-), not a forward slash (/).</span></span> <span data-ttu-id="e6e1c-177">Használhatja a Cmd.exe kötőjel vagy perjel.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-177">You can use either a hyphen or forward slash in Cmd.exe.</span></span>

> [!NOTE]
> <span data-ttu-id="e6e1c-178">Hibaelhárítási Megjegyzés: A PowerShell 2.0-s, néhány programok indítása a Windows PowerShell konzol nem tud egy LastExitCode 0xc0000142 a.</span><span class="sxs-lookup"><span data-stu-id="e6e1c-178">Troubleshooting Note: In PowerShell 2.0, starting some programs in the Windows PowerShell console fails with a LastExitCode of 0xc0000142.</span></span>

## <a name="examples"></a><span data-ttu-id="e6e1c-179">EXAMPLES</span><span class="sxs-lookup"><span data-stu-id="e6e1c-179">EXAMPLES</span></span>

```powershell
# Create a new PowerShell session and load a saved console file
PowerShell -PSConsoleFile sqlsnapin.psc1

# Create a new PowerShell V2 session with text input, XML output, and no logo
PowerShell -Version 2.0 -NoLogo -InputFormat text -OutputFormat XML

# Execute a PowerShell Command in a session
PowerShell -Command "Get-EventLog -LogName security"

# Run a script block in a session
PowerShell -Command {Get-EventLog -LogName security}

# An alternate way to run a command in a new session
PowerShell -Command "& {Get-EventLog -LogName security}"

# To use the -EncodedCommand parameter:
$command = "dir 'c:\program files' "
$bytes = [System.Text.Encoding]::Unicode.GetBytes($command)
$encodedCommand = [Convert]::ToBase64String($bytes)
powershell.exe -encodedCommand $encodedCommand
```