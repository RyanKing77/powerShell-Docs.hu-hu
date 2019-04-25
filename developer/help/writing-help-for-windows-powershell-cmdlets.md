---
title: A PowerShell-parancsmagok súgóinak |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 55908d67-7cbe-482a-a105-5a6da93c5311
caps.latest.revision: 4
ms.openlocfilehash: 8d692cf88d1d356886ef973f0989294d6b51ee6d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083161"
---
# <a name="writing-help-for-powershell-cmdlets"></a><span data-ttu-id="814ff-102">PowerShell-parancsmagok súgójának írása</span><span class="sxs-lookup"><span data-stu-id="814ff-102">Writing Help for PowerShell Cmdlets</span></span>

<span data-ttu-id="814ff-103">PowerShell-parancsmagokkal lehet hasznos, de, kivéve, ha a súgótémakörök egyértelműen ismertetik a parancsmag funkciója, és hogyan kell használni, a parancsmag nem get használja, vagy még rosszabb, akkor előfordulhat, hogy akadályozná felhasználók.</span><span class="sxs-lookup"><span data-stu-id="814ff-103">PowerShell cmdlets can be useful, but unless your Help topics clearly explain what the cmdlet does and how to use it, the cmdlet may not get used or, even worse, it might frustrate users.</span></span>
<span data-ttu-id="814ff-104">Az XML-alapú parancsmag súgó-fájlformátum fokozza a konzisztencia, de nagyszerű sokkal igényel.</span><span class="sxs-lookup"><span data-stu-id="814ff-104">The XML-based cmdlet Help file format enhances consistency, but great help requires much more.</span></span>

<span data-ttu-id="814ff-105">Ha soha nem írt parancsmag súgójában, tekintse át az alábbi útmutatást.</span><span class="sxs-lookup"><span data-stu-id="814ff-105">If you have never written cmdlet Help, review the following guidelines.</span></span>
<span data-ttu-id="814ff-106">A szükséges ahhoz, hogy a parancsmag súgó-témakörének XML-séma a következő szakaszban leírt.</span><span class="sxs-lookup"><span data-stu-id="814ff-106">The XML schema required to author the cmdlet Help topic is described in the following section.</span></span>
<span data-ttu-id="814ff-107">Kezdje [a parancsmag súgóját fájl létrehozása](./how-to-create-the-cmdlet-help-file.md).</span><span class="sxs-lookup"><span data-stu-id="814ff-107">Start with [Creating the Cmdlet Help File](./how-to-create-the-cmdlet-help-file.md).</span></span>
<span data-ttu-id="814ff-108">A témakör a felső szintű XML-csomópontnak leírását tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="814ff-108">That topic includes a description of the top-level XML nodes.</span></span>

## <a name="writing-guidelines-for-cmdlet-help"></a><span data-ttu-id="814ff-109">A parancsmag súgóját írása irányelvek</span><span class="sxs-lookup"><span data-stu-id="814ff-109">Writing Guidelines for Cmdlet Help</span></span>

### <a name="write-well"></a><span data-ttu-id="814ff-110">Jól írása</span><span class="sxs-lookup"><span data-stu-id="814ff-110">Write well</span></span>
<span data-ttu-id="814ff-111">Semmi nem váltja fel egy jól megírt témakört.</span><span class="sxs-lookup"><span data-stu-id="814ff-111">Nothing replaces a well-written topic.</span></span>
<span data-ttu-id="814ff-112">Ha nem egy professzionális író, író vagy szerkesztő segítségével keresése.</span><span class="sxs-lookup"><span data-stu-id="814ff-112">If you are not a professional writer, find a writer or editor to help you.</span></span>
<span data-ttu-id="814ff-113">Másik lehetőségként a súgószöveg másolja be a Microsoft Word, és a szintaxis használata, és helyesírás-ellenőrzés ellenőrzi, hogy a munkahelyi javítása.</span><span class="sxs-lookup"><span data-stu-id="814ff-113">Another alternative is to copy your Help text into Microsoft Word and use the grammar and spelling checks to improve your work.</span></span>

### <a name="write-simply"></a><span data-ttu-id="814ff-114">Írás egyszerűen</span><span class="sxs-lookup"><span data-stu-id="814ff-114">Write simply</span></span>
<span data-ttu-id="814ff-115">Egyszerű szavak és kifejezések használata.</span><span class="sxs-lookup"><span data-stu-id="814ff-115">Use simple words and phrases.</span></span>
<span data-ttu-id="814ff-116">Kerülje a beszédben.</span><span class="sxs-lookup"><span data-stu-id="814ff-116">Avoid jargon.</span></span>
<span data-ttu-id="814ff-117">Vegye figyelembe, hogy sok olvasók felszerelt csak egy idegen nyelvű szótárban, és a Súgó-témakör.</span><span class="sxs-lookup"><span data-stu-id="814ff-117">Consider that many readers are equipped only with a foreign-language dictionary and your Help topic.</span></span>

### <a name="write-consistently"></a><span data-ttu-id="814ff-118">Folyamatosan írása</span><span class="sxs-lookup"><span data-stu-id="814ff-118">Write consistently</span></span>
<span data-ttu-id="814ff-119">Súgó kapcsolódó parancsmagok (a példában a get-x és a set-x) hasonló lesz.</span><span class="sxs-lookup"><span data-stu-id="814ff-119">Help for related cmdlets should be similar (for example, get-x and set-x).</span></span>
<span data-ttu-id="814ff-120">A standard szintű leírások használata szabványos paraméterek, például **kényszerített** és **InputObject**.</span><span class="sxs-lookup"><span data-stu-id="814ff-120">Use the standard descriptions for standard parameters, like **Force** and **InputObject**.</span></span>
<span data-ttu-id="814ff-121">(Másolja be azokat a Súgó a fő parancsmagjainak.) Normál használati használja.</span><span class="sxs-lookup"><span data-stu-id="814ff-121">(Copy them from Help for the core cmdlets.) Use standard terms.</span></span>
<span data-ttu-id="814ff-122">Például használja "paraméter", nem "argumentum", és használja a "parancsmag" nem "parancs" vagy "parancsmagot."</span><span class="sxs-lookup"><span data-stu-id="814ff-122">For example, use "parameter", not "argument", and use "cmdlet" not "command" or "command-let."</span></span>

### <a name="start-the-synopsis-with-a-verb"></a><span data-ttu-id="814ff-123">Indítsa el a szinopszist és a egy művelet</span><span class="sxs-lookup"><span data-stu-id="814ff-123">Start the synopsis with a verb</span></span>
<span data-ttu-id="814ff-124">A szinopszist mező tájékoztatja a felhasználót, mely a parancsmag nem, mi és működését.</span><span class="sxs-lookup"><span data-stu-id="814ff-124">The synopsis field informs the user what the cmdlet does, not what it is or how it works.</span></span>
<span data-ttu-id="814ff-125">Műveletek hozzon létre egy feladatalapú utasításban, amely tájékoztatja a felhasználókat, ha ez a parancsmag megfelel a követelményeknek.</span><span class="sxs-lookup"><span data-stu-id="814ff-125">Verbs create a task-based statement that informs users if this cmdlet meets their requirements.</span></span>
<span data-ttu-id="814ff-126">Használhat egyszerű műveleteket, például a "get", "create" és "módosítása".</span><span class="sxs-lookup"><span data-stu-id="814ff-126">Use simple verbs like "get", "create", and "change."</span></span>
<span data-ttu-id="814ff-127">Kerülje a "set", amely lehet például a "módosítása" országról és divatos szavakat.</span><span class="sxs-lookup"><span data-stu-id="814ff-127">Avoid "set", which can be vague and fancy words like "modify".</span></span>

### <a name="focus-on-objects"></a><span data-ttu-id="814ff-128">Összpontosítson az objektumok</span><span class="sxs-lookup"><span data-stu-id="814ff-128">Focus on objects</span></span>
<span data-ttu-id="814ff-129">A legtöbb "get" parancsmagok megjelenítési hiba, de az elsődleges funkciója, hogy az objektum lekérése.</span><span class="sxs-lookup"><span data-stu-id="814ff-129">Most "get" cmdlets display something, but their primary function is to get an object.</span></span>
<span data-ttu-id="814ff-130">A segítségre van szüksége dolgozni az objektumot, így a felhasználóknak megérteni, hogy az alapértelmezett megjelenítést egyike legyen, és, hogy használhatják-e a módszerek és a lekért számukra különböző módon objektum tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="814ff-130">In your Help, focus on the object, so that users understand that the default display is one of many, and that they can use the methods and properties of the object that you retrieved for them in different ways.</span></span>

### <a name="write-detailed-descriptions"></a><span data-ttu-id="814ff-131">Részletes leírását írása</span><span class="sxs-lookup"><span data-stu-id="814ff-131">Write detailed descriptions</span></span>
<span data-ttu-id="814ff-132">Röviden listája mindent, ami a parancsmag részletes leírása a végezheti el.</span><span class="sxs-lookup"><span data-stu-id="814ff-132">Briefly list everything that the cmdlet can do in the detailed description.</span></span>
<span data-ttu-id="814ff-133">A fő függvényt egy tulajdonság, de a parancsmag az összes tulajdonságait módosíthatja, ha listájában ez a részletes leírása.</span><span class="sxs-lookup"><span data-stu-id="814ff-133">If the main function is to change one property, but the cmdlet can change all properties, list this in the detailed description.</span></span>

### <a name="use-conventional-syntax"></a><span data-ttu-id="814ff-134">A hagyományos szintaxissal</span><span class="sxs-lookup"><span data-stu-id="814ff-134">Use conventional syntax</span></span>
<span data-ttu-id="814ff-135">A standard Backus-Naur formátum, amely Windows és UNIX rendszerű parancssori súgó gyakori használja.</span><span class="sxs-lookup"><span data-stu-id="814ff-135">Use the standard Backus-Naur format which is common for Windows and UNIX command-line Help.</span></span>

### <a name="use-microsoft-net-framework-types-for-parameter-values"></a><span data-ttu-id="814ff-136">A Microsoft .NET-keretrendszer típusok használata paraméterértékek</span><span class="sxs-lookup"><span data-stu-id="814ff-136">Use Microsoft .NET Framework types for parameter values</span></span>
<span data-ttu-id="814ff-137">A helyőrzőket az paramétereket (a szintaxist és a paraméter leírása) a .NET-keretrendszer az objektumtípus, amely elfogadja a paraméter megjelenítése.</span><span class="sxs-lookup"><span data-stu-id="814ff-137">The placeholders for parameter values (in the syntax and parameter descriptions) show the .NET Framework types of the objects that the parameter will accept.</span></span>
<span data-ttu-id="814ff-138">A PowerShell csapata az egyezmény bemutatja a .NET-keretrendszer segítségével fejlesztett ki.</span><span class="sxs-lookup"><span data-stu-id="814ff-138">The PowerShell team developed this convention to help teach users about the .NET Framework.</span></span>

### <a name="write-complete-parameter-descriptions"></a><span data-ttu-id="814ff-139">A paraméter teljes leírását írása</span><span class="sxs-lookup"><span data-stu-id="814ff-139">Write complete parameter descriptions</span></span>
<span data-ttu-id="814ff-140">Paraméter leírása kell tájékoztatni a felhasználókat két dolgokat: milyen a paraméter nem (a hatás), és mit kell írniuk a paraméterértékeket.</span><span class="sxs-lookup"><span data-stu-id="814ff-140">Parameter descriptions must inform users of two things: what the parameter does (its effect) and what they must type for the parameter values.</span></span>

### <a name="write-practical-examples"></a><span data-ttu-id="814ff-141">Gyakorlati példák írása</span><span class="sxs-lookup"><span data-stu-id="814ff-141">Write practical examples</span></span>
<span data-ttu-id="814ff-142">A példákból kell használata az összes paramétert, de a legfontosabb, hogy a parancsmag használata a való életből vett feladatok megjelenítése.</span><span class="sxs-lookup"><span data-stu-id="814ff-142">The examples should show how to use all of the parameters, but the most important thing is to show how to use the cmdlet in real-world tasks.</span></span>
<span data-ttu-id="814ff-143">Kezdje egy egyszerű példa, és egyre összetettebb példák írása.</span><span class="sxs-lookup"><span data-stu-id="814ff-143">Start with a simple example and write increasingly complex examples.</span></span>
<span data-ttu-id="814ff-144">Az utolsó példában szemléltetik a parancsmag használata egy folyamatban.</span><span class="sxs-lookup"><span data-stu-id="814ff-144">In the final example, show how to use the cmdlet in a pipeline.</span></span>

### <a name="use-the-notes-field"></a><span data-ttu-id="814ff-145">A megjegyzések mezője használata</span><span class="sxs-lookup"><span data-stu-id="814ff-145">Use the Notes field</span></span>
<span data-ttu-id="814ff-146">Használja a megjegyzések mezője annak magyarázata, hogy felhasználóknak tisztában kell lenniük a parancsmag fogalmakat.</span><span class="sxs-lookup"><span data-stu-id="814ff-146">Use the Notes field to explain concepts that users need to understand the cmdlet.</span></span>
<span data-ttu-id="814ff-147">Megjegyzések használatával segítség a felhasználóknak a gyakori hibák elkerülése érdekében.</span><span class="sxs-lookup"><span data-stu-id="814ff-147">You can also use notes to help users avoid common errors.</span></span>
<span data-ttu-id="814ff-148">Kerülje az URL-címek, ahogy változnak.</span><span class="sxs-lookup"><span data-stu-id="814ff-148">Avoid URLs as they change.</span></span>
<span data-ttu-id="814ff-149">Ehelyett adja meg a felhasználók használati kereséséhez.</span><span class="sxs-lookup"><span data-stu-id="814ff-149">Instead, provide users terms to search for.</span></span>

### <a name="test-your-help"></a><span data-ttu-id="814ff-150">A Súgó tesztelése</span><span class="sxs-lookup"><span data-stu-id="814ff-150">Test your Help</span></span>
<span data-ttu-id="814ff-151">Tesztelje a Súgó, ugyanúgy, mint a tesztelhetnek.</span><span class="sxs-lookup"><span data-stu-id="814ff-151">Test the Help just like you test your code.</span></span>
<span data-ttu-id="814ff-152">Barátok és munkatársakkal olvassa el a Súgó tartalma, és visszajelzést.</span><span class="sxs-lookup"><span data-stu-id="814ff-152">Have friends and colleagues read your Help content and provide feedback.</span></span>
<span data-ttu-id="814ff-153">Akkor is hozzájárulásával hírcsoportokat visszajelzést is.</span><span class="sxs-lookup"><span data-stu-id="814ff-153">You can also solicit feedback from newsgroups.</span></span>

## <a name="see-also"></a><span data-ttu-id="814ff-154">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="814ff-154">See Also</span></span>

 [<span data-ttu-id="814ff-155">A parancsmag súgóját fájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="814ff-155">How to Create the Cmdlet Help File</span></span>](./how-to-create-the-cmdlet-help-file.md)

 [<span data-ttu-id="814ff-156">A parancsmag neve és a Szinopszist parancsmag Súgó-témakör hozzáadása</span><span class="sxs-lookup"><span data-stu-id="814ff-156">How to Add the Cmdlet Name and Synopsis to a Cmdlet Help Topic</span></span>](./how-to-add-the-cmdlet-name-and-synopsis-to-a-cmdlet-help-topic.md)

 [<span data-ttu-id="814ff-157">A részletes leírás egy parancsmag Súgó-témakör hozzáadása</span><span class="sxs-lookup"><span data-stu-id="814ff-157">How to Add the Detailed Description to a Cmdlet Help Topic</span></span>](./how-to-add-a-cmdlet-description.md)

 [<span data-ttu-id="814ff-158">Szintaxis egy parancsmag Súgó-témakör hozzáadása</span><span class="sxs-lookup"><span data-stu-id="814ff-158">How to Add Syntax to a Cmdlet Help Topic</span></span>](./how-to-add-syntax-to-a-cmdlet-help-topic.md)

 [<span data-ttu-id="814ff-159">Egy parancsmag súgó-témakörének paraméterek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="814ff-159">How to Add Parameters to a Cmdlet Help Topic</span></span>](./how-to-add-parameter-information.md)

 [<span data-ttu-id="814ff-160">Bemeneti típusok egy parancsmag Súgó-témakör hozzáadása</span><span class="sxs-lookup"><span data-stu-id="814ff-160">How to add Input Types to a Cmdlet Help Topic</span></span>](./how-to-add-input-types-to-a-cmdlet-help-topic.md)

 [<span data-ttu-id="814ff-161">Visszaadott értékeket a parancsmag Súgó-témakör hozzáadása</span><span class="sxs-lookup"><span data-stu-id="814ff-161">How to Add Return Values to a Cmdlet Help Topic</span></span>](./how-to-add-return-values-to-a-cmdlet-help-topic.md)

 [<span data-ttu-id="814ff-162">Egy parancsmag súgó-témakörének megjegyzések hozzáadása</span><span class="sxs-lookup"><span data-stu-id="814ff-162">How to Add Notes to a Cmdlet Help Topic</span></span>](./how-to-add-notes-to-a-cmdlet-help-topic.md)

 [<span data-ttu-id="814ff-163">Példák, a parancsmag Súgó-témakör hozzáadása</span><span class="sxs-lookup"><span data-stu-id="814ff-163">How to Add Examples to a Cmdlet Help Topic</span></span>](./how-to-add-examples-to-a-cmdlet-help-topic.md)

 [<span data-ttu-id="814ff-164">Kapcsolódó hivatkozások hozzáadása egy parancsmag Súgó-témakör</span><span class="sxs-lookup"><span data-stu-id="814ff-164">How to Add Related Links to a Cmdlet Help Topic</span></span>](./how-to-add-related-links-to-a-cmdlet-help-topic.md)

 [<span data-ttu-id="814ff-165">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="814ff-165">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)