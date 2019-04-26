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
ms.openlocfilehash: ffc45f6b80a2b7ed22f27d083d042b1de7f353f6
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067178"
---
# <a name="validatecount-attribute-declaration"></a><span data-ttu-id="2bca2-102">ValidateCount attribútumdeklarációja</span><span class="sxs-lookup"><span data-stu-id="2bca2-102">ValidateCount Attribute Declaration</span></span>

<span data-ttu-id="2bca2-103">A ValidateCount attribútum határozza meg a minimális és maximális számú argumentum az engedélyezett egy parancsmag-paraméterben.</span><span class="sxs-lookup"><span data-stu-id="2bca2-103">The ValidateCount attribute specifies the minimum and maximum number of arguments allowed for a cmdlet parameter.</span></span>

## <a name="syntax"></a><span data-ttu-id="2bca2-104">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="2bca2-104">Syntax</span></span>

```csharp
[ValidateCount(int minLength, int maxlength)]
```

#### <a name="parameters"></a><span data-ttu-id="2bca2-105">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="2bca2-105">Parameters</span></span>

<span data-ttu-id="2bca2-106">`MinLength` ([System.Int32][]) szükséges.</span><span class="sxs-lookup"><span data-stu-id="2bca2-106">`MinLength` ([System.Int32][]) Required.</span></span> <span data-ttu-id="2bca2-107">Adja meg a minimális számú argumentumot.</span><span class="sxs-lookup"><span data-stu-id="2bca2-107">Specifies the minimum number of arguments.</span></span>

<span data-ttu-id="2bca2-108">`MaxLength`([System.Int32][]) szükséges.</span><span class="sxs-lookup"><span data-stu-id="2bca2-108">`MaxLength`([System.Int32][]) Required.</span></span> <span data-ttu-id="2bca2-109">Megadja a maximális számú argumentumot.</span><span class="sxs-lookup"><span data-stu-id="2bca2-109">Specifies the maximum number of arguments.</span></span>

## <a name="remarks"></a><span data-ttu-id="2bca2-110">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="2bca2-110">Remarks</span></span>

- <span data-ttu-id="2bca2-111">Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [Az argumentumok száma ellenőrzése][].</span><span class="sxs-lookup"><span data-stu-id="2bca2-111">For more information about how to declare this attribute, see [How to Validate an Argument Count][].</span></span>

- <span data-ttu-id="2bca2-112">Ez az attribútum nem hív, ha a megfelelő parancsmag paraméter rendelkezhet tetszőleges számú argumentum.</span><span class="sxs-lookup"><span data-stu-id="2bca2-112">When this attribute is not invoked, the corresponding cmdlet parameter can have any number of arguments.</span></span>

- <span data-ttu-id="2bca2-113">A Windows PowerShell-modul a következő feltételek hibát jelez:</span><span class="sxs-lookup"><span data-stu-id="2bca2-113">The Windows PowerShell runtime throws an error under the following conditions:</span></span>

    - <span data-ttu-id="2bca2-114">A `MinLength` és `MaxLength` attribútum paraméterek nejsou typu [System.Int32][].</span><span class="sxs-lookup"><span data-stu-id="2bca2-114">The `MinLength` and `MaxLength` attribute parameters are not of type [System.Int32][].</span></span>

    - <span data-ttu-id="2bca2-115">Értékét a `MaxLength` attribútum paraméter értéke kisebb, mint az értékét a `MinLength` paraméter attribútum.</span><span class="sxs-lookup"><span data-stu-id="2bca2-115">The value of the `MaxLength` attribute parameter is less than the value of the `MinLength` attribute parameter.</span></span>

- <span data-ttu-id="2bca2-116">A ValidateCount attribútum határozza meg a [System.Management.Automation.ValidateCountAttribute][] osztály.</span><span class="sxs-lookup"><span data-stu-id="2bca2-116">The ValidateCount attribute is defined by the [System.Management.Automation.ValidateCountAttribute][] class.</span></span>

## <a name="see-also"></a><span data-ttu-id="2bca2-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2bca2-117">See Also</span></span>

<span data-ttu-id="2bca2-118">[System.Management.Automation.ValidateCountAttribute][]</span><span class="sxs-lookup"><span data-stu-id="2bca2-118">[System.Management.Automation.ValidateCountAttribute][]</span></span>

<span data-ttu-id="2bca2-119">[Az argumentumok száma ellenőrzése][]</span><span class="sxs-lookup"><span data-stu-id="2bca2-119">[How to Validate an Argument Count][]</span></span>

<span data-ttu-id="2bca2-120">[Egy Windows PowerShell-parancsmag írása][]</span><span class="sxs-lookup"><span data-stu-id="2bca2-120">[Writing a Windows PowerShell Cmdlet][]</span></span>

[Az argumentumok száma ellenőrzése]: how-to-validate-an-argument-count.md
[How to Validate an Argument Count]: how-to-validate-an-argument-count.md
[Egy Windows PowerShell-parancsmag írása]: writing-a-windows-powershell-cmdlet.md
[Writing a Windows PowerShell Cmdlet]: writing-a-windows-powershell-cmdlet.md

[System.Int32]: /dotnet/api/System.Int32
[System.Management.Automation.ValidateCountAttribute]: /dotnet/api/System.Management.Automation.ValidateCountAttribute
