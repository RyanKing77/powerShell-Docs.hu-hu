---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: A Windows PowerShell 2.0 motor
ms.assetid: edafc2fa-7576-49c2-bbba-9336f4bcfc28
ms.openlocfilehash: 88d4374891e38501f6bbcd0793c86692eaed2f22
ms.sourcegitcommit: 3720ce4efb6735694cfb53a1b793d949af5d1bc5
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/29/2017
---
# <a name="starting-the-windows-powershell-20-engine"></a>A Windows PowerShell 2.0 motor
Ez a szakasz ismerteti, hogyan kell elindítani a Windows PowerShell 2.0 motor a Windows 8.1, Windows Server 2012 R2, Windows 8 és Windows Server 2012, többek között a Windows PowerShell 2.0 motor, és más rendszerek mely Windows PowerShell 2.0, a Windows PowerShell 3.0 és a Windows PowerShell 4.0-s verzióját telepíti.

Visszafelé kompatibilis a Windows PowerShell 2.0 a Windows PowerShell 4.0-s verzióját és a Windows PowerShell 3.0 tervezték. Parancsmagok, szolgáltatók, beépülő modulok, modulok és a Windows PowerShell 2.0 parancsfájlokat futtassa a Windows PowerShell 4.0-s verzióját és a Windows PowerShell 3.0 változatlan. Azonban módosulásának eredményeképpen a futásidejű aktiválási házirend a Microsoft .NET-keretrendszer 4-es, Windows PowerShell gazdagépre programok az Windows PowerShell 2.0-s verziójához és a közös nyelvi futtatókörnyezet (CLR) 2.0 fordítása nem futtatható a Windows rendszerben módosítás nélkül A PowerShell 3.0 vagy a Windows PowerShell 4.0, amelyek a közös nyelvi futtató környezet 4.0-s fordításának. A Windows PowerShell 2.0 motor kívánják használni, ha egy meglévő parancsfájl vagy a gazdagép program nem futtatható, mert nem kompatibilis a Windows PowerShell 4.0-s verzióját, a Windows PowerShell 3.0 vagy a Microsoft .NET-keretrendszer 4. Ilyen esetekben várhatóan ritkán fordul elő.

A Windows PowerShell 2.0 motor igénylő sok programok indítsa el automatikusan. Ezek az utasítások megtalálhatók a ritka helyzetekben, ahol kell elindítania a motor manuálisan.

## <a name="installing-and-enabling-required-programs"></a>Telepíti és engedélyezi a szükséges programok
A Windows PowerShell 2.0 motor megkezdése előtt a Windows PowerShell 2.0 motor és a Microsoft .NET-keretrendszer 3.5 Service Pack 1 engedélyezése. Útmutatásért lásd: [Windows PowerShell telepítése](Installing-Windows-PowerShell.md).

Rendszerek, amelyeken [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881) vagy a Windows Management Framework 3.0 telepítve vannak az összes szükséges összetevőt. További beállításokra nincs is szükség. További információ [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881) vagy a Windows Management Framework 3.0, lásd: [Windows PowerShell telepítése](Installing-Windows-PowerShell.md).

## <a name="how-to-start-the-windows-powershell-20-engine"></a>A Windows PowerShell 2.0 motor indítása
Ha a Windows PowerShell elindítása a legújabb verzió alapértelmezés szerint elindul. A Windows PowerShell 2.0 motor Windows PowerShell indításához használja a PowerShell.exe verzió paramétere. A parancsot a parancssorba, beleértve a Windows PowerShell és a Cmd.exe.

```
PowerShell.exe -Version 2
```

## <a name="how-to-start-a-remote-session-with-the-windows-powershell-20-engine"></a>A távoli munkamenet indítása a Windows PowerShell 2.0 motor
Futtassa a Windows PowerShell 2.0 motor egy távoli munkamenetben, a távoli számítógépen, amely betölti a Windows PowerShell 2.0 motor hozzon létre egy munkamenet-konfiguráció (más néven "végpont"). A munkamenet-konfiguráció a távoli számítógépre menti, és segítségével hitelesített felhasználó számára, amelyek a Windows PowerShell 2.0 motor-munkameneteket hozzon létre.

Ez az egy speciális feladat általában a rendszergazda által végrehajtott műveletek.

A következő eljárás használja a **PSVersion** paramétere a [Register-PSSessionConfiguration](https://technet.microsoft.com/en-us/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) parancsmaggal hozzon létre egy munkamenet-konfiguráció, amely a Windows PowerShell 2.0 motor használja. Használhatja a **PowerShellVersion** paramétere a [New-PSSessionConfigurationFile](https://technet.microsoft.com/en-us/library/5f3e3633-6e90-479c-aea9-ba45a1954866) parancsmaggal hozzon létre egy munkamenet-konfigurációs fájlt egy munkamenet esetében, amelyek a Windows PowerShell 2.0 motor betölti és használhatja a **PSVersion** paramétere a [Set-PSSessionConfiguration](https://technet.microsoft.com/en-us/library/b21fbad3-1759-4260-b206-dcb8431cd6ea) paraméter használata a Windows PowerShell 2.0 motor egy munkamenet-konfiguráció módosításához.

Munkamenet-konfiguráció fájlokkal kapcsolatos további információkért lásd: [about_Session_Configuration_Files](https://technet.microsoft.com/en-us/library/c7217447-1ebf-477b-a8ef-4dbe9a1473b8). További információ a munkamenet-konfigurációkkal, például a telepítési és a biztonság érdekében: [about_session_configuration_files [v4]](https://technet.microsoft.com/en-us/library/a2fbe12a-350c-4d04-be50-24102824e3ab).

#### <a name="to-start-a-remote-windows-powershell-20-session"></a>A Windows PowerShell 2.0 távoli munkamenet indításához

1. A munkamenet-konfiguráció, amelyhez a Windows PowerShell 2.0 motor létrehozásához használja a **PSVersion** paramétere a [Register-PSSessionConfiguration](https://technet.microsoft.com/en-us/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) parancsmag "2.0" értékű. Ez a parancs futtatása a számítógépen a "server side" vagy a fogadó oldalon a kapcsolat.

    A következő minta parancs PS2 munkamenet-konfigurációt a kiszolgalo01 számítógépen hoz létre. A parancs futtatásához, indítsa el a Windows PowerShell 4.0-s vagy Windows PowerShell 3.0 a **Futtatás rendszergazdaként** lehetőséget.

    ```
    Register-PSSessionConfiguration -Name PS2 -PSVersion 2.0
    ```

2. A munkamenet létrehozásához a kiszolgalo01 számítógépen, amely a PS2 munkamenet-konfigurációt használ, használja a **ConfigurationName** parancsmag-készlettel hozzon létre például egy távoli munkamenet paraméter a [New-PSSession](https://technet.microsoft.com/en-us/library/76f6628c-054c-4eda-ba7a-a6f28daaa26f) parancsmag.

    A munkamenet-konfigurációt használó munkamenet akkor kezdődik, amikor a Windows PowerShell 2.0 motor automatikusan betöltődik abba a munkamenetbe.

    A következő parancsot egy munkamenet indítása a kiszolgalo01 számítógépen, amely a PS2 munkamenet-konfigurációt használ. A parancs a munkamenet a $s változóban menti.

    ```
    $s = New-PSSession -ComputerName Server01 -ConfigurationName PS2
    ```

## <a name="how-to-start-a-background-job-with-the-windows-powershell-20-engine"></a>A háttérben futó feladat indítása a Windows PowerShell 2.0 motor
A Windows PowerShell 2.0 motor egy háttérben történő feldolgozás indításához használja a **PSVersion** paramétere a [indítási-feladat](https://technet.microsoft.com/en-us/library/2bc04935-0deb-4ec0-b856-d7290cca6442) parancsmag.

A következő parancsot egy háttérben történő feldolgozás kezdődik-e a Windows PowerShell 2.0 motor

```
Start-Job {Get-Process} -PSVersion 2.0
```

További információ a feladatok a háttérben: [about_Jobs [v4]](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_jobs?view=powershell-4.0).

