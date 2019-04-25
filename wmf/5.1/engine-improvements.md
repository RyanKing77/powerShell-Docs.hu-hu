---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: A WMF 5.1 PowerShell motor fejlesztései
ms.openlocfilehash: 738f72b910de7d44f48309013237d523d0dd40a4
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62055564"
---
# <a name="powershell-engine-improvements"></a>PowerShell motor fejlesztései

A core PowerShell motor a következő fejlesztések történtek a WMF 5.1:

## <a name="performance"></a>Teljesítmény

Teljesítmény javulását néhány fontos területeken:

- Indítás
- Az adatcsatornás feldolgozás parancsmagokhoz hasonlóan `ForEach-Object` és `Where-Object` körülbelül 50 %-kal gyorsabb van

Néhány példa fejlesztései (a az eredményeket a hardverektől függően változhat):

| Forgatókönyv | 5.0-s idő (ms) | 5.1 idő (ms) |
| -------- | :---------------: | :---------------: |
| `powershell -command "echo 1"` | 900 | 250 |
| Először minden eddiginél PowerShell futtatása: `powershell -command "Unknown-Command"` | 30000 | 13000 |
| Parancs a beépített elemzési gyorsítótár: `powershell -command "Unknown-Command"` | 7000 | 520 |
| <code>1..1000000 &#124; % { }</code> | 1400 | 750 |

> [!Note]
> Indítási kapcsolatos egy módosítása hatással lehet a bizonyos nem támogatott forgatókönyveket.
> PowerShell már nem olvassa a fájlokat `$pshome\*.ps1xml` – ezek a fájlok konvertált C# néhány fájl és a Processzor terhelését az XML-fájlok feldolgozásának elkerülése érdekében.
> A fájlok továbbra is léteznek támogatási V2 egymás mellett, így a fájl tartalmának módosítása esetén ez nem lesz bármilyen hatása V5 verzióra, csak V2.
> Vegye figyelembe, hogy ezek a fájlok tartalmának módosítása soha nem volt támogatott.

Egy másik látható változást, hogy hogyan gyorsítótárazza a PowerShell, az exportált parancsokat és más információkat rendszerre telepített modulok.
Korábban, a gyorsítótár a könyvtár a tárolt `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\CommandAnalysis`.
A WMF 5.1-es, a gyorsítótár nem egyetlen fájl `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.
Lásd: [modul elemzési gyorsítótár](scenarios-features.md#module-analysis-cache) további részletekért.