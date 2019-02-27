---
title: ValidateLength típusattribútum-deklaráció |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ValidateLength attribute, described
- attributes, ValidateLength
- ValidateLength attribute
ms.assetid: 82fe3a35-a94b-4bc1-ad9e-dfc5f1e788b3
caps.latest.revision: 13
ms.openlocfilehash: 1e8364c78abba5272007019550ffcb2cedaf9fd0
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848817"
---
# <a name="validatelength-attribute-declaration"></a><span data-ttu-id="87a09-102">ValidateLength attribútumdeklarációja</span><span class="sxs-lookup"><span data-stu-id="87a09-102">ValidateLength Attribute Declaration</span></span>

<span data-ttu-id="87a09-103">A ValidateLength attribútum határozza meg, hogy egy parancsmag-paraméterrel argumentumként karakterek minimális és maximális száma.</span><span class="sxs-lookup"><span data-stu-id="87a09-103">The ValidateLength attribute specifies the minimum and maximum number of characters for a cmdlet parameter argument.</span></span> <span data-ttu-id="87a09-104">Ez az attribútum is használható Windows PowerShell-függvényekkel.</span><span class="sxs-lookup"><span data-stu-id="87a09-104">This attribute can also be used by Windows PowerShell functions.</span></span>

## <a name="syntax"></a><span data-ttu-id="87a09-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="87a09-105">Syntax</span></span>

```csharp
[ValidateLength(int minLength, int maxlength)]
```

#### <a name="parameters"></a><span data-ttu-id="87a09-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="87a09-106">Parameters</span></span>

<span data-ttu-id="87a09-107">`MinLength` ([System.Integer](/dotnet/api/System.Integer)) szükséges.</span><span class="sxs-lookup"><span data-stu-id="87a09-107">`MinLength` ([System.Integer](/dotnet/api/System.Integer)) Required.</span></span> <span data-ttu-id="87a09-108">Meghatározza az engedélyezett karakterek minimális számát.</span><span class="sxs-lookup"><span data-stu-id="87a09-108">Specifies the minimum number of characters allowed.</span></span>

<span data-ttu-id="87a09-109">`MaxLength` ([System.Integer](/dotnet/api/System.Integer)) szükséges.</span><span class="sxs-lookup"><span data-stu-id="87a09-109">`MaxLength` ([System.Integer](/dotnet/api/System.Integer)) Required.</span></span> <span data-ttu-id="87a09-110">Meghatározza az engedélyezett maximális karakterszámot.</span><span class="sxs-lookup"><span data-stu-id="87a09-110">Specifies the maximum number of characters allowed.</span></span>

## <a name="remarks"></a><span data-ttu-id="87a09-111">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="87a09-111">Remarks</span></span>

- <span data-ttu-id="87a09-112">Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [bemenet-ellenőrzési szabályok deklarálja hogyan](http://msdn.microsoft.com/en-us/544c2100-62ba-4be4-b2a2-cc0d4e4fc45b).</span><span class="sxs-lookup"><span data-stu-id="87a09-112">For more information about how to declare this attribute, see [How to Declare Input Validation Rules](http://msdn.microsoft.com/en-us/544c2100-62ba-4be4-b2a2-cc0d4e4fc45b).</span></span>
- <span data-ttu-id="87a09-113">Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [bemenet-ellenőrzési szabályok deklarálja hogyan](http://msdn.microsoft.com/en-us/544c2100-62ba-4be4-b2a2-cc0d4e4fc45b).</span><span class="sxs-lookup"><span data-stu-id="87a09-113">For more information about how to declare this attribute, see [How to Declare Input Validation Rules](http://msdn.microsoft.com/en-us/544c2100-62ba-4be4-b2a2-cc0d4e4fc45b).</span></span>

- <span data-ttu-id="87a09-114">Ez az attribútum nem használata esetén a megfelelő paraméterargumentum lehet hossza.</span><span class="sxs-lookup"><span data-stu-id="87a09-114">When this attribute is not used, the corresponding parameter argument can be of any length.</span></span>

- <span data-ttu-id="87a09-115">A Windows PowerShell-modul a következő feltételek hibát jelez:</span><span class="sxs-lookup"><span data-stu-id="87a09-115">The Windows PowerShell runtime throws an error under the following conditions:</span></span>

    - <span data-ttu-id="87a09-116">Amikor értékét a `MaxLength` attribútum paraméter értéke kisebb, mint az értékét a `MinLength` paraméter attribútum.</span><span class="sxs-lookup"><span data-stu-id="87a09-116">When the value of the `MaxLength` attribute parameter is less than the value of the `MinLength` attribute parameter.</span></span>

    - <span data-ttu-id="87a09-117">Ha a `MaxLength` attribútum paraméter 0 értékre van állítva.</span><span class="sxs-lookup"><span data-stu-id="87a09-117">When the `MaxLength` attribute parameter is set to 0.</span></span>

    - <span data-ttu-id="87a09-118">Ha az argumentuma nem karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="87a09-118">When the argument is not a string.</span></span>

- <span data-ttu-id="87a09-119">A ValidateLength attribútum határozza meg a [System.Management.Automation.Validatelengthattribute](/dotnet/api/System.Management.Automation.ValidateLengthAttribute) osztály.</span><span class="sxs-lookup"><span data-stu-id="87a09-119">The ValidateLength attribute is defined by the [System.Management.Automation.Validatelengthattribute](/dotnet/api/System.Management.Automation.ValidateLengthAttribute) class.</span></span>

## <a name="see-also"></a><span data-ttu-id="87a09-120">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="87a09-120">See Also</span></span>

[<span data-ttu-id="87a09-121">System.Management.Automation.Validatelengthattribute</span><span class="sxs-lookup"><span data-stu-id="87a09-121">System.Management.Automation.Validatelengthattribute</span></span>](/dotnet/api/System.Management.Automation.ValidateLengthAttribute)

[<span data-ttu-id="87a09-122">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="87a09-122">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
