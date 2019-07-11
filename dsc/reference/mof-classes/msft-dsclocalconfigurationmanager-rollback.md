---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: RollBack metódusa
ms.openlocfilehash: 6452bdffd5160d9956576fb59c98e2f9ff7ddbbb
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727026"
---
# <a name="rollback-method"></a><span data-ttu-id="fc30f-103">RollBack metódusa</span><span class="sxs-lookup"><span data-stu-id="fc30f-103">RollBack method</span></span>

<span data-ttu-id="fc30f-104">Visszaállítja a konfigurációt egy korábbi verzióra.</span><span class="sxs-lookup"><span data-stu-id="fc30f-104">Rolls back the configuration to a previous version.</span></span>

## <a name="syntax"></a><span data-ttu-id="fc30f-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="fc30f-105">Syntax</span></span>

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

## <a name="parameters"></a><span data-ttu-id="fc30f-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="fc30f-106">Parameters</span></span>

<span data-ttu-id="fc30f-107">*configurationNumber* \[a\] adja meg a kért konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="fc30f-107">*configurationNumber* \[in\] Specifies the requested configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="fc30f-108">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="fc30f-108">Return value</span></span>

<span data-ttu-id="fc30f-109">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="fc30f-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="fc30f-110">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="fc30f-110">Remarks</span></span>

<span data-ttu-id="fc30f-111">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="fc30f-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="fc30f-112">Követelmények</span><span class="sxs-lookup"><span data-stu-id="fc30f-112">Requirements</span></span>

<span data-ttu-id="fc30f-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="fc30f-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="fc30f-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="fc30f-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="fc30f-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="fc30f-115">See also</span></span>

[<span data-ttu-id="fc30f-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="fc30f-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
