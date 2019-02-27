---
title: Megjegyzés-alapú súgó-témaköröket írása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e619ab16-90ad-46e9-9bde-d6dce492ba56
caps.latest.revision: 4
ms.openlocfilehash: e3d32f36b597088abc41e229bb0955c1b25504e6
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847914"
---
# <a name="writing-comment-based-help-topics"></a><span data-ttu-id="53bd3-102">Megjegyzésalapú súgótémakörök írása</span><span class="sxs-lookup"><span data-stu-id="53bd3-102">Writing Comment-Based Help Topics</span></span>

<span data-ttu-id="53bd3-103">Megjegyzés-alapú súgó-témaköröket függvények és parancsfájlok speciális súgó Megjegyzés kulcsszó használatával írhat.</span><span class="sxs-lookup"><span data-stu-id="53bd3-103">You can write comment-based Help topics for functions and scripts by using special Help comment keywords.</span></span>

 <span data-ttu-id="53bd3-104">A `Get-Help` parancsmag megjeleníti a Megjegyzés-alapú súgó ugyanebben a formátumban, amelyben a parancsmag Súgó-témaköröket, amelyek akkor jönnek létre, az XML-fájlok jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="53bd3-104">The `Get-Help` cmdlet displays comment-based Help in the same format in which it displays the cmdlet Help topics that are generated from XML files.</span></span> <span data-ttu-id="53bd3-105">A felhasználók használhatják az összes paramétereinek `Get-Help`, például a részletes, teljes, például és Online, függvény megjelenítéséhez, és parancsfájl-súgó.</span><span class="sxs-lookup"><span data-stu-id="53bd3-105">Users can use all of the parameters of `Get-Help`, such as Detailed, Full, Example, and Online, to display function and script Help.</span></span>

 <span data-ttu-id="53bd3-106">XML-alapú súgó-témaköröket a parancsfájlokban és függvényekben írni, és használja a Súgó Megjegyzés kulcsszavak felhasználók átirányítása az XML-alapú témakörök vagy egyéb témakörök is.</span><span class="sxs-lookup"><span data-stu-id="53bd3-106">You can also write XML-based Help topics for scripts and functions and use the Help comment keywords to redirect users to the XML-based topics or other topics.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="53bd3-107">A szakasz tartalma</span><span class="sxs-lookup"><span data-stu-id="53bd3-107">In This Section</span></span>

 <span data-ttu-id="53bd3-108">[Megjegyzés-alapú súgó szintaxisát](./syntax-of-comment-based-help.md) Megjegyzés-alapú súgó szintaxisát.</span><span class="sxs-lookup"><span data-stu-id="53bd3-108">[Syntax of Comment-Based Help](./syntax-of-comment-based-help.md) Describes the syntax of comment-based help.</span></span>

 <span data-ttu-id="53bd3-109">[Megjegyzés-alapú súgó kulcsszavak](./comment-based-help-keywords.md) felsorolja a Megjegyzés-alapú súgó kulcsszavakat.</span><span class="sxs-lookup"><span data-stu-id="53bd3-109">[Comment-Based Help Keywords](./comment-based-help-keywords.md) Lists the keywords in comment-based help.</span></span>

 <span data-ttu-id="53bd3-110">[A függvények helyezi el a Megjegyzés-alapú súgó](./placing-comment-based-help-in-functions.md) Megjegyzés-alapú súgó-függvény helyét jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="53bd3-110">[Placing Comment-Based Help in Functions](./placing-comment-based-help-in-functions.md) Shows where to place comment-based help for a function.</span></span>

 <span data-ttu-id="53bd3-111">[Helyezi el a Megjegyzés-alapú súgó parancsfájlok](./placing-comment-based-help-in-scripts.md) Megjegyzés-alapú súgó parancsfájl helyét jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="53bd3-111">[Placing Comment-Based Help in Scripts](./placing-comment-based-help-in-scripts.md) Shows where to place comment-based help for a script.</span></span>