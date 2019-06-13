---
ms.date: 08/27/2018
keywords: PowerShell, a parancsmag
title: Jól ismert parancsnevek használata
ms.openlocfilehash: 30b33bc8739975c1a40e51c04a3ee4e426c199e7
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030893"
---
# <a name="using-familiar-command-names"></a><span data-ttu-id="9fa86-103">Jól ismert parancsnevek használata</span><span class="sxs-lookup"><span data-stu-id="9fa86-103">Using familiar command names</span></span>

<span data-ttu-id="9fa86-104">PowerShell alternatív névvel parancsok hivatkozik aliasokat támogatja.</span><span class="sxs-lookup"><span data-stu-id="9fa86-104">PowerShell supports aliases to refer to commands by alternate names.</span></span> <span data-ttu-id="9fa86-105">Aliasképző segítségével a felhasználók élményét a gyakori, a már ismert parancsnevek használata hasonló műveletek a PowerShellben más ismertetése.</span><span class="sxs-lookup"><span data-stu-id="9fa86-105">Aliasing allows users with experience in other shells to use common command names that they already know for similar operations in PowerShell.</span></span>

<span data-ttu-id="9fa86-106">Aliasképző hozzárendeli egy másik parancs egy új nevet.</span><span class="sxs-lookup"><span data-stu-id="9fa86-106">Aliasing associates a new name with another command.</span></span> <span data-ttu-id="9fa86-107">Például, a PowerShell, egy belső függvény nevű `Clear-Host` , amely törli a kimeneti ablakban.</span><span class="sxs-lookup"><span data-stu-id="9fa86-107">For example, PowerShell has an internal function named `Clear-Host` that clears the output window.</span></span> <span data-ttu-id="9fa86-108">Beírhatja, vagy a `cls` vagy `clear` alias parancsot a parancssorba.</span><span class="sxs-lookup"><span data-stu-id="9fa86-108">You can type either the `cls` or `clear` alias at a command prompt.</span></span> <span data-ttu-id="9fa86-109">PowerShell ezek az aliasok értelmezi, és futtatja a `Clear-Host` függvény.</span><span class="sxs-lookup"><span data-stu-id="9fa86-109">PowerShell interprets these aliases and runs the `Clear-Host` function.</span></span>

<span data-ttu-id="9fa86-110">Ez a funkció segít a felhasználóknak további PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9fa86-110">This feature helps users to learn PowerShell.</span></span> <span data-ttu-id="9fa86-111">Első, a legtöbb **cmd.exe** és a Unix-felhasználók vannak egy nagy repertoire, amely a felhasználók már tudja név alapján.</span><span class="sxs-lookup"><span data-stu-id="9fa86-111">First, most **cmd.exe** and Unix users have a large repertoire of commands that users already know by name.</span></span> <span data-ttu-id="9fa86-112">A PowerShell-megfelelőik nem azonos eredményeket hozhat.</span><span class="sxs-lookup"><span data-stu-id="9fa86-112">The PowerShell equivalents may not produce identical results.</span></span> <span data-ttu-id="9fa86-113">Azonban az eredmény Bezárás nem elegendő, amelyeket a felhasználók a PowerShell-parancs neve ismerete nélkül működnek.</span><span class="sxs-lookup"><span data-stu-id="9fa86-113">However, the results are close enough that users can do work without knowing the PowerShell command name.</span></span> <span data-ttu-id="9fa86-114">"Finger memória" as gazdasági válság után egy másik fő forrásai akkor, ha egy új parancs-rendszerhéj tanulási.</span><span class="sxs-lookup"><span data-stu-id="9fa86-114">"Finger memory" is another major source of frustration when learning a new command shell.</span></span> <span data-ttu-id="9fa86-115">Ha már használt **cmd.exe** éve reflexively írja be a `cls` paranccsal törölje a képernyőn.</span><span class="sxs-lookup"><span data-stu-id="9fa86-115">If you have used **cmd.exe** for years, you might reflexively type the `cls` command to clear the screen.</span></span> <span data-ttu-id="9fa86-116">Az alias nélkül `Clear-Host`, hibaüzenetet kap, és nem tudja, mi a teendő a kimenet törlése.</span><span class="sxs-lookup"><span data-stu-id="9fa86-116">Without the alias for `Clear-Host`, you receive an error message and won't know what to do to clear the output.</span></span>

<span data-ttu-id="9fa86-117">Az alábbi lista tartalmazza a közös néhány **cmd.exe** és a Unix-parancsok a PowerShellben is használhatja:</span><span class="sxs-lookup"><span data-stu-id="9fa86-117">The following list shows a few of the common **cmd.exe** and Unix commands that you can use in PowerShell:</span></span>

|||||
|-|-|-|-|
|<span data-ttu-id="9fa86-118">cat</span><span class="sxs-lookup"><span data-stu-id="9fa86-118">cat</span></span>|<span data-ttu-id="9fa86-119">a dir parancs</span><span class="sxs-lookup"><span data-stu-id="9fa86-119">dir</span></span>|<span data-ttu-id="9fa86-120">Csatlakoztatási</span><span class="sxs-lookup"><span data-stu-id="9fa86-120">mount</span></span>|<span data-ttu-id="9fa86-121">rm</span><span class="sxs-lookup"><span data-stu-id="9fa86-121">rm</span></span>|
|<span data-ttu-id="9fa86-122">cd</span><span class="sxs-lookup"><span data-stu-id="9fa86-122">cd</span></span>|<span data-ttu-id="9fa86-123">echo</span><span class="sxs-lookup"><span data-stu-id="9fa86-123">echo</span></span>|<span data-ttu-id="9fa86-124">Áthelyezés</span><span class="sxs-lookup"><span data-stu-id="9fa86-124">move</span></span>|<span data-ttu-id="9fa86-125">rmdir</span><span class="sxs-lookup"><span data-stu-id="9fa86-125">rmdir</span></span>|
|<span data-ttu-id="9fa86-126">chdir</span><span class="sxs-lookup"><span data-stu-id="9fa86-126">chdir</span></span>|<span data-ttu-id="9fa86-127">Tartalmának végleges törlése</span><span class="sxs-lookup"><span data-stu-id="9fa86-127">erase</span></span>|<span data-ttu-id="9fa86-128">popd</span><span class="sxs-lookup"><span data-stu-id="9fa86-128">popd</span></span>|<span data-ttu-id="9fa86-129">Alvó állapot</span><span class="sxs-lookup"><span data-stu-id="9fa86-129">sleep</span></span>|
|<span data-ttu-id="9fa86-130">Világos</span><span class="sxs-lookup"><span data-stu-id="9fa86-130">clear</span></span>|<span data-ttu-id="9fa86-131">H</span><span class="sxs-lookup"><span data-stu-id="9fa86-131">h</span></span>|<span data-ttu-id="9fa86-132">PS</span><span class="sxs-lookup"><span data-stu-id="9fa86-132">ps</span></span>|<span data-ttu-id="9fa86-133">Rendezés</span><span class="sxs-lookup"><span data-stu-id="9fa86-133">sort</span></span>|
|<span data-ttu-id="9fa86-134">CLS</span><span class="sxs-lookup"><span data-stu-id="9fa86-134">cls</span></span>|<span data-ttu-id="9fa86-135">Előzmények</span><span class="sxs-lookup"><span data-stu-id="9fa86-135">history</span></span>|<span data-ttu-id="9fa86-136">pushd</span><span class="sxs-lookup"><span data-stu-id="9fa86-136">pushd</span></span>|<span data-ttu-id="9fa86-137">TEE</span><span class="sxs-lookup"><span data-stu-id="9fa86-137">tee</span></span>|
|<span data-ttu-id="9fa86-138">Másolás</span><span class="sxs-lookup"><span data-stu-id="9fa86-138">copy</span></span>|<span data-ttu-id="9fa86-139">Kill</span><span class="sxs-lookup"><span data-stu-id="9fa86-139">kill</span></span>|<span data-ttu-id="9fa86-140">pwd</span><span class="sxs-lookup"><span data-stu-id="9fa86-140">pwd</span></span>|<span data-ttu-id="9fa86-141">típus</span><span class="sxs-lookup"><span data-stu-id="9fa86-141">type</span></span>|
|<span data-ttu-id="9fa86-142">del</span><span class="sxs-lookup"><span data-stu-id="9fa86-142">del</span></span>|<span data-ttu-id="9fa86-143">LP</span><span class="sxs-lookup"><span data-stu-id="9fa86-143">lp</span></span>|<span data-ttu-id="9fa86-144">r</span><span class="sxs-lookup"><span data-stu-id="9fa86-144">r</span></span>|<span data-ttu-id="9fa86-145">Írási</span><span class="sxs-lookup"><span data-stu-id="9fa86-145">write</span></span>|
|<span data-ttu-id="9fa86-146">a diff</span><span class="sxs-lookup"><span data-stu-id="9fa86-146">diff</span></span>|<span data-ttu-id="9fa86-147">ls</span><span class="sxs-lookup"><span data-stu-id="9fa86-147">ls</span></span>|<span data-ttu-id="9fa86-148">ren</span><span class="sxs-lookup"><span data-stu-id="9fa86-148">ren</span></span>||

<span data-ttu-id="9fa86-149">A `Get-Alias` parancsmag megjeleníti a valódi neve alias társított natív PowerShell-parancsot.</span><span class="sxs-lookup"><span data-stu-id="9fa86-149">The `Get-Alias` cmdlet shows you the real name of the native PowerShell command associated with an alias.</span></span>

```powershell
PS> Get-Alias cls
```

```Output
CommandType     Name                               Version    Source
-----------     ----                               -------    ------
Alias           cls -> Clear-Host
```

## <a name="interpreting-standard-aliases"></a><span data-ttu-id="9fa86-150">Standard aliasok értelmezése</span><span class="sxs-lookup"><span data-stu-id="9fa86-150">Interpreting standard aliases</span></span>

<span data-ttu-id="9fa86-151">Az aliasokat, hogy a korábban ismertetett egyéb parancsrendszerhéjakban neve kompatibilitást lettek tervezve.</span><span class="sxs-lookup"><span data-stu-id="9fa86-151">The aliases we described previously were designed for name-compatibility with other command shells.</span></span>
<span data-ttu-id="9fa86-152">A legtöbb aliasok beépített PowerShell áttekinthetőség lettek kialakítva.</span><span class="sxs-lookup"><span data-stu-id="9fa86-152">Most aliases built into PowerShell are designed for brevity.</span></span> <span data-ttu-id="9fa86-153">Rövidebb nevek használata egyszerűbb, írja be, de a rendszer nehezen olvasható, ha nem tudja, hogy mire hivatkoznak.</span><span class="sxs-lookup"><span data-stu-id="9fa86-153">Shorter names are easier to type, but are difficult to read if you don't know what they refer to.</span></span>

<span data-ttu-id="9fa86-154">PowerShell-aliasok megpróbálhatja az érthetőség és az áttekinthetőség között.</span><span class="sxs-lookup"><span data-stu-id="9fa86-154">PowerShell aliases try to compromise between clarity and brevity.</span></span> <span data-ttu-id="9fa86-155">PowerShell közös főneveket és műveletek aliasok szabványos készletét használja.</span><span class="sxs-lookup"><span data-stu-id="9fa86-155">PowerShell uses a standard set of aliases for common nouns and verbs.</span></span>

<span data-ttu-id="9fa86-156">Példa rövidítések:</span><span class="sxs-lookup"><span data-stu-id="9fa86-156">Example abbreviations:</span></span>

| <span data-ttu-id="9fa86-157">Főnév vagy művelet</span><span class="sxs-lookup"><span data-stu-id="9fa86-157">Noun or Verb</span></span> | <span data-ttu-id="9fa86-158">Rövidítése</span><span class="sxs-lookup"><span data-stu-id="9fa86-158">Abbreviation</span></span> |
|--------------|--------------|
| <span data-ttu-id="9fa86-159">Lekérés</span><span class="sxs-lookup"><span data-stu-id="9fa86-159">Get</span></span>          | <span data-ttu-id="9fa86-160">g</span><span class="sxs-lookup"><span data-stu-id="9fa86-160">g</span></span>            |
| <span data-ttu-id="9fa86-161">Beállítás</span><span class="sxs-lookup"><span data-stu-id="9fa86-161">Set</span></span>          | <span data-ttu-id="9fa86-162">s</span><span class="sxs-lookup"><span data-stu-id="9fa86-162">s</span></span>            |
| <span data-ttu-id="9fa86-163">Elem</span><span class="sxs-lookup"><span data-stu-id="9fa86-163">Item</span></span>         | <span data-ttu-id="9fa86-164">I</span><span class="sxs-lookup"><span data-stu-id="9fa86-164">i</span></span>            |
| <span data-ttu-id="9fa86-165">Hely</span><span class="sxs-lookup"><span data-stu-id="9fa86-165">Location</span></span>     | <span data-ttu-id="9fa86-166">l</span><span class="sxs-lookup"><span data-stu-id="9fa86-166">l</span></span>            |
| <span data-ttu-id="9fa86-167">Parancs</span><span class="sxs-lookup"><span data-stu-id="9fa86-167">Command</span></span>      | <span data-ttu-id="9fa86-168">cm</span><span class="sxs-lookup"><span data-stu-id="9fa86-168">cm</span></span>           |
| <span data-ttu-id="9fa86-169">Alias</span><span class="sxs-lookup"><span data-stu-id="9fa86-169">Alias</span></span>        | <span data-ttu-id="9fa86-170">Al</span><span class="sxs-lookup"><span data-stu-id="9fa86-170">al</span></span>           |

<span data-ttu-id="9fa86-171">Ezek az aliasok akkor érthető, ha ismeri a hónapok rövid nevét.</span><span class="sxs-lookup"><span data-stu-id="9fa86-171">These aliases are understandable when you know the shorthand names.</span></span>

| <span data-ttu-id="9fa86-172">Parancsmag neve</span><span class="sxs-lookup"><span data-stu-id="9fa86-172">Cmdlet name</span></span>    | <span data-ttu-id="9fa86-173">Alias</span><span class="sxs-lookup"><span data-stu-id="9fa86-173">Alias</span></span> |
|----------------|-------|
| `Get-Item`     | <span data-ttu-id="9fa86-174">gi</span><span class="sxs-lookup"><span data-stu-id="9fa86-174">gi</span></span>    |
| `Set-Item`     | <span data-ttu-id="9fa86-175">SI</span><span class="sxs-lookup"><span data-stu-id="9fa86-175">si</span></span>    |
| `Get-Location` | <span data-ttu-id="9fa86-176">GL</span><span class="sxs-lookup"><span data-stu-id="9fa86-176">gl</span></span>    |
| `Set-Location` | <span data-ttu-id="9fa86-177">SL</span><span class="sxs-lookup"><span data-stu-id="9fa86-177">sl</span></span>    |
| `Get-Command`  | <span data-ttu-id="9fa86-178">gcm –</span><span class="sxs-lookup"><span data-stu-id="9fa86-178">gcm</span></span>   |
| `Get-Alias`    | <span data-ttu-id="9fa86-179">gal</span><span class="sxs-lookup"><span data-stu-id="9fa86-179">gal</span></span>   |

<span data-ttu-id="9fa86-180">Ha ismeri, a PowerShell aliasképző, könnyebbé vált a kitalálja, hogy a **sal** alias hivatkozik `Set-Alias`.</span><span class="sxs-lookup"><span data-stu-id="9fa86-180">Once you're familiar with PowerShell aliasing, it's easy to guess that the **sal** alias refers to `Set-Alias`.</span></span>

## <a name="creating-new-aliases"></a><span data-ttu-id="9fa86-181">Új aliasok létrehozása</span><span class="sxs-lookup"><span data-stu-id="9fa86-181">Creating new aliases</span></span>

<span data-ttu-id="9fa86-182">A saját alias használatával is létrehozhat a `Set-Alias` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="9fa86-182">You can create your own aliases using the `Set-Alias` cmdlet.</span></span> <span data-ttu-id="9fa86-183">Például a következő utasításokat a korábban tárgyalt szabványos parancsmag-aliasok hozzon létre:</span><span class="sxs-lookup"><span data-stu-id="9fa86-183">For example, the following statements create the standard cmdlet aliases previously discussed:</span></span>

```powershell
Set-Alias -Name gi -Value Get-Item
Set-Alias -Name si -Value Set-Item
Set-Alias -Name gl -Value Get-Location
Set-Alias -Name sl -Value Set-Location
Set-Alias -Name gcm -Value Get-Command
```

<span data-ttu-id="9fa86-184">Belsőleg PowerShell indítása során hasonló parancsokat használja, de ezek az aliasok nem módosítható.</span><span class="sxs-lookup"><span data-stu-id="9fa86-184">Internally, PowerShell uses similar commands during startup, but these aliases are not changeable.</span></span>
<span data-ttu-id="9fa86-185">Ha megpróbálja hajtsa végre az alábbi parancsok egyikét, hibaüzenet elmagyarázza, hogy az alias nem lehet módosítani.</span><span class="sxs-lookup"><span data-stu-id="9fa86-185">If you try to execute one of these commands, you get an error explaining that the alias can't be modified.</span></span> <span data-ttu-id="9fa86-186">Például:</span><span class="sxs-lookup"><span data-stu-id="9fa86-186">For example:</span></span>

```
PS> Set-Alias -Name gi -Value Get-Item
Set-Alias : Alias is not writeable because alias gi is read-only or constant and cannot be written to.
At line:1 char:10
+ Set-Alias  <<<< -Name gi -Value Get-Item
```
