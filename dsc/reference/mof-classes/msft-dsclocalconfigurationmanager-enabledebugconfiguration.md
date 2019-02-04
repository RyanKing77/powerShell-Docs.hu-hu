---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály EnableDebugConfiguration metódusa
ms.openlocfilehash: b2eaebfa901cb5d93fd0183287073e6b31f975d1
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684807"
---
# <a name="enabledebugconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="1eae0-103">Az MSFT_DSCLocalConfigurationManager osztály EnableDebugConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="1eae0-103">EnableDebugConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="1eae0-104">Lehetővé teszi a DSC-erőforrás hibakeresés.</span><span class="sxs-lookup"><span data-stu-id="1eae0-104">Enables DSC resource debugging.</span></span>

## <a name="syntax"></a><span data-ttu-id="1eae0-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="1eae0-105">Syntax</span></span>

```mof
uint32 EnableDebugConfiguration(
  [in] boolean BreakAll
);
```

## <a name="parameters"></a><span data-ttu-id="1eae0-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="1eae0-106">Parameters</span></span>

<span data-ttu-id="1eae0-107">*BreakAll* \[a\] állítja be egy töréspontot minden sor az erőforrás-szkriptben.</span><span class="sxs-lookup"><span data-stu-id="1eae0-107">*BreakAll* \[in\] Sets a breakpoint at every line in the resource script.</span></span>

## <a name="return-value"></a><span data-ttu-id="1eae0-108">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="1eae0-108">Return value</span></span>

<span data-ttu-id="1eae0-109">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="1eae0-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="1eae0-110">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="1eae0-110">Remarks</span></span>

<span data-ttu-id="1eae0-111">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="1eae0-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="1eae0-112">Követelmények</span><span class="sxs-lookup"><span data-stu-id="1eae0-112">Requirements</span></span>

<span data-ttu-id="1eae0-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="1eae0-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="1eae0-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="1eae0-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="1eae0-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="1eae0-115">See also</span></span>

[<span data-ttu-id="1eae0-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="1eae0-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)