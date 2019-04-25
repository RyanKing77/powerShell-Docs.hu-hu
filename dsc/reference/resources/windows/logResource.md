---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-Log erőforrás
ms.openlocfilehash: 1f94a2d847a4ef63f81e2fb83d1a0f76f5677b09
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62077228"
---
# <a name="dsc-log-resource"></a><span data-ttu-id="37a46-103">DSC-Log erőforrás</span><span class="sxs-lookup"><span data-stu-id="37a46-103">DSC Log Resource</span></span>

> <span data-ttu-id="37a46-104">_A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0_</span><span class="sxs-lookup"><span data-stu-id="37a46-104">_Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0_</span></span>

<span data-ttu-id="37a46-105">A __Log__ erőforrás a Windows PowerShell Desired State Configuration (DSC) biztosít olyan mechanizmus, amellyel üzeneteket írhat a Microsoft-Windows-Desired State Configuration / elemzési eseménynaplójában.</span><span class="sxs-lookup"><span data-stu-id="37a46-105">The __Log__ resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to write messages to the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>

```
Syntax

Log [string] #ResourceName
{
    Message = [string]
    [ DependsOn = [string[]] ]
}
```

> [!NOTE]
> <span data-ttu-id="37a46-106">A DSC csak a műveleti naplókban alapértelmezés szerint engedélyezve van.</span><span class="sxs-lookup"><span data-stu-id="37a46-106">By default only the Operational logs for DSC are enabled.</span></span> <span data-ttu-id="37a46-107">Mielőtt az elemzési naplóját érhető el vagy látható lesz, azt engedélyezni kell.</span><span class="sxs-lookup"><span data-stu-id="37a46-107">Before the Analytic log will be available or visible, it must be enabled.</span></span> <span data-ttu-id="37a46-108">További információkért lásd: [hol vannak a DSC-eseménynaplók?](../../../troubleshooting/troubleshooting.md#where-are-dsc-event-logs).</span><span class="sxs-lookup"><span data-stu-id="37a46-108">For more information, see [Where are DSC Event Logs?](../../../troubleshooting/troubleshooting.md#where-are-dsc-event-logs).</span></span>

## <a name="properties"></a><span data-ttu-id="37a46-109">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="37a46-109">Properties</span></span>

| <span data-ttu-id="37a46-110">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="37a46-110">Property</span></span> | <span data-ttu-id="37a46-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="37a46-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="37a46-112">Üzenet</span><span class="sxs-lookup"><span data-stu-id="37a46-112">Message</span></span>| <span data-ttu-id="37a46-113">Azt jelzi, hogy az üzenetet a konfigurációs és elemzési Microsoft-Windows-Desired állapot eseménynaplójába írhatja.</span><span class="sxs-lookup"><span data-stu-id="37a46-113">Indicates the message you want to write to the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>|
| <span data-ttu-id="37a46-114">DependsOn</span><span class="sxs-lookup"><span data-stu-id="37a46-114">DependsOn</span></span> | <span data-ttu-id="37a46-115">Azt jelzi, hogy egy másik erőforrás konfigurációját a naplófájlüzenetre lekérdezi írása előtt kell futtatni.</span><span class="sxs-lookup"><span data-stu-id="37a46-115">Indicates that the configuration of another resource must run before this log message gets written.</span></span> <span data-ttu-id="37a46-116">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van **ResourceName** és a típusa **ResourceType**, ez a tulajdonság használata esetén `DependsOn = '[ResourceType]ResourceName'`.</span><span class="sxs-lookup"><span data-stu-id="37a46-116">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = '[ResourceType]ResourceName'`.</span></span>|

## <a name="example"></a><span data-ttu-id="37a46-117">Példa</span><span class="sxs-lookup"><span data-stu-id="37a46-117">Example</span></span>

<span data-ttu-id="37a46-118">Az alábbi példa bemutatja, hogyan üzenet hozzáadása a konfigurációs és elemzési Microsoft-Windows-Desired állapot eseménynaplójában.</span><span class="sxs-lookup"><span data-stu-id="37a46-118">The following example shows how to include a message in the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>

> [!NOTE]
> <span data-ttu-id="37a46-119">Ha [a Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) ehhez az erőforráshoz konfigurált, és mindig adja vissza **$false**.</span><span class="sxs-lookup"><span data-stu-id="37a46-119">If you run [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) with this resource configured, it will always return **$false**.</span></span>

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
