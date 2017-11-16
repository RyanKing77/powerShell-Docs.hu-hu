---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "PowerShell.exe parancssori súgó"
ms.assetid: 1ab7b93b-6785-42c6-a1c9-35ff686a958f
ms.openlocfilehash: 262c21e44e509746314ed44d91bb3de16a4b854b
ms.sourcegitcommit: 4807ab554d55fdee499980835bcc279368b1df68
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/07/2017
---
# <a name="powershellexe-command-line-help"></a><span data-ttu-id="025e4-103">PowerShell.exe parancssori súgó</span><span class="sxs-lookup"><span data-stu-id="025e4-103">PowerShell.exe Command-Line Help</span></span>
<span data-ttu-id="025e4-104">egy Windows PowerShell-munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="025e4-104">a Windows PowerShell session.</span></span> <span data-ttu-id="025e4-105">Egy PowerShell-munkamenet indítása egy másik eszköz, például a Cmd.exe, a parancssorban a PowerShell.exe segítségével, vagy használja a PowerShell-parancssorban egy új munkamenet indításához.</span><span class="sxs-lookup"><span data-stu-id="025e4-105">You can use PowerShell.exe to start a PowerShell session from the command line of another tool, such as Cmd.exe, or use it at the PowerShell command line to start a new session.</span></span> <span data-ttu-id="025e4-106">A paraméterek segítségével testre szabhatja a munkamenet.</span><span class="sxs-lookup"><span data-stu-id="025e4-106">Use the parameters to customize the session.</span></span>

## <a name="syntax"></a><span data-ttu-id="025e4-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="025e4-107">Syntax</span></span>

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

## <a name="parameters"></a><span data-ttu-id="025e4-108">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="025e4-108">Parameters</span></span>

### <a name="-encodedcommand-base64encodedcommand"></a><span data-ttu-id="025e4-109">-EncodedCommand<Base64EncodedCommand></span><span class="sxs-lookup"><span data-stu-id="025e4-109">-EncodedCommand <Base64EncodedCommand></span></span>
<span data-ttu-id="025e4-110">Egy parancs egy base-64 kódolású karakterlánc verziója fogad el.</span><span class="sxs-lookup"><span data-stu-id="025e4-110">Accepts a base-64-encoded string version of a command.</span></span> <span data-ttu-id="025e4-111">Ez a paraméter használatával küldje el a PowerShell vagy a komplex idézőjelek és a kapcsos zárójelek parancsokat.</span><span class="sxs-lookup"><span data-stu-id="025e4-111">Use this parameter to submit commands to PowerShell that require complex quotation marks or curly braces.</span></span>

### <a name="-executionpolicy-executionpolicy"></a><span data-ttu-id="025e4-112">-ExecutionPolicy<ExecutionPolicy></span><span class="sxs-lookup"><span data-stu-id="025e4-112">-ExecutionPolicy <ExecutionPolicy></span></span>
<span data-ttu-id="025e4-113">Az alapértelmezett végrehajtási házirend beállítása a jelenlegi munkamenet, és menti a $env: PSExecutionPolicyPreference környezeti változó.</span><span class="sxs-lookup"><span data-stu-id="025e4-113">Sets the default execution policy for the current session and saves it in the $env:PSExecutionPolicyPreference environment variable.</span></span> <span data-ttu-id="025e4-114">Ez a paraméter nem módosítja a PowerShell végrehajtási házirend, amely a beállításjegyzékben.</span><span class="sxs-lookup"><span data-stu-id="025e4-114">This parameter does not change the PowerShell execution policy that is set in the registry.</span></span> <span data-ttu-id="025e4-115">További információ a PowerShell végrehajtási házirendet, beleértve az érvényes értékek listáját lásd: about_Execution_Policies (http://go.microsoft.com/fwlink/?LinkID=135170).</span><span class="sxs-lookup"><span data-stu-id="025e4-115">For information about PowerShell execution policies, including a list of valid values, see about_Execution_Policies (http://go.microsoft.com/fwlink/?LinkID=135170).</span></span>

### <a name="-file-filepath-parameters"></a><span data-ttu-id="025e4-116">-Fájl <FilePath> \[ <Parameters>]</span><span class="sxs-lookup"><span data-stu-id="025e4-116">-File <FilePath> \[<Parameters>]</span></span>
<span data-ttu-id="025e4-117">A megadott parancsfájlt futtatja a helyi hatókör ("pont-forrása"), hogy a funkciók és a változókat a parancsfájl hoz létre az aktuális munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="025e4-117">Runs the specified script in the local scope ("dot-sourced"), so that the functions and variables that the script creates are available in the current session.</span></span> <span data-ttu-id="025e4-118">Adja meg a parancsprogram-fájl elérési útját és bármely paraméterét.</span><span class="sxs-lookup"><span data-stu-id="025e4-118">Enter the script file path and any parameters.</span></span> <span data-ttu-id="025e4-119">**Fájl** kell lennie az utolsó paramétert a parancsba, mert az összes karakter után adta-e a **fájl** paraméter neve, a parancsfájl fájl elérési útját a parancsfájl paramétereit és azok értékét követi értelmezi.</span><span class="sxs-lookup"><span data-stu-id="025e4-119">**File** must be the last parameter in the command, because all characters typed after the **File** parameter name are interpreted as the script file path followed by the script parameters and their values.</span></span>

<span data-ttu-id="025e4-120">Egy parancsfájlt, és a paraméterértékek, a paraméterek értéke felvehető a **fájl** paraméter.</span><span class="sxs-lookup"><span data-stu-id="025e4-120">You can include the parameters of a script, and parameter values, in the value of the **File** parameter.</span></span> <span data-ttu-id="025e4-121">Például: `-File .\Get-Script.ps1 -Domain Central` vegye figyelembe, hogy a parancsfájlnak átadott paraméterek át lettek adva a szöveges karakterláncok (után az aktuális rendszerhéj értelmezése).</span><span class="sxs-lookup"><span data-stu-id="025e4-121">For example: `-File .\Get-Script.ps1 -Domain Central` Note that parameters passed to the script are passed as literal strings (after interpretation by the current shell).</span></span>
<span data-ttu-id="025e4-122">Például, ha a cmd.exe, és hogy egy környezeti változó értékével, használhatja a cmd.exe Szintaxis: `powershell -File .\test.ps1 -Sample %windir%` Ha PowerShell-szintaxis távolítana el, akkor ebben a példában a parancsfájl kapja a szövegkonstans "$env: windir", és nem az adott érték környezeti változó:`powershell -File .\test.ps1 -Sample $env:windir`</span><span class="sxs-lookup"><span data-stu-id="025e4-122">For example, if you are in cmd.exe and want to pass an environment variable value, you would use the cmd.exe syntax: `powershell -File .\test.ps1 -Sample %windir%` If you were to use PowerShell syntax, then in this example your script would receive the literal "$env:windir" and not the value of that environmental variable: `powershell -File .\test.ps1 -Sample $env:windir`</span></span>

<span data-ttu-id="025e4-123">Általában egy parancsfájl kapcsoló paramétereinek található vagy nincs megadva.</span><span class="sxs-lookup"><span data-stu-id="025e4-123">Typically, the switch parameters of a script are either included or omitted.</span></span> <span data-ttu-id="025e4-124">Például a következő parancsot használja a **összes** paramétert a Get-Script.ps1 parancsfájl:`-File .\Get-Script.ps1 -All`</span><span class="sxs-lookup"><span data-stu-id="025e4-124">For example, the following command uses the **All** parameter of the Get-Script.ps1 script file: `-File .\Get-Script.ps1 -All`</span></span>

### <a name="-inputformat-text--xml"></a><span data-ttu-id="025e4-125">\-InputFormat {szöveg |} XML}</span><span class="sxs-lookup"><span data-stu-id="025e4-125">\-InputFormat {Text | XML}</span></span>
<span data-ttu-id="025e4-126">PowerShell küldött adatok formátumát írja le.</span><span class="sxs-lookup"><span data-stu-id="025e4-126">Describes the format of data sent to PowerShell.</span></span> <span data-ttu-id="025e4-127">Érvényes értékek: "Text" (karakterlánc) vagy az "XML" (szerializált CLIXML formátumban).</span><span class="sxs-lookup"><span data-stu-id="025e4-127">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-mta"></a><span data-ttu-id="025e4-128">-Mta</span><span class="sxs-lookup"><span data-stu-id="025e4-128">-Mta</span></span>
<span data-ttu-id="025e4-129">A PowerShell használatával a többszálas apartmanban kezdődik.</span><span class="sxs-lookup"><span data-stu-id="025e4-129">Starts PowerShell using a multi-threaded apartment.</span></span> <span data-ttu-id="025e4-130">Ez a paraméter megjelent a PowerShell 3.0.</span><span class="sxs-lookup"><span data-stu-id="025e4-130">This parameter is introduced in PowerShell 3.0.</span></span> <span data-ttu-id="025e4-131">A PowerShell 3.0 egyszálas apartman (STA) az alapértelmezett beállítás.</span><span class="sxs-lookup"><span data-stu-id="025e4-131">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="025e4-132">A PowerShell 2.0-s többszálas apartmanban az alapértelmezett beállítás.</span><span class="sxs-lookup"><span data-stu-id="025e4-132">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-noexit"></a><span data-ttu-id="025e4-133">-NoExit</span><span class="sxs-lookup"><span data-stu-id="025e4-133">-NoExit</span></span>
<span data-ttu-id="025e4-134">Indítási parancsok futtatása után nem létezik.</span><span class="sxs-lookup"><span data-stu-id="025e4-134">Does not exit after running startup commands.</span></span>

### <a name="-nologo"></a><span data-ttu-id="025e4-135">-NoLogo</span><span class="sxs-lookup"><span data-stu-id="025e4-135">-NoLogo</span></span>
<span data-ttu-id="025e4-136">A szerzői jogi információ indításkor elrejti.</span><span class="sxs-lookup"><span data-stu-id="025e4-136">Hides the copyright banner at startup.</span></span>

### <a name="-noninteractive"></a><span data-ttu-id="025e4-137">-A nem interaktív</span><span class="sxs-lookup"><span data-stu-id="025e4-137">-NonInteractive</span></span>
<span data-ttu-id="025e4-138">Nem jelent-e egy interaktív kérdés jelenik a felhasználó számára.</span><span class="sxs-lookup"><span data-stu-id="025e4-138">Does not present an interactive prompt to the user.</span></span>

### <a name="-noprofile"></a><span data-ttu-id="025e4-139">-NoProfile</span><span class="sxs-lookup"><span data-stu-id="025e4-139">-NoProfile</span></span>
<span data-ttu-id="025e4-140">Nem tölt be a PowerShell-profilt.</span><span class="sxs-lookup"><span data-stu-id="025e4-140">Does not load the PowerShell profile.</span></span>

### <a name="-outputformat-text--xml"></a><span data-ttu-id="025e4-141">-OutputFormat {szöveg |} XML}</span><span class="sxs-lookup"><span data-stu-id="025e4-141">-OutputFormat {Text | XML}</span></span>
<span data-ttu-id="025e4-142">Meghatározza, hogy PowerShell kimenete formázását.</span><span class="sxs-lookup"><span data-stu-id="025e4-142">Determines how output from PowerShell is formatted.</span></span> <span data-ttu-id="025e4-143">Érvényes értékek: "Text" (karakterlánc) vagy az "XML" (szerializált CLIXML formátumban).</span><span class="sxs-lookup"><span data-stu-id="025e4-143">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-psconsolefile-filepath"></a><span data-ttu-id="025e4-144">-PSConsoleFile<FilePath></span><span class="sxs-lookup"><span data-stu-id="025e4-144">-PSConsoleFile <FilePath></span></span>
<span data-ttu-id="025e4-145">Betölti a megadott PowerShell-konzol fájlt.</span><span class="sxs-lookup"><span data-stu-id="025e4-145">Loads the specified PowerShell console file.</span></span> <span data-ttu-id="025e4-146">Adja meg az elérési útja és neve a konzol fájlt.</span><span class="sxs-lookup"><span data-stu-id="025e4-146">Enter the path and name of the console file.</span></span> <span data-ttu-id="025e4-147">A konzol fájl létrehozásához használja a [Export-konzol](https://technet.microsoft.com/en-us/library/4bab1c02-9e61-4aaf-9957-11d1934ef4ef) PowerShell parancsmag.</span><span class="sxs-lookup"><span data-stu-id="025e4-147">To create a console file, use the [Export-Console](https://technet.microsoft.com/en-us/library/4bab1c02-9e61-4aaf-9957-11d1934ef4ef) cmdlet in PowerShell.</span></span>

### <a name="-sta"></a><span data-ttu-id="025e4-148">-Sta</span><span class="sxs-lookup"><span data-stu-id="025e4-148">-Sta</span></span>
<span data-ttu-id="025e4-149">Elindítja a PowerShell használatával egyszálas apartman.</span><span class="sxs-lookup"><span data-stu-id="025e4-149">Starts PowerShell using a single-threaded apartment.</span></span> <span data-ttu-id="025e4-150">A PowerShell 3.0 egyszálas apartman (STA) az alapértelmezett beállítás.</span><span class="sxs-lookup"><span data-stu-id="025e4-150">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="025e4-151">A PowerShell 2.0-s többszálas apartmanban az alapértelmezett beállítás.</span><span class="sxs-lookup"><span data-stu-id="025e4-151">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-version-powershell-version"></a><span data-ttu-id="025e4-152">-Verzió<PowerShell Version></span><span class="sxs-lookup"><span data-stu-id="025e4-152">-Version <PowerShell Version></span></span>
<span data-ttu-id="025e4-153">Elindítja a megadott PowerShell-verzió.</span><span class="sxs-lookup"><span data-stu-id="025e4-153">Starts the specified version of PowerShell.</span></span> <span data-ttu-id="025e4-154">A megadott verzió telepítenie kell a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="025e4-154">The version that you specify must be installed on the system.</span></span> <span data-ttu-id="025e4-155">Ha a számítógépen telepítve van a PowerShell 3.0-s, érvényes értékei a "2.0" és "3.0-s".</span><span class="sxs-lookup"><span data-stu-id="025e4-155">If PowerShell 3.0 is installed on the computer, valid values are "2.0" and "3.0".</span></span> <span data-ttu-id="025e4-156">Az alapértelmezett érték: "3.0-s".</span><span class="sxs-lookup"><span data-stu-id="025e4-156">The default value is "3.0".</span></span>

<span data-ttu-id="025e4-157">Ha a PowerShell 3.0 nincs telepítve, az egyetlen érvényes érték a "2.0".</span><span class="sxs-lookup"><span data-stu-id="025e4-157">If PowerShell 3.0 is not installed, the only valid value is "2.0".</span></span> <span data-ttu-id="025e4-158">Egyéb értékek figyelmen kívül lesznek hagyva.</span><span class="sxs-lookup"><span data-stu-id="025e4-158">Other values are ignored.</span></span>

<span data-ttu-id="025e4-159">További információkért lásd a "PowerShell telepítése" a [Ismerkedés a PowerShell [régi MSDN]](https://technet.microsoft.com/en-us/library/69555d95-b481-43e1-86e7-b46d68b3e2dd).</span><span class="sxs-lookup"><span data-stu-id="025e4-159">For more information, see "Installing PowerShell" in the [Getting Started with PowerShell [OLD MSDN]](https://technet.microsoft.com/en-us/library/69555d95-b481-43e1-86e7-b46d68b3e2dd).</span></span>

### <a name="-windowstyle-window-style"></a><span data-ttu-id="025e4-160">-WindowStyle<Window style></span><span class="sxs-lookup"><span data-stu-id="025e4-160">-WindowStyle <Window style></span></span>
<span data-ttu-id="025e4-161">A munkamenet beállítja a az ablak stílusát.</span><span class="sxs-lookup"><span data-stu-id="025e4-161">Sets the window style for the session.</span></span> <span data-ttu-id="025e4-162">Érvényes értékek: a normál, a kisméretű, a teljes méretű és a rejtett.</span><span class="sxs-lookup"><span data-stu-id="025e4-162">Valid values are Normal, Minimized, Maximized and Hidden.</span></span>

### <a name="-command"></a><span data-ttu-id="025e4-163">-Parancs</span><span class="sxs-lookup"><span data-stu-id="025e4-163">-Command</span></span>
<span data-ttu-id="025e4-164">Végrehajtja a megadott parancsok (és bármilyen paraméterek), mintha a PowerShell-parancssorba írt volt, és majd kilép, ha a NoExit paraméter nincs megadva.</span><span class="sxs-lookup"><span data-stu-id="025e4-164">Executes the specified commands (and any parameters) as though they were typed at the PowerShell command prompt, and then exits, unless the NoExit parameter is specified.</span></span>
<span data-ttu-id="025e4-165">Tulajdonképpen bármely szöveg után `-Command` ként legyen elküldve, egyetlen parancssori PowerShell (ez nem azonos a hogyan `-File` kezeli a parancsfájl küldött paramétereket).</span><span class="sxs-lookup"><span data-stu-id="025e4-165">Essentially, any text after `-Command` is sent as a single command line to PowerShell (this is different from how `-File` handles parameters sent to a script).</span></span>

<span data-ttu-id="025e4-166">A parancs értéke lehet "-", egy karakterláncot.</span><span class="sxs-lookup"><span data-stu-id="025e4-166">The value of Command can be "-", a string.</span></span> <span data-ttu-id="025e4-167">vagy parancsprogram-blokkot tartalmazzon.</span><span class="sxs-lookup"><span data-stu-id="025e4-167">or a script block.</span></span> <span data-ttu-id="025e4-168">Ha a parancs értéke "-", a parancs szövege szabványos bemeneti olvasható.</span><span class="sxs-lookup"><span data-stu-id="025e4-168">If the value of Command is "-", the command text is read from standard input.</span></span>

<span data-ttu-id="025e4-169">Parancsfájl-blokkokban kapcsos zárójelek ({}) kell foglalni.</span><span class="sxs-lookup"><span data-stu-id="025e4-169">Script blocks must be enclosed in braces ({}).</span></span> <span data-ttu-id="025e4-170">Parancsprogram-blokkot is megadhat, csak ha a PowerShell.exe PowerShell.</span><span class="sxs-lookup"><span data-stu-id="025e4-170">You can specify a script block only when running PowerShell.exe in PowerShell.</span></span> <span data-ttu-id="025e4-171">A parancsfájl eredményeinek a szülő rendszerhéj objektumokként deszerializált XML nem élő objektumokat.</span><span class="sxs-lookup"><span data-stu-id="025e4-171">The results of the script are returned to the parent shell as deserialized XML objects, not live objects.</span></span>

<span data-ttu-id="025e4-172">Ha a parancs értéke egy karakterlánc **parancs** kell lennie az utolsó paramétert a parancsba, mert egyetlen karakter adta-e a parancs argumentumként értelmezi a parancs után.</span><span class="sxs-lookup"><span data-stu-id="025e4-172">If the value of Command is a string, **Command** must be the last parameter in the command, because any characters typed after the command are interpreted as the command arguments.</span></span>

<span data-ttu-id="025e4-173">Karakterlánc, amely egy PowerShell-parancs futtatása, használja a formátumban:</span><span class="sxs-lookup"><span data-stu-id="025e4-173">To write a string that runs a PowerShell command, use the format:</span></span>

```
"& {<command>}"
```

<span data-ttu-id="025e4-174">Ha az idézőjelek közötti jelzik, hogy egy karakterláncot, és az invoke operátor (&) hatására végrehajtani a parancsot.</span><span class="sxs-lookup"><span data-stu-id="025e4-174">where the quotation marks indicate a string and the invoke operator (&) causes the command to be executed.</span></span>

### <a name="-help---"></a><span data-ttu-id="025e4-175">-Súgó-,?, /?</span><span class="sxs-lookup"><span data-stu-id="025e4-175">-Help, -?, /?</span></span>
<span data-ttu-id="025e4-176">Ezt az üzenetet jelenít meg.</span><span class="sxs-lookup"><span data-stu-id="025e4-176">Shows this message.</span></span> <span data-ttu-id="025e4-177">Ha a PowerShell.exe parancsot a PowerShell beírt, illesztenie a parancs paraméterei a kötőjel (-), nem perjellel (/).</span><span class="sxs-lookup"><span data-stu-id="025e4-177">If you are typing a PowerShell.exe command in PowerShell, prepend the command parameters with a hyphen (-), not a forward slash (/).</span></span> <span data-ttu-id="025e4-178">Használhatja a Cmd.exe kötőjel vagy perjel.</span><span class="sxs-lookup"><span data-stu-id="025e4-178">You can use either a hyphen or forward slash in Cmd.exe.</span></span>

> [!NOTE]
> <span data-ttu-id="025e4-179">Hibaelhárítási Megjegyzés: A PowerShell 2.0-s, néhány programok indítása a Windows PowerShell konzol nem tud egy LastExitCode 0xc0000142 a.</span><span class="sxs-lookup"><span data-stu-id="025e4-179">Troubleshooting Note: In PowerShell 2.0, starting some programs in the Windows PowerShell console fails with a LastExitCode of 0xc0000142.</span></span>

## <a name="examples"></a><span data-ttu-id="025e4-180">PÉLDÁK</span><span class="sxs-lookup"><span data-stu-id="025e4-180">EXAMPLES</span></span>

```
# Create a new PowerShell session and load a saved console file
PowerShell -PSConsoleFile sqlsnapin.psc1

# Create a new PowerShell V2 session with text input, XML output, and no logo
PowerShell -Version 2.0 -NoLogo -InputFormat text -OutputFormat XML

# Execute a Powerhell Command in a session
PowerShell -Command "Get-EventLog -LogName security"

# Run a script block in a session
PowerShell -Command {Get-EventLog -LogName security}

# An alternate wayh to run a command in a new session
PowerShell -Command "& {Get-EventLog -LogName security}"

# To use the -EncodedCommand parameter:
$command = "dir 'c:\program files' "
$bytes = [System.Text.Encoding]::Unicode.GetBytes($command)
$encodedCommand = [Convert]::ToBase64String($bytes)
powershell.exe -encodedCommand $encodedCommand
```

