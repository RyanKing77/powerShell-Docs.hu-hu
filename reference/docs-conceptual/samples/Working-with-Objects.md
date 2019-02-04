---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Objektumok használata
ms.assetid: 7ecc94a4-015c-4459-ae58-85289ea09030
ms.openlocfilehash: 5d86e1658286055f8a7dc57d488a6adcef577a10
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684737"
---
# <a name="working-with-objects"></a><span data-ttu-id="d7f92-103">Objektumok használata</span><span class="sxs-lookup"><span data-stu-id="d7f92-103">Working with Objects</span></span>

<span data-ttu-id="d7f92-104">Azt tárgyalja, hogyan Windows PowerShell használja az objektumok a parancsmagok közötti adatátvitelhez, és mutatja be néhány módszer objektumok kapcsolatos részletes információk megtekintéséhez használja a Get-Member és formátum parancsmagok objektumok adott tulajdonságainak megtekintése.</span><span class="sxs-lookup"><span data-stu-id="d7f92-104">We have discussed how Windows PowerShell uses objects to transfer data between cmdlets, and demonstrated a few ways to view detailed information about objects by using Get-Member and Format cmdlets to view particular properties of objects.</span></span>

<span data-ttu-id="d7f92-105">A teljesítmény-objektumok, hogy azok a nagy mennyiségű adat összetett hozzáférést biztosítson, és azt már visszamenőleges korrelációban állnak.</span><span class="sxs-lookup"><span data-stu-id="d7f92-105">The power of objects is that they provide you with access to a lot of complex data, and it is already correlated.</span></span> <span data-ttu-id="d7f92-106">Néhány egyszerű technikák is további módosíthatja ezt a munkát még több objektumokat.</span><span class="sxs-lookup"><span data-stu-id="d7f92-106">With some simple techniques you can further manipulate objects to do even more work.</span></span> <span data-ttu-id="d7f92-107">Tekintse meg néhány adott típusú objektumokat, és hogy hogyan kezelheti azokat ebben a fejezetben fogjuk.</span><span class="sxs-lookup"><span data-stu-id="d7f92-107">We are going to look at some specific types of objects and ways you can manipulate them in this chapter.</span></span>