---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
title: A PowerShell parancsfájlokban végzett hibakeresésének javításai
ms.openlocfilehash: f1771a451ba671da2371fcfc95374e6131573ddc
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65856174"
---
# <a name="improvements-in-powershell-script-debugging"></a>A PowerShell parancsfájlokban végzett hibakeresésének javításai

PowerShell 5.0, amelyek javítják a hibakeresési folyamatot számos fejlesztést tartalmaz.

## <a name="break-all"></a>Törés az összes

A PowerShell-konzolt és a PowerShell ISE-ben mostantól lehetővé teszi, hogy megszakítással belépjen a hibakeresőbe parancsfájlok futtatásához. Ez a módszer a helyi és távoli munkamenetek során.

Nyomja meg a konzolon <kbd>Ctrl</kbd>+<kbd>felosztása</kbd>.

A ISE-ben, nyomja le az ENTER <kbd>Ctrl</kbd>+<kbd>B</kbd>, vagy használja a **hibakeresése -> minden felosztása** parancs.

## <a name="remote-debugging-and-remote-file-editing-in-powershell-ise"></a>Távoli hibakeresés és a távoli fájl szerkesztése a PowerShell ISE-ben

PowerShell ISE-ben mostantól lehetővé teszi megnyithatja és szerkesztheti a fájlokat a távoli kapcsolat a PSEdit parancsnak futtatásával.
Például nyithatja meg egy fájlt szerkesztésre a parancssorból egy távoli munkamenetet a következőképpen:

```powershell
[RemoteComputer1]: PS C:\> PSEdit C:\DebugDemoScripts\Test-GetMutex.ps1
```

Emellett most már szerkesztheti és menti a változásokat egy távoli fájlt, amely automatikusan megnyílik a PowerShell ISE-ben a töréspont elérésekor. Most hibakeresése egy parancsfájlt, amely egy távoli számítógépen fut, javítsa ki a hibát, és futtassa újból a módosított szkriptet a fájl szerkesztésével.

## <a name="advanced-script-debugging"></a>Speciális Erőforrásparancsfájlokban végzett hibakeresés

Nincsenek új, fejlett hibakeresési funkciók, amelyekkel bármely helyi számítógép folyamatot, amely be van töltve a PowerShell csatolja, és a hibakeresés tetszőleges futási terek, az adott folyamatban.

### <a name="runspace-debugging"></a>Futási térben hibakeresés

Új parancsmagok, amelyekkel egy folyamat az aktuális futási terek listában, és a PowerShell-konzol vagy a PowerShell ISE-ben Hibakereső csatlakoztatása a parancsprogram-hibakeresés futási térben lettek hozzáadva:

- Get-Runspace
- Debug-Runspace
- Enable-RunspaceDebug
- Disable-RunspaceDebug
- Get-RunspaceDebug

### <a name="attach-to-process-hosting-powershell"></a>PowerShell tartalmazó folyamat csatolása

Most már minden olyan számítógép folyamata, amely rendelkezik betöltött PowerShell csatlakoztathat. Ehhez be a gazdagép-folyamat az az interaktív munkamenet megadásával. További információ:

- [Enter-PSHostProcess](/powershell/module/Microsoft.PowerShell.Core/Enter-PSHostProcess)
- [Exit-PSHostProcess](/powershell/module/Microsoft.PowerShell.Core/Exit-PSHostProcess)
