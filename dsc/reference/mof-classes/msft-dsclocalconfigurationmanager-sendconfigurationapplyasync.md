---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: SendConfigurationApplyAsync metódusa
ms.openlocfilehash: c0e6dc9418757ee719e848fa8e7006dd73d91ad8
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67734305"
---
# <a name="sendconfigurationapplyasync-method"></a><span data-ttu-id="5fe74-103">SendConfigurationApplyAsync metódusa</span><span class="sxs-lookup"><span data-stu-id="5fe74-103">SendConfigurationApplyAsync method</span></span>

<span data-ttu-id="5fe74-104">A konfigurációs dokumentum aszinkron módon elküldi a felügyelt csomóponthoz, és a konfigurációs ügynök használja a alkalmazni a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="5fe74-104">Sends the configuration document asynchronously to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="5fe74-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="5fe74-105">Syntax</span></span>

```mof
uint32 SendConfigurationApplyAsync(
  [in] uint8   ConfigurationData[],
  [in] boolean force,
  [in] string  jobId
);
```

## <a name="parameters"></a><span data-ttu-id="5fe74-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="5fe74-106">Parameters</span></span>

<span data-ttu-id="5fe74-107">*ConfigurationData* \[a\] konfigurációjának a környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="5fe74-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="5fe74-108">*kényszerített* \[a\] **igaz** kényszerített leállítása a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="5fe74-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

<span data-ttu-id="5fe74-109">*jobId* \[a\] az azonosító a feladat, amelynek meg szeretné elküldeni a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="5fe74-109">*jobId* \[in\] The ID of the job for which to send the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="5fe74-110">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="5fe74-110">Return value</span></span>

<span data-ttu-id="5fe74-111">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="5fe74-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="5fe74-112">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="5fe74-112">Remarks</span></span>

<span data-ttu-id="5fe74-113">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="5fe74-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="5fe74-114">Követelmények</span><span class="sxs-lookup"><span data-stu-id="5fe74-114">Requirements</span></span>

<span data-ttu-id="5fe74-115">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="5fe74-115">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="5fe74-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="5fe74-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="5fe74-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5fe74-117">See also</span></span>

[<span data-ttu-id="5fe74-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="5fe74-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
