---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: SendConfigurationApply method
ms.openlocfilehash: 11b9d435bbaac1600d25ff074b6c55b236a8378b
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727014"
---
# <a name="sendconfigurationapply-method"></a><span data-ttu-id="9a70d-103">SendConfigurationApply method</span><span class="sxs-lookup"><span data-stu-id="9a70d-103">SendConfigurationApply method</span></span>

<span data-ttu-id="9a70d-104">A konfigurációs dokumentum a felügyelt csomópont küld, és a konfigurációs ügynök használja a alkalmazni a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="9a70d-104">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="9a70d-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="9a70d-105">Syntax</span></span>

```mof
uint32 SendConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="9a70d-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="9a70d-106">Parameters</span></span>

<span data-ttu-id="9a70d-107">*ConfigurationData* \[a\] konfigurációjának a környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="9a70d-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="9a70d-108">*kényszerített* \[a\] **igaz** kényszerített leállítása a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="9a70d-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="9a70d-109">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="9a70d-109">Return value</span></span>

<span data-ttu-id="9a70d-110">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="9a70d-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="9a70d-111">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="9a70d-111">Remarks</span></span>

<span data-ttu-id="9a70d-112">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="9a70d-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="9a70d-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="9a70d-113">Requirements</span></span>

<span data-ttu-id="9a70d-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="9a70d-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="9a70d-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="9a70d-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="9a70d-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9a70d-116">See also</span></span>

[<span data-ttu-id="9a70d-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="9a70d-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
