---
title: Megszakítást nem hibák |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 468dabd6-bfeb-448d-8e09-0996db516edd
caps.latest.revision: 8
ms.openlocfilehash: 5f804756e0e3e867832f15f50967fd6987f160a5
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58054357"
---
# <a name="non-terminating-errors"></a><span data-ttu-id="fb931-102">Megszakítást nem okozó hibák</span><span class="sxs-lookup"><span data-stu-id="fb931-102">Non-Terminating Errors</span></span>

<span data-ttu-id="fb931-103">Ez a témakör ismerteti a metódus okozó jelentésére használhatók.</span><span class="sxs-lookup"><span data-stu-id="fb931-103">This topic discusses the method used to report non-terminating errors.</span></span> <span data-ttu-id="fb931-104">Emellett ismerteti a a módszerrel belül a parancsmag meghívása.</span><span class="sxs-lookup"><span data-stu-id="fb931-104">It also discusses how to call the method from within the cmdlet.</span></span>

<span data-ttu-id="fb931-105">Ha egy nem megszakító hiba történik, a parancsmag meghívásával jelentse ezt a hibát a [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) metódust.</span><span class="sxs-lookup"><span data-stu-id="fb931-105">When a non-terminating error occurs, the cmdlet should report this error by calling the [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) method.</span></span> <span data-ttu-id="fb931-106">A parancsmag egy nem megszakító hibát jelent, ha a parancsmag továbbra is megfelelően működjenek a bemeneti objektum és a további bejövő folyamat-objektumokat.</span><span class="sxs-lookup"><span data-stu-id="fb931-106">When the cmdlet reports a non-terminating error, the cmdlet can continue to operate on this input object and on further incoming pipeline objects.</span></span> <span data-ttu-id="fb931-107">Ha a parancsmagot hívja a [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) metódus, a parancsmag egy hiba rekordot, amely leírja a megszakítást nem okozó hiba kiváltó írhat.</span><span class="sxs-lookup"><span data-stu-id="fb931-107">If the cmdlet calls the [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) method, the cmdlet can write an error record that describes the condition that caused the non-terminating error.</span></span> <span data-ttu-id="fb931-108">Hiba a rekordok kapcsolatos további információkért lásd: [Windows PowerShell Hibarekordjainak](./windows-powershell-error-records.md).</span><span class="sxs-lookup"><span data-stu-id="fb931-108">For more information about error records, see [Windows PowerShell Error Records](./windows-powershell-error-records.md).</span></span>

<span data-ttu-id="fb931-109">Parancsmagok segítségével meghívhatja [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) szükség szerint a saját feldolgozási módszerek bemeneti adatban.</span><span class="sxs-lookup"><span data-stu-id="fb931-109">Cmdlets can call [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) as necessary from within their input processing methods.</span></span> <span data-ttu-id="fb931-110">Azonban a parancsmagok segítségével meghívhatja [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) csak a hozzászólásláncot, amelynek a neve, a [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing), [ System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord), vagy [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) bemeneti metódusához feldolgozásra.</span><span class="sxs-lookup"><span data-stu-id="fb931-110">However, cmdlets can call [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) only from the thread that called the [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing), [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord), or [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) input processing method.</span></span> <span data-ttu-id="fb931-111">Ne hívja [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) egy másik szálból.</span><span class="sxs-lookup"><span data-stu-id="fb931-111">Do not call [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) from another thread.</span></span> <span data-ttu-id="fb931-112">Ehelyett kommunikálnak a főszálban vissza a hibákat.</span><span class="sxs-lookup"><span data-stu-id="fb931-112">Instead, communicate errors back to the main thread.</span></span>

## <a name="see-also"></a><span data-ttu-id="fb931-113">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="fb931-113">See Also</span></span>

[<span data-ttu-id="fb931-114">System.Management.Automation.Cmdlet.WriteError</span><span class="sxs-lookup"><span data-stu-id="fb931-114">System.Management.Automation.Cmdlet.WriteError</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.WriteError)

[<span data-ttu-id="fb931-115">System.Management.Automation.Cmdlet.BeginProcessing</span><span class="sxs-lookup"><span data-stu-id="fb931-115">System.Management.Automation.Cmdlet.BeginProcessing</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing)

[<span data-ttu-id="fb931-116">System.Management.Automation.Cmdlet.ProcessRecord</span><span class="sxs-lookup"><span data-stu-id="fb931-116">System.Management.Automation.Cmdlet.ProcessRecord</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord)

[<span data-ttu-id="fb931-117">System.Management.Automation.Cmdlet.EndProcessing</span><span class="sxs-lookup"><span data-stu-id="fb931-117">System.Management.Automation.Cmdlet.EndProcessing</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing)

[<span data-ttu-id="fb931-118">Windows PowerShell Hibarekordjainak</span><span class="sxs-lookup"><span data-stu-id="fb931-118">Windows PowerShell Error Records</span></span>](./windows-powershell-error-records.md)

[<span data-ttu-id="fb931-119">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="fb931-119">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
