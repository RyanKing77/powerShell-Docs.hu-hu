---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A Windows PowerShell SDK telepítése"
ms.assetid: c3636b45-61aa-4720-85f0-58312c4fc8f9
ms.openlocfilehash: c6acba828e469e716c80603ec2432176652a7280
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="installing-the-windows-powershell-sdk"></a><span data-ttu-id="66ed7-103">A Windows PowerShell SDK telepítése</span><span class="sxs-lookup"><span data-stu-id="66ed7-103">Installing the Windows PowerShell SDK</span></span>

<span data-ttu-id="66ed7-104">A következő témakör ismerteti a PowerShell SDK telepíthető a Windows különböző verzióiban.</span><span class="sxs-lookup"><span data-stu-id="66ed7-104">The following topic describes how to install the PowerShell SDK on different versions of Windows.</span></span>

## <a name="installing-windows-powershell-30-sdk-for-windows-8-and-windows-server-2012"></a><span data-ttu-id="66ed7-105">A Windows PowerShell 3.0 telepítése a Windows 8 és Windows Server 2012 SDK</span><span class="sxs-lookup"><span data-stu-id="66ed7-105">Installing Windows PowerShell 3.0 SDK for Windows 8 and Windows Server 2012</span></span>

<span data-ttu-id="66ed7-106">A Windows PowerShell 3.0 automatikusan telepítve van a Windows 8 és Windows Server 2012-ben.</span><span class="sxs-lookup"><span data-stu-id="66ed7-106">Windows PowerShell 3.0 is automatically installed with Windows 8 and Windows Server 2012.</span></span>
<span data-ttu-id="66ed7-107">Emellett letöltheti és telepítheti a referencia szerelvényeket a Windows PowerShell 3.0 a Windows 8 SDK részeként.</span><span class="sxs-lookup"><span data-stu-id="66ed7-107">In addition, you can download and install the reference assemblies for Windows PowerShell 3.0 as part of the Windows 8 SDK.</span></span>
<span data-ttu-id="66ed7-108">A szerelvények engedélyezi, hogy a parancsmagok, a szolgáltatók és a gazdagépre programok írni a Windows PowerShell 3.0.</span><span class="sxs-lookup"><span data-stu-id="66ed7-108">These assemblies allow you to write cmdlets, providers, and host programs for Windows PowerShell 3.0.</span></span>
<span data-ttu-id="66ed7-109">Amikor telepíti a Windows SDK a Windows 8, a Windows PowerShell-szerelvények automatikusan települnek a referencia szerelvény mappájában, \Program fájlok (x86) \Reference Assemblies\Microsoft\WindowsPowerShell\3.0.</span><span class="sxs-lookup"><span data-stu-id="66ed7-109">When you install the Windows SDK for Windows 8, the Windows PowerShell assemblies are automatically installed in the reference assembly folder, in \Program Files (x86)\Reference Assemblies\Microsoft\WindowsPowerShell\3.0.</span></span>
<span data-ttu-id="66ed7-110">További információkért lásd: a [Windows 8 SDK letöltési hely](http://msdn.microsoft.com/windows/hardware/hh852363.aspx).</span><span class="sxs-lookup"><span data-stu-id="66ed7-110">For more information, see the [Windows 8 SDK download site](http://msdn.microsoft.com/windows/hardware/hh852363.aspx).</span></span>
<span data-ttu-id="66ed7-111">Windows PowerShell-Kódminták is rendelkezésre állnak a fejlesztői központjában.</span><span class="sxs-lookup"><span data-stu-id="66ed7-111">Windows PowerShell code samples are also available on the Development Center.</span></span>
<span data-ttu-id="66ed7-112">További információkért lásd: a minta asztali kódlap a a [Dev center webhely](http://code.msdn.microsoft.com/windowsdesktop/).</span><span class="sxs-lookup"><span data-stu-id="66ed7-112">For more information, see the Desktop code sample page on the [Dev center site](http://code.msdn.microsoft.com/windowsdesktop/).</span></span>

<span data-ttu-id="66ed7-113">Ezenkívül a Windows PowerShell 3.0 is visszafelé kompatibilis a Windows PowerShell 2.0 SDK-t, amely számos olyan mintakódok.</span><span class="sxs-lookup"><span data-stu-id="66ed7-113">In addition, Windows PowerShell 3.0 is backwards-compatible with the Windows PowerShell 2.0 SDK, which includes a number of code samples.</span></span>
<span data-ttu-id="66ed7-114">A Windows PowerShell 2.0 SDK letöltési további információkért lásd az alábbi.</span><span class="sxs-lookup"><span data-stu-id="66ed7-114">For more information on how to download the Windows PowerShell 2.0 SDK, see below.</span></span>
<span data-ttu-id="66ed7-115">(Vegye figyelembe, hogy a 2.0-s mintakódok kompatibilisek-e a Windows 8 és Windows PowerShell 3.0 összetevőt, amíg nem telepíthető Windows PowerShell 2.0 a Windows 8 platformra.)</span><span class="sxs-lookup"><span data-stu-id="66ed7-115">(Note that while the 2.0 code samples are compatible with Windows 8 and Windows PowerShell 3.0, you cannot install Windows PowerShell 2.0 on a Windows 8 platform.)</span></span>

##<a name="installing-windows-powershell-30-sdk-for-windows-7-and-windows-server-2008-r2"></a><span data-ttu-id="66ed7-116">A Windows PowerShell 3.0 telepítése a Windows 7 és Windows Server 2008 R2 SDK</span><span class="sxs-lookup"><span data-stu-id="66ed7-116">Installing Windows PowerShell 3.0 SDK for Windows 7 and Windows Server 2008 R2</span></span>

<span data-ttu-id="66ed7-117">Windows 7 és Windows Server 2008 R2 automatikusan rendelkezik a PowerShell 2.0-s verziójával.</span><span class="sxs-lookup"><span data-stu-id="66ed7-117">Windows 7 and Windows Server 2008 R2 automatically have PowerShell 2.0 installed.</span></span>
<span data-ttu-id="66ed7-118">A PowerShell 3.0 ezenkívül telepítheti a rendszerek óráit.</span><span class="sxs-lookup"><span data-stu-id="66ed7-118">In addition, you can install PowerShell 3.0 on these systems.</span></span>
<span data-ttu-id="66ed7-119">(További információkért lásd: [Windows PowerShell telepítése](Installing-Windows-PowerShell.md).).</span><span class="sxs-lookup"><span data-stu-id="66ed7-119">(For more information, see [Installing Windows PowerShell](Installing-Windows-PowerShell.md).).</span></span>
<span data-ttu-id="66ed7-120">A fent leírtaknak megfelelően is telepíthet a Windows 8 SDK a Windows 7 és Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="66ed7-120">As described above, you can also install the Windows 8 SDK on Windows 7 and Windows Server 2008 R2.</span></span>

## <a name="installing-windows-powershell-20-sdk-for-windows-7-vista-xp-server-2003-and-server-2008"></a><span data-ttu-id="66ed7-121">A Windows PowerShell 2.0 telepítése a Windows 7, Vista, XP, Server 2003 és a Server 2008 SDK</span><span class="sxs-lookup"><span data-stu-id="66ed7-121">Installing Windows PowerShell 2.0 SDK for Windows 7, Vista, XP, Server 2003, and Server 2008</span></span>

<span data-ttu-id="66ed7-122">A Windows PowerShell 2.0 SDK biztosít a hivatkozási szerelvények parancsmagok, a szolgáltatók és az üzemeltetési alkalmazások írása szükséges, és C# mintakód programozás megkezdésekor a kiindulási pontként használható biztosít.</span><span class="sxs-lookup"><span data-stu-id="66ed7-122">The Windows PowerShell 2.0 SDK provides the reference assemblies needed to write cmdlets, providers, and hosting applications, and it provides C# sample code that can be used as the starting point when you begin writing code.</span></span>

<span data-ttu-id="66ed7-123">Ez az SDK telepítéséhez tekintse át [Windows PowerShell 2.0 SDK](http://go.microsoft.com/fwlink/?LinkId=184611).</span><span class="sxs-lookup"><span data-stu-id="66ed7-123">To install this SDK, see [Windows PowerShell 2.0 SDK](http://go.microsoft.com/fwlink/?LinkId=184611).</span></span>

## <a name="reference-assemblies"></a><span data-ttu-id="66ed7-124">A hivatkozási szerelvények</span><span class="sxs-lookup"><span data-stu-id="66ed7-124">Reference assemblies</span></span>

<span data-ttu-id="66ed7-125">Alapértelmezés szerint a következő helyen vannak telepítve a hivatkozási szerelvények: `c:\Program Files\Reference Assemblies\Microsoft\WindowsPowerShell\V1.0`.</span><span class="sxs-lookup"><span data-stu-id="66ed7-125">Reference assemblies are installed in the following location by default: `c:\Program Files\Reference Assemblies\Microsoft\WindowsPowerShell\V1.0`.</span></span>

> <span data-ttu-id="66ed7-126">**Megjegyzés:**: a Windows PowerShell 2.0 szerelvények elleni lefordított kódot nem tölthetők be a Windows PowerShell 1.0 telepítések.</span><span class="sxs-lookup"><span data-stu-id="66ed7-126">**Note**: Code that is compiled against the Windows PowerShell 2.0 assemblies cannot be loaded into Windows PowerShell 1.0 installations.</span></span>
><span data-ttu-id="66ed7-127">Azonban a Windows PowerShell 1.0 szerelvények elleni lefordított kódot töltődnek be a Windows PowerShell 2.0 telepítése.</span><span class="sxs-lookup"><span data-stu-id="66ed7-127">However, code that is compiled against the Windows PowerShell 1.0 assemblies can be loaded into Windows PowerShell 2.0 installations.</span></span>

## <a name="samples"></a><span data-ttu-id="66ed7-128">Minták</span><span class="sxs-lookup"><span data-stu-id="66ed7-128">Samples</span></span>

<span data-ttu-id="66ed7-129">Kódminták alapértelmezés szerint telepítve a következő helyen: `C:\Program Files\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\`.</span><span class="sxs-lookup"><span data-stu-id="66ed7-129">Code samples are installed in the following location by default: `C:\Program Files\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\`.</span></span>

<span data-ttu-id="66ed7-130">A következő szakaszokban röviden minden egyes minta funkciója.</span><span class="sxs-lookup"><span data-stu-id="66ed7-130">The following sections provide a brief description of what each sample does.</span></span>

## <a name="cmdlet-samples"></a><span data-ttu-id="66ed7-131">Parancsmag-minták</span><span class="sxs-lookup"><span data-stu-id="66ed7-131">Cmdlet samples</span></span>
<span data-ttu-id="66ed7-132">**GetProcessSample01**</span><span class="sxs-lookup"><span data-stu-id="66ed7-132">**GetProcessSample01**</span></span>

<span data-ttu-id="66ed7-133">Bemutatja, hogyan írása egy egyszerű parancsmag, amely lekérdezi a folyamatokat a helyi számítógépen.</span><span class="sxs-lookup"><span data-stu-id="66ed7-133">Shows how to write a simple cmdlet that gets all the processes on the local computer.</span></span>

<span data-ttu-id="66ed7-134">**GetProcessSample02**</span><span class="sxs-lookup"><span data-stu-id="66ed7-134">**GetProcessSample02**</span></span>

<span data-ttu-id="66ed7-135">Bemutatja, hogyan adja meg a parancsmag paramétereit.</span><span class="sxs-lookup"><span data-stu-id="66ed7-135">Shows how to add parameters to the cmdlet.</span></span>
<span data-ttu-id="66ed7-136">A parancsmag szükséges egy vagy több folyamat neve, és a megfelelő folyamatokat adja vissza.</span><span class="sxs-lookup"><span data-stu-id="66ed7-136">The cmdlet takes one or more process names and returns the matching processes.</span></span>

<span data-ttu-id="66ed7-137">**GetProcessSample03**</span><span class="sxs-lookup"><span data-stu-id="66ed7-137">**GetProcessSample03**</span></span>

<span data-ttu-id="66ed7-138">Mutatja, amelyekben a feldolgozási sor paraméterek hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="66ed7-138">Shows how to add parameters that accept input from the pipeline.</span></span>

<span data-ttu-id="66ed7-139">**GetProcessSample04**</span><span class="sxs-lookup"><span data-stu-id="66ed7-139">**GetProcessSample04**</span></span>

<span data-ttu-id="66ed7-140">Megjeleníti a nonterminating hibák kezelésének módját.</span><span class="sxs-lookup"><span data-stu-id="66ed7-140">Shows how to handle nonterminating errors.</span></span>

<span data-ttu-id="66ed7-141">**GetProcessSample05**</span><span class="sxs-lookup"><span data-stu-id="66ed7-141">**GetProcessSample05**</span></span>

<span data-ttu-id="66ed7-142">Bemutatja, hogyan megadott folyamatok listájának megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="66ed7-142">Shows how to display a list of specified processes.</span></span>

<span data-ttu-id="66ed7-143">**ObjektumKijelölése**</span><span class="sxs-lookup"><span data-stu-id="66ed7-143">**SelectObject**</span></span>

<span data-ttu-id="66ed7-144">Bemutatja, hogyan írhat egy szűrőt, amely csak bizonyos objektumok kijelölése.</span><span class="sxs-lookup"><span data-stu-id="66ed7-144">Shows how to write a filter to select only certain objects.</span></span>

<span data-ttu-id="66ed7-145">**SelectString**</span><span class="sxs-lookup"><span data-stu-id="66ed7-145">**SelectString**</span></span>

<span data-ttu-id="66ed7-146">Bemutatja, hogyan megadott mintára fájlok kereséséhez.</span><span class="sxs-lookup"><span data-stu-id="66ed7-146">Shows how to search files for specified patterns.</span></span>

<span data-ttu-id="66ed7-147">**StopProcessSample01**</span><span class="sxs-lookup"><span data-stu-id="66ed7-147">**StopProcessSample01**</span></span>

<span data-ttu-id="66ed7-148">Bemutatja, hogyan végrehajtásához egy *PassThru* paraméter, és hogyan kérjen felhasználói visszajelzés hívásainak a [ShouldProcess](https://technet.microsoft.com/library/system.management.automation.cmdlet.shouldprocess.aspx) és [ShouldContinue](https://technet.microsoft.com/library/system.management.automation.cmdlet.shouldcontinue.aspx) módszerek.</span><span class="sxs-lookup"><span data-stu-id="66ed7-148">Shows how to implement a *PassThru* parameter, and how to request user feedback by calls to the [ShouldProcess](https://technet.microsoft.com/library/system.management.automation.cmdlet.shouldprocess.aspx) and [ShouldContinue](https://technet.microsoft.com/library/system.management.automation.cmdlet.shouldcontinue.aspx) methods.</span></span>
<span data-ttu-id="66ed7-149">Adja meg a felhasználók a *PassThru* paraméter szeretne vissza objektumot, a parancsmag kényszerítése</span><span class="sxs-lookup"><span data-stu-id="66ed7-149">Users specify the *PassThru* parameter when they want to force the cmdlet to return an object,</span></span>

<span data-ttu-id="66ed7-150">**StopProcessSample02**</span><span class="sxs-lookup"><span data-stu-id="66ed7-150">**StopProcessSample02**</span></span>

<span data-ttu-id="66ed7-151">Megjeleníti egy adott folyamat leállítása.</span><span class="sxs-lookup"><span data-stu-id="66ed7-151">Shows how to stop a specific process.</span></span>

<span data-ttu-id="66ed7-152">**StopProcessSample03**</span><span class="sxs-lookup"><span data-stu-id="66ed7-152">**StopProcessSample03**</span></span>

<span data-ttu-id="66ed7-153">Bemutatja, hogyan deklarálható paraméter aliasok és a hogyan támogatja a helyettesítő karaktereket.</span><span class="sxs-lookup"><span data-stu-id="66ed7-153">Shows how to declare aliases for parameters and how to support wildcards.</span></span>

<span data-ttu-id="66ed7-154">**StopProcessSample04**</span><span class="sxs-lookup"><span data-stu-id="66ed7-154">**StopProcessSample04**</span></span>

<span data-ttu-id="66ed7-155">Bemutatja, hogyan deklarálható paraméterkészletei, az objektum, amely a parancsmag bemeneti és a használandó alapértelmezett paraméter megadása szükséges.</span><span class="sxs-lookup"><span data-stu-id="66ed7-155">Shows how to declare parameter sets, the object that the cmdlet takes as input, and how to specify the default parameter set to use.</span></span>

## <a name="remoting-samples"></a><span data-ttu-id="66ed7-156">Távoli eljáráshívás minták</span><span class="sxs-lookup"><span data-stu-id="66ed7-156">Remoting samples</span></span>

<span data-ttu-id="66ed7-157">**RemoteRunspace01**</span><span class="sxs-lookup"><span data-stu-id="66ed7-157">**RemoteRunspace01**</span></span>

<span data-ttu-id="66ed7-158">Bemutatja, hogyan hozzon létre egy távoli futási térből, amellyel távoli kapcsolatot létesíteni.</span><span class="sxs-lookup"><span data-stu-id="66ed7-158">Shows how to create a remote runspace that is used to establish a remote connection.</span></span>

<span data-ttu-id="66ed7-159">**RemoteRunspacePool01**</span><span class="sxs-lookup"><span data-stu-id="66ed7-159">**RemoteRunspacePool01**</span></span>

<span data-ttu-id="66ed7-160">Egy távoli futási teret készlet létrehozásához és több parancs egyidejű futtatását a készlet használatával jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="66ed7-160">Shows how to construct a remote runspace pool and how to run multiple commands concurrently by using this pool.</span></span>

<span data-ttu-id="66ed7-161">**Serialization01**</span><span class="sxs-lookup"><span data-stu-id="66ed7-161">**Serialization01**</span></span>

<span data-ttu-id="66ed7-162">Bemutatja, hogyan tekintse meg egy meglévő .NET-osztályt, és győződjön meg arról, hogy ez az osztály a megadott nyilvános tulajdonságokat adatait megőrzi a szerializálás/deszerializálás között.</span><span class="sxs-lookup"><span data-stu-id="66ed7-162">Shows how to look at an existing .NET class and make sure that information from selected public properties of this class is preserved across serialization/deserialization.</span></span>

<span data-ttu-id="66ed7-163">**Serialization02**</span><span class="sxs-lookup"><span data-stu-id="66ed7-163">**Serialization02**</span></span>

<span data-ttu-id="66ed7-164">Bemutatja, hogyan tekintse meg egy meglévő .NET-osztályt, és győződjön meg arról, hogy ez az osztály példánya adatait megőrzi szerializálás/deszerializálás között, amikor az információ nem érhető el az osztály nyilvános tulajdonságai.</span><span class="sxs-lookup"><span data-stu-id="66ed7-164">Shows how to look at an existing .NET class and make sure that information from instance of this class is preserved across serialization/deserialization when the information is not available in public properties of the class.</span></span>

<span data-ttu-id="66ed7-165">**Serialization03**</span><span class="sxs-lookup"><span data-stu-id="66ed7-165">**Serialization03**</span></span>

<span data-ttu-id="66ed7-166">Bemutatja, hogyan tekintse meg egy meglévő .NET-osztályt, és győződjön meg arról, hogy ez az osztály és származtatott osztályainak példányok deszerializálni van élő .NET-objektumokba (rehydrated).</span><span class="sxs-lookup"><span data-stu-id="66ed7-166">Shows how to look at an existing .NET class and make sure that instances of this class and of derived classes are deserialized (rehydrated) into live .NET objects.</span></span>

## <a name="event-samples"></a><span data-ttu-id="66ed7-167">Esemény minták</span><span class="sxs-lookup"><span data-stu-id="66ed7-167">Event samples</span></span>

<span data-ttu-id="66ed7-168">**Event01**</span><span class="sxs-lookup"><span data-stu-id="66ed7-168">**Event01**</span></span>

<span data-ttu-id="66ed7-169">Bemutatja, hogyan hozhat létre a eseményregisztráció parancsmag ObjectEventRegistrationBase származó.</span><span class="sxs-lookup"><span data-stu-id="66ed7-169">Shows how to create a cmdlet for event registration by deriving from ObjectEventRegistrationBase.</span></span>

<span data-ttu-id="66ed7-170">**Event02**</span><span class="sxs-lookup"><span data-stu-id="66ed7-170">**Event02**</span></span>

<span data-ttu-id="66ed7-171">Bemutatja, hogyan való jeleníti meg, amelyek akkor jönnek létre, a távoli számítógépeken lévő Windows PowerShell-események értesítést szeretne kapni.</span><span class="sxs-lookup"><span data-stu-id="66ed7-171">Shows how to shows how to receive notifications of Windows PowerShell events that are generated on remote computers.</span></span>
<span data-ttu-id="66ed7-172">A PSEventReceived esemény keresztül közzétett használ a [futási térben](https://technet.microsoft.com/library/system.management.automation.runspaces.runspace.aspx) osztály.</span><span class="sxs-lookup"><span data-stu-id="66ed7-172">It uses the PSEventReceived event exposed through the [Runspace](https://technet.microsoft.com/library/system.management.automation.runspaces.runspace.aspx) class.</span></span>

## <a name="hosting-application-samples"></a><span data-ttu-id="66ed7-173">Üzemeltetési alkalmazás minták</span><span class="sxs-lookup"><span data-stu-id="66ed7-173">Hosting application samples</span></span>

<span data-ttu-id="66ed7-174">**Runspace01**</span><span class="sxs-lookup"><span data-stu-id="66ed7-174">**Runspace01**</span></span>

<span data-ttu-id="66ed7-175">Bemutatja, hogyan használható a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) osztály futtatásához a [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) parancsmag szinkron módon történik.</span><span class="sxs-lookup"><span data-stu-id="66ed7-175">Shows how to use the [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) class to run the [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) cmdlet synchronously.</span></span>
<span data-ttu-id="66ed7-176">A [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) parancsmag visszaadja [folyamat](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objektumokat az összes a helyi számítógépen futó folyamat.</span><span class="sxs-lookup"><span data-stu-id="66ed7-176">The [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) cmdlet returns [Process](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objects for each process running on the local computer.</span></span>

<span data-ttu-id="66ed7-177">**Runspace02**</span><span class="sxs-lookup"><span data-stu-id="66ed7-177">**Runspace02**</span></span>

<span data-ttu-id="66ed7-178">Bemutatja, hogyan használható a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) osztály futtatásához a [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) és [rendezési-objektum](http://go.microsoft.com/fwlink/?LinkID=113403) parancsmagok szinkron módon történik.</span><span class="sxs-lookup"><span data-stu-id="66ed7-178">Shows how to use the [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) class to run the [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) and [Sort-Object](http://go.microsoft.com/fwlink/?LinkID=113403) cmdlets synchronously.</span></span>
<span data-ttu-id="66ed7-179">A [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) parancsmag visszaadja [folyamat](https://technet.microsoft.com/library/system.diagnostics.process.aspx) az egyes objektumok feldolgozásához, a helyi számítógépen fut, és a rendezés-objektum az objektumok alapján rendezi a [azonosító](https://technet.microsoft.com/library/system.diagnostics.process.id.aspx) tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="66ed7-179">The [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) cmdlet returns [Process](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objects for each process running on the local computer, and the Sort-Object sorts the objects based on their [Id](https://technet.microsoft.com/library/system.diagnostics.process.id.aspx) property.</span></span>
<span data-ttu-id="66ed7-180">Az eredmények parancsok használatával megjelenik egy [DataGridView](https://technet.microsoft.com/library/system.windows.forms.datagridview.aspx) vezérlő.</span><span class="sxs-lookup"><span data-stu-id="66ed7-180">The results of these commands is displayed by using a [DataGridView](https://technet.microsoft.com/library/system.windows.forms.datagridview.aspx) control.</span></span>

<span data-ttu-id="66ed7-181">**Runspace03**</span><span class="sxs-lookup"><span data-stu-id="66ed7-181">**Runspace03**</span></span>

<span data-ttu-id="66ed7-182">Bemutatja, hogyan használható a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) osztály parancsfájllal szinkron módon történik, és nem okozó hibák kezelésének módját.</span><span class="sxs-lookup"><span data-stu-id="66ed7-182">Shows how to use the [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) class to run a script synchronously, and how to handle non-terminating errors.</span></span>
<span data-ttu-id="66ed7-183">A parancsfájl fogadása folyamat neveinek listáját, és ezután lekéri a folyamatok.</span><span class="sxs-lookup"><span data-stu-id="66ed7-183">The script receives a list of process names and then retrieves those processes.</span></span>
<span data-ttu-id="66ed7-184">A parancsfájl, beleértve a parancsprogram futtatása során létrehozott nem okozó hibákat is eredményeit a konzolablakban jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="66ed7-184">The results of the script, including any non-terminating errors that were generated when running the script, are displayed in a console window.</span></span>

<span data-ttu-id="66ed7-185">**Runspace04**</span><span class="sxs-lookup"><span data-stu-id="66ed7-185">**Runspace04**</span></span>

<span data-ttu-id="66ed7-186">Bemutatja, hogyan használható a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) osztályt a parancsokat, és hogyan catch lezáró hibát okozott a parancsok futtatásakor.</span><span class="sxs-lookup"><span data-stu-id="66ed7-186">Shows how to use the [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) class to run commands, and how to catch terminating errors that are thrown when running the commands.</span></span>
<span data-ttu-id="66ed7-187">Két parancs futtatása, és az utolsó parancs átadása egy paraméter argumentum érvénytelen.</span><span class="sxs-lookup"><span data-stu-id="66ed7-187">Two commands are run, and the last command is passed a parameter argument that is not valid.</span></span>
<span data-ttu-id="66ed7-188">Emiatt nem lesznek visszaadva, és a leállítási hibát vált ki.</span><span class="sxs-lookup"><span data-stu-id="66ed7-188">As a result, no objects are returned and a terminating error is thrown.</span></span>

<span data-ttu-id="66ed7-189">**Runspace05**</span><span class="sxs-lookup"><span data-stu-id="66ed7-189">**Runspace05**</span></span>

<span data-ttu-id="66ed7-190">Bemutatja, hogyan egy beépülő modul hozzáadása egy [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx) objektumot, hogy a beépülő modul a parancsmag akkor használható, ha a futási teret már meg van nyitva.</span><span class="sxs-lookup"><span data-stu-id="66ed7-190">Shows how to add a snap-in to an [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx) object so that the cmdlet of the snap-in is available when the runspace is opened.</span></span>
<span data-ttu-id="66ed7-191">A beépülő modul a Get-Proc parancsmag (határozzák meg a [GetProcessSample01 minta](https://technet.microsoft.com/library/ff602028.aspx)) használatával párhuzamosan futtatott egy [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objektum.</span><span class="sxs-lookup"><span data-stu-id="66ed7-191">The snap-in provides a Get-Proc cmdlet (defined by the [GetProcessSample01 Sample](https://technet.microsoft.com/library/ff602028.aspx)) that is run synchronously by using a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) object.</span></span>

<span data-ttu-id="66ed7-192">**Runspace06**</span><span class="sxs-lookup"><span data-stu-id="66ed7-192">**Runspace06**</span></span>

<span data-ttu-id="66ed7-193">Bemutatja, hogyan vehető fel a modul egy [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx) objektumot, hogy a modul be van töltve, a futási teret megnyitásakor.</span><span class="sxs-lookup"><span data-stu-id="66ed7-193">Shows how to add a module to an [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx) object so that the module is loaded when the runspace is opened.</span></span>
<span data-ttu-id="66ed7-194">A modul adja meg a Get-Proc parancsmag (határozzák meg a [GetProcessSample02 minta](https://technet.microsoft.com/library/ff602027.aspx)) használatával párhuzamosan futtatott egy [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objektum.</span><span class="sxs-lookup"><span data-stu-id="66ed7-194">The module provides a Get-Proc cmdlet (defined by the [GetProcessSample02 Sample](https://technet.microsoft.com/library/ff602027.aspx)) that is run synchronously by using a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) object.</span></span>

<span data-ttu-id="66ed7-195">**Runspace07**</span><span class="sxs-lookup"><span data-stu-id="66ed7-195">**Runspace07**</span></span>

<span data-ttu-id="66ed7-196">Bemutatja, hogyan hozzon létre egy futási teret, és, hogy futási térben segítségével két parancsmagok használatával szinkron módon futtassa egy [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objektum.</span><span class="sxs-lookup"><span data-stu-id="66ed7-196">Shows how to create a runspace, and then use that runspace to run two cmdlets synchronously by using a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) object.</span></span>

<span data-ttu-id="66ed7-197">**Runspace08**</span><span class="sxs-lookup"><span data-stu-id="66ed7-197">**Runspace08**</span></span>

<span data-ttu-id="66ed7-198">Bemutatja, hogyan parancsok és argumentumok hozzáadása az adatcsatorna egy [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objektum és a szinkron módon futtassa a parancsokat.</span><span class="sxs-lookup"><span data-stu-id="66ed7-198">Shows how to add commands and arguments to the pipeline of a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) object and how to run the commands synchronously.</span></span>

<span data-ttu-id="66ed7-199">**Runspace09**</span><span class="sxs-lookup"><span data-stu-id="66ed7-199">**Runspace09**</span></span>

<span data-ttu-id="66ed7-200">Bemutatja, hogyan a folyamat egy parancsfájl hozzáadása egy [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objektum és az aszinkron módon futtassa a parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="66ed7-200">Shows how to add a script to the pipeline of a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) object and how to run the script asynchronously.</span></span>
<span data-ttu-id="66ed7-201">Események a parancsfájl kezelésére használhatók.</span><span class="sxs-lookup"><span data-stu-id="66ed7-201">Events are used to handle the output of the script.</span></span>

<span data-ttu-id="66ed7-202">**Runspace10**</span><span class="sxs-lookup"><span data-stu-id="66ed7-202">**Runspace10**</span></span>

<span data-ttu-id="66ed7-203">Bemutatja, hogyan hozzon létre egy alapértelmezett kezdeti munkamenet-állapot, a parancsmag hozzáadása a [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx), hozzon létre egy futási teret, amely a kezdeti munkamenet-állapotot használ, és a parancs futtatásához a egy [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx)objektum.</span><span class="sxs-lookup"><span data-stu-id="66ed7-203">Shows how to create a default initial session state, how to add a cmdlet to the [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx), how to create a runspace that uses the initial session state, and how to run the command by using a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) object.</span></span>

<span data-ttu-id="66ed7-204">**Runspace11**</span><span class="sxs-lookup"><span data-stu-id="66ed7-204">**Runspace11**</span></span>

<span data-ttu-id="66ed7-205">Bemutatja, hogyan használható a [ProxyCommand](https://technet.microsoft.com/library/system.management.automation.proxycommand.aspx) osztály, amely egy meglévő parancsmagot hívja, de korlátozza a rendelkezésre álló paraméterkészletet proxy-parancsot hozhat létre.</span><span class="sxs-lookup"><span data-stu-id="66ed7-205">Shows how to use the [ProxyCommand](https://technet.microsoft.com/library/system.management.automation.proxycommand.aspx) class to create a proxy command that calls an existing cmdlet, but restricts the set of available parameters.</span></span>
<span data-ttu-id="66ed7-206">A proxy paranccsal egy korlátozott futási térrel létrehozásához használt kezdeti munkamenet állapotba kerül.</span><span class="sxs-lookup"><span data-stu-id="66ed7-206">The proxy command is then added to an initial session state that is used to create a constrained runspace.</span></span>
<span data-ttu-id="66ed7-207">Ez azt jelenti, hogy a felhasználó hozzáférhet-e a funkció a parancsmag csak a proxy parancs használatával.</span><span class="sxs-lookup"><span data-stu-id="66ed7-207">This means that the user can access the functionality of the cmdlet only through the proxy command.</span></span>

<span data-ttu-id="66ed7-208">**PowerShell01**</span><span class="sxs-lookup"><span data-stu-id="66ed7-208">**PowerShell01**</span></span>

<span data-ttu-id="66ed7-209">Bemutatja, hogyan hozzon létre egy korlátozott futási teret használ egy [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx) objektum.</span><span class="sxs-lookup"><span data-stu-id="66ed7-209">Shows how to create a constrained runspace using an [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx) object.</span></span>

<span data-ttu-id="66ed7-210">**PowerShell02**</span><span class="sxs-lookup"><span data-stu-id="66ed7-210">**PowerShell02**</span></span>

<span data-ttu-id="66ed7-211">Bemutatja, hogyan használja a futási teret több parancs egyidejű futtatását.</span><span class="sxs-lookup"><span data-stu-id="66ed7-211">Shows how to use a runspace pool to run multiple commands concurrently.</span></span>

## <a name="host-samples"></a><span data-ttu-id="66ed7-212">Host minták</span><span class="sxs-lookup"><span data-stu-id="66ed7-212">Host samples</span></span>

<span data-ttu-id="66ed7-213">**Host01**</span><span class="sxs-lookup"><span data-stu-id="66ed7-213">**Host01**</span></span>

<span data-ttu-id="66ed7-214">Bemutatja, hogyan egyéni állomást egy fogadó alkalmazás végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="66ed7-214">Shows how to implement a host application that uses a custom host.</span></span>
<span data-ttu-id="66ed7-215">A mintában a futási teret jön létre, amely használja az egyéni állomást, majd a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) API olyan parancsfájlt, amely meghívja az "exit" futtatására szolgál.</span><span class="sxs-lookup"><span data-stu-id="66ed7-215">In this sample a runspace is created that uses the custom host, and then the [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) API is used to run a script that calls "exit".</span></span>
<span data-ttu-id="66ed7-216">A fogadó alkalmazás majd ellenőrzi, hogy a parancsfájl, és megjeleníti az eredményeket.</span><span class="sxs-lookup"><span data-stu-id="66ed7-216">The host application then looks at the output of the script and prints out the results.</span></span>

<span data-ttu-id="66ed7-217">**Host02**</span><span class="sxs-lookup"><span data-stu-id="66ed7-217">**Host02**</span></span>

<span data-ttu-id="66ed7-218">Bemutatja, hogyan egy fogadó alkalmazás, amely a Windows PowerShell futási idejű együtt egy egyéni állomást végrehajtása írni.</span><span class="sxs-lookup"><span data-stu-id="66ed7-218">Shows how to write a host application that uses the Windows PowerShell runtime along with a custom host implementation.</span></span>
<span data-ttu-id="66ed7-219">A gazdaalkalmazást értékűre állítja be a gazdagép kulturális környezet német, futtatja a [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) parancsmag és megjeleníti az eredményeket, ha Ön jelenik meg azokat a német pwrsh.exe, és az aktuális dátumát és időpontját majd kinyomtatása segítségével.</span><span class="sxs-lookup"><span data-stu-id="66ed7-219">The host application sets the host culture to German, runs the [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) cmdlet and displays the results as you would see them by using pwrsh.exe, and then prints out the current data and time in German.</span></span>

<span data-ttu-id="66ed7-220">**Host03**</span><span class="sxs-lookup"><span data-stu-id="66ed7-220">**Host03**</span></span>

<span data-ttu-id="66ed7-221">Bemutatja, hogyan hozhat létre egy interaktív Konzolalapú gazdaalkalmazást parancsok beolvassa a parancssorból, a parancsok végrehajtása és a eredményeit jeleníti meg a konzolon.</span><span class="sxs-lookup"><span data-stu-id="66ed7-221">Shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span>

<span data-ttu-id="66ed7-222">**Host04**</span><span class="sxs-lookup"><span data-stu-id="66ed7-222">**Host04**</span></span>

<span data-ttu-id="66ed7-223">Bemutatja, hogyan hozhat létre egy interaktív Konzolalapú gazdaalkalmazást parancsok beolvassa a parancssorból, a parancsok végrehajtása és a eredményeit jeleníti meg a konzolon.</span><span class="sxs-lookup"><span data-stu-id="66ed7-223">Shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span>
<span data-ttu-id="66ed7-224">A fogadó alkalmazás megjelenítését megjelenő utasításokat, amelyek lehetővé teszik a felhasználó megadhatja a több lehetőség is támogatja.</span><span class="sxs-lookup"><span data-stu-id="66ed7-224">This host application also supports displaying prompts that allow the user to specify multiple choices.</span></span>

<span data-ttu-id="66ed7-225">**Host05**</span><span class="sxs-lookup"><span data-stu-id="66ed7-225">**Host05**</span></span>

<span data-ttu-id="66ed7-226">Bemutatja, hogyan hozhat létre egy interaktív Konzolalapú gazdaalkalmazást parancsok beolvassa a parancssorból, a parancsok végrehajtása és a eredményeit jeleníti meg a konzolon.</span><span class="sxs-lookup"><span data-stu-id="66ed7-226">Shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span>
<span data-ttu-id="66ed7-227">A fogadó alkalmazás is támogatja a távoli számítógépek hívások a [Enter-PsSession](http://go.microsoft.com/fwlink/?LinkId=135210) és [kilépési-PsSession](http://go.microsoft.com/fwlink/?LinkId=135212) parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="66ed7-227">This host application also supports calls to remote computers by using the [Enter-PsSession](http://go.microsoft.com/fwlink/?LinkId=135210) and [Exit-PsSession](http://go.microsoft.com/fwlink/?LinkId=135212) cmdlets.</span></span>

<span data-ttu-id="66ed7-228">**Host06**</span><span class="sxs-lookup"><span data-stu-id="66ed7-228">**Host06**</span></span>

<span data-ttu-id="66ed7-229">Bemutatja, hogyan hozhat létre egy interaktív Konzolalapú gazdaalkalmazást parancsok beolvassa a parancssorból, a parancsok végrehajtása és a eredményeit jeleníti meg a konzolon.</span><span class="sxs-lookup"><span data-stu-id="66ed7-229">Shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span>
<span data-ttu-id="66ed7-230">Emellett ez a minta használja a jogkivonatokat létrehozó API-k, a felhasználó által megadott szöveg színét.</span><span class="sxs-lookup"><span data-stu-id="66ed7-230">In addition, this sample uses the Tokenizer APIs to specify the color of the text that is entered by the user.</span></span>

## <a name="provider-samples"></a><span data-ttu-id="66ed7-231">Szolgáltató minták</span><span class="sxs-lookup"><span data-stu-id="66ed7-231">Provider samples</span></span>

<span data-ttu-id="66ed7-232">**AccessDBProviderSample01**</span><span class="sxs-lookup"><span data-stu-id="66ed7-232">**AccessDBProviderSample01**</span></span>

<span data-ttu-id="66ed7-233">Bemutatja, hogyan deklarál egy szolgáltatóosztállyal, amely közvetlenül a származik a [CmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.cmdletprovider.aspx) osztály.</span><span class="sxs-lookup"><span data-stu-id="66ed7-233">Shows how to declare a provider class that derives directly from the [CmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.cmdletprovider.aspx) class.</span></span>
<span data-ttu-id="66ed7-234">Szerepel itt csak a teljesség.</span><span class="sxs-lookup"><span data-stu-id="66ed7-234">It is included here only for completeness.</span></span>

<span data-ttu-id="66ed7-235">**AccessDBProviderSample02**</span><span class="sxs-lookup"><span data-stu-id="66ed7-235">**AccessDBProviderSample02**</span></span>

<span data-ttu-id="66ed7-236">Bemutatja, hogyan írhatja felül a [NewDrive](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.newdrive.aspx) és [RemoveDrive](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.removedrive.aspx) módszerek támogatásához a New-PSDrive és a Remove-PSDrive parancsmagok hívásokat.</span><span class="sxs-lookup"><span data-stu-id="66ed7-236">Shows how to overwrite the [NewDrive](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.newdrive.aspx) and [RemoveDrive](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.removedrive.aspx) methods to support calls to the New-PSDrive and Remove-PSDrive cmdlets.</span></span>
<span data-ttu-id="66ed7-237">Ez a példa a Szolgáltatóosztály származik a [DriveCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.aspx) osztály.</span><span class="sxs-lookup"><span data-stu-id="66ed7-237">The provider class in this sample derives from the [DriveCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.aspx) class.</span></span>

<span data-ttu-id="66ed7-238">**AccessDBProviderSample03**</span><span class="sxs-lookup"><span data-stu-id="66ed7-238">**AccessDBProviderSample03**</span></span>

<span data-ttu-id="66ed7-239">Bemutatja, hogyan írhatja felül a [GetItem](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.getitem.aspx) és [SetItem](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.setitem.aspx) módszerek támogatásához a Get-elem és a Set-cikk parancsmagok hívásokat.</span><span class="sxs-lookup"><span data-stu-id="66ed7-239">Shows how to overwrite the [GetItem](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.getitem.aspx) and [SetItem](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.setitem.aspx) methods to support calls to the Get-Item and Set-Item cmdlets.</span></span>
<span data-ttu-id="66ed7-240">Ez a példa a Szolgáltatóosztály származik a [ItemCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.aspx) osztály.</span><span class="sxs-lookup"><span data-stu-id="66ed7-240">The provider class in this sample derives from the [ItemCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.aspx) class.</span></span>

<span data-ttu-id="66ed7-241">**AccessDBProviderSample04**</span><span class="sxs-lookup"><span data-stu-id="66ed7-241">**AccessDBProviderSample04**</span></span>

<span data-ttu-id="66ed7-242">Bemutatja, hogyan felülírja a tároló módszerek az elem, Get-ChildItem, hívások támogatásához új-elemen, illetve a Remove-cikk parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="66ed7-242">Shows how to overwrite container methods to support calls to the Copy-Item, Get-ChildItem, New-Item, and Remove-Item cmdlets.</span></span>
<span data-ttu-id="66ed7-243">Ezek a módszerek kell kell végrehajtani, ha az adattár tárolók elemeket tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="66ed7-243">These methods should be implemented when the data store contains items that are containers.</span></span>
<span data-ttu-id="66ed7-244">Egy tároló olyan alárendelt elemek egy közös szülő elem alatt.</span><span class="sxs-lookup"><span data-stu-id="66ed7-244">A container is a group of child items under a common parent item.</span></span>
<span data-ttu-id="66ed7-245">Ez a példa a Szolgáltatóosztály származik a [ItemCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.aspx) osztály.</span><span class="sxs-lookup"><span data-stu-id="66ed7-245">The provider class in this sample derives from the [ItemCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.aspx) class.</span></span>

<span data-ttu-id="66ed7-246">**AccessDBProviderSample05**</span><span class="sxs-lookup"><span data-stu-id="66ed7-246">**AccessDBProviderSample05**</span></span>

<span data-ttu-id="66ed7-247">Bemutatja, hogyan tároló módszerek támogatásához az elem áthelyezése és Join-Path parancsmagok hívásainak felülírásához.</span><span class="sxs-lookup"><span data-stu-id="66ed7-247">Shows how to overwrite container methods to support calls to the Move-Item and Join-Path cmdlets.</span></span>
<span data-ttu-id="66ed7-248">Ezek a módszerek kell végrehajtani, ha a felhasználó nem a tárolóban lévő elemek áthelyezése, és az adattár tartalmaz beágyazott tárolók.</span><span class="sxs-lookup"><span data-stu-id="66ed7-248">These methods should be implemented when the user needs to move items within a container and if the data store contains nested containers.</span></span>
<span data-ttu-id="66ed7-249">Ez a példa a Szolgáltatóosztály származik a [NavigationCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.navigationcmdletprovider.aspx) osztály.</span><span class="sxs-lookup"><span data-stu-id="66ed7-249">The provider class in this sample derives from the [NavigationCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.navigationcmdletprovider.aspx) class.</span></span>

<span data-ttu-id="66ed7-250">**AccessDBProviderSample06**</span><span class="sxs-lookup"><span data-stu-id="66ed7-250">**AccessDBProviderSample06**</span></span>

<span data-ttu-id="66ed7-251">Bemutatja, hogyan felülírja a tartalom módszerek támogatásához a tiszta tartalom hívásainak Get-tartalom és a Set-tartalom parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="66ed7-251">Shows how to overwrite content methods to support calls to the Clear-Content, Get-Content, and Set-Content cmdlets.</span></span>
<span data-ttu-id="66ed7-252">Ezek a módszerek kell végrehajtani, ha a felhasználó nem szerepel az adattárban elemek tartalom kezelése.</span><span class="sxs-lookup"><span data-stu-id="66ed7-252">These methods should be implemented when the user needs to manage the content of the items in the data store.</span></span>
<span data-ttu-id="66ed7-253">Ez a példa a Szolgáltatóosztály származik a [NavigationCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.navigationcmdletprovider.aspx) osztály, és megvalósítja az [IContentCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.icontentcmdletprovider.aspx) felületet.</span><span class="sxs-lookup"><span data-stu-id="66ed7-253">The provider class in this sample derives from the [NavigationCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.navigationcmdletprovider.aspx) class, and it implements the [IContentCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.icontentcmdletprovider.aspx) interface.</span></span>

