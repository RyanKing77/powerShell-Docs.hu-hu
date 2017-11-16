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
# <a name="powershellexe-command-line-help"></a>PowerShell.exe parancssori súgó
egy Windows PowerShell-munkamenetben. Egy PowerShell-munkamenet indítása egy másik eszköz, például a Cmd.exe, a parancssorban a PowerShell.exe segítségével, vagy használja a PowerShell-parancssorban egy új munkamenet indításához. A paraméterek segítségével testre szabhatja a munkamenet.

## <a name="syntax"></a>Szintaxis

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

## <a name="parameters"></a>Paraméterek

### <a name="-encodedcommand-base64encodedcommand"></a>-EncodedCommand<Base64EncodedCommand>
Egy parancs egy base-64 kódolású karakterlánc verziója fogad el. Ez a paraméter használatával küldje el a PowerShell vagy a komplex idézőjelek és a kapcsos zárójelek parancsokat.

### <a name="-executionpolicy-executionpolicy"></a>-ExecutionPolicy<ExecutionPolicy>
Az alapértelmezett végrehajtási házirend beállítása a jelenlegi munkamenet, és menti a $env: PSExecutionPolicyPreference környezeti változó. Ez a paraméter nem módosítja a PowerShell végrehajtási házirend, amely a beállításjegyzékben. További információ a PowerShell végrehajtási házirendet, beleértve az érvényes értékek listáját lásd: about_Execution_Policies (http://go.microsoft.com/fwlink/?LinkID=135170).

### <a name="-file-filepath-parameters"></a>-Fájl <FilePath> \[ <Parameters>]
A megadott parancsfájlt futtatja a helyi hatókör ("pont-forrása"), hogy a funkciók és a változókat a parancsfájl hoz létre az aktuális munkamenetben. Adja meg a parancsprogram-fájl elérési útját és bármely paraméterét. **Fájl** kell lennie az utolsó paramétert a parancsba, mert az összes karakter után adta-e a **fájl** paraméter neve, a parancsfájl fájl elérési útját a parancsfájl paramétereit és azok értékét követi értelmezi.

Egy parancsfájlt, és a paraméterértékek, a paraméterek értéke felvehető a **fájl** paraméter. Például: `-File .\Get-Script.ps1 -Domain Central` vegye figyelembe, hogy a parancsfájlnak átadott paraméterek át lettek adva a szöveges karakterláncok (után az aktuális rendszerhéj értelmezése).
Például, ha a cmd.exe, és hogy egy környezeti változó értékével, használhatja a cmd.exe Szintaxis: `powershell -File .\test.ps1 -Sample %windir%` Ha PowerShell-szintaxis távolítana el, akkor ebben a példában a parancsfájl kapja a szövegkonstans "$env: windir", és nem az adott érték környezeti változó:`powershell -File .\test.ps1 -Sample $env:windir`

Általában egy parancsfájl kapcsoló paramétereinek található vagy nincs megadva. Például a következő parancsot használja a **összes** paramétert a Get-Script.ps1 parancsfájl:`-File .\Get-Script.ps1 -All`

### <a name="-inputformat-text--xml"></a>\-InputFormat {szöveg |} XML}
PowerShell küldött adatok formátumát írja le. Érvényes értékek: "Text" (karakterlánc) vagy az "XML" (szerializált CLIXML formátumban).

### <a name="-mta"></a>-Mta
A PowerShell használatával a többszálas apartmanban kezdődik. Ez a paraméter megjelent a PowerShell 3.0. A PowerShell 3.0 egyszálas apartman (STA) az alapértelmezett beállítás. A PowerShell 2.0-s többszálas apartmanban az alapértelmezett beállítás.

### <a name="-noexit"></a>-NoExit
Indítási parancsok futtatása után nem létezik.

### <a name="-nologo"></a>-NoLogo
A szerzői jogi információ indításkor elrejti.

### <a name="-noninteractive"></a>-A nem interaktív
Nem jelent-e egy interaktív kérdés jelenik a felhasználó számára.

### <a name="-noprofile"></a>-NoProfile
Nem tölt be a PowerShell-profilt.

### <a name="-outputformat-text--xml"></a>-OutputFormat {szöveg |} XML}
Meghatározza, hogy PowerShell kimenete formázását. Érvényes értékek: "Text" (karakterlánc) vagy az "XML" (szerializált CLIXML formátumban).

### <a name="-psconsolefile-filepath"></a>-PSConsoleFile<FilePath>
Betölti a megadott PowerShell-konzol fájlt. Adja meg az elérési útja és neve a konzol fájlt. A konzol fájl létrehozásához használja a [Export-konzol](https://technet.microsoft.com/en-us/library/4bab1c02-9e61-4aaf-9957-11d1934ef4ef) PowerShell parancsmag.

### <a name="-sta"></a>-Sta
Elindítja a PowerShell használatával egyszálas apartman. A PowerShell 3.0 egyszálas apartman (STA) az alapértelmezett beállítás. A PowerShell 2.0-s többszálas apartmanban az alapértelmezett beállítás.

### <a name="-version-powershell-version"></a>-Verzió<PowerShell Version>
Elindítja a megadott PowerShell-verzió. A megadott verzió telepítenie kell a rendszeren. Ha a számítógépen telepítve van a PowerShell 3.0-s, érvényes értékei a "2.0" és "3.0-s". Az alapértelmezett érték: "3.0-s".

Ha a PowerShell 3.0 nincs telepítve, az egyetlen érvényes érték a "2.0". Egyéb értékek figyelmen kívül lesznek hagyva.

További információkért lásd a "PowerShell telepítése" a [Ismerkedés a PowerShell [régi MSDN]](https://technet.microsoft.com/en-us/library/69555d95-b481-43e1-86e7-b46d68b3e2dd).

### <a name="-windowstyle-window-style"></a>-WindowStyle<Window style>
A munkamenet beállítja a az ablak stílusát. Érvényes értékek: a normál, a kisméretű, a teljes méretű és a rejtett.

### <a name="-command"></a>-Parancs
Végrehajtja a megadott parancsok (és bármilyen paraméterek), mintha a PowerShell-parancssorba írt volt, és majd kilép, ha a NoExit paraméter nincs megadva.
Tulajdonképpen bármely szöveg után `-Command` ként legyen elküldve, egyetlen parancssori PowerShell (ez nem azonos a hogyan `-File` kezeli a parancsfájl küldött paramétereket).

A parancs értéke lehet "-", egy karakterláncot. vagy parancsprogram-blokkot tartalmazzon. Ha a parancs értéke "-", a parancs szövege szabványos bemeneti olvasható.

Parancsfájl-blokkokban kapcsos zárójelek ({}) kell foglalni. Parancsprogram-blokkot is megadhat, csak ha a PowerShell.exe PowerShell. A parancsfájl eredményeinek a szülő rendszerhéj objektumokként deszerializált XML nem élő objektumokat.

Ha a parancs értéke egy karakterlánc **parancs** kell lennie az utolsó paramétert a parancsba, mert egyetlen karakter adta-e a parancs argumentumként értelmezi a parancs után.

Karakterlánc, amely egy PowerShell-parancs futtatása, használja a formátumban:

```
"& {<command>}"
```

Ha az idézőjelek közötti jelzik, hogy egy karakterláncot, és az invoke operátor (&) hatására végrehajtani a parancsot.

### <a name="-help---"></a>-Súgó-,?, /?
Ezt az üzenetet jelenít meg. Ha a PowerShell.exe parancsot a PowerShell beírt, illesztenie a parancs paraméterei a kötőjel (-), nem perjellel (/). Használhatja a Cmd.exe kötőjel vagy perjel.

> [!NOTE]
> Hibaelhárítási Megjegyzés: A PowerShell 2.0-s, néhány programok indítása a Windows PowerShell konzol nem tud egy LastExitCode 0xc0000142 a.

## <a name="examples"></a>PÉLDÁK

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

