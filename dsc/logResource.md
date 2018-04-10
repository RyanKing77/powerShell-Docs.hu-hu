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
# <a name="dsc-log-resource"></a><span data-ttu-id="5d40c-103">A DSC-napló erőforrás</span><span class="sxs-lookup"><span data-stu-id="5d40c-103">DSC Log Resource</span></span>

> <span data-ttu-id="5d40c-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="5d40c-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="5d40c-105">A __napló__ erőforrás a Windows PowerShell szükséges konfiguráló (DSC) üzeneteket írni a Microsoft-Windows-kívánt állapot konfigurációs/elemzési Eseménynapló mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="5d40c-105">The __Log__ resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to write messages to the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>

```
Syntax

Log [string] #ResourceName
{
    Message = [string]
    [ DependsOn = [string[]] ]
}
```

<span data-ttu-id="5d40c-106">Megjegyzés: Alapértelmezés szerint csak a műveleti naplókat DSC engedélyezve van.</span><span class="sxs-lookup"><span data-stu-id="5d40c-106">NOTE: By default only the Operational logs for DSC are enabled.</span></span>
<span data-ttu-id="5d40c-107">Mielőtt a elemzési naplóját lesznek elérhetők, engedélyezni kell.</span><span class="sxs-lookup"><span data-stu-id="5d40c-107">Before the Analytic log will be available or visible, it must be enabled.</span></span>
<span data-ttu-id="5d40c-108">Tekintse meg a következő cikket.</span><span class="sxs-lookup"><span data-stu-id="5d40c-108">See the following article.</span></span>

[<span data-ttu-id="5d40c-109">Hol találhatók a DSC-eseménynaplók?</span><span class="sxs-lookup"><span data-stu-id="5d40c-109">Where are DSC Event Logs?</span></span>](https://msdn.microsoft.com/en-us/powershell/dsc/troubleshooting#where-are-dsc-event-logs)

## <a name="properties"></a><span data-ttu-id="5d40c-110">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="5d40c-110">Properties</span></span>
|  <span data-ttu-id="5d40c-111">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="5d40c-111">Property</span></span>  |  <span data-ttu-id="5d40c-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="5d40c-112">Description</span></span>   |
|---|---|
| <span data-ttu-id="5d40c-113">Üzenet</span><span class="sxs-lookup"><span data-stu-id="5d40c-113">Message</span></span>| <span data-ttu-id="5d40c-114">Azt jelzi, hogy a konfiguráció/elemzési Microsoft-Windows-Desired állapot eseménynaplójába írhatja kívánt üzenetet.</span><span class="sxs-lookup"><span data-stu-id="5d40c-114">Indicates the message you want to write to the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>|
| <span data-ttu-id="5d40c-115">dependsOn</span><span class="sxs-lookup"><span data-stu-id="5d40c-115">DependsOn</span></span> | <span data-ttu-id="5d40c-116">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, a napló üzenet beolvasása előtt.</span><span class="sxs-lookup"><span data-stu-id="5d40c-116">Indicates that the configuration of another resource must run before this log message gets written.</span></span> <span data-ttu-id="5d40c-117">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="5d40c-117">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="5d40c-118">Példa</span><span class="sxs-lookup"><span data-stu-id="5d40c-118">Example</span></span>

<span data-ttu-id="5d40c-119">A következő példa bemutatja, hogyan üzenet tartalmazza a Microsoft-Windows-Desired állapot konfigurációs/elemzési eseménynaplójában.</span><span class="sxs-lookup"><span data-stu-id="5d40c-119">The following example shows how to include a message in the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>

> <span data-ttu-id="5d40c-120">**Megjegyzés:**: futtatásakor [teszt-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) az ehhez az erőforráshoz konfigurált, akkor a rendszer mindig visszaküldi **$false**.</span><span class="sxs-lookup"><span data-stu-id="5d40c-120">**Note**: if you run [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) with this resource configured, it will always return **$false**.</span></span>

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