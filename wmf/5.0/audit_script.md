---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 28cd186ab3a08a0da4ff81f5a21514f239770d13
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058080"
---
# <a name="script-tracing-and-logging"></a><span data-ttu-id="c6039-102">Parancsfájlok nyomkövetése és naplózása</span><span class="sxs-lookup"><span data-stu-id="c6039-102">Script Tracing and Logging</span></span>

<span data-ttu-id="c6039-103">Bár a Windows PowerShell már rendelkezik a **LogPipelineExecutionDetails** csoportházirend beállítás parancsmagok meghívását bejelentkezni, a PowerShell szkriptelési nyelv rendelkezik, amelyeket érdemes naplózni, és/vagy a naplózási szolgáltatások rengeteg.</span><span class="sxs-lookup"><span data-stu-id="c6039-103">While Windows PowerShell already has the **LogPipelineExecutionDetails** Group Policy setting to log the invocation of cmdlets, PowerShell’s scripting language has plenty of features that you might want to log and/or audit.</span></span> <span data-ttu-id="c6039-104">Az új parancsfájl részletes nyomkövetési szolgáltatás engedélyezi a részletes nyomon követési és elemzési rendszerek a Windows PowerShell parancsfájl-kezelési használati teszi lehetővé.</span><span class="sxs-lookup"><span data-stu-id="c6039-104">The new Detailed Script Tracing feature lets you enable detailed tracking and analysis of Windows PowerShell scripting use on a system.</span></span> <span data-ttu-id="c6039-105">Miután engedélyezte a részletes parancsfájl nyomkövetés, Windows PowerShell az összes parancsfájl-blokkokban naplózza az ETW-eseménynaplóba **Microsoft-Windows-PowerShell/műveleti**.</span><span class="sxs-lookup"><span data-stu-id="c6039-105">After you enable detailed script tracing, Windows PowerShell logs all script blocks to the ETW event log, **Microsoft-Windows-PowerShell/Operational**.</span></span> <span data-ttu-id="c6039-106">Ha parancsprogram-blokkot hoz létre egy másik parancsfájlblokkban (például egy parancsfájlt, amely meghívja az Invoke-Expression parancsmag egy karakterlánc), a létrejövő parancsfájlblokkban, valamint a rendszer naplózza.</span><span class="sxs-lookup"><span data-stu-id="c6039-106">If a script block creates another script block (for example, a script that calls the Invoke-Expression cmdlet on a string), that resulting script block is logged as well.</span></span>

<span data-ttu-id="c6039-107">Ezek az események naplózása keresztül engedélyezhető a **kapcsolja be a PowerShell parancsfájl-blokk naplózás** csoportházirend-beállítás (Felügyeleti sablonok -> Windows-összetevők Windows PowerShell ->).</span><span class="sxs-lookup"><span data-stu-id="c6039-107">Logging of these events can be enabled through the **Turn on PowerShell Script Block Logging** Group Policy setting (in Administrative Templates -> Windows Components -> Windows PowerShell).</span></span>

<span data-ttu-id="c6039-108">Az események a következők:</span><span class="sxs-lookup"><span data-stu-id="c6039-108">The events are:</span></span>

| <span data-ttu-id="c6039-109">Csatorna</span><span class="sxs-lookup"><span data-stu-id="c6039-109">Channel</span></span> | <span data-ttu-id="c6039-110">Működési</span><span class="sxs-lookup"><span data-stu-id="c6039-110">Operational</span></span>                                 |
|---------|---------------------------------------------|
| <span data-ttu-id="c6039-111">Szint</span><span class="sxs-lookup"><span data-stu-id="c6039-111">Level</span></span>   | <span data-ttu-id="c6039-112">Részletes</span><span class="sxs-lookup"><span data-stu-id="c6039-112">Verbose</span></span>                                     |
| <span data-ttu-id="c6039-113">Opcode</span><span class="sxs-lookup"><span data-stu-id="c6039-113">Opcode</span></span>  | <span data-ttu-id="c6039-114">Létrehozás</span><span class="sxs-lookup"><span data-stu-id="c6039-114">Create</span></span>                                      |
| <span data-ttu-id="c6039-115">Művelet</span><span class="sxs-lookup"><span data-stu-id="c6039-115">Task</span></span>    | <span data-ttu-id="c6039-116">CommandStart</span><span class="sxs-lookup"><span data-stu-id="c6039-116">CommandStart</span></span>                                |
| <span data-ttu-id="c6039-117">Kulcsszó</span><span class="sxs-lookup"><span data-stu-id="c6039-117">Keyword</span></span> | <span data-ttu-id="c6039-118">Futási térben</span><span class="sxs-lookup"><span data-stu-id="c6039-118">Runspace</span></span>                                    |
| <span data-ttu-id="c6039-119">EventId</span><span class="sxs-lookup"><span data-stu-id="c6039-119">EventId</span></span> | <span data-ttu-id="c6039-120">Engine_ScriptBlockCompiled (0x1008 = 4104)</span><span class="sxs-lookup"><span data-stu-id="c6039-120">Engine_ScriptBlockCompiled (0x1008 = 4104)</span></span>  |
| <span data-ttu-id="c6039-121">Üzenet</span><span class="sxs-lookup"><span data-stu-id="c6039-121">Message</span></span> | <span data-ttu-id="c6039-122">Hozza létre a scriptblock kulcsszót szöveg (%1 % 2):</span><span class="sxs-lookup"><span data-stu-id="c6039-122">Creating Scriptblock text (%1 of %2):</span></span> </br> <span data-ttu-id="c6039-123">%3</span><span class="sxs-lookup"><span data-stu-id="c6039-123">%3</span></span> </br> <span data-ttu-id="c6039-124">ScriptBlock azonosítója: %4</span><span class="sxs-lookup"><span data-stu-id="c6039-124">ScriptBlock ID: %4</span></span> |


<span data-ttu-id="c6039-125">Ágyazva az üzenet szövege a lefordított parancsfájlblokk mértékét.</span><span class="sxs-lookup"><span data-stu-id="c6039-125">The text embedded in the message is the extent of the script block compiled.</span></span> <span data-ttu-id="c6039-126">Az azonosító egy GUID Azonosítót a parancsprogram-blokkot élettartama a megőrzött.</span><span class="sxs-lookup"><span data-stu-id="c6039-126">The ID is a GUID that is retained for the life of the script block.</span></span>

<span data-ttu-id="c6039-127">Ha engedélyezi a részletes naplózást, funkció kezdő és záró jelölők:</span><span class="sxs-lookup"><span data-stu-id="c6039-127">When you enable verbose logging, the feature writes begin and end markers:</span></span>

| <span data-ttu-id="c6039-128">Csatorna</span><span class="sxs-lookup"><span data-stu-id="c6039-128">Channel</span></span> | <span data-ttu-id="c6039-129">Működési</span><span class="sxs-lookup"><span data-stu-id="c6039-129">Operational</span></span>                                            |
|---------|--------------------------------------------------------|
| <span data-ttu-id="c6039-130">Szint</span><span class="sxs-lookup"><span data-stu-id="c6039-130">Level</span></span>   | <span data-ttu-id="c6039-131">Részletes</span><span class="sxs-lookup"><span data-stu-id="c6039-131">Verbose</span></span>                                                |
| <span data-ttu-id="c6039-132">Opcode</span><span class="sxs-lookup"><span data-stu-id="c6039-132">Opcode</span></span>  | <span data-ttu-id="c6039-133">Nyissa meg a (/ bezárása)</span><span class="sxs-lookup"><span data-stu-id="c6039-133">Open (/ Close)</span></span>                                         |
| <span data-ttu-id="c6039-134">Művelet</span><span class="sxs-lookup"><span data-stu-id="c6039-134">Task</span></span>    | <span data-ttu-id="c6039-135">CommandStart (/ CommandStop)</span><span class="sxs-lookup"><span data-stu-id="c6039-135">CommandStart (/ CommandStop)</span></span>                           |
| <span data-ttu-id="c6039-136">Kulcsszó</span><span class="sxs-lookup"><span data-stu-id="c6039-136">Keyword</span></span> | <span data-ttu-id="c6039-137">Futási térben</span><span class="sxs-lookup"><span data-stu-id="c6039-137">Runspace</span></span>                                               |
| <span data-ttu-id="c6039-138">EventId</span><span class="sxs-lookup"><span data-stu-id="c6039-138">EventId</span></span> | <span data-ttu-id="c6039-139">ScriptBlock\_meghívása\_Start\_Detail (0x1009 = 4105) /</span><span class="sxs-lookup"><span data-stu-id="c6039-139">ScriptBlock\_Invoke\_Start\_Detail (0x1009 = 4105) /</span></span> </br> <span data-ttu-id="c6039-140">ScriptBlock\_meghívása\_teljes\_Detail (0x100A Határolók = 4106)</span><span class="sxs-lookup"><span data-stu-id="c6039-140">ScriptBlock\_Invoke\_Complete\_Detail (0x100A = 4106)</span></span> |
| <span data-ttu-id="c6039-141">Üzenet</span><span class="sxs-lookup"><span data-stu-id="c6039-141">Message</span></span> | <span data-ttu-id="c6039-142">Elindítva (/ befejezett) hívja meg a scriptblock kulcsszó-azonosító: %1</span><span class="sxs-lookup"><span data-stu-id="c6039-142">Started (/ Completed) invocation of ScriptBlock ID: %1</span></span> </br> <span data-ttu-id="c6039-143">Futási térben azonosítója: %2</span><span class="sxs-lookup"><span data-stu-id="c6039-143">Runspace ID: %2</span></span> |

<span data-ttu-id="c6039-144">Az azonosító a globálisan egyedi Azonosítót a parancsprogram-blokkot (hogy összekapcsolhatók legyenek 0x1008 eseményazonosító) jelölő, és a futási térben Azonosítóját jelöli, amelyben a parancsprogram-blokkot volt futtatva futási térben.</span><span class="sxs-lookup"><span data-stu-id="c6039-144">The ID is the GUID representing the script block (that can be correlated with event ID 0x1008), and the Runspace ID represents the runspace in which this script block was run.</span></span>

<span data-ttu-id="c6039-145">A meghívási üzenetben százalékjelek strukturált ETW-tulajdonságok jelentik.</span><span class="sxs-lookup"><span data-stu-id="c6039-145">Percent signs in the invocation message represent structured ETW properties.</span></span> <span data-ttu-id="c6039-146">Az üzenet szövege a tényleges értékek cserélése, amíg az robusztusabb úgy érheti el őket, hogy le az üzenetet a Get-WinEvent parancsmaggal, és használja a **tulajdonságok** az üzenet tömbje.</span><span class="sxs-lookup"><span data-stu-id="c6039-146">While they are replaced with the actual values in the message text, a more robust way to access them is to retrieve the message with the Get-WinEvent cmdlet, and then use the **Properties** array of the message.</span></span>

<span data-ttu-id="c6039-147">Íme egy példa hogyan segíthet az ezt a funkciót egy rosszindulatú kísérlet titkosítására és a egy parancsfájl rejtse kicsomagolása:</span><span class="sxs-lookup"><span data-stu-id="c6039-147">Here's an example of how this functionality can help unwrap a malicious attempt to encrypt and obfuscate a script:</span></span>

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

<span data-ttu-id="c6039-148">Ez futó állít elő, a következő naplófájl-bejegyzéseket:</span><span class="sxs-lookup"><span data-stu-id="c6039-148">Running this generates the following log entries:</span></span>

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

Ha a parancsfájl-blokk hossza meghaladja a ETW mi képes üzem egy adott esemény, Windows PowerShell a parancsfájl több részre működésképtelenné válik. <span data-ttu-id="c6039-150">A következő mintakód segítségével egy parancsfájlt annak naplóüzenetek újraegyesítésére:</span><span class="sxs-lookup"><span data-stu-id="c6039-150">Here is sample code to recombine a script from its log messages:</span></span>

```powershell
$created = Get-WinEvent -FilterHashtable @{ ProviderName="Microsoft-Windows-PowerShell"; Id = 4104 } | Where-Object { $_.<...> }
$sortedScripts = $created | sort { $_.Properties[0].Value }
$mergedScript = -join ($sortedScripts | % { $_.Properties[2].Value })
```

<span data-ttu-id="c6039-151">Csakúgy, mint az összes naplózási rendszerek, amelyek egy korlátozott megőrzési puffert (azaz ETW-naplók), ez az infrastruktúra egyik támadások az kéréssekkel túlterhelheti a naplót a korábbi bizonyíték elrejtése jelezhet eseményeket.</span><span class="sxs-lookup"><span data-stu-id="c6039-151">As with all logging systems that have a limited retention buffer (i.e. ETW logs), one attack against this infrastructure is to flood the log with spurious events to hide earlier evidence.</span></span> <span data-ttu-id="c6039-152">Megóvhatja a támadás, gondoskodjon arról, hogy van-e valamilyen esemény naplógyűjtés beállítása (azaz a Windows-Eseménytovábbítás, [gyorsabban a támadó a Windows Eseménynapló-figyelést](https://www.iad.gov/iad/library/reports/spotting-the-adversary-with-windows-event-log-monitoring.cfm)) minden, a számítógép eseménynaplóinak áthelyezése a lehető leghamarabb.</span><span class="sxs-lookup"><span data-stu-id="c6039-152">To protect yourself from this attack, ensure that you have some form of event log collection set up (i.e., Windows Event Forwarding, [Spotting the Adversary with Windows Event Log Monitoring](https://www.iad.gov/iad/library/reports/spotting-the-adversary-with-windows-event-log-monitoring.cfm)) to move event logs off of the computer as soon as possible.</span></span>
