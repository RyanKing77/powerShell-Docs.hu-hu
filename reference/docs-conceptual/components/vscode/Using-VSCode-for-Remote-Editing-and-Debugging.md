---
title: A Visual Studio Code használata távoli szerkesztéshez és hibakereséshez
description: A Visual Studio Code használata távoli szerkesztéshez és hibakereséshez
ms.date: 08/06/2018
ms.openlocfilehash: fbc1ee3556e822b4afb2b37111d0688dc89fdab3
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62086671"
---
# <a name="using-visual-studio-code-for-remote-editing-and-debugging"></a>A Visual Studio Code használata távoli szerkesztéshez és hibakereséshez

Azoknak, azokat az ISE ismernie, előfordulhat, hogy már ismert, hogy futtatja sikerült `psedit file.ps1` az integrált konzol – helyi vagy távoli - fájlok megnyitásához a jobb gombbal az ISE-ben.

Azt tapasztaltuk, ez a funkció érhető el a PowerShell-VSCode-bővítményben. Ez az útmutató bemutatja, hogyan kell tenni.

## <a name="prerequisites"></a>Előfeltételek

Ez az útmutató feltételezi, hogy:

- a távoli erőforrás (például: virtuális gép, egy tárolót), hogy rendelkezik-e a hozzáférést
- A PowerShell, és a gazdagépen futó
- VSCode és a PowerShell-bővítmény VSCode-

Ez a funkció a Windows PowerShell és a PowerShell Core működik.

Ez a funkció is működik, ha egy távoli gépen a Rendszerfelügyeleti webszolgáltatások, a PowerShell Directet vagy az SSH-n keresztül csatlakozik. Ha az SSH-val szeretne, de Windows használ, tekintse meg a [SSH Win32 verziója](https://github.com/PowerShell/Win32-OpenSSH)!

## <a name="lets-go"></a>gyerünk

Ebben a szakaszban I fog végig távoli szerkesztése és a hibakeresést a saját MacBook Pro egy Ubuntu virtuális gép futtatása az Azure-ban. E nem a Windows, de **megegyezik a folyamat**.

### <a name="local-file-editing-with-open-editorfile"></a>Szerkesztés az Open-EditorFile helyi fájl

A PowerShell-bővítmény a VSCode elindult, és a PowerShell integrált konzol nyitja meg, hogy írja be `Open-EditorFile foo.ps1` vagy `psedit foo.ps1` megnyitása a helyi foo.ps1 fájlt közvetlenül a szerkesztőben.

![Open-EditorFile foo.ps1 helyileg működik](https://user-images.githubusercontent.com/2644648/34895897-7c2c46ac-f79c-11e7-9410-a252aff52f13.png)

>[!NOTE]
> foo.ps1 már léteznie kell.

Itt is:

Töréspont hozzáadása a területbe ![margó a Töréspont hozzáadása](https://user-images.githubusercontent.com/2644648/34895893-7bdc38e2-f79c-11e7-8026-8ad53f9a1bad.png)

és nyomja le az F5 való hibakeresés a PowerShell-parancsfájlt.
![a helyi PowerShell-parancsprogram-hibakeresés](https://user-images.githubusercontent.com/2644648/34895894-7bedb874-f79c-11e7-9180-7e0dc2d02af8.png)

Hibakeresés közben is együttműködhet a hibakeresési konzolt, tekintse meg a változók a bal oldalon, és hibakeresési eszközök minden más standard hatókörében.

### <a name="remote-file-editing-with-open-editorfile"></a>Szerkesztés az Open-EditorFile távoli fájl

Most már folytassuk a Szerkesztés és hibakeresés távoli fájlba. A lépések nagyjából azonosak a, igazolnia kell a kezdeti lépések – adja meg a PowerShell-munkamenetet a távoli kiszolgáló csak egy dolog van.

A parancsmag van ehhez. Azt nevezzük `Enter-PSSession`.

A parancsmag watered le leírását a következő:

- `Enter-PSSession -ComputerName foo` a WinRM-n keresztül munkamenet indítása
- `Enter-PSSession -ContainerId foo` és `Enter-PSSession -VmId foo` keresztül a PowerShell Directet munkamenet indítása
- `Enter-PSSession -HostName foo` SSH-kapcsolaton keresztül egy munkamenet indítása

További információ az `Enter-PSSession`, tekintse meg a docs [Itt](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enter-pssession?view=powershell-6).

E fogja használni az SSH a távelérése óta egy Ubuntu virtuális gép az Azure-ban macOS rendszerről fogom.

Először az integrált konzol az Enter-PSSession futtassa. Tudni fogja, hogy használja-e a munkamenet mert `[something]` bal oldalán, az üzenet fog megjelenni.

![Enter-PSSession-hívás](https://user-images.githubusercontent.com/2644648/34895896-7c18e0bc-f79c-11e7-9b36-6f4bd0e9b0db.png)

Itt tehetjük a pontos lépések, ha azt egy helyi parancsfájl szerkesztése.

1. Futtatás `Open-EditorFile test.ps1` vagy `psedit test.ps1` megnyitása a távoli `test.ps1` fájl ![nyílt-EditorFile test.ps1 fájl](https://user-images.githubusercontent.com/2644648/34895898-7c3e6a12-f79c-11e7-8bdf-549b591ecbcb.png)
2. A fájl/set töréspontok szerkesztése ![szerkesztheti, és állítson be töréspontokat](https://user-images.githubusercontent.com/2644648/34895892-7bb68246-f79c-11e7-8c0a-c2121773afbb.png)
3. Hibakeresés (F5), a távoli fájl

![a távoli fájl hibakeresés](https://user-images.githubusercontent.com/2644648/34895895-7c040782-f79c-11e7-93ea-47724fa5c10d.png)

Ez minden van rá! Reméljük, hogy ez az útmutató segítségével törölje a távoli hibakeresés és a PowerShell használatával a VSCode szerkesztésével kapcsolatos kérdése mentése.

Ha bármilyen problémába ütközik, nyugodtan megnyithat problémákat [a GitHub-adattárat a](http://github.com/powershell/vscode-powershell).
