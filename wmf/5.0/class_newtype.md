---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 85e9206ffef76fb4bd7714d847888e6e5bbcc4ec
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="new-language-features-in-powershell-50"></a>PowerShell 5.0 nyelvi újdonságai

PowerShell 5.0 vezet be a következő új nyelvi elemek a Windows PowerShellben:

## <a name="class-keyword"></a>Osztály kulcsszó

A **osztály** kulcsszó egy új osztályt határoz meg. Ez a .NET-keretrendszer típus igaz értékű.
A osztályelemen nyilvános, de csak nyilvános modul hatókörében.
Nem lehet hivatkozni a következő típusnév karakterláncként (például `New-Object` nem működik), és ebben a kiadásban szövegkonstans típus nem használható (például `[MyClass]`) kívül a parancsfájl/modul fájlt, amelyben az osztály definiálva van.

```powershell
class MyClass
{
    ...
}
```

## <a name="enum-keyword-and-enumerations"></a>Enum kulcsszó és az

Támogatja a **enum** kulcsszó bővült, melyik soremelés használ elválasztóként.
Aktuális korlátozások: enumerátor tekintetében maga nem határozhat meg, de egy felsorolás egy másik enum tekintetében is inicializálására, az alábbi példában látható módon.
Emellett az alaptípus tartalomtípusa nem jelenleg adható meg; mindig [int].

```powershell
enum Color2
{
    Yellow = [Color]::Blue
}
```

Az enumerálóérték elemzési idő állandónak; kell lennie. egy meghívott parancs eredménye nem állítható be azt.

```powershell
enum MyEnum
{
    Enum1
    Enum2
    Enum3 = 42
    Enum4 = [int]::MaxValue
}
```

Felsorolások matematikai művelteket is támogatja, a következő példában látható módon.

```powershell
enum SomeEnum { Max = 42 }
enum OtherEnum { Max = [SomeEnum]::Max + 1 }
```

## <a name="import-dscresource"></a>Import-DscResource

**Importálás – DscResource** mostantól egy igaz dinamikus kulcsszóval.
PowerShell elemzi a megadott modul gyökérmodult, tartalmazó osztályok keresése a **DscResource** attribútum.

## <a name="implementingassembly"></a>ImplementingAssembly

Új mező **ImplementingAssembly**, ModuleInfo hozzá lett adva. A dinamikus szerelvény egy szkriptmodulba készült, ha a parancsfájl osztályok határozza meg, vagy a bináris modulok betöltött szerelvény érték. Nincs beállítva mikor ModuleType jegyzékfájl =.

A reflexió a **ImplementingAssembly** mező a modulokban lévő erőforrások felderítésére szolgál. Ez azt jelenti, hogy is felderítheti, PowerShell vagy más felügyelt nyelvek erőforrásokat.

Az inicializálók mezők:

```powershell
[int] $i = 5
```

Statikus támogatott; az működik, mint egy attribútum, mint a típusmegkötések, így bármilyen sorrendben adható meg.

```powershell
static [int] $count = 0
```

A típus nem kötelező megadni.

```powershell
$s = "hello"
```

Minden tagjai nyilvános.

## <a name="constructors-and-instantiation"></a>Konstruktorok és a példánylétrehozás

A Windows PowerShell-osztályokat lehet konstruktorok; az osztály megegyező névvel rendelkeznek. Konstruktorok is túlterhelt. Statikus konstruktorok támogatottak. Inicializálási kifejezések értékkel rendelkező tulajdonságok a rendszer konstruktorban kód futtatása előtt inicializálja. A statikus tulajdonságok inicializálása előtt statikus konstruktorban törzsét, és objektumpéldány tulajdonságai inicializálása előtt nem statikus konstruktorban törzsét. Jelenleg nincs konstruktor a másik konstruktor hívásakor szintaxis (például a C\# szintaxis ": this()"). Kerülő megoldás lehet egy közös Init metódus meghatározásához.

A következő módon példányának osztályok ebben a kiadásban.

Létrehozza az alapértelmezett konstruktor használatával. Vegye figyelembe, hogy a New-Object nem támogatott ebben a kiadásban.

```powershell
$a = [MyClass]::new()
```

Egy paraméterrel rendelkező konstruktor hívása

```powershell
$b = [MyClass]::new(42)
```

Egy tömb átadni több paraméterekkel rendelkező konstruktor
```powershell
$c = [MyClass]::new(@(42,43,44), "Hello")
```

Ebben a kiadásban a New-Object nem működik a Windows PowerShell-ben definiált osztályokkal. Ebben a kiadásban a következő típusnév is csak látható lexically, ami azt jelenti, nem látható a modul vagy a parancsfájl az osztályt definiáló kívül. Funkciók Windows PowerShell meghatározott osztály példányainak lépjen vissza, és példányok működik jól kívül a modul vagy a parancsfájlhoz.

`Get-Member -Static` konstruktorok, sorolja fel, mint bármely más módszerrel túlterhelések szeretné megjeleníteni. Az ezen szintakszist teljesítménye is jelentősen gyorsabb, mint a New-Object.

A pszeudo statikus metódus nevű **új** .NET tárolóhelytípussal működik, a következő példában látható módon.

```powershell
[hashtable]::new()
```

Most már megtekintheti konstruktor túlterhelések Get-tag, illetve ez a példa látható:

```powershell
PS> [hashtable]::new
OverloadDefinitions
-------------------
hashtable new()
hashtable new(int capacity)
hashtable new(int capacity, float loadFactor)
```

## <a name="methods"></a>Metódusok

A Windows PowerShell osztály adott metódusát, a scriptblock kulcsszót, amelynek csak egy záró blokk lett megvalósítva. Minden módszereket nyilvános. A következő nevű metódus meghatározásának példáját mutatja be **DoSomething**.

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

A metódushívás:

```powershell
$b = [MyClass]::new()
$b.DoSomething(42)
```

Túlterhelt metódusok – Ez azt jelenti, hogy a meglévő metódus azonos nevű, de a megadott értékek--szerint megkülönböztetett is támogatott.

## <a name="properties"></a>Tulajdonságok

Az összes tulajdonság olyan nyilvános. Tulajdonságok szükség soremelés vagy pontosvesszővel válassza el. Ha nincs objektum típusaként van megadva, a a tulajdonság típusa nem objektum.

Érvényesítési attribútumot, vagy argumentum átalakítása attribútumok használó tulajdonságok (pl. `[ValidateSet("aaa")]`) a várt módon működik.

## <a name="hidden"></a>Rejtett

Egy új kulcsszó **rejtett**, hozzá lett adva. **Rejtett** tulajdonságai és metódusai (beleértve a konstruktorok) alkalmazhatók.

A rejtett tagokat nyilvános, de nem jelennek meg a Get-tag kimeneti kivéve, ha a - Force paramétert.

Rejtett tagok nincsenek mikor befejeződését, vagy az Intellisense segítségével, kivéve, ha a létrehozása után következik be, a rejtett tag definiáló osztály fülre.

Új attribútum **System.Management.Automation.HiddenAttribute** bővült, így C#-kódban a Windows PowerShell belül azonos szemantikáját.

## <a name="return-types"></a>Visszatérési típusokat

Visszatérési típusa a szerződést; az eredményül kapott értéket alakítja át a várt típusú. Ha nincs visszatérési típusa van megadva, a visszatérési típus érvénytelen. Nincsenek objektumok; streaming van objektumok nem lehet írni a feldolgozási sor szándékosan vagy véletlenül.

## <a name="attributes"></a>Attribútumok

Két új attribútum **DscResource** és **DscProperty** lettek hozzáadva.

## <a name="lexical-scoping-of-variables"></a>A változók lexikális hatókörének beállítása

A következő példáját mutatja be, hogyan lexikális tartalmazó works ebben a kiadásban.

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

## <a name="end-to-end-example"></a>Végpontok – példa

Az alábbi példa létrehoz egy HTML dinamikus stílus lap nyelvi (DSL) megvalósításának számos új, egyéni osztályok.
Ezt követően a példa ad segédfüggvények találhatók, az elem osztályt, például címsorok és táblák, részeként meghatározott elemtípus létrehozásához, mert típusok nem használhatók a modulok hatókörén kívül.

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