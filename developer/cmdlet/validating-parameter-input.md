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
ms.openlocfilehash: f7e5d4fb2f89bd6bc7036fdcff8f38e017d5d0e4
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848803"
---
# <a name="validating-parameter-input"></a><span data-ttu-id="97e37-102">Paraméterbevitel érvényesítése</span><span class="sxs-lookup"><span data-stu-id="97e37-102">Validating Parameter Input</span></span>

<span data-ttu-id="97e37-103">Windows PowerShell parancsmag-paraméterek többféleképpen számára továbbított argumentumok ellenőrizheti.</span><span class="sxs-lookup"><span data-stu-id="97e37-103">Windows PowerShell can validate the arguments passed to cmdlet parameters in several ways.</span></span> <span data-ttu-id="97e37-104">Windows PowerShell ellenőrizheti a hossza, a tartomány és a minta az argumentum a karaktereket.</span><span class="sxs-lookup"><span data-stu-id="97e37-104">Windows PowerShell can validate the length, the range, and the pattern of the characters of the argument.</span></span> <span data-ttu-id="97e37-105">Ellenőrizheti, hogy a rendelkezésre álló argumentumok (count) száma.</span><span class="sxs-lookup"><span data-stu-id="97e37-105">It can validate the number of arguments available (the count).</span></span> <span data-ttu-id="97e37-106">Ezek a szabályok érvényesítése érvényesítési attribútumokat, amelyek deklarált a nyilvános tulajdonságok parancsmag osztály paraméter attribútummal határozza meg.</span><span class="sxs-lookup"><span data-stu-id="97e37-106">These validation rules are defined by validation attributes that are declared with the Parameter attribute on public properties of the cmdlet class.</span></span>

<span data-ttu-id="97e37-107">A paraméterargumentum ellenőrzése, a Windows PowerShell-modul a parancsmag futtatása előtt, győződjön meg arról, hogy a paraméter értékét, az érvényesítési attribútumok által biztosított információkat használja.</span><span class="sxs-lookup"><span data-stu-id="97e37-107">To validate a parameter argument, the Windows PowerShell runtime uses the information provided by the validation attributes to confirm the value of the parameter before the cmdlet is run.</span></span> <span data-ttu-id="97e37-108">Ha a paraméter bemeneti nem érvényes, akkor a felhasználó hibaüzenetet kap.</span><span class="sxs-lookup"><span data-stu-id="97e37-108">If the parameter input is not valid, the user receives an error message.</span></span> <span data-ttu-id="97e37-109">Minden egyes érvényesítési paraméter határozza meg, hogy egy érvényesítési szabály, amely kikényszeríti a Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97e37-109">Each validation parameter defines a validation rule that is enforced by Windows PowerShell.</span></span>

<span data-ttu-id="97e37-110">Windows PowerShell kikényszeríti az ellenőrzési szabályok alapján a következő attribútumokkal.</span><span class="sxs-lookup"><span data-stu-id="97e37-110">Windows PowerShell enforces the validation rules based on the following attributes.</span></span>

<span data-ttu-id="97e37-111">ValidateCount paraméter elfogadó argumentumok minimális és maximális számát adja meg.</span><span class="sxs-lookup"><span data-stu-id="97e37-111">ValidateCount Specifies the minimum and maximum number of arguments that a parameter can accept.</span></span> <span data-ttu-id="97e37-112">Ennek az attribútumnak kódcsomagjaihoz a szintaxissal kapcsolatos további információkért lásd: [ValidateCount típusattribútum-deklaráció](./validatecount-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="97e37-112">For more information about the syntax used to declare this attribute, see [ValidateCount Attribute Declaration](./validatecount-attribute-declaration.md).</span></span>

<span data-ttu-id="97e37-113">ValidateLength a paraméterargumentum karakterek minimális és maximális száma határozza meg.</span><span class="sxs-lookup"><span data-stu-id="97e37-113">ValidateLength Specifies the minimum and maximum number of characters in the parameter argument.</span></span> <span data-ttu-id="97e37-114">Ennek az attribútumnak kódcsomagjaihoz a szintaxissal kapcsolatos további információkért lásd: [ValidateLength típusattribútum-deklaráció](./validatelength-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="97e37-114">For more information about the syntax used to declare this attribute, see [ValidateLength Attribute Declaration](./validatelength-attribute-declaration.md).</span></span>

<span data-ttu-id="97e37-115">ValidatePattern adja meg, amely ellenőrzi a paraméterargumentum reguláris kifejezést.</span><span class="sxs-lookup"><span data-stu-id="97e37-115">ValidatePattern Specifies a regular expression that validates the parameter argument.</span></span> <span data-ttu-id="97e37-116">Ennek az attribútumnak kódcsomagjaihoz a szintaxissal kapcsolatos további információkért lásd: [ValidatePattern típusattribútum-deklaráció](./validatepattern-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="97e37-116">For more information about the syntax used to declare this attribute, see [ValidatePattern Attribute Declaration](./validatepattern-attribute-declaration.md).</span></span>

<span data-ttu-id="97e37-117">ValidateRange megadja a paraméterargumentum minimális és maximális értékét.</span><span class="sxs-lookup"><span data-stu-id="97e37-117">ValidateRange Specifies the minimum and maximum values of the parameter argument.</span></span> <span data-ttu-id="97e37-118">Ennek az attribútumnak kódcsomagjaihoz a szintaxissal kapcsolatos további információkért lásd: [ValidateRange típusattribútum-deklaráció](./validaterange-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="97e37-118">For more information about the syntax used to declare this attribute, see [ValidateRange Attribute Declaration](./validaterange-attribute-declaration.md).</span></span>

<span data-ttu-id="97e37-119">ValidateSet adja meg az érvényes értékek a paraméter argumentum.</span><span class="sxs-lookup"><span data-stu-id="97e37-119">ValidateSet Specifies the valid values for the parameter argument.</span></span> <span data-ttu-id="97e37-120">Ennek az attribútumnak kódcsomagjaihoz a szintaxissal kapcsolatos további információkért lásd: [ValidateSet típusattribútum-deklaráció](./validateset-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="97e37-120">For more information about the syntax used to declare this attribute, see [ValidateSet Attribute Declaration](./validateset-attribute-declaration.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="97e37-121">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="97e37-121">See Also</span></span>

[<span data-ttu-id="97e37-122">A paraméter bemeneti ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="97e37-122">How to Validate Parameter Input</span></span>](./how-to-validate-parameter-input.md)

[<span data-ttu-id="97e37-123">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="97e37-123">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
