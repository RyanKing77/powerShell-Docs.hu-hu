---
title: Paraméter hozzáadása a parancsmag beállítja |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- parameter sets [PowerShell Programmer's Guide]
ms.assetid: a6131db4-fd6e-45f1-bd47-17e7174afd56
caps.latest.revision: 8
ms.openlocfilehash: b02a2e0d4b0a27c261b0bc05febda7826ad5276e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849097"
---
# <a name="adding-parameter-sets-to-a-cmdlet"></a><span data-ttu-id="02196-102">Paraméterkészletek hozzáadása parancsmagokhoz</span><span class="sxs-lookup"><span data-stu-id="02196-102">Adding Parameter Sets to a Cmdlet</span></span>

<span data-ttu-id="02196-103">Ez a szakasz ismerteti a Stop-Proc parancsmaghoz paraméterkészletek hozzáadása (ismertetett [létrehozása egy parancsmag, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md)).</span><span class="sxs-lookup"><span data-stu-id="02196-103">This section describes how to add parameter sets to the Stop-Proc cmdlet (described in [Creating a Cmdlet that Modifies the System](./creating-a-cmdlet-that-modifies-the-system.md)).</span></span> <span data-ttu-id="02196-104">Hasonló a Stop-Proc más parancsmagoknak a programozói útmutatóban leírt, ez a parancsmag megkísérli leállítani folyamatokat, amelyek a Get-Proc parancsmaggal olvassa be (ismertetett [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md)).</span><span class="sxs-lookup"><span data-stu-id="02196-104">Similar to the other Stop-Proc cmdlets described in this Programmer's Guide, this cmdlet attempts to stop processes that are retrieved using the Get-Proc cmdlet (described in [Creating Your First Cmdlet](./creating-a-cmdlet-without-parameters.md)).</span></span>

<span data-ttu-id="02196-105">Ez a szakasz témakörei a következők:</span><span class="sxs-lookup"><span data-stu-id="02196-105">Topics in this section include the following:</span></span>

- [<span data-ttu-id="02196-106">Tudnivaló paraméterkészlettel kapcsolatban</span><span class="sxs-lookup"><span data-stu-id="02196-106">Things to Know About Parameter Sets</span></span>](#Adding-Parameter-Sets-to-a-Cmdlet)

- [<span data-ttu-id="02196-107">A parancsmag osztály deklaráló</span><span class="sxs-lookup"><span data-stu-id="02196-107">Declaring the Cmdlet Class</span></span>](#Declaring-the-Cmdlet-Class)

- [<span data-ttu-id="02196-108">A parancsmag paramétereit deklaráló</span><span class="sxs-lookup"><span data-stu-id="02196-108">Declaring the Parameters of the Cmdlet</span></span>](#Declaring-the-Parameters-of-the-Cmdlet)

- [<span data-ttu-id="02196-109">Egy bemeneti metódus feldolgozási felülbírálása</span><span class="sxs-lookup"><span data-stu-id="02196-109">Overriding an Input Processing Method</span></span>](#Overriding-an-Input-Processing-Method)

- [<span data-ttu-id="02196-110">Kódminta</span><span class="sxs-lookup"><span data-stu-id="02196-110">Code Sample</span></span>](#Declaring-the-Parameters-of-the-Cmdlet)

- [<span data-ttu-id="02196-111">Objektumtípusok definiálása és formázása</span><span class="sxs-lookup"><span data-stu-id="02196-111">Defining Object Types and Formatting</span></span>](#Defining-Object-Types-and-Formatting)

- [<span data-ttu-id="02196-112">A parancsmag készítése</span><span class="sxs-lookup"><span data-stu-id="02196-112">Building the Cmdlet</span></span>](#Building-the-Cmdlet)

- [<span data-ttu-id="02196-113">A parancsmag tesztelése</span><span class="sxs-lookup"><span data-stu-id="02196-113">Testing the Cmdlet</span></span>](#Testing-the-Cmdlet)

## <a name="things-to-know-about-parameter-sets"></a><span data-ttu-id="02196-114">Tudnivaló paraméterkészlettel kapcsolatban</span><span class="sxs-lookup"><span data-stu-id="02196-114">Things to Know About Parameter Sets</span></span>

<span data-ttu-id="02196-115">Windows PowerShell-paramétert olyan paramétereket, működjön együtt határozza meg.</span><span class="sxs-lookup"><span data-stu-id="02196-115">Windows PowerShell defines a parameter set as a group of parameters that operate together.</span></span> <span data-ttu-id="02196-116">-Okat a parancsmag paramétereit, hozzon létre egy egyetlen parancsmag, amely alapján a csoport milyen paraméterek a felhasználó adja meg a működését is módosíthatja.</span><span class="sxs-lookup"><span data-stu-id="02196-116">By grouping the parameters of a cmdlet, you can create a single cmdlet that can change its functionality based on what group of parameters the user specifies.</span></span>

<span data-ttu-id="02196-117">Például olyan parancsmagot, amely két paraméterkészlettel használ a különböző funkciók meghatározására a `Get-EventLog` parancsmag Windows PowerShell által biztosított.</span><span class="sxs-lookup"><span data-stu-id="02196-117">An example of a cmdlet that uses two parameter sets to define different functionalities is the `Get-EventLog` cmdlet that is provided by Windows PowerShell.</span></span> <span data-ttu-id="02196-118">Ez a parancsmag különböző információkat ad vissza, ha a felhasználó adja meg a `List` vagy `LogName` paraméter.</span><span class="sxs-lookup"><span data-stu-id="02196-118">This cmdlet returns different information when the user specifies the `List` or `LogName` parameter.</span></span> <span data-ttu-id="02196-119">Ha a `LogName` paraméter meg van adva, a parancsmag visszaadja a eseményekkel kapcsolatos információkat lévő adott eseménynaplóból.</span><span class="sxs-lookup"><span data-stu-id="02196-119">If the `LogName` parameter is specified, the cmdlet returns information about the events in a given event log.</span></span> <span data-ttu-id="02196-120">Ha a `List` paraméter meg van adva, a parancsmag visszaadja a napló információ fájlok magukat (nem az események adatait tartalmazzák).</span><span class="sxs-lookup"><span data-stu-id="02196-120">If the `List` parameter is specified, the cmdlet returns information about the log files themselves (not the event information they contain).</span></span> <span data-ttu-id="02196-121">Ebben az esetben a `List` és `LogName` paraméterek két külön paraméterkészlettel azonosításához.</span><span class="sxs-lookup"><span data-stu-id="02196-121">In this case, the `List` and `LogName` parameters identify two separate parameter sets.</span></span>

<span data-ttu-id="02196-122">Tudnivalók paraméterkészlettel két fontos dolog, hogy a Windows PowerShell-modul egy adott bevitel beállítása csak egyetlen paramétert használ, és, hogy minden egyes paraméterkészletet rendelkeznie kell legalább egy paramétert, amely egyedi az adott paraméterkészletet.</span><span class="sxs-lookup"><span data-stu-id="02196-122">Two important things to remember about parameter sets is that the Windows PowerShell runtime uses only one parameter set for a particular input, and that each parameter set must have at least one parameter that is unique for that parameter set.</span></span>

<span data-ttu-id="02196-123">A legutóbbi pont mutatja be, a Stop-Proc parancsmag három paraméterkészlettel használ: `ProcessName`, `ProcessId`, és `InputObject`.</span><span class="sxs-lookup"><span data-stu-id="02196-123">To illustrate that last point, this Stop-Proc cmdlet uses three parameter sets: `ProcessName`, `ProcessId`, and `InputObject`.</span></span> <span data-ttu-id="02196-124">Ezek paraméterkészlettel mindegyike rendelkezik, amely nem szerepel a többi paraméterkészlettel egy paramétert.</span><span class="sxs-lookup"><span data-stu-id="02196-124">Each of these parameter sets has one parameter that is not in the other parameter sets.</span></span> <span data-ttu-id="02196-125">A paraméterkészlettel megoszthat más paramétereket, de a parancsmag az egyedi paramétereket használja `ProcessName`, `ProcessId`, és `InputObject` azonosításához, mely a Windows PowerShell-modul használandó paraméterek készletével.</span><span class="sxs-lookup"><span data-stu-id="02196-125">The parameter sets could share other parameters, but the cmdlet uses the unique parameters `ProcessName`, `ProcessId`, and `InputObject` to identify which set of parameters that the Windows PowerShell runtime should use.</span></span>

## <a name="declaring-the-cmdlet-class"></a><span data-ttu-id="02196-126">A parancsmag osztály deklaráló</span><span class="sxs-lookup"><span data-stu-id="02196-126">Declaring the Cmdlet Class</span></span>

<span data-ttu-id="02196-127">Mindig a parancsmag elnevezési és a .NET-osztály, amely megvalósítja a parancsmag deklaráló parancsmag létrehozásának első lépése.</span><span class="sxs-lookup"><span data-stu-id="02196-127">The first step in cmdlet creation is always naming the cmdlet and declaring the .NET class that implements the cmdlet.</span></span> <span data-ttu-id="02196-128">A parancsmag az életciklus-művelet "Stop" használatos, mert a parancsmag rendszerfolyamatok leáll.</span><span class="sxs-lookup"><span data-stu-id="02196-128">For this cmdlet, the life-cycle verb "Stop" is used because the cmdlet stops system processes.</span></span> <span data-ttu-id="02196-129">A főnév neve "Proc" használata a parancsmag a folyamatok működik.</span><span class="sxs-lookup"><span data-stu-id="02196-129">The noun name "Proc" is used because the cmdlet works on processes.</span></span> <span data-ttu-id="02196-130">Az alábbi nyilatkozatot jegyezze fel, hogy a parancsmag ige és főnév neve jelennek-e be a parancsmag az osztály nevét.</span><span class="sxs-lookup"><span data-stu-id="02196-130">In the declaration below, note that the cmdlet verb and noun name are reflected in the name of the cmdlet class.</span></span>

> [!NOTE]
> <span data-ttu-id="02196-131">További információ a jóváhagyott művelet neve: [művelet neve](./approved-verbs-for-windows-powershell-commands.md).</span><span class="sxs-lookup"><span data-stu-id="02196-131">For more information about approved cmdlet verb names, see [Cmdlet Verb Names](./approved-verbs-for-windows-powershell-commands.md).</span></span>

<span data-ttu-id="02196-132">A következő kódot a Stop-Proc parancsmag osztálydefiníció.</span><span class="sxs-lookup"><span data-stu-id="02196-132">The following code is the class definition for this Stop-Proc cmdlet.</span></span>

```csharp
[Cmdlet(VerbsLifecycle.Stop, "Proc",
        DefaultParameterSetName = "ProcessId",
        SupportsShouldProcess = true)]
public class StopProcCommand : PSCmdlet
```

```vb
<Cmdlet(VerbsLifecycle.Stop, "Proc", DefaultParameterSetName:="ProcessId", _
SupportsShouldProcess:=True)> _
Public Class StopProcCommand
    Inherits PSCmdlet
```

## <a name="declaring-the-parameters-of-the-cmdlet"></a><span data-ttu-id="02196-133">A parancsmag paramétereit deklaráló</span><span class="sxs-lookup"><span data-stu-id="02196-133">Declaring the Parameters of the Cmdlet</span></span>

<span data-ttu-id="02196-134">Ez a parancsmag három paraméter szükséges a parancsmag (ezeket a paramétereket is megadhatja a paraméterkészlettel), majd határozza meg, valamint egy `Force` paraméter, amely kezeli a parancsmag funkciója és a egy `PassThru` paraméter, amely meghatározza, hogy küld-e a parancsmag egy a folyamat keretében kimeneti objektumot.</span><span class="sxs-lookup"><span data-stu-id="02196-134">This cmdlet defines three parameters needed as input to the cmdlet (these parameters also define the parameter sets), as well as a `Force` parameter that manages what the cmdlet does and a `PassThru` parameter that determines whether the cmdlet sends an output object through the pipeline.</span></span> <span data-ttu-id="02196-135">Alapértelmezés szerint ez a parancsmag nem felel meg a folyamat használatával egy objektumot.</span><span class="sxs-lookup"><span data-stu-id="02196-135">By default, this cmdlet does not pass an object through the pipeline.</span></span> <span data-ttu-id="02196-136">Ezen utolsó két paraméterekkel kapcsolatos további információkért lásd: [létrehozása egy parancsmag, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md).</span><span class="sxs-lookup"><span data-stu-id="02196-136">For more information about these last two parameters, see [Creating a Cmdlet that Modifies the System](./creating-a-cmdlet-that-modifies-the-system.md).</span></span>

### <a name="declaring-the-name-parameter"></a><span data-ttu-id="02196-137">A Name paraméter deklaráló</span><span class="sxs-lookup"><span data-stu-id="02196-137">Declaring the Name Parameter</span></span>

<span data-ttu-id="02196-138">A bemeneti paraméter lehetővé teszi, hogy a felhasználó számára le kell állítani a folyamatok nevét adja meg.</span><span class="sxs-lookup"><span data-stu-id="02196-138">This input parameter allows the user to specify the names of the processes to be stopped.</span></span> <span data-ttu-id="02196-139">Vegye figyelembe, hogy a `ParameterSetName` kulcsszó az attribútum a [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) attribútum meghatározza, hogy a `ProcessName` paraméterkészlet ehhez a paraméterhez.</span><span class="sxs-lookup"><span data-stu-id="02196-139">Note that the `ParameterSetName` attribute keyword of the [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) attribute specifies the `ProcessName` parameter set for this parameter.</span></span>

[!code-csharp[StopProcessSample04.cs](../../powershell-sdk-samples/SDK-2.0/csharp/StopProcessSample04/StopProcessSample04.cs#L44-L58 "StopProcessSample04.cs")]

```vb
<Parameter(Position:=0, ParameterSetName:="ProcessName", _
Mandatory:=True, _
ValueFromPipeline:=True, ValueFromPipelineByPropertyName:=True, _
HelpMessage:="The name of one or more processes to stop. " & _
    "Wildcards are permitted."), [Alias]("ProcessName")> _
Public Property Name() As String()
    Get
        Return processNames
    End Get
    Set(ByVal value As String())
        processNames = value
    End Set
End Property

Private processNames() As String
```

<span data-ttu-id="02196-140">Fontos megjegyezni, hogy az alias "ProcessName" a paraméter van megadva.</span><span class="sxs-lookup"><span data-stu-id="02196-140">Note also that the alias "ProcessName" is given to this parameter.</span></span>

### <a name="declaring-the-id-parameter"></a><span data-ttu-id="02196-141">Az Id paraméter deklaráló</span><span class="sxs-lookup"><span data-stu-id="02196-141">Declaring the Id Parameter</span></span>

<span data-ttu-id="02196-142">A bemeneti paraméter lehetővé teszi, hogy a felhasználó számára le kell állítani a folyamatok azonosítóját adja meg.</span><span class="sxs-lookup"><span data-stu-id="02196-142">This input parameter allows the user to specify the identifiers of the processes to be stopped.</span></span> <span data-ttu-id="02196-143">Vegye figyelembe, hogy a `ParameterSetName` kulcsszó az attribútum a [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) attribútum meghatározza, hogy a `ProcessId` paraméterkészletet.</span><span class="sxs-lookup"><span data-stu-id="02196-143">Note that the `ParameterSetName` attribute keyword of the [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) attribute specifies the `ProcessId` parameter set.</span></span>

```csharp
[Parameter(
           ParameterSetName = "ProcessId",
           Mandatory = true,
           ValueFromPipelineByPropertyName = true,
           ValueFromPipeline = true
)]
[Alias("ProcessId")]
public int[] Id
{
  get { return processIds; }
  set { processIds = value; }
}
private int[] processIds;
```

```vb
<Parameter(ParameterSetName:="ProcessId", _
Mandatory:=True, _
ValueFromPipelineByPropertyName:=True, _
ValueFromPipeline:=True), [Alias]("ProcessId")> _
Public Property Id() As Integer()
    Get
        Return processIds
    End Get
    Set(ByVal value As Integer())
        processIds = value
    End Set
End Property
Private processIds() As Integer
```

<span data-ttu-id="02196-144">Fontos megjegyezni, hogy az alias "Folyamatazonosító" a paraméter van megadva.</span><span class="sxs-lookup"><span data-stu-id="02196-144">Note also that the alias "ProcessId" is given to this parameter.</span></span>

### <a name="declaring-the-inputobject-parameter"></a><span data-ttu-id="02196-145">Deklaráló InputObject paraméter</span><span class="sxs-lookup"><span data-stu-id="02196-145">Declaring the InputObject Parameter</span></span>

<span data-ttu-id="02196-146">A bemeneti paraméter lehetővé teszi, hogy a felhasználó megadhatja a bemeneti objektum, amely le kell állítani a folyamatokkal kapcsolatos információkat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="02196-146">This input parameter allows the user to specify an input object that contains information about the processes to be stopped.</span></span> <span data-ttu-id="02196-147">Vegye figyelembe, hogy a `ParameterSetName` kulcsszó az attribútum a [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) attribútum meghatározza, hogy a `InputObject` paraméterkészlet ehhez a paraméterhez.</span><span class="sxs-lookup"><span data-stu-id="02196-147">Note that the `ParameterSetName` attribute keyword of the [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) attribute specifies the `InputObject` parameter set for this parameter.</span></span>

```csharp
[Parameter(
           ParameterSetName = "InputObject",
           Mandatory = true,
           ValueFromPipeline = true)]
public Process[] InputObject
{
  get { return inputObject; }
  set { inputObject = value; }
}
private Process[] inputObject;
```

```vb
<Parameter(ParameterSetName:="InputObject", _
Mandatory:=True, ValueFromPipeline:=True)> _
Public Property InputObject() As Process()
    Get
        Return myInputObject
    End Get
    Set(ByVal value As Process())
        myInputObject = value
    End Set
End Property
Private myInputObject() As Process
```

<span data-ttu-id="02196-148">Ne feledje is, hogy ez a paraméter nincs aliasneve.</span><span class="sxs-lookup"><span data-stu-id="02196-148">Note also that this parameter has no alias.</span></span>

### <a name="declaring-parameters-in-multiple-parameter-sets"></a><span data-ttu-id="02196-149">Paramétereket a több paraméterkészlettel deklaráló</span><span class="sxs-lookup"><span data-stu-id="02196-149">Declaring Parameters in Multiple Parameter Sets</span></span>

<span data-ttu-id="02196-150">Bár az egyes paraméternek egyedi paraméternek kell lennie, paraméterek egynél több paraméterkészlettel is tartozhat.</span><span class="sxs-lookup"><span data-stu-id="02196-150">Although there must be a unique parameter for each parameter set, parameters can belong to more than one parameter set.</span></span> <span data-ttu-id="02196-151">Ezekben az esetekben adja meg a megosztott paraméter egy [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) típusattribútum-deklaráció egyes beállítása mely, amely a paraméter tartozik.</span><span class="sxs-lookup"><span data-stu-id="02196-151">In these cases, give the shared parameter a [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) attribute declaration for each set to which that the parameter belongs.</span></span> <span data-ttu-id="02196-152">Ha egy paraméter paraméterkészlettel minden, akkor csak egyszer deklarálja a paraméter-attribútumhoz kell, és nem kell megadnia a paraméterkészlet neve.</span><span class="sxs-lookup"><span data-stu-id="02196-152">If a parameter is in all parameter sets, you only have to declare the parameter attribute once and do not need to specify the parameter set name.</span></span>

## <a name="overriding-an-input-processing-method"></a><span data-ttu-id="02196-153">Egy bemeneti metódus feldolgozási felülbírálása</span><span class="sxs-lookup"><span data-stu-id="02196-153">Overriding an Input Processing Method</span></span>

<span data-ttu-id="02196-154">Minden parancsmagot felül kell írnia egy bemeneti metódus feldolgozása, a leggyakrabban ez lesz a [System.Management.Automation.Cmdlet.Processrecord\*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust.</span><span class="sxs-lookup"><span data-stu-id="02196-154">Every cmdlet must override an input processing method, most often this will be the [System.Management.Automation.Cmdlet.Processrecord\*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method.</span></span> <span data-ttu-id="02196-155">Ebben a parancsmagban a [System.Management.Automation.Cmdlet.Processrecord\*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) úgy, hogy a parancsmag képes feldolgozni a folyamatok tetszőleges számú módszert felülbírálja.</span><span class="sxs-lookup"><span data-stu-id="02196-155">In this cmdlet, the [System.Management.Automation.Cmdlet.Processrecord\*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method is overridden so that the cmdlet can process any number of processes.</span></span> <span data-ttu-id="02196-156">Tartalmaz egy kiválasztási utasítás, amely meghívja a melyik paraméterkészlet alapján más módszert a felhasználó adta meg.</span><span class="sxs-lookup"><span data-stu-id="02196-156">It contains a Select statement that calls a different method based on which parameter set the user has specified.</span></span>

```csharp
protected override void ProcessRecord()
{
  switch (ParameterSetName)
  {
    case "ProcessName":
         ProcessByName();
         break;

    case "ProcessId":
         ProcessById();
         break;

    case "InputObject":
         foreach (Process process in inputObject)
         {
           SafeStopProcess(process);
         }
         break;

    default:
         throw new ArgumentException("Bad ParameterSet Name");
  } // switch (ParameterSetName...
} // ProcessRecord
```

```vb
Protected Overrides Sub ProcessRecord()
    Select Case ParameterSetName
        Case "ProcessName"
            ProcessByName()

        Case "ProcessId"
            ProcessById()

        Case "InputObject"
            Dim process As Process
            For Each process In myInputObject
                SafeStopProcess(process)
            Next process

        Case Else
            Throw New ArgumentException("Bad ParameterSet Name")
    End Select

End Sub 'ProcessRecord ' ProcessRecord
```

<span data-ttu-id="02196-157">Az a Select-utasítás által meghívott segédmetódusokat nem ebben a témakörben találhatók, de megtekintheti a teljes kódmintát a következő szakaszban a végrehajtásuk.</span><span class="sxs-lookup"><span data-stu-id="02196-157">The Helper methods called by the Select statement are not described here, but you can see their implementation in the complete code sample in the next section.</span></span>

## <a name="code-sample"></a><span data-ttu-id="02196-158">Kódminta</span><span class="sxs-lookup"><span data-stu-id="02196-158">Code Sample</span></span>

<span data-ttu-id="02196-159">A teljes C# mintakód, lásd: [StopProcessSample04 minta](./stopprocesssample04-sample.md).</span><span class="sxs-lookup"><span data-stu-id="02196-159">For the complete C# sample code, see [StopProcessSample04 Sample](./stopprocesssample04-sample.md).</span></span>

## <a name="defining-object-types-and-formatting"></a><span data-ttu-id="02196-160">Objektumtípusok definiálása és formázása</span><span class="sxs-lookup"><span data-stu-id="02196-160">Defining Object Types and Formatting</span></span>

<span data-ttu-id="02196-161">Windows PowerShell parancsmagok használatával a .NET-objektumokká közötti továbbítja.</span><span class="sxs-lookup"><span data-stu-id="02196-161">Windows PowerShell passes information between cmdlets using .NET objects.</span></span> <span data-ttu-id="02196-162">Ennek következtében a parancsmag előfordulhat, hogy meg kell határoznia a saját típusát, vagy a parancsmag előfordulhat, hogy ki kell terjesztenie egy másik parancsmag által biztosított meglévő típus.</span><span class="sxs-lookup"><span data-stu-id="02196-162">Consequently, a cmdlet might need to define its own type, or the cmdlet might need to extend an existing type provided by another cmdlet.</span></span> <span data-ttu-id="02196-163">Új típusok meghatározása, vagy meglévő típusok bővítésével kapcsolatos további információkért lásd: [objektumtípusok kiterjesztése és formázás](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).</span><span class="sxs-lookup"><span data-stu-id="02196-163">For more information about defining new types or extending existing types, see [Extending Object Types and Formatting](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).</span></span>

## <a name="building-the-cmdlet"></a><span data-ttu-id="02196-164">A parancsmag készítése</span><span class="sxs-lookup"><span data-stu-id="02196-164">Building the Cmdlet</span></span>

<span data-ttu-id="02196-165">Parancsmag-k megvalósítása után regisztrálnia kell azt a Windows PowerShell-lel a Windows PowerShell beépülő modullal.</span><span class="sxs-lookup"><span data-stu-id="02196-165">After implementing a cmdlet, you must register it with Windows PowerShell through a Windows PowerShell snap-in.</span></span> <span data-ttu-id="02196-166">Parancsmagok regisztrálásával kapcsolatos további információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).</span><span class="sxs-lookup"><span data-stu-id="02196-166">For more information about registering cmdlets, see [How to Register Cmdlets, Providers, and Host Applications](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).</span></span>

## <a name="testing-the-cmdlet"></a><span data-ttu-id="02196-167">A parancsmag tesztelése</span><span class="sxs-lookup"><span data-stu-id="02196-167">Testing the Cmdlet</span></span>

<span data-ttu-id="02196-168">Ha a parancsmagot a Windows PowerShell-lel regisztrálva lett, tesztelje azt a parancssorból való futtatásával.</span><span class="sxs-lookup"><span data-stu-id="02196-168">When your cmdlet has been registered with Windows PowerShell, test it by running it on the command line.</span></span> <span data-ttu-id="02196-169">Az alábbiakban néhány tesztek azt mutatják be, hogyan a `ProcessId` és `InputObject` paraméterek azok paraméterkészlettel leállítani a folyamat teszteléséhez használhatók.</span><span class="sxs-lookup"><span data-stu-id="02196-169">Here are some tests that show how the `ProcessId` and `InputObject` parameters can be used to test their parameter sets to stop a process.</span></span>

- <span data-ttu-id="02196-170">A Windows PowerShell-lel elindult, futtassa a Stop-Proc parancsmagot a `ProcessId` paraméter beállítása annak azonosítója alapján a folyamat leállítása.</span><span class="sxs-lookup"><span data-stu-id="02196-170">With Windows PowerShell started, run the Stop-Proc cmdlet with the `ProcessId` parameter set to stop a process based on its identifier.</span></span> <span data-ttu-id="02196-171">Ebben az esetben a parancsmagot használja a `ProcessId` paraméterkészlet a folyamat leállítása érdekében.</span><span class="sxs-lookup"><span data-stu-id="02196-171">In this case, the cmdlet is using the `ProcessId` parameter set to stop the process.</span></span>

    ```
    PS> stop-proc -Id 444
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "notepad (444)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y
    ```

- <span data-ttu-id="02196-172">A Windows PowerShell-lel elindult, futtassa a Stop-Proc parancsmagot a `InputObject` paraméterkészlet folyamatok leállítani a Jegyzettömb objektum által beolvasott a `Get-Process` parancsot.</span><span class="sxs-lookup"><span data-stu-id="02196-172">With Windows PowerShell started, run the Stop-Proc cmdlet with the `InputObject` parameter set to stop processes on the Notepad object retrieved by the `Get-Process` command.</span></span>

    ```
    PS> get-process notepad | stop-proc
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "notepad (444)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): N
    ```

## <a name="see-also"></a><span data-ttu-id="02196-173">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="02196-173">See Also</span></span>

[<span data-ttu-id="02196-174">A parancsmag létrehozása, amely módosítja a rendszer</span><span class="sxs-lookup"><span data-stu-id="02196-174">Creating a Cmdlet that Modifies the System</span></span>](./creating-a-cmdlet-that-modifies-the-system.md)

[<span data-ttu-id="02196-175">Hogyan hozhat létre egy Windows PowerShell-parancsmag</span><span class="sxs-lookup"><span data-stu-id="02196-175">How to Create a Windows PowerShell Cmdlet</span></span>](http://msdn.microsoft.com/en-us/0d721742-c849-4d0d-964f-78ddd9cd258c)

[<span data-ttu-id="02196-176">Objektumtípusok kiterjesztése és formázása</span><span class="sxs-lookup"><span data-stu-id="02196-176">Extending Object Types and Formatting</span></span>](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[<span data-ttu-id="02196-177">How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez</span><span class="sxs-lookup"><span data-stu-id="02196-177">How to Register Cmdlets, Providers, and Host Applications</span></span>](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[<span data-ttu-id="02196-178">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="02196-178">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
