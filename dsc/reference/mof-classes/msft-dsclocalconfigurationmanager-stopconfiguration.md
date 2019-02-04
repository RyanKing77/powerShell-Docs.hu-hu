---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály StopConfiguration metódusa
ms.openlocfilehash: 1cd887d205967c3d282143df4e6199027639230e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687754"
---
# <a name="stopconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="56160-103">Az MSFT_DSCLocalConfigurationManager osztály StopConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="56160-103">StopConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="56160-104">Leállítja a módosítás folyamatban van.</span><span class="sxs-lookup"><span data-stu-id="56160-104">Stops the configuration change that is in progress.</span></span>

## <a name="syntax"></a><span data-ttu-id="56160-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="56160-105">Syntax</span></span>

```mof
uint32 StopConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="56160-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="56160-106">Parameters</span></span>

<span data-ttu-id="56160-107">*kényszerített* \[a\] **igaz** kényszerített leállítása a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="56160-107">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="56160-108">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="56160-108">Return value</span></span>

<span data-ttu-id="56160-109">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="56160-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="56160-110">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="56160-110">Remarks</span></span>

<span data-ttu-id="56160-111">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="56160-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="56160-112">Követelmények</span><span class="sxs-lookup"><span data-stu-id="56160-112">Requirements</span></span>

<span data-ttu-id="56160-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="56160-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="56160-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="56160-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="56160-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="56160-115">See also</span></span>

[<span data-ttu-id="56160-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="56160-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)