---
title: ValidateRange típusattribútum-deklaráció |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ValidateRange, described
- ValidateRange attribute
- attributes, ValidateRange
ms.assetid: 1f8066e6-e5d3-4f4e-8948-a90af5dace82
caps.latest.revision: 11
ms.openlocfilehash: 155a406b9855c435041fe175ac7d983a4b4eb8b7
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847536"
---
# <a name="validaterange-attribute-declaration"></a><span data-ttu-id="e86d3-102">ValidateRange attribútumdeklarációja</span><span class="sxs-lookup"><span data-stu-id="e86d3-102">ValidateRange Attribute Declaration</span></span>

<span data-ttu-id="e86d3-103">A ValidateRange attribútum határozza meg a minimális és maximális értékek (tartomány) a parancsmag paraméter argumentum.</span><span class="sxs-lookup"><span data-stu-id="e86d3-103">The ValidateRange attribute specifies the minimum and maximum values (the range) for the cmdlet parameter argument.</span></span> <span data-ttu-id="e86d3-104">Ez az attribútum is használható Windows PowerShell-függvényekkel.</span><span class="sxs-lookup"><span data-stu-id="e86d3-104">This attribute can also be used by Windows PowerShell functions.</span></span>

## <a name="syntax"></a><span data-ttu-id="e86d3-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="e86d3-105">Syntax</span></span>

```csharp
[ValidateRange(object minRange, object maxRange)]
```

#### <a name="parameters"></a><span data-ttu-id="e86d3-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="e86d3-106">Parameters</span></span>

<span data-ttu-id="e86d3-107">`MinRange` ([System.Object](/dotnet/api/system.object)) szükséges.</span><span class="sxs-lookup"><span data-stu-id="e86d3-107">`MinRange` ([System.Object](/dotnet/api/system.object)) Required.</span></span> <span data-ttu-id="e86d3-108">Meghatározza az engedélyezett minimális értéknél.</span><span class="sxs-lookup"><span data-stu-id="e86d3-108">Specifies the minimum value allowed.</span></span>

<span data-ttu-id="e86d3-109">`MaxRange` ([System.Object](/dotnet/api/system.object)) szükséges.</span><span class="sxs-lookup"><span data-stu-id="e86d3-109">`MaxRange` ([System.Object](/dotnet/api/system.object)) Required.</span></span> <span data-ttu-id="e86d3-110">Megadja a maximális engedélyezett érték.</span><span class="sxs-lookup"><span data-stu-id="e86d3-110">Specifies the maximum value allowed.</span></span>

## <a name="remarks"></a><span data-ttu-id="e86d3-111">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="e86d3-111">Remarks</span></span>

- <span data-ttu-id="e86d3-112">A Windows PowerShell-modul egy konstrukció hibát jelenít amikor értékét a `MinRange` paraméter értéke nagyobb a `MaxRange` paraméter.</span><span class="sxs-lookup"><span data-stu-id="e86d3-112">The Windows PowerShell runtime throws a construction error when the value of the `MinRange` parameter is greater than the value of the `MaxRange` parameter.</span></span>

- <span data-ttu-id="e86d3-113">A Windows PowerShell-modul a következő feltételek ellenőrzési hibát jelez:</span><span class="sxs-lookup"><span data-stu-id="e86d3-113">The Windows PowerShell runtime throws a validation error under the following conditions:</span></span>

    - <span data-ttu-id="e86d3-114">Ha az argumentum értéke kisebb, mint a `MinRange` korlátot vagy nagyobb, mint a `MaxRange` korlátot.</span><span class="sxs-lookup"><span data-stu-id="e86d3-114">When the value of the argument is less than the `MinRange` limit or greater than the `MaxRange` limit.</span></span>

    - <span data-ttu-id="e86d3-115">Ha az argumentuma nem ugyanolyan típusú, mint a `MinRange` és a `MaxRange` paramétereket.</span><span class="sxs-lookup"><span data-stu-id="e86d3-115">When the argument is not of the same type as the `MinRange` and the `MaxRange` parameters.</span></span>

- <span data-ttu-id="e86d3-116">A ValidateRange attribútum határozza meg a [System.Management.Automation.Validaterangeattribute](/dotnet/api/System.Management.Automation.ValidateRangeAttribute) osztály.</span><span class="sxs-lookup"><span data-stu-id="e86d3-116">The ValidateRange attribute is defined by the [System.Management.Automation.Validaterangeattribute](/dotnet/api/System.Management.Automation.ValidateRangeAttribute) class.</span></span>

## <a name="see-also"></a><span data-ttu-id="e86d3-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e86d3-117">See Also</span></span>

[<span data-ttu-id="e86d3-118">System.Management.Automation.Validaterangeattribute</span><span class="sxs-lookup"><span data-stu-id="e86d3-118">System.Management.Automation.Validaterangeattribute</span></span>](/dotnet/api/System.Management.Automation.ValidateRangeAttribute)

[<span data-ttu-id="e86d3-119">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="e86d3-119">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
