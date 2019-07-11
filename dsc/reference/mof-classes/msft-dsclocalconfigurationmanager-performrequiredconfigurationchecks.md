---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: PerformRequiredConfigurationChecks method
ms.openlocfilehash: 909e3a48d08e0220ab0efc6a03bea7ead5d9843e
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67734405"
---
# <a name="performrequiredconfigurationchecks-method"></a><span data-ttu-id="a8550-103">PerformRequiredConfigurationChecks method</span><span class="sxs-lookup"><span data-stu-id="a8550-103">PerformRequiredConfigurationChecks method</span></span>

<span data-ttu-id="a8550-104">A Feladatütemező használatával egy konzisztencia-ellenőrzés indítása.</span><span class="sxs-lookup"><span data-stu-id="a8550-104">Starts a consistency check by using the Task Scheduler.</span></span>

## <a name="syntax"></a><span data-ttu-id="a8550-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="a8550-105">Syntax</span></span>

```mof
uint32 PerformRequiredConfigurationChecks(
  [in] uint32 Flags
);
```

## <a name="parameters"></a><span data-ttu-id="a8550-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="a8550-106">Parameters</span></span>

<span data-ttu-id="a8550-107">*Jelölők* \[a\] bitmaszk, amely meghatározza a konzisztencia-ellenőrzés futtatásához.</span><span class="sxs-lookup"><span data-stu-id="a8550-107">*Flags* \[in\] A bitmask that specifies the type of consistency check to run.</span></span> <span data-ttu-id="a8550-108">A következő értékek érvényesek, és a egy bitenkénti használatával egyesíthető **vagy** műveletet:</span><span class="sxs-lookup"><span data-stu-id="a8550-108">The following values are valid, and can be combined by using a bitwise **OR** operation:</span></span>

|<span data-ttu-id="a8550-109">Érték</span><span class="sxs-lookup"><span data-stu-id="a8550-109">Value</span></span> |<span data-ttu-id="a8550-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="a8550-110">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="a8550-111">**1**</span><span class="sxs-lookup"><span data-stu-id="a8550-111">**1**</span></span> | <span data-ttu-id="a8550-112">Normál konzisztencia-ellenőrzést.</span><span class="sxs-lookup"><span data-stu-id="a8550-112">A normal consistency check.</span></span> |
|<span data-ttu-id="a8550-113">**2**</span><span class="sxs-lookup"><span data-stu-id="a8550-113">**2**</span></span> | <span data-ttu-id="a8550-114">Újraindítás után konzisztencia-ellenőrzést folytatása.</span><span class="sxs-lookup"><span data-stu-id="a8550-114">A continuation of a consistency check after a reboot.</span></span> <span data-ttu-id="a8550-115">Ez az érték nem egyesíthetők más értékeket.</span><span class="sxs-lookup"><span data-stu-id="a8550-115">This value should not be combined with other values.</span></span> |
|<span data-ttu-id="a8550-116">**4**</span><span class="sxs-lookup"><span data-stu-id="a8550-116">**4**</span></span> | <span data-ttu-id="a8550-117">A megadott csomópont a metaconfiguration lekéréses kiszolgálón kell kéri le a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="a8550-117">The configuration should be pulled from the pull server specified in the metaconfiguration for the node.</span></span> <span data-ttu-id="a8550-118">Ez az érték mindig kombinálni kell **1**, a egy értéke **5**.</span><span class="sxs-lookup"><span data-stu-id="a8550-118">This value should always be combined with **1**, for a value of **5**.</span></span> |
|<span data-ttu-id="a8550-119">**8**</span><span class="sxs-lookup"><span data-stu-id="a8550-119">**8**</span></span> | <span data-ttu-id="a8550-120">A jelentéskészítő kiszolgáló állapota küldeni.</span><span class="sxs-lookup"><span data-stu-id="a8550-120">Send status to the report server.</span></span> |

## <a name="return-value"></a><span data-ttu-id="a8550-121">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="a8550-121">Return value</span></span>

<span data-ttu-id="a8550-122">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="a8550-122">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="a8550-123">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="a8550-123">Remarks</span></span>

<span data-ttu-id="a8550-124">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="a8550-124">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="a8550-125">Követelmények</span><span class="sxs-lookup"><span data-stu-id="a8550-125">Requirements</span></span>

<span data-ttu-id="a8550-126">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="a8550-126">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="a8550-127">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="a8550-127">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="a8550-128">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="a8550-128">See also</span></span>

[<span data-ttu-id="a8550-129">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="a8550-129">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
