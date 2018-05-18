---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApply metódusa
ms.openlocfilehash: c578f4f52d3ea70e7bcf683ac204d6e484d4630d
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="sendconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="7e465-103">Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApply metódusa</span><span class="sxs-lookup"><span data-stu-id="7e465-103">SendConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="7e465-104">A konfigurációs dokumentum küld a felügyelt csomóponthoz, és a konfigurációs ügynök segítségével a konfiguráció alkalmazásához.</span><span class="sxs-lookup"><span data-stu-id="7e465-104">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="7e465-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="7e465-105">Syntax</span></span>
------

```mof
uint32 SendConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="7e465-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="7e465-106">Parameters</span></span>
----------

<span data-ttu-id="7e465-107">*ConfigurationData* \[a\] konfigurációjának a környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="7e465-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="7e465-108">*kényszerített* \[a\] **igaz** kényszerítése a konfigurációját, és állítsa le.</span><span class="sxs-lookup"><span data-stu-id="7e465-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="7e465-109">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="7e465-109">Return value</span></span>
------------

<span data-ttu-id="7e465-110">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="7e465-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="7e465-111">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="7e465-111">Remarks</span></span>

<span data-ttu-id="7e465-112">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="7e465-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="7e465-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="7e465-113">Requirements</span></span>
------------
><span data-ttu-id="7e465-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="7e465-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="7e465-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="7e465-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="7e465-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="7e465-116">See also</span></span>


[<span data-ttu-id="7e465-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="7e465-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)