---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály SendConfigurationApplyAsync módszer"
ms.openlocfilehash: e680bfd1c5b39d364c90cf5ef6b43d0a568af23a
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="sendconfigurationapplyasync-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="34a69-103">A MSFT_DSCLocalConfigurationManager osztály SendConfigurationApplyAsync módszer</span><span class="sxs-lookup"><span data-stu-id="34a69-103">SendConfigurationApplyAsync method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="34a69-104">A konfigurációs dokumentum aszinkron módon küld a felügyelt csomóponthoz, és a konfigurációs ügynök segítségével a konfiguráció alkalmazásához.</span><span class="sxs-lookup"><span data-stu-id="34a69-104">Sends the configuration document asynchronously to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="34a69-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="34a69-105">Syntax</span></span>
------

```mof
uint32 SendConfigurationApplyAsync(
  [in] uint8   ConfigurationData[],
  [in] boolean force,
  [in] string  jobId
);
```

<a name="parameters"></a><span data-ttu-id="34a69-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="34a69-106">Parameters</span></span>
----------

<span data-ttu-id="34a69-107">*ConfigurationData* \[a\]</span><span class="sxs-lookup"><span data-stu-id="34a69-107">*ConfigurationData* \[in\]</span></span>  
<span data-ttu-id="34a69-108">A környezet konfigurációjának adatait.</span><span class="sxs-lookup"><span data-stu-id="34a69-108">The environment data for the configuration.</span></span>

<span data-ttu-id="34a69-109">*kényszerített* \[a\]</span><span class="sxs-lookup"><span data-stu-id="34a69-109">*force* \[in\]</span></span>  
<span data-ttu-id="34a69-110">**Igaz** kényszerítése a konfigurációját, és állítsa le.</span><span class="sxs-lookup"><span data-stu-id="34a69-110">**true** to force the configuration to stop.</span></span>

<span data-ttu-id="34a69-111">*a JobId értékének* \[a\]</span><span class="sxs-lookup"><span data-stu-id="34a69-111">*jobId* \[in\]</span></span>  
<span data-ttu-id="34a69-112">A konfigurációs küldési feladat Azonosítóját.</span><span class="sxs-lookup"><span data-stu-id="34a69-112">The ID of the job for which to send the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="34a69-113">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="34a69-113">Return value</span></span>
------------

<span data-ttu-id="34a69-114">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="34a69-114">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="34a69-115">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="34a69-115">Remarks</span></span>

<span data-ttu-id="34a69-116">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="34a69-116">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="34a69-117">Követelmények</span><span class="sxs-lookup"><span data-stu-id="34a69-117">Requirements</span></span>
------------
><span data-ttu-id="34a69-118">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="34a69-118">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="34a69-119">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="34a69-119">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="34a69-120">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="34a69-120">See also</span></span>


[<span data-ttu-id="34a69-121">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="34a69-121">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



