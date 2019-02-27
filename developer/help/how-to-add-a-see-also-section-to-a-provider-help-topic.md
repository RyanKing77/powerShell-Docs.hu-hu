---
title: Hogyan lehet hozzáadni egy lásd is szakasz szolgáltató súgótémakör |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9c754ac3-cee3-4c13-9bad-e499c8a68a09
caps.latest.revision: 4
ms.openlocfilehash: f5c48fd04c620828a6e99c5c5424d11b31fd10e5
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848453"
---
# <a name="how-to-add-a-see-also-section-to-a-provider-help-topic"></a><span data-ttu-id="e6c5b-102">„Lásd még” szakasz hozzáadása egy szolgáltatói súgótémakörhöz</span><span class="sxs-lookup"><span data-stu-id="e6c5b-102">How to Add a See Also Section to a Provider Help Topic</span></span>

<span data-ttu-id="e6c5b-103">Ez a szakasz azt ismerteti, hogyan töltse fel a **lásd még** szolgáltató súgótémakör szakaszában.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-103">This section explains how to populate the **SEE ALSO** section of a provider help topic.</span></span>

<span data-ttu-id="e6c5b-104">A **lásd még** szakasz témaköröket a szolgáltatóhoz kapcsolódó vagy segíthetnek a felhasználó jobb megismerésében és a szolgáltatóval áll.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-104">The **SEE ALSO** section consists of a list of topics that are related to the provider or might help the user better understand and use the provider.</span></span> <span data-ttu-id="e6c5b-105">A témakör lehetnek parancsmag súgóját, szolgáltató Súgó és fogalmi ("tudnivalók") a Windows PowerShellben Súgó-témaköröket.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-105">The topic list can include cmdlet help, provider help and conceptual ("about") help topics in Windows PowerShell.</span></span> <span data-ttu-id="e6c5b-106">Könyvekben, tanulmány és online témaköreit, beleértve az aktuális szolgáltató témakör online verzióját mutató hivatkozásokat is tartalmazhat.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-106">It can also include references to books, paper, and online topics, including an online version of the current provider help topic.</span></span>

<span data-ttu-id="e6c5b-107">Amikor online témaköröket, adja meg az URI-t vagy egyszerű szöveges keresési kifejezés.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-107">When you refer to online topics, provide the URI or a search term in plain text.</span></span> <span data-ttu-id="e6c5b-108">A `Get-Help` parancsmag nem hivatkozásra, és irányítsa át a listában a tájékozódhat.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-108">The `Get-Help` cmdlet does not link or redirect to any of the topics in the list.</span></span> <span data-ttu-id="e6c5b-109">Emellett a `Online` paraméterében a `Get-Help` parancsmag nem működik a szolgáltató segítségével.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-109">Also, the `Online` parameter of the `Get-Help` cmdlet does not work with provider help.</span></span>

<span data-ttu-id="e6c5b-110">A Lásd még szakaszban alapján hozza létre a `RelatedLinks` elem és a benne található címkéket.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-110">The See Also section is created from the `RelatedLinks` element and the tags that it contains.</span></span> <span data-ttu-id="e6c5b-111">A következő XML formátumú bemutatja, hogyan adja hozzá a címkéket.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-111">The following XML shows how to add the tags.</span></span>

### <a name="to-add-see-also-topics"></a><span data-ttu-id="e6c5b-112">"Lásd még" témakörök hozzáadása</span><span class="sxs-lookup"><span data-stu-id="e6c5b-112">To Add "SEE ALSO" Topics</span></span>

1. <span data-ttu-id="e6c5b-113">Az a *AssemblyName*belül a .dll-help.xml fájlt a `providerHelp` elem, adjon hozzá egy `RelatedLinks` elem.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-113">In the *AssemblyName*.dll-help.xml file, within the `providerHelp` element, add a `RelatedLinks` element.</span></span> <span data-ttu-id="e6c5b-114">A `RelatedLinks` elemnek kell lennie az utolsó elem az a `providerHelp` elemet.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-114">The `RelatedLinks` element should be the last element in the `providerHelp` element.</span></span> <span data-ttu-id="e6c5b-115">Csak egy `RelatedLinks` elem engedélyezett a minden szolgáltató Súgó-témakör.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-115">Only one `RelatedLinks` element is permitted in each provider help topic.</span></span>

   <span data-ttu-id="e6c5b-116">Például:</span><span class="sxs-lookup"><span data-stu-id="e6c5b-116">For example:</span></span>

    ```xml
    <providerHelp>
        <RelatedLinks>
        </RelatedLinks>
    </providerHelp>
    ```

2. <span data-ttu-id="e6c5b-117">Az egyes témakörében a **lásd még** szakasz belül a `RelatedLinks` elem, adjon hozzá egy `navigationLink` elem.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-117">For each topic in the **SEE ALSO** section, within the `RelatedLinks` element, add a `navigationLink` element.</span></span> <span data-ttu-id="e6c5b-118">Ezt követően belül `navigationLink` elem, vegyen fel egy `linkText` elem és a egy `uri` elemet.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-118">Then, within each `navigationLink` element, add one `linkText` element and one `uri` element.</span></span> <span data-ttu-id="e6c5b-119">Ha nem használ a `uri` elemben adhatja hozzá őket egy üres elemeként (\<uri / >).</span><span class="sxs-lookup"><span data-stu-id="e6c5b-119">If you are not using the `uri` element, you can add it as an empty element (\<uri/>).</span></span>

   <span data-ttu-id="e6c5b-120">Például:</span><span class="sxs-lookup"><span data-stu-id="e6c5b-120">For example:</span></span>

    ```xml
    <providerHelp>
        <RelatedLinks>
            <navigationLink>
                <linkText> </linkText>
                <uri> </uri>
            </navigationLink>
        </RelatedLinks>
    </providerHelp>
    ```

3. <span data-ttu-id="e6c5b-121">Írja be a témakör nevét között a `linkText` címkék.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-121">Type the topic name between the `linkText` tags.</span></span> <span data-ttu-id="e6c5b-122">Ha meg van adva egy URI-t, írja be között a `uri` címkék.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-122">If you are providing a URI, type it between the `uri` tags.</span></span> <span data-ttu-id="e6c5b-123">Az aktuális szolgáltató témakör online verzióját között jelzi a `linkText` címkék, típus "Online verzió:" a témakör neve helyett.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-123">To indicate the online version of the current provider help topic, between the `linkText` tags, type "Online version:" instead of the topic name.</span></span> <span data-ttu-id="e6c5b-124">Általában a "Online verzió:" hivatkozás az első témakörében a Lásd még a témakör listában.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-124">Typically, the "Online version:" link is the first topic in the SEE ALSO topic list.</span></span>

   <span data-ttu-id="e6c5b-125">Az alábbi példa három lásd még témakörök tartalmazzák.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-125">The following example include three SEE ALSO topics.</span></span> <span data-ttu-id="e6c5b-126">Az első tekintse meg az aktuális témakör online verzióját.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-126">The first refer to the online version of the current topic.</span></span> <span data-ttu-id="e6c5b-127">A második egy Windows PowerShell parancsmag súgó-témakörének hivatkozik.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-127">The second refers to a Windows PowerShell cmdlet help topic.</span></span> <span data-ttu-id="e6c5b-128">A harmadik hivatkozik egy online témakört.</span><span class="sxs-lookup"><span data-stu-id="e6c5b-128">The third refers to another online topic.</span></span>

    ```xml
    <providerHelp>
        <RelatedLinks>
            <navigationLink>
                <linkText> Online version: </linkText>
                <uri>http://www.fabrikam.com/help/myFunction.htm</uri>
            </navigationLink>
            <navigationLink>
                <linkText> about_functions </linkText>
                <uri/>
            </navigationLink>
            <navigationLink>
                <linkText> Windows PowerShell Getting Started Guide </linkText>
                <uri>http://go.microsoft.com/fwlink/?LinkID=89597<uri/>
            </navigationLink>
        </RelatedLinks>
    </providerHelp>
    ```