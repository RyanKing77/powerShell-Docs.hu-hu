---
title: Windows PowerShell-parancsmag fogalmak |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7b3ef3f4-c626-4679-884f-406a37412b3e
caps.latest.revision: 16
ms.openlocfilehash: 2f84c57da7429462c69b2a020d9f8ac04f8d0f35
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846661"
---
# <a name="windows-powershell-cmdlet-concepts"></a><span data-ttu-id="3d510-102">Windows PowerShell-parancsmagok – Fogalmak</span><span class="sxs-lookup"><span data-stu-id="3d510-102">Windows PowerShell Cmdlet Concepts</span></span>

<span data-ttu-id="3d510-103">Ez a szakasz ismerteti, hogyan működnek a parancsmagokat.</span><span class="sxs-lookup"><span data-stu-id="3d510-103">This section describes how cmdlets work.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="3d510-104">A szakasz tartalma</span><span class="sxs-lookup"><span data-stu-id="3d510-104">In This Section</span></span>

<span data-ttu-id="3d510-105">Ez a szakasz a következő témakörökből áll.</span><span class="sxs-lookup"><span data-stu-id="3d510-105">This section includes the following topics.</span></span>

<span data-ttu-id="3d510-106">[A parancsmag fejlesztési irányelvek](./cmdlet-development-guidelines.md) megfelelően formázott parancsmagok létrehozásához használható fejlesztési hasznos útmutatást ad a ebben a témakörben.</span><span class="sxs-lookup"><span data-stu-id="3d510-106">[Cmdlet Development Guidelines](./cmdlet-development-guidelines.md) This topic provides development guidelines that can be used to produce well-formed cmdlets.</span></span>

<span data-ttu-id="3d510-107">[A parancsmag osztálydeklaráció](./cmdlet-class-declaration.md) Ez a témakör ismerteti a parancsmag osztálydeklaráció.</span><span class="sxs-lookup"><span data-stu-id="3d510-107">[Cmdlet Class Declaration](./cmdlet-class-declaration.md) This topic describes cmdlet class declaration.</span></span>

<span data-ttu-id="3d510-108">[Jóváhagyott igék a Windows PowerShell-parancsok](./approved-verbs-for-windows-powershell-commands.md) Ez a témakör felsorolja az előre megadott parancsmag-utasítások egy parancsmag osztály deklarálásakor használható.</span><span class="sxs-lookup"><span data-stu-id="3d510-108">[Approved Verbs for Windows PowerShell Commands](./approved-verbs-for-windows-powershell-commands.md) This topic lists the predefined cmdlet verbs that you can use when you declare a cmdlet class.</span></span>

<span data-ttu-id="3d510-109">[A parancsmag bemeneti feldolgozása módszerek](./cmdlet-input-processing-methods.md) Ez a témakör ismerteti a módszereket, amelyek lehetővé teszik a parancsmag előfeldolgozási műveletek végrehajtására, bemeneti feldolgozási műveleteket, és feldolgozási műveletei közzététele.</span><span class="sxs-lookup"><span data-stu-id="3d510-109">[Cmdlet Input Processing Methods](./cmdlet-input-processing-methods.md) This topic describes the methods that allow a cmdlet to perform preprocessing operations, input processing operations, and post processing operations.</span></span>

<span data-ttu-id="3d510-110">[Parancsmag-paraméterek](./cmdlet-parameters.md) Ez a szakasz ismerteti a különböző típusú paramétereket,-parancsmagok is hozzáadhat.</span><span class="sxs-lookup"><span data-stu-id="3d510-110">[Cmdlet Parameters](./cmdlet-parameters.md) This section describes the different types of parameters that you can add to cmdlets.</span></span>

<span data-ttu-id="3d510-111">[A parancsmag attribútumok](./cmdlet-attributes.md) ebben a szakaszban a .NET-osztályok deklarálja a parancsmagok, mint deklarálnia parancsmag-paraméterek mezőket és paraméterek bemeneti ellenőrzési szabályok deklarálásához használt attribútumait ismerteti.</span><span class="sxs-lookup"><span data-stu-id="3d510-111">[Cmdlet Attributes](./cmdlet-attributes.md) This section describes the attributes that are used to declare .NET Framework classes as cmdlets, to declare fields as cmdlet parameters, and to declare input validation rules for parameters.</span></span>

<span data-ttu-id="3d510-112">[A parancsmag aliasok](./cmdlet-aliases.md) Ez a témakör ismerteti a parancsmag aliasok.</span><span class="sxs-lookup"><span data-stu-id="3d510-112">[Cmdlet Aliases](./cmdlet-aliases.md) This topic describes cmdlet aliases.</span></span>

<span data-ttu-id="3d510-113">[A parancsmag kimenete](./cmdlet-output.md) Ez a szakasz ismerteti a kimeneti parancsmagok adhatnak vissza, és határozza meg, és a parancsmagok által visszaadott objektumok megjelenítése típusát.</span><span class="sxs-lookup"><span data-stu-id="3d510-113">[Cmdlet Output](./cmdlet-output.md) This section describes the type of output that cmdlets can return and how to define and display the objects that are returned by cmdlets.</span></span>

<span data-ttu-id="3d510-114">[Regisztrálás parancsmagok](./modules-and-snap-ins.md) Ez a szakasz ismerteti, hogyan lehet regisztrálni a parancsmagok modul és beépülő modulok használatával.</span><span class="sxs-lookup"><span data-stu-id="3d510-114">[Registering Cmdlets](./modules-and-snap-ins.md) This section describes how to register cmdlets by using modules and snap-ins.</span></span>

<span data-ttu-id="3d510-115">[Megerősítést kér](./requesting-confirmation-from-cmdlets.md) Ez a szakasz ismerteti, hogyan parancsmagok kérhet megerősítő a felhasználó előtt a rendszer akkor lehet módosítani.</span><span class="sxs-lookup"><span data-stu-id="3d510-115">[Requesting Confirmation](./requesting-confirmation-from-cmdlets.md) This section describes how cmdlets request confirmation from a user before they make a change to the system.</span></span>

<span data-ttu-id="3d510-116">[Windows PowerShell hibajelentés](./error-reporting-concepts.md) Ez a szakasz ismerteti, hogyan parancsmagok jelentést megszakítást hibák és okozó, és értelmezése hibarekordjainak ismerteti.</span><span class="sxs-lookup"><span data-stu-id="3d510-116">[Windows PowerShell Error Reporting](./error-reporting-concepts.md) This section describes how cmdlets report terminating errors and non-terminating errors, and it describes how to interpret error records.</span></span>

<span data-ttu-id="3d510-117">[Háttérben futó feladatok](./background-jobs.md) Ez a témakör azt ismerteti, hogyan hajthat végre parancsmagok a háttérben futó feladatok, amelyek nem zavarják a parancsok, amely végrehajtja az aktuális munkamenetben lévő munkahelyi.</span><span class="sxs-lookup"><span data-stu-id="3d510-117">[Background Jobs](./background-jobs.md) This topic describes how cmdlets can perform their work within background jobs that do not interfere with the commands that are executing in the current session.</span></span>

<span data-ttu-id="3d510-118">[Parancsmagok és parancsfájlok belül egy parancsmag meghívása](./invoking-cmdlets-and-scripts-within-a-cmdlet.md) Ez a témakör ismerteti, hogyan parancsmagok hívhat meg más parancsmagok és parancsfájlok belül a feldolgozási módszerek beavatkozást.</span><span class="sxs-lookup"><span data-stu-id="3d510-118">[Invoking Cmdlets and Scripts Within a Cmdlet](./invoking-cmdlets-and-scripts-within-a-cmdlet.md) This topic describes how cmdlets can invoke other cmdlets and scripts from within their input processing methods.</span></span>

<span data-ttu-id="3d510-119">[A parancsmag beállítja](./cmdlet-sets.md) Ez a témakör ismerteti az alaposztályok parancsmagok csoportok létrehozására használ.</span><span class="sxs-lookup"><span data-stu-id="3d510-119">[Cmdlet Sets](./cmdlet-sets.md) This topic describes using base classes to create sets of cmdlets.</span></span>

<span data-ttu-id="3d510-120">[Windows PowerShell munkamenet-állapot](./windows-powershell-session-state.md) Ez a témakör ismerteti a Windows PowerShell-munkamenet-állapot.</span><span class="sxs-lookup"><span data-stu-id="3d510-120">[Windows PowerShell Session State](./windows-powershell-session-state.md) This topic describes Windows PowerShell session state.</span></span>
