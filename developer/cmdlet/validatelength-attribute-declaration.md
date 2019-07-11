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
ms.openlocfilehash: a25fa2410fcc6803563573596af1bc99052c3ffa
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67735110"
---
# <a name="validatelength-attribute-declaration"></a><span data-ttu-id="d63c9-102">ValidateLength attribútumdeklarációja</span><span class="sxs-lookup"><span data-stu-id="d63c9-102">ValidateLength Attribute Declaration</span></span>

<span data-ttu-id="d63c9-103">A ValidateLength attribútum határozza meg, hogy egy parancsmag-paraméterrel argumentumként karakterek minimális és maximális száma.</span><span class="sxs-lookup"><span data-stu-id="d63c9-103">The ValidateLength attribute specifies the minimum and maximum number of characters for a cmdlet parameter argument.</span></span> <span data-ttu-id="d63c9-104">Ez az attribútum is használható Windows PowerShell-függvényekkel.</span><span class="sxs-lookup"><span data-stu-id="d63c9-104">This attribute can also be used by Windows PowerShell functions.</span></span>

## <a name="syntax"></a><span data-ttu-id="d63c9-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="d63c9-105">Syntax</span></span>

```csharp
[ValidateLength(int minLength, int maxlength)]
```

#### <a name="parameters"></a><span data-ttu-id="d63c9-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="d63c9-106">Parameters</span></span>

<span data-ttu-id="d63c9-107">`MinLength` ([System.Int32](/dotnet/api/System.Int32)) szükséges.</span><span class="sxs-lookup"><span data-stu-id="d63c9-107">`MinLength` ([System.Int32](/dotnet/api/System.Int32)) Required.</span></span> <span data-ttu-id="d63c9-108">Meghatározza az engedélyezett karakterek minimális számát.</span><span class="sxs-lookup"><span data-stu-id="d63c9-108">Specifies the minimum number of characters allowed.</span></span>

<span data-ttu-id="d63c9-109">`MaxLength` ([System.Int32](/dotnet/api/System.Int32)) szükséges.</span><span class="sxs-lookup"><span data-stu-id="d63c9-109">`MaxLength` ([System.Int32](/dotnet/api/System.Int32)) Required.</span></span> <span data-ttu-id="d63c9-110">Meghatározza az engedélyezett maximális karakterszámot.</span><span class="sxs-lookup"><span data-stu-id="d63c9-110">Specifies the maximum number of characters allowed.</span></span>

## <a name="remarks"></a><span data-ttu-id="d63c9-111">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="d63c9-111">Remarks</span></span>

- <span data-ttu-id="d63c9-112">Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [bemenet-ellenőrzési szabályok deklarálja hogyan](./how-to-validate-parameter-input.md).</span><span class="sxs-lookup"><span data-stu-id="d63c9-112">For more information about how to declare this attribute, see [How to Declare Input Validation Rules](./how-to-validate-parameter-input.md).</span></span>

- <span data-ttu-id="d63c9-113">Ez az attribútum nem használata esetén a megfelelő paraméterargumentum lehet hossza.</span><span class="sxs-lookup"><span data-stu-id="d63c9-113">When this attribute is not used, the corresponding parameter argument can be of any length.</span></span>

- <span data-ttu-id="d63c9-114">A Windows PowerShell-modul a következő feltételek hibát jelez:</span><span class="sxs-lookup"><span data-stu-id="d63c9-114">The Windows PowerShell runtime throws an error under the following conditions:</span></span>

    - <span data-ttu-id="d63c9-115">Amikor értékét a `MaxLength` attribútum paraméter értéke kisebb, mint az értékét a `MinLength` paraméter attribútum.</span><span class="sxs-lookup"><span data-stu-id="d63c9-115">When the value of the `MaxLength` attribute parameter is less than the value of the `MinLength` attribute parameter.</span></span>

    - <span data-ttu-id="d63c9-116">Ha a `MaxLength` attribútum paraméter 0 értékre van állítva.</span><span class="sxs-lookup"><span data-stu-id="d63c9-116">When the `MaxLength` attribute parameter is set to 0.</span></span>

    - <span data-ttu-id="d63c9-117">Ha az argumentuma nem karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="d63c9-117">When the argument is not a string.</span></span>

- <span data-ttu-id="d63c9-118">A ValidateLength attribútum határozza meg a [System.Management.Automation.Validatelengthattribute](/dotnet/api/System.Management.Automation.ValidateLengthAttribute) osztály.</span><span class="sxs-lookup"><span data-stu-id="d63c9-118">The ValidateLength attribute is defined by the [System.Management.Automation.Validatelengthattribute](/dotnet/api/System.Management.Automation.ValidateLengthAttribute) class.</span></span>

## <a name="see-also"></a><span data-ttu-id="d63c9-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d63c9-119">See Also</span></span>

[<span data-ttu-id="d63c9-120">System.Management.Automation.Validatelengthattribute</span><span class="sxs-lookup"><span data-stu-id="d63c9-120">System.Management.Automation.Validatelengthattribute</span></span>](/dotnet/api/System.Management.Automation.ValidateLengthAttribute)

[<span data-ttu-id="d63c9-121">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="d63c9-121">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
