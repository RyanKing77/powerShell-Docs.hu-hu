---
title: Dátum és idő paraméterek |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 71da921b-7c32-4155-b2f8-b19f30ec774d
caps.latest.revision: 7
ms.openlocfilehash: 49f6c667b0fd9678586559af39a33f982de0a68c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846710"
---
# <a name="date-and-time-parameters"></a><span data-ttu-id="7a8b8-102">Dátum- és időparaméterek</span><span class="sxs-lookup"><span data-stu-id="7a8b8-102">Date and Time Parameters</span></span>

<span data-ttu-id="7a8b8-103">A következő táblázat felsorolja a javasolt nevek és funkciók a paramétereket, dátum és idő adatok kezelésére.</span><span class="sxs-lookup"><span data-stu-id="7a8b8-103">The following table lists recommended names and functionality for parameters that handle date and time information.</span></span> <span data-ttu-id="7a8b8-104">Dátum és idő paraméterek jellemzően rögzíti, ha a hiba jön létre vagy érhető el.</span><span class="sxs-lookup"><span data-stu-id="7a8b8-104">Date and time parameters are typically used to record when something is created or accessed.</span></span>

<span data-ttu-id="7a8b8-105">Írja be az elért adatok: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="7a8b8-105">Accessed Data type: SwitchParameter</span></span>

<span data-ttu-id="7a8b8-106">Végrehajtja ezt a paramétert, hogy mikor van megadva a parancsmag végre lesznek hajtva elért erőforrások alapján a megadott dátum és idő alapján a `Before` és `After` paramétereket.</span><span class="sxs-lookup"><span data-stu-id="7a8b8-106">Implement this parameter so that when it is specified the cmdlet will operate on the resources that have been accessed based on the date and time specified by the `Before` and `After` parameters.</span></span>

<span data-ttu-id="7a8b8-107">Ha ez a paraméter van megadva, a `Created` és `Modified` kell lennie a paraméterek nem adható meg.</span><span class="sxs-lookup"><span data-stu-id="7a8b8-107">If this parameter is specified, the `Created` and `Modified` parameters must be not be specified.</span></span>

<span data-ttu-id="7a8b8-108">Adattípus: után DateTime</span><span class="sxs-lookup"><span data-stu-id="7a8b8-108">After Data type: DateTime</span></span>

<span data-ttu-id="7a8b8-109">Ezzel a paraméterrel adja meg a dátum és idő, amely után a parancsmag értek megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="7a8b8-109">Implement this parameter to specify the date and time after which the cmdlet was used.</span></span> <span data-ttu-id="7a8b8-110">Az a `After` paraméter működjön, a parancsmag is rendelkeznie kell egy `Accessed`, `Created`, vagy `Modified` paraméter.</span><span class="sxs-lookup"><span data-stu-id="7a8b8-110">For the `After` parameter to work, the cmdlet must also have an `Accessed`, `Created`, or `Modified` parameter.</span></span> <span data-ttu-id="7a8b8-111">És meg kell arra a paraméterre `true` amikor a parancsmag beszerzését kezdeményezték.</span><span class="sxs-lookup"><span data-stu-id="7a8b8-111">And, that parameter must be set to `true` when the cmdlet is called.</span></span>

<span data-ttu-id="7a8b8-112">Mielőtt adattípus: DateTime</span><span class="sxs-lookup"><span data-stu-id="7a8b8-112">Before Data type: DateTime</span></span>

<span data-ttu-id="7a8b8-113">Ezzel a paraméterrel adja meg a dátum és idő, ameddig a parancsmag értek megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="7a8b8-113">Implement this parameter to specify the date and time before which the cmdlet was used.</span></span> <span data-ttu-id="7a8b8-114">Az a `Before` paraméter működjön, a parancsmag is rendelkeznie kell egy `Accessed`, `Created`, vagy `Modified` paraméter.</span><span class="sxs-lookup"><span data-stu-id="7a8b8-114">For the `Before` parameter to work, the cmdlet must also have an `Accessed`, `Created`, or `Modified` parameter.</span></span> <span data-ttu-id="7a8b8-115">És meg kell arra a paraméterre `true` amikor a parancsmag beszerzését kezdeményezték.</span><span class="sxs-lookup"><span data-stu-id="7a8b8-115">And, that parameter must be set to `true` when the cmdlet is called.</span></span>

<span data-ttu-id="7a8b8-116">Hozza létre a típusú adatokat: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="7a8b8-116">Created Data type: SwitchParameter</span></span>

<span data-ttu-id="7a8b8-117">Végrehajtja ezt a paramétert, hogy mikor van megadva a parancsmag végre lesznek hajtva a létrehozott erőforrások alapján a megadott dátum és idő alapján a `Before` és `After` paramétereket.</span><span class="sxs-lookup"><span data-stu-id="7a8b8-117">Implement this parameter so that when it is specified the cmdlet will operate on the resources that have been created based on the date and time specified by the `Before` and `After` parameters.</span></span>

<span data-ttu-id="7a8b8-118">Ha ez a paraméter van megadva, a `Accessed` és `Modified` paraméter megadása nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="7a8b8-118">If this parameter is specified, the `Accessed` and `Modified` parameters must not be specified.</span></span>

<span data-ttu-id="7a8b8-119">Pontos adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="7a8b8-119">Exact Data type: SwitchParameter</span></span>

<span data-ttu-id="7a8b8-120">Ez a paraméter valósítja meg, hogy mikor van megadva az erőforrás kifejezés pontosan meg kell egyeznie az erőforrás neve.</span><span class="sxs-lookup"><span data-stu-id="7a8b8-120">Implement this parameter so that when it is specified the resource term must match the resource name exactly.</span></span> <span data-ttu-id="7a8b8-121">Ha a paraméter nincs megadva az erőforrás kifejezés és neve nem pontosan egyeznie kell.</span><span class="sxs-lookup"><span data-stu-id="7a8b8-121">When the parameter is not specified the resource term and name do not need to match exactly.</span></span>

<span data-ttu-id="7a8b8-122">Írja be a módosított adatokat: DateTime</span><span class="sxs-lookup"><span data-stu-id="7a8b8-122">Modified Data type: DateTime</span></span>

<span data-ttu-id="7a8b8-123">Megvalósítani ezt a paramétert, hogy mikor van megadva a parancsmag végre lesznek hajtva megváltozott erőforrásokat alapján a megadott dátum és idő alapján a `Before` és `After` paramétereket.</span><span class="sxs-lookup"><span data-stu-id="7a8b8-123">Implement this parameter so that when it is specified the cmdlet will operate on resources that have been changed based on the date and time specified by the `Before` and `After` parameters.</span></span>

<span data-ttu-id="7a8b8-124">Ha ez a paraméter van megadva, a `Accessed` és `Created` paraméter megadása nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="7a8b8-124">If this parameter is specified, the `Accessed` and `Created` parameters must not be specified.</span></span>

## <a name="see-also"></a><span data-ttu-id="7a8b8-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="7a8b8-125">See Also</span></span>

[<span data-ttu-id="7a8b8-126">Parancsmag-paraméterek</span><span class="sxs-lookup"><span data-stu-id="7a8b8-126">Cmdlet Parameters</span></span>](./cmdlet-parameters.md)

[<span data-ttu-id="7a8b8-127">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="7a8b8-127">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)

[<span data-ttu-id="7a8b8-128">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="7a8b8-128">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
