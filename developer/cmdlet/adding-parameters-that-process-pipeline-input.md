---
title: Adatcsatorna bemenetének feldolgozott-paramétereket adunk hozzá |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cmdlets [PowerShell Programmer's Guide], pipeline input
- parameters [PowerShell Programmer's Guide], pipeline input
ms.assetid: 09bf70a9-7c76-4ffe-b3f0-a1d5f10a0931
caps.latest.revision: 8
ms.openlocfilehash: 34643d20c16f8cc45e7fb20dc2a87d78b18bbf10
ms.sourcegitcommit: f60fa420bdc81db174e6168d3aeb11371e483162
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/20/2019
ms.locfileid: "67298629"
---
# <a name="adding-parameters-that-process-pipeline-input"></a><span data-ttu-id="85638-102">Láncbemenetet feldolgozó paraméterek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="85638-102">Adding Parameters that Process Pipeline Input</span></span>

<span data-ttu-id="85638-103">A parancsmag bemenete egy forrása az objektumot, a folyamat, amely egy felsőbb rétegbeli parancsmag származik.</span><span class="sxs-lookup"><span data-stu-id="85638-103">One source of input for a cmdlet is an object on the pipeline that originates from an upstream cmdlet.</span></span> <span data-ttu-id="85638-104">Ez a szakasz ismerteti, hogyan lehet egy paraméter hozzáadása a Get-Proc parancsmag (ismertetett [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md)), hogy a parancsmag folyamat objektumot tud feldolgozni.</span><span class="sxs-lookup"><span data-stu-id="85638-104">This section describes how to add a parameter to the Get-Proc cmdlet (described in [Creating Your First Cmdlet](./creating-a-cmdlet-without-parameters.md)) so that the cmdlet can process pipeline objects.</span></span>

<span data-ttu-id="85638-105">A Get-Proc parancsmagot használja egy `Name` paraméter, amely egy folyamat objektumot a bemenetet elfogadja folyamat adatait kérdezi le a helyi számítógép megadott neve alapján, és ezután megjeleníti a folyamatok adatait a parancssorban.</span><span class="sxs-lookup"><span data-stu-id="85638-105">This Get-Proc cmdlet uses a `Name` parameter that accepts input from a pipeline object, retrieves process information from the local computer based on the supplied names, and then displays information about the processes at the command line.</span></span>

## <a name="defining-the-cmdlet-class"></a><span data-ttu-id="85638-106">A parancsmag osztály meghatározása</span><span class="sxs-lookup"><span data-stu-id="85638-106">Defining the Cmdlet Class</span></span>

<span data-ttu-id="85638-107">Mindig a parancsmag elnevezési és a .NET-osztály, amely megvalósítja a parancsmag deklaráló parancsmag létrehozásának első lépése.</span><span class="sxs-lookup"><span data-stu-id="85638-107">The first step in cmdlet creation is always naming the cmdlet and declaring the .NET class that implements the cmdlet.</span></span> <span data-ttu-id="85638-108">Ez a parancsmag folyamat adatait, kérdezi le, így az itt választott művelet neve "Get".</span><span class="sxs-lookup"><span data-stu-id="85638-108">This cmdlet retrieves process information, so the verb name chosen here is "Get".</span></span> <span data-ttu-id="85638-109">(A szinte bármilyen rendezési parancsmag, amely képes adatok beolvasása a parancssori bemenet tud feldolgozni.) A parancsmag jóváhagyott igék kapcsolatos további információkért lásd: [művelet neve](./approved-verbs-for-windows-powershell-commands.md).</span><span class="sxs-lookup"><span data-stu-id="85638-109">(Almost any sort of cmdlet that is capable of retrieving information can process command-line input.) For more information about approved cmdlet verbs, see [Cmdlet Verb Names](./approved-verbs-for-windows-powershell-commands.md).</span></span>

<span data-ttu-id="85638-110">A Get-Proc parancsmag definícióját a következő:</span><span class="sxs-lookup"><span data-stu-id="85638-110">The following is the definition for this Get-Proc cmdlet.</span></span> <span data-ttu-id="85638-111">Ez a definíció részleteit [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="85638-111">Details of this definition are given in [Creating Your First Cmdlet](./creating-a-cmdlet-without-parameters.md).</span></span>

```csharp
[Cmdlet(VerbsCommon.Get, "proc")]
public class GetProcCommand : Cmdlet
```

```vb
<Cmdlet(VerbsCommon.Get, "Proc")> _
Public Class GetProcCommand
    Inherits Cmdlet
```

## <a name="defining-input-from-the-pipeline"></a><span data-ttu-id="85638-112">A bemenetet a folyamat meghatározása</span><span class="sxs-lookup"><span data-stu-id="85638-112">Defining Input from the Pipeline</span></span>

<span data-ttu-id="85638-113">Ez a szakasz ismerteti, hogyan adhat meg a folyamat a parancsmag a bemenetet.</span><span class="sxs-lookup"><span data-stu-id="85638-113">This section describes how to define input from the pipeline for a cmdlet.</span></span> <span data-ttu-id="85638-114">A Get-Proc parancsmag képviselő tulajdonság határozza meg a `Name` paraméter leírtak szerint [a folyamat parancssori bemenet-paramétereket adunk hozzá](./adding-parameters-that-process-command-line-input.md).</span><span class="sxs-lookup"><span data-stu-id="85638-114">This Get-Proc cmdlet defines a property that represents the `Name` parameter as described in [Adding Parameters that Process Command Line Input](./adding-parameters-that-process-command-line-input.md).</span></span> <span data-ttu-id="85638-115">(Lásd a paraméterek deklaráló kapcsolatos általános információkat szakasza.)</span><span class="sxs-lookup"><span data-stu-id="85638-115">(See that topic for general information about declaring parameters.)</span></span>

<span data-ttu-id="85638-116">Azonban parancsmag kell feldolgoznia az adatcsatorna bemenetének, amikor kell legyen kötve a Windows PowerShell-modul által bemeneti értékek paramétereit.</span><span class="sxs-lookup"><span data-stu-id="85638-116">However, when a cmdlet needs to process pipeline input, it must have its parameters bound to input values by the Windows PowerShell runtime.</span></span> <span data-ttu-id="85638-117">Ehhez hozzá kell adnia a `ValueFromPipeline` kulcsszó, vagy adja hozzá a `ValueFromPipelineByProperty` kulcsszó használatával a [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) deklarace attribútum.</span><span class="sxs-lookup"><span data-stu-id="85638-117">To do this, you must add the `ValueFromPipeline` keyword or add the `ValueFromPipelineByProperty` keyword to the [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) attribute declaration.</span></span> <span data-ttu-id="85638-118">Adja meg a `ValueFromPipeline` kulcsszót, ha a parancsmag fér hozzá a teljes bemeneti objektum.</span><span class="sxs-lookup"><span data-stu-id="85638-118">Specify the `ValueFromPipeline` keyword if the cmdlet accesses the complete input object.</span></span> <span data-ttu-id="85638-119">Adja meg a `ValueFromPipelineByProperty` Ha a parancsmag csak az objektum osztályát fér hozzá.</span><span class="sxs-lookup"><span data-stu-id="85638-119">Specify the `ValueFromPipelineByProperty` if the cmdlet accesses only a property of the object.</span></span>

<span data-ttu-id="85638-120">Íme a paraméterdeklarációhoz a a `Name` a Get-Proc parancsmag, amely elfogadja a folyamat bemeneti paraméter.</span><span class="sxs-lookup"><span data-stu-id="85638-120">Here is the parameter declaration for the `Name` parameter of this Get-Proc cmdlet that accepts pipeline input.</span></span>

[!code-csharp[GetProcessSample03.cs](../../powershell-sdk-samples/SDK-2.0/csharp/GetProcessSample03/GetProcessSample03.cs#L35-L44 "GetProcessSample03.cs")]

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

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplesgetproc03#GetProc03VBNameParameter](Msh_samplesgetproc03#GetProc03VBNameParameter)]  -->

<span data-ttu-id="85638-121">Az előző deklarace készleteket a `ValueFromPipeline` kulcsszó használatával `true` úgy, hogy a Windows PowerShell-modul fog kötődni a paraméter a bejövő objektum, ha az objektum ugyanolyan típusú, mint a paramétert, vagy ha az azonos típusú is kényszeríthető.</span><span class="sxs-lookup"><span data-stu-id="85638-121">The previous declaration sets the `ValueFromPipeline` keyword to `true` so that the Windows PowerShell runtime will bind the parameter to the incoming object if the object is the same type as the parameter, or if it can be coerced to the same type.</span></span> <span data-ttu-id="85638-122">A `ValueFromPipelineByPropertyName` kulcsszó is értékre van állítva `true` úgy, hogy a Windows PowerShell-modul ellenőrzi a bejövő objektumot egy `Name` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="85638-122">The `ValueFromPipelineByPropertyName` keyword is also set to `true` so that the Windows PowerShell runtime will check the incoming object for a `Name` property.</span></span> <span data-ttu-id="85638-123">A bejövő objektumnak a tulajdonságot, ha a futtatókörnyezet köti a `Name` paramétert a `Name` bejövő objektum tulajdonságának.</span><span class="sxs-lookup"><span data-stu-id="85638-123">If the incoming object has such a property, the runtime will bind the `Name` parameter to the `Name` property of the incoming object.</span></span>

> [!NOTE]
> <span data-ttu-id="85638-124">A beállítást, a `ValueFromPipeline` kulcsszó attribútum esetében egy paraméter elsőbbséget élvez a beállítása a `ValueFromPipelineByPropertyName` kulcsszót.</span><span class="sxs-lookup"><span data-stu-id="85638-124">The setting of the `ValueFromPipeline` attribute keyword for a parameter takes precedence over the setting for the `ValueFromPipelineByPropertyName` keyword.</span></span>

## <a name="overriding-an-input-processing-method"></a><span data-ttu-id="85638-125">Egy bemeneti metódus feldolgozási felülbírálása</span><span class="sxs-lookup"><span data-stu-id="85638-125">Overriding an Input Processing Method</span></span>

<span data-ttu-id="85638-126">Ha a parancsmagot, a folyamat bemeneti kezelni, kell a megfelelő bemenet feldolgozása metódusok felülbírálása.</span><span class="sxs-lookup"><span data-stu-id="85638-126">If your cmdlet is to handle pipeline input, it needs to override the appropriate input processing methods.</span></span> <span data-ttu-id="85638-127">Az alapszintű bemeneti feldolgozási módszerek jelennek meg a [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="85638-127">The basic input processing methods are introduced in [Creating Your First Cmdlet](./creating-a-cmdlet-without-parameters.md).</span></span>

<span data-ttu-id="85638-128">A Get-Proc parancsmag felülbírálja a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust a `Name` paraméter megadott információ a felhasználó vagy egy parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="85638-128">This Get-Proc cmdlet overrides the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method to handle the `Name` parameter input provided by the user or a script.</span></span> <span data-ttu-id="85638-129">Ez a módszer a folyamatok minden kért Folyamatnév vagy az összes folyamat fog kapni, ha nincs név megadva.</span><span class="sxs-lookup"><span data-stu-id="85638-129">This method will get the processes for each requested process name or all processes if no name is provided.</span></span> <span data-ttu-id="85638-130">Figyelje meg, hogy belül [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord), a hívást [WriteObject(System.Object,System.Boolean)](/dotnet/api/system.management.automation.cmdlet.writeobject?view=pscore-6.2.0#System_Management_Automation_Cmdlet_WriteObject_System_Object_System_Boolean_) az kimeneti objektumok küld kimeneti mechanizmusa a folyamat.</span><span class="sxs-lookup"><span data-stu-id="85638-130">Notice that within [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord), the call to [WriteObject(System.Object,System.Boolean)](/dotnet/api/system.management.automation.cmdlet.writeobject?view=pscore-6.2.0#System_Management_Automation_Cmdlet_WriteObject_System_Object_System_Boolean_) is the output mechanism for sending output objects to the pipeline.</span></span> <span data-ttu-id="85638-131">A második paraméter a hívás `enumerateCollection`, értékre van állítva `true` állapítható meg, hogy a Windows PowerShell modul enumerálása folyamat objektumok tömbje, és a egy folyamat egyszerre írni a parancssorból.</span><span class="sxs-lookup"><span data-stu-id="85638-131">The second parameter of this call, `enumerateCollection`, is set to `true` to tell the Windows PowerShell runtime to enumerate the array of process objects, and write one process at a time to the command line.</span></span>

```csharp
protected override void ProcessRecord()
{
  // If no process names are passed to the cmdlet, get all processes.
  if (processNames == null)
  {
      // Write the processes to the pipeline making them available
      // to the next cmdlet. The second argument of this call tells
      // PowerShell to enumerate the array, and send one process at a
      // time to the pipeline.
      WriteObject(Process.GetProcesses(), true);
  }
  else
  {
    // If process names are passed to the cmdlet, get and write
    // the associated processes.
    foreach (string name in processNames)
    {
      WriteObject(Process.GetProcessesByName(name), true);
    } // End foreach (string name...).
  }
}
```

```vb
Protected Overrides Sub ProcessRecord()
    Dim processes As Process()

    '/ If no process names are passed to the cmdlet, get all processes.
    If processNames Is Nothing Then
        processes = Process.GetProcesses()
    Else

        '/ If process names are specified, write the processes to the
        '/ pipeline to display them or make them available to the next cmdlet.
        For Each name As String In processNames
            '/ The second parameter of this call tells PowerShell to enumerate the
            '/ array, and send one process at a time to the pipeline.
            WriteObject(Process.GetProcessesByName(name), True)
        Next
    End If

End Sub 'ProcessRecord
```

## <a name="code-sample"></a><span data-ttu-id="85638-132">Kódminta</span><span class="sxs-lookup"><span data-stu-id="85638-132">Code Sample</span></span>

<span data-ttu-id="85638-133">A teljes C# mintakód, lásd: [GetProcessSample03 minta](./getprocesssample03-sample.md).</span><span class="sxs-lookup"><span data-stu-id="85638-133">For the complete C# sample code, see [GetProcessSample03 Sample](./getprocesssample03-sample.md).</span></span>

## <a name="defining-object-types-and-formatting"></a><span data-ttu-id="85638-134">Objektumtípusok definiálása és formázása</span><span class="sxs-lookup"><span data-stu-id="85638-134">Defining Object Types and Formatting</span></span>

<span data-ttu-id="85638-135">Windows PowerShell parancsmagok használatával a .net-objektumokká közötti továbbítja.</span><span class="sxs-lookup"><span data-stu-id="85638-135">Windows PowerShell passes information between cmdlets using .Net objects.</span></span> <span data-ttu-id="85638-136">Ennek következtében a parancsmag előfordulhat, hogy meg kell határoznia a saját típusát, vagy a parancsmag előfordulhat, hogy ki kell terjesztenie egy másik parancsmag által biztosított meglévő típus.</span><span class="sxs-lookup"><span data-stu-id="85638-136">Consequently, a cmdlet may need to define its own type, or the cmdlet may need to extend an existing type provided by another cmdlet.</span></span> <span data-ttu-id="85638-137">Új típusok meghatározása, vagy meglévő típusok bővítésével kapcsolatos további információkért lásd: [objektumtípusok kiterjesztése és formázás](/previous-versions//ms714665(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="85638-137">For more information about defining new types or extending existing types, see [Extending Object Types and Formatting](/previous-versions//ms714665(v=vs.85)).</span></span>

## <a name="building-the-cmdlet"></a><span data-ttu-id="85638-138">A parancsmag készítése</span><span class="sxs-lookup"><span data-stu-id="85638-138">Building the Cmdlet</span></span>

<span data-ttu-id="85638-139">A parancsmag megvalósítása után regisztrálni kell a Windows PowerShell-lel a Windows PowerShell beépülő modullal.</span><span class="sxs-lookup"><span data-stu-id="85638-139">After implementing a cmdlet it must be registered with Windows PowerShell through a Windows PowerShell snap-in.</span></span> <span data-ttu-id="85638-140">Parancsmagok regisztrálásával kapcsolatos további információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](/previous-versions//ms714644(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="85638-140">For more information about registering cmdlets, see [How to Register Cmdlets, Providers, and Host Applications](/previous-versions//ms714644(v=vs.85)).</span></span>

## <a name="testing-the-cmdlet"></a><span data-ttu-id="85638-141">A parancsmag tesztelése</span><span class="sxs-lookup"><span data-stu-id="85638-141">Testing the Cmdlet</span></span>

<span data-ttu-id="85638-142">Ha a parancsmagot a Windows PowerShell-lel regisztrálva lett, tesztelje azt a parancssorból való futtatásával.</span><span class="sxs-lookup"><span data-stu-id="85638-142">When your cmdlet has been registered with Windows PowerShell, test it by running it on the command line.</span></span> <span data-ttu-id="85638-143">Például tesztelheti a kódját a minta parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="85638-143">For example, test the code for the sample cmdlet.</span></span> <span data-ttu-id="85638-144">A parancssorból-parancsmagokkal kapcsolatos további információkért lásd: a [első lépések a Windows PowerShell-lel](/powershell/scripting/getting-started/getting-started-with-windows-powershell).</span><span class="sxs-lookup"><span data-stu-id="85638-144">For more information about using cmdlets from the command line, see the [Getting Started with Windows PowerShell](/powershell/scripting/getting-started/getting-started-with-windows-powershell).</span></span>

- <span data-ttu-id="85638-145">A Windows PowerShell parancssorába a következő parancsokat a folyamat nevét a folyamat keretében lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="85638-145">At the Windows PowerShell prompt, enter the following commands to retrieve the process names through the pipeline.</span></span>

    ```powershell
    PS> type ProcessNames | get-proc
    ```

<span data-ttu-id="85638-146">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="85638-146">The following output appears.</span></span>

    ```
    Handles  NPM(K)  PM(K)   WS(K)  VS(M)  CPU(s)    Id  ProcessName
    -------  ------  -----   ----- -----   ------    --  -----------
        809      21  40856    4448    147    9.50  2288  iexplore
        737      21  26036   16348    144   22.03  3860  iexplore
         39       2   1024     388     30    0.08  3396  notepad
       3927      62  71836   26984    467  195.19  1848  OUTLOOK
    ```

- <span data-ttu-id="85638-147">Adja meg a következő sorokat a folyamat az objektumokat, amelyek rendelkeznek egy `Name` a folyamatok "IEXPLORE" nevű tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="85638-147">Enter the following lines to get the process objects that have a `Name` property from the processes called "IEXPLORE".</span></span> <span data-ttu-id="85638-148">Ez a példa a `Get-Process` parancsmag (a Windows PowerShell által biztosított), egy fölérendelt parancs használatával kérje le a "IEXPLORE" folyamatokat.</span><span class="sxs-lookup"><span data-stu-id="85638-148">This example uses the `Get-Process` cmdlet (provided by Windows PowerShell) as an upstream command to retrieve the "IEXPLORE" processes.</span></span>

    ```powershell
    PS> get-process iexplore | get-proc
    ```

<span data-ttu-id="85638-149">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="85638-149">The following output appears.</span></span>

    ```
    Handles  NPM(K)  PM(K)   WS(K)  VS(M)  CPU(s)    Id  ProcessName
    -------  ------  -----      ----- -----   ------     -- -----------
        801      21  40720    6544    142    9.52  2288  iexplore
        726      21  25872   16652    138   22.09  3860  iexplore
        801      21  40720    6544    142    9.52  2288  iexplore
        726      21  25872   16652    138   22.09  3860  iexplore
    ```

## <a name="see-also"></a><span data-ttu-id="85638-150">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="85638-150">See Also</span></span>

[<span data-ttu-id="85638-151">Parancssori bemenet feldolgozása paraméterek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="85638-151">Adding Parameters that Process Command Line Input</span></span>](./adding-parameters-that-process-command-line-input.md)

[<span data-ttu-id="85638-152">Az első parancsmag létrehozása</span><span class="sxs-lookup"><span data-stu-id="85638-152">Creating Your First Cmdlet</span></span>](./creating-a-cmdlet-without-parameters.md)

<span data-ttu-id="85638-153">[Objektumtípusok kiterjesztése és formázása](/previous-versions//ms714665(v=vs.85))</span><span class="sxs-lookup"><span data-stu-id="85638-153">[Extending Object Types and Formatting](/previous-versions//ms714665(v=vs.85))</span></span>

<span data-ttu-id="85638-154">[How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez](/previous-versions//ms714644(v=vs.85))</span><span class="sxs-lookup"><span data-stu-id="85638-154">[How to Register Cmdlets, Providers, and Host Applications](/previous-versions//ms714644(v=vs.85))</span></span>

[<span data-ttu-id="85638-155">Windows PowerShell-referencia</span><span class="sxs-lookup"><span data-stu-id="85638-155">Windows PowerShell Reference</span></span>](../windows-powershell-reference.md)

[<span data-ttu-id="85638-156">Parancsmag-minták</span><span class="sxs-lookup"><span data-stu-id="85638-156">Cmdlet Samples</span></span>](./cmdlet-samples.md)
