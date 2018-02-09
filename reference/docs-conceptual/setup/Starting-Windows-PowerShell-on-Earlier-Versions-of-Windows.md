---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A Windows PowerShell indítása a Windows korábbi verzióin"
ms.assetid: 57125436-3d1e-4e7f-b5c4-8f0ecb49d642
ms.openlocfilehash: 52e3acc1fd3009ecad3b7134008e38d4edfb5ca7
ms.sourcegitcommit: 18e3bfae83ffe282d3fd1a45f5386f3b7250f0c0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/08/2018
---
# <a name="starting-windows-powershell-on-earlier-versions-of-windows"></a>A Windows PowerShell indítása a Windows korábbi verzióin
Ez a szakasz ismerteti, hogyan kell elindítani a Windows PowerShell és a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) a Windows® 7, Windows Server® 2008 R2 és Windows Server® 2008. A választható szolgáltatás engedélyezése a Windows PowerShell 2.0 a Windows Server® 2008 R2 és Windows Server® 2008 a Windows PowerShell ISE is ismerteti.

A Windows PowerShell 4.0 telepítése támogatott rendszeren, töltse le és telepítse [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881). További információkért lásd: [Windows PowerShell telepítése](Installing-Windows-PowerShell.md).

Telepítse a Windows PowerShell 3.0 támogatott rendszeren, töltse le és telepítse [Windows Management Framework 3.0](http://go.microsoft.com/fwlink/?LinkID=240290). További információkért lásd: [Windows PowerShell telepítése](Installing-Windows-PowerShell.md).

## <a name="how-to-start-windows-powershell-on-earlier-versions-of-windows"></a>A Windows korábbi verzióiban Windows PowerShell indítása
A következő módszerekkel segítségével adott esetben indítsa el a Windows PowerShell 3.0 vagy a Windows PowerShell 4.0-s verzióját.

#### <a name="from-the-start-menu"></a>A Start menüből

- Kattintson a **Start**, típus **PowerShell**, és kattintson a **Windows PowerShell**.

- A a **Start** menüben kattintson **Start**, kattintson **minden program**, kattintson a **Kellékek**, kattintson a **Windows PowerShell**  mappa, és kattintson **Windows PowerShell**.

#### <a name="at-the-command-prompt"></a>A parancssorba

- A Cmd.exe, a Windows PowerShell vagy a Windows PowerShell ISE indítsa el a Windows Powershellt, írja be:

    ```
    PowerShell
    ```

    A paraméterek a PowerShell.exe program segítségével testre szabhatja a munkamenet. További információkért lásd: [PowerShell.exe parancssori súgó](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).

#### <a name="with-administrative-privileges-run-as-administrator"></a>A felügyeleti jogosultságok ("Futtatás rendszergazdaként")

1. Kattintson a **Start**, típus **PowerShell**, kattintson a jobb gombbal **Windows PowerShell**, és kattintson a **Futtatás rendszergazdaként**.

## <a name="how-to-start-windows-powershell-ise-on-earlier-releases-of-windows"></a>A Windows PowerShell ISE indítása a Windows operációs rendszerek régebbi kiadásaiban
A Windows PowerShell ISE elindításához használja a következő módszerekkel.

#### <a name="from-the-start-menu"></a>A Start menüből

- Kattintson a **Start**, típus **ISE**, és kattintson a **Windows PowerShell ISE**.

- A a **Start** menüben kattintson **Start**, kattintson **minden program**, kattintson a **Kellékek**, kattintson a **Windows PowerShell**  mappa, és kattintson **Windows PowerShell ISE**.

#### <a name="at-the-command-prompt"></a>A parancssorba

- A Cmd.exe, a Windows PowerShell vagy a Windows PowerShell ISE indítsa el a Windows Powershellt, írja be:

    ```
    PowerShell_ISE
    ```

    vagy a

    ```
    ISE
    ```

#### <a name="with-administrative-privileges-run-as-administrator"></a>A felügyeleti jogosultságok ("Futtatás rendszergazdaként")

1. Kattintson a **Start**, típus **ISE**, kattintson a jobb gombbal **Windows PowerShell ISE**, és kattintson a **Futtatás rendszergazdaként**.

## <a name="how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows"></a>A Windows korábbi verzióiban Windows PowerShell ISE engedélyezése
A Windows PowerShell 4.0-s verzióját és a Windows PowerShell 3.0, a Windows PowerShell ISE alapértelmezés szerint engedélyezve van a Windows összes verzióján. Ha már nincs engedélyezve, a Windows Management Framework 4.0 vagy a Windows Management Framework 3.0 engedélyezi.

A Windows PowerShell 2.0 a Windows PowerShell ISE alapértelmezés szerint engedélyezve van a Windows 7. Azonban a Windows Server 2008 R2 és Windows Server 2008, akkor választható lehetőség.

Ahhoz, hogy a Windows PowerShell ISE a Windows PowerShell 2.0 a Windows Server 2008 R2 vagy Windows Server 2008, a következő eljárással.

#### <a name="to-enable-windows-powershell-integrated-scripting-environment-ise"></a>Ahhoz, hogy a Windows PowerShell integrált parancsfájl-kezelési környezet (ISE)

1. Indítsa el a Kiszolgálókezelőt.

2. Kattintson a **szolgáltatások** majd **szolgáltatások hozzáadása**.

3. A szolgáltatások kiválasztása párbeszédpanelen kattintson a Windows PowerShell integrált parancsfájlkezelési környezet (ISE).

