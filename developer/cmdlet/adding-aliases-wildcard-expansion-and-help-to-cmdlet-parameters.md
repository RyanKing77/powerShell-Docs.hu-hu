---
title: Aliasok, helyettesítő bővítése, hozzáadását és parancsmag-paraméterek segítségével |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 931ccace-c565-4a98-8dcc-df00f86394b1
caps.latest.revision: 8
ms.openlocfilehash: db664e589f625855b5a33a02c522d6b238ad2810
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62075256"
---
# <a name="adding-aliases-wildcard-expansion-and-help-to-cmdlet-parameters"></a><span data-ttu-id="653ba-102">Aliasok, helyettesítő bővítők és súgó hozzáadása a parancsmag-paraméterekhez</span><span class="sxs-lookup"><span data-stu-id="653ba-102">Adding Aliases, Wildcard Expansion, and Help to Cmdlet Parameters</span></span>

<span data-ttu-id="653ba-103">Ez a szakasz ismerteti, hogyan lehet aliasokat, helyettesítő bővítése, szeretne felvenni, és segítséget a Stop-Proc parancsmag paramétereinek üzenetek (ismertetett [létrehozása egy parancsmag, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md)).</span><span class="sxs-lookup"><span data-stu-id="653ba-103">This section describes how to add aliases, wildcard expansion, and Help messages to the parameters of the Stop-Proc cmdlet (described in [Creating a Cmdlet that Modifies the System](./creating-a-cmdlet-that-modifies-the-system.md)).</span></span>

<span data-ttu-id="653ba-104">A Stop-Proc parancsmag megkísérli leállítani a folyamatokat, amelyek a Get-Proc parancsmaggal olvassa be (ismertetett [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md)).</span><span class="sxs-lookup"><span data-stu-id="653ba-104">This Stop-Proc cmdlet attempts to stop processes that are retrieved using the Get-Proc cmdlet (described in [Creating Your First Cmdlet](./creating-a-cmdlet-without-parameters.md)).</span></span>

<span data-ttu-id="653ba-105">Ez a szakasz témakörei a következők:</span><span class="sxs-lookup"><span data-stu-id="653ba-105">Topics in this section include the following:</span></span>

- [<span data-ttu-id="653ba-106">A parancsmag meghatározása</span><span class="sxs-lookup"><span data-stu-id="653ba-106">Defining the Cmdlet</span></span>](#Defining-the-Cmdlet)

- [<span data-ttu-id="653ba-107">A rendszer módosítás paraméterek megadása</span><span class="sxs-lookup"><span data-stu-id="653ba-107">Defining Parameters for System Modification</span></span>](#Defining-Parameters-for-System-Modification)

- [<span data-ttu-id="653ba-108">A paraméter-Alias meghatározása</span><span class="sxs-lookup"><span data-stu-id="653ba-108">Defining a Parameter Alias</span></span>](#Defining-a-Parameter-Alias)

- [<span data-ttu-id="653ba-109">Paraméterek súgóját létrehozása</span><span class="sxs-lookup"><span data-stu-id="653ba-109">Creating Help for Parameters</span></span>](#Creating-Help-for-Parameters)

- [<span data-ttu-id="653ba-110">Egy bemeneti metódus feldolgozási felülbírálása</span><span class="sxs-lookup"><span data-stu-id="653ba-110">Overriding an Input Processing Method</span></span>](#Overriding-an-Input-Processing-Method)

- [<span data-ttu-id="653ba-111">Helyettesítő karakteres bővítésének támogatása</span><span class="sxs-lookup"><span data-stu-id="653ba-111">Supporting Wildcard Expansion</span></span>](#Supporting-Wildcard-Expansion)

- [<span data-ttu-id="653ba-112">Kódminta</span><span class="sxs-lookup"><span data-stu-id="653ba-112">Code Sample</span></span>](#Defining-a-Parameter-Alias)

- [<span data-ttu-id="653ba-113">Objektumtípusok definiálása és formázása</span><span class="sxs-lookup"><span data-stu-id="653ba-113">Defining Object Types and Formatting</span></span>](#Define-Object-Types-and-Formatting)

- [<span data-ttu-id="653ba-114">A parancsmag készítése</span><span class="sxs-lookup"><span data-stu-id="653ba-114">Building the Cmdlet</span></span>](#Building-the-Cmdlet)

- [<span data-ttu-id="653ba-115">A parancsmag tesztelése</span><span class="sxs-lookup"><span data-stu-id="653ba-115">Testing the Cmdlet</span></span>](#Testing-the-Cmdlet)

## <a name="defining-the-cmdlet"></a><span data-ttu-id="653ba-116">A parancsmag meghatározása</span><span class="sxs-lookup"><span data-stu-id="653ba-116">Defining the Cmdlet</span></span>

<span data-ttu-id="653ba-117">Mindig a parancsmag elnevezési és a .NET-osztály, amely megvalósítja a parancsmag deklaráló parancsmag létrehozásának első lépése.</span><span class="sxs-lookup"><span data-stu-id="653ba-117">The first step in cmdlet creation is always naming the cmdlet and declaring the .NET class that implements the cmdlet.</span></span> <span data-ttu-id="653ba-118">Kell írnia egy parancsmaggal módosíthatja, a rendszer, mert ennek megfelelően kell elnevezni azt.</span><span class="sxs-lookup"><span data-stu-id="653ba-118">Because you are writing a cmdlet to change the system, it should be named accordingly.</span></span> <span data-ttu-id="653ba-119">Ez a parancsmag rendszerfolyamatok leáll, mert a által meghatározott műveletet "Stop", használja a [System.Management.Automation.Verbslifecycle](/dotnet/api/System.Management.Automation.VerbsLifeCycle) osztályt, a főnév "Proc" folyamatot jelzi.</span><span class="sxs-lookup"><span data-stu-id="653ba-119">Because this cmdlet stops system processes, it uses the verb "Stop", defined by the [System.Management.Automation.Verbslifecycle](/dotnet/api/System.Management.Automation.VerbsLifeCycle) class, with the noun "Proc" to indicate process.</span></span> <span data-ttu-id="653ba-120">A parancsmag jóváhagyott igék kapcsolatos további információkért lásd: [művelet neve](./approved-verbs-for-windows-powershell-commands.md).</span><span class="sxs-lookup"><span data-stu-id="653ba-120">For more information about approved cmdlet verbs, see [Cmdlet Verb Names](./approved-verbs-for-windows-powershell-commands.md).</span></span>

<span data-ttu-id="653ba-121">A következő kódot a Stop-Proc parancsmag osztálydefiníció.</span><span class="sxs-lookup"><span data-stu-id="653ba-121">The following code is the class definition for this Stop-Proc cmdlet.</span></span>

```csharp
[Cmdlet(VerbsLifecycle.Stop, "proc",
        SupportsShouldProcess = true)]
public class StopProcCommand : Cmdlet
```

## <a name="defining-parameters-for-system-modification"></a><span data-ttu-id="653ba-122">A rendszer módosítás paraméterek megadása</span><span class="sxs-lookup"><span data-stu-id="653ba-122">Defining Parameters for System Modification</span></span>

<span data-ttu-id="653ba-123">A parancsmag paramétereit, a támogatási rendszer módosítását és a felhasználói visszajelzések kell.</span><span class="sxs-lookup"><span data-stu-id="653ba-123">Your cmdlet needs to define parameters that support system modifications and user feedback.</span></span> <span data-ttu-id="653ba-124">A parancsmag meg kell határoznia egy `Name` paraméter vagy ezzel egyenértékű, hogy a parancsmag fogja tudni módosítani, a rendszer valamilyen azonosítója.</span><span class="sxs-lookup"><span data-stu-id="653ba-124">The cmdlet should define a `Name` parameter or equivalent so that the cmdlet will be able to modify the system by some sort of identifier.</span></span> <span data-ttu-id="653ba-125">Emellett a parancsmag meg kell határoznia a `Force` és `PassThru` paramétereket.</span><span class="sxs-lookup"><span data-stu-id="653ba-125">In addition, the cmdlet should define the `Force` and `PassThru` parameters.</span></span> <span data-ttu-id="653ba-126">További információ ezekről a paraméterekről: [létrehozása egy parancsmag, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md).</span><span class="sxs-lookup"><span data-stu-id="653ba-126">For more information about these parameters, see [Creating a Cmdlet that Modifies the System](./creating-a-cmdlet-that-modifies-the-system.md).</span></span>

## <a name="defining-a-parameter-alias"></a><span data-ttu-id="653ba-127">A paraméter-Alias meghatározása</span><span class="sxs-lookup"><span data-stu-id="653ba-127">Defining a Parameter Alias</span></span>

<span data-ttu-id="653ba-128">A paraméter-alias lehet egy másik nevet vagy egy jól definiált levelek 1 vagy 2 levelek rövid nevét egy parancsmag-paraméterben.</span><span class="sxs-lookup"><span data-stu-id="653ba-128">A parameter alias can be an alternate name or a well-defined 1-letter or 2-letter short name for a cmdlet parameter.</span></span> <span data-ttu-id="653ba-129">Mindkét esetben az aliasok célja, hogy egyszerűsítse a parancssorból felhasználói bejegyzés.</span><span class="sxs-lookup"><span data-stu-id="653ba-129">In both cases, the goal of using aliases is to simplify user entry from the command line.</span></span> <span data-ttu-id="653ba-130">Windows PowerShell paraméter-aliasok keresztül támogatja a [System.Management.Automation.Aliasattribute](/dotnet/api/System.Management.Automation.AliasAttribute) attribútuma, amely a deklaráció szintaxisa [Alias()].</span><span class="sxs-lookup"><span data-stu-id="653ba-130">Windows PowerShell supports parameter aliases through the [System.Management.Automation.Aliasattribute](/dotnet/api/System.Management.Automation.AliasAttribute) attribute, which uses the declaration syntax [Alias()].</span></span>

<span data-ttu-id="653ba-131">A következő kód bemutatja, hogyan alias adnak hozzá a `Name` paraméter.</span><span class="sxs-lookup"><span data-stu-id="653ba-131">The following code shows how an alias is added to the `Name` parameter.</span></span>

```csharp
/// <summary>
/// Specify the mandatory Name parameter used to identify the
/// processes to be stopped.
/// </summary>
[Parameter(
           Position = 0,
           Mandatory = true,
           ValueFromPipeline = true,
           ValueFromPipelineByPropertyName = true,
           HelpMessage = "The name of one or more processes to stop. Wildcards are permitted."
)]
[Alias("ProcessName")]
public string[] Name
{
  get { return processNames; }
  set { processNames = value; }
}
private string[] processNames;
```

<span data-ttu-id="653ba-132">Használata mellett a [System.Management.Automation.Aliasattribute](/dotnet/api/System.Management.Automation.AliasAttribute) attribútum, a Windows PowerShell-futtatókörnyezet végzi a részleges névegyeztetés, még akkor is, ha nincsenek aliasok vannak megadva.</span><span class="sxs-lookup"><span data-stu-id="653ba-132">In addition to using the [System.Management.Automation.Aliasattribute](/dotnet/api/System.Management.Automation.AliasAttribute) attribute, the Windows PowerShell runtime performs partial name matching, even if no aliases are specified.</span></span> <span data-ttu-id="653ba-133">Például, ha a parancsmag rendelkezik egy `FileName` és, hogy a csak paraméter kezdetű `F`, adja meg a felhasználó `Filename`, `Filenam`, `File`, `Fi`, vagy `F` és továbbra is ismeri fel a bejegyzést a `FileName` paraméter.</span><span class="sxs-lookup"><span data-stu-id="653ba-133">For example, if your cmdlet has a `FileName` parameter and that is the only parameter that starts with `F`, the user could enter `Filename`, `Filenam`, `File`, `Fi`, or `F` and still recognize the entry as the `FileName` parameter.</span></span>

## <a name="creating-help-for-parameters"></a><span data-ttu-id="653ba-134">Paraméterek súgóját létrehozása</span><span class="sxs-lookup"><span data-stu-id="653ba-134">Creating Help for Parameters</span></span>

<span data-ttu-id="653ba-135">Windows PowerShell parancsmag-paraméterek súgó létrehozása teszi lehetővé.</span><span class="sxs-lookup"><span data-stu-id="653ba-135">Windows PowerShell allows you to create Help for cmdlet parameters.</span></span> <span data-ttu-id="653ba-136">Ehhez a rendszer módosítás- és felhasználói visszajelzési használt bármelyik paraméternél.</span><span class="sxs-lookup"><span data-stu-id="653ba-136">Do this for any parameter used for system modification and user feedback.</span></span> <span data-ttu-id="653ba-137">Súgó támogatásához minden egyes paraméterhez beállíthat a `HelpMessage` kulcsszó az attribútum a [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) deklarace attribútum.</span><span class="sxs-lookup"><span data-stu-id="653ba-137">For each parameter to support Help, you can set the `HelpMessage` attribute keyword in the [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) attribute declaration.</span></span> <span data-ttu-id="653ba-138">Ezt a kulcsszót a szöveg megjelenítése a felhasználónak, ha segítségre van szüksége a paraméter használatával határozza meg.</span><span class="sxs-lookup"><span data-stu-id="653ba-138">This keyword defines the text to display to the user for assistance in using the parameter.</span></span> <span data-ttu-id="653ba-139">Is beállíthat a `HelpMessageBaseName` kulcsszó egy erőforrást használja, az üzenet alapneveként azonosításához.</span><span class="sxs-lookup"><span data-stu-id="653ba-139">You can also set the `HelpMessageBaseName` keyword to identify the base name of a resource to use for the message.</span></span> <span data-ttu-id="653ba-140">Ha ezt a kulcsszót, is meg kell adni a `HelpMessageResourceId` kulcsszó használatával adja meg az erőforrás-azonosítója.</span><span class="sxs-lookup"><span data-stu-id="653ba-140">If you set this keyword, you must also set the `HelpMessageResourceId` keyword to specify the resource identifier.</span></span>

<span data-ttu-id="653ba-141">A következő kódot a Stop-Proc parancsmag az határozza meg a `HelpMessage` attribútum kulcsszó a `Name` paraméter.</span><span class="sxs-lookup"><span data-stu-id="653ba-141">The following code from this Stop-Proc cmdlet defines the `HelpMessage` attribute keyword for the `Name` parameter.</span></span>

```csharp
/// <summary>
/// Specify the mandatory Name parameter used to identify the
/// processes to be stopped.
/// </summary>
[Parameter(
           Position = 0,
           Mandatory = true,
           ValueFromPipeline = true,
           ValueFromPipelineByPropertyName = true,
           HelpMessage = "The name of one or more processes to stop. Wildcards are permitted."
)]
```

## <a name="overriding-an-input-processing-method"></a><span data-ttu-id="653ba-142">Egy bemeneti metódus feldolgozási felülbírálása</span><span class="sxs-lookup"><span data-stu-id="653ba-142">Overriding an Input Processing Method</span></span>

<span data-ttu-id="653ba-143">A parancsmag felül kell írnia egy bemeneti metódus feldolgozása, a leggyakrabban ez lesz [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord).</span><span class="sxs-lookup"><span data-stu-id="653ba-143">Your cmdlet must override an input processing method, most often this will be [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord).</span></span> <span data-ttu-id="653ba-144">Ha módosítja a rendszer, a parancsmag meg kell hívnia a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) és [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) módszereket, hogy a felhasználó Ha visszajelzést előtt módosításakor.</span><span class="sxs-lookup"><span data-stu-id="653ba-144">When modifying the system, the cmdlet should call the [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) and [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) methods to allow the user to provide feedback before a change is made.</span></span> <span data-ttu-id="653ba-145">Ezek a metódusok kapcsolatos további információkért lásd: [létrehozása egy parancsmag, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md).</span><span class="sxs-lookup"><span data-stu-id="653ba-145">For more information about these methods, see [Creating a Cmdlet that Modifies the System](./creating-a-cmdlet-that-modifies-the-system.md).</span></span>

## <a name="supporting-wildcard-expansion"></a><span data-ttu-id="653ba-146">Helyettesítő karakteres bővítésének támogatása</span><span class="sxs-lookup"><span data-stu-id="653ba-146">Supporting Wildcard Expansion</span></span>

<span data-ttu-id="653ba-147">Ahhoz, hogy a kijelölt objektumok több, a parancsmag használható a [System.Management.Automation.Wildcardpattern](/dotnet/api/System.Management.Automation.WildcardPattern) és [System.Management.Automation.Wildcardoptions](/dotnet/api/System.Management.Automation.WildcardOptions) biztosít osztályok bemeneti paraméter helyettesítő bővítésének támogatása.</span><span class="sxs-lookup"><span data-stu-id="653ba-147">To allow the selection of multiple objects, your cmdlet can use the [System.Management.Automation.Wildcardpattern](/dotnet/api/System.Management.Automation.WildcardPattern) and [System.Management.Automation.Wildcardoptions](/dotnet/api/System.Management.Automation.WildcardOptions) classes to provide wildcard expansion support for parameter input.</span></span> <span data-ttu-id="653ba-148">Helyettesítő karakterek mintái példák lsa \* \*.txt és [a – c]\*.</span><span class="sxs-lookup"><span data-stu-id="653ba-148">Examples of wildcard patterns are lsa\*, \*.txt, and [a-c]\*.</span></span> <span data-ttu-id="653ba-149">Akkor használják, karakteréhez escape-karakter a biztonsági idézőjelet ('), amikor a minta szó szerint használandó karaktert tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="653ba-149">Use the back-quote character (\`) as an escape character when the pattern contains a character that should be used literally.</span></span>

<span data-ttu-id="653ba-150">Fájl elérési útja és neve helyettesítő bővülésből példák gyakori forgatókönyvek, ahol lehetséges, hogy szeretné, a parancsmag is lehetővé teszik az elérési út bemenetek támogatása, ha több objektum kiválasztásának megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="653ba-150">Wildcard expansions of file and path names are examples of common scenarios where the cmdlet may want to allow support for path inputs when the selection of multiple objects is required.</span></span> <span data-ttu-id="653ba-151">Gyakori eset a fájlrendszer, ahol a felhasználó szeretné látni a az aktuális mappában található összes fájl szerepel.</span><span class="sxs-lookup"><span data-stu-id="653ba-151">A common case is in the file system, where a user wants to see all files residing in the current folder.</span></span>

<span data-ttu-id="653ba-152">A testre szabott helyettesítő minta egyező megvalósítás csak ritkán kell.</span><span class="sxs-lookup"><span data-stu-id="653ba-152">You should need a customized wildcard pattern matching implementation only rarely.</span></span> <span data-ttu-id="653ba-153">A parancsmag ebben az esetben támogatnia kell a teljes POSIX 1003.2, 3.13 specifikáció helyettesítő bővítés céljából, vagy a következő egyszerűsített részére:</span><span class="sxs-lookup"><span data-stu-id="653ba-153">In this case, your cmdlet should support either the full POSIX 1003.2, 3.13 specification for wildcard expansion or the following simplified subset:</span></span>

- <span data-ttu-id="653ba-154">**A kérdőjel (?).**</span><span class="sxs-lookup"><span data-stu-id="653ba-154">**Question mark (?).**</span></span> <span data-ttu-id="653ba-155">Egyeztet bármilyen karaktert, a megadott helyen.</span><span class="sxs-lookup"><span data-stu-id="653ba-155">Matches any character at the specified location.</span></span>

- <span data-ttu-id="653ba-156">**Csillag (\*).**</span><span class="sxs-lookup"><span data-stu-id="653ba-156">**Asterisk (\*).**</span></span> <span data-ttu-id="653ba-157">A megadott helyen indítása nulla vagy több karakterre illeszkedik.</span><span class="sxs-lookup"><span data-stu-id="653ba-157">Matches zero or more characters starting at the specified location.</span></span>

- <span data-ttu-id="653ba-158">**Nyitó zárójel ([]).**</span><span class="sxs-lookup"><span data-stu-id="653ba-158">**Open bracket ([).**</span></span> <span data-ttu-id="653ba-159">Egy minta zárójel kifejezés, amely vagy egy karaktertartományt tartalmazhat mutatja be.</span><span class="sxs-lookup"><span data-stu-id="653ba-159">Introduces a pattern bracket expression that can contain characters or a range of characters.</span></span> <span data-ttu-id="653ba-160">Tartomány megadása kötelező, ha a kötőjelet (-) jelzi a tartomány szolgál.</span><span class="sxs-lookup"><span data-stu-id="653ba-160">If a range is required, a hyphen (-) is used to indicate the range.</span></span>

- <span data-ttu-id="653ba-161">**Záró zárójel (]).**</span><span class="sxs-lookup"><span data-stu-id="653ba-161">**Close bracket (]).**</span></span> <span data-ttu-id="653ba-162">Egy minta zárójel kifejezés befejeződik.</span><span class="sxs-lookup"><span data-stu-id="653ba-162">Ends a pattern bracket expression.</span></span>

- <span data-ttu-id="653ba-163">**Ajánlat vissza escape-karaktert (').**</span><span class="sxs-lookup"><span data-stu-id="653ba-163">**Back-quote escape character (\`).**</span></span> <span data-ttu-id="653ba-164">Azt jelzi, hogy a következő karaktert szó szerint kell tenni.</span><span class="sxs-lookup"><span data-stu-id="653ba-164">Indicates that the next character should be taken literally.</span></span> <span data-ttu-id="653ba-165">Vegye figyelembe, hogy a biztonsági-idézőjelet (programozott módon megadása) szemben a parancssorból megadásakor a vissza-ajánlat escape-karakter meg kell adni kétszer.</span><span class="sxs-lookup"><span data-stu-id="653ba-165">Be aware that when specifying the back-quote character from the command line (as opposed to specifying it programmatically), the back-quote escape character must be specified twice.</span></span>

> [!NOTE]
> <span data-ttu-id="653ba-166">Helyettesítő karakterek mintái kapcsolatos további információkért lásd: [helyettesítő karaktereket támogató parancsmag-paraméterek](./supporting-wildcard-characters-in-cmdlet-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="653ba-166">For more information about wildcard patterns, see [Supporting Wildcards in Cmdlet Parameters](./supporting-wildcard-characters-in-cmdlet-parameters.md).</span></span>

<span data-ttu-id="653ba-167">A következő kód bemutatja, hogyan helyettesítő beállítások megadása és definiálása a helyettesítő karakterrel feloldásához használt a `Name` parancsmag paraméter.</span><span class="sxs-lookup"><span data-stu-id="653ba-167">The following code shows how to set wildcard options and define the wildcard pattern used for resolving the `Name` parameter for this cmdlet.</span></span>

```csharp
WildcardOptions options = WildcardOptions.IgnoreCase |
                          WildcardOptions.Compiled;
WildcardPattern wildcard = new WildcardPattern(name,options);
```

<span data-ttu-id="653ba-168">A következő kód bemutatja tesztelése, hogy a folyamat neve megegyezik-e a meghatározott helyettesítő karakterrel.</span><span class="sxs-lookup"><span data-stu-id="653ba-168">The following code shows how to test whether the process name matches the defined wildcard pattern.</span></span> <span data-ttu-id="653ba-169">Figyelje meg, hogy, ebben az esetben a folyamat neve nem egyezik meg a mintát, ha a parancsmag továbbra is a következő folyamat nevét.</span><span class="sxs-lookup"><span data-stu-id="653ba-169">Notice that, in this case, if the process name does not match the pattern, the cmdlet continues on to get the next process name.</span></span>

```csharp
if (!wildcard.IsMatch(processName))
{
  continue;
}
```

## <a name="code-sample"></a><span data-ttu-id="653ba-170">Kódminta</span><span class="sxs-lookup"><span data-stu-id="653ba-170">Code Sample</span></span>

<span data-ttu-id="653ba-171">A teljes C# mintakód, lásd: [StopProcessSample03 minta](./stopprocesssample03-sample.md).</span><span class="sxs-lookup"><span data-stu-id="653ba-171">For the complete C# sample code, see [StopProcessSample03 Sample](./stopprocesssample03-sample.md).</span></span>

## <a name="define-object-types-and-formatting"></a><span data-ttu-id="653ba-172">Objektumtípusok és formázása</span><span class="sxs-lookup"><span data-stu-id="653ba-172">Define Object Types and Formatting</span></span>

<span data-ttu-id="653ba-173">Windows PowerShell parancsmagok használatával a .net-objektumokká közötti továbbítja.</span><span class="sxs-lookup"><span data-stu-id="653ba-173">Windows PowerShell passes information between cmdlets using .Net objects.</span></span> <span data-ttu-id="653ba-174">Ennek következtében a parancsmag előfordulhat, hogy meg kell határoznia a saját típusát, vagy a parancsmag előfordulhat, hogy ki kell terjesztenie egy másik parancsmag által biztosított meglévő típus.</span><span class="sxs-lookup"><span data-stu-id="653ba-174">Consequently, a cmdlet may need to define its own type, or the cmdlet may need to extend an existing type provided by another cmdlet.</span></span> <span data-ttu-id="653ba-175">Új típusok meghatározása, vagy meglévő típusok bővítésével kapcsolatos további információkért lásd: [objektumtípusok kiterjesztése és formázás](https://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).</span><span class="sxs-lookup"><span data-stu-id="653ba-175">For more information about defining new types or extending existing types, see [Extending Object Types and Formatting](https://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).</span></span>

## <a name="building-the-cmdlet"></a><span data-ttu-id="653ba-176">A parancsmag készítése</span><span class="sxs-lookup"><span data-stu-id="653ba-176">Building the Cmdlet</span></span>

<span data-ttu-id="653ba-177">Parancsmag-k megvalósítása után regisztrálni kell a Windows PowerShell-lel a Windows PowerShell beépülő modullal.</span><span class="sxs-lookup"><span data-stu-id="653ba-177">After implementing a cmdlet, it must be registered with Windows PowerShell through a Windows PowerShell snap-in.</span></span> <span data-ttu-id="653ba-178">Parancsmagok regisztrálásával kapcsolatos további információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).</span><span class="sxs-lookup"><span data-stu-id="653ba-178">For more information about registering cmdlets, see [How to Register Cmdlets, Providers, and Host Applications](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).</span></span>

## <a name="testing-the-cmdlet"></a><span data-ttu-id="653ba-179">A parancsmag tesztelése</span><span class="sxs-lookup"><span data-stu-id="653ba-179">Testing the Cmdlet</span></span>

<span data-ttu-id="653ba-180">Ha a parancsmagot a Windows PowerShell-lel regisztrálva lett, azt a parancssorból való futtatásával tesztelheti.</span><span class="sxs-lookup"><span data-stu-id="653ba-180">When your cmdlet has been registered with Windows PowerShell, you can test it by running it on the command line.</span></span> <span data-ttu-id="653ba-181">Most tesztelje a parancsmagra állítsa le a folyamaton.</span><span class="sxs-lookup"><span data-stu-id="653ba-181">Let's test the sample Stop-Proc cmdlet.</span></span> <span data-ttu-id="653ba-182">A parancssorból-parancsmagokkal kapcsolatos további információkért lásd: a [első lépések a Windows PowerShell-lel](/powershell/scripting/getting-started/getting-started-with-windows-powershell).</span><span class="sxs-lookup"><span data-stu-id="653ba-182">For more information about using cmdlets from the command line, see the [Getting Started with Windows PowerShell](/powershell/scripting/getting-started/getting-started-with-windows-powershell).</span></span>

- <span data-ttu-id="653ba-183">Indítsa el a Windows Powershellt, és állítsa le a folyamaton segítségével egy folyamatot a Folyamatnév alias használatával állítsa le a `Name` paraméter.</span><span class="sxs-lookup"><span data-stu-id="653ba-183">Start Windows PowerShell and use Stop-Proc to stop a process using the ProcessName alias for the `Name` parameter.</span></span>

    ```powershell
    PS> stop-proc -ProcessName notepad
    ```

<span data-ttu-id="653ba-184">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="653ba-184">The following output appears.</span></span>

    ```
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "notepad (3496)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y
    ```

- <span data-ttu-id="653ba-185">Győződjön meg a következő bejegyzést a parancssoron.</span><span class="sxs-lookup"><span data-stu-id="653ba-185">Make the following entry on the command line.</span></span> <span data-ttu-id="653ba-186">A Name paraméter megadása kötelező, mivel azt kéri.</span><span class="sxs-lookup"><span data-stu-id="653ba-186">Because the Name parameter is mandatory, you are prompted for it.</span></span> <span data-ttu-id="653ba-187">Írja be "!"</span><span class="sxs-lookup"><span data-stu-id="653ba-187">Entering "!?"</span></span> <span data-ttu-id="653ba-188">Megjeleníti a paraméter kapcsolódó súgószöveg.</span><span class="sxs-lookup"><span data-stu-id="653ba-188">brings up the help text associated with the parameter.</span></span>

    ```powershell
    PS> stop-proc
    ```

<span data-ttu-id="653ba-189">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="653ba-189">The following output appears.</span></span>

    ```
    Cmdlet stop-proc at command pipeline position 1
    Supply values for the following parameters:
    (Type !? for Help.)
    Name[0]: !?
    The name of one or more processes to stop. Wildcards are permitted.
    Name[0]: notepad
    ```

- <span data-ttu-id="653ba-190">Most ellenőrizze az összes folyamat, amely megfelel a helyettesítő karakteres mintának leállítani a következő bejegyzés "\* Megjegyzés\*".</span><span class="sxs-lookup"><span data-stu-id="653ba-190">Now make the following entry to stop all processes that match the wildcard pattern "\*note\*".</span></span> <span data-ttu-id="653ba-191">Minden egyes folyamat, amely megfelel a mintának leállítása előtt a rendszer kéri.</span><span class="sxs-lookup"><span data-stu-id="653ba-191">You are prompted before stopping each process that matches the pattern.</span></span>

    ```powershell
    PS> stop-proc -Name *note*
    ```

<span data-ttu-id="653ba-192">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="653ba-192">The following output appears.</span></span>

    ```
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "notepad (1112)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y
    ```

<span data-ttu-id="653ba-193">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="653ba-193">The following output appears.</span></span>

    ```
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "ONENOTEM (3712)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): N
    ```

<span data-ttu-id="653ba-194">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="653ba-194">The following output appears.</span></span>

    ```
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "ONENOTE (3592)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): N
    ```

## <a name="see-also"></a><span data-ttu-id="653ba-195">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="653ba-195">See Also</span></span>

[<span data-ttu-id="653ba-196">Hozzon létre egy parancsmag, amely módosítja a rendszer</span><span class="sxs-lookup"><span data-stu-id="653ba-196">Create a Cmdlet that Modifies the System</span></span>](./creating-a-cmdlet-that-modifies-the-system.md)

[<span data-ttu-id="653ba-197">Hogyan hozhat létre egy Windows PowerShell-parancsmag</span><span class="sxs-lookup"><span data-stu-id="653ba-197">How to Create a Windows PowerShell Cmdlet</span></span>](https://msdn.microsoft.com/en-us/0d721742-c849-4d0d-964f-78ddd9cd258c)

[<span data-ttu-id="653ba-198">Objektumtípusok kiterjesztése és formázása</span><span class="sxs-lookup"><span data-stu-id="653ba-198">Extending Object Types and Formatting</span></span>](https://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[<span data-ttu-id="653ba-199">How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez</span><span class="sxs-lookup"><span data-stu-id="653ba-199">How to Register Cmdlets, Providers, and Host Applications</span></span>](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[<span data-ttu-id="653ba-200">A helyettesítő karakterek támogató parancsmag-paraméterek</span><span class="sxs-lookup"><span data-stu-id="653ba-200">Supporting Wildcards in Cmdlet Parameters</span></span>](./supporting-wildcard-characters-in-cmdlet-parameters.md)

[<span data-ttu-id="653ba-201">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="653ba-201">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
