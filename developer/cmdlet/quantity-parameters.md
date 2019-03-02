---
title: Mennyiség paraméterek |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8c0bd8a9-1749-4885-ab24-38c0a4d9f2cb
caps.latest.revision: 6
ms.openlocfilehash: 7a3efc60fcc8729d833f6de070016cfd08cc9b88
ms.sourcegitcommit: ce46e5098786e19d521b4bf948ff62d2b90bc53e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/02/2019
ms.locfileid: "57251370"
---
# <a name="quantity-parameters"></a><span data-ttu-id="ae61a-102">Mennyiségparaméterek</span><span class="sxs-lookup"><span data-stu-id="ae61a-102">Quantity Parameters</span></span>

<span data-ttu-id="ae61a-103">Az alábbi táblázat a javasolt nevei és -funkcióinak mennyiség paraméterek.</span><span class="sxs-lookup"><span data-stu-id="ae61a-103">The following table lists the recommended names and functionality for quantity parameters.</span></span>

|<span data-ttu-id="ae61a-104">Paraméter</span><span class="sxs-lookup"><span data-stu-id="ae61a-104">Parameter</span></span>|<span data-ttu-id="ae61a-105">Funkció</span><span class="sxs-lookup"><span data-stu-id="ae61a-105">Functionality</span></span>|
|---|---|
|<span data-ttu-id="ae61a-106">**Összes**</span><span class="sxs-lookup"><span data-stu-id="ae61a-106">**All**</span></span><br><span data-ttu-id="ae61a-107">Adattípus: Boolean</span><span class="sxs-lookup"><span data-stu-id="ae61a-107">Data type: Boolean</span></span>|<span data-ttu-id="ae61a-108">Végrehajtja ezt a paramétert, hogy `true` azt jelzi, hogy az összes erőforrás kell intézkedni helyett az erőforrások egy alapértelmezett részhalmazát.</span><span class="sxs-lookup"><span data-stu-id="ae61a-108">Implement this parameter so that `true` indicates that all resources should be acted upon instead of a default subset of resources.</span></span> <span data-ttu-id="ae61a-109">Végrehajtja ezt a paramétert, hogy `false` azt jelzi, hogy az erőforrások egy részét.</span><span class="sxs-lookup"><span data-stu-id="ae61a-109">Implement this parameter so that `false` indicates a subset of the resources.</span></span>|
|<span data-ttu-id="ae61a-110">**Felosztás**</span><span class="sxs-lookup"><span data-stu-id="ae61a-110">**Allocation**</span></span><br><span data-ttu-id="ae61a-111">Adattípus: Int32</span><span class="sxs-lookup"><span data-stu-id="ae61a-111">Data type: Int32</span></span>|<span data-ttu-id="ae61a-112">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a felosztandó elemek száma.</span><span class="sxs-lookup"><span data-stu-id="ae61a-112">Implement this parameter so that the user can specify the number of items to allocate.</span></span>|
|<span data-ttu-id="ae61a-113">**BlockCount**</span><span class="sxs-lookup"><span data-stu-id="ae61a-113">**BlockCount**</span></span><br><span data-ttu-id="ae61a-114">Adattípus: Int64</span><span class="sxs-lookup"><span data-stu-id="ae61a-114">Data type: Int64</span></span>|<span data-ttu-id="ae61a-115">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a blokkok száma.</span><span class="sxs-lookup"><span data-stu-id="ae61a-115">Implement this parameter so that the user can specify the block count.</span></span>|
|<span data-ttu-id="ae61a-116">**Száma**</span><span class="sxs-lookup"><span data-stu-id="ae61a-116">**Count**</span></span><br><span data-ttu-id="ae61a-117">Adattípus: Int64</span><span class="sxs-lookup"><span data-stu-id="ae61a-117">Data type: Int64</span></span>|<span data-ttu-id="ae61a-118">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a száma.</span><span class="sxs-lookup"><span data-stu-id="ae61a-118">Implement this parameter so that the user can specify the count.</span></span>|
|<span data-ttu-id="ae61a-119">**Hatókör**</span><span class="sxs-lookup"><span data-stu-id="ae61a-119">**Scope**</span></span><br><span data-ttu-id="ae61a-120">Adattípus: Kulcsszó</span><span class="sxs-lookup"><span data-stu-id="ae61a-120">Data type: Keyword</span></span>|<span data-ttu-id="ae61a-121">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a hatókört a művelethez.</span><span class="sxs-lookup"><span data-stu-id="ae61a-121">Implement this parameter so that the user can specify the scope to operate on.</span></span>|

## <a name="see-also"></a><span data-ttu-id="ae61a-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ae61a-122">See Also</span></span>

[<span data-ttu-id="ae61a-123">Parancsmag-paraméterek</span><span class="sxs-lookup"><span data-stu-id="ae61a-123">Cmdlet Parameters</span></span>](./cmdlet-parameters.md)

[<span data-ttu-id="ae61a-124">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="ae61a-124">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)

[<span data-ttu-id="ae61a-125">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="ae61a-125">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
