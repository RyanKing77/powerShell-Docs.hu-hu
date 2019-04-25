---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: ff2c2bd7369893d72db001ecabf63991ded0bfd5
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058981"
---
# <a name="unified-and-consistent-state-and-status-representation"></a><span data-ttu-id="afd11-102">Egyesített és konzisztens állapotreprezentáció</span><span class="sxs-lookup"><span data-stu-id="afd11-102">Unified and Consistent State and Status Representation</span></span>

<span data-ttu-id="afd11-103">Ebben a kiadásban az LCM állapotának és a DSC-állapot automatizálását a fejlesztésen került sor.</span><span class="sxs-lookup"><span data-stu-id="afd11-103">A series of enhancements have been made in this release for automations built LCM state and DSC status.</span></span> <span data-ttu-id="afd11-104">Ezek közé tartozik a egyesített és konzisztens állapot reprezentációinak, kezelhető dátum/idő tulajdonság által visszaadott állapot objektumok `Get-DscConfigurationStatus` parancsmag és a továbbfejlesztett LCM állapot részletei tulajdonság által visszaadott `Get-DscLocalConfigurationManager` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="afd11-104">These include unified and consistent state and status representations, manageable datetime property of status objects returned by `Get-DscConfigurationStatus` cmdlet and enhanced LCM state details property returned by `Get-DscLocalConfigurationManager` cmdlet.</span></span>

<span data-ttu-id="afd11-105">Leképezése az LCM állapotának és a DSC műveleti állapotának javított változat, és a következő szabályok szerint egyesített:</span><span class="sxs-lookup"><span data-stu-id="afd11-105">The representation of LCM state and DSC operation status are revisited and unified according to following rules:</span></span>

1. <span data-ttu-id="afd11-106">Az LCM állapotának és a DSC-állapot Notprocessed erőforrás nincs hatással.</span><span class="sxs-lookup"><span data-stu-id="afd11-106">Notprocessed resource does not impact LCM state and DSC status.</span></span>
2. <span data-ttu-id="afd11-107">Az LCM stop további erőforrások feldolgozása, miután újraindítást kérő erőforrás tapasztal.</span><span class="sxs-lookup"><span data-stu-id="afd11-107">LCM stop processing further resources once it encounters a resource that requests reboot.</span></span>
3. <span data-ttu-id="afd11-108">Egy újraindítást kérő erőforrás nem áll a szükséges állapotban, amíg újraindítást ténylegesen történik.</span><span class="sxs-lookup"><span data-stu-id="afd11-108">A resource that requests reboot is not in desired state until reboot actually happens.</span></span>
4. <span data-ttu-id="afd11-109">Hajt végre, amikor egy erőforrást, amelyet nem sikerül, LCM tartja a feldolgozás után további erőforrásokat, amíg azok nem függnek a hiba egyik.</span><span class="sxs-lookup"><span data-stu-id="afd11-109">After encountering a resource that fails, LCM keeps processing further resources as long as they are not dependent on the failure one.</span></span>
5. <span data-ttu-id="afd11-110">A törlés összesített állapotát által visszaadott `Get-DscConfigurationStatus` parancsmag az összes erőforrás állapotának a felügyelői készlete.</span><span class="sxs-lookup"><span data-stu-id="afd11-110">The overall status returned by `Get-DscConfigurationStatus` cmdlet is the super set of all resources' status.</span></span>
6. <span data-ttu-id="afd11-111">A PendingReboot állapota felülbírálja a PendingConfiguration állapota.</span><span class="sxs-lookup"><span data-stu-id="afd11-111">The PendingReboot state is a superset of PendingConfiguration state.</span></span>

<span data-ttu-id="afd11-112">Az alábbi táblázatban látható a létrejövő állapot kapcsolódó tulajdonságok alapján néhány gyakori forgatókönyveket.</span><span class="sxs-lookup"><span data-stu-id="afd11-112">The table below illustrates the resultant state and status related properties under a few typical scenarios.</span></span>

| <span data-ttu-id="afd11-113">Forgatókönyv</span><span class="sxs-lookup"><span data-stu-id="afd11-113">Scenario</span></span>                        | <span data-ttu-id="afd11-114">LCMState</span><span class="sxs-lookup"><span data-stu-id="afd11-114">LCMState</span></span>             | <span data-ttu-id="afd11-115">Állapot</span><span class="sxs-lookup"><span data-stu-id="afd11-115">Status</span></span>     | <span data-ttu-id="afd11-116">A kért újraindítási</span><span class="sxs-lookup"><span data-stu-id="afd11-116">Reboot Requested</span></span> | <span data-ttu-id="afd11-117">ResourcesInDesiredState</span><span class="sxs-lookup"><span data-stu-id="afd11-117">ResourcesInDesiredState</span></span>   | <span data-ttu-id="afd11-118">ResourcesNotInDesiredState</span><span class="sxs-lookup"><span data-stu-id="afd11-118">ResourcesNotInDesiredState</span></span> |
|---------------------------------|----------------------|------------|---------------|------------------------------|--------------------------------|
| <span data-ttu-id="afd11-119">S<sub>i</sub></span><span class="sxs-lookup"><span data-stu-id="afd11-119">S<sub>i</sub></span></span>                   | <span data-ttu-id="afd11-120">Inaktív</span><span class="sxs-lookup"><span data-stu-id="afd11-120">Idle</span></span>                 | <span data-ttu-id="afd11-121">Siker</span><span class="sxs-lookup"><span data-stu-id="afd11-121">Success</span></span>    | <span data-ttu-id="afd11-122">$false</span><span class="sxs-lookup"><span data-stu-id="afd11-122">$false</span></span>        | <span data-ttu-id="afd11-123">S</span><span class="sxs-lookup"><span data-stu-id="afd11-123">S</span></span>                            | <span data-ttu-id="afd11-124">$null</span><span class="sxs-lookup"><span data-stu-id="afd11-124">$null</span></span>                          |
| <span data-ttu-id="afd11-125">F<sub>i</sub></span><span class="sxs-lookup"><span data-stu-id="afd11-125">F<sub>i</sub></span></span>                   | <span data-ttu-id="afd11-126">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="afd11-126">PendingConfiguration</span></span> | <span data-ttu-id="afd11-127">Hiba</span><span class="sxs-lookup"><span data-stu-id="afd11-127">Failure</span></span>    | <span data-ttu-id="afd11-128">$false</span><span class="sxs-lookup"><span data-stu-id="afd11-128">$false</span></span>        | <span data-ttu-id="afd11-129">$null</span><span class="sxs-lookup"><span data-stu-id="afd11-129">$null</span></span>                        | <span data-ttu-id="afd11-130">F</span><span class="sxs-lookup"><span data-stu-id="afd11-130">F</span></span>                              |
| <span data-ttu-id="afd11-131">S,F</span><span class="sxs-lookup"><span data-stu-id="afd11-131">S,F</span></span>                             | <span data-ttu-id="afd11-132">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="afd11-132">PendingConfiguration</span></span> | <span data-ttu-id="afd11-133">Hiba</span><span class="sxs-lookup"><span data-stu-id="afd11-133">Failure</span></span>    | <span data-ttu-id="afd11-134">$false</span><span class="sxs-lookup"><span data-stu-id="afd11-134">$false</span></span>        | <span data-ttu-id="afd11-135">S</span><span class="sxs-lookup"><span data-stu-id="afd11-135">S</span></span>                            | <span data-ttu-id="afd11-136">F</span><span class="sxs-lookup"><span data-stu-id="afd11-136">F</span></span>                              |
| <span data-ttu-id="afd11-137">F,S</span><span class="sxs-lookup"><span data-stu-id="afd11-137">F,S</span></span>                             | <span data-ttu-id="afd11-138">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="afd11-138">PendingConfiguration</span></span> | <span data-ttu-id="afd11-139">Hiba</span><span class="sxs-lookup"><span data-stu-id="afd11-139">Failure</span></span>    | <span data-ttu-id="afd11-140">$false</span><span class="sxs-lookup"><span data-stu-id="afd11-140">$false</span></span>        | <span data-ttu-id="afd11-141">S</span><span class="sxs-lookup"><span data-stu-id="afd11-141">S</span></span>                            | <span data-ttu-id="afd11-142">F</span><span class="sxs-lookup"><span data-stu-id="afd11-142">F</span></span>                              |
| <span data-ttu-id="afd11-143">S<sub>1</sub>, F, S<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="afd11-143">S<sub>1</sub>, F, S<sub>2</sub></span></span> | <span data-ttu-id="afd11-144">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="afd11-144">PendingConfiguration</span></span> | <span data-ttu-id="afd11-145">Hiba</span><span class="sxs-lookup"><span data-stu-id="afd11-145">Failure</span></span>    | <span data-ttu-id="afd11-146">$false</span><span class="sxs-lookup"><span data-stu-id="afd11-146">$false</span></span>        | <span data-ttu-id="afd11-147">S<sub>1</sub>, S<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="afd11-147">S<sub>1</sub>, S<sub>2</sub></span></span> | <span data-ttu-id="afd11-148">F</span><span class="sxs-lookup"><span data-stu-id="afd11-148">F</span></span>                              |
| <span data-ttu-id="afd11-149">F<sub>1</sub>, S, F<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="afd11-149">F<sub>1</sub>, S, F<sub>2</sub></span></span> | <span data-ttu-id="afd11-150">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="afd11-150">PendingConfiguration</span></span> | <span data-ttu-id="afd11-151">Hiba</span><span class="sxs-lookup"><span data-stu-id="afd11-151">Failure</span></span>    | <span data-ttu-id="afd11-152">$false</span><span class="sxs-lookup"><span data-stu-id="afd11-152">$false</span></span>        | <span data-ttu-id="afd11-153">S</span><span class="sxs-lookup"><span data-stu-id="afd11-153">S</span></span>                            | <span data-ttu-id="afd11-154">F<sub>1</sub>, F<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="afd11-154">F<sub>1</sub>, F<sub>2</sub></span></span>   |
| <span data-ttu-id="afd11-155">S, r</span><span class="sxs-lookup"><span data-stu-id="afd11-155">S, r</span></span>                            | <span data-ttu-id="afd11-156">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="afd11-156">PendingReboot</span></span>        | <span data-ttu-id="afd11-157">Siker</span><span class="sxs-lookup"><span data-stu-id="afd11-157">Success</span></span>    | <span data-ttu-id="afd11-158">$true</span><span class="sxs-lookup"><span data-stu-id="afd11-158">$true</span></span>         | <span data-ttu-id="afd11-159">S</span><span class="sxs-lookup"><span data-stu-id="afd11-159">S</span></span>                            | <span data-ttu-id="afd11-160">r</span><span class="sxs-lookup"><span data-stu-id="afd11-160">r</span></span>                              |
| <span data-ttu-id="afd11-161">F, r</span><span class="sxs-lookup"><span data-stu-id="afd11-161">F, r</span></span>                            | <span data-ttu-id="afd11-162">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="afd11-162">PendingReboot</span></span>        | <span data-ttu-id="afd11-163">Hiba</span><span class="sxs-lookup"><span data-stu-id="afd11-163">Failure</span></span>    | <span data-ttu-id="afd11-164">$true</span><span class="sxs-lookup"><span data-stu-id="afd11-164">$true</span></span>         | <span data-ttu-id="afd11-165">$null</span><span class="sxs-lookup"><span data-stu-id="afd11-165">$null</span></span>                        | <span data-ttu-id="afd11-166">F, r</span><span class="sxs-lookup"><span data-stu-id="afd11-166">F, r</span></span>                           |
| <span data-ttu-id="afd11-167">r, S</span><span class="sxs-lookup"><span data-stu-id="afd11-167">r, S</span></span>                            | <span data-ttu-id="afd11-168">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="afd11-168">PendingReboot</span></span>        | <span data-ttu-id="afd11-169">Siker</span><span class="sxs-lookup"><span data-stu-id="afd11-169">Success</span></span>    | <span data-ttu-id="afd11-170">$true</span><span class="sxs-lookup"><span data-stu-id="afd11-170">$true</span></span>         | <span data-ttu-id="afd11-171">$null</span><span class="sxs-lookup"><span data-stu-id="afd11-171">$null</span></span>                        | <span data-ttu-id="afd11-172">r</span><span class="sxs-lookup"><span data-stu-id="afd11-172">r</span></span>                              |
| <span data-ttu-id="afd11-173">r, F</span><span class="sxs-lookup"><span data-stu-id="afd11-173">r, F</span></span>                            | <span data-ttu-id="afd11-174">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="afd11-174">PendingReboot</span></span>        | <span data-ttu-id="afd11-175">Siker</span><span class="sxs-lookup"><span data-stu-id="afd11-175">Success</span></span>    | <span data-ttu-id="afd11-176">$true</span><span class="sxs-lookup"><span data-stu-id="afd11-176">$true</span></span>         | <span data-ttu-id="afd11-177">$null</span><span class="sxs-lookup"><span data-stu-id="afd11-177">$null</span></span>                        | <span data-ttu-id="afd11-178">r</span><span class="sxs-lookup"><span data-stu-id="afd11-178">r</span></span>                              |

- <span data-ttu-id="afd11-179">S<sub>i</sub>: Az erőforrások sikeresen végrehajtott egy sorozat</span><span class="sxs-lookup"><span data-stu-id="afd11-179">S<sub>i</sub>: A series of resources that applied successfully</span></span>
- <span data-ttu-id="afd11-180">F<sub>i</sub>: Sikertelenül telepített erőforrások sorozata</span><span class="sxs-lookup"><span data-stu-id="afd11-180">F<sub>i</sub>: A series of resources that applied unsuccessfully</span></span>
- <span data-ttu-id="afd11-181">r: Egy erőforrás, amely újraindítást igényel</span><span class="sxs-lookup"><span data-stu-id="afd11-181">r: A resource that requires reboot</span></span>

```powershell
$LCMState = (Get-DscLocalConfigurationManager).LCMState
$Status = (Get-DscConfigurationStatus).Status

$RebootRequested = (Get-DscConfigurationStatus).RebootRequested

$ResourcesInDesiredState = (Get-DscConfigurationStatus).ResourcesInDesiredState

$ResourcesNotInDesiredState = (Get-DscConfigurationStatus).ResourcesNotInDesiredState
```

## <a name="enhancement-in-get-dscconfigurationstatus-cmdlet"></a><span data-ttu-id="afd11-182">Fejlesztés a Get-DscConfigurationStatus parancsmagban</span><span class="sxs-lookup"><span data-stu-id="afd11-182">Enhancement in Get-DscConfigurationStatus cmdlet</span></span>

<span data-ttu-id="afd11-183">Néhány kiegészítésre került sor a `Get-DscConfigurationStatus` parancsmag ebben a kiadásban.</span><span class="sxs-lookup"><span data-stu-id="afd11-183">A few enhancements have been made to `Get-DscConfigurationStatus` cmdlet in this release.</span></span> <span data-ttu-id="afd11-184">Korábban a StartDate a parancsmag által visszaadott objektumok tulajdonság karakterlánc típusú.</span><span class="sxs-lookup"><span data-stu-id="afd11-184">Previously, the StartDate property of objects returned by the cmdlet is of String type.</span></span> <span data-ttu-id="afd11-185">Eljött a Datetime típusú, amely lehetővé teszi az összetett kiválasztása és szűrése a belső tulajdonságok egy dátum és idő objektum egyszerűbb alapján.</span><span class="sxs-lookup"><span data-stu-id="afd11-185">Now, it is of Datetime type, which enables complex selecting and filtering easier based on the intrinsic properties of a Datetime object.</span></span>

```powershell
(Get-DscConfigurationStatus).StartDate | Format-List *

DateTime    : Friday, November 13, 2015 1:39:44 PM
Date        : 11/13/2015 12:00:00 AM
Day         : 13
DayOfWeek   : Friday
DayOfYear   : 317
Hour        : 13
Kind        : Local
Millisecond : 886
Minute      : 39
Month       : 11
Second      : 44
Ticks       : 635830187848860000
TimeOfDay   : 13:39:44.8860000
Year        : 2015
```

<span data-ttu-id="afd11-186">Az alábbi példa a, és ismételje meg az aktuális nap, hét ugyanazon a napon minden DSC művelet rekordokat adja vissza.</span><span class="sxs-lookup"><span data-stu-id="afd11-186">The following example returns all DSC operation records that happened on the same day of week as the current day.</span></span>

```powershell
(Get-DscConfigurationStatus –All) | Where-Object { $_.startdate.dayofweek -eq (Get-Date).DayOfWeek }
```

<span data-ttu-id="afd11-187">Kiküszöbölhetők azok a rekordok műveletek, amelyek a csomópont-konfiguráció (azaz olvasási csak műveletek), ne módosítsa.</span><span class="sxs-lookup"><span data-stu-id="afd11-187">Records of operations that do not make changes to node’s configuration (i.e. read only operations) are eliminated.</span></span> <span data-ttu-id="afd11-188">Ezért `Test-DscConfiguration`, `Get-DscConfiguration` műveletek már nem a visszaadott objektumok a rendszer tiltott `Get-DscConfigurationStatus` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="afd11-188">Therefore, `Test-DscConfiguration`, `Get-DscConfiguration` operations are no longer adulterated in returned objects from `Get-DscConfigurationStatus` cmdlet.</span></span> <span data-ttu-id="afd11-189">Meta konfigurációs beállítás művelet rekordok kerül, a visszatérési `Get-DscConfigurationStatus` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="afd11-189">Records of meta configuration setting operation is added to the return of `Get-DscConfigurationStatus` cmdlet.</span></span>

<span data-ttu-id="afd11-190">Az alábbiakban egy példát eredményt adott vissza a `Get-DscConfigurationStatus –All` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="afd11-190">Following is an example of result returned from `Get-DscConfigurationStatus –All` cmdlet.</span></span>

```output
All configuration operations:

Status StartDate Type RebootRequested
------ --------- ---- ---------------
Success 11/13/2015 11:38:16 AM Consistency False
Success 11/13/2015 11:23:16 AM Reboot False
Success 11/13/2015 11:21:43 AM Reboot True
Success 11/13/2015 11:20:44 AM Initial True
Success 11/13/2015 11:20:44 AM LocalConfigurationManager False
```

## <a name="enhancement-in-get-dsclocalconfigurationmanager-cmdlet"></a><span data-ttu-id="afd11-191">A Get-DscLocalConfigurationManager parancsmag a fejlesztés</span><span class="sxs-lookup"><span data-stu-id="afd11-191">Enhancement in Get-DscLocalConfigurationManager cmdlet</span></span>

<span data-ttu-id="afd11-192">Egy új mezőt LCMStateDetail a visszaadott objektum hozzáadódik `Get-DscLocalConfigurationManager` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="afd11-192">A new field of LCMStateDetail is added to the object returned from `Get-DscLocalConfigurationManager` cmdlet.</span></span> <span data-ttu-id="afd11-193">Ez a mező kitöltése LCMState "Foglalt" esetén.</span><span class="sxs-lookup"><span data-stu-id="afd11-193">This field is populated when LCMState is "Busy".</span></span> <span data-ttu-id="afd11-194">A következő parancsmaggal kérhető:</span><span class="sxs-lookup"><span data-stu-id="afd11-194">It can be retrieved by following cmdlet:</span></span>

```powershell
(Get-DscLocalConfigurationManager).LCMStateDetail
```

<span data-ttu-id="afd11-195">Következő egy példa a kimenetre végzett folyamatos figyelés a olyan konfigurációt, amely a távoli csomóponton két újraindításra van szükség.</span><span class="sxs-lookup"><span data-stu-id="afd11-195">Following is an example output of a continuous monitoring on a configuration that requires two reboots on a remote node.</span></span>

```output
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
