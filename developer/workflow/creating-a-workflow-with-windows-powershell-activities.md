---
title: Tevékenységek feldolgozása Windows PowerShell-munkafolyamat létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fb55971a-4ea4-4c51-aeff-4e0bb05a51b2
caps.latest.revision: 6
ms.openlocfilehash: 98cac43698b3f537ee318cd2570b2174631665a7
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58055427"
---
# <a name="creating-a-workflow-with-windows-powershell-activities"></a>Munkafolyamat létrehozása Windows PowerShell-tevékenységekkel

Létrehozhat egy Windows PowerShell-munkafolyamat tevékenységek kiválasztásával a Visual Studio eszközkészletből, és húzza őket a munkafolyamat-Tervező ablak. A Visual Studio-eszközkészlet Windows PowerShell-tevékenységek hozzáadásával kapcsolatos további információkért lásd: [hozzáadása Windows PowerShell tevékenységek a Visual Studio-eszközkészlet](./adding-windows-powershell-activities-to-the-visual-studio-toolbox.md).

Az alábbi eljárásokból megtudhatja, hogyan hozhat létre egy munkafolyamatot, amely ellenőrzi a felhasználó által megadott számítógépek egy csoportja tartomány állapotát, a tartományhoz csatlakoztatja azokat, ha már nem csatlakozó, és újra az állapotát ellenőrzi.

### <a name="setting-up-the-project"></a>A projekt beállítása

1. Kövesse a [hozzáadása Windows PowerShell tevékenységek a Visual Studio-eszközkészlet](./adding-windows-powershell-activities-to-the-visual-studio-toolbox.md) hozzon létre egy munkafolyamat-projektet, és adja hozzá az tevékenységei a [Microsoft.Powershell.Activities](/dotnet/api/Microsoft.PowerShell.Activities) és [ Microsoft.Powershell.Management.Activities](/dotnet/api/Microsoft.PowerShell.Management.Activities) szerelvényeket az eszközkészlet.

2. Adja hozzá System.Management.Automation, Microsoft.PowerShell.Activities, System.Management, Microsoft.PowerShell.Management.Activities és Microsoft.PowerShell.Commands.Management feltárhatja, hogy a projekt referenciaszerelvényeket.

### <a name="adding-activities-to-the-workflow"></a>Tevékenységek hozzáadása a munkafolyamathoz

1. Adjon hozzá egy **feladatütemezési** tevékenység, amely a munkafolyamatot.

2. Hozzon létre egy argumentum nevű `ComputerName` egy argumentum típusú `String[]`. Ez az argumentum ellenőrzi, és csatlakozzon a számítógépek nevét jelöli.

3. Hozzon létre egy argumentum nevű `DomainCred` típusú [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential). Ez az argumentum egy tartományfiókot, amely jogosult a számítógép csatlakoztatása a tartományhoz, a tartományi hitelesítő adatok jelöli.

4. Hozzon létre egy argumentum nevű `MachineCred` típusú [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential). Ez az argumentum egy rendszergazda azokon a számítógépeken és csatlakozás hitelesítő adatait jelöli.

5. Adjon hozzá egy **ParallelForEach** belül a tevékenység a **feladatütemezési** tevékenység. Adja meg `comp` és `ComputerName` a a szövegdobozok, hogy a hurok elemeinek végighalad a `ComputerName` tömb.

6. Adjon hozzá egy **feladatütemezési** törzse tevékenységet a **ParallelForEach** tevékenység. Állítsa be a **DisplayName** való feladatütemezések tulajdonságát `JoinDomain`.

7. Adjon hozzá egy **GetWmiObject** tevékenység, amely a **JoinDomain** feladatütemezési.

8. A tulajdonságainak szerkesztése a **GetWmiObject** tevékenység az alábbiak szerint.

   |Tulajdonság|Érték|
   |--------------|-----------|
   |**Osztály**|"Win32_ComputerSystem"|
   |**PSComputerName**|{comp}|
   |**PSCredential**|MachineCred|

9. Adjon hozzá egy **AddComputer** tevékenység, amely a **JoinDomain** előkészítése után a **GetWmiObject** tevékenység.

10. A tulajdonságainak szerkesztése a **AddComputer** tevékenység az alábbiak szerint.

    |Tulajdonság|Érték|
    |--------------|-----------|
    |**Számítógépnév**|{comp}|
    |**DomainCredential**|DomainCred|

11. Adjon hozzá egy **RestartComputer** tevékenység, amely a **JoinDomain** előkészítése után a **AddComputer** tevékenység.

12. A tulajdonságainak szerkesztése a **RestartComputer** tevékenység az alábbiak szerint.

    |Tulajdonság|Érték|
    |--------------|-----------|
    |**Számítógépnév**|{comp}|
    |**Hitelesítő adatok**|MachineCred|
    |**a**|Microsoft.PowerShell.Commands.WaitForServiceTypes.PowerShell|
    |**Kényszerített**|Igaz|
    |várj|Igaz|
    |PSComputerName|{""}|

13. Adjon hozzá egy **GetWmiObject** tevékenység, amely a **JoinDomain** előkészítése után a **RestartComputer** tevékenység. Ugyanaz, mint az előző lehet a tulajdonságainak szerkesztése **GetWmiObject** tevékenység.

    Ha befejezte az eljárásokat, a munkafolyamat-Tervező ablak hasonlónak kell lennie.

    ![A munkafolyamat-tervezővel JoinDomain XAML](../media/joindomainworkflow.png)
    ![JoinDomain XAML munkafolyamat-tervezőben](../media/joindomainworkflow.png "JoinDomainWorkflow")