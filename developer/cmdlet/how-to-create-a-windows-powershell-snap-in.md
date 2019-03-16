---
title: Egy Windows PowerShell beépülő modul létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snap-ins [PowerShell SDK], examples
ms.assetid: 71bd9b2c-5f2e-4aa8-b5fe-08c956540d37
caps.latest.revision: 10
ms.openlocfilehash: 43199544dc02ccae4b61053c30d6ed36576adfcf
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58055937"
---
# <a name="how-to-create-a-windows-powershell-snap-in"></a><span data-ttu-id="60329-102">Windows PowerShelles beépülő modul létrehozása</span><span class="sxs-lookup"><span data-stu-id="60329-102">How to Create a Windows PowerShell Snap-in</span></span>

<span data-ttu-id="60329-103">Egy Windows PowerShell beépülő modul lehetővé teszi a parancsmagok és a egy másik Windows PowerShell-szolgáltató regisztrálása a rendszerhéj, így kiterjesztése a rendszerhéj működését.</span><span class="sxs-lookup"><span data-stu-id="60329-103">A Windows PowerShell snap-in provides a mechanism for registering sets of cmdlets and another Windows PowerShell provider with the shell, thus extending the functionality of the shell.</span></span> <span data-ttu-id="60329-104">A Windows PowerShell beépülő modult is regisztrálhat a parancsmagok és szolgáltatók egyetlen szerelvényt, vagy hogy regisztrálni tudjon a parancsmagok és szolgáltatók adott listáját.</span><span class="sxs-lookup"><span data-stu-id="60329-104">A Windows PowerShell snap-in can register all the cmdlets and providers in a single assembly, or it can register a specific list of cmdlets and providers.</span></span>

<span data-ttu-id="60329-105">Beépülő modul szerelvényeket egy védett könyvtárban kell telepíteni, ugyanúgy, mint más operációs rendszerekkel lennének.</span><span class="sxs-lookup"><span data-stu-id="60329-105">Snap-in assemblies should be installed in a protected directory, just as they would be with other operating systems.</span></span> <span data-ttu-id="60329-106">Ellenkező esetben a rosszindulatú felhasználók is cserélje le egy szerelvény nem biztonságos kódra.</span><span class="sxs-lookup"><span data-stu-id="60329-106">Otherwise, malicious users can replace an assembly with unsafe code.</span></span>

## <a name="windows-powershell-snap-in-classes"></a><span data-ttu-id="60329-107">Windows PowerShell beépülő modul osztályai</span><span class="sxs-lookup"><span data-stu-id="60329-107">Windows PowerShell Snap-in Classes</span></span>

<span data-ttu-id="60329-108">Minden Windows PowerShell beépülő modul osztályai célosztályából származik a [System.Management.Automation.PSSnapIn](/dotnet/api/System.Management.Automation.PSSnapIn) vagy [System.Management.Automation.Custompssnapin](/dotnet/api/System.Management.Automation.CustomPSSnapIn) osztályokat.</span><span class="sxs-lookup"><span data-stu-id="60329-108">All Windows PowerShell snap-in classes derive from the [System.Management.Automation.PSSnapIn](/dotnet/api/System.Management.Automation.PSSnapIn) or [System.Management.Automation.Custompssnapin](/dotnet/api/System.Management.Automation.CustomPSSnapIn) classes.</span></span>

## <a name="examples"></a><span data-ttu-id="60329-109">Példák</span><span class="sxs-lookup"><span data-stu-id="60329-109">Examples</span></span>

<span data-ttu-id="60329-110">[Egy Windows PowerShell beépülő modul írása](./writing-a-windows-powershell-snap-in.md): Ez a példa bemutatja, hogyan hozhat létre, amellyel a parancsmagok és szolgáltatók regisztrálása egy szerelvény beépülő.</span><span class="sxs-lookup"><span data-stu-id="60329-110">[Writing a Windows PowerShell Snap-in](./writing-a-windows-powershell-snap-in.md): This example shows how to create a snap-in that is used to register all the cmdlets and providers in an assembly.</span></span>

<span data-ttu-id="60329-111">[Egy egyéni Windows PowerShell beépülő modul írása](./writing-a-custom-windows-powershell-snap-in.md): Ez a példa bemutatja, hogyan hozhat létre egy egyéni beépülő modul, amely egyetlen szerelvényben parancsmagok és szolgáltatók, amely már nem létezik, vagy egy meghatározott készletének regisztrálásához használatos.</span><span class="sxs-lookup"><span data-stu-id="60329-111">[Writing a Custom Windows PowerShell Snap-in](./writing-a-custom-windows-powershell-snap-in.md): This example shows how to create a custom snap-in that is used to register a specific set of cmdlets and providers that might or might not exist in a single assembly.</span></span>

## <a name="see-also"></a><span data-ttu-id="60329-112">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="60329-112">See Also</span></span>

[<span data-ttu-id="60329-113">System.Management.Automation.PSSnapIn</span><span class="sxs-lookup"><span data-stu-id="60329-113">System.Management.Automation.PSSnapIn</span></span>](/dotnet/api/System.Management.Automation.PSSnapIn)

[<span data-ttu-id="60329-114">System.Management.Automation.Custompssnapin</span><span class="sxs-lookup"><span data-stu-id="60329-114">System.Management.Automation.Custompssnapin</span></span>](/dotnet/api/System.Management.Automation.CustomPSSnapIn)

[<span data-ttu-id="60329-115">Parancsmagok regisztrálása</span><span class="sxs-lookup"><span data-stu-id="60329-115">Registering Cmdlets</span></span>](./registering-cmdlets.md)

[<span data-ttu-id="60329-116">Windows PowerShell Shell SDK</span><span class="sxs-lookup"><span data-stu-id="60329-116">Windows PowerShell Shell SDK</span></span>](../windows-powershell-reference.md)
