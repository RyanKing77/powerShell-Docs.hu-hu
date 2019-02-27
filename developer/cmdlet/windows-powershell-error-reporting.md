---
title: Windows PowerShell hibajelentési |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 61b7773a-c346-4835-a928-7212dc4c85bc
caps.latest.revision: 7
ms.openlocfilehash: 259de341fd2fcce2b0c4629f806b4348cba1ff2c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846920"
---
# <a name="windows-powershell-error-reporting"></a><span data-ttu-id="ac0c6-102">Windows PowerShell hibajelentés</span><span class="sxs-lookup"><span data-stu-id="ac0c6-102">Windows PowerShell Error Reporting</span></span>

<span data-ttu-id="ac0c6-103">Ez a szakasz témakörei azt ismertetjük, hogyan parancsmagok hibát jeleznek.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-103">The topics in this section discuss how cmdlets report errors.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="ac0c6-104">A szakasz tartalma</span><span class="sxs-lookup"><span data-stu-id="ac0c6-104">In This Section</span></span>

<span data-ttu-id="ac0c6-105">[Hiba Reporting fogalmak](./error-reporting-concepts.md) leírja a két mechanizmus, amellyel parancsmagok hibák jelentése.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-105">[Error Reporting Concepts](./error-reporting-concepts.md) Describes the two mechanisms that cmdlets can use to report errors.</span></span>

<span data-ttu-id="ac0c6-106">[Megszakítást okozó hibák](./terminating-errors.md) jelentést a megszakítást okozó hibák, ahol a metódus nem hívható a belül a parancsmagot, és a kivételeket, amelyek a Windows PowerShell-modul által visszaadott is, ha a metódus lehívásra kerül módját ismerteti.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-106">[Terminating Errors](./terminating-errors.md) Describes the method used to report terminating errors, where that method can be called from within the cmdlet, and exceptions that can be returned by the Windows PowerShell runtime when the method is called.</span></span>

<span data-ttu-id="ac0c6-107">[A nem okozó](./non-terminating-errors.md) jelentést okozó, és ha a metódus nem hívható a belül a parancsmag módját ismerteti.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-107">[Non-Terminating Errors](./non-terminating-errors.md) Describes the method used to report non-terminating errors and where that method can be called from within the cmdlet.</span></span>

<span data-ttu-id="ac0c6-108">[Hiba történt adatainak megjelenítése kategória szerint](./displaying-error-information.md) ismerteti a módon, hogy a felhasználók megjeleníthetik hiba.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-108">[Displaying Error Information by Category](./displaying-error-information.md) Discusses the ways that users can display error.</span></span>

<span data-ttu-id="ac0c6-109">[Windows PowerShell Hibarekordjainak](./windows-powershell-error-records.md) egy hibarekord összetevőit ismerteti.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-109">[Windows PowerShell Error Records](./windows-powershell-error-records.md) Describes the components of an error record.</span></span>

<span data-ttu-id="ac0c6-110">[ErrorRecord objektumok értelmezése](./interpreting-errorrecord-objects.md) ismerteti, hogyan legyenek értelmezve ErrorRecord objektumokat.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-110">[Interpreting ErrorRecord Objects](./interpreting-errorrecord-objects.md) Discusses how ErrorRecord objects are interpreted.</span></span>

## <a name="see-also"></a><span data-ttu-id="ac0c6-111">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ac0c6-111">See Also</span></span>

[<span data-ttu-id="ac0c6-112">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="ac0c6-112">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
