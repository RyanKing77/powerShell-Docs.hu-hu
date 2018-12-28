---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Folyamatok kezelése folyamatparancsmagokkal
ms.assetid: 5038f612-d149-4698-8bbb-999986959e31
ms.openlocfilehash: 741a3464bce6284c4933384398c4e9ddcca2572c
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404157"
---
# <a name="managing-processes-with-process-cmdlets"></a>Folyamatok kezelése folyamatparancsmagokkal

A folyamat parancsmagok a Windows PowerShell segítségével a Windows PowerShellben a helyi és távoli folyamatok kezeléséhez.

## <a name="getting-processes-get-process"></a>Folyamatok lekérdezése (Get-Process)

A helyi számítógépen futó folyamatok lekéréséhez futtassa a **Get-Process** nélkül.

Bizonyos folyamatok kaphat a folyamat nevét vagy a folyamat azonosítók megadásával. Az alábbi parancs lekéri az üresjárati folyamat:

```
PS> Get-Process -id 0

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
      0       0        0         16     0               0 Idle
```

Bár előfordulhat, hogy parancsmagokat nem adnak vissza adatokat bizonyos helyzetekben, amikor megad egy folyamat, a folyamatazonosító **Get-Process** hibát generál, ha úgy találja, hogy nincs egyezés, mert szokásos célja beolvasni egy ismert futó folyamat. Ha van ilyen azonosítójú folyamatot sem, akkor valószínű, hogy az azonosító helytelen, vagy a folyamat a lényeges már kilépett:

```
PS> Get-Process -Id 99

Get-Process : No process with process ID 99 was found.
At line:1 char:12
+ Get-Process  <<<< -Id 99
```

A Name paraméter, a Get-Process-parancsmag segítségével adja meg a folyamat neve alapján a folyamat egy részét. A Name paraméter is igénybe vehet a neveket vesszővel elválasztott listáját, és támogatja a helyettesítő karakterekkel, így beírhatja a név minták.

Például az alábbi parancs lekéri a "például" kezdődő folyamat

```
PS> Get-Process -Name ex*

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    234       7     5572      12484   134     2.98   1684 EXCEL
    555      15    34500      12384   134   105.25    728 explorer
```

Mivel a Windows PowerShell-folyamatok alapját, a .NET System.Diagnostics.Process osztály követi a egyezmények System.Diagnostics.Process által használt néhány. Ezen egyezmények egyike, hogy a folyamat nevét, egy végrehajtható fájl soha nem tartalmazza a ".exe" végén található a végrehajtható fájl nevét.

**Get-Process** a Name paraméter több értéket is fogad.

```
PS> Get-Process -Name exp*,power*

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    540      15    35172      48148   141    88.44    408 explorer
    605       9    30668      29800   155     7.11   3052 powershell
```

A Get-Process-ComputerName paraméter használatával a távoli számítógépeken lévő folyamatok beolvasása. Például a következő parancs lekérdezi a helyi számítógépen (a "localhost" által jelölt) a PowerShell-folyamatokat, és két távoli számítógépen.

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server02

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    258       8    29772      38636   130            3700 powershell
    398      24    75988      76800   572            5816 powershell
    605       9    30668      29800   155     7.11   3052 powershell
```

A számítógép nevében a rendszer nem egyértelmű, a kijelzett, de a számítógépnév tulajdonság, amely visszaadja a Get-Process folyamat objektumot tárolódnak. A következő parancsot a Format-Table-parancsmag használatával jeleníti meg, a Folyamatazonosítója, ProcessName és MachineName (ComputerName) a folyamat objektumok tulajdonságait.

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server01 | Format-Table -Property ID, ProcessName, MachineName

  Id ProcessName MachineName
  -- ----------- -----------
3700 powershell  Server01
3052 powershell  Server02
5816 powershell  localhost
```

Összetettebb hozzáadja a számítógépnév tulajdonság a standard szintű Get-Process megjelenítése.

```
PS> Get-Process powershell -ComputerName localhost, Server01, Server02 |
    Format-Table -Property Handles,
        @{Label="NPM(K)";Expression={[int]($_.NPM/1024)}},
        @{Label="PM(K)";Expression={[int]($_.PM/1024)}},
        @{Label="WS(K)";Expression={[int]($_.WS/1024)}},
        @{Label="VM(M)";Expression={[int]($_.VM/1MB)}},
        @{Label="CPU(s)";Expression={if ($_.CPU -ne $()){$_.CPU.ToString("N")}}},
        Id, ProcessName, MachineName -auto

Handles  NPM(K)  PM(K) WS(K) VM(M) CPU(s)  Id ProcessName  MachineName
-------  ------  ----- ----- ----- ------  -- -----------  -----------
    258       8  29772 38636   130         3700 powershell Server01
    398      24  75988 76800   572         5816 powershell localhost
    605       9  30668 29800   155 7.11    3052 powershell Server02
```

## <a name="stopping-processes-stop-process"></a>Folyamatok (Stop-Process) leállítása

Windows PowerShell a folyamatok listázása, de mi a helyzet a folyamat leállítása rugalmasságot biztosít?

A **Stop-Process** parancsmagnál egy név vagy azonosító megadása egy folyamat meg szeretné szüntetni. Állítsa le a folyamat képességét az engedélyektől függ. Bizonyos folyamatok nem lehet leállítani. Ha például meg az üresjárati folyamat leállítása, ha hibaüzenetet kap:

```
PS> Stop-Process -Name Idle
Stop-Process : Process 'Idle (0)' cannot be stopped due to the following error:
 Access is denied
At line:1 char:13
+ Stop-Process  <<<< -Name Idle
```

A kérdés is kényszeríthető a **megerősítése** paraméter. Ez a paraméter különösen hasznos használatakor egy helyettesítő karaktert tartalmazó megadásakor a folyamat nevét, mert előfordulhat, hogy véletlenül felel meg bizonyos folyamatok nem szeretné, hogy állítsa le:

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

Összetett folyamat manipuláció lehetőség néhány, a parancsmagok szűrés objektum használatával. Egy folyamat objektumot válaszol tulajdonsága igaz, amikor nem válaszol, mivel az összes nem válaszoló alkalmazásokat az alábbi paranccsal állíthatja le:

```powershell
Get-Process | Where-Object -FilterScript {$_.Responding -eq $false} | Stop-Process
```

Más helyzetekben használhatja ugyanazt a megközelítést. Tegyük fel például, hogy egy másodlagos értesítési terület alkalmazás automatikusan fut egy másik alkalmazás indításakor. Előfordulhat, hogy ez nem működik megfelelően a Terminálszolgáltatások munkamenetek során, de továbbra is szeretné a fizikai számítógép-konzolt futtató munkamenetet tárolja. Mindig csatlakozik a fizikai számítógép, asztali munkamenetek rendelkezik egy munkamenet-azonosító értéke 0, így a folyamat összes példánya vannak más munkamenetek használatával állítsa le **Where-Object** és a folyamat **SessionId** :

```powershell
Get-Process -Name BadApp | Where-Object -FilterScript {$_.SessionId -neq 0} | Stop-Process
```

A Stop-Process parancsmaghoz nem tartozik a ComputerName paramétert. Ezért egy leállítási folyamatot parancs futtatása egy távoli számítógépen szeretné használni az Invoke-Command parancsmagot. Írja be például a kiszolgalo01 távoli számítógépen a PowerShell-folyamat leállításához:

```powershell
Invoke-Command -ComputerName Server01 {Stop-Process Powershell}
```

## <a name="stopping-all-other-windows-powershell-sessions"></a>Minden más Windows PowerShell-munkamenetekben leállítása

Időnként hasznos lehet a tudnak állni eltérő az aktuális munkamenet összes futó Windows PowerShell-munkameneteket. Ha egy munkamenetben túl sok erőforrást használ, vagy nem érhető el (azt is futnia távolról, vagy egy másik asztal munkamenetben), nem lehet közvetlenül állítsa le. Ha megpróbálja leállítani az összes futó munkameneteket, azonban a jelenlegi munkamenet megszüntethető helyette.

Minden Windows PowerShell-munkamenetet, egy környezeti változót, amely tartalmazza a Windows PowerShell-folyamat azonosítója PID. Ellenőrizze a $PID mindegyik munkamenet azonosítója alapján, és csak Windows PowerShell-munkamenetekben, amelyek egy másik azonosítót. megszüntetheti A következő folyamat parancs azért teszi ezt, és elbocsátott munkamenetek listáját adja vissza (a használata miatt a **PassThru** paraméter):

```
PS> Get-Process -Name powershell | Where-Object -FilterScript {$_.Id -ne $PID} | Stop-Process -PassThru

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    334       9    23348      29136   143     1.03    388 powershell
    304       9    23152      29040   143     1.03    632 powershell
    302       9    20916      26804   143     1.03   1116 powershell
    335       9    25656      31412   143     1.09   3452 powershell
    303       9    23156      29044   143     1.05   3608 powershell
    287       9    21044      26928   143     1.02   3672 powershell
```

## <a name="starting-debugging-and-waiting-for-processes"></a>Indítása, a Hibakeresés és a folyamatok Várakozás

Windows PowerShell-parancsmagokkal indítása (vagy újraindítása), is tartalmaz, hibakeresési egy folyamatot, és várja meg a folyamat befejeződését, mielőtt a következő parancs futtatásával. Ezekkel a parancsmagokkal kapcsolatos információkért tekintse meg az egyes parancsmagok parancsmag Súgó-témakör.

## <a name="see-also"></a>Lásd még:

- [Get-Process [m2]](https://technet.microsoft.com/en-us/library/27a05dbd-4b69-48a3-8d55-b295f6225f15)
- [STOP-Process [m2]](https://technet.microsoft.com/en-us/library/12454238-9881-457a-bde4-fb6cd124deec)
- [Folyamatának elindítása](https://technet.microsoft.com/en-us/library/41a7e43c-9bb3-4dc2-8b0c-f6c32962e72c)
- [Wait-folyamat](https://technet.microsoft.com/en-us/library/9222af7a-789d-4a09-aa90-09d7c256c799)
- [Hibakeresési-folyamat](https://technet.microsoft.com/en-us/library/eea1dace-3913-4dbd-b659-5a94a610eee1)
- [Invoke-Command](https://technet.microsoft.com/en-us/library/22fd98ba-1874-492e-95a5-c069467b8462)
