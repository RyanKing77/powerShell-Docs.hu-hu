---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: dee5e8206c61d79faadf8573a82c74d4ac0fb8e0
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="improvements-in-powershell-script-debugging"></a>A PowerShell parancsfájlokban végzett hibakeresésének javításai

Számos fejlesztéssel PowerShell 5.0 került sor a hibakeresési élmény javítása érdekében:

## <a name="break-all"></a>Törés az összes

A PowerShell-konzolban és a Windows PowerShell ISE most engedélyezi, hogy megszakítással belépjen a hibakeresőbe parancsfájlok futtatásához. Ez a helyi és távoli munkamenetek működik.

A konzolon nyomja le az **Ctrl + Break**.

ISE, nyomja le az **Ctrl + B**, vagy használja a **hibakeresési -> minden törés** menüparancshoz.

## <a name="remote-debugging-and-remote-file-editing-in-windows-powershell-ise"></a>Távoli hibakereséssel és a távoli fájl szerkesztése a Windows PowerShell ISE

A Windows PowerShell ISE lehetővé teszi a megnyitni és módosítani a fájlok a távoli kapcsolat a PSEdit parancs futtatásával.
Például nyithatja meg a fájlt szerkesztésre a parancssorból egy távoli munkamenet az alábbiak szerint:

```powershell
[RemoteComputer1]: PS C:\> PSEdit C:\DebugDemoScripts\Test-GetMutex.ps1
```

Emellett mostantól szerkeszteni és menteni egy távoli fájlban, amely automatikusan megnyílik a Windows PowerShell ISE, amikor a töréspont kattint.
Most debug egy parancsfájlt, amely egy távoli számítógépen fut, a hiba javításához, és futtassa újból a módosítási parancsfájl fájl szerkesztésével.

## <a name="advanced-script-debugging"></a>Speciális parancsprogram-hibakeresés engedélyezése

Nincsenek új, speciális hibakeresési szolgáltatásokat, amelyek lehetővé teszik a helyi számítógép folyamat, amely be van töltve a Windows PowerShell csatolja, és hibakeresési tetszőleges futási terek a folyamatba.

### <a name="runspace-debugging"></a>Futási térben hibakeresés

Új parancsmagokkal bővült, amelyek lehetővé teszik, hogy a folyamat az aktuális futási terek listában, és a Windows PowerShell-konzolt vagy az ISE hibakereső csatlakoztatni, hogy futási térben a parancsprogram-hibakeresés engedélyezése:

-   Get-Runspace
-   Debug-Runspace
-   Enable-RunspaceDebug
-   Disable-RunspaceDebug
-   Get-RunspaceDebug

### <a name="attach-to-process-hosting-powershell"></a>PowerShell tartalmazó folyamat csatolása

E számítógép folyamat, amely rendelkezik a Windows PowerShell betöltött most csatlakoztatni. Ehhez a folyamathoz hasonló módon, hogy miként meg interaktív távoli munkamenetbe a Enter-PSSession parancsmag futtatásával egy interaktív munkamenet megadva:

-   Enter-PSHostProcess
-   Exit-PSHostProcess