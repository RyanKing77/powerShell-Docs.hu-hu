---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 0e8d0cb1e4afa7bc791d45bfb0b981654cb09ed5
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892569"
---
# <a name="unified-and-consistent-state-and-status-representation"></a><span data-ttu-id="62dfc-102">Egyesített és konzisztens állapotreprezentáció</span><span class="sxs-lookup"><span data-stu-id="62dfc-102">Unified and Consistent State and Status Representation</span></span>

<span data-ttu-id="62dfc-103">Ebben a kiadásban az LCM állapotának és a DSC-állapot automatizálását a fejlesztésen került sor.</span><span class="sxs-lookup"><span data-stu-id="62dfc-103">A series of enhancements have been made in this release for automations built LCM state and DSC status.</span></span> <span data-ttu-id="62dfc-104">Ezek közé tartozik a egyesített és konzisztens állapot reprezentációinak, kezelhető dátum/idő tulajdonság által visszaadott állapot objektumok `Get-DscConfigurationStatus` parancsmag és a továbbfejlesztett LCM állapot részletei tulajdonság által visszaadott `Get-DscLocalConfigurationManager` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="62dfc-104">These include unified and consistent state and status representations, manageable datetime property of status objects returned by `Get-DscConfigurationStatus` cmdlet and enhanced LCM state details property returned by `Get-DscLocalConfigurationManager` cmdlet.</span></span>

<span data-ttu-id="62dfc-105">Leképezése az LCM állapotának és a DSC műveleti állapotának javított változat, és a következő szabályok szerint egyesített:</span><span class="sxs-lookup"><span data-stu-id="62dfc-105">The representation of LCM state and DSC operation status are revisited and unified according to following rules:</span></span>

1. <span data-ttu-id="62dfc-106">Az LCM állapotának és a DSC-állapot Notprocessed erőforrás nincs hatással.</span><span class="sxs-lookup"><span data-stu-id="62dfc-106">Notprocessed resource does not impact LCM state and DSC status.</span></span>
2. <span data-ttu-id="62dfc-107">Az LCM stop további erőforrások feldolgozása, miután újraindítást kérő erőforrás tapasztal.</span><span class="sxs-lookup"><span data-stu-id="62dfc-107">LCM stop processing further resources once it encounters a resource that requests reboot.</span></span>
3. <span data-ttu-id="62dfc-108">Egy újraindítást kérő erőforrás nem áll a szükséges állapotban, amíg újraindítást ténylegesen történik.</span><span class="sxs-lookup"><span data-stu-id="62dfc-108">A resource that requests reboot is not in desired state until reboot actually happens.</span></span>
4. <span data-ttu-id="62dfc-109">Hajt végre, amikor egy erőforrást, amelyet nem sikerül, LCM tartja a feldolgozás után további erőforrásokat, amíg azok nem függnek a hiba egyik.</span><span class="sxs-lookup"><span data-stu-id="62dfc-109">After encountering a resource that fails, LCM keeps processing further resources as long as they are not dependent on the failure one.</span></span>
5. <span data-ttu-id="62dfc-110">A törlés összesített állapotát által visszaadott `Get-DscConfigurationStatus` parancsmag az összes erőforrás állapotának a felügyelői készlete.</span><span class="sxs-lookup"><span data-stu-id="62dfc-110">The overall status returned by `Get-DscConfigurationStatus` cmdlet is the super set of all resources' status.</span></span>
6. <span data-ttu-id="62dfc-111">A PendingReboot állapota felülbírálja a PendingConfiguration állapota.</span><span class="sxs-lookup"><span data-stu-id="62dfc-111">The PendingReboot state is a superset of PendingConfiguration state.</span></span>

   <span data-ttu-id="62dfc-112">Az alábbi táblázatban látható a létrejövő állapot kapcsolódó tulajdonságok alapján néhány gyakori forgatókönyveket.</span><span class="sxs-lookup"><span data-stu-id="62dfc-112">The table below illustrates the resultant state and status related properties under a few typical scenarios.</span></span>

   | <span data-ttu-id="62dfc-113">Forgatókönyv</span><span class="sxs-lookup"><span data-stu-id="62dfc-113">Scenario</span></span>                    | <span data-ttu-id="62dfc-114">LCMState</span><span class="sxs-lookup"><span data-stu-id="62dfc-114">LCMState</span></span>       | <span data-ttu-id="62dfc-115">Állapot</span><span class="sxs-lookup"><span data-stu-id="62dfc-115">Status</span></span> | <span data-ttu-id="62dfc-116">A kért újraindítási</span><span class="sxs-lookup"><span data-stu-id="62dfc-116">Reboot Requested</span></span>  | <span data-ttu-id="62dfc-117">ResourcesInDesiredState</span><span class="sxs-lookup"><span data-stu-id="62dfc-117">ResourcesInDesiredState</span></span>  | <span data-ttu-id="62dfc-118">ResourcesNotInDesiredState</span><span class="sxs-lookup"><span data-stu-id="62dfc-118">ResourcesNotInDesiredState</span></span> |
   |---------------------------------|----------------------|------------|---------------|------------------------------|--------------------------------|
   | <span data-ttu-id="62dfc-119">S**^**</span><span class="sxs-lookup"><span data-stu-id="62dfc-119">S**^**</span></span>                          | <span data-ttu-id="62dfc-120">Inaktív</span><span class="sxs-lookup"><span data-stu-id="62dfc-120">Idle</span></span>                 | <span data-ttu-id="62dfc-121">Siker</span><span class="sxs-lookup"><span data-stu-id="62dfc-121">Success</span></span>    | <span data-ttu-id="62dfc-122">$false</span><span class="sxs-lookup"><span data-stu-id="62dfc-122">$false</span></span>        | <span data-ttu-id="62dfc-123">S</span><span class="sxs-lookup"><span data-stu-id="62dfc-123">S</span></span>                            | <span data-ttu-id="62dfc-124">$null</span><span class="sxs-lookup"><span data-stu-id="62dfc-124">$null</span></span>                          |
   | <span data-ttu-id="62dfc-125">F**^**</span><span class="sxs-lookup"><span data-stu-id="62dfc-125">F**^**</span></span>                          | <span data-ttu-id="62dfc-126">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="62dfc-126">PendingConfiguration</span></span> | <span data-ttu-id="62dfc-127">Hiba</span><span class="sxs-lookup"><span data-stu-id="62dfc-127">Failure</span></span>    | <span data-ttu-id="62dfc-128">$false</span><span class="sxs-lookup"><span data-stu-id="62dfc-128">$false</span></span>        | <span data-ttu-id="62dfc-129">$null</span><span class="sxs-lookup"><span data-stu-id="62dfc-129">$null</span></span>                        | <span data-ttu-id="62dfc-130">F</span><span class="sxs-lookup"><span data-stu-id="62dfc-130">F</span></span>                              |
   | <span data-ttu-id="62dfc-131">S, F</span><span class="sxs-lookup"><span data-stu-id="62dfc-131">S,F</span></span>                             | <span data-ttu-id="62dfc-132">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="62dfc-132">PendingConfiguration</span></span> | <span data-ttu-id="62dfc-133">Hiba</span><span class="sxs-lookup"><span data-stu-id="62dfc-133">Failure</span></span>    | <span data-ttu-id="62dfc-134">$false</span><span class="sxs-lookup"><span data-stu-id="62dfc-134">$false</span></span>        | <span data-ttu-id="62dfc-135">S</span><span class="sxs-lookup"><span data-stu-id="62dfc-135">S</span></span>                            | <span data-ttu-id="62dfc-136">F</span><span class="sxs-lookup"><span data-stu-id="62dfc-136">F</span></span>                              |
   | <span data-ttu-id="62dfc-137">F,S</span><span class="sxs-lookup"><span data-stu-id="62dfc-137">F,S</span></span>                             | <span data-ttu-id="62dfc-138">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="62dfc-138">PendingConfiguration</span></span> | <span data-ttu-id="62dfc-139">Hiba</span><span class="sxs-lookup"><span data-stu-id="62dfc-139">Failure</span></span>    | <span data-ttu-id="62dfc-140">$false</span><span class="sxs-lookup"><span data-stu-id="62dfc-140">$false</span></span>        | <span data-ttu-id="62dfc-141">S</span><span class="sxs-lookup"><span data-stu-id="62dfc-141">S</span></span>                            | <span data-ttu-id="62dfc-142">F</span><span class="sxs-lookup"><span data-stu-id="62dfc-142">F</span></span>                              |
   | <span data-ttu-id="62dfc-143">S<sub>1</sub>, F, S<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="62dfc-143">S<sub>1</sub>, F, S<sub>2</sub></span></span> | <span data-ttu-id="62dfc-144">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="62dfc-144">PendingConfiguration</span></span> | <span data-ttu-id="62dfc-145">Hiba</span><span class="sxs-lookup"><span data-stu-id="62dfc-145">Failure</span></span>    | <span data-ttu-id="62dfc-146">$false</span><span class="sxs-lookup"><span data-stu-id="62dfc-146">$false</span></span>        | <span data-ttu-id="62dfc-147">S<sub>1</sub>, S<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="62dfc-147">S<sub>1</sub>, S<sub>2</sub></span></span> | <span data-ttu-id="62dfc-148">F</span><span class="sxs-lookup"><span data-stu-id="62dfc-148">F</span></span>                              |
   | <span data-ttu-id="62dfc-149">F<sub>1</sub>, S, F<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="62dfc-149">F<sub>1</sub>, S, F<sub>2</sub></span></span> | <span data-ttu-id="62dfc-150">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="62dfc-150">PendingConfiguration</span></span> | <span data-ttu-id="62dfc-151">Hiba</span><span class="sxs-lookup"><span data-stu-id="62dfc-151">Failure</span></span>    | <span data-ttu-id="62dfc-152">$false</span><span class="sxs-lookup"><span data-stu-id="62dfc-152">$false</span></span>        | <span data-ttu-id="62dfc-153">S</span><span class="sxs-lookup"><span data-stu-id="62dfc-153">S</span></span>                            | <span data-ttu-id="62dfc-154">F<sub>1</sub>, F<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="62dfc-154">F<sub>1</sub>, F<sub>2</sub></span></span>   |
   | <span data-ttu-id="62dfc-155">S-, r</span><span class="sxs-lookup"><span data-stu-id="62dfc-155">S, r</span></span>                            | <span data-ttu-id="62dfc-156">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="62dfc-156">PendingReboot</span></span>        | <span data-ttu-id="62dfc-157">Siker</span><span class="sxs-lookup"><span data-stu-id="62dfc-157">Success</span></span>    | <span data-ttu-id="62dfc-158">$true</span><span class="sxs-lookup"><span data-stu-id="62dfc-158">$true</span></span>         | <span data-ttu-id="62dfc-159">S</span><span class="sxs-lookup"><span data-stu-id="62dfc-159">S</span></span>                            | <span data-ttu-id="62dfc-160">r</span><span class="sxs-lookup"><span data-stu-id="62dfc-160">r</span></span>                              |
   | <span data-ttu-id="62dfc-161">F, r</span><span class="sxs-lookup"><span data-stu-id="62dfc-161">F, r</span></span>                            | <span data-ttu-id="62dfc-162">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="62dfc-162">PendingReboot</span></span>        | <span data-ttu-id="62dfc-163">Hiba</span><span class="sxs-lookup"><span data-stu-id="62dfc-163">Failure</span></span>    | <span data-ttu-id="62dfc-164">$true</span><span class="sxs-lookup"><span data-stu-id="62dfc-164">$true</span></span>         | <span data-ttu-id="62dfc-165">$null</span><span class="sxs-lookup"><span data-stu-id="62dfc-165">$null</span></span>                        | <span data-ttu-id="62dfc-166">F, r</span><span class="sxs-lookup"><span data-stu-id="62dfc-166">F, r</span></span>                           |
   | <span data-ttu-id="62dfc-167">r, S</span><span class="sxs-lookup"><span data-stu-id="62dfc-167">r, S</span></span>                            | <span data-ttu-id="62dfc-168">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="62dfc-168">PendingReboot</span></span>        | <span data-ttu-id="62dfc-169">Siker</span><span class="sxs-lookup"><span data-stu-id="62dfc-169">Success</span></span>    | <span data-ttu-id="62dfc-170">$true</span><span class="sxs-lookup"><span data-stu-id="62dfc-170">$true</span></span>         | <span data-ttu-id="62dfc-171">$null</span><span class="sxs-lookup"><span data-stu-id="62dfc-171">$null</span></span>                        | <span data-ttu-id="62dfc-172">r</span><span class="sxs-lookup"><span data-stu-id="62dfc-172">r</span></span>                              |
   | <span data-ttu-id="62dfc-173">r, F</span><span class="sxs-lookup"><span data-stu-id="62dfc-173">r, F</span></span>                            | <span data-ttu-id="62dfc-174">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="62dfc-174">PendingReboot</span></span>        | <span data-ttu-id="62dfc-175">Siker</span><span class="sxs-lookup"><span data-stu-id="62dfc-175">Success</span></span>    | <span data-ttu-id="62dfc-176">$true</span><span class="sxs-lookup"><span data-stu-id="62dfc-176">$true</span></span>         | <span data-ttu-id="62dfc-177">$null</span><span class="sxs-lookup"><span data-stu-id="62dfc-177">$null</span></span>                        | <span data-ttu-id="62dfc-178">r</span><span class="sxs-lookup"><span data-stu-id="62dfc-178">r</span></span>                              |

   <span data-ttu-id="62dfc-179">^
   S<sub>i</sub>: erőforrások, amelyek sikeresen alkalmazva F sorozata<sub>i</sub>: egy sorozat erőforrásokat, amelyeket a alkalmazni sikertelenül r: egy erőforrás, amelyhez újraindítás szükséges \*</span><span class="sxs-lookup"><span data-stu-id="62dfc-179">^
   S<sub>i</sub>: A series of resources that applied successfully F<sub>i</sub>: A series of resources that applied unsuccessfully r: A resource that requires reboot \*</span></span>

   ```powershell
   $LCMState = (Get-DscLocalConfigurationManager).LCMState
   $Status = (Get-DscConfigurationStatus).Status

   $RebootRequested = (Get-DscConfigurationStatus).RebootRequested

   $ResourcesInDesiredState = (Get-DscConfigurationStatus).ResourcesInDesiredState

   $ResourcesNotInDesiredState = (Get-DscConfigurationStatus).ResourcesNotInDesiredState
   ```

## <a name="enhancement-in-get-dscconfigurationstatus-cmdlet"></a><span data-ttu-id="62dfc-180">Fejlesztés a Get-DscConfigurationStatus parancsmagban</span><span class="sxs-lookup"><span data-stu-id="62dfc-180">Enhancement in Get-DscConfigurationStatus cmdlet</span></span>

<span data-ttu-id="62dfc-181">Néhány kiegészítésre került sor a `Get-DscConfigurationStatus` parancsmag ebben a kiadásban.</span><span class="sxs-lookup"><span data-stu-id="62dfc-181">A few enhancements have been made to `Get-DscConfigurationStatus` cmdlet in this release.</span></span> <span data-ttu-id="62dfc-182">Korábban a StartDate a parancsmag által visszaadott objektumok tulajdonság karakterlánc típusú.</span><span class="sxs-lookup"><span data-stu-id="62dfc-182">Previously, the StartDate property of objects returned by the cmdlet is of String type.</span></span> <span data-ttu-id="62dfc-183">Eljött a Datetime típusú, amely lehetővé teszi az összetett kiválasztása és szűrése a belső tulajdonságok egy dátum és idő objektum egyszerűbb alapján.</span><span class="sxs-lookup"><span data-stu-id="62dfc-183">Now, it is of Datetime type, which enables complex selecting and filtering easier based on the intrinsic properties of a Datetime object.</span></span>

```powershell
(Get-DscConfigurationStatus).StartDate | Format-List *
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

<span data-ttu-id="62dfc-184">Következő egy példa, amely visszaadja az összes DSC műveleti rekordok történt a hét ma is ugyanazon a napon.</span><span class="sxs-lookup"><span data-stu-id="62dfc-184">Following is an example that returns all DSC operation records happened on the same day of week as today.</span></span>

```powershell
(Get-DscConfigurationStatus –All) | Where-Object { $_.startdate.dayofweek -eq (Get-Date).DayOfWeek }
```

<span data-ttu-id="62dfc-185">Kiküszöbölhetők azok a rekordok műveletek, amelyek a csomópont-konfiguráció (azaz olvasási csak műveletek), ne módosítsa.</span><span class="sxs-lookup"><span data-stu-id="62dfc-185">Records of operations that do not make changes to node’s configuration (i.e. read only operations) are eliminated.</span></span> <span data-ttu-id="62dfc-186">Ezért `Test-DscConfiguration`, `Get-DscConfiguration` műveletek már nem a visszaadott objektumok a rendszer tiltott `Get-DscConfigurationStatus` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="62dfc-186">Therefore, `Test-DscConfiguration`, `Get-DscConfiguration` operations are no longer adulterated in returned objects from `Get-DscConfigurationStatus` cmdlet.</span></span>
<span data-ttu-id="62dfc-187">Meta konfigurációs beállítás művelet rekordok kerül, a visszatérési `Get-DscConfigurationStatus` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="62dfc-187">Records of meta configuration setting operation is added to the return of `Get-DscConfigurationStatus` cmdlet.</span></span>

<span data-ttu-id="62dfc-188">Az alábbiakban egy példát eredményt adott vissza a `Get-DscConfigurationStatus` – minden parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="62dfc-188">Following is an example of result returned from `Get-DscConfigurationStatus` –All cmdlet.</span></span>

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

## <a name="enhancement-in-get-dsclocalconfigurationmanager-cmdlet"></a><span data-ttu-id="62dfc-189">A Get-DscLocalConfigurationManager parancsmag a fejlesztés</span><span class="sxs-lookup"><span data-stu-id="62dfc-189">Enhancement in Get-DscLocalConfigurationManager cmdlet</span></span>

<span data-ttu-id="62dfc-190">Egy új mezőt LCMStateDetail a visszaadott objektum hozzáadódik `Get-DscLocalConfigurationManager` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="62dfc-190">A new field of LCMStateDetail is added to the object returned from `Get-DscLocalConfigurationManager` cmdlet.</span></span> <span data-ttu-id="62dfc-191">Ez a mező kitöltése LCMState "Foglalt" esetén.</span><span class="sxs-lookup"><span data-stu-id="62dfc-191">This field is populated when LCMState is "Busy".</span></span> <span data-ttu-id="62dfc-192">A következő parancsmaggal kérhető:</span><span class="sxs-lookup"><span data-stu-id="62dfc-192">It can be retrieved by following cmdlet:</span></span>

```powershell
(Get-DscLocalConfigurationManager).LCMStateDetail
```

<span data-ttu-id="62dfc-193">Következő egy példa a kimenetre végzett folyamatos figyelés a olyan konfigurációt, amely a távoli csomóponton két újraindításra van szükség.</span><span class="sxs-lookup"><span data-stu-id="62dfc-193">Following is an example output of a continuous monitoring on a configuration that requires two reboots on a remote node.</span></span>

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