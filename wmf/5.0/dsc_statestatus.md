---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 9a8c261c01a7970f2e7f89172007768b63295673
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="unified-and-consistent-state-and-status-representation"></a><span data-ttu-id="cad90-102">Egyesített és konzisztens állapotreprezentáció</span><span class="sxs-lookup"><span data-stu-id="cad90-102">Unified and Consistent State and Status Representation</span></span>

<span data-ttu-id="cad90-103">Fejlesztésen végzett ebben a kiadásban a beépített LCM állapotát és DSC állapot automatizálása.</span><span class="sxs-lookup"><span data-stu-id="cad90-103">A series of enhancements have been made in this release for automations built LCM state and DSC status.</span></span> <span data-ttu-id="cad90-104">Ezek közé tartozik a egyesített és konzisztens állapotban és állapot formátumban, az állapot objektumok kezelhető dátum/idő tulajdonság Get-DscConfigurationStatus parancsmag által visszaadott és fokozott LCM állapot részletei tulajdonság Get-DscLocalConfigurationManager által visszaadott parancsmag.</span><span class="sxs-lookup"><span data-stu-id="cad90-104">These include unified and consistent state and status representations, manageable datetime property of status objects returned by Get-DscConfigurationStatus cmdlet and enhanced LCM state details property returned by Get-DscLocalConfigurationManager cmdlet.</span></span>

<span data-ttu-id="cad90-105">LCM állapot és a DSC műveleti állapotának ábrázolása javított változat, és a következő szabályok szerint egyesített:</span><span class="sxs-lookup"><span data-stu-id="cad90-105">The representation of LCM state and DSC operation status are revisited and unified according to following rules:</span></span>
1.  <span data-ttu-id="cad90-106">Notprocessed erőforrás nem befolyásolja a LCM állapotot és a DSC-állapota.</span><span class="sxs-lookup"><span data-stu-id="cad90-106">Notprocessed resource does not impact LCM state and DSC status.</span></span>
2.  <span data-ttu-id="cad90-107">További erőforrások feldolgozásának, miután újraindítást kérő erőforrás ütközik LCM leállítása.</span><span class="sxs-lookup"><span data-stu-id="cad90-107">LCM stop processing further resources once it encounters a resource that requests reboot.</span></span>
3.  <span data-ttu-id="cad90-108">Egy erőforrás újraindítást kérő nincs megfelelő állapotban amíg újraindítást ténylegesen történik.</span><span class="sxs-lookup"><span data-stu-id="cad90-108">A resource that requests reboot is not in desired state until reboot actually happens.</span></span>
4.  <span data-ttu-id="cad90-109">Amikor egy erőforrást, amely nem sikerül, LCM tartja a feldolgozás után további erőforrások mindaddig, amíg azok nem függ a hiba egyik.</span><span class="sxs-lookup"><span data-stu-id="cad90-109">After encountering a resource that fails, LCM keeps processing further resources as long as they are not dependent on the failure one.</span></span>
5.  <span data-ttu-id="cad90-110">A Get-DscConfigurationStatus parancsmag által visszaadott összesített állapotát az összes erőforrás állapotának super összessége.</span><span class="sxs-lookup"><span data-stu-id="cad90-110">The overall status returned by Get-DscConfigurationStatus cmdlet is the super set of all resources’ status.</span></span>
6.  <span data-ttu-id="cad90-111">A PendingReboot állapota felülbírálja a PendingConfiguration állapotát.</span><span class="sxs-lookup"><span data-stu-id="cad90-111">The PendingReboot state is a superset of PendingConfiguration state.</span></span>

<span data-ttu-id="cad90-112">Az alábbi táblázat szemlélteti a eredő állapot kapcsolódó tulajdonságok néhány jellemző forgatókönyvek alapján.</span><span class="sxs-lookup"><span data-stu-id="cad90-112">The table below illustrates the resultant state and status related properties under a few typical scenarios.</span></span>

| <span data-ttu-id="cad90-113">**Scenario**</span><span class="sxs-lookup"><span data-stu-id="cad90-113">**Scenario**</span></span>                    | <span data-ttu-id="cad90-114">**LCMState\***</span><span class="sxs-lookup"><span data-stu-id="cad90-114">**LCMState\***</span></span>       | <span data-ttu-id="cad90-115">**Status**</span><span class="sxs-lookup"><span data-stu-id="cad90-115">**Status**</span></span> | <span data-ttu-id="cad90-116">**A kért újraindítás**</span><span class="sxs-lookup"><span data-stu-id="cad90-116">**Reboot Requested**</span></span>  | <span data-ttu-id="cad90-117">**ResourcesInDesiredState**</span><span class="sxs-lookup"><span data-stu-id="cad90-117">**ResourcesInDesiredState**</span></span>  | <span data-ttu-id="cad90-118">**ResourcesNotInDesiredState**</span><span class="sxs-lookup"><span data-stu-id="cad90-118">**ResourcesNotInDesiredState**</span></span> |
|---------------------------------|----------------------|------------|---------------|------------------------------|--------------------------------|
| <span data-ttu-id="cad90-119">S**^**</span><span class="sxs-lookup"><span data-stu-id="cad90-119">S**^**</span></span>                          | <span data-ttu-id="cad90-120">Üresjárati</span><span class="sxs-lookup"><span data-stu-id="cad90-120">Idle</span></span>                 | <span data-ttu-id="cad90-121">Siker</span><span class="sxs-lookup"><span data-stu-id="cad90-121">Success</span></span>    | <span data-ttu-id="cad90-122">$false</span><span class="sxs-lookup"><span data-stu-id="cad90-122">$false</span></span>        | <span data-ttu-id="cad90-123">S</span><span class="sxs-lookup"><span data-stu-id="cad90-123">S</span></span>                            | <span data-ttu-id="cad90-124">$null</span><span class="sxs-lookup"><span data-stu-id="cad90-124">$null</span></span>                          |
| <span data-ttu-id="cad90-125">F**^**</span><span class="sxs-lookup"><span data-stu-id="cad90-125">F**^**</span></span>                          | <span data-ttu-id="cad90-126">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="cad90-126">PendingConfiguration</span></span> | <span data-ttu-id="cad90-127">Hiba</span><span class="sxs-lookup"><span data-stu-id="cad90-127">Failure</span></span>    | <span data-ttu-id="cad90-128">$false</span><span class="sxs-lookup"><span data-stu-id="cad90-128">$false</span></span>        | <span data-ttu-id="cad90-129">$null</span><span class="sxs-lookup"><span data-stu-id="cad90-129">$null</span></span>                        | <span data-ttu-id="cad90-130">F</span><span class="sxs-lookup"><span data-stu-id="cad90-130">F</span></span>                              |
| <span data-ttu-id="cad90-131">S,F</span><span class="sxs-lookup"><span data-stu-id="cad90-131">S,F</span></span>                             | <span data-ttu-id="cad90-132">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="cad90-132">PendingConfiguration</span></span> | <span data-ttu-id="cad90-133">Hiba</span><span class="sxs-lookup"><span data-stu-id="cad90-133">Failure</span></span>    | <span data-ttu-id="cad90-134">$false</span><span class="sxs-lookup"><span data-stu-id="cad90-134">$false</span></span>        | <span data-ttu-id="cad90-135">S</span><span class="sxs-lookup"><span data-stu-id="cad90-135">S</span></span>                            | <span data-ttu-id="cad90-136">F</span><span class="sxs-lookup"><span data-stu-id="cad90-136">F</span></span>                              |
| <span data-ttu-id="cad90-137">F,S</span><span class="sxs-lookup"><span data-stu-id="cad90-137">F,S</span></span>                             | <span data-ttu-id="cad90-138">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="cad90-138">PendingConfiguration</span></span> | <span data-ttu-id="cad90-139">Hiba</span><span class="sxs-lookup"><span data-stu-id="cad90-139">Failure</span></span>    | <span data-ttu-id="cad90-140">$false</span><span class="sxs-lookup"><span data-stu-id="cad90-140">$false</span></span>        | <span data-ttu-id="cad90-141">S</span><span class="sxs-lookup"><span data-stu-id="cad90-141">S</span></span>                            | <span data-ttu-id="cad90-142">F</span><span class="sxs-lookup"><span data-stu-id="cad90-142">F</span></span>                              |
| <span data-ttu-id="cad90-143">S<sub>1</sub>, F, S<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="cad90-143">S<sub>1</sub>, F, S<sub>2</sub></span></span> | <span data-ttu-id="cad90-144">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="cad90-144">PendingConfiguration</span></span> | <span data-ttu-id="cad90-145">Hiba</span><span class="sxs-lookup"><span data-stu-id="cad90-145">Failure</span></span>    | <span data-ttu-id="cad90-146">$false</span><span class="sxs-lookup"><span data-stu-id="cad90-146">$false</span></span>        | <span data-ttu-id="cad90-147">S<sub>1</sub>, S<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="cad90-147">S<sub>1</sub>, S<sub>2</sub></span></span> | <span data-ttu-id="cad90-148">F</span><span class="sxs-lookup"><span data-stu-id="cad90-148">F</span></span>                              |
| <span data-ttu-id="cad90-149">F<sub>1</sub>, S, F<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="cad90-149">F<sub>1</sub>, S, F<sub>2</sub></span></span> | <span data-ttu-id="cad90-150">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="cad90-150">PendingConfiguration</span></span> | <span data-ttu-id="cad90-151">Hiba</span><span class="sxs-lookup"><span data-stu-id="cad90-151">Failure</span></span>    | <span data-ttu-id="cad90-152">$false</span><span class="sxs-lookup"><span data-stu-id="cad90-152">$false</span></span>        | <span data-ttu-id="cad90-153">S</span><span class="sxs-lookup"><span data-stu-id="cad90-153">S</span></span>                            | <span data-ttu-id="cad90-154">F<sub>1</sub>, F<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="cad90-154">F<sub>1</sub>, F<sub>2</sub></span></span>   |
| <span data-ttu-id="cad90-155">S, r</span><span class="sxs-lookup"><span data-stu-id="cad90-155">S, r</span></span>                            | <span data-ttu-id="cad90-156">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="cad90-156">PendingReboot</span></span>        | <span data-ttu-id="cad90-157">Siker</span><span class="sxs-lookup"><span data-stu-id="cad90-157">Success</span></span>    | <span data-ttu-id="cad90-158">$true</span><span class="sxs-lookup"><span data-stu-id="cad90-158">$true</span></span>         | <span data-ttu-id="cad90-159">S</span><span class="sxs-lookup"><span data-stu-id="cad90-159">S</span></span>                            | <span data-ttu-id="cad90-160">r</span><span class="sxs-lookup"><span data-stu-id="cad90-160">r</span></span>                              |
| <span data-ttu-id="cad90-161">F, r</span><span class="sxs-lookup"><span data-stu-id="cad90-161">F, r</span></span>                            | <span data-ttu-id="cad90-162">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="cad90-162">PendingReboot</span></span>        | <span data-ttu-id="cad90-163">Hiba</span><span class="sxs-lookup"><span data-stu-id="cad90-163">Failure</span></span>    | <span data-ttu-id="cad90-164">$true</span><span class="sxs-lookup"><span data-stu-id="cad90-164">$true</span></span>         | <span data-ttu-id="cad90-165">$null</span><span class="sxs-lookup"><span data-stu-id="cad90-165">$null</span></span>                        | <span data-ttu-id="cad90-166">F, r</span><span class="sxs-lookup"><span data-stu-id="cad90-166">F, r</span></span>                           |
| <span data-ttu-id="cad90-167">r, S</span><span class="sxs-lookup"><span data-stu-id="cad90-167">r, S</span></span>                            | <span data-ttu-id="cad90-168">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="cad90-168">PendingReboot</span></span>        | <span data-ttu-id="cad90-169">Siker</span><span class="sxs-lookup"><span data-stu-id="cad90-169">Success</span></span>    | <span data-ttu-id="cad90-170">$true</span><span class="sxs-lookup"><span data-stu-id="cad90-170">$true</span></span>         | <span data-ttu-id="cad90-171">$null</span><span class="sxs-lookup"><span data-stu-id="cad90-171">$null</span></span>                        | <span data-ttu-id="cad90-172">r</span><span class="sxs-lookup"><span data-stu-id="cad90-172">r</span></span>                              |
| <span data-ttu-id="cad90-173">r, F</span><span class="sxs-lookup"><span data-stu-id="cad90-173">r, F</span></span>                            | <span data-ttu-id="cad90-174">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="cad90-174">PendingReboot</span></span>        | <span data-ttu-id="cad90-175">Siker</span><span class="sxs-lookup"><span data-stu-id="cad90-175">Success</span></span>    | <span data-ttu-id="cad90-176">$true</span><span class="sxs-lookup"><span data-stu-id="cad90-176">$true</span></span>         | <span data-ttu-id="cad90-177">$null</span><span class="sxs-lookup"><span data-stu-id="cad90-177">$null</span></span>                        | <span data-ttu-id="cad90-178">r</span><span class="sxs-lookup"><span data-stu-id="cad90-178">r</span></span>                              |

<span data-ttu-id="cad90-179">^ S<sub>i</sub>: erőforrásokat, a rendszer sikeresen alkalmazta F sorozata<sub>i</sub>: a rendszer újraindítását igénylő r: A erőforrás sikertelenül telepített erőforrások több \*</span><span class="sxs-lookup"><span data-stu-id="cad90-179">^ S<sub>i</sub>: A series of resources that applied successfully F<sub>i</sub>: A series of resources that applied unsuccessfully r: A resource that requires reboot \*</span></span>

```powershell
$LCMState = (Get-DscLocalConfigurationManager).LCMState
$Status = (Get-DscConfigurationStatus).Status

$RebootRequested = (Get-DscConfigurationStatus).RebootRequested

$ResourcesInDesiredState = (Get-DscConfigurationStatus).ResourcesInDesiredState

$ResourcesNotInDesiredState = (Get-DscConfigurationStatus).ResourcesNotInDesiredState
```
## <a name="enhancement-in-get-dscconfigurationstatus-cmdlet"></a><span data-ttu-id="cad90-180">A Get-DscConfigurationStatus parancsmag továbbfejlesztése</span><span class="sxs-lookup"><span data-stu-id="cad90-180">Enhancement in Get-DscConfigurationStatus cmdlet</span></span>

<span data-ttu-id="cad90-181">Ebben a kiadásban a Get-DscConfigurationStatus parancsmagnak néhány kiegészítésre került sor.</span><span class="sxs-lookup"><span data-stu-id="cad90-181">A few enhancements have been made to Get-DscConfigurationStatus cmdlet in this release.</span></span> <span data-ttu-id="cad90-182">Korábban a Kezdődátum a parancsmag által visszaadott objektumok tulajdonsága karakterlánc típusú.</span><span class="sxs-lookup"><span data-stu-id="cad90-182">Previously, the StartDate property of objects returned by the cmdlet is of String type.</span></span> <span data-ttu-id="cad90-183">Most már dátum/idő típusú, amely lehetővé teszi összetett, válassza ki, majd a szűrési beállítások könnyebb a belső tulajdonságok egy DateTime típusú objektum.</span><span class="sxs-lookup"><span data-stu-id="cad90-183">Now, it is of Datetime type, which enables complex selecting and filtering easier based on the intrinsic properties of a Datetime object.</span></span>
```powershell
(Get-DscConfigurationStatus).StartDate | fl \*
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

<span data-ttu-id="cad90-184">Az alábbiakban látható egy példa, amely ugyanarra a napra esnek ennek ma hét történt a DSC-művelet az összes rekord visszaadása.</span><span class="sxs-lookup"><span data-stu-id="cad90-184">Following is an example that returns all DSC operation records happened on the same day of week as today.</span></span>
```powershell
(Get-DscConfigurationStatus –All) | where { $\_.startdate.dayofweek -eq (Get-Date).DayOfWeek }
```

<span data-ttu-id="cad90-185">Ne módosítsa a csomópont konfigurációs (vagyis olvasási csak műveletek) műveletkészlet rekordok szűrni.</span><span class="sxs-lookup"><span data-stu-id="cad90-185">Records of operations that do not make changes to node’s configuration (i.e. read only operations) are eliminated.</span></span> <span data-ttu-id="cad90-186">Ezért teszt-DscConfiguration, Get-DscConfiguration műveletek vannak már nem tiltott a Get-DscConfigurationStatus parancsmag objektumot sem adott vissza.</span><span class="sxs-lookup"><span data-stu-id="cad90-186">Therefore, Test-DscConfiguration, Get-DscConfiguration operations are no longer adulterated in returned objects from Get-DscConfigurationStatus cmdlet.</span></span>
<span data-ttu-id="cad90-187">Meta konfigurációs beállítás művelet rögzíti a Get-DscConfigurationStatus parancsmag visszatérési kerül.</span><span class="sxs-lookup"><span data-stu-id="cad90-187">Records of meta configuration setting operation is added to the return of Get-DscConfigurationStatus cmdlet.</span></span>

<span data-ttu-id="cad90-188">Az alábbiakban látható egy példa a Get-DscConfigurationStatus visszaadott eredmény – az összes parancsmag.</span><span class="sxs-lookup"><span data-stu-id="cad90-188">Following is an example of result returned from Get-DscConfigurationStatus –All cmdlet.</span></span>
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

## <a name="enhancement-in-get-dsclocalconfigurationmanager-cmdlet"></a><span data-ttu-id="cad90-189">A Get-DscLocalConfigurationManager parancsmag továbbfejlesztése</span><span class="sxs-lookup"><span data-stu-id="cad90-189">Enhancement in Get-DscLocalConfigurationManager cmdlet</span></span>
<span data-ttu-id="cad90-190">Egy új mezőt a LCMStateDetail hozzáadódik a Get-DscLocalConfigurationManager parancsmag által visszaadott objektum.</span><span class="sxs-lookup"><span data-stu-id="cad90-190">A new field of LCMStateDetail is added to the object returned from Get-DscLocalConfigurationManager cmdlet.</span></span> <span data-ttu-id="cad90-191">Ebben a mezőben van feltöltve, ha LCMState "Foglalt".</span><span class="sxs-lookup"><span data-stu-id="cad90-191">This field is populated when LCMState is “Busy”.</span></span> <span data-ttu-id="cad90-192">Lekérhető által a következő parancsmagot:</span><span class="sxs-lookup"><span data-stu-id="cad90-192">It can be retrieved by following cmdlet:</span></span>
```powershell
(Get-DscLocalConfigurationManager).LCMStateDetail
```

<span data-ttu-id="cad90-193">Az alábbiakban látható egy példa a kimenetre végzett folyamatos figyelés a olyan konfigurációt, amely a távoli csomóponton levő két újraindításra van szükség.</span><span class="sxs-lookup"><span data-stu-id="cad90-193">Following is an example output of a continuous monitoring on a configuration that requires two reboots on a remote node.</span></span>
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