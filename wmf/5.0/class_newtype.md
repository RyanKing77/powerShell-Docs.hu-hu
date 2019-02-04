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
# <a name="new-language-features-in-powershell-50"></a>A PowerShell 5.0 új nyelvi funkciók

PowerShell 5.0 vezet be a következő új nyelvi elemei a Windows PowerShellben:

## <a name="class-keyword"></a>Osztály kulcsszó

A **osztály** kulcsszó határozza meg egy új osztályt. Ez a valódi .NET-keretrendszer típusa.
A osztályelemen nyilvános, de csak nyilvános modul hatókörébe.
Nem lehet hivatkozni a típusnév karakterláncként (például `New-Object` nem működik), ebben a kiadásban, és nem használhat olyan típusú konstans (például `[MyClass]`) kívül a parancsfájl nebo modul fájlt, amelyben az osztály definiálva van.

```powershell
class MyClass
{
    ...
}
```

## <a name="enum-keyword-and-enumerations"></a>Enum kulcsszó és enumerálásokat tartalmaznak

Támogatja a **enum** kulcsszó hozzá lett adva, melyik soremelés használ elválasztóként.
Aktuális korlátozások: nem lehet definiálni enumerátor tekintetében magát, de szempontjából egy másik enum enum is inicializálása, az alábbi példában látható módon.
Ezenkívül az alaptípus nem jelenleg adható meg; minden esetben [int].

```powershell
enum Color2
{
    Yellow = [Color]::Blue
}
```

Az enumerálóérték állandónak kell lennie parse time; egy meghívott parancs eredménye nem állítható be azt.

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

**Az import-DscResource** már igaz dinamikus kulcsszó.
PowerShell elemzi a megadott modul legfelső szintű modul, osztályban, amelyek tartalmazzák a Keresés a **DscResource** attribútum.

## <a name="implementingassembly"></a>ImplementingAssembly

Egy új mezőt **ImplementingAssembly**, ModuleInfo bővült. Azt a dinamikus szerelvény egy szkriptmodulba készült, ha a parancsfájl definiálja azokat az osztályokat, vagy a betöltött szerelvény a bináris modulok van beállítva. Nincs beállítva mikor ModuleType = jegyzékfájlt.

A reflexió a **ImplementingAssembly** mező felderítette az erőforrásokat egy modulban. Ez azt jelenti, hogy a PowerShell vagy más felügyelt nyelveken írt erőforrások deríthet fel.

Inicializátory mezőket:

```powershell
[int] $i = 5
```

Statikus támogatott; működik egy attribútum, például az ajánlattípusra vonatkozó megkötések, ahogy, így bármilyen sorrendben adható meg.

```powershell
static [int] $count = 0
```

Egy nem kötelező.

```powershell
$s = "hello"
```

Minden tag nyilvánosak legyenek.

## <a name="constructors-and-instantiation"></a>Konstruktorok és példányosítás

Windows PowerShell-osztályok rendelkezhet konstruktorok; a neve megegyezik az osztály rendelkeznek. Is túlterhelt konstruktorral. Statikus konstruktorok támogatottak. Tulajdonságok inicializálási kifejezésekkel inicializálása konstruktorban kód futtatása előtt. A statikus tulajdonságok inicializálása előtt egy statikus konstruktor törzse, és a példány tulajdonságainak inicializálása előtt nem statikus konstruktor törzse. Jelenleg nincs másik konstruktor konstruktor megismernie szintaxisának (például a C\# szintaxis ": this()"). A megoldás, hogy egy közös Init módszer meghatározásához.

A következő módon osztályok hárítható el ebben a kiadásban.

Hárítható el, az alapértelmezett konstruktort használatával. Vegye figyelembe, hogy a New-Object nem támogatott ebben a kiadásban.

```powershell
$a = [MyClass]::new()
```

A konstruktor egy paraméterrel hívása

```powershell
$b = [MyClass]::new(42)
```

Egy tömb átadása több paraméterekkel rendelkező konstruktor
```powershell
$c = [MyClass]::new(@(42,43,44), "Hello")
```

Az ebben a kiadásban a New-Object nem működik Windows PowerShell-ben definiált osztályokkal. Ebben a kiadásban název typu is csak látható betűrendbe, ami azt jelenti, már nem látható a modul vagy a parancsfájl az osztályt definiáló kívül. Funkciók a Windows PowerShellben meghatározott osztály példányainak adhat vissza, és példányok működnek jól kívül a modul vagy a parancsfájl.

`Get-Member -Static` konstruktorok, sorolja fel, hogy meg tudja tekinteni a túlterhelések, mint bármely más módszerrel. Ezt a szintaxist teljesítménye is jelentősen gyorsabb, mint a New-Object.

A pszeudo statikus metódust **új** együttműködik a .NET-típusok, az alábbi példában látható módon.

```powershell
[hashtable]::new()
```

Most már megtekintheti a konstruktor túlterheléssel Get-Member, vagy ebben a példában látható módon:

```powershell
PS> [hashtable]::new
OverloadDefinitions
-------------------
hashtable new()
hashtable new(int capacity)
hashtable new(int capacity, float loadFactor)
```

## <a name="methods"></a>Metódusok

A Windows PowerShell-osztály metódusának a scriptblock kulcsszót, amelynek csak egy záró blokk van megvalósítva. Az összes módszer nyilvánosak legyenek. A következő nevű metódus meghatározása példán látható **DoSomething**.

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

--Metódusok túlterhelt, azokkal, amelyek neve megegyezik egy meglévő módszer, de különbözteti meg a megadott értékek – is támogatottak.

## <a name="properties"></a>Tulajdonságok

Az összes tulajdonság nyilvánosak legyenek. Tulajdonságok szükség soremelés vagy pontosvesszővel válassza el. Ha nincs objektum típus van megadva, a tulajdonság típusának egy objektum.

Érvényesítési attribútumok vagy az argumentum-átalakítás attribútumok tulajdonságok (pl. `[ValidateSet("aaa")]`) a várt módon működik.

## <a name="hidden"></a>Rejtett

Egy új kulcsszó, **Hidden**, hozzá van adva. **Rejtett** tulajdonságai és metódusai (beleértve a konstruktorok) is alkalmazható.

Rejtett tagok nyilvános, de nem jelennek meg a Get-Member kimenetét, kivéve, ha a - Force paramétert.

A tagok nem tartoznak mikor rejtett lapon befejezése vagy az IntelliSense segítségével, kivéve, ha az osztály a rejtett tag meghatározása befejezése után történik.

Egy új attribútum **System.Management.Automation.HiddenAttribute** , hogy a C#-kód azonos szemantikáját Windows Powershellen belülről lehet hozzá lett adva.

## <a name="return-types"></a>Návratové typy

Typ vrácené hodnoty je szerződés; a visszaadott érték a várt típus alakítja át. Ha nincs visszatérési típus van megadva, a typ vrácené hodnoty je typ void. Nincsenek objektumok; streamelési van objektumok nem lehet írni a folyamat szándékosan vagy véletlenül iratkozott le.

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

A következő példában létrehozunk egy HTML dinamikus stílus lap nyelv (DSL) megvalósításának számos új, egyéni osztályok.
Ezt követően a példa ad segédfüggvények hozhat létre egyedi elemtípus az elem osztályt, például a címsorok és a táblázatok, részeként, mert típusok nem használhatók egy modul hatókörén kívül.

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
