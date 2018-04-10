---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApply metódusa
ms.openlocfilehash: 8edf8c55089e767394ba21b42fe74072777a45c9
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="sendconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="73548-103">Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApply metódusa</span><span class="sxs-lookup"><span data-stu-id="73548-103">SendConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="73548-104">A konfigurációs dokumentum küld a felügyelt csomóponthoz, és a konfigurációs ügynök segítségével a konfiguráció alkalmazásához.</span><span class="sxs-lookup"><span data-stu-id="73548-104">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="73548-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="73548-105">Syntax</span></span>
------

```mof
uint32 SendConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="73548-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="73548-106">Parameters</span></span>
----------

<span data-ttu-id="73548-107">*ConfigurationData* \[a\] konfigurációjának a környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="73548-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="73548-108">*kényszerített* \[a\] **igaz** kényszerítése a konfigurációját, és állítsa le.</span><span class="sxs-lookup"><span data-stu-id="73548-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="73548-109">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="73548-109">Return value</span></span>
------------

<span data-ttu-id="73548-110">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="73548-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="73548-111">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="73548-111">Remarks</span></span>

<span data-ttu-id="73548-112">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="73548-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="73548-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="73548-113">Requirements</span></span>
------------
><span data-ttu-id="73548-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="73548-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="73548-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="73548-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="73548-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="73548-116">See also</span></span>


[<span data-ttu-id="73548-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="73548-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)