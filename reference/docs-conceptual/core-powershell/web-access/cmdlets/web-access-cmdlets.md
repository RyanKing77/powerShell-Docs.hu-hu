---
ms.topic: reference
keywords: PowerShell parancsmag
ms.date: 12/12/2016
title: Webes PowerShell-elérés parancsmagjai
ms.openlocfilehash: 34a7a01f154b2e43416dfe8ea43d4d8e937816d9
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34188020"
---
# <a name="windows-powershell-web-access-cmdlets"></a><span data-ttu-id="ec1b4-103">A Webes Windows PowerShell-elérés parancsmagjai</span><span class="sxs-lookup"><span data-stu-id="ec1b4-103">Windows PowerShell Web Access Cmdlets</span></span>

<span data-ttu-id="ec1b4-104">Ezt a hivatkozást parancsmagot és szintaxist tartalmazza az összes Windows PowerShell® Web Access-specifikus parancsmagjai.</span><span class="sxs-lookup"><span data-stu-id="ec1b4-104">This reference provides cmdlet descriptions and syntax for all Windows PowerShell® Web Access-specific cmdlets.</span></span> <span data-ttu-id="ec1b4-105">Felsorolja a parancsmagok betűrendben a parancsmag elején utasítás alapján.</span><span class="sxs-lookup"><span data-stu-id="ec1b4-105">It lists the cmdlets in alphabetical order based on the verb at the beginning of the cmdlet.</span></span>

## <a name="add-pswaauthorizationruleadd-pswaauthorizationrulemd"></a>[<span data-ttu-id="ec1b4-106">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="ec1b4-106">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)

<span data-ttu-id="ec1b4-107">Új engedélyezési szabály hozzáadása a Windows PowerShell® Web Access engedélyezési szabályok készletéhez.</span><span class="sxs-lookup"><span data-stu-id="ec1b4-107">Adds a new authorization rule to the Windows PowerShell® Web Access authorization rule set.</span></span>

## <a name="get-pswaauthorizationruleget-pswaauthorizationrulemd"></a>[<span data-ttu-id="ec1b4-108">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="ec1b4-108">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)

<span data-ttu-id="ec1b4-109">A Windows PowerShell Web Access-engedélyezési szabályok készletét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="ec1b4-109">Returns a set of the Windows PowerShell Web Access authorization rules.</span></span>

## <a name="install-pswawebapplicationinstall-pswawebapplicationmd"></a>[<span data-ttu-id="ec1b4-110">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="ec1b4-110">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)

<span data-ttu-id="ec1b4-111">A Windows PowerShell Web Access webalkalmazás konfigurálja az IIS-ben.</span><span class="sxs-lookup"><span data-stu-id="ec1b4-111">Configures the Windows PowerShell Web Access web application in IIS.</span></span>

## <a name="remove-pswaauthorizationruleremove-pswaauthorizationrulemd"></a>[<span data-ttu-id="ec1b4-112">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="ec1b4-112">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)

<span data-ttu-id="ec1b4-113">A megadott engedélyezési szabály eltávolítása a Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="ec1b4-113">Removes a specified authorization rule from Windows PowerShell Web Access.</span></span>

## <a name="test-pswaauthorizationruletest-pswaauthorizationrulemd"></a>[<span data-ttu-id="ec1b4-114">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="ec1b4-114">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)

<span data-ttu-id="ec1b4-115">Teszteli engedélyezési szabályokat, hogy ellenőrizze, hogy egy adott felhasználó, számítógép, végpont hozzáférési kérelem engedélyezve van.</span><span class="sxs-lookup"><span data-stu-id="ec1b4-115">Tests authorization rules to validate that a particular user, computer, endpoint access request is authorized.</span></span>

## <a name="uninstall-pswawebapplicationuninstall-pswawebapplicationmd"></a>[<span data-ttu-id="ec1b4-116">Távolítsa el PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="ec1b4-116">Uninstall-PswaWebApplication</span></span>](uninstall-pswawebapplication.md)

<span data-ttu-id="ec1b4-117">Eltávolítja a Windows PowerShell webalkalmazás IIS-ből.</span><span class="sxs-lookup"><span data-stu-id="ec1b4-117">Uninstalls the Windows PowerShell web application from IIS.</span></span>

><span data-ttu-id="ec1b4-118">**Megjegyzés:**:</span><span class="sxs-lookup"><span data-stu-id="ec1b4-118">**Note**:</span></span>
>
><span data-ttu-id="ec1b4-119">A rendelkezésre álló parancsmagok kilistázhatja a:</span><span class="sxs-lookup"><span data-stu-id="ec1b4-119">To list all the cmdlets that are available, use the:</span></span>
>
> <span data-ttu-id="ec1b4-120">`Get-Command –Module PowerShellWebAccess` parancsmag.</span><span class="sxs-lookup"><span data-stu-id="ec1b4-120">`Get-Command –Module PowerShellWebAccess` cmdlet.</span></span>

<span data-ttu-id="ec1b4-121">További információt, vagy szintaxisának, a parancsmagokat használja: `Get-Help ` *&lt;parancsmag neve&gt;* ahol *&lt;parancsmag neve&gt;* az a név a parancsmagot, hogy meg szeretné vizsgálni.</span><span class="sxs-lookup"><span data-stu-id="ec1b4-121">For more information about, or for the syntax of, any of the cmdlets, use: `Get-Help `*&lt;cmdlet name&gt;* where *&lt;cmdlet name&gt;* is the name of the cmdlet that you want to research.</span></span>

<span data-ttu-id="ec1b4-122">Részletesebb információk megismeréséhez ezeket a parancsmagokat futtathatja:</span><span class="sxs-lookup"><span data-stu-id="ec1b4-122">For more detailed information, you can run any of the following cmdlets:</span></span>

- <span data-ttu-id="ec1b4-123">`Get-Help `*&lt;Parancsmag neve&gt;*` -Detailed`</span><span class="sxs-lookup"><span data-stu-id="ec1b4-123">`Get-Help `*&lt;cmdlet name&gt;*` -Detailed`</span></span>
- <span data-ttu-id="ec1b4-124">`Get-Help `*&lt;Parancsmag neve&gt;*` -Examples`</span><span class="sxs-lookup"><span data-stu-id="ec1b4-124">`Get-Help `*&lt;cmdlet name&gt;*` -Examples`</span></span>
- <span data-ttu-id="ec1b4-125">`Get-Help `*&lt;Parancsmag neve&gt;*` -Full`</span><span class="sxs-lookup"><span data-stu-id="ec1b4-125">`Get-Help `*&lt;cmdlet name&gt;*` -Full`</span></span>

### <a name="more-information"></a><span data-ttu-id="ec1b4-126">További információ</span><span class="sxs-lookup"><span data-stu-id="ec1b4-126">More Information</span></span>

<span data-ttu-id="ec1b4-127">PowerShell Web Access kapcsolatos további információkért tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="ec1b4-127">For more information about PowerShell Web Access, see the following:</span></span>

- [<span data-ttu-id="ec1b4-128">Telepítheti és használhatja a Windows PowerShell Web Access</span><span class="sxs-lookup"><span data-stu-id="ec1b4-128">Install and Use Windows PowerShell Web Access</span></span>](../install-and-use-windows-powershell-web-access.md)