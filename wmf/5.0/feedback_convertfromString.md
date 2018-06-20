---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: e4588e8c69efb965cd33c273ad09a8bef8e9bf16
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189567"
---
# <a name="extract-and-parse-structured-objects-out-of-string"></a><span data-ttu-id="87ea7-102">Strukturált objektumok karakterláncokból való kibontása és elemzése</span><span class="sxs-lookup"><span data-stu-id="87ea7-102">Extract and Parse Structured Objects out of String</span></span>
<span data-ttu-id="87ea7-103">Az azzal a ConvertFrom-karakterlánc parancsmag további funkciókkal is:</span><span class="sxs-lookup"><span data-stu-id="87ea7-103">This also introduces some additional functionality for the ConvertFrom-String cmdlet:</span></span>

-   <span data-ttu-id="87ea7-104">Alapértelmezés szerint eltávolítja a mértékben text tulajdonságához.</span><span class="sxs-lookup"><span data-stu-id="87ea7-104">Removes the extent text property by default.</span></span> <span data-ttu-id="87ea7-105">Megadhatja a - IncludeExtent paraméterrel.</span><span class="sxs-lookup"><span data-stu-id="87ea7-105">You can include it with the -IncludeExtent parameter.</span></span>

-   <span data-ttu-id="87ea7-106">Sok tanulási algoritmus hibajavításokat tartalmaz az MVP és közösségi visszajelzését.</span><span class="sxs-lookup"><span data-stu-id="87ea7-106">Many learning algorithm bug fixes from MVP and community feedback.</span></span>

-   <span data-ttu-id="87ea7-107">Új - UpdateTemplate paramétere a tanulási algoritmus-eredményeket menteni a sablonfájl megjegyzést.</span><span class="sxs-lookup"><span data-stu-id="87ea7-107">A new -UpdateTemplate parameter to save the results of the learning algorithm into a comment in the template file.</span></span> <span data-ttu-id="87ea7-108">Így a tanulási (a leglassabb szakasza) feldolgozása egy egyszeri költség.</span><span class="sxs-lookup"><span data-stu-id="87ea7-108">This makes the learning process (the slowest stage) a one-time cost.</span></span> <span data-ttu-id="87ea7-109">A sablont, amely tartalmazza a kódolt tanulási algoritmus Convert-karakterlánc fut már szinte azonnali.</span><span class="sxs-lookup"><span data-stu-id="87ea7-109">Running Convert-String with a template that contains the encoded learning algorithm is now nearly instantaneous.</span></span>


<a name="extract-and-parse-structured-objects-out-of-string-content"></a><span data-ttu-id="87ea7-110">Bontsa ki és értelmezni a karakterlánc tartalmakhoz strukturált objektumok</span><span class="sxs-lookup"><span data-stu-id="87ea7-110">Extract and parse structured objects out of string content</span></span>
----------------------------------------------------------

<span data-ttu-id="87ea7-111">Együttműködve [Microsoft Research](http://research.microsoft.com/), egy új **ConvertFrom-karakterlánc** parancsmaggal hozzá lett adva.</span><span class="sxs-lookup"><span data-stu-id="87ea7-111">In collaboration with [Microsoft Research](http://research.microsoft.com/), a new **ConvertFrom-String** cmdlet has been added.</span></span>

<span data-ttu-id="87ea7-112">Ez a parancsmag két módot támogat: basic tagolt elemzése, és automatikusan létrejön példa adatvezérelt elemzésekor.</span><span class="sxs-lookup"><span data-stu-id="87ea7-112">This cmdlet supports two modes: basic delimited parsing, and auto generated example-driven parsing.</span></span>

<span data-ttu-id="87ea7-113">Tagolt elemzése, alapértelmezés szerint felosztja a bemeneti: szóköz, és a tulajdonságnevek rendel az eredményül kapott csoportok.</span><span class="sxs-lookup"><span data-stu-id="87ea7-113">Delimited parsing, by default, splits the input at white space, and assigns property names to the resulting groups.</span></span> <span data-ttu-id="87ea7-114">Testre szabhatja az elválasztó karakter:</span><span class="sxs-lookup"><span data-stu-id="87ea7-114">You can customize the delimiter:</span></span>

> <span data-ttu-id="87ea7-115">1 \[C:\\temp\] &gt; &gt; "Hello, World" |} ConvertFrom-karakterlánc |} Táblázat formázása-automatikus</span><span class="sxs-lookup"><span data-stu-id="87ea7-115">1 \[C:\\temp\] &gt;&gt; "Hello World" | ConvertFrom-String | Format-Table -Auto</span></span>

<span data-ttu-id="87ea7-116">P1    P2</span><span class="sxs-lookup"><span data-stu-id="87ea7-116">P1    P2</span></span>
--    --

<span data-ttu-id="87ea7-117">A parancsmag is támogatja a alapján automatikusan létrehozott példa adatvezérelt elemzése a [FlashExtract](http://research.microsoft.com/en-us/um/people/sumitg/flashextract.html) munka kutatás [Microsoft Research](http://research.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="87ea7-117">The cmdlet also supports auto-generated example-driven parsing based on the [FlashExtract](http://research.microsoft.com/en-us/um/people/sumitg/flashextract.html) research work in [Microsoft Research](http://research.microsoft.com).</span></span>

<span data-ttu-id="87ea7-118">A kezdéshez, fontolja meg a szöveges címjegyzék:</span><span class="sxs-lookup"><span data-stu-id="87ea7-118">To get started, consider a text-based address book:</span></span>

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

<span data-ttu-id="87ea7-119">Néhány példa átmásolja a fájlt, amely a sablont használhatja:</span><span class="sxs-lookup"><span data-stu-id="87ea7-119">Copy a few examples into a file, which you will use as your template:</span></span>

    Ana Trujillo

    Redmond, WA

    Antonio Moreno

    Renton, WA



<span data-ttu-id="87ea7-120">Helyezze a kinyerési, kívánt adatok körül kapcsos zárójelek adjon neki egy nevet, azt megteheti.</span><span class="sxs-lookup"><span data-stu-id="87ea7-120">Put curly braces around data that you want to extract, giving it a name as you do so.</span></span> <span data-ttu-id="87ea7-121">Mivel a **neve** tulajdonság (és a kapcsolódó egyéb tulajdonságok) is többször jelenik meg, használja a csillag (\*) jelzi, hogy az eredmény több rekordot (helyett álló, lemezcsoport típusú tulajdonságok csomagolja ki egy rekord):</span><span class="sxs-lookup"><span data-stu-id="87ea7-121">Because the **Name** property (and its associated other properties) can appear multiple times, use an asterisk (\*) to indicate that this results in multiple records (rather than extracting a bunch of properties into one record):</span></span>

    {Name\*:Ana Trujillo}

    {City:Redmond}, {State:WA}

    {Name\*:Antonio Moreno}

    {City:Renton}, {State:WA}

<span data-ttu-id="87ea7-122">Példák, a készletből **ConvertFrom-karakterlánc** mostantól automatikusan nyerhet objektum alapú kimeneti hasonló struktúrájú bemeneti fájlokból.</span><span class="sxs-lookup"><span data-stu-id="87ea7-122">From this set of examples, **ConvertFrom-String** can now automatically extract object-based output from input files with similar structure.</span></span>

> <span data-ttu-id="87ea7-123">2 \[C:\\temp\]</span><span class="sxs-lookup"><span data-stu-id="87ea7-123">2 \[C:\\temp\]</span></span>
>
> <span data-ttu-id="87ea7-124">&gt;&gt; Get-tartalom. \\addresses.output.txt |} ConvertFrom-karakterlánc - TemplateFile. \\addresses.template.txt |} &gt; &gt; &gt; Format-Table-automatikus</span><span class="sxs-lookup"><span data-stu-id="87ea7-124">&gt;&gt; Get-Content .\\addresses.output.txt | ConvertFrom-String -TemplateFile .\\addresses.template.txt | &gt;&gt;&gt; Format-Table -Auto</span></span>
>
> <span data-ttu-id="87ea7-125">ExtentText neve város állapota</span><span class="sxs-lookup"><span data-stu-id="87ea7-125">ExtentText                     Name               City     State</span></span>
> ----------                     ----               ----     -----
> <span data-ttu-id="87ea7-126">Ana Trujillo...                Ana Trujillo Redmond WA Antonio Moreno...              Antonio Moreno Renton WA Thomas Zsigmond...                Thomas Zsigmond Seattle WA lengyel Berglund...          Lengyel Berglund Redmond WA Hanna Moos...                  Hanna Moos Puyallup WA</span><span class="sxs-lookup"><span data-stu-id="87ea7-126">Ana Trujillo...                Ana Trujillo       Redmond  WA Antonio Moreno...              Antonio Moreno     Renton   WA Thomas Hardy...                Thomas Hardy       Seattle  WA Christina Berglund...          Christina Berglund Redmond  WA Hanna Moos...                  Hanna Moos         Puyallup WA</span></span>

<span data-ttu-id="87ea7-127">További adatok módosítását. a kibontott szöveg, amelyet ehhez a **ExtentText** tulajdonság rögzíti a raw szöveg, amelyből a rekordot ki lett olvasni.</span><span class="sxs-lookup"><span data-stu-id="87ea7-127">To do additional data manipulation on extracted text, the **ExtentText** property captures the raw text from which the record was extracted.</span></span> <span data-ttu-id="87ea7-128">Visszajelzés a szolgáltatást, vagy amelynek nehézségei vannak példák írása tartalmak megosztása, írjon e-mailt <psdmfb@microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="87ea7-128">To provide feedback on this feature, or to share content for which you are having difficulty writing examples, please email <psdmfb@microsoft.com>.</span></span>
