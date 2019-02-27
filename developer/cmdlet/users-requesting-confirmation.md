---
title: Felhasználói jóváhagyás kérése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6f337498-c534-40ed-968a-09d4d9ca3849
caps.latest.revision: 8
ms.openlocfilehash: e4abbb14b31406b845d9b6af6b6372338fb0d926
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846976"
---
# <a name="users-requesting-confirmation"></a><span data-ttu-id="2d316-102">Megerősítést kérő felhasználók</span><span class="sxs-lookup"><span data-stu-id="2d316-102">Users Requesting Confirmation</span></span>

<span data-ttu-id="2d316-103">Érték megadása `true` számára a `SupportsShouldProcess` paramétert, a parancsmag attribútum nyilatkozat, a felhasználók megadhatják a `Confirm` paraméter a parancssorban.</span><span class="sxs-lookup"><span data-stu-id="2d316-103">When you specify a value of `true` for the `SupportsShouldProcess` parameter of the Cmdlet attribute declaration, users can specify the `Confirm` parameter at the command prompt.</span></span>

<span data-ttu-id="2d316-104">Az alapértelmezett környezetben a felhasználók megadhatják a `Confirm` paraméter vagy `"-Confirm:$true` megerősítési kérés érkezett, hogy amikor a [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) módszert hívja meg.</span><span class="sxs-lookup"><span data-stu-id="2d316-104">In the default environment, users can specify the `Confirm` parameter or `"-Confirm:$true` so that confirmation is requested when the [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) method is called.</span></span> <span data-ttu-id="2d316-105">Ez nincs hatással lévő [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) eseménymegerősítési kéréseknek, akár nagy hatású műveletek esetében.</span><span class="sxs-lookup"><span data-stu-id="2d316-105">This bypasses [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) confirmation requests, even for high-impact operations.</span></span>

<span data-ttu-id="2d316-106">Ha `Confirm` nincs megadva, a [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) hívás megerősítését kéri, ha a `$ConfirmPreference` preferenciaváltozó egyenlő vagy nagyobb, mint a `ConfirmImpact` beállításaként a a parancsmag vagy szolgáltató.</span><span class="sxs-lookup"><span data-stu-id="2d316-106">If `Confirm` is not specified, the [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) call requests confirmation if the `$ConfirmPreference` preference variable is equal to or greater than the `ConfirmImpact` setting of the cmdlet or provider.</span></span> <span data-ttu-id="2d316-107">A beállítás alapértelmezett értékét `$ConfirmPreference` magas.</span><span class="sxs-lookup"><span data-stu-id="2d316-107">The default setting of `$ConfirmPreference` is High.</span></span> <span data-ttu-id="2d316-108">Ezért az alapértelmezett környezet csak a parancsmagok és szolgáltatók, amely nagy hatású művelet megadása kér megerősítést.</span><span class="sxs-lookup"><span data-stu-id="2d316-108">Therefore, in the default environment, only cmdlets and providers that specify a high-impact action request confirmation.</span></span>

<span data-ttu-id="2d316-109">Ha `Confirm` false (hamis), vagy ha `"-Confirm:$false` meg van adva, a [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) hívás megerősítését kéri a felhasználótól, és a `$ConfirmPreference` felületváltozóban a rendszer figyelmen kívül hagyja.</span><span class="sxs-lookup"><span data-stu-id="2d316-109">If `Confirm` is false or if `"-Confirm:$false` is specified, the [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) call requests confirmation from the user, and the `$ConfirmPreference` shell variable is ignored.</span></span>

## <a name="remarks"></a><span data-ttu-id="2d316-110">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="2d316-110">Remarks</span></span>

- <span data-ttu-id="2d316-111">A parancsmagok és szolgáltatók által megadott `SupportsShouldProcess`, azonban nem `ConfirmImpact`, műveletek kezelése "közepes hatású" műveleteket, és nem alapértelmezés szerint fogja kérni.</span><span class="sxs-lookup"><span data-stu-id="2d316-111">For cmdlets and providers that specify `SupportsShouldProcess`, but not `ConfirmImpact`, those actions are handled as "medium impact" actions, and they will not prompt by default.</span></span> <span data-ttu-id="2d316-112">A hatás szintje nem éri el az alapértelmezett beállítás, a `$ConfirmPreference` preferenciaváltozót.</span><span class="sxs-lookup"><span data-stu-id="2d316-112">Their impact level is less than the default setting of the `$ConfirmPreference` preference variable.</span></span>

- <span data-ttu-id="2d316-113">Ha a felhasználó adja meg a `Verbose` paramétert, akkor értesítjük a művelet akkor is, ha azok nem megerősítést kér.</span><span class="sxs-lookup"><span data-stu-id="2d316-113">If the user specifies the `Verbose` parameter, they will be notified of the operation even if they are not prompted for confirmation.</span></span>

## <a name="see-also"></a><span data-ttu-id="2d316-114">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2d316-114">See Also</span></span>

[<span data-ttu-id="2d316-115">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="2d316-115">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
