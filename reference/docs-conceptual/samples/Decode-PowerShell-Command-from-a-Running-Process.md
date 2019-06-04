---
ms.date: 11/13/2018
keywords: PowerShell, a parancsmag
title: PowerShell-parancs dekódolása futó folyamatból
author: randomnote1
ms.openlocfilehash: a6c01d8edf67aba6c47350a97cc0ceec4801ad29
ms.sourcegitcommit: bc42c9166857147a1ecf9924b718d4a48eb901e3
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/03/2019
ms.locfileid: "66470967"
---
# <a name="decode-a-powershell-command-from-a-running-process"></a>PowerShell-parancs dekódolása futó folyamatból

Időnként szükség lehet egy PowerShell-folyamat fut, amely nagy mennyiségű erőforrást másolatot tart.
Ez a folyamat keretében is futhat egy [A Feladatütemező][] feladat vagy egy [SQL Server Agent][] feladat. Amennyiben több PowerShell processzorához, nehéz meghatározni, melyik folyamat jelenti. a probléma lehet. Ez a cikk bemutatja, hogyan való dekódolandó egy PowerShell-folyamat éppen futó parancsprogram-blokkot.

## <a name="create-a-long-running-process"></a>Hozzon létre egy hosszú ideig futó folyamatot

Ebben a forgatókönyvben bemutatása, nyisson meg egy új PowerShell-ablakot, és futtassa a következő kódot. Egy PowerShell-parancsot, amely egy száma percenként 10 percig végrehajtása.

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

## <a name="view-the-process"></a>A folyamat megtekintése

A paranccsal, amely végrehajtja az PowerShell törzse tárolja a **CommandLine** tulajdonságát a [Win32_Process][] osztály. Ha a parancs egy kódolt parancsot a **CommandLine** tulajdonság "EncodedCommand" karakterláncot tartalmazza. Ezen információk alapján a kódolt parancs lehet megszüntetéséhez rejtjelezett a következő folyamat-n keresztül.

Indítsa el a Powershellt rendszergazdaként. Rendkívül fontos, hogy rendszergazdaként futtatja-e a PowerShell, ellenkező esetben nem jár eredménnyel a futó folyamatok lekérdezése során.

Hajtsa végre a következő parancsot a PowerShell-folyamatokat, amelyek egy kódolt parancs minden:

```powershell
$powerShellProcesses = Get-CimInstance -ClassName Win32_Process -Filter 'CommandLine LIKE "%EncodedCommand%"'
```

A következő parancs létrehoz egy egyéni PowerShell-objektumot, amely tartalmazza a Folyamatazonosítója, és a kódolt parancsot.

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

Most már vissza tudja fejteni a kódolt parancsot. Az alábbi kódrészlet a parancsobjektumban részletek ismétel, visszafejti a kódolt parancsot és a dekódolt parancs hozzáadja az objektumra további vizsgálat.

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

A dekódolt parancs most a dekódolt parancs tulajdonságát kiválasztásával tekinthető meg.

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

[A Feladatütemező]: /windows/desktop/TaskSchd/task-scheduler-start-page
[SQL Server Agent]: /sql/ssms/agent/sql-server-agent
[Win32_Process]: /windows/desktop/CIMWin32Prov/win32-process
