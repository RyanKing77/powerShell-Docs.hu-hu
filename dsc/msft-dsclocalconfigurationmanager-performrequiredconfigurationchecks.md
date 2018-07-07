---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály PerformRequiredConfigurationChecks metódusa
ms.openlocfilehash: b92eefb7fbea6d96afa31f6b802ba10fe20d4103
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893229"
---
# <a name="performrequiredconfigurationchecks-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="e7242-103">Az MSFT_DSCLocalConfigurationManager osztály PerformRequiredConfigurationChecks metódusa</span><span class="sxs-lookup"><span data-stu-id="e7242-103">PerformRequiredConfigurationChecks method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="e7242-104">A Feladatütemező használatával egy konzisztencia-ellenőrzés indítása.</span><span class="sxs-lookup"><span data-stu-id="e7242-104">Starts a consistency check by using the Task Scheduler.</span></span>

## <a name="syntax"></a><span data-ttu-id="e7242-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="e7242-105">Syntax</span></span>

```mof
uint32 PerformRequiredConfigurationChecks(
  [in] uint32 Flags
);
```

## <a name="parameters"></a><span data-ttu-id="e7242-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="e7242-106">Parameters</span></span>

<span data-ttu-id="e7242-107">*Jelölők* \[a\] bitmaszk, amely meghatározza a konzisztencia-ellenőrzés futtatásához.</span><span class="sxs-lookup"><span data-stu-id="e7242-107">*Flags* \[in\] A bitmask that specifies the type of consistency check to run.</span></span> <span data-ttu-id="e7242-108">A következő értékek érvényesek, és a egy bitenkénti használatával egyesíthető **vagy** műveletet:</span><span class="sxs-lookup"><span data-stu-id="e7242-108">The following values are valid, and can be combined by using a bitwise **OR** operation:</span></span>

|<span data-ttu-id="e7242-109">Érték</span><span class="sxs-lookup"><span data-stu-id="e7242-109">Value</span></span> |<span data-ttu-id="e7242-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="e7242-110">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="e7242-111">**1**</span><span class="sxs-lookup"><span data-stu-id="e7242-111">**1**</span></span> | <span data-ttu-id="e7242-112">Normál konzisztencia-ellenőrzést.</span><span class="sxs-lookup"><span data-stu-id="e7242-112">A normal consistency check.</span></span> |
|<span data-ttu-id="e7242-113">**2**</span><span class="sxs-lookup"><span data-stu-id="e7242-113">**2**</span></span> | <span data-ttu-id="e7242-114">Újraindítás után konzisztencia-ellenőrzést folytatása.</span><span class="sxs-lookup"><span data-stu-id="e7242-114">A continuation of a consistency check after a reboot.</span></span> <span data-ttu-id="e7242-115">Ez az érték nem egyesíthetők más értékeket.</span><span class="sxs-lookup"><span data-stu-id="e7242-115">This value should not be combined with other values.</span></span> |
|<span data-ttu-id="e7242-116">**4**</span><span class="sxs-lookup"><span data-stu-id="e7242-116">**4**</span></span> | <span data-ttu-id="e7242-117">A megadott csomópont a metaconfiguration lekéréses kiszolgálón kell kéri le a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="e7242-117">The configuration should be pulled from the pull server specified in the metaconfiguration for the node.</span></span> <span data-ttu-id="e7242-118">Ez az érték mindig kombinálni kell **1**, a egy értéke **5**.</span><span class="sxs-lookup"><span data-stu-id="e7242-118">This value should always be combined with **1**, for a value of **5**.</span></span> |
|<span data-ttu-id="e7242-119">**8**</span><span class="sxs-lookup"><span data-stu-id="e7242-119">**8**</span></span> | <span data-ttu-id="e7242-120">A jelentéskészítő kiszolgáló állapota küldeni.</span><span class="sxs-lookup"><span data-stu-id="e7242-120">Send status to the report server.</span></span> |

## <a name="return-value"></a><span data-ttu-id="e7242-121">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="e7242-121">Return value</span></span>

<span data-ttu-id="e7242-122">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="e7242-122">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="e7242-123">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="e7242-123">Remarks</span></span>

<span data-ttu-id="e7242-124">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="e7242-124">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="e7242-125">Követelmények</span><span class="sxs-lookup"><span data-stu-id="e7242-125">Requirements</span></span>

<span data-ttu-id="e7242-126">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="e7242-126">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="e7242-127">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="e7242-127">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="e7242-128">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e7242-128">See also</span></span>

[<span data-ttu-id="e7242-129">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="e7242-129">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)