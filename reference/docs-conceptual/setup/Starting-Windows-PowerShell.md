---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: A Windows PowerShell indítása
ms.assetid: 59b649a2-c90c-4cf4-bf95-a740c59148e7
ms.openlocfilehash: b56ddc2f577225646729b99f3a2abcb8cc60d307
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30953123"
---
# <a name="starting-windows-powershell"></a>A Windows PowerShell indítása
PowerShell egy parancsfájl-kezelési motor dll, amely több gazdagép be van ágyazva.  A leggyakrabban használt állomás hozzákezdhet a következők: interaktív parancssori PowerShell.exe és parancsfájl-kezelési környezet interaktív PowerShell_ISE.exe.

A Windows Server® 2012 R2, Windows® 8.1, Windows Server 2012 és Windows 8 Windows PowerShell® elindításához lásd: [általános kezelési feladatok és navigáció](http://technet.microsoft.com/library/hh831491.aspx).

## <a name="how-to-start-windows-powershell-on-earlier-versions-of-windows"></a>A Windows korábbi verzióiban Windows PowerShell indítása

Ez a szakasz ismerteti, hogyan kell elindítani a Windows PowerShell és a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) a Windows® 7, Windows Server® 2008 R2 és Windows Server® 2008. A választható szolgáltatás engedélyezése a Windows PowerShell 2.0 a Windows Server® 2008 R2 és Windows Server® 2008 a Windows PowerShell ISE is ismerteti.

A következő módszerekkel segítségével adott esetben indítsa el a Windows PowerShell 3.0 vagy a Windows PowerShell 4.0-s verzióját.

#### <a name="from-the-start-menu"></a>A Start menüből

- Kattintson a **Start**, típus **PowerShell**, és kattintson a **Windows PowerShell**.
- A a **Start** menüben kattintson **Start**, kattintson **minden program**, kattintson a **Kellékek**, kattintson a **Windows PowerShell**  mappa, és kattintson **Windows PowerShell**.

#### <a name="at-the-command-prompt"></a>A parancssorba

A Cmd.exe, a Windows PowerShell vagy a Windows PowerShell ISE indítsa el a Windows Powershellt, írja be:

```
PowerShell
```

A paraméterek a PowerShell.exe program segítségével testre szabhatja a munkamenet. További információkért lásd: [PowerShell.exe parancssori súgó](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).

#### <a name="with-administrative-privileges-run-as-administrator"></a>A felügyeleti jogosultságok ("Futtatás rendszergazdaként")

Kattintson a **Start**, típus **PowerShell**, kattintson a jobb gombbal **Windows PowerShell**, és kattintson a **Futtatás rendszergazdaként**.

## <a name="how-to-start-windows-powershell-ise-on-earlier-releases-of-windows"></a>A Windows PowerShell ISE indítása a Windows operációs rendszerek régebbi kiadásaiban

A Windows PowerShell ISE elindításához használja a következő módszerekkel.

#### <a name="from-the-start-menu"></a>A Start menüből

- Kattintson a **Start**, típus **ISE**, és kattintson a **Windows PowerShell ISE**.
- A a **Start** menüben kattintson **Start**, kattintson **minden program**, kattintson a **Kellékek**, kattintson a **Windows PowerShell**  mappa, és kattintson **Windows PowerShell ISE**.

#### <a name="at-the-command-prompt"></a>A parancssorba

A Cmd.exe, a Windows PowerShell vagy a Windows PowerShell ISE indítsa el a Windows Powershellt, írja be:

```
PowerShell_ISE
```

vagy a

```
ISE
```

#### <a name="with-administrative-privileges-run-as-administrator"></a>A felügyeleti jogosultságok ("Futtatás rendszergazdaként")

Kattintson a **Start**, típus **ISE**, kattintson a jobb gombbal **Windows PowerShell ISE**, és kattintson a **Futtatás rendszergazdaként**.

## <a name="how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows"></a>A Windows korábbi verzióiban Windows PowerShell ISE engedélyezése

A Windows PowerShell 4.0-s verzióját és a Windows PowerShell 3.0, a Windows PowerShell ISE alapértelmezés szerint engedélyezve van a Windows összes verzióján. Ha már nincs engedélyezve, a Windows Management Framework 4.0 vagy a Windows Management Framework 3.0 engedélyezi.

A Windows PowerShell 2.0 a Windows PowerShell ISE alapértelmezés szerint engedélyezve van a Windows 7. Azonban a Windows Server 2008 R2 és Windows Server 2008, akkor választható lehetőség.

Ahhoz, hogy a Windows PowerShell ISE a Windows PowerShell 2.0 a Windows Server 2008 R2 vagy Windows Server 2008, a következő eljárással.

#### <a name="to-enable-windows-powershell-integrated-scripting-environment-ise"></a>Ahhoz, hogy a Windows PowerShell integrált parancsfájl-kezelési környezet (ISE)

1. Indítsa el a Kiszolgálókezelőt.
2. Kattintson a **szolgáltatások** majd **szolgáltatások hozzáadása**.
3. A szolgáltatások kiválasztása párbeszédpanelen kattintson a Windows PowerShell integrált parancsfájlkezelési környezet (ISE).

## <a name="starting-the-32-bit-version-of-windows-powershell"></a>A 32 bites Windows PowerShell elindítása

Ha egy 64 bites számítógépen, telepítse a Windows PowerShell **Windows PowerShell (x86)**, egy 32 bites Windows PowerShell mellett a 64 bites verziója telepítve van. Amikor futtatja a Windows PowerShell, a 64 bites alapértelmezés szerint fut.

Azonban előfordulhat, hogy időnként futtatásához szükséges **Windows PowerShell (x86)**, például egy modul használata esetén, amely 32 bites verziója szükséges hozzá, vagy ha távolról csatlakozik egy 32 bites számítógépen.

Egy 32 bites Windows PowerShell indításához használja az alábbi eljárások valamelyikét.

#### <a name="in-windows-server-2012-r2"></a>In Windows Server® 2012 R2

- Az a **Start** írja be **Windows PowerShell (x86)**. Kattintson a **Windows PowerShell x86** csempére.
- A **Kiszolgálókezelő**, az a **eszközök** menüjében válassza **Windows PowerShell (x86)**.
- Az asztalon vigye a mutatót a jobb felső sarokban, kattintson a **keresési**, típus **PowerShell x86** majd **Windows PowerShell (x86)**.
- A parancssorból írja be: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-server-2012"></a>In Windows Server® 2012

- Az a **Start** írja be **PowerShell** majd **Windows PowerShell (x86)**.
- A **Kiszolgálókezelő**, az a **eszközök** menüjében válassza **Windows PowerShell (x86)**.
- Az asztalon vigye a mutatót a jobb felső sarokban, kattintson a **keresési**, típus **PowerShell** majd **Windows PowerShell (x86)**.
- A parancssorból írja be: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-81"></a>A Windows® 8.1

- Az a **Start** írja be **Windows PowerShell (x86)**. Kattintson a **Windows PowerShell x86** csempére.
- Ha futtatja [távoli kiszolgálófelügyelet eszközei](http://go.microsoft.com/fwlink/?LinkID=304145) a Windows 8.1, nyissa meg a Windows PowerShell x86 a a **Server ManagerTools** menü.
  Válassza ki **Windows PowerShell (x86)**.
- Az asztalon vigye a mutatót a jobb felső sarokban, kattintson a **keresési**, típus **PowerShell x86** majd **Windows PowerShell (x86)**.
- A parancssorból írja be: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-8"></a>In Windows® 8

- A a **Start** képernyőn, a kurzor jobb felső sarokban, kattintson a **beállítások**, kattintson a **Csempék**, és anélkül helyezhet át a **felügyeleti eszközök megjelenítése** Igen csúszkát. Írja be, **PowerShell** kattintson **Windows PowerShell (x86)**.
- Ha futtatja [távoli kiszolgálófelügyelet eszközei](http://www.microsoft.com/download/details.aspx?id=28972) a Windows 8, nyissa meg a Windows PowerShell x86 a a **Server ManagerTools** menü. Válassza ki **Windows PowerShell (x86)**.
- A a **Start** képernyő vagy az asztal, írja be a **PowerShell (x86)** , majd **Windows PowerShell (x86)**.
- A parancssorból írja be: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`