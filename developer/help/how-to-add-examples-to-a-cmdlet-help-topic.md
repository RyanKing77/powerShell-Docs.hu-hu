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
ms.openlocfilehash: b6f8aef76a5f4b5dc1a60425541856ead9a9c77a
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65855115"
---
# <a name="how-to-add-examples-to-a-cmdlet-help-topic"></a><span data-ttu-id="53a37-102">Példák hozzáadása egy parancsmagokkal kapcsolatos súgótémakörhöz</span><span class="sxs-lookup"><span data-stu-id="53a37-102">How to Add Examples to a Cmdlet Help Topic</span></span>

## <a name="things-to-know-about-examples-in-cmdlet-help"></a><span data-ttu-id="53a37-103">Tudnivaló a parancsmag súgóját példái kapcsolatban</span><span class="sxs-lookup"><span data-stu-id="53a37-103">Things to Know about Examples in Cmdlet Help</span></span>

- <span data-ttu-id="53a37-104">Listán minden, a parancsban a paraméter neve, akkor is, ha a paraméter nevének megadása nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="53a37-104">List all of the parameter names in the command, even when the parameter names are optional.</span></span> <span data-ttu-id="53a37-105">Ez segít a felhasználó könnyen értelmezni a parancsot.</span><span class="sxs-lookup"><span data-stu-id="53a37-105">This helps the user to interpret the command easily.</span></span>

- <span data-ttu-id="53a37-106">Kerülje a aliasok és a részleges paraméterneveket, annak ellenére, hogy a Windows PowerShell® működnek.</span><span class="sxs-lookup"><span data-stu-id="53a37-106">Avoid aliases and partial parameter names, even though they work in Windows PowerShell®.</span></span>

- <span data-ttu-id="53a37-107">Példa leírásában adja meg a parancs építésére ésszerű ismertetik.</span><span class="sxs-lookup"><span data-stu-id="53a37-107">In the example description, explain the rational for the construction of the command.</span></span> <span data-ttu-id="53a37-108">Azt ismerteti, miért döntött az adott paramétereket és értékeket, és a változók használatának módjáról.</span><span class="sxs-lookup"><span data-stu-id="53a37-108">Explain why you chose particular parameters and values, and how you use variables.</span></span>

- <span data-ttu-id="53a37-109">Ha a parancs kifejezéseket használ, ezeket részletesen elmagyarázza.</span><span class="sxs-lookup"><span data-stu-id="53a37-109">If the command uses expressions, explain them in detail.</span></span>

- <span data-ttu-id="53a37-110">Ha a parancs tulajdonságai és metódusai objektumok használ, különösen olyan tulajdonságok, amelyek nem jelennek meg az alapértelmezett megjelenítést a példát követve, mert lehetőséget a felhasználó értesítése az objektumra vonatkozó.</span><span class="sxs-lookup"><span data-stu-id="53a37-110">If the command uses properties and methods of objects, especially properties that do not appear in the default display, use the example as an opportunity tell the user about the object.</span></span>

## <a name="help-views-that-display-examples"></a><span data-ttu-id="53a37-111">Példák megjelenítő nézetek segítségével</span><span class="sxs-lookup"><span data-stu-id="53a37-111">Help Views that Display Examples</span></span>

<span data-ttu-id="53a37-112">Példák csak a Súgó parancsmag részletes és a teljes nézetek jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="53a37-112">Examples appear only in the Detailed and Full views of cmdlet Help.</span></span>

## <a name="adding-an-examples-node"></a><span data-ttu-id="53a37-113">Egy példa csomópont hozzáadása</span><span class="sxs-lookup"><span data-stu-id="53a37-113">Adding an Examples Node</span></span>

<span data-ttu-id="53a37-114">A következő XML-példákat csomópont, amely tartalmazza a példában egyetlen csomópont hozzáadása mutatja be.</span><span class="sxs-lookup"><span data-stu-id="53a37-114">The following XML shows how to add an Examples node that contains a single Example node.</span></span> <span data-ttu-id="53a37-115">Minden egyes példák fel szeretne venni a témakör a további példa csomópontok hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="53a37-115">Add additional example nodes for each examples you want to include in the topic.</span></span>

```xml
<command:examples>
  <command:example>
  </command:example>
</command:examples>
```

## <a name="adding-an-example-title"></a><span data-ttu-id="53a37-116">Egy példa cím hozzáadása</span><span class="sxs-lookup"><span data-stu-id="53a37-116">Adding an Example Title</span></span>

<span data-ttu-id="53a37-117">A következő XML formátumú bemutatja, hogyan például cím megadásához.</span><span class="sxs-lookup"><span data-stu-id="53a37-117">The following XML shows how to add a title for the example.</span></span> <span data-ttu-id="53a37-118">A cím beállítása mellett további példák a példa szolgál.</span><span class="sxs-lookup"><span data-stu-id="53a37-118">The title is used to set the example apart from other examples.</span></span> <span data-ttu-id="53a37-119">Windows PowerShell® használ egy standard fejlécet, amely több egymást követő példában.</span><span class="sxs-lookup"><span data-stu-id="53a37-119">Windows PowerShell® uses a standard header that includes a sequential example number.</span></span>

```xml
<command:examples>
  <command:example>
    <maml:title>----------  EXAMPLE 1  ----------</maml:title>
  </command:example>
</command:examples>
```

## <a name="adding-preceding-characters"></a><span data-ttu-id="53a37-120">Karakterek megelőző hozzáadása</span><span class="sxs-lookup"><span data-stu-id="53a37-120">Adding Preceding Characters</span></span>

<span data-ttu-id="53a37-121">A következő XML formátumú karaktereket, például a Windows PowerShell-parancssort, amely jelennek meg azonnal a példaparancs (bármely beavatkozó szóközök nélkül) előtt adjon hozzá mutatja be.</span><span class="sxs-lookup"><span data-stu-id="53a37-121">The following XML shows how to add characters, such as the Windows PowerShell prompt, that are displayed immediately before the example command (without any intervening spaces).</span></span> <span data-ttu-id="53a37-122">Windows PowerShell® használja a Windows PowerShell-parancssorba: C:\PS>.</span><span class="sxs-lookup"><span data-stu-id="53a37-122">Windows PowerShell® uses the Windows PowerShell prompt: C:\PS>.</span></span>

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

## <a name="adding-the-command"></a><span data-ttu-id="53a37-123">A parancs felvétele</span><span class="sxs-lookup"><span data-stu-id="53a37-123">Adding the Command</span></span>

<span data-ttu-id="53a37-124">A következő XML formátumú adja hozzá a tényleges parancsot a példa szemlélteti.</span><span class="sxs-lookup"><span data-stu-id="53a37-124">The following XML shows how to add the actual command of the example.</span></span> <span data-ttu-id="53a37-125">A parancs való hozzáadásakor, írja be a teljes nevét (ne használja a alias) parancsmagok és paraméterek.</span><span class="sxs-lookup"><span data-stu-id="53a37-125">When adding the command, type the entire name (do not use alias) of cmdlets and parameters.</span></span> <span data-ttu-id="53a37-126">Továbbá a használnak kisbetűs karaktert, amikor csak lehetséges.</span><span class="sxs-lookup"><span data-stu-id="53a37-126">Also, use lowercase characters whenever possible.</span></span>

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

## <a name="adding-a-description"></a><span data-ttu-id="53a37-127">Leírás hozzáadása</span><span class="sxs-lookup"><span data-stu-id="53a37-127">Adding a Description</span></span>

<span data-ttu-id="53a37-128">A következő XML-kódot adjon meg egy leírást a példa szemlélteti.</span><span class="sxs-lookup"><span data-stu-id="53a37-128">The following XML shows how to add a description for the example.</span></span> <span data-ttu-id="53a37-129">Windows PowerShell® használja egyetlen \<maml:para > címkék leírására, akkor is, ha több \<maml:para > címkék használhatók.</span><span class="sxs-lookup"><span data-stu-id="53a37-129">Windows PowerShell® uses a single set of \<maml:para> tags for the description, even though multiple \<maml:para> tags can be used.</span></span>

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

## <a name="adding-example-output"></a><span data-ttu-id="53a37-130">Példa kimenet hozzáadása</span><span class="sxs-lookup"><span data-stu-id="53a37-130">Adding Example Output</span></span>

<span data-ttu-id="53a37-131">A következő XML formátumú adja hozzá a parancs kimenetét mutatja be.</span><span class="sxs-lookup"><span data-stu-id="53a37-131">The following XML shows how to add the output of the command.</span></span> <span data-ttu-id="53a37-132">A parancs eredménye információ megadása nem kötelező, de bizonyos esetekben hasznos lehet a megadott paraméterekkel hatásának bemutatása.</span><span class="sxs-lookup"><span data-stu-id="53a37-132">The command results information is optional, but in some cases it is helpful to demonstrate the effect of using specific parameters.</span></span> <span data-ttu-id="53a37-133">Windows PowerShell® használ üres két készletnyi \<maml:para > címkéket, hogy a parancs kimenete elkülönítése a parancsot.</span><span class="sxs-lookup"><span data-stu-id="53a37-133">Windows PowerShell® uses two sets of blank \<maml:para> tags to separate the command output from the command.</span></span>

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