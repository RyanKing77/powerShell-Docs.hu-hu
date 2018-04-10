---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály SendMetaConfigurationApply metódusa
ms.openlocfilehash: ab82b239ddfdb4075d9440cd66343266b3c08eda
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="sendmetaconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="cf682-103">Az MSFT_DSCLocalConfigurationManager osztály SendMetaConfigurationApply metódusa</span><span class="sxs-lookup"><span data-stu-id="cf682-103">SendMetaConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="cf682-104">Beállítja a helyi Configuration Manager beállítások konfigurációs ügynök használt.</span><span class="sxs-lookup"><span data-stu-id="cf682-104">Sets the Local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

<a name="syntax"></a><span data-ttu-id="cf682-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="cf682-105">Syntax</span></span>
------

```mof
uint32 SendMetaConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="cf682-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="cf682-106">Parameters</span></span>
----------

<span data-ttu-id="cf682-107">*ConfigurationData* \[a\] konfigurációjának a környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="cf682-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="cf682-108">*kényszerített* \[a\] **igaz** kényszerítése a konfigurációját, és állítsa le.</span><span class="sxs-lookup"><span data-stu-id="cf682-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="cf682-109">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="cf682-109">Return value</span></span>
------------

<span data-ttu-id="cf682-110">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="cf682-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="cf682-111">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="cf682-111">Remarks</span></span>

<span data-ttu-id="cf682-112">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="cf682-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="cf682-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="cf682-113">Requirements</span></span>
------------
><span data-ttu-id="cf682-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="cf682-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="cf682-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="cf682-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="cf682-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="cf682-116">See also</span></span>


[<span data-ttu-id="cf682-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="cf682-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)