---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: StopConfiguration metódusa
ms.openlocfilehash: e1de175032a3bddf11af218bc4a15bdbe554a9d5
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726986"
---
# <a name="stopconfiguration-method"></a><span data-ttu-id="44269-103">StopConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="44269-103">StopConfiguration method</span></span>

<span data-ttu-id="44269-104">Leállítja a módosítás folyamatban van.</span><span class="sxs-lookup"><span data-stu-id="44269-104">Stops the configuration change that is in progress.</span></span>

## <a name="syntax"></a><span data-ttu-id="44269-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="44269-105">Syntax</span></span>

```mof
uint32 StopConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="44269-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="44269-106">Parameters</span></span>

<span data-ttu-id="44269-107">*kényszerített* \[a\] **igaz** kényszerített leállítása a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="44269-107">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="44269-108">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="44269-108">Return value</span></span>

<span data-ttu-id="44269-109">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="44269-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="44269-110">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="44269-110">Remarks</span></span>

<span data-ttu-id="44269-111">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="44269-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="44269-112">Követelmények</span><span class="sxs-lookup"><span data-stu-id="44269-112">Requirements</span></span>

<span data-ttu-id="44269-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="44269-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="44269-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="44269-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="44269-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="44269-115">See also</span></span>

[<span data-ttu-id="44269-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="44269-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
