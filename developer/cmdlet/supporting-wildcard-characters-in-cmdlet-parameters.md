---
title: A helyettesítő karakterek támogató parancsmag-paraméterek |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- wildcards [PowerShell Programmer's Guide]
- parameters [PowerShell Programmer's Guide], wildcards
ms.assetid: 9b26e1e9-9350-4a5a-aad5-ddcece658d93
caps.latest.revision: 12
ms.openlocfilehash: 6c762d3889bc4b649252390625525db4735f4c1d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067399"
---
# <a name="supporting-wildcard-characters-in-cmdlet-parameters"></a><span data-ttu-id="abc0e-102">Helyettesítő karakterek támogatása parancsmag-paraméterekben</span><span class="sxs-lookup"><span data-stu-id="abc0e-102">Supporting Wildcard Characters in Cmdlet Parameters</span></span>

<span data-ttu-id="abc0e-103">Gyakran előfordul akkor tervezhet a parancsmag futtatásához az erőforrások csoportjához, nem pedig egy egyetlen erőforrás ellen.</span><span class="sxs-lookup"><span data-stu-id="abc0e-103">Often, you will have to design a cmdlet to run against a group of resources rather than against a single resource.</span></span> <span data-ttu-id="abc0e-104">Például a parancsmag található összes fájl egy azonos nevű vagy kiterjesztéssel rendelkező adattárban előfordulhat, hogy kell.</span><span class="sxs-lookup"><span data-stu-id="abc0e-104">For example, a cmdlet might need to locate all the files in a data store that have the same name or extension.</span></span> <span data-ttu-id="abc0e-105">Egy parancsmag, amely akkor erőforrások csoportjához kialakításakor kell biztosítanak támogatást a helyettesítő karakterek.</span><span class="sxs-lookup"><span data-stu-id="abc0e-105">You must provide support for wildcard characters when you design a cmdlet that will be run against a group of resources.</span></span>

> [!NOTE]
> <span data-ttu-id="abc0e-106">A helyettesítő karakterek használatával van más néven *helyettesítés*.</span><span class="sxs-lookup"><span data-stu-id="abc0e-106">Using wildcard characters is sometimes referred to as *globbing*.</span></span>

## <a name="windows-powershell-cmdlets-that-use-wildcards"></a><span data-ttu-id="abc0e-107">A helyettesítő karakterek használata, a Windows PowerShell-parancsmagok</span><span class="sxs-lookup"><span data-stu-id="abc0e-107">Windows PowerShell Cmdlets That Use Wildcards</span></span>

 <span data-ttu-id="abc0e-108">Számos Windows PowerShell-parancsmagok a helyettesítő karakterek támogatása a paraméterértékeket.</span><span class="sxs-lookup"><span data-stu-id="abc0e-108">Many Windows PowerShell cmdlets support wildcard characters for their parameter values.</span></span> <span data-ttu-id="abc0e-109">Ha például szinte minden parancsmag, amely rendelkezik egy `Name` vagy `Path` paraméter támogatja a helyettesítő karakterek ezeket a paramétereket.</span><span class="sxs-lookup"><span data-stu-id="abc0e-109">For example, almost every cmdlet that has a `Name` or `Path` parameter supports wildcard characters for these parameters.</span></span> <span data-ttu-id="abc0e-110">(Bár a legtöbb parancsmag, amely rendelkezik egy `Path` paraméter is rendelkezik egy `LiteralPath` paraméter, amely nem támogatja a helyettesítő karakterek.) A következő parancs bemutatja, hogyan helyettesítő karaktert adja vissza az összes parancsmagot a jelenlegi munkamenet, amelynek a neve tartalmazza a Get-verb szolgál.</span><span class="sxs-lookup"><span data-stu-id="abc0e-110">(Although most cmdlets that have a `Path` parameter also have a `LiteralPath` parameter that does not support wildcard characters.) The following command shows how a wildcard character is used to return all the cmdlets in the current session whose name contains the Get verb.</span></span>

 <span data-ttu-id="abc0e-111">**PS > get-command get -\***</span><span class="sxs-lookup"><span data-stu-id="abc0e-111">**PS>get-command get-\***</span></span>

## <a name="supported-wildcard-characters"></a><span data-ttu-id="abc0e-112">Támogatott helyettesítő karakterek</span><span class="sxs-lookup"><span data-stu-id="abc0e-112">Supported Wildcard Characters</span></span>

<span data-ttu-id="abc0e-113">Windows PowerShell támogatja a következő helyettesítő karaktereket.</span><span class="sxs-lookup"><span data-stu-id="abc0e-113">Windows PowerShell supports the following wildcard characters.</span></span>

|<span data-ttu-id="abc0e-114">Helyettesítő karakter</span><span class="sxs-lookup"><span data-stu-id="abc0e-114">Wildcard character</span></span>|<span data-ttu-id="abc0e-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="abc0e-115">Description</span></span>|<span data-ttu-id="abc0e-116">Példa</span><span class="sxs-lookup"><span data-stu-id="abc0e-116">Example</span></span>|<span data-ttu-id="abc0e-117">Egyezik</span><span class="sxs-lookup"><span data-stu-id="abc0e-117">Matches</span></span>|<span data-ttu-id="abc0e-118">Nem egyezik</span><span class="sxs-lookup"><span data-stu-id="abc0e-118">Does not match</span></span>|
|------------------------|-----------------|-------------|-------------|--------------------|
|*|<span data-ttu-id="abc0e-119">A megadott pozíciótól kezdődően nulla vagy több karakterre illeszkedik</span><span class="sxs-lookup"><span data-stu-id="abc0e-119">Matches zero or more characters, starting at the specified position</span></span>|<span data-ttu-id="abc0e-120">a\*</span><span class="sxs-lookup"><span data-stu-id="abc0e-120">a\*</span></span>|<span data-ttu-id="abc0e-121">A, ag, Apple</span><span class="sxs-lookup"><span data-stu-id="abc0e-121">A, ag, Apple</span></span>||
|<span data-ttu-id="abc0e-122">?</span><span class="sxs-lookup"><span data-stu-id="abc0e-122">?</span></span>|<span data-ttu-id="abc0e-123">A megadott pozíciónál található egyezés anycharacter</span><span class="sxs-lookup"><span data-stu-id="abc0e-123">Matches anycharacter at the specified position</span></span>|<span data-ttu-id="abc0e-124">?n</span><span class="sxs-lookup"><span data-stu-id="abc0e-124">?n</span></span>|<span data-ttu-id="abc0e-125">Egy, a, a</span><span class="sxs-lookup"><span data-stu-id="abc0e-125">An, in, on</span></span>|<span data-ttu-id="abc0e-126">futott</span><span class="sxs-lookup"><span data-stu-id="abc0e-126">ran</span></span>|
|<span data-ttu-id="abc0e-127">[ ]</span><span class="sxs-lookup"><span data-stu-id="abc0e-127">[ ]</span></span>|<span data-ttu-id="abc0e-128">Egy karaktertartományt megfelel</span><span class="sxs-lookup"><span data-stu-id="abc0e-128">Matches a range of characters</span></span>|<span data-ttu-id="abc0e-129">[a-l]ook</span><span class="sxs-lookup"><span data-stu-id="abc0e-129">[a-l]ook</span></span>|<span data-ttu-id="abc0e-130">könyv, cook, tekintse meg</span><span class="sxs-lookup"><span data-stu-id="abc0e-130">book, cook, look</span></span>|<span data-ttu-id="abc0e-131">tartott</span><span class="sxs-lookup"><span data-stu-id="abc0e-131">took</span></span>|
|<span data-ttu-id="abc0e-132">[ ]</span><span class="sxs-lookup"><span data-stu-id="abc0e-132">[ ]</span></span>|<span data-ttu-id="abc0e-133">A megadott karakterre illeszkedik</span><span class="sxs-lookup"><span data-stu-id="abc0e-133">Matches the specified characters</span></span>|<span data-ttu-id="abc0e-134">[bc]ook</span><span class="sxs-lookup"><span data-stu-id="abc0e-134">[bc]ook</span></span>|<span data-ttu-id="abc0e-135">könyv, cook</span><span class="sxs-lookup"><span data-stu-id="abc0e-135">book, cook</span></span>|<span data-ttu-id="abc0e-136">nézd</span><span class="sxs-lookup"><span data-stu-id="abc0e-136">look</span></span>|

<span data-ttu-id="abc0e-137">A helyettesítő karakterek támogató parancsmagok tervezésekor lehetővé teszi a helyettesítő karakterek kombinációját.</span><span class="sxs-lookup"><span data-stu-id="abc0e-137">When you design cmdlets that support wildcard characters, allow for combinations of wildcard characters.</span></span> <span data-ttu-id="abc0e-138">Használja az alábbi parancs például a `Get-ChildItem` parancsmag a .txt fájlok, amelyek a c:\Techdocs mappában, és, betűkkel kezdődik "a" és "l."</span><span class="sxs-lookup"><span data-stu-id="abc0e-138">For example, the following command uses the `Get-ChildItem` cmdlet to retrieve all the .txt files that are in the c:\Techdocs folder and that begin with the letters "a" through "l."</span></span>

<span data-ttu-id="abc0e-139">**Get-childitem c:\techdocs\\[a-l]\*.txt**</span><span class="sxs-lookup"><span data-stu-id="abc0e-139">**get-childitem c:\techdocs\\[a-l]\*.txt**</span></span>

<span data-ttu-id="abc0e-140">Az előző parancs használja a tartomány helyettesítő **[a-l]** megadásához, hogy a fájl nevét kell karakterekkel kezdődnek "a" és "l."</span><span class="sxs-lookup"><span data-stu-id="abc0e-140">The previous command uses the range wildcard **[a-l]** to specify that the file name should begin with the characters "a" through "l."</span></span> <span data-ttu-id="abc0e-141">A parancsot, majd használja a \* helyettesítő karaktert bármely karakter között a fájl nevének első betűje és a .txt kiterjesztése helyettesíti.</span><span class="sxs-lookup"><span data-stu-id="abc0e-141">The command then uses the \* wildcard character as a placeholder for any characters between the first letter of the file name and the .txt extension.</span></span>

<span data-ttu-id="abc0e-142">Az alábbi példában egy tartomány helyettesítő karakterrel, amely nem tartalmazza a "d" betű, de a "a" és "f." az összes többi betűt tartalmaz</span><span class="sxs-lookup"><span data-stu-id="abc0e-142">The following example uses a range wildcard pattern that excludes the letter "d" but includes all the other letters from "a" through "f."</span></span>

<span data-ttu-id="abc0e-143">**Get-childitem c:\techdocs\\[a-cef]\*.txt**</span><span class="sxs-lookup"><span data-stu-id="abc0e-143">**get-childitem c:\techdocs\\[a-cef]\*.txt**</span></span>

## <a name="handling-literal-characters-in-wildcard-patterns"></a><span data-ttu-id="abc0e-144">Helyettesítő karakterek mintái literális karakter kezelése</span><span class="sxs-lookup"><span data-stu-id="abc0e-144">Handling Literal Characters in Wildcard Patterns</span></span>

<span data-ttu-id="abc0e-145">Ha a helyettesítő karakterrel megadott szövegkonstans karaktereket tartalmaz, használja a használni kívánt szintaxiskiemelést karaktert (') escape-karakter.</span><span class="sxs-lookup"><span data-stu-id="abc0e-145">If the wildcard pattern you specify contains literal characters, use the backtick character (\`) as an escape character.</span></span> <span data-ttu-id="abc0e-146">Ha programozott módon adja meg a literális karakter, használja egy egyetlen használni kívánt szintaxiskiemelést.</span><span class="sxs-lookup"><span data-stu-id="abc0e-146">When you specify literal characters programmatically, use a single backtick.</span></span> <span data-ttu-id="abc0e-147">A parancssorban literális karakter megadása esetén két backticks használja.</span><span class="sxs-lookup"><span data-stu-id="abc0e-147">When you specify literal characters at the command prompt, use two backticks.</span></span> <span data-ttu-id="abc0e-148">A következő mintát tartalmazza például két zárójelben, amely szerint kell értelmezni.</span><span class="sxs-lookup"><span data-stu-id="abc0e-148">For example, the following pattern contains two brackets that must be taken literally.</span></span>

<span data-ttu-id="abc0e-149">"John Smith \`[\*"] "(megadott programozott módon)</span><span class="sxs-lookup"><span data-stu-id="abc0e-149">"John Smith \`[\*\`]" (specified programmatically)</span></span>

<span data-ttu-id="abc0e-150">"John Smith \` \`[\*\`"] "(a parancssorban megadott)</span><span class="sxs-lookup"><span data-stu-id="abc0e-150">"John Smith \`\`[\*\`\`]"  (specified at the command prompt)</span></span>

<span data-ttu-id="abc0e-151">Ez a minta illeszkedik "John Smith [Marketing]" vagy "John Smith [fejlesztési]".</span><span class="sxs-lookup"><span data-stu-id="abc0e-151">This pattern matches "John Smith [Marketing]" or "John Smith [Development]".</span></span>

## <a name="cmdlet-output-and-wildcard-characters"></a><span data-ttu-id="abc0e-152">A parancsmag kimenete és a helyettesítő karakterek</span><span class="sxs-lookup"><span data-stu-id="abc0e-152">Cmdlet Output and Wildcard Characters</span></span>

<span data-ttu-id="abc0e-153">Parancsmag-paraméterek támogatja a helyettesítő karaktereket, amikor egy parancsmag-műveletet, az általában egy tömb kimeneti állít elő.</span><span class="sxs-lookup"><span data-stu-id="abc0e-153">When cmdlet parameters support wildcard characters, a cmdlet operation usually generates an array output.</span></span> <span data-ttu-id="abc0e-154">Néha előfordul logikus nem támogatja a kimeneti, mert a felhasználó egyszerre csak egy elemet lehet, hogy használ egy tömb.</span><span class="sxs-lookup"><span data-stu-id="abc0e-154">Occasionally, it makes no sense to support an array output because the user might use only a single item at a time.</span></span> <span data-ttu-id="abc0e-155">Ha például a `Set-Location` parancsmag támogatja a tömb kimeneti, mert a felhasználó csak egyetlen helyen állítja.</span><span class="sxs-lookup"><span data-stu-id="abc0e-155">For example, the `Set-Location` cmdlet does support an array output because the user sets only a single location.</span></span> <span data-ttu-id="abc0e-156">Ebben a példában a parancsmag továbbra is támogatja a helyettesítő karaktereket, de feloldási kényszerül, egyetlen helyen.</span><span class="sxs-lookup"><span data-stu-id="abc0e-156">In this instance, the cmdlet still supports wildcard characters, but it forces resolution to a single location.</span></span>

## <a name="see-also"></a><span data-ttu-id="abc0e-157">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="abc0e-157">See Also</span></span>

[<span data-ttu-id="abc0e-158">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="abc0e-158">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)

[<span data-ttu-id="abc0e-159">WildcardPattern osztályban</span><span class="sxs-lookup"><span data-stu-id="abc0e-159">WildcardPattern Class</span></span>](/dotnet/api/system.management.automation.wildcardpattern)
