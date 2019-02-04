---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: a96a4a58dafa01fb43f5bdffb52ef833816148e7
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688475"
---
# <a name="new-language-features-in-powershell-50"></a><span data-ttu-id="a670e-102">A PowerShell 5.0 új nyelvi funkciók</span><span class="sxs-lookup"><span data-stu-id="a670e-102">New language features in PowerShell 5.0</span></span>

<span data-ttu-id="a670e-103">PowerShell 5.0 vezet be a következő új nyelvi elemei a Windows PowerShellben:</span><span class="sxs-lookup"><span data-stu-id="a670e-103">PowerShell 5.0 introduces the following new language elements in Windows PowerShell:</span></span>

## <a name="class-keyword"></a><span data-ttu-id="a670e-104">Osztály kulcsszó</span><span class="sxs-lookup"><span data-stu-id="a670e-104">Class keyword</span></span>

<span data-ttu-id="a670e-105">A **osztály** kulcsszó határozza meg egy új osztályt.</span><span class="sxs-lookup"><span data-stu-id="a670e-105">The **class** keyword defines a new class.</span></span> <span data-ttu-id="a670e-106">Ez a valódi .NET-keretrendszer típusa.</span><span class="sxs-lookup"><span data-stu-id="a670e-106">This is a true .NET Framework type.</span></span>
<span data-ttu-id="a670e-107">A osztályelemen nyilvános, de csak nyilvános modul hatókörébe.</span><span class="sxs-lookup"><span data-stu-id="a670e-107">Class members are public, but only public within the module scope.</span></span>
<span data-ttu-id="a670e-108">Nem lehet hivatkozni a típusnév karakterláncként (például `New-Object` nem működik), ebben a kiadásban, és nem használhat olyan típusú konstans (például `[MyClass]`) kívül a parancsfájl nebo modul fájlt, amelyben az osztály definiálva van.</span><span class="sxs-lookup"><span data-stu-id="a670e-108">You can't refer to the type name as a string (for example, `New-Object` doesn't work), and in this release, you can't use a type literal (for example, `[MyClass]`) outside the script/module file in which the class is defined.</span></span>

```powershell
class MyClass
{
    ...
}
```

## <a name="enum-keyword-and-enumerations"></a><span data-ttu-id="a670e-109">Enum kulcsszó és enumerálásokat tartalmaznak</span><span class="sxs-lookup"><span data-stu-id="a670e-109">Enum keyword and enumerations</span></span>

<span data-ttu-id="a670e-110">Támogatja a **enum** kulcsszó hozzá lett adva, melyik soremelés használ elválasztóként.</span><span class="sxs-lookup"><span data-stu-id="a670e-110">Support for the **enum** keyword has been added, which uses newline as the delimiter.</span></span>
<span data-ttu-id="a670e-111">Aktuális korlátozások: nem lehet definiálni enumerátor tekintetében magát, de szempontjából egy másik enum enum is inicializálása, az alábbi példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="a670e-111">Current limitations: you cannot define an enumerator in terms of itself, but you can initialize an enum in terms of another enum, as shown in the following example.</span></span>
<span data-ttu-id="a670e-112">Ezenkívül az alaptípus nem jelenleg adható meg; minden esetben [int].</span><span class="sxs-lookup"><span data-stu-id="a670e-112">Also, the base type cannot currently be specified; it is always [int].</span></span>

```powershell
enum Color2
{
    Yellow = [Color]::Blue
}
```

<span data-ttu-id="a670e-113">Az enumerálóérték állandónak kell lennie parse time; egy meghívott parancs eredménye nem állítható be azt.</span><span class="sxs-lookup"><span data-stu-id="a670e-113">An enumerator value must be a parse time constant; you cannot set it to the result of an invoked command.</span></span>

```powershell
enum MyEnum
{
    Enum1
    Enum2
    Enum3 = 42
    Enum4 = [int]::MaxValue
}
```

<span data-ttu-id="a670e-114">Enumerálások aritmetikai műveletek támogatásához, az alábbi példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="a670e-114">Enums support arithmetic operations, as shown in the following example.</span></span>

```powershell
enum SomeEnum { Max = 42 }
enum OtherEnum { Max = [SomeEnum]::Max + 1 }
```

## <a name="import-dscresource"></a><span data-ttu-id="a670e-115">Import-DscResource</span><span class="sxs-lookup"><span data-stu-id="a670e-115">Import-DscResource</span></span>

<span data-ttu-id="a670e-116">**Az import-DscResource** már igaz dinamikus kulcsszó.</span><span class="sxs-lookup"><span data-stu-id="a670e-116">**Import-DscResource** is now a true dynamic keyword.</span></span>
<span data-ttu-id="a670e-117">PowerShell elemzi a megadott modul legfelső szintű modul, osztályban, amelyek tartalmazzák a Keresés a **DscResource** attribútum.</span><span class="sxs-lookup"><span data-stu-id="a670e-117">PowerShell parses the specified module’s root module, searching for classes that contain the **DscResource** attribute.</span></span>

## <a name="implementingassembly"></a><span data-ttu-id="a670e-118">ImplementingAssembly</span><span class="sxs-lookup"><span data-stu-id="a670e-118">ImplementingAssembly</span></span>

<span data-ttu-id="a670e-119">Egy új mezőt **ImplementingAssembly**, ModuleInfo bővült.</span><span class="sxs-lookup"><span data-stu-id="a670e-119">A new field, **ImplementingAssembly**, has been added to ModuleInfo.</span></span> <span data-ttu-id="a670e-120">Azt a dinamikus szerelvény egy szkriptmodulba készült, ha a parancsfájl definiálja azokat az osztályokat, vagy a betöltött szerelvény a bináris modulok van beállítva.</span><span class="sxs-lookup"><span data-stu-id="a670e-120">It is set to the dynamic assembly created for a script module if the script defines classes, or the loaded assembly for binary modules.</span></span> <span data-ttu-id="a670e-121">Nincs beállítva mikor ModuleType = jegyzékfájlt.</span><span class="sxs-lookup"><span data-stu-id="a670e-121">It is not set when ModuleType = Manifest.</span></span>

<span data-ttu-id="a670e-122">A reflexió a **ImplementingAssembly** mező felderítette az erőforrásokat egy modulban.</span><span class="sxs-lookup"><span data-stu-id="a670e-122">Reflection on the **ImplementingAssembly** field discovers resources in a module.</span></span> <span data-ttu-id="a670e-123">Ez azt jelenti, hogy a PowerShell vagy más felügyelt nyelveken írt erőforrások deríthet fel.</span><span class="sxs-lookup"><span data-stu-id="a670e-123">This means you can discover resources written in either PowerShell or other managed languages.</span></span>

<span data-ttu-id="a670e-124">Inicializátory mezőket:</span><span class="sxs-lookup"><span data-stu-id="a670e-124">Fields with initializers:</span></span>

```powershell
[int] $i = 5
```

<span data-ttu-id="a670e-125">Statikus támogatott; működik egy attribútum, például az ajánlattípusra vonatkozó megkötések, ahogy, így bármilyen sorrendben adható meg.</span><span class="sxs-lookup"><span data-stu-id="a670e-125">Static is supported; it works like an attribute, as do the type constraints, so it can be specified in any order.</span></span>

```powershell
static [int] $count = 0
```

<span data-ttu-id="a670e-126">Egy nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="a670e-126">A type is optional.</span></span>

```powershell
$s = "hello"
```

<span data-ttu-id="a670e-127">Minden tag nyilvánosak legyenek.</span><span class="sxs-lookup"><span data-stu-id="a670e-127">All members are public.</span></span>

## <a name="constructors-and-instantiation"></a><span data-ttu-id="a670e-128">Konstruktorok és példányosítás</span><span class="sxs-lookup"><span data-stu-id="a670e-128">Constructors and instantiation</span></span>

<span data-ttu-id="a670e-129">Windows PowerShell-osztályok rendelkezhet konstruktorok; a neve megegyezik az osztály rendelkeznek.</span><span class="sxs-lookup"><span data-stu-id="a670e-129">Windows PowerShell classes can have constructors; they have the same name as their class.</span></span> <span data-ttu-id="a670e-130">Is túlterhelt konstruktorral.</span><span class="sxs-lookup"><span data-stu-id="a670e-130">Constructors can be overloaded.</span></span> <span data-ttu-id="a670e-131">Statikus konstruktorok támogatottak.</span><span class="sxs-lookup"><span data-stu-id="a670e-131">Static constructors are supported.</span></span> <span data-ttu-id="a670e-132">Tulajdonságok inicializálási kifejezésekkel inicializálása konstruktorban kód futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="a670e-132">Properties with initialization expressions are initialized before running any code in a constructor.</span></span> <span data-ttu-id="a670e-133">A statikus tulajdonságok inicializálása előtt egy statikus konstruktor törzse, és a példány tulajdonságainak inicializálása előtt nem statikus konstruktor törzse.</span><span class="sxs-lookup"><span data-stu-id="a670e-133">Static properties are initialized before the body of a static constructor, and instance properties are initialized before the body of the non-static constructor.</span></span> <span data-ttu-id="a670e-134">Jelenleg nincs másik konstruktor konstruktor megismernie szintaxisának (például a C\# szintaxis ": this()").</span><span class="sxs-lookup"><span data-stu-id="a670e-134">Currently, there is no syntax for calling a constructor from another constructor (like the C\# syntax ": this()").</span></span> <span data-ttu-id="a670e-135">A megoldás, hogy egy közös Init módszer meghatározásához.</span><span class="sxs-lookup"><span data-stu-id="a670e-135">The workaround is to define a common Init method.</span></span>

<span data-ttu-id="a670e-136">A következő módon osztályok hárítható el ebben a kiadásban.</span><span class="sxs-lookup"><span data-stu-id="a670e-136">The following are ways of instantiating classes in this release.</span></span>

<span data-ttu-id="a670e-137">Hárítható el, az alapértelmezett konstruktort használatával.</span><span class="sxs-lookup"><span data-stu-id="a670e-137">Instantiating by using the default constructor.</span></span> <span data-ttu-id="a670e-138">Vegye figyelembe, hogy a New-Object nem támogatott ebben a kiadásban.</span><span class="sxs-lookup"><span data-stu-id="a670e-138">Note that New-Object is not supported in this release.</span></span>

```powershell
$a = [MyClass]::new()
```

<span data-ttu-id="a670e-139">A konstruktor egy paraméterrel hívása</span><span class="sxs-lookup"><span data-stu-id="a670e-139">Calling a constructor with a parameter</span></span>

```powershell
$b = [MyClass]::new(42)
```

<span data-ttu-id="a670e-140">Egy tömb átadása több paraméterekkel rendelkező konstruktor</span><span class="sxs-lookup"><span data-stu-id="a670e-140">Passing an array to a constructor with multiple parameters</span></span>
```powershell
$c = [MyClass]::new(@(42,43,44), "Hello")
```

<span data-ttu-id="a670e-141">Az ebben a kiadásban a New-Object nem működik Windows PowerShell-ben definiált osztályokkal.</span><span class="sxs-lookup"><span data-stu-id="a670e-141">In this release, New-Object does not work with classes defined in Windows PowerShell.</span></span> <span data-ttu-id="a670e-142">Ebben a kiadásban název typu is csak látható betűrendbe, ami azt jelenti, már nem látható a modul vagy a parancsfájl az osztályt definiáló kívül.</span><span class="sxs-lookup"><span data-stu-id="a670e-142">Also for this release, the type name is only visible lexically, meaning it is not visible outside of the module or script that defines the class.</span></span> <span data-ttu-id="a670e-143">Funkciók a Windows PowerShellben meghatározott osztály példányainak adhat vissza, és példányok működnek jól kívül a modul vagy a parancsfájl.</span><span class="sxs-lookup"><span data-stu-id="a670e-143">Functions can return instances of a class defined in Windows PowerShell, and instances work well outside of the module or script.</span></span>

<span data-ttu-id="a670e-144">`Get-Member -Static` konstruktorok, sorolja fel, hogy meg tudja tekinteni a túlterhelések, mint bármely más módszerrel.</span><span class="sxs-lookup"><span data-stu-id="a670e-144">`Get-Member -Static` lists constructors, so you can view overloads like any other method.</span></span> <span data-ttu-id="a670e-145">Ezt a szintaxist teljesítménye is jelentősen gyorsabb, mint a New-Object.</span><span class="sxs-lookup"><span data-stu-id="a670e-145">The performance of this syntax is also considerably faster than New-Object.</span></span>

<span data-ttu-id="a670e-146">A pszeudo statikus metódust **új** együttműködik a .NET-típusok, az alábbi példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="a670e-146">The pseudo-static method named **new** works with .NET types, as shown in the following example.</span></span>

```powershell
[hashtable]::new()
```

<span data-ttu-id="a670e-147">Most már megtekintheti a konstruktor túlterheléssel Get-Member, vagy ebben a példában látható módon:</span><span class="sxs-lookup"><span data-stu-id="a670e-147">You can now see constructor overloads with Get-Member, or as shown in this example:</span></span>

```powershell
PS> [hashtable]::new
OverloadDefinitions
-------------------
hashtable new()
hashtable new(int capacity)
hashtable new(int capacity, float loadFactor)
```

## <a name="methods"></a><span data-ttu-id="a670e-148">Metódusok</span><span class="sxs-lookup"><span data-stu-id="a670e-148">Methods</span></span>

<span data-ttu-id="a670e-149">A Windows PowerShell-osztály metódusának a scriptblock kulcsszót, amelynek csak egy záró blokk van megvalósítva.</span><span class="sxs-lookup"><span data-stu-id="a670e-149">A Windows PowerShell class method is implemented as a ScriptBlock that has only an end block.</span></span> <span data-ttu-id="a670e-150">Az összes módszer nyilvánosak legyenek.</span><span class="sxs-lookup"><span data-stu-id="a670e-150">All methods are public.</span></span> <span data-ttu-id="a670e-151">A következő nevű metódus meghatározása példán látható **DoSomething**.</span><span class="sxs-lookup"><span data-stu-id="a670e-151">The following shows an example of defining a method named **DoSomething**.</span></span>

```powershell
class MyClass
{
    DoSomething($x)
    {
        $this._doSomething($x) # method syntax
    }
    private _doSomething($a) {}
}
```

<span data-ttu-id="a670e-152">Metódushívás:</span><span class="sxs-lookup"><span data-stu-id="a670e-152">Method invocation:</span></span>

```powershell
$b = [MyClass]::new()
$b.DoSomething(42)
```

<span data-ttu-id="a670e-153">--Metódusok túlterhelt, azokkal, amelyek neve megegyezik egy meglévő módszer, de különbözteti meg a megadott értékek – is támogatottak.</span><span class="sxs-lookup"><span data-stu-id="a670e-153">Overloaded methods--that is, those that are named the same as an existing method, but differentiated by their specified values--are also supported.</span></span>

## <a name="properties"></a><span data-ttu-id="a670e-154">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="a670e-154">Properties</span></span>

<span data-ttu-id="a670e-155">Az összes tulajdonság nyilvánosak legyenek.</span><span class="sxs-lookup"><span data-stu-id="a670e-155">All properties are public.</span></span> <span data-ttu-id="a670e-156">Tulajdonságok szükség soremelés vagy pontosvesszővel válassza el.</span><span class="sxs-lookup"><span data-stu-id="a670e-156">Properties require either a newline or semicolon.</span></span> <span data-ttu-id="a670e-157">Ha nincs objektum típus van megadva, a tulajdonság típusának egy objektum.</span><span class="sxs-lookup"><span data-stu-id="a670e-157">If no object type is specified, the property type is object.</span></span>

<span data-ttu-id="a670e-158">Érvényesítési attribútumok vagy az argumentum-átalakítás attribútumok tulajdonságok (pl. `[ValidateSet("aaa")]`) a várt módon működik.</span><span class="sxs-lookup"><span data-stu-id="a670e-158">Properties that use validation attributes or argument transformation attributes (e.g. `[ValidateSet("aaa")]`) work as expected.</span></span>

## <a name="hidden"></a><span data-ttu-id="a670e-159">Rejtett</span><span class="sxs-lookup"><span data-stu-id="a670e-159">Hidden</span></span>

<span data-ttu-id="a670e-160">Egy új kulcsszó, **Hidden**, hozzá van adva.</span><span class="sxs-lookup"><span data-stu-id="a670e-160">A new keyword, **Hidden**, has been added.</span></span> <span data-ttu-id="a670e-161">**Rejtett** tulajdonságai és metódusai (beleértve a konstruktorok) is alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="a670e-161">**Hidden** can be applied to properties and methods (including constructors).</span></span>

<span data-ttu-id="a670e-162">Rejtett tagok nyilvános, de nem jelennek meg a Get-Member kimenetét, kivéve, ha a - Force paramétert.</span><span class="sxs-lookup"><span data-stu-id="a670e-162">Hidden members are public, but do not appear in the output of Get-Member unless the -Force parameter is added.</span></span>

<span data-ttu-id="a670e-163">A tagok nem tartoznak mikor rejtett lapon befejezése vagy az IntelliSense segítségével, kivéve, ha az osztály a rejtett tag meghatározása befejezése után történik.</span><span class="sxs-lookup"><span data-stu-id="a670e-163">Hidden members are not included when tab completing or using Intellisense unless the completion occurs in the class defining the hidden member.</span></span>

<span data-ttu-id="a670e-164">Egy új attribútum **System.Management.Automation.HiddenAttribute** , hogy a C#-kód azonos szemantikáját Windows Powershellen belülről lehet hozzá lett adva.</span><span class="sxs-lookup"><span data-stu-id="a670e-164">A new attribute, **System.Management.Automation.HiddenAttribute** has been added so that C# code can have the same semantics within Windows PowerShell.</span></span>

## <a name="return-types"></a><span data-ttu-id="a670e-165">Návratové typy</span><span class="sxs-lookup"><span data-stu-id="a670e-165">Return types</span></span>

<span data-ttu-id="a670e-166">Typ vrácené hodnoty je szerződés; a visszaadott érték a várt típus alakítja át.</span><span class="sxs-lookup"><span data-stu-id="a670e-166">Return type is a contract; the return value is converted to the expected type.</span></span> <span data-ttu-id="a670e-167">Ha nincs visszatérési típus van megadva, a typ vrácené hodnoty je typ void.</span><span class="sxs-lookup"><span data-stu-id="a670e-167">If no return type is specified, the return type is void.</span></span> <span data-ttu-id="a670e-168">Nincsenek objektumok; streamelési van objektumok nem lehet írni a folyamat szándékosan vagy véletlenül iratkozott le.</span><span class="sxs-lookup"><span data-stu-id="a670e-168">There is no streaming of objects; objects cannot be written to the pipeline either intentionally or by accident.</span></span>

## <a name="attributes"></a><span data-ttu-id="a670e-169">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="a670e-169">Attributes</span></span>

<span data-ttu-id="a670e-170">Két új attribútum **DscResource** és **DscProperty** lettek hozzáadva.</span><span class="sxs-lookup"><span data-stu-id="a670e-170">Two new attributes, **DscResource** and **DscProperty** have been added.</span></span>

## <a name="lexical-scoping-of-variables"></a><span data-ttu-id="a670e-171">Lexikális hatókörkezeléséhez kapcsolódó változók</span><span class="sxs-lookup"><span data-stu-id="a670e-171">Lexical scoping of variables</span></span>

<span data-ttu-id="a670e-172">Az alábbi példán látható hogyan lexikai hatókörkezelési működik Ebben a kiadásban.</span><span class="sxs-lookup"><span data-stu-id="a670e-172">The following shows an example of how lexical scoping works in this release.</span></span>

```powershell
$d = 42 # Script scope

function bar
{
    $d = 0 # Function scope
    [MyClass]::DoSomething()
}

class MyClass
{
    static [object] DoSomething()
    {
        return $d # error, not found dynamically
        return $script:d # no error
        $d = $script:d
        return $d # no error, found lexically
    }
}

$v = bar
$v -eq $d # true
```

## <a name="end-to-end-example"></a><span data-ttu-id="a670e-173">Teljes körű – példa</span><span class="sxs-lookup"><span data-stu-id="a670e-173">End-to-End Example</span></span>

<span data-ttu-id="a670e-174">A következő példában létrehozunk egy HTML dinamikus stílus lap nyelv (DSL) megvalósításának számos új, egyéni osztályok.</span><span class="sxs-lookup"><span data-stu-id="a670e-174">The following example creates several new, custom classes to implement an HTML dynamic style sheet language (DSL).</span></span>
<span data-ttu-id="a670e-175">Ezt követően a példa ad segédfüggvények hozhat létre egyedi elemtípus az elem osztályt, például a címsorok és a táblázatok, részeként, mert típusok nem használhatók egy modul hatókörén kívül.</span><span class="sxs-lookup"><span data-stu-id="a670e-175">Then, the example adds helper functions to create specific element types as part of the element class, such as heading styles and tables, because types cannot be used outside the scope of a module.</span></span>

```powershell
# Classes that define the structure of the document
#
class Html
{
    [string] $docType
    [HtmlHead] $Head
    [Element[]] $Body

    [string] Render()
    {
        $text = "<html>`n<head>`n"
        $text += $this.Head
        $text += "`n</head>`n<body>`n"
        $text += $this.Body -join "`n" # Render all of the body elements
        $text += "</body>`n</html>"
        return $text
    }
    [string] ToString() { return $this.Render() }
}

class HtmlHead
{
    $Title
    $Base
    $Link
    $Style
    $Meta
    $Script
    [string] Render() { return "<title>$($this.Title)</title>" }
    [string] ToString() { return $this.Render() }
}

class Element
{
    [string] $Tag
    [string] $Text
    [hashtable] $Attributes
    [string] Render() {
        $attributesText= ""
        if ($this.Attributes)
        {
            foreach ($attr in $this.Attributes.Keys)
            {
                #BUGBUG - need to validate keys against attribute
                $attributesText += " $attr=`"$($this.Attributes[$attr])\`""
            }
        }
        return "<$($this.tag)${attributesText}>$($this.text)</$($this.tag)>`n"
    }
[string] ToString() { return $this.Render() }
}

#
# Helper functions for creating specific element types on top of the classes.
# These are required because types aren’t visible outside of the module.
#

function H1 { [Element] @{ Tag = "H1" ; Text = $args.foreach{$_} -join " " }}
function H2 { [Element] @{ Tag = "H2" ; Text = $args.foreach{$_} -join " " }}
function H3 { [Element] @{ Tag = "H3" ; Text = $args.foreach{$_} -join " " }}
function P { [Element] @{ Tag = "P" ; Text = $args.foreach{$_} -join " " }}
function B { [Element] @{ Tag = "B" ; Text = $args.foreach{$_} -join " " }}
function I { [Element] @{ Tag = "I" ; Text = $args.foreach{$_} -join " " }}
function HREF
{
    param (
        $Name,
        $Link
    )
    return [Element] @{
        Tag = "A"
        Attributes = @{ HREF = $link }
        Text = $name
    }
}
function Table
{
    param (
    [Parameter(Mandatory)]
    [object[]]
        $Data,
    [Parameter()]
    [string[]]
        $Properties = "*",
    [Parameter()]
    [hashtable]
        $Attributes = @{ border=2; cellpadding=2; cellspacing=2 }
    )
$bodyText = ""
# Add the header tags
$bodyText += $Properties.foreach{TH $_}
# Add the rows
$bodyText += foreach ($row in $Data)
    {
        TR (-join $Properties.Foreach{ TD ($row.$_) } )
    }

    $table = [Element] @{
        Tag = "Table"
        Attributes = $Attributes
        Text = $bodyText
    }
$table
}
function TH { ([Element] @{ Tag = "TH" ; Text = $args.foreach{$_} -join " " }) }
function TR { ([Element] @{ Tag = "TR" ; Text = $args.foreach{$_} -join " " }) }
function TD { ([Element] @{ Tag = "TD" ; Text = $args.foreach{$_} -join " " }) }
function Style

{
    return [Element] @{
        Tag = "style"
        Text = "$args"
    }
}

# Takes a hash table, casts it to and HTML document
# and then returns the resulting type.
#
function Html ([HTML] $doc) { return $doc }
```
