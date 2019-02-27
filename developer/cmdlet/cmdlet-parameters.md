---
title: Parancsmag-paraméterek |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- optional parameters [PowerShell SDK]
- aliases [PowerShell SDK]
- parameter sets [PowerShell SDK]
- parameters [PowerShell SDK]
- mandatory parameters [PowerShell SDK]
- positional parameters [PowerShell SDK]
- cmdlets [PowerShell SDK], parameters
ms.assetid: 3f1cca5f-5b95-4bce-94a6-a22db1aefd47
caps.latest.revision: 23
ms.openlocfilehash: 914a10907bcf980eed8d7e2f819c382fe6b341ad
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845303"
---
# <a name="cmdlet-parameters"></a><span data-ttu-id="76a5d-102">Parancsmag-paraméterek</span><span class="sxs-lookup"><span data-stu-id="76a5d-102">Cmdlet Parameters</span></span>

<span data-ttu-id="76a5d-103">Parancsmag-paraméterek adja meg a mechanizmus, amely lehetővé teszi a parancsmag bemeneti fogadására.</span><span class="sxs-lookup"><span data-stu-id="76a5d-103">Cmdlet parameters provide the mechanism that allows a cmdlet to accept input.</span></span> <span data-ttu-id="76a5d-104">Paramétereket is fogad bevitelt a közvetlenül a parancssorból, vagy az objektumot a parancsmagnak átadni a folyamatban, az argumentumok (más néven *értékek*), ezeket a paramétereket adhatja meg a bemeneti, amely elfogadja a parancsmagot, a a parancsmag végre kell hajtania a műveletek és az adatok, amelyek a parancsmag visszaadja a folyamat számára.</span><span class="sxs-lookup"><span data-stu-id="76a5d-104">Parameters can accept input directly from the command line, or from objects passed to the cmdlet through the pipeline, The arguments (also known as *values*) of these parameters can specify the input that the cmdlet accepts, how the cmdlet should perform its actions, and the data that the cmdlet returns to the pipeline.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="76a5d-105">A szakasz tartalma</span><span class="sxs-lookup"><span data-stu-id="76a5d-105">In This Section</span></span>

<span data-ttu-id="76a5d-106">[Tulajdonságok paraméterekként deklaráló](./declaring-properties-as-parameters.md) látnia kell, mielőtt azt deklarálja, hogy a parancsmag paramétereit alapvető információkat biztosít.</span><span class="sxs-lookup"><span data-stu-id="76a5d-106">[Declaring Properties as Parameters](./declaring-properties-as-parameters.md) Provides basic information you must understand before you declare the parameters of a cmdlet.</span></span>

<span data-ttu-id="76a5d-107">[Parancsmag-paraméterek típusú](./types-of-cmdlet-parameters.md) ismerteti a különböző típusú paramétereket, a parancsmagok eszközhöz adhat.</span><span class="sxs-lookup"><span data-stu-id="76a5d-107">[Types of Cmdlet Parameters](./types-of-cmdlet-parameters.md) Describes the different types of parameters that you can declare in cmdlets.</span></span>

<span data-ttu-id="76a5d-108">[Parancsmag paraméter nevének és a funkciók irányelvek](./standard-cmdlet-parameter-names-and-types.md) diszkosz a nevek, adattípus és funkciók a standard szintű paraméterek ajánlott.</span><span class="sxs-lookup"><span data-stu-id="76a5d-108">[Cmdlet Parameter Name and Functionality Guidelines](./standard-cmdlet-parameter-names-and-types.md) Discuses the names, recommended data type, and functionality of standard parameters.</span></span>

<span data-ttu-id="76a5d-109">[A paraméter-aliasok](./parameter-aliases.md) aliasról, amelyek a paraméterek számára definiálható ismerteti.</span><span class="sxs-lookup"><span data-stu-id="76a5d-109">[Parameter Aliases](./parameter-aliases.md) Discusses the aliases that you can define for parameters.</span></span>

<span data-ttu-id="76a5d-110">[Közös paraméterneveket](./common-parameter-names.md) Ez a témakör ismerteti, amely a Windows PowerShell-parancsmagok hozzáadása a paramétereket.</span><span class="sxs-lookup"><span data-stu-id="76a5d-110">[Common Parameter Names](./common-parameter-names.md) This topic describes the parameters that Windows PowerShell adds to cmdlets.</span></span>

<span data-ttu-id="76a5d-111">[A parancsmag paraméterkészletek](./cmdlet-parameter-sets.md) ismerteti, hogyan paraméter csoportok lehetővé teszik, hogy egyetlen parancsmag, amely a különböző helyzetekhez különböző műveleteket hajthat végre írási.</span><span class="sxs-lookup"><span data-stu-id="76a5d-111">[Cmdlet Parameter Sets](./cmdlet-parameter-sets.md) Discusses how parameter sets enable you to write a single cmdlet that can perform different actions for different scenarios.</span></span>

<span data-ttu-id="76a5d-112">[A dinamikus parancsmag-paraméterek](./cmdlet-dynamic-parameters.md) különleges körülmények között a felhasználó számára elérhető paramétereket ismerteti.</span><span class="sxs-lookup"><span data-stu-id="76a5d-112">[Cmdlet Dynamic Parameters](./cmdlet-dynamic-parameters.md) Discusses parameters that are available to the user under special conditions.</span></span>

<span data-ttu-id="76a5d-113">[A helyettesítő karakterek támogató parancsmag-paraméterek](./supporting-wildcard-characters-in-cmdlet-parameters.md) ismerteti, hogyan lehet támogatást nyújt a helyettesítő karakterek egy parancsmag, amely akkor erőforrások csoportjához tervezésekor.</span><span class="sxs-lookup"><span data-stu-id="76a5d-113">[Supporting Wildcard Characters in Cmdlet Parameters](./supporting-wildcard-characters-in-cmdlet-parameters.md) Describes how to provide support for wildcard characters when you design a cmdlet that will be run against a group of resources.</span></span>

<span data-ttu-id="76a5d-114">[A paraméter bemeneti ellenőrzése](./validating-parameter-input.md) ismerteti, hogyan a Windows PowerShell parancsmag-paraméterek számára továbbított argumentumok ellenőrzi.</span><span class="sxs-lookup"><span data-stu-id="76a5d-114">[Validating Parameter Input](./validating-parameter-input.md) Describes how Windows PowerShell validates the arguments passed to cmdlet parameters.</span></span>

<span data-ttu-id="76a5d-115">[Adjon meg szűrési paraméterekhez](./input-filter-parameters.md) foglalkozik a `Filter`, `Include`, és `Exclude` szűrése, amely befolyásolja a parancsmag bemeneti objektumok készlete paramétereket.</span><span class="sxs-lookup"><span data-stu-id="76a5d-115">[Input Filter Parameters](./input-filter-parameters.md) Discusses the `Filter`, `Include`, and `Exclude` parameters that filter the set of input objects that the cmdlet affects.</span></span>

## <a name="related-sections"></a><span data-ttu-id="76a5d-116">Kapcsolódó témakörök</span><span class="sxs-lookup"><span data-stu-id="76a5d-116">Related Sections</span></span>

[<span data-ttu-id="76a5d-117">A paraméter bemeneti ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="76a5d-117">How to Validate Parameter Input</span></span>](./how-to-validate-parameter-input.md)

## <a name="see-also"></a><span data-ttu-id="76a5d-118">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="76a5d-118">See Also</span></span>

[<span data-ttu-id="76a5d-119">Deklarace parametru attribútum</span><span class="sxs-lookup"><span data-stu-id="76a5d-119">Parameter Attribute Declaration</span></span>](./parameter-attribute-declaration.md)

[<span data-ttu-id="76a5d-120">Windows PowerShell-parancsmagok</span><span class="sxs-lookup"><span data-stu-id="76a5d-120">Windows PowerShell Cmdlets</span></span>](./cmdlet-overview.md)
