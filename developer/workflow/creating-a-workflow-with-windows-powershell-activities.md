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
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62080446"
---
# <a name="creating-a-workflow-with-windows-powershell-activities"></a><span data-ttu-id="0df57-102">Munkafolyamat létrehozása Windows PowerShell-tevékenységekkel</span><span class="sxs-lookup"><span data-stu-id="0df57-102">Creating a Workflow with Windows PowerShell Activities</span></span>

<span data-ttu-id="0df57-103">Létrehozhat egy Windows PowerShell-munkafolyamat tevékenységek kiválasztásával a Visual Studio eszközkészletből, és húzza őket a munkafolyamat-Tervező ablak.</span><span class="sxs-lookup"><span data-stu-id="0df57-103">You can create a Windows PowerShell workflow by selecting activities from the Visual Studio Toolbox and dragging them to the Workflow Designer window.</span></span> <span data-ttu-id="0df57-104">A Visual Studio-eszközkészlet Windows PowerShell-tevékenységek hozzáadásával kapcsolatos további információkért lásd: [hozzáadása Windows PowerShell tevékenységek a Visual Studio-eszközkészlet](./adding-windows-powershell-activities-to-the-visual-studio-toolbox.md).</span><span class="sxs-lookup"><span data-stu-id="0df57-104">For information about adding Windows PowerShell activities to the Visual Studio Toolbox, see [Adding Windows PowerShell Activities to the Visual Studio Toolbox](./adding-windows-powershell-activities-to-the-visual-studio-toolbox.md).</span></span>

<span data-ttu-id="0df57-105">Az alábbi eljárásokból megtudhatja, hogyan hozhat létre egy munkafolyamatot, amely ellenőrzi a felhasználó által megadott számítógépek egy csoportja tartomány állapotát, a tartományhoz csatlakoztatja azokat, ha már nem csatlakozó, és újra az állapotát ellenőrzi.</span><span class="sxs-lookup"><span data-stu-id="0df57-105">The following procedures describe how to create a workflow that checks the domain status of a group of user-specified computers, joins them to a domain if they are not already joined, and then checks the status again.</span></span>

### <a name="setting-up-the-project"></a><span data-ttu-id="0df57-106">A projekt beállítása</span><span class="sxs-lookup"><span data-stu-id="0df57-106">Setting up the Project</span></span>

1. <span data-ttu-id="0df57-107">Kövesse a [hozzáadása Windows PowerShell tevékenységek a Visual Studio-eszközkészlet](./adding-windows-powershell-activities-to-the-visual-studio-toolbox.md) hozzon létre egy munkafolyamat-projektet, és adja hozzá az tevékenységei a [Microsoft.Powershell.Activities](/dotnet/api/Microsoft.PowerShell.Activities) és [ Microsoft.Powershell.Management.Activities](/dotnet/api/Microsoft.PowerShell.Management.Activities) szerelvényeket az eszközkészlet.</span><span class="sxs-lookup"><span data-stu-id="0df57-107">Follow the procedure in [Adding Windows PowerShell Activities to the Visual Studio Toolbox](./adding-windows-powershell-activities-to-the-visual-studio-toolbox.md) to create a workflow project and add the activities from the [Microsoft.Powershell.Activities](/dotnet/api/Microsoft.PowerShell.Activities) and [Microsoft.Powershell.Management.Activities](/dotnet/api/Microsoft.PowerShell.Management.Activities) assemblies to the toolbox.</span></span>

2. <span data-ttu-id="0df57-108">Adja hozzá System.Management.Automation, Microsoft.PowerShell.Activities, System.Management, Microsoft.PowerShell.Management.Activities és Microsoft.PowerShell.Commands.Management feltárhatja, hogy a projekt referenciaszerelvényeket.</span><span class="sxs-lookup"><span data-stu-id="0df57-108">Add System.Management.Automation, Microsoft.PowerShell.Activities, System.Management, Microsoft.PowerShell.Management.Activities, and Microsoft.PowerShell.Commands.Management as to the project as reference assemblies.</span></span>

### <a name="adding-activities-to-the-workflow"></a><span data-ttu-id="0df57-109">Tevékenységek hozzáadása a munkafolyamathoz</span><span class="sxs-lookup"><span data-stu-id="0df57-109">Adding Activities to the Workflow</span></span>

1. <span data-ttu-id="0df57-110">Adjon hozzá egy **feladatütemezési** tevékenység, amely a munkafolyamatot.</span><span class="sxs-lookup"><span data-stu-id="0df57-110">Add a **Sequence** activity to the workflow.</span></span>

2. <span data-ttu-id="0df57-111">Hozzon létre egy argumentum nevű `ComputerName` egy argumentum típusú `String[]`.</span><span class="sxs-lookup"><span data-stu-id="0df57-111">Create an argument named `ComputerName` with an argument type of `String[]`.</span></span> <span data-ttu-id="0df57-112">Ez az argumentum ellenőrzi, és csatlakozzon a számítógépek nevét jelöli.</span><span class="sxs-lookup"><span data-stu-id="0df57-112">This argument represents the names of the computers to check and join.</span></span>

3. <span data-ttu-id="0df57-113">Hozzon létre egy argumentum nevű `DomainCred` típusú [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential).</span><span class="sxs-lookup"><span data-stu-id="0df57-113">Create an argument named `DomainCred` of type [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential).</span></span> <span data-ttu-id="0df57-114">Ez az argumentum egy tartományfiókot, amely jogosult a számítógép csatlakoztatása a tartományhoz, a tartományi hitelesítő adatok jelöli.</span><span class="sxs-lookup"><span data-stu-id="0df57-114">This argument represents the domain credentials of a domain account that is authorized to join a computer to the domain.</span></span>

4. <span data-ttu-id="0df57-115">Hozzon létre egy argumentum nevű `MachineCred` típusú [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential).</span><span class="sxs-lookup"><span data-stu-id="0df57-115">Create an argument named `MachineCred` of type [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential).</span></span> <span data-ttu-id="0df57-116">Ez az argumentum egy rendszergazda azokon a számítógépeken és csatlakozás hitelesítő adatait jelöli.</span><span class="sxs-lookup"><span data-stu-id="0df57-116">This argument represents the credentials of an administrator on the computers to check and join.</span></span>

5. <span data-ttu-id="0df57-117">Adjon hozzá egy **ParallelForEach** belül a tevékenység a **feladatütemezési** tevékenység.</span><span class="sxs-lookup"><span data-stu-id="0df57-117">Add a **ParallelForEach** activity inside the **Sequence** activity.</span></span> <span data-ttu-id="0df57-118">Adja meg `comp` és `ComputerName` a a szövegdobozok, hogy a hurok elemeinek végighalad a `ComputerName` tömb.</span><span class="sxs-lookup"><span data-stu-id="0df57-118">Enter `comp` and `ComputerName` in the text boxes so that the loop iterates through the elements of the `ComputerName` array.</span></span>

6. <span data-ttu-id="0df57-119">Adjon hozzá egy **feladatütemezési** törzse tevékenységet a **ParallelForEach** tevékenység.</span><span class="sxs-lookup"><span data-stu-id="0df57-119">Add a **Sequence** activity to the body of the **ParallelForEach** activity.</span></span> <span data-ttu-id="0df57-120">Állítsa be a **DisplayName** való feladatütemezések tulajdonságát `JoinDomain`.</span><span class="sxs-lookup"><span data-stu-id="0df57-120">Set the **DisplayName** property of the sequence to `JoinDomain`.</span></span>

7. <span data-ttu-id="0df57-121">Adjon hozzá egy **GetWmiObject** tevékenység, amely a **JoinDomain** feladatütemezési.</span><span class="sxs-lookup"><span data-stu-id="0df57-121">Add a **GetWmiObject** activity to the **JoinDomain** sequence.</span></span>

8. <span data-ttu-id="0df57-122">A tulajdonságainak szerkesztése a **GetWmiObject** tevékenység az alábbiak szerint.</span><span class="sxs-lookup"><span data-stu-id="0df57-122">Edit the properties of the **GetWmiObject** activity as follows.</span></span>

   |<span data-ttu-id="0df57-123">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="0df57-123">Property</span></span>|<span data-ttu-id="0df57-124">Érték</span><span class="sxs-lookup"><span data-stu-id="0df57-124">Value</span></span>|
   |--------------|-----------|
   |<span data-ttu-id="0df57-125">**Osztály**</span><span class="sxs-lookup"><span data-stu-id="0df57-125">**Class**</span></span>|<span data-ttu-id="0df57-126">"Win32_ComputerSystem"</span><span class="sxs-lookup"><span data-stu-id="0df57-126">"Win32_ComputerSystem"</span></span>|
   |<span data-ttu-id="0df57-127">**PSComputerName**</span><span class="sxs-lookup"><span data-stu-id="0df57-127">**PSComputerName**</span></span>|<span data-ttu-id="0df57-128">{comp}</span><span class="sxs-lookup"><span data-stu-id="0df57-128">{comp}</span></span>|
   |<span data-ttu-id="0df57-129">**PSCredential**</span><span class="sxs-lookup"><span data-stu-id="0df57-129">**PSCredential**</span></span>|<span data-ttu-id="0df57-130">MachineCred</span><span class="sxs-lookup"><span data-stu-id="0df57-130">MachineCred</span></span>|

9. <span data-ttu-id="0df57-131">Adjon hozzá egy **AddComputer** tevékenység, amely a **JoinDomain** előkészítése után a **GetWmiObject** tevékenység.</span><span class="sxs-lookup"><span data-stu-id="0df57-131">Add an **AddComputer** activity to the **JoinDomain** sequence after the **GetWmiObject** activity.</span></span>

10. <span data-ttu-id="0df57-132">A tulajdonságainak szerkesztése a **AddComputer** tevékenység az alábbiak szerint.</span><span class="sxs-lookup"><span data-stu-id="0df57-132">Edit the properties of the **AddComputer** activity as follows.</span></span>

    |<span data-ttu-id="0df57-133">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="0df57-133">Property</span></span>|<span data-ttu-id="0df57-134">Érték</span><span class="sxs-lookup"><span data-stu-id="0df57-134">Value</span></span>|
    |--------------|-----------|
    |<span data-ttu-id="0df57-135">**Számítógépnév**</span><span class="sxs-lookup"><span data-stu-id="0df57-135">**ComputerName**</span></span>|<span data-ttu-id="0df57-136">{comp}</span><span class="sxs-lookup"><span data-stu-id="0df57-136">{comp}</span></span>|
    |<span data-ttu-id="0df57-137">**DomainCredential**</span><span class="sxs-lookup"><span data-stu-id="0df57-137">**DomainCredential**</span></span>|<span data-ttu-id="0df57-138">DomainCred</span><span class="sxs-lookup"><span data-stu-id="0df57-138">DomainCred</span></span>|

11. <span data-ttu-id="0df57-139">Adjon hozzá egy **RestartComputer** tevékenység, amely a **JoinDomain** előkészítése után a **AddComputer** tevékenység.</span><span class="sxs-lookup"><span data-stu-id="0df57-139">Add a **RestartComputer** activity to the **JoinDomain** sequence after the **AddComputer** activity.</span></span>

12. <span data-ttu-id="0df57-140">A tulajdonságainak szerkesztése a **RestartComputer** tevékenység az alábbiak szerint.</span><span class="sxs-lookup"><span data-stu-id="0df57-140">Edit the properties of the **RestartComputer** activity as follows.</span></span>

    |<span data-ttu-id="0df57-141">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="0df57-141">Property</span></span>|<span data-ttu-id="0df57-142">Érték</span><span class="sxs-lookup"><span data-stu-id="0df57-142">Value</span></span>|
    |--------------|-----------|
    |<span data-ttu-id="0df57-143">**Számítógépnév**</span><span class="sxs-lookup"><span data-stu-id="0df57-143">**ComputerName**</span></span>|<span data-ttu-id="0df57-144">{comp}</span><span class="sxs-lookup"><span data-stu-id="0df57-144">{comp}</span></span>|
    |<span data-ttu-id="0df57-145">**Hitelesítő adatok**</span><span class="sxs-lookup"><span data-stu-id="0df57-145">**Credential**</span></span>|<span data-ttu-id="0df57-146">MachineCred</span><span class="sxs-lookup"><span data-stu-id="0df57-146">MachineCred</span></span>|
    |<span data-ttu-id="0df57-147">**a**</span><span class="sxs-lookup"><span data-stu-id="0df57-147">**For**</span></span>|<span data-ttu-id="0df57-148">Microsoft.PowerShell.Commands.WaitForServiceTypes.PowerShell</span><span class="sxs-lookup"><span data-stu-id="0df57-148">Microsoft.PowerShell.Commands.WaitForServiceTypes.PowerShell</span></span>|
    |<span data-ttu-id="0df57-149">**Kényszerített**</span><span class="sxs-lookup"><span data-stu-id="0df57-149">**Force**</span></span>|<span data-ttu-id="0df57-150">True</span><span class="sxs-lookup"><span data-stu-id="0df57-150">True</span></span>|
    |<span data-ttu-id="0df57-151">várj</span><span class="sxs-lookup"><span data-stu-id="0df57-151">Wait</span></span>|<span data-ttu-id="0df57-152">True</span><span class="sxs-lookup"><span data-stu-id="0df57-152">True</span></span>|
    |<span data-ttu-id="0df57-153">PSComputerName</span><span class="sxs-lookup"><span data-stu-id="0df57-153">PSComputerName</span></span>|<span data-ttu-id="0df57-154">{""}</span><span class="sxs-lookup"><span data-stu-id="0df57-154">{""}</span></span>|

13. <span data-ttu-id="0df57-155">Adjon hozzá egy **GetWmiObject** tevékenység, amely a **JoinDomain** előkészítése után a **RestartComputer** tevékenység.</span><span class="sxs-lookup"><span data-stu-id="0df57-155">Add a **GetWmiObject** activity to the **JoinDomain** sequence after the **RestartComputer** activity.</span></span> <span data-ttu-id="0df57-156">Ugyanaz, mint az előző lehet a tulajdonságainak szerkesztése **GetWmiObject** tevékenység.</span><span class="sxs-lookup"><span data-stu-id="0df57-156">Edit its properties to be the same as the previous **GetWmiObject** activity.</span></span>

    <span data-ttu-id="0df57-157">Ha befejezte az eljárásokat, a munkafolyamat-Tervező ablak hasonlónak kell lennie.</span><span class="sxs-lookup"><span data-stu-id="0df57-157">When you have finished the procedures, the workflow design window should look like this.</span></span>

    <span data-ttu-id="0df57-158">![A munkafolyamat-tervezővel JoinDomain XAML](../media/joindomainworkflow.png)
    ![JoinDomain XAML munkafolyamat-tervezőben](../media/joindomainworkflow.png "JoinDomainWorkflow")</span><span class="sxs-lookup"><span data-stu-id="0df57-158">![JoinDomain XAML in Workflow designer](../media/joindomainworkflow.png)
![JoinDomain XAML in Workflow designer](../media/joindomainworkflow.png "JoinDomainWorkflow")</span></span>