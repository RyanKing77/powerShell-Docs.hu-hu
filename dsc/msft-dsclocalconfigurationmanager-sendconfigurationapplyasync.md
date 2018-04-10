---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApplyAsync metódusa
ms.openlocfilehash: 7ff821a277a548869862741551ee9897e417ea45
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="sendconfigurationapplyasync-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="d1eff-103">Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApplyAsync metódusa</span><span class="sxs-lookup"><span data-stu-id="d1eff-103">SendConfigurationApplyAsync method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="d1eff-104">A konfigurációs dokumentum aszinkron módon küld a felügyelt csomóponthoz, és a konfigurációs ügynök segítségével a konfiguráció alkalmazásához.</span><span class="sxs-lookup"><span data-stu-id="d1eff-104">Sends the configuration document asynchronously to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="d1eff-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="d1eff-105">Syntax</span></span>
------

```mof
uint32 SendConfigurationApplyAsync(
  [in] uint8   ConfigurationData[],
  [in] boolean force,
  [in] string  jobId
);
```

<a name="parameters"></a><span data-ttu-id="d1eff-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="d1eff-106">Parameters</span></span>
----------

<span data-ttu-id="d1eff-107">*ConfigurationData* \[a\] konfigurációjának a környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="d1eff-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="d1eff-108">*kényszerített* \[a\] **igaz** kényszerítése a konfigurációját, és állítsa le.</span><span class="sxs-lookup"><span data-stu-id="d1eff-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

<span data-ttu-id="d1eff-109">*a JobId értékének* \[a\] küldési a konfigurációs feladat az azonosító.</span><span class="sxs-lookup"><span data-stu-id="d1eff-109">*jobId* \[in\] The ID of the job for which to send the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="d1eff-110">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="d1eff-110">Return value</span></span>
------------

<span data-ttu-id="d1eff-111">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="d1eff-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="d1eff-112">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="d1eff-112">Remarks</span></span>

<span data-ttu-id="d1eff-113">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="d1eff-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="d1eff-114">Követelmények</span><span class="sxs-lookup"><span data-stu-id="d1eff-114">Requirements</span></span>
------------
><span data-ttu-id="d1eff-115">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="d1eff-115">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="d1eff-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="d1eff-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="d1eff-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d1eff-117">See also</span></span>


[<span data-ttu-id="d1eff-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="d1eff-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)