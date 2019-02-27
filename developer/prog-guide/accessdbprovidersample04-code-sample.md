---
title: Kódminta AccessDbProviderSample04 |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f9374c4a-e499-4516-9eb6-107c59df98d9
caps.latest.revision: 7
ms.openlocfilehash: 43f01b9cd6af3ab6c26f88ee0c1e9269499b2bc3
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845135"
---
# <a name="accessdbprovidersample04-code-sample"></a><span data-ttu-id="947cd-102">AccessDbProviderSample04 – kódminta</span><span class="sxs-lookup"><span data-stu-id="947cd-102">AccessDbProviderSample04 Code Sample</span></span>

<span data-ttu-id="947cd-103">A következő kód bemutatja a Windows PowerShell-szolgáltatóban ismertetett végrehajtásának [létrehozása a Windows PowerShell-tároló szolgáltató](./creating-a-windows-powershell-container-provider.md).</span><span class="sxs-lookup"><span data-stu-id="947cd-103">The following code shows the implementation of the Windows PowerShell provider described in [Creating a Windows PowerShell Container Provider](./creating-a-windows-powershell-container-provider.md).</span></span> <span data-ttu-id="947cd-104">Ez a szolgáltató a többrétegű adattárak működik.</span><span class="sxs-lookup"><span data-stu-id="947cd-104">This provider works on multi-layer data stores.</span></span> <span data-ttu-id="947cd-105">Az ilyen típusú adattárat a legfelső szintre a tároló a legfelső szintű elemeket tartalmaz, és minden további szint gyermekelemek csomópont neve.</span><span class="sxs-lookup"><span data-stu-id="947cd-105">For this type of data store, the top level of the store contains the root items and each subsequent level is referred to as a node of child items.</span></span> <span data-ttu-id="947cd-106">Azáltal, hogy a felhasználót, hogy ezek gyermekcsomópontokat működjön, a felhasználók beavatkozhatnak hierarchikusan keresztül az adattárban.</span><span class="sxs-lookup"><span data-stu-id="947cd-106">By allowing the user to work on these child nodes, a user can interact hierarchically through the data store.</span></span>

## <a name="code-sample"></a><span data-ttu-id="947cd-107">Kódminta</span><span class="sxs-lookup"><span data-stu-id="947cd-107">Code Sample</span></span>

[!code-csharp[AccessDBProviderSample04.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample04/AccessDBProviderSample04.cs#L11-L1635 "AccessDBProviderSample04.cs")]

## <a name="see-also"></a><span data-ttu-id="947cd-108">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="947cd-108">See Also</span></span>

[<span data-ttu-id="947cd-109">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="947cd-109">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)