---
title: Megszakítást nem a parancsmaghoz a hibajelentés hozzáadása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f2a1531a-a92a-4606-9d54-c5df80d34f33
caps.latest.revision: 8
ms.openlocfilehash: e0550dacc33f45f45ba105ca5cb4d2e5b5d675fb
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58056056"
---
# <a name="adding-non-terminating-error-reporting-to-your-cmdlet"></a><span data-ttu-id="198e4-102">Megszakítást nem okozó hibajelentések hozzáadása a parancsmaghoz</span><span class="sxs-lookup"><span data-stu-id="198e4-102">Adding Non-Terminating Error Reporting to Your Cmdlet</span></span>

<span data-ttu-id="198e4-103">Parancsmagok meghívásával nonterminating hibák jelentheti a [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) módszer továbbra is megfelelően működjenek, az aktuális bemeneti objektumon, vagy további bejövő és folyamat-objektumok.</span><span class="sxs-lookup"><span data-stu-id="198e4-103">Cmdlets can report nonterminating errors by calling the [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) method and still continue to operate on the current input object or on further incoming pipeline objects.</span></span> <span data-ttu-id="198e4-104">Ez a szakasz ismerteti, hogyan hozhat létre olyan parancsmagot, amely a bemeneti feldolgozási módszerei a nonterminating hibát jelez.</span><span class="sxs-lookup"><span data-stu-id="198e4-104">This section explains how to create a cmdlet that reports nonterminating errors from its input processing methods.</span></span>

<span data-ttu-id="198e4-105">Nonterminating hibák (csakúgy, mint a hibák megszakítást), a parancsmag át kell adnia egy [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektum a hiba azonosítása.</span><span class="sxs-lookup"><span data-stu-id="198e4-105">For nonterminating errors (as well as terminating errors), the cmdlet must pass an [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) object identifying the error.</span></span> <span data-ttu-id="198e4-106">Minden egyes hibarekord azonosíthatók egy egyedi karakterlánccá, úgynevezett "hiba azonosítója."</span><span class="sxs-lookup"><span data-stu-id="198e4-106">Each error record is identified by a unique string called the "error identifier."</span></span> <span data-ttu-id="198e4-107">Az azonosító mellett minden egyes hibához kategóriáját állandók határozzák meg által meghatározott egy [System.Management.Automation.Errorcategory](/dotnet/api/System.Management.Automation.ErrorCategory) enumerálása.</span><span class="sxs-lookup"><span data-stu-id="198e4-107">In addition to the identifier, the category of each error is specified by constants defined by a [System.Management.Automation.Errorcategory](/dotnet/api/System.Management.Automation.ErrorCategory) enumeration.</span></span> <span data-ttu-id="198e4-108">A felhasználó megtekintheti a hibákat azok kategória alapján beállításával a `$ErrorView` "CategoryView" változó.</span><span class="sxs-lookup"><span data-stu-id="198e4-108">The user can view errors based on their category by setting the `$ErrorView` variable to "CategoryView".</span></span>

<span data-ttu-id="198e4-109">Hiba a rekordok kapcsolatos további információkért lásd: [Windows PowerShell Hibarekordjainak](./windows-powershell-error-records.md).</span><span class="sxs-lookup"><span data-stu-id="198e4-109">For more information about error records, see [Windows PowerShell Error Records](./windows-powershell-error-records.md).</span></span>

<span data-ttu-id="198e4-110">Ez a szakasz témakörei a következők:</span><span class="sxs-lookup"><span data-stu-id="198e4-110">Topics in this section include the following:</span></span>

- [<span data-ttu-id="198e4-111">A parancsmag meghatározása</span><span class="sxs-lookup"><span data-stu-id="198e4-111">Defining the Cmdlet</span></span>](#Defining-the-Cmdlet)

- [<span data-ttu-id="198e4-112">Paraméterek megadása</span><span class="sxs-lookup"><span data-stu-id="198e4-112">Defining Parameters</span></span>](#Defining-Parameters)

- [<span data-ttu-id="198e4-113">Bemeneti feldolgozási módszerek felülbírálása</span><span class="sxs-lookup"><span data-stu-id="198e4-113">Overriding Input Processing Methods</span></span>](#Overriding-Input-Processing-Methods)

- [<span data-ttu-id="198e4-114">Nonterminating hibát jelentett</span><span class="sxs-lookup"><span data-stu-id="198e4-114">Reporting Nonterminating Errors</span></span>](#Reporting-Nonterminating-Errors)

- [<span data-ttu-id="198e4-115">Kódminta</span><span class="sxs-lookup"><span data-stu-id="198e4-115">Code Sample</span></span>](#Code-Sample)

- [<span data-ttu-id="198e4-116">Objektumtípusok definiálása és formázása</span><span class="sxs-lookup"><span data-stu-id="198e4-116">Defining Object Types and Formatting</span></span>](#Define-Object-Types-and-Formatting)

- [<span data-ttu-id="198e4-117">A parancsmag készítése</span><span class="sxs-lookup"><span data-stu-id="198e4-117">Building the Cmdlet</span></span>](#Building-the-Cmdlet)

- [<span data-ttu-id="198e4-118">A parancsmag tesztelése</span><span class="sxs-lookup"><span data-stu-id="198e4-118">Testing the Cmdlet</span></span>](#Testing-the-Cmdlet)

## <a name="defining-the-cmdlet"></a><span data-ttu-id="198e4-119">A parancsmag meghatározása</span><span class="sxs-lookup"><span data-stu-id="198e4-119">Defining the Cmdlet</span></span>

<span data-ttu-id="198e4-120">Mindig a parancsmag elnevezési és a .NET-osztály, amely megvalósítja a parancsmag deklaráló parancsmag létrehozásának első lépése.</span><span class="sxs-lookup"><span data-stu-id="198e4-120">The first step in cmdlet creation is always naming the cmdlet and declaring the .NET class that implements the cmdlet.</span></span> <span data-ttu-id="198e4-121">Ez a parancsmag folyamat adatait, kérdezi le, így az itt választott művelet neve "Get".</span><span class="sxs-lookup"><span data-stu-id="198e4-121">This cmdlet retrieves process information, so the verb name chosen here is "Get".</span></span> <span data-ttu-id="198e4-122">(A szinte bármilyen rendezési parancsmag, amely képes adatok beolvasása a parancssori bemenet tud feldolgozni.) A parancsmag jóváhagyott igék kapcsolatos további információkért lásd: [művelet neve](./approved-verbs-for-windows-powershell-commands.md).</span><span class="sxs-lookup"><span data-stu-id="198e4-122">(Almost any sort of cmdlet that is capable of retrieving information can process command-line input.) For more information about approved cmdlet verbs, see [Cmdlet Verb Names](./approved-verbs-for-windows-powershell-commands.md).</span></span>

<span data-ttu-id="198e4-123">A Get-Proc parancsmag definícióját a következő:</span><span class="sxs-lookup"><span data-stu-id="198e4-123">The following is the definition for this Get-Proc cmdlet.</span></span> <span data-ttu-id="198e4-124">Ez a definíció részleteit [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="198e4-124">Details of this definition are given in [Creating Your First Cmdlet](./creating-a-cmdlet-without-parameters.md).</span></span>

```csharp
[Cmdlet(VerbsCommon.Get, "proc")]
public class GetProcCommand: Cmdlet
```

```vb
<Cmdlet(VerbsCommon.Get, "Proc")> _
Public Class GetProcCommand
    Inherits Cmdlet
```

## <a name="defining-parameters"></a><span data-ttu-id="198e4-125">Paraméterek megadása</span><span class="sxs-lookup"><span data-stu-id="198e4-125">Defining Parameters</span></span>

<span data-ttu-id="198e4-126">Ha szükséges, a parancsmag meg kell határoznia a feldolgozása a bemeneti paraméterek.</span><span class="sxs-lookup"><span data-stu-id="198e4-126">If necessary, your cmdlet must define parameters for processing input.</span></span> <span data-ttu-id="198e4-127">Meghatározza a Get-Proc parancsmag egy `Name` paraméter leírtak szerint [a folyamat parancssori bemenet-paramétereket adunk hozzá](./adding-parameters-that-process-command-line-input.md).</span><span class="sxs-lookup"><span data-stu-id="198e4-127">This Get-Proc cmdlet defines a `Name` parameter as described in [Adding Parameters that Process Command-Line Input](./adding-parameters-that-process-command-line-input.md).</span></span>

<span data-ttu-id="198e4-128">Íme a paraméterdeklarációhoz a a `Name` paramétert a Get-Proc parancsmag.</span><span class="sxs-lookup"><span data-stu-id="198e4-128">Here is the parameter declaration for the `Name` parameter of this Get-Proc cmdlet.</span></span>

```csharp
[Parameter(
           Position = 0,
           ValueFromPipeline = true,
           ValueFromPipelineByPropertyName = true
)]
[ValidateNotNullOrEmpty]
public string[] Name
{
  get { return processNames; }
  set { processNames = value; }
}
private string[] processNames;
```

```vb
<Parameter(Position:=0, ValueFromPipeline:=True, _
ValueFromPipelineByPropertyName:=True), ValidateNotNullOrEmpty()> _
Public Property Name() As String()
    Get
        Return processNames
    End Get

    Set(ByVal value As String())
        processNames = value
    End Set

End Property
```

## <a name="overriding-input-processing-methods"></a><span data-ttu-id="198e4-129">Bemeneti feldolgozási módszerek felülbírálása</span><span class="sxs-lookup"><span data-stu-id="198e4-129">Overriding Input Processing Methods</span></span>

<span data-ttu-id="198e4-130">Minden parancsmag felül kell írnia a bemeneti feldolgozási által biztosított módszerek közül legalább az [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) osztály.</span><span class="sxs-lookup"><span data-stu-id="198e4-130">All cmdlets must override at least one of the input processing methods provided by the [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) class.</span></span> <span data-ttu-id="198e4-131">Ezek a metódusok tárgyalja [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="198e4-131">These methods are discussed in [Creating Your First Cmdlet](./creating-a-cmdlet-without-parameters.md).</span></span>

> [!NOTE]
> <span data-ttu-id="198e4-132">A parancsmag minden rekord lehető egymástól függetlenül kell kezelni.</span><span class="sxs-lookup"><span data-stu-id="198e4-132">Your cmdlet should handle each record as independently as possible.</span></span>

<span data-ttu-id="198e4-133">A Get-Proc parancsmag felülbírálja a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust a `Name` paramétere a felhasználó vagy egy parancsfájl által megadott bemenetet.</span><span class="sxs-lookup"><span data-stu-id="198e4-133">This Get-Proc cmdlet overrides the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method to handle the `Name` parameter for input provided by the user or a script.</span></span> <span data-ttu-id="198e4-134">Ez a módszer a folyamatok minden kért Folyamatnév vagy az összes folyamat fog kapni, ha nincs név megadva.</span><span class="sxs-lookup"><span data-stu-id="198e4-134">This method will get the processes for each requested process name or all processes if no name is provided.</span></span> <span data-ttu-id="198e4-135">Ez a felülbírálás részleteit [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="198e4-135">Details of this override are given in [Creating Your First Cmdlet](./creating-a-cmdlet-without-parameters.md).</span></span>

#### <a name="things-to-remember-when-reporting-errors"></a><span data-ttu-id="198e4-136">Megjegyzendő tudnivalók jelentése hiba esetén</span><span class="sxs-lookup"><span data-stu-id="198e4-136">Things to Remember When Reporting Errors</span></span>

<span data-ttu-id="198e4-137">A [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektumot, hogy a parancsmag továbbítja, ha maga kivétel hiba írása szükséges.</span><span class="sxs-lookup"><span data-stu-id="198e4-137">The [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) object that the cmdlet passes when writing an error requires an exception at its core.</span></span> <span data-ttu-id="198e4-138">Kövesse a .NET használata a kivétel meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="198e4-138">Follow the .NET guidelines when determining the exception to use.</span></span> <span data-ttu-id="198e4-139">Alapvetően Ha a hiba szemantikailag ugyanaz, mint a meglévő kivételt, a parancsmag kell használni vagy származtassa. a kivétel.</span><span class="sxs-lookup"><span data-stu-id="198e4-139">Basically, if the error is semantically the same as an existing exception, the cmdlet should use or derive from that exception.</span></span> <span data-ttu-id="198e4-140">Ellenkező esetben a kell származtatni egy új kivétel vagy közvetlenül a kivétel hierarchia a [System.Exception](/dotnet/api/System.Exception) osztály.</span><span class="sxs-lookup"><span data-stu-id="198e4-140">Otherwise, it should derive a new exception or exception hierarchy directly from the [System.Exception](/dotnet/api/System.Exception) class.</span></span>

<span data-ttu-id="198e4-141">(FullyQualifiedErrorId osztály tulajdonságához tartozó a ErrorRecord keresztül érhetők el) hiba azonosítók létrehozása során vegye figyelembe a következőket.</span><span class="sxs-lookup"><span data-stu-id="198e4-141">When creating error identifiers (accessed through the FullyQualifiedErrorId property of the ErrorRecord class) keep the following in mind.</span></span>

- <span data-ttu-id="198e4-142">Megcélzott diagnosztikai céllal, hogy amikor a teljes azonosítót vizsgálatával megadhatja, hogy milyen a hiba van, és ahol a hiba érkezett karakterláncok használatát.</span><span class="sxs-lookup"><span data-stu-id="198e4-142">Use strings that are targeted for diagnostic purposes so that when inspecting the fully qualified identifier you can determine what the error is and where the error came from.</span></span>

- <span data-ttu-id="198e4-143">Egy megfelelően formázott abszolút hiba azonosítója a következő lehet.</span><span class="sxs-lookup"><span data-stu-id="198e4-143">A well formed fully qualified error identifier might be as follows.</span></span>

`CommandNotFoundException,Micrososft.PowerShell.Commands.GetCommanddCommand.`

<span data-ttu-id="198e4-144">Figyelje meg, hogy az előző példában a hiba azonosítója (az első token) jelöl ki a hibát, és a fennmaradó rész azt jelzi, hogy a hiba, honnan származnak.</span><span class="sxs-lookup"><span data-stu-id="198e4-144">Notice that in the previous example, the error identifier (the first token) designates what the error is and the remaining part indicates where the error came from.</span></span>

- <span data-ttu-id="198e4-145">Az összetettebb esetekhez ponttal elválasztott jogkivonat, amely képes elemezni az ellenőrzési hiba azonosítója lehet.</span><span class="sxs-lookup"><span data-stu-id="198e4-145">For more complex scenarios, the error identifier can be a dot separated token that can be parsed on inspection.</span></span> <span data-ttu-id="198e4-146">Ez lehetővé teszi, hogy hiba azonosítóját, valamint az azonosítóját, valamint a hiba hibakategória részeit túl ágban.</span><span class="sxs-lookup"><span data-stu-id="198e4-146">This allows you too branch on the parts of the error identifier as well as the error identifier and error category.</span></span>

<span data-ttu-id="198e4-147">A parancsmag adott hiba általános jelentését azonosítók kell rendelni különböző kódhoz tartozó elérési út.</span><span class="sxs-lookup"><span data-stu-id="198e4-147">The cmdlet should assign specific error identifiers to different code paths.</span></span> <span data-ttu-id="198e4-148">Hozzárendelés hiba azonosítók szem előtt tartani a következő információkat:</span><span class="sxs-lookup"><span data-stu-id="198e4-148">Keep the following information in mind for assignment of error identifiers:</span></span>

- <span data-ttu-id="198e4-149">Hiba azonosítója a parancsmag életciklusa során állandó kell maradnia.</span><span class="sxs-lookup"><span data-stu-id="198e4-149">An error identifier should remain constant throughout the cmdlet life cycle.</span></span> <span data-ttu-id="198e4-150">Ne módosítsa a parancsmag-verziók közötti hiba azonosítója szemantikáját.</span><span class="sxs-lookup"><span data-stu-id="198e4-150">Do not change the semantics of an error identifier between cmdlet versions.</span></span>

- <span data-ttu-id="198e4-151">Egy hiba azonosító, termékről a jelentett hiba szövege használja.</span><span class="sxs-lookup"><span data-stu-id="198e4-151">Use text for an error identifier that tersely corresponds to the error being reported.</span></span> <span data-ttu-id="198e4-152">Ne használjon szóközöket vagy absztrakt.</span><span class="sxs-lookup"><span data-stu-id="198e4-152">Do not use white space or punctuation.</span></span>

- <span data-ttu-id="198e4-153">A parancsmag csak az olyan hiba azonosítók, amelyek reprodukálható készítése rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="198e4-153">Have your cmdlet generate only error identifiers that are reproducible.</span></span> <span data-ttu-id="198e4-154">Ez például nem hozhat létre egy azonosítót, amely egy folyamat azonosítóját tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="198e4-154">For example, it should not generate an identifier that includes a process identifier.</span></span> <span data-ttu-id="198e4-155">Hiba azonosítók hasznosak a felhasználó, csak akkor, ha azok megegyeznek-azonosítók, amelyeket más azonos problémát tapasztalt felhasználók által is látható.</span><span class="sxs-lookup"><span data-stu-id="198e4-155">Error identifiers are useful to a user only when they correspond to identifiers that are seen by other users experiencing the same problem.</span></span>

<span data-ttu-id="198e4-156">Nem kezelt kivételek nem észlelt Windows PowerShell a következő feltételek esetében alkalmazhatja:</span><span class="sxs-lookup"><span data-stu-id="198e4-156">Unhandled exceptions are not caught by Windows PowerShell in the following conditions:</span></span>

- <span data-ttu-id="198e4-157">Parancsmag hoz létre egy új hozzászóláslánc és futó abban, hogy a szál nem kezelt kivételt jelez, ha a Windows PowerShell nem képes a hibát, és a folyamat leáll.</span><span class="sxs-lookup"><span data-stu-id="198e4-157">If a cmdlet creates a new thread and code running in that thread throws an unhandled exception, Windows PowerShell will not catch the error and will terminate the process.</span></span>

- <span data-ttu-id="198e4-158">Ha egy objektum nem kezelt kivételt okozó kód destruktoru vagy Dispose függvényhez módszereket, a Windows PowerShell nem képes a hibát, és a folyamat leáll.</span><span class="sxs-lookup"><span data-stu-id="198e4-158">If an object has code in its destructor or Dispose methods that causes an unhandled exception, Windows PowerShell will not catch the error and will terminate the process.</span></span>

## <a name="reporting-nonterminating-errors"></a><span data-ttu-id="198e4-159">Nonterminating hibát jelentett</span><span class="sxs-lookup"><span data-stu-id="198e4-159">Reporting Nonterminating Errors</span></span>

<span data-ttu-id="198e4-160">A bemeneti feldolgozási módszerek közül is tud jelentéseket nonterminating hiba a kimeneti adatfolyamhoz a a [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) metódust.</span><span class="sxs-lookup"><span data-stu-id="198e4-160">Any one of the input processing methods can report a nonterminating error to the output stream using the [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) method.</span></span> <span data-ttu-id="198e4-161">Íme egy példa a Get-Proc parancsmag, amely bemutatja a hívást a [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) a felülbírálását belül a [ System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust.</span><span class="sxs-lookup"><span data-stu-id="198e4-161">Here is a code example from this Get-Proc cmdlet that illustrates the call to [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) from within the override of the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method.</span></span> <span data-ttu-id="198e4-162">Ebben az esetben a rendszer hívást kezdeményez, ha a parancsmag egy folyamatot egy adott folyamat azonosítója nem található.</span><span class="sxs-lookup"><span data-stu-id="198e4-162">In this case, the call is made if the cmdlet cannot find a process for a specified process identifier.</span></span>

```csharp
protected override void ProcessRecord()
{
  // If no name parameter passed to cmdlet, get all processes.
  if (processNames == null)
  {
    WriteObject(Process.GetProcesses(), true);
  }
    else
    {
      // If a name parameter is passed to cmdlet, get and write
      // the associated processes.
      // Write a nonterminating error for failure to retrieve
      // a process.
      foreach (string name in processNames)
      {
        Process[] processes;

        try
        {
          processes = Process.GetProcessesByName(name);
        }
        catch (InvalidOperationException ex)
        {
          WriteError(new ErrorRecord(
                     ex,
                     "NameNotFound",
                     ErrorCategory.InvalidOperation,
                     name));
          continue;
        }

        WriteObject(processes, true);
      } // foreach (...
    } // else
  }
```

#### <a name="things-to-remember-about-writing-nonterminating-errors"></a><span data-ttu-id="198e4-163">Megjegyzendő tudnivalók Nonterminating hibák írása</span><span class="sxs-lookup"><span data-stu-id="198e4-163">Things to Remember About Writing Nonterminating Errors</span></span>

<span data-ttu-id="198e4-164">Nonterminating hiba esetén a parancsmag kell létrehoznia egy adott hiba minden egyes megadott bemeneti objektum azonosítója.</span><span class="sxs-lookup"><span data-stu-id="198e4-164">For a nonterminating error, the cmdlet must generate a specific error identifier for each specific input object.</span></span>

<span data-ttu-id="198e4-165">A parancsmag gyakran van szükség, a Windows PowerShell-művelet nonterminating hiba által előállított módosításához.</span><span class="sxs-lookup"><span data-stu-id="198e4-165">A cmdlet frequently needs to modify the Windows PowerShell action produced by a nonterminating error.</span></span> <span data-ttu-id="198e4-166">Ez ehhez meghatározása a `ErrorAction` és `ErrorVariable` paramétereket.</span><span class="sxs-lookup"><span data-stu-id="198e4-166">It can do this by defining the `ErrorAction` and `ErrorVariable` parameters.</span></span> <span data-ttu-id="198e4-167">Ha az határozza meg a `ErrorAction` paramétert, a parancsmag megjeleníti a felhasználói beállítások [System.Management.Automation.Actionpreference](/dotnet/api/system.management.automation.actionpreference), beállításával közvetlenül is befolyásolhatja a művelet a `$ErrorActionPreference` változó.</span><span class="sxs-lookup"><span data-stu-id="198e4-167">If defining the `ErrorAction` parameter, the cmdlet presents the user options [System.Management.Automation.Actionpreference](/dotnet/api/system.management.automation.actionpreference), you can also directly influence the action by setting the `$ErrorActionPreference` variable.</span></span>

<span data-ttu-id="198e4-168">A parancsmag nonterminating hibák mentheti egy változó használatával a `ErrorVariable` paramétert, amely nem befolyásolja a beállítását `ErrorAction`.</span><span class="sxs-lookup"><span data-stu-id="198e4-168">The cmdlet can save nonterminating errors to a variable using the `ErrorVariable` parameter, which is not affected by the setting of `ErrorAction`.</span></span> <span data-ttu-id="198e4-169">Hibák fűzhető egy létező hiba változó plusz jelre (+) hozzáadásával az előtérben, a változó nevét.</span><span class="sxs-lookup"><span data-stu-id="198e4-169">Failures can be appended to an existing error variable by adding a plus sign (+) to the front of the variable name.</span></span>

## <a name="code-sample"></a><span data-ttu-id="198e4-170">Kódminta</span><span class="sxs-lookup"><span data-stu-id="198e4-170">Code Sample</span></span>

<span data-ttu-id="198e4-171">A teljes C# mintakód, lásd: [GetProcessSample04 minta](./getprocesssample04-sample.md).</span><span class="sxs-lookup"><span data-stu-id="198e4-171">For the complete C# sample code, see [GetProcessSample04 Sample](./getprocesssample04-sample.md).</span></span>

## <a name="define-object-types-and-formatting"></a><span data-ttu-id="198e4-172">Objektumtípusok és formázása</span><span class="sxs-lookup"><span data-stu-id="198e4-172">Define Object Types and Formatting</span></span>

<span data-ttu-id="198e4-173">Windows PowerShell parancsmagok használatával a .NET-objektumokká közötti továbbítja.</span><span class="sxs-lookup"><span data-stu-id="198e4-173">Windows PowerShell passes information between cmdlets using .NET objects.</span></span> <span data-ttu-id="198e4-174">Ennek következtében a parancsmag előfordulhat, hogy meg kell határoznia a saját típusát, vagy a parancsmag előfordulhat, hogy ki kell terjesztenie egy másik parancsmag által biztosított meglévő típus.</span><span class="sxs-lookup"><span data-stu-id="198e4-174">Consequently, a cmdlet might need to define its own type, or the cmdlet might need to extend an existing type provided by another cmdlet.</span></span> <span data-ttu-id="198e4-175">Új típusok meghatározása, vagy meglévő típusok bővítésével kapcsolatos további információkért lásd: [objektumtípusok kiterjesztése és formázás](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).</span><span class="sxs-lookup"><span data-stu-id="198e4-175">For more information about defining new types or extending existing types, see [Extending Object Types and Formatting](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).</span></span>

## <a name="building-the-cmdlet"></a><span data-ttu-id="198e4-176">A parancsmag készítése</span><span class="sxs-lookup"><span data-stu-id="198e4-176">Building the Cmdlet</span></span>

<span data-ttu-id="198e4-177">Parancsmag-k megvalósítása után regisztrálnia kell azt a Windows PowerShell-lel a Windows PowerShell beépülő modullal.</span><span class="sxs-lookup"><span data-stu-id="198e4-177">After implementing a cmdlet, you must register it with Windows PowerShell through a Windows PowerShell snap-in.</span></span> <span data-ttu-id="198e4-178">Parancsmagok regisztrálásával kapcsolatos további információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).</span><span class="sxs-lookup"><span data-stu-id="198e4-178">For more information about registering cmdlets, see [How to Register Cmdlets, Providers, and Host Applications](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).</span></span>

## <a name="testing-the-cmdlet"></a><span data-ttu-id="198e4-179">A parancsmag tesztelése</span><span class="sxs-lookup"><span data-stu-id="198e4-179">Testing the Cmdlet</span></span>

<span data-ttu-id="198e4-180">Ha a parancsmagot a Windows PowerShell-lel regisztrálva lett, azt a parancssorból való futtatásával tesztelheti.</span><span class="sxs-lookup"><span data-stu-id="198e4-180">When your cmdlet has been registered with Windows PowerShell, you can test it by running it on the command line.</span></span> <span data-ttu-id="198e4-181">Most tesztelheti a minta Get-Proc parancsmaggal ellenőrizheti, hogy hibát jelez:</span><span class="sxs-lookup"><span data-stu-id="198e4-181">Let's test the sample Get-Proc cmdlet to see whether it reports an error:</span></span>

- <span data-ttu-id="198e4-182">Indítsa el a Windows Powershellt, és a Get-Proc parancsmag használatával lekérheti az a "Teszt" nevű folyamatokat.</span><span class="sxs-lookup"><span data-stu-id="198e4-182">Start Windows PowerShell, and use the Get-Proc cmdlet to retrieve the processes named "TEST".</span></span>

    ```powershell
    PS> get-proc -name test
    ```

<span data-ttu-id="198e4-183">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="198e4-183">The following output appears.</span></span>

    ```
    get-proc : Operation is not valid due to the current state of the object.
    At line:1 char:9
    + get-proc  <<<< -name test
    ```

## <a name="see-also"></a><span data-ttu-id="198e4-184">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="198e4-184">See Also</span></span>

[<span data-ttu-id="198e4-185">Folyamat folyamat bemeneti paraméterek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="198e4-185">Adding Parameters that Process Pipeline Input</span></span>](./adding-parameters-that-process-pipeline-input.md)

[<span data-ttu-id="198e4-186">Parancssori bemenet feldolgozása paraméterek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="198e4-186">Adding Parameters that Process Command-Line Input</span></span>](./adding-parameters-that-process-command-line-input.md)

[<span data-ttu-id="198e4-187">Az első parancsmag létrehozása</span><span class="sxs-lookup"><span data-stu-id="198e4-187">Creating Your First Cmdlet</span></span>](./creating-a-cmdlet-without-parameters.md)

[<span data-ttu-id="198e4-188">Objektumtípusok kiterjesztése és formázása</span><span class="sxs-lookup"><span data-stu-id="198e4-188">Extending Object Types and Formatting</span></span>](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[<span data-ttu-id="198e4-189">How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez</span><span class="sxs-lookup"><span data-stu-id="198e4-189">How to Register Cmdlets, Providers, and Host Applications</span></span>](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[<span data-ttu-id="198e4-190">Windows PowerShell-referencia</span><span class="sxs-lookup"><span data-stu-id="198e4-190">Windows PowerShell Reference</span></span>](../windows-powershell-reference.md)

[<span data-ttu-id="198e4-191">Parancsmag-minták</span><span class="sxs-lookup"><span data-stu-id="198e4-191">Cmdlet Samples</span></span>](./cmdlet-samples.md)
