---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály RollBack metódusa
ms.openlocfilehash: c0a801c4037921e700e447d1434e246df0a63a4f
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="rollback-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="81e3c-103">Az MSFT_DSCLocalConfigurationManager osztály RollBack metódusa</span><span class="sxs-lookup"><span data-stu-id="81e3c-103">RollBack method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="81e3c-104">Visszaállítja a konfigurációt egy korábbi verzióját.</span><span class="sxs-lookup"><span data-stu-id="81e3c-104">Rolls back the configuration to a previous version.</span></span>

<a name="syntax"></a><span data-ttu-id="81e3c-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="81e3c-105">Syntax</span></span>
------

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

<a name="parameters"></a><span data-ttu-id="81e3c-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="81e3c-106">Parameters</span></span>
----------

<span data-ttu-id="81e3c-107">*configurationNumber* \[a\] kért konfigurációját.</span><span class="sxs-lookup"><span data-stu-id="81e3c-107">*configurationNumber* \[in\] Specifies the requested configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="81e3c-108">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="81e3c-108">Return value</span></span>
------------

<span data-ttu-id="81e3c-109">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="81e3c-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="81e3c-110">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="81e3c-110">Remarks</span></span>

<span data-ttu-id="81e3c-111">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="81e3c-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="81e3c-112">Követelmények</span><span class="sxs-lookup"><span data-stu-id="81e3c-112">Requirements</span></span>
------------
><span data-ttu-id="81e3c-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="81e3c-113">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="81e3c-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="81e3c-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="81e3c-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="81e3c-115">See also</span></span>


[<span data-ttu-id="81e3c-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="81e3c-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)