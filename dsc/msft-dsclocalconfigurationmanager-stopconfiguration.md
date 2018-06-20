---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály StopConfiguration metódusa
ms.openlocfilehash: aaed29cb81e2079c4673b621b81c52e109aa7b48
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34218875"
---
# <a name="stopconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="c790d-103">Az MSFT_DSCLocalConfigurationManager osztály StopConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="c790d-103">StopConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="c790d-104">Leállítja a folyamatban lévő konfigurációs módosítást.</span><span class="sxs-lookup"><span data-stu-id="c790d-104">Stops the configuration change that is in progress.</span></span>

<a name="syntax"></a><span data-ttu-id="c790d-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="c790d-105">Syntax</span></span>
------

```mof
uint32 StopConfiguration(
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="c790d-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="c790d-106">Parameters</span></span>
----------

<span data-ttu-id="c790d-107">*kényszerített* \[a\] **igaz** kényszerítése a konfigurációját, és állítsa le.</span><span class="sxs-lookup"><span data-stu-id="c790d-107">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="c790d-108">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="c790d-108">Return value</span></span>
------------

<span data-ttu-id="c790d-109">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="c790d-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="c790d-110">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="c790d-110">Remarks</span></span>

<span data-ttu-id="c790d-111">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="c790d-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="c790d-112">Követelmények</span><span class="sxs-lookup"><span data-stu-id="c790d-112">Requirements</span></span>
------------
><span data-ttu-id="c790d-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="c790d-113">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="c790d-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="c790d-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="c790d-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c790d-115">See also</span></span>


[<span data-ttu-id="c790d-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="c790d-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)