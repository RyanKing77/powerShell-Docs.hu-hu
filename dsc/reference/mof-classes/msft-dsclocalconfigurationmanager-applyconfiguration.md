---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: ApplyConfiguration metódusa
ms.openlocfilehash: 0425b9a7db37e421830ba37da8f5c0a4877a1b72
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727179"
---
# <a name="applyconfiguration-method"></a><span data-ttu-id="69427-103">ApplyConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="69427-103">ApplyConfiguration method</span></span>

<span data-ttu-id="69427-104">A konfigurációs ügynök használja a alkalmazni a konfigurációt, amely függőben van.</span><span class="sxs-lookup"><span data-stu-id="69427-104">Uses the Configuration Agent to apply the configuration that is pending.</span></span>

<span data-ttu-id="69427-105">Ha nem tartozik függőben lévő konfiguráció, ezt a módszert a jelenlegi konfiguráció újra alkalmazza.</span><span class="sxs-lookup"><span data-stu-id="69427-105">If there is no configuration pending, this method reapplies the current configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="69427-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="69427-106">Syntax</span></span>

```mof
uint32 ApplyConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="69427-107">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="69427-107">Parameters</span></span>

<span data-ttu-id="69427-108">*kényszerített* \[a\] -e az **igaz**, a jelenlegi konfiguráció vissza, akkor is, ha egy függőben lévő konfigurációs van.</span><span class="sxs-lookup"><span data-stu-id="69427-108">*force* \[in\] If this is **true**, the current configuration is reapplied, even if there is a configuration pending.</span></span>

## <a name="return-value"></a><span data-ttu-id="69427-109">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="69427-109">Return value</span></span>

<span data-ttu-id="69427-110">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="69427-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="69427-111">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="69427-111">Remarks</span></span>

<span data-ttu-id="69427-112">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="69427-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="69427-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="69427-113">Requirements</span></span>

<span data-ttu-id="69427-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="69427-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="69427-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="69427-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="69427-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="69427-116">See also</span></span>

[<span data-ttu-id="69427-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="69427-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
