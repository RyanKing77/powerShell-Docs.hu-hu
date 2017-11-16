---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "ApplyConfiguration metódust a MSFT_DSCLocalConfigurationManager osztály"
ms.openlocfilehash: febaf972a2a452eb9aaf3ec7fbc5e41f3f463a58
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="applyconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="07699-103">ApplyConfiguration metódust a MSFT_DSCLocalConfigurationManager osztály</span><span class="sxs-lookup"><span data-stu-id="07699-103">ApplyConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="07699-104">A konfigurációs ügynök használja a beállítások, amelyek függőben van.</span><span class="sxs-lookup"><span data-stu-id="07699-104">Uses the Configuration Agent to apply the configuration that is pending.</span></span> 

<span data-ttu-id="07699-105">Nincs függőben lévő konfiguráció, ha ez a módszer az aktuális konfigurációt újra alkalmazza.</span><span class="sxs-lookup"><span data-stu-id="07699-105">If there is no configuration pending, this method reapplies the current configuration.</span></span>


## <a name="syntax"></a><span data-ttu-id="07699-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="07699-106">Syntax</span></span>
------

```mof
uint32 ApplyConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="07699-107">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="07699-107">Parameters</span></span>
----------

<span data-ttu-id="07699-108">*kényszerített* \[a\]</span><span class="sxs-lookup"><span data-stu-id="07699-108">*force* \[in\]</span></span>  
<span data-ttu-id="07699-109">Ha ez **igaz**, a jelenlegi konfiguráció megváltoztatni, még akkor is, ha egy konfigurációjának kiszámítása függőben van.</span><span class="sxs-lookup"><span data-stu-id="07699-109">If this is **true**, the current configuration is reapplied, even if there is a configuration pending.</span></span>

## <a name="return-value"></a><span data-ttu-id="07699-110">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="07699-110">Return value</span></span>
------------

<span data-ttu-id="07699-111">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="07699-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="07699-112">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="07699-112">Remarks</span></span>

<span data-ttu-id="07699-113">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="07699-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="07699-114">Követelmények</span><span class="sxs-lookup"><span data-stu-id="07699-114">Requirements</span></span>
------------
><span data-ttu-id="07699-115">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="07699-115">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="07699-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="07699-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="07699-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="07699-117">See also</span></span>


[<span data-ttu-id="07699-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="07699-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)

 

 



