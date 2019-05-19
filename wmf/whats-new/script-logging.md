---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
title: Parancsfájlok nyomkövetése és naplózása
ms.openlocfilehash: 6b7e5022cb4c974da5ddb3d670b5808dc9fb7bdc
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65856153"
---
# <a name="script-tracing-and-logging"></a><span data-ttu-id="080ec-103">Parancsfájlok nyomkövetése és naplózása</span><span class="sxs-lookup"><span data-stu-id="080ec-103">Script Tracing and Logging</span></span>

<span data-ttu-id="080ec-104">Míg a PowerShell már a **LogPipelineExecutionDetails** csoportházirend beállítás parancsmagok meghívását bejelentkezni, a PowerShell szkriptelési nyelv számos funkcióval rendelkezik, amelyeket érdemes jelentkezzen és naplózása.</span><span class="sxs-lookup"><span data-stu-id="080ec-104">While PowerShell already has the **LogPipelineExecutionDetails** Group Policy setting to log the invocation of cmdlets, PowerShell's scripting language has several features that you might want to log and audit.</span></span> <span data-ttu-id="080ec-105">Az új parancsfájl részletes nyomkövetési szolgáltatás nyújt részletes nyomon követési és a PowerShell-parancsprogram-tevékenység elemzése a rendszer.</span><span class="sxs-lookup"><span data-stu-id="080ec-105">The new Detailed Script Tracing feature provides detailed tracking and analysis of PowerShell script activity on a system.</span></span> <span data-ttu-id="080ec-106">Miután engedélyezte a részletes parancsfájl nyomkövetés, PowerShell az összes parancsfájl-blokkokban naplózza az ETW-eseménynaplóban **Microsoft-Windows-PowerShell/műveleti**.</span><span class="sxs-lookup"><span data-stu-id="080ec-106">After enabling detailed script tracing, PowerShell logs all script blocks to the ETW event log, **Microsoft-Windows-PowerShell/Operational**.</span></span> <span data-ttu-id="080ec-107">Ha a parancsprogram-blokkot hoz létre egy másik parancsfájlblokkban, például meghívásával `Invoke-Expression`, a meghívott parancsfájlblokk is rögzíti.</span><span class="sxs-lookup"><span data-stu-id="080ec-107">If a script block creates another script block, for example, by calling `Invoke-Expression`, the invoked script block also logged.</span></span>

<span data-ttu-id="080ec-108">Keresztül a naplózás engedélyezve van a **kapcsolja be a PowerShell parancsfájl-blokk naplózás** a csoportházirend-beállítás **felügyeleti sablonok** -> **Windows-összetevők**  ->  **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="080ec-108">Logging is enabled through the **Turn on PowerShell Script Block Logging** Group Policy setting in **Administrative Templates** -> **Windows Components** -> **Windows PowerShell**.</span></span>

<span data-ttu-id="080ec-109">Az események a következők:</span><span class="sxs-lookup"><span data-stu-id="080ec-109">The events are:</span></span>

| <span data-ttu-id="080ec-110">Csatorna</span><span class="sxs-lookup"><span data-stu-id="080ec-110">Channel</span></span> |                               <span data-ttu-id="080ec-111">Működési</span><span class="sxs-lookup"><span data-stu-id="080ec-111">Operational</span></span>                               |
| ------- | ----------------------------------------------------------------------- |
| <span data-ttu-id="080ec-112">Szint</span><span class="sxs-lookup"><span data-stu-id="080ec-112">Level</span></span>   | <span data-ttu-id="080ec-113">Részletes</span><span class="sxs-lookup"><span data-stu-id="080ec-113">Verbose</span></span>                                                                 |
| <span data-ttu-id="080ec-114">Opcode</span><span class="sxs-lookup"><span data-stu-id="080ec-114">Opcode</span></span>  | <span data-ttu-id="080ec-115">Létrehozás</span><span class="sxs-lookup"><span data-stu-id="080ec-115">Create</span></span>                                                                  |
| <span data-ttu-id="080ec-116">Művelet</span><span class="sxs-lookup"><span data-stu-id="080ec-116">Task</span></span>    | <span data-ttu-id="080ec-117">CommandStart</span><span class="sxs-lookup"><span data-stu-id="080ec-117">CommandStart</span></span>                                                            |
| <span data-ttu-id="080ec-118">Kulcsszó</span><span class="sxs-lookup"><span data-stu-id="080ec-118">Keyword</span></span> | <span data-ttu-id="080ec-119">Futási térben</span><span class="sxs-lookup"><span data-stu-id="080ec-119">Runspace</span></span>                                                                |
| <span data-ttu-id="080ec-120">EventId</span><span class="sxs-lookup"><span data-stu-id="080ec-120">EventId</span></span> | <span data-ttu-id="080ec-121">Engine_ScriptBlockCompiled (0x1008 = 4104)</span><span class="sxs-lookup"><span data-stu-id="080ec-121">Engine_ScriptBlockCompiled (0x1008 = 4104)</span></span>                              |
| <span data-ttu-id="080ec-122">Üzenet</span><span class="sxs-lookup"><span data-stu-id="080ec-122">Message</span></span> | <span data-ttu-id="080ec-123">Hozza létre a scriptblock kulcsszót szöveg (%1 % 2):</span><span class="sxs-lookup"><span data-stu-id="080ec-123">Creating Scriptblock text (%1 of %2):</span></span> </br> <span data-ttu-id="080ec-124">%3</span><span class="sxs-lookup"><span data-stu-id="080ec-124">%3</span></span> </br> <span data-ttu-id="080ec-125">ScriptBlock azonosítója: %4</span><span class="sxs-lookup"><span data-stu-id="080ec-125">ScriptBlock ID: %4</span></span> |


<span data-ttu-id="080ec-126">Ágyazva az üzenet szövege a lefordított parancsfájlblokk mértékét.</span><span class="sxs-lookup"><span data-stu-id="080ec-126">The text embedded in the message is the extent of the script block compiled.</span></span> <span data-ttu-id="080ec-127">Az azonosító egy GUID Azonosítót a parancsprogram-blokkot élettartama a megőrzött.</span><span class="sxs-lookup"><span data-stu-id="080ec-127">The ID is a GUID that is retained for the life of the script block.</span></span>

<span data-ttu-id="080ec-128">Ha engedélyezi a részletes naplózást, funkció kezdő és záró jelölők:</span><span class="sxs-lookup"><span data-stu-id="080ec-128">When you enable verbose logging, the feature writes begin and end markers:</span></span>

| <span data-ttu-id="080ec-129">Csatorna</span><span class="sxs-lookup"><span data-stu-id="080ec-129">Channel</span></span> |                                 <span data-ttu-id="080ec-130">Működési</span><span class="sxs-lookup"><span data-stu-id="080ec-130">Operational</span></span>                                |
| ------- | -------------------------------------------------------------------------- |
| <span data-ttu-id="080ec-131">Szint</span><span class="sxs-lookup"><span data-stu-id="080ec-131">Level</span></span>   | <span data-ttu-id="080ec-132">Részletes</span><span class="sxs-lookup"><span data-stu-id="080ec-132">Verbose</span></span>                                                                    |
| <span data-ttu-id="080ec-133">Opcode</span><span class="sxs-lookup"><span data-stu-id="080ec-133">Opcode</span></span>  | <span data-ttu-id="080ec-134">Nyissa meg a / bezárása</span><span class="sxs-lookup"><span data-stu-id="080ec-134">Open / Close</span></span>                                                               |
| <span data-ttu-id="080ec-135">Művelet</span><span class="sxs-lookup"><span data-stu-id="080ec-135">Task</span></span>    | <span data-ttu-id="080ec-136">CommandStart / CommandStop</span><span class="sxs-lookup"><span data-stu-id="080ec-136">CommandStart / CommandStop</span></span>                                                 |
| <span data-ttu-id="080ec-137">Kulcsszó</span><span class="sxs-lookup"><span data-stu-id="080ec-137">Keyword</span></span> | <span data-ttu-id="080ec-138">Futási térben</span><span class="sxs-lookup"><span data-stu-id="080ec-138">Runspace</span></span>                                                                   |
| <span data-ttu-id="080ec-139">EventId</span><span class="sxs-lookup"><span data-stu-id="080ec-139">EventId</span></span> | <span data-ttu-id="080ec-140">ScriptBlock\_meghívása\_Start\_Detail (0x1009 = 4105) /</span><span class="sxs-lookup"><span data-stu-id="080ec-140">ScriptBlock\_Invoke\_Start\_Detail (0x1009 = 4105) /</span></span> </br> <span data-ttu-id="080ec-141">ScriptBlock\_meghívása\_teljes\_Detail (0x100A Határolók = 4106)</span><span class="sxs-lookup"><span data-stu-id="080ec-141">ScriptBlock\_Invoke\_Complete\_Detail (0x100A = 4106)</span></span> |
| <span data-ttu-id="080ec-142">Üzenet</span><span class="sxs-lookup"><span data-stu-id="080ec-142">Message</span></span> | <span data-ttu-id="080ec-143">Lépések / befejeződött a scriptblock kulcsszót azonosító lett meghívva: %1</span><span class="sxs-lookup"><span data-stu-id="080ec-143">Started / Completed invocation of ScriptBlock ID: %1</span></span> </br> <span data-ttu-id="080ec-144">Futási térben azonosítója: %2</span><span class="sxs-lookup"><span data-stu-id="080ec-144">Runspace ID: %2</span></span> |

<span data-ttu-id="080ec-145">Az azonosító a globálisan egyedi Azonosítót a parancsprogram-blokkot (hogy összekapcsolhatók legyenek 0x1008 eseményazonosító) jelölő, és a futási térben Azonosítóját jelöli, amelyben a parancsprogram-blokkot volt futtatva futási térben.</span><span class="sxs-lookup"><span data-stu-id="080ec-145">The ID is the GUID representing the script block (that can be correlated with event ID 0x1008), and the Runspace ID represents the runspace in which this script block was run.</span></span>

<span data-ttu-id="080ec-146">A meghívási üzenetben százalékjelek strukturált ETW-tulajdonságok jelentik.</span><span class="sxs-lookup"><span data-stu-id="080ec-146">Percent signs in the invocation message represent structured ETW properties.</span></span> <span data-ttu-id="080ec-147">Az üzenet szövege a tényleges értékek cserélése, amíg az robusztusabb úgy érheti el őket, hogy le az üzenetet a Get-WinEvent parancsmaggal, és használja a **tulajdonságok** az üzenet tömbje.</span><span class="sxs-lookup"><span data-stu-id="080ec-147">While they are replaced with the actual values in the message text, a more robust way to access them is to retrieve the message with the Get-WinEvent cmdlet, and then use the **Properties** array of the message.</span></span>

<span data-ttu-id="080ec-148">Íme egy példa hogyan segíthet az ezt a funkciót egy rosszindulatú kísérlet titkosítására és a egy parancsfájl rejtse kicsomagolása:</span><span class="sxs-lookup"><span data-stu-id="080ec-148">Here's an example of how this functionality can help unwrap a malicious attempt to encrypt and obfuscate a script:</span></span>

```powershell
## Malware
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

$decrypted = SuperDecrypt "FUIwQitCNkInQm9CCkItQjFCNkJiQmVCEkI1QixCJkJlQg=="
Invoke-Expression $decrypted
```

<span data-ttu-id="080ec-149">Ez futó állít elő, a következő naplófájl-bejegyzéseket:</span><span class="sxs-lookup"><span data-stu-id="080ec-149">Running this generates the following log entries:</span></span>

```Output
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

Ha a parancsfájl-blokk hossza meghaladja a kapacitás egy egyszeri esemény, a PowerShell a parancsfájl több részre működésképtelenné válik. <span data-ttu-id="080ec-151">A következő mintakód segítségével egy parancsfájlt annak naplóüzenetek újraegyesítésére:</span><span class="sxs-lookup"><span data-stu-id="080ec-151">Here is sample code to recombine a script from its log messages:</span></span>

```powershell
$created = Get-WinEvent -FilterHashtable @{ ProviderName="Microsoft-Windows-PowerShell"; Id = 4104 } |
  Where-Object { $_.<...> }
$sortedScripts = $created | sort { $_.Properties[0].Value }
$mergedScript = -join ($sortedScripts | % { $_.Properties[2].Value })
```

<span data-ttu-id="080ec-152">Csakúgy, mint az összes naplózási rendszerek, amelyek egy korlátozott megőrzési puffer, a támadásokkal szemben az infrastruktúra egyik módja az kéréssekkel túlterhelheti a naplót a korábbi bizonyíték elrejtése jelezhet eseményeket.</span><span class="sxs-lookup"><span data-stu-id="080ec-152">As with all logging systems that have a limited retention buffer, one way to attack this infrastructure is to flood the log with spurious events to hide earlier evidence.</span></span> <span data-ttu-id="080ec-153">Megóvhatja a támadás, győződjön meg arról, hogy rendelkezik-e valamilyen Windows-Eseménytovábbítás beállítása Eseménynapló gyűjtemény.</span><span class="sxs-lookup"><span data-stu-id="080ec-153">To protect yourself from this attack, ensure that you have some form of event log collection set up Windows Event Forwarding.</span></span> <span data-ttu-id="080ec-154">További információkért lásd: [gyorsabban a támadó a Windows Eseménynapló-figyelést](https://apps.nsa.gov/iaarchive/library/reports/spotting-the-adversary-with-windows-event-log-monitoring.cfm).</span><span class="sxs-lookup"><span data-stu-id="080ec-154">For more information, see [Spotting the Adversary with Windows Event Log Monitoring](https://apps.nsa.gov/iaarchive/library/reports/spotting-the-adversary-with-windows-event-log-monitoring.cfm).</span></span>