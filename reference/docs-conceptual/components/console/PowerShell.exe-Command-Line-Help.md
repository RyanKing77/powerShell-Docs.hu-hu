---
ms.date: 08/14/2018
keywords: PowerShell, a parancsmag
title: A PowerShell.exe parancssori súgója
ms.assetid: 1ab7b93b-6785-42c6-a1c9-35ff686a958f
ms.openlocfilehash: 0a11ebb11d29adf5853c232b3aa10bc72f92bf0c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688825"
---
# <a name="powershellexe-command-line-help"></a>PowerShell.exe parancssori súgója

Használja a PowerShell.exe egy PowerShell-munkamenet indítása a parancssorból egy másik eszköz, például a Cmd.exe vagy a használata a PowerShell parancssorból egy új munkamenet indításához. A paraméterek segítségével testre szabhatja a munkamenetet.

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

### <a name="-encodedcommand-base64encodedcommand"></a>-EncodedCommand <Base64EncodedCommand>

Egy base-64 kódolású karakterlánc verziója parancsot fogad. Ez a paraméter használatával küldje el a PowerShell vagy összetett idézőjelek között, és kapcsos zárójelek parancsokat.

### <a name="-executionpolicy-executionpolicy"></a>-ExecutionPolicy <ExecutionPolicy>

Az alapértelmezett végrehajtási házirend beállítása a jelenlegi munkamenet, és menti azt a $env: PSExecutionPolicyPreference környezeti változót. Ez a paraméter nem módosul a PowerShell végrehajtási házirend, amely van beállítva a beállításjegyzékben. További információ a PowerShell végrehajtási házirendek, például az érvényes értékek: [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).

### <a name="-file-filepath-parameters"></a>-Fájl <FilePath> \[ <Parameters>]

A megadott parancsfájlt futtatja a helyi hatókörében ("dot forráskódú"), így az a funkciók és a szkript által létrehozott változók érhetők el a jelenlegi munkamenet. Adja meg a parancsprogram elérési útja és a paramétereket. **Fájl** kell lennie az utolsó paramétert a parancsba. Után minden érték a **-fájl** paraméter legyenek értelmezve a szkriptet a szkript elérési útja és a paraméterek átadott.

A parancsfájlnak átadott paraméterek után értelmezése az aktuális felületen által átadott szöveges karakterláncként. Például ha a cmd.exe és a egy környezeti változó értékével továbbítani kívánt használna a cmd.exe szintaxist: `powershell.exe -File .\test.ps1 -TestParam %windir%`

Ezzel szemben a futó `powershell.exe -File .\test.ps1 -TestParam $env:windir` cmd.exe eredmények a szkriptben a konstans sztring fogadása `$env:windir` , mert ez nem bír speciális jelentéssel a jelenlegi cmd.exe rendszerhéjba.
A `$env:windir` környezeti változó hivatkozás stílusát _is_ használni egy `-Command` paramétert, mivel a hiba azt fogja értelmezni PowerShell-kódot.

### <a name="-inputformat-text--xml"></a>\-InputFormat {Text |} XML}

Ismerteti a PowerShell küldött adatok formátumát. Érvényes értékek: "Text" (szöveges karakterláncok) vagy "XML" (szerializált CLIXML formátumban).

### <a name="-mta"></a>-Mta

A PowerShell használatával egy többszálas apartmanban elindul. Ez a paraméter PowerShell 3.0-s verziójában jelent meg. A PowerShell 3.0-s egyszálas apartman (STA) az alapértelmezett érték. A PowerShell 2.0 a többszálas apartmanban az alapértelmezett érték.

### <a name="-noexit"></a>-NoExit

Nem lépjen ki az indítási parancsok futtatása után.

### <a name="-nologo"></a>-NoLogo

A szerzői jogi szalagcím indításkor elrejtése.

### <a name="-noninteractive"></a>-NonInteractive

Egy interaktív kérdés nem jelenik meg a felhasználónak.

### <a name="-noprofile"></a>-NoProfile

A PowerShell-profil nem tölthető be.

### <a name="-outputformat-text--xml"></a>-OutputFormat {Text |} XML}

Azt határozza meg, hogyan van formázva PowerShell kimenete. Érvényes értékek: "Text" (szöveges karakterláncok) vagy "XML" (szerializált CLIXML formátumban).

### <a name="-psconsolefile-filepath"></a>-PSConsoleFile <FilePath>

A PowerShell-konzolon megadott fájl betöltődik. Adja meg az elérési út és a konzol fájl nevét. Hozzon létre egy konzol fájlt, használja a [ `Export-Console` ](/powershell/module/Microsoft.PowerShell.Core/Export-Console) parancsmagot a PowerShellben.

### <a name="-sta"></a>-Sta

A PowerShell használatával egy egyszálas apartman elindul. A PowerShell 3.0-s egyszálas apartman (STA) az alapértelmezett érték. A PowerShell 2.0 a többszálas apartmanban az alapértelmezett érték.

### <a name="-version-powershell-version"></a>-Verzió <PowerShell Version>

A megadott verzióját, a PowerShell elindul. A rendszer az Ön által megadott verzió kell telepíteni. Ha a számítógépen telepítve van a PowerShell 3.0, érvényes értékek: "2.0" és "3.0". Az alapértelmezett érték: "3.0-s".

Ha a PowerShell 3.0 nincs telepítve, az egyetlen érvényes érték a "2.0-s". Más értéket figyelmen kívül hagyja.

További információkért lásd: [Windows PowerShell telepítése](../../setup/installing-windows-powershell.md).

### <a name="-windowstyle-window-style"></a>-Je hodnota allowstransparency Nastavena <Window style>

A munkamenet a styl okna állítja be. Érvényes értékek: Normal, kis méretű, Maximized és rejtett.

### <a name="-command"></a>-Parancs

A megadott parancsokat (paraméterek) végrehajtja a, hogy azok lettek írta be a PowerShell-parancssorba.
Végrehajtás után a PowerShell kilép, kivéve, ha a **NoExit** paraméter meg van adva.
Szöveg után `-Command` a PowerShell érkezik, egy egyetlen parancssori paranccsal futtathatja.
Ez eltér attól, hogy miként `-File` kezeli a parancsfájl küldött paramétereket.

Értékét `-Command` lehet "-", karakterlánc vagy parancsprogram-blokkot.
A parancs eredményét, a szülő rendszerhéj mezeje deszerializált XML-objektumok, nem élő objektumokat.

Ha az értéke `-Command` van "-", a parancs szövege a standard bemenetet olvasható.

Amikor értékét `-Command` egy karakterlánc **parancs** _kell_ utolsó paramétere helyén megadott bármely karakter beírása után a parancsot, a parancs argumentumainak értelmez miatt lehet.

A **parancs** paraméter csak fogad végrehajtási parancsprogram-blokkot, amikor felismerhető átadott érték `-Command` ScriptBlock típusként.
Ez a _csak_ lehetséges egy másik PowerShell-gazdagépet a PowerShell.exe futtatásakor.
A scriptblock kulcsszót, írja be egy meglévő változó, egy kifejezésből visszaadott vagy a PowerShell által elemzett szereplő állomás kapcsos zárójelek közé szövegkonstans parancsprogram-blokkot, `{}`, mielőtt a PowerShell.exe átadott.

A cmd.exe esetében nincs ilyen, mint egy parancsprogram-blokkot (vagy a scriptblock kulcsszót típus), ezért az átadott érték **parancs** fog _mindig_ karakterláncot.
Egy parancsfájl-blokkon belül a karakterláncot írhat, de a végrehajtás alatt helyett úgy működik, pontosan, hogy a beírt egy tipikus PowerShell-parancssorba, a parancsfájl tartalmát, a nyomtatási kitiltás vissza is.

Az átadott karakterlánc `-Command` továbbra is hajtják végre, a PowerShell-lel, így a parancsfájl-blokk kapcsos zárójelek gyakran nem szükségesek az elsőként a cmd.exe futtatásakor.
Egy karakterláncot, definiált beágyazott parancsprogram-blokkot végrehajtásához a [hívási operátor](/powershell/module/microsoft.powershell.core/about/about_operators#call-operator-) `&` használható:

```console
"& {<command>}"
```

### <a name="-help---"></a>-Help-,?, /?

Powershell.exe szintaxisát jeleníti meg. Ha elkezdi beírni a PowerShell.exe parancsot a PowerShellben, illesztenie a parancs paraméterei a kötőjel (-), nem perjellel (/). A Cmd.exe egy kötőjel vagy a perjelet is használható.

> [!NOTE]
> Hibaelhárítási megjegyzés: A PowerShell 2.0 néhány program, a Windows PowerShell konzol sikertelen kezdve egy LastExitCode, 0xc0000142.

## <a name="examples"></a>EXAMPLES

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
