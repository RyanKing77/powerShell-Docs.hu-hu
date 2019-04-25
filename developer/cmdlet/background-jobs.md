---
title: Háttérben futó feladatok |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a0ef5ac9-8254-4832-ace8-84b356c10f08
caps.latest.revision: 13
ms.openlocfilehash: ff4fe159eedc47fc69f4d783cd90d2b0e888c0d5
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068681"
---
# <a name="background-jobs"></a>Háttérfeladatok

Parancsmagok a művelet végrehajtása belső használatra, illetve a Windows PowerShell*háttérfeladat*. Amikor egy parancsmagot háttérfeladatként futtatja, a munkahelyi aszinkron módon történik a saját külön, a parancsmag által használt folyamat szálból hozzászólásláncban. A felhasználó szemszögéből háttérfeladatként, a parancsmag futtatásakor a parancssor használatával azonnal visszatér még akkor is, ha a feladat végrehajtásához egy kiterjesztett időn vesz igénybe, és a felhasználói megszakítás nélkül továbbra is, a feladat futtatása közben.

## <a name="background-jobs-child-jobs-and-the-job-repository"></a>A háttérben futó feladatok Gyermekfeladatok és a feladat-tárház

A háttérben futó feladatok támogató parancsmagok által visszaadott feladatobjektumot határozza meg a feladatot. (A [a Start-Job](/powershell/module/Microsoft.PowerShell.Core/Start-Job) parancsmag is visszaad egy feladatobjektumot.) Ez a definíció megtalálhatók a feladatot, adja meg a feladatot, az állapotadatok és a gyermekfeladatok használt azonosító nevét. A feladat nem végezze el a munkát. Minden egyes háttérfeladat, a gyermek legalább egy feladat, mert a gyermek feladat végzi a tényleges munkát. A parancsmag futtatásakor, hogy a munka háttérfeladatként történik, a parancsmag hozzá kell adnia a feladat és a gyermekfeladatok közös tárházhoz, a továbbiakban a *feladat tárház*.

Hogyan történik a háttérben futó feladatok kezelése parancssori kapcsolatos további információkért tekintse meg a következőket:

- [about_Jobs](/powershell/module/microsoft.powershell.core/about/about_jobs)

- [about_Job_Details](/powershell/module/microsoft.powershell.core/about/about_job_details)

- [about_Remote_Jobs](/powershell/module/microsoft.powershell.core/about/about_remote_jobs)

## <a name="writing-a-cmdlet-that-runs-as-a-background-job"></a>A parancsmagot háttérfeladatként futó írása

A parancsmagot háttérfeladatként futó írni a következő feladatokat kell elvégeznie:

- Adja meg egy `asJob` váltson paramétert, hogy a felhasználó eldöntheti, hogy futtassa a parancsmagot háttérfeladatként-e.

- Hozzon létre egy objektumot származó a [System.Management.Automation.Job](/dotnet/api/System.Management.Automation.Job) osztály. Ez az objektum lehet egy egyéni feladat vagy egy Windows PowerShell, például a megadott feladat objektum egy [System.Management.Automation.Pseventjob](/dotnet/api/System.Management.Automation.PSEventJob) objektum.

- A rekord a feldolgozási mód, adjon hozzá egy `if` utasítás, amely észleli, hogy a parancsmagot háttérfeladatként kell futnia.

- Egyéni feladat objektumok a feladat osztály megvalósításához.

- Vissza a megfelelő objektumokat, attól függően, hogy a parancsmagot háttérfeladatként futtatja.

A kód példa: [támogatási feladatok hogyan](./how-to-support-jobs.md).

## <a name="background-job-related-apis"></a>Háttérben futó feladatokkal kapcsolatos API-k

A következő API-kat a háttérben futó feladatok kezelése a Windows PowerShell által biztosított.

[System.Management.Automation.Job](/dotnet/api/System.Management.Automation.Job) egyéni feladatobjektum használatából. Ez az absztrakt osztályra.

[System.Management.Automation.Jobrepository](/dotnet/api/System.Management.Automation.JobRepository) nyelveket kezeli és a jelenlegi active háttérfeladatok információkat biztosít.

[System.Management.Automation.Jobstate](/dotnet/api/System.Management.Automation.JobState) határozza meg a háttérben futó feladat állapotát. Állapotok a következők: elindítva, futtatása és leállítva.

[System.Management.Automation.Jobstateinfo](/dotnet/api/System.Management.Automation.JobStateInfo) háttérfeladat állapotával kapcsolatos információkat nyújt, és ha az utolsó állapotváltozás okozta hiba, a feladat a jelenlegi állapotában megadott okát.

[System.Management.Automation.Jobstateeventargs](/dotnet/api/System.Management.Automation.JobStateEventArgs) egy esemény jelenik meg, ha a háttérben futó feladatok állapota, az argumentumok biztosít.

## <a name="windows-powershell-job-cmdlets"></a>Windows PowerShell feladat parancsmagok

A következő parancsmagok a háttérben futó feladatok kezelése a Windows PowerShell által biztosított.

[Get-Job](/powershell/module/Microsoft.PowerShell.Core/Get-Job)

Lekérdezi az aktuális munkamenet-ban futó Windows PowerShell-háttérfeladatokkal.

[Receive-Job](/powershell/module/Microsoft.PowerShell.Core/Receive-Job)

A Windows PowerShell-háttérfeladatokkal eredményeit lekérdezi az aktuális munkamenetben.

[Remove-Job](/powershell/module/Microsoft.PowerShell.Core/Remove-Job)

A Windows PowerShell a háttérben futó feladat törlése.

[Feladat indítása](/powershell/module/Microsoft.PowerShell.Core/Start-Job)

A Windows PowerShell háttérben futó feladat elindítása.

[Stop-Job](/powershell/module/Microsoft.PowerShell.Core/Stop-Job)

Egy Windows PowerShell háttérben futó feladatot leállítja.

[Wait-feladat](/powershell/module/Microsoft.PowerShell.Core/Wait-Job)

A parancssor használatával elrejti a addig, amíg egyikét vagy mindegyikét a Windows PowerShell-háttérfeladatokkal futnak a munkamenetben nem teljes.

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
