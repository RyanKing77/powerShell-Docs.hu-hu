---
title: Tevékenység-paraméterek |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6e4e0cf6-19e0-44b8-8b40-d6f6075276cf
caps.latest.revision: 5
ms.openlocfilehash: 32e2b8acf33bc733c5e4cab94a721076ff46225d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849090"
---
# <a name="activity-parameters"></a><span data-ttu-id="8358e-102">Tevékenység-paraméterek</span><span class="sxs-lookup"><span data-stu-id="8358e-102">Activity Parameters</span></span>

<span data-ttu-id="8358e-103">A következő táblázat felsorolja a javasolt nevek és a funkciók a tevékenység-paraméterek.</span><span class="sxs-lookup"><span data-stu-id="8358e-103">The following table lists the recommended names and functionality for activity parameters.</span></span>

<span data-ttu-id="8358e-104">Hozzáfűzés adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-104">Append Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-105">Ez a paraméter valósítja meg, hogy a felhasználó hozzáadhat tartalmat erőforrás végére Ha paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-105">Implement this parameter so that the user can add content to the end of a resource when the parameter is specified.</span></span>

<span data-ttu-id="8358e-106">CaseSensitive adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-106">CaseSensitive Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-107">Végrehajtja ezt a paramétert, így a felhasználó megkövetelheti a kis-és nagybetűk, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-107">Implement this parameter so the user can require case sensitivity when the parameter is specified.</span></span>

<span data-ttu-id="8358e-108">A parancs adattípus: Sztring</span><span class="sxs-lookup"><span data-stu-id="8358e-108">Command Data type: String</span></span>

<span data-ttu-id="8358e-109">Végrehajtja ezt a paramétert, így a felhasználó is futtatása paranccsal karakterláncot kell megadni.</span><span class="sxs-lookup"><span data-stu-id="8358e-109">Implement this parameter so the user can specify a command string to run.</span></span>

<span data-ttu-id="8358e-110">CompatibleVersion adattípus: System.Version objektum</span><span class="sxs-lookup"><span data-stu-id="8358e-110">CompatibleVersion Data type: System.Version object</span></span>

<span data-ttu-id="8358e-111">Végrehajtja ezt a paramétert, így a felhasználó megadhatja a szemantika, amely a parancsmag korábbi verzióival való kompatibilitás érdekében kompatibilisnek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="8358e-111">Implement this parameter so the user can specify the semantics that the cmdlet must be compatible with for compatibility with previous versions.</span></span>

<span data-ttu-id="8358e-112">Tömörítés adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-112">Compress Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-113">Ez a paraméter valósítja meg, hogy az adatok tömörítésének használatos, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-113">Implement this parameter so that data compression is used when the parameter is specified.</span></span>

<span data-ttu-id="8358e-114">Tömörítés adattípus: Kulcsszó</span><span class="sxs-lookup"><span data-stu-id="8358e-114">Compress Data type: Keyword</span></span>

<span data-ttu-id="8358e-115">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a algoritmus használata az adatok tömörítés.</span><span class="sxs-lookup"><span data-stu-id="8358e-115">Implement this parameter so that the user can specify the algorithm to use for data compression.</span></span>

<span data-ttu-id="8358e-116">Folyamatos adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-116">Continuous Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-117">Ez a paraméter valósítja meg, hogy az adatok feldolgozása mindaddig, amíg a felhasználó leállítja a parancsmag, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-117">Implement this parameter so that data is processed until the user terminates the cmdlet when the parameter is specified.</span></span> <span data-ttu-id="8358e-118">Ha a paraméter nincs megadva, a parancsmag egy előre meghatározott mennyiségű adatot dolgoz fel, és ezután befejezi a műveletet.</span><span class="sxs-lookup"><span data-stu-id="8358e-118">If the parameter is not specified, the cmdlet processes a predefined amount of data and then terminates the operation.</span></span>

<span data-ttu-id="8358e-119">Hozzon létre adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-119">Create Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-120">Ez a paraméter jelzi, hogy egy erőforrás létrejött-e, ha egy még nem létezik a paraméter megadásakor megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="8358e-120">Implement this parameter to indicate that a resource is created if one does not already exist when the parameter is specified.</span></span>

<span data-ttu-id="8358e-121">Törölje az adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-121">Delete Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-122">Ez a paraméter valósítja meg, hogy az erőforrások törlődnek, amikor a parancsmag befejezte a műveletet, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-122">Implement this parameter so that resources are deleted when the cmdlet has completed its operation when the parameter is specified.</span></span>

<span data-ttu-id="8358e-123">Kiürítési adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-123">Drain Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-124">Ez a paraméter jelzi, hogy szálankénti függőben lévő munkaelemek feldolgozása előtt a parancsmag új adatokat dolgoz fel, ha a paraméter meg van adva megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="8358e-124">Implement this parameter to indicate that outstanding work items are processed before the cmdlet processes new data when the parameter is specified.</span></span> <span data-ttu-id="8358e-125">Ha a paraméter nincs megadva, a munkaelemek feldolgozása azonnal megtörténik.</span><span class="sxs-lookup"><span data-stu-id="8358e-125">If the parameter is not specified, the work items are processed immediately.</span></span>

<span data-ttu-id="8358e-126">Adattípus törlése: Int32</span><span class="sxs-lookup"><span data-stu-id="8358e-126">Erase Data type: Int32</span></span>

<span data-ttu-id="8358e-127">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja, hogy hányszor erőforrás törölve lesz, mielőtt törölnénk őket.</span><span class="sxs-lookup"><span data-stu-id="8358e-127">Implement this parameter so that the user can specify the number of times a resource is erased before it is deleted.</span></span>

<span data-ttu-id="8358e-128">ErrorLevel adattípus: Int32</span><span class="sxs-lookup"><span data-stu-id="8358e-128">ErrorLevel Data type: Int32</span></span>

<span data-ttu-id="8358e-129">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a jelentés hibák szintjét.</span><span class="sxs-lookup"><span data-stu-id="8358e-129">Implement this parameter so that the user can specify the level of errors to report.</span></span>

<span data-ttu-id="8358e-130">Adattípus kizárása: String]</span><span class="sxs-lookup"><span data-stu-id="8358e-130">Exclude Data type: String[]</span></span>

<span data-ttu-id="8358e-131">Ez a paraméter valósítja meg, hogy a felhasználó lehet kizárni valami tevékenység.</span><span class="sxs-lookup"><span data-stu-id="8358e-131">Implement this parameter so that the user can exclude something from an activity.</span></span> <span data-ttu-id="8358e-132">A bemeneti szűrők használatával kapcsolatos további információkért lásd: [bemeneti Szűrőparaméterrel](./input-filter-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="8358e-132">For more information about how to use input filters, see [Input Filter Parameters](./input-filter-parameters.md).</span></span>

<span data-ttu-id="8358e-133">Szűrés adattípus: Kulcsszó</span><span class="sxs-lookup"><span data-stu-id="8358e-133">Filter Data type: Keyword</span></span>

<span data-ttu-id="8358e-134">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja egy szűrőt, amely az erőforrásokat, amelyen a parancsmag a művelet végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="8358e-134">Implement this parameter so that the user can specify a filter that selects the resources upon which to perform the cmdlet action.</span></span> <span data-ttu-id="8358e-135">A bemeneti szűrők használatával kapcsolatos további információkért lásd: [bemeneti Szűrőparaméterrel](./input-filter-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="8358e-135">For more information about how to use input filters, see [Input Filter Parameters](./input-filter-parameters.md).</span></span>

<span data-ttu-id="8358e-136">Hajtsa végre az adatok típusa: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-136">Follow Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-137">Ez a paraméter valósítja meg, hogy a folyamat nyomon követi, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-137">Implement this parameter so that progress is tracked when the parameter is specified.</span></span>

<span data-ttu-id="8358e-138">Kényszerített adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-138">Force Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-139">Ez a paraméter jelzi, hogy a felhasználó egy művelet hajtható végre, akkor is, ha korlátozások vannak észlelt, amikor a paraméter meg van adva megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="8358e-139">Implement this parameter to indicate that the user can perform an action even if restrictions are encountered when the parameter is specified.</span></span> <span data-ttu-id="8358e-140">A paraméter nem engedélyezi a biztonsági legyen feltörni.</span><span class="sxs-lookup"><span data-stu-id="8358e-140">The parameter does not allow security to be compromised.</span></span> <span data-ttu-id="8358e-141">Például ez a paraméter lehetővé teszi, hogy egy felhasználó egy csak olvasható fájl felülírása.</span><span class="sxs-lookup"><span data-stu-id="8358e-141">For example, this parameter lets a user overwrite a read-only file.</span></span>

<span data-ttu-id="8358e-142">Adatok típusa a következők: String]</span><span class="sxs-lookup"><span data-stu-id="8358e-142">Include Data type: String[]</span></span>

<span data-ttu-id="8358e-143">Ez a paraméter valósítja meg, hogy a felhasználó belefoglalhatja a hiba egy tevékenységet.</span><span class="sxs-lookup"><span data-stu-id="8358e-143">Implement this parameter so that the user can include something in an activity.</span></span> <span data-ttu-id="8358e-144">A bemeneti szűrők használatával kapcsolatos további információkért lásd: [bemeneti Szűrőparaméterrel](./input-filter-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="8358e-144">For more information about how to use input filters, see [Input Filter Parameters](./input-filter-parameters.md).</span></span>

<span data-ttu-id="8358e-145">A növekményes adatok típusa: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-145">Incremental Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-146">Ez a paraméter jelzi, hogy a feldolgozás történik növekményes paraméter megadásakor megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="8358e-146">Implement this parameter to indicate that processing is performed incrementally when the parameter is specified.</span></span> <span data-ttu-id="8358e-147">Például ez a paraméter lehetővé teszi, hogy a felhasználók, fájlok biztonsági mentése a legutóbbi biztonsági mentés óta csak növekményes biztonsági mentések végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="8358e-147">For example, this parameter lets a user perform incremental backups that back up files only since the last backup.</span></span>

<span data-ttu-id="8358e-148">InputObject adattípus: Objektum</span><span class="sxs-lookup"><span data-stu-id="8358e-148">InputObject Data type: Object</span></span>

<span data-ttu-id="8358e-149">A parancsmag bemenete más parancsmagoknak a megvalósítási ezt a paramétert.</span><span class="sxs-lookup"><span data-stu-id="8358e-149">Implement this parameter when the cmdlet takes input from other cmdlets.</span></span> <span data-ttu-id="8358e-150">Amikor határoz meg egy `InputObject` paramétert, mindig adja meg a `ValueFromPipeline` deklarálásakor kulcsszó a **paraméter** attribútum.</span><span class="sxs-lookup"><span data-stu-id="8358e-150">When you define an `InputObject` parameter, always specify the `ValueFromPipeline` keyword when you declare the **Parameter** attribute.</span></span> <span data-ttu-id="8358e-151">A bemeneti szűrők használatával kapcsolatos további információkért lásd: [bemeneti Szűrőparaméterrel](./input-filter-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="8358e-151">For more information about using input filters, see [Input Filter Parameters](./input-filter-parameters.md).</span></span>

<span data-ttu-id="8358e-152">Illessze be az adat típusa: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-152">Insert Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-153">Ez a paraméter valósítja meg, hogy a parancsmag egy elemet szúr be, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-153">Implement this parameter so that the cmdlet inserts an item when the parameter is specified.</span></span>

<span data-ttu-id="8358e-154">Interaktív adatok típusa: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-154">Interactive Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-155">Ez a paraméter valósítja meg, hogy a parancsmag működését interaktív módon a felhasználóval, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-155">Implement this parameter so that the cmdlet works interactively with the user when the parameter is specified.</span></span>

<span data-ttu-id="8358e-156">Intervallum adattípus: Kivonattábla</span><span class="sxs-lookup"><span data-stu-id="8358e-156">Interval Data type: HashTable</span></span>

<span data-ttu-id="8358e-157">Ez a paraméter valósítja meg, hogy a felhasználó úgy adhat meg a kulcsszavak egy kivonattábla, amely tartalmazza az értékeket.</span><span class="sxs-lookup"><span data-stu-id="8358e-157">Implement this parameter so that the user can specify a hash table of keywords that contains the values.</span></span> <span data-ttu-id="8358e-158">Az alábbi példa bemutatja mintaértékek a `Interval` paraméter: `-interval @{ResumeScan=15; Retry=3}`.</span><span class="sxs-lookup"><span data-stu-id="8358e-158">The following example shows sample values for the `Interval` parameter: `-interval @{ResumeScan=15; Retry=3}`.</span></span>

<span data-ttu-id="8358e-159">Jelentkezzen be az adat típusa: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-159">Log Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-160">Megvalósítási Ez a paraméter naplózási műveletek a parancsmag a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-160">Implement this parameter audit the actions of the cmdlet when the parameter is specified.</span></span>

<span data-ttu-id="8358e-161">NoClobber adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-161">NoClobber Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-162">Ez a paraméter valósítja meg, hogy az erőforrás nem írható felül, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-162">Implement this parameter so that the resource will not be overwritten when the parameter is specified.</span></span> <span data-ttu-id="8358e-163">Ez a paraméter általában parancsmagok, amelyek felülírják a meglévő objektumok ugyanazzal a névvel megelőzhető, hogy új objektumok létrehozására vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="8358e-163">This parameter generally applies to cmdlets that create new objects so that they can be prevented from overwriting existing objects with the same name.</span></span>

<span data-ttu-id="8358e-164">Értesítés adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-164">Notify Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-165">Ez a paraméter valósítja meg, hogy a felhasználó értesítést kap, hogy a tevékenység befejeződött, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-165">Implement this parameter so that the user will be notified that the activity is complete when the parameter is specified.</span></span>

<span data-ttu-id="8358e-166">NotifyAddress adattípus: E-mail cím</span><span class="sxs-lookup"><span data-stu-id="8358e-166">NotifyAddress Data type: E-mail address</span></span>

<span data-ttu-id="8358e-167">Végrehajtja ezt a paramétert, hogy a felhasználó megadhatja azt az e-mail címet, egy értesítés küldéséhez során a `Notify` paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-167">Implement this parameter so that the user can specify the e-mail address to use to send a notification when the `Notify` parameter is specified.</span></span>

<span data-ttu-id="8358e-168">Felülírás adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-168">Overwrite Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-169">Ez a paraméter valósítja meg, hogy a parancsmag felülírja a meglévő adatokat, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-169">Implement this parameter so that the cmdlet overwrites any existing data when the parameter is specified.</span></span>

<span data-ttu-id="8358e-170">Rákérdezés adattípus: Sztring</span><span class="sxs-lookup"><span data-stu-id="8358e-170">Prompt Data type: String</span></span>

<span data-ttu-id="8358e-171">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a parancsmag egy parancssort.</span><span class="sxs-lookup"><span data-stu-id="8358e-171">Implement this parameter so that the user can specify a prompt for the cmdlet.</span></span>

<span data-ttu-id="8358e-172">Csendes adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-172">Quiet Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-173">Ez a paraméter valósítja meg, hogy a parancsmag a műveletek során elrejti felhasználói visszajelzéseket, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-173">Implement this parameter so that the cmdlet suppresses user feedback during its actions when the parameter is specified.</span></span>

<span data-ttu-id="8358e-174">Recurse adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-174">Recurse Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-175">Ez a paraméter valósítja meg, hogy a parancsmag rekurzív módon annak műveleteket erőforrásokon hajtja végre, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-175">Implement this parameter so that the cmdlet recursively performs its actions on resources when the parameter is specified.</span></span>

<span data-ttu-id="8358e-176">Írja be a javítási adatok: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-176">Repair Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-177">Ez a paraméter valósítja meg, hogy a parancsmag javítása valamit a hibás állapotból, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-177">Implement this parameter so that the cmdlet will attempt to correct something from a broken state when the parameter is specified.</span></span>

<span data-ttu-id="8358e-178">RepairString adattípus: Sztring</span><span class="sxs-lookup"><span data-stu-id="8358e-178">RepairString Data type: String</span></span>

<span data-ttu-id="8358e-179">Végrehajtja ezt a paramétert, hogy a felhasználó megadhatja egy karakterláncot szeretne használni, amikor a `Repair` paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-179">Implement this parameter so that the user can specify a string to use when the `Repair` parameter is specified.</span></span>

<span data-ttu-id="8358e-180">Ismételje meg az adattípus: Int32</span><span class="sxs-lookup"><span data-stu-id="8358e-180">Retry Data type: Int32</span></span>

<span data-ttu-id="8358e-181">Végrehajtja ezt a paramétert, így a felhasználó megadhatja a parancsmag megkísérli a művelet hányszor.</span><span class="sxs-lookup"><span data-stu-id="8358e-181">Implement this parameter so the user can specify the number of times the cmdlet will attempt an action.</span></span>

<span data-ttu-id="8358e-182">Adatok típusának kiválasztása: Kulcsszó tömb</span><span class="sxs-lookup"><span data-stu-id="8358e-182">Select Data type: Keyword array</span></span>

<span data-ttu-id="8358e-183">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja, milyen típusú elemek tömbjét.</span><span class="sxs-lookup"><span data-stu-id="8358e-183">Implement this parameter so that the user can specify an array of the types of items.</span></span>

<span data-ttu-id="8358e-184">Stream-adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-184">Stream Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-185">Végrehajtja ezt a paramétert, így a felhasználó streamelheti a folyamat több kimeneti objektumok, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-185">Implement this parameter so the user can stream multiple output objects through the pipeline when the parameter is specified.</span></span>

<span data-ttu-id="8358e-186">A szigorú adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-186">Strict Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-187">Ez a paraméter valósítja meg, hogy az összes hiba kezelésének megszakító hibaként, amikor a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-187">Implement this parameter so that all errors are handled as terminating errors when the parameter is specified.</span></span>

<span data-ttu-id="8358e-188">TempLocation adattípus: Sztring</span><span class="sxs-lookup"><span data-stu-id="8358e-188">TempLocation Data type: String</span></span>

<span data-ttu-id="8358e-189">Hajtja végre ezt a paramétert, így a felhasználó megadhatja a parancsmag a művelet során használt ideiglenes adatokat helyét.</span><span class="sxs-lookup"><span data-stu-id="8358e-189">Implement this parameter so the user can specify the location of temporary data that is used during the operation of the cmdlet.</span></span>

<span data-ttu-id="8358e-190">Időtúllépés adattípus: Int32</span><span class="sxs-lookup"><span data-stu-id="8358e-190">Timeout Data type: Int32</span></span>

<span data-ttu-id="8358e-191">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja az időtúllépési időköz (ezredmásodpercben).</span><span class="sxs-lookup"><span data-stu-id="8358e-191">Implement this parameter so that the user can specify the timeout interval (in milliseconds).</span></span>

<span data-ttu-id="8358e-192">TRUNCATE adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-192">Truncate Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-193">Ez a paraméter valósítja meg, hogy a parancsmag csonkolja a műveleteket, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-193">Implement this parameter so that the cmdlet will truncate its actions when the parameter is specified.</span></span> <span data-ttu-id="8358e-194">Ha a paraméter nincs megadva, a parancsmag egy másik műveletet hajt végre.</span><span class="sxs-lookup"><span data-stu-id="8358e-194">If the parameter is not specified, the cmdlet performs another action.</span></span>

<span data-ttu-id="8358e-195">Ellenőrizze az adatok típusát: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-195">Verify Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-196">Ez a paraméter valósítja meg, hogy a parancsmag tesztelni fogja meghatározni, hogy művelet történt-e, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-196">Implement this parameter so that the cmdlet will test to determine whether an action has occurred when the parameter is specified.</span></span>

<span data-ttu-id="8358e-197">Várjon, adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="8358e-197">Wait Data type: SwitchParameter</span></span>

<span data-ttu-id="8358e-198">Ez a paraméter valósítja meg, hogy a parancsmag várakozik a felhasználói bevitelhez, ha a paraméter meg van adva a folytatás előtt.</span><span class="sxs-lookup"><span data-stu-id="8358e-198">Implement this parameter so that the cmdlet will wait for user input before continuing when the parameter is specified.</span></span>

<span data-ttu-id="8358e-199">Várakozási idő adattípus: Int32</span><span class="sxs-lookup"><span data-stu-id="8358e-199">WaitTime Data type: Int32</span></span>

<span data-ttu-id="8358e-200">Végrehajtja ezt a paramétert, hogy a felhasználó megadhatja a időtartama (másodpercben), hogy a felhasználó várakozik a parancsmag bemeneti mikor a `Wait` paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="8358e-200">Implement this parameter so that the user can specify the duration (in seconds) that the cmdlet will wait for user input when the `Wait` parameter is specified.</span></span>

## <a name="see-also"></a><span data-ttu-id="8358e-201">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="8358e-201">See Also</span></span>

[<span data-ttu-id="8358e-202">Parancsmag-paraméterek</span><span class="sxs-lookup"><span data-stu-id="8358e-202">Cmdlet Parameters</span></span>](./cmdlet-parameters.md)

[<span data-ttu-id="8358e-203">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="8358e-203">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)

[<span data-ttu-id="8358e-204">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="8358e-204">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
