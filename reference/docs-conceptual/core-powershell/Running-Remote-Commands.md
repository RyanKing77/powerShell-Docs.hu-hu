---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Távoli parancsok futtatása"
ms.assetid: d6938b56-7dc8-44ba-b4d4-cd7b169fd74d
ms.openlocfilehash: 5cf9690b8fe4549a99186f172cb6f0de156a4dea
ms.sourcegitcommit: c5251755c4442487f99ff74fadf7e37bbf039089
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/18/2017
---
# <a name="running-remote-commands"></a>Távoli parancsok futtatása
A parancsokat egy vagy több száz számítógép egyetlen Windows PowerShell-parancsot. A Windows PowerShell támogatja a távoli számítási különböző technológiákkal, például WMI, RPC és WS-Management használatával.

## <a name="remoting-without-configuration"></a>Távelérési konfiguráció nélkül
Számos Windows PowerShell-parancsmagok a ComputerName paraméterre, amely lehetővé teszi az adatok gyűjtéséhez és módosíthatja a beállításokat egy vagy több távoli számítógépeken van. Számos különböző kommunikációs technológiák és számos munkahelyi használata az összes Windows operációs rendszeren, amely a Windows PowerShell támogatja a Speciális konfiguráció nélkül.

Ezek a parancsmagok a következők:
* [Indítsa újra a számítógépet](https://go.microsoft.com/fwlink/?LinkId=821625)
* [Kapcsolat tesztelése](https://go.microsoft.com/fwlink/?LinkId=821646)
* [Az eseménynaplóban törlése](https://go.microsoft.com/fwlink/?LinkId=821568)
* [Get-Eseménynapló](https://go.microsoft.com/fwlink/?LinkId=821585)
* [Get-gyorsjavítás](https://go.microsoft.com/fwlink/?LinkId=821586)
  - [Get-Process](https://go.microsoft.com/fwlink/?linkid=821590)
* [Get-szolgáltatás](https://go.microsoft.com/fwlink/?LinkId=821593)
* [Szolgáltatás beállítása](https://go.microsoft.com/fwlink/?LinkId=821633)
* [Get-WinEvent parancsmaggal](https://go.microsoft.com/fwlink/?linkid=821529)
* [Get-WmiObject](https://go.microsoft.com/fwlink/?LinkId=821595)

Speciális konfiguráció nélkül távelérése támogató parancsmagok általában a ComputerName paraméterrel, és a munkamenet-paraméter nem rendelkezik. Ezeket a parancsmagokat a munkamenetben, írja be:

```
Get-Command | where { $_.parameters.keys -contains "ComputerName" -and $_.parameters.keys -notcontains "Session"}
```

## <a name="windows-powershell-remoting"></a>A Windows PowerShell-távelérés
A Windows PowerShell-távelérést, a WS-Management protokollt használja, amely lehetővé teszi, hogy egy vagy több távoli számítógépeken bármely Windows PowerShell-parancs futtatása. Lehetővé teszi az állandó kapcsolatot létrehozni, 1:1 interaktív munkamenetek indításához és parancsfájlok futtatása több számítógépen.

A Windows PowerShell távoli eljáráshívás használatához a távoli számítógép távoli kezelési be kell állítani. További információt, beleértve az utasításokat, lásd: [távoli követelmények](https://technet.microsoft.com/en-us/library/dd315349.aspx).

Miután konfigurálta a Windows PowerShell-távelérést, sok távelérési stratégia a következő elérhető. Ez a dokumentum tovább részében csak néhány őket a sorolja fel. További információkért lásd: [kapcsolatos távoli](https://technet.microsoft.com/en-us/library/dd347744.aspx) és [távoli GYIK](https://technet.microsoft.com/en-us/library/dd347744.aspx).

### <a name="start-an-interactive-session"></a>Egy interaktív munkamenet indítása
Egy távoli számítógéppel egy interaktív munkamenet indításához használja a [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) parancsmag.
Például a kiszolgalo01 távoli számítógéppel egy interaktív munkamenet elindításához írja be:

```
Enter-PSSession Server01
```

A parancssor módosításai jeleníti meg, amely csatlakozik a számítógép nevét. Ettől a távoli számítógépen futó parancsok, amely parancssorába írja be, és az eredmények jelennek meg a helyi számítógépen.

Az interaktív munkamenet befejezéséhez írja be:

```
Exit-PSSession
```

A Enter-PSSession és kilépési-PSSession parancsmag kapcsolatos további információkért lásd: [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) és [kilépési-PSSession](https://go.microsoft.com/fwlink/?LinkID=821478).

### <a name="run-a-remote-command"></a>Távoli parancs futtatása
Egy vagy több távoli számítógépeken bármely parancs futtatásához használja a [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493) parancsmag.
Ahhoz például, hogy futtassa egy [Get-UICulture](https://go.microsoft.com/fwlink/?LinkId=821806) parancsot a kiszolgalo01 és Server02 távoli számítógépeken, típus:

```
Invoke-Command -ComputerName Server01, Server02 -ScriptBlock {Get-UICulture}
```

A kimenetet visszaadja a számítógépre.

```
LCID    Name     DisplayName               PSComputerName
----    ----     -----------               --------------
1033    en-US    English (United States)   server01.corp.fabrikam.com
1033    en-US    English (United States)   server02.corp.fabrikam.com
```
Az Invoke-Command parancsmaggal kapcsolatos további információkért lásd: [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).

### <a name="run-a-script"></a>Parancsfájl futtatása
Parancsprogram futtatása egy vagy több távoli számítógépet, használja az Invoke-Command parancsmaggal FilePath paraméterében. A parancsfájl vagy a helyi számítógép által elérhető kell lennie. Az eredmény akkor minősül, a helyi számítógépen.

Például a következő parancsot a DiskCollect.ps1 parancsfájlt futtatja a kiszolgalo01 és Server02 távoli számítógépeken.

```
Invoke-Command -ComputerName Server01, Server02 -FilePath c:\Scripts\DiskCollect.ps1
```

Az Invoke-Command parancsmaggal kapcsolatos további információkért lásd: [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).

### <a name="establish-a-persistent-connection"></a>Állandó kapcsolatot létesíteni
Kapcsolódó parancsokat, amelyek közös adatok futtatásához hozzon létre egy munkamenetet a távoli számítógépen, és az Invoke-Command parancsmaggal futtassa a parancsokat az Ön által létrehozott munkamenetben. Távoli munkamenet létrehozása a New-PSSession parancsmag használható.

Például a következő parancs létrehoz egy távoli munkamenet a kiszolgalo01 számítógépre és egy másik távoli munkamenet Server02 számítógépen. A munkamenet-objektumok a $s változóban menti.

```
$s = New-PSSession -ComputerName Server01, Server02
```

Most, hogy a munkamenet jött létre, bennük valamelyik parancsának is futtathatja. És a munkameneteket állandó, mert egy parancs az adatgyűjtés, és a következő parancsot használhatja.

Például a következő parancsot a Get-gyorsjavítás parancsot futtatja, a $s változóban munkamenetekben, és az eredményeket a $h változóban menti. A $h változó minden $s munkamenetekben létrejött, de nem létezik a helyi munkamenetben.

```
Invoke-Command -Session $s {$h = Get-HotFix}
```

Most már használhatja az adatokat a következő parancsok, például a következő $h változót. Az eredmények jelennek meg a helyi számítógépen.

```
Invoke-Command -Session $s {$h | where {$_.InstalledBy -ne "NTAUTHORITY\SYSTEM"}}
```

### <a name="advanced-remoting"></a>Speciális távelérés
A Windows PowerShell távoli felügyeleti csak itt kezdődik. A telepített Windows PowerShell parancsmagok segítségével létrehozása és konfigurálása mindkét távoli munkamenetek a helyi és távoli véget ér, a testre szabott és korlátozott-munkameneteket hozzon létre engedélyezése a felhasználók parancsok importálása egy távoli munkamenetet, amely futtatja ténylegesen implicit módon adja meg a távoli munkamenet azt a távoli munkamenetet, és még sok más biztonságát.

Lehetővé teszi a távoli konfiguráció, a Windows PowerShell a WSMan-szolgáltató foglal magában. A WSMAN: a meghajtó a szolgáltató által létrehozott lehetővé teszi haladjon végig a konfigurációs beállításokat a helyi számítógépen és a távoli számítógépek hierarchiáját.
A WSMan-szolgáltató kapcsolatos további információkért lásd: [WSMan szolgáltató](https://technet.microsoft.com/en-us/library/dd819476.aspx) és [WS-Management parancsmagok](https://technet.microsoft.com/en-us/library/dd819481.aspx), vagy a Windows PowerShell-konzolban, írja be a "Get-Help wsman".

További információ:
- [Kapcsolatos távoli – gyakori kérdések](https://technet.microsoft.com/en-us/library/dd315359.aspx)
- [Register-PSSessionConfiguration](https://go.microsoft.com/fwlink/?LinkId=821508)
- [Import-PSSession](https://go.microsoft.com/fwlink/?LinkId=821821)

Távoli eljáráshívás hibákkal kapcsolatban lásd: [about_Remote_Troubleshooting](https://technet.microsoft.com/en-us/library/dd347642.aspx).

## <a name="see-also"></a>Lásd még:
- [about_Remote](https://technet.microsoft.com/en-us/library/9b4a5c87-9162-4adf-bdfe-fbc80b9b8970)
- [about_Remote_FAQ](https://technet.microsoft.com/en-us/library/e23702fd-9415-4a98-9975-390a4d3adc42)
- [about_Remote_Requirements](https://technet.microsoft.com/en-us/library/da213949-134c-4741-b307-81f4492ba1bd)
- [about_Remote_Troubleshooting](https://technet.microsoft.com/en-us/library/2f890148-8578-49ed-85ea-79a489dd6317)
- [about_PSSessions](https://technet.microsoft.com/en-us/library/7a9b4e0e-fa1b-47b0-92f6-6e2995d70acb)
- [about_WS-Management_Cmdlets](https://technet.microsoft.com/en-us/library/6ed3370a-ea10-45a5-9493-696aeace27ed)
- [Invoke-Command parancsot](https://go.microsoft.com/fwlink/?LinkId=821493)
- [Import-PSSession](https://go.microsoft.com/fwlink/?LinkId=821821)
- [Új-PSSession](https://go.microsoft.com/fwlink/?LinkId=821498)
- [Register-PSSessionConfiguration](https://go.microsoft.com/fwlink/?LinkId=821508)
- [A WSMan-szolgáltató](https://technet.microsoft.com/en-us/library/66fe1241-e08f-49ca-832f-a84c33ca8735)
