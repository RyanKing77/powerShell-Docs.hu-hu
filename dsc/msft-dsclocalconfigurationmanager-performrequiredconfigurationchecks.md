---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály PerformRequiredConfigurationChecks módszer"
ms.openlocfilehash: 687c92f2dac5e8855731713e81390ac67615231e
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="performrequiredconfigurationchecks-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="fef79-103">A MSFT_DSCLocalConfigurationManager osztály PerformRequiredConfigurationChecks módszer</span><span class="sxs-lookup"><span data-stu-id="fef79-103">PerformRequiredConfigurationChecks method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="fef79-104">A Feladatütemező használatával egy konzisztencia-ellenőrzés indítása.</span><span class="sxs-lookup"><span data-stu-id="fef79-104">Starts a consistency check by using the Task Scheduler.</span></span>

<a name="syntax"></a><span data-ttu-id="fef79-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="fef79-105">Syntax</span></span>
------

```mof
uint32 PerformRequiredConfigurationChecks(
  [in] uint32 Flags
);
```

<a name="parameters"></a><span data-ttu-id="fef79-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="fef79-106">Parameters</span></span>
----------

<span data-ttu-id="fef79-107">*Jelzők* \[a\]</span><span class="sxs-lookup"><span data-stu-id="fef79-107">*Flags* \[in\]</span></span>  
<span data-ttu-id="fef79-108">Bitmaszk, amely határozza meg a konzisztencia-ellenőrzés futtatásához.</span><span class="sxs-lookup"><span data-stu-id="fef79-108">A bitmask that specifies the type of consistency check to run.</span></span> <span data-ttu-id="fef79-109">A következő értékek érvényesek, és egy bitenkénti használatával egyesíthetők **vagy** műveletet:</span><span class="sxs-lookup"><span data-stu-id="fef79-109">The following values are valid, and can be combined by using a bitwise **OR** operation:</span></span>

|<span data-ttu-id="fef79-110">Érték</span><span class="sxs-lookup"><span data-stu-id="fef79-110">Value</span></span> |<span data-ttu-id="fef79-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="fef79-111">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="fef79-112">**1**</span><span class="sxs-lookup"><span data-stu-id="fef79-112">**1**</span></span> | <span data-ttu-id="fef79-113">Normál konzisztencia-ellenőrzést.</span><span class="sxs-lookup"><span data-stu-id="fef79-113">A normal consistency check.</span></span> |
|<span data-ttu-id="fef79-114">**2**</span><span class="sxs-lookup"><span data-stu-id="fef79-114">**2**</span></span> | <span data-ttu-id="fef79-115">A rendszer újraindítása után konzisztencia-ellenőrzést fenntartása.</span><span class="sxs-lookup"><span data-stu-id="fef79-115">A continuation of a consistency check after a reboot.</span></span> <span data-ttu-id="fef79-116">Ezt az értéket nem használható együtt más értékekkel.</span><span class="sxs-lookup"><span data-stu-id="fef79-116">This value should not be combined with other values.</span></span> |
|<span data-ttu-id="fef79-117">**4**</span><span class="sxs-lookup"><span data-stu-id="fef79-117">**4**</span></span> | <span data-ttu-id="fef79-118">A konfigurációs kell kell húzni a csomópont metakonfigurációját megadott lekérési kiszolgálójáról.</span><span class="sxs-lookup"><span data-stu-id="fef79-118">The configuration should be pulled from the pull server specified in the metaconfiguration for the node.</span></span> <span data-ttu-id="fef79-119">Ez az érték mindig használható együtt **1**, az érték **5**.</span><span class="sxs-lookup"><span data-stu-id="fef79-119">This value should always be combined with **1**, for a value of **5**.</span></span> |
|<span data-ttu-id="fef79-120">**8**</span><span class="sxs-lookup"><span data-stu-id="fef79-120">**8**</span></span> | <span data-ttu-id="fef79-121">A jelentéskészítő kiszolgáló állapota küldeni.</span><span class="sxs-lookup"><span data-stu-id="fef79-121">Send status to the report server.</span></span> |

## <a name="return-value"></a><span data-ttu-id="fef79-122">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="fef79-122">Return value</span></span>
------------

<span data-ttu-id="fef79-123">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="fef79-123">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="fef79-124">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="fef79-124">Remarks</span></span>

<span data-ttu-id="fef79-125">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="fef79-125">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="fef79-126">Követelmények</span><span class="sxs-lookup"><span data-stu-id="fef79-126">Requirements</span></span>
------------
><span data-ttu-id="fef79-127">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="fef79-127">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="fef79-128">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="fef79-128">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="fef79-129">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="fef79-129">See also</span></span>


[<span data-ttu-id="fef79-130">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="fef79-130">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



