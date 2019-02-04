---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApply metódusa
ms.openlocfilehash: da3a08307122ab38ee4a6fd5d4a9b97579a988f7
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685388"
---
# <a name="sendconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="3402f-103">Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApply metódusa</span><span class="sxs-lookup"><span data-stu-id="3402f-103">SendConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="3402f-104">A konfigurációs dokumentum a felügyelt csomópont küld, és a konfigurációs ügynök használja a alkalmazni a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="3402f-104">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="3402f-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="3402f-105">Syntax</span></span>

```mof
uint32 SendConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="3402f-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="3402f-106">Parameters</span></span>

<span data-ttu-id="3402f-107">*ConfigurationData* \[a\] konfigurációjának a környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="3402f-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="3402f-108">*kényszerített* \[a\] **igaz** kényszerített leállítása a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="3402f-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="3402f-109">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="3402f-109">Return value</span></span>

<span data-ttu-id="3402f-110">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="3402f-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="3402f-111">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="3402f-111">Remarks</span></span>

<span data-ttu-id="3402f-112">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="3402f-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="3402f-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="3402f-113">Requirements</span></span>

<span data-ttu-id="3402f-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="3402f-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="3402f-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="3402f-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="3402f-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="3402f-116">See also</span></span>

[<span data-ttu-id="3402f-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="3402f-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)