---
title: ValidateCount típusattribútum-deklaráció |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- attributes, ValidateCount
- ValidateCount attribute, described
- ValidateCount attribute
ms.assetid: 516af1ef-2c2e-408d-84bc-865f5bccf761
caps.latest.revision: 11
ms.openlocfilehash: 4e0be34b6f7a56dcf02a4381de4d2a5d08db14df
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57794440"
---
# <a name="validatecount-attribute-declaration"></a><span data-ttu-id="de3bc-102">ValidateCount attribútumdeklarációja</span><span class="sxs-lookup"><span data-stu-id="de3bc-102">ValidateCount Attribute Declaration</span></span>

<span data-ttu-id="de3bc-103">A ValidateCount attribútum határozza meg a minimális és maximális számú argumentum az engedélyezett egy parancsmag-paraméterben.</span><span class="sxs-lookup"><span data-stu-id="de3bc-103">The ValidateCount attribute specifies the minimum and maximum number of arguments allowed for a cmdlet parameter.</span></span>

## <a name="syntax"></a><span data-ttu-id="de3bc-104">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="de3bc-104">Syntax</span></span>

```csharp
[ValidateCount(int minLength, int maxlength)]
```

#### <a name="parameters"></a><span data-ttu-id="de3bc-105">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="de3bc-105">Parameters</span></span>

<span data-ttu-id="de3bc-106">`MinLength` ([System.Int32](/dotnet/api/System.Int32)) szükséges.</span><span class="sxs-lookup"><span data-stu-id="de3bc-106">`MinLength` ([System.Int32](/dotnet/api/System.Int32)) Required.</span></span> <span data-ttu-id="de3bc-107">Adja meg a minimális számú argumentumot.</span><span class="sxs-lookup"><span data-stu-id="de3bc-107">Specifies the minimum number of arguments.</span></span>

<span data-ttu-id="de3bc-108">`MaxLength`([System.Int32](/dotnet/api/System.Int32)) szükséges.</span><span class="sxs-lookup"><span data-stu-id="de3bc-108">`MaxLength`([System.Int32](/dotnet/api/System.Int32)) Required.</span></span> <span data-ttu-id="de3bc-109">Megadja a maximális számú argumentumot.</span><span class="sxs-lookup"><span data-stu-id="de3bc-109">Specifies the maximum number of arguments.</span></span>

## <a name="remarks"></a><span data-ttu-id="de3bc-110">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="de3bc-110">Remarks</span></span>

- <span data-ttu-id="de3bc-111">Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [bemenet-ellenőrzési szabályok deklarálja hogyan](http://msdn.microsoft.com/en-us/544c2100-62ba-4be4-b2a2-cc0d4e4fc45b).</span><span class="sxs-lookup"><span data-stu-id="de3bc-111">For more information about how to declare this attribute, see [How to Declare Input Validation Rules](http://msdn.microsoft.com/en-us/544c2100-62ba-4be4-b2a2-cc0d4e4fc45b).</span></span>

- <span data-ttu-id="de3bc-112">Ez az attribútum nem hív, ha a megfelelő parancsmag paraméter rendelkezhet tetszőleges számú argumentum.</span><span class="sxs-lookup"><span data-stu-id="de3bc-112">When this attribute is not invoked, the corresponding cmdlet parameter can have any number of arguments.</span></span>

- <span data-ttu-id="de3bc-113">A Windows PowerShell-modul a következő feltételek hibát jelez:</span><span class="sxs-lookup"><span data-stu-id="de3bc-113">The Windows PowerShell runtime throws an error under the following conditions:</span></span>

    - <span data-ttu-id="de3bc-114">A `MinLength` és `MaxLength` attribútum paraméterek nejsou typu [System.Int32](/dotnet/api/System.Int32).</span><span class="sxs-lookup"><span data-stu-id="de3bc-114">The `MinLength` and `MaxLength` attribute parameters are not of type [System.Int32](/dotnet/api/System.Int32).</span></span>

    - <span data-ttu-id="de3bc-115">Értékét a `MaxLength` attribútum paraméter értéke kisebb, mint az értékét a `MinLength` paraméter attribútum.</span><span class="sxs-lookup"><span data-stu-id="de3bc-115">The value of the `MaxLength` attribute parameter is less than the value of the `MinLength` attribute parameter.</span></span>

- <span data-ttu-id="de3bc-116">A ValidateCount attribútum határozza meg a [System.Management.Automation.Validatecount](/dotnet/api/System.Management.Automation.ValidateCount) osztály.</span><span class="sxs-lookup"><span data-stu-id="de3bc-116">The ValidateCount attribute is defined by the [System.Management.Automation.Validatecount](/dotnet/api/System.Management.Automation.ValidateCount) class.</span></span>

## <a name="see-also"></a><span data-ttu-id="de3bc-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="de3bc-117">See Also</span></span>

[<span data-ttu-id="de3bc-118">System.Management.Automation.Validatecount</span><span class="sxs-lookup"><span data-stu-id="de3bc-118">System.Management.Automation.Validatecount</span></span>](/dotnet/api/System.Management.Automation.ValidateCount)

[<span data-ttu-id="de3bc-119">Hogyan deklarálja a bemeneti érvényesítési szabályok</span><span class="sxs-lookup"><span data-stu-id="de3bc-119">How to Declare Input Validation Rules</span></span>](http://msdn.microsoft.com/en-us/544c2100-62ba-4be4-b2a2-cc0d4e4fc45b)

[<span data-ttu-id="de3bc-120">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="de3bc-120">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
