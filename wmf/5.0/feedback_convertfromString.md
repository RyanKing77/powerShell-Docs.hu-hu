---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: fcf2adf67f36edb534df3e2a849459fb20e1c2de
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685619"
---
# <a name="extract-and-parse-structured-objects-out-of-string"></a><span data-ttu-id="c9e65-102">Strukturált objektumok sztringekből való kibontása és elemzése</span><span class="sxs-lookup"><span data-stu-id="c9e65-102">Extract and Parse Structured Objects out of String</span></span>

<span data-ttu-id="c9e65-103">Néhány további funkciókat is azzal az `ConvertFrom-String` parancsmagot:</span><span class="sxs-lookup"><span data-stu-id="c9e65-103">This also introduces some additional functionality for the `ConvertFrom-String` cmdlet:</span></span>

- <span data-ttu-id="c9e65-104">Eltávolítja a mértékben a text tulajdonság alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="c9e65-104">Removes the extent text property by default.</span></span> <span data-ttu-id="c9e65-105">Megadhatja a - IncludeExtent paraméterrel.</span><span class="sxs-lookup"><span data-stu-id="c9e65-105">You can include it with the -IncludeExtent parameter.</span></span>

- <span data-ttu-id="c9e65-106">Számos tanulási algoritmus hibajavítások az MVP és a közösségi visszajelzések.</span><span class="sxs-lookup"><span data-stu-id="c9e65-106">Many learning algorithm bug fixes from MVP and community feedback.</span></span>

- <span data-ttu-id="c9e65-107">Új - UpdateTemplate paraméter a tanulási algoritmus-eredményeket menteni a sablonfájlt megjegyzést.</span><span class="sxs-lookup"><span data-stu-id="c9e65-107">A new -UpdateTemplate parameter to save the results of the learning algorithm into a comment in the template file.</span></span> <span data-ttu-id="c9e65-108">Ez lehetővé teszi a learning feldolgozásához (a leglassabb fázis) egy egyszeri költség.</span><span class="sxs-lookup"><span data-stu-id="c9e65-108">This makes the learning process (the slowest stage) a one-time cost.</span></span> <span data-ttu-id="c9e65-109">Futó Convert-karakterlánc, amely tartalmazza a kódolt tanulási algoritmus-sablonnal már szinte azonnali.</span><span class="sxs-lookup"><span data-stu-id="c9e65-109">Running Convert-String with a template that contains the encoded learning algorithm is now nearly instantaneous.</span></span>

## <a name="extract-and-parse-structured-objects-out-of-string-content"></a><span data-ttu-id="c9e65-110">Strukturált objektumok karakterlánc tartalmakhoz kibontása és elemzése</span><span class="sxs-lookup"><span data-stu-id="c9e65-110">Extract and parse structured objects out of string content</span></span>

<span data-ttu-id="c9e65-111">Együttműködve [a Microsoft Research](https://www.microsoft.com/en-us/research/?from=http%3A%2F%2Fresearch.microsoft.com%2F), egy új `ConvertFrom-String` parancsmaggal hozzá lett adva.</span><span class="sxs-lookup"><span data-stu-id="c9e65-111">In collaboration with [Microsoft Research](https://www.microsoft.com/en-us/research/?from=http%3A%2F%2Fresearch.microsoft.com%2F), a new `ConvertFrom-String` cmdlet has been added.</span></span>

<span data-ttu-id="c9e65-112">Ez a parancsmag két módot támogat: alapszintű tagolt elemzés, és automatikusan létrehozott példa adatvezérelt elemzése.</span><span class="sxs-lookup"><span data-stu-id="c9e65-112">This cmdlet supports two modes: basic delimited parsing, and auto generated example-driven parsing.</span></span>

<span data-ttu-id="c9e65-113">Tagolt elemzés, alapértelmezés szerint bontja a bemenet üres helyet, és a tulajdonságnevek rendel az eredményül kapott csoportok.</span><span class="sxs-lookup"><span data-stu-id="c9e65-113">Delimited parsing, by default, splits the input at white space, and assigns property names to the resulting groups.</span></span> <span data-ttu-id="c9e65-114">Testre szabhatja az elválasztó karakter:</span><span class="sxs-lookup"><span data-stu-id="c9e65-114">You can customize the delimiter:</span></span>

```powershell
"Hello World" | ConvertFrom-String | Format-Table -Auto
```

```output
P1     P2
--     --
Hello  World
```

<span data-ttu-id="c9e65-115">A parancsmag is támogatja a alapján automatikusan létrehozott példa adatvezérelt elemzés a [FlashExtract](https://www.microsoft.com/en-us/research/publication/flashextract-framework-data-extraction-examples/?from=http%3A%2F%2Fresearch.microsoft.com%2Fen-us%2Fum%2Fpeople%2Fsumitg%2Fflashextract.html) kutatási munka [a Microsoft Research](https://www.microsoft.com/en-us/research/?from=http%3A%2F%2Fresearch.microsoft.com%2F).</span><span class="sxs-lookup"><span data-stu-id="c9e65-115">The cmdlet also supports auto-generated example-driven parsing based on the [FlashExtract](https://www.microsoft.com/en-us/research/publication/flashextract-framework-data-extraction-examples/?from=http%3A%2F%2Fresearch.microsoft.com%2Fen-us%2Fum%2Fpeople%2Fsumitg%2Fflashextract.html) research work in [Microsoft Research](https://www.microsoft.com/en-us/research/?from=http%3A%2F%2Fresearch.microsoft.com%2F).</span></span>

<span data-ttu-id="c9e65-116">Első lépésként fontolja meg egy szöveges alapú címjegyzék:</span><span class="sxs-lookup"><span data-stu-id="c9e65-116">To get started, consider a text-based address book:</span></span>

```
    Ana Trujillo

    Redmond, WA

    Antonio Moreno

    Renton, WA

    Thomas Hardy

    Seattle, WA

    Christina Berglund

    Redmond, WA

    Hanna Moos

    Puyallup, WA
```

<span data-ttu-id="c9e65-117">Néhány példa másolja egy fájlba, melyiket fogja használni a sablont:</span><span class="sxs-lookup"><span data-stu-id="c9e65-117">Copy a few examples into a file, which you will use as your template:</span></span>

```
    Ana Trujillo

    Redmond, WA

    Antonio Moreno

    Renton, WA
```

<span data-ttu-id="c9e65-118">Nevezi el, hogy ehhez kapcsos zárójelek körül adatokat szeretne kinyerni, helyezze el.</span><span class="sxs-lookup"><span data-stu-id="c9e65-118">Put curly braces around data that you want to extract, giving it a name as you do so.</span></span> <span data-ttu-id="c9e65-119">Mivel a **neve** tulajdonság (és a kapcsolódó egyéb tulajdonságok) is többször jelenik meg, egy csillag (\*) jelzi, hogy ennek hatására a több rekord (nem pedig a tulajdonságok többféle csomagolja ki az egyik rekord):</span><span class="sxs-lookup"><span data-stu-id="c9e65-119">Because the **Name** property (and its associated other properties) can appear multiple times, use an asterisk (\*) to indicate that this results in multiple records (rather than extracting a bunch of properties into one record):</span></span>

```
    {Name\*:Ana Trujillo}

    {City:Redmond}, {State:WA}

    {Name\*:Antonio Moreno}

    {City:Renton}, {State:WA}
```

<span data-ttu-id="c9e65-120">A példákban egy készlete `ConvertFrom-String` most már automatikusan kinyerheti az objektum alapú kimeneti bemeneti fájlok hasonló struktúrával.</span><span class="sxs-lookup"><span data-stu-id="c9e65-120">From this set of examples, `ConvertFrom-String` can now automatically extract object-based output from input files with similar structure.</span></span>

```powershell
Get-Content .\addresses.output.txt | ConvertFrom-String -TemplateFile .\addresses.template.txt | Format-Table -Auto
```

```output
ExtentText                     Name               City     State
----------                     ----               ----     -----
Ana Trujillo...                Ana Trujillo       Redmond  WA
Antonio Moreno...              Antonio Moreno     Renton   WA
Thomas Hardy...                Thomas Hardy       Seattle  WA
Christina Berglund...          Christina Berglund Redmond  WA
Hanna Moos...                  Hanna Moos         Puyallup WA
```

<span data-ttu-id="c9e65-121">Ehhez a kinyert szöveg további adatkezelés a **ExtentText** tulajdonság a nyers szöveg, amelyből a rekordot kinyert rögzíti.</span><span class="sxs-lookup"><span data-stu-id="c9e65-121">To do additional data manipulation on extracted text, the **ExtentText** property captures the raw text from which the record was extracted.</span></span> <span data-ttu-id="c9e65-122">Szeretne visszajelzést adni ezt a szolgáltatást, vagy oszthat meg tartalmakat, amelyhez problémái vannak példák írása, írjon e-mailt <psdmfb@microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="c9e65-122">To provide feedback on this feature, or to share content for which you are having difficulty writing examples, please email <psdmfb@microsoft.com>.</span></span>