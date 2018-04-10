---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC-napló erőforrás
ms.openlocfilehash: f1a528767508d4a0e7f0ea2e58fd27a6a4d7ec75
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-log-resource"></a>A DSC-napló erőforrás

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A __napló__ erőforrás a Windows PowerShell szükséges konfiguráló (DSC) üzeneteket írni a Microsoft-Windows-kívánt állapot konfigurációs/elemzési Eseménynapló mechanizmust biztosít.

```
Syntax

Log [string] #ResourceName
{
    Message = [string]
    [ DependsOn = [string[]] ]
}
```

Megjegyzés: Alapértelmezés szerint csak a műveleti naplókat DSC engedélyezve van.
Mielőtt a elemzési naplóját lesznek elérhetők, engedélyezni kell.
Tekintse meg a következő cikket.

[Hol találhatók a DSC-eseménynaplók?](https://msdn.microsoft.com/en-us/powershell/dsc/troubleshooting#where-are-dsc-event-logs)

## <a name="properties"></a>Tulajdonságok
|  Tulajdonság  |  Leírás   |
|---|---|
| Üzenet| Azt jelzi, hogy a konfiguráció/elemzési Microsoft-Windows-Desired állapot eseménynaplójába írhatja kívánt üzenetet.|
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, a napló üzenet beolvasása előtt. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Példa

A következő példa bemutatja, hogyan üzenet tartalmazza a Microsoft-Windows-Desired állapot konfigurációs/elemzési eseménynaplójában.

> **Megjegyzés:**: futtatásakor [teszt-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) az ehhez az erőforráshoz konfigurált, akkor a rendszer mindig visszaküldi **$false**.

```powershell
Configuration logResourceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node localhost

    {
        Log LogExample
        {
            Message = "This message will appear in the Microsoft-Windows-Desired State Configuration/Analytic event log."
        }
    }
}
```