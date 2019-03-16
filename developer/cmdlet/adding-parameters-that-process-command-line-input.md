---
title: Parancssori bemenet feldolgozása-paramétereket adunk hozzá |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cmdlets [PowerShell Programmer's Guide], parameters
- Get-Proc cmdlet [PowerShell Programmer's Guide]
- cmdlets [PowerShell Programmer's Guide], command line input
- command line input [PowerShell Programmer's Guide]
- parameters [PowerShell Programmer's Guide]
- cmdlets [PowerShell Programmer's Guide], creating
ms.assetid: da0b32f8-7b51-440e-a061-3177b5759e0e
caps.latest.revision: 9
ms.openlocfilehash: fb113086ce89e4becff9bcaf3232905fde2bf610
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58055920"
---
# <a name="adding-parameters-that-process-command-line-input"></a><span data-ttu-id="3c6e8-102">Parancssori bemenetet feldolgozó paraméterek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="3c6e8-102">Adding Parameters That Process Command-Line Input</span></span>

<span data-ttu-id="3c6e8-103">A parancsmag bemenete egy forrása a parancssorból.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-103">One source of input for a cmdlet is the command line.</span></span> <span data-ttu-id="3c6e8-104">Ez a témakör ismerteti, hogyan adhat hozzá egy paramétert a **Get-Proc** parancsmag (amely leírt [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md)), hogy a parancsmag bemeneti a helyi számítógépről explicit alapján tud feldolgozni. a parancsmagnak átadott objektum.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-104">This topic describes how to add a parameter to the **Get-Proc** cmdlet (which is described in [Creating Your First Cmdlet](./creating-a-cmdlet-without-parameters.md)) so that the cmdlet can process input from the local computer based on explicit objects passed to the cmdlet.</span></span> <span data-ttu-id="3c6e8-105">A **Get-Proc** leírt parancsmag itt lekéri a nevük alapján folyamatok, majd megjeleníti a a folyamatokra vonatkozó parancsot a parancssorba.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-105">The **Get-Proc** cmdlet described here retrieves processes based on their names, and then displays information about the processes at a command prompt.</span></span>

<span data-ttu-id="3c6e8-106">A következő szakaszok ebben a témakörben a következők:</span><span class="sxs-lookup"><span data-stu-id="3c6e8-106">The following sections are in this topic:</span></span>

- [<span data-ttu-id="3c6e8-107">A parancsmag osztály meghatározása</span><span class="sxs-lookup"><span data-stu-id="3c6e8-107">Defining the Cmdlet Class</span></span>](#Defining-the-Cmdlet-Class)

- [<span data-ttu-id="3c6e8-108">Paraméterek deklaráló</span><span class="sxs-lookup"><span data-stu-id="3c6e8-108">Declaring Parameters</span></span>](#Declaring-Parameters)

- [<span data-ttu-id="3c6e8-109">Támogató paraméter ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="3c6e8-109">Supporting Parameter Validation</span></span>](#Supporting-Parameter-Validation)

- [<span data-ttu-id="3c6e8-110">Egy bemeneti metódus feldolgozási felülbírálása</span><span class="sxs-lookup"><span data-stu-id="3c6e8-110">Overriding an Input Processing Method</span></span>](#Overriding-an-Input-Processing-Method)

- [<span data-ttu-id="3c6e8-111">Kódminta</span><span class="sxs-lookup"><span data-stu-id="3c6e8-111">Code Sample</span></span>](#Code-Sample)

- [<span data-ttu-id="3c6e8-112">Objektumtípusok definiálása és formázása</span><span class="sxs-lookup"><span data-stu-id="3c6e8-112">Defining Object Types and Formatting</span></span>](#Defining-Object-Types-and-Formatting)

- [<span data-ttu-id="3c6e8-113">A parancsmag készítése</span><span class="sxs-lookup"><span data-stu-id="3c6e8-113">Building the Cmdlet</span></span>](#Building-the-Cmdlet)

- [<span data-ttu-id="3c6e8-114">A parancsmag tesztelése</span><span class="sxs-lookup"><span data-stu-id="3c6e8-114">Testing the Cmdlet</span></span>](#Testing-the-Cmdlet)

## <a name="defining-the-cmdlet-class"></a><span data-ttu-id="3c6e8-115">A parancsmag osztály meghatározása</span><span class="sxs-lookup"><span data-stu-id="3c6e8-115">Defining the Cmdlet Class</span></span>

<span data-ttu-id="3c6e8-116">A parancsmag létrehozásának első lépése elnevezési parancsmag és a .NET-keretrendszer osztály, amely megvalósítja a parancsmag a nyilatkozat.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-116">The first step in cmdlet creation is cmdlet naming and the declaration of the .NET Framework class that implements the cmdlet.</span></span> <span data-ttu-id="3c6e8-117">Ez a parancsmag folyamat adatait, kérdezi le, így az itt választott művelet neve "Get".</span><span class="sxs-lookup"><span data-stu-id="3c6e8-117">This cmdlet retrieves process information, so the verb name chosen here is "Get."</span></span> <span data-ttu-id="3c6e8-118">(A szinte bármilyen rendezési parancsmag, amely képes adatok beolvasása a parancssori bemenet tud feldolgozni.) A parancsmag jóváhagyott igék kapcsolatos további információkért lásd: [művelet neve](./approved-verbs-for-windows-powershell-commands.md).</span><span class="sxs-lookup"><span data-stu-id="3c6e8-118">(Almost any sort of cmdlet that is capable of retrieving information can process command-line input.) For more information about approved cmdlet verbs, see [Cmdlet Verb Names](./approved-verbs-for-windows-powershell-commands.md).</span></span>

<span data-ttu-id="3c6e8-119">Íme az osztálydeklaráció számára a **Get-Proc** parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-119">Here's the class declaration for the **Get-Proc** cmdlet.</span></span> <span data-ttu-id="3c6e8-120">Ez a definíció kapcsolatos részletes információkat [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="3c6e8-120">Details about this definition are provided in [Creating Your First Cmdlet](./creating-a-cmdlet-without-parameters.md).</span></span>

```csharp
[Cmdlet(VerbsCommon.Get, "proc")]
public class GetProcCommand: Cmdlet
```

```vb
<Cmdlet(VerbsCommon.Get, "Proc")> _
Public Class GetProcCommand
    Inherits Cmdlet
```

## <a name="declaring-parameters"></a><span data-ttu-id="3c6e8-121">Paraméterek deklaráló</span><span class="sxs-lookup"><span data-stu-id="3c6e8-121">Declaring Parameters</span></span>

<span data-ttu-id="3c6e8-122">Egy parancsmag-paraméterben lehetővé teszi, hogy a felhasználó számára információk megadása a parancsmaghoz.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-122">A cmdlet parameter enables the user to provide input to the cmdlet.</span></span> <span data-ttu-id="3c6e8-123">A következő példában **Get-Proc** és `Get-Member` átadott parancsmagok nevei és `MemberType` egy paraméter a `Get-Member` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-123">In the following example, **Get-Proc** and `Get-Member` are the names of pipelined cmdlets, and `MemberType` is a parameter for the `Get-Member` cmdlet.</span></span> <span data-ttu-id="3c6e8-124">A paraméter argumentuma a "property".</span><span class="sxs-lookup"><span data-stu-id="3c6e8-124">The parameter has the argument "property."</span></span>

<span data-ttu-id="3c6e8-125">**PS > get-proc; `get-member` - membertype tulajdonság**</span><span class="sxs-lookup"><span data-stu-id="3c6e8-125">**PS> get-proc ; `get-member` -membertype property**</span></span>

<span data-ttu-id="3c6e8-126">Deklarálja a parancsmag paraméterei, először meg kell határoznia a tulajdonságokat, amelyek a paramétereket.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-126">To declare parameters for a cmdlet, you must first define the properties that represent the parameters.</span></span> <span data-ttu-id="3c6e8-127">Az a **Get-Proc** , a parancsmag csak paraméter `Name`, amely ebben az esetben a .NET-keretrendszer folyamat lekérni kívánt objektum nevét jelöli.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-127">In the **Get-Proc** cmdlet, the only parameter is `Name`, which in this case represents the name of the .NET Framework process object to retrieve.</span></span> <span data-ttu-id="3c6e8-128">Ezért a parancsmag osztály nevének tömbjét fogadására karakterlánc típusú tulajdonsága határozza meg.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-128">Therefore, the cmdlet class defines a property of type string to accept an array of names.</span></span>

<span data-ttu-id="3c6e8-129">Íme a paraméterdeklarációhoz a a `Name` paraméterében a **Get-Proc** parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-129">Here's the parameter declaration for the `Name` parameter of the **Get-Proc** cmdlet.</span></span>

```csharp
/// <summary>
/// Specify the cmdlet Name parameter.
/// </summary>
  [Parameter(Position = 0)]
  [ValidateNotNullOrEmpty]
  public string[] Name
  {
    get { return processNames; }
    set { processNames = value; }
  }
  private string[] processNames;

  #endregion Parameters
```

```vb
<Parameter(Position:=0), ValidateNotNullOrEmpty()> _
Public Property Name() As String()
    Get
        Return processNames
    End Get

    Set(ByVal value As String())
        processNames = value
    End Set

End Property
```

<span data-ttu-id="3c6e8-130">A Windows PowerShell-modult, amely Ez a tulajdonság tájékoztatja a `Name` paramétert, egy [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) attribútummal egészül ki a tulajdonság meghatározása.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-130">To inform the Windows PowerShell runtime that this property is the `Name` parameter, a [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) attribute is added to the property definition.</span></span> <span data-ttu-id="3c6e8-131">Alapszintű szintaxis miatt ez az attribútum `[Parameter()]`.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-131">The basic syntax for declaring this attribute is `[Parameter()]`.</span></span>

> [!NOTE]
> <span data-ttu-id="3c6e8-132">Egy paraméter fel kell tüntetni explicit módon is nyilvános.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-132">A parameter must be explicitly marked as public.</span></span> <span data-ttu-id="3c6e8-133">Nem nyilvános, belső alapértelmezett vannak megjelölve, és a Windows PowerShell-modul nem találhatók paraméterek.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-133">Parameters that are not marked as public default to internal and are not found by the Windows PowerShell runtime.</span></span>

<span data-ttu-id="3c6e8-134">Ezt a parancsmagot használja a karakterláncok a `Name` paraméter.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-134">This cmdlet uses an array of strings for the `Name` parameter.</span></span> <span data-ttu-id="3c6e8-135">Ha lehetséges a parancsmaghoz is meg kell határozniuk paraméter egy tömb, mert ez lehetővé teszi a parancsmagot, amely egynél több elem fogadja el.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-135">If possible, your cmdlet should also define a parameter as an array, because this allows the cmdlet to accept more than one item.</span></span>

#### <a name="things-to-remember-about-parameter-definitions"></a><span data-ttu-id="3c6e8-136">Megjegyzendő Paraméterdefiníciókra kapcsolatos tudnivalók</span><span class="sxs-lookup"><span data-stu-id="3c6e8-136">Things to Remember About Parameter Definitions</span></span>

- <span data-ttu-id="3c6e8-137">Előre meghatározott Windows PowerShell paraméter nevükkel és adattípusukkal kell annak biztosításához, hogy a parancsmag kompatibilis a Windows PowerShell-parancsmagok, a lehetséges használható újra.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-137">Predefined Windows PowerShell parameter names and data types should be reused as much as possible to ensure that your cmdlet is compatible with Windows PowerShell cmdlets.</span></span> <span data-ttu-id="3c6e8-138">Például, ha az összes parancsmagot használja az előre definiált `Id` paraméternév egy erőforrást, a felhasználó fog könnyedén azonosíthatja a paramétert, függetlenül attól, milyen parancsmagot használják szerinti ismertetése.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-138">For example, if all cmdlets use the predefined `Id` parameter name to identify a resource, user will easily understand the meaning of the parameter, regardless of what cmdlet they are using.</span></span> <span data-ttu-id="3c6e8-139">Paraméterek nevei alapvetően ugyanazokat a szabályokat használ a közös nyelvi futtatókörnyezet (CLR) a változók nevében hajtsa végre.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-139">Basically, parameter names follow the same rules as those used for variable names in the common language runtime (CLR).</span></span> <span data-ttu-id="3c6e8-140">A paraméter elnevezésével kapcsolatos további információkért lásd: [parancsmag-paraméterek nevei](https://msdn.microsoft.com/en-us/c4500737-0a05-4d01-911b-394424c65bfb).</span><span class="sxs-lookup"><span data-stu-id="3c6e8-140">For more information about parameter naming, see [Cmdlet Parameter Names](https://msdn.microsoft.com/en-us/c4500737-0a05-4d01-911b-394424c65bfb).</span></span>

- <span data-ttu-id="3c6e8-141">Windows PowerShell fenntart egy egységes felhasználói élmény érdekében néhány paraméterek nevei.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-141">Windows PowerShell reserves a few parameter names to provide a consistent user experience.</span></span> <span data-ttu-id="3c6e8-142">Ne használja a következő paraméter neve: `WhatIf`, `Confirm`, `Verbose`, `Debug`, `Warn`, `ErrorAction`, `ErrorVariable`, `OutVariable`, és `OutBuffer`.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-142">Do not use these parameter names: `WhatIf`, `Confirm`, `Verbose`, `Debug`, `Warn`, `ErrorAction`, `ErrorVariable`, `OutVariable`, and `OutBuffer`.</span></span> <span data-ttu-id="3c6e8-143">Ezenkívül ezek a paraméterek nevei a következő aliasok vannak fenntartva: `vb`, `db`, `ea`, `ev`, `ov`, és `ob`.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-143">Additionally, the following aliases for these parameter names are reserved: `vb`, `db`, `ea`, `ev`, `ov`, and `ob`.</span></span>

- <span data-ttu-id="3c6e8-144">`Name` van egy egyszerű és közös paraméter neve, a parancsmagok használata ajánlott.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-144">`Name` is a simple and common parameter name, recommended for use in your cmdlets.</span></span> <span data-ttu-id="3c6e8-145">Célszerűbb válassza ki a paraméter neve, mint egy összetett nevét, amely egy adott parancsmag egyedi, és nehéz megjegyezni ehhez hasonló.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-145">It is better to choose a parameter name like this than a complex name that is unique to a specific cmdlet and hard to remember.</span></span>

- <span data-ttu-id="3c6e8-146">Paramétereket is kis-és a Windows PowerShellben, noha alapértelmezés szerint a rendszerhéj megőrzi az esetet.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-146">Parameters are case-insensitive in Windows PowerShell, although by default the shell preserves case.</span></span> <span data-ttu-id="3c6e8-147">Kisbetű/nagybetű megkülönböztetése argumentum attól függ, hogy a parancsmag a műveletet.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-147">Case-sensitivity of the arguments depends on the operation of the cmdlet.</span></span> <span data-ttu-id="3c6e8-148">Megadott parancssori argumentumot továbbítson a paramétert.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-148">Arguments are passed to a parameter as specified at the command line.</span></span>

- <span data-ttu-id="3c6e8-149">Más paraméter deklarációinak példákért lásd [parancsmag-paraméterek](./cmdlet-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="3c6e8-149">For examples of other parameter declarations, see [Cmdlet Parameters](./cmdlet-parameters.md).</span></span>

## <a name="declaring-parameters-as-positional-or-named"></a><span data-ttu-id="3c6e8-150">A Helyzetbeállító vagy elnevezett paraméterek deklaráló</span><span class="sxs-lookup"><span data-stu-id="3c6e8-150">Declaring Parameters as Positional or Named</span></span>

<span data-ttu-id="3c6e8-151">A parancsmag be kell állítania minden paraméter, vagy egy csak pozíciórekord vagy elnevezett paraméter.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-151">A cmdlet must set each parameter as either a positional or named parameter.</span></span> <span data-ttu-id="3c6e8-152">Mindkét típusú paramétereket fogadja el az egyetlen argumentumot, vesszővel válassza el egymástól, és logikai beállítások elválasztva több argumentumot.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-152">Both kinds of parameters accept single arguments, multiple arguments separated by commas, and Boolean settings.</span></span> <span data-ttu-id="3c6e8-153">Egy logikai paramétert, más néven egy *váltson*, csak a logikai beállítások kezeli.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-153">A Boolean parameter, also called a *switch*, handles only Boolean settings.</span></span> <span data-ttu-id="3c6e8-154">A kapcsoló a paraméter meglétének szolgál.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-154">The switch is used to determine the presence of the parameter.</span></span> <span data-ttu-id="3c6e8-155">Az ajánlott alapértelmezett érték `false`.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-155">The recommended default is `false`.</span></span>

<span data-ttu-id="3c6e8-156">A minta **Get-Proc** parancsmag határozza meg a `Name` paraméter 0 pozíciója a Helyzetbeállító paraméterként.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-156">The sample **Get-Proc** cmdlet defines the `Name` parameter as a positional parameter with position 0.</span></span> <span data-ttu-id="3c6e8-157">Ez azt jelenti, hogy a rendszer automatikusan beszúrja az első argumentum a parancssorban a felhasználó megadja ezt a paramétert.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-157">This means that the first argument the user enters on the command line is automatically inserted for this parameter.</span></span> <span data-ttu-id="3c6e8-158">Ha szeretne meghatározni egy elnevezett paraméterhez, amelyhez a felhasználónak meg kell adnia a paraméternév megadásához, a parancssorból, ne módosítsa a `Position` kulcsszó a típusattribútum-deklaráció kívül.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-158">If you want to define a named parameter, for which the user must specify the parameter name from the command line, leave the `Position` keyword out of the attribute declaration.</span></span>

> [!NOTE]
> <span data-ttu-id="3c6e8-159">Paraméterek névvel kell rendelkeznie, hacsak azt javasoljuk, hogy a leggyakrabban használt paraméterek csak pozíciórekord, hogy a felhasználóknak nem kell írja be a paraméter neve.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-159">Unless parameters must be named, we recommend that you make the most-used parameters positional so that users will not have to type the parameter name.</span></span>

## <a name="declaring-parameters-as-mandatory-or-optional"></a><span data-ttu-id="3c6e8-160">Kötelező vagy választható paramétereket deklaráló</span><span class="sxs-lookup"><span data-stu-id="3c6e8-160">Declaring Parameters as Mandatory or Optional</span></span>

<span data-ttu-id="3c6e8-161">A parancsmag be kell állítania minden paraméter egy választható vagy egy kötelező paraméter.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-161">A cmdlet must set each parameter as either an optional or a mandatory parameter.</span></span> <span data-ttu-id="3c6e8-162">A minta **Get-Proc** parancsmagot, a `Name` paraméter nem kötelező megadni, mert a `Mandatory` kulcsszó a típusattribútum-deklaráció nem állítható.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-162">In the sample **Get-Proc** cmdlet, the `Name` parameter is defined as optional because the `Mandatory` keyword is not set in the attribute declaration.</span></span>

## <a name="supporting-parameter-validation"></a><span data-ttu-id="3c6e8-163">Támogató paraméter ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="3c6e8-163">Supporting Parameter Validation</span></span>

<span data-ttu-id="3c6e8-164">A minta **Get-Proc** parancsmag hozzáadja egy bemenet-ellenőrzés attribútum [System.Management.Automation.Validatenotnulloremptyattribute](/dotnet/api/System.Management.Automation.ValidateNotNullOrEmptyAttribute), az a `Name` érvényesítéséhez paraméter, amely a bemeneti adat sem `null` , se nem üres.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-164">The sample **Get-Proc** cmdlet adds an input validation attribute, [System.Management.Automation.Validatenotnulloremptyattribute](/dotnet/api/System.Management.Automation.ValidateNotNullOrEmptyAttribute), to the `Name` parameter to enable validation that the input is neither `null` nor empty.</span></span> <span data-ttu-id="3c6e8-165">Ez az attribútum a Windows PowerShell által biztosított több ellenőrzési attribútumok egyike.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-165">This attribute is one of several validation attributes provided by Windows PowerShell.</span></span> <span data-ttu-id="3c6e8-166">Egyéb ellenőrzési attribútumok példákért lásd [paraméter bemeneti ellenőrzése](./validating-parameter-input.md).</span><span class="sxs-lookup"><span data-stu-id="3c6e8-166">For examples of other validation attributes, see [Validating Parameter Input](./validating-parameter-input.md).</span></span>

```
[Parameter(Position = 0)]
[ValidateNotNullOrEmpty]
public string[] Name
```

## <a name="overriding-an-input-processing-method"></a><span data-ttu-id="3c6e8-167">Egy bemeneti metódus feldolgozási felülbírálása</span><span class="sxs-lookup"><span data-stu-id="3c6e8-167">Overriding an Input Processing Method</span></span>

<span data-ttu-id="3c6e8-168">A parancsmagot, a parancssori bemenet kezelésére, ha azt a megfelelő bemeneti feldolgozási módszerek felül kell írnia.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-168">If your cmdlet is to handle command-line input, it must override the appropriate input processing methods.</span></span> <span data-ttu-id="3c6e8-169">Az alapszintű bemeneti feldolgozási módszerek jelennek meg a [létrehozásához az első parancsmag](./creating-a-cmdlet-without-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="3c6e8-169">The basic input processing methods are introduced in [Creating Your First Cmdlet](./creating-a-cmdlet-without-parameters.md).</span></span>

<span data-ttu-id="3c6e8-170">A **Get-Proc** parancsmag felülbírálja a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust a `Name` paraméter megadott információ a felhasználó vagy egy parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-170">The **Get-Proc** cmdlet overrides the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method to handle the `Name` parameter input provided by the user or a script.</span></span> <span data-ttu-id="3c6e8-171">Ez a módszer beolvassa a folyamatok minden kért Folyamatnév, és az összes folyamat, ha nincs név megadva.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-171">This method gets the processes for each requested process name, or all for processes if no name is provided.</span></span> <span data-ttu-id="3c6e8-172">Figyelje meg, hogy a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord), a hívást [System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29](/dotnet/api/system.management.automation.cmdlet.writeobject?view=powershellsdk-1.1.0#System_Management_Automation_Cmdlet_WriteObject_System_Object_System_Boolean_) a kimenete a folyamat küld kimeneti mechanizmus objektumokat.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-172">Notice that in [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord), the call to [System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29](/dotnet/api/system.management.automation.cmdlet.writeobject?view=powershellsdk-1.1.0#System_Management_Automation_Cmdlet_WriteObject_System_Object_System_Boolean_) is the output mechanism for sending output objects to the pipeline.</span></span> <span data-ttu-id="3c6e8-173">A második paraméter a hívás `enumerateCollection`, értékre van állítva `true` tájékoztatja a Windows PowerShell-futtatókörnyezet, a kimeneti tömbben folyamat objektumok számbavétele és a egy folyamat egyszerre írni a parancssorból.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-173">The second parameter of this call, `enumerateCollection`, is set to `true` to inform the Windows PowerShell runtime to enumerate the output array of process objects and write one process at a time to the command line.</span></span>

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
    }
  }
}
```

```vb
Protected Overrides Sub ProcessRecord()

    '/ If no process names are passed to the cmdlet, get all processes.
    If processNames Is Nothing Then
        Dim processes As Process()
        processes = Process.GetProcesses()
    End If

    '/ If process names are specified, write the processes to the
    '/ pipeline to display them or make them available to the next cmdlet.

    For Each name As String In processNames
        '/ The second parameter of this call tells PowerShell to enumerate the
        '/ array, and send one process at a time to the pipeline.
        WriteObject(Process.GetProcessesByName(name), True)
    Next

End Sub 'ProcessRecord
```

## <a name="code-sample"></a><span data-ttu-id="3c6e8-174">Kódminta</span><span class="sxs-lookup"><span data-stu-id="3c6e8-174">Code Sample</span></span>

<span data-ttu-id="3c6e8-175">A teljes C# mintakód, lásd: [GetProcessSample02 minta](./getprocesssample02-sample.md).</span><span class="sxs-lookup"><span data-stu-id="3c6e8-175">For the complete C# sample code, see [GetProcessSample02 Sample](./getprocesssample02-sample.md).</span></span>

## <a name="defining-object-types-and-formatting"></a><span data-ttu-id="3c6e8-176">Objektumtípusok definiálása és formázása</span><span class="sxs-lookup"><span data-stu-id="3c6e8-176">Defining Object Types and Formatting</span></span>

<span data-ttu-id="3c6e8-177">Windows PowerShell parancsmagok használatával a .NET-keretrendszer objektumok közötti továbbítja.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-177">Windows PowerShell passes information between cmdlets by using .NET Framework objects.</span></span> <span data-ttu-id="3c6e8-178">Ennek következtében a parancsmag előfordulhat, hogy meg kell határoznia a saját típusát, vagy parancsmag előfordulhat, hogy ki kell terjesztenie egy másik parancsmag által biztosított meglévő típus.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-178">Consequently, a cmdlet might need to define its own type, or a cmdlet might need to extend an existing type provided by another cmdlet.</span></span> <span data-ttu-id="3c6e8-179">Új típusok meghatározása, vagy meglévő típusok bővítésével kapcsolatos további információkért lásd: [objektumtípusok kiterjesztése és formázás](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).</span><span class="sxs-lookup"><span data-stu-id="3c6e8-179">For more information about defining new types or extending existing types, see [Extending Object Types and Formatting](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).</span></span>

## <a name="building-the-cmdlet"></a><span data-ttu-id="3c6e8-180">A parancsmag készítése</span><span class="sxs-lookup"><span data-stu-id="3c6e8-180">Building the Cmdlet</span></span>

<span data-ttu-id="3c6e8-181">A parancsmag megvalósítása, után regisztrálnia kell azt a Windows PowerShell-lel a Windows PowerShell beépülő modul használatával.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-181">After you implement a cmdlet, you must register it with Windows PowerShell by using a Windows PowerShell snap-in.</span></span> <span data-ttu-id="3c6e8-182">Parancsmagok regisztrálásával kapcsolatos további információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).</span><span class="sxs-lookup"><span data-stu-id="3c6e8-182">For more information about registering cmdlets, see [How to Register Cmdlets, Providers, and Host Applications](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).</span></span>

## <a name="testing-the-cmdlet"></a><span data-ttu-id="3c6e8-183">A parancsmag tesztelése</span><span class="sxs-lookup"><span data-stu-id="3c6e8-183">Testing the Cmdlet</span></span>

<span data-ttu-id="3c6e8-184">Amikor a parancsmag a Windows PowerShell használatával regisztrál, azt a parancssorból való futtatásával tesztelheti.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-184">When your cmdlet is registered with Windows PowerShell, you can test it by running it on the command line.</span></span> <span data-ttu-id="3c6e8-185">Itt két módon a minta parancsmagot a kódja tesztelésére.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-185">Here are two ways to test the code for the sample cmdlet.</span></span> <span data-ttu-id="3c6e8-186">A parancssorból-parancsmagokkal kapcsolatos további információkért lásd: [első lépések a Windows PowerShell-lel](/powershell/scripting/getting-started/getting-started-with-windows-powershell).</span><span class="sxs-lookup"><span data-stu-id="3c6e8-186">For more information about using cmdlets from the command line, see [Getting Started with Windows PowerShell](/powershell/scripting/getting-started/getting-started-with-windows-powershell).</span></span>

- <span data-ttu-id="3c6e8-187">A Windows PowerShell parancssorába a következő paranccsal listázhatja az Internet Explorer folyamat, amely a neve "IEXPLORE."</span><span class="sxs-lookup"><span data-stu-id="3c6e8-187">At the Windows PowerShell prompt, use the following command to list the Internet Explorer process, which is named "IEXPLORE."</span></span>

    ```powershell
    PS> get-proc -name iexplore
    ```

<span data-ttu-id="3c6e8-188">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-188">The following output appears.</span></span>

    ```
    Handles  NPM(K)  PM(K)   WS(K)  VS(M)  CPU(s)   Id   ProcessName
    -------  ------  -----   -----  -----   ------ --   -----------
        354      11  10036   18992    85   0.67   3284   iexplore
    ```

- <span data-ttu-id="3c6e8-189">A listán az Internet Explorer, az Outlook és a Jegyzettömb folyamatok "IEXPLORE" nevű, "OUTLOOK" és "A JEGYZETTÖMB," a következő paranccsal.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-189">To list the Internet Explorer, Outlook, and Notepad processes named "IEXPLORE," "OUTLOOK," and "NOTEPAD," use the following command.</span></span> <span data-ttu-id="3c6e8-190">Ha több folyamatot, ezek mindegyike jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-190">If there are multiple processes, all of them are displayed.</span></span>

    ```powershell
    PS> get-proc -name iexplore, outlook, notepad
    ```

<span data-ttu-id="3c6e8-191">A következő eredmény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="3c6e8-191">The following output appears.</span></span>

    ```
    Handles  NPM(K)  PM(K)   WS(K)  VS(M)  CPU(s)   Id   ProcessName
    -------  ------  -----   -----  -----  ------   --    -----------
        732      21  24696    5000    138   2.25  2288   iexplore
        715      19  20556   14116    136   1.78  3860   iexplore
       3917      62  74096   58112    468 191.56  1848   OUTLOOK
         39       2   1024    3280     30   0.09  1444   notepad
         39       2   1024     356     30   0.08  3396   notepad
    ```

## <a name="see-also"></a><span data-ttu-id="3c6e8-192">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="3c6e8-192">See Also</span></span>

[<span data-ttu-id="3c6e8-193">Folyamat folyamat bemeneti paraméterek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="3c6e8-193">Adding Parameters that Process Pipeline Input</span></span>](./adding-parameters-that-process-pipeline-input.md)

[<span data-ttu-id="3c6e8-194">Az első parancsmag létrehozása</span><span class="sxs-lookup"><span data-stu-id="3c6e8-194">Creating Your First Cmdlet</span></span>](./creating-a-cmdlet-without-parameters.md)

[<span data-ttu-id="3c6e8-195">Objektumtípusok kiterjesztése és formázása</span><span class="sxs-lookup"><span data-stu-id="3c6e8-195">Extending Object Types and Formatting</span></span>](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[<span data-ttu-id="3c6e8-196">How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez</span><span class="sxs-lookup"><span data-stu-id="3c6e8-196">How to Register Cmdlets, Providers, and Host Applications</span></span>](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[<span data-ttu-id="3c6e8-197">Windows PowerShell-referencia</span><span class="sxs-lookup"><span data-stu-id="3c6e8-197">Windows PowerShell Reference</span></span>](../windows-powershell-reference.md)

[<span data-ttu-id="3c6e8-198">Parancsmag-minták</span><span class="sxs-lookup"><span data-stu-id="3c6e8-198">Cmdlet Samples</span></span>](./cmdlet-samples.md)
