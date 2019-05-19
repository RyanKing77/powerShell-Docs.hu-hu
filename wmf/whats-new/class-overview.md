---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
title: Egyéni típusok létrehozása PowerShell-osztályokkal
ms.openlocfilehash: 0dd5bbaca50abb746e15a7bb64a706c7eceee905
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65856237"
---
# <a name="creating-custom-types-using-powershell-classes"></a><span data-ttu-id="f5ee4-103">Egyéni típusok létrehozása PowerShell-osztályokkal</span><span class="sxs-lookup"><span data-stu-id="f5ee4-103">Creating Custom Types using PowerShell Classes</span></span>

<span data-ttu-id="f5ee4-104">PowerShell 5.0 új lehetőség a teljesen definiálják az osztályokat és a többi felhasználó által meghatározott típusok formális szintaxis és hasonlóan más objektumorientált programozási nyelveket szemantika használatával.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-104">PowerShell 5.0 added the ability to define classes and other user-defined types using formal syntax and semantics like other object-oriented programming languages.</span></span> <span data-ttu-id="f5ee4-105">A cél, hogy a fejlesztők és informatikai szakemberek PowerShell kihasználni a használati esetek szélesebb köre, leegyszerűsítheti a fejlesztést az PowerShell-összetevők (például a DSC-erőforrások) és gyorsítsa fel a felügyeleti felületek lefedettség engedélyezése.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-105">The goal is to enable developers and IT professionals to embrace PowerShell for a wider range of use cases, simplify development of PowerShell artifacts (such as DSC resources), and accelerate coverage of management surfaces.</span></span>

## <a name="supported-scenarios-in-this-release"></a><span data-ttu-id="f5ee4-106">Ebben a kiadásban támogatott helyzetek</span><span class="sxs-lookup"><span data-stu-id="f5ee4-106">Supported scenarios in this release</span></span>

- <span data-ttu-id="f5ee4-107">DSC-erőforrások és az azokhoz társított típusokat megadása a PowerShell nyelv segítségével</span><span class="sxs-lookup"><span data-stu-id="f5ee4-107">Define DSC resources and their associated types by using the PowerShell language</span></span>
- <span data-ttu-id="f5ee4-108">Egyéni típusok definiálása a PowerShellben a jól ismert objektumorientált programozási módszerek, például az osztályokat, tulajdonságokat, módszerek használatával.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-108">Define custom types in PowerShell by using familiar object-oriented programming constructs, such as classes, properties, methods, etc.</span></span>
- <span data-ttu-id="f5ee4-109">Öröklés támogatására az osztály a PowerShell és az osztály base DSC-erőforrás</span><span class="sxs-lookup"><span data-stu-id="f5ee4-109">Inheritance support with class in PowerShell and class base DSC resource</span></span>
- <span data-ttu-id="f5ee4-110">Típusok hibakeresés a PowerShell nyelv használatával</span><span class="sxs-lookup"><span data-stu-id="f5ee4-110">Debug types by using the PowerShell language</span></span>
- <span data-ttu-id="f5ee4-111">Hozzon létre, és a kivételek kezelésére, formális mechanizmusok használatával, és a megfelelő szinten</span><span class="sxs-lookup"><span data-stu-id="f5ee4-111">Generate and handle exceptions by using formal mechanisms, and at the right level</span></span>

# <a name="declare-base-class"></a><span data-ttu-id="f5ee4-112">Alaposztály deklarálása</span><span class="sxs-lookup"><span data-stu-id="f5ee4-112">Declare Base Class</span></span>

<span data-ttu-id="f5ee4-113">Egy PowerShell osztály eszközhöz adhat meg, egy másik PowerShell osztály alaptípusa.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-113">You can declare a PowerShell class as a base type for another PowerShell class.</span></span>

```powershell
class bar
{
   [int]foo()
       {
           return 100500
       }
}

class baz : bar {}

[baz]::new().foo() # return 100500
```

<span data-ttu-id="f5ee4-114">Használhatja a meglévő .NET-keretrendszer típusok osztályok:</span><span class="sxs-lookup"><span data-stu-id="f5ee4-114">You can also use existing .NET Framework types as base classes:</span></span>

```powershell
class MyIntList : system.collections.generic.list[int]
{

}

$list = [MyIntList]::new()

$list.Add(100)

$list[0] # return 100
```

# <a name="call-base-class-constructor"></a><span data-ttu-id="f5ee4-115">Alaposztály konstruktorának hívása</span><span class="sxs-lookup"><span data-stu-id="f5ee4-115">Call Base Class Constructor</span></span>

<span data-ttu-id="f5ee4-116">Alaposztály konstruktorának hívása egy alosztályt, használja a kulcsszó **alap**:</span><span class="sxs-lookup"><span data-stu-id="f5ee4-116">To call a base class constructor from a subclass, use the keyword **base**:</span></span>

```powershell
class A
{
    [int]$a

    A([int]$a)
    {
        $this.a = $a
    }
}

class B : A
{
    B() : base(103) {}
}

[B]::new().a # return 103
```

<span data-ttu-id="f5ee4-117">Ha egy osztály (nincs paraméter) alapértelmezett konstruktort, kihagyhatja egy explicit konstruktor hívás:</span><span class="sxs-lookup"><span data-stu-id="f5ee4-117">If a base class has a default (no parameter) constructor, you can omit an explicit constructor call:</span></span>

```powershell
class C : B
{
    C([int]$c) {}
}
```

# <a name="call-base-class-method"></a><span data-ttu-id="f5ee4-118">Alaposztály metódusának hívása</span><span class="sxs-lookup"><span data-stu-id="f5ee4-118">Call Base Class Method</span></span>

<span data-ttu-id="f5ee4-119">A meglévő módszerek az alosztályok felül lehet bírálni.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-119">You can override existing methods in subclasses.</span></span> <span data-ttu-id="f5ee4-120">Ehhez deklarálja a módszerek ilyen névvel és aláírás használatával:</span><span class="sxs-lookup"><span data-stu-id="f5ee4-120">To do this, declare methods by using the same name and signature:</span></span>

```powershell
class baseClass
{
    [int]foo() {return 100500}
}

class childClass1 : baseClass
{
    [int]foo() {return 200600}
}

[childClass1]::new().foo() # return 200600
```

<span data-ttu-id="f5ee4-121">Alaposztály módszerek meghívhatnak felülbírált megvalósításokhoz, konvertálni az alaposztály (`[baseClass]$this`) a meghívási:</span><span class="sxs-lookup"><span data-stu-id="f5ee4-121">To call base class methods from overridden implementations, cast to the base class (`[baseClass]$this`) on invocation:</span></span>

```powershell
class childClass2 : baseClass
{
    [int]foo()
    {
        return 3 * ([baseClass]$this).foo()
    }
}

[childClass2]::new().foo() # return 301500
```

<span data-ttu-id="f5ee4-122">Az összes PowerShell-módszer olyan virtuális.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-122">All PowerShell methods are virtual.</span></span> <span data-ttu-id="f5ee4-123">Ugyanazt a szintaxist is felülbírálást, azonos nevű és aláírás módszerek deklarálásával használatával elrejtheti alosztályát nem virtuális .NET-metódusokat.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-123">You can hide non-virtual .NET methods in a subclass by using the same syntax as you do for an override, by declaring methods with same name and signature.</span></span>

```powershell
class MyIntList : system.collections.generic.list[int]
{
    # Add is final in system.collections.generic.list
    [void] Add([int]$arg)
    {
        ([system.collections.generic.list[int]]$this).Add($arg * 2)
    }
}

$list = [MyIntList]::new()
$list.Add(100)
$list[0] # return 200
```

# <a name="declare-implemented-interface"></a><span data-ttu-id="f5ee4-124">Megvalósított interfész deklarálása</span><span class="sxs-lookup"><span data-stu-id="f5ee4-124">Declare Implemented Interface</span></span>

<span data-ttu-id="f5ee4-125">Eszközhöz adhat meg implementovaná rozhraní típusok, vagy közvetlenül egy kettőspontot (:), ha nincs megadva alap típus.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-125">You can declare implemented interfaces after base types, or immediately after a colon (:), if there is no base type specified.</span></span> <span data-ttu-id="f5ee4-126">Írja be az összes vesszőkkel válassza el egymástól a neveket.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-126">Separate all type names by using commas.</span></span> <span data-ttu-id="f5ee4-127">Ez hasonlít C# szintaxist.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-127">It's similar to C# syntax.</span></span>

```powershell
class MyComparable : system.IComparable
{
    [int] CompareTo([object] $obj)
    {
        return 0;
    }
}

class MyComparableBar : bar, system.IComparable
{
    [int] CompareTo([object] $obj)
    {
        return 0;
    }
}
```

# <a name="new-language-features-in-powershell-50"></a><span data-ttu-id="f5ee4-128">A PowerShell 5.0 új nyelvi funkciók</span><span class="sxs-lookup"><span data-stu-id="f5ee4-128">New language features in PowerShell 5.0</span></span>

<span data-ttu-id="f5ee4-129">PowerShell 5.0 vezet be a következő új nyelvi elemei a PowerShellben:</span><span class="sxs-lookup"><span data-stu-id="f5ee4-129">PowerShell 5.0 introduces the following new language elements in PowerShell:</span></span>

## <a name="class-keyword"></a><span data-ttu-id="f5ee4-130">Osztály kulcsszó</span><span class="sxs-lookup"><span data-stu-id="f5ee4-130">Class keyword</span></span>

<span data-ttu-id="f5ee4-131">A `class` kulcsszó határozza meg egy új osztályt.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-131">The `class` keyword defines a new class.</span></span> <span data-ttu-id="f5ee4-132">Ez a valódi .NET-keretrendszer típusa.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-132">This is a true .NET Framework type.</span></span> <span data-ttu-id="f5ee4-133">A osztályelemen nyilvános, de csak nyilvános modul hatókörébe.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-133">Class members are public, but only public within the module scope.</span></span> <span data-ttu-id="f5ee4-134">Nem lehet hivatkozni a típusnév karakterláncként (például `New-Object` nem működik), ebben a kiadásban, és nem használhat olyan típusú konstans (például `[MyClass]`) kívül a parancsfájlt vagy modul fájlt, amelyhez az osztály definiálva van.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-134">You can't refer to the type name as a string (for example, `New-Object` doesn't work), and in this release, you can't use a type literal (for example, `[MyClass]`) outside the script or module file in which the class is defined.</span></span>

```powershell
class MyClass
{
    ...
}
```

## <a name="enum-keyword-and-enumerations"></a><span data-ttu-id="f5ee4-135">Enum kulcsszó és enumerálásokat tartalmaznak</span><span class="sxs-lookup"><span data-stu-id="f5ee4-135">Enum keyword and enumerations</span></span>

<span data-ttu-id="f5ee4-136">Támogatja a `enum` kulcsszó hozzá lett adva, melyik soremelés használ elválasztóként.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-136">Support for the `enum` keyword has been added, which uses newline as the delimiter.</span></span> <span data-ttu-id="f5ee4-137">Jelenleg nem lehet definiálni enumerátor maga tekintetében.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-137">Currently, you cannot define an enumerator in terms of itself.</span></span> <span data-ttu-id="f5ee4-138">Azonban egy másik enum tekintetében enum inicializálása, az alábbi példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-138">However, you can initialize an enum in terms of another enum, as shown in the following example.</span></span> <span data-ttu-id="f5ee4-139">Základní typ is, nem adható meg; a rendszer mindig `[int]`.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-139">Also, the base type cannot be specified; it is always `[int]`.</span></span>

```powershell
enum Color2
{
    Yellow = [Color]::Blue
}
```

<span data-ttu-id="f5ee4-140">Az enumerálóérték parse time állandónak kell lennie.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-140">An enumerator value must be a parse time constant.</span></span> <span data-ttu-id="f5ee4-141">Egy meghívott parancs eredménye nem állítható be azt.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-141">You cannot set it to the result of an invoked command.</span></span>

```powershell
enum MyEnum
{
    Enum1
    Enum2
    Enum3 = 42
    Enum4 = [int]::MaxValue
}
```

<span data-ttu-id="f5ee4-142">Enumerálások aritmetikai műveletek támogatásához, az alábbi példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-142">Enums support arithmetic operations, as shown in the following example.</span></span>

```powershell
enum SomeEnum { Max = 42 }
enum OtherEnum { Max = [SomeEnum]::Max + 1 }
```

## <a name="import-dscresource"></a><span data-ttu-id="f5ee4-143">Import-DscResource</span><span class="sxs-lookup"><span data-stu-id="f5ee4-143">Import-DscResource</span></span>

<span data-ttu-id="f5ee4-144">`Import-DscResource` már true dinamikus kulcsszó.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-144">`Import-DscResource` is now a true dynamic keyword.</span></span> <span data-ttu-id="f5ee4-145">PowerShell elemzi a megadott modul legfelső szintű modul, osztályban, amelyek tartalmazzák a Keresés a **DscResource** attribútum.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-145">PowerShell parses the specified module's root module, searching for classes that contain the **DscResource** attribute.</span></span>

## <a name="implementingassembly"></a><span data-ttu-id="f5ee4-146">ImplementingAssembly</span><span class="sxs-lookup"><span data-stu-id="f5ee4-146">ImplementingAssembly</span></span>

<span data-ttu-id="f5ee4-147">Egy új mezőt **ImplementingAssembly**, hozzá van adva **ModuleInfo**.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-147">A new field, **ImplementingAssembly**, has been added to **ModuleInfo**.</span></span> <span data-ttu-id="f5ee4-148">Azt a dinamikus szerelvény egy szkriptmodulba készült, ha a parancsfájl definiálja azokat az osztályokat, vagy a betöltött szerelvény a bináris modulok van beállítva.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-148">It is set to the dynamic assembly created for a script module if the script defines classes, or the loaded assembly for binary modules.</span></span> <span data-ttu-id="f5ee4-149">Nincs beállítva mikor **ModuleType** van **Manifest**.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-149">It is not set when **ModuleType** is **Manifest**.</span></span>

<span data-ttu-id="f5ee4-150">A reflexió a **ImplementingAssembly** mező felderítette az erőforrásokat egy modulban.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-150">Reflection on the **ImplementingAssembly** field discovers resources in a module.</span></span> <span data-ttu-id="f5ee4-151">Ez azt jelenti, hogy a PowerShell vagy más felügyelt nyelveken írt erőforrások deríthet fel.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-151">This means you can discover resources written in either PowerShell or other managed languages.</span></span>

<span data-ttu-id="f5ee4-152">Inicializátory mezőket:</span><span class="sxs-lookup"><span data-stu-id="f5ee4-152">Fields with initializers:</span></span>

```powershell
[int] $i = 5
```

<span data-ttu-id="f5ee4-153">`Static` támogatott.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-153">`Static` is supported.</span></span> <span data-ttu-id="f5ee4-154">Úgy működik egy attribútum, például, mint az ajánlattípusra vonatkozó megkötések.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-154">It works like an attribute, as do the type constraints.</span></span> <span data-ttu-id="f5ee4-155">Bármilyen sorrendben adható meg.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-155">It can be specified in any order.</span></span>

```powershell
static [int] $count = 0
```

<span data-ttu-id="f5ee4-156">Egy nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-156">A type is optional.</span></span>

```powershell
$s = "hello"
```

<span data-ttu-id="f5ee4-157">Minden tag nyilvánosak legyenek.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-157">All members are public.</span></span>

## <a name="constructors-and-instantiation"></a><span data-ttu-id="f5ee4-158">Konstruktorok és példányosítás</span><span class="sxs-lookup"><span data-stu-id="f5ee4-158">Constructors and instantiation</span></span>

<span data-ttu-id="f5ee4-159">PowerShell-osztályok konstruktorok is rendelkezhet.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-159">PowerShell classes can have constructors.</span></span> <span data-ttu-id="f5ee4-160">A neve megegyezik az osztály rendelkeznek.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-160">They have the same name as their class.</span></span> <span data-ttu-id="f5ee4-161">Is túlterhelt konstruktorral.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-161">Constructors can be overloaded.</span></span> <span data-ttu-id="f5ee4-162">Statikus konstruktorok támogatottak.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-162">Static constructors are supported.</span></span> <span data-ttu-id="f5ee4-163">Tulajdonságok inicializálási kifejezésekkel inicializálása konstruktorban kód futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-163">Properties with initialization expressions are initialized before running any code in a constructor.</span></span> <span data-ttu-id="f5ee4-164">A statikus tulajdonságok inicializálása előtt egy statikus konstruktor törzse, és a példány tulajdonságainak inicializálása előtt nem statikus konstruktor törzse.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-164">Static properties are initialized before the body of a static constructor, and instance properties are initialized before the body of the non-static constructor.</span></span> <span data-ttu-id="f5ee4-165">Jelenleg nincs másik konstruktor konstruktor megismernie szintaxisának (például a C\# szintaxis ": this()").</span><span class="sxs-lookup"><span data-stu-id="f5ee4-165">Currently, there is no syntax for calling a constructor from another constructor (like the C\# syntax ": this()").</span></span> <span data-ttu-id="f5ee4-166">A megoldás az, hogy egy közös definiálása `Init()` metódust.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-166">The workaround is to define a common `Init()` method.</span></span>

### <a name="creating-instances"></a><span data-ttu-id="f5ee4-167">Példány létrehozása</span><span class="sxs-lookup"><span data-stu-id="f5ee4-167">Creating instances</span></span>

> [!NOTE]
> <span data-ttu-id="f5ee4-168">A PowerShell 5.0-s `New-Object` PowerShell-ben definiált osztályokkal nem működik.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-168">In PowerShell 5.0, `New-Object` does not work with classes defined in PowerShell.</span></span> <span data-ttu-id="f5ee4-169">Název typu is csak látható betűrendbe, ami azt jelenti, már nem látható a modul vagy a parancsfájl az osztályt definiáló kívül.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-169">Also, the type name is only visible lexically, meaning it is not visible outside of the module or script that defines the class.</span></span> <span data-ttu-id="f5ee4-170">Függvények PowerShell meghatározott osztály példányainak adhat vissza.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-170">Functions can return instances of a class defined in PowerShell.</span></span> <span data-ttu-id="f5ee4-171">Ezekhez a példányokhoz kívül a modul vagy a parancsfájl működik.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-171">Those instances work outside of the module or script.</span></span>

1. <span data-ttu-id="f5ee4-172">Hárítható el, az alapértelmezett konstruktort használatával.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-172">Instantiating by using the default constructor.</span></span>

   ```powershell
   $a = [MyClass]::new()
   ```

1. <span data-ttu-id="f5ee4-173">A konstruktor egy paraméterrel hívása</span><span class="sxs-lookup"><span data-stu-id="f5ee4-173">Calling a constructor with a parameter</span></span>

   ```powershell
   $b = [MyClass]::new(42)
   ```

1. <span data-ttu-id="f5ee4-174">Egy tömb átadja egy több paraméterekkel rendelkező konstruktort.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-174">Passing an array to a constructor with multiple parameters.</span></span>

   ```powershell
   $c = [MyClass]::new(@(42,43,44), "Hello")
   ```

<span data-ttu-id="f5ee4-175">A pszeudo statická metoda `new()` együttműködik a .NET-típusok, az alábbi példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-175">The pseudo-static method `new()` works with .NET types, as shown in the following example.</span></span>

```powershell
[hashtable]::new()
```

### <a name="discovering-constructors"></a><span data-ttu-id="f5ee4-176">Konstruktorok felderítése</span><span class="sxs-lookup"><span data-stu-id="f5ee4-176">Discovering constructors</span></span>

<span data-ttu-id="f5ee4-177">Most már megtekintheti a konstruktor túlterheléssel `Get-Member`, vagy az ebben a példában látható módon:</span><span class="sxs-lookup"><span data-stu-id="f5ee4-177">You can now see constructor overloads with `Get-Member`, or as shown in this example:</span></span>

```powershell
PS> [hashtable]::new
OverloadDefinitions
-------------------
hashtable new()
hashtable new(int capacity)
hashtable new(int capacity, float loadFactor)
```

<span data-ttu-id="f5ee4-178">`Get-Member -Static` konstruktorok, sorolja fel, hogy meg tudja tekinteni a túlterhelések, mint bármely más módszerrel.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-178">`Get-Member -Static` lists constructors, so you can view overloads like any other method.</span></span> <span data-ttu-id="f5ee4-179">Ez a szintaxis teljesítményét egyben jelentősen gyorsabb, mint `New-Object`.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-179">The performance of this syntax is also considerably faster than `New-Object`.</span></span>

## <a name="methods"></a><span data-ttu-id="f5ee4-180">Metódusok</span><span class="sxs-lookup"><span data-stu-id="f5ee4-180">Methods</span></span>

<span data-ttu-id="f5ee4-181">Egy PowerShell-osztály metódusának van megvalósítva egy **ScriptBlock** , amelynek csak egy záró blokk.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-181">A PowerShell class method is implemented as a **ScriptBlock** that has only an end block.</span></span> <span data-ttu-id="f5ee4-182">Az összes módszer nyilvánosak legyenek.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-182">All methods are public.</span></span> <span data-ttu-id="f5ee4-183">A következő nevű metódus meghatározása példán látható **DoSomething**.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-183">The following shows an example of defining a method named **DoSomething**.</span></span>

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

<span data-ttu-id="f5ee4-184">Metódushívás:</span><span class="sxs-lookup"><span data-stu-id="f5ee4-184">Method invocation:</span></span>

```powershell
$b = [MyClass]::new()
$b.DoSomething(42)
```

<span data-ttu-id="f5ee4-185">Többszörösen definiált metódusok használata is támogatott.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-185">Overloaded methods are also supported.</span></span>

## <a name="properties"></a><span data-ttu-id="f5ee4-186">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="f5ee4-186">Properties</span></span>

<span data-ttu-id="f5ee4-187">Az összes tulajdonság nyilvánosak legyenek.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-187">All properties are public.</span></span> <span data-ttu-id="f5ee4-188">Tulajdonságok szükség soremelés vagy pontosvesszővel válassza el.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-188">Properties require either a newline or semicolon.</span></span> <span data-ttu-id="f5ee4-189">Ha nincs objektum típus van megadva, a tulajdonság típusának egy objektum.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-189">If no object type is specified, the property type is object.</span></span>

<span data-ttu-id="f5ee4-190">Érvényesítés vagy argumentum átalakítása attribútum használó tulajdonságok (például `[ValidateSet("aaa")]`) a várt módon működik.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-190">Properties that use validation or argument transformation attributes (like `[ValidateSet("aaa")]`) work as expected.</span></span>

## <a name="hidden"></a><span data-ttu-id="f5ee4-191">Rejtett</span><span class="sxs-lookup"><span data-stu-id="f5ee4-191">Hidden</span></span>

<span data-ttu-id="f5ee4-192">Egy új kulcsszó, `Hidden`, hozzá van adva.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-192">A new keyword, `Hidden`, has been added.</span></span> <span data-ttu-id="f5ee4-193">`Hidden` Tulajdonságok és metódusok (beleértve a konstruktorok) alkalmazhatók.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-193">`Hidden` can be applied to properties and methods (including constructors).</span></span>

<span data-ttu-id="f5ee4-194">Rejtett tagok nyilvános, de nem jelennek meg a kimenetét `Get-Member` , kivéve, ha a - Force paramétert.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-194">Hidden members are public, but do not appear in the output of `Get-Member` unless the -Force parameter is added.</span></span> <span data-ttu-id="f5ee4-195">A tagok nem tartoznak mikor rejtett lapon befejezése vagy az IntelliSense segítségével, kivéve, ha az osztály a rejtett tag meghatározása befejezése után történik.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-195">Hidden members are not included when tab completing or using Intellisense unless the completion occurs in the class defining the hidden member.</span></span>

<span data-ttu-id="f5ee4-196">Egy új attribútum **System.Management.Automation.HiddenAttribute** hozzá lett adva, a C\# kódot a Powershellen belülről azonos szemantikát is rendelkezhet.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-196">A new attribute, **System.Management.Automation.HiddenAttribute** has been added so that C\# code can have the same semantics within PowerShell.</span></span>

## <a name="return-types"></a><span data-ttu-id="f5ee4-197">Návratové typy</span><span class="sxs-lookup"><span data-stu-id="f5ee4-197">Return types</span></span>

<span data-ttu-id="f5ee4-198">Typ vrácené hodnoty je egy szerződést.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-198">Return type is a contract.</span></span> <span data-ttu-id="f5ee4-199">A visszaadott érték a várt típus alakítja át.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-199">The return value is converted to the expected type.</span></span> <span data-ttu-id="f5ee4-200">Ha nincs visszatérési típus van megadva, a typ vrácené hodnoty je **void**.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-200">If no return type is specified, the return type is **void**.</span></span> <span data-ttu-id="f5ee4-201">Nincs nem streaming-objektumok.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-201">There is no streaming of objects.</span></span> <span data-ttu-id="f5ee4-202">Bbjects nem lehet írni a folyamat szándékosan vagy véletlenül iratkozott le.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-202">Bbjects cannot be written to the pipeline either intentionally or by accident.</span></span>

## <a name="attributes"></a><span data-ttu-id="f5ee4-203">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="f5ee4-203">Attributes</span></span>

<span data-ttu-id="f5ee4-204">Két új attribútum **DscResource** és **DscProperty** lettek hozzáadva.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-204">Two new attributes, **DscResource** and **DscProperty** have been added.</span></span>

## <a name="lexical-scoping-of-variables"></a><span data-ttu-id="f5ee4-205">Lexikális hatókörkezeléséhez kapcsolódó változók</span><span class="sxs-lookup"><span data-stu-id="f5ee4-205">Lexical scoping of variables</span></span>

<span data-ttu-id="f5ee4-206">Az alábbi példán látható hogyan lexikai hatókörkezelési működik Ebben a kiadásban.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-206">The following shows an example of how lexical scoping works in this release.</span></span>

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

## <a name="end-to-end-example"></a><span data-ttu-id="f5ee4-207">Teljes körű – példa</span><span class="sxs-lookup"><span data-stu-id="f5ee4-207">End-to-End Example</span></span>

<span data-ttu-id="f5ee4-208">A következő példában létrehozunk néhány egyéni osztályok megvalósítása egy HTML dinamikus stílus lap nyelv (DSL).</span><span class="sxs-lookup"><span data-stu-id="f5ee4-208">The following example creates some custom classes to implement an HTML dynamic style sheet language (DSL).</span></span> <span data-ttu-id="f5ee4-209">Ezt követően a példa ad segédfüggvények hozhat létre egyedi elemtípus az elem osztályt, például a címsorok és a táblázatok, részeként, mert típusok nem használhatók egy modul hatókörén kívül.</span><span class="sxs-lookup"><span data-stu-id="f5ee4-209">Then, the example adds helper functions to create specific element types as part of the element class, such as heading styles and tables, because types cannot be used outside the scope of a module.</span></span>

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
# These are required because types aren't visible outside of the module.
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
