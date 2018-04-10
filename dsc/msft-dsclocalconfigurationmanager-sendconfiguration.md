---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály SendConfiguration metódusa
ms.openlocfilehash: 07ae48dd456e68be4ad0b09127ba9801359fd101
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="sendconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="17b32-103">Az MSFT_DSCLocalConfigurationManager osztály SendConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="17b32-103">SendConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="17b32-104">A konfigurációs dokumentum küld a felügyelt csomóponthoz, és menti a függőben lévő módosítása.</span><span class="sxs-lookup"><span data-stu-id="17b32-104">Sends the configuration document to the managed node and saves it as a pending change.</span></span>

<a name="syntax"></a><span data-ttu-id="17b32-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="17b32-105">Syntax</span></span>
------

```mof
uint32 SendConfiguration(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="17b32-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="17b32-106">Parameters</span></span>
----------

<span data-ttu-id="17b32-107">*ConfigurationData* \[a\] konfigurációjának a környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="17b32-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="17b32-108">*kényszerített* \[a\] **igaz** kényszerítése a konfigurációját, és állítsa le.</span><span class="sxs-lookup"><span data-stu-id="17b32-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="17b32-109">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="17b32-109">Return value</span></span>
------------

<span data-ttu-id="17b32-110">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="17b32-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="17b32-111">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="17b32-111">Remarks</span></span>

<span data-ttu-id="17b32-112">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="17b32-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="17b32-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="17b32-113">Requirements</span></span>
------------
><span data-ttu-id="17b32-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="17b32-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="17b32-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="17b32-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="17b32-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="17b32-116">See also</span></span>


[<span data-ttu-id="17b32-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="17b32-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)