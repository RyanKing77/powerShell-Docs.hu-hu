---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály EnableDebugConfiguration metódusa
ms.openlocfilehash: 9fe41fa806a6abff1d36dadd0c041a5cf0e78caf
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="enabledebugconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="057bf-103">Az MSFT_DSCLocalConfigurationManager osztály EnableDebugConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="057bf-103">EnableDebugConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="057bf-104">A DSC-erőforrás hibakeresésének engedélyezése.</span><span class="sxs-lookup"><span data-stu-id="057bf-104">Enables DSC resource debugging.</span></span>

<a name="syntax"></a><span data-ttu-id="057bf-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="057bf-105">Syntax</span></span>
------

```mof
uint32 EnableDebugConfiguration(
  [in] boolean BreakAll
);
```

<a name="parameters"></a><span data-ttu-id="057bf-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="057bf-106">Parameters</span></span>
----------

<span data-ttu-id="057bf-107">*BreakAll* \[a\] töréspont beállítja az erőforrást parancsprogram minden sorában.</span><span class="sxs-lookup"><span data-stu-id="057bf-107">*BreakAll* \[in\] Sets a breakpoint at every line in the resource script.</span></span>

## <a name="return-value"></a><span data-ttu-id="057bf-108">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="057bf-108">Return value</span></span>
------------

<span data-ttu-id="057bf-109">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="057bf-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="057bf-110">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="057bf-110">Remarks</span></span>

<span data-ttu-id="057bf-111">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="057bf-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="057bf-112">Követelmények</span><span class="sxs-lookup"><span data-stu-id="057bf-112">Requirements</span></span>
------------
><span data-ttu-id="057bf-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="057bf-113">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="057bf-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="057bf-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="057bf-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="057bf-115">See also</span></span>


[<span data-ttu-id="057bf-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="057bf-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)