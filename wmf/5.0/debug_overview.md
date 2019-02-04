---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 22a027ebc97e15075980bc77ce272d8ecdae0b5f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686991"
---
# <a name="improvements-in-powershell-script-debugging"></a>A PowerShell parancsfájlokban végzett hibakeresésének javításai

Számos fejlesztéssel történtek a PowerShell 5.0 a hibakeresési élmény:

## <a name="break-all"></a>Törés az összes

A PowerShell-konzolt és a Windows PowerShell ISE-ben mostantól lehetővé teszi, hogy megszakítással belépjen a hibakeresőbe parancsfájlok futtatásához. Ez a módszer a helyi és távoli munkamenetek során.

Nyomja meg a konzolon **Ctrl + Break**.

A ISE-ben, nyomja le az ENTER **Ctrl + B**, vagy használja a **hibakeresése -> minden felosztása** parancs.

## <a name="remote-debugging-and-remote-file-editing-in-windows-powershell-ise"></a>Távoli hibakeresés és a távoli fájl szerkesztése a Windows PowerShell ISE-ben

Windows PowerShell ISE-ben mostantól lehetővé teszi megnyithatja és szerkesztheti a fájlokat a távoli kapcsolat a PSEdit parancsnak futtatásával.
Például nyithatja meg egy fájlt szerkesztésre a parancssorból egy távoli munkamenetet a következőképpen:

```powershell
[RemoteComputer1]: PS C:\> PSEdit C:\DebugDemoScripts\Test-GetMutex.ps1
```

Emellett most már szerkesztheti és menti a változásokat egy távoli fájlt, amely automatikusan megnyílik a Windows PowerShell ISE-ben a töréspont elérésekor.
Most hibakeresése egy parancsfájlt, amely egy távoli számítógépen fut, javítsa ki a hibát, és futtassa újból a módosított szkriptet a fájl szerkesztésével.

## <a name="advanced-script-debugging"></a>Speciális Erőforrásparancsfájlokban végzett hibakeresés

Nincsenek új, fejlett hibakeresési funkciók, amelyekkel bármely helyi számítógép folyamatot, amely be van töltve a Windows PowerShell csatolja, és a hibakeresés tetszőleges futási terek, az adott folyamatban.

### <a name="runspace-debugging"></a>Futási térben hibakeresés

Új parancsmagok, amelyekkel egy folyamat az aktuális futási terek listában, és a Windows PowerShell-konzolt vagy az ISE Hibakereső csatlakoztatása a parancsprogram-hibakeresés futási térben lettek hozzáadva:

-   Get-Runspace
-   Debug-Runspace
-   Enable-RunspaceDebug
-   Disable-RunspaceDebug
-   Get-RunspaceDebug

### <a name="attach-to-process-hosting-powershell"></a>PowerShell tartalmazó folyamat csatolása

Most már minden olyan számítógép folyamata, amely rendelkezik a Windows PowerShell betöltött csatlakoztathat. Ehhez a folyamathoz hasonló módon, hogy hogyan ad meg egy interaktív távoli munkamenetet a Enter-PSSession parancsmag futtatásával egy interaktív munkamenetbe írja be:

-   Enter-PSHostProcess
-   Exit-PSHostProcess
