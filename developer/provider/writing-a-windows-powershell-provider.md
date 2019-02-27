---
title: A Windows PowerShell-szolgáltató írása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a54ce657-e0e0-4b3e-b9dc-aed39876f933
caps.latest.revision: 11
ms.openlocfilehash: 58252956184703fdcdb3aa9b1db617c6e91294c1
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849650"
---
# <a name="writing-a-windows-powershell-provider"></a><span data-ttu-id="ba72d-102">Windows PowerShell-szolgáltató írása</span><span class="sxs-lookup"><span data-stu-id="ba72d-102">Writing a Windows PowerShell Provider</span></span>

<span data-ttu-id="ba72d-103">"A Windows PowerShell-szolgáltató írása" van, a program vezetők, akik a Windows PowerShell-szolgáltató tervezése és a fejlesztőknek szól, akik fontolgatja, hogy szolgáltató kód.</span><span class="sxs-lookup"><span data-stu-id="ba72d-103">"Writing a Windows PowerShell Provider" is for program managers who are designing Windows PowerShell providers and for developers who are implementing provider code.</span></span> <span data-ttu-id="ba72d-104">Amelyekkel megtudhatja, hogyan működnek a Windows PowerShell-szolgáltatók, és biztosít, amelyek segítségével indítsa el a kialakítása vagy a saját szolgáltató írása.</span><span class="sxs-lookup"><span data-stu-id="ba72d-104">It will help you understand how Windows PowerShell providers work, and it provides sample code that you can use to start designing or writing your own providers.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="ba72d-105">A szakasz tartalma</span><span class="sxs-lookup"><span data-stu-id="ba72d-105">In This Section</span></span>

<span data-ttu-id="ba72d-106">[Windows PowerShell szolgáltató a rövid útmutató](./windows-powershell-provider-quickstart.md) példakódot és a egy nagyon alapszintű szolgáltató forgatókönyv.</span><span class="sxs-lookup"><span data-stu-id="ba72d-106">[Windows PowerShell Provider QuickStart](./windows-powershell-provider-quickstart.md) Example code and walkthrough of a very basic provider.</span></span>

<span data-ttu-id="ba72d-107">[Windows PowerShell-szolgáltató áttekintése](./windows-powershell-provider-overview.md) ebben a szakaszban található témakörök, amelyek leírják a Windows PowerShell-szolgáltatók és azok működéséről.</span><span class="sxs-lookup"><span data-stu-id="ba72d-107">[Windows PowerShell Provider Overview](./windows-powershell-provider-overview.md) This section contains topics that describe what Windows PowerShell providers are and how they work.</span></span>

<span data-ttu-id="ba72d-108">[Egy elem szolgáltató írása](./writing-an-item-provider.md) példakódot és módszerek beszerzésének és beállításának elemek támogató forgatókönyv.</span><span class="sxs-lookup"><span data-stu-id="ba72d-108">[Writing an item provider](./writing-an-item-provider.md) Example code and walkthrough of methods that support getting and setting items.</span></span>

<span data-ttu-id="ba72d-109">[Egy tároló-szolgáltató írása](./writing-a-container-provider.md) példakódot és forgatókönyv módszereket, amelyek támogatják a tárolókat (egyéb elemek gyermekeként elem).</span><span class="sxs-lookup"><span data-stu-id="ba72d-109">[Writing a container provider](./writing-a-container-provider.md) Example code and walkthrough of methods that support containers (items that have other items as children).</span></span>

<span data-ttu-id="ba72d-110">[A navigációs szolgáltató írása](./writing-a-navigation-provider.md) példakódot és a forgatókönyv, amely támogatja a beágyazott tárolók, a relatív elérési utakat és a egy elérési útról a másikra történő áthelyezésének elemek módszerek.</span><span class="sxs-lookup"><span data-stu-id="ba72d-110">[Writing a navigation provider](./writing-a-navigation-provider.md) Example code and walkthrough of methods that support nested containers, relative paths, and moving items from one path to another.</span></span>

<span data-ttu-id="ba72d-111">[Szolgáltató minták](./provider-samples.md) ebben a szakaszban a szolgáltatók mintáit tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="ba72d-111">[Provider Samples](./provider-samples.md) This section provides samples of providers.</span></span>

## <a name="see-also"></a><span data-ttu-id="ba72d-112">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ba72d-112">See Also</span></span>

[<span data-ttu-id="ba72d-113">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="ba72d-113">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)