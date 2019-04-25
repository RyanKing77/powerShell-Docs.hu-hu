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
# <a name="creating-a-workflow-by-using-a-windows-powershell-script"></a><span data-ttu-id="59ad3-102">Munkafolyamat létrehozása egy Windows PowerShell-szkripttel</span><span class="sxs-lookup"><span data-stu-id="59ad3-102">Creating a Workflow by Using a Windows PowerShell Script</span></span>

<span data-ttu-id="59ad3-103">Létrehozhat egy munkafolyamatot, ha a Windows PowerShell-szkriptet.</span><span class="sxs-lookup"><span data-stu-id="59ad3-103">You can create a workflow by writing a Windows PowerShell script.</span></span> <span data-ttu-id="59ad3-104">A munkafolyamat létrehozásához használja a munkafolyamat kulcsszót a parancsprogram törzse előtt a munkafolyamat nevét.</span><span class="sxs-lookup"><span data-stu-id="59ad3-104">To create a workflow, use the workflow keyword followed by a name for the workflow before the body of the script.</span></span> <span data-ttu-id="59ad3-105">Például:</span><span class="sxs-lookup"><span data-stu-id="59ad3-105">For example:</span></span>

```powershell

workflow Invoke-HelloWorld {"Hello World from workflow"}
```

<span data-ttu-id="59ad3-106">A munkafolyamat bármely más Windows PowerShell-paranccsal ugyanúgy találja.</span><span class="sxs-lookup"><span data-stu-id="59ad3-106">You find the workflow in the same way you would any other Windows PowerShell command.</span></span>

## <a name="implementing-parallel-and-sequence"></a><span data-ttu-id="59ad3-107">Párhuzamos és a feladatütemezés végrehajtása</span><span class="sxs-lookup"><span data-stu-id="59ad3-107">Implementing Parallel and Sequence</span></span>

<span data-ttu-id="59ad3-108">[Windows Workflow Foundation](https://msdn.microsoft.com/en-us/library/ms735967.aspx) párhuzamos tevékenységek végrehajtása támogatja.</span><span class="sxs-lookup"><span data-stu-id="59ad3-108">[Windows Workflow Foundation](https://msdn.microsoft.com/en-us/library/ms735967.aspx) supports execution of activities in parallel.</span></span> <span data-ttu-id="59ad3-109">Ez a funkció végrehajtásához egy Windows PowerShell-parancsprogram, használja a `parallel` kulcsszót a parancsprogram-blokkot elé.</span><span class="sxs-lookup"><span data-stu-id="59ad3-109">To implement this capability in a Windows PowerShell script, use the `parallel` keyword in front of a script block.</span></span> <span data-ttu-id="59ad3-110">Is használhatja a `foreach -parallel` párhuzamos objektumok gyűjteményét iterálódnak-létrehozás feladatait.</span><span class="sxs-lookup"><span data-stu-id="59ad3-110">You can also use the `foreach -parallel` construction to iterate through a collection of objects in parallel.</span></span> <span data-ttu-id="59ad3-111">Belül egy párhuzamos letiltása egymást követő sorrendben hajtsa végre a tevékenységek csoportjai, tegye a tevékenységek csoportjai parancsprogram-blokkot, és a blokkot a feladatütemezési kulcsszóval megelőző.</span><span class="sxs-lookup"><span data-stu-id="59ad3-111">To execute a group of activities in sequential order within a parallel block, enclose that group of activities in a script block and precede the block with the sequence keyword.</span></span>

## <a name="joining-computers-to-a-domain"></a><span data-ttu-id="59ad3-112">Számítógépek csatlakoztatása a tartományhoz</span><span class="sxs-lookup"><span data-stu-id="59ad3-112">Joining Computers to a Domain</span></span>

<span data-ttu-id="59ad3-113">A következő szkript létrehoz egy munkafolyamatot, amely ellenőrzi a felhasználó által megadott számítógépek egy csoportja tartomány állapotát, a tartományhoz csatlakoztatja azokat, ha már nem csatlakozó, és újra az állapotát ellenőrzi.</span><span class="sxs-lookup"><span data-stu-id="59ad3-113">The following script creates a workflow that checks the domain status of a group of user-specified computers, joins them to a domain if they are not already joined, and then checks the status again.</span></span> <span data-ttu-id="59ad3-114">Egy parancsfájl verziója, amelyet a XAML munkafolyamat ismertetett [tevékenységekkel a Windows PowerShell-munkafolyamat létrehozása](./creating-a-workflow-with-windows-powershell-activities.md).</span><span class="sxs-lookup"><span data-stu-id="59ad3-114">This is a script version of the XAML workflow explained in [Creating a Workflow with Windows PowerShell Activities](./creating-a-workflow-with-windows-powershell-activities.md).</span></span>

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