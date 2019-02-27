---
title: A hibajelentési fogalmak |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- non-terminating errors [PowerShell SDK]
- errors [PowerShell SDK], described
- terminating errors [PowerShell SDK]
- errors [PowerShell SDK]
ms.assetid: 0dce97c0-bd9a-4691-8ca3-e8d5dea902c5
caps.latest.revision: 11
ms.openlocfilehash: aac6b7b6ac8a0fad15194b6d3f92c434524fabdb
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846164"
---
# <a name="error-reporting-concepts"></a><span data-ttu-id="f3176-102">Hibajelentés – Fogalmak</span><span class="sxs-lookup"><span data-stu-id="f3176-102">Error Reporting Concepts</span></span>

<span data-ttu-id="f3176-103">Windows PowerShell biztosít, két mechanizmusok hibákat jelentő: egy mechanizmusa *megszakítást okozó hibák* és a egy másik mechanizmust *okozó*.</span><span class="sxs-lookup"><span data-stu-id="f3176-103">Windows PowerShell provides two mechanisms for reporting errors: one mechanism for *terminating errors* and another mechanism for *non-terminating errors*.</span></span> <span data-ttu-id="f3176-104">Fontos a parancsmag hibák jelentéséhez megfelelően, hogy a megfelelő módon reagálhat, amelyen fut a parancsmagokat a gazdaalkalmazást.</span><span class="sxs-lookup"><span data-stu-id="f3176-104">It is important for your cmdlet to report errors correctly so that the host application that is running your cmdlets can react in an appropriate manner.</span></span>

<span data-ttu-id="f3176-105">A parancsmag meg kell hívnia a [System.Management.Automation.Cmdlet.Throwterminatingerror\*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) módszer, ha hiba történik, amely nem létezik, vagy nem teszi lehetővé a parancsmagot, hogy a bemeneti objektumok feldolgozásához.</span><span class="sxs-lookup"><span data-stu-id="f3176-105">Your cmdlet should call the [System.Management.Automation.Cmdlet.Throwterminatingerror\*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) method when an error occurs that does not or should not allow the cmdlet to continue to process its input objects.</span></span> <span data-ttu-id="f3176-106">A parancsmag meg kell hívnia a [System.Management.Automation.Cmdlet.Writeerror\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) okozó jelentés küldése, ha a parancsmag továbbra is a bemeneti objektumok feldolgozása metódust.</span><span class="sxs-lookup"><span data-stu-id="f3176-106">Your cmdlet should call the [System.Management.Automation.Cmdlet.Writeerror\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) method to report non-terminating errors when the cmdlet can continue processing the input objects.</span></span> <span data-ttu-id="f3176-107">Mindkét módszer adjon meg egy hiba rekordot, amely a gazdaalkalmazást a hiba okának kivizsgálására használható.</span><span class="sxs-lookup"><span data-stu-id="f3176-107">Both methods provide an error record that the host application can use to investigate the cause of the error.</span></span>

<span data-ttu-id="f3176-108">Az alábbi irányelvek segítségével meghatározhatja, hogy hiba a megszakítást okozó vagy megszakítást nem okozó hiba.</span><span class="sxs-lookup"><span data-stu-id="f3176-108">Use the following guidelines to determine whether an error is a terminating or non-terminating error.</span></span>

- <span data-ttu-id="f3176-109">Hiba a megszakító hiba esetén megakadályozza, hogy a parancsmag az aktuális objektum feldolgozása továbbra is, illetve további bemeneti objektumokat, függetlenül attól, hogy a tartalmat sikerült feldolgozása.</span><span class="sxs-lookup"><span data-stu-id="f3176-109">An error is a terminating error if it prevents your cmdlet from continuing to process the current object or from successfully processing any further input objects, regardless of their content.</span></span>

- <span data-ttu-id="f3176-110">Hiba megszakító hibát, ha nem szeretné, a parancsmag folytatja az aktuális objektum vagy bármilyen további bemeneti objektumokhoz, függetlenül attól, hogy a tartalmat feldolgozása.</span><span class="sxs-lookup"><span data-stu-id="f3176-110">An error is a terminating error if you do not want your cmdlet to continue processing the current object or any further input objects, regardless of their content.</span></span>

- <span data-ttu-id="f3176-111">Hiba egy hibát, amely nem fogadja el vagy egy objektumot ad vissza a parancsmag a esetén vagy akkor következik be, amely fogad el, vagy csak egy objektumot ad vissza a parancsmag.</span><span class="sxs-lookup"><span data-stu-id="f3176-111">An error is a terminating error if it occurs in a cmdlet that does not accept or return an object or if it occurs in a cmdlet that accepts or returns only one object.</span></span>

- <span data-ttu-id="f3176-112">Hiba történt egy nem megszakító hiba esetén folytatja a parancsmag az aktuális objektum és minden további bemeneti objektumot feldolgozása.</span><span class="sxs-lookup"><span data-stu-id="f3176-112">An error is a non-terminating error if you want your cmdlet to continue processing the current object and any further input objects.</span></span>

- <span data-ttu-id="f3176-113">Hiba történt egy nem megszakító hiba esetén kapcsolatos, adott bemeneti objektum vagy bemeneti objektumok részét.</span><span class="sxs-lookup"><span data-stu-id="f3176-113">An error is a non-terminating error if it is related to a specific input object or subset of input objects.</span></span>

## <a name="see-also"></a><span data-ttu-id="f3176-114">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="f3176-114">See Also</span></span>

[<span data-ttu-id="f3176-115">System.Management.Automation.Cmdlet.Throwterminatingerror\*</span><span class="sxs-lookup"><span data-stu-id="f3176-115">System.Management.Automation.Cmdlet.Throwterminatingerror\*</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError)

[<span data-ttu-id="f3176-116">System.Management.Automation.Cmdlet.Writeerror\*</span><span class="sxs-lookup"><span data-stu-id="f3176-116">System.Management.Automation.Cmdlet.Writeerror\*</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.WriteError)

[<span data-ttu-id="f3176-117">Windows PowerShell Hibarekordjainak</span><span class="sxs-lookup"><span data-stu-id="f3176-117">Windows PowerShell Error Records</span></span>](./windows-powershell-error-records.md)

[<span data-ttu-id="f3176-118">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="f3176-118">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
