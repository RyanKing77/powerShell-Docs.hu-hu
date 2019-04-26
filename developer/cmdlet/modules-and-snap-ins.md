---
title: Modulok és beépülő modulok |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2d342f91-23e0-467f-8de2-f9657d820693
caps.latest.revision: 6
ms.openlocfilehash: 157cd64e286392f3fd770e1e34542682b1e63625
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067620"
---
# <a name="modules-and-snap-ins"></a><span data-ttu-id="09c7f-102">Modulok és beépülő modulok</span><span class="sxs-lookup"><span data-stu-id="09c7f-102">Modules and Snap-ins</span></span>

<span data-ttu-id="09c7f-103">Parancsmagok modulok (bevezetett Windows PowerShell 2.0-s) vagy a beépülő modulok használata a munkamenet lehet hozzáadni. Miután hozzáadta a parancsmag futtatása programozott módon egy fogadó alkalmazás vagy a parancssorból interaktív módon a munkamenet.</span><span class="sxs-lookup"><span data-stu-id="09c7f-103">Cmdlets can be added to a session using modules (introduced by Windows PowerShell 2.0) or snap-ins. Once the cmdlet is added to the session it can be run programmatically by a host application or interactively at the command line.</span></span>

<span data-ttu-id="09c7f-104">Javasoljuk, hogy a modulok parancsmagok hozzáadása a munkamenet a következő okok miatt a kézbesítési módszerként használja:</span><span class="sxs-lookup"><span data-stu-id="09c7f-104">We recommend that you use modules as the delivery method for adding cmdlets to a session for the following reasons:</span></span>

- <span data-ttu-id="09c7f-105">Modulok adhat hozzá parancsmagok által a szerelvény betöltése során, a parancsmag van definiálva.</span><span class="sxs-lookup"><span data-stu-id="09c7f-105">Modules allow you to add cmdlets by loading the assembly where the cmdlet is defined.</span></span> <span data-ttu-id="09c7f-106">Hiba esetén nem kell egy beépülő modul osztály megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="09c7f-106">There is no need to implement a snap-in class.</span></span>

- <span data-ttu-id="09c7f-107">Modulok adhat hozzá más erőforrások, például a változókat, függvények, parancsfájlok, típusok és formázási fájlok és több.</span><span class="sxs-lookup"><span data-stu-id="09c7f-107">Modules allow you to add other resources, such as variables, functions, scripts, types and formatting files, and more.</span></span>

- <span data-ttu-id="09c7f-108">Beépülő modulok segítségével csak parancsmagok és szolgáltatók hozzáadása a munkamenethez.</span><span class="sxs-lookup"><span data-stu-id="09c7f-108">Snap-ins can be used only to add cmdlets and providers to the session.</span></span>

## <a name="see-also"></a><span data-ttu-id="09c7f-109">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="09c7f-109">See Also</span></span>

[<span data-ttu-id="09c7f-110">Windows PowerShell-modul írása</span><span class="sxs-lookup"><span data-stu-id="09c7f-110">Writing a Windows PowerShell Module</span></span>](../module/writing-a-windows-powershell-module.md)

[<span data-ttu-id="09c7f-111">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="09c7f-111">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
