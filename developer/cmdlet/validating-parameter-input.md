---
title: A paraméter bemeneti ellenőrzése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- parameters, validation rules
- validation, examples
- validation
ms.assetid: 3f15bf20-a068-4a7d-a170-bc43f755d1fe
caps.latest.revision: 14
ms.openlocfilehash: 171e3e974619e197a0bcc9dfc759297005e34568
ms.sourcegitcommit: 69abc5ad16e5dd29ddfb1853e266a4bfd1d59d59
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/05/2019
ms.locfileid: "57429839"
---
# <a name="validating-parameter-input"></a><span data-ttu-id="79cd1-102">Paraméterbevitel érvényesítése</span><span class="sxs-lookup"><span data-stu-id="79cd1-102">Validating Parameter Input</span></span>

<span data-ttu-id="79cd1-103">PowerShell parancsmag-paraméterek többféleképpen számára továbbított argumentumok ellenőrizheti.</span><span class="sxs-lookup"><span data-stu-id="79cd1-103">PowerShell can validate the arguments passed to cmdlet parameters in several ways.</span></span>
<span data-ttu-id="79cd1-104">PowerShell ellenőrizheti a hossza, a tartomány és a minta az argumentum a karaktereket.</span><span class="sxs-lookup"><span data-stu-id="79cd1-104">PowerShell can validate the length, the range, and the pattern of the characters of the argument.</span></span>
<span data-ttu-id="79cd1-105">Ellenőrizheti, hogy a rendelkezésre álló argumentumok (count) száma.</span><span class="sxs-lookup"><span data-stu-id="79cd1-105">It can validate the number of arguments available (the count).</span></span>
<span data-ttu-id="79cd1-106">Ezek a szabályok érvényesítése érvényesítési attribútumokat, amelyek deklarált a nyilvános tulajdonságok parancsmag osztály paraméter attribútummal határozza meg.</span><span class="sxs-lookup"><span data-stu-id="79cd1-106">These validation rules are defined by validation attributes that are declared with the Parameter attribute on public properties of the cmdlet class.</span></span>

<span data-ttu-id="79cd1-107">A paraméterargumentum ellenőrzéséhez a PowerShell-modul a parancsmag futtatása előtt, győződjön meg arról, hogy a paraméter értékét, az érvényesítési attribútumok által biztosított információkat használja.</span><span class="sxs-lookup"><span data-stu-id="79cd1-107">To validate a parameter argument, the PowerShell runtime uses the information provided by the validation attributes to confirm the value of the parameter before the cmdlet is run.</span></span>
<span data-ttu-id="79cd1-108">Ha a paraméter bemeneti nem érvényes, akkor a felhasználó hibaüzenetet kap.</span><span class="sxs-lookup"><span data-stu-id="79cd1-108">If the parameter input is not valid, the user receives an error message.</span></span>
<span data-ttu-id="79cd1-109">Minden egyes érvényesítési paraméter határozza meg, hogy egy érvényesítési szabály, amely kikényszeríti a PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79cd1-109">Each validation parameter defines a validation rule that is enforced by PowerShell.</span></span>

<span data-ttu-id="79cd1-110">PowerShell az ellenőrzési szabályok alapján a következő attribútumok érvénybe lépteti.</span><span class="sxs-lookup"><span data-stu-id="79cd1-110">PowerShell enforces the validation rules based on the following attributes.</span></span>

### <a name="validatecount"></a><span data-ttu-id="79cd1-111">ValidateCount</span><span class="sxs-lookup"><span data-stu-id="79cd1-111">ValidateCount</span></span>

<span data-ttu-id="79cd1-112">Adja meg a minimális és maximális számú argumentumot, amely egy paraméter tud fogadni.</span><span class="sxs-lookup"><span data-stu-id="79cd1-112">Specifies the minimum and maximum number of arguments that a parameter can accept.</span></span>
<span data-ttu-id="79cd1-113">További információkért lásd: [ValidateCount típusattribútum-deklaráció](./validatecount-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="79cd1-113">For more information, see [ValidateCount Attribute Declaration](./validatecount-attribute-declaration.md).</span></span>

### <a name="validatelength"></a><span data-ttu-id="79cd1-114">ValidateLength</span><span class="sxs-lookup"><span data-stu-id="79cd1-114">ValidateLength</span></span>

<span data-ttu-id="79cd1-115">A paraméterargumentum adja meg a minimális és maximális karakterszámot.</span><span class="sxs-lookup"><span data-stu-id="79cd1-115">Specifies the minimum and maximum number of characters in the parameter argument.</span></span>
<span data-ttu-id="79cd1-116">További információkért lásd: [ValidateLength típusattribútum-deklaráció](./validatelength-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="79cd1-116">For more information, see [ValidateLength Attribute Declaration](./validatelength-attribute-declaration.md).</span></span>

### <a name="validatepattern"></a><span data-ttu-id="79cd1-117">ValidatePattern</span><span class="sxs-lookup"><span data-stu-id="79cd1-117">ValidatePattern</span></span>

<span data-ttu-id="79cd1-118">Itt adhatja meg, amely ellenőrzi a paraméterargumentum reguláris kifejezést.</span><span class="sxs-lookup"><span data-stu-id="79cd1-118">Specifies a regular expression that validates the parameter argument.</span></span>
<span data-ttu-id="79cd1-119">További információkért lásd: [ValidatePattern típusattribútum-deklaráció](./validatepattern-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="79cd1-119">For more information, see [ValidatePattern Attribute Declaration](./validatepattern-attribute-declaration.md).</span></span>

### <a name="validaterange"></a><span data-ttu-id="79cd1-120">ValidateRange</span><span class="sxs-lookup"><span data-stu-id="79cd1-120">ValidateRange</span></span>

<span data-ttu-id="79cd1-121">Adja meg a paraméterargumentum minimális és maximális értékét.</span><span class="sxs-lookup"><span data-stu-id="79cd1-121">Specifies the minimum and maximum values of the parameter argument.</span></span>
<span data-ttu-id="79cd1-122">További információkért lásd: [ValidateRange típusattribútum-deklaráció](./validaterange-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="79cd1-122">For more information, see [ValidateRange Attribute Declaration](./validaterange-attribute-declaration.md).</span></span>

### <a name="validateset"></a><span data-ttu-id="79cd1-123">ValidateSet</span><span class="sxs-lookup"><span data-stu-id="79cd1-123">ValidateSet</span></span>

<span data-ttu-id="79cd1-124">Adja meg az érvényes értékek a paraméter argumentum.</span><span class="sxs-lookup"><span data-stu-id="79cd1-124">Specifies the valid values for the parameter argument.</span></span>
<span data-ttu-id="79cd1-125">További információkért lásd: [ValidateSet típusattribútum-deklaráció](./validateset-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="79cd1-125">For more information, see [ValidateSet Attribute Declaration](./validateset-attribute-declaration.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="79cd1-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="79cd1-126">See Also</span></span>

[<span data-ttu-id="79cd1-127">A paraméter bemeneti ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="79cd1-127">How to Validate Parameter Input</span></span>](./how-to-validate-parameter-input.md)

[<span data-ttu-id="79cd1-128">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="79cd1-128">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
