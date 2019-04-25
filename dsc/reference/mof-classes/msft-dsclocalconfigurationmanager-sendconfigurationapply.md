---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApply metódusa
ms.openlocfilehash: da3a08307122ab38ee4a6fd5d4a9b97579a988f7
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62078260"
---
# <a name="sendconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="23dc5-103">Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApply metódusa</span><span class="sxs-lookup"><span data-stu-id="23dc5-103">SendConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="23dc5-104">A konfigurációs dokumentum a felügyelt csomópont küld, és a konfigurációs ügynök használja a alkalmazni a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="23dc5-104">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="23dc5-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="23dc5-105">Syntax</span></span>

```mof
uint32 SendConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="23dc5-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="23dc5-106">Parameters</span></span>

<span data-ttu-id="23dc5-107">*ConfigurationData* \[a\] konfigurációjának a környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="23dc5-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="23dc5-108">*kényszerített* \[a\] **igaz** kényszerített leállítása a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="23dc5-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="23dc5-109">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="23dc5-109">Return value</span></span>

<span data-ttu-id="23dc5-110">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="23dc5-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="23dc5-111">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="23dc5-111">Remarks</span></span>

<span data-ttu-id="23dc5-112">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="23dc5-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="23dc5-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="23dc5-113">Requirements</span></span>

<span data-ttu-id="23dc5-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="23dc5-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="23dc5-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="23dc5-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="23dc5-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="23dc5-116">See also</span></span>

[<span data-ttu-id="23dc5-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="23dc5-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)