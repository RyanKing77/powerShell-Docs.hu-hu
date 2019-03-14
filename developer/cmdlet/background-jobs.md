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
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57794705"
---
# <a name="background-jobs"></a><span data-ttu-id="6dcef-102">Háttérfeladatok</span><span class="sxs-lookup"><span data-stu-id="6dcef-102">Background Jobs</span></span>

<span data-ttu-id="6dcef-103">Parancsmagok a művelet végrehajtása belső használatra, illetve a Windows PowerShell*háttérfeladat*.</span><span class="sxs-lookup"><span data-stu-id="6dcef-103">Cmdlets can perform their action internally or as a Windows PowerShell*background job*.</span></span> <span data-ttu-id="6dcef-104">Amikor egy parancsmagot háttérfeladatként futtatja, a munkahelyi aszinkron módon történik a saját külön, a parancsmag által használt folyamat szálból hozzászólásláncban.</span><span class="sxs-lookup"><span data-stu-id="6dcef-104">When a cmdlet runs as a background job, the work is done asynchronously in its own thread separate from the pipeline thread that the cmdlet is using.</span></span> <span data-ttu-id="6dcef-105">A felhasználó szemszögéből háttérfeladatként, a parancsmag futtatásakor a parancssor használatával azonnal visszatér még akkor is, ha a feladat végrehajtásához egy kiterjesztett időn vesz igénybe, és a felhasználói megszakítás nélkül továbbra is, a feladat futtatása közben.</span><span class="sxs-lookup"><span data-stu-id="6dcef-105">From the user perspective, when a cmdlet runs as a background job, the command prompt returns immediately even if the job takes an extended amount of time to complete, and the user can continue without interruption while the job runs.</span></span>

## <a name="background-jobs-child-jobs-and-the-job-repository"></a><span data-ttu-id="6dcef-106">A háttérben futó feladatok Gyermekfeladatok és a feladat-tárház</span><span class="sxs-lookup"><span data-stu-id="6dcef-106">Background Jobs, Child Jobs, and the Job Repository</span></span>

<span data-ttu-id="6dcef-107">A háttérben futó feladatok támogató parancsmagok által visszaadott feladatobjektumot határozza meg a feladatot.</span><span class="sxs-lookup"><span data-stu-id="6dcef-107">The job object that is returned by the cmdlets that support background jobs defines the job.</span></span> <span data-ttu-id="6dcef-108">(A [a Start-Job](/powershell/module/Microsoft.PowerShell.Core/Start-Job) parancsmag is visszaad egy feladatobjektumot.) Ez a definíció megtalálhatók a feladatot, adja meg a feladatot, az állapotadatok és a gyermekfeladatok használt azonosító nevét.</span><span class="sxs-lookup"><span data-stu-id="6dcef-108">(The [Start-Job](/powershell/module/Microsoft.PowerShell.Core/Start-Job) cmdlet also returns a job object.) The name of the job, an identifier that is used to specify the job, the state information, and the child jobs are included in this definition.</span></span> <span data-ttu-id="6dcef-109">A feladat nem végezze el a munkát.</span><span class="sxs-lookup"><span data-stu-id="6dcef-109">The job does not perform any of the work.</span></span> <span data-ttu-id="6dcef-110">Minden egyes háttérfeladat, a gyermek legalább egy feladat, mert a gyermek feladat végzi a tényleges munkát.</span><span class="sxs-lookup"><span data-stu-id="6dcef-110">Each background job has at least one child job because the child job performs the actual work.</span></span> <span data-ttu-id="6dcef-111">A parancsmag futtatásakor, hogy a munka háttérfeladatként történik, a parancsmag hozzá kell adnia a feladat és a gyermekfeladatok közös tárházhoz, a továbbiakban a *feladat tárház*.</span><span class="sxs-lookup"><span data-stu-id="6dcef-111">When you run a cmdlet so that the work is performed as a background job, the cmdlet must add the job and the child jobs to a common repository, referred to as the *job repository*.</span></span>

<span data-ttu-id="6dcef-112">Hogyan történik a háttérben futó feladatok kezelése parancssori kapcsolatos további információkért tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="6dcef-112">For more information about how background jobs are handled at the command line, see the following:</span></span>

- [<span data-ttu-id="6dcef-113">about_Jobs</span><span class="sxs-lookup"><span data-stu-id="6dcef-113">about_Jobs</span></span>](/powershell/module/microsoft.powershell.core/about/about_jobs)

- [<span data-ttu-id="6dcef-114">about_Job_Details</span><span class="sxs-lookup"><span data-stu-id="6dcef-114">about_Job_Details</span></span>](/powershell/module/microsoft.powershell.core/about/about_job_details)

- [<span data-ttu-id="6dcef-115">about_Remote_Jobs</span><span class="sxs-lookup"><span data-stu-id="6dcef-115">about_Remote_Jobs</span></span>](/powershell/module/microsoft.powershell.core/about/about_remote_jobs)

## <a name="writing-a-cmdlet-that-runs-as-a-background-job"></a><span data-ttu-id="6dcef-116">A parancsmagot háttérfeladatként futó írása</span><span class="sxs-lookup"><span data-stu-id="6dcef-116">Writing a Cmdlet That Runs as a Background Job</span></span>

<span data-ttu-id="6dcef-117">A parancsmagot háttérfeladatként futó írni a következő feladatokat kell elvégeznie:</span><span class="sxs-lookup"><span data-stu-id="6dcef-117">To write a cmdlet that can be run as a background job, you must complete the following tasks:</span></span>

- <span data-ttu-id="6dcef-118">Adja meg egy `asJob` váltson paramétert, hogy a felhasználó eldöntheti, hogy futtassa a parancsmagot háttérfeladatként-e.</span><span class="sxs-lookup"><span data-stu-id="6dcef-118">Define an `asJob` switch parameter so that the user can decide whether to run the cmdlet as a background job.</span></span>

- <span data-ttu-id="6dcef-119">Hozzon létre egy objektumot származó a [System.Management.Automation.Job](/dotnet/api/System.Management.Automation.Job) osztály.</span><span class="sxs-lookup"><span data-stu-id="6dcef-119">Create an object that derives from the [System.Management.Automation.Job](/dotnet/api/System.Management.Automation.Job) class.</span></span> <span data-ttu-id="6dcef-120">Ez az objektum lehet egy egyéni feladat vagy egy Windows PowerShell, például a megadott feladat objektum egy [System.Management.Automation.Pseventjob](/dotnet/api/System.Management.Automation.PSEventJob) objektum.</span><span class="sxs-lookup"><span data-stu-id="6dcef-120">This object can be a custom job object or a job object provided by Windows PowerShell, such as a [System.Management.Automation.Pseventjob](/dotnet/api/System.Management.Automation.PSEventJob) object.</span></span>

- <span data-ttu-id="6dcef-121">A rekord a feldolgozási mód, adjon hozzá egy `if` utasítás, amely észleli, hogy a parancsmagot háttérfeladatként kell futnia.</span><span class="sxs-lookup"><span data-stu-id="6dcef-121">In a record processing method, add an `if` statement that detects whether the cmdlet should run as a background job.</span></span>

- <span data-ttu-id="6dcef-122">Egyéni feladat objektumok a feladat osztály megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="6dcef-122">For custom job objects, implement the job class.</span></span>

- <span data-ttu-id="6dcef-123">Vissza a megfelelő objektumokat, attól függően, hogy a parancsmagot háttérfeladatként futtatja.</span><span class="sxs-lookup"><span data-stu-id="6dcef-123">Return the appropriate objects, depending on whether the cmdlet is run as a background job.</span></span>

<span data-ttu-id="6dcef-124">A kód példa: [támogatási feladatok hogyan](./how-to-support-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="6dcef-124">For a code example, see [How to Support Jobs](./how-to-support-jobs.md).</span></span>

## <a name="background-job-related-apis"></a><span data-ttu-id="6dcef-125">Háttérben futó feladatokkal kapcsolatos API-k</span><span class="sxs-lookup"><span data-stu-id="6dcef-125">Background Job-Related APIs</span></span>

<span data-ttu-id="6dcef-126">A következő API-kat a háttérben futó feladatok kezelése a Windows PowerShell által biztosított.</span><span class="sxs-lookup"><span data-stu-id="6dcef-126">The following APIs are provided by Windows PowerShell to manage background jobs.</span></span>

<span data-ttu-id="6dcef-127">[System.Management.Automation.Job](/dotnet/api/System.Management.Automation.Job) egyéni feladatobjektum használatából.</span><span class="sxs-lookup"><span data-stu-id="6dcef-127">[System.Management.Automation.Job](/dotnet/api/System.Management.Automation.Job) Derives custom job objects.</span></span> <span data-ttu-id="6dcef-128">Ez az absztrakt osztályra.</span><span class="sxs-lookup"><span data-stu-id="6dcef-128">This is an abstract class.</span></span>

<span data-ttu-id="6dcef-129">[System.Management.Automation.Jobrepository](/dotnet/api/System.Management.Automation.JobRepository) nyelveket kezeli és a jelenlegi active háttérfeladatok információkat biztosít.</span><span class="sxs-lookup"><span data-stu-id="6dcef-129">[System.Management.Automation.Jobrepository](/dotnet/api/System.Management.Automation.JobRepository) Manages and provides information about the current active background jobs.</span></span>

<span data-ttu-id="6dcef-130">[System.Management.Automation.Jobstate](/dotnet/api/System.Management.Automation.JobState) határozza meg a háttérben futó feladat állapotát.</span><span class="sxs-lookup"><span data-stu-id="6dcef-130">[System.Management.Automation.Jobstate](/dotnet/api/System.Management.Automation.JobState) Defines the state of the background job.</span></span> <span data-ttu-id="6dcef-131">Állapotok a következők: elindítva, futtatása és leállítva.</span><span class="sxs-lookup"><span data-stu-id="6dcef-131">States include Started, Running, and Stopped.</span></span>

<span data-ttu-id="6dcef-132">[System.Management.Automation.Jobstateinfo](/dotnet/api/System.Management.Automation.JobStateInfo) háttérfeladat állapotával kapcsolatos információkat nyújt, és ha az utolsó állapotváltozás okozta hiba, a feladat a jelenlegi állapotában megadott okát.</span><span class="sxs-lookup"><span data-stu-id="6dcef-132">[System.Management.Automation.Jobstateinfo](/dotnet/api/System.Management.Automation.JobStateInfo) Provides information about the state of a background job and, if the last state change was caused by an error, the reason the job entered its current state.</span></span>

<span data-ttu-id="6dcef-133">[System.Management.Automation.Jobstateeventargs](/dotnet/api/System.Management.Automation.JobStateEventArgs) egy esemény jelenik meg, ha a háttérben futó feladatok állapota, az argumentumok biztosít.</span><span class="sxs-lookup"><span data-stu-id="6dcef-133">[System.Management.Automation.Jobstateeventargs](/dotnet/api/System.Management.Automation.JobStateEventArgs) Provides the arguments for an event that is raised when a background job changes state.</span></span>

## <a name="windows-powershell-job-cmdlets"></a><span data-ttu-id="6dcef-134">Windows PowerShell feladat parancsmagok</span><span class="sxs-lookup"><span data-stu-id="6dcef-134">Windows PowerShell Job Cmdlets</span></span>

<span data-ttu-id="6dcef-135">A következő parancsmagok a háttérben futó feladatok kezelése a Windows PowerShell által biztosított.</span><span class="sxs-lookup"><span data-stu-id="6dcef-135">The following cmdlets are provided by Windows PowerShell to manage background jobs.</span></span>

[<span data-ttu-id="6dcef-136">Get-Job</span><span class="sxs-lookup"><span data-stu-id="6dcef-136">Get-Job</span></span>](/powershell/module/Microsoft.PowerShell.Core/Get-Job)

<span data-ttu-id="6dcef-137">Lekérdezi az aktuális munkamenet-ban futó Windows PowerShell-háttérfeladatokkal.</span><span class="sxs-lookup"><span data-stu-id="6dcef-137">Gets Windows PowerShell background jobs that are running in the current session.</span></span>

[<span data-ttu-id="6dcef-138">Receive-Job</span><span class="sxs-lookup"><span data-stu-id="6dcef-138">Receive-Job</span></span>](/powershell/module/Microsoft.PowerShell.Core/Receive-Job)

<span data-ttu-id="6dcef-139">A Windows PowerShell-háttérfeladatokkal eredményeit lekérdezi az aktuális munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="6dcef-139">Gets the results of the Windows PowerShell background jobs in the current session.</span></span>

[<span data-ttu-id="6dcef-140">Remove-Job</span><span class="sxs-lookup"><span data-stu-id="6dcef-140">Remove-Job</span></span>](/powershell/module/Microsoft.PowerShell.Core/Remove-Job)

<span data-ttu-id="6dcef-141">A Windows PowerShell a háttérben futó feladat törlése.</span><span class="sxs-lookup"><span data-stu-id="6dcef-141">Deletes a Windows PowerShell background job.</span></span>

[<span data-ttu-id="6dcef-142">Feladat indítása</span><span class="sxs-lookup"><span data-stu-id="6dcef-142">Start-Job</span></span>](/powershell/module/Microsoft.PowerShell.Core/Start-Job)

<span data-ttu-id="6dcef-143">A Windows PowerShell háttérben futó feladat elindítása.</span><span class="sxs-lookup"><span data-stu-id="6dcef-143">Starts a Windows PowerShell background job.</span></span>

[<span data-ttu-id="6dcef-144">Stop-Job</span><span class="sxs-lookup"><span data-stu-id="6dcef-144">Stop-Job</span></span>](/powershell/module/Microsoft.PowerShell.Core/Stop-Job)

<span data-ttu-id="6dcef-145">Egy Windows PowerShell háttérben futó feladatot leállítja.</span><span class="sxs-lookup"><span data-stu-id="6dcef-145">Stops a Windows PowerShell background job.</span></span>

[<span data-ttu-id="6dcef-146">Wait-feladat</span><span class="sxs-lookup"><span data-stu-id="6dcef-146">Wait-Job</span></span>](/powershell/module/Microsoft.PowerShell.Core/Wait-Job)

<span data-ttu-id="6dcef-147">A parancssor használatával elrejti a addig, amíg egyikét vagy mindegyikét a Windows PowerShell-háttérfeladatokkal futnak a munkamenetben nem teljes.</span><span class="sxs-lookup"><span data-stu-id="6dcef-147">Suppresses the command prompt until one or all of the Windows PowerShell background jobs running in the session are complete.</span></span>

## <a name="see-also"></a><span data-ttu-id="6dcef-148">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="6dcef-148">See Also</span></span>

[<span data-ttu-id="6dcef-149">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="6dcef-149">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
