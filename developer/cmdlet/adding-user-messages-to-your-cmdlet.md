---
title: Felhasználói üzenetek hozzáadása a parancsmaghoz |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- WriteWarning
- notifications, writing
- progress notification
- WriteVerbose
- Stop-Proc
- WriteProgress
- WriteDebug
- notifications, debug
- ProgressRecord
- samples, Stop-Proc cmdlet
- notifications, progress
- notifications, warning
- WriteObject
- WriteError
- verbose notification
- ProcessRecord
- notifications, verbose
- debug notification
- cmdlet, writing notifications
- warning
- code sample, user notifications
- user notifications
ms.assetid: 14c13acb-f0b7-4613-bc7d-c361d14da1a2
caps.latest.revision: 8
ms.openlocfilehash: 5b3a5f5d5d02c7d5a3c1d622ec1a3740739c694f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068776"
---
# <a name="adding-user-messages-to-your-cmdlet"></a><span data-ttu-id="1b783-102">Felhasználói üzenetek hozzáadása a parancsmaghoz</span><span class="sxs-lookup"><span data-stu-id="1b783-102">Adding User Messages to Your Cmdlet</span></span>

<span data-ttu-id="1b783-103">Parancsmagok írhat a különböző típusú üzeneteket, amelyek a felhasználó által a Windows PowerShell-modul is megjelenik.</span><span class="sxs-lookup"><span data-stu-id="1b783-103">Cmdlets can write several kinds of messages that can be displayed to the user by the Windows PowerShell runtime.</span></span> <span data-ttu-id="1b783-104">Ezek az üzenetek közé tartozik a következők:</span><span class="sxs-lookup"><span data-stu-id="1b783-104">These messages include the following types:</span></span>

- <span data-ttu-id="1b783-105">Részletes üzeneteket, amelyek tartalmazzák az általános információkat.</span><span class="sxs-lookup"><span data-stu-id="1b783-105">Verbose messages that contain general user information.</span></span>

- <span data-ttu-id="1b783-106">A hibakeresési információkat tartalmazó üzenetek.</span><span class="sxs-lookup"><span data-stu-id="1b783-106">Debug messages that contain troubleshooting information.</span></span>

- <span data-ttu-id="1b783-107">Figyelmeztető üzeneteket, amelyek tartalmaznak egy értesítés, hogy a parancsmag arra készül, hogy egy művelettel, amelyeken nem várt eredmények.</span><span class="sxs-lookup"><span data-stu-id="1b783-107">Warning messages that contain a notification that the cmdlet is about to perform an operation that can have unexpected results.</span></span>

- <span data-ttu-id="1b783-108">Mennyi információkat tartalmazó üzenetek működik a parancsmag állapotjelentés befejeződött, amelyek hosszú ideig tart a művelet végrehajtása során.</span><span class="sxs-lookup"><span data-stu-id="1b783-108">Progress report messages that contain information about how much work the cmdlet has completed when performing an operation that takes a long time.</span></span>

<span data-ttu-id="1b783-109">Nincs korlátozva van, a parancsmag be írni képes üzenetek száma vagy a parancsmag írja az üzeneteket a típusát.</span><span class="sxs-lookup"><span data-stu-id="1b783-109">There are no limits to the number of messages that your cmdlet can write or the type of messages that your cmdlet writes.</span></span> <span data-ttu-id="1b783-110">Mindegyik üzenet íródik azáltal, hogy egy adott hívás a feldolgozási mód a parancsmag bemeneti adatban.</span><span class="sxs-lookup"><span data-stu-id="1b783-110">Each message is written by making a specific call from within the input processing method of your cmdlet.</span></span>

## <a name="the-stopproc-cmdlet"></a><span data-ttu-id="1b783-111">A StopProc parancsmag</span><span class="sxs-lookup"><span data-stu-id="1b783-111">The StopProc Cmdlet</span></span>

<span data-ttu-id="1b783-112">Ez a szakasz témakörei a következők:</span><span class="sxs-lookup"><span data-stu-id="1b783-112">Topics in this section include the following:</span></span>

- [<span data-ttu-id="1b783-113">A parancsmag meghatározása</span><span class="sxs-lookup"><span data-stu-id="1b783-113">Defining the Cmdlet</span></span>](#Defining-the-Cmdlet)

- [<span data-ttu-id="1b783-114">A rendszer módosítás paraméterek megadása</span><span class="sxs-lookup"><span data-stu-id="1b783-114">Defining Parameters for System Modification</span></span>](#Defining-Parameters-for-System-Modification)

- [<span data-ttu-id="1b783-115">Egy bemeneti metódus feldolgozási felülbírálása</span><span class="sxs-lookup"><span data-stu-id="1b783-115">Overriding an Input Processing Method</span></span>](#Overriding-an-Input-Processing-Method)

- [<span data-ttu-id="1b783-116">Részletes üzenet írásának</span><span class="sxs-lookup"><span data-stu-id="1b783-116">Writing a Verbose Message</span></span>](#Writing-a-Verbose-Message)

- [<span data-ttu-id="1b783-117">Hibakeresési üzenet írásának</span><span class="sxs-lookup"><span data-stu-id="1b783-117">Writing a Debug Message</span></span>](#Writing-a-Debug-Message)

- [<span data-ttu-id="1b783-118">Egy figyelmeztető üzenet írása</span><span class="sxs-lookup"><span data-stu-id="1b783-118">Writing a Warning Message</span></span>](#Writing-a-Warning-Message)

- [<span data-ttu-id="1b783-119">A folyamatállapot-üzenet írása</span><span class="sxs-lookup"><span data-stu-id="1b783-119">Writing a Progress Message</span></span>](#Writing-a-Progress-Message)

- [<span data-ttu-id="1b783-120">Kódminta</span><span class="sxs-lookup"><span data-stu-id="1b783-120">Code Sample</span></span>](#Code-Sample)

- [<span data-ttu-id="1b783-121">Objektumtípusok és formázása</span><span class="sxs-lookup"><span data-stu-id="1b783-121">Define Object Types and Formatting</span></span>](#Define-Object-Types-and-Formatting)

- [<span data-ttu-id="1b783-122">A parancsmag készítése</span><span class="sxs-lookup"><span data-stu-id="1b783-122">Building the Cmdlet</span></span>](#Building-the-Cmdlet)

- [<span data-ttu-id="1b783-123">A parancsmag tesztelése</span><span class="sxs-lookup"><span data-stu-id="1b783-123">Testing the Cmdlet</span></span>](#Testing-the-Cmdlet)

## <a name="defining-the-cmdlet"></a><span data-ttu-id="1b783-124">A parancsmag meghatározása</span><span class="sxs-lookup"><span data-stu-id="1b783-124">Defining the Cmdlet</span></span>

<span data-ttu-id="1b783-125">Mindig a parancsmag elnevezési és a .NET-osztály, amely megvalósítja a parancsmag deklaráló parancsmag létrehozásának első lépése.</span><span class="sxs-lookup"><span data-stu-id="1b783-125">The first step in cmdlet creation is always naming the cmdlet and declaring the .NET class that implements the cmdlet.</span></span> <span data-ttu-id="1b783-126">Parancsmag rendezést felhasználói értesítések írhat a bemeneti feldolgozási módszerek; tehát általában nevet adhat a parancsmag minden olyan művelet, amely azt jelzi, hogy milyen system módosításokat végez a parancsmag használatával.</span><span class="sxs-lookup"><span data-stu-id="1b783-126">Any sort of cmdlet can write user notifications from its input processing methods; so, in general, you can name this cmdlet using any verb that indicates what system modifications the cmdlet performs.</span></span> <span data-ttu-id="1b783-127">A parancsmag jóváhagyott igék kapcsolatos további információkért lásd: [művelet neve](./approved-verbs-for-windows-powershell-commands.md).</span><span class="sxs-lookup"><span data-stu-id="1b783-127">For more information about approved cmdlet verbs, see [Cmdlet Verb Names](./approved-verbs-for-windows-powershell-commands.md).</span></span>

<span data-ttu-id="1b783-128">A Stop-Proc parancsmag úgy tervezték, hogy a rendszer; módosítása ezért a [System.Management.Automation.CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute) tartalmaznia kell a .NET deklarációjában a `SupportsShouldProcess` kulcsszó attribútumot, és állítható `true`.</span><span class="sxs-lookup"><span data-stu-id="1b783-128">The Stop-Proc cmdlet is designed to modify the system; therefore, the [System.Management.Automation.CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute) declaration for the .NET class must include the `SupportsShouldProcess` attribute keyword and be set to `true`.</span></span>

<span data-ttu-id="1b783-129">A következő kódot a Stop-Proc parancsmag osztály definícióját.</span><span class="sxs-lookup"><span data-stu-id="1b783-129">The following code is the definition for this Stop-Proc cmdlet class.</span></span> <span data-ttu-id="1b783-130">Ez a definíció kapcsolatos további információkért lásd: [létrehozása egy parancsmag, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md).</span><span class="sxs-lookup"><span data-stu-id="1b783-130">For more information about this definition, see [Creating a Cmdlet that Modifies the System](./creating-a-cmdlet-that-modifies-the-system.md).</span></span>

```csharp
[Cmdlet(VerbsLifecycle.Stop, "proc",
        SupportsShouldProcess = true)]
public class StopProcCommand : Cmdlet
```

## <a name="defining-parameters-for-system-modification"></a><span data-ttu-id="1b783-131">A rendszer módosítás paraméterek megadása</span><span class="sxs-lookup"><span data-stu-id="1b783-131">Defining Parameters for System Modification</span></span>

<span data-ttu-id="1b783-132">A Stop-Proc parancsmag meghatározása három paramétert: `Name`, `Force`, és `PassThru`.</span><span class="sxs-lookup"><span data-stu-id="1b783-132">The Stop-Proc cmdlet defines three parameters: `Name`, `Force`, and `PassThru`.</span></span> <span data-ttu-id="1b783-133">Ezek a paraméterek meghatározása kapcsolatos további információkért lásd: [létrehozása egy parancsmag, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md).</span><span class="sxs-lookup"><span data-stu-id="1b783-133">For more information about defining these parameters, see [Creating a Cmdlet that Modifies the System](./creating-a-cmdlet-that-modifies-the-system.md).</span></span>

<span data-ttu-id="1b783-134">Íme a Stop-Proc parancsmagok a paraméterdeklarációhoz.</span><span class="sxs-lookup"><span data-stu-id="1b783-134">Here is the parameter declaration for the Stop-Proc cmdlet.</span></span>

```csharp
[Parameter(
           Position = 0,
           Mandatory = true,
           ValueFromPipeline = true,
           ValueFromPipelineByPropertyName = true
)]
public string[] Name
{
  get { return processNames; }
  set { processNames = value; }
}
private string[] processNames;

/// <summary>
/// Specify the Force parameter that allows the user to override
/// the ShouldContinue call to force the stop operation. This
/// parameter should always be used with caution.
/// </summary>
[Parameter]
public SwitchParameter Force
{
  get { return force; }
  set { force = value; }
}
private bool force;

/// <summary>
/// Specify the PassThru parameter that allows the user to specify
/// that the cmdlet should pass the process object down the pipeline
/// after the process has been stopped.
/// </summary>
[Parameter]
public SwitchParameter PassThru
{
  get { return passThru; }
  set { passThru = value; }
}
private bool passThru;
```

## <a name="overriding-an-input-processing-method"></a><span data-ttu-id="1b783-135">Egy bemeneti metódus feldolgozási felülbírálása</span><span class="sxs-lookup"><span data-stu-id="1b783-135">Overriding an Input Processing Method</span></span>

<span data-ttu-id="1b783-136">A parancsmag felül kell írnia egy bemeneti metódus feldolgozása, leggyakrabban lesz [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord).</span><span class="sxs-lookup"><span data-stu-id="1b783-136">Your cmdlet must override an input processing method, most often it will be [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord).</span></span> <span data-ttu-id="1b783-137">A Stop-Proc parancsmag felülbírálja a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) bemeneti metódusához feldolgozásra.</span><span class="sxs-lookup"><span data-stu-id="1b783-137">This Stop-Proc cmdlet overrides the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) input processing method.</span></span> <span data-ttu-id="1b783-138">Ez a megvalósítás a Stop-Proc parancsmag a hívások végrehajtott írási részletes üzeneteket, a hibakeresési üzeneteket és a figyelmeztető üzeneteket.</span><span class="sxs-lookup"><span data-stu-id="1b783-138">In this implementation of the Stop-Proc cmdlet, calls are made to write verbose messages, debug messages, and warning messages.</span></span>

> [!NOTE]
> <span data-ttu-id="1b783-139">További információ a hogyan Ez a metódus meghívja a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) és [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) módszereket, tekintse meg a [Létrehozása egy parancsmag, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md).</span><span class="sxs-lookup"><span data-stu-id="1b783-139">For more information about how this method calls the [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) and [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) methods, see [Creating a Cmdlet that Modifies the System](./creating-a-cmdlet-that-modifies-the-system.md).</span></span>

## <a name="writing-a-verbose-message"></a><span data-ttu-id="1b783-140">Részletes üzenet írásának</span><span class="sxs-lookup"><span data-stu-id="1b783-140">Writing a Verbose Message</span></span>

<span data-ttu-id="1b783-141">A [System.Management.Automation.Cmdlet.WriteVerbose](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose) általános, nem kapcsolódó meghatározott hibafeltételek felhasználói szintű információkat írásához használt módszert.</span><span class="sxs-lookup"><span data-stu-id="1b783-141">The [System.Management.Automation.Cmdlet.WriteVerbose](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose) method is used to write general user-level information that is unrelated to specific error conditions.</span></span> <span data-ttu-id="1b783-142">A rendszergazda folytatja a más parancsok feldolgozási felhasználhatja ezt az információt.</span><span class="sxs-lookup"><span data-stu-id="1b783-142">The system administrator can then use that information to continue processing other commands.</span></span> <span data-ttu-id="1b783-143">Emellett ez a módszer használatával írt minden olyan információt kell kell honosított igény szerint.</span><span class="sxs-lookup"><span data-stu-id="1b783-143">In addition, any information written using this method should be localized as needed.</span></span>

<span data-ttu-id="1b783-144">A Stop-Proc parancsmag a következő kód bemutatja, két hívásainak a [System.Management.Automation.Cmdlet.WriteVerbose](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose) metódus felülbírálását, a [System.Management.Automation.Cmdlet.ProcessRecord ](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust.</span><span class="sxs-lookup"><span data-stu-id="1b783-144">The following code from this Stop-Proc cmdlet shows two calls to the [System.Management.Automation.Cmdlet.WriteVerbose](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose) method from the override of the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method.</span></span>

```csharp
message = String.Format("Attempting to stop process \"{0}\".", name);
WriteVerbose(message);
```

```csharp
message = String.Format("Stopped process \"{0}\", pid {1}.",
                        processName, process.Id);

WriteVerbose(message);
```

## <a name="writing-a-debug-message"></a><span data-ttu-id="1b783-145">Hibakeresési üzenet írásának</span><span class="sxs-lookup"><span data-stu-id="1b783-145">Writing a Debug Message</span></span>

<span data-ttu-id="1b783-146">A [System.Management.Automation.Cmdlet.WriteDebug](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) módszert a parancsmag működésének hibaelhárítására használható hibakeresési üzeneteket írni.</span><span class="sxs-lookup"><span data-stu-id="1b783-146">The [System.Management.Automation.Cmdlet.WriteDebug](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) method is used to write debug messages that can be used to troubleshoot the operation of the cmdlet.</span></span> <span data-ttu-id="1b783-147">A hívás érkezett egy bemeneti metódus feldolgozása.</span><span class="sxs-lookup"><span data-stu-id="1b783-147">The call is made from an input processing method.</span></span>

> [!NOTE]
> <span data-ttu-id="1b783-148">Windows PowerShell is meghatároz egy `Debug` paraméter, amely egyaránt részletes mutat be, és a hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="1b783-148">Windows PowerShell also defines a `Debug` parameter that presents both verbose and debug information.</span></span> <span data-ttu-id="1b783-149">A parancsmag támogatja ezt a paramétert, ha nem kell meghívni [System.Management.Automation.Cmdlet.WriteDebug](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) ugyanazt a kódot, amely meghívja a [System.Management.Automation.Cmdlet.WriteVerbose](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose) .</span><span class="sxs-lookup"><span data-stu-id="1b783-149">If your cmdlet supports this parameter, it does not need to call [System.Management.Automation.Cmdlet.WriteDebug](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) in the same code that calls [System.Management.Automation.Cmdlet.WriteVerbose](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose).</span></span>

<span data-ttu-id="1b783-150">A kód a minta Stop-Proc parancsmag a következő két szakasz hívásainak megjelenítéséhez a [System.Management.Automation.Cmdlet.WriteDebug](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) metódus felülbírálását, a [ System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust.</span><span class="sxs-lookup"><span data-stu-id="1b783-150">The following two sections of code from the sample Stop-Proc cmdlet show calls to the [System.Management.Automation.Cmdlet.WriteDebug](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) method from the override of the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method.</span></span>

<span data-ttu-id="1b783-151">Hibakeresési üzenet írása előtt közvetlenül [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) nevezzük.</span><span class="sxs-lookup"><span data-stu-id="1b783-151">This debug message is written immediately before [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) is called.</span></span>

```csharp
message =
          String.Format("Acquired name for pid {0} : \"{1}\"",
                       process.Id, processName);
WriteDebug(message);
```

<span data-ttu-id="1b783-152">Hibakeresési üzenet írása előtt közvetlenül [System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) nevezzük.</span><span class="sxs-lookup"><span data-stu-id="1b783-152">This debug message is written immediately before [System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) is called.</span></span>

```csharp
message =
         String.Format("Writing process \"{0}\" to pipeline",
         processName);
WriteDebug(message);
WriteObject(process);
```

<span data-ttu-id="1b783-153">Windows PowerShell automatikusan átirányítja a bármely [System.Management.Automation.Cmdlet.WriteDebug](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) hívásokat a nyomkövetés infrastruktúrát és a parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="1b783-153">Windows PowerShell automatically routes any [System.Management.Automation.Cmdlet.WriteDebug](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) calls to the tracing infrastructure and cmdlets.</span></span> <span data-ttu-id="1b783-154">Ez lehetővé teszi a metódust hívja, nem kell tennie minden olyan további fejlesztési munkálatok során, a parancsmag belül az üzemeltetési alkalmazás, egy fájl vagy egy hibakereső nyomon követését.</span><span class="sxs-lookup"><span data-stu-id="1b783-154">This allows the method calls to be traced to the hosting application, a file, or a debugger without your having to do any extra development work within the cmdlet.</span></span> <span data-ttu-id="1b783-155">A következő parancssori bejegyzés egy nyomkövetési művelet valósítja meg.</span><span class="sxs-lookup"><span data-stu-id="1b783-155">The following command-line entry implements a tracing operation.</span></span>

<span data-ttu-id="1b783-156">**PS > nyomkövetési-kifejezés stop-proc-fájl proc.log-paranccsal állítsa le a folyamaton Jegyzettömb**</span><span class="sxs-lookup"><span data-stu-id="1b783-156">**PS> trace-expression stop-proc -file proc.log -command stop-proc notepad**</span></span>

## <a name="writing-a-warning-message"></a><span data-ttu-id="1b783-157">Egy figyelmeztető üzenet írása</span><span class="sxs-lookup"><span data-stu-id="1b783-157">Writing a Warning Message</span></span>

<span data-ttu-id="1b783-158">A [System.Management.Automation.Cmdlet.WriteWarning](/dotnet/api/System.Management.Automation.Cmdlet.WriteWarning) metódus írási egy figyelmeztetés, amikor a parancsmag arra készül, hogy előfordulhat, hogy nem várt eredményt, ha például egy csak olvasható fájlok felülírása művelet végrehajtására szolgál.</span><span class="sxs-lookup"><span data-stu-id="1b783-158">The [System.Management.Automation.Cmdlet.WriteWarning](/dotnet/api/System.Management.Automation.Cmdlet.WriteWarning) method is used to write a warning when the cmdlet is about to perform an operation that might have an unexpected result, for example, overwriting a read-only file.</span></span>

<span data-ttu-id="1b783-159">A következő kód a minta Stop-Proc parancsmag megjeleníti a hívást a [System.Management.Automation.Cmdlet.WriteWarning](/dotnet/api/System.Management.Automation.Cmdlet.WriteWarning) metódus felülbírálását, a [ System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust.</span><span class="sxs-lookup"><span data-stu-id="1b783-159">The following code from the sample Stop-Proc cmdlet shows the call to the [System.Management.Automation.Cmdlet.WriteWarning](/dotnet/api/System.Management.Automation.Cmdlet.WriteWarning) method from the override of the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method.</span></span>

```csharp
 if (criticalProcess)
 {
   message =
             String.Format("Stopping the critical process \"{0}\".",
                           processName);
   WriteWarning(message);
} // if (criticalProcess...
```

## <a name="writing-a-progress-message"></a><span data-ttu-id="1b783-160">A folyamatállapot-üzenet írása</span><span class="sxs-lookup"><span data-stu-id="1b783-160">Writing a Progress Message</span></span>

<span data-ttu-id="1b783-161">A [System.Management.Automation.Cmdlet.WriteProgress](/dotnet/api/System.Management.Automation.Cmdlet.WriteProgress) folyamatüzeneteket írhat, amikor a parancsmag operations igénybe egy kiterjesztett sok időt vesz igénybe.</span><span class="sxs-lookup"><span data-stu-id="1b783-161">The [System.Management.Automation.Cmdlet.WriteProgress](/dotnet/api/System.Management.Automation.Cmdlet.WriteProgress) is used to write progress messages when cmdlet operations take an extended amount of time to complete.</span></span> <span data-ttu-id="1b783-162">Hívás [System.Management.Automation.Cmdlet.WriteProgress](/dotnet/api/System.Management.Automation.Cmdlet.WriteProgress) átadja egy [System.Management.Automation.Progressrecord](/dotnet/api/System.Management.Automation.ProgressRecord) objektum, amely a renderelést a felhasználó számára a tároló alkalmazás érkezik.</span><span class="sxs-lookup"><span data-stu-id="1b783-162">A call to [System.Management.Automation.Cmdlet.WriteProgress](/dotnet/api/System.Management.Automation.Cmdlet.WriteProgress) passes a [System.Management.Automation.Progressrecord](/dotnet/api/System.Management.Automation.ProgressRecord) object that is sent to the hosting application for rendering to the user.</span></span>

> [!NOTE]
> <span data-ttu-id="1b783-163">A Stop-Proc parancsmag nem tartalmazza a hívást a [System.Management.Automation.Cmdlet.WriteProgress](/dotnet/api/System.Management.Automation.Cmdlet.WriteProgress) metódust.</span><span class="sxs-lookup"><span data-stu-id="1b783-163">This Stop-Proc cmdlet does not include a call to the [System.Management.Automation.Cmdlet.WriteProgress](/dotnet/api/System.Management.Automation.Cmdlet.WriteProgress) method.</span></span>

<span data-ttu-id="1b783-164">A következő kódot a folyamatállapot-üzenet, amely megpróbálja elem másolása a parancsmag által írt példája.</span><span class="sxs-lookup"><span data-stu-id="1b783-164">The following code is an example of a progress message written by a cmdlet that is attempting to copy an item.</span></span>

```csharp
int myId = 0;
string myActivity = "Copy-item: Copying *.* to c:\abc";
string myStatus = "Copying file bar.txt";
ProgressRecord pr = new ProgressRecord(myId, myActivity, myStatus);
WriteProgress(pr);

pr.RecordType = ProgressRecordType.Completed;
WriteProgress(pr);
```

## <a name="code-sample"></a><span data-ttu-id="1b783-165">Kódminta</span><span class="sxs-lookup"><span data-stu-id="1b783-165">Code Sample</span></span>

<span data-ttu-id="1b783-166">A teljes C# mintakód, lásd: [StopProcessSample02 minta](./stopprocesssample02-sample.md).</span><span class="sxs-lookup"><span data-stu-id="1b783-166">For the complete C# sample code, see [StopProcessSample02 Sample](./stopprocesssample02-sample.md).</span></span>

## <a name="define-object-types-and-formatting"></a><span data-ttu-id="1b783-167">Objektumtípusok és formázása</span><span class="sxs-lookup"><span data-stu-id="1b783-167">Define Object Types and Formatting</span></span>

<span data-ttu-id="1b783-168">Windows PowerShell parancsmagok használatával a .NET-objektumokká közötti továbbítja.</span><span class="sxs-lookup"><span data-stu-id="1b783-168">Windows PowerShell passes information between cmdlets using .NET objects.</span></span> <span data-ttu-id="1b783-169">Ennek következtében a parancsmag előfordulhat, hogy meg kell határoznia a saját típusát, vagy a parancsmag előfordulhat, hogy ki kell terjesztenie egy másik parancsmag által biztosított meglévő típus.</span><span class="sxs-lookup"><span data-stu-id="1b783-169">Consequently, a cmdlet might need to define its own type, or the cmdlet might need to extend an existing type provided by another cmdlet.</span></span> <span data-ttu-id="1b783-170">Új típusok meghatározása, vagy meglévő típusok bővítésével kapcsolatos további információkért lásd: [objektumtípusok kiterjesztése és formázás](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).</span><span class="sxs-lookup"><span data-stu-id="1b783-170">For more information about defining new types or extending existing types, see [Extending Object Types and Formatting](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).</span></span>

## <a name="building-the-cmdlet"></a><span data-ttu-id="1b783-171">A parancsmag készítése</span><span class="sxs-lookup"><span data-stu-id="1b783-171">Building the Cmdlet</span></span>

<span data-ttu-id="1b783-172">Parancsmag-k megvalósítása után regisztrálni kell a Windows PowerShell-lel a Windows PowerShell beépülő modullal.</span><span class="sxs-lookup"><span data-stu-id="1b783-172">After implementing a cmdlet, it must be registered with Windows PowerShell through a Windows PowerShell snap-in.</span></span> <span data-ttu-id="1b783-173">Parancsmagok regisztrálásával kapcsolatos további információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).</span><span class="sxs-lookup"><span data-stu-id="1b783-173">For more information about registering cmdlets, see [How to Register Cmdlets, Providers, and Host Applications](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).</span></span>

## <a name="testing-the-cmdlet"></a><span data-ttu-id="1b783-174">A parancsmag tesztelése</span><span class="sxs-lookup"><span data-stu-id="1b783-174">Testing the Cmdlet</span></span>

<span data-ttu-id="1b783-175">Ha a parancsmagot a Windows PowerShell-lel regisztrálva lett, azt a parancssorból való futtatásával tesztelheti.</span><span class="sxs-lookup"><span data-stu-id="1b783-175">When your cmdlet has been registered with Windows PowerShell, you can test it by running it on the command line.</span></span> <span data-ttu-id="1b783-176">Most tesztelje a parancsmagra állítsa le a folyamaton.</span><span class="sxs-lookup"><span data-stu-id="1b783-176">Let's test the sample Stop-Proc cmdlet.</span></span> <span data-ttu-id="1b783-177">A parancssorból-parancsmagokkal kapcsolatos további információkért lásd: a [első lépések a Windows PowerShell-lel](/powershell/scripting/getting-started/getting-started-with-windows-powershell).</span><span class="sxs-lookup"><span data-stu-id="1b783-177">For more information about using cmdlets from the command line, see the [Getting Started with Windows PowerShell](/powershell/scripting/getting-started/getting-started-with-windows-powershell).</span></span>

- <span data-ttu-id="1b783-178">A következő parancssori bejegyzés állítsa le a folyamaton használatával állítsa le a "JEGYZETTÖMB" nevű folyamatot, adja meg a részletes értesítések és a nyomtatási ladicí informace.</span><span class="sxs-lookup"><span data-stu-id="1b783-178">The following command-line entry uses Stop-Proc to stop the process named "NOTEPAD", provide verbose notifications, and print debug information.</span></span>

    ```powershell
    PS> stop-proc -Name notepad -Verbose -Debug
    ```

<span data-ttu-id="1b783-179">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="1b783-179">The following output appears.</span></span>

    ```
    VERBOSE: Attempting to stop process " notepad ".
    DEBUG: Acquired name for pid 5584 : "notepad"

    Confirm
    Continue with this operation?
    [Y] Yes  [A] Yes to All  [H] Halt Command  [S] Suspend  [?] Help (default is "Y"): Y

    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "notepad (5584)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y
    VERBOSE: Stopped process "notepad", pid 5584.
    ```

## <a name="see-also"></a><span data-ttu-id="1b783-180">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="1b783-180">See Also</span></span>

[<span data-ttu-id="1b783-181">Hozzon létre egy parancsmag, amely módosítja a rendszer</span><span class="sxs-lookup"><span data-stu-id="1b783-181">Create a Cmdlet that Modifies the System</span></span>](./creating-a-cmdlet-that-modifies-the-system.md)

[<span data-ttu-id="1b783-182">Hogyan hozhat létre egy Windows PowerShell-parancsmag</span><span class="sxs-lookup"><span data-stu-id="1b783-182">How to Create a Windows PowerShell Cmdlet</span></span>](http://msdn.microsoft.com/en-us/0d721742-c849-4d0d-964f-78ddd9cd258c)

[<span data-ttu-id="1b783-183">Objektumtípusok kiterjesztése és formázása</span><span class="sxs-lookup"><span data-stu-id="1b783-183">Extending Object Types and Formatting</span></span>](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[<span data-ttu-id="1b783-184">How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez</span><span class="sxs-lookup"><span data-stu-id="1b783-184">How to Register Cmdlets, Providers, and Host Applications</span></span>](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[<span data-ttu-id="1b783-185">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="1b783-185">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
