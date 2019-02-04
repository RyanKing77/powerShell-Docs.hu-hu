---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály ApplyConfiguration metódusa
ms.openlocfilehash: 559ff1793a18e28dad2f176bdb20eb53bc08630d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55683911"
---
# <a name="applyconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="43078-103">Az MSFT_DSCLocalConfigurationManager osztály ApplyConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="43078-103">ApplyConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="43078-104">A konfigurációs ügynök használja a alkalmazni a konfigurációt, amely függőben van.</span><span class="sxs-lookup"><span data-stu-id="43078-104">Uses the Configuration Agent to apply the configuration that is pending.</span></span>

<span data-ttu-id="43078-105">Ha nem tartozik függőben lévő konfiguráció, ezt a módszert a jelenlegi konfiguráció újra alkalmazza.</span><span class="sxs-lookup"><span data-stu-id="43078-105">If there is no configuration pending, this method reapplies the current configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="43078-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="43078-106">Syntax</span></span>

```mof
uint32 ApplyConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="43078-107">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="43078-107">Parameters</span></span>

<span data-ttu-id="43078-108">*kényszerített* \[a\] -e az **igaz**, a jelenlegi konfiguráció vissza, akkor is, ha egy függőben lévő konfigurációs van.</span><span class="sxs-lookup"><span data-stu-id="43078-108">*force* \[in\] If this is **true**, the current configuration is reapplied, even if there is a configuration pending.</span></span>

## <a name="return-value"></a><span data-ttu-id="43078-109">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="43078-109">Return value</span></span>

<span data-ttu-id="43078-110">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="43078-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="43078-111">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="43078-111">Remarks</span></span>

<span data-ttu-id="43078-112">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="43078-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="43078-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="43078-113">Requirements</span></span>

<span data-ttu-id="43078-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="43078-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="43078-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="43078-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="43078-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="43078-116">See also</span></span>

[<span data-ttu-id="43078-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="43078-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)