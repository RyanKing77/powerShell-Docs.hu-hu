---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: SendMetaConfigurationApply method
ms.openlocfilehash: b2e420bafb8ea22aea43800f6e429d3ed785d1e8
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727046"
---
# <a name="sendmetaconfigurationapply-method"></a><span data-ttu-id="2a5bc-103">SendMetaConfigurationApply method</span><span class="sxs-lookup"><span data-stu-id="2a5bc-103">SendMetaConfigurationApply method</span></span>

<span data-ttu-id="2a5bc-104">Beállítja a helyi Configuration Manager beállításokat, hogy a konfigurációs ügynök szabályozására szolgálnak.</span><span class="sxs-lookup"><span data-stu-id="2a5bc-104">Sets the Local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

## <a name="syntax"></a><span data-ttu-id="2a5bc-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="2a5bc-105">Syntax</span></span>

```mof
uint32 SendMetaConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="2a5bc-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="2a5bc-106">Parameters</span></span>

<span data-ttu-id="2a5bc-107">*ConfigurationData* \[a\] konfigurációjának a környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="2a5bc-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="2a5bc-108">*kényszerített* \[a\] **igaz** kényszerített leállítása a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="2a5bc-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="2a5bc-109">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="2a5bc-109">Return value</span></span>

<span data-ttu-id="2a5bc-110">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="2a5bc-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="2a5bc-111">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="2a5bc-111">Remarks</span></span>

<span data-ttu-id="2a5bc-112">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="2a5bc-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="2a5bc-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="2a5bc-113">Requirements</span></span>

<span data-ttu-id="2a5bc-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="2a5bc-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="2a5bc-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="2a5bc-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="2a5bc-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2a5bc-116">See also</span></span>

[<span data-ttu-id="2a5bc-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="2a5bc-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
