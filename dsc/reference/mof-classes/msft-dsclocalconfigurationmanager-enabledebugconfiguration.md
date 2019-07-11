---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: EnableDebugConfiguration metódusa
ms.openlocfilehash: f1290e4d898332361850ffc85aa0a8d79863c8f7
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727146"
---
# <a name="enabledebugconfiguration-method"></a><span data-ttu-id="dacf3-103">EnableDebugConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="dacf3-103">EnableDebugConfiguration method</span></span>

<span data-ttu-id="dacf3-104">Lehetővé teszi a DSC-erőforrás hibakeresés.</span><span class="sxs-lookup"><span data-stu-id="dacf3-104">Enables DSC resource debugging.</span></span>

## <a name="syntax"></a><span data-ttu-id="dacf3-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="dacf3-105">Syntax</span></span>

```mof
uint32 EnableDebugConfiguration(
  [in] boolean BreakAll
);
```

## <a name="parameters"></a><span data-ttu-id="dacf3-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="dacf3-106">Parameters</span></span>

<span data-ttu-id="dacf3-107">*BreakAll* \[a\] állítja be egy töréspontot minden sor az erőforrás-szkriptben.</span><span class="sxs-lookup"><span data-stu-id="dacf3-107">*BreakAll* \[in\] Sets a breakpoint at every line in the resource script.</span></span>

## <a name="return-value"></a><span data-ttu-id="dacf3-108">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="dacf3-108">Return value</span></span>

<span data-ttu-id="dacf3-109">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="dacf3-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="dacf3-110">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="dacf3-110">Remarks</span></span>

<span data-ttu-id="dacf3-111">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="dacf3-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="dacf3-112">Követelmények</span><span class="sxs-lookup"><span data-stu-id="dacf3-112">Requirements</span></span>

<span data-ttu-id="dacf3-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="dacf3-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="dacf3-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="dacf3-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="dacf3-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="dacf3-115">See also</span></span>

[<span data-ttu-id="dacf3-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="dacf3-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
