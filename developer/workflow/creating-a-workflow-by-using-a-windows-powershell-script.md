---
title: Egy Windows PowerShell-parancsprogram használatával-munkafolyamat létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 70532e7e-9cac-43c3-9687-e77011ecc878
caps.latest.revision: 4
ms.openlocfilehash: 5eb2186cbceee21f8b4a8c88b812e9c71f15e0af
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62080373"
---
# <a name="creating-a-workflow-by-using-a-windows-powershell-script"></a>Munkafolyamat létrehozása egy Windows PowerShell-szkripttel

Létrehozhat egy munkafolyamatot, ha a Windows PowerShell-szkriptet. A munkafolyamat létrehozásához használja a munkafolyamat kulcsszót a parancsprogram törzse előtt a munkafolyamat nevét. Például:

```powershell

workflow Invoke-HelloWorld {"Hello World from workflow"}
```

A munkafolyamat bármely más Windows PowerShell-paranccsal ugyanúgy találja.

## <a name="implementing-parallel-and-sequence"></a>Párhuzamos és a feladatütemezés végrehajtása

[Windows Workflow Foundation](https://msdn.microsoft.com/en-us/library/ms735967.aspx) párhuzamos tevékenységek végrehajtása támogatja. Ez a funkció végrehajtásához egy Windows PowerShell-parancsprogram, használja a `parallel` kulcsszót a parancsprogram-blokkot elé. Is használhatja a `foreach -parallel` párhuzamos objektumok gyűjteményét iterálódnak-létrehozás feladatait. Belül egy párhuzamos letiltása egymást követő sorrendben hajtsa végre a tevékenységek csoportjai, tegye a tevékenységek csoportjai parancsprogram-blokkot, és a blokkot a feladatütemezési kulcsszóval megelőző.

## <a name="joining-computers-to-a-domain"></a>Számítógépek csatlakoztatása a tartományhoz

A következő szkript létrehoz egy munkafolyamatot, amely ellenőrzi a felhasználó által megadott számítógépek egy csoportja tartomány állapotát, a tartományhoz csatlakoztatja azokat, ha már nem csatlakozó, és újra az állapotát ellenőrzi. Egy parancsfájl verziója, amelyet a XAML munkafolyamat ismertetett [tevékenységekkel a Windows PowerShell-munkafolyamat létrehozása](./creating-a-workflow-with-windows-powershell-activities.md).

```powershell
workflow Join-Domain
{
    param([string[]] $ComputerName, [PSCredential] $DomainCred, [PsCredential] $MachineCred)

    foreach -parallel($Computer in $ComputerName)
    {
        sequence {
        Get-WmiObject -PSComputerName $Computer -PSCredential $MachineCred
        Add-Computer -PSComputerName $Computer -PSCredential $DomainCred
        Restart-Computer -ComputerName $Computer -Credential $MachineCred -For PowerShell -Force -Wait -PSComputerName ""
        Get-WmiObject -PSComputerName $Computer -PSCredential $MachineCred
        }
    }
 }

```