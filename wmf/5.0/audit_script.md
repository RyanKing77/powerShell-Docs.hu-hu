---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 2c3cc6d5d226daf22c7ee83a1b7068d6a08b7f45
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="script-tracing-and-logging"></a>Parancsfájl- naplózását

Amíg a Windows PowerShell már rendelkezik a **LogPipelineExecutionDetails** csoportházirend beállítás parancsmagok meghívását bejelentkezni, PowerShell programozási nyelv bőven van, amelyeket érdemes naplózni és/vagy a naplózási szolgáltatások. Az új részletes parancsfájl követés funkcióját lehetővé teheti, hogy részletes nyomon követését és a Windows PowerShell parancsfájl-kezelési a rendszerben használt elemzését. Részletes parancsfájl nyomkövetésének engedélyezése után a Windows PowerShell naplózza az összes parancsfájl-blokkokban ETW Eseménynapló **Microsoft-Windows-PowerShell/műveleti**. Parancsprogram-blokkot egy másik parancsfájlblokk (például egy parancsfájlt, amely meghívja az Invoke-Expression parancsmag egy karakterlánc) hoz létre, ha adott eredményül kapott parancsfájlblokk is naplózza.

Ezek az események naplózása keresztül engedélyezhető a **kapcsolja be a PowerShell parancsfájl-blokk naplózás** csoportházirend-beállítás (Felügyeleti sablonok -> Windows-összetevők Windows PowerShell ->).

Az események a következők:

| Csatorna | Működési                                 |
|---------|---------------------------------------------|
| Szint   | Részletes                                     |
| Műveleti kód  | Létrehozás                                      |
| Művelet    | CommandStart                                |
| Kulcsszó | Futási térben                                    |
| Eseményazonosító | Engine_ScriptBlockCompiled (0x1008 = 4104)  |
| Üzenet | A parancsprogram-blokk szöveg (%1 % 2) létrehozása: </br> %3 </br> A parancsprogram-blokk azonosítója: %4 |


A ágyazva az üzenet szövege felméréséhez összeállítani a parancsprogram-blokkot tartalmazzon. Az azonosító egy GUID, amely a parancsprogram-blokkot tartalmazzon élettartama megmarad:.

Ha engedélyezi a részletes naplózást, a záró jelölők, és a szolgáltatás írási megkezdéséhez:

| Csatorna | Működési                                            |
|---------|--------------------------------------------------------|
| Szint   | Részletes                                                |
| Műveleti kód  | Nyissa meg a (/ bezárása)                                         |
| Művelet    | CommandStart (/ CommandStop)                           |
| Kulcsszó | Futási térben                                               |
| Eseményazonosító | A parancsprogram-blokk\_meghívása\_Start\_(0x1009 = 4105) részletei / </br> A parancsprogram-blokk\_meghívása\_teljes\_részletei (0x100A Határolók = 4106) |
| Üzenet | Elindítva (/ befejezett) hívása nem volt a parancsprogram-blokk-azonosító: %1 </br> Futási térben azonosítója: %2 |

Az azonosító a script blokkból (amelyek is egyeztetés szükséges eseményazonosító 0x1008) képviselő GUID, és a futási teret ID jelöli, amelyben a parancsfájl-blokkban futtatták futási térben.

A meghívási üzenetben százalékjelek strukturált ETW-tulajdonságok jelölik. Váltják fel az üzenet szövege a tényleges értékek, amíg egy sokkal hatékonyabban elérhet módja a Get-WinEvent parancsmaggal üzenet olvasható be, és használja a **tulajdonságok** tömb az üzenet.

Itt látható egy példa hogyan Ez a funkció elősegíti titkosítására és takarják a parancsfájl egy rosszindulatú kísérlet kicsomagolásához:

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

A következő naplóbejegyzések fut állít elő:

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

Ha a parancsfájl a blokk hossza meghaladja az ETW Újdonságok képes egy adott esemény üzem, a Windows PowerShell bontja a parancsfájl több részből. Itt látható mintakód kombinálhatja az a naplózott üzeneteket egy parancsfájlt:

```powershell
$created = Get-WinEvent -FilterHashtable @{ ProviderName="Microsoft-Windows-PowerShell"; Id = 4104 } | Where-Object { $_.<...> }
$sortedScripts = $created | sort { $_.Properties[0].Value }
$mergedScript = -join ($sortedScripts | % { $_.Properties[2].Value })
```

Összes naplózási rendszerekhez, amelyek rendelkeznek egy korlátozott megőrzési puffer (azaz ETW-naplók), egy az infrastruktúra elleni, mindig a naplófájl korábbi bizonyító adatok elrejtése jelezhet események kéréssekkel. Saját kezűleg a támadások elleni védelméhez, győződjön meg arról, hogy rendelkezik-e valamilyen esemény naplógyűjtést beállítása (például Windows-Eseménytovábbítással, [a Windows Eseménynapló figyelési ellenfél gyorsabban](http://www.nsa.gov/ia/_files/app/Spotting_the_Adversary_with_Windows_Event_Log_Monitoring.pdf)) eseménynaplók ki a számítógépre, nem helyezhető át a lehető leghamarabb.

