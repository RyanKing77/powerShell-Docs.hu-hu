---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApplyAsync metódusa
ms.openlocfilehash: acd8f380f1c49eb008563398c2c3de3fce5477f9
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="sendconfigurationapplyasync-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="d9bd1-103">Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApplyAsync metódusa</span><span class="sxs-lookup"><span data-stu-id="d9bd1-103">SendConfigurationApplyAsync method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="d9bd1-104">A konfigurációs dokumentum aszinkron módon küld a felügyelt csomóponthoz, és a konfigurációs ügynök segítségével a konfiguráció alkalmazásához.</span><span class="sxs-lookup"><span data-stu-id="d9bd1-104">Sends the configuration document asynchronously to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="d9bd1-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="d9bd1-105">Syntax</span></span>
------

```mof
uint32 SendConfigurationApplyAsync(
  [in] uint8   ConfigurationData[],
  [in] boolean force,
  [in] string  jobId
);
```

<a name="parameters"></a><span data-ttu-id="d9bd1-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="d9bd1-106">Parameters</span></span>
----------

<span data-ttu-id="d9bd1-107">*ConfigurationData* \[a\] konfigurációjának a környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="d9bd1-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="d9bd1-108">*kényszerített* \[a\] **igaz** kényszerítése a konfigurációját, és állítsa le.</span><span class="sxs-lookup"><span data-stu-id="d9bd1-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

<span data-ttu-id="d9bd1-109">*a JobId értékének* \[a\] küldési a konfigurációs feladat az azonosító.</span><span class="sxs-lookup"><span data-stu-id="d9bd1-109">*jobId* \[in\] The ID of the job for which to send the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="d9bd1-110">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="d9bd1-110">Return value</span></span>
------------

<span data-ttu-id="d9bd1-111">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="d9bd1-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="d9bd1-112">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="d9bd1-112">Remarks</span></span>

<span data-ttu-id="d9bd1-113">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="d9bd1-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="d9bd1-114">Követelmények</span><span class="sxs-lookup"><span data-stu-id="d9bd1-114">Requirements</span></span>
------------
><span data-ttu-id="d9bd1-115">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="d9bd1-115">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="d9bd1-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="d9bd1-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="d9bd1-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d9bd1-117">See also</span></span>


[<span data-ttu-id="d9bd1-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="d9bd1-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)