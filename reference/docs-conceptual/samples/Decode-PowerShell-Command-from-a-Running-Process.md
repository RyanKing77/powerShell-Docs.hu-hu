---
ms.date: 11/13/2018
keywords: PowerShell, a parancsmag
title: PowerShell-parancs dekódolása futó folyamatból
author: randomnote1
ms.openlocfilehash: a0602070a8c5b60ce0bb09e227690f48d970a868
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404170"
---
# <a name="decode-a-powershell-command-from-a-running-process"></a><span data-ttu-id="69ae1-103">PowerShell-parancs dekódolása futó folyamatból</span><span class="sxs-lookup"><span data-stu-id="69ae1-103">Decode a PowerShell command from a running process</span></span>

<span data-ttu-id="69ae1-104">Időnként szükség lehet egy PowerShell-folyamat fut, amely nagy mennyiségű erőforrást másolatot tart.</span><span class="sxs-lookup"><span data-stu-id="69ae1-104">At times, you may have a PowerShell process running that is taking up a large amount of resources.</span></span>
<span data-ttu-id="69ae1-105">Ez a folyamat keretében is futhat egy [Feladatütemező][] feladat vagy egy [SQL Server Agent][] feladat.</span><span class="sxs-lookup"><span data-stu-id="69ae1-105">This process could be running in the context of a [Task Scheduler][] job or a [SQL Server Agent][] job.</span></span> <span data-ttu-id="69ae1-106">Amennyiben több PowerShell processzorához, nehéz meghatározni, melyik folyamat jelenti. a probléma lehet.</span><span class="sxs-lookup"><span data-stu-id="69ae1-106">Where there are multiple PowerShell processes running, it can be difficult to know which process represents the problem.</span></span> <span data-ttu-id="69ae1-107">Ez a cikk bemutatja, hogyan való dekódolandó egy PowerShell-folyamat éppen futó parancsprogram-blokkot.</span><span class="sxs-lookup"><span data-stu-id="69ae1-107">This article shows how to decode a script block that a PowerShell process is currently running.</span></span>

## <a name="create-a-long-running-process"></a><span data-ttu-id="69ae1-108">Hozzon létre egy hosszú ideig futó folyamatot</span><span class="sxs-lookup"><span data-stu-id="69ae1-108">Create a long running process</span></span>

<span data-ttu-id="69ae1-109">Ebben a forgatókönyvben bemutatása, nyisson meg egy új PowerShell-ablakot, és futtassa a következő kódot.</span><span class="sxs-lookup"><span data-stu-id="69ae1-109">To demonstrate this scenario, open a new PowerShell window and run the following code.</span></span> <span data-ttu-id="69ae1-110">Egy PowerShell-parancsot, amely egy száma percenként 10 percig végrehajtása.</span><span class="sxs-lookup"><span data-stu-id="69ae1-110">It executes a PowerShell command that outputs a number every minute for 10 minutes.</span></span>

```powershell
powershell.exe -Command {
    $i = 1
    while ( $i -le 10 )
    {
        Write-Output -InputObject $i
        Start-Sleep -Seconds 60
        $i++
    }
}
```

## <a name="view-the-process"></a><span data-ttu-id="69ae1-111">A folyamat megtekintése</span><span class="sxs-lookup"><span data-stu-id="69ae1-111">View the process</span></span>

<span data-ttu-id="69ae1-112">A paranccsal, amely végrehajtja az PowerShell törzse tárolja a **CommandLine** tulajdonságát a [Win32_Process][] osztály.</span><span class="sxs-lookup"><span data-stu-id="69ae1-112">The body of the command which PowerShell is executing is stored in the **CommandLine** property of the [Win32_Process][] class.</span></span> <span data-ttu-id="69ae1-113">Ha a parancs egy [parancs kódolású][], a **CommandLine** tulajdonság "EncodedCommand" karakterláncot tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="69ae1-113">If the command is an [encoded command][], the **CommandLine** property contains the string "EncodedCommand".</span></span> <span data-ttu-id="69ae1-114">Ezen információk alapján a kódolt parancs lehet megszüntetéséhez rejtjelezett a következő folyamat-n keresztül.</span><span class="sxs-lookup"><span data-stu-id="69ae1-114">Using this information, the encoded command can be de-obfuscated via the following process.</span></span>

<span data-ttu-id="69ae1-115">Indítsa el a Powershellt rendszergazdaként.</span><span class="sxs-lookup"><span data-stu-id="69ae1-115">Start PowerShell as Administrator.</span></span> <span data-ttu-id="69ae1-116">Rendkívül fontos, hogy rendszergazdaként futtatja-e a PowerShell, ellenkező esetben nem jár eredménnyel a futó folyamatok lekérdezése során.</span><span class="sxs-lookup"><span data-stu-id="69ae1-116">It is vital that PowerShell is running as administrator, otherwise no results are returned when querying the running processes.</span></span>

<span data-ttu-id="69ae1-117">Hajtsa végre a következő parancsot a PowerShell-folyamatokat, amelyek egy kódolt parancs minden:</span><span class="sxs-lookup"><span data-stu-id="69ae1-117">Execute the following command to get all of the PowerShell processes that have an encoded command:</span></span>

```powershell
$powerShellProcesses = Get-CimInstance -ClassName Win32_Process -Filter 'CommandLine LIKE "%EncodedCommand%"'
```

<span data-ttu-id="69ae1-118">A következő parancs létrehoz egy egyéni PowerShell-objektumot, amely tartalmazza a Folyamatazonosítója, és a kódolt parancsot.</span><span class="sxs-lookup"><span data-stu-id="69ae1-118">The following command creates a custom PowerShell object that contains the process ID and the encoded command.</span></span>

```powershell
$commandDetails = $powerShellProcesses | Select-Object -Property ProcessId,
@{
    name       = 'EncodedCommand'
    expression = {
        if ( $_.CommandLine -match 'encodedCommand (.*) -inputFormat' )
        {
            return $matches[1]
        }
    }
}
```

<span data-ttu-id="69ae1-119">Most már vissza tudja fejteni a kódolt parancsot.</span><span class="sxs-lookup"><span data-stu-id="69ae1-119">Now the encoded command can be decoded.</span></span> <span data-ttu-id="69ae1-120">Az alábbi kódrészlet a parancsobjektumban részletek ismétel, visszafejti a kódolt parancsot és a dekódolt parancs hozzáadja az objektumra további vizsgálat.</span><span class="sxs-lookup"><span data-stu-id="69ae1-120">The following snippet iterates over the command details object, decodes the encoded command, and adds the decoded command back to the object for further investigation.</span></span>

```powershell
$commandDetails | ForEach-Object -Process {
    # Get the current process
    $currentProcess = $_

    # Convert the Base 64 string to a Byte Array
    $commandBytes = [System.Convert]::FromBase64String($currentProcess.EncodedCommand)

    # Convert the Byte Array to a string
    $decodedCommand = [System.Text.Encoding]::Unicode.GetString($commandBytes)

    # Add the decoded command back to the object
    $commandDetails |
        Where-Object -FilterScript { $_.ProcessId -eq $_.ProcessId } |
        Add-Member -MemberType NoteProperty -Name DecodedCommand -Value $decodedCommand
}
$commandDetails[0]
```

<span data-ttu-id="69ae1-121">A dekódolt parancs most a dekódolt parancs tulajdonságát kiválasztásával tekinthető meg.</span><span class="sxs-lookup"><span data-stu-id="69ae1-121">The decoded command can now be reviewed by selecting the decoded command property.</span></span>

```output
ProcessId      : 8752
EncodedCommand : IAAKAAoACgAgAAoAIAAgACAAIAAkAGkAIAA9ACAAMQAgAAoACgAKACAACgAgACAAIAAgAHcAaABpAGwAZQAgACgAIAAkAGkAIAAtAG
                 wAZQAgADEAMAAgACkAIAAKAAoACgAgAAoAIAAgACAAIAB7ACAACgAKAAoAIAAKACAAIAAgACAAIAAgACAAIABXAHIAaQB0AGUALQBP
                 AHUAdABwAHUAdAAgAC0ASQBuAHAAdQB0AE8AYgBqAGUAYwB0ACAAJABpACAACgAKAAoAIAAKACAAIAAgACAAIAAgACAAIABTAHQAYQ
                 ByAHQALQBTAGwAZQBlAHAAIAAtAFMAZQBjAG8AbgBkAHMAIAA2ADAAIAAKAAoACgAgAAoAIAAgACAAIAAgACAAIAAgACQAaQArACsA
                 IAAKAAoACgAgAAoAIAAgACAAIAB9ACAACgAKAAoAIAAKAA==
DecodedCommand :
                     $i = 1

                     while ( $i -le 10 )

                     {

                         Write-Output -InputObject $i

                         Start-Sleep -Seconds 60

                         $i++

                     }
```

[Feladatütemező]: /windows/desktop/TaskSchd/task-scheduler-start-page
[Task Scheduler]: /windows/desktop/TaskSchd/task-scheduler-start-page
[SQL Server Agent]: /sql/ssms/agent/sql-server-agent
[Win32_Process]: /windows/desktop/CIMWin32Prov/win32-process
[parancs kódolású]: /powershell/scripting/core-powershell/console/powershell.exe-command-line-help#-encodedcommand-
[encoded command]: /powershell/scripting/core-powershell/console/powershell.exe-command-line-help#-encodedcommand-
