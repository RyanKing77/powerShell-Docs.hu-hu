---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: b440ea4a8208d5c576fa566a19e2de377bf5f475
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="script-tracing-and-logging"></a><span data-ttu-id="3e9bb-102">Parancsfájlok nyomkövetése és naplózása</span><span class="sxs-lookup"><span data-stu-id="3e9bb-102">Script Tracing and Logging</span></span>

<span data-ttu-id="3e9bb-103">Amíg a Windows PowerShell már rendelkezik a **LogPipelineExecutionDetails** csoportházirend beállítás parancsmagok meghívását bejelentkezni, PowerShell programozási nyelv bőven van, amelyeket érdemes naplózni és/vagy a naplózási szolgáltatások.</span><span class="sxs-lookup"><span data-stu-id="3e9bb-103">While Windows PowerShell already has the **LogPipelineExecutionDetails** Group Policy setting to log the invocation of cmdlets, PowerShell’s scripting language has plenty of features that you might want to log and/or audit.</span></span> <span data-ttu-id="3e9bb-104">Az új részletes parancsfájl követés funkcióját lehetővé teheti, hogy részletes nyomon követését és a Windows PowerShell parancsfájl-kezelési a rendszerben használt elemzését.</span><span class="sxs-lookup"><span data-stu-id="3e9bb-104">The new Detailed Script Tracing feature lets you enable detailed tracking and analysis of Windows PowerShell scripting use on a system.</span></span> <span data-ttu-id="3e9bb-105">Részletes parancsfájl nyomkövetésének engedélyezése után a Windows PowerShell naplózza az összes parancsfájl-blokkokban ETW Eseménynapló **Microsoft-Windows-PowerShell/műveleti**.</span><span class="sxs-lookup"><span data-stu-id="3e9bb-105">After you enable detailed script tracing, Windows PowerShell logs all script blocks to the ETW event log, **Microsoft-Windows-PowerShell/Operational**.</span></span> <span data-ttu-id="3e9bb-106">Parancsprogram-blokkot egy másik parancsfájlblokk (például egy parancsfájlt, amely meghívja az Invoke-Expression parancsmag egy karakterlánc) hoz létre, ha adott eredményül kapott parancsfájlblokk is naplózza.</span><span class="sxs-lookup"><span data-stu-id="3e9bb-106">If a script block creates another script block (for example, a script that calls the Invoke-Expression cmdlet on a string), that resulting script block is logged as well.</span></span>

<span data-ttu-id="3e9bb-107">Ezek az események naplózása keresztül engedélyezhető a **kapcsolja be a PowerShell parancsfájl-blokk naplózás** csoportházirend-beállítás (Felügyeleti sablonok -> Windows-összetevők Windows PowerShell ->).</span><span class="sxs-lookup"><span data-stu-id="3e9bb-107">Logging of these events can be enabled through the **Turn on PowerShell Script Block Logging** Group Policy setting (in Administrative Templates -> Windows Components -> Windows PowerShell).</span></span>

<span data-ttu-id="3e9bb-108">Az események a következők:</span><span class="sxs-lookup"><span data-stu-id="3e9bb-108">The events are:</span></span>

| <span data-ttu-id="3e9bb-109">Csatorna</span><span class="sxs-lookup"><span data-stu-id="3e9bb-109">Channel</span></span> | <span data-ttu-id="3e9bb-110">Működési</span><span class="sxs-lookup"><span data-stu-id="3e9bb-110">Operational</span></span>                                 |
|---------|---------------------------------------------|
| <span data-ttu-id="3e9bb-111">Szint</span><span class="sxs-lookup"><span data-stu-id="3e9bb-111">Level</span></span>   | <span data-ttu-id="3e9bb-112">Részletes</span><span class="sxs-lookup"><span data-stu-id="3e9bb-112">Verbose</span></span>                                     |
| <span data-ttu-id="3e9bb-113">Műveleti kód</span><span class="sxs-lookup"><span data-stu-id="3e9bb-113">Opcode</span></span>  | <span data-ttu-id="3e9bb-114">Létrehozás</span><span class="sxs-lookup"><span data-stu-id="3e9bb-114">Create</span></span>                                      |
| <span data-ttu-id="3e9bb-115">Művelet</span><span class="sxs-lookup"><span data-stu-id="3e9bb-115">Task</span></span>    | <span data-ttu-id="3e9bb-116">CommandStart</span><span class="sxs-lookup"><span data-stu-id="3e9bb-116">CommandStart</span></span>                                |
| <span data-ttu-id="3e9bb-117">Kulcsszó</span><span class="sxs-lookup"><span data-stu-id="3e9bb-117">Keyword</span></span> | <span data-ttu-id="3e9bb-118">Futási térben</span><span class="sxs-lookup"><span data-stu-id="3e9bb-118">Runspace</span></span>                                    |
| <span data-ttu-id="3e9bb-119">EventId</span><span class="sxs-lookup"><span data-stu-id="3e9bb-119">EventId</span></span> | <span data-ttu-id="3e9bb-120">Engine_ScriptBlockCompiled (0x1008 = 4104)</span><span class="sxs-lookup"><span data-stu-id="3e9bb-120">Engine_ScriptBlockCompiled (0x1008 = 4104)</span></span>  |
| <span data-ttu-id="3e9bb-121">Üzenet</span><span class="sxs-lookup"><span data-stu-id="3e9bb-121">Message</span></span> | <span data-ttu-id="3e9bb-122">A parancsprogram-blokk szöveg (%1 % 2) létrehozása:</span><span class="sxs-lookup"><span data-stu-id="3e9bb-122">Creating Scriptblock text (%1 of %2):</span></span> </br> <span data-ttu-id="3e9bb-123">%3</span><span class="sxs-lookup"><span data-stu-id="3e9bb-123">%3</span></span> </br> <span data-ttu-id="3e9bb-124">A parancsprogram-blokk azonosítója: %4</span><span class="sxs-lookup"><span data-stu-id="3e9bb-124">ScriptBlock ID: %4</span></span> |


<span data-ttu-id="3e9bb-125">A ágyazva az üzenet szövege felméréséhez összeállítani a parancsprogram-blokkot tartalmazzon.</span><span class="sxs-lookup"><span data-stu-id="3e9bb-125">The text embedded in the message is the extent of the script block compiled.</span></span> <span data-ttu-id="3e9bb-126">Az azonosító egy GUID, amely a parancsprogram-blokkot tartalmazzon élettartama megmarad:.</span><span class="sxs-lookup"><span data-stu-id="3e9bb-126">The ID is a GUID that is retained for the life of the script block.</span></span>

<span data-ttu-id="3e9bb-127">Ha engedélyezi a részletes naplózást, a záró jelölők, és a szolgáltatás írási megkezdéséhez:</span><span class="sxs-lookup"><span data-stu-id="3e9bb-127">When you enable verbose logging, the feature writes begin and end markers:</span></span>

| <span data-ttu-id="3e9bb-128">Csatorna</span><span class="sxs-lookup"><span data-stu-id="3e9bb-128">Channel</span></span> | <span data-ttu-id="3e9bb-129">Működési</span><span class="sxs-lookup"><span data-stu-id="3e9bb-129">Operational</span></span>                                            |
|---------|--------------------------------------------------------|
| <span data-ttu-id="3e9bb-130">Szint</span><span class="sxs-lookup"><span data-stu-id="3e9bb-130">Level</span></span>   | <span data-ttu-id="3e9bb-131">Részletes</span><span class="sxs-lookup"><span data-stu-id="3e9bb-131">Verbose</span></span>                                                |
| <span data-ttu-id="3e9bb-132">Műveleti kód</span><span class="sxs-lookup"><span data-stu-id="3e9bb-132">Opcode</span></span>  | <span data-ttu-id="3e9bb-133">Nyissa meg a (/ bezárása)</span><span class="sxs-lookup"><span data-stu-id="3e9bb-133">Open (/ Close)</span></span>                                         |
| <span data-ttu-id="3e9bb-134">Művelet</span><span class="sxs-lookup"><span data-stu-id="3e9bb-134">Task</span></span>    | <span data-ttu-id="3e9bb-135">CommandStart (/ CommandStop)</span><span class="sxs-lookup"><span data-stu-id="3e9bb-135">CommandStart (/ CommandStop)</span></span>                           |
| <span data-ttu-id="3e9bb-136">Kulcsszó</span><span class="sxs-lookup"><span data-stu-id="3e9bb-136">Keyword</span></span> | <span data-ttu-id="3e9bb-137">Futási térben</span><span class="sxs-lookup"><span data-stu-id="3e9bb-137">Runspace</span></span>                                               |
| <span data-ttu-id="3e9bb-138">EventId</span><span class="sxs-lookup"><span data-stu-id="3e9bb-138">EventId</span></span> | <span data-ttu-id="3e9bb-139">A parancsprogram-blokk\_meghívása\_Start\_(0x1009 = 4105) részletei /</span><span class="sxs-lookup"><span data-stu-id="3e9bb-139">ScriptBlock\_Invoke\_Start\_Detail (0x1009 = 4105) /</span></span> </br> <span data-ttu-id="3e9bb-140">A parancsprogram-blokk\_meghívása\_teljes\_részletei (0x100A Határolók = 4106)</span><span class="sxs-lookup"><span data-stu-id="3e9bb-140">ScriptBlock\_Invoke\_Complete\_Detail (0x100A = 4106)</span></span> |
| <span data-ttu-id="3e9bb-141">Üzenet</span><span class="sxs-lookup"><span data-stu-id="3e9bb-141">Message</span></span> | <span data-ttu-id="3e9bb-142">Elindítva (/ befejezett) hívása nem volt a parancsprogram-blokk-azonosító: %1</span><span class="sxs-lookup"><span data-stu-id="3e9bb-142">Started (/ Completed) invocation of ScriptBlock ID: %1</span></span> </br> <span data-ttu-id="3e9bb-143">Futási térben azonosítója: %2</span><span class="sxs-lookup"><span data-stu-id="3e9bb-143">Runspace ID: %2</span></span> |

<span data-ttu-id="3e9bb-144">Az azonosító a script blokkból (amelyek is egyeztetés szükséges eseményazonosító 0x1008) képviselő GUID, és a futási teret ID jelöli, amelyben a parancsfájl-blokkban futtatták futási térben.</span><span class="sxs-lookup"><span data-stu-id="3e9bb-144">The ID is the GUID representing the script block (that can be correlated with event ID 0x1008), and the Runspace ID represents the runspace in which this script block was run.</span></span>

<span data-ttu-id="3e9bb-145">A meghívási üzenetben százalékjelek strukturált ETW-tulajdonságok jelölik.</span><span class="sxs-lookup"><span data-stu-id="3e9bb-145">Percent signs in the invocation message represent structured ETW properties.</span></span> <span data-ttu-id="3e9bb-146">Váltják fel az üzenet szövege a tényleges értékek, amíg egy sokkal hatékonyabban elérhet módja a Get-WinEvent parancsmaggal üzenet olvasható be, és használja a **tulajdonságok** tömb az üzenet.</span><span class="sxs-lookup"><span data-stu-id="3e9bb-146">While they are replaced with the actual values in the message text, a more robust way to access them is to retrieve the message with the Get-WinEvent cmdlet, and then use the **Properties** array of the message.</span></span>

<span data-ttu-id="3e9bb-147">Itt látható egy példa hogyan Ez a funkció elősegíti titkosítására és takarják a parancsfájl egy rosszindulatú kísérlet kicsomagolásához:</span><span class="sxs-lookup"><span data-stu-id="3e9bb-147">Here's an example of how this functionality can help unwrap a malicious attempt to encrypt and obfuscate a script:</span></span>

```powershell
## Malware
function SuperDecrypt
{
    param($script)
    $bytes = [Convert]::FromBase64String($script)

    ## XOR “encryption”
    $xorKey = 0x42
    for($counter = 0; $counter -lt $bytes.Length; $counter++)
    {
        $bytes[$counter] = $bytes[$counter] -bxor $xorKey
    }
    [System.Text.Encoding]::Unicode.GetString($bytes)
}

$decrypted = SuperDecrypt "FUIwQitCNkInQm9CCkItQjFCNkJiQmVCEkI1QixCJkJlQg=="
Invoke-Expression $decrypted
```

<span data-ttu-id="3e9bb-148">A következő naplóbejegyzések fut állít elő:</span><span class="sxs-lookup"><span data-stu-id="3e9bb-148">Running this generates the following log entries:</span></span>

```
Compiling Scriptblock text (1 of 1):
function SuperDecrypt
{
    param($script)
    $bytes = [Convert]::FromBase64String($script)
    ## XOR "encryption"
    $xorKey = 0x42
    for($counter = 0; $counter -lt $bytes.Length; $counter++)
    {
        $bytes[$counter] = $bytes[$counter] -bxor $xorKey
    }
    [System.Text.Encoding]::Unicode.GetString($bytes)

}
ScriptBlock ID: ad8ae740-1f33-42aa-8dfc-1314411877e3

Compiling Scriptblock text (1 of 1):
$decrypted = SuperDecrypt "FUIwQitCNkInQm9CCkItQjFCNkJiQmVCEkI1QixCJkJlQg=="
ScriptBlock ID: ba11c155-d34c-4004-88e3-6502ecb50f52

Compiling Scriptblock text (1 of 1):
Invoke-Expression $decrypted
ScriptBlock ID: 856c01ca-85d7-4989-b47f-e6a09ee4eeb3

Compiling Scriptblock text (1 of 1):
Write-Host 'Pwnd'
ScriptBlock ID: 5e618414-4e77-48e3-8f65-9a863f54b4c8
```

Ha a parancsfájl a blokk hossza meghaladja az ETW Újdonságok képes egy adott esemény üzem, a Windows PowerShell bontja a parancsfájl több részből. <span data-ttu-id="3e9bb-150">Itt látható mintakód kombinálhatja az a naplózott üzeneteket egy parancsfájlt:</span><span class="sxs-lookup"><span data-stu-id="3e9bb-150">Here is sample code to recombine a script from its log messages:</span></span>

```powershell
$created = Get-WinEvent -FilterHashtable @{ ProviderName="Microsoft-Windows-PowerShell"; Id = 4104 } | Where-Object { $_.<...> }
$sortedScripts = $created | sort { $_.Properties[0].Value }
$mergedScript = -join ($sortedScripts | % { $_.Properties[2].Value })
```

<span data-ttu-id="3e9bb-151">Összes naplózási rendszerekhez, amelyek rendelkeznek egy korlátozott megőrzési puffer (azaz ETW-naplók), egy az infrastruktúra elleni, mindig a naplófájl korábbi bizonyító adatok elrejtése jelezhet események kéréssekkel.</span><span class="sxs-lookup"><span data-stu-id="3e9bb-151">As with all logging systems that have a limited retention buffer (i.e. ETW logs), one attack against this infrastructure is to flood the log with spurious events to hide earlier evidence.</span></span> <span data-ttu-id="3e9bb-152">Saját kezűleg a támadások elleni védelméhez, győződjön meg arról, hogy rendelkezik-e valamilyen esemény naplógyűjtést beállítása (például Windows-Eseménytovábbítással, [a Windows Eseménynapló figyelési ellenfél gyorsabban](http://www.nsa.gov/ia/_files/app/Spotting_the_Adversary_with_Windows_Event_Log_Monitoring.pdf)) eseménynaplók ki a számítógépre, nem helyezhető át a lehető leghamarabb.</span><span class="sxs-lookup"><span data-stu-id="3e9bb-152">To protect yourself from this attack, ensure that you have some form of event log collection set up (i.e., Windows Event Forwarding, [Spotting the Adversary with Windows Event Log Monitoring](http://www.nsa.gov/ia/_files/app/Spotting_the_Adversary_with_Windows_Event_Log_Monitoring.pdf)) to move event logs off of the computer as soon as possible.</span></span>