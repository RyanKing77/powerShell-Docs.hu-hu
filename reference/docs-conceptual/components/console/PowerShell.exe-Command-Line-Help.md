---
ms.date: 08/14/2018
keywords: PowerShell, a parancsmag
title: A PowerShell.exe parancssori súgója
ms.assetid: 1ab7b93b-6785-42c6-a1c9-35ff686a958f
ms.openlocfilehash: 0a11ebb11d29adf5853c232b3aa10bc72f92bf0c
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404211"
---
# <a name="powershellexe-command-line-help"></a><span data-ttu-id="a8808-103">PowerShell.exe parancssori súgója</span><span class="sxs-lookup"><span data-stu-id="a8808-103">PowerShell.exe Command-Line Help</span></span>

<span data-ttu-id="a8808-104">Használja a PowerShell.exe egy PowerShell-munkamenet indítása a parancssorból egy másik eszköz, például a Cmd.exe vagy a használata a PowerShell parancssorból egy új munkamenet indításához.</span><span class="sxs-lookup"><span data-stu-id="a8808-104">You can use PowerShell.exe to start a PowerShell session from the command line of another tool, such as Cmd.exe, or use it at the PowerShell command line to start a new session.</span></span> <span data-ttu-id="a8808-105">A paraméterek segítségével testre szabhatja a munkamenetet.</span><span class="sxs-lookup"><span data-stu-id="a8808-105">Use the parameters to customize the session.</span></span>

## <a name="syntax"></a><span data-ttu-id="a8808-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="a8808-106">Syntax</span></span>

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

## <a name="parameters"></a><span data-ttu-id="a8808-107">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="a8808-107">Parameters</span></span>

### <a name="-encodedcommand-base64encodedcommand"></a><span data-ttu-id="a8808-108">-EncodedCommand <Base64EncodedCommand></span><span class="sxs-lookup"><span data-stu-id="a8808-108">-EncodedCommand <Base64EncodedCommand></span></span>

<span data-ttu-id="a8808-109">Egy base-64 kódolású karakterlánc verziója parancsot fogad.</span><span class="sxs-lookup"><span data-stu-id="a8808-109">Accepts a base-64-encoded string version of a command.</span></span> <span data-ttu-id="a8808-110">Ez a paraméter használatával küldje el a PowerShell vagy összetett idézőjelek között, és kapcsos zárójelek parancsokat.</span><span class="sxs-lookup"><span data-stu-id="a8808-110">Use this parameter to submit commands to PowerShell that require complex quotation marks or curly braces.</span></span>

### <a name="-executionpolicy-executionpolicy"></a><span data-ttu-id="a8808-111">-ExecutionPolicy <ExecutionPolicy></span><span class="sxs-lookup"><span data-stu-id="a8808-111">-ExecutionPolicy <ExecutionPolicy></span></span>

<span data-ttu-id="a8808-112">Az alapértelmezett végrehajtási házirend beállítása a jelenlegi munkamenet, és menti azt a $env: PSExecutionPolicyPreference környezeti változót.</span><span class="sxs-lookup"><span data-stu-id="a8808-112">Sets the default execution policy for the current session and saves it in the $env:PSExecutionPolicyPreference environment variable.</span></span> <span data-ttu-id="a8808-113">Ez a paraméter nem módosul a PowerShell végrehajtási házirend, amely van beállítva a beállításjegyzékben.</span><span class="sxs-lookup"><span data-stu-id="a8808-113">This parameter doesn't change the PowerShell execution policy that is set in the registry.</span></span> <span data-ttu-id="a8808-114">További információ a PowerShell végrehajtási házirendek, például az érvényes értékek: [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span><span class="sxs-lookup"><span data-stu-id="a8808-114">For information about PowerShell execution policies, including a list of valid values, see [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span></span>

### <a name="-file-filepath-parameters"></a><span data-ttu-id="a8808-115">-Fájl <FilePath> \[ <Parameters>]</span><span class="sxs-lookup"><span data-stu-id="a8808-115">-File <FilePath> \[<Parameters>]</span></span>

<span data-ttu-id="a8808-116">A megadott parancsfájlt futtatja a helyi hatókörében ("dot forráskódú"), így az a funkciók és a szkript által létrehozott változók érhetők el a jelenlegi munkamenet.</span><span class="sxs-lookup"><span data-stu-id="a8808-116">Runs the specified script in the local scope ("dot-sourced"), so that the functions and variables that the script creates are available in the current session.</span></span> <span data-ttu-id="a8808-117">Adja meg a parancsprogram elérési útja és a paramétereket.</span><span class="sxs-lookup"><span data-stu-id="a8808-117">Enter the script file path and any parameters.</span></span> <span data-ttu-id="a8808-118">**Fájl** kell lennie az utolsó paramétert a parancsba.</span><span class="sxs-lookup"><span data-stu-id="a8808-118">**File** must be the last parameter in the command.</span></span> <span data-ttu-id="a8808-119">Után minden érték a **-fájl** paraméter legyenek értelmezve a szkriptet a szkript elérési útja és a paraméterek átadott.</span><span class="sxs-lookup"><span data-stu-id="a8808-119">All values typed after the **-File** parameter are interpreted as the script file path and parameters passed to that script.</span></span>

<span data-ttu-id="a8808-120">A parancsfájlnak átadott paraméterek után értelmezése az aktuális felületen által átadott szöveges karakterláncként.</span><span class="sxs-lookup"><span data-stu-id="a8808-120">Parameters passed to the script are passed as literal strings, after interpretation by the current shell.</span></span> <span data-ttu-id="a8808-121">Például ha a cmd.exe és a egy környezeti változó értékével továbbítani kívánt használna a cmd.exe szintaxist: `powershell.exe -File .\test.ps1 -TestParam %windir%`</span><span class="sxs-lookup"><span data-stu-id="a8808-121">For example, if you are in cmd.exe and want to pass an environment variable value, you would use the cmd.exe syntax: `powershell.exe -File .\test.ps1 -TestParam %windir%`</span></span>

<span data-ttu-id="a8808-122">Ezzel szemben a futó `powershell.exe -File .\test.ps1 -TestParam $env:windir` cmd.exe eredmények a szkriptben a konstans sztring fogadása `$env:windir` , mert ez nem bír speciális jelentéssel a jelenlegi cmd.exe rendszerhéjba.</span><span class="sxs-lookup"><span data-stu-id="a8808-122">In contrast, running `powershell.exe -File .\test.ps1 -TestParam $env:windir` in cmd.exe results in the script receiving the literal string `$env:windir` because it has no special meaning to the current cmd.exe shell.</span></span>
<span data-ttu-id="a8808-123">A `$env:windir` környezeti változó hivatkozás stílusát _is_ használni egy `-Command` paramétert, mivel a hiba azt fogja értelmezni PowerShell-kódot.</span><span class="sxs-lookup"><span data-stu-id="a8808-123">The `$env:windir` style of environment variable reference _can_ be used inside a `-Command` parameter, since there it will be interpreted as PowerShell code.</span></span>

### <a name="-inputformat-text--xml"></a><span data-ttu-id="a8808-124">\-InputFormat {Text |} XML}</span><span class="sxs-lookup"><span data-stu-id="a8808-124">\-InputFormat {Text | XML}</span></span>

<span data-ttu-id="a8808-125">Ismerteti a PowerShell küldött adatok formátumát.</span><span class="sxs-lookup"><span data-stu-id="a8808-125">Describes the format of data sent to PowerShell.</span></span> <span data-ttu-id="a8808-126">Érvényes értékek: "Text" (szöveges karakterláncok) vagy "XML" (szerializált CLIXML formátumban).</span><span class="sxs-lookup"><span data-stu-id="a8808-126">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-mta"></a><span data-ttu-id="a8808-127">-Mta</span><span class="sxs-lookup"><span data-stu-id="a8808-127">-Mta</span></span>

<span data-ttu-id="a8808-128">A PowerShell használatával egy többszálas apartmanban elindul.</span><span class="sxs-lookup"><span data-stu-id="a8808-128">Starts PowerShell using a multi-threaded apartment.</span></span> <span data-ttu-id="a8808-129">Ez a paraméter PowerShell 3.0-s verziójában jelent meg.</span><span class="sxs-lookup"><span data-stu-id="a8808-129">This parameter is introduced in PowerShell 3.0.</span></span> <span data-ttu-id="a8808-130">A PowerShell 3.0-s egyszálas apartman (STA) az alapértelmezett érték.</span><span class="sxs-lookup"><span data-stu-id="a8808-130">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="a8808-131">A PowerShell 2.0 a többszálas apartmanban az alapértelmezett érték.</span><span class="sxs-lookup"><span data-stu-id="a8808-131">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-noexit"></a><span data-ttu-id="a8808-132">-NoExit</span><span class="sxs-lookup"><span data-stu-id="a8808-132">-NoExit</span></span>

<span data-ttu-id="a8808-133">Nem lépjen ki az indítási parancsok futtatása után.</span><span class="sxs-lookup"><span data-stu-id="a8808-133">Doesn't exit after running startup commands.</span></span>

### <a name="-nologo"></a><span data-ttu-id="a8808-134">-NoLogo</span><span class="sxs-lookup"><span data-stu-id="a8808-134">-NoLogo</span></span>

<span data-ttu-id="a8808-135">A szerzői jogi szalagcím indításkor elrejtése.</span><span class="sxs-lookup"><span data-stu-id="a8808-135">Hides the copyright banner at startup.</span></span>

### <a name="-noninteractive"></a><span data-ttu-id="a8808-136">– Nem interaktív</span><span class="sxs-lookup"><span data-stu-id="a8808-136">-NonInteractive</span></span>

<span data-ttu-id="a8808-137">Egy interaktív kérdés nem jelenik meg a felhasználónak.</span><span class="sxs-lookup"><span data-stu-id="a8808-137">Doesn't present an interactive prompt to the user.</span></span>

### <a name="-noprofile"></a><span data-ttu-id="a8808-138">-NoProfile</span><span class="sxs-lookup"><span data-stu-id="a8808-138">-NoProfile</span></span>

<span data-ttu-id="a8808-139">A PowerShell-profil nem tölthető be.</span><span class="sxs-lookup"><span data-stu-id="a8808-139">Doesn't load the PowerShell profile.</span></span>

### <a name="-outputformat-text--xml"></a><span data-ttu-id="a8808-140">-OutputFormat {Text |} XML}</span><span class="sxs-lookup"><span data-stu-id="a8808-140">-OutputFormat {Text | XML}</span></span>

<span data-ttu-id="a8808-141">Azt határozza meg, hogyan van formázva PowerShell kimenete.</span><span class="sxs-lookup"><span data-stu-id="a8808-141">Determines how output from PowerShell is formatted.</span></span> <span data-ttu-id="a8808-142">Érvényes értékek: "Text" (szöveges karakterláncok) vagy "XML" (szerializált CLIXML formátumban).</span><span class="sxs-lookup"><span data-stu-id="a8808-142">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-psconsolefile-filepath"></a><span data-ttu-id="a8808-143">-PSConsoleFile <FilePath></span><span class="sxs-lookup"><span data-stu-id="a8808-143">-PSConsoleFile <FilePath></span></span>

<span data-ttu-id="a8808-144">A PowerShell-konzolon megadott fájl betöltődik.</span><span class="sxs-lookup"><span data-stu-id="a8808-144">Loads the specified PowerShell console file.</span></span> <span data-ttu-id="a8808-145">Adja meg az elérési út és a konzol fájl nevét.</span><span class="sxs-lookup"><span data-stu-id="a8808-145">Enter the path and name of the console file.</span></span> <span data-ttu-id="a8808-146">Hozzon létre egy konzol fájlt, használja a [ `Export-Console` ](/powershell/module/Microsoft.PowerShell.Core/Export-Console) parancsmagot a PowerShellben.</span><span class="sxs-lookup"><span data-stu-id="a8808-146">To create a console file, use the [`Export-Console`](/powershell/module/Microsoft.PowerShell.Core/Export-Console) cmdlet in PowerShell.</span></span>

### <a name="-sta"></a><span data-ttu-id="a8808-147">-Sta</span><span class="sxs-lookup"><span data-stu-id="a8808-147">-Sta</span></span>

<span data-ttu-id="a8808-148">A PowerShell használatával egy egyszálas apartman elindul.</span><span class="sxs-lookup"><span data-stu-id="a8808-148">Starts PowerShell using a single-threaded apartment.</span></span> <span data-ttu-id="a8808-149">A PowerShell 3.0-s egyszálas apartman (STA) az alapértelmezett érték.</span><span class="sxs-lookup"><span data-stu-id="a8808-149">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="a8808-150">A PowerShell 2.0 a többszálas apartmanban az alapértelmezett érték.</span><span class="sxs-lookup"><span data-stu-id="a8808-150">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-version-powershell-version"></a><span data-ttu-id="a8808-151">-Verzió <PowerShell Version></span><span class="sxs-lookup"><span data-stu-id="a8808-151">-Version <PowerShell Version></span></span>

<span data-ttu-id="a8808-152">A megadott verzióját, a PowerShell elindul.</span><span class="sxs-lookup"><span data-stu-id="a8808-152">Starts the specified version of PowerShell.</span></span> <span data-ttu-id="a8808-153">A rendszer az Ön által megadott verzió kell telepíteni.</span><span class="sxs-lookup"><span data-stu-id="a8808-153">The version that you specify must be installed on the system.</span></span> <span data-ttu-id="a8808-154">Ha a számítógépen telepítve van a PowerShell 3.0, érvényes értékek: "2.0" és "3.0".</span><span class="sxs-lookup"><span data-stu-id="a8808-154">If PowerShell 3.0 is installed on the computer, valid values are "2.0" and "3.0".</span></span> <span data-ttu-id="a8808-155">Az alapértelmezett érték: "3.0-s".</span><span class="sxs-lookup"><span data-stu-id="a8808-155">The default value is "3.0".</span></span>

<span data-ttu-id="a8808-156">Ha a PowerShell 3.0 nincs telepítve, az egyetlen érvényes érték a "2.0-s".</span><span class="sxs-lookup"><span data-stu-id="a8808-156">If PowerShell 3.0 isn't installed, the only valid value is "2.0".</span></span> <span data-ttu-id="a8808-157">Más értéket figyelmen kívül hagyja.</span><span class="sxs-lookup"><span data-stu-id="a8808-157">Other values are ignored.</span></span>

<span data-ttu-id="a8808-158">További információkért lásd: [Windows PowerShell telepítése](../../setup/installing-windows-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a8808-158">For more information, see [Installing Windows PowerShell](../../setup/installing-windows-powershell.md).</span></span>

### <a name="-windowstyle-window-style"></a><span data-ttu-id="a8808-159">-Je hodnota allowstransparency Nastavena <Window style></span><span class="sxs-lookup"><span data-stu-id="a8808-159">-WindowStyle <Window style></span></span>

<span data-ttu-id="a8808-160">A munkamenet a styl okna állítja be.</span><span class="sxs-lookup"><span data-stu-id="a8808-160">Sets the window style for the session.</span></span> <span data-ttu-id="a8808-161">Érvényes értékek: Normal, kis méretű, Maximized és rejtett.</span><span class="sxs-lookup"><span data-stu-id="a8808-161">Valid values are Normal, Minimized, Maximized, and Hidden.</span></span>

### <a name="-command"></a><span data-ttu-id="a8808-162">-Parancs</span><span class="sxs-lookup"><span data-stu-id="a8808-162">-Command</span></span>

<span data-ttu-id="a8808-163">A megadott parancsokat (paraméterek) végrehajtja a, hogy azok lettek írta be a PowerShell-parancssorba.</span><span class="sxs-lookup"><span data-stu-id="a8808-163">Executes the specified commands (with any parameters) as though they were typed at the PowerShell command prompt.</span></span>
<span data-ttu-id="a8808-164">Végrehajtás után a PowerShell kilép, kivéve, ha a **NoExit** paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="a8808-164">After execution, PowerShell exits unless the **NoExit** parameter is specified.</span></span>
<span data-ttu-id="a8808-165">Szöveg után `-Command` a PowerShell érkezik, egy egyetlen parancssori paranccsal futtathatja.</span><span class="sxs-lookup"><span data-stu-id="a8808-165">Any text after `-Command` is sent as a single command line to PowerShell.</span></span>
<span data-ttu-id="a8808-166">Ez eltér attól, hogy miként `-File` kezeli a parancsfájl küldött paramétereket.</span><span class="sxs-lookup"><span data-stu-id="a8808-166">This is different from how `-File` handles parameters sent to a script.</span></span>

<span data-ttu-id="a8808-167">Értékét `-Command` lehet "-", karakterlánc vagy parancsprogram-blokkot.</span><span class="sxs-lookup"><span data-stu-id="a8808-167">The value of `-Command` can be "-", a string, or a script block.</span></span>
<span data-ttu-id="a8808-168">A parancs eredményét, a szülő rendszerhéj mezeje deszerializált XML-objektumok, nem élő objektumokat.</span><span class="sxs-lookup"><span data-stu-id="a8808-168">The results of the command are returned to the parent shell as deserialized XML objects, not live objects.</span></span>

<span data-ttu-id="a8808-169">Ha az értéke `-Command` van "-", a parancs szövege a standard bemenetet olvasható.</span><span class="sxs-lookup"><span data-stu-id="a8808-169">If the value of `-Command` is "-", the command text is read from standard input.</span></span>

<span data-ttu-id="a8808-170">Amikor értékét `-Command` egy karakterlánc **parancs** _kell_ utolsó paramétere helyén megadott bármely karakter beírása után a parancsot, a parancs argumentumainak értelmez miatt lehet.</span><span class="sxs-lookup"><span data-stu-id="a8808-170">When the value of `-Command` is a string, **Command** _must_ be the last parameter specified because any characters typed after the command are interpreted as the command arguments.</span></span>

<span data-ttu-id="a8808-171">A **parancs** paraméter csak fogad végrehajtási parancsprogram-blokkot, amikor felismerhető átadott érték `-Command` ScriptBlock típusként.</span><span class="sxs-lookup"><span data-stu-id="a8808-171">The **Command** parameter only accepts a script block for execution when it can recognize the value passed to `-Command` as a ScriptBlock type.</span></span>
<span data-ttu-id="a8808-172">Ez a _csak_ lehetséges egy másik PowerShell-gazdagépet a PowerShell.exe futtatásakor.</span><span class="sxs-lookup"><span data-stu-id="a8808-172">This is _only_ possible when running PowerShell.exe from another PowerShell host.</span></span>
<span data-ttu-id="a8808-173">A scriptblock kulcsszót, írja be egy meglévő változó, egy kifejezésből visszaadott vagy a PowerShell által elemzett szereplő állomás kapcsos zárójelek közé szövegkonstans parancsprogram-blokkot, `{}`, mielőtt a PowerShell.exe átadott.</span><span class="sxs-lookup"><span data-stu-id="a8808-173">The ScriptBlock type may be contained in an existing variable, returned from an expression, or parsed by the PowerShell host as a literal script block enclosed in curly braces `{}`, before being passed to PowerShell.exe.</span></span>

<span data-ttu-id="a8808-174">A cmd.exe esetében nincs ilyen, mint egy parancsprogram-blokkot (vagy a scriptblock kulcsszót típus), ezért az átadott érték **parancs** fog _mindig_ karakterláncot.</span><span class="sxs-lookup"><span data-stu-id="a8808-174">In cmd.exe, there is no such thing as a script block (or ScriptBlock type), so the value passed to **Command** will _always_ be a string.</span></span>
<span data-ttu-id="a8808-175">Egy parancsfájl-blokkon belül a karakterláncot írhat, de a végrehajtás alatt helyett úgy működik, pontosan, hogy a beírt egy tipikus PowerShell-parancssorba, a parancsfájl tartalmát, a nyomtatási kitiltás vissza is.</span><span class="sxs-lookup"><span data-stu-id="a8808-175">You can write a script block inside the string, but instead of being executed it will behave exactly as though you typed it at a typical PowerShell prompt, printing the contents of the script block back out to you.</span></span>

<span data-ttu-id="a8808-176">Az átadott karakterlánc `-Command` továbbra is hajtják végre, a PowerShell-lel, így a parancsfájl-blokk kapcsos zárójelek gyakran nem szükségesek az elsőként a cmd.exe futtatásakor.</span><span class="sxs-lookup"><span data-stu-id="a8808-176">A string passed to `-Command` will still be executed as PowerShell, so the script block curly braces are often not required in the first place when running from cmd.exe.</span></span>
<span data-ttu-id="a8808-177">Egy karakterláncot, definiált beágyazott parancsprogram-blokkot végrehajtásához a [hívási operátor](/powershell/module/microsoft.powershell.core/about/about_operators#call-operator-) `&` használható:</span><span class="sxs-lookup"><span data-stu-id="a8808-177">To execute an inline script block defined inside a string, the [call operator](/powershell/module/microsoft.powershell.core/about/about_operators#call-operator-) `&` can be used:</span></span>

```console
"& {<command>}"
```

### <a name="-help---"></a><span data-ttu-id="a8808-178">-Help-,?, /?</span><span class="sxs-lookup"><span data-stu-id="a8808-178">-Help, -?, /?</span></span>

<span data-ttu-id="a8808-179">Powershell.exe szintaxisát jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="a8808-179">Shows the syntax of powershell.exe.</span></span> <span data-ttu-id="a8808-180">Ha elkezdi beírni a PowerShell.exe parancsot a PowerShellben, illesztenie a parancs paraméterei a kötőjel (-), nem perjellel (/).</span><span class="sxs-lookup"><span data-stu-id="a8808-180">If you are typing a PowerShell.exe command in PowerShell, prepend the command parameters with a hyphen (-), not a forward slash (/).</span></span> <span data-ttu-id="a8808-181">A Cmd.exe egy kötőjel vagy a perjelet is használható.</span><span class="sxs-lookup"><span data-stu-id="a8808-181">You can use either a hyphen or forward slash in Cmd.exe.</span></span>

> [!NOTE]
> <span data-ttu-id="a8808-182">Hibaelhárítási megjegyzés: A PowerShell 2.0 néhány program, a Windows PowerShell konzol sikertelen kezdve egy LastExitCode, 0xc0000142.</span><span class="sxs-lookup"><span data-stu-id="a8808-182">Troubleshooting Note: In PowerShell 2.0, starting some programs in the Windows PowerShell console fails with a LastExitCode of 0xc0000142.</span></span>

## <a name="examples"></a><span data-ttu-id="a8808-183">PÉLDÁK</span><span class="sxs-lookup"><span data-stu-id="a8808-183">EXAMPLES</span></span>

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
