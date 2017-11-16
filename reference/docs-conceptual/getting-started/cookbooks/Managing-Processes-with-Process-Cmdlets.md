---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A folyamat-parancsmagokkal folyamatok kezelése"
ms.assetid: 5038f612-d149-4698-8bbb-999986959e31
ms.openlocfilehash: 3786fb77167746d6a477dffdd4ea13e863c99964
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="managing-processes-with-process-cmdlets"></a>A folyamat-parancsmagokkal folyamatok kezelése
A folyamat parancsmagok a Windows PowerShell segítségével kezelheti a Windows PowerShell helyi és távoli folyamatokhoz.

## <a name="getting-processes-get-process"></a>Folyamatok lekérdezése (Get-Process)
Ahhoz, hogy a helyi számítógépen futó folyamatok, futtassa a **Get-Process** paraméter nélkül.

Adja meg a folyamat neve vagy a folyamat azonosítók kaphat olyan folyamatokat. A következő parancs beolvassa az üresjárati folyamat:

```
PS> Get-Process -id 0
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
      0       0        0         16     0               0 Idle
```

Bár ez normális vissza adatot nem bizonyos esetekben, amikor megad egy folyamat. a folyamatazonosító parancsmagok **Get-Process** hibát generál, ha nincs találat megtalálja, mert a szokásos szándéka az, hogy beolvasni egy ismert futó folyamat. Egyetlen folyamat sem ezzel az azonosítóval van, akkor valószínű, hogy az azonosító érvénytelen, vagy az, hogy már kilépett a folyamat egyik fontos:

```
PS> Get-Process -Id 99
Get-Process : No process with process ID 99 was found.
At line:1 char:12
+ Get-Process  <<<< -Id 99
```

A Name paraméter, a Get-Process parancsmag segítségével adja meg a folyamat neve alapján folyamatok egy részét. A Name paraméter hajthatja végre több név a vesszővel tagolt listáját, és helyettesítő karakterekkel, támogatja, megadhatja a mintában.

Például a következő paranccsal lekérdezi a "ex." kezdődő folyamat

```
PS> Get-Process -Name ex*
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    234       7     5572      12484   134     2.98   1684 EXCEL
    555      15    34500      12384   134   105.25    728 explorer
```

Mivel a .NET System.Diagnostics.Process osztály a Windows PowerShell folyamatok alapját, követi a egyezmények System.Diagnostics.Process által használt néhány. Ezen egyezmények egyike, hogy a folyamat végrehajtható fájl nevét soha nem tartalmazza a ".exe" végén található a végrehajtható fájl nevét.

**Get-Process** a Name paraméter több értéket is fogad.

```
PS> Get-Process -Name exp*,power* 
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    540      15    35172      48148   141    88.44    408 explorer
    605       9    30668      29800   155     7.11   3052 powershell
```

A ComputerName paraméterre, a Get-Process folyamatok lekérni a távoli számítógépeken használható. A következő parancs például a PowerShell folyamatok lekérdezi a helyi számítógépen (a "localhost" képviseli) és két távoli számítógépen.

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server02
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    258       8    29772      38636   130            3700 powershell
    398      24    75988      76800   572            5816 powershell
    605       9    30668      29800   155     7.11   3052 powershell
```

A számítógép nevében a rendszer nem egyértelmű a kijelzett, de a számítógépnév tulajdonság Get-Process visszaadó folyamat objektum tárolódnak. A következő parancsot a Format-Table parancsmag segítségével jeleníti meg, a folyamat azonosítója, a folyamatnév és a számítógépnév (számítógépnév) a folyamat objektumok tulajdonságai.

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server01 | Format-Table -Property ID, ProcessName, MachineName
  Id ProcessName MachineName
  -- ----------- -----------
3700 powershell  Server01
3052 powershell  Server02
5816 powershell  localhost
```

Összetettebb hozzáadja a számítógépnév tulajdonság Get-Process szabványos megjelenítéséhez. A backtick (\`)(ASCII 96) az a Windows PowerShell folytatási karakter.

```
get-process powershell -computername localhost, Server01, Server02 | format-table -property Handles, `
                    @{Label="NPM(K)";Expression={[int]($_.NPM/1024)}}, `
                    @{Label="PM(K)";Expression={[int]($_.PM/1024)}}, `
                    @{Label="WS(K)";Expression={[int]($_.WS/1024)}}, `
                    @{Label="VM(M)";Expression={[int]($_.VM/1MB)}}, `
                    @{Label="CPU(s)";Expression={if ($_.CPU -ne $()` 
                    {$_.CPU.ToString("N")}}}, `                                                                         
                    Id, ProcessName, MachineName -auto

Handles  NPM(K)  PM(K) WS(K) VM(M) CPU(s)  Id ProcessName  MachineName
-------  ------  ----- ----- ----- ------  -- -----------  -----------
    258       8  29772 38636   130         3700 powershell Server01
    398      24  75988 76800   572         5816 powershell localhost
    605       9  30668 29800   155 7.11    3052 powershell Server02
```

## <a name="stopping-processes-stop-process"></a>Folyamatok (Stop-Process) leállítása
A Windows PowerShell folyamatok listázása, de mi a helyzet a folyamat leállítása rugalmasságot biztosít?

A **Stop-Process** parancsmag időt vesz igénybe, egy nevű vagy azonosítójú adhatja meg a folyamat le kívánja állítani. A folyamat leállítása függ az engedélyeket. Egyes folyamatok nem lehet leállítani. Például ha megpróbálja leállítani az üresjárati folyamat, hibaüzenetet kap:

```
PS> Stop-Process -Name Idle
Stop-Process : Process 'Idle (0)' cannot be stopped due to the following error:
 Access is denied
At line:1 char:13
+ Stop-Process  <<<< -Name Idle
```

A kérdés is kényszeríthető a **megerősítése** paraméter. Ez a paraméter különösen hasznos, ha egy helyettesítő karakter adható meg a folyamat neve, mert előfordulhat, hogy véletlenül felel meg valamelyik folyamat nem szeretné leállítani:

```
PS> Stop-Process -Name t*,e* -Confirm
Confirm
Are you sure you want to perform this action?
Performing operation "Stop-Process" on Target "explorer (408)".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):n
Confirm
Are you sure you want to perform this action?
Performing operation "Stop-Process" on Target "taskmgr (4072)".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):n
```

Összetett folyamat adatkezelési esetében néhány, a parancsmagok szűrés objektum használatával. Egy folyamat objektumot válaszoló tulajdonsága igaz, ha már nem válaszol, mivel le lehet állítani az összes nem válaszoló alkalmazásokat a következő paranccsal:

```
Get-Process | Where-Object -FilterScript {$_.Responding -eq $false} | Stop-Process
```

Más helyzetekben használhatja ugyanezt a megközelítést. Tegyük fel például, hogy egy másodlagos értesítési terület alkalmazás automatikusan fut, amikor a felhasználók egy másik alkalmazás indításához. Előfordulhat, hogy ez nem működik megfelelően a Terminálszolgáltatások-munkamenetekben, de továbbra is szeretné tartani a fizikai számítógép konzol futó munkameneteket. Mindig kapcsolódik a fizikai számítógép asztali munkamenetek rendelkezik egy munkamenet-Azonosítót, 0, így a folyamat összes példánya esetén más munkamenetekben használatával történő leállíthatja **Where-Object** és a folyamat **SessionId** :

```
Get-Process -Name BadApp | Where-Object -FilterScript {$_.SessionId -neq 0} | Stop-Process
```

A Stop-Process parancsmaghoz nem tartozik a ComputerName paraméterre. Ezért a stop-process parancs futtatása távoli számítógépen, akkor kell az Invoke-Command parancsmaggal. Például a kiszolgalo01 távoli számítógépen a PowerShell folyamat leállításához írja be:

```
Invoke-Command -ComputerName Server01 {Stop-Process Powershell}
```

## <a name="stopping-all-other-windows-powershell-sessions"></a>Minden más Windows PowerShell-munkamenetekben leállítása
Alkalmanként lehet hasznos, ha szeretné tudni állítsa le az összes futó Windows PowerShell-munkamenetekben eltérő az aktuális munkamenet. Ha a munkamenet túl sok erőforrást használ, vagy nem érhető el (Ez futtathatnak távolról, vagy egy másik asztal munkamenetben), nem lehet közvetlenül állítsa le. Ha megpróbálja leállítani az összes futó munkameneteket, azonban az aktuális munkamenet megszüntethető helyette.

Minden Windows PowerShell-munkamenetet egy környezeti változó, amely tartalmazza a Windows PowerShell-folyamat azonosítója azonosítója (PID) rendelkezik. Ellenőrizze a $PID minden munkamenet azonosítója alapján, és állítsa le a csak a Windows PowerShell-munkamenetekben, amelyek egy másik azonosítót. A következő adatcsatorna parancs ezt, és leállított munkamenetek listáját adja vissza (használata miatt a **PassThru** paraméter):

```
PS> Get-Process -Name powershell | Where-Object -FilterScript {$_.Id -ne $PID} | Stop-Process -
PassThru
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    334       9    23348      29136   143     1.03    388 powershell
    304       9    23152      29040   143     1.03    632 powershell
    302       9    20916      26804   143     1.03   1116 powershell
    335       9    25656      31412   143     1.09   3452 powershell
    303       9    23156      29044   143     1.05   3608 powershell
    287       9    21044      26928   143     1.02   3672 powershell
```

## <a name="starting-debugging-and-waiting-for-processes"></a>Indítása, a Hibakeresés és a folyamatok vár
Windows PowerShell is tartalmaz parancsmagokat indítása (vagy újraindítása), hibakeresési egy folyamatot, és várja meg a folyamat befejezéséhez a parancs futtatása előtt. Ezekkel a parancsmagokkal kapcsolatos információkért lásd a parancsmag súgó-témakörének parancsmagok.

## <a name="see-also"></a>Lásd még:
- [Get-Process [m2]](https://technet.microsoft.com/en-us/library/27a05dbd-4b69-48a3-8d55-b295f6225f15)
- [STOP-Process [m2]](https://technet.microsoft.com/en-us/library/12454238-9881-457a-bde4-fb6cd124deec)
- [Folyamat](https://technet.microsoft.com/en-us/library/41a7e43c-9bb3-4dc2-8b0c-f6c32962e72c)
- [Várjon, amíg-folyamat](https://technet.microsoft.com/en-us/library/9222af7a-789d-4a09-aa90-09d7c256c799)
- [Hibakeresési-folyamat](https://technet.microsoft.com/en-us/library/eea1dace-3913-4dbd-b659-5a94a610eee1)
- [Invoke-Command parancsot](https://technet.microsoft.com/en-us/library/22fd98ba-1874-492e-95a5-c069467b8462)

