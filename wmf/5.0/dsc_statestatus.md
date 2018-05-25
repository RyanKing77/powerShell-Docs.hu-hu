---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 7b4e4dbeaf9c3c48e7b2dfc74435dfa2cd9c7ea7
ms.sourcegitcommit: 735ccab3fb3834ccd8559fab6700b798e8e5ffbf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/25/2018
---
# <a name="unified-and-consistent-state-and-status-representation"></a><span data-ttu-id="a289c-102">Egyesített és konzisztens állapotreprezentáció</span><span class="sxs-lookup"><span data-stu-id="a289c-102">Unified and Consistent State and Status Representation</span></span>

<span data-ttu-id="a289c-103">Fejlesztésen végzett ebben a kiadásban a beépített LCM állapotát és DSC állapot automatizálása.</span><span class="sxs-lookup"><span data-stu-id="a289c-103">A series of enhancements have been made in this release for automations built LCM state and DSC status.</span></span> <span data-ttu-id="a289c-104">Ezek közé tartozik a egyesített és konzisztens állapotban és állapot formátumban, az állapot objektumok kezelhető dátum/idő tulajdonság Get-DscConfigurationStatus parancsmag által visszaadott és fokozott LCM állapot részletei tulajdonság Get-DscLocalConfigurationManager által visszaadott parancsmag.</span><span class="sxs-lookup"><span data-stu-id="a289c-104">These include unified and consistent state and status representations, manageable datetime property of status objects returned by Get-DscConfigurationStatus cmdlet and enhanced LCM state details property returned by Get-DscLocalConfigurationManager cmdlet.</span></span>

<span data-ttu-id="a289c-105">LCM állapot és a DSC műveleti állapotának ábrázolása javított változat, és a következő szabályok szerint egyesített:</span><span class="sxs-lookup"><span data-stu-id="a289c-105">The representation of LCM state and DSC operation status are revisited and unified according to following rules:</span></span>
1.  <span data-ttu-id="a289c-106">Notprocessed erőforrás nem befolyásolja a LCM állapotot és a DSC-állapota.</span><span class="sxs-lookup"><span data-stu-id="a289c-106">Notprocessed resource does not impact LCM state and DSC status.</span></span>
2.  <span data-ttu-id="a289c-107">További erőforrások feldolgozásának, miután újraindítást kérő erőforrás ütközik LCM leállítása.</span><span class="sxs-lookup"><span data-stu-id="a289c-107">LCM stop processing further resources once it encounters a resource that requests reboot.</span></span>
3.  <span data-ttu-id="a289c-108">Egy erőforrás újraindítást kérő nincs megfelelő állapotban amíg újraindítást ténylegesen történik.</span><span class="sxs-lookup"><span data-stu-id="a289c-108">A resource that requests reboot is not in desired state until reboot actually happens.</span></span>
4.  <span data-ttu-id="a289c-109">Amikor egy erőforrást, amely nem sikerül, LCM tartja a feldolgozás után további erőforrások mindaddig, amíg azok nem függ a hiba egyik.</span><span class="sxs-lookup"><span data-stu-id="a289c-109">After encountering a resource that fails, LCM keeps processing further resources as long as they are not dependent on the failure one.</span></span>
5.  <span data-ttu-id="a289c-110">A Get-DscConfigurationStatus parancsmag által visszaadott összesített állapotát az összes erőforrás állapotának super összessége.</span><span class="sxs-lookup"><span data-stu-id="a289c-110">The overall status returned by Get-DscConfigurationStatus cmdlet is the super set of all resources' status.</span></span>
6.  <span data-ttu-id="a289c-111">A PendingReboot állapota felülbírálja a PendingConfiguration állapotát.</span><span class="sxs-lookup"><span data-stu-id="a289c-111">The PendingReboot state is a superset of PendingConfiguration state.</span></span>

<span data-ttu-id="a289c-112">Az alábbi táblázat szemlélteti a eredő állapot kapcsolódó tulajdonságok néhány jellemző forgatókönyvek alapján.</span><span class="sxs-lookup"><span data-stu-id="a289c-112">The table below illustrates the resultant state and status related properties under a few typical scenarios.</span></span>

| <span data-ttu-id="a289c-113">Forgatókönyv</span><span class="sxs-lookup"><span data-stu-id="a289c-113">Scenario</span></span>                    | <span data-ttu-id="a289c-114">LCMState</span><span class="sxs-lookup"><span data-stu-id="a289c-114">LCMState</span></span>       | <span data-ttu-id="a289c-115">Állapot</span><span class="sxs-lookup"><span data-stu-id="a289c-115">Status</span></span> | <span data-ttu-id="a289c-116">A kért újraindítás</span><span class="sxs-lookup"><span data-stu-id="a289c-116">Reboot Requested</span></span>  | <span data-ttu-id="a289c-117">ResourcesInDesiredState</span><span class="sxs-lookup"><span data-stu-id="a289c-117">ResourcesInDesiredState</span></span>  | <span data-ttu-id="a289c-118">ResourcesNotInDesiredState</span><span class="sxs-lookup"><span data-stu-id="a289c-118">ResourcesNotInDesiredState</span></span> |
|---------------------------------|----------------------|------------|---------------|------------------------------|--------------------------------|
| <span data-ttu-id="a289c-119">S**^**</span><span class="sxs-lookup"><span data-stu-id="a289c-119">S**^**</span></span>                          | <span data-ttu-id="a289c-120">Üresjárati</span><span class="sxs-lookup"><span data-stu-id="a289c-120">Idle</span></span>                 | <span data-ttu-id="a289c-121">Siker</span><span class="sxs-lookup"><span data-stu-id="a289c-121">Success</span></span>    | <span data-ttu-id="a289c-122">$false</span><span class="sxs-lookup"><span data-stu-id="a289c-122">$false</span></span>        | <span data-ttu-id="a289c-123">S</span><span class="sxs-lookup"><span data-stu-id="a289c-123">S</span></span>                            | <span data-ttu-id="a289c-124">$null</span><span class="sxs-lookup"><span data-stu-id="a289c-124">$null</span></span>                          |
| <span data-ttu-id="a289c-125">F**^**</span><span class="sxs-lookup"><span data-stu-id="a289c-125">F**^**</span></span>                          | <span data-ttu-id="a289c-126">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="a289c-126">PendingConfiguration</span></span> | <span data-ttu-id="a289c-127">Hiba</span><span class="sxs-lookup"><span data-stu-id="a289c-127">Failure</span></span>    | <span data-ttu-id="a289c-128">$false</span><span class="sxs-lookup"><span data-stu-id="a289c-128">$false</span></span>        | <span data-ttu-id="a289c-129">$null</span><span class="sxs-lookup"><span data-stu-id="a289c-129">$null</span></span>                        | <span data-ttu-id="a289c-130">F</span><span class="sxs-lookup"><span data-stu-id="a289c-130">F</span></span>                              |
| <span data-ttu-id="a289c-131">S, F</span><span class="sxs-lookup"><span data-stu-id="a289c-131">S,F</span></span>                             | <span data-ttu-id="a289c-132">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="a289c-132">PendingConfiguration</span></span> | <span data-ttu-id="a289c-133">Hiba</span><span class="sxs-lookup"><span data-stu-id="a289c-133">Failure</span></span>    | <span data-ttu-id="a289c-134">$false</span><span class="sxs-lookup"><span data-stu-id="a289c-134">$false</span></span>        | <span data-ttu-id="a289c-135">S</span><span class="sxs-lookup"><span data-stu-id="a289c-135">S</span></span>                            | <span data-ttu-id="a289c-136">F</span><span class="sxs-lookup"><span data-stu-id="a289c-136">F</span></span>                              |
| <span data-ttu-id="a289c-137">F,S</span><span class="sxs-lookup"><span data-stu-id="a289c-137">F,S</span></span>                             | <span data-ttu-id="a289c-138">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="a289c-138">PendingConfiguration</span></span> | <span data-ttu-id="a289c-139">Hiba</span><span class="sxs-lookup"><span data-stu-id="a289c-139">Failure</span></span>    | <span data-ttu-id="a289c-140">$false</span><span class="sxs-lookup"><span data-stu-id="a289c-140">$false</span></span>        | <span data-ttu-id="a289c-141">S</span><span class="sxs-lookup"><span data-stu-id="a289c-141">S</span></span>                            | <span data-ttu-id="a289c-142">F</span><span class="sxs-lookup"><span data-stu-id="a289c-142">F</span></span>                              |
| <span data-ttu-id="a289c-143">S<sub>1</sub>, F, S<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="a289c-143">S<sub>1</sub>, F, S<sub>2</sub></span></span> | <span data-ttu-id="a289c-144">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="a289c-144">PendingConfiguration</span></span> | <span data-ttu-id="a289c-145">Hiba</span><span class="sxs-lookup"><span data-stu-id="a289c-145">Failure</span></span>    | <span data-ttu-id="a289c-146">$false</span><span class="sxs-lookup"><span data-stu-id="a289c-146">$false</span></span>        | <span data-ttu-id="a289c-147">S<sub>1</sub>, S<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="a289c-147">S<sub>1</sub>, S<sub>2</sub></span></span> | <span data-ttu-id="a289c-148">F</span><span class="sxs-lookup"><span data-stu-id="a289c-148">F</span></span>                              |
| <span data-ttu-id="a289c-149">F<sub>1</sub>, S, F<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="a289c-149">F<sub>1</sub>, S, F<sub>2</sub></span></span> | <span data-ttu-id="a289c-150">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="a289c-150">PendingConfiguration</span></span> | <span data-ttu-id="a289c-151">Hiba</span><span class="sxs-lookup"><span data-stu-id="a289c-151">Failure</span></span>    | <span data-ttu-id="a289c-152">$false</span><span class="sxs-lookup"><span data-stu-id="a289c-152">$false</span></span>        | <span data-ttu-id="a289c-153">S</span><span class="sxs-lookup"><span data-stu-id="a289c-153">S</span></span>                            | <span data-ttu-id="a289c-154">F<sub>1</sub>, F<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="a289c-154">F<sub>1</sub>, F<sub>2</sub></span></span>   |
| <span data-ttu-id="a289c-155">S, r</span><span class="sxs-lookup"><span data-stu-id="a289c-155">S, r</span></span>                            | <span data-ttu-id="a289c-156">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="a289c-156">PendingReboot</span></span>        | <span data-ttu-id="a289c-157">Siker</span><span class="sxs-lookup"><span data-stu-id="a289c-157">Success</span></span>    | <span data-ttu-id="a289c-158">$true</span><span class="sxs-lookup"><span data-stu-id="a289c-158">$true</span></span>         | <span data-ttu-id="a289c-159">S</span><span class="sxs-lookup"><span data-stu-id="a289c-159">S</span></span>                            | <span data-ttu-id="a289c-160">r</span><span class="sxs-lookup"><span data-stu-id="a289c-160">r</span></span>                              |
| <span data-ttu-id="a289c-161">F, r</span><span class="sxs-lookup"><span data-stu-id="a289c-161">F, r</span></span>                            | <span data-ttu-id="a289c-162">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="a289c-162">PendingReboot</span></span>        | <span data-ttu-id="a289c-163">Hiba</span><span class="sxs-lookup"><span data-stu-id="a289c-163">Failure</span></span>    | <span data-ttu-id="a289c-164">$true</span><span class="sxs-lookup"><span data-stu-id="a289c-164">$true</span></span>         | <span data-ttu-id="a289c-165">$null</span><span class="sxs-lookup"><span data-stu-id="a289c-165">$null</span></span>                        | <span data-ttu-id="a289c-166">F, r</span><span class="sxs-lookup"><span data-stu-id="a289c-166">F, r</span></span>                           |
| <span data-ttu-id="a289c-167">r, S</span><span class="sxs-lookup"><span data-stu-id="a289c-167">r, S</span></span>                            | <span data-ttu-id="a289c-168">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="a289c-168">PendingReboot</span></span>        | <span data-ttu-id="a289c-169">Siker</span><span class="sxs-lookup"><span data-stu-id="a289c-169">Success</span></span>    | <span data-ttu-id="a289c-170">$true</span><span class="sxs-lookup"><span data-stu-id="a289c-170">$true</span></span>         | <span data-ttu-id="a289c-171">$null</span><span class="sxs-lookup"><span data-stu-id="a289c-171">$null</span></span>                        | <span data-ttu-id="a289c-172">r</span><span class="sxs-lookup"><span data-stu-id="a289c-172">r</span></span>                              |
| <span data-ttu-id="a289c-173">r, F</span><span class="sxs-lookup"><span data-stu-id="a289c-173">r, F</span></span>                            | <span data-ttu-id="a289c-174">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="a289c-174">PendingReboot</span></span>        | <span data-ttu-id="a289c-175">Siker</span><span class="sxs-lookup"><span data-stu-id="a289c-175">Success</span></span>    | <span data-ttu-id="a289c-176">$true</span><span class="sxs-lookup"><span data-stu-id="a289c-176">$true</span></span>         | <span data-ttu-id="a289c-177">$null</span><span class="sxs-lookup"><span data-stu-id="a289c-177">$null</span></span>                        | <span data-ttu-id="a289c-178">r</span><span class="sxs-lookup"><span data-stu-id="a289c-178">r</span></span>                              |

<span data-ttu-id="a289c-179">^ S<sub>i</sub>: erőforrásokat, a rendszer sikeresen alkalmazta F sorozata<sub>i</sub>: a rendszer újraindítását igénylő r: A erőforrás sikertelenül telepített erőforrások több \*</span><span class="sxs-lookup"><span data-stu-id="a289c-179">^ S<sub>i</sub>: A series of resources that applied successfully F<sub>i</sub>: A series of resources that applied unsuccessfully r: A resource that requires reboot \*</span></span>

```powershell
$LCMState = (Get-DscLocalConfigurationManager).LCMState
$Status = (Get-DscConfigurationStatus).Status

$RebootRequested = (Get-DscConfigurationStatus).RebootRequested

$ResourcesInDesiredState = (Get-DscConfigurationStatus).ResourcesInDesiredState

$ResourcesNotInDesiredState = (Get-DscConfigurationStatus).ResourcesNotInDesiredState
```

## <a name="enhancement-in-get-dscconfigurationstatus-cmdlet"></a><span data-ttu-id="a289c-180">A Get-DscConfigurationStatus parancsmag továbbfejlesztése</span><span class="sxs-lookup"><span data-stu-id="a289c-180">Enhancement in Get-DscConfigurationStatus cmdlet</span></span>

<span data-ttu-id="a289c-181">Ebben a kiadásban a Get-DscConfigurationStatus parancsmagnak néhány kiegészítésre került sor.</span><span class="sxs-lookup"><span data-stu-id="a289c-181">A few enhancements have been made to Get-DscConfigurationStatus cmdlet in this release.</span></span> <span data-ttu-id="a289c-182">Korábban a Kezdődátum a parancsmag által visszaadott objektumok tulajdonsága karakterlánc típusú.</span><span class="sxs-lookup"><span data-stu-id="a289c-182">Previously, the StartDate property of objects returned by the cmdlet is of String type.</span></span> <span data-ttu-id="a289c-183">Most már dátum/idő típusú, amely lehetővé teszi összetett, válassza ki, majd a szűrési beállítások könnyebb a belső tulajdonságok egy DateTime típusú objektum.</span><span class="sxs-lookup"><span data-stu-id="a289c-183">Now, it is of Datetime type, which enables complex selecting and filtering easier based on the intrinsic properties of a Datetime object.</span></span>

```powershell
(Get-DscConfigurationStatus).StartDate | fl *
DateTime : Friday, November 13, 2015 1:39:44 PM
Date : 11/13/2015 12:00:00 AM
Day : 13
DayOfWeek : Friday
DayOfYear : 317
Hour : 13
Kind : Local
Millisecond : 886
Minute : 39
Month : 11
Second : 44
Ticks : 635830187848860000
TimeOfDay : 13:39:44.8860000
Year : 2015
```

<span data-ttu-id="a289c-184">Az alábbiakban látható egy példa, amely ugyanarra a napra esnek ennek ma hét történt a DSC-művelet az összes rekord visszaadása.</span><span class="sxs-lookup"><span data-stu-id="a289c-184">Following is an example that returns all DSC operation records happened on the same day of week as today.</span></span>

```powershell
(Get-DscConfigurationStatus –All) | where { $_.startdate.dayofweek -eq (Get-Date).DayOfWeek }
```

<span data-ttu-id="a289c-185">Ne módosítsa a csomópont konfigurációs (vagyis olvasási csak műveletek) műveletkészlet rekordok szűrni.</span><span class="sxs-lookup"><span data-stu-id="a289c-185">Records of operations that do not make changes to node’s configuration (i.e. read only operations) are eliminated.</span></span> <span data-ttu-id="a289c-186">Ezért teszt-DscConfiguration, Get-DscConfiguration műveletek vannak már nem tiltott a Get-DscConfigurationStatus parancsmag objektumot sem adott vissza.</span><span class="sxs-lookup"><span data-stu-id="a289c-186">Therefore, Test-DscConfiguration, Get-DscConfiguration operations are no longer adulterated in returned objects from Get-DscConfigurationStatus cmdlet.</span></span>
<span data-ttu-id="a289c-187">Meta konfigurációs beállítás művelet rögzíti a Get-DscConfigurationStatus parancsmag visszatérési kerül.</span><span class="sxs-lookup"><span data-stu-id="a289c-187">Records of meta configuration setting operation is added to the return of Get-DscConfigurationStatus cmdlet.</span></span>

<span data-ttu-id="a289c-188">Az alábbiakban látható egy példa a Get-DscConfigurationStatus visszaadott eredmény – az összes parancsmag.</span><span class="sxs-lookup"><span data-stu-id="a289c-188">Following is an example of result returned from Get-DscConfigurationStatus –All cmdlet.</span></span>

```powershell
All configuration operations:

Status StartDate Type RebootRequested
------ --------- ---- ---------------
Success 11/13/2015 11:38:16 AM Consistency False
Success 11/13/2015 11:23:16 AM Reboot False
Success 11/13/2015 11:21:43 AM Reboot True
Success 11/13/2015 11:20:44 AM Initial True
Success 11/13/2015 11:20:44 AM LocalConfigurationManager False
```

## <a name="enhancement-in-get-dsclocalconfigurationmanager-cmdlet"></a><span data-ttu-id="a289c-189">A Get-DscLocalConfigurationManager parancsmag továbbfejlesztése</span><span class="sxs-lookup"><span data-stu-id="a289c-189">Enhancement in Get-DscLocalConfigurationManager cmdlet</span></span>

<span data-ttu-id="a289c-190">Egy új mezőt a LCMStateDetail hozzáadódik a Get-DscLocalConfigurationManager parancsmag által visszaadott objektum.</span><span class="sxs-lookup"><span data-stu-id="a289c-190">A new field of LCMStateDetail is added to the object returned from Get-DscLocalConfigurationManager cmdlet.</span></span> <span data-ttu-id="a289c-191">Ebben a mezőben van feltöltve, ha LCMState "Foglalt".</span><span class="sxs-lookup"><span data-stu-id="a289c-191">This field is populated when LCMState is "Busy".</span></span> <span data-ttu-id="a289c-192">Lekérhető által a következő parancsmagot:</span><span class="sxs-lookup"><span data-stu-id="a289c-192">It can be retrieved by following cmdlet:</span></span>

```powershell
(Get-DscLocalConfigurationManager).LCMStateDetail
```

<span data-ttu-id="a289c-193">Az alábbiakban látható egy példa a kimenetre végzett folyamatos figyelés a olyan konfigurációt, amely a távoli csomóponton levő két újraindításra van szükség.</span><span class="sxs-lookup"><span data-stu-id="a289c-193">Following is an example output of a continuous monitoring on a configuration that requires two reboots on a remote node.</span></span>

```powershell
Start a configuration that requires two reboots

Monitor LCM State:
LCM State: Busy, LCM is applying a new configuration.
LCM State: PendingReboot,
Machine is rebooting...
LCM State: Busy, LCM is continuing applying configuration after last reboot.
LCM State: PendingReboot,
Machine is rebooting...
LCM State: Busy, LCM is continuing applying configuration after last reboot.
LCM State: Idle,
LCM State: Busy, LCM is performing a consistency check.
LCM State: Idle,
```
