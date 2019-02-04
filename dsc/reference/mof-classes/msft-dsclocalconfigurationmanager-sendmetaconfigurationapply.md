---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály SendMetaConfigurationApply metódusa
ms.openlocfilehash: b372a6c0ab9d4561dcf67026275e7d3ca6aa2584
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688069"
---
# <a name="sendmetaconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="118a9-103">Az MSFT_DSCLocalConfigurationManager osztály SendMetaConfigurationApply metódusa</span><span class="sxs-lookup"><span data-stu-id="118a9-103">SendMetaConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="118a9-104">Beállítja a helyi Configuration Manager beállításokat, hogy a konfigurációs ügynök szabályozására szolgálnak.</span><span class="sxs-lookup"><span data-stu-id="118a9-104">Sets the Local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

## <a name="syntax"></a><span data-ttu-id="118a9-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="118a9-105">Syntax</span></span>

```mof
uint32 SendMetaConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="118a9-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="118a9-106">Parameters</span></span>

<span data-ttu-id="118a9-107">*ConfigurationData* \[a\] konfigurációjának a környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="118a9-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="118a9-108">*kényszerített* \[a\] **igaz** kényszerített leállítása a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="118a9-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="118a9-109">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="118a9-109">Return value</span></span>

<span data-ttu-id="118a9-110">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="118a9-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="118a9-111">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="118a9-111">Remarks</span></span>

<span data-ttu-id="118a9-112">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="118a9-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="118a9-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="118a9-113">Requirements</span></span>

<span data-ttu-id="118a9-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="118a9-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="118a9-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="118a9-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="118a9-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="118a9-116">See also</span></span>

[<span data-ttu-id="118a9-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="118a9-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)