---
title: A parancsmag létrehozása, amely módosítja a rendszer |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- should process [PowerShell Programmer's Guide]
- should continue [PowerShell Programmer's Guide]
- user feedback [PowerShell Programmer's Guide]
- confirm impact [PowerShell Programmer's Guide]
ms.assetid: 59be4120-1700-4d92-a308-ef4a32ccf11a
caps.latest.revision: 8
ms.openlocfilehash: 8a65915b88a04e36e773853b903528a65fe11e99
ms.sourcegitcommit: f60fa420bdc81db174e6168d3aeb11371e483162
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/20/2019
ms.locfileid: "67301389"
---
# <a name="creating-a-cmdlet-that-modifies-the-system"></a><span data-ttu-id="7ae43-102">Rendszermódosító parancsmag létrehozása</span><span class="sxs-lookup"><span data-stu-id="7ae43-102">Creating a Cmdlet that Modifies the System</span></span>

<span data-ttu-id="7ae43-103">A parancsmag néha módosítani kell a futó állapotot a rendszer, nem csak a Windows PowerShell-modul állapotát.</span><span class="sxs-lookup"><span data-stu-id="7ae43-103">Sometimes a cmdlet must modify the running state of the system, not just the state of the Windows PowerShell runtime.</span></span> <span data-ttu-id="7ae43-104">Ezekben az esetekben a parancsmag engedélyezi a felhasználó egy alkalommal-e a módosítás megerősítéséhez.</span><span class="sxs-lookup"><span data-stu-id="7ae43-104">In these cases, the cmdlet should allow the user a chance to confirm whether or not to make the change.</span></span>

<span data-ttu-id="7ae43-105">A parancsmag megerősítést támogatásához két dolgot kell tennie.</span><span class="sxs-lookup"><span data-stu-id="7ae43-105">To support confirmation a cmdlet must do two things.</span></span>

- <span data-ttu-id="7ae43-106">Deklarálja, hogy a parancsmag megerősítést támogatja a megadása esetén a [System.Management.Automation.CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute) úgy, hogy kulcsszó Cmdletbinding attribútum `true`.</span><span class="sxs-lookup"><span data-stu-id="7ae43-106">Declare that the cmdlet supports confirmation when you specify the [System.Management.Automation.CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute) attribute by setting the SupportsShouldProcess keyword to `true`.</span></span>

- <span data-ttu-id="7ae43-107">Hívás [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) (ahogyan az az alábbi példában látható) a parancsmag végrehajtása közben.</span><span class="sxs-lookup"><span data-stu-id="7ae43-107">Call [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) during the execution of the cmdlet (as shown in the following example).</span></span>

<span data-ttu-id="7ae43-108">Megerősítő támogatásával parancsmag tesz elérhetővé a `Confirm` és `WhatIf` paraméterek, amelyeket a Windows PowerShell által biztosított, és megfelel a fejlesztési irányelveket a parancsmagok (parancsmag fejlesztési irányelvek kapcsolatos további információkért lásd: [ A parancsmag fejlesztési irányelvek](./cmdlet-development-guidelines.md).).</span><span class="sxs-lookup"><span data-stu-id="7ae43-108">By supporting confirmation, a cmdlet exposes the `Confirm` and `WhatIf` parameters that are provided by Windows PowerShell, and also meets the development guidelines for cmdlets (For more information about cmdlet development guidelines, see [Cmdlet Development Guidelines](./cmdlet-development-guidelines.md).).</span></span>

## <a name="changing-the-system"></a><span data-ttu-id="7ae43-109">A rendszer módosítása</span><span class="sxs-lookup"><span data-stu-id="7ae43-109">Changing the System</span></span>

<span data-ttu-id="7ae43-110">A művelet, "módosítása a rendszer", amely potenciálisan a Windows PowerShell kívül a rendszer állapotának módosítása minden parancsmag hivatkozik.</span><span class="sxs-lookup"><span data-stu-id="7ae43-110">The act of "changing the system" refers to any cmdlet that potentially changes the state of the system outside Windows PowerShell.</span></span> <span data-ttu-id="7ae43-111">Ha például leállítása folyamatban van egy folyamat, engedélyezése vagy letiltása egy felhasználói fiókot, vagy egy sort egy adatbázistábla soraihoz való is meg kell erősíteni a rendszer az összes változtatás hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="7ae43-111">For example, stopping a process, enabling or disabling a user account, or adding a row to a database table are all changes to the system that should be confirmed.</span></span> <span data-ttu-id="7ae43-112">Ezzel szemben az operatív adatok olvasása vagy átmeneti kapcsolatokat hozhat létre ne módosítsa a rendszer, és általában nem kell megerősítést.</span><span class="sxs-lookup"><span data-stu-id="7ae43-112">In contrast, operations that read data or establish transient connections do not change the system and generally do not require confirmation.</span></span> <span data-ttu-id="7ae43-113">Megerősítő is nem szükséges műveleteket, amelynek érvénybe korlátozódik belül a Windows PowerShell-futtatókörnyezet, mint például a `set-variable`.</span><span class="sxs-lookup"><span data-stu-id="7ae43-113">Confirmation is also not needed for actions whose effect is limited to inside the Windows PowerShell runtime, such as `set-variable`.</span></span> <span data-ttu-id="7ae43-114">Parancsmagok, amelyek vagy előfordulhat, hogy nem módosítsa egy állandó deklarálnia kell `SupportsShouldProcess` hívja [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) csak akkor, ha azok készül, hogy módosítsa egy állandó.</span><span class="sxs-lookup"><span data-stu-id="7ae43-114">Cmdlets that might or might not make a persistent change should declare `SupportsShouldProcess` and call [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) only if they are about to make a persistent change.</span></span>

> [!NOTE]
> <span data-ttu-id="7ae43-115">ShouldProcess megerősítő csak parancsmagok vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="7ae43-115">ShouldProcess confirmation applies only to cmdlets.</span></span> <span data-ttu-id="7ae43-116">Ha egy parancs vagy parancsfájl módosítja a futó állapotot a rendszer közvetlenül meghívásával a .NET-metódusokat és tulajdonságokat, vagy a hívó alkalmazások, kívül a Windows PowerShell, az ilyen típusú megerősítő nem lesz elérhető.</span><span class="sxs-lookup"><span data-stu-id="7ae43-116">If a command or script modifies the running state of a system by directly calling .NET methods or properties, or by calling applications outside of Windows PowerShell, this form of confirmation will not be available.</span></span>

## <a name="the-stopproc-cmdlet"></a><span data-ttu-id="7ae43-117">A StopProc parancsmag</span><span class="sxs-lookup"><span data-stu-id="7ae43-117">The StopProc Cmdlet</span></span>

<span data-ttu-id="7ae43-118">Ez a témakör ismerteti, amely megpróbálja leállítani a folyamatokat, amelyek a Get-Proc parancsmaggal olvassa be a Stop-Proc parancsmag (ismertetett [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md)).</span><span class="sxs-lookup"><span data-stu-id="7ae43-118">This topic describes a Stop-Proc cmdlet that attempts to stop processes that are retrieved using the Get-Proc cmdlet (described in [Creating Your First Cmdlet](./creating-a-cmdlet-without-parameters.md)).</span></span>

## <a name="defining-the-cmdlet"></a><span data-ttu-id="7ae43-119">A parancsmag meghatározása</span><span class="sxs-lookup"><span data-stu-id="7ae43-119">Defining the Cmdlet</span></span>

<span data-ttu-id="7ae43-120">Mindig a parancsmag elnevezési és a .NET-osztály, amely megvalósítja a parancsmag deklaráló parancsmag létrehozásának első lépése.</span><span class="sxs-lookup"><span data-stu-id="7ae43-120">The first step in cmdlet creation is always naming the cmdlet and declaring the .NET class that implements the cmdlet.</span></span> <span data-ttu-id="7ae43-121">Kell írnia egy parancsmaggal módosíthatja, a rendszer, mert ennek megfelelően kell elnevezni azt.</span><span class="sxs-lookup"><span data-stu-id="7ae43-121">Because you are writing a cmdlet to change the system, it should be named accordingly.</span></span> <span data-ttu-id="7ae43-122">A parancsmag leáll rendszer folyamataihoz, így az itt választott művelet neve "Stop" határozzák meg a [System.Management.Automation.Verbslifecycle](/dotnet/api/System.Management.Automation.VerbsLifeCycle) osztályt, a főnév "Proc" jelzi, hogy a parancsmag leállítja a folyamatot.</span><span class="sxs-lookup"><span data-stu-id="7ae43-122">This cmdlet stops system processes, so the verb name chosen here is "Stop", defined by the [System.Management.Automation.Verbslifecycle](/dotnet/api/System.Management.Automation.VerbsLifeCycle) class, with the noun "Proc" to indicate that the cmdlet stops processes.</span></span> <span data-ttu-id="7ae43-123">A parancsmag jóváhagyott igék kapcsolatos további információkért lásd: [művelet neve](./approved-verbs-for-windows-powershell-commands.md).</span><span class="sxs-lookup"><span data-stu-id="7ae43-123">For more information about approved cmdlet verbs, see [Cmdlet Verb Names](./approved-verbs-for-windows-powershell-commands.md).</span></span>

<span data-ttu-id="7ae43-124">A Stop-Proc parancsmag osztály definícióját a következő:</span><span class="sxs-lookup"><span data-stu-id="7ae43-124">The following is the class definition for this Stop-Proc cmdlet.</span></span>

```csharp
[Cmdlet(VerbsLifecycle.Stop, "Proc",
        SupportsShouldProcess = true)]
public class StopProcCommand : Cmdlet
```

<span data-ttu-id="7ae43-125">Vegye figyelembe, hogy a [System.Management.Automation.CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute) nyilatkozat, a `SupportsShouldProcess` kulcsszó attribútum értéke `true` engedélyezéséhez a parancsmag való meghíváshoz [ System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) és [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue).</span><span class="sxs-lookup"><span data-stu-id="7ae43-125">Be aware that in the [System.Management.Automation.CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute) declaration, the `SupportsShouldProcess` attribute keyword is set to `true` to enable the cmdlet to make calls to [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) and [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue).</span></span> <span data-ttu-id="7ae43-126">A kulcsszó beállítása nélkül a `Confirm` és `WhatIf` paraméterek nem lesz elérhető, a felhasználó számára.</span><span class="sxs-lookup"><span data-stu-id="7ae43-126">Without this keyword set, the `Confirm` and `WhatIf` parameters will not be available to the user.</span></span>

### <a name="extremely-destructive-actions"></a><span data-ttu-id="7ae43-127">Rendkívül felülíró művelet</span><span class="sxs-lookup"><span data-stu-id="7ae43-127">Extremely Destructive Actions</span></span>

<span data-ttu-id="7ae43-128">Egyes műveletek károsak rendkívül, például egy aktív merevlemez-partíciók újraformázást.</span><span class="sxs-lookup"><span data-stu-id="7ae43-128">Some operations are extremely destructive, such as reformatting an active hard disk partition.</span></span> <span data-ttu-id="7ae43-129">Ezekben az esetekben a parancsmag kell beállítania `ConfirmImpact`  =  `ConfirmImpact.High` deklarálásakor a [System.Management.Automation.CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute) attribútum.</span><span class="sxs-lookup"><span data-stu-id="7ae43-129">In these cases, the cmdlet should set `ConfirmImpact` = `ConfirmImpact.High` when declaring the [System.Management.Automation.CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute) attribute.</span></span> <span data-ttu-id="7ae43-130">Ez a beállítás kényszeríti a parancsmag kérelem felhasználói jóváhagyás, akkor is, ha a felhasználó nem adta meg a `Confirm` paraméter.</span><span class="sxs-lookup"><span data-stu-id="7ae43-130">This setting forces the cmdlet to request user confirmation even when the user has not specified the `Confirm` parameter.</span></span> <span data-ttu-id="7ae43-131">Azonban a parancsmag a fejlesztők kerülendő túlzott mértékű használata `ConfirmImpact` műveletek, amelyek csak potenciálisan ártalmas, például a felhasználói fiók törlése.</span><span class="sxs-lookup"><span data-stu-id="7ae43-131">However, cmdlet developers should avoid overusing `ConfirmImpact` for operations that are just potentially destructive, such as deleting a user account.</span></span> <span data-ttu-id="7ae43-132">Ne feledje, hogy `ConfirmImpact` értékre van állítva [System.Management.Automation.ConfirmImpact](/dotnet/api/System.Management.Automation.ConfirmImpact) **magas**.</span><span class="sxs-lookup"><span data-stu-id="7ae43-132">Remember that if `ConfirmImpact` is set to [System.Management.Automation.ConfirmImpact](/dotnet/api/System.Management.Automation.ConfirmImpact) **High**.</span></span>

<span data-ttu-id="7ae43-133">Egyes műveletekre hasonló módon, nagy valószínűséggel nem romboló, Bár elméletben módosíthatják kívül a Windows PowerShell rendszert a futó állapotot.</span><span class="sxs-lookup"><span data-stu-id="7ae43-133">Similarly, some operations are unlikely to be destructive, although they do in theory modify the running state of a system outside Windows PowerShell.</span></span> <span data-ttu-id="7ae43-134">Az ilyen parancsmagok állíthatja `ConfirmImpact` való [System.Management.Automation.Confirmimpact.Low](/dotnet/api/system.management.automation.confirmimpact?view=powershellsdk-1.1.0).</span><span class="sxs-lookup"><span data-stu-id="7ae43-134">Such cmdlets can set `ConfirmImpact` to [System.Management.Automation.Confirmimpact.Low](/dotnet/api/system.management.automation.confirmimpact?view=powershellsdk-1.1.0).</span></span> <span data-ttu-id="7ae43-135">Ez fog kerülni eseménymegerősítési kéréseknek, ahol a felhasználó erősítse meg a csak a közepes hatású és a nagy hatású műveletek kérte.</span><span class="sxs-lookup"><span data-stu-id="7ae43-135">This will bypass confirmation requests where the user has asked to confirm only medium-impact and high-impact operations.</span></span>

## <a name="defining-parameters-for-system-modification"></a><span data-ttu-id="7ae43-136">A rendszer módosítás paraméterek megadása</span><span class="sxs-lookup"><span data-stu-id="7ae43-136">Defining Parameters for System Modification</span></span>

<span data-ttu-id="7ae43-137">Ez a szakasz ismerteti, hogyan adhat meg a parancsmag paramétereit, beleértve azokat is, a támogatási rendszerben módosítás van szükség.</span><span class="sxs-lookup"><span data-stu-id="7ae43-137">This section describes how to define the cmdlet parameters, including those that are needed to support system modification.</span></span> <span data-ttu-id="7ae43-138">Lásd: [a folyamat CommandLine bemeneti paramétereket adunk hozzá](./adding-parameters-that-process-command-line-input.md) Ha paramétereket meghatározó kapcsolatos általános információra van szüksége.</span><span class="sxs-lookup"><span data-stu-id="7ae43-138">See [Adding Parameters that Process CommandLine Input](./adding-parameters-that-process-command-line-input.md) if you need general information about defining parameters.</span></span>

<span data-ttu-id="7ae43-139">A Stop-Proc parancsmag meghatározása három paramétert: `Name`, `Force`, és `PassThru`.</span><span class="sxs-lookup"><span data-stu-id="7ae43-139">The Stop-Proc cmdlet defines three parameters: `Name`, `Force`, and `PassThru`.</span></span>

<span data-ttu-id="7ae43-140">A `Name` paraméter felel meg a `Name` a folyamat bemeneti objektum tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="7ae43-140">The `Name` parameter corresponds to the `Name` property of the process input object.</span></span> <span data-ttu-id="7ae43-141">Vegye figyelembe, hogy a `Name` ebben a példában paramétert kötelező, mivel a parancsmag sikertelen lesz, ha nem rendelkezik egy névvel ellátott folyamat leállítása.</span><span class="sxs-lookup"><span data-stu-id="7ae43-141">Be aware that the `Name` parameter in this sample is mandatory, as the cmdlet will fail if it does not have a named process to stop.</span></span>

<span data-ttu-id="7ae43-142">A `Force` paraméter lehetővé teszi, hogy a felhasználó felülbírálhatja a hívások [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue).</span><span class="sxs-lookup"><span data-stu-id="7ae43-142">The `Force` parameter allows the user to override calls to [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue).</span></span> <span data-ttu-id="7ae43-143">Tulajdonképpen bármely parancsmag, amely meghívja a [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) rendelkeznie kell egy `Force` paramétert, hogy amikor `Force` van megadva, a parancsmag meghívása kihagyja [ System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) és folytatja a műveletet.</span><span class="sxs-lookup"><span data-stu-id="7ae43-143">In fact, any cmdlet that calls [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) should have a `Force` parameter so that when `Force` is specified, the cmdlet skips the call to [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) and proceeds with the operation.</span></span> <span data-ttu-id="7ae43-144">Vegye figyelembe, hogy ez nincs hatással a hívások [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess).</span><span class="sxs-lookup"><span data-stu-id="7ae43-144">Be aware that this does not affect calls to [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess).</span></span>

<span data-ttu-id="7ae43-145">A `PassThru` paraméter lehetővé teszi, hogy a felhasználó-e a parancsmag adja át a kimeneti objektum keresztül, ebben az esetben egy folyamat Leállítás utáni jelzi.</span><span class="sxs-lookup"><span data-stu-id="7ae43-145">The `PassThru` parameter allows the user to indicate whether the cmdlet passes an output object through the pipeline, in this case, after a process is stopped.</span></span> <span data-ttu-id="7ae43-146">Vegye figyelembe, hogy ezt a paramétert a parancsmaghoz saját maga helyett egy tulajdonság a bemeneti objektum van kötve.</span><span class="sxs-lookup"><span data-stu-id="7ae43-146">Be aware that this parameter is tied to the cmdlet itself instead of to a property of the input object.</span></span>

<span data-ttu-id="7ae43-147">Íme a Stop-Proc parancsmagok a paraméterdeklarációhoz.</span><span class="sxs-lookup"><span data-stu-id="7ae43-147">Here is the parameter declaration for the Stop-Proc cmdlet.</span></span>

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

## <a name="overriding-an-input-processing-method"></a><span data-ttu-id="7ae43-148">Egy bemeneti metódus feldolgozási felülbírálása</span><span class="sxs-lookup"><span data-stu-id="7ae43-148">Overriding an Input Processing Method</span></span>

<span data-ttu-id="7ae43-149">A parancsmag felül kell írnia egy bemeneti metódus feldolgozása.</span><span class="sxs-lookup"><span data-stu-id="7ae43-149">The cmdlet must override an input processing method.</span></span> <span data-ttu-id="7ae43-150">Az alábbi kód bemutatja a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) használja a Stop-Proc parancsmagra felülbírálás.</span><span class="sxs-lookup"><span data-stu-id="7ae43-150">The following code illustrates the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) override used in the sample Stop-Proc cmdlet.</span></span> <span data-ttu-id="7ae43-151">Az egyes kért Folyamatnév, ez a módszer biztosítja, hogy a folyamat nem egy külön folyamat, megkísérli leállítani a folyamatot, és ezután elküldi a kimeneti objektum, ha a `PassThru` paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="7ae43-151">For each requested process name, this method ensures that the process is not a special process, tries to stop the process, and then sends an output object if the `PassThru` parameter is specified.</span></span>

```csharp
protected override void ProcessRecord()
{
  foreach (string name in processNames)
  {
    // For every process name passed to the cmdlet, get the associated
    // process(es). For failures, write a non-terminating error
    Process[] processes;

    try
    {
      processes = Process.GetProcessesByName(name);
    }
    catch (InvalidOperationException ioe)
    {
      WriteError(new ErrorRecord(ioe,"Unable to access the target process by name",
                 ErrorCategory.InvalidOperation, name));
      continue;
    }

    // Try to stop the process(es) that have been retrieved for a name
    foreach (Process process in processes)
    {
      string processName;

      try
      {
        processName = process.ProcessName;
      }

      catch (Win32Exception e)
        {
          WriteError(new ErrorRecord(e, "ProcessNameNotFound",
                     ErrorCategory.ReadError, process));
          continue;
        }

        // Call Should Process to confirm the operation first.
        // This is always false if WhatIf is set.
        if (!ShouldProcess(string.Format("{0} ({1})", processName,
                           process.Id)))
        {
          continue;
        }
        // Call ShouldContinue to make sure the user really does want
        // to stop a critical process that could possibly stop the computer.
        bool criticalProcess =
             criticalProcessNames.Contains(processName.ToLower());

        if (criticalProcess &&!force)
        {
          string message = String.Format
                ("The process \"{0}\" is a critical process and should not be stopped. Are you sure you wish to stop the process?",
                processName);

          // It is possible that ProcessRecord is called multiple times
          // when the Name parameter receives objects as input from the
          // pipeline. So to retain YesToAll and NoToAll input that the
          // user may enter across multiple calls to ProcessRecord, this
          // information is stored as private members of the cmdlet.
          if (!ShouldContinue(message, "Warning!",
                              ref yesToAll,
                              ref noToAll))
          {
            continue;
          }
        } // if (criticalProcess...
        // Stop the named process.
        try
        {
          process.Kill();
        }
        catch (Exception e)
        {
          if ((e is Win32Exception) || (e is SystemException) ||
              (e is InvalidOperationException))
          {
            // This process could not be stopped so write
            // a non-terminating error.
            string message = String.Format("{0} {1} {2}",
                             "Could not stop process \"", processName,
                             "\".");
            WriteError(new ErrorRecord(e, message,
                       ErrorCategory.CloseError, process));
                       continue;
          } // if ((e is...
          else throw;
        } // catch

        // If the PassThru parameter argument is
        // True, pass the terminated process on.
        if (passThru)
        {
          WriteObject(process);
        }
    } // foreach (Process...
  } // foreach (string...
} // ProcessRecord
```

## <a name="calling-the-shouldprocess-method"></a><span data-ttu-id="7ae43-152">A ShouldProcess metódus hívása</span><span class="sxs-lookup"><span data-stu-id="7ae43-152">Calling the ShouldProcess Method</span></span>

<span data-ttu-id="7ae43-153">A feldolgozási mód a parancsmag bemeneti meg kell hívnia a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódust (például törlése fájlok) módosításakor a működőképes állapotba előtt, győződjön meg arról, hogy egy művelet végrehajtása a rendszer.</span><span class="sxs-lookup"><span data-stu-id="7ae43-153">The input processing method of your cmdlet should call the [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) method to confirm execution of an operation before a change (for example, deleting files) is made to the running state of the system.</span></span> <span data-ttu-id="7ae43-154">Ez lehetővé teszi a Windows PowerShell modul megadnia a rendszerhéjból a megfelelő "WhatIf" és "Confirm" viselkedését.</span><span class="sxs-lookup"><span data-stu-id="7ae43-154">This allows the Windows PowerShell runtime to supply the correct "WhatIf" and "Confirm" behavior within the shell.</span></span>

> [!NOTE]
> <span data-ttu-id="7ae43-155">Ha a parancsmag kijelenti, hogy támogatja a kell dolgoznia, és győződjön meg arról, hogy nem sikerül a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) hívja, a felhasználó váratlanul előfordulhat, hogy módosítsa a rendszer.</span><span class="sxs-lookup"><span data-stu-id="7ae43-155">If a cmdlet states that it supports should process and fails to make the [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) call, the user might modify the system unexpectedly.</span></span>

<span data-ttu-id="7ae43-156">A hívás [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) küld a felhasználó a Windows PowerShell-futtatókörnyezetben, figyelembe véve parancssori beállítást vagy preferenciaváltozók módosítani az erőforrás neve a meghatározása, mi megjelenjenek a felhasználó számára.</span><span class="sxs-lookup"><span data-stu-id="7ae43-156">The call to [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) sends the name of the resource to be changed to the user, with the Windows PowerShell runtime taking into account any command-line settings or preference variables in determining what should be displayed to the user.</span></span>

<span data-ttu-id="7ae43-157">Az alábbi példa bemutatja a hívást [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) a felülbírálását a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódusban a minta Állítsa le a folyamaton parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="7ae43-157">The following example shows the call to [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) from the override of the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method in the sample Stop-Proc cmdlet.</span></span>

```csharp
if (!ShouldProcess(string.Format("{0} ({1})", processName,
                   process.Id)))
{
  continue;
}
```

## <a name="calling-the-shouldcontinue-method"></a><span data-ttu-id="7ae43-158">A ShouldContinue metódus hívása</span><span class="sxs-lookup"><span data-stu-id="7ae43-158">Calling the ShouldContinue Method</span></span>

<span data-ttu-id="7ae43-159">A hívást a [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) metódus elküld egy másodlagos üzenetet a felhasználónak.</span><span class="sxs-lookup"><span data-stu-id="7ae43-159">The call to the [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) method sends a secondary message to the user.</span></span> <span data-ttu-id="7ae43-160">A kérés érkezett hívása után [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) adja vissza `true` , és ha a `Force` paraméter nem volt beállítva `true`.</span><span class="sxs-lookup"><span data-stu-id="7ae43-160">This call is made after the call to [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) returns `true` and if the `Force` parameter was not set to `true`.</span></span> <span data-ttu-id="7ae43-161">A felhasználó ezután visszajelzést küldhet a tegyük fel, hogy a művelet folytatni kell.</span><span class="sxs-lookup"><span data-stu-id="7ae43-161">The user can then provide feedback to say whether the operation should be continued.</span></span> <span data-ttu-id="7ae43-162">A parancsmag hívásokat [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) , egy további ellenőrzési potenciálisan veszélyes rendszermódosítások, vagy ha szeretné, hogy a felhasználó igen-mindig és nem mindig beállításokat biztosítson.</span><span class="sxs-lookup"><span data-stu-id="7ae43-162">Your cmdlet calls [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) as an additional check for potentially dangerous system modifications or when you want to provide yes-to-all and no-to-all options to the user.</span></span>

<span data-ttu-id="7ae43-163">Az alábbi példa bemutatja a hívást [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) a felülbírálását a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódusban a minta Állítsa le a folyamaton parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="7ae43-163">The following example shows the call to [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) from the override of the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method in the sample Stop-Proc cmdlet.</span></span>

```csharp
if (criticalProcess &&!force)
{
  string message = String.Format
        ("The process \"{0}\" is a critical process and should not be stopped. Are you sure you wish to stop the process?",
        processName);

  // It is possible that ProcessRecord is called multiple times
  // when the Name parameter receives objects as input from the
  // pipeline. So to retain YesToAll and NoToAll input that the
  // user may enter across multiple calls to ProcessRecord, this
  // information is stored as private members of the cmdlet.
  if (!ShouldContinue(message, "Warning!",
                      ref yesToAll,
                      ref noToAll))
  {
    continue;
  }
} // if (criticalProcess...
```

## <a name="stopping-input-processing"></a><span data-ttu-id="7ae43-164">A bemeneti feldolgozó leállítása</span><span class="sxs-lookup"><span data-stu-id="7ae43-164">Stopping Input Processing</span></span>

<span data-ttu-id="7ae43-165">A bemenet feldolgozásának leállítása lehetőséget kell biztosítani a metódus egy parancsmag, amellyel a rendszer a módosítások feldolgozása a bemeneti.</span><span class="sxs-lookup"><span data-stu-id="7ae43-165">The input processing method of a cmdlet that makes system modifications must provide a way of stopping the processing of input.</span></span> <span data-ttu-id="7ae43-166">A Stop-Proc parancsmag esetében a kérés érkezett a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust a [System.Diagnostics.Process.Kill\*](/dotnet/api/System.Diagnostics.Process.Kill) metódust.</span><span class="sxs-lookup"><span data-stu-id="7ae43-166">In the case of this Stop-Proc cmdlet, a call is made from the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method to the [System.Diagnostics.Process.Kill\*](/dotnet/api/System.Diagnostics.Process.Kill) method.</span></span> <span data-ttu-id="7ae43-167">Mivel a `PassThru` paraméter értéke `true`, [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) is meghívja [System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) küldése a folyamat objektumról a folyamathoz.</span><span class="sxs-lookup"><span data-stu-id="7ae43-167">Because the `PassThru` parameter is set to `true`, [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) also calls [System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) to send the process object to the pipeline.</span></span>

## <a name="code-sample"></a><span data-ttu-id="7ae43-168">Kódminta</span><span class="sxs-lookup"><span data-stu-id="7ae43-168">Code Sample</span></span>

<span data-ttu-id="7ae43-169">A teljes C# mintakód, lásd: [StopProcessSample01 minta](./stopprocesssample01-sample.md).</span><span class="sxs-lookup"><span data-stu-id="7ae43-169">For the complete C# sample code, see [StopProcessSample01 Sample](./stopprocesssample01-sample.md).</span></span>

## <a name="defining-object-types-and-formatting"></a><span data-ttu-id="7ae43-170">Objektumtípusok definiálása és formázása</span><span class="sxs-lookup"><span data-stu-id="7ae43-170">Defining Object Types and Formatting</span></span>

<span data-ttu-id="7ae43-171">Windows PowerShell parancsmagok használatával a .net-objektumokká közötti továbbítja.</span><span class="sxs-lookup"><span data-stu-id="7ae43-171">Windows PowerShell passes information between cmdlets using .Net objects.</span></span> <span data-ttu-id="7ae43-172">Ennek következtében a parancsmag előfordulhat, hogy meg kell határoznia a saját típusát, vagy a parancsmag előfordulhat, hogy ki kell terjesztenie egy másik parancsmag által biztosított meglévő típus.</span><span class="sxs-lookup"><span data-stu-id="7ae43-172">Consequently, a cmdlet may need to define its own type, or the cmdlet may need to extend an existing type provided by another cmdlet.</span></span> <span data-ttu-id="7ae43-173">Új típusok meghatározása, vagy meglévő típusok bővítésével kapcsolatos további információkért lásd: [objektumtípusok kiterjesztése és formázás](/previous-versions//ms714665(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="7ae43-173">For more information about defining new types or extending existing types, see [Extending Object Types and Formatting](/previous-versions//ms714665(v=vs.85)).</span></span>

## <a name="building-the-cmdlet"></a><span data-ttu-id="7ae43-174">A parancsmag készítése</span><span class="sxs-lookup"><span data-stu-id="7ae43-174">Building the Cmdlet</span></span>

<span data-ttu-id="7ae43-175">Parancsmag-k megvalósítása után regisztrálni kell a Windows PowerShell-lel a Windows PowerShell beépülő modullal.</span><span class="sxs-lookup"><span data-stu-id="7ae43-175">After implementing a cmdlet, it must be registered with Windows PowerShell through a Windows PowerShell snap-in.</span></span> <span data-ttu-id="7ae43-176">Parancsmagok regisztrálásával kapcsolatos további információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](/previous-versions//ms714644(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="7ae43-176">For more information about registering cmdlets, see [How to Register Cmdlets, Providers, and Host Applications](/previous-versions//ms714644(v=vs.85)).</span></span>

## <a name="testing-the-cmdlet"></a><span data-ttu-id="7ae43-177">A parancsmag tesztelése</span><span class="sxs-lookup"><span data-stu-id="7ae43-177">Testing the Cmdlet</span></span>

<span data-ttu-id="7ae43-178">Ha a parancsmagot a Windows PowerShell-lel regisztrálva lett, azt a parancssorból való futtatásával tesztelheti.</span><span class="sxs-lookup"><span data-stu-id="7ae43-178">When your cmdlet has been registered with Windows PowerShell, you can test it by running it on the command line.</span></span> <span data-ttu-id="7ae43-179">Az alábbiakban számos tesztet, amely a Stop-Proc parancsmag teszteléséhez.</span><span class="sxs-lookup"><span data-stu-id="7ae43-179">Here are several tests that test the Stop-Proc cmdlet.</span></span> <span data-ttu-id="7ae43-180">A parancssorból-parancsmagokkal kapcsolatos további információkért lásd: a [első lépések a Windows PowerShell-lel](/powershell/scripting/getting-started/getting-started-with-windows-powershell).</span><span class="sxs-lookup"><span data-stu-id="7ae43-180">For more information about using cmdlets from the command line, see the [Getting Started with Windows PowerShell](/powershell/scripting/getting-started/getting-started-with-windows-powershell).</span></span>

- <span data-ttu-id="7ae43-181">Indítsa el a Windows Powershellt, és leállítja a feldolgozást, ahogy az alábbi a Stop-Proc parancsmag használatával.</span><span class="sxs-lookup"><span data-stu-id="7ae43-181">Start Windows PowerShell and use the Stop-Proc cmdlet to stop processing as shown below.</span></span> <span data-ttu-id="7ae43-182">Mivel a parancsmag a határozza meg a `Name` , kötelező paraméter, a parancsmag-lekérdezések a paraméterhez.</span><span class="sxs-lookup"><span data-stu-id="7ae43-182">Because the cmdlet specifies the `Name` parameter as mandatory, the cmdlet queries for the parameter.</span></span>

    ```powershell
    PS> stop-proc
    ```

<span data-ttu-id="7ae43-183">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="7ae43-183">The following output appears.</span></span>

    ```
    Cmdlet stop-proc at command pipeline position 1
    Supply values for the following parameters:
    Name[0]:
    ```

- <span data-ttu-id="7ae43-184">Most pedig a parancsmag használatával állítsa le a "JEGYZETTÖMB" nevű folyamatot.</span><span class="sxs-lookup"><span data-stu-id="7ae43-184">Now let's use the cmdlet to stop the process named "NOTEPAD".</span></span> <span data-ttu-id="7ae43-185">A parancsmag kéri, hogy erősítse meg a műveletet.</span><span class="sxs-lookup"><span data-stu-id="7ae43-185">The cmdlet asks you to confirm the action.</span></span>

    ```powershell
    PS> stop-proc -Name notepad
    ```

<span data-ttu-id="7ae43-186">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="7ae43-186">The following output appears.</span></span>

    ```
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "notepad (4996)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y
    ```

- <span data-ttu-id="7ae43-187">Használatával állítsa le a folyamaton látható módon állítsa le a kritikus fontosságú "WINLOGON" folyamatot.</span><span class="sxs-lookup"><span data-stu-id="7ae43-187">Use Stop-Proc as shown to stop the critical process named "WINLOGON".</span></span> <span data-ttu-id="7ae43-188">Ön kéri, és a művelet végrehajtása, mert ennek az operációs rendszer újraindítását kapcsolatos figyelmeztetést kap.</span><span class="sxs-lookup"><span data-stu-id="7ae43-188">You are prompted and warned about performing this action because it will cause the operating system to reboot.</span></span>

    ```powershell
    PS> stop-proc -Name Winlogon
    ```

<span data-ttu-id="7ae43-189">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="7ae43-189">The following output appears.</span></span>

    ```output
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "winlogon (656)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y
    Warning!
    The process " winlogon " is a critical process and should not be stopped. Are you sure you wish to stop the process?
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): N
    ```

- <span data-ttu-id="7ae43-190">Most próbáljon nélkül figyelmeztetést kap a WINLOGON folyamat leállítása érdekében.</span><span class="sxs-lookup"><span data-stu-id="7ae43-190">Let's now try to stop the WINLOGON process without receiving a warning.</span></span> <span data-ttu-id="7ae43-191">Vegye figyelembe, hogy használja-e ez a parancs a bejegyzés a `Force` paraméter a figyelmeztetés felülbírálása.</span><span class="sxs-lookup"><span data-stu-id="7ae43-191">Be aware that this command entry uses the `Force` parameter to override the warning.</span></span>

    ```powershell
    PS> stop-proc -Name winlogon -Force
    ```

<span data-ttu-id="7ae43-192">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="7ae43-192">The following output appears.</span></span>

    ```output
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "winlogon (656)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): N
    ```

## <a name="see-also"></a><span data-ttu-id="7ae43-193">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="7ae43-193">See Also</span></span>

[<span data-ttu-id="7ae43-194">Parancssori bemenet feldolgozása paraméterek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="7ae43-194">Adding Parameters that Process Command-Line Input</span></span>](./adding-parameters-that-process-command-line-input.md)

<span data-ttu-id="7ae43-195">[Objektumtípusok kiterjesztése és formázása](/previous-versions//ms714665(v=vs.85))</span><span class="sxs-lookup"><span data-stu-id="7ae43-195">[Extending Object Types and Formatting](/previous-versions//ms714665(v=vs.85))</span></span>

<span data-ttu-id="7ae43-196">[How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez](/previous-versions//ms714644(v=vs.85))</span><span class="sxs-lookup"><span data-stu-id="7ae43-196">[How to Register Cmdlets, Providers, and Host Applications](/previous-versions//ms714644(v=vs.85))</span></span>

[<span data-ttu-id="7ae43-197">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="7ae43-197">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)

[<span data-ttu-id="7ae43-198">Parancsmag-minták</span><span class="sxs-lookup"><span data-stu-id="7ae43-198">Cmdlet Samples</span></span>](./cmdlet-samples.md)