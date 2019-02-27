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
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849958"
---
# <a name="modules-and-snap-ins"></a><span data-ttu-id="7f431-102">Modulok és beépülő modulok</span><span class="sxs-lookup"><span data-stu-id="7f431-102">Modules and Snap-ins</span></span>

<span data-ttu-id="7f431-103">Parancsmagok modulok (bevezetett Windows PowerShell 2.0-s) vagy a beépülő modulok használata a munkamenet lehet hozzáadni. Miután hozzáadta a parancsmag futtatása programozott módon egy fogadó alkalmazás vagy a parancssorból interaktív módon a munkamenet.</span><span class="sxs-lookup"><span data-stu-id="7f431-103">Cmdlets can be added to a session using modules (introduced by Windows PowerShell 2.0) or snap-ins. Once the cmdlet is added to the session it can be run programmatically by a host application or interactively at the command line.</span></span>

<span data-ttu-id="7f431-104">Javasoljuk, hogy a modulok parancsmagok hozzáadása a munkamenet a következő okok miatt a kézbesítési módszerként használja:</span><span class="sxs-lookup"><span data-stu-id="7f431-104">We recommend that you use modules as the delivery method for adding cmdlets to a session for the following reasons:</span></span>

- <span data-ttu-id="7f431-105">Modulok adhat hozzá parancsmagok által a szerelvény betöltése során, a parancsmag van definiálva.</span><span class="sxs-lookup"><span data-stu-id="7f431-105">Modules allow you to add cmdlets by loading the assembly where the cmdlet is defined.</span></span> <span data-ttu-id="7f431-106">Hiba esetén nem kell egy beépülő modul osztály megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="7f431-106">There is no need to implement a snap-in class.</span></span>

- <span data-ttu-id="7f431-107">Modulok adhat hozzá más erőforrások, például a változókat, függvények, parancsfájlok, típusok és formázási fájlok és több.</span><span class="sxs-lookup"><span data-stu-id="7f431-107">Modules allow you to add other resources, such as variables, functions, scripts, types and formatting files, and more.</span></span>

- <span data-ttu-id="7f431-108">Beépülő modulok segítségével csak parancsmagok és szolgáltatók hozzáadása a munkamenethez.</span><span class="sxs-lookup"><span data-stu-id="7f431-108">Snap-ins can be used only to add cmdlets and providers to the session.</span></span>

## <a name="see-also"></a><span data-ttu-id="7f431-109">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="7f431-109">See Also</span></span>

[<span data-ttu-id="7f431-110">Windows PowerShell-modul írása</span><span class="sxs-lookup"><span data-stu-id="7f431-110">Writing a Windows PowerShell Module</span></span>](../module/writing-a-windows-powershell-module.md)

[<span data-ttu-id="7f431-111">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="7f431-111">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
