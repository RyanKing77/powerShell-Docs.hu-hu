---
ms.date: 08/14/2018
keywords: PowerShell, a parancsmag
title: Távoli parancsok futtatása
ms.assetid: d6938b56-7dc8-44ba-b4d4-cd7b169fd74d
ms.openlocfilehash: 2001b5509acde6ec4259bb1442944958a67aa66f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058913"
---
# <a name="running-remote-commands"></a>Távoli parancsok futtatása

Egy vagy több száz számítógépről, egyetlen PowerShell-paranccsal, futtathat parancsokat. Windows PowerShell támogatja a távoli számítógépek különböző technológiákkal, beleértve a WMI távoli Eljáráshívás és WS-Management használatával.

A PowerShell Core WMI, támogatja a WS-Management és az SSH-távelérésének lehetővé tétele. RPC már nem támogatott.

A távoli eljáráshívás a PowerShell Core kapcsolatos további információkért tekintse meg a következő cikkeket:

- [SSH távoli eljáráshívás a PowerShell Core][ssh-remoting]
- [A PowerShell Core a wsman által használt távoli eljáráshívás][wsman-remoting]

## <a name="windows-powershell-remoting-without-configuration"></a>Windows PowerShell távoli eljáráshívás konfiguráció nélkül

Számos Windows PowerShell-parancsmagok rendelkeznie a ComputerName paraméter, amely lehetővé teszi az adatok gyűjtéséhez és a egy vagy több távoli számítógépeken lévő beállítások módosításához. Ezek a parancsmagok különböző kommunikációs protokollokat használ, és az összes Windows operációs rendszeren külön konfigurálás nélkül működik.

Ezek a parancsmagok a következők:

- [Restart-Computer](/powershell/module/microsoft.powershell.management/restart-computer)
- [Test-Connection](/powershell/module/microsoft.powershell.management/test-connection)
- [CLEAR-Eseménynapló](/powershell/module/microsoft.powershell.management/clear-eventlog)
- [Get-EventLog](/powershell/module/microsoft.powershell.management/get-eventlog)
- [Get-HotFix](/powershell/module/microsoft.powershell.management/get-hotfix)
- [Get-Process](/powershell/module/microsoft.powershell.management/get-process)
- [Get-Service](/powershell/module/microsoft.powershell.management/get-service)
- [Set-Service](/powershell/module/microsoft.powershell.management/set-service)
- [Get-WinEvent](/powershell/module/microsoft.powershell.diagnostics/get-winevent)
- [Get-WmiObject](/powershell/module/microsoft.powershell.management/get-wmiobject)

Általában a távoli eljáráshívás külön konfigurálás nélkül támogató parancsmagok a ComputerName paraméterrel rendelkezik, és a munkamenet-paraméter nem rendelkezik. Ezeket a parancsmagokat a munkamenetben, írja be:

```powershell
Get-Command | where { $_.parameters.keys -contains "ComputerName" -and $_.parameters.keys -notcontains "Session"}
```

## <a name="windows-powershell-remoting"></a>Windows PowerShell távoli eljáráshívás

A WS-Management protokoll használatával, a Windows PowerShell távoli eljáráshívás lehetővé teszi egy vagy több távoli számítógépeken bármely Windows PowerShell-parancs futtatása. Állandó kapcsolatot, interaktív munkamenetek indításához és szkriptek futtatása távoli számítógépeken.

Windows PowerShell távoli eljáráshívás használatához konfigurálni kell a távoli számítógép távoli felügyeletére.
További információt, többek között az utasításokért lásd: [távoli követelmények](/powershell/module/microsoft.powershell.core/about/about_remote_requirements).

Miután konfigurálta a Windows PowerShell-táveléréssel, sok távoli eljáráshívás stratégiák lesznek elérhetők.
Ez a cikk ezek közül néhány sorolja fel. További információkért lásd: [kapcsolatos távoli](/powershell/module/microsoft.powershell.core/about/about_remote).

### <a name="start-an-interactive-session"></a>Az interaktív munkamenet indítása

Az interaktív munkamenet indításához és a egy távoli számítógépen használja a [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession) parancsmagot.
Írja be például a kiszolgalo01 távoli számítógépekkel az interaktív munkamenet indításához:

```powershell
Enter-PSSession Server01
```

A parancssor megváltozik a távoli számítógép neve jelenik meg. Minden olyan parancsokat, amelyek a parancssorba írja be a távoli számítógépen futtatja, és az eredmények jelennek meg a helyi számítógépen.

Az interaktív munkamenet befejezéséhez írja be:

```powershell
Exit-PSSession
```

Enter-PSSession és kilépési-PSSession-parancsmagokkal kapcsolatos további információkért lásd:

- [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession)
- [Exit-PSSession](/powershell/module/microsoft.powershell.core/exit-pssession)

### <a name="run-a-remote-command"></a>Távoli parancs futtatása

Egy vagy több számítógépet a parancs futtatásához használja a [Invoke-Command](/powershell/module/microsoft.powershell.core/invoke-command) parancsmagot. Futtassa például egy [Get-UICulture](/powershell/module/microsoft.powershell.utility/get-uiculture) parancsot a kiszolgalo01 és Server02 távoli számítógépeken, írja be:

```powershell
Invoke-Command -ComputerName Server01, Server02 -ScriptBlock {Get-UICulture}
```

A kimenetet visszaadja a számítógépen.

```output
LCID    Name     DisplayName               PSComputerName
----    ----     -----------               --------------
1033    en-US    English (United States)   server01.corp.fabrikam.com
1033    en-US    English (United States)   server02.corp.fabrikam.com
```

### <a name="run-a-script"></a>Parancsfájl futtatása

Parancsfájl futtatása egy vagy több távoli számítógépeken használja a fájl elérési útja paramétert, a `Invoke-Command` parancsmagot. A parancsfájl vagy elérhető-e a helyi számítógépen kell lennie. Az eredmény a helyi számítógépen.

Ha például a következő parancsot a DiskCollect.ps1 szkriptet futtat a távoli számítógépek kiszolgalo01 és Server02.

```powershell
Invoke-Command -ComputerName Server01, Server02 -FilePath c:\Scripts\DiskCollect.ps1
```

### <a name="establish-a-persistent-connection"></a>Állandó kapcsolatot létesíteni

Használja a `New-PSSession` parancsmaggal hozzon létre egy állandó munkamenetet egy távoli számítógépen. A következő példa távoli munkamenetek kiszolgalo01 és Server02 hoz létre. A munkamenet-objektumok vannak tárolva a `$s` változó.

```powershell
$s = New-PSSession -ComputerName Server01, Server02
```

Most, hogy a munkamenet jött létre, bármely parancsot futtathatja bennük. És mivel a munkamenet tartós, egy parancs adatokat gyűjteni, és azokat a egy másik parancs használja.

Például a következő parancsot a Get-HotFix parancsot futtatja, a foglalkozások a $s változóban, és az eredmények $h változóba menti. A $h változó jön létre az egyes $s munkamenetekben, de a helyi munkamenet nem létezik.

```powershell
Invoke-Command -Session $s {$h = Get-HotFix}
```

Most már használhatja az adatok a `$h` változó más parancsokkal ugyanabban a munkamenetben. Az eredmények jelennek meg a helyi számítógépen. Például:

```powershell
Invoke-Command -Session $s {$h | where {$_.InstalledBy -ne "NTAUTHORITY\SYSTEM"}}
```

### <a name="advanced-remoting"></a>Speciális távelérés

Windows PowerShell távoli felügyeleti csak itt kezdődik. A Windows PowerShell használatával telepített parancsmagokat használatával is létrehozni, valamint mindkét távoli munkamenetek a helyi és távoli véget ér, a hozzon létre személyre szabott és korlátozott munkamenet engedélyezése a felhasználóknak parancsok importálhat egy távoli munkamenetet, amely futtatja ténylegesen implicit módon a távoli munkamenetet a távoli munkamenetet, és még sok más biztonságát konfigurálja.

Windows PowerShell a wsman által használt szolgáltatót tartalmaz. A szolgáltató létrehoz egy `WSMAN:` meghajtó, amely lehetővé teszi a hierarchiájában a konfigurációs beállításokat a helyi számítógépen, és a távoli számítógépek közötti navigáláshoz.

A wsman által használt szolgáltató kapcsolatos további információkért lásd: [WSMan szolgáltató](https://technet.microsoft.com/library/dd819476.aspx) és [WS-Management-parancsmagok](/powershell/module/microsoft.powershell.core/about/about_ws-management_cmdlets), vagy írja be a Windows PowerShell-konzol `Get-Help wsman`.

További információ:

- [Tudnivalók a távoli – gyakori kérdések](https://technet.microsoft.com/library/dd315359.aspx)
- [Register-PSSessionConfiguration](https://go.microsoft.com/fwlink/?LinkId=821508)
- [Import-PSSession](https://go.microsoft.com/fwlink/?LinkId=821821)

Távoli eljáráshívás hibákkal kapcsolatos útmutatásért lásd: [about_Remote_Troubleshooting](https://technet.microsoft.com/library/dd347642.aspx).

## <a name="see-also"></a>Lásd még:

- [about_Remote](https://technet.microsoft.com/library/9b4a5c87-9162-4adf-bdfe-fbc80b9b8970)
- [about_Remote_FAQ](https://technet.microsoft.com/library/e23702fd-9415-4a98-9975-390a4d3adc42)
- [about_Remote_Requirements](https://technet.microsoft.com/library/da213949-134c-4741-b307-81f4492ba1bd)
- [about_Remote_Troubleshooting](https://technet.microsoft.com/library/2f890148-8578-49ed-85ea-79a489dd6317)
- [about_PSSessions](https://technet.microsoft.com/library/7a9b4e0e-fa1b-47b0-92f6-6e2995d70acb)
- [about_WS-Management_Cmdlets](https://technet.microsoft.com/library/6ed3370a-ea10-45a5-9493-696aeace27ed)
- [Invoke-Command](/powershell/module/microsoft.powershell.core/invoke-command)
- [Import-PSSession](https://go.microsoft.com/fwlink/?LinkId=821821)
- [New-PSSession](https://go.microsoft.com/fwlink/?LinkId=821498)
- [Register-PSSessionConfiguration](https://go.microsoft.com/fwlink/?LinkId=821508)
- [WSMan Provider](https://technet.microsoft.com/library/66fe1241-e08f-49ca-832f-a84c33ca8735)

[wsman-remoting]: WSMan-Remoting-in-PowerShell-Core.md
[ssh-remoting]: SSH-Remoting-in-PowerShell-Core.md