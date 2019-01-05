---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApplyAsync metódusa
ms.openlocfilehash: b028079cf826719967858f50e357b441ba8f9d79
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048453"
---
# <a name="sendconfigurationapplyasync-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="b1d7c-103">Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApplyAsync metódusa</span><span class="sxs-lookup"><span data-stu-id="b1d7c-103">SendConfigurationApplyAsync method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="b1d7c-104">A konfigurációs dokumentum aszinkron módon elküldi a felügyelt csomóponthoz, és a konfigurációs ügynök használja a alkalmazni a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="b1d7c-104">Sends the configuration document asynchronously to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="b1d7c-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="b1d7c-105">Syntax</span></span>

```mof
uint32 SendConfigurationApplyAsync(
  [in] uint8   ConfigurationData[],
  [in] boolean force,
  [in] string  jobId
);
```

## <a name="parameters"></a><span data-ttu-id="b1d7c-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="b1d7c-106">Parameters</span></span>

<span data-ttu-id="b1d7c-107">*ConfigurationData* \[a\] konfigurációjának a környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="b1d7c-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="b1d7c-108">*kényszerített* \[a\] **igaz** kényszerített leállítása a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="b1d7c-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

<span data-ttu-id="b1d7c-109">*jobId* \[a\] az azonosító a feladat, amelynek meg szeretné elküldeni a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="b1d7c-109">*jobId* \[in\] The ID of the job for which to send the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="b1d7c-110">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="b1d7c-110">Return value</span></span>

<span data-ttu-id="b1d7c-111">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="b1d7c-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="b1d7c-112">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="b1d7c-112">Remarks</span></span>

<span data-ttu-id="b1d7c-113">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="b1d7c-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="b1d7c-114">Követelmények</span><span class="sxs-lookup"><span data-stu-id="b1d7c-114">Requirements</span></span>

<span data-ttu-id="b1d7c-115">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="b1d7c-115">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="b1d7c-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="b1d7c-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="b1d7c-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b1d7c-117">See also</span></span>

[<span data-ttu-id="b1d7c-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="b1d7c-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)