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
# <a name="creating-custom-types-using-powershell-classes"></a>Egyéni típusok létrehozása PowerShell-osztályokkal

PowerShell 5.0 új lehetőség a teljesen definiálják az osztályokat és a többi felhasználó által meghatározott típusok formális szintaxis és hasonlóan más objektumorientált programozási nyelveket szemantika használatával. A cél, hogy a fejlesztők és informatikai szakemberek PowerShell kihasználni a használati esetek szélesebb köre, leegyszerűsítheti a fejlesztést az PowerShell-összetevők (például a DSC-erőforrások) és gyorsítsa fel a felügyeleti felületek lefedettség engedélyezése.

## <a name="supported-scenarios-in-this-release"></a>Ebben a kiadásban támogatott helyzetek

- DSC-erőforrások és az azokhoz társított típusokat megadása a PowerShell nyelv segítségével
- Egyéni típusok definiálása a PowerShellben a jól ismert objektumorientált programozási módszerek, például az osztályokat, tulajdonságokat, módszerek használatával.
- Öröklés támogatására az osztály a PowerShell és az osztály base DSC-erőforrás
- Típusok hibakeresés a PowerShell nyelv használatával
- Hozzon létre, és a kivételek kezelésére, formális mechanizmusok használatával, és a megfelelő szinten

# <a name="declare-base-class"></a>Alaposztály deklarálása

Egy PowerShell osztály eszközhöz adhat meg, egy másik PowerShell osztály alaptípusa.

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

Használhatja a meglévő .NET-keretrendszer típusok osztályok:

```powershell
class MyIntList : system.collections.generic.list[int]
{

}

$list = [MyIntList]::new()

$list.Add(100)

$list[0] # return 100
```

# <a name="call-base-class-constructor"></a>Alaposztály konstruktorának hívása

Alaposztály konstruktorának hívása egy alosztályt, használja a kulcsszó **alap**:

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

Ha egy osztály (nincs paraméter) alapértelmezett konstruktort, kihagyhatja egy explicit konstruktor hívás:

```powershell
class C : B
{
    C([int]$c) {}
}
```

# <a name="call-base-class-method"></a>Alaposztály metódusának hívása

A meglévő módszerek az alosztályok felül lehet bírálni. Ehhez deklarálja a módszerek ilyen névvel és aláírás használatával:

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

Alaposztály módszerek meghívhatnak felülbírált megvalósításokhoz, konvertálni az alaposztály (`[baseClass]$this`) a meghívási:

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

Az összes PowerShell-módszer olyan virtuális. Ugyanazt a szintaxist is felülbírálást, azonos nevű és aláírás módszerek deklarálásával használatával elrejtheti alosztályát nem virtuális .NET-metódusokat.

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

# <a name="declare-implemented-interface"></a>Megvalósított interfész deklarálása

Eszközhöz adhat meg implementovaná rozhraní típusok, vagy közvetlenül egy kettőspontot (:), ha nincs megadva alap típus. Írja be az összes vesszőkkel válassza el egymástól a neveket. Ez hasonlít C# szintaxist.

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

# <a name="new-language-features-in-powershell-50"></a>A PowerShell 5.0 új nyelvi funkciók

PowerShell 5.0 vezet be a következő új nyelvi elemei a PowerShellben:

## <a name="class-keyword"></a>Osztály kulcsszó

A `class` kulcsszó határozza meg egy új osztályt. Ez a valódi .NET-keretrendszer típusa. A osztályelemen nyilvános, de csak nyilvános modul hatókörébe. Nem lehet hivatkozni a típusnév karakterláncként (például `New-Object` nem működik), ebben a kiadásban, és nem használhat olyan típusú konstans (például `[MyClass]`) kívül a parancsfájlt vagy modul fájlt, amelyhez az osztály definiálva van.

```powershell
class MyClass
{
    ...
}
```

## <a name="enum-keyword-and-enumerations"></a>Enum kulcsszó és enumerálásokat tartalmaznak

Támogatja a `enum` kulcsszó hozzá lett adva, melyik soremelés használ elválasztóként. Jelenleg nem lehet definiálni enumerátor maga tekintetében. Azonban egy másik enum tekintetében enum inicializálása, az alábbi példában látható módon. Základní typ is, nem adható meg; a rendszer mindig `[int]`.

```powershell
enum Color2
{
    Yellow = [Color]::Blue
}
```

Az enumerálóérték parse time állandónak kell lennie. Egy meghívott parancs eredménye nem állítható be azt.

```powershell
enum MyEnum
{
    Enum1
    Enum2
    Enum3 = 42
    Enum4 = [int]::MaxValue
}
```

Enumerálások aritmetikai műveletek támogatásához, az alábbi példában látható módon.

```powershell
enum SomeEnum { Max = 42 }
enum OtherEnum { Max = [SomeEnum]::Max + 1 }
```

## <a name="import-dscresource"></a>Import-DscResource

`Import-DscResource` már true dinamikus kulcsszó. PowerShell elemzi a megadott modul legfelső szintű modul, osztályban, amelyek tartalmazzák a Keresés a **DscResource** attribútum.

## <a name="implementingassembly"></a>ImplementingAssembly

Egy új mezőt **ImplementingAssembly**, hozzá van adva **ModuleInfo**. Azt a dinamikus szerelvény egy szkriptmodulba készült, ha a parancsfájl definiálja azokat az osztályokat, vagy a betöltött szerelvény a bináris modulok van beállítva. Nincs beállítva mikor **ModuleType** van **Manifest**.

A reflexió a **ImplementingAssembly** mező felderítette az erőforrásokat egy modulban. Ez azt jelenti, hogy a PowerShell vagy más felügyelt nyelveken írt erőforrások deríthet fel.

Inicializátory mezőket:

```powershell
[int] $i = 5
```

`Static` támogatott. Úgy működik egy attribútum, például, mint az ajánlattípusra vonatkozó megkötések. Bármilyen sorrendben adható meg.

```powershell
static [int] $count = 0
```

Egy nem kötelező.

```powershell
$s = "hello"
```

Minden tag nyilvánosak legyenek.

## <a name="constructors-and-instantiation"></a>Konstruktorok és példányosítás

PowerShell-osztályok konstruktorok is rendelkezhet. A neve megegyezik az osztály rendelkeznek. Is túlterhelt konstruktorral. Statikus konstruktorok támogatottak. Tulajdonságok inicializálási kifejezésekkel inicializálása konstruktorban kód futtatása előtt. A statikus tulajdonságok inicializálása előtt egy statikus konstruktor törzse, és a példány tulajdonságainak inicializálása előtt nem statikus konstruktor törzse. Jelenleg nincs másik konstruktor konstruktor megismernie szintaxisának (például a C\# szintaxis ": this()"). A megoldás az, hogy egy közös definiálása `Init()` metódust.

### <a name="creating-instances"></a>Példány létrehozása

> [!NOTE]
> A PowerShell 5.0-s `New-Object` PowerShell-ben definiált osztályokkal nem működik. Název typu is csak látható betűrendbe, ami azt jelenti, már nem látható a modul vagy a parancsfájl az osztályt definiáló kívül. Függvények PowerShell meghatározott osztály példányainak adhat vissza. Ezekhez a példányokhoz kívül a modul vagy a parancsfájl működik.

1. Hárítható el, az alapértelmezett konstruktort használatával.

   ```powershell
   $a = [MyClass]::new()
   ```

1. A konstruktor egy paraméterrel hívása

   ```powershell
   $b = [MyClass]::new(42)
   ```

1. Egy tömb átadja egy több paraméterekkel rendelkező konstruktort.

   ```powershell
   $c = [MyClass]::new(@(42,43,44), "Hello")
   ```

A pszeudo statická metoda `new()` együttműködik a .NET-típusok, az alábbi példában látható módon.

```powershell
[hashtable]::new()
```

### <a name="discovering-constructors"></a>Konstruktorok felderítése

Most már megtekintheti a konstruktor túlterheléssel `Get-Member`, vagy az ebben a példában látható módon:

```powershell
PS> [hashtable]::new
OverloadDefinitions
-------------------
hashtable new()
hashtable new(int capacity)
hashtable new(int capacity, float loadFactor)
```

`Get-Member -Static` konstruktorok, sorolja fel, hogy meg tudja tekinteni a túlterhelések, mint bármely más módszerrel. Ez a szintaxis teljesítményét egyben jelentősen gyorsabb, mint `New-Object`.

## <a name="methods"></a>Metódusok

Egy PowerShell-osztály metódusának van megvalósítva egy **ScriptBlock** , amelynek csak egy záró blokk. Az összes módszer nyilvánosak legyenek. A következő nevű metódus meghatározása példán látható **DoSomething**.

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

Metódushívás:

```powershell
$b = [MyClass]::new()
$b.DoSomething(42)
```

Többszörösen definiált metódusok használata is támogatott.

## <a name="properties"></a>Tulajdonságok

Az összes tulajdonság nyilvánosak legyenek. Tulajdonságok szükség soremelés vagy pontosvesszővel válassza el. Ha nincs objektum típus van megadva, a tulajdonság típusának egy objektum.

Érvényesítés vagy argumentum átalakítása attribútum használó tulajdonságok (például `[ValidateSet("aaa")]`) a várt módon működik.

## <a name="hidden"></a>Rejtett

Egy új kulcsszó, `Hidden`, hozzá van adva. `Hidden` Tulajdonságok és metódusok (beleértve a konstruktorok) alkalmazhatók.

Rejtett tagok nyilvános, de nem jelennek meg a kimenetét `Get-Member` , kivéve, ha a - Force paramétert. A tagok nem tartoznak mikor rejtett lapon befejezése vagy az IntelliSense segítségével, kivéve, ha az osztály a rejtett tag meghatározása befejezése után történik.

Egy új attribútum **System.Management.Automation.HiddenAttribute** hozzá lett adva, a C\# kódot a Powershellen belülről azonos szemantikát is rendelkezhet.

## <a name="return-types"></a>Návratové typy

Typ vrácené hodnoty je egy szerződést. A visszaadott érték a várt típus alakítja át. Ha nincs visszatérési típus van megadva, a typ vrácené hodnoty je **void**. Nincs nem streaming-objektumok. Bbjects nem lehet írni a folyamat szándékosan vagy véletlenül iratkozott le.

## <a name="attributes"></a>Attribútumok

Két új attribútum **DscResource** és **DscProperty** lettek hozzáadva.

## <a name="lexical-scoping-of-variables"></a>Lexikális hatókörkezeléséhez kapcsolódó változók

Az alábbi példán látható hogyan lexikai hatókörkezelési működik Ebben a kiadásban.

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

## <a name="end-to-end-example"></a>Teljes körű – példa

A következő példában létrehozunk néhány egyéni osztályok megvalósítása egy HTML dinamikus stílus lap nyelv (DSL). Ezt követően a példa ad segédfüggvények hozhat létre egyedi elemtípus az elem osztályt, például a címsorok és a táblázatok, részeként, mert típusok nem használhatók egy modul hatókörén kívül.

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
