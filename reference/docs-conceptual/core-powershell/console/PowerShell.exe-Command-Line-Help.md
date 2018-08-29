---
ms.date: 08/14/2018
keywords: PowerShell, a parancsmag
title: A PowerShell.exe parancssori súgója
ms.assetid: 1ab7b93b-6785-42c6-a1c9-35ff686a958f
ms.openlocfilehash: c7f35511e876e8e5189d8a2b949555603d43f731
ms.sourcegitcommit: 56b9be8503a5a1342c0b85b36f5ba6f57c281b63
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/21/2018
ms.locfileid: "43133867"
---
# <a name="powershellexe-command-line-help"></a><span data-ttu-id="ebe91-103">PowerShell.exe parancssori súgója</span><span class="sxs-lookup"><span data-stu-id="ebe91-103">PowerShell.exe Command-Line Help</span></span>

<span data-ttu-id="ebe91-104">Használja a PowerShell.exe egy PowerShell-munkamenet indítása a parancssorból egy másik eszköz, például a Cmd.exe vagy a használata a PowerShell parancssorból egy új munkamenet indításához.</span><span class="sxs-lookup"><span data-stu-id="ebe91-104">You can use PowerShell.exe to start a PowerShell session from the command line of another tool, such as Cmd.exe, or use it at the PowerShell command line to start a new session.</span></span> <span data-ttu-id="ebe91-105">A paraméterek segítségével testre szabhatja a munkamenetet.</span><span class="sxs-lookup"><span data-stu-id="ebe91-105">Use the parameters to customize the session.</span></span>

## <a name="syntax"></a><span data-ttu-id="ebe91-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="ebe91-106">Syntax</span></span>

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

## <a name="parameters"></a><span data-ttu-id="ebe91-107">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="ebe91-107">Parameters</span></span>

### <a name="-encodedcommand-base64encodedcommand"></a><span data-ttu-id="ebe91-108">-EncodedCommand <Base64EncodedCommand></span><span class="sxs-lookup"><span data-stu-id="ebe91-108">-EncodedCommand <Base64EncodedCommand></span></span>

<span data-ttu-id="ebe91-109">Egy base-64 kódolású karakterlánc verziója parancsot fogad.</span><span class="sxs-lookup"><span data-stu-id="ebe91-109">Accepts a base-64-encoded string version of a command.</span></span> <span data-ttu-id="ebe91-110">Ez a paraméter használatával küldje el a PowerShell vagy összetett idézőjelek között, és kapcsos zárójelek parancsokat.</span><span class="sxs-lookup"><span data-stu-id="ebe91-110">Use this parameter to submit commands to PowerShell that require complex quotation marks or curly braces.</span></span>

### <a name="-executionpolicy-executionpolicy"></a><span data-ttu-id="ebe91-111">-ExecutionPolicy <ExecutionPolicy></span><span class="sxs-lookup"><span data-stu-id="ebe91-111">-ExecutionPolicy <ExecutionPolicy></span></span>

<span data-ttu-id="ebe91-112">Az alapértelmezett végrehajtási házirend beállítása a jelenlegi munkamenet, és menti azt a $env: PSExecutionPolicyPreference környezeti változót.</span><span class="sxs-lookup"><span data-stu-id="ebe91-112">Sets the default execution policy for the current session and saves it in the $env:PSExecutionPolicyPreference environment variable.</span></span> <span data-ttu-id="ebe91-113">Ez a paraméter nem módosul a PowerShell végrehajtási házirend, amely van beállítva a beállításjegyzékben.</span><span class="sxs-lookup"><span data-stu-id="ebe91-113">This parameter doesn't change the PowerShell execution policy that is set in the registry.</span></span> <span data-ttu-id="ebe91-114">További információ a PowerShell végrehajtási házirendek, például az érvényes értékek: [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span><span class="sxs-lookup"><span data-stu-id="ebe91-114">For information about PowerShell execution policies, including a list of valid values, see [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span></span>

### <a name="-file-filepath-parameters"></a><span data-ttu-id="ebe91-115">-Fájl <FilePath> \[ <Parameters>]</span><span class="sxs-lookup"><span data-stu-id="ebe91-115">-File <FilePath> \[<Parameters>]</span></span>

<span data-ttu-id="ebe91-116">A megadott parancsfájlt futtatja a helyi hatókörében ("dot forráskódú"), így az a funkciók és a szkript által létrehozott változók érhetők el a jelenlegi munkamenet.</span><span class="sxs-lookup"><span data-stu-id="ebe91-116">Runs the specified script in the local scope ("dot-sourced"), so that the functions and variables that the script creates are available in the current session.</span></span> <span data-ttu-id="ebe91-117">Adja meg a parancsprogram elérési útja és a paramétereket.</span><span class="sxs-lookup"><span data-stu-id="ebe91-117">Enter the script file path and any parameters.</span></span> <span data-ttu-id="ebe91-118">**Fájl** kell lennie az utolsó paramétert a parancsba.</span><span class="sxs-lookup"><span data-stu-id="ebe91-118">**File** must be the last parameter in the command.</span></span> <span data-ttu-id="ebe91-119">Után minden érték a **-fájl** paraméter legyenek értelmezve a szkriptet a szkript elérési útja és a paraméterek átadott.</span><span class="sxs-lookup"><span data-stu-id="ebe91-119">All values typed after the **-File** parameter are interpreted as the script file path and parameters passed to that script.</span></span>

<span data-ttu-id="ebe91-120">A parancsfájlnak átadott paraméterek adhatók be a szövegkonstansok (után értelmezése az aktuális felületen szerint).</span><span class="sxs-lookup"><span data-stu-id="ebe91-120">Parameters passed to the script are passed as literal strings (after interpretation by the current shell).</span></span> <span data-ttu-id="ebe91-121">Például ha a cmd.exe és a egy környezeti változó értékével továbbítani kívánt lenne használhatja a cmd.exe Szintaxis: `powershell -File .\test.ps1 -Sample %windir%` ebben a példában a parancsfájl kap a szövegkonstanst `$env:windir` és nem a környezeti változó értékét: `powershell -File .\test.ps1 -Sample $env:windir`</span><span class="sxs-lookup"><span data-stu-id="ebe91-121">For example, if you are in cmd.exe and want to pass an environment variable value, you would use the cmd.exe syntax: `powershell -File .\test.ps1 -Sample %windir%` In this example, the script receives the literal string `$env:windir` and not the value of that environmental variable: `powershell -File .\test.ps1 -Sample $env:windir`</span></span>

### <a name="-inputformat-text--xml"></a><span data-ttu-id="ebe91-122">\-InputFormat {Text |} XML}</span><span class="sxs-lookup"><span data-stu-id="ebe91-122">\-InputFormat {Text | XML}</span></span>

<span data-ttu-id="ebe91-123">Ismerteti a PowerShell küldött adatok formátumát.</span><span class="sxs-lookup"><span data-stu-id="ebe91-123">Describes the format of data sent to PowerShell.</span></span> <span data-ttu-id="ebe91-124">Érvényes értékek: "Text" (szöveges karakterláncok) vagy "XML" (szerializált CLIXML formátumban).</span><span class="sxs-lookup"><span data-stu-id="ebe91-124">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-mta"></a><span data-ttu-id="ebe91-125">-Mta</span><span class="sxs-lookup"><span data-stu-id="ebe91-125">-Mta</span></span>

<span data-ttu-id="ebe91-126">A PowerShell használatával egy többszálas apartmanban elindul.</span><span class="sxs-lookup"><span data-stu-id="ebe91-126">Starts PowerShell using a multi-threaded apartment.</span></span> <span data-ttu-id="ebe91-127">Ez a paraméter PowerShell 3.0-s verziójában jelent meg.</span><span class="sxs-lookup"><span data-stu-id="ebe91-127">This parameter is introduced in PowerShell 3.0.</span></span> <span data-ttu-id="ebe91-128">A PowerShell 3.0-s egyszálas apartman (STA) az alapértelmezett érték.</span><span class="sxs-lookup"><span data-stu-id="ebe91-128">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="ebe91-129">A PowerShell 2.0 a többszálas apartmanban az alapértelmezett érték.</span><span class="sxs-lookup"><span data-stu-id="ebe91-129">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-noexit"></a><span data-ttu-id="ebe91-130">-NoExit</span><span class="sxs-lookup"><span data-stu-id="ebe91-130">-NoExit</span></span>

<span data-ttu-id="ebe91-131">Nem lépjen ki az indítási parancsok futtatása után.</span><span class="sxs-lookup"><span data-stu-id="ebe91-131">Doesn't exit after running startup commands.</span></span>

### <a name="-nologo"></a><span data-ttu-id="ebe91-132">-NoLogo</span><span class="sxs-lookup"><span data-stu-id="ebe91-132">-NoLogo</span></span>

<span data-ttu-id="ebe91-133">A szerzői jogi szalagcím indításkor elrejtése.</span><span class="sxs-lookup"><span data-stu-id="ebe91-133">Hides the copyright banner at startup.</span></span>

### <a name="-noninteractive"></a><span data-ttu-id="ebe91-134">– Nem interaktív</span><span class="sxs-lookup"><span data-stu-id="ebe91-134">-NonInteractive</span></span>

<span data-ttu-id="ebe91-135">Egy interaktív kérdés nem jelenik meg a felhasználónak.</span><span class="sxs-lookup"><span data-stu-id="ebe91-135">Doesn't present an interactive prompt to the user.</span></span>

### <a name="-noprofile"></a><span data-ttu-id="ebe91-136">-NoProfile</span><span class="sxs-lookup"><span data-stu-id="ebe91-136">-NoProfile</span></span>

<span data-ttu-id="ebe91-137">A PowerShell-profil nem tölthető be.</span><span class="sxs-lookup"><span data-stu-id="ebe91-137">Doesn't load the PowerShell profile.</span></span>

### <a name="-outputformat-text--xml"></a><span data-ttu-id="ebe91-138">-OutputFormat {Text |} XML}</span><span class="sxs-lookup"><span data-stu-id="ebe91-138">-OutputFormat {Text | XML}</span></span>

<span data-ttu-id="ebe91-139">Azt határozza meg, hogyan van formázva PowerShell kimenete.</span><span class="sxs-lookup"><span data-stu-id="ebe91-139">Determines how output from PowerShell is formatted.</span></span> <span data-ttu-id="ebe91-140">Érvényes értékek: "Text" (szöveges karakterláncok) vagy "XML" (szerializált CLIXML formátumban).</span><span class="sxs-lookup"><span data-stu-id="ebe91-140">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-psconsolefile-filepath"></a><span data-ttu-id="ebe91-141">-PSConsoleFile <FilePath></span><span class="sxs-lookup"><span data-stu-id="ebe91-141">-PSConsoleFile <FilePath></span></span>

<span data-ttu-id="ebe91-142">A PowerShell-konzolon megadott fájl betöltődik.</span><span class="sxs-lookup"><span data-stu-id="ebe91-142">Loads the specified PowerShell console file.</span></span> <span data-ttu-id="ebe91-143">Adja meg az elérési út és a konzol fájl nevét.</span><span class="sxs-lookup"><span data-stu-id="ebe91-143">Enter the path and name of the console file.</span></span> <span data-ttu-id="ebe91-144">Hozzon létre egy konzol fájlt, használja a [ `Export-Console` ](/powershell/module/Microsoft.PowerShell.Core/Export-Console) parancsmagot a PowerShellben.</span><span class="sxs-lookup"><span data-stu-id="ebe91-144">To create a console file, use the [`Export-Console`](/powershell/module/Microsoft.PowerShell.Core/Export-Console) cmdlet in PowerShell.</span></span>

### <a name="-sta"></a><span data-ttu-id="ebe91-145">-Sta</span><span class="sxs-lookup"><span data-stu-id="ebe91-145">-Sta</span></span>

<span data-ttu-id="ebe91-146">A PowerShell használatával egy egyszálas apartman elindul.</span><span class="sxs-lookup"><span data-stu-id="ebe91-146">Starts PowerShell using a single-threaded apartment.</span></span> <span data-ttu-id="ebe91-147">A PowerShell 3.0-s egyszálas apartman (STA) az alapértelmezett érték.</span><span class="sxs-lookup"><span data-stu-id="ebe91-147">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="ebe91-148">A PowerShell 2.0 a többszálas apartmanban az alapértelmezett érték.</span><span class="sxs-lookup"><span data-stu-id="ebe91-148">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-version-powershell-version"></a><span data-ttu-id="ebe91-149">-Verzió <PowerShell Version></span><span class="sxs-lookup"><span data-stu-id="ebe91-149">-Version <PowerShell Version></span></span>

<span data-ttu-id="ebe91-150">A megadott verzióját, a PowerShell elindul.</span><span class="sxs-lookup"><span data-stu-id="ebe91-150">Starts the specified version of PowerShell.</span></span> <span data-ttu-id="ebe91-151">A rendszer az Ön által megadott verzió kell telepíteni.</span><span class="sxs-lookup"><span data-stu-id="ebe91-151">The version that you specify must be installed on the system.</span></span> <span data-ttu-id="ebe91-152">Ha a számítógépen telepítve van a PowerShell 3.0, érvényes értékek: "2.0" és "3.0".</span><span class="sxs-lookup"><span data-stu-id="ebe91-152">If PowerShell 3.0 is installed on the computer, valid values are "2.0" and "3.0".</span></span> <span data-ttu-id="ebe91-153">Az alapértelmezett érték: "3.0-s".</span><span class="sxs-lookup"><span data-stu-id="ebe91-153">The default value is "3.0".</span></span>

<span data-ttu-id="ebe91-154">Ha a PowerShell 3.0 nincs telepítve, az egyetlen érvényes érték a "2.0-s".</span><span class="sxs-lookup"><span data-stu-id="ebe91-154">If PowerShell 3.0 isn't installed, the only valid value is "2.0".</span></span> <span data-ttu-id="ebe91-155">Más értéket figyelmen kívül hagyja.</span><span class="sxs-lookup"><span data-stu-id="ebe91-155">Other values are ignored.</span></span>

<span data-ttu-id="ebe91-156">További információkért lásd: [Windows PowerShell telepítése](../../setup/installing-windows-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ebe91-156">For more information, see [Installing Windows PowerShell](../../setup/installing-windows-powershell.md).</span></span>

### <a name="-windowstyle-window-style"></a><span data-ttu-id="ebe91-157">-Je hodnota allowstransparency Nastavena <Window style></span><span class="sxs-lookup"><span data-stu-id="ebe91-157">-WindowStyle <Window style></span></span>

<span data-ttu-id="ebe91-158">A munkamenet a styl okna állítja be.</span><span class="sxs-lookup"><span data-stu-id="ebe91-158">Sets the window style for the session.</span></span> <span data-ttu-id="ebe91-159">Érvényes értékek: Normal, kis méretű, Maximized és rejtett.</span><span class="sxs-lookup"><span data-stu-id="ebe91-159">Valid values are Normal, Minimized, Maximized, and Hidden.</span></span>

### <a name="-command"></a><span data-ttu-id="ebe91-160">-Parancs</span><span class="sxs-lookup"><span data-stu-id="ebe91-160">-Command</span></span>

<span data-ttu-id="ebe91-161">A megadott parancsokat (paraméterek) végrehajtja a, hogy azok lettek írta be a PowerShell-parancssorba.</span><span class="sxs-lookup"><span data-stu-id="ebe91-161">Executes the specified commands (with any parameters) as though they were typed at the PowerShell command prompt.</span></span> <span data-ttu-id="ebe91-162">Végrehajtás után a PowerShell kilép, kivéve, ha a `-NoExit` paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="ebe91-162">After execution, PowerShell exits unless the `-NoExit` parameter is specified.</span></span>
<span data-ttu-id="ebe91-163">Szöveg után `-Command` a PowerShell érkezik, egy egyetlen parancssori paranccsal futtathatja.</span><span class="sxs-lookup"><span data-stu-id="ebe91-163">Any text after `-Command` is sent as a single command line to PowerShell.</span></span> <span data-ttu-id="ebe91-164">Ez eltér attól, hogy miként `-File` kezeli a parancsfájl küldött paramétereket.</span><span class="sxs-lookup"><span data-stu-id="ebe91-164">This is different from how `-File` handles parameters sent to a script.</span></span>

<span data-ttu-id="ebe91-165">A parancs értéke lehet "-", egy karakterláncot.</span><span class="sxs-lookup"><span data-stu-id="ebe91-165">The value of Command can be "-", a string.</span></span> <span data-ttu-id="ebe91-166">vagy parancsprogram-blokkot.</span><span class="sxs-lookup"><span data-stu-id="ebe91-166">or a script block.</span></span> <span data-ttu-id="ebe91-167">Ha a parancs értéke "-", a parancs szövege a standard bemenetet olvasható.</span><span class="sxs-lookup"><span data-stu-id="ebe91-167">If the value of Command is "-", the command text is read from standard input.</span></span>

<span data-ttu-id="ebe91-168">Parancsfájl-blokkokban kapcsos zárójelek közé kell lennie ({}).</span><span class="sxs-lookup"><span data-stu-id="ebe91-168">Script blocks must be enclosed in braces ({}).</span></span> <span data-ttu-id="ebe91-169">Parancsprogram-blokkot is megadhat, csak akkor, ha a PowerShell.exe fut a PowerShellben.</span><span class="sxs-lookup"><span data-stu-id="ebe91-169">You can specify a script block only when running PowerShell.exe in PowerShell.</span></span> <span data-ttu-id="ebe91-170">A parancsfájl eredményét a szülő rendszerhéjba mezeje deszerializált XML-objektumok, nem élő objektumokat.</span><span class="sxs-lookup"><span data-stu-id="ebe91-170">The results of the script are returned to the parent shell as deserialized XML objects, not live objects.</span></span>

<span data-ttu-id="ebe91-171">Ha a parancs értéke egy karakterlánc **parancs** kell lennie az utolsó paramétert a parancsba, bármilyen karakter beírása után a parancsot, a parancs argumentumainak értelmez miatt.</span><span class="sxs-lookup"><span data-stu-id="ebe91-171">If the value of Command is a string, **Command** must be the last parameter in the command, because any characters typed after the command are interpreted as the command arguments.</span></span>

<span data-ttu-id="ebe91-172">Egy karakterláncot egy PowerShell-parancsot futtató ír, formátumot használja:</span><span class="sxs-lookup"><span data-stu-id="ebe91-172">To write a string that runs a PowerShell command, use the format:</span></span>

```powershell
"& {<command>}"
```

<span data-ttu-id="ebe91-173">Az idézőjelek jelzik, hogy egy karakterláncot és az invoke-operátor (&) hatására végrehajtani a parancsot.</span><span class="sxs-lookup"><span data-stu-id="ebe91-173">The quotation marks indicate a string and the invoke operator (&) causes the command to be executed.</span></span>

### <a name="-help---"></a><span data-ttu-id="ebe91-174">-Help-,?, /?</span><span class="sxs-lookup"><span data-stu-id="ebe91-174">-Help, -?, /?</span></span>

<span data-ttu-id="ebe91-175">Powershell.exe szintaxisát jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="ebe91-175">Shows the syntax of powershell.exe.</span></span> <span data-ttu-id="ebe91-176">Ha elkezdi beírni a PowerShell.exe parancsot a PowerShellben, illesztenie a parancs paraméterei a kötőjel (-), nem perjellel (/).</span><span class="sxs-lookup"><span data-stu-id="ebe91-176">If you are typing a PowerShell.exe command in PowerShell, prepend the command parameters with a hyphen (-), not a forward slash (/).</span></span> <span data-ttu-id="ebe91-177">A Cmd.exe egy kötőjel vagy a perjelet is használható.</span><span class="sxs-lookup"><span data-stu-id="ebe91-177">You can use either a hyphen or forward slash in Cmd.exe.</span></span>

> [!NOTE]
> <span data-ttu-id="ebe91-178">Hibaelhárítási Megjegyzés: A PowerShell 2.0, néhány programok indítása a Windows PowerShell konzol sikertelen egy LastExitCode 0xc0000142.</span><span class="sxs-lookup"><span data-stu-id="ebe91-178">Troubleshooting Note: In PowerShell 2.0, starting some programs in the Windows PowerShell console fails with a LastExitCode of 0xc0000142.</span></span>

## <a name="examples"></a><span data-ttu-id="ebe91-179">PÉLDÁK</span><span class="sxs-lookup"><span data-stu-id="ebe91-179">EXAMPLES</span></span>

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
