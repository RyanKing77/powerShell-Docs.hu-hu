---
title: Helyettesítő karakterek támogatása parancsmag-paraméterekben
ms.custom: ''
ms.date: 08/26/2019
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.openlocfilehash: 19644c5bc186a5554d6b134a67fc7c4d7aa7b64c
ms.sourcegitcommit: a02ccbeaa17c0e513d6c4a21b877c88ac7725458
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/28/2019
ms.locfileid: "70104448"
---
# <a name="supporting-wildcard-characters-in-cmdlet-parameters"></a><span data-ttu-id="b1df1-102">Helyettesítő karakterek támogatása parancsmag-paraméterekben</span><span class="sxs-lookup"><span data-stu-id="b1df1-102">Supporting Wildcard Characters in Cmdlet Parameters</span></span>

<span data-ttu-id="b1df1-103">Gyakran olyan parancsmagot kell megterveznie, amely egy erőforrás-csoporton fut ahelyett, hogy egyetlen erőforrásra lenne szüksége.</span><span class="sxs-lookup"><span data-stu-id="b1df1-103">Often, you will have to design a cmdlet to run against a group of resources rather than against a single resource.</span></span> <span data-ttu-id="b1df1-104">Előfordulhat például, hogy egy parancsmagnak meg kell keresnie egy azonos nevű vagy kiterjesztésű adattár összes fájlját.</span><span class="sxs-lookup"><span data-stu-id="b1df1-104">For example, a cmdlet might need to locate all the files in a data store that have the same name or extension.</span></span> <span data-ttu-id="b1df1-105">Meg kell adnia a helyettesítő karakterek támogatását, ha olyan parancsmagot tervez, amely egy erőforrás-csoporton fog futni.</span><span class="sxs-lookup"><span data-stu-id="b1df1-105">You must provide support for wildcard characters when you design a cmdlet that will be run against a group of resources.</span></span>

> [!NOTE]
> <span data-ttu-id="b1df1-106">A helyettesítő karakterek használata más néven *globbing*.</span><span class="sxs-lookup"><span data-stu-id="b1df1-106">Using wildcard characters is sometimes referred to as *globbing*.</span></span>

## <a name="windows-powershell-cmdlets-that-use-wildcards"></a><span data-ttu-id="b1df1-107">Helyettesítő karaktereket használó Windows PowerShell-parancsmagok</span><span class="sxs-lookup"><span data-stu-id="b1df1-107">Windows PowerShell Cmdlets That Use Wildcards</span></span>

 <span data-ttu-id="b1df1-108">Számos Windows PowerShell-parancsmag támogatja a helyettesítő karaktereket a paraméter értékeinél.</span><span class="sxs-lookup"><span data-stu-id="b1df1-108">Many Windows PowerShell cmdlets support wildcard characters for their parameter values.</span></span> <span data-ttu-id="b1df1-109">Például szinte minden olyan parancsmag, amely a vagy `Name` `Path` a paraméterrel rendelkezik, helyettesítő karaktereket is támogat ezekhez a paraméterekhez.</span><span class="sxs-lookup"><span data-stu-id="b1df1-109">For example, almost every cmdlet that has a `Name` or `Path` parameter supports wildcard characters for these parameters.</span></span> <span data-ttu-id="b1df1-110">(Habár a `Path` paraméterrel rendelkező legtöbb parancsmag olyan paraméterrel is `LiteralPath` rendelkezik, amely nem támogatja a helyettesítő karaktereket.) A következő parancs bemutatja, hogyan használható helyettesítő karakter az aktuális munkamenetben lévő összes olyan parancsmag visszaküldéséhez, amelynek a neve tartalmazza a Get műveletet.</span><span class="sxs-lookup"><span data-stu-id="b1df1-110">(Although most cmdlets that have a `Path` parameter also have a `LiteralPath` parameter that does not support wildcard characters.) The following command shows how a wildcard character is used to return all the cmdlets in the current session whose name contains the Get verb.</span></span>

 `Get-Command get-*`

## <a name="supported-wildcard-characters"></a><span data-ttu-id="b1df1-111">Támogatott helyettesítő karakterek</span><span class="sxs-lookup"><span data-stu-id="b1df1-111">Supported Wildcard Characters</span></span>

<span data-ttu-id="b1df1-112">A Windows PowerShell a következő helyettesítő karaktereket támogatja.</span><span class="sxs-lookup"><span data-stu-id="b1df1-112">Windows PowerShell supports the following wildcard characters.</span></span>

| <span data-ttu-id="b1df1-113">Helyettesítő</span><span class="sxs-lookup"><span data-stu-id="b1df1-113">Wildcard</span></span> |                             <span data-ttu-id="b1df1-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="b1df1-114">Description</span></span>                             |  <span data-ttu-id="b1df1-115">Példa</span><span class="sxs-lookup"><span data-stu-id="b1df1-115">Example</span></span>   |     <span data-ttu-id="b1df1-116">Egyezik</span><span class="sxs-lookup"><span data-stu-id="b1df1-116">Matches</span></span>      | <span data-ttu-id="b1df1-117">Nem egyezik</span><span class="sxs-lookup"><span data-stu-id="b1df1-117">Does not match</span></span> |
| -------- | ------------------------------------------------------------------- | ---------- | ---------------- | -------------- |
| *        | <span data-ttu-id="b1df1-118">Nulla vagy több karakternek felel meg, a megadott pozíciótól kezdve</span><span class="sxs-lookup"><span data-stu-id="b1df1-118">Matches zero or more characters, starting at the specified position</span></span> | `a*`       | <span data-ttu-id="b1df1-119">A, AG, Apple</span><span class="sxs-lookup"><span data-stu-id="b1df1-119">A, ag, Apple</span></span>     |                |
| <span data-ttu-id="b1df1-120">?</span><span class="sxs-lookup"><span data-stu-id="b1df1-120">?</span></span>        | <span data-ttu-id="b1df1-121">Minden karakternek megfelel a megadott pozícióban</span><span class="sxs-lookup"><span data-stu-id="b1df1-121">Matches any character at the specified position</span></span>                     | `?n`       | <span data-ttu-id="b1df1-122">Egy, a, be</span><span class="sxs-lookup"><span data-stu-id="b1df1-122">An, in, on</span></span>       | <span data-ttu-id="b1df1-123">futott</span><span class="sxs-lookup"><span data-stu-id="b1df1-123">ran</span></span>            |
| <span data-ttu-id="b1df1-124">[ ]</span><span class="sxs-lookup"><span data-stu-id="b1df1-124">[ ]</span></span>      | <span data-ttu-id="b1df1-125">Számos karakterből áll</span><span class="sxs-lookup"><span data-stu-id="b1df1-125">Matches a range of characters</span></span>                                       | `[a-l]ook` | <span data-ttu-id="b1df1-126">könyv, Cook, Look</span><span class="sxs-lookup"><span data-stu-id="b1df1-126">book, cook, look</span></span> | <span data-ttu-id="b1df1-127">Zug, elvitt</span><span class="sxs-lookup"><span data-stu-id="b1df1-127">nook, took</span></span>     |
| <span data-ttu-id="b1df1-128">[ ]</span><span class="sxs-lookup"><span data-stu-id="b1df1-128">[ ]</span></span>      | <span data-ttu-id="b1df1-129">Megfelel a megadott karaktereknek</span><span class="sxs-lookup"><span data-stu-id="b1df1-129">Matches the specified characters</span></span>                                    | `[bn]ook`  | <span data-ttu-id="b1df1-130">könyv, Zug</span><span class="sxs-lookup"><span data-stu-id="b1df1-130">book, nook</span></span>       | <span data-ttu-id="b1df1-131">Cook, Look</span><span class="sxs-lookup"><span data-stu-id="b1df1-131">cook, look</span></span>     |

<span data-ttu-id="b1df1-132">A helyettesítő karaktereket támogató parancsmagok tervezésekor engedélyezze a helyettesítő karakterek kombinációját.</span><span class="sxs-lookup"><span data-stu-id="b1df1-132">When you design cmdlets that support wildcard characters, allow for combinations of wildcard characters.</span></span> <span data-ttu-id="b1df1-133">A következő parancs például a `Get-ChildItem` parancsmag használatával kéri le a c:\Techdocs mappában található összes. txt fájlt, amely az "a" betűvel kezdődik az "l" értékkel.</span><span class="sxs-lookup"><span data-stu-id="b1df1-133">For example, the following command uses the `Get-ChildItem` cmdlet to retrieve all the .txt files that are in the c:\Techdocs folder and that begin with the letters "a" through "l."</span></span>

`Get-ChildItem c:\techdocs\[a-l]\*.txt`

<span data-ttu-id="b1df1-134">Az előző parancs a tartomány helyettesítő karakterét `[a-l]` használja annak megadásához, hogy a fájl nevének az "a" karakterrel kell kezdődnie, és a `*` helyettesítő karaktert használja helyőrzőként a fájlnév első betűje és a a **. txt** kiterjesztés.</span><span class="sxs-lookup"><span data-stu-id="b1df1-134">The previous command uses the range wildcard `[a-l]` to specify that the file name should begin with the characters "a" through "l" and uses the `*` wildcard character as a placeholder for any characters between the first letter of the filename and the **.txt** extension.</span></span>

<span data-ttu-id="b1df1-135">Az alábbi példa egy tartományhoz tartozó helyettesítő karaktert használ, amely kizárja a "d" betűt, de az "a" és az "f" közötti összes többi betűt is tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="b1df1-135">The following example uses a range wildcard pattern that excludes the letter "d" but includes all the other letters from "a" through "f."</span></span>

`Get-ChildItem c:\techdocs\[a-cef]\*.txt`

## <a name="handling-literal-characters-in-wildcard-patterns"></a><span data-ttu-id="b1df1-136">Literális karakterek használata helyettesítő karakteres mintákban</span><span class="sxs-lookup"><span data-stu-id="b1df1-136">Handling Literal Characters in Wildcard Patterns</span></span>

<span data-ttu-id="b1df1-137">Ha a megadott helyettesítő karakter olyan literál karaktereket tartalmaz, amelyek nem értelmezendő helyettesítő karakterként, használja a kezdő karaktert (`` ` ``) Escape-karakterként.</span><span class="sxs-lookup"><span data-stu-id="b1df1-137">If the wildcard pattern you specify contains literal characters that should not be interpretted as wildcard characters, use the backtick character (`` ` ``) as an escape character.</span></span> <span data-ttu-id="b1df1-138">Ha literál karaktereket ad meg a PowerShell API-val, egyetlen kezdő használjon.</span><span class="sxs-lookup"><span data-stu-id="b1df1-138">When you specify literal characters int the PowerShell API, use a single backtick.</span></span> <span data-ttu-id="b1df1-139">Ha literál karaktereket ad meg a PowerShell parancssorába, használjon két aposztrófokkal.</span><span class="sxs-lookup"><span data-stu-id="b1df1-139">When you specify literal characters at the PowerShell command prompt, use two backticks.</span></span>

<span data-ttu-id="b1df1-140">Az alábbi minta például két zárójelet tartalmaz, amelyeket szó szerint kell elvégeznie.</span><span class="sxs-lookup"><span data-stu-id="b1df1-140">For example, the following pattern contains two brackets that must be taken literally.</span></span>

<span data-ttu-id="b1df1-141">A PowerShell API használatakor használja a következőket:</span><span class="sxs-lookup"><span data-stu-id="b1df1-141">When used in the PowerShell API use:</span></span>

- <span data-ttu-id="b1df1-142">"John Smith \`[\*"] "</span><span class="sxs-lookup"><span data-stu-id="b1df1-142">"John Smith \`[\*\`]"</span></span>

<span data-ttu-id="b1df1-143">A PowerShell-parancssorból való használat esetén:</span><span class="sxs-lookup"><span data-stu-id="b1df1-143">When used from the PowerShell command prompt:</span></span>

- <span data-ttu-id="b1df1-144">"John Smith \` \`[\*\`"] "</span><span class="sxs-lookup"><span data-stu-id="b1df1-144">"John Smith \`\`[\*\`\`]"</span></span>

<span data-ttu-id="b1df1-145">Ez a minta a következőnek felel meg: "John Smith [marketing]" vagy "John Smith [Development]".</span><span class="sxs-lookup"><span data-stu-id="b1df1-145">This pattern matches "John Smith [Marketing]" or "John Smith [Development]".</span></span> <span data-ttu-id="b1df1-146">Például:</span><span class="sxs-lookup"><span data-stu-id="b1df1-146">For example:</span></span>

```
PS> "John Smith [Marketing]" -like "John Smith ``[*``]"
True

PS> "John Smith [Development]" -like "John Smith ``[*``]"
True
```

## <a name="cmdlet-output-and-wildcard-characters"></a><span data-ttu-id="b1df1-147">Parancsmag kimenete és helyettesítő karakterei</span><span class="sxs-lookup"><span data-stu-id="b1df1-147">Cmdlet Output and Wildcard Characters</span></span>

<span data-ttu-id="b1df1-148">Ha a parancsmag paraméterei helyettesítő karaktereket is támogatnak, a művelet általában egy tömb kimenetét állítja elő.</span><span class="sxs-lookup"><span data-stu-id="b1df1-148">When cmdlet parameters support wildcard characters, the operation usually generates an array output.</span></span>
<span data-ttu-id="b1df1-149">Alkalmanként a tömb kimenetét nem érdemes támogatni, mivel a felhasználó csak egyetlen elem használatát teszi lehetővé.</span><span class="sxs-lookup"><span data-stu-id="b1df1-149">Occasionally, it makes no sense to support an array output because the user might use only a single item.</span></span> <span data-ttu-id="b1df1-150">A `Set-Location` parancsmag például nem támogatja a tömb kimenetét, mert a felhasználó csak egyetlen helyet állít be.</span><span class="sxs-lookup"><span data-stu-id="b1df1-150">For example, the `Set-Location` cmdlet does not support array output because the user sets only a single location.</span></span> <span data-ttu-id="b1df1-151">Ebben az esetben a parancsmag továbbra is támogatja a helyettesítő karaktereket, de egyetlen helyre kényszeríti a feloldást.</span><span class="sxs-lookup"><span data-stu-id="b1df1-151">In this instance, the cmdlet still supports wildcard characters, but it forces resolution to a single location.</span></span>

## <a name="see-also"></a><span data-ttu-id="b1df1-152">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b1df1-152">See Also</span></span>

[<span data-ttu-id="b1df1-153">Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="b1df1-153">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)

[<span data-ttu-id="b1df1-154">WildcardPattern osztály</span><span class="sxs-lookup"><span data-stu-id="b1df1-154">WildcardPattern Class</span></span>](/dotnet/api/system.management.automation.wildcardpattern)
