---
title: Windows PowerShell fogalmak |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3dd5608e-50b6-4c6a-aee3-dde0e86032bc
caps.latest.revision: 7
ms.openlocfilehash: c4b13518ad6452a39ca49e897e1d3e353818d332
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62081036"
---
# <a name="windows-powershell-concepts"></a><span data-ttu-id="c8dfc-102">Windows PowerShell – Fogalmak</span><span class="sxs-lookup"><span data-stu-id="c8dfc-102">Windows PowerShell Concepts</span></span>

<span data-ttu-id="c8dfc-103">Ez a szakasz tartalmazza a elméleti információk segítségével megismerheti a Windows PowerShell a fejlesztők szempontjából.</span><span class="sxs-lookup"><span data-stu-id="c8dfc-103">This section contains conceptual information that will help you understand Windows PowerShell from the viewpoint of a developer.</span></span>

|<span data-ttu-id="c8dfc-104">Témakör neve</span><span class="sxs-lookup"><span data-stu-id="c8dfc-104">Topic Name</span></span>|<span data-ttu-id="c8dfc-105">Leírás</span><span class="sxs-lookup"><span data-stu-id="c8dfc-105">Description</span></span>|
|----------------|-----------------|
|[<span data-ttu-id="c8dfc-106">Windows PowerShell-szolgáltatók</span><span class="sxs-lookup"><span data-stu-id="c8dfc-106">Windows PowerShell Providers</span></span>](http://msdn.microsoft.com/en-us/a65c5c75-1131-4ade-90d3-a613dbe620e9)|<span data-ttu-id="c8dfc-107">Adatok elérésére használt Windows PowerShell-szolgáltatók szóló vita tárolja.</span><span class="sxs-lookup"><span data-stu-id="c8dfc-107">A discussion about Windows PowerShell providers that are used to access data stores.</span></span>|
|[<span data-ttu-id="c8dfc-108">Windows PowerShell beépülő modulok</span><span class="sxs-lookup"><span data-stu-id="c8dfc-108">Windows PowerShell Snap-ins</span></span>](http://msdn.microsoft.com/en-us/20e081a9-522c-48bf-9f21-faaf8cca2e82)|<span data-ttu-id="c8dfc-109">A parancsmagok és szolgáltatók regisztrálása mechanizmust.</span><span class="sxs-lookup"><span data-stu-id="c8dfc-109">A mechanism for registering cmdlets and providers.</span></span> <span data-ttu-id="c8dfc-110">(Lásd még a [Windows PowerShell-modul írása](../module/writing-a-windows-powershell-module.md).)</span><span class="sxs-lookup"><span data-stu-id="c8dfc-110">(See also, [Writing a Windows PowerShell Module](../module/writing-a-windows-powershell-module.md).)</span></span>|
|[<span data-ttu-id="c8dfc-111">Windows PowerShell-modul</span><span class="sxs-lookup"><span data-stu-id="c8dfc-111">Windows PowerShell Runtime</span></span>](http://msdn.microsoft.com/en-us/949f06e8-0224-4cd3-bbad-a0cebbb5dec8)|<span data-ttu-id="c8dfc-112">A Windows PowerShell futási térben jelenlegi példányát.</span><span class="sxs-lookup"><span data-stu-id="c8dfc-112">The current instance of the Windows PowerShell runspace.</span></span>|
|[<span data-ttu-id="c8dfc-113">Windows PowerShell futási terek</span><span class="sxs-lookup"><span data-stu-id="c8dfc-113">Windows PowerShell Runspaces</span></span>](http://msdn.microsoft.com/en-us/a1582cfe-f06d-4aff-adc6-71f49a860ce9)|<span data-ttu-id="c8dfc-114">A működési környezetek, ahol parancsok feldolgozása.</span><span class="sxs-lookup"><span data-stu-id="c8dfc-114">The operating environments where commands are processed.</span></span>|
|[<span data-ttu-id="c8dfc-115">Windows PowerShell-névterek</span><span class="sxs-lookup"><span data-stu-id="c8dfc-115">Windows PowerShell Namespaces</span></span>](http://msdn.microsoft.com/en-us/04bd2841-e90c-47d2-8a1f-3aeb3df35176)|<span data-ttu-id="c8dfc-116">Windows PowerShell API-névtérre áttekintése.</span><span class="sxs-lookup"><span data-stu-id="c8dfc-116">Overview of Windows PowerShell API namespaces.</span></span>|
|[<span data-ttu-id="c8dfc-117">Windows PowerShell súgója</span><span class="sxs-lookup"><span data-stu-id="c8dfc-117">Windows PowerShell Help</span></span>](http://msdn.microsoft.com/en-us/097b7c1c-a056-4b36-9c86-65b2ee702fc7)|<span data-ttu-id="c8dfc-118">Vita írása parancsmag súgójában.</span><span class="sxs-lookup"><span data-stu-id="c8dfc-118">A discussion about writing cmdlet Help.</span></span>|
|[<span data-ttu-id="c8dfc-119">Jóváhagyás kérése</span><span class="sxs-lookup"><span data-stu-id="c8dfc-119">Requesting Confirmation</span></span>](../cmdlet/requesting-confirmation-from-cmdlets.md)|<span data-ttu-id="c8dfc-120">Hogyan parancsmagok és szolgáltatók visszajelzés kérése a művelet előtt a felhasználónak szóló vita használatban van.</span><span class="sxs-lookup"><span data-stu-id="c8dfc-120">A discussion about how cmdlets and providers request feedback from the user before an action is taken.</span></span>|
|[<span data-ttu-id="c8dfc-121">Windows PowerShell-objektummá fogalmak</span><span class="sxs-lookup"><span data-stu-id="c8dfc-121">Windows PowerShell Object Concepts</span></span>](http://msdn.microsoft.com/en-us/a1449178-b6fd-4ca8-a5e1-d747c2c54181)|<span data-ttu-id="c8dfc-122">Windows PowerShell hogyan kezeli az objektumokat.</span><span class="sxs-lookup"><span data-stu-id="c8dfc-122">How Windows PowerShell handles objects.</span></span>|
|[<span data-ttu-id="c8dfc-123">Kiterjesztett típus System (ETS) Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8dfc-123">Windows PowerShell Extended Type System (ETS)</span></span>](http://msdn.microsoft.com/en-us/12700631-be23-4e6b-9bf0-81ea0d166353)|<span data-ttu-id="c8dfc-124">Programozott módon kiterjesztése objektumokat.</span><span class="sxs-lookup"><span data-stu-id="c8dfc-124">Programmatically extending objects.</span></span>|

## <a name="see-also"></a><span data-ttu-id="c8dfc-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c8dfc-125">See Also</span></span>

[<span data-ttu-id="c8dfc-126">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="c8dfc-126">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)