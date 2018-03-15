---
ms.date: 2017-06-12
author: rpsqrd
ms.topic: conceptual
keywords: "jea, a powershell, a biztonsági"
title: "JEA szerepkör képességek"
ms.openlocfilehash: 083cab3b44348168fe20e8355f5076b28be78702
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="jea-role-capabilities"></a><span data-ttu-id="df872-103">JEA szerepkör képességek</span><span class="sxs-lookup"><span data-stu-id="df872-103">JEA Role Capabilities</span></span>

> <span data-ttu-id="df872-104">A következőkre vonatkozik: a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="df872-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="df872-105">A JEA-végpont létrehozása, ha szüksége lesz legalább "szerepkör képességek", amelyeket meghatározásához *mi* valaki teheti meg egy JEA-munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="df872-105">When creating a JEA endpoint, you will need to define one or more "role capabilities" which describe *what* someone can do in a JEA session.</span></span>
<span data-ttu-id="df872-106">Egy szerepkör képesség, a parancsmagok, függvények, szolgáltatók, és biztosítani kell a Kapcsolódás a felhasználók külső programok .psrc kiterjesztésű PowerShell adatfájlt.</span><span class="sxs-lookup"><span data-stu-id="df872-106">A role capability is a PowerShell data file with the .psrc extension that lists all the cmdlets, functions, providers, and external programs that should be made available to connecting users.</span></span>

<span data-ttu-id="df872-107">Ez a témakör ismerteti, hogyan JEA szinkronizálásával PowerShell szerepkör funkció fájl létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="df872-107">This topic describes how to create a PowerShell role capability file for your JEA users.</span></span>

## <a name="determine-which-commands-to-allow"></a><span data-ttu-id="df872-108">Határozza meg, mely parancsok engedélyezése</span><span class="sxs-lookup"><span data-stu-id="df872-108">Determine which commands to allow</span></span>

<span data-ttu-id="df872-109">Az első lépés, amikor a szerepkör funkció fájl létrehozásakor fontolja meg, mi a felhasználókat, akik a szerepkör hozzáféréssel kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="df872-109">The first step when creating a role capability file is to consider what the users who are assigned the role will need access to.</span></span>
<span data-ttu-id="df872-110">Az adatgyűjtési folyamatot követelmények időt vehet igénybe, de egy rendkívül fontos folyamat.</span><span class="sxs-lookup"><span data-stu-id="df872-110">This requirements gathering process can take a while, but it is a very important process.</span></span>
<span data-ttu-id="df872-111">Mivel a felhasználók számára hozzáférést a túl kevés parancsmag és funkció is megakadályozza, hogy azok a munkájához beolvasásakor.</span><span class="sxs-lookup"><span data-stu-id="df872-111">Giving users access to too few cmdlets and functions can prevent them from getting their job done.</span></span>
<span data-ttu-id="df872-112">Túl sok parancsmag és funkció való hozzáférés történt egynél védelméről az implicit rendszergazda jogosultságokkal a biztonsági hatékonyabb védelem gyengítése felhasználók vezethet.</span><span class="sxs-lookup"><span data-stu-id="df872-112">Allowing access to too many cmdlets and functions can lead to users doing more than you intended with their implicit admin privileges, weakening your security stance.</span></span>

<span data-ttu-id="df872-113">Hogyan lépjen erről a folyamatról függ a szervezet és a célokat, azonban a következő tippek segítségével, nyissa meg a megfelelő elérési úton.</span><span class="sxs-lookup"><span data-stu-id="df872-113">How you go about this process will depend on your organization and goals, however the following tips can help ensure you're on the right path.</span></span>

1. <span data-ttu-id="df872-114">**Azonosítsa** a parancsok felhasználók használnak a munkájuk elvégzéséhez.</span><span class="sxs-lookup"><span data-stu-id="df872-114">**Identify** the commands users are using to get their jobs done.</span></span> <span data-ttu-id="df872-115">Ez magában foglalhatja felmérve az informatikai részleg, automatizálási parancsfájlokat ellenőrzése vagy PowerShell-munkamenethez ki vagy naplók elemzése.</span><span class="sxs-lookup"><span data-stu-id="df872-115">This may involve surveying IT staff, checking automation scripts, or analyzing PowerShell session transcripts or logs.</span></span>
2. <span data-ttu-id="df872-116">**Frissítés** használata PowerShell alakokat parancssori eszköze, a legjobb naplózás és a JEA testreszabási felületet.</span><span class="sxs-lookup"><span data-stu-id="df872-116">**Update** use of command line tools to PowerShell equivalents, where possible, for the best auditing and JEA customization experience.</span></span> <span data-ttu-id="df872-117">Külső programok, granularly natív PowerShell-parancsmagok és a JEA funkciók nem korlátozható.</span><span class="sxs-lookup"><span data-stu-id="df872-117">External programs cannot be constrained as granularly as native PowerShell cmdlets and functions in JEA.</span></span>
3. <span data-ttu-id="df872-118">**Korlátozása** a parancsmagok, ha szükséges, hogy csak adott paraméterek vagy értékek paraméter engedélyezése körét.</span><span class="sxs-lookup"><span data-stu-id="df872-118">**Restrict** the scope of the cmdlets if necessary to only allow specific parameters or parameter values.</span></span> <span data-ttu-id="df872-119">Ez különösen fontos, ha a felhasználók csak egy rendszer kezelése képesnek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="df872-119">This is particularly important if users should only be able to manage part of a system.</span></span>
4. <span data-ttu-id="df872-120">**Hozzon létre** használ parancsok összetett vagy nehéz korlátozhatja a JEA-parancsok egyéni függvényekhez.</span><span class="sxs-lookup"><span data-stu-id="df872-120">**Create** custom functions to replace complex commands or commands which are difficult to constrain in JEA.</span></span> <span data-ttu-id="df872-121">Egy egyszerű függvényt, amely egy összetett parancs becsomagolja, vagy további ellenőrzési logika vonatkozik a rendszergazdák és a végfelhasználói egyszerűség vezérelhetőséget kínálhat.</span><span class="sxs-lookup"><span data-stu-id="df872-121">A simple function that wraps a complex command or applies additional validation logic can offer additional control for admins and end-user simplicity.</span></span>
5. <span data-ttu-id="df872-122">**Teszt** engedélyezett parancsok a felhasználók és/vagy automation hatókörön belüli listáját szolgáltatását, és szükség szerint módosítsa.</span><span class="sxs-lookup"><span data-stu-id="df872-122">**Test** the scoped list of allowable commands with your users and/or automation services and adjust as necessary.</span></span>

<span data-ttu-id="df872-123">Fontos megjegyezni, hogy JEA munkamenetben parancsok pedig gyakran Futtatás rendszergazdai (vagy egyéb emelt szintű) jogosultságokkal.</span><span class="sxs-lookup"><span data-stu-id="df872-123">It is important to remember that commands in a JEA session are often run with admin (or otherwise elevated) privileges.</span></span>
<span data-ttu-id="df872-124">A használható gondos érték fontos, hogy a JEA-végpont nem teszi lehetővé a rájuk vonatkozó engedélyek jogosultságszintjének emeléséhez csatlakozó felhasználó.</span><span class="sxs-lookup"><span data-stu-id="df872-124">Careful selection of available commands is important to ensure the JEA endpoint does not allow the connecting user to elevate their permissions.</span></span>
<span data-ttu-id="df872-125">Az alábbiakban néhány olyan parancsokat, amelyek használható ártó engedélyezett, ha egy korlátozás nélküli állapotot.</span><span class="sxs-lookup"><span data-stu-id="df872-125">Below are some examples of commands that can be used maliciously if allowed in an unconstrained state.</span></span>
<span data-ttu-id="df872-126">Vegye figyelembe, hogy ez nem egy tárgyal minden releváns kérdést, és csak figyelmeztető kiindulási pontként használható.</span><span class="sxs-lookup"><span data-stu-id="df872-126">Note that this is not an exhaustive list and should only be used as a cautionary starting point.</span></span>

### <a name="examples-of-potentially-dangerous-commands"></a><span data-ttu-id="df872-127">Potenciálisan veszélyes parancsok példák</span><span class="sxs-lookup"><span data-stu-id="df872-127">Examples of potentially dangerous commands</span></span>

<span data-ttu-id="df872-128">Kockázati</span><span class="sxs-lookup"><span data-stu-id="df872-128">Risk</span></span> | <span data-ttu-id="df872-129">Példa</span><span class="sxs-lookup"><span data-stu-id="df872-129">Example</span></span> | <span data-ttu-id="df872-130">Kapcsolódó parancsok</span><span class="sxs-lookup"><span data-stu-id="df872-130">Related commands</span></span>
-----|---------|-----------------
<span data-ttu-id="df872-131">A csatlakozó felhasználó JEA elkerülésére rendszergazdai jogosultságok megadása</span><span class="sxs-lookup"><span data-stu-id="df872-131">Granting the connecting user admin privileges to bypass JEA</span></span> | `Add-LocalGroupMember -Member 'CONTOSO\jdoe' -Group 'Administrators'` | <span data-ttu-id="df872-132">`Add-ADGroupMember`, `Add-LocalGroupMember`, `net.exe`, `dsadd.exe`</span><span class="sxs-lookup"><span data-stu-id="df872-132">`Add-ADGroupMember`, `Add-LocalGroupMember`, `net.exe`, `dsadd.exe`</span></span>
<span data-ttu-id="df872-133">Tetszőleges kódot, például a kártevő, biztonsági réseket és védelmet elkerülésére egyéni parancsfájlok</span><span class="sxs-lookup"><span data-stu-id="df872-133">Running arbitrary code, such as malware, exploits, or custom scripts to bypass protections</span></span> | `Start-Process -FilePath '\\san\share\malware.exe'` | <span data-ttu-id="df872-134">`Start-Process`, `New-Service`, `Invoke-Item`, `Invoke-WmiMethod`, `Invoke-CimMethod`, `Invoke-Expression`, `Invoke-Command`, `New-ScheduledTask`, `Register-ScheduledJob`</span><span class="sxs-lookup"><span data-stu-id="df872-134">`Start-Process`, `New-Service`, `Invoke-Item`, `Invoke-WmiMethod`, `Invoke-CimMethod`, `Invoke-Expression`, `Invoke-Command`, `New-ScheduledTask`, `Register-ScheduledJob`</span></span>

## <a name="create-a-role-capability-file"></a><span data-ttu-id="df872-135">Egy szerepkör funkció fájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="df872-135">Create a role capability file</span></span>

<span data-ttu-id="df872-136">Az új PowerShell-szerepkör funkció fájlt létrehozhatja a [New-PSRoleCapabilityFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSRoleCapabilityFile) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="df872-136">You can create a new PowerShell role capability file with the [New-PSRoleCapabilityFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSRoleCapabilityFile) cmdlet.</span></span>

```powershell
New-PSRoleCapabilityFile -Path .\MyFirstJEARole.psrc
```

<span data-ttu-id="df872-137">Az eredményül kapott szerepet funkció fájl egy szövegszerkesztőben megnyitott, és módosítani kell, hogy a szerepkör a kívánt parancsokat.</span><span class="sxs-lookup"><span data-stu-id="df872-137">The resulting role capability file can be opened in a text editor and modified to allow the desired commands for the role.</span></span>
<span data-ttu-id="df872-138">A PowerShell súgójának Néhány példa hogyan konfigurálható a fájl tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="df872-138">The PowerShell help documentation contains several examples of how you can configure the file.</span></span>

### <a name="allowing-powershell-cmdlets-and-functions"></a><span data-ttu-id="df872-139">PowerShell-parancsmagok és a Funkciók</span><span class="sxs-lookup"><span data-stu-id="df872-139">Allowing PowerShell cmdlets and functions</span></span>

<span data-ttu-id="df872-140">Felhasználókat, hogy futtassák a PowerShell-parancsmagok és a funkciók engedélyezésére, vegye fel a parancsmag vagy függvény neve a VisbibleCmdlets vagy VisibleFunctions mezőket.</span><span class="sxs-lookup"><span data-stu-id="df872-140">To authorize users to run PowerShell cmdlets or functions, add the cmdlet or function name to the VisbibleCmdlets or VisibleFunctions fields.</span></span>
<span data-ttu-id="df872-141">Ha nem nem biztos benne, hogy egy parancs egy parancsmag vagy függvény-e, futtassa `Get-Command <name>` és a "CommandType" tulajdonságot a kimenetben.</span><span class="sxs-lookup"><span data-stu-id="df872-141">If you aren't sure whether a command is a cmdlet or function, you can run `Get-Command <name>` and check the "CommandType" property in the output.</span></span>

```powershell
VisibleCmdlets = 'Restart-Computer', 'Get-NetIPAddress'
```

<span data-ttu-id="df872-142">Egyes esetekben az egy adott parancsmag vagy függvény hatóköre túl széleskörű, a felhasználók igényei szerint.</span><span class="sxs-lookup"><span data-stu-id="df872-142">Sometimes the scope of a specific cmdlet or function is too broad for your users' needs.</span></span>
<span data-ttu-id="df872-143">A DNS-rendszergazdai például, valószínűleg csak igényeinek érhetik el a DNS-szolgáltatás újraindítására.</span><span class="sxs-lookup"><span data-stu-id="df872-143">A DNS admin, for example, probably only needs access to restart the DNS service.</span></span>
<span data-ttu-id="df872-144">Több-bérlős környezetben, ahol bérlők által elérhető adatbázisnézet önkiszolgáló kezelőeszközöket bérlők kell korlátozni kezelése a saját erőforrásait.</span><span class="sxs-lookup"><span data-stu-id="df872-144">In a multi-tenant environment where tenants are granted access to self-service management tools, tenants should be limited to managing with their own resources.</span></span>
<span data-ttu-id="df872-145">Ezekben az esetekben a korlátozhatja, mely paraméterek érhetők el a parancsmag vagy a függvény.</span><span class="sxs-lookup"><span data-stu-id="df872-145">For these cases, you can restrict which parameters are exposed from the cmdlet or function.</span></span>

```powershell

VisibleCmdlets = @{ Name = 'Restart-Computer'; Parameters = @{ Name = 'Name' }}

```

<span data-ttu-id="df872-146">A speciális esetben is szükség lehet valaki megadhatja értékek korlátozása ezeket a paramétereket.</span><span class="sxs-lookup"><span data-stu-id="df872-146">In more advanced scenarios, you may also need to restrict which values someone can supply to these parameters.</span></span>
<span data-ttu-id="df872-147">Szerepkör képességek lehetővé teszik, hogy a megengedett értékek vagy egy reguláris kifejezési minta annak meghatározásához, hogy engedélyezett-e egy adott bemeneti kiértékelt a kulcstulajdonságokat határozza meg.</span><span class="sxs-lookup"><span data-stu-id="df872-147">Role capabilities let you define a set of allowed values or a regular expression pattern that is evaluated to determine if a given input is allowed.</span></span>

```powershell
VisibleCmdlets = @{ Name = 'Restart-Service'; Parameters = @{ Name = 'Name'; ValidateSet = 'Dns', 'Spooler' }},
                 @{ Name = 'Start-Website'; Parameters = @{ Name = 'Name'; ValidatePattern = 'HR_*' }}
```

> [!NOTE]
> <span data-ttu-id="df872-148">A [gyakori PowerShell-paramétereket](https://technet.microsoft.com/library/hh847884.aspx) mindig engedélyezettek, még akkor is, ha korlátozza az elérhető paramétereket.</span><span class="sxs-lookup"><span data-stu-id="df872-148">The [common PowerShell parameters](https://technet.microsoft.com/library/hh847884.aspx) are always allowed, even if you restrict the available parameters.</span></span>
> <span data-ttu-id="df872-149">Nem kifejezetten sorolja fel azokat a paramétereket mezőben.</span><span class="sxs-lookup"><span data-stu-id="df872-149">You should not explicitly list them in the Parameters field.</span></span>

<span data-ttu-id="df872-150">Az alábbi táblázat ismerteti a különböző módszereket testre szabhatja látható parancsmag vagy egy függvényt.</span><span class="sxs-lookup"><span data-stu-id="df872-150">The table below describes the various ways you can customize a visible cmdlet or function.</span></span>
<span data-ttu-id="df872-151">Szabadon kombinálhatók felel meg az alábbi a VisibleCmdlets mezőbe.</span><span class="sxs-lookup"><span data-stu-id="df872-151">You can mix and match any of the below in the VisibleCmdlets field.</span></span>

<span data-ttu-id="df872-152">Példa</span><span class="sxs-lookup"><span data-stu-id="df872-152">Example</span></span>                                                                                      | <span data-ttu-id="df872-153">Használati eset</span><span class="sxs-lookup"><span data-stu-id="df872-153">Use case</span></span>
---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------
<span data-ttu-id="df872-154">`'My-Func'` vagy `@{ Name = 'My-Func' }`</span><span class="sxs-lookup"><span data-stu-id="df872-154">`'My-Func'` or `@{ Name = 'My-Func' }`</span></span>                                                       | <span data-ttu-id="df872-155">Lehetővé teszi a felhasználó futtatásához `My-Func` a paraméterek korlátozások nélkül.</span><span class="sxs-lookup"><span data-stu-id="df872-155">Allows the user to run `My-Func` without any restrictions on the parameters.</span></span>
`'MyModule\My-Func'`                                                                         | <span data-ttu-id="df872-156">Lehetővé teszi a felhasználó futtatásához `My-Func` a modulból `MyModule` a paraméterek korlátozások nélkül.</span><span class="sxs-lookup"><span data-stu-id="df872-156">Allows the user to run `My-Func` from the module `MyModule` without any restrictions on the parameters.</span></span>
`'My-*'`                                                                                     | <span data-ttu-id="df872-157">Lehetővé teszi a felhasználónak, amelyben bármely parancsmag vagy a funkció futtatásához `My`.</span><span class="sxs-lookup"><span data-stu-id="df872-157">Allows the user to run any cmdlet or function with the verb `My`.</span></span>
`'*-Func'`                                                                                   | <span data-ttu-id="df872-158">Lehetővé teszi a felhasználó bármely parancsmag vagy a funkció futtatásához a főnév `Func`.</span><span class="sxs-lookup"><span data-stu-id="df872-158">Allows the user to run any cmdlet or function with the noun `Func`.</span></span>
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'}, @{ Name = 'Param2' }}`               | <span data-ttu-id="df872-159">Lehetővé teszi a felhasználó futtatásához `My-Func` rendelkező a `Param1` és/vagy `Param2` paraméterek.</span><span class="sxs-lookup"><span data-stu-id="df872-159">Allows the user to run `My-Func` with the `Param1` and/or `Param2` parameters.</span></span> <span data-ttu-id="df872-160">Bármely érték lehet biztosítani a paramétereket.</span><span class="sxs-lookup"><span data-stu-id="df872-160">Any value can be supplied to the parameters.</span></span>
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidateSet = 'Value1', 'Value2' }}`  | <span data-ttu-id="df872-161">Lehetővé teszi a felhasználó futtatásához `My-Func` rendelkező a `Param1` paraméter.</span><span class="sxs-lookup"><span data-stu-id="df872-161">Allows the user to run `My-Func` with the `Param1` parameter.</span></span> <span data-ttu-id="df872-162">A paraméter csak "Érték1" és "Érték2" kell adni.</span><span class="sxs-lookup"><span data-stu-id="df872-162">Only "Value1" and "Value2" can be supplied to the parameter.</span></span>
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidatePattern = 'contoso.*' }}`     | <span data-ttu-id="df872-163">Lehetővé teszi a felhasználó futtatásához `My-Func` rendelkező a `Param1` paraméter.</span><span class="sxs-lookup"><span data-stu-id="df872-163">Allows the user to run `My-Func` with the `Param1` parameter.</span></span> <span data-ttu-id="df872-164">Kezdve a "contoso" értéket a paraméter lehet biztosítani.</span><span class="sxs-lookup"><span data-stu-id="df872-164">Any value starting with "contoso" can be supplied to the parameter.</span></span>


> [!WARNING]
> <span data-ttu-id="df872-165">Ajánlott biztonsági eljárások azt nem javasolt helyettesítő karaktereket használ, látható parancsmagok és a funkciók meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="df872-165">For best security practices, it is not recommended to use wildcards when defining visible cmdlets or functions.</span></span>
> <span data-ttu-id="df872-166">Ehelyett minden megbízható parancsot annak biztosítására a többi parancs nincs, amelyek azonos elnevezési sémája véletlenül jogosult explicit módon listában.</span><span class="sxs-lookup"><span data-stu-id="df872-166">Instead, you should explicitly list each trusted command to ensure no other commands that share the same naming scheme are unintentionally authorized.</span></span>

<span data-ttu-id="df872-167">Egy ValidatePattern és a ValidateSet egy parancsmag vagy függvény nem alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="df872-167">You cannot apply both a ValidatePattern and ValidateSet to the same cmdlet or function.</span></span>

<span data-ttu-id="df872-168">Ha így tesz, a ValidatePattern felülírja a ValidateSet.</span><span class="sxs-lookup"><span data-stu-id="df872-168">If you do, the ValidatePattern will override the ValidateSet.</span></span>

<span data-ttu-id="df872-169">ValidatePattern kapcsolatos további információkért tekintse meg [ez *Hey, Scripting Guy!* utáni](https://blogs.technet.microsoft.com/heyscriptingguy/2011/01/11/validate-powershell-parameters-before-running-the-script/) és a [PowerShell reguláris kifejezések](https://technet.microsoft.com/library/hh847880.aspx) tartalom hivatkozik.</span><span class="sxs-lookup"><span data-stu-id="df872-169">For more information about ValidatePattern, check out [this *Hey, Scripting Guy!* post](https://blogs.technet.microsoft.com/heyscriptingguy/2011/01/11/validate-powershell-parameters-before-running-the-script/) and the [PowerShell Regular Expressions](https://technet.microsoft.com/library/hh847880.aspx) reference content.</span></span>

### <a name="allowing-external-commands-and-powershell-scripts"></a><span data-ttu-id="df872-170">Külső parancsok és a PowerShell parancsfájlok</span><span class="sxs-lookup"><span data-stu-id="df872-170">Allowing external commands and PowerShell scripts</span></span>

<span data-ttu-id="df872-171">A felhasználók egy JEA munkameneten belül futó végrehajtható fájlok és a PowerShell-parancsfájlokat (.ps1), fel kell vennie a teljes elérési útja a VisibleExternalCommands mezőben programhoz.</span><span class="sxs-lookup"><span data-stu-id="df872-171">To allow users to run executables and PowerShell scripts (.ps1) in a JEA session, you have to add the full path to each program in the VisibleExternalCommands field.</span></span>

```powershell
VisibleExternalCommands = 'C:\Windows\System32\whoami.exe', 'C:\Program Files\Contoso\Scripts\UpdateITSoftware.ps1'
```

<span data-ttu-id="df872-172">Javasoljuk, ahol lehetséges, a PowerShell parancsmag/függvény alakokat a bármely külső végrehajtható fájlok, mivel az informatikai részleg ellenőrzése, mely paraméterek megengedett, a PowerShell-parancsmagok/funkciók engedélyezésére.</span><span class="sxs-lookup"><span data-stu-id="df872-172">It is advised, where possible, to use PowerShell cmdlet/function equivalents of any external executables you authorize since you have control over which parameters are allowed with PowerShell cmdlets/functions.</span></span>

<span data-ttu-id="df872-173">Sok végrehajtható fájlok lehetővé teszik a jelenlegi állapotában olvasására és csak a különböző paraméterek megadásával módosítsa.</span><span class="sxs-lookup"><span data-stu-id="df872-173">Many executables allow you to both read the current state and then change it just by providing different parameters.</span></span>

<span data-ttu-id="df872-174">Tegyük fel, ellenőrizze, hogy melyik hálózati megosztások a helyi számítógép által üzemeltetett kívánó fájl kiszolgálói rendszergazda szerepkör.</span><span class="sxs-lookup"><span data-stu-id="df872-174">For example, consider the role of a file server admin who wants to check which network shares are hosted by the local machine.</span></span>
<span data-ttu-id="df872-175">Ellenőrizze, hogy egy módja `net share`.</span><span class="sxs-lookup"><span data-stu-id="df872-175">One way to check is to use `net share`.</span></span>
<span data-ttu-id="df872-176">Azonban, így a net.exe nem nagyon súlyos, mert a rendszergazda ugyanilyen könnyen használhatja a parancs ahhoz, hogy a rendszergazda jogosultságokkal rendelkező `net group Administrators unprivilegedjeauser /add`.</span><span class="sxs-lookup"><span data-stu-id="df872-176">However, allowing net.exe is very dangerous becuase the admin could just as easily use the command to gain admin privileges with `net group Administrators unprivilegedjeauser /add`.</span></span>
<span data-ttu-id="df872-177">A jobb megoldás, hogy [Get-SmbShare](https://technet.microsoft.com/library/jj635704.aspx) amely ugyanazt az eredményt éri el, de korlátozottabb hatókörrel rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="df872-177">A better approach is to allow [Get-SmbShare](https://technet.microsoft.com/library/jj635704.aspx) which achieves the same result but has a much more limited scope.</span></span>

<span data-ttu-id="df872-178">Külső parancsok elérhetővé tétele a felhasználók számára a JEA-munkamenetben, mindig adja meg annak érdekében, hogy egy hasonlóan elnevezett (és potenciálisan malicous) programot, máshová helyezve a rendszer nem hajtódnak inkább a végrehajtható fájl teljes elérési útvonalát.</span><span class="sxs-lookup"><span data-stu-id="df872-178">When making external commands available to users in a JEA session, always specify the complete path to the executable to ensure a similarly named (and potentially malicous) program placed elsewhere on the system does not get executed instead.</span></span>

### <a name="allowing-access-to-powershell-providers"></a><span data-ttu-id="df872-179">PowerShell-szolgáltatók való hozzáférés</span><span class="sxs-lookup"><span data-stu-id="df872-179">Allowing access to PowerShell providers</span></span>

<span data-ttu-id="df872-180">Alapértelmezés szerint nem PowerShell szolgáltatók érhetők el a JEA-munkamenetekben.</span><span class="sxs-lookup"><span data-stu-id="df872-180">By default, no PowerShell providers are available in JEA sessions.</span></span>

<span data-ttu-id="df872-181">Ez az elsősorban a bizalmas adatokat és beállításokat adatokat tesznek közzé a kapcsolódó felhasználó a kockázat csökkentésére.</span><span class="sxs-lookup"><span data-stu-id="df872-181">This is primarily to reduce the risk of sensitive information and configuration settings being disclosed to the connecting user.</span></span>

<span data-ttu-id="df872-182">Ha szükséges, a PowerShell-szolgáltató használatával hozzáférést biztosíthat a `VisibleProviders` parancsot.</span><span class="sxs-lookup"><span data-stu-id="df872-182">When necessary, you can allow access to the PowerShell providers using the `VisibleProviders` command.</span></span>
<span data-ttu-id="df872-183">A szolgáltatók teljes listájának megtekintéséhez futtassa a `Get-PSProvider`.</span><span class="sxs-lookup"><span data-stu-id="df872-183">For a full list of providers, run `Get-PSProvider`.</span></span>

```powershell
VisibleProviders = 'Registry'
```

<span data-ttu-id="df872-184">Egyszerű tevékenység, amelynek szüksége van a fájlrendszer, a beállításjegyzék, a tanúsítványtároló vagy a többi bizalmas szolgáltatók esetén is érdemes lehet írása, amely kompatibilis a szolgáltató, a felhasználó nevében egyéni függvény.</span><span class="sxs-lookup"><span data-stu-id="df872-184">For simple tasks that require access to the file system, registry, certificate store, or other sensitive providers, you can also consider writing a custom function that works with the provider on the user's behalf.</span></span>
<span data-ttu-id="df872-185">Funkciók, a parancsmagok és a külső programok által biztosított JEA munkamenetben nem tartoznak ugyanazon a korlátozások tartoznak, mint JEA – alapértelmezés szerint bármely szolgáltató eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="df872-185">Functions, cmdlets, and external programs that are available in a JEA session are not subject to the same constraints as JEA -- they can access any provider by default.</span></span>
<span data-ttu-id="df872-186">Is érdemes lehet a [felhasználói meghajtó](session-configurations.md#user-drive) fájlok másolása a JEA végpont onnan esetén szükséges.</span><span class="sxs-lookup"><span data-stu-id="df872-186">Also consider using the [user drive](session-configurations.md#user-drive) when copying files to/from a JEA endpoint is required.</span></span>

### <a name="creating-custom-functions"></a><span data-ttu-id="df872-187">Egyéni függvények létrehozása</span><span class="sxs-lookup"><span data-stu-id="df872-187">Creating custom functions</span></span>

<span data-ttu-id="df872-188">Egyszerűbbé teheti az összetett feladatok a végfelhasználóknak a szerepkör funkció fájlban egyéni funkciók hozhat létre.</span><span class="sxs-lookup"><span data-stu-id="df872-188">You can author custom functions in a role capability file to simplify complex tasks for your end users.</span></span>
<span data-ttu-id="df872-189">Egyéni funkciók is hasznosak, ha speciális ellenőrzési logika az parancsmag-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="df872-189">Custom functions are also useful when you require advanced validation logic for cmdlet parameter values.</span></span>
<span data-ttu-id="df872-190">Egyszerű funkciók írhat a **FunctionDefinitions** mező:</span><span class="sxs-lookup"><span data-stu-id="df872-190">You can write simple functions in the **FunctionDefinitions** field:</span></span>

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
> <span data-ttu-id="df872-191">Ne feledje, a nevet az egyéni funkciók a **VisibleFunctions** mezőt, így a JEA felhasználók által futtatható.</span><span class="sxs-lookup"><span data-stu-id="df872-191">Don't forget to add the name of your custom functions to the **VisibleFunctions** field so they can be run by the JEA users.</span></span>


<span data-ttu-id="df872-192">Egyéni funkciók törzsében (parancsfájlblokkban) a rendszer az alapértelmezett nyelv módban fut, és nincs JEA tartozó nyelvi korlátok.</span><span class="sxs-lookup"><span data-stu-id="df872-192">The body (script block) of custom functions runs in the default language mode for the system and is not subject to JEA's language constraints.</span></span>
<span data-ttu-id="df872-193">Ez azt jelenti, hogy funkciók is a fájlrendszert és beállításjegyzéket, majd futtassa a parancsokat elvégzett nem látható a szerepkör funkció fájlban.</span><span class="sxs-lookup"><span data-stu-id="df872-193">This means that functions can access the file system and registry, and run commands that were not made visible in the role capability file.</span></span>
<span data-ttu-id="df872-194">Elkerülése érdekében, így tetszőleges kód futtatható, ha a paraméterek használatával kezeli, és elkerülheti a átirányítás felhasználói bevitel közvetlenül be például a parancsmagok `Invoke-Expression`.</span><span class="sxs-lookup"><span data-stu-id="df872-194">Take care to avoid allowing arbitrary code to be run when using parameters and avoid piping user input directly into cmdlets like `Invoke-Expression`.</span></span>

<span data-ttu-id="df872-195">A fenti példában, megfigyelheti, hogy a teljesen minősített Modulnév (FQMN) `Microsoft.PowerShell.Utility\Select-Object` helyett a rövid szintaxist használta `Select-Object`.</span><span class="sxs-lookup"><span data-stu-id="df872-195">In the above example, you will notice that the fully qualified module name (FQMN) `Microsoft.PowerShell.Utility\Select-Object` was used instead of the shorthand `Select-Object`.</span></span>
<span data-ttu-id="df872-196">Szerepkör szolgáltatásfájlokban definiált függvények még lépnek JEA munkamenetek, beleértve a proxy funkciók körét korlátozhatja a meglévő parancsok JEA hoz létre.</span><span class="sxs-lookup"><span data-stu-id="df872-196">Functions defined in role capability files are still subject to the scope of JEA sessions, which includes the proxy functions JEA creates to constrain existing commands.</span></span>

<span data-ttu-id="df872-197">Select-Object alapértelmezett, korlátozott parancsmag minden JEA-munkamenetekben, amelyek nem teszik lehetővé a objektumokon tetszőleges Tulajdonságok parancsra.</span><span class="sxs-lookup"><span data-stu-id="df872-197">Select-Object is a default, constrained cmdlet in all JEA sessions that doesn't allow you to select arbitrary properties on objects.</span></span>
<span data-ttu-id="df872-198">A korlátozás nélküli Select-Object funkciók használatához explicit módon a FQMN megadásával kell igényelnie a teljes megvalósítás.</span><span class="sxs-lookup"><span data-stu-id="df872-198">To use the unconstrained Select-Object in functions, you must explicitly request the full implementation by specifying the FQMN.</span></span>
<span data-ttu-id="df872-199">Bármely korlátozott parancsmag JEA munkamenetben virágot fog hozni a kívánt viselkedést eredményező beállítást egy függvényből összhangban PowerShell meghívásakor [sorrend parancs](https://msdn.microsoft.com/en-us/powershell/reference/3.0/microsoft.powershell.core/about/about_command_precedence).</span><span class="sxs-lookup"><span data-stu-id="df872-199">Any constrained cmdlet in a JEA session will exhibit the same behavior when invoked from a function, in line with PowerShell's [command precedence](https://msdn.microsoft.com/en-us/powershell/reference/3.0/microsoft.powershell.core/about/about_command_precedence).</span></span>

<span data-ttu-id="df872-200">Ha egyéni funkciók számos, helyezze őket könnyebben lehet egy [PowerShell parancsfájl modul](https://msdn.microsoft.com/en-us/library/dd878340(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="df872-200">If you are writing a lot of custom functions, it may be easier to put them in a [PowerShell Script Module](https://msdn.microsoft.com/en-us/library/dd878340(v=vs.85).aspx).</span></span>
<span data-ttu-id="df872-201">Majd tehet olyan feladatokat a JEA munkamenet VisibleFunctions mező meg, mint a beépített és harmadik féltől származó modulok látható.</span><span class="sxs-lookup"><span data-stu-id="df872-201">You can then make those functions visible in the JEA session using the VisibleFunctions field like you would with built-in and third party modules.</span></span>

## <a name="place-role-capabilities-in-a-module"></a><span data-ttu-id="df872-202">A modul hely szerepkör képességei</span><span class="sxs-lookup"><span data-stu-id="df872-202">Place role capabilities in a module</span></span>

<span data-ttu-id="df872-203">Ahhoz, hogy PowerShell található szerepkör-funkció fájl akkor kell tárolni egy PowerShell-moduljának "RoleCapabilities" mappában.</span><span class="sxs-lookup"><span data-stu-id="df872-203">In order for PowerShell to find a role capability file, it must be stored in a "RoleCapabilities" folder in a PowerShell module.</span></span>
<span data-ttu-id="df872-204">A modul bármely mappában szereplő tárolhatók a `$env:PSModulePath` környezeti változó, azonban kell nem elhelyezés System32 (beépített modulok számára fenntartott) vagy egy mappa ahol a nem megbízható, csatlakozó felhasználók módosíthatják a fájlok.</span><span class="sxs-lookup"><span data-stu-id="df872-204">The module can be stored in any folder included in the `$env:PSModulePath` environment variable, however you should not place it in System32 (reserved for built-in modules) or a folder where the untrusted, connecting users could modify the files.</span></span>
<span data-ttu-id="df872-205">Az alábbiakban látható egy példa egy egyszerű PowerShell parancsfájl modul nevű létrehozása *ContosoJEA* a "Program fájlok" elérési úton.</span><span class="sxs-lookup"><span data-stu-id="df872-205">Below is an example of creating a basic PowerShell script module called *ContosoJEA* in the "Program Files" path.</span></span>

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

<span data-ttu-id="df872-206">Lásd: [egy PowerShell-modul ismertetése](https://msdn.microsoft.com/en-us/library/dd878324.aspx) további információt a PSModulePath környezeti változó, a PowerShell modulok és a modul jegyzékfájljai.</span><span class="sxs-lookup"><span data-stu-id="df872-206">See [Understanding a PowerShell Module](https://msdn.microsoft.com/en-us/library/dd878324.aspx) for more information about PowerShell modules, module manifests, and the PSModulePath environment variable.</span></span>

## <a name="updating-role-capabilities"></a><span data-ttu-id="df872-207">Szerepkör képességek frissítése</span><span class="sxs-lookup"><span data-stu-id="df872-207">Updating role capabilities</span></span>


<span data-ttu-id="df872-208">Egy szerepkör funkció fájl frissíthetjük bármikor egyszerűen módosításainak mentése folyamatban van a szerepkör funkció fájlt.</span><span class="sxs-lookup"><span data-stu-id="df872-208">You can update a role capability file at any time by simply saving changes to the role capability file.</span></span>
<span data-ttu-id="df872-209">Bármely új JEA munkameneteket a szerepkör funkció frissítése után a módosított képességek fogja tartalmazni.</span><span class="sxs-lookup"><span data-stu-id="df872-209">Any new JEA sessions started after the role capability has been updated will reflect the revised capabilities.</span></span>

<span data-ttu-id="df872-210">Ezért a szerepkör képességek mappa hozzáférés szabályozása, ezért fontos.</span><span class="sxs-lookup"><span data-stu-id="df872-210">This is why controlling access to the role capabilities folder is so important.</span></span>
<span data-ttu-id="df872-211">Csak messzemenően megbízható rendszergazdák szerepkör szolgáltatásfájlokban módosítása képesnek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="df872-211">Only highly trusted administrators should be able to change role capability files.</span></span>
<span data-ttu-id="df872-212">Egy nem megbízható felhasználói szerepkör szolgáltatásfájlokban módosíthatja, ha azok könnyen magukat hozzáférést biztosíthat a parancsmagok, ami lehetővé teszi, hogy függesztheti.</span><span class="sxs-lookup"><span data-stu-id="df872-212">If an untrusted user can change role capability files, they can easily give themselves access to cmdlets which allow them to elevate their privileges.</span></span>


<span data-ttu-id="df872-213">A rendszergazdák szeretnék a hozzáférést a szerepkör funkciókat zárolása győződjön meg arról, helyi rendszer rendelkezik olvasási hozzáférés a szerepkör szolgáltatásfájlokban és tartalmazó modult.</span><span class="sxs-lookup"><span data-stu-id="df872-213">For administrators looking to lock down access to the role capabilities, ensure Local System has read access to the role capability files and containing modules.</span></span>

## <a name="how-role-capabilities-are-merged"></a><span data-ttu-id="df872-214">Hogyan egyesítve lesznek szerepkör képességek</span><span class="sxs-lookup"><span data-stu-id="df872-214">How role capabilities are merged</span></span>

<span data-ttu-id="df872-215">Felhasználók is hozzáférhetnek, hogy több szerepkör képességek attól függően, hogy a szerepkör-hozzárendelések a JEA munkamenet be a [munkamenet konfigurációs fájl](session-configurations.md).</span><span class="sxs-lookup"><span data-stu-id="df872-215">Users can be granted access to multiple role capabilities when they enter a JEA session depending on the role mappings in the [session configuration file](session-configurations.md).</span></span>
<span data-ttu-id="df872-216">Ha ez történik, JEA a felhasználó megpróbál az *leghatékonyabb* valamelyik szerepkörnél által engedélyezett parancsokat.</span><span class="sxs-lookup"><span data-stu-id="df872-216">When this happens, JEA tries to give the user the *most permissive* set of commands allowed by any of the roles.</span></span>

<span data-ttu-id="df872-217">**VisibleCmdlets és VisibleFunctions**</span><span class="sxs-lookup"><span data-stu-id="df872-217">**VisibleCmdlets and VisibleFunctions**</span></span>

<span data-ttu-id="df872-218">A legösszetettebb egyesítési logika hatással van a parancsmag és funkció, a paraméterek és a paraméterértékeket a JEA korlátozott lehet.</span><span class="sxs-lookup"><span data-stu-id="df872-218">The most complex merge logic affects cmdlets and functions, which can have their parameters and parameter values limited in JEA.</span></span>

<span data-ttu-id="df872-219">A szabályok a következők:</span><span class="sxs-lookup"><span data-stu-id="df872-219">The rules are as follows:</span></span>

1. <span data-ttu-id="df872-220">A parancsmag csak akkor jelenik meg egy szerepkör, ha bármely alkalmazandó típusparaméter-korlátozásokkal rendelkező felhasználó számára látható lesz.</span><span class="sxs-lookup"><span data-stu-id="df872-220">If a cmdlet is only made visible in one role, it will be visible to the user with any applicable parameter constraints.</span></span>
2. <span data-ttu-id="df872-221">Ha a parancsmag több szerepkör láthatóvá válnak, és mindegyik szerepkör tartalmazza a parancsmag azonos korlátozásaival, a parancsmag az e-korlátozásokkal rendelkező felhasználó számára látható lesz.</span><span class="sxs-lookup"><span data-stu-id="df872-221">If a cmdlet is made visible in more than one role, and each role has the same constraints on the cmdlet, the cmdlet will be visible to the user with those constraints.</span></span>
3. <span data-ttu-id="df872-222">Ha a parancsmag több szerepkör láthatóvá válnak, és minden egyes szerepkör lehetővé teszi, hogy a különböző paraméterek, a parancsmag és az összes megadott paraméterek között minden szerepkör lesz a felhasználó számára látható.</span><span class="sxs-lookup"><span data-stu-id="df872-222">If a cmdlet is made visible in more than one role, and each role allows a different set of parameters, the cmdlet and all of the parameters defined across every role will be visible to the user.</span></span> <span data-ttu-id="df872-223">Ha egy szerepkör nem rendelkezik a paraméterek vonatkozóan, minden paraméter engedélyezett lesz.</span><span class="sxs-lookup"><span data-stu-id="df872-223">If one role doesn't have constraints on the parameters, all parameters will be allowed.</span></span>
4. <span data-ttu-id="df872-224">Ha egy szerepkör ellenőrzése set vagy egy parancsmag-paraméterben ellenőrzése mintát határoz meg, és a többi szerepkör lehetővé teszi, hogy a paraméter, de nem korlátozhatják a paraméterértékeket, az érvényesítés set vagy -mintát lesz figyelembe véve.</span><span class="sxs-lookup"><span data-stu-id="df872-224">If one role defines a validate set or validate pattern for a cmdlet parameter, and the other role allows the parameter but does not constrain the parameter values, the validate set or pattern will be ignored.</span></span>
5. <span data-ttu-id="df872-225">Ha ellenőrzése meg egynél több szerepkör ugyanazon parancsmag paraméter meg van adva, származó összes ellenőrzése minden érték engedélyezett lesz.</span><span class="sxs-lookup"><span data-stu-id="df872-225">If a validate set is defined for the same cmdlet parameter in more than one role, all values from all validate sets will be allowed.</span></span>
6. <span data-ttu-id="df872-226">Ha a validate minta egynél több szerepkör ugyanazon parancsmag paraméter meg van adva, a minták valamelyikének megfelelő értékeket engedélyezett lesz.</span><span class="sxs-lookup"><span data-stu-id="df872-226">If a validate pattern is defined for the same cmdlet parameter in more than one role, any values that match any of the patterns will be allowed.</span></span>
7. <span data-ttu-id="df872-227">Ha egy ellenőrzése készlet egy vagy több szerepkör van definiálva, és ellenőrzése mintát egy másik szerepkör ugyanazon parancsmag paraméter van megadva, az érvényesítés beállítása a rendszer figyelmen kívül hagyja, és szabály (6) a fennmaradó ellenőrzése minták vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="df872-227">If a validate set is defined in one or more roles, and a validate pattern is defined in another role for the same cmdlet parameter, the validate set is ignored and rule (6) applies to the remaining validate patterns.</span></span>

<span data-ttu-id="df872-228">Alább látható egy példa hogyan szerepkörök szerint ezek a szabályok egyesítve lesznek:</span><span class="sxs-lookup"><span data-stu-id="df872-228">Below is an example of how roles are merged according to these rules:</span></span>

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



<span data-ttu-id="df872-229">**VisibleExternalCommands, VisibleAliases, VisibleProviders, ScriptsToProcess**</span><span class="sxs-lookup"><span data-stu-id="df872-229">**VisibleExternalCommands, VisibleAliases, VisibleProviders, ScriptsToProcess**</span></span>

<span data-ttu-id="df872-230">A szerepkör funkció fájlban lévő többi mezőt egyszerűen összesített csoportja engedélyezett külső parancsok, a aliasok, a szolgáltatók és az indítási parancsfájlok hozzáadódnak.</span><span class="sxs-lookup"><span data-stu-id="df872-230">All other fields in the role capability file are simply added to a cumulative set of allowable external commands, aliases, providers, and startup scripts.</span></span>
<span data-ttu-id="df872-231">Bármely parancs, az alias, a szolgáltató vagy a parancsfájl egy szerepkör képesség érhető el a JEA felhasználó számára elérhető lesz.</span><span class="sxs-lookup"><span data-stu-id="df872-231">Any command, alias, provider, or script available in one role capability will be available to the JEA user.</span></span>

<span data-ttu-id="df872-232">Ügyeljen arra, hogy ellenőrizze, hogy a szolgáltatók egy kombinált készlete szerepkör funkció és parancsmagok/funkciók/parancsok egy másik nem csatlakozó felhasználóknak hozzáférést véletlen rendszererőforrások.</span><span class="sxs-lookup"><span data-stu-id="df872-232">Be careful to ensure that the combined set of providers from one role capability and cmdlets/functions/commands from another do not allow connecting users unintentional access to system resources.</span></span>
<span data-ttu-id="df872-233">Például, ha egy szerepkör lehetővé teszi a `Remove-Item` parancsmag és egy másik lehetővé teszi, hogy a `FileSystem` szolgáltató, amelyek kockázata, hogy a JEA felhasználó törlése tetszőleges fájlokat a számítógépre.</span><span class="sxs-lookup"><span data-stu-id="df872-233">For example, if one role allows the `Remove-Item` cmdlet and another allows the `FileSystem` provider, you are at risk of a JEA user deleting arbitrary files on your computer.</span></span>
<span data-ttu-id="df872-234">Felhasználók érvényes engedélyeit azonosításával kapcsolatos további információk találhatók a [JEA témakör naplózás](audit-and-report.md).</span><span class="sxs-lookup"><span data-stu-id="df872-234">Additional information about identifying users' effective permissions can be found in the [auditing JEA topic](audit-and-report.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="df872-235">További lépések</span><span class="sxs-lookup"><span data-stu-id="df872-235">Next steps</span></span>

- [<span data-ttu-id="df872-236">Egy munkamenet-konfigurációs fájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="df872-236">Create a session configuration file</span></span>](session-configurations.md)

