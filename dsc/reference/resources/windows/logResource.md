---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-Log erőforrás
ms.openlocfilehash: 1f94a2d847a4ef63f81e2fb83d1a0f76f5677b09
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684240"
---
# <a name="dsc-log-resource"></a>DSC-Log erőforrás

> _A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0_

A __Log__ erőforrás a Windows PowerShell Desired State Configuration (DSC) biztosít olyan mechanizmus, amellyel üzeneteket írhat a Microsoft-Windows-Desired State Configuration / elemzési eseménynaplójában.

```
Syntax

Log [string] #ResourceName
{
    Message = [string]
    [ DependsOn = [string[]] ]
}
```

> [!NOTE]
> A DSC csak a műveleti naplókban alapértelmezés szerint engedélyezve van. Mielőtt az elemzési naplóját érhető el vagy látható lesz, azt engedélyezni kell. További információkért lásd: [hol vannak a DSC-eseménynaplók?](../../../troubleshooting/troubleshooting.md#where-are-dsc-event-logs).

## <a name="properties"></a>Tulajdonságok

| Tulajdonság | Leírás |
| --- | --- |
| Üzenet| Azt jelzi, hogy az üzenetet a konfigurációs és elemzési Microsoft-Windows-Desired állapot eseménynaplójába írhatja.|
| DependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációját a naplófájlüzenetre lekérdezi írása előtt kell futtatni. Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van **ResourceName** és a típusa **ResourceType**, ez a tulajdonság használata esetén `DependsOn = '[ResourceType]ResourceName'`.|

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan üzenet hozzáadása a konfigurációs és elemzési Microsoft-Windows-Desired állapot eseménynaplójában.

> [!NOTE]
> Ha [a Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) ehhez az erőforráshoz konfigurált, és mindig adja vissza **$false**.

```powershell
Configuration logResourceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node localhost
    {
        Log LogExample
        {
            Message = 'This message will appear in the Microsoft-Windows-Desired State Configuration/Analytic event log.'
        }
    }
}
```
