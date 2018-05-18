---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály EnableDebugConfiguration metódusa
ms.openlocfilehash: 9e2a978f9d16abaed959be022229db4da5fd65bd
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="enabledebugconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="12642-103">Az MSFT_DSCLocalConfigurationManager osztály EnableDebugConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="12642-103">EnableDebugConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="12642-104">A DSC-erőforrás hibakeresésének engedélyezése.</span><span class="sxs-lookup"><span data-stu-id="12642-104">Enables DSC resource debugging.</span></span>

<a name="syntax"></a><span data-ttu-id="12642-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="12642-105">Syntax</span></span>
------

```mof
uint32 EnableDebugConfiguration(
  [in] boolean BreakAll
);
```

<a name="parameters"></a><span data-ttu-id="12642-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="12642-106">Parameters</span></span>
----------

<span data-ttu-id="12642-107">*BreakAll* \[a\] töréspont beállítja az erőforrást parancsprogram minden sorában.</span><span class="sxs-lookup"><span data-stu-id="12642-107">*BreakAll* \[in\] Sets a breakpoint at every line in the resource script.</span></span>

## <a name="return-value"></a><span data-ttu-id="12642-108">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="12642-108">Return value</span></span>
------------

<span data-ttu-id="12642-109">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="12642-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="12642-110">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="12642-110">Remarks</span></span>

<span data-ttu-id="12642-111">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="12642-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="12642-112">Követelmények</span><span class="sxs-lookup"><span data-stu-id="12642-112">Requirements</span></span>
------------
><span data-ttu-id="12642-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="12642-113">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="12642-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="12642-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="12642-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="12642-115">See also</span></span>


[<span data-ttu-id="12642-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="12642-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)