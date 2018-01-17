---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály EnableDebugConfiguration módszer"
ms.openlocfilehash: fa34a583af7c3fd46d99307d582973410e4c0e31
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="enabledebugconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="0ba76-103">A MSFT_DSCLocalConfigurationManager osztály EnableDebugConfiguration módszer</span><span class="sxs-lookup"><span data-stu-id="0ba76-103">EnableDebugConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="0ba76-104">A DSC-erőforrás hibakeresésének engedélyezése.</span><span class="sxs-lookup"><span data-stu-id="0ba76-104">Enables DSC resource debugging.</span></span>

<a name="syntax"></a><span data-ttu-id="0ba76-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="0ba76-105">Syntax</span></span>
------

```mof
uint32 EnableDebugConfiguration(
  [in] boolean BreakAll
);
```

<a name="parameters"></a><span data-ttu-id="0ba76-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="0ba76-106">Parameters</span></span>
----------

<span data-ttu-id="0ba76-107">*BreakAll* \[in\]</span><span class="sxs-lookup"><span data-stu-id="0ba76-107">*BreakAll* \[in\]</span></span>  
<span data-ttu-id="0ba76-108">Beállítja a töréspont minden sor a erőforrás parancsfájlban.</span><span class="sxs-lookup"><span data-stu-id="0ba76-108">Sets a breakpoint at every line in the resource script.</span></span>

## <a name="return-value"></a><span data-ttu-id="0ba76-109">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="0ba76-109">Return value</span></span>
------------

<span data-ttu-id="0ba76-110">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="0ba76-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="0ba76-111">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="0ba76-111">Remarks</span></span>

<span data-ttu-id="0ba76-112">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="0ba76-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="0ba76-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="0ba76-113">Requirements</span></span>
------------
><span data-ttu-id="0ba76-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="0ba76-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="0ba76-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="0ba76-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="0ba76-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0ba76-116">See also</span></span>


[<span data-ttu-id="0ba76-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="0ba76-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
 

 



