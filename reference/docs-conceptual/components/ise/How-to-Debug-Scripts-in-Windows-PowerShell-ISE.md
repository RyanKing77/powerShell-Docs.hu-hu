---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Parancsfájlokban való hibakeresés a PowerShell ISE-ben
ms.openlocfilehash: b7af2de83a3f796a2057514e36ad8b74367e8ce2
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62086867"
---
# <a name="how-to-debug-scripts-in-windows-powershell-ise"></a>Parancsfájlokban való hibakeresés a PowerShell ISE-ben

Ez a cikk bemutatja, hogyan parancsfájlokban való hibakeresés a helyi számítógépen a Windows PowerShell integrált parancsfájl-kezelési környezet (ISE) vizuális hibakeresési funkciók használatával.

## <a name="how-to-manage-breakpoints"></a>Töréspontok kezelése

Egy töréspontot a kijelölt helyszínen egy parancsfájlban, hova szeretné felfüggeszteni, így megvizsgálhatja a változókat és a környezet, amelyben a parancsprogram fut. az aktuális állapotát a művelet. Miután a parancsfájl által egy töréspontot szüneteltetve van, futtathat parancsokat vizsgálata a szkript állapotát a konzol ablaktáblában.  Kimeneti változókat, vagy más parancsok futtatásához. Az aktuálisan futó szkript kontextusában számára látható minden változó értékét akkor is módosíthatja. Milyen meg szeretné tekinteni ellenőrzését követően folytathatja a parancsfájl működésére.

A Windows PowerShell hibakeresési környezetben töréspontok három típusú állíthatja be:

1. **Töréspont sor**. A parancsfájl felfüggeszti a szkript a művelet során a kijelölt sor elérésekor

2. **Változó töréspontot.** A parancsfájl minden alkalommal, amikor megváltozik a kijelölt változó értéke felfüggesztése.

3. **Parancs töréspontot.** A parancsfájl minden alkalommal, amikor a kijelölt parancsot arra készül, hogy a parancsfájl működésére során futtatandó felfüggesztése. További szűréséhez, csak a kívánt műveletet a töréspont paramétereket is alkalmas. A parancsot is létrehozott egy függvényt.

Ezeket a Windows PowerShell ISE-hibakeresési környezetben csak a sor töréspontok állítható a menüből vagy a billentyűparancsok segítségével. Akkor állítható be töréspontokat a másik két típusú, de azok-beállításokat a konzol panelen a [Set-PSBreakpoint](https://technet.microsoft.com/library/88d2d9ad-17dc-44ae-99aa-f841125b9dc8) parancsmagot. Ez a szakasz ismerteti, hogyan hajtsa végre a hibakeresési feladatokat Windows PowerShell ISE-ben menüket használja, ha elérhetők, és hajtsa végre a parancsokat szélesebb körének teszik a konzol panelen parancsfájlok használatával.

### <a name="to-set-a-breakpoint"></a>Állítson be egy töréspontot a

Töréspont beállítható egy parancsfájlban csak azt követően lett mentve. Kattintson a jobb gombbal a sor, ahol állítson be egy sor töréspontot, és kattintson a kívánt **töréspont**. Vagy kattintson a sorra, ahol szeretné állítani egy sor töréspontot, nyomja le az ENTER **F9** vagy a a **Debug** menüben kattintson a **töréspont**.

A következő parancsfájl egy példát, hogyan között állítható be változó Töréspont a konzol panel használatával a [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420) parancsmagot.

```powershell
# This command sets a breakpoint on the Server variable in the Sample.ps1 script.
Set-PSBreakpoint -Script sample.ps1 -Variable Server
```

### <a name="list-all-breakpoints"></a>Töréspontokat listázása

Töréspontokat megjeleníti az aktuális Windows PowerShell-munkamenetben.

Az a **Debug** menüben kattintson a **lista töréspontok**. A következő parancsfájl egy példát, hogyan listázhatja a konzol panelen töréspontokat használatával a [Get-PSBreakpoint](https://technet.microsoft.com/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) parancsmagot.

```powershell
# This command lists all breakpoints in the current session.
Get-PSBreakpoint
```

### <a name="remove-a-breakpoint"></a>Töréspont eltávolítása

Töréspont eltávolítása törli őket.

Ha úgy véli, hogy később újra felhasználhatja, érdemes lehet érdemes [tiltsa le a töréspont](#disable-a-breakpoint) , helyette.
Kattintson a jobb gombbal a sor, ahol szeretné eltávolítani egy töréspontot, és kattintson a **töréspont**.
Vagy kattintson a sort, amelyben el kívánja távolítani egy töréspontot, és az a **Debug** menüben kattintson a **töréspont**.
A következő parancsfájl példaként szolgál a megadott Azonosítóval rendelkező töréspont eltávolítása a konzol panel használatával a [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) parancsmagot.

```powershell
# This command deletes the breakpoint with breakpoint ID 2.
Remove-PSBreakpoint -Id 2
```

### <a name="remove-all-breakpoints"></a>Az összes töréspont eltávolítása

Töréspontokat definiálva az aktuális munkamenetben eltávolítása a **Debug** menüben kattintson a **minden töréspont eltávolítása**.

Az alábbi parancsfájlt minden töréspont eltávolítása a konzol panel használatával példája a [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) parancsmagot.

```powershell
# This command deletes all of the breakpoints in the current session.
Get-PSBreakpoint | Remove-PSBreakpoint
```

### <a name="disable-a-breakpoint"></a>Töréspont letiltása

Töréspont letiltása nem távolítja el azt. azt kikapcsolja, amíg az nincs engedélyezve.  Egy adott sor töréspontot letiltásához kattintson a jobb gombbal a sor, ahol szeretné letiltani egy töréspontot, és kattintson a **letiltása töréspontot**. Vagy kattintson a sor, amikor le kívánja tiltani egy töréspontot, nyomja le az ENTER **F9** vagy a a **hibakeresése** menüben kattintson a **letiltása töréspontot**. A következő parancsfájl egy példát, hogyan eltávolíthatja a megadott Azonosítóval rendelkező egy töréspontot a konzol panelen használatával a [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) parancsmagot.

```powershell
# This command disables the breakpoint with breakpoint ID 0.
Disable-PSBreakpoint -Id 0
```

### <a name="disable-all-breakpoints"></a>Tiltsa le az összes töréspontok keresése

Töréspont letiltása nem távolítja el azt. azt kikapcsolja, amíg az nincs engedélyezve.  Le kívánja tiltani töréspontokat a jelenlegi munkamenet a **Debug** menüben kattintson a **töréspontokat letiltása**. A következő parancsfájl példaként szolgál a letiltásáról töréspontokat a konzol panelen használatával a [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) parancsmagot.

```powershell
# This command disables all breakpoints in the current session.
# You can abbreviate this command as: "gbp | dbp".
Get-PSBreakpoint | Disable-PSBreakpoint
```

### <a name="enable-a-breakpoint"></a>Töréspont engedélyezése

Ahhoz, hogy egy adott töréspontot, kattintson a jobb gombbal a sor hol szeretne engedélyezni egy töréspontot, és kattintson a **engedélyezése töréspontot**. Vagy kattintson a sorra, ahol szeretne engedélyezni egy töréspontot, és nyomja le az **F9** vagy a a **Debug** menüben kattintson a **engedélyezése töréspontot**. A következő parancsfájl egy példát, hogyan engedélyezheti a konzol panelen adott töréspontok használatával a [engedélyezése – PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) parancsmagot.

```powershell
# This command enables breakpoints with breakpoint IDs 0, 1, and 5.
Enable-PSBreakpoint -Id 0, 1, 5
```

### <a name="enable-all-breakpoints"></a>Az összes töréspontok engedélyezése

Ahhoz, hogy definiálva az aktuális munkamenetben töréspontokat a **hibakeresése** menüben kattintson **töréspontokat engedélyezése**. A következő parancsfájl egy példát, hogyan engedélyezheti a konzol panelen töréspontokat a rendszer a [engedélyezése – PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) parancsmagot.

```powershell
# This command enables all breakpoints in the current session.
# You can abbreviate the command by using their aliases: "gbp | ebp".
Get-PSBreakpoint | Enable-PSBreakpoint
```

## <a name="how-to-manage-a-debugging-session"></a>A hibakeresési munkamenet kezelése

Mielőtt elkezdené, hibakeresés, be kell egy vagy több töréspontokat a kiválasztott. Nem lehet állítson be egy töréspontot, kivéve, ha a parancsfájl, amelyen hibakeresést végez, a rendszer menti. Bemutatja, hogyan állítson be egy töréspontot a irányban, lásd: [töréspontok kezelése](#how-to-manage-breakpoints) vagy [Set-PSBreakpoint](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/set-psbreakpoint). Után elindítja a hibakeresés, amíg le nem állítják hibakeresés parancsfájl nem szerkeszthető. Egy parancsfájl, amely rendelkezik egy vagy több töréspontokat a kiválasztott állítsa be a rendszer automatikusan menti azt futtatása előtt.

### <a name="to-start-debugging"></a>A hibakeresés

Nyomja meg **F5** vagy az eszköztáron kattintson a **parancsfájl futtatása** ikonra, vagy a a **Debug** menüben kattintson **Futtatás/Folytatás**. A szkript futtatása, amíg az első töréspont tapasztal. Nincs művelet megszakítja, és kiemeli a sort, amelyen szünetel.

### <a name="to-continue-debugging"></a>A folytatáshoz a hibakeresés

Nyomja meg **F5** vagy az eszköztáron kattintson a **parancsfájl futtatása** ikonra, vagy a a **Debug** menüben kattintson a **Futtatás/Folytatás** vagy írja be a konzol ablaktáblában **C** , és nyomja le az **ENTER**. Ennek hatására a szkript a következő töréspontig vagy a teljes körű parancsfájl futtatását, ha nincsenek további töréspontokat a kiválasztott program hibát.

### <a name="to-view-the-call-stack"></a>A hívási veremben megtekintése

A hívási veremben jeleníti meg az aktuális Futtatás helye a szkriptben. Ha a parancsfájl egy másik függvény által hívott függvény fut, majd, amely képviseli jelennek meg a további sorokat a kimenetben. A legalsó sor jeleníti meg az eredeti parancsfájl és a sort, amelyben egy függvényt hívták. A következő a sor megmutatja, hogy a függvény és a sort, amelyben egy másik függvény előfordulhat, hogy hívták.  A legfelső sor látható, amelyen a töréspont be van állítva az aktuális sor az aktuális környezetben.

Fel van függesztve, amíg a jelenlegi hívási vermet, nyomja le a **CTRL + SHIFT + D** vagy a a **Debug** menüben kattintson a **megjelenített hívási veremnek** vagy írja be a konzol ablaktáblában **K**  , és nyomja le az **ENTER**.

### <a name="to-stop-debugging"></a>A hibakereső leállítása

Nyomja le az **SHIFT-F5** vagy a a **Debug** menüben kattintson a **hibakereső leállítása**, vagy írja be a konzol ablaktáblában **Q** , és nyomja le az  **Adja meg**.

## <a name="how-to-step-over-step-into-and-step-out-while-debugging"></a>Átlépés, lépjen be és hibakeresése során krokovat s vystoupením

Lépjen az a folyamat egy utasítás egy időben futnak. Állítsa le az egy sor kódot, és vizsgálja meg az értékeket a változók és a rendszer állapotát. A következő táblázat ismerteti a gyakori hibakeresési feladatokat, mint a ke krokování keresztül, lépjen be és lépjen.

| A feladat hibakeresési | Leírás | Hogyan végezheti el, a PowerShell ISE-ben |
| --- | --- | --- |
| **Lépjen be** | Az aktuális utasítás végrehajtása, és a következő utasítást, majd leáll. Ha az aktuális utasítás egy függvény vagy parancsfájl hívást, majd a hibakeresőt a lépéseket, hogy a függvény vagy parancsfájl, ellenkező esetben leállítja, a következő utasítást. | Nyomja le az **F11** vagy a a **Debug** menüben kattintson a **lépés be**, vagy írja be a konzol ablaktáblában **S** nyomja le az ENTER **ENTER**. |
| **Átlépés** | Az aktuális utasítás végrehajtása, és a következő utasítást, majd leáll. Ha az aktuális utasítás függvény vagy parancsfájl-hívást, majd a hibakeresőt a teljes függvény vagy parancsfájl hajt végre, és a következő utasítást a függvény hívása után megáll. | Nyomja le az **F10** vagy a a **Debug** menüben kattintson a **Átlépés**, vagy írja be a konzol ablaktáblában **V** nyomja le az ENTER **ENTER**. |
| **Krokovat s Vystoupením** | Lépések az aktuális függvény és egy szinttel, ha a függvény van beágyazva. Ha a fő törzsében, a parancsfájl végrehajtása a teljes körű, vagy a következő töréspontig. A rendszer kihagyta utasításokat végrehajtva, de nem lépcsőzetes keresztül. | Nyomja le az **SHIFT + F11**, vagy a a **Debug** menüben kattintson a **lépés ki**, vagy írja be a konzol ablaktáblában **O** nyomja le az ENTER **ENTER**. |
| **Továbbra is** | A teljes körű, vagy a következő töréspontig végrehajtása folytatódik. A rendszer kihagyta funkciók és indítások végrehajtva, de nem lépcsőzetes keresztül. | Nyomja le az **F5** vagy a a **Debug** menüben kattintson a **Futtatás/Folytatás**, vagy írja be a konzol ablaktáblában **C** nyomja le az ENTER **ENTER**. |

## <a name="how-to-display-the-values-of-variables-while-debugging"></a>Hibakeresés közben változók értékeinek megjelenítése

A változók aktuális értékeit megjelenítheti a szkriptben, a kód lépéseit.

### <a name="to-display-the-values-of-standard-variables"></a>Standard változók értékeinek megjelenítése

Az alábbi módszerek valamelyikével:

- A parancsfájl panelen a kurzort a változót, egy elemleírás jelenít meg az értékét.

- A konzol ablaktáblában írja be a változó nevét, majd nyomja le **ENTER**.

A ISE-ben minden ablaktáblák mindig ugyanabban a hatókörben vannak. Ezért egy parancsfájlt, hibakeresés során, írja be a konzol ablaktáblában parancsok futtatása parancsfájl hatókörében. Ez lehetővé teszi, hogy a konzol panel használata a változók értékeit, és csak a szkriptben meghatározott függvényeket.

### <a name="to-display-the-values-of-automatic-variables"></a>Az automatikus változók értékeinek megjelenítése

A fenti módszer segítségével szinte minden változó értékének megjelenítése egy parancsfájl hibakeresés során. Ezek a módszerek azonban nem működnek a következő automatikus változók.

- $_

- $Input

- $MyInvocation

- $PSBoundParameters

- $Args

Meg ezeket a változókat bármelyikének értéket jeleníti meg, ha a változó értékét kap a belső folyamatban a hibakeresőt használ, nem a szkriptben a változó értékét. Ön megkerüléséhez Ez néhány változóhoz ($_, $Input, $MyInvocation, $PSBoundParameters és $Args) a következő módszerrel:

1. Új változó az automatikus változó értékét hozzárendelése a szkriptben.

2. Megjeleníti az új változó értékét, vagy az egérmutatót a parancsfájl panelen az új változó, vagy írja be az új változó a konzol ablaktáblában.

Például szeretné megjeleníteni a $MyInvocation változó értékét a szkriptben, rendelni az értéket az új változó, például a $scriptname, és ezután mutasson vagy $scriptname változó értékéhez megjelenítéséhez írja be.

```powershell
# In C:\ps-test\MyScript.ps1
$scriptname = $MyInvocation.MyCommand.Path
```

```output
# In the Console Pane:
PS> .\MyScript.ps1
PS> $scriptname
C:\ps-test\MyScript.ps1
```

## <a name="see-also"></a>Lásd még:

- [A Windows PowerShell ISE felfedezése](../../getting-started/fundamental/exploring-the-windows-powershell-ise.md)