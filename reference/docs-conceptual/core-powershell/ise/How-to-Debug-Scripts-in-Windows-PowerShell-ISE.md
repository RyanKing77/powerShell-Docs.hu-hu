---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A Windows PowerShell ISE parancsfájlok hibakeresése"
ms.openlocfilehash: 0ec520dfcba5e4562258256570f140e618e77cdb
ms.sourcegitcommit: 3720ce4efb6735694cfb53a1b793d949af5d1bc5
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/29/2017
---
# <a name="how-to-debug-scripts-in-windows-powershell-ise"></a>A Windows PowerShell ISE parancsfájlok hibakeresése

Ez a témakör ismerteti a helyi számítógép parancsfájlok hibakeresése a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) visual hibakeresési szolgáltatások segítségével.

## <a name="how-to-manage-breakpoints"></a>Töréspontokat kezelése
Töréspont a kijelölt helyszínen egy parancsfájlban, hol szeretné művelet szüneteltetéséhez, hogy a változók és a környezet, amelyben a parancsprogram fut. az aktuális állapotának ellenőrzéséhez. Miután a parancsfájl által töréspont fel van függesztve, a parancsok a konzol ablaktáblában, a parancsfájl állapotának vizsgálata is futtathatja.  A kimeneti változók, vagy más parancsok futtatásához. A jelenleg futó parancsfájl keretében számára látható változó értékét is módosíthatja. Ellenőrzését szeretné látni, követően újból engedélyezheti a parancsfájl működésére.

A Windows PowerShell hibakeresési környezetben töréspontok három típusú állíthatja be:

1. **. Sor töréspont**. A parancsfájl szünetelteti, amikor a kijelölt sor elérése során a parancsfájl működésére

2. **Változó töréspont.** A parancsfájl felfüggesztése, amikor megváltozik a kijelölt változó értékét.

3. **Parancs töréspont.** A parancsfájl felfüggesztése, amikor a kijelölt parancs arra készül, hogy a parancsfájl működésére során futtatni. További szűréséhez a töréspont csak a kívánt művelet paraméterek része lehet. A parancsot is egy olyan létrehozott függvényt.

Ezek a Windows PowerShell ISE hibakeresési környezetben csak a sor töréspontokat állíthat be a vagy a billentyűparancsok használatával. A más kétféle töréspontokat állíthat, de be lettek állítva a konzol ablaktáblában használatával a [Set-PSBreakpoint](https://technet.microsoft.com/library/88d2d9ad-17dc-44ae-99aa-f841125b9dc8) parancsmag. Ez a szakasz ismerteti, hogyan lehet a Windows PowerShell ISE hibakeresési feladatok végrehajtása a menük használatával, ahol az rendelkezésre áll, és parancsok szélesebb körének végezni a konzol ablaktáblában parancsfájlok használatával.

### <a name="to-set-a-breakpoint"></a>Töréspontokat állíthasson
Csak akkor mentését követően egy parancsfájlban állítható be töréspont. Kattintson a jobb gombbal az adott sor beállítására, és kattintson a kívánt sor **töréspont**. Vagy kattintson a sor sor beállítására, ahová nyomja le az ENTER **F9** vagy a a **Debug** menüben kattintson a **töréspont**.

A következő parancsfájl példája hogyan között állítható be változó töréspont konzolpanelen használatával a [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420) parancsmag.

``` PowerShell
# This command sets a breakpoint on the Server variable in the Sample.ps1 script.
Set-PSBreakpoint -Script sample.ps1 -Variable Server
```

### <a name="list-all-breakpoints"></a>Töréspontokat felsorolása

Töréspontokat megjeleníti az aktuális Windows PowerShell-munkamenetben.

Az a **Debug** menüben kattintson a **lista töréspontok**. A következő parancsfájl példája hogyan listázhatja a konzol ablaktáblában töréspontokat használatával a [Get-PSBreakpoint](https://technet.microsoft.com/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) parancsmag.

``` PowerShell
# This command lists all breakpoints in the current session. 
Get-PSBreakpoint
```

### <a name="remove-a-breakpoint"></a>Távolítsa el a töréspont

Töréspont eltávolítása törli őket.

Ha úgy gondolja, hogy később újra felhasználhatja, érdemes lehet érdemes [tiltsa le a töréspont](#disable-a-breakpoint) , helyette.
Kattintson a jobb gombbal a sort, ahol töréspont, és kattintson a kívánt **töréspont**.
Vagy kattintson a sor, ha szeretné eltávolítani a töréspont, és a a **Debug** menüben kattintson a **töréspont**.
Az alábbi parancsfájl a megadott Azonosítójú töréspont eltávolítása a konzol ablaktáblában használatával példája a [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) parancsmag.

``` PowerShell
# This command deletes the breakpoint with breakpoint ID 2.
Remove-PSBreakpoint -Id 2
```

### <a name="remove-all-breakpoints"></a>Törölje a töréspontokat
Eltávolítja az aktuális munkamenetben definiált töréspontokat a **Debug** menüben kattintson **eltávolítása töréspontokat**.

A következő parancsfájl töréspontokat eltávolítása a konzol ablaktáblában használatával példája a [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) parancsmag.

``` PowerShell
# This command deletes all of the breakpoints in the current session.
Get-PSBreakpoint | Remove-PSBreakpoint
```

### <a name="disable-a-breakpoint"></a>Tiltsa le a töréspont
Töréspont letiltásával nem távolítja el azt. az kikapcsolja, amíg az nincs engedélyezve.  Egy adott sor töréspont letiltásához kattintson a jobb gombbal a sort, ahol tiltsa le a töréspont, és kattintson a kívánt **tiltsa le a töréspont**. Vagy kattintson a sor, ha le szeretné tiltani a töréspont nyomja le az ENTER **F9** vagy a a **Debug** menüben kattintson **tiltsa le a töréspont**. A következő parancsfájl példája hogyan eltávolíthatja a megadott Azonosítójú töréspont konzolpanelen használatával a [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) parancsmag.

``` PowerShell
# This command disables the breakpoint with breakpoint ID 0.
Disable-PSBreakpoint -Id 0
```

### <a name="disable-all-breakpoints"></a>Töréspontokat letiltása
Töréspont letiltásával nem távolítja el azt. az kikapcsolja, amíg az nincs engedélyezve.  Le kívánja tiltani töréspontokat a jelenlegi munkamenet a **Debug** menüben kattintson a **tiltsa le a töréspontokat**. A következő parancsfájl példája letiltásáról töréspontokat a konzol ablaktáblában használatával a [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) parancsmag.

``` PowerShell
# This command disables all breakpoints in the current session. 
# You can abbreviate this command as: "gbp | dbp".
Get-PSBreakpoint | Disable-PSBreakpoint
```

### <a name="enable-a-breakpoint"></a>Töréspont engedélyezése
Ahhoz, hogy az adott töréspont, kattintson a jobb gombbal a sort, ahol Töréspont engedélyezése, és kattintson a kívánt **engedélyezése töréspont**. Vagy kattintson a sorra, ahová Töréspont engedélyezése, és nyomja le az **F9** vagy a a **Debug** menüben kattintson a **engedélyezése töréspont**. A következő parancsfájl egy példát, hogyan engedélyezheti a konzol ablaktáblában adott töréspontok használatával a [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) parancsmag.

``` PowerShell
# This command enables breakpoints with breakpoint IDs 0, 1, and 5.
Enable-PSBreakpoint -Id 0, 1, 5
```

### <a name="enable-all-breakpoints"></a>Töréspontokat engedélyezése
Ahhoz, hogy az aktuális munkamenetben definiált töréspontokat a **Debug** menüben kattintson a **töréspontokat engedélyezése**. A következő parancsfájl egy példát, hogyan engedélyezheti a konzol ablaktáblában töréspontokat használatával a [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) parancsmag.

``` PowerShell
# This command enables all breakpoints in the current session. 
# You can abbreviate the command by using their aliases: "gbp | ebp".
Get-PSBreakpoint | Enable-PSBreakpoint
```

## <a name="how-to-manage-a-debugging-session"></a>A hibakeresési munkamenetben kezelése
Mielőtt elkezdené a hibakeresést, meg kell adni egy vagy több töréspontok. Nem állítható be töréspont, kivéve, ha a parancsfájl debug kívánt menti. Bemutatja, hogyan állítható be töréspont az utasításokat, lásd: [töréspontok kezelése](#how-to-manage-breakpoints) vagy [Set-PSBreakpoint](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/set-psbreakpoint). Hibakeresés indítása után nem szerkeszthetők egy parancsfájl, amíg le nem állítják hibakeresés. Egy parancsfájl, amely rendelkezik egy vagy több töréspontok beállítása előtt fut, automatikusan menti.

### <a name="to-start-debugging"></a>A hibakeresés
Nyomja le az **F5** vagy az eszköztáron kattintson a **-parancsfájl futtatása** ikonra, vagy a a **Debug** menüben kattintson **Futtatás/Folytatás**. A parancsprogram lefut, amíg az első töréspont ütközik. Megszakítja a műveletet, és kiemeli a sor, amikor szünetel.

### <a name="to-continue-debugging"></a>A folytatáshoz a hibakeresés
Nyomja le az **F5** vagy az eszköztáron kattintson a **-parancsfájl futtatása** ikonra, vagy a a **Debug** menüben kattintson a **Futtatás/Folytatás** vagy, írja be a konzol ablaktáblájában **C** , és nyomja le az **ENTER**. Ez azt eredményezi, hogy a parancsfájl a következő töréspont vagy a parancsfájl végén futtatását, ha nincsenek további töréspontok hibát.

### <a name="to-view-the-call-stack"></a>A hívási verem megtekintése
A hívási verem megjeleníti az aktuális hely a parancsfájl futtatása. Ha a parancsfájl egy másik függvény által hívott függvény fut, majd, amely képviseli jelennek meg a kimenet további sorokat. A legalsó sor jeleníti meg az eredeti parancsfájlt és a sor, amelyben a következő függvényt hívták. A Tovább gombra. a függvény és a sort, amelyben egy másik művelet lehet, hogy rendelkezik hívása történt a sor megmutatja.  A legfelső sor tartalmazza az aktuális környezetben, amelyen a töréspont van állítva az aktuális sor.

Szünetel, amíg a jelenlegi hívásverem megtekintéséhez nyomja le az ENTER **CTRL + SHIFT + D** vagy a a **Debug** menüben kattintson a **megjelenítési hívási veremnek megfelelő** vagy, írja be a konzol ablaktáblájában **K**  , és nyomja le az **ENTER**.

### <a name="to-stop-debugging"></a>A hibakereső leállítása
Nyomja le az ENTER **SHIFT-F5** vagy a a **Debug** menüben kattintson a **hibakereső leállítása**, vagy írja be a konzol ablaktáblájában **Q** , és nyomja le az  **Adja meg**.

## <a name="how-to-step-over-step-into-and-step-out-while-debugging"></a>Ugorja át, lépjen be és hibakeresés során lépés
Lépjen az a folyamat egy utasítás fut egyszerre. Állítsa le a kód sor, és vizsgálja meg a változók és a rendszer állapotát. A következő táblázat ismerteti a gyakori hibakeresési feladatokat, mint a léptetési keresztül, lépjen be, és lépjen.

| Hibakeresési feladat | Leírás | A PowerShell ISE elvégzésére |
| --- | --- | --- |
| **Lépjen be** | Az aktuális utasítás végrehajtása, és majd leállítja a következő utasításnál. Ha az aktuális utasítás függvény vagy parancsfájl hívás, majd az adott függvény vagy parancsfájl hibakereső a lépéseket, ellenkező esetben leállítja a következő utasításnál. | Nyomja le az ENTER **F11** vagy a a **Debug** menüben kattintson a **lépésenként**, vagy írja be a konzol ablaktáblájában **S** nyomja le az ENTER **ENTER**. |
| **Átlépés** | Az aktuális utasítás végrehajtása, és majd leállítja a következő utasításnál. Ha az aktuális utasítás olyan függvény vagy parancsfájl hívás, amely a hibakereső végrehajtja a teljes függvény vagy parancsfájl, és leállítja a függvény hívása után a következő utasításnál. | Nyomja le az ENTER **F10** vagy a a **Debug** menüben kattintson a **Átlépés**, vagy írja be a konzol ablaktáblájában **V** nyomja le az ENTER **ENTER**. |
| **Kilépés** | A current függvény kívül, és egy szinttel, ha a függvény van beágyazva lépéseket. Ha törzsébe, a parancsfájl végrehajtása végén, vagy a következő töréspont. A rendszer kihagyta utasítás végrehajtása, de nem lépcsőzetes keresztül. | Nyomja le az ENTER **SHIFT + F11**, vagy a a **Debug** menüben kattintson a **lépés kimenő**, vagy írja be a konzol ablaktáblájában **O** nyomja le az ENTER **ENTER**. |
| **Továbbra is** | Végén, vagy a következő töréspont végrehajtása folytatódik. A kihagyott funkciók és indítások hajtotta végre, de nem lépcsőzetes keresztül. | Nyomja le az ENTER **F5** vagy a a **Debug** menüben kattintson a **Futtatás/Folytatás**, vagy írja be a konzol ablaktáblájában **C** nyomja le az ENTER **ENTER**. |

## <a name="how-to-display-the-values-of-variables-while-debugging"></a>Hibakeresés során változók értékeinek megjelenítése
A változók aktuális értékeit megjelenítheti a parancsfájl lépéseit a kódot.

### <a name="to-display-the-values-of-standard-variables"></a>Standard változók értékeinek megjelenítéséhez
Az alábbi módszerek valamelyikével:

- A parancsfájl ablaktáblán mutasson a változó értéke eszközleírásként megjelenítéséhez.

- A konzol ablaktáblában írja be a változó nevét, és nyomja le az **ENTER**.

Minden ablaktáblái ISE mindig ugyanabban a hatókörben van. Ezért egy parancsfájl hibakeresést, amíg a konzolpanelen beírt parancsot futtathatja parancsfájl hatókörében. Ez lehetővé teszi, hogy a konzol ablaktáblában található változók értékeit, és csak a parancsfájl definiált függvényeket.

### <a name="to-display-the-values-of-automatic-variables"></a>Az automatikus változók értékek megjelenítése
A fenti módszer segítségével szinte minden változók levő értéket jeleníti meg, amíg parancsfájl hibakeresés alatt. Ezek a módszerek azonban nem működnek a következő automatikus változók.

- $_

- $Input

- $MyInvocation

- $PSBoundParameters

- $Args

Kísérli meg ezek a változók bármelyikének levő értéket jeleníti meg, ha a változó értékét elérhetővé az egy belső folyamat a hibakeresőben, nem értékét használja a változót a parancsfájl. Megkerüléséhez Ez néhány változók ($_ $Input, $MyInvocation, $PSBoundParameters és $Args) a következő módszerrel:

1. A parancsfájl az automatikus változó értékének hozzárendelése egy új változót.

2. Megjeleníti az új változó értékét, vagy a parancssori panelbe az új változó fölé, vagy írja be az új változó a konzol ablaktáblában.

Például $MyInvocation változó értékének megjelennek a parancsfájlt, az érték hozzárendelése egy új változót, például a $scriptname, és majd vigye vagy vagy típusú értéket $scriptname változó.

``` PowerShell
#In MyScript.ps1
$scriptname = $MyInvocation.MyCommand.Path

#In the Console Pane:
C:\ps-test> $scriptname
C:\ps-test\MyScript.ps1
```

## <a name="see-also"></a>Lásd még:
- [A Windows PowerShell ISE használatával](Using-the-Windows-PowerShell-ISE.md)

