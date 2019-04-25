---
title: Paraméterek nélkül a parancsmag létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cmdlets [PowerShell Programmers Guide], creating
- cmdlets [PowerShell Programmers Guide], basic cmdlet
ms.assetid: 54236ef3-82db-45f8-9114-1ecb7ff65d3e
caps.latest.revision: 8
ms.openlocfilehash: c380b28570c955de6f41152fd617f5c1b0f9e4bd
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068334"
---
# <a name="creating-a-cmdlet-without-parameters"></a><span data-ttu-id="fbc9f-102">Paraméterek nélküli parancsmag létrehozása</span><span class="sxs-lookup"><span data-stu-id="fbc9f-102">Creating a Cmdlet without Parameters</span></span>

<span data-ttu-id="fbc9f-103">Ez a szakasz ismerteti, hogyan hozhat létre olyan parancsmagot, amely adatait kérdezi le a helyi számítógépen, a paraméterek nélkül, és a folyamat ezután beírja az információkat.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-103">This section describes how to create a cmdlet that retrieves information from the local computer without the use of parameters, and then writes the information to the pipeline.</span></span> <span data-ttu-id="fbc9f-104">A parancsmag az itt leírtak szerint egy Get-Proc parancsmag, amely a folyamatok a helyi számítógép adatait kérdezi le, majd megjeleníti ezt az információt a parancssorból.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-104">The cmdlet described here is a Get-Proc cmdlet that retrieves information about the processes of the local computer, and then displays that information at the command line.</span></span>

<span data-ttu-id="fbc9f-105">Ez a szakasz témakörei a következők:</span><span class="sxs-lookup"><span data-stu-id="fbc9f-105">Topics in this section include the following:</span></span>

- [<span data-ttu-id="fbc9f-106">A parancsmag elnevezése</span><span class="sxs-lookup"><span data-stu-id="fbc9f-106">Naming the Cmdlet</span></span>](#Naming-the-Cmdlet)

- [<span data-ttu-id="fbc9f-107">A parancsmag osztály meghatározása</span><span class="sxs-lookup"><span data-stu-id="fbc9f-107">Defining the Cmdlet Class</span></span>](#Defining-the-Cmdlet-Class)

- [<span data-ttu-id="fbc9f-108">Egy bemeneti metódus feldolgozási felülbírálása</span><span class="sxs-lookup"><span data-stu-id="fbc9f-108">Overriding an Input Processing Method</span></span>](#Overriding-an-Input-Processing-Method)

- [<span data-ttu-id="fbc9f-109">Kódminta</span><span class="sxs-lookup"><span data-stu-id="fbc9f-109">Code Sample</span></span>](#Code-Sample)

- [<span data-ttu-id="fbc9f-110">Objektumtípusok definiálása és formázása</span><span class="sxs-lookup"><span data-stu-id="fbc9f-110">Defining Object Types and Formatting</span></span>](#Defining-Object-Types-and-Formatting)

- [<span data-ttu-id="fbc9f-111">A parancsmag készítése</span><span class="sxs-lookup"><span data-stu-id="fbc9f-111">Building the Cmdlet</span></span>](#Building-the-Cmdlet)

- [<span data-ttu-id="fbc9f-112">A parancsmag tesztelése</span><span class="sxs-lookup"><span data-stu-id="fbc9f-112">Testing the Cmdlet</span></span>](#Testing-the-Cmdlet)

> [!NOTE]
> <span data-ttu-id="fbc9f-113">Vegye figyelembe, hogy parancsmagok írásakor, a Windows PowerShell® referenciaszerelvények letöltődnek lemezre (alapértelmezés szerint a C:\Program Files\Reference Assemblies\Microsoft\WindowsPowerShell\v1.0). A globális szerelvény gyorsítótárban (GAC) a telepítés nem.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-113">Be aware that when writing cmdlets, the Windows PowerShell® reference assemblies are downloaded onto disk (by default at C:\Program Files\Reference Assemblies\Microsoft\WindowsPowerShell\v1.0).They are not installed in the Global Assembly Cache (GAC).</span></span>

## <a name="naming-the-cmdlet"></a><span data-ttu-id="fbc9f-114">A parancsmag elnevezése</span><span class="sxs-lookup"><span data-stu-id="fbc9f-114">Naming the Cmdlet</span></span>

<span data-ttu-id="fbc9f-115">Egy parancsmag neve, amely jelzi, hogy a művelet a parancsmag lép igeként és főnév, amely azt jelzi, hogy az elemek, amelyek a parancsmagot a közvetítőtől áll.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-115">A cmdlet name consists of a verb that indicates the action the cmdlet takes and a noun that indicates the items that the cmdlet acts upon.</span></span> <span data-ttu-id="fbc9f-116">A Get-Proc parancsmagra folyamat objektumok kér le, mert használja a művelet "Get", határozzák meg a [System.Management.Automation.Verbscommon](/dotnet/api/System.Management.Automation.VerbsCommon) enumerálása, és a főnév jelzi, hogy működik-e a parancsmag folyamat elemeken a "Proc".</span><span class="sxs-lookup"><span data-stu-id="fbc9f-116">Because this sample Get-Proc cmdlet retrieves process objects, it uses the verb "Get", defined by the [System.Management.Automation.Verbscommon](/dotnet/api/System.Management.Automation.VerbsCommon) enumeration, and the noun "Proc" to indicate that the cmdlet works on process items.</span></span>

<span data-ttu-id="fbc9f-117">Parancsmagok elnevezésekor ne használja a következő karaktereket: #, () {} [] & - / \ $;: "" <> &#124; ?</span><span class="sxs-lookup"><span data-stu-id="fbc9f-117">When naming cmdlets, do not use any of the following characters: # , () {} [] & - /\ $ ; : " '<> &#124; ?</span></span> <span data-ttu-id="fbc9f-118">@ \` .</span><span class="sxs-lookup"><span data-stu-id="fbc9f-118">@ \` .</span></span>

### <a name="choosing-a-noun"></a><span data-ttu-id="fbc9f-119">Főnév kiválasztása</span><span class="sxs-lookup"><span data-stu-id="fbc9f-119">Choosing a Noun</span></span>

<span data-ttu-id="fbc9f-120">Egy adott főnév kell kiválasztani.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-120">You should choose a noun that is specific.</span></span> <span data-ttu-id="fbc9f-121">A legcélszerűbb jedné főnév előtaggal van ellátva a termék neve akkor használhatja rövidített verzióját használja.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-121">It is best to use a singular noun prefixed with a shortened version of the product name.</span></span> <span data-ttu-id="fbc9f-122">Egy ilyen példa parancsmag neve "`Get-SQLServer`".</span><span class="sxs-lookup"><span data-stu-id="fbc9f-122">An example cmdlet name of this type is "`Get-SQLServer`".</span></span>

### <a name="choosing-a-verb"></a><span data-ttu-id="fbc9f-123">Egy művelet kiválasztása</span><span class="sxs-lookup"><span data-stu-id="fbc9f-123">Choosing a Verb</span></span>

<span data-ttu-id="fbc9f-124">Jóváhagyott parancsmag művelet nevek a készletből egy műveletet kell használnia.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-124">You should use a verb from the set of approved cmdlet verb names.</span></span> <span data-ttu-id="fbc9f-125">A parancsmag jóváhagyott igék kapcsolatos további információkért lásd: [művelet neve](./approved-verbs-for-windows-powershell-commands.md).</span><span class="sxs-lookup"><span data-stu-id="fbc9f-125">For more information about the approved cmdlet verbs, see [Cmdlet Verb Names](./approved-verbs-for-windows-powershell-commands.md).</span></span>

## <a name="defining-the-cmdlet-class"></a><span data-ttu-id="fbc9f-126">A parancsmag osztály meghatározása</span><span class="sxs-lookup"><span data-stu-id="fbc9f-126">Defining the Cmdlet Class</span></span>

<span data-ttu-id="fbc9f-127">Miután kiválasztotta a parancsmag neve, adja meg a parancsmag végrehajtása érdekében egy .NET-osztály.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-127">Once you have chosen a cmdlet name, define a .NET class to implement the cmdlet.</span></span> <span data-ttu-id="fbc9f-128">A Get-Proc parancsmagra osztály definícióját a következő:</span><span class="sxs-lookup"><span data-stu-id="fbc9f-128">Here is the class definition for this sample Get-Proc cmdlet:</span></span>

```csharp
[Cmdlet(VerbsCommon.Get, "Proc")]
  public class GetProcCommand : Cmdlet
```

```vb
<Cmdlet(VerbsCommon.Get, "Proc")> _
Public Class GetProcCommand
    Inherits Cmdlet
```

<span data-ttu-id="fbc9f-129">Figyelje meg, hogy az osztály definícióját vissza a [System.Management.Automation.CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute) attribútum szintaxissal `[Cmdlet(verb, noun, ...)]`, a parancsmag, ez az osztály azonosítására szolgál.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-129">Notice that previous to the class definition, the [System.Management.Automation.CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute) attribute, with the syntax `[Cmdlet(verb, noun, ...)]`, is used to identify this class as a cmdlet.</span></span> <span data-ttu-id="fbc9f-130">Ez az egyetlen szükséges összes parancsmagjához, és lehetővé teszi a Windows PowerShell futtatási helyesen hívja meg őket.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-130">This is the only required attribute for all cmdlets, and it allows the Windows PowerShell runtime to call them correctly.</span></span> <span data-ttu-id="fbc9f-131">Attribútum az osztály tovább deklarálja, szükség esetén kulcsszavakkal állíthatja be.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-131">You can set attribute keywords to further declare the class if necessary.</span></span> <span data-ttu-id="fbc9f-132">Vegye figyelembe, hogy a minta GetProcCommand osztály típusattribútum-deklaráció deklarálja csak főnevet és a művelet nevét a Get-Proc parancsmaghoz.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-132">Be aware that the attribute declaration for our sample GetProcCommand class declares only the noun and verb names for the Get-Proc cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="fbc9f-133">Minden Windows PowerShell attribútum osztály, amely lehet a kulcsszavak felelnek meg az attribútum az osztály tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-133">For all Windows PowerShell attribute classes, the keywords that you can set correspond to properties of the attribute class.</span></span>

<span data-ttu-id="fbc9f-134">Az osztály a parancsmag elnevezésekor tanácsos tükrözik az osztály nevét a parancsmag neve.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-134">When naming the class of the cmdlet, it is a good practice to reflect the cmdlet name in the class name.</span></span> <span data-ttu-id="fbc9f-135">Ehhez használja az űrlap "VerbNounCommand" és "Művelet" és "Főnév" cserélje a ige és főnév, a parancsmag neve szerepel.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-135">To do this, use the form "VerbNounCommand" and replace "Verb" and "Noun" with the verb and noun used in the cmdlet name.</span></span> <span data-ttu-id="fbc9f-136">Amint azt az előző osztálykiterjesztések definíciója, a Get-Proc parancsmagra meghatározása GetProcCommand, amely származó nevű osztály a [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) alaposztály.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-136">As is shown in the previous class definition, the sample Get-Proc cmdlet defines a class called GetProcCommand, which derives from the [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) base class.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fbc9f-137">Ha szeretne meghatározni egy parancsmag, amely a Windows PowerShell-modul közvetlenül hozzáfér, a .NET-osztály típusból kell származtatni a [System.Management.Automation.PSCmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) alaposztály.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-137">If you want to define a cmdlet that accesses the Windows PowerShell runtime directly, your .NET class should derive from the [System.Management.Automation.PSCmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) base class.</span></span> <span data-ttu-id="fbc9f-138">Ez az osztály kapcsolatos további információkért lásd: [létrehozása parancsmag adott meghatározása paraméterkészlettel](./adding-parameter-sets-to-a-cmdlet.md).</span><span class="sxs-lookup"><span data-stu-id="fbc9f-138">For more information about this class, see [Creating a Cmdlet that Defines Parameter Sets](./adding-parameter-sets-to-a-cmdlet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fbc9f-139">Az osztály a parancsmag fel kell tüntetni explicit módon is nyilvános.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-139">The class for a cmdlet must be explicitly marked as public.</span></span> <span data-ttu-id="fbc9f-140">Nem jelölt nyilvános osztályok belső alapértelmezés szerint, és nem található a Windows PowerShell-modul által.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-140">Classes that are not marked as public will default to internal and will not be found by the Windows PowerShell runtime.</span></span>

<span data-ttu-id="fbc9f-141">Használja a Windows PowerShell a [Microsoft.PowerShell.Commands](/dotnet/api/Microsoft.PowerShell.Commands) parancsmag osztályt névterét.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-141">Windows PowerShell uses the [Microsoft.PowerShell.Commands](/dotnet/api/Microsoft.PowerShell.Commands) namespace for its cmdlet classes.</span></span> <span data-ttu-id="fbc9f-142">Javasoljuk, hogy a parancsmag osztályok helyezze az API-t névtér, például xxx.PS.Commands parancsok névtérben.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-142">It is recommended to place your cmdlet classes in a Commands namespace of your API namespace, for example, xxx.PS.Commands.</span></span>

## <a name="overriding-an-input-processing-method"></a><span data-ttu-id="fbc9f-143">Egy bemeneti metódus feldolgozási felülbírálása</span><span class="sxs-lookup"><span data-stu-id="fbc9f-143">Overriding an Input Processing Method</span></span>

<span data-ttu-id="fbc9f-144">A [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) osztály, amely legalább egy a parancsmag felül kell írnia, három bemeneti feldolgozás fő metódusokat biztosít.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-144">The [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) class provides three main input processing methods, at least one of which your cmdlet must override.</span></span> <span data-ttu-id="fbc9f-145">Hogyan dolgozza fel a Windows PowerShell a rekordok kapcsolatos további információkért lásd: [Windows PowerShell működése](https://msdn.microsoft.com/en-us/ced30e23-10af-4700-8933-49873bd84d58).</span><span class="sxs-lookup"><span data-stu-id="fbc9f-145">For more information about how Windows PowerShell processes records, see [How Windows PowerShell Works](https://msdn.microsoft.com/en-us/ced30e23-10af-4700-8933-49873bd84d58).</span></span>

<span data-ttu-id="fbc9f-146">Bemeneti minden típusú, a Windows PowerShell-modult meghívja [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) feldolgozási engedélyezéséhez.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-146">For all types of input, the Windows PowerShell runtime calls [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) to enable processing.</span></span> <span data-ttu-id="fbc9f-147">A parancsmag néhány előfeldolgozása vagy a telepítő kell végrehajtania, ha azt teheti ezt a módszert felülbírálja.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-147">If your cmdlet must perform some preprocessing or setup, it can do this by overriding this method.</span></span>

> [!NOTE]
> <span data-ttu-id="fbc9f-148">Windows PowerShell "rekord" kifejezés használatával ismertetik az megadásakor a parancsmag neve paraméterértékeket.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-148">Windows PowerShell uses the term "record" to describe the set of parameter values supplied when a cmdlet is called.</span></span>

<span data-ttu-id="fbc9f-149">Ha a parancsmag elfogadja az adatcsatorna bemenetének, hogy felül kell írnia a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust, és szükség esetén a [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing)metódust.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-149">If your cmdlet accepts pipeline input, it must override the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method, and optionally the [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) method.</span></span> <span data-ttu-id="fbc9f-150">Például a parancsmag felülírhatják a két módszert ha összes bemeneti használatával gyűjt [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) , és ezután a bemenet egy elemet, hanem a teljes egyszerre, mint a `Sort-Object` a parancsmag hajtja végre.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-150">For example, a cmdlet might override both methods if it gathers all input using [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) and then operates on the input as a whole rather than one element at a time, as the `Sort-Object` cmdlet does.</span></span>

<span data-ttu-id="fbc9f-151">Ha a parancsmag nem hozza a folyamat bemeneti, hogy felül kell írni a [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) metódust.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-151">If your cmdlet does not take pipeline input, it should override the [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) method.</span></span> <span data-ttu-id="fbc9f-152">Vegye figyelembe, hogy ezt a módszert gyakran használt helyén [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) amikor a parancsmag nem működik egy elem egyszerre, mint a rendezési parancsmag.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-152">Be aware that this method is frequently used in place of [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) when the cmdlet cannot operate on one element at a time, as is the case for a sorting cmdlet.</span></span>

<span data-ttu-id="fbc9f-153">A Get-Proc parancsmagra adatcsatorna bemenetének kell kapnia, mert ez a beállítás felülbírálja a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust, és használja az alapértelmezett megvalósítása esetében [ System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) és [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing).</span><span class="sxs-lookup"><span data-stu-id="fbc9f-153">Because this sample Get-Proc cmdlet must receive pipeline input, it overrides the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method and uses the default implementations for [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) and [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing).</span></span> <span data-ttu-id="fbc9f-154">A [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) felülbírálás kérdezi le a folyamatokat, és írja őket a parancssor használatával a [System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) metódust.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-154">The [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) override retrieves processes and writes them to the command line using the [System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) method.</span></span>

```csharp
protected override void ProcessRecord()
{
  // Get the current processes
  Process[] processes = Process.GetProcesses();

  // Write the processes to the pipeline making them available
  // to the next cmdlet. The second parameter of this call tells
  // PowerShell to enumerate the array, and send one process at a
  // time to the pipeline.
  WriteObject(processes, true);
}
```

```vb
Protected Overrides Sub ProcessRecord()

    '/ Get the current processes.
    Dim processes As Process()
    processes = Process.GetProcesses()

    '/ Write the processes to the pipeline making them available
    '/ to the next cmdlet. The second parameter of this call tells
    '/ PowerShell to enumerate the array, and send one process at a
    '/ time to the pipeline.
    WriteObject(processes, True)

End Sub 'ProcessRecord
```

#### <a name="things-to-remember-about-input-processing"></a><span data-ttu-id="fbc9f-155">Megjegyzendő tudnivalók kapcsolatos bemeneti feldolgozása</span><span class="sxs-lookup"><span data-stu-id="fbc9f-155">Things to Remember About Input Processing</span></span>

- <span data-ttu-id="fbc9f-156">A bemeneti alapértelmezett forrása a parancssorban a felhasználó által megadott explicit objektum (például egy karakterlánc).</span><span class="sxs-lookup"><span data-stu-id="fbc9f-156">The default source for input is an explicit object (for example, a string) provided by the user on the command line.</span></span> <span data-ttu-id="fbc9f-157">További információkért lásd: [létrehozásának folyamata parancssori bemeneti parancsmag](./adding-parameters-that-process-command-line-input.md).</span><span class="sxs-lookup"><span data-stu-id="fbc9f-157">For more information, see [Creating a Cmdlet to Process Command Line Input](./adding-parameters-that-process-command-line-input.md).</span></span>

- <span data-ttu-id="fbc9f-158">Egy bemeneti metódus feldolgozási is fogadhatnak bemenet a folyamathoz egy felsőbb rétegbeli parancsmag kimeneti objektumot.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-158">An input processing method can also receive input from the output object of an upstream cmdlet on the pipeline.</span></span> <span data-ttu-id="fbc9f-159">További információkért lásd: [létrehozásának folyamata folyamat bemeneti parancsmag](./adding-parameters-that-process-pipeline-input.md).</span><span class="sxs-lookup"><span data-stu-id="fbc9f-159">For more information, see [Creating a Cmdlet to Process Pipeline Input](./adding-parameters-that-process-pipeline-input.md).</span></span> <span data-ttu-id="fbc9f-160">Vegye figyelembe, hogy a parancsmag bemeneti fogadjon parancssori kombinációját, és folyamat adatforrásokat.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-160">Be aware that your cmdlet can receive input from a combination of command-line and pipeline sources.</span></span>

- <span data-ttu-id="fbc9f-161">Az alsóbb rétegbeli parancsmag előfordulhat, hogy nem ad vissza, hosszú ideje, vagy egyáltalán nem.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-161">The downstream cmdlet might not return for a long time, or not at all.</span></span> <span data-ttu-id="fbc9f-162">Éppen ezért a feldolgozási mód a parancsmag a bemeneti kell tartalmaz a zárolások hívások során [System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject), különösen a zárolásokat, amelyhez a hatókör túlnyúlik a parancsmag-példány.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-162">For that reason, the input processing method in your cmdlet should not hold locks during calls to [System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject), especially locks for which the scope extends beyond the cmdlet instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fbc9f-163">Parancsmagok soha nem kell hívnia [System.Console.Writeline\*](/dotnet/api/System.Console.WriteLine) vagy azzal egyenértékű.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-163">Cmdlets should never call [System.Console.Writeline\*](/dotnet/api/System.Console.WriteLine) or its equivalent.</span></span>

- <span data-ttu-id="fbc9f-164">Előfordulhat, hogy a parancsmag objektum változók végeztével karbantartása feldolgozása (például akkor, ha a fájlleíró megnyílik a [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) metódust, és korlátlan ideig megőrzi a leíró használatra megnyitásához[ System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord)).</span><span class="sxs-lookup"><span data-stu-id="fbc9f-164">Your cmdlet might have object variables to clean up when it is finished processing (for example, if it opens a file handle in the [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) method and keeps the handle open for use by [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord)).</span></span> <span data-ttu-id="fbc9f-165">Fontos megjegyezni, hogy a Windows PowerShell-modul nem mindig hívja a [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) metódussal, amely végre kell hajtania objektum karbantartása.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-165">It is important to remember that the Windows PowerShell runtime does not always call the [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) method, which should perform object cleanup.</span></span>

<span data-ttu-id="fbc9f-166">Ha például [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) előfordulhat, hogy nem hívható meg, ha a parancsmag midway megszakadt, vagy ha egy megszakítást okozó hiba jelenik meg a parancsmag bármely részén.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-166">For example, [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) might not be called if the cmdlet is canceled midway or if a terminating error occurs in any part of the cmdlet.</span></span> <span data-ttu-id="fbc9f-167">Ezért egy objektum karbantartási igénylő parancsmag meg kell valósítania a teljes [System.IDisposable](/dotnet/api/System.IDisposable) minta, beleértve a befejezővel úgy, hogy a futtatókörnyezet is meghívhat [ System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) és [System.IDisposable.Dispose\*](/dotnet/api/System.IDisposable.Dispose) feldolgozás végén.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-167">Therefore, a cmdlet that requires object cleanup should implement the complete [System.IDisposable](/dotnet/api/System.IDisposable) pattern, including the finalizer, so that the runtime can call both [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) and [System.IDisposable.Dispose\*](/dotnet/api/System.IDisposable.Dispose) at the end of processing.</span></span>

## <a name="code-sample"></a><span data-ttu-id="fbc9f-168">Kódminta</span><span class="sxs-lookup"><span data-stu-id="fbc9f-168">Code Sample</span></span>

<span data-ttu-id="fbc9f-169">A teljes C# mintakód, lásd: [GetProcessSample01 minta](./getprocesssample01-sample.md).</span><span class="sxs-lookup"><span data-stu-id="fbc9f-169">For the complete C# sample code, see [GetProcessSample01 Sample](./getprocesssample01-sample.md).</span></span>

## <a name="defining-object-types-and-formatting"></a><span data-ttu-id="fbc9f-170">Objektumtípusok definiálása és formázása</span><span class="sxs-lookup"><span data-stu-id="fbc9f-170">Defining Object Types and Formatting</span></span>

<span data-ttu-id="fbc9f-171">Windows PowerShell parancsmagok használatával a .NET-objektumokká közötti továbbítja.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-171">Windows PowerShell passes information between cmdlets using .NET objects.</span></span> <span data-ttu-id="fbc9f-172">Ennek következtében a parancsmag előfordulhat, hogy meg kell határoznia a saját típusát, vagy a parancsmag előfordulhat, hogy ki kell terjesztenie egy másik parancsmag által biztosított meglévő típus.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-172">Consequently, a cmdlet might need to define its own type, or the cmdlet might need to extend an existing type provided by another cmdlet.</span></span> <span data-ttu-id="fbc9f-173">Új típusok meghatározása, vagy meglévő típusok bővítésével kapcsolatos további információkért lásd: [objektumtípusok kiterjesztése és formázás](https://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).</span><span class="sxs-lookup"><span data-stu-id="fbc9f-173">For more information about defining new types or extending existing types, see [Extending Object Types and Formatting](https://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).</span></span>

## <a name="building-the-cmdlet"></a><span data-ttu-id="fbc9f-174">A parancsmag készítése</span><span class="sxs-lookup"><span data-stu-id="fbc9f-174">Building the Cmdlet</span></span>

<span data-ttu-id="fbc9f-175">Parancsmag-k megvalósítása után regisztrálnia kell azt a Windows PowerShell-lel a Windows PowerShell beépülő modullal.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-175">After implementing a cmdlet, you must register it with Windows PowerShell through a Windows PowerShell snap-in.</span></span> <span data-ttu-id="fbc9f-176">Parancsmagok regisztrálásával kapcsolatos további információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).</span><span class="sxs-lookup"><span data-stu-id="fbc9f-176">For more information about registering cmdlets, see [How to Register Cmdlets, Providers, and Host Applications](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).</span></span>

## <a name="testing-the-cmdlet"></a><span data-ttu-id="fbc9f-177">A parancsmag tesztelése</span><span class="sxs-lookup"><span data-stu-id="fbc9f-177">Testing the Cmdlet</span></span>

<span data-ttu-id="fbc9f-178">Ha a parancsmagot a Windows PowerShell-lel regisztrálva lett, azt a parancssorból való futtatásával tesztelheti.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-178">When your cmdlet has been registered with Windows PowerShell, you can test it by running it on the command line.</span></span> <span data-ttu-id="fbc9f-179">A kód a minta-Get-Proc parancsmag kis, de továbbra is használja a Windows PowerShell-modul és a egy meglévő .NET objektum, amely elegendő az, hogy hasznos.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-179">The code for our sample Get-Proc cmdlet is small, but it still uses the Windows PowerShell runtime and an existing .NET object, which is enough to make it useful.</span></span> <span data-ttu-id="fbc9f-180">Most tesztelheti, hogy jobban megismerheti, mi mindent az Get-Proc, és hogyan használhatók a kimenetét.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-180">Let's test it to better understand what Get-Proc can do and how its output can be used.</span></span> <span data-ttu-id="fbc9f-181">A parancssorból-parancsmagokkal kapcsolatos további információkért lásd: a [első lépések a Windows PowerShell-lel](/powershell/scripting/getting-started/getting-started-with-windows-powershell).</span><span class="sxs-lookup"><span data-stu-id="fbc9f-181">For more information about using cmdlets from the command line, see the [Getting Started with Windows PowerShell](/powershell/scripting/getting-started/getting-started-with-windows-powershell).</span></span>

1. <span data-ttu-id="fbc9f-182">Indítsa el a Windows Powershellt, és az aktuális, a számítógépen futó folyamatok beolvasása.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-182">Start Windows PowerShell, and get the current processes running on the computer.</span></span>

    ```powershell
    get-proc
    ```

    <span data-ttu-id="fbc9f-183">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-183">The following output appears.</span></span>

    ```output
    Handles  NPM(K)  PM(K)  WS(K)  VS(M)  CPU(s)  Id   ProcessName
    -------  ------  -----  -----  -----  ------  --   ----------
    254      7       7664   12048  66     173.75  1200  QCTRAY
    32       2       1372   2628   31       0.04  1860  DLG
    271      6       1216   3688   33       0.03  3816  lg
    27       2       560    1920   24       0.01  1768  TpScrex
    ...
    ```

2. <span data-ttu-id="fbc9f-184">Rendelje hozzá egy változót a parancsmag eredményei egyszerűbb kezelését.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-184">Assign a variable to the cmdlet results for easier manipulation.</span></span>

    ```powershell
    $p=get-proc
    ```

3. <span data-ttu-id="fbc9f-185">A folyamatok számát beolvasása.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-185">Get the number of processes.</span></span>

    ```powershell
    $p.length
    ```

    <span data-ttu-id="fbc9f-186">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-186">The following output appears.</span></span>

    ```output
    63
    ```

4. <span data-ttu-id="fbc9f-187">Egy adott folyamat lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-187">Retrieve a specific process.</span></span>

    ```powershell
    $p[6]
    ```

    <span data-ttu-id="fbc9f-188">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-188">The following output appears.</span></span>

    ```output
    Handles  NPM(K)  PM(K)  WS(K)  VS(M)  CPU(s)  Id    ProcessName
    -------  ------  -----  -----  -----  ------  --    -----------
    1033     3       2400   3336   35     0.53    1588  rundll32
    ```

5. <span data-ttu-id="fbc9f-189">Ez a folyamat kezdési idejét beolvasása.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-189">Get the start time of this process.</span></span>

    ```powershell
    $p[6].starttime
    ```

    <span data-ttu-id="fbc9f-190">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-190">The following output appears.</span></span>

    ```output
    Tuesday, July 26, 2005 9:34:15 AM
    ```

    ```powershell
    $p[6].starttime.dayofyear
    ```

    ```output
    207
    ```

6. <span data-ttu-id="fbc9f-191">A folyamatok, amelynek az ablakleírók száma nagyobb, mint 500 beolvasása, és rendezze az eredmény.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-191">Get the processes for which the handle count is greater than 500, and sort the result.</span></span>

    ```powershell
    $p | Where-Object {$_.HandleCount -gt 500 } | Sort-Object HandleCount
    ```

    <span data-ttu-id="fbc9f-192">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-192">The following output appears.</span></span>

    ```output
    Handles  NPM(K)  PM(K)  WS(K)  VS(M)  CPU(s)  Id   ProcessName
    -------  ------  -----  -----  -----  ------  --   ----------
    568      14      2164   4972   39     5.55    824  svchost
    716       7      2080   5332   28    25.38    468  csrss
    761      21      33060  56608  440  393.56    3300 WINWORD
    791      71      7412   4540   59     3.31    492  winlogon
    ...
    ```

7. <span data-ttu-id="fbc9f-193">Használja a `Get-Member` parancsmagot, hogy minden egyes folyamat esetében elérhető tulajdonságok listája.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-193">Use the `Get-Member` cmdlet to list the properties available for each process.</span></span>

    ```powershell
    $p | Get-Member -MemberType property
    ```

    ```output
        TypeName: System.Diagnostics.Process
    ```

    <span data-ttu-id="fbc9f-194">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="fbc9f-194">The following output appears.</span></span>

    ```output
    Name                     MemberType Definition
    ----                     ---------- ----------
    BasePriority             Property   System.Int32 BasePriority {get;}
    Container                Property   System.ComponentModel.IContainer Conta...
    EnableRaisingEvents      Property   System.Boolean EnableRaisingEvents {ge...
    ...
    ```

## <a name="see-also"></a><span data-ttu-id="fbc9f-195">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="fbc9f-195">See Also</span></span>

[<span data-ttu-id="fbc9f-196">A parancsmag parancssori bemenet feldolgozása létrehozása</span><span class="sxs-lookup"><span data-stu-id="fbc9f-196">Creating a Cmdlet to Process Command Line Input</span></span>](./adding-parameters-that-process-command-line-input.md)

[<span data-ttu-id="fbc9f-197">Adatcsatorna bemenetének feldolgozni a parancsmag létrehozása</span><span class="sxs-lookup"><span data-stu-id="fbc9f-197">Creating a Cmdlet to Process Pipeline Input</span></span>](./adding-parameters-that-process-pipeline-input.md)

[<span data-ttu-id="fbc9f-198">Hogyan hozhat létre egy Windows PowerShell-parancsmag</span><span class="sxs-lookup"><span data-stu-id="fbc9f-198">How to Create a Windows PowerShell Cmdlet</span></span>](https://msdn.microsoft.com/en-us/0d721742-c849-4d0d-964f-78ddd9cd258c)

[<span data-ttu-id="fbc9f-199">Objektumtípusok kiterjesztése és formázása</span><span class="sxs-lookup"><span data-stu-id="fbc9f-199">Extending Object Types and Formatting</span></span>](https://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[<span data-ttu-id="fbc9f-200">Hogyan működik a Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbc9f-200">How Windows PowerShell Works</span></span>](https://msdn.microsoft.com/en-us/ced30e23-10af-4700-8933-49873bd84d58)

[<span data-ttu-id="fbc9f-201">How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez</span><span class="sxs-lookup"><span data-stu-id="fbc9f-201">How to Register Cmdlets, Providers, and Host Applications</span></span>](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[<span data-ttu-id="fbc9f-202">Windows PowerShell-referencia</span><span class="sxs-lookup"><span data-stu-id="fbc9f-202">Windows PowerShell Reference</span></span>](../windows-powershell-reference.md)

[<span data-ttu-id="fbc9f-203">Parancsmag-minták</span><span class="sxs-lookup"><span data-stu-id="fbc9f-203">Cmdlet Samples</span></span>](./cmdlet-samples.md)