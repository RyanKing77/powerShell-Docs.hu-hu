---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: A Windows PowerShell SDK telepítése
ms.assetid: c3636b45-61aa-4720-85f0-58312c4fc8f9
ms.openlocfilehash: fa876bac0c1afac24f93d11dd2e7ecfb1165cf5f
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893538"
---
# <a name="installing-the-windows-powershell-sdk"></a><span data-ttu-id="4c4fa-103">A Windows PowerShell SDK telepítése</span><span class="sxs-lookup"><span data-stu-id="4c4fa-103">Installing the Windows PowerShell SDK</span></span>

<span data-ttu-id="4c4fa-104">A következő témakör ismerteti a PowerShell SDK telepítése a Windows különböző verzióiban.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-104">The following topic describes how to install the PowerShell SDK on different versions of Windows.</span></span>

## <a name="installing-windows-powershell-30-sdk-for-windows-8-and-windows-server-2012"></a><span data-ttu-id="4c4fa-105">Windows PowerShell 3.0-s telepítése SDK for Windows 8 és Windows Server 2012-ben</span><span class="sxs-lookup"><span data-stu-id="4c4fa-105">Installing Windows PowerShell 3.0 SDK for Windows 8 and Windows Server 2012</span></span>

<span data-ttu-id="4c4fa-106">A Windows 8 és Windows Server 2012 automatikusan települ a Windows PowerShell 3.0.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-106">Windows PowerShell 3.0 is automatically installed with Windows 8 and Windows Server 2012.</span></span>
<span data-ttu-id="4c4fa-107">Emellett letöltheti és telepítheti a referenciaszerelvények a Windows PowerShell 3.0 a Windows 8 SDK részeként.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-107">In addition, you can download and install the reference assemblies for Windows PowerShell 3.0 as part of the Windows 8 SDK.</span></span>
<span data-ttu-id="4c4fa-108">Ezekkel a szerelvényekkel lehetővé teszik a parancsmagok, a szolgáltatók és a gazdagép programok írni a Windows PowerShell 3.0.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-108">These assemblies allow you to write cmdlets, providers, and host programs for Windows PowerShell 3.0.</span></span>
<span data-ttu-id="4c4fa-109">Amikor telepíti a Windows SDK for Windows 8, a Windows PowerShell-szerelvények automatikusan települnek a referencia-szerelvény mappában, a `\Program Files (x86)\Reference Assemblies\Microsoft\WindowsPowerShell\3.0`.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-109">When you install the Windows SDK for Windows 8, the Windows PowerShell assemblies are automatically installed in the reference assembly folder, in `\Program Files (x86)\Reference Assemblies\Microsoft\WindowsPowerShell\3.0`.</span></span>
<span data-ttu-id="4c4fa-110">További információkért lásd: a [Windows 8 SDK letöltési hely](https://developer.microsoft.com/en-us/windows/downloads/sdk-archive).</span><span class="sxs-lookup"><span data-stu-id="4c4fa-110">For more information, see the [Windows 8 SDK download site](https://developer.microsoft.com/en-us/windows/downloads/sdk-archive).</span></span>
<span data-ttu-id="4c4fa-111">Windows PowerShell-Kódminták a fejlesztői központ is érhetők el.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-111">Windows PowerShell code samples are also available on the Development Center.</span></span>
<span data-ttu-id="4c4fa-112">További információkért tekintse meg a mintául szolgáló asztali kódlapot az [Dev center webhely](https://code.msdn.microsoft.com:443/windowsdesktop/).</span><span class="sxs-lookup"><span data-stu-id="4c4fa-112">For more information, see the Desktop code sample page on the [Dev center site](https://code.msdn.microsoft.com:443/windowsdesktop/).</span></span>

<span data-ttu-id="4c4fa-113">Emellett a Windows PowerShell 3.0 is visszafelé kompatibilis az Windows PowerShell 2.0 SDK-val, amely számos olyan Kódminták.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-113">In addition, Windows PowerShell 3.0 is backwards-compatible with the Windows PowerShell 2.0 SDK, which includes a number of code samples.</span></span>
<span data-ttu-id="4c4fa-114">A Windows PowerShell 2.0 SDK letöltése a további információkért lásd az alábbi.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-114">For more information on how to download the Windows PowerShell 2.0 SDK, see below.</span></span>
<span data-ttu-id="4c4fa-115">(Vegye figyelembe, hogy a Windows 8 és Windows PowerShell 3.0 kompatibilis a 2.0-s mintakódokat, amelyek nem telepíthető Windows PowerShell 2.0 a Windows 8 platform.)</span><span class="sxs-lookup"><span data-stu-id="4c4fa-115">(Note that while the 2.0 code samples are compatible with Windows 8 and Windows PowerShell 3.0, you cannot install Windows PowerShell 2.0 on a Windows 8 platform.)</span></span>

## <a name="installing-windows-powershell-30-sdk-for-windows-7-and-windows-server-2008-r2"></a><span data-ttu-id="4c4fa-116">Windows PowerShell 3.0-s telepítése SDK for Windows 7 és Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="4c4fa-116">Installing Windows PowerShell 3.0 SDK for Windows 7 and Windows Server 2008 R2</span></span>

<span data-ttu-id="4c4fa-117">Windows 7 és Windows Server 2008 R2 automatikusan rendelkezik a PowerShell 2.0 telepítve van.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-117">Windows 7 and Windows Server 2008 R2 automatically have PowerShell 2.0 installed.</span></span>
<span data-ttu-id="4c4fa-118">Ezenkívül telepítheti a PowerShell 3.0 ezen rendszerek.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-118">In addition, you can install PowerShell 3.0 on these systems.</span></span>
<span data-ttu-id="4c4fa-119">(További információkért lásd: [Windows PowerShell telepítése](Installing-Windows-PowerShell.md).).</span><span class="sxs-lookup"><span data-stu-id="4c4fa-119">(For more information, see [Installing Windows PowerShell](Installing-Windows-PowerShell.md).).</span></span>
<span data-ttu-id="4c4fa-120">A fent leírtaknak megfelelően a Windows 7 és Windows Server 2008 R2 is telepítheti a Windows 8 SDK-t.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-120">As described above, you can also install the Windows 8 SDK on Windows 7 and Windows Server 2008 R2.</span></span>

## <a name="installing-windows-powershell-20-sdk-for-windows-7-vista-xp-server-2003-and-server-2008"></a><span data-ttu-id="4c4fa-121">Windows PowerShell 2.0 telepítése a Windows 7, Vista, XP, Server 2003 és a Server 2008 SDK</span><span class="sxs-lookup"><span data-stu-id="4c4fa-121">Installing Windows PowerShell 2.0 SDK for Windows 7, Vista, XP, Server 2003, and Server 2008</span></span>

<span data-ttu-id="4c4fa-122">A Windows PowerShell 2.0 SDK-t biztosít a referenciaszerelvények parancsmagok, a szolgáltatók és az üzemeltetési alkalmazások írása szükséges, és a C# minta-kódot, amely kiindulási pontként is használható, ha a kódírás megkezdése biztosít.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-122">The Windows PowerShell 2.0 SDK provides the reference assemblies needed to write cmdlets, providers, and hosting applications, and it provides C# sample code that can be used as the starting point when you begin writing code.</span></span>

<span data-ttu-id="4c4fa-123">Ez az SDK telepítése: [Windows PowerShell 2.0 SDK-t](http://www.microsoft.com/en-us/download/details.aspx?id=2560).</span><span class="sxs-lookup"><span data-stu-id="4c4fa-123">To install this SDK, see [Windows PowerShell 2.0 SDK](http://www.microsoft.com/en-us/download/details.aspx?id=2560).</span></span>

## <a name="reference-assemblies"></a><span data-ttu-id="4c4fa-124">Referencia-szerelvények</span><span class="sxs-lookup"><span data-stu-id="4c4fa-124">Reference assemblies</span></span>

<span data-ttu-id="4c4fa-125">Referenciaszerelvények alapértelmezés szerint a következő helyen települnek: `c:\Program Files\Reference Assemblies\Microsoft\WindowsPowerShell\V1.0`.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-125">Reference assemblies are installed in the following location by default: `c:\Program Files\Reference Assemblies\Microsoft\WindowsPowerShell\V1.0`.</span></span>

> [!NOTE] 
> <span data-ttu-id="4c4fa-126">A Windows PowerShell 2.0 szerelvényeket elleni lefordított kódot nem tölthetők be Windows PowerShell 1.0-s telepítésekre.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-126">Code that is compiled against the Windows PowerShell 2.0 assemblies cannot be loaded into Windows PowerShell 1.0 installations.</span></span>
> <span data-ttu-id="4c4fa-127">Azonban a Windows PowerShell 1.0-szerelvények elleni lefordított kódot töltődnek be a Windows PowerShell 2.0-s telepítésekre.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-127">However, code that is compiled against the Windows PowerShell 1.0 assemblies can be loaded into Windows PowerShell 2.0 installations.</span></span>

## <a name="samples"></a><span data-ttu-id="4c4fa-128">Minták</span><span class="sxs-lookup"><span data-stu-id="4c4fa-128">Samples</span></span>

<span data-ttu-id="4c4fa-129">Kódminták alapértelmezés szerint a következő helyen települnek: `C:\Program Files\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\`.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-129">Code samples are installed in the following location by default: `C:\Program Files\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\`.</span></span>

<span data-ttu-id="4c4fa-130">A következő szakaszok rövid leírását tartalmazza minden egyes a minta működésével.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-130">The following sections provide a brief description of what each sample does.</span></span>

## <a name="cmdlet-samples"></a><span data-ttu-id="4c4fa-131">Parancsmag-minták</span><span class="sxs-lookup"><span data-stu-id="4c4fa-131">Cmdlet samples</span></span>

### <a name="getprocesssample01"></a><span data-ttu-id="4c4fa-132">GetProcessSample01</span><span class="sxs-lookup"><span data-stu-id="4c4fa-132">GetProcessSample01</span></span>

<span data-ttu-id="4c4fa-133">Bemutatja, hogyan írhat egy egyszerű parancsmag, amely lekéri az összes folyamat a helyi számítógépen.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-133">Shows how to write a simple cmdlet that gets all the processes on the local computer.</span></span>

### <a name="getprocesssample02"></a><span data-ttu-id="4c4fa-134">GetProcessSample02</span><span class="sxs-lookup"><span data-stu-id="4c4fa-134">GetProcessSample02</span></span>

<span data-ttu-id="4c4fa-135">Bemutatja, hogyan paraméterek hozzáadása a parancsmaghoz.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-135">Shows how to add parameters to the cmdlet.</span></span>
<span data-ttu-id="4c4fa-136">A parancsmag egy vagy több folyamat nevét fogadja, és a megfelelő folyamatokat adja vissza.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-136">The cmdlet takes one or more process names and returns the matching processes.</span></span>

### <a name="getprocesssample03"></a><span data-ttu-id="4c4fa-137">GetProcessSample03</span><span class="sxs-lookup"><span data-stu-id="4c4fa-137">GetProcessSample03</span></span>

<span data-ttu-id="4c4fa-138">Adja hozzá, amelyek fogadják az a folyamat bemeneti paramétereket ismerteti.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-138">Shows how to add parameters that accept input from the pipeline.</span></span>

### <a name="getprocesssample04"></a><span data-ttu-id="4c4fa-139">GetProcessSample04</span><span class="sxs-lookup"><span data-stu-id="4c4fa-139">GetProcessSample04</span></span>

<span data-ttu-id="4c4fa-140">Bemutatja, hogyan nonterminating hibáinak kezelése.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-140">Shows how to handle nonterminating errors.</span></span>

### <a name="getprocesssample05"></a><span data-ttu-id="4c4fa-141">GetProcessSample05</span><span class="sxs-lookup"><span data-stu-id="4c4fa-141">GetProcessSample05</span></span>

<span data-ttu-id="4c4fa-142">Bemutatja, hogyan megadott folyamatok listájának megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-142">Shows how to display a list of specified processes.</span></span>

### <a name="selectobject"></a><span data-ttu-id="4c4fa-143">ObjektumKijelölése</span><span class="sxs-lookup"><span data-stu-id="4c4fa-143">SelectObject</span></span>

<span data-ttu-id="4c4fa-144">Bemutatja, hogyan írhat egy szűrőt, hogy csak bizonyos objektumok kiválasztása.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-144">Shows how to write a filter to select only certain objects.</span></span>

### <a name="selectstring"></a><span data-ttu-id="4c4fa-145">SelectString</span><span class="sxs-lookup"><span data-stu-id="4c4fa-145">SelectString</span></span>

<span data-ttu-id="4c4fa-146">Bemutatja, hogyan fájlok megadott mintákat kereshet.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-146">Shows how to search files for specified patterns.</span></span>

### <a name="stopprocesssample01"></a><span data-ttu-id="4c4fa-147">StopProcessSample01</span><span class="sxs-lookup"><span data-stu-id="4c4fa-147">StopProcessSample01</span></span>

<span data-ttu-id="4c4fa-148">Bemutatja, hogyan valósíthat meg egy *PassThru* paramétert, és hogyan felé irányuló hívások szerinti felhasználói visszajelzés kérése a [ShouldProcess](/dotnet/api/system.management.automation.cmdlet.shouldprocess) és [ShouldContinue](/dotnet/api/system.management.automation.cmdlet.shouldcontinue) módszereket.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-148">Shows how to implement a *PassThru* parameter, and how to request user feedback by calls to the [ShouldProcess](/dotnet/api/system.management.automation.cmdlet.shouldprocess) and [ShouldContinue](/dotnet/api/system.management.automation.cmdlet.shouldcontinue) methods.</span></span>
<span data-ttu-id="4c4fa-149">A felhasználóknak megadniuk a *PassThru* paraméter szeretne egy objektumot ad vissza a parancsmag kényszerítése</span><span class="sxs-lookup"><span data-stu-id="4c4fa-149">Users specify the *PassThru* parameter when they want to force the cmdlet to return an object,</span></span>

### <a name="stopprocesssample02"></a><span data-ttu-id="4c4fa-150">StopProcessSample02</span><span class="sxs-lookup"><span data-stu-id="4c4fa-150">StopProcessSample02</span></span>

<span data-ttu-id="4c4fa-151">Megjeleníti egy adott folyamat leállítása.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-151">Shows how to stop a specific process.</span></span>

### <a name="stopprocesssample03"></a><span data-ttu-id="4c4fa-152">StopProcessSample03</span><span class="sxs-lookup"><span data-stu-id="4c4fa-152">StopProcessSample03</span></span>

<span data-ttu-id="4c4fa-153">Bemutatja, hogyan deklarálja paraméterek aliasok és a hogyan támogatja a helyettesítő karaktereket.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-153">Shows how to declare aliases for parameters and how to support wildcards.</span></span>

### <a name="stopprocesssample04"></a><span data-ttu-id="4c4fa-154">StopProcessSample04</span><span class="sxs-lookup"><span data-stu-id="4c4fa-154">StopProcessSample04</span></span>

<span data-ttu-id="4c4fa-155">Mutatja be jelentenie paraméterkészlettel, az objektum, amely a parancsmag kimenetként, és hogyan adja meg az alapértelmezett paramétert használja.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-155">Shows how to declare parameter sets, the object that the cmdlet takes as input, and how to specify the default parameter set to use.</span></span>

## <a name="remoting-samples"></a><span data-ttu-id="4c4fa-156">Távoli eljáráshívás minták</span><span class="sxs-lookup"><span data-stu-id="4c4fa-156">Remoting samples</span></span>

### <a name="remoterunspace01"></a><span data-ttu-id="4c4fa-157">RemoteRunspace01</span><span class="sxs-lookup"><span data-stu-id="4c4fa-157">RemoteRunspace01</span></span>

<span data-ttu-id="4c4fa-158">Bemutatja, hogyan hozhat létre egy távoli futási teret, amely a távoli kapcsolat létesítésére szolgál.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-158">Shows how to create a remote runspace that is used to establish a remote connection.</span></span>

### <a name="remoterunspacepool01"></a><span data-ttu-id="4c4fa-159">RemoteRunspacePool01</span><span class="sxs-lookup"><span data-stu-id="4c4fa-159">RemoteRunspacePool01</span></span>

<span data-ttu-id="4c4fa-160">Bemutatja, hogyan hozható létre egy távoli futási teret készletet, és hogyan egyidejű futtatását több parancs a készlet használatával.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-160">Shows how to construct a remote runspace pool and how to run multiple commands concurrently by using this pool.</span></span>

### <a name="serialization01"></a><span data-ttu-id="4c4fa-161">Serialization01</span><span class="sxs-lookup"><span data-stu-id="4c4fa-161">Serialization01</span></span>

<span data-ttu-id="4c4fa-162">Bemutatja, hogyan tekintse meg egy meglévő .NET-osztályt, és győződjön meg arról, hogy ez az osztály a kiválasztott nyilvános tulajdonságok alapján adatai megmaradnak szerializálás/deszerializálás között.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-162">Shows how to look at an existing .NET class and make sure that information from selected public properties of this class is preserved across serialization/deserialization.</span></span>

### <a name="serialization02"></a><span data-ttu-id="4c4fa-163">Serialization02</span><span class="sxs-lookup"><span data-stu-id="4c4fa-163">Serialization02</span></span>

<span data-ttu-id="4c4fa-164">Tekintse meg egy meglévő .NET-osztály, és győződjön meg arról, hogy ez az osztály példánya származó információk esetén is megőrződik szerializálás/deszerializálás között az információ nem érhető el a nyilvános tulajdonságok osztály mutatja.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-164">Shows how to look at an existing .NET class and make sure that information from instance of this class is preserved across serialization/deserialization when the information is not available in public properties of the class.</span></span>

### <a name="serialization03"></a><span data-ttu-id="4c4fa-165">Serialization03</span><span class="sxs-lookup"><span data-stu-id="4c4fa-165">Serialization03</span></span>

<span data-ttu-id="4c4fa-166">Bemutatja, hogyan tekintse meg egy meglévő .NET-osztályt, és győződjön meg arról, hogy ez az osztály és származtatott osztályainak példányok deszerializálni (rehydrated) élő .NET-objektumokká vannak.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-166">Shows how to look at an existing .NET class and make sure that instances of this class and of derived classes are deserialized (rehydrated) into live .NET objects.</span></span>

## <a name="event-samples"></a><span data-ttu-id="4c4fa-167">Esemény-minták</span><span class="sxs-lookup"><span data-stu-id="4c4fa-167">Event samples</span></span>

### <a name="event01"></a><span data-ttu-id="4c4fa-168">Event01</span><span class="sxs-lookup"><span data-stu-id="4c4fa-168">Event01</span></span>

<span data-ttu-id="4c4fa-169">Bemutatja, hogyan hozhat létre-eseményregisztráció parancsmag ObjectEventRegistrationBase kapcsolatból származtatott kapcsolatot.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-169">Shows how to create a cmdlet for event registration by deriving from ObjectEventRegistrationBase.</span></span>

### <a name="event02"></a><span data-ttu-id="4c4fa-170">Event02</span><span class="sxs-lookup"><span data-stu-id="4c4fa-170">Event02</span></span>

<span data-ttu-id="4c4fa-171">Bemutatja, hogyan jeleníti meg, amelyek akkor jönnek létre, a távoli számítógépeken lévő Windows PowerShell-események, értesítések fogadása.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-171">Shows how to shows how to receive notifications of Windows PowerShell events that are generated on remote computers.</span></span>
<span data-ttu-id="4c4fa-172">A PSEventReceived esemény keresztül használja a [futási térben](/dotnet/api/system.management.automation.runspaces.runspace) osztály.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-172">It uses the PSEventReceived event exposed through the [Runspace](/dotnet/api/system.management.automation.runspaces.runspace) class.</span></span>

## <a name="hosting-application-samples"></a><span data-ttu-id="4c4fa-173">Üzemeltetési alkalmazásminták</span><span class="sxs-lookup"><span data-stu-id="4c4fa-173">Hosting application samples</span></span>

### <a name="runspace01"></a><span data-ttu-id="4c4fa-174">Runspace01</span><span class="sxs-lookup"><span data-stu-id="4c4fa-174">Runspace01</span></span>

<span data-ttu-id="4c4fa-175">Bemutatja, hogyan használható a [PowerShell](/dotnet/api/system.management.automation.powershell) futtatásához az osztály a [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) parancsmag szinkron módon történik.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-175">Shows how to use the [PowerShell](/dotnet/api/system.management.automation.powershell) class to run the [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) cmdlet synchronously.</span></span>
<span data-ttu-id="4c4fa-176">A [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) parancsmag ad vissza [folyamat](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objektumot a helyi számítógépen futó összes folyamat.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-176">The [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) cmdlet returns [Process](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objects for each process running on the local computer.</span></span>

### <a name="runspace02"></a><span data-ttu-id="4c4fa-177">Runspace02</span><span class="sxs-lookup"><span data-stu-id="4c4fa-177">Runspace02</span></span>

<span data-ttu-id="4c4fa-178">Bemutatja, hogyan használható a [PowerShell](/dotnet/api/system.management.automation.powershell) futtatásához az osztály a [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) és [Sort-Object](/powershell/module/Microsoft.PowerShell.Utility/Sort-Object) parancsmagok szinkron módon történik.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-178">Shows how to use the [PowerShell](/dotnet/api/system.management.automation.powershell) class to run the [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) and [Sort-Object](/powershell/module/Microsoft.PowerShell.Utility/Sort-Object) cmdlets synchronously.</span></span>
<span data-ttu-id="4c4fa-179">A [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) parancsmag ad vissza [folyamat](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objektumot a helyi számítógépen futó összes folyamat és a `Sort-Object` az objektumok alapján rendezi a [azonosító](https://technet.microsoft.com/library/system.diagnostics.process.id.aspx) tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-179">The [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) cmdlet returns [Process](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objects for each process running on the local computer, and the `Sort-Object` sorts the objects based on their [Id](https://technet.microsoft.com/library/system.diagnostics.process.id.aspx) property.</span></span>
<span data-ttu-id="4c4fa-180">Az eredmények az alábbi parancsok használatával jelenik meg egy [DataGridView](https://technet.microsoft.com/library/system.windows.forms.datagridview.aspx) vezérlő.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-180">The results of these commands is displayed by using a [DataGridView](https://technet.microsoft.com/library/system.windows.forms.datagridview.aspx) control.</span></span>

### <a name="runspace03"></a><span data-ttu-id="4c4fa-181">Runspace03</span><span class="sxs-lookup"><span data-stu-id="4c4fa-181">Runspace03</span></span>

<span data-ttu-id="4c4fa-182">Bemutatja, hogyan használható a [PowerShell](/dotnet/api/system.management.automation.powershell) osztály parancsfájllal szinkron módon történik, és nem megszakító hibáinak kezelése.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-182">Shows how to use the [PowerShell](/dotnet/api/system.management.automation.powershell) class to run a script synchronously, and how to handle non-terminating errors.</span></span>
<span data-ttu-id="4c4fa-183">A parancsfájl folyamat nevének listáját fogadja, és ezután lekéri a folyamatokat.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-183">The script receives a list of process names and then retrieves those processes.</span></span>
<span data-ttu-id="4c4fa-184">A parancsfájl, beleértve a parancsfájl futtatásakor létrehozott megszakítást nem okozó hibákat is az eredményeket a konzolablakban jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-184">The results of the script, including any non-terminating errors that were generated when running the script, are displayed in a console window.</span></span>

### <a name="runspace04"></a><span data-ttu-id="4c4fa-185">Runspace04</span><span class="sxs-lookup"><span data-stu-id="4c4fa-185">Runspace04</span></span>

<span data-ttu-id="4c4fa-186">Bemutatja, hogyan használhatja a [PowerShell](/dotnet/api/system.management.automation.powershell) osztály parancsokat futtathat, és hogyan catch okozott a parancsok futtatásakor megszakítást hibák.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-186">Shows how to use the [PowerShell](/dotnet/api/system.management.automation.powershell) class to run commands, and how to catch terminating errors that are thrown when running the commands.</span></span>
<span data-ttu-id="4c4fa-187">Két parancsok futtatása, és az utolsó parancs, amely nem érvényes a paraméter argumentumként átadott.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-187">Two commands are run, and the last command is passed a parameter argument that is not valid.</span></span>
<span data-ttu-id="4c4fa-188">Ennek eredményeképpen nem lesznek visszaadva, és a megszakító hiba lépett fel.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-188">As a result, no objects are returned and a terminating error is thrown.</span></span>

### <a name="runspace05"></a><span data-ttu-id="4c4fa-189">Runspace05</span><span class="sxs-lookup"><span data-stu-id="4c4fa-189">Runspace05</span></span>

<span data-ttu-id="4c4fa-190">Bemutatja, hogyan adja hozzá a beépülő modul segítségével egy [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate) objektumot, hogy a beépülő modul a parancsmag érhető el a futási térben megnyitásakor.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-190">Shows how to add a snap-in to an [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate) object so that the cmdlet of the snap-in is available when the runspace is opened.</span></span>
<span data-ttu-id="4c4fa-191">A beépülő modult biztosít a Get-Proc parancsmag (határozzák meg a [GetProcessSample01 minta](https://technet.microsoft.com/library/ff602028.aspx)), amely a szinkron módon fut egy [PowerShell](/dotnet/api/system.management.automation.powershell) objektum.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-191">The snap-in provides a Get-Proc cmdlet (defined by the [GetProcessSample01 Sample](https://technet.microsoft.com/library/ff602028.aspx)) that is run synchronously by using a [PowerShell](/dotnet/api/system.management.automation.powershell) object.</span></span>

### <a name="runspace06"></a><span data-ttu-id="4c4fa-192">Runspace06</span><span class="sxs-lookup"><span data-stu-id="4c4fa-192">Runspace06</span></span>

<span data-ttu-id="4c4fa-193">Bemutatja, hogyan modulhoz hozzáadása egy [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate) objektumot, hogy a modul betöltése a futási térben megnyitásakor.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-193">Shows how to add a module to an [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate) object so that the module is loaded when the runspace is opened.</span></span>
<span data-ttu-id="4c4fa-194">A modul adja meg a Get-Proc parancsmag (határozzák meg a [GetProcessSample02 minta](https://technet.microsoft.com/library/ff602027.aspx)), amely a szinkron módon fut egy [PowerShell](/dotnet/api/system.management.automation.powershell) objektum.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-194">The module provides a Get-Proc cmdlet (defined by the [GetProcessSample02 Sample](https://technet.microsoft.com/library/ff602027.aspx)) that is run synchronously by using a [PowerShell](/dotnet/api/system.management.automation.powershell) object.</span></span>

### <a name="runspace07"></a><span data-ttu-id="4c4fa-195">Runspace07</span><span class="sxs-lookup"><span data-stu-id="4c4fa-195">Runspace07</span></span>

<span data-ttu-id="4c4fa-196">Bemutatja, hogyan hozhat létre egy futási teret, és a futási térben használatával két parancsmag használatával szinkron módon futnak a [PowerShell](/dotnet/api/system.management.automation.powershell) objektum.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-196">Shows how to create a runspace, and then use that runspace to run two cmdlets synchronously by using a [PowerShell](/dotnet/api/system.management.automation.powershell) object.</span></span>

### <a name="runspace08"></a><span data-ttu-id="4c4fa-197">Runspace08</span><span class="sxs-lookup"><span data-stu-id="4c4fa-197">Runspace08</span></span>

<span data-ttu-id="4c4fa-198">Bemutatja, hogyan parancsokat és argumentumokat adhat hozzá, a folyamat egy [PowerShell](/dotnet/api/system.management.automation.powershell) objektum és a parancsok futtatása szinkron módon történik.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-198">Shows how to add commands and arguments to the pipeline of a [PowerShell](/dotnet/api/system.management.automation.powershell) object and how to run the commands synchronously.</span></span>

### <a name="runspace09"></a><span data-ttu-id="4c4fa-199">Runspace09</span><span class="sxs-lookup"><span data-stu-id="4c4fa-199">Runspace09</span></span>

<span data-ttu-id="4c4fa-200">Mutatja be, a folyamat egy parancsfájl hozzáadása egy [PowerShell](/dotnet/api/system.management.automation.powershell) objektum és a parancsfájl futtatása aszinkron módon történik.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-200">Shows how to add a script to the pipeline of a [PowerShell](/dotnet/api/system.management.automation.powershell) object and how to run the script asynchronously.</span></span>
<span data-ttu-id="4c4fa-201">Események a szkript kimenetének kezelésére szolgálnak.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-201">Events are used to handle the output of the script.</span></span>

### <a name="runspace10"></a><span data-ttu-id="4c4fa-202">Runspace10</span><span class="sxs-lookup"><span data-stu-id="4c4fa-202">Runspace10</span></span>

<span data-ttu-id="4c4fa-203">Bemutatja, hogyan hozhat létre egy alapértelmezett kezdeti munkamenet-állapot, a parancsmag hozzáadása a [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate), hogyan hozhat létre egy futási teret, amely a kezdeti munkamenet-állapotot használ, és annak használatával futtassa a parancsot egy [PowerShell](/dotnet/api/system.management.automation.powershell)objektum.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-203">Shows how to create a default initial session state, how to add a cmdlet to the [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate), how to create a runspace that uses the initial session state, and how to run the command by using a [PowerShell](/dotnet/api/system.management.automation.powershell) object.</span></span>

### <a name="runspace11"></a><span data-ttu-id="4c4fa-204">Runspace11</span><span class="sxs-lookup"><span data-stu-id="4c4fa-204">Runspace11</span></span>

<span data-ttu-id="4c4fa-205">Bemutatja, hogyan használható a [ProxyCommand](/dotnet/api/system.management.automation.proxycommand) osztállyal hoz létre, amely meghív egy meglévő parancsmagot, de korlátozza az elérhető paraméterek készletét proxy parancsot.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-205">Shows how to use the [ProxyCommand](/dotnet/api/system.management.automation.proxycommand) class to create a proxy command that calls an existing cmdlet, but restricts the set of available parameters.</span></span>
<span data-ttu-id="4c4fa-206">A proxy parancsot, amellyel egy korlátozott futási térrel hozzon létre egy kezdeti munkamenet-állapothoz kerül.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-206">The proxy command is then added to an initial session state that is used to create a constrained runspace.</span></span>
<span data-ttu-id="4c4fa-207">Ez azt jelenti, hogy a felhasználó hozzáférhet-e az a Funkciók, a parancsmag csak a proxy parancs keresztül.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-207">This means that the user can access the functionality of the cmdlet only through the proxy command.</span></span>

### <a name="powershell01"></a><span data-ttu-id="4c4fa-208">PowerShell01</span><span class="sxs-lookup"><span data-stu-id="4c4fa-208">PowerShell01</span></span>

<span data-ttu-id="4c4fa-209">Bemutatja, hogyan hozzon létre egy korlátozott futási térrel egy [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate) objektum.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-209">Shows how to create a constrained runspace using an [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate) object.</span></span>

### <a name="powershell02"></a><span data-ttu-id="4c4fa-210">PowerShell02</span><span class="sxs-lookup"><span data-stu-id="4c4fa-210">PowerShell02</span></span>

<span data-ttu-id="4c4fa-211">Bemutatja, hogyan egy futási térben készletet használja egyidejűleg több parancsok futtatásához.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-211">Shows how to use a runspace pool to run multiple commands concurrently.</span></span>

## <a name="host-samples"></a><span data-ttu-id="4c4fa-212">Gazdagép-minták</span><span class="sxs-lookup"><span data-stu-id="4c4fa-212">Host samples</span></span>

### <a name="host01"></a><span data-ttu-id="4c4fa-213">Host01</span><span class="sxs-lookup"><span data-stu-id="4c4fa-213">Host01</span></span>

<span data-ttu-id="4c4fa-214">Bemutatja, hogyan valósíthat meg egy egyéni gazdagép használó gazdagép-alkalmazás.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-214">Shows how to implement a host application that uses a custom host.</span></span>
<span data-ttu-id="4c4fa-215">A mintában egy futási teret jön létre, amely az egyéni gazdagépet használ, majd a [PowerShell](/dotnet/api/system.management.automation.powershell) API, amely meghívja a "kilépéshez" parancsfájl futtatására szolgál.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-215">In this sample a runspace is created that uses the custom host, and then the [PowerShell](/dotnet/api/system.management.automation.powershell) API is used to run a script that calls "exit".</span></span>
<span data-ttu-id="4c4fa-216">A gazdaalkalmazást majd megvizsgálja a szkript a kimenetét, és az eredményeket kiírja.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-216">The host application then looks at the output of the script and prints out the results.</span></span>

### <a name="host02"></a><span data-ttu-id="4c4fa-217">Host02</span><span class="sxs-lookup"><span data-stu-id="4c4fa-217">Host02</span></span>

<span data-ttu-id="4c4fa-218">Bemutatja, hogyan írhat egy gazdagép egy egyéni gazdagép megvalósítás mellett a Windows PowerShell modul használó alkalmazás.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-218">Shows how to write a host application that uses the Windows PowerShell runtime along with a custom host implementation.</span></span>
<span data-ttu-id="4c4fa-219">A gazdaalkalmazást állítja be a gazdagép kulturális környezet német, lefut a [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) parancsmagot, és megjeleníti az eredményeket, látnák őket a német pwrsh.exe, és ezután jelenít meg az aktuális dátumát és időpontját segítségével.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-219">The host application sets the host culture to German, runs the [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) cmdlet and displays the results as you would see them by using pwrsh.exe, and then prints out the current data and time in German.</span></span>

### <a name="host03"></a><span data-ttu-id="4c4fa-220">Host03</span><span class="sxs-lookup"><span data-stu-id="4c4fa-220">Host03</span></span>

<span data-ttu-id="4c4fa-221">Bemutatja, hogyan hozhat létre olyan interaktív konzol-alapú gazdagép alkalmazás, amely beolvassa a parancsok a parancssorból, a parancsok végrehajtása és az eredményeket a konzolon jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-221">Shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span>

### <a name="host04"></a><span data-ttu-id="4c4fa-222">Host04</span><span class="sxs-lookup"><span data-stu-id="4c4fa-222">Host04</span></span>

<span data-ttu-id="4c4fa-223">Bemutatja, hogyan hozhat létre olyan interaktív konzol-alapú gazdagép alkalmazás, amely beolvassa a parancsok a parancssorból, a parancsok végrehajtása és az eredményeket a konzolon jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-223">Shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span>
<span data-ttu-id="4c4fa-224">A gazdaalkalmazást megjelenítésének utasításokat, amelyek lehetővé teszik a felhasználó megadhatja a több lehetőség is támogatja.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-224">This host application also supports displaying prompts that allow the user to specify multiple choices.</span></span>

### <a name="host05"></a><span data-ttu-id="4c4fa-225">Host05</span><span class="sxs-lookup"><span data-stu-id="4c4fa-225">Host05</span></span>

<span data-ttu-id="4c4fa-226">Bemutatja, hogyan hozhat létre olyan interaktív konzol-alapú gazdagép alkalmazás, amely beolvassa a parancsok a parancssorból, a parancsok végrehajtása és az eredményeket a konzolon jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-226">Shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span>
<span data-ttu-id="4c4fa-227">A gazdaalkalmazást is támogatja a távoli számítógépek hívásainak a [Enter-PsSession](/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession) és [kilépési-PsSession](/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession) parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-227">This host application also supports calls to remote computers by using the [Enter-PsSession](/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession) and [Exit-PsSession](/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession) cmdlets.</span></span>

### <a name="host06"></a><span data-ttu-id="4c4fa-228">Host06</span><span class="sxs-lookup"><span data-stu-id="4c4fa-228">Host06</span></span>

<span data-ttu-id="4c4fa-229">Bemutatja, hogyan hozhat létre olyan interaktív konzol-alapú gazdagép alkalmazás, amely beolvassa a parancsok a parancssorból, a parancsok végrehajtása és az eredményeket a konzolon jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-229">Shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span>
<span data-ttu-id="4c4fa-230">Emellett ez a példa a jogkivonatokat létrehozó API-k segítségével adja meg a felhasználó által beírt szöveg színe.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-230">In addition, this sample uses the Tokenizer APIs to specify the color of the text that is entered by the user.</span></span>

## <a name="provider-samples"></a><span data-ttu-id="4c4fa-231">Szolgáltató minták</span><span class="sxs-lookup"><span data-stu-id="4c4fa-231">Provider samples</span></span>

### <a name="accessdbprovidersample01"></a><span data-ttu-id="4c4fa-232">AccessDBProviderSample01</span><span class="sxs-lookup"><span data-stu-id="4c4fa-232">AccessDBProviderSample01</span></span>

<span data-ttu-id="4c4fa-233">Bemutatja, hogyan deklaráljon egy szolgáltató osztályt, amely közvetlenül a [CmdletProvider](/dotnet/api/system.management.automation.provider.cmdletprovider) osztály.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-233">Shows how to declare a provider class that derives directly from the [CmdletProvider](/dotnet/api/system.management.automation.provider.cmdletprovider) class.</span></span>
<span data-ttu-id="4c4fa-234">Része Itt csak a teljesség.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-234">It is included here only for completeness.</span></span>

### <a name="accessdbprovidersample02"></a><span data-ttu-id="4c4fa-235">AccessDBProviderSample02</span><span class="sxs-lookup"><span data-stu-id="4c4fa-235">AccessDBProviderSample02</span></span>

<span data-ttu-id="4c4fa-236">Bemutatja, hogyan felülírja a [NewDrive](/dotnet/api/system.management.automation.provider.drivecmdletprovider.newdrive) és [RemoveDrive](/dotnet/api/system.management.automation.provider.drivecmdletprovider.removedrive) módszereket támogatja a hívást a `New-PSDrive` és `Remove-PSDrive` parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-236">Shows how to overwrite the [NewDrive](/dotnet/api/system.management.automation.provider.drivecmdletprovider.newdrive) and [RemoveDrive](/dotnet/api/system.management.automation.provider.drivecmdletprovider.removedrive) methods to support calls to the `New-PSDrive` and `Remove-PSDrive` cmdlets.</span></span>
<span data-ttu-id="4c4fa-237">Ebben a példában a szolgáltató osztálya származik a [DriveCmdletProvider](/dotnet/api/system.management.automation.provider.drivecmdletprovider) osztály.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-237">The provider class in this sample derives from the [DriveCmdletProvider](/dotnet/api/system.management.automation.provider.drivecmdletprovider) class.</span></span>

### <a name="accessdbprovidersample03"></a><span data-ttu-id="4c4fa-238">AccessDBProviderSample03</span><span class="sxs-lookup"><span data-stu-id="4c4fa-238">AccessDBProviderSample03</span></span>

<span data-ttu-id="4c4fa-239">Bemutatja, hogyan felülírja a [GetItem](/dotnet/api/system.management.automation.provider.itemcmdletprovider.getitem) és [SetItem](/dotnet/api/system.management.automation.provider.itemcmdletprovider.setitem) módszereket támogatja a hívást a `Get-Item` és `Set-Item` parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-239">Shows how to overwrite the [GetItem](/dotnet/api/system.management.automation.provider.itemcmdletprovider.getitem) and [SetItem](/dotnet/api/system.management.automation.provider.itemcmdletprovider.setitem) methods to support calls to the `Get-Item` and `Set-Item` cmdlets.</span></span>
<span data-ttu-id="4c4fa-240">Ebben a példában a szolgáltató osztálya származik a [ItemCmdletProvider](/dotnet/api/system.management.automation.provider.itemcmdletprovider) osztály.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-240">The provider class in this sample derives from the [ItemCmdletProvider](/dotnet/api/system.management.automation.provider.itemcmdletprovider) class.</span></span>

### <a name="accessdbprovidersample04"></a><span data-ttu-id="4c4fa-241">AccessDBProviderSample04</span><span class="sxs-lookup"><span data-stu-id="4c4fa-241">AccessDBProviderSample04</span></span>

<span data-ttu-id="4c4fa-242">Bemutatja, hogyan tároló módszerek támogatásához a hívásokat írja felül a `Copy-Item`, `Get-ChildItem`, `New-Item`, és `Remove-Item` parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-242">Shows how to overwrite container methods to support calls to the `Copy-Item`, `Get-ChildItem`, `New-Item`, and `Remove-Item` cmdlets.</span></span>
<span data-ttu-id="4c4fa-243">Ezek a metódusok kell végrehajtani, ha az adattár tartalmaz, amelyek olyan tárolók elemek.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-243">These methods should be implemented when the data store contains items that are containers.</span></span>
<span data-ttu-id="4c4fa-244">A tároló egy olyan csoport gyermekelemek egy közös szülő elem alatt.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-244">A container is a group of child items under a common parent item.</span></span>
<span data-ttu-id="4c4fa-245">Ebben a példában a szolgáltató osztálya származik a [ItemCmdletProvider](/dotnet/api/system.management.automation.provider.itemcmdletprovider) osztály.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-245">The provider class in this sample derives from the [ItemCmdletProvider](/dotnet/api/system.management.automation.provider.itemcmdletprovider) class.</span></span>

### <a name="accessdbprovidersample05"></a><span data-ttu-id="4c4fa-246">AccessDBProviderSample05</span><span class="sxs-lookup"><span data-stu-id="4c4fa-246">AccessDBProviderSample05</span></span>

<span data-ttu-id="4c4fa-247">Bemutatja, hogyan tároló módszerek támogatásához a hívásokat írja felül a `Move-Item` és `Join-Path` parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-247">Shows how to overwrite container methods to support calls to the `Move-Item` and `Join-Path` cmdlets.</span></span>
<span data-ttu-id="4c4fa-248">Ezek a metódusok kell végrehajtani, amikor a felhasználónak szüksége van a tárolóban lévő elemek áthelyezése, és ha az adattár tartalmaz beágyazott tárolók.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-248">These methods should be implemented when the user needs to move items within a container and if the data store contains nested containers.</span></span>
<span data-ttu-id="4c4fa-249">Ebben a példában a szolgáltató osztálya származik a [NavigationCmdletProvider](/dotnet/api/system.management.automation.provider.navigationcmdletprovider) osztály.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-249">The provider class in this sample derives from the [NavigationCmdletProvider](/dotnet/api/system.management.automation.provider.navigationcmdletprovider) class.</span></span>

### <a name="accessdbprovidersample06"></a><span data-ttu-id="4c4fa-250">AccessDBProviderSample06</span><span class="sxs-lookup"><span data-stu-id="4c4fa-250">AccessDBProviderSample06</span></span>

<span data-ttu-id="4c4fa-251">Bemutatja, hogyan tartalom módszerek támogatásához a hívásokat írja felül a `Clear-Content`, `Get-Content`, és `Set-Content` parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-251">Shows how to overwrite content methods to support calls to the `Clear-Content`, `Get-Content`, and `Set-Content` cmdlets.</span></span>
<span data-ttu-id="4c4fa-252">Ezek a metódusok kell végrehajtani, amikor a felhasználó az adattárban lévő cikkek a tartalom kezelésére kell.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-252">These methods should be implemented when the user needs to manage the content of the items in the data store.</span></span>
<span data-ttu-id="4c4fa-253">Ebben a példában a szolgáltató osztálya származik a [NavigationCmdletProvider](/dotnet/api/system.management.automation.provider.navigationcmdletprovider) osztály, és implementálja a [IContentCmdletProvider](/dotnet/api/system.management.automation.provider.icontentcmdletprovider) felületet.</span><span class="sxs-lookup"><span data-stu-id="4c4fa-253">The provider class in this sample derives from the [NavigationCmdletProvider](/dotnet/api/system.management.automation.provider.navigationcmdletprovider) class, and it implements the [IContentCmdletProvider](/dotnet/api/system.management.automation.provider.icontentcmdletprovider) interface.</span></span>