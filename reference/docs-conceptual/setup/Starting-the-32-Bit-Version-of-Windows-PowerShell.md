---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A Windows PowerShell 32 bites verziójának indítása"
ms.assetid: 12b31890-2609-4a76-8c24-0ebe78084f50
ms.openlocfilehash: d682ce45ebc92cda3a9008ab608bacf9ef8eba57
ms.sourcegitcommit: 18e3bfae83ffe282d3fd1a45f5386f3b7250f0c0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/08/2018
---
# <a name="starting-the-32-bit-version-of-windows-powershell"></a>A 32 bites Windows PowerShell elindítása
Ha egy 64 bites számítógépen, telepítse a Windows PowerShell **Windows PowerShell (x86)**, egy 32 bites Windows PowerShell mellett a 64 bites verziója telepítve van. Amikor futtatja a Windows PowerShell, a 64 bites alapértelmezés szerint fut.

Azonban előfordulhat, hogy időnként futtatásához szükséges **Windows PowerShell (x86)**, például egy modul használata esetén, amely 32 bites verziója szükséges hozzá, vagy ha távolról csatlakozik egy 32 bites számítógépen.

Egy 32 bites Windows PowerShell indításához használja az alábbi eljárások valamelyikét.

#### <a name="in-windows-server-2012-r2"></a>In Windows Server® 2012 R2

- Az a **Start** írja be **Windows PowerShell (x86)**. Kattintson a **Windows PowerShell x86** csempére.

- A **Kiszolgálókezelő**, az a **eszközök** menüjében válassza **Windows PowerShell (x86)**.

- Az asztalon vigye a mutatót a jobb felső sarokban, kattintson a **keresési**, típus **PowerShell x86** majd **Windows PowerShell (x86)**.

- A parancssorból írja be:`%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-server-2012"></a>In Windows Server® 2012

- Az a **Start** írja be **PowerShell** majd **Windows PowerShell (x86)**.

- A **Kiszolgálókezelő**, az a **eszközök** menüjében válassza **Windows PowerShell (x86)**.

- Az asztalon vigye a mutatót a jobb felső sarokban, kattintson a **keresési**, típus **PowerShell** majd **Windows PowerShell (x86)**.

- A parancssorból írja be:`%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-81"></a>A Windows® 8.1

- Az a **Start** írja be **Windows PowerShell (x86)**. Kattintson a **Windows PowerShell x86** csempére.

- Ha futtatja [távoli kiszolgálófelügyelet eszközei](http://go.microsoft.com/fwlink/?LinkID=304145) a Windows 8.1, nyissa meg a Windows PowerShell x86 a a **Server ManagerTools** menü. Válassza ki **Windows PowerShell (x86)**.

- Az asztalon vigye a mutatót a jobb felső sarokban, kattintson a **keresési**, típus **PowerShell x86** majd **Windows PowerShell (x86)**.
   
- A parancssorból írja be:`%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-8"></a>In Windows® 8

- A a **Start** képernyőn, a kurzor jobb felső sarokban, kattintson a **beállítások**, kattintson a **Csempék**, és anélkül helyezhet át a **felügyeleti eszközök megjelenítése** Igen csúszkát. Írja be, **PowerShell** kattintson **Windows PowerShell (x86)**.

- Ha futtatja [távoli kiszolgálófelügyelet eszközei](http://www.microsoft.com/download/details.aspx?id=28972) a Windows 8, nyissa meg a Windows PowerShell x86 a a **Server ManagerTools** menü. Válassza ki **Windows PowerShell (x86)**.

- A a **Start** képernyő vagy az asztal, írja be a **PowerShell (x86)** , majd **Windows PowerShell (x86)**.

- A parancssorból írja be:`%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

