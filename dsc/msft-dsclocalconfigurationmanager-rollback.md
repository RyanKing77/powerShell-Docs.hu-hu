---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály RollBack metódusa
ms.openlocfilehash: d2f9b7025d611912e119800408e25fcb66bc0228
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219878"
---
# <a name="rollback-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="1b786-103">Az MSFT_DSCLocalConfigurationManager osztály RollBack metódusa</span><span class="sxs-lookup"><span data-stu-id="1b786-103">RollBack method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="1b786-104">Visszaállítja a konfigurációt egy korábbi verzióját.</span><span class="sxs-lookup"><span data-stu-id="1b786-104">Rolls back the configuration to a previous version.</span></span>

<a name="syntax"></a><span data-ttu-id="1b786-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="1b786-105">Syntax</span></span>
------

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

<a name="parameters"></a><span data-ttu-id="1b786-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="1b786-106">Parameters</span></span>
----------

<span data-ttu-id="1b786-107">*configurationNumber* \[a\] kért konfigurációját.</span><span class="sxs-lookup"><span data-stu-id="1b786-107">*configurationNumber* \[in\] Specifies the requested configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="1b786-108">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="1b786-108">Return value</span></span>
------------

<span data-ttu-id="1b786-109">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="1b786-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="1b786-110">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="1b786-110">Remarks</span></span>

<span data-ttu-id="1b786-111">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="1b786-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="1b786-112">Követelmények</span><span class="sxs-lookup"><span data-stu-id="1b786-112">Requirements</span></span>
------------
><span data-ttu-id="1b786-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="1b786-113">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="1b786-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="1b786-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="1b786-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="1b786-115">See also</span></span>


[<span data-ttu-id="1b786-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="1b786-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)