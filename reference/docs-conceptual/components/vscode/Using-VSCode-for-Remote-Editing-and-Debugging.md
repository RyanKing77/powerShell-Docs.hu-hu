---
title: A Visual Studio Code használata távoli szerkesztéshez és hibakereséshez
description: A Visual Studio Code használata távoli szerkesztéshez és hibakereséshez
ms.date: 06/13/2019
ms.openlocfilehash: ae3b7a3709498fcd547a48d0849b0dc880217225
ms.sourcegitcommit: 13f24786ed39ca1c07eff2b73a1974c366e31cb8
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/19/2019
ms.locfileid: "67264016"
---
# <a name="using-visual-studio-code-for-remote-editing-and-debugging"></a>A Visual Studio Code használata távoli szerkesztéshez és hibakereséshez

Azok számára, az, hogy ismeri az ISE-ben, előfordulhat, hogy már ismert, hogy futtatja sikerült `psedit file.ps1` az integrált konzol – helyi vagy távoli - fájlok megnyitásához a jobb gombbal az ISE-ben.

Ez a funkció a VSCode-PowerShell-bővítményének is érhető el. Ez az útmutató bemutatja, hogyan teheti meg.

## <a name="prerequisites"></a>Előfeltételek

Ez az útmutató feltételezi, hogy:

- a távoli erőforrás (például: virtuális gép, egy tárolót), hogy rendelkezik-e a hozzáférést
- A PowerShell, és a gazdagépen futó
- VSCode és a PowerShell-bővítmény VSCode-

Ez a funkció a Windows PowerShell és a PowerShell Core működik.

Ez a funkció is működik, ha egy távoli gépen a Rendszerfelügyeleti webszolgáltatások, a PowerShell Directet vagy az SSH-n keresztül csatlakozik. Ha az SSH-val szeretne, de Windows használ, tekintse meg a [SSH Win32 verziója](https://github.com/PowerShell/Win32-OpenSSH)!

> [!IMPORTANT]
> A `Open-EditorFile` és `psedit` parancsok csak munkahelyi a **PowerShell integrált konzol** VSCode-a PowerShell-bővítmény által létrehozott.

## <a name="usage-examples"></a>Használati példák

A példákból látható Szerkesztés és hibakeresés egy MacBook Pro az Ubuntu virtuális géphez távoli Azure-ban. A folyamat megegyezik a Windows.

### <a name="local-file-editing-with-open-editorfile"></a>Szerkesztés az Open-EditorFile helyi fájl

A PowerShell-bővítmény a VSCode elindult, és a PowerShell integrált konzol nyitja meg, hogy írja be `Open-EditorFile foo.ps1` vagy `psedit foo.ps1` megnyitása a helyi foo.ps1 fájlt közvetlenül a szerkesztőben.

![Open-EditorFile foo.ps1 helyileg működik](images/Using-VSCode-for-Remote-Editing-and-Debugging/1-open-local-file.png)

>[!NOTE]
> A fájl `foo.ps1` már léteznie kell.

Itt is:

- Töréspont hozzáadása a területbe

  ![margó a Töréspont hozzáadása](images/Using-VSCode-for-Remote-Editing-and-Debugging/2-adding-breakpoint-gutter.png)

- Nyomja le az F5 való hibakeresés a PowerShell-parancsfájlt.

  ![a helyi PowerShell-parancsprogram-hibakeresés](images/Using-VSCode-for-Remote-Editing-and-Debugging/3-local-debug.png)

Hibakeresés közben is együttműködhet a hibakeresési konzolt, tekintse meg a változók a bal oldalon, és hibakeresési eszközök minden más standard hatókörében.

### <a name="remote-file-editing-with-open-editorfile"></a>Szerkesztés az Open-EditorFile távoli fájl

Most már folytassuk a Szerkesztés és hibakeresés távoli fájlba. A lépések nagyjából azonosak a, igazolnia kell a kezdeti lépések – adja meg a PowerShell-munkamenetet a távoli kiszolgáló csak egy dolog van.

A parancsmag van ehhez. Azt nevezzük `Enter-PSSession`.

A parancsmag watered le leírását a következő:

- `Enter-PSSession -ComputerName foo` a WinRM-n keresztül munkamenet indítása
- `Enter-PSSession -ContainerId foo` és `Enter-PSSession -VmId foo` keresztül a PowerShell Directet munkamenet indítása
- `Enter-PSSession -HostName foo` SSH-kapcsolaton keresztül egy munkamenet indítása

További információkért lásd a dokumentációban [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession).

Mivel mi maradunk a macOS egy Ubuntu virtuális gép az Azure-ban, használjuk SSH a távelérése.

Először a integrált konzol futtassa `Enter-PSSession`. Csatlakozik a távoli munkamenet során `[<hostname>]` bal oldalán, az üzenet legfeljebb mutat be.

![Enter-PSSession-hívás](images/Using-VSCode-for-Remote-Editing-and-Debugging/4-enter-pssession.png)

Most tehetjük ugyanazokat a lépéseket, ha azt egy helyi parancsfájl szerkesztése.

1. Futtatás `Open-EditorFile test.ps1` vagy `psedit test.ps1` megnyitása a távoli `test.ps1` fájl

  ![Open-EditorFile test.ps1 fájl](images/Using-VSCode-for-Remote-Editing-and-Debugging/5-open-remote-file.png)

1. A fájl/set töréspontok szerkesztése

   ![szerkesztheti, és állítson be töréspontokat](images/Using-VSCode-for-Remote-Editing-and-Debugging/6-set-breakpoints.png)

1. Hibakeresés (F5), a távoli fájl

   ![a távoli fájl hibakeresés](images/Using-VSCode-for-Remote-Editing-and-Debugging/7-start-debugging.png)

Ha bármilyen problémába ütközik, a problémák megnyithatja a [GitHub-adattárat](https://github.com/powershell/vscode-powershell).
