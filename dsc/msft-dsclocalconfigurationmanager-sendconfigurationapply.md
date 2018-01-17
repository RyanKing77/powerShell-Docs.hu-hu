---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály SendConfigurationApply módszer"
ms.openlocfilehash: 20f732d35860cccde4e507dc6916e27d0cf8c5f6
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="sendconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="1a540-103">A MSFT_DSCLocalConfigurationManager osztály SendConfigurationApply módszer</span><span class="sxs-lookup"><span data-stu-id="1a540-103">SendConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="1a540-104">A konfigurációs dokumentum küld a felügyelt csomóponthoz, és a konfigurációs ügynök segítségével a konfiguráció alkalmazásához.</span><span class="sxs-lookup"><span data-stu-id="1a540-104">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="1a540-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="1a540-105">Syntax</span></span>
------

```mof
uint32 SendConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="1a540-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="1a540-106">Parameters</span></span>
----------

<span data-ttu-id="1a540-107">*ConfigurationData* \[a\]</span><span class="sxs-lookup"><span data-stu-id="1a540-107">*ConfigurationData* \[in\]</span></span>  
<span data-ttu-id="1a540-108">A környezet konfigurációjának adatait.</span><span class="sxs-lookup"><span data-stu-id="1a540-108">The environment data for the configuration.</span></span>

<span data-ttu-id="1a540-109">*kényszerített* \[a\]</span><span class="sxs-lookup"><span data-stu-id="1a540-109">*force* \[in\]</span></span>  
<span data-ttu-id="1a540-110">**Igaz** kényszerítése a konfigurációját, és állítsa le.</span><span class="sxs-lookup"><span data-stu-id="1a540-110">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="1a540-111">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="1a540-111">Return value</span></span>
------------

<span data-ttu-id="1a540-112">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="1a540-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="1a540-113">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="1a540-113">Remarks</span></span>

<span data-ttu-id="1a540-114">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="1a540-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="1a540-115">Követelmények</span><span class="sxs-lookup"><span data-stu-id="1a540-115">Requirements</span></span>
------------
><span data-ttu-id="1a540-116">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="1a540-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="1a540-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="1a540-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="1a540-118">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="1a540-118">See also</span></span>


[<span data-ttu-id="1a540-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="1a540-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



