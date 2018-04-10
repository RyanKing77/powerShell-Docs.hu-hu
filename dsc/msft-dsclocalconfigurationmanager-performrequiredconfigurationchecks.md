---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály PerformRequiredConfigurationChecks metódusa
ms.openlocfilehash: 9cc4384088fcc39b09979b8ae4d023fc46307b13
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="performrequiredconfigurationchecks-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="36ea6-103">Az MSFT_DSCLocalConfigurationManager osztály PerformRequiredConfigurationChecks metódusa</span><span class="sxs-lookup"><span data-stu-id="36ea6-103">PerformRequiredConfigurationChecks method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="36ea6-104">A Feladatütemező használatával egy konzisztencia-ellenőrzés indítása.</span><span class="sxs-lookup"><span data-stu-id="36ea6-104">Starts a consistency check by using the Task Scheduler.</span></span>

<a name="syntax"></a><span data-ttu-id="36ea6-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="36ea6-105">Syntax</span></span>
------

```mof
uint32 PerformRequiredConfigurationChecks(
  [in] uint32 Flags
);
```

<a name="parameters"></a><span data-ttu-id="36ea6-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="36ea6-106">Parameters</span></span>
----------

<span data-ttu-id="36ea6-107">*Jelzők* \[a\] bitmaszk, amely határozza meg a konzisztencia-ellenőrzés futtatásához.</span><span class="sxs-lookup"><span data-stu-id="36ea6-107">*Flags* \[in\] A bitmask that specifies the type of consistency check to run.</span></span> <span data-ttu-id="36ea6-108">A következő értékek érvényesek, és egy bitenkénti használatával egyesíthetők **vagy** műveletet:</span><span class="sxs-lookup"><span data-stu-id="36ea6-108">The following values are valid, and can be combined by using a bitwise **OR** operation:</span></span>

|<span data-ttu-id="36ea6-109">Érték</span><span class="sxs-lookup"><span data-stu-id="36ea6-109">Value</span></span> |<span data-ttu-id="36ea6-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="36ea6-110">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="36ea6-111">**1**</span><span class="sxs-lookup"><span data-stu-id="36ea6-111">**1**</span></span> | <span data-ttu-id="36ea6-112">Normál konzisztencia-ellenőrzést.</span><span class="sxs-lookup"><span data-stu-id="36ea6-112">A normal consistency check.</span></span> |
|<span data-ttu-id="36ea6-113">**2**</span><span class="sxs-lookup"><span data-stu-id="36ea6-113">**2**</span></span> | <span data-ttu-id="36ea6-114">A rendszer újraindítása után konzisztencia-ellenőrzést fenntartása.</span><span class="sxs-lookup"><span data-stu-id="36ea6-114">A continuation of a consistency check after a reboot.</span></span> <span data-ttu-id="36ea6-115">Ezt az értéket nem használható együtt más értékekkel.</span><span class="sxs-lookup"><span data-stu-id="36ea6-115">This value should not be combined with other values.</span></span> |
|<span data-ttu-id="36ea6-116">**4**</span><span class="sxs-lookup"><span data-stu-id="36ea6-116">**4**</span></span> | <span data-ttu-id="36ea6-117">A konfigurációs kell kell húzni a csomópont metakonfigurációját megadott lekérési kiszolgálójáról.</span><span class="sxs-lookup"><span data-stu-id="36ea6-117">The configuration should be pulled from the pull server specified in the metaconfiguration for the node.</span></span> <span data-ttu-id="36ea6-118">Ez az érték mindig használható együtt **1**, az érték **5**.</span><span class="sxs-lookup"><span data-stu-id="36ea6-118">This value should always be combined with **1**, for a value of **5**.</span></span> |
|<span data-ttu-id="36ea6-119">**8**</span><span class="sxs-lookup"><span data-stu-id="36ea6-119">**8**</span></span> | <span data-ttu-id="36ea6-120">A jelentéskészítő kiszolgáló állapota küldeni.</span><span class="sxs-lookup"><span data-stu-id="36ea6-120">Send status to the report server.</span></span> |

## <a name="return-value"></a><span data-ttu-id="36ea6-121">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="36ea6-121">Return value</span></span>
------------

<span data-ttu-id="36ea6-122">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="36ea6-122">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="36ea6-123">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="36ea6-123">Remarks</span></span>

<span data-ttu-id="36ea6-124">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="36ea6-124">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="36ea6-125">Követelmények</span><span class="sxs-lookup"><span data-stu-id="36ea6-125">Requirements</span></span>
------------
><span data-ttu-id="36ea6-126">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="36ea6-126">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="36ea6-127">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="36ea6-127">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="36ea6-128">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="36ea6-128">See also</span></span>


[<span data-ttu-id="36ea6-129">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="36ea6-129">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)