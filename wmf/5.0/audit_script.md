---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 28cd186ab3a08a0da4ff81f5a21514f239770d13
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684660"
---
# <a name="script-tracing-and-logging"></a>Parancsfájlok nyomkövetése és naplózása

Bár a Windows PowerShell már rendelkezik a **LogPipelineExecutionDetails** csoportházirend beállítás parancsmagok meghívását bejelentkezni, a PowerShell szkriptelési nyelv rendelkezik, amelyeket érdemes naplózni, és/vagy a naplózási szolgáltatások rengeteg. Az új parancsfájl részletes nyomkövetési szolgáltatás engedélyezi a részletes nyomon követési és elemzési rendszerek a Windows PowerShell parancsfájl-kezelési használati teszi lehetővé. Miután engedélyezte a részletes parancsfájl nyomkövetés, Windows PowerShell az összes parancsfájl-blokkokban naplózza az ETW-eseménynaplóba **Microsoft-Windows-PowerShell/műveleti**. Ha parancsprogram-blokkot hoz létre egy másik parancsfájlblokkban (például egy parancsfájlt, amely meghívja az Invoke-Expression parancsmag egy karakterlánc), a létrejövő parancsfájlblokkban, valamint a rendszer naplózza.

Ezek az események naplózása keresztül engedélyezhető a **kapcsolja be a PowerShell parancsfájl-blokk naplózás** csoportházirend-beállítás (Felügyeleti sablonok -> Windows-összetevők Windows PowerShell ->).

Az események a következők:

| Csatorna | Működési                                 |
|---------|---------------------------------------------|
| Szint   | Részletes                                     |
| Opcode  | Létrehozás                                      |
| Művelet    | CommandStart                                |
| Kulcsszó | futási térben                                    |
| EventId | Engine_ScriptBlockCompiled (0x1008 = 4104)  |
| Üzenet | Hozza létre a scriptblock kulcsszót szöveg (%1 % 2): </br> %3 </br> ScriptBlock azonosítója: %4 |


Ágyazva az üzenet szövege a lefordított parancsfájlblokk mértékét. Az azonosító egy GUID Azonosítót a parancsprogram-blokkot élettartama a megőrzött.

Ha engedélyezi a részletes naplózást, funkció kezdő és záró jelölők:

| Csatorna | Működési                                            |
|---------|--------------------------------------------------------|
| Szint   | Részletes                                                |
| Opcode  | Nyissa meg a (/ bezárása)                                         |
| Művelet    | CommandStart (/ CommandStop)                           |
| Kulcsszó | futási térben                                               |
| EventId | ScriptBlock\_meghívása\_Start\_Detail (0x1009 = 4105) / </br> ScriptBlock\_meghívása\_teljes\_Detail (0x100A Határolók = 4106) |
| Üzenet | Elindítva (/ befejezett) hívja meg a scriptblock kulcsszó-azonosító: %1 </br> Futási térben azonosítója: %2 |

Az azonosító a globálisan egyedi Azonosítót a parancsprogram-blokkot (hogy összekapcsolhatók legyenek 0x1008 eseményazonosító) jelölő, és a futási térben Azonosítóját jelöli, amelyben a parancsprogram-blokkot volt futtatva futási térben.

A meghívási üzenetben százalékjelek strukturált ETW-tulajdonságok jelentik. Az üzenet szövege a tényleges értékek cserélése, amíg az robusztusabb úgy érheti el őket, hogy le az üzenetet a Get-WinEvent parancsmaggal, és használja a **tulajdonságok** az üzenet tömbje.

Íme egy példa hogyan segíthet az ezt a funkciót egy rosszindulatú kísérlet titkosítására és a egy parancsfájl rejtse kicsomagolása:

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

Ez futó állít elő, a következő naplófájl-bejegyzéseket:

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

Ha a parancsfájl-blokk hossza meghaladja a ETW mi képes üzem egy adott esemény, Windows PowerShell a parancsfájl több részre működésképtelenné válik. A következő mintakód segítségével egy parancsfájlt annak naplóüzenetek újraegyesítésére:

```powershell
$created = Get-WinEvent -FilterHashtable @{ ProviderName="Microsoft-Windows-PowerShell"; Id = 4104 } | Where-Object { $_.<...> }
$sortedScripts = $created | sort { $_.Properties[0].Value }
$mergedScript = -join ($sortedScripts | % { $_.Properties[2].Value })
```

Csakúgy, mint az összes naplózási rendszerek, amelyek egy korlátozott megőrzési puffert (azaz ETW-naplók), ez az infrastruktúra egyik támadások az kéréssekkel túlterhelheti a naplót a korábbi bizonyíték elrejtése jelezhet eseményeket. Megóvhatja a támadás, gondoskodjon arról, hogy van-e valamilyen esemény naplógyűjtés beállítása (azaz a Windows-Eseménytovábbítás, [gyorsabban a támadó a Windows Eseménynapló-figyelést](https://www.iad.gov/iad/library/reports/spotting-the-adversary-with-windows-event-log-monitoring.cfm)) minden, a számítógép eseménynaplóinak áthelyezése a lehető leghamarabb.
