---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
title: A WMF 5.1 PowerShell motor fejlesztései
ms.openlocfilehash: 3c69c4e13f64683f743eb78b0c9e177ff5b3a771
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
#<a name="powershell-engine-improvements"></a>PowerShell-motor fejlesztései

A core PowerShell motor az alábbi fejlesztések történtek WMF 5.1:


## <a name="performance"></a>Teljesítmény ##

Jobb teljesítmény, néhány fontos területeken:

- Indítás
- Például a ForEach-Object és a Where-Object-parancsmagjainak futószalagos körülbelül 50 %-kal gyorsabb

Néhány példa fejlesztései (az eltérő attól függően, hogy a hardver):

| Forgatókönyv | 5.0 idő (ms) | 5.1 idő (ms) |
| -------- | :---------------: | :---------------: |
| `powershell -command "echo 1"` | 900 | 250 |
| Első legalább egyszer PowerShell futtatása: `powershell -command "Unknown-Command"` | 30000 | 13000 |
| A parancs elemzési gyorsítótár beépített: `powershell -command "Unknown-Command"` | 7000 | 520 |
| <code>1..1000000 &#124; % { }</code> | 1400 | 750 |

> Megjegyzés: indítási kapcsolódik egy módosítása hatással lehet egyes forgatókönyvek nem támogatott.
> PowerShell már nem olvassa a fájlokat `$pshome\*.ps1xml` – ezek a fájlok konvertált C# elkerülése érdekében néhány fájlt, és a CPU-terhelés az XML feldolgozási fájlokat.
A fájlok még mindig léteznek támogatásához V2-mellé, ha módosítja a fájl tartalmát, azt fogja nincs hatása V5, csak V2.
Vegye figyelembe, hogy ezek a fájlok tartalmának módosítása nem támogatott.

Egy másik látható változást, hogy milyen módon gyorsítótárazza a PowerShell az exportált parancsokat és egyéb adatait, amely a rendszerre telepített modulok.
Korábban, a gyorsítótárban tárolta a címtárban `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\CommandAnalysis`.
WMF 5.1, a gyorsítótár egy olyan egyetlen fájl `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.
Lásd: [modul elemzés gyorsítótár](scenarios-features.md#module-analysis-cache) további részleteket.