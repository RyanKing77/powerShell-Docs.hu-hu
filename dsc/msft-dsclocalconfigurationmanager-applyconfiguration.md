---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály ApplyConfiguration metódusa
ms.openlocfilehash: ef8488246b2c8614452d32009e45535f0ff2e184
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34222139"
---
# <a name="applyconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="baf1c-103">Az MSFT_DSCLocalConfigurationManager osztály ApplyConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="baf1c-103">ApplyConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="baf1c-104">A konfigurációs ügynök használja a beállítások, amelyek függőben van.</span><span class="sxs-lookup"><span data-stu-id="baf1c-104">Uses the Configuration Agent to apply the configuration that is pending.</span></span>

<span data-ttu-id="baf1c-105">Nincs függőben lévő konfiguráció, ha ez a módszer az aktuális konfigurációt újra alkalmazza.</span><span class="sxs-lookup"><span data-stu-id="baf1c-105">If there is no configuration pending, this method reapplies the current configuration.</span></span>


## <a name="syntax"></a><span data-ttu-id="baf1c-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="baf1c-106">Syntax</span></span>
------

```mof
uint32 ApplyConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="baf1c-107">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="baf1c-107">Parameters</span></span>
----------

<span data-ttu-id="baf1c-108">*kényszerített* \[a\] ebben **igaz**, a jelenlegi konfiguráció megváltoztatni, még akkor is, ha egy konfigurációjának kiszámítása függőben van.</span><span class="sxs-lookup"><span data-stu-id="baf1c-108">*force* \[in\] If this is **true**, the current configuration is reapplied, even if there is a configuration pending.</span></span>

## <a name="return-value"></a><span data-ttu-id="baf1c-109">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="baf1c-109">Return value</span></span>
------------

<span data-ttu-id="baf1c-110">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="baf1c-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="baf1c-111">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="baf1c-111">Remarks</span></span>

<span data-ttu-id="baf1c-112">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="baf1c-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="baf1c-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="baf1c-113">Requirements</span></span>
------------
><span data-ttu-id="baf1c-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="baf1c-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="baf1c-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="baf1c-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="baf1c-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="baf1c-116">See also</span></span>


[<span data-ttu-id="baf1c-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="baf1c-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)