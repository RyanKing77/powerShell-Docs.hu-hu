---
ms.date: 06/12/2017
keywords: a jea, powershell, biztonsági
title: A JEA szerepköri funkciók
ms.openlocfilehash: bd0a995adc60e50049ff99d6b23e7c2aeb745a18
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/13/2018
ms.locfileid: "45522941"
---
# <a name="jea-role-capabilities"></a><span data-ttu-id="31059-103">A JEA szerepköri funkciók</span><span class="sxs-lookup"><span data-stu-id="31059-103">JEA Role Capabilities</span></span>

> <span data-ttu-id="31059-104">A következőkre vonatkozik: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="31059-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="31059-105">A JEA-végpont létrehozása, amikor szüksége lesz legalább "szerepkör-funkciókkal" ismertetik meghatározásához *mi* valaki a JEA-munkamenet az teheti meg.</span><span class="sxs-lookup"><span data-stu-id="31059-105">When creating a JEA endpoint, you will need to define one or more "role capabilities" which describe *what* someone can do in a JEA session.</span></span>
<span data-ttu-id="31059-106">Egy szerepkör szolgáltatás érhető el egy PowerShell-adatfájlt .psrc kiterjesztése, amely felsorolja az összes a parancsmagok, függvények, szolgáltatók és külső programok, amelyek a felhasználók kapcsolódás elérhetővé kell tenni.</span><span class="sxs-lookup"><span data-stu-id="31059-106">A role capability is a PowerShell data file with the .psrc extension that lists all the cmdlets, functions, providers, and external programs that should be made available to connecting users.</span></span>

<span data-ttu-id="31059-107">Ez a témakör ismerteti, hogyan hozzon létre egy PowerShell szerepkör képesség fájlt a JEA-felhasználók számára.</span><span class="sxs-lookup"><span data-stu-id="31059-107">This topic describes how to create a PowerShell role capability file for your JEA users.</span></span>

## <a name="determine-which-commands-to-allow"></a><span data-ttu-id="31059-108">Határozza meg, hogy mely parancsok</span><span class="sxs-lookup"><span data-stu-id="31059-108">Determine which commands to allow</span></span>

<span data-ttu-id="31059-109">Az első lépés egy szerepkör képesség fájl létrehozásakor, hogy fontolja meg, mi a felhasználók, akik a szerepkör hozzá kell férniük.</span><span class="sxs-lookup"><span data-stu-id="31059-109">The first step when creating a role capability file is to consider what the users who are assigned the role will need access to.</span></span>
<span data-ttu-id="31059-110">A követelmények adatgyűjtési folyamatának eltarthat egy ideig, de rendkívül fontos folyamat.</span><span class="sxs-lookup"><span data-stu-id="31059-110">This requirements gathering process can take a while, but it is a very important process.</span></span>
<span data-ttu-id="31059-111">Mivel a felhasználók számára hozzáférést túl kevés parancsmagok és funkciók megakadályozhatja azokat a feladat végrehajtása.</span><span class="sxs-lookup"><span data-stu-id="31059-111">Giving users access to too few cmdlets and functions can prevent them from getting their job done.</span></span>
<span data-ttu-id="31059-112">Túl sok parancsmagok és funkciók elérésének engedélyezése a felhasználók számára ez több, mint a kívánt azok implicit rendszergazda jogosultságokkal a biztonsági forgalmazóval gyengítése vezethet.</span><span class="sxs-lookup"><span data-stu-id="31059-112">Allowing access to too many cmdlets and functions can lead to users doing more than you intended with their implicit admin privileges, weakening your security stance.</span></span>

<span data-ttu-id="31059-113">Hogyan nyissa meg a folyamat függ a szervezet és a célokat, azonban az alábbi tippek segítségével, győződjön meg arról, hogy jó úton.</span><span class="sxs-lookup"><span data-stu-id="31059-113">How you go about this process will depend on your organization and goals, however the following tips can help ensure you're on the right path.</span></span>

1. <span data-ttu-id="31059-114">**Azonosítsa** a parancsok felhasználóknak a munkájuk elvégzéséhez használ.</span><span class="sxs-lookup"><span data-stu-id="31059-114">**Identify** the commands users are using to get their jobs done.</span></span> <span data-ttu-id="31059-115">Ez magában foglalhatja felmérve az informatikai részleg, automatizálási szkriptek ellenőrzése vagy a PowerShell-munkamenet átiratok vagy naplók elemzése.</span><span class="sxs-lookup"><span data-stu-id="31059-115">This may involve surveying IT staff, checking automation scripts, or analyzing PowerShell session transcripts or logs.</span></span>
2. <span data-ttu-id="31059-116">**Frissítés** felhasználása parancssori eszközök használatával PowerShell megfelelője, ahol lehetséges, a legjobb naplózás és a JEA testreszabási munkáját.</span><span class="sxs-lookup"><span data-stu-id="31059-116">**Update** use of command line tools to PowerShell equivalents, where possible, for the best auditing and JEA customization experience.</span></span> <span data-ttu-id="31059-117">Külső programok nem korlátozható, natív PowerShell-parancsmagok és a JEA funkciókat kínálja.</span><span class="sxs-lookup"><span data-stu-id="31059-117">External programs cannot be constrained as granularly as native PowerShell cmdlets and functions in JEA.</span></span>
3. <span data-ttu-id="31059-118">**Korlátozása** hatóköre a parancsmagok, ha csak szükség esetén engedélyezi a megadott paramétereket, vagy a paraméterértékeket.</span><span class="sxs-lookup"><span data-stu-id="31059-118">**Restrict** the scope of the cmdlets if necessary to only allow specific parameters or parameter values.</span></span> <span data-ttu-id="31059-119">Ez különösen fontos, ha a felhasználók kezeléséhez a rendszer csak tudnia kell.</span><span class="sxs-lookup"><span data-stu-id="31059-119">This is particularly important if users should only be able to manage part of a system.</span></span>
4. <span data-ttu-id="31059-120">**Hozzon létre** összetett parancsokat vagy parancsokat, amelyeket nehéz a JEA képeinek egyéni függvényekhez.</span><span class="sxs-lookup"><span data-stu-id="31059-120">**Create** custom functions to replace complex commands or commands which are difficult to constrain in JEA.</span></span> <span data-ttu-id="31059-121">Egyszerű függvény, amely becsomagolja a komplex parancsot, vagy további érvényesítési logika vonatkozik a rendszergazdák és a végfelhasználói egyszerűség további vezérlőelemek kínálnak.</span><span class="sxs-lookup"><span data-stu-id="31059-121">A simple function that wraps a complex command or applies additional validation logic can offer additional control for admins and end-user simplicity.</span></span>
5. <span data-ttu-id="31059-122">**Teszt** a hatókörrel rendelkező parancsok listájához, engedélyezett a felhasználók és/vagy az automation-szolgáltatásokat és szükség szerint módosíthatja.</span><span class="sxs-lookup"><span data-stu-id="31059-122">**Test** the scoped list of allowable commands with your users and/or automation services and adjust as necessary.</span></span>

<span data-ttu-id="31059-123">Fontos megjegyezni, hogy a JEA-munkamenet parancsai gyakran futtassa az admin (vagy más módon emelt szintű) jogosultságokkal.</span><span class="sxs-lookup"><span data-stu-id="31059-123">It is important to remember that commands in a JEA session are often run with admin (or otherwise elevated) privileges.</span></span>
<span data-ttu-id="31059-124">Az elérhető parancsok gondos lehetőség kiválasztva fontos, hogy a JEA-végpont nem engedélyezi a csatlakozó felhasználó emelheti az engedélyeit.</span><span class="sxs-lookup"><span data-stu-id="31059-124">Careful selection of available commands is important to ensure the JEA endpoint does not allow the connecting user to elevate their permissions.</span></span>
<span data-ttu-id="31059-125">Az alábbiakban néhány példa, amely használható ártó szándékkal Ha engedélyezett korlátozás állapotban.</span><span class="sxs-lookup"><span data-stu-id="31059-125">Below are some examples of commands that can be used maliciously if allowed in an unconstrained state.</span></span>
<span data-ttu-id="31059-126">Vegye figyelembe, hogy ez nem egy kimerítően teljes lista, és csak a figyelmeztető kiindulási pontként használható.</span><span class="sxs-lookup"><span data-stu-id="31059-126">Note that this is not an exhaustive list and should only be used as a cautionary starting point.</span></span>

### <a name="examples-of-potentially-dangerous-commands"></a><span data-ttu-id="31059-127">Példák a potenciálisan veszélyes parancsok</span><span class="sxs-lookup"><span data-stu-id="31059-127">Examples of potentially dangerous commands</span></span>

<span data-ttu-id="31059-128">Kockázat</span><span class="sxs-lookup"><span data-stu-id="31059-128">Risk</span></span> | <span data-ttu-id="31059-129">Példa</span><span class="sxs-lookup"><span data-stu-id="31059-129">Example</span></span> | <span data-ttu-id="31059-130">Kapcsolódó parancsok</span><span class="sxs-lookup"><span data-stu-id="31059-130">Related commands</span></span>
-----|---------|-----------------
<span data-ttu-id="31059-131">A kapcsolódó felhasználó rendszergazdai jogosultságokat a JEA Mellőzés megadása</span><span class="sxs-lookup"><span data-stu-id="31059-131">Granting the connecting user admin privileges to bypass JEA</span></span> | `Add-LocalGroupMember -Member 'CONTOSO\jdoe' -Group 'Administrators'` | <span data-ttu-id="31059-132">`Add-ADGroupMember`, `Add-LocalGroupMember`, `net.exe`, `dsadd.exe`</span><span class="sxs-lookup"><span data-stu-id="31059-132">`Add-ADGroupMember`, `Add-LocalGroupMember`, `net.exe`, `dsadd.exe`</span></span>
<span data-ttu-id="31059-133">Tetszőleges kódot, például a kártevők, a biztonsági rések vagy a védelem megkerülésére egyéni parancsfájlok</span><span class="sxs-lookup"><span data-stu-id="31059-133">Running arbitrary code, such as malware, exploits, or custom scripts to bypass protections</span></span> | `Start-Process -FilePath '\\san\share\malware.exe'` | <span data-ttu-id="31059-134">`Start-Process`, `New-Service`, `Invoke-Item`, `Invoke-WmiMethod`, `Invoke-CimMethod`, `Invoke-Expression`, `Invoke-Command`, `New-ScheduledTask`, `Register-ScheduledJob`</span><span class="sxs-lookup"><span data-stu-id="31059-134">`Start-Process`, `New-Service`, `Invoke-Item`, `Invoke-WmiMethod`, `Invoke-CimMethod`, `Invoke-Expression`, `Invoke-Command`, `New-ScheduledTask`, `Register-ScheduledJob`</span></span>

## <a name="create-a-role-capability-file"></a><span data-ttu-id="31059-135">Hozzon létre egy szerepkört képesség fájlt</span><span class="sxs-lookup"><span data-stu-id="31059-135">Create a role capability file</span></span>

<span data-ttu-id="31059-136">Az új PowerShell-szerepkör képesség fájlt létrehozhatja a [New-PSRoleCapabilityFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSRoleCapabilityFile) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="31059-136">You can create a new PowerShell role capability file with the [New-PSRoleCapabilityFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSRoleCapabilityFile) cmdlet.</span></span>

```powershell
New-PSRoleCapabilityFile -Path .\MyFirstJEARole.psrc
```

<span data-ttu-id="31059-137">Az eredményül kapott szerepkör képesség fájl egy szövegszerkesztőben megnyitott és a kívánt parancsokat a szerepkör engedélyezéséhez módosítani kell.</span><span class="sxs-lookup"><span data-stu-id="31059-137">The resulting role capability file can be opened in a text editor and modified to allow the desired commands for the role.</span></span>
<span data-ttu-id="31059-138">A PowerShell súgójában számos példát, hogyan konfigurálhatja a fájl tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="31059-138">The PowerShell help documentation contains several examples of how you can configure the file.</span></span>

### <a name="allowing-powershell-cmdlets-and-functions"></a><span data-ttu-id="31059-139">PowerShell-parancsmagok és funkciók</span><span class="sxs-lookup"><span data-stu-id="31059-139">Allowing PowerShell cmdlets and functions</span></span>

<span data-ttu-id="31059-140">Való használatának engedélyezése a felhasználók PowerShell-parancsmagok vagy a függvények futtatását, adja hozzá a VisbibleCmdlets vagy VisibleFunctions mezőket a parancsmag vagy függvény neve.</span><span class="sxs-lookup"><span data-stu-id="31059-140">To authorize users to run PowerShell cmdlets or functions, add the cmdlet or function name to the VisbibleCmdlets or VisibleFunctions fields.</span></span>
<span data-ttu-id="31059-141">Ha nem tudja,-e a parancs a egy parancsmag vagy a funkciót, futtathatja `Get-Command <name>` , és ellenőrizze a "Parancstípus" tulajdonságot a kimenetben.</span><span class="sxs-lookup"><span data-stu-id="31059-141">If you aren't sure whether a command is a cmdlet or function, you can run `Get-Command <name>` and check the "CommandType" property in the output.</span></span>

```powershell
VisibleCmdlets = 'Restart-Computer', 'Get-NetIPAddress'
```

<span data-ttu-id="31059-142">Néha egy adott parancsmag vagy a funkció célja túl széleskörű, a felhasználók igényei szerint.</span><span class="sxs-lookup"><span data-stu-id="31059-142">Sometimes the scope of a specific cmdlet or function is too broad for your users' needs.</span></span>
<span data-ttu-id="31059-143">Egy DNS-rendszergazdai például valószínűleg csak igényeinek megfelelően elérni a DNS-szolgáltatás újraindítására.</span><span class="sxs-lookup"><span data-stu-id="31059-143">A DNS admin, for example, probably only needs access to restart the DNS service.</span></span>
<span data-ttu-id="31059-144">Egy több-bérlős környezetben, ahol a bérlők önkiszolgáló felügyeleti eszközök hozzáférést kapnak, a bérlők kell korlátozni kezelése a saját erőforrásaikat.</span><span class="sxs-lookup"><span data-stu-id="31059-144">In a multi-tenant environment where tenants are granted access to self-service management tools, tenants should be limited to managing with their own resources.</span></span>
<span data-ttu-id="31059-145">Ezekben az esetekben korlátozhatja a paramétereket a parancsmag vagy a funkció teszi közzé.</span><span class="sxs-lookup"><span data-stu-id="31059-145">For these cases, you can restrict which parameters are exposed from the cmdlet or function.</span></span>

```powershell

VisibleCmdlets = @{ Name = 'Restart-Computer'; Parameters = @{ Name = 'Name' }}

```

<span data-ttu-id="31059-146">A speciális esetben is szükség lehet mely értékeket adhat meg valaki korlátozhatja a ezeket a paramétereket.</span><span class="sxs-lookup"><span data-stu-id="31059-146">In more advanced scenarios, you may also need to restrict which values someone can supply to these parameters.</span></span>
<span data-ttu-id="31059-147">Szerepköri funkciók segítségével meghatározhatja a megengedett értékek vagy a meghatározásához, hogy engedélyezett-e a megadott bemeneti kiértékelt Reguláriskifejezés-mintának.</span><span class="sxs-lookup"><span data-stu-id="31059-147">Role capabilities let you define a set of allowed values or a regular expression pattern that is evaluated to determine if a given input is allowed.</span></span>

```powershell
VisibleCmdlets = @{ Name = 'Restart-Service'; Parameters = @{ Name = 'Name'; ValidateSet = 'Dns', 'Spooler' }},
                 @{ Name = 'Start-Website'; Parameters = @{ Name = 'Name'; ValidatePattern = 'HR_*' }}
```

> [!NOTE]
> <span data-ttu-id="31059-148">A [gyakori PowerShell-paramétereket](https://technet.microsoft.com/library/hh847884.aspx) mindig engedélyezett, még akkor is, ha a rendelkezésre álló paraméterek korlátozza.</span><span class="sxs-lookup"><span data-stu-id="31059-148">The [common PowerShell parameters](https://technet.microsoft.com/library/hh847884.aspx) are always allowed, even if you restrict the available parameters.</span></span>
> <span data-ttu-id="31059-149">Nem explicit módon sorolja fel azokat a paramétereket mezőben.</span><span class="sxs-lookup"><span data-stu-id="31059-149">You should not explicitly list them in the Parameters field.</span></span>

<span data-ttu-id="31059-150">Az alábbi táblázat ismerteti a különböző módszereket testre szabhatja a látható parancsmag vagy függvény.</span><span class="sxs-lookup"><span data-stu-id="31059-150">The table below describes the various ways you can customize a visible cmdlet or function.</span></span>
<span data-ttu-id="31059-151">Szabadon kombinálhatók felel meg az alábbi a VisibleCmdlets mezőbe.</span><span class="sxs-lookup"><span data-stu-id="31059-151">You can mix and match any of the below in the VisibleCmdlets field.</span></span>

<span data-ttu-id="31059-152">Példa</span><span class="sxs-lookup"><span data-stu-id="31059-152">Example</span></span>                                                                                      | <span data-ttu-id="31059-153">Használati eset</span><span class="sxs-lookup"><span data-stu-id="31059-153">Use case</span></span>
---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------
<span data-ttu-id="31059-154">`'My-Func'` vagy `@{ Name = 'My-Func' }`</span><span class="sxs-lookup"><span data-stu-id="31059-154">`'My-Func'` or `@{ Name = 'My-Func' }`</span></span>                                                       | <span data-ttu-id="31059-155">Lehetővé teszi a felhasználó futtatásához `My-Func` paramétereknek korlátozása nélkül.</span><span class="sxs-lookup"><span data-stu-id="31059-155">Allows the user to run `My-Func` without any restrictions on the parameters.</span></span>
`'MyModule\My-Func'`                                                                         | <span data-ttu-id="31059-156">Lehetővé teszi a felhasználó futtatásához `My-Func` modulból `MyModule` paramétereknek korlátozása nélkül.</span><span class="sxs-lookup"><span data-stu-id="31059-156">Allows the user to run `My-Func` from the module `MyModule` without any restrictions on the parameters.</span></span>
`'My-*'`                                                                                     | <span data-ttu-id="31059-157">Lehetővé teszi a felhasználó bármely parancsmag vagy a funkció futtatását a művelettel `My`.</span><span class="sxs-lookup"><span data-stu-id="31059-157">Allows the user to run any cmdlet or function with the verb `My`.</span></span>
`'*-Func'`                                                                                   | <span data-ttu-id="31059-158">Lehetővé teszi, hogy a felhasználót, hogy a főnév futtassa bármely parancsmag vagy függvény `Func`.</span><span class="sxs-lookup"><span data-stu-id="31059-158">Allows the user to run any cmdlet or function with the noun `Func`.</span></span>
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'}, @{ Name = 'Param2' }}`               | <span data-ttu-id="31059-159">Lehetővé teszi a felhasználó futtatásához `My-Func` együtt a `Param1` és/vagy `Param2` paramétereket.</span><span class="sxs-lookup"><span data-stu-id="31059-159">Allows the user to run `My-Func` with the `Param1` and/or `Param2` parameters.</span></span> <span data-ttu-id="31059-160">Bármilyen érték lehet biztosítani a paraméterekhez.</span><span class="sxs-lookup"><span data-stu-id="31059-160">Any value can be supplied to the parameters.</span></span>
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidateSet = 'Value1', 'Value2' }}`  | <span data-ttu-id="31059-161">Lehetővé teszi a felhasználó futtatásához `My-Func` együtt a `Param1` paraméter.</span><span class="sxs-lookup"><span data-stu-id="31059-161">Allows the user to run `My-Func` with the `Param1` parameter.</span></span> <span data-ttu-id="31059-162">Csak a "Érték1" és "Érték2" a paraméter lehet biztosítani.</span><span class="sxs-lookup"><span data-stu-id="31059-162">Only "Value1" and "Value2" can be supplied to the parameter.</span></span>
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidatePattern = 'contoso.*' }}`     | <span data-ttu-id="31059-163">Lehetővé teszi a felhasználó futtatásához `My-Func` együtt a `Param1` paraméter.</span><span class="sxs-lookup"><span data-stu-id="31059-163">Allows the user to run `My-Func` with the `Param1` parameter.</span></span> <span data-ttu-id="31059-164">"Contoso" kezdetű bármilyen érték lehet biztosítani a paraméterhez.</span><span class="sxs-lookup"><span data-stu-id="31059-164">Any value starting with "contoso" can be supplied to the parameter.</span></span>


> [!WARNING]
> <span data-ttu-id="31059-165">Az ajánlott biztonsági eljárások nem ajánlott a helyettesítő karakterek használata látható parancsmagok és funkciók meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="31059-165">For best security practices, it is not recommended to use wildcards when defining visible cmdlets or functions.</span></span>
> <span data-ttu-id="31059-166">Ehelyett minden egyes megbízható parancsot annak biztosítására, hogy véletlenül jogosultak a többi parancs, amely ugyanazt a elnevezési sémát használja explicit módon listája.</span><span class="sxs-lookup"><span data-stu-id="31059-166">Instead, you should explicitly list each trusted command to ensure no other commands that share the same naming scheme are unintentionally authorized.</span></span>

<span data-ttu-id="31059-167">Egy parancsmag vagy függvény nem tudja alkalmazni a ValidatePattern és ValidateSet is.</span><span class="sxs-lookup"><span data-stu-id="31059-167">You cannot apply both a ValidatePattern and ValidateSet to the same cmdlet or function.</span></span>

<span data-ttu-id="31059-168">Ha így tesz, a ValidatePattern felülírja a ValidateSet.</span><span class="sxs-lookup"><span data-stu-id="31059-168">If you do, the ValidatePattern will override the ValidateSet.</span></span>

<span data-ttu-id="31059-169">ValidatePattern kapcsolatos további információkért tekintse meg [ez *Hey, Scripting Guy!* közzététele](https://blogs.technet.microsoft.com/heyscriptingguy/2011/01/11/validate-powershell-parameters-before-running-the-script/) és a [PowerShell reguláris kifejezések](https://technet.microsoft.com/library/hh847880.aspx) referenciákra.</span><span class="sxs-lookup"><span data-stu-id="31059-169">For more information about ValidatePattern, check out [this *Hey, Scripting Guy!* post](https://blogs.technet.microsoft.com/heyscriptingguy/2011/01/11/validate-powershell-parameters-before-running-the-script/) and the [PowerShell Regular Expressions](https://technet.microsoft.com/library/hh847880.aspx) reference content.</span></span>

### <a name="allowing-external-commands-and-powershell-scripts"></a><span data-ttu-id="31059-170">Lehetővé teszi a külső parancsok és a PowerShell-parancsprogramok</span><span class="sxs-lookup"><span data-stu-id="31059-170">Allowing external commands and PowerShell scripts</span></span>

<span data-ttu-id="31059-171">Ahhoz, hogy a felhasználók számára a végrehajtható fájlok és a PowerShell-parancsfájlok (.ps1) futtassa a JEA-munkamenetben, fel kell vennie a teljes elérési útja az egyes programokat a VisibleExternalCommands mezőben.</span><span class="sxs-lookup"><span data-stu-id="31059-171">To allow users to run executables and PowerShell scripts (.ps1) in a JEA session, you have to add the full path to each program in the VisibleExternalCommands field.</span></span>

```powershell
VisibleExternalCommands = 'C:\Windows\System32\whoami.exe', 'C:\Program Files\Contoso\Scripts\UpdateITSoftware.ps1'
```

<span data-ttu-id="31059-172">Javasolt, ha lehetséges, a PowerShell parancsmag/függvény megfelelője, külső végrehajtható fájlokat is engedélyezni szeretné, mivel azt szabályozza, amely fölött paramétereket a PowerShell-parancsmagok és funkciók használatára.</span><span class="sxs-lookup"><span data-stu-id="31059-172">It is advised, where possible, to use PowerShell cmdlet/function equivalents of any external executables you authorize since you have control over which parameters are allowed with PowerShell cmdlets/functions.</span></span>

<span data-ttu-id="31059-173">Számos végrehajtható fájlok lehetővé teszik az aktuális állapot olvasására és majd módosítsa azt csak a különböző paraméterek megadásával.</span><span class="sxs-lookup"><span data-stu-id="31059-173">Many executables allow you to both read the current state and then change it just by providing different parameters.</span></span>

<span data-ttu-id="31059-174">Vegyük példaként egy fájlt, ellenőrizze, hogy mely hálózati megosztások a helyi számítógép által üzemeltetett szeretné kiszolgálói rendszergazda szerepe.</span><span class="sxs-lookup"><span data-stu-id="31059-174">For example, consider the role of a file server admin who wants to check which network shares are hosted by the local machine.</span></span>
<span data-ttu-id="31059-175">Ellenőrizze, hogy egy módja `net share`.</span><span class="sxs-lookup"><span data-stu-id="31059-175">One way to check is to use `net share`.</span></span>
<span data-ttu-id="31059-176">Azonban, így a net.exe nagyon súlyos, mert a rendszergazda sikerült ugyanilyen egyszerűen használja a parancsot a rendszergazdai jogosultságokat kapjanak `net group Administrators unprivilegedjeauser /add`.</span><span class="sxs-lookup"><span data-stu-id="31059-176">However, allowing net.exe is very dangerous becuase the admin could just as easily use the command to gain admin privileges with `net group Administrators unprivilegedjeauser /add`.</span></span>
<span data-ttu-id="31059-177">Jobb módszer, hogy lehetővé tegyék [Get-SmbShare](https://technet.microsoft.com/library/jj635704.aspx) amely ugyanazt az eredményt éri el, de korlátozottabb hatóköre.</span><span class="sxs-lookup"><span data-stu-id="31059-177">A better approach is to allow [Get-SmbShare](https://technet.microsoft.com/library/jj635704.aspx) which achieves the same result but has a much more limited scope.</span></span>

<span data-ttu-id="31059-178">Külső parancsok elérhetővé tétele a felhasználók számára a JEA-munkamenetben, mindig adjon meg egy hasonlóan elnevezett (és potenciálisan malicous) program máshol helyezhető el a rendszer nem végrehajtásra kerülhetnek inkább biztosításához a végrehajtható fájl teljes elérési útja.</span><span class="sxs-lookup"><span data-stu-id="31059-178">When making external commands available to users in a JEA session, always specify the complete path to the executable to ensure a similarly named (and potentially malicous) program placed elsewhere on the system does not get executed instead.</span></span>

### <a name="allowing-access-to-powershell-providers"></a><span data-ttu-id="31059-179">Engedélyezi a hozzáférést a PowerShell-szolgáltatók</span><span class="sxs-lookup"><span data-stu-id="31059-179">Allowing access to PowerShell providers</span></span>

<span data-ttu-id="31059-180">Alapértelmezés szerint nem PowerShell-szolgáltatók a JEA-munkamenetek érhető el.</span><span class="sxs-lookup"><span data-stu-id="31059-180">By default, no PowerShell providers are available in JEA sessions.</span></span>

<span data-ttu-id="31059-181">Ez az elsősorban bizalmas információkat és adatokat tesznek közzé a csatlakozó felhasználó beállításainak kockázatának csökkentése érdekében.</span><span class="sxs-lookup"><span data-stu-id="31059-181">This is primarily to reduce the risk of sensitive information and configuration settings being disclosed to the connecting user.</span></span>

<span data-ttu-id="31059-182">Ha szükséges, a PowerShell-szolgáltató használatával hozzáférést biztosíthat a `VisibleProviders` parancsot.</span><span class="sxs-lookup"><span data-stu-id="31059-182">When necessary, you can allow access to the PowerShell providers using the `VisibleProviders` command.</span></span>
<span data-ttu-id="31059-183">Szolgáltatók teljes listájának megtekintéséhez futtassa az alábbi parancsot `Get-PSProvider`.</span><span class="sxs-lookup"><span data-stu-id="31059-183">For a full list of providers, run `Get-PSProvider`.</span></span>

```powershell
VisibleProviders = 'Registry'
```

<span data-ttu-id="31059-184">A fájlrendszer, a beállításjegyzék, a tanúsítványtároló vagy a más bizalmas szolgáltatók hozzáférést igénylő egyszerű feladatok is érdemes lehet egyéni függvény, amely együttműködik a szolgáltató, a felhasználó nevében írása.</span><span class="sxs-lookup"><span data-stu-id="31059-184">For simple tasks that require access to the file system, registry, certificate store, or other sensitive providers, you can also consider writing a custom function that works with the provider on the user's behalf.</span></span>
<span data-ttu-id="31059-185">Funkciók, a parancsmagok és a egy JEA munkamenetben rendelkezésre álló külső programok nem vonatkozik a JEA azonos kötöttségek – alapértelmezés szerint hozzáférhet a bármely szolgáltatónál.</span><span class="sxs-lookup"><span data-stu-id="31059-185">Functions, cmdlets, and external programs that are available in a JEA session are not subject to the same constraints as JEA -- they can access any provider by default.</span></span>
<span data-ttu-id="31059-186">Megfontolni a [felhasználói meghajtó](session-configurations.md#user-drive) amikor fájlokat másol és- tárolókról a JEA-végpont megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="31059-186">Also consider using the [user drive](session-configurations.md#user-drive) when copying files to/from a JEA endpoint is required.</span></span>

### <a name="creating-custom-functions"></a><span data-ttu-id="31059-187">Egyéni függvények létrehozása</span><span class="sxs-lookup"><span data-stu-id="31059-187">Creating custom functions</span></span>

<span data-ttu-id="31059-188">Egy szerepkör képesség fájlban, az összetett feladatok egyszerűbbé tétele a végfelhasználók számára az egyéni függvények hozhat létre.</span><span class="sxs-lookup"><span data-stu-id="31059-188">You can author custom functions in a role capability file to simplify complex tasks for your end users.</span></span>
<span data-ttu-id="31059-189">Egyéni funkciók is hasznosak, ha speciális ellenőrzési logika parancsmag paraméterértékeket.</span><span class="sxs-lookup"><span data-stu-id="31059-189">Custom functions are also useful when you require advanced validation logic for cmdlet parameter values.</span></span>
<span data-ttu-id="31059-190">Egyszerű funkciók írhat a **FunctionDefinitions** mező:</span><span class="sxs-lookup"><span data-stu-id="31059-190">You can write simple functions in the **FunctionDefinitions** field:</span></span>

```powershell
VisibleFunctions = 'Get-TopProcess'

FunctionDefinitions = @{
    Name = 'Get-TopProcess'

    ScriptBlock = {
        param($Count = 10)

        Get-Process | Sort-Object -Property CPU -Descending | Microsoft.PowerShell.Utility\Select-Object -First $Count
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="31059-191">Ne felejtse el hozzáadni az egyéni függvények nevét a **VisibleFunctions** mezőt, így a JEA-felhasználók által futtatható.</span><span class="sxs-lookup"><span data-stu-id="31059-191">Don't forget to add the name of your custom functions to the **VisibleFunctions** field so they can be run by the JEA users.</span></span>


<span data-ttu-id="31059-192">Egyéni függvény törzsében (parancsfájl-blokk) a rendszer az alapértelmezett nyelv módját fut, és nem a JEA nyelvi korlátozások vonatkoznak.</span><span class="sxs-lookup"><span data-stu-id="31059-192">The body (script block) of custom functions runs in the default language mode for the system and is not subject to JEA's language constraints.</span></span>
<span data-ttu-id="31059-193">Ez azt jelenti, hogy funkciók is fájlrendszert és beállításjegyzéket, majd futtassa a parancsokat elvégzett nem látható a szerepkör képesség fájlban.</span><span class="sxs-lookup"><span data-stu-id="31059-193">This means that functions can access the file system and registry, and run commands that were not made visible in the role capability file.</span></span>
<span data-ttu-id="31059-194">Ügyeljen arra, hogy kerülje, lehetővé téve tetszőleges kód futtatható, ha a paraméterek használatával, és elkerülheti az átirányítás felhasználói bevitel közvetlenül be például a parancsmagok `Invoke-Expression`.</span><span class="sxs-lookup"><span data-stu-id="31059-194">Take care to avoid allowing arbitrary code to be run when using parameters and avoid piping user input directly into cmdlets like `Invoke-Expression`.</span></span>

<span data-ttu-id="31059-195">A fenti példában megfigyelheti, hogy a modul teljesen minősített nevét (FQMN) `Microsoft.PowerShell.Utility\Select-Object` helyett a gyorsírás használt `Select-Object`.</span><span class="sxs-lookup"><span data-stu-id="31059-195">In the above example, you will notice that the fully qualified module name (FQMN) `Microsoft.PowerShell.Utility\Select-Object` was used instead of the shorthand `Select-Object`.</span></span>
<span data-ttu-id="31059-196">Szerepkör képesség fájlban meghatározott függvényeket továbbra is vonatkozik JEA munkamenetek, amely tartalmazza a proxy funkciók hatókörének korlátozásához a meglévő parancsok JEA hoz létre.</span><span class="sxs-lookup"><span data-stu-id="31059-196">Functions defined in role capability files are still subject to the scope of JEA sessions, which includes the proxy functions JEA creates to constrain existing commands.</span></span>

<span data-ttu-id="31059-197">Select-Object a egy alapértelmezett, korlátozott parancsmag az összes JEA-munkamenetekben, amelyek nem teszik lehetővé tetszőleges tulajdonságok objektumok kiválasztása.</span><span class="sxs-lookup"><span data-stu-id="31059-197">Select-Object is a default, constrained cmdlet in all JEA sessions that doesn't allow you to select arbitrary properties on objects.</span></span>
<span data-ttu-id="31059-198">A korlátozás Select-Object az funkciók használatához explicit módon a FQMN megadásával kell igényelnie a teljes megvalósítás.</span><span class="sxs-lookup"><span data-stu-id="31059-198">To use the unconstrained Select-Object in functions, you must explicitly request the full implementation by specifying the FQMN.</span></span>
<span data-ttu-id="31059-199">A JEA munkamenetben korlátozott parancsmagokhoz fog ugyanígy viselkednek, a PowerShell megfelelően függvény meghívásakor [elsőbbséget parancs](https://msdn.microsoft.com/powershell/reference/3.0/microsoft.powershell.core/about/about_command_precedence).</span><span class="sxs-lookup"><span data-stu-id="31059-199">Any constrained cmdlet in a JEA session will exhibit the same behavior when invoked from a function, in line with PowerShell's [command precedence](https://msdn.microsoft.com/powershell/reference/3.0/microsoft.powershell.core/about/about_command_precedence).</span></span>

<span data-ttu-id="31059-200">Ha egyéni függvények rengeteg, állítsa őket az egyszerűbb lehet egy [PowerShell-parancsfájl modul](https://msdn.microsoft.com/library/dd878340(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="31059-200">If you are writing a lot of custom functions, it may be easier to put them in a [PowerShell Script Module](https://msdn.microsoft.com/library/dd878340(v=vs.85).aspx).</span></span>
<span data-ttu-id="31059-201">Majd ezekhez a függvényekhez láthatóvá teheti a JEA-munkamenet VisibleFunctions mező használatával, mint a beépített és külső modulok.</span><span class="sxs-lookup"><span data-stu-id="31059-201">You can then make those functions visible in the JEA session using the VisibleFunctions field like you would with built-in and third party modules.</span></span>

## <a name="place-role-capabilities-in-a-module"></a><span data-ttu-id="31059-202">Szerepköri funkciók helyezze egy modulban</span><span class="sxs-lookup"><span data-stu-id="31059-202">Place role capabilities in a module</span></span>

<span data-ttu-id="31059-203">Ahhoz, hogy a PowerShell-lel szerepkör képesség fájl található, az azt kell tárolni egy PowerShell-modul a "RoleCapabilities" mappájában.</span><span class="sxs-lookup"><span data-stu-id="31059-203">In order for PowerShell to find a role capability file, it must be stored in a "RoleCapabilities" folder in a PowerShell module.</span></span>
<span data-ttu-id="31059-204">A modul bármelyik mappájában található tárolhatók a `$env:PSModulePath` környezeti változót, azonban ne jelölje azt a System32 (beépített modulok számára fenntartott) vagy egy mappában, a nem megbízható, csatlakozás a felhasználók módosíthatják a fájlok.</span><span class="sxs-lookup"><span data-stu-id="31059-204">The module can be stored in any folder included in the `$env:PSModulePath` environment variable, however you should not place it in System32 (reserved for built-in modules) or a folder where the untrusted, connecting users could modify the files.</span></span>
<span data-ttu-id="31059-205">Az alábbi példában egy egyszerű PowerShell parancsfájl modul nevű létrehozásának, *ContosoJEA* a "Program Files" elérési úton.</span><span class="sxs-lookup"><span data-stu-id="31059-205">Below is an example of creating a basic PowerShell script module called *ContosoJEA* in the "Program Files" path.</span></span>

```powershell
# Create a folder for the module
$modulePath = Join-Path $env:ProgramFiles "WindowsPowerShell\Modules\ContosoJEA"
New-Item -ItemType Directory -Path $modulePath

# Create an empty script module and module manifest. At least one file in the module folder must have the same name as the folder itself.
New-Item -ItemType File -Path (Join-Path $modulePath "ContosoJEAFunctions.psm1")
New-ModuleManifest -Path (Join-Path $modulePath "ContosoJEA.psd1") -RootModule "ContosoJEAFunctions.psm1"

# Create the RoleCapabilities folder and copy in the PSRC file
$rcFolder = Join-Path $modulePath "RoleCapabilities"
New-Item -ItemType Directory $rcFolder
Copy-Item -Path .\MyFirstJEARole.psrc -Destination $rcFolder
```

<span data-ttu-id="31059-206">Lásd: [egy PowerShell-modul ismertetése](https://msdn.microsoft.com/library/dd878324.aspx) PowerShell modulok, a modul jegyzékek és a PSModulePath környezeti változó további információt.</span><span class="sxs-lookup"><span data-stu-id="31059-206">See [Understanding a PowerShell Module](https://msdn.microsoft.com/library/dd878324.aspx) for more information about PowerShell modules, module manifests, and the PSModulePath environment variable.</span></span>

## <a name="updating-role-capabilities"></a><span data-ttu-id="31059-207">Szerepköri funkciók frissítése</span><span class="sxs-lookup"><span data-stu-id="31059-207">Updating role capabilities</span></span>


<span data-ttu-id="31059-208">Egyszerűen módosításainak mentése folyamatban van a szerepkör képesség fájl által bármikor frissítheti egy szerepkör képesség fájlt.</span><span class="sxs-lookup"><span data-stu-id="31059-208">You can update a role capability file at any time by simply saving changes to the role capability file.</span></span>
<span data-ttu-id="31059-209">Minden olyan új JEA munkamenetek, a szerepkör funkció frissítése után elindult a módosított képességek fogja tartalmazni.</span><span class="sxs-lookup"><span data-stu-id="31059-209">Any new JEA sessions started after the role capability has been updated will reflect the revised capabilities.</span></span>

<span data-ttu-id="31059-210">Ezért a szerepkörrel képességeket mappa hozzáférés szabályozása, ezért fontos.</span><span class="sxs-lookup"><span data-stu-id="31059-210">This is why controlling access to the role capabilities folder is so important.</span></span>
<span data-ttu-id="31059-211">Kizárólag megbízható rendszergazdák tudják módosítani a szerepkör képesség fájlokat kell lennie.</span><span class="sxs-lookup"><span data-stu-id="31059-211">Only highly trusted administrators should be able to change role capability files.</span></span>
<span data-ttu-id="31059-212">Nem megbízható felhasználók módosíthatják a szerepkör képesség fájlokat, ha azok segítségével könnyedén magukat hozzáférést biztosíthat parancsmagok, amelyek lehetővé teszik a jogosultságai kibővítésére őket.</span><span class="sxs-lookup"><span data-stu-id="31059-212">If an untrusted user can change role capability files, they can easily give themselves access to cmdlets which allow them to elevate their privileges.</span></span>


<span data-ttu-id="31059-213">A rendszergazdáknak a szerepkör lehetőségekhez zároljuk szeretne győződjön meg arról, helyi rendszer szerepkör képesség fájlokat és tartalmazó modulok olvasási hozzáféréssel rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="31059-213">For administrators looking to lock down access to the role capabilities, ensure Local System has read access to the role capability files and containing modules.</span></span>

## <a name="how-role-capabilities-are-merged"></a><span data-ttu-id="31059-214">Szerepköri funkciók hogyan egyesítésekor</span><span class="sxs-lookup"><span data-stu-id="31059-214">How role capabilities are merged</span></span>

<span data-ttu-id="31059-215">Felhasználók számára hozzáférés engedélyezhető több szerepkörrel képességeket, amikor belép a JEA munkamenet függően a szerepkör-hozzárendelések a [munkamenet konfigurációs fájl](session-configurations.md).</span><span class="sxs-lookup"><span data-stu-id="31059-215">Users can be granted access to multiple role capabilities when they enter a JEA session depending on the role mappings in the [session configuration file](session-configurations.md).</span></span>
<span data-ttu-id="31059-216">Ha ez történik, a JEA próbál-e a felhasználónak, a *legmegengedőbb* valamelyik szerepkörnél által engedélyezett parancsokat.</span><span class="sxs-lookup"><span data-stu-id="31059-216">When this happens, JEA tries to give the user the *most permissive* set of commands allowed by any of the roles.</span></span>

<span data-ttu-id="31059-217">**VisibleCmdlets és VisibleFunctions**</span><span class="sxs-lookup"><span data-stu-id="31059-217">**VisibleCmdlets and VisibleFunctions**</span></span>

<span data-ttu-id="31059-218">A legösszetettebb egyesítési logikai hatással van a parancsmagok és a függvények, amelyek a paramétereket és a paraméterértékek a JEA korlátozott lehet.</span><span class="sxs-lookup"><span data-stu-id="31059-218">The most complex merge logic affects cmdlets and functions, which can have their parameters and parameter values limited in JEA.</span></span>

<span data-ttu-id="31059-219">A szabályok a következők:</span><span class="sxs-lookup"><span data-stu-id="31059-219">The rules are as follows:</span></span>

1. <span data-ttu-id="31059-220">Ha a parancsmag csak akkor jelenik meg egy szerepkör, a bármely alkalmazandó paraméter megkötésekkel rendelkező felhasználó számára látható lesz.</span><span class="sxs-lookup"><span data-stu-id="31059-220">If a cmdlet is only made visible in one role, it will be visible to the user with any applicable parameter constraints.</span></span>
2. <span data-ttu-id="31059-221">A parancsmag láthatóvá válik a több szerepkört, és mindegyik szerepkör tartalmazza a parancsmag azonos korlátait, a parancsmag az adott megkötésekkel rendelkező felhasználó számára látható lesz.</span><span class="sxs-lookup"><span data-stu-id="31059-221">If a cmdlet is made visible in more than one role, and each role has the same constraints on the cmdlet, the cmdlet will be visible to the user with those constraints.</span></span>
3. <span data-ttu-id="31059-222">Ha a parancsmag láthatóvá válik a több szerepkört, és minden egyes szerepkör lehetővé teszi, hogy a paraméterek külön készletét, a parancsmag és az összes megadott paraméterek között minden szerepkör lesz a felhasználó számára látható.</span><span class="sxs-lookup"><span data-stu-id="31059-222">If a cmdlet is made visible in more than one role, and each role allows a different set of parameters, the cmdlet and all of the parameters defined across every role will be visible to the user.</span></span> <span data-ttu-id="31059-223">Ha egy szerepkör nem rendelkezik a paraméterek korlátait, minden paraméter engedélyezett lesz.</span><span class="sxs-lookup"><span data-stu-id="31059-223">If one role doesn't have constraints on the parameters, all parameters will be allowed.</span></span>
4. <span data-ttu-id="31059-224">Ha egy szerepkör ellenőrzése set vagy egy parancsmag-paraméterben ellenőrzése mintája határoz meg, és a többi szerepkör lehetővé teszi, hogy a paraméter, de nem korlátozza a paraméterértékeket, ellenőrzése beállított vagy minta figyelmen kívül.</span><span class="sxs-lookup"><span data-stu-id="31059-224">If one role defines a validate set or validate pattern for a cmdlet parameter, and the other role allows the parameter but does not constrain the parameter values, the validate set or pattern will be ignored.</span></span>
5. <span data-ttu-id="31059-225">Ha egy ellenőrzés beállítása egynél több szerepkör ugyanazon parancsmag paraméter meg van adva, minden érték ellenőrzése minden portprofilkészletéből engedélyezett lesz.</span><span class="sxs-lookup"><span data-stu-id="31059-225">If a validate set is defined for the same cmdlet parameter in more than one role, all values from all validate sets will be allowed.</span></span>
6. <span data-ttu-id="31059-226">Ha az érvényesítés mintát egynél több szerepkör ugyanazon parancsmag paraméter van megadva, azokat az értékeket, a minták megfelelő engedélyezett lesz.</span><span class="sxs-lookup"><span data-stu-id="31059-226">If a validate pattern is defined for the same cmdlet parameter in more than one role, any values that match any of the patterns will be allowed.</span></span>
7. <span data-ttu-id="31059-227">Egy ellenőrzés beállítása van meghatározva egy vagy több szerepkört, és ugyanezt a parancsmagot paramétert egy másik szerepkör ellenőrzése mintát van definiálva, az ellenőrzés beállítása a rendszer figyelmen kívül hagyja, és (6) a szabály vonatkozik a fennmaradó ellenőrzése minták.</span><span class="sxs-lookup"><span data-stu-id="31059-227">If a validate set is defined in one or more roles, and a validate pattern is defined in another role for the same cmdlet parameter, the validate set is ignored and rule (6) applies to the remaining validate patterns.</span></span>

<span data-ttu-id="31059-228">Alább egy példát, hogyan szerepkörök egyesítésekor ezek a szabályok megfelelően van:</span><span class="sxs-lookup"><span data-stu-id="31059-228">Below is an example of how roles are merged according to these rules:</span></span>

```powershell
# Role A Visible Cmdlets
$roleA = @{
    VisibleCmdlets = 'Get-Service',
                     @{ Name = 'Restart-Service'; Parameters = @{ Name = 'DisplayName'; ValidateSet = 'DNS Client' } }
}

# Role B Visible Cmdlets
$roleB = @{
    VisibleCmdlets = @{ Name = 'Get-Service'; Parameters = @{ Name = 'DisplayName'; ValidatePattern = 'DNS.*' } },
                     @{ Name = 'Restart-Service'; Parameters = @{ Name = 'DisplayName'; ValidateSet = 'DNS Server' } }
}

# Resulting permisisons for a user who belongs to both role A and B
# - The constraint in role B for the DisplayName parameter on Get-Service is ignored becuase of rule #4
# - The ValidateSets for Restart-Service are merged because both roles use ValidateSet on the same parameter per rule #5
$mergedAandB = @{
    VisibleCmdlets = 'Get-Service',
                     @{ Name = 'Restart-Service'; Parameters = @{ Name = 'DisplayName'; ValidateSet = 'DNS Client', 'DNS Server' } }
}
```



<span data-ttu-id="31059-229">**VisibleExternalCommands, VisibleAliases, VisibleProviders, ScriptsToProcess**</span><span class="sxs-lookup"><span data-stu-id="31059-229">**VisibleExternalCommands, VisibleAliases, VisibleProviders, ScriptsToProcess**</span></span>

<span data-ttu-id="31059-230">A szerepkör képesség fájlban a többi mező egyszerűen kerülnek engedélyezett külső parancsok, aliasok, szolgáltatók és az indítási parancsfájlok összesített csoportja.</span><span class="sxs-lookup"><span data-stu-id="31059-230">All other fields in the role capability file are simply added to a cumulative set of allowable external commands, aliases, providers, and startup scripts.</span></span>
<span data-ttu-id="31059-231">Minden parancs, a alias, a szolgáltató vagy a parancsfájl egy szerepkör képesség érhető el a JEA-felhasználó számára elérhető lesz.</span><span class="sxs-lookup"><span data-stu-id="31059-231">Any command, alias, provider, or script available in one role capability will be available to the JEA user.</span></span>

<span data-ttu-id="31059-232">Ügyeljen arra, hogy ellenőrizze, hogy a szolgáltatók egy kombinált készletét szerepkörrel képességeket és a parancsmagok és funkciók/parancsok egy másik nem csatlakozó felhasználók véletlen erőforrások hozzáférésének engedélyezéséhez rendszer.</span><span class="sxs-lookup"><span data-stu-id="31059-232">Be careful to ensure that the combined set of providers from one role capability and cmdlets/functions/commands from another do not allow connecting users unintentional access to system resources.</span></span>
<span data-ttu-id="31059-233">Például, ha egy szerepkör lehetővé teszi a `Remove-Item` parancsmag és a egy másik lehetővé teszi, hogy a `FileSystem` szolgáltató, vannak kockázata, hogy a JEA felhasználó törlése tetszőleges fájlokat a számítógépre.</span><span class="sxs-lookup"><span data-stu-id="31059-233">For example, if one role allows the `Remove-Item` cmdlet and another allows the `FileSystem` provider, you are at risk of a JEA user deleting arbitrary files on your computer.</span></span>
<span data-ttu-id="31059-234">További információ a felhasználók érvényes engedélyeit azonosító megtalálható a [JEA témakört naplózás](audit-and-report.md).</span><span class="sxs-lookup"><span data-stu-id="31059-234">Additional information about identifying users' effective permissions can be found in the [auditing JEA topic](audit-and-report.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31059-235">További lépések</span><span class="sxs-lookup"><span data-stu-id="31059-235">Next steps</span></span>

- [<span data-ttu-id="31059-236">Egy munkamenet-konfigurációs fájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="31059-236">Create a session configuration file</span></span>](session-configurations.md)