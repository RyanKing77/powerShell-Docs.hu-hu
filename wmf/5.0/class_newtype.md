---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: c7318552969c44f3b79f82efd71e6a72bfabef6b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="new-language-features-in-powershell-50"></a><span data-ttu-id="b3737-102">PowerShell 5.0 nyelvi újdonságai</span><span class="sxs-lookup"><span data-stu-id="b3737-102">New language features in PowerShell 5.0</span></span> 

<span data-ttu-id="b3737-103">PowerShell 5.0 vezet be a következő új nyelvi elemek a Windows PowerShellben:</span><span class="sxs-lookup"><span data-stu-id="b3737-103">PowerShell 5.0 introduces the following new language elements in Windows PowerShell:</span></span>

## <a name="class-keyword"></a><span data-ttu-id="b3737-104">Osztály kulcsszó</span><span class="sxs-lookup"><span data-stu-id="b3737-104">Class keyword</span></span>

<span data-ttu-id="b3737-105">A **osztály** kulcsszó egy új osztályt határoz meg.</span><span class="sxs-lookup"><span data-stu-id="b3737-105">The **class** keyword defines a new class.</span></span> <span data-ttu-id="b3737-106">Ez a .NET-keretrendszer típus igaz értékű.</span><span class="sxs-lookup"><span data-stu-id="b3737-106">This is a true .NET Framework type.</span></span> <span data-ttu-id="b3737-107">A osztályelemen nyilvános, de csak nyilvános modul hatókörében.</span><span class="sxs-lookup"><span data-stu-id="b3737-107">Class members are public, but only public within the module scope.</span></span>
<span data-ttu-id="b3737-108">Nem lehet hivatkozni a következő típusnév karakterláncként (például `New-Object` nem működik), és ebben a kiadásban szövegkonstans típus nem használható (például `[MyClass]`) kívül a parancsfájl/modul fájlt, amelyben az osztály definiálva van.</span><span class="sxs-lookup"><span data-stu-id="b3737-108">You can't refer to the type name as a string (for example, `New-Object` doesn't work), and in this release, you can't use a type literal (for example, `[MyClass]`) outside the script/module file in which the class is defined.</span></span>

```powershell
class MyClass
{
    ...
}
```

## <a name="enum-keyword-and-enumerations"></a><span data-ttu-id="b3737-109">Enum kulcsszó és az</span><span class="sxs-lookup"><span data-stu-id="b3737-109">Enum keyword and enumerations</span></span>

<span data-ttu-id="b3737-110">Támogatja a **enum** kulcsszó bővült, melyik soremelés használ elválasztóként.</span><span class="sxs-lookup"><span data-stu-id="b3737-110">Support for the **enum** keyword has been added, which uses newline as the delimiter.</span></span>
<span data-ttu-id="b3737-111">Aktuális korlátozások: enumerátor tekintetében maga nem határozhat meg, de egy felsorolás egy másik enum tekintetében is inicializálására, az alábbi példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="b3737-111">Current limitations: you cannot define an enumerator in terms of itself, but you can initialize an enum in terms of another enum, as shown in the following example.</span></span>
<span data-ttu-id="b3737-112">Emellett az alaptípus tartalomtípusa nem jelenleg adható meg; mindig [int].</span><span class="sxs-lookup"><span data-stu-id="b3737-112">Also, the base type cannot currently be specified; it is always [int].</span></span>

```powershell
enum Color2
{
    Yellow = [Color]::Blue
}
```

<span data-ttu-id="b3737-113">Az enumerálóérték elemzési idő állandónak; kell lennie. egy meghívott parancs eredménye nem állítható be azt.</span><span class="sxs-lookup"><span data-stu-id="b3737-113">An enumerator value must be a parse time constant; you cannot set it to the result of an invoked command.</span></span>

```powershell
enum MyEnum
{
    Enum1
    Enum2
    Enum3 = 42
    Enum4 = [int]::MaxValue
}
```

<span data-ttu-id="b3737-114">Felsorolások matematikai művelteket is támogatja, a következő példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="b3737-114">Enums support arithmetic operations, as shown in the following example.</span></span>

```powershell
enum SomeEnum { Max = 42 }
enum OtherEnum { Max = [SomeEnum]::Max + 1 }
```

## <a name="import-dscresource"></a><span data-ttu-id="b3737-115">Importálás – DscResource</span><span class="sxs-lookup"><span data-stu-id="b3737-115">Import-DscResource</span></span>

<span data-ttu-id="b3737-116">**Importálás – DscResource** mostantól egy igaz dinamikus kulcsszóval.</span><span class="sxs-lookup"><span data-stu-id="b3737-116">**Import-DscResource** is now a true dynamic keyword.</span></span>
<span data-ttu-id="b3737-117">PowerShell elemzi a megadott modul gyökérmodult, tartalmazó osztályok keresése a **DscResource** attribútum.</span><span class="sxs-lookup"><span data-stu-id="b3737-117">PowerShell parses the specified module’s root module, searching for classes that contain the **DscResource** attribute.</span></span>

## <a name="implementingassembly"></a><span data-ttu-id="b3737-118">ImplementingAssembly</span><span class="sxs-lookup"><span data-stu-id="b3737-118">ImplementingAssembly</span></span>

<span data-ttu-id="b3737-119">Új mező **ImplementingAssembly**, ModuleInfo hozzá lett adva.</span><span class="sxs-lookup"><span data-stu-id="b3737-119">A new field, **ImplementingAssembly**, has been added to ModuleInfo.</span></span> <span data-ttu-id="b3737-120">A dinamikus szerelvény egy szkriptmodulba készült, ha a parancsfájl osztályok határozza meg, vagy a bináris modulok betöltött szerelvény érték.</span><span class="sxs-lookup"><span data-stu-id="b3737-120">It is set to the dynamic assembly created for a script module if the script defines classes, or the loaded assembly for binary modules.</span></span> <span data-ttu-id="b3737-121">Nincs beállítva mikor ModuleType jegyzékfájl =.</span><span class="sxs-lookup"><span data-stu-id="b3737-121">It is not set when ModuleType = Manifest.</span></span> 

<span data-ttu-id="b3737-122">A reflexió a **ImplementingAssembly** mező a modulokban lévő erőforrások felderítésére szolgál.</span><span class="sxs-lookup"><span data-stu-id="b3737-122">Reflection on the **ImplementingAssembly** field discovers resources in a module.</span></span> <span data-ttu-id="b3737-123">Ez azt jelenti, hogy is felderítheti, PowerShell vagy más felügyelt nyelvek erőforrásokat.</span><span class="sxs-lookup"><span data-stu-id="b3737-123">This means you can discover resources written in either PowerShell or other managed languages.</span></span>

<span data-ttu-id="b3737-124">Az inicializálók mezők:</span><span class="sxs-lookup"><span data-stu-id="b3737-124">Fields with initializers:</span></span>      

```powershell
[int] $i = 5
```

<span data-ttu-id="b3737-125">Statikus támogatott; az működik, mint egy attribútum, mint a típusmegkötések, így bármilyen sorrendben adható meg.</span><span class="sxs-lookup"><span data-stu-id="b3737-125">Static is supported; it works like an attribute, as do the type constraints, so it can be specified in any order.</span></span>

```powershell
static [int] $count = 0
```

<span data-ttu-id="b3737-126">A típus nem kötelező megadni.</span><span class="sxs-lookup"><span data-stu-id="b3737-126">A type is optional.</span></span>

```powershell
$s = "hello"
```

<span data-ttu-id="b3737-127">Minden tagjai nyilvános.</span><span class="sxs-lookup"><span data-stu-id="b3737-127">All members are public.</span></span> 

## <a name="constructors-and-instantiation"></a><span data-ttu-id="b3737-128">Konstruktorok és a példánylétrehozás</span><span class="sxs-lookup"><span data-stu-id="b3737-128">Constructors and instantiation</span></span>

<span data-ttu-id="b3737-129">A Windows PowerShell-osztályokat lehet konstruktorok; az osztály megegyező névvel rendelkeznek.</span><span class="sxs-lookup"><span data-stu-id="b3737-129">Windows PowerShell classes can have constructors; they have the same name as their class.</span></span> <span data-ttu-id="b3737-130">Konstruktorok is túlterhelt.</span><span class="sxs-lookup"><span data-stu-id="b3737-130">Constructors can be overloaded.</span></span> <span data-ttu-id="b3737-131">Statikus konstruktorok támogatottak.</span><span class="sxs-lookup"><span data-stu-id="b3737-131">Static constructors are supported.</span></span> <span data-ttu-id="b3737-132">Inicializálási kifejezések értékkel rendelkező tulajdonságok a rendszer konstruktorban kód futtatása előtt inicializálja.</span><span class="sxs-lookup"><span data-stu-id="b3737-132">Properties with initialization expressions are initialized before running any code in a constructor.</span></span> <span data-ttu-id="b3737-133">A statikus tulajdonságok inicializálása előtt statikus konstruktorban törzsét, és objektumpéldány tulajdonságai inicializálása előtt nem statikus konstruktorban törzsét.</span><span class="sxs-lookup"><span data-stu-id="b3737-133">Static properties are initialized before the body of a static constructor, and instance properties are initialized before the body of the non-static constructor.</span></span> <span data-ttu-id="b3737-134">Jelenleg nincs konstruktor a másik konstruktor hívásakor szintaxis (például a C\# szintaxis ": this()").</span><span class="sxs-lookup"><span data-stu-id="b3737-134">Currently, there is no syntax for calling a constructor from another constructor (like the C\# syntax ": this()").</span></span> <span data-ttu-id="b3737-135">Kerülő megoldás lehet egy közös Init metódus meghatározásához.</span><span class="sxs-lookup"><span data-stu-id="b3737-135">The workaround is to define a common Init method.</span></span> 

<span data-ttu-id="b3737-136">A következő módon példányának osztályok ebben a kiadásban.</span><span class="sxs-lookup"><span data-stu-id="b3737-136">The following are ways of instantiating classes in this release.</span></span>

<span data-ttu-id="b3737-137">Létrehozza az alapértelmezett konstruktor használatával.</span><span class="sxs-lookup"><span data-stu-id="b3737-137">Instantiating by using the default constructor.</span></span> <span data-ttu-id="b3737-138">Vegye figyelembe, hogy a New-Object nem támogatott ebben a kiadásban.</span><span class="sxs-lookup"><span data-stu-id="b3737-138">Note that New-Object is not supported in this release.</span></span>

```powershell
$a = [MyClass]::new()
```

<span data-ttu-id="b3737-139">Egy paraméterrel rendelkező konstruktor hívása</span><span class="sxs-lookup"><span data-stu-id="b3737-139">Calling a constructor with a parameter</span></span>

```powershell
$b = [MyClass]::new(42)
```

<span data-ttu-id="b3737-140">Egy tömb átadni több paraméterekkel rendelkező konstruktor</span><span class="sxs-lookup"><span data-stu-id="b3737-140">Passing an array to a constructor with multiple parameters</span></span>
```powershell
$c = [MyClass]::new(@(42,43,44), "Hello")
```

<span data-ttu-id="b3737-141">Ebben a kiadásban a New-Object nem működik a Windows PowerShell-ben definiált osztályokkal.</span><span class="sxs-lookup"><span data-stu-id="b3737-141">In this release, New-Object does not work with classes defined in Windows PowerShell.</span></span> <span data-ttu-id="b3737-142">Ebben a kiadásban a következő típusnév is csak látható lexically, ami azt jelenti, nem látható a modul vagy a parancsfájl az osztályt definiáló kívül.</span><span class="sxs-lookup"><span data-stu-id="b3737-142">Also for this release, the type name is only visible lexically, meaning it is not visible outside of the module or script that defines the class.</span></span> <span data-ttu-id="b3737-143">Funkciók Windows PowerShell meghatározott osztály példányainak lépjen vissza, és példányok működik jól kívül a modul vagy a parancsfájlhoz.</span><span class="sxs-lookup"><span data-stu-id="b3737-143">Functions can return instances of a class defined in Windows PowerShell, and instances work well outside of the module or script.</span></span>

<span data-ttu-id="b3737-144">`Get-Member -Static`konstruktorok, sorolja fel, mint bármely más módszerrel túlterhelések szeretné megjeleníteni.</span><span class="sxs-lookup"><span data-stu-id="b3737-144">`Get-Member -Static` lists constructors, so you can view overloads like any other method.</span></span> <span data-ttu-id="b3737-145">Az ezen szintakszist teljesítménye is jelentősen gyorsabb, mint a New-Object.</span><span class="sxs-lookup"><span data-stu-id="b3737-145">The performance of this syntax is also considerably faster than New-Object.</span></span>

<span data-ttu-id="b3737-146">A pszeudo statikus metódus nevű **új** .NET tárolóhelytípussal működik, a következő példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="b3737-146">The pseudo-static method named **new** works with .NET types, as shown in the following example.</span></span>

```powershell
[hashtable]::new()
```

<span data-ttu-id="b3737-147">Most már megtekintheti konstruktor túlterhelések Get-tag, illetve ez a példa látható:</span><span class="sxs-lookup"><span data-stu-id="b3737-147">You can now see constructor overloads with Get-Member, or as shown in this example:</span></span>

```powershell
PS> [hashtable]::new
OverloadDefinitions
-------------------
hashtable new()
hashtable new(int capacity)
hashtable new(int capacity, float loadFactor)
```

## <a name="methods"></a><span data-ttu-id="b3737-148">Metódusok</span><span class="sxs-lookup"><span data-stu-id="b3737-148">Methods</span></span>

<span data-ttu-id="b3737-149">A Windows PowerShell osztály adott metódusát, a scriptblock kulcsszót, amelynek csak egy záró blokk lett megvalósítva.</span><span class="sxs-lookup"><span data-stu-id="b3737-149">A Windows PowerShell class method is implemented as a ScriptBlock that has only an end block.</span></span> <span data-ttu-id="b3737-150">Minden módszereket nyilvános.</span><span class="sxs-lookup"><span data-stu-id="b3737-150">All methods are public.</span></span> <span data-ttu-id="b3737-151">A következő nevű metódus meghatározásának példáját mutatja be **DoSomething**.</span><span class="sxs-lookup"><span data-stu-id="b3737-151">The following shows an example of defining a method named **DoSomething**.</span></span>

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

<span data-ttu-id="b3737-152">A metódushívás:</span><span class="sxs-lookup"><span data-stu-id="b3737-152">Method invocation:</span></span>

```powershell
$b = [MyClass]::new()
$b.DoSomething(42) 
```

<span data-ttu-id="b3737-153">Túlterhelt metódusok – Ez azt jelenti, hogy a meglévő metódus azonos nevű, de a megadott értékek--szerint megkülönböztetett is támogatott.</span><span class="sxs-lookup"><span data-stu-id="b3737-153">Overloaded methods--that is, those that are named the same as an existing method, but differentiated by their specified values--are also supported.</span></span>

## <a name="properties"></a><span data-ttu-id="b3737-154">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="b3737-154">Properties</span></span> 

<span data-ttu-id="b3737-155">Az összes tulajdonság olyan nyilvános.</span><span class="sxs-lookup"><span data-stu-id="b3737-155">All properties are public.</span></span> <span data-ttu-id="b3737-156">Tulajdonságok szükség soremelés vagy pontosvesszővel válassza el.</span><span class="sxs-lookup"><span data-stu-id="b3737-156">Properties require either a newline or semicolon.</span></span> <span data-ttu-id="b3737-157">Ha nincs objektum típusaként van megadva, a a tulajdonság típusa nem objektum.</span><span class="sxs-lookup"><span data-stu-id="b3737-157">If no object type is specified, the property type is object.</span></span>

<span data-ttu-id="b3737-158">Érvényesítési attribútumot, vagy argumentum átalakítása attribútumok használó tulajdonságok (pl. `[ValidateSet("aaa")]`) a várt módon működik.</span><span class="sxs-lookup"><span data-stu-id="b3737-158">Properties that use validation attributes or argument transformation attributes (e.g. `[ValidateSet("aaa")]`) work as expected.</span></span>

## <a name="hidden"></a><span data-ttu-id="b3737-159">Rejtett</span><span class="sxs-lookup"><span data-stu-id="b3737-159">Hidden</span></span>

<span data-ttu-id="b3737-160">Egy új kulcsszó **rejtett**, hozzá lett adva.</span><span class="sxs-lookup"><span data-stu-id="b3737-160">A new keyword, **Hidden**, has been added.</span></span> <span data-ttu-id="b3737-161">**Rejtett** tulajdonságai és metódusai (beleértve a konstruktorok) alkalmazhatók.</span><span class="sxs-lookup"><span data-stu-id="b3737-161">**Hidden** can be applied to properties and methods (including constructors).</span></span>

<span data-ttu-id="b3737-162">A rejtett tagokat nyilvános, de nem jelennek meg a Get-tag kimeneti kivéve, ha a - Force paramétert.</span><span class="sxs-lookup"><span data-stu-id="b3737-162">Hidden members are public, but do not appear in the output of Get-Member unless the -Force parameter is added.</span></span>

<span data-ttu-id="b3737-163">Rejtett tagok nincsenek mikor befejeződését, vagy az Intellisense segítségével, kivéve, ha a létrehozása után következik be, a rejtett tag definiáló osztály fülre.</span><span class="sxs-lookup"><span data-stu-id="b3737-163">Hidden members are not included when tab completing or using Intellisense unless the completion occurs in the class defining the hidden member.</span></span>

<span data-ttu-id="b3737-164">Új attribútum **System.Management.Automation.HiddenAttribute** bővült, így C#-kódban a Windows PowerShell belül azonos szemantikáját.</span><span class="sxs-lookup"><span data-stu-id="b3737-164">A new attribute, **System.Management.Automation.HiddenAttribute** has been added so that C# code can have the same semantics within Windows PowerShell.</span></span>

## <a name="return-types"></a><span data-ttu-id="b3737-165">Visszatérési típusokat</span><span class="sxs-lookup"><span data-stu-id="b3737-165">Return types</span></span>

<span data-ttu-id="b3737-166">Visszatérési típusa a szerződést; az eredményül kapott értéket alakítja át a várt típusú.</span><span class="sxs-lookup"><span data-stu-id="b3737-166">Return type is a contract; the return value is converted to the expected type.</span></span> <span data-ttu-id="b3737-167">Ha nincs visszatérési típusa van megadva, a visszatérési típus érvénytelen.</span><span class="sxs-lookup"><span data-stu-id="b3737-167">If no return type is specified, the return type is void.</span></span> <span data-ttu-id="b3737-168">Nincsenek objektumok; streaming van objektumok nem lehet írni a feldolgozási sor szándékosan vagy véletlenül.</span><span class="sxs-lookup"><span data-stu-id="b3737-168">There is no streaming of objects; objects cannot be written to the pipeline either intentionally or by accident.</span></span>

## <a name="attributes"></a><span data-ttu-id="b3737-169">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="b3737-169">Attributes</span></span>

<span data-ttu-id="b3737-170">Két új attribútum **DscResource** és **DscProperty** lettek hozzáadva.</span><span class="sxs-lookup"><span data-stu-id="b3737-170">Two new attributes, **DscResource** and **DscProperty** have been added.</span></span>

## <a name="lexical-scoping-of-variables"></a><span data-ttu-id="b3737-171">A változók lexikális hatókörének beállítása</span><span class="sxs-lookup"><span data-stu-id="b3737-171">Lexical scoping of variables</span></span>

<span data-ttu-id="b3737-172">A következő példáját mutatja be, hogyan lexikális tartalmazó works ebben a kiadásban.</span><span class="sxs-lookup"><span data-stu-id="b3737-172">The following shows an example of how lexical scoping works in this release.</span></span>

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

## <a name="end-to-end-example"></a><span data-ttu-id="b3737-173">Végpontok – példa</span><span class="sxs-lookup"><span data-stu-id="b3737-173">End-to-End Example</span></span>

<span data-ttu-id="b3737-174">Az alábbi példa létrehoz egy HTML dinamikus stílus lap nyelvi (DSL) megvalósításának számos új, egyéni osztályok.</span><span class="sxs-lookup"><span data-stu-id="b3737-174">The following example creates several new, custom classes to implement an HTML dynamic style sheet language (DSL).</span></span> <span data-ttu-id="b3737-175">Ezt követően a példa ad segédfüggvények találhatók, az elem osztályt, például címsorok és táblák, részeként meghatározott elemtípus létrehozásához, mert típusok nem használhatók a modulok hatókörén kívül.</span><span class="sxs-lookup"><span data-stu-id="b3737-175">Then, the example adds helper functions to create specific element types as part of the element class, such as heading styles and tables, because types cannot be used outside the scope of a module.</span></span>

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
        TR (-join $Properties.Foreach{ TD ($row.$\_) } )
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

