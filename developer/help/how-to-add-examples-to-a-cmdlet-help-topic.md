---
title: Példák, a parancsmag Súgó-témakör hozzáadása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8f723b21-8f95-4981-8b6e-4f07c22d601a
caps.latest.revision: 5
ms.openlocfilehash: 5e8d1df6b423bfd2cd6b0a64a8875dea9c3fb4ef
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847732"
---
# <a name="how-to-add-examples-to-a-cmdlet-help-topic"></a><span data-ttu-id="e49b8-102">Példák hozzáadása egy parancsmagokkal kapcsolatos súgótémakörhöz</span><span class="sxs-lookup"><span data-stu-id="e49b8-102">How to Add Examples to a Cmdlet Help Topic</span></span>

- [<span data-ttu-id="e49b8-103">Tudnivaló a parancsmag súgóját példái kapcsolatban</span><span class="sxs-lookup"><span data-stu-id="e49b8-103">Things to Know about Examples in Cmdlet Help</span></span>](#Things-to-Know-about-Examples-in-Cmdlet-Help)

- [<span data-ttu-id="e49b8-104">Példák megjelenítő nézetek segítségével</span><span class="sxs-lookup"><span data-stu-id="e49b8-104">Help Views that Display Examples</span></span>](#Help-Views-that-Display-Examples)

- [<span data-ttu-id="e49b8-105">Egy példa csomópont hozzáadása</span><span class="sxs-lookup"><span data-stu-id="e49b8-105">Adding an Examples Node</span></span>](#Adding-an-Examples-Node)

- [<span data-ttu-id="e49b8-106">Karakterek megelőző hozzáadása</span><span class="sxs-lookup"><span data-stu-id="e49b8-106">Adding Preceding Characters</span></span>](#Adding-Preceding-Characters)

- [<span data-ttu-id="e49b8-107">A parancs felvétele</span><span class="sxs-lookup"><span data-stu-id="e49b8-107">Adding the Command</span></span>](#Adding-the-Command)

- [<span data-ttu-id="e49b8-108">Leírás hozzáadása</span><span class="sxs-lookup"><span data-stu-id="e49b8-108">Adding a Description</span></span>](#Adding-a-Description)

- [<span data-ttu-id="e49b8-109">Példa kimenet hozzáadása</span><span class="sxs-lookup"><span data-stu-id="e49b8-109">Adding Example Output</span></span>](#Adding-Example-Output)

## <a name="things-to-know-about-examples-in-cmdlet-help"></a><span data-ttu-id="e49b8-110">Tudnivaló a parancsmag súgóját példái kapcsolatban</span><span class="sxs-lookup"><span data-stu-id="e49b8-110">Things to Know about Examples in Cmdlet Help</span></span>

- <span data-ttu-id="e49b8-111">Listán minden, a parancsban a paraméter neve, akkor is, ha a paraméter nevének megadása nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="e49b8-111">List all of the parameter names in the command, even when the parameter names are optional.</span></span> <span data-ttu-id="e49b8-112">Ez segít a felhasználó könnyen értelmezni a parancsot.</span><span class="sxs-lookup"><span data-stu-id="e49b8-112">This helps the user to interpret the command easily.</span></span>

- <span data-ttu-id="e49b8-113">Kerülje a aliasok és a részleges paraméterneveket, annak ellenére, hogy a Windows PowerShell® működnek.</span><span class="sxs-lookup"><span data-stu-id="e49b8-113">Avoid aliases and partial parameter names, even though they work in Windows PowerShell®.</span></span>

- <span data-ttu-id="e49b8-114">Példa leírásában adja meg a parancs építésére ésszerű ismertetik.</span><span class="sxs-lookup"><span data-stu-id="e49b8-114">In the example description, explain the rational for the construction of the command.</span></span> <span data-ttu-id="e49b8-115">Azt ismerteti, miért döntött az adott paramétereket és értékeket, és a változók használatának módjáról.</span><span class="sxs-lookup"><span data-stu-id="e49b8-115">Explain why you chose particular parameters and values, and how you use variables.</span></span>

- <span data-ttu-id="e49b8-116">Ha a parancs kifejezéseket használ, ezeket részletesen elmagyarázza.</span><span class="sxs-lookup"><span data-stu-id="e49b8-116">If the command uses expressions, explain them in detail.</span></span>

- <span data-ttu-id="e49b8-117">Ha a parancs tulajdonságai és metódusai objektumok használ, különösen olyan tulajdonságok, amelyek nem jelennek meg az alapértelmezett megjelenítést a példát követve, mert lehetőséget a felhasználó értesítése az objektumra vonatkozó.</span><span class="sxs-lookup"><span data-stu-id="e49b8-117">If the command uses properties and methods of objects, especially properties that do not appear in the default display, use the example as an opportunity tell the user about the object.</span></span>

## <a name="help-views-that-display-examples"></a><span data-ttu-id="e49b8-118">Példák megjelenítő nézetek segítségével</span><span class="sxs-lookup"><span data-stu-id="e49b8-118">Help Views that Display Examples</span></span>

<span data-ttu-id="e49b8-119">Példák csak a Súgó parancsmag részletes és a teljes nézetek jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="e49b8-119">Examples appear only in the Detailed and Full views of cmdlet Help.</span></span>

## <a name="adding-an-examples-node"></a><span data-ttu-id="e49b8-120">Egy példa csomópont hozzáadása</span><span class="sxs-lookup"><span data-stu-id="e49b8-120">Adding an Examples Node</span></span>

<span data-ttu-id="e49b8-121">A következő XML-példákat csomópont, amely tartalmazza a példában egyetlen csomópont hozzáadása mutatja be.</span><span class="sxs-lookup"><span data-stu-id="e49b8-121">The following XML shows how to add an Examples node that contains a single Example node.</span></span> <span data-ttu-id="e49b8-122">Minden egyes példák fel szeretne venni a témakör a további példa csomópontok hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="e49b8-122">Add additional example nodes for each examples you want to include in the topic.</span></span>

```xml
<command:examples>
  <command:example>
  </command:example>
</command:examples>
```

## <a name="adding-an-example-title"></a><span data-ttu-id="e49b8-123">Egy példa cím hozzáadása</span><span class="sxs-lookup"><span data-stu-id="e49b8-123">Adding an Example Title</span></span>

<span data-ttu-id="e49b8-124">A következő XML formátumú bemutatja, hogyan például cím megadásához.</span><span class="sxs-lookup"><span data-stu-id="e49b8-124">The following XML shows how to add a title for the example.</span></span> <span data-ttu-id="e49b8-125">A cím beállítása mellett további példák a példa szolgál.</span><span class="sxs-lookup"><span data-stu-id="e49b8-125">The title is used to set the example apart from other examples.</span></span> <span data-ttu-id="e49b8-126">Windows PowerShell® használ egy standard fejlécet, amely több egymást követő példában.</span><span class="sxs-lookup"><span data-stu-id="e49b8-126">Windows PowerShell® uses a standard header that includes a sequential example number.</span></span>

```xml
<command:examples>
  <command:example>
    <maml:title>----------  EXAMPLE 1  ----------</maml:title>
  </command:example>
</command:examples>
```

## <a name="adding-preceding-characters"></a><span data-ttu-id="e49b8-127">Karakterek megelőző hozzáadása</span><span class="sxs-lookup"><span data-stu-id="e49b8-127">Adding Preceding Characters</span></span>

<span data-ttu-id="e49b8-128">A következő XML formátumú karaktereket, például a Windows PowerShell-parancssort, amely jelennek meg azonnal a példaparancs (bármely beavatkozó szóközök nélkül) előtt adjon hozzá mutatja be.</span><span class="sxs-lookup"><span data-stu-id="e49b8-128">The following XML shows how to add characters, such as the Windows PowerShell prompt, that are displayed immediately before the example command (without any intervening spaces).</span></span> <span data-ttu-id="e49b8-129">Windows PowerShell® használja a Windows PowerShell-parancssorba: C:\PS>.</span><span class="sxs-lookup"><span data-stu-id="e49b8-129">Windows PowerShell® uses the Windows PowerShell prompt: C:\PS>.</span></span>

```xml
<command:examples>
  <command:example>
    <maml:title>----------  EXAMPLE 1  ----------</maml:title>
    <maml:Introduction>
      <maml:paragraph>C:\PS></maml:paragraph>
    </maml:Introduction>
</command:example>
</command:examples>
```

## <a name="adding-the-command"></a><span data-ttu-id="e49b8-130">A parancs felvétele</span><span class="sxs-lookup"><span data-stu-id="e49b8-130">Adding the Command</span></span>

<span data-ttu-id="e49b8-131">A következő XML formátumú adja hozzá a tényleges parancsot a példa szemlélteti.</span><span class="sxs-lookup"><span data-stu-id="e49b8-131">The following XML shows how to add the actual command of the example.</span></span> <span data-ttu-id="e49b8-132">A parancs való hozzáadásakor, írja be a teljes nevét (ne használja a alias) parancsmagok és paraméterek.</span><span class="sxs-lookup"><span data-stu-id="e49b8-132">When adding the command, type the entire name (do not use alias) of cmdlets and parameters.</span></span> <span data-ttu-id="e49b8-133">Továbbá a használnak kisbetűs karaktert, amikor csak lehetséges.</span><span class="sxs-lookup"><span data-stu-id="e49b8-133">Also, use lowercase characters whenever possible.</span></span>

```xml
<command:examples>
  <command:example>
    <maml:title>----------  EXAMPLE 1  ----------</maml:title>
    <maml:Introduction>
      <maml:paragraph>C:\PS></maml:paragraph>
    </maml:Introduction>
    <dev:code> command </dev:code>
</command:example>
</command:examples>
```

## <a name="adding-a-description"></a><span data-ttu-id="e49b8-134">Leírás hozzáadása</span><span class="sxs-lookup"><span data-stu-id="e49b8-134">Adding a Description</span></span>

<span data-ttu-id="e49b8-135">A következő XML-kódot adjon meg egy leírást a példa szemlélteti.</span><span class="sxs-lookup"><span data-stu-id="e49b8-135">The following XML shows how to add a description for the example.</span></span> <span data-ttu-id="e49b8-136">Windows PowerShell® használja egyetlen \<maml:para > címkék leírására, akkor is, ha több \<maml:para > címkék használhatók.</span><span class="sxs-lookup"><span data-stu-id="e49b8-136">Windows PowerShell® uses a single set of \<maml:para> tags for the description, even though multiple \<maml:para> tags can be used.</span></span>

```xml
<command:examples>
  <command:example>
    <maml:title>----------  EXAMPLE 1  ----------</maml:title>
    <maml:Introduction>
      <maml:paragraph>C:\PS></maml:paragraph>
    </maml:Introduction>
    <dev:code> command </dev:code>
    <dev:remarks>
      <maml:para> command description </maml:para>
    </dev:remarks>
</command:example>
</command:examples>
```

## <a name="adding-example-output"></a><span data-ttu-id="e49b8-137">Példa kimenet hozzáadása</span><span class="sxs-lookup"><span data-stu-id="e49b8-137">Adding Example Output</span></span>

<span data-ttu-id="e49b8-138">A következő XML formátumú adja hozzá a parancs kimenetét mutatja be.</span><span class="sxs-lookup"><span data-stu-id="e49b8-138">The following XML shows how to add the output of the command.</span></span> <span data-ttu-id="e49b8-139">A parancs eredménye információ megadása nem kötelező, de bizonyos esetekben hasznos lehet a megadott paraméterekkel hatásának bemutatása.</span><span class="sxs-lookup"><span data-stu-id="e49b8-139">The command results information is optional, but in some cases it is helpful to demonstrate the effect of using specific parameters.</span></span> <span data-ttu-id="e49b8-140">Windows PowerShell® használ üres két készletnyi \<maml:para > címkéket, hogy a parancs kimenete elkülönítése a parancsot.</span><span class="sxs-lookup"><span data-stu-id="e49b8-140">Windows PowerShell® uses two sets of blank \<maml:para> tags to separate the command output from the command.</span></span>

```xml
<command:examples>
  <command:example>
    <maml:title>----------  EXAMPLE 1  ----------</maml:title>
    <maml:Introduction>
      <maml:paragraph>C:\PS></maml:paragraph>
    </maml:Introduction>
    <dev:code> command </dev:code>
    <dev:remarks>
      <maml:para> command description </maml:para>
      <maml:para></maml:para>
      <maml:para></maml:para>
      <maml:para> command output </maml:para>
</dev:remarks>
</command:example>
</command:examples>
```