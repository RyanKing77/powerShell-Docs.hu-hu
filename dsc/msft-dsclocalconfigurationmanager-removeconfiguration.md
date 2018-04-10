---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály RemoveConfiguration metódusa
ms.openlocfilehash: e0ae8a50212b70841d210d7b2d666a2855218d1a
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="removeconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="14a33-103">Az MSFT_DSCLocalConfigurationManager osztály RemoveConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="14a33-103">RemoveConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="14a33-104">Eltávolítja a konfigurációs fájlok.</span><span class="sxs-lookup"><span data-stu-id="14a33-104">Removes the configuration files.</span></span>

<a name="syntax"></a><span data-ttu-id="14a33-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="14a33-105">Syntax</span></span>
------

```mof
uint32 RemoveConfiguration(
  [in] uint32  Stage,
  [in] boolean Force
);
```

<a name="parameters"></a><span data-ttu-id="14a33-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="14a33-106">Parameters</span></span>
----------

<span data-ttu-id="14a33-107">*Szakasz* \[a\] határozza meg, melyik konfigurációs dokumentum eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="14a33-107">*Stage* \[in\] Specifies which configuration document to remove.</span></span> <span data-ttu-id="14a33-108">A következő értékek érvényesek:</span><span class="sxs-lookup"><span data-stu-id="14a33-108">The following values are valid:</span></span>

|<span data-ttu-id="14a33-109">Érték</span><span class="sxs-lookup"><span data-stu-id="14a33-109">Value</span></span> |<span data-ttu-id="14a33-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="14a33-110">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="14a33-111">**1**</span><span class="sxs-lookup"><span data-stu-id="14a33-111">**1**</span></span> | <span data-ttu-id="14a33-112">A **aktuális** konfigurációs dokumentum (current.mof).</span><span class="sxs-lookup"><span data-stu-id="14a33-112">The **Current** configuration document (current.mof).</span></span> |
|<span data-ttu-id="14a33-113">**2**</span><span class="sxs-lookup"><span data-stu-id="14a33-113">**2**</span></span> | <span data-ttu-id="14a33-114">A **függőben lévő** konfigurációs dokumentum (pending.mof).</span><span class="sxs-lookup"><span data-stu-id="14a33-114">The **Pending** configuration document (pending.mof).</span></span>  |
|<span data-ttu-id="14a33-115">**4**</span><span class="sxs-lookup"><span data-stu-id="14a33-115">**4**</span></span> | <span data-ttu-id="14a33-116">A **előző** konfigurációs dokumentum (previous.mof).</span><span class="sxs-lookup"><span data-stu-id="14a33-116">The **Previous** configuration document (previous.mof).</span></span> |

<span data-ttu-id="14a33-117">*Kényszerített* \[a\] **igaz** a konfiguráció eltávolításának kényszerítése.</span><span class="sxs-lookup"><span data-stu-id="14a33-117">*Force* \[in\] **true** to force the removal of the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="14a33-118">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="14a33-118">Return value</span></span>
------------

<span data-ttu-id="14a33-119">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="14a33-119">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="14a33-120">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="14a33-120">Remarks</span></span>

<span data-ttu-id="14a33-121">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="14a33-121">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="14a33-122">Követelmények</span><span class="sxs-lookup"><span data-stu-id="14a33-122">Requirements</span></span>
------------
><span data-ttu-id="14a33-123">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="14a33-123">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="14a33-124">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="14a33-124">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="14a33-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="14a33-125">See also</span></span>


[<span data-ttu-id="14a33-126">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="14a33-126">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)