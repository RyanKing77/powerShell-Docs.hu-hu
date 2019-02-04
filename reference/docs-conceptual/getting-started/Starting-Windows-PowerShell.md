---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: A Windows PowerShell indítása
ms.assetid: 59b649a2-c90c-4cf4-bf95-a740c59148e7
ms.openlocfilehash: 9184e8b0e508610e7f4775f1032f3a69c93bb8c1
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688321"
---
# <a name="starting-windows-powershell"></a>A Windows PowerShell indítása
PowerShell parancsfájl-kezelési motor dll, amely több gazdagép be lesz ágyazva az.  A leggyakoribb gazdagépet meg fogja kezdeni a következők: interaktív a PowerShell.exe parancssori és az interaktív parancsfájl-kezelési környezet PowerShell_ISE.exe.

A Windows Server® 2012 R2, Windows® 8.1, Windows Server 2012 és Windows 8 Windows PowerShell® indításához lásd: [általános felügyeleti feladatok és navigáció](https://technet.microsoft.com/library/hh831491.aspx).

## <a name="how-to-start-windows-powershell-on-earlier-versions-of-windows"></a>Windows PowerShell indítása a Windows korábbi verzióin

Ez a szakasz ismerteti a Windows PowerShell és a Windows PowerShell integrált parancsfájl-kezelési környezet (ISE) indítása a Windows® 7, Windows Server® 2008 R2 és Windows Server® 2008. Azt is bemutatja, hogyan engedélyezhető a választható szolgáltatás Windows PowerShell ISE-ben a Windows PowerShell 2.0 a Windows Server® 2008 R2 és Windows Server® 2008.

Az alábbi módszerek bármelyikét használatával indítsa el a Windows PowerShell 3.0 vagy a Windows PowerShell 4.0-s verzióját, ha vannak ilyenek.

#### <a name="from-the-start-menu"></a>A Start menüből

- Kattintson a **Start**, típus **PowerShell**, és kattintson a **Windows PowerShell**.
- A a **Start** menüben kattintson **Start**, kattintson a **minden program**, kattintson a **Kellékek**, kattintson a **Windows PowerShell**  mappát, és kattintson **Windows PowerShell**.

#### <a name="at-the-command-prompt"></a>A parancssorban

A Cmd.exe, a Windows PowerShell vagy a Windows PowerShell ISE-t indítsa el a Windows Powershellt, írja be:

```
PowerShell
```

A paraméterek a PowerShell.exe program segítségével testre szabhatja a munkamenetet. További információkért lásd: [PowerShell.exe parancssori súgója](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).

#### <a name="with-administrative-privileges-run-as-administrator"></a>A felügyeleti jogosultságok ("Futtatás rendszergazdaként")

Kattintson a **Start**, típus **PowerShell**, kattintson a jobb gombbal **Windows PowerShell**, és kattintson a **Futtatás rendszergazdaként**.

## <a name="how-to-start-windows-powershell-ise-on-earlier-releases-of-windows"></a>A Windows korábbi verzióiban elindítása a Windows PowerShell ISE-ben

Az alábbi módszerek bármelyikét használatával indítsa el a Windows PowerShell ISE-ben.

#### <a name="from-the-start-menu"></a>A Start menüből

- Kattintson a **Start**, típus **ISE**, és kattintson a **Windows PowerShell ISE-ben**.
- A a **Start** menüben kattintson **Start**, kattintson a **minden program**, kattintson a **Kellékek**, kattintson a **Windows PowerShell**  mappát, és kattintson **Windows PowerShell ISE-ben**.

#### <a name="at-the-command-prompt"></a>A parancssorban

A Cmd.exe, a Windows PowerShell vagy a Windows PowerShell ISE-t indítsa el a Windows Powershellt, írja be:

```
PowerShell_ISE
```

vagy a

```
ISE
```

#### <a name="with-administrative-privileges-run-as-administrator"></a>A felügyeleti jogosultságok ("Futtatás rendszergazdaként")

Kattintson a **Start**, típus **ISE**, kattintson a jobb gombbal **Windows PowerShell ISE-ben**, és kattintson a **Futtatás rendszergazdaként**.

## <a name="how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows"></a>Windows PowerShell ISE-ben a Windows korábbi verzióiban engedélyezése

A Windows PowerShell 4.0-s és a Windows PowerShell 3.0-s Windows PowerShell ISE-ben alapértelmezés szerint engedélyezve van Windows összes verzióján. Ha ez nem engedélyezett, Windows Management Framework 4.0 vagy a Windows Management Framework 3.0 lehetővé teszi, hogy azt.

A Windows PowerShell 2.0, Windows PowerShell ISE-ben alapértelmezés szerint engedélyezve van a Windows 7. Azonban a Windows Server 2008 R2 és Windows Server 2008, egy nem kötelező funkciót.

Ahhoz, hogy a Windows PowerShell ISE-ben a Windows PowerShell 2.0 a Windows Server 2008 R2 vagy Windows Server 2008, az alábbi eljárással.

#### <a name="to-enable-windows-powershell-integrated-scripting-environment-ise"></a>Windows PowerShell integrált parancsfájl-kezelési környezet (ISE) engedélyezése

1. Indítsa el a Kiszolgálókezelőt.
2. Kattintson a **funkciók** majd **szolgáltatások hozzáadása**.
3. A szolgáltatások kiválasztása párbeszédpanelen kattintson a Windows PowerShell integrált parancsfájl-kezelési környezet (ISE).

## <a name="starting-the-32-bit-version-of-windows-powershell"></a>A Windows PowerShell 32 bites verziójának indítása

Ha egy 64 bites számítógépen Windows PowerShell telepítése **Windows PowerShell (x86)**, egy Windows PowerShell 32 bites verziója van telepítve, mellett a 64 bites verziót. Amikor futtatja a Windows PowerShell, a 64 bites verziót futtatja, alapértelmezés szerint.

Azonban néha szüksége lehet futtatni **Windows PowerShell (x86)**, például a modul használata esetén, amelyek 32 bites verzióját igényli, vagy ha távolról csatlakozik egy 32 bites számítógépen.

Egy Windows PowerShell 32 bites verziójának indítása, használja az alábbi eljárások valamelyikét.

#### <a name="in-windows-server-2012-r2"></a>A Windows Server® 2012 R2-ben

- Az a **Start** írja be **Windows PowerShell (x86)**. Kattintson a **Windows PowerShell x86** csempére.
- A **Kiszolgálókezelő**, az a **eszközök** menüjében válassza **Windows PowerShell (x86)**.
- Az asztalon vigye a kurzort a jobb felső sarokban, kattintson **keresési**, típus **PowerShell x86** majd **Windows PowerShell (x86)**.
- A parancssorban adja meg: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-server-2012"></a>A Windows Server® 2012

- Az a **Start** írja be **PowerShell** majd **Windows PowerShell (x86)**.
- A **Kiszolgálókezelő**, az a **eszközök** menüjében válassza **Windows PowerShell (x86)**.
- Az asztalon vigye a kurzort a jobb felső sarokban kattintson **keresési**, típusa **PowerShell** majd **Windows PowerShell (x86)**.
- A parancssorban adja meg: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-81"></a>A 8.1-es Windows®

- Az a **Start** írja be **Windows PowerShell (x86)**. Kattintson a **Windows PowerShell x86** csempére.
- Ha futtatja [távoli kiszolgálófelügyelet eszközei](https://go.microsoft.com/fwlink/?LinkID=304145) for Windows 8.1, szintén nyissa meg a Windows PowerShell x86 a a **kiszolgáló ManagerTools** menü.
  Válassza ki **Windows PowerShell (x86)**.
- Az asztalon vigye a kurzort a jobb felső sarokban, kattintson **keresési**, típus **PowerShell x86** majd **Windows PowerShell (x86)**.
- A parancssorban adja meg: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-8"></a>A 8 Windows®

- A a **Start** képernyőn, vigye a kurzort a jobb felső sarokban, kattintson a **beállítások**, kattintson a **Csempék**, és helyezze a **felügyeleti eszközök megjelenítése** csúszka igen. Ezután írja be a **PowerShell** kattintson **Windows PowerShell (x86)**.
- Ha futtatja [távoli kiszolgálófelügyelet eszközei](https://www.microsoft.com/download/details.aspx?id=28972) Windows 8, is nyissa meg a Windows Powershellt x86 származó a **kiszolgáló ManagerTools** menü. Válassza ki **Windows PowerShell (x86)**.
- A a **Start** képernyőt vagy a desktopban, és írja be a **PowerShell (x86)** és kattintson a **Windows PowerShell (x86)**.
- A parancssorban adja meg: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`