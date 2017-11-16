---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály SendConfigurationApply módszer"
ms.openlocfilehash: 9552fd5b5feb862fbe8ef95a7746776e7fe2f5c8
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="sendconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="f8041-103">A MSFT_DSCLocalConfigurationManager osztály SendConfigurationApply módszer</span><span class="sxs-lookup"><span data-stu-id="f8041-103">SendConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="f8041-104">A konfigurációs dokumentum küld a felügyelt csomóponthoz, és a konfigurációs ügynök segítségével a konfiguráció alkalmazásához.</span><span class="sxs-lookup"><span data-stu-id="f8041-104">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="f8041-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="f8041-105">Syntax</span></span>
------

```mof
uint32 SendConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="f8041-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="f8041-106">Parameters</span></span>
----------

<span data-ttu-id="f8041-107">*ConfigurationData* \[a\]</span><span class="sxs-lookup"><span data-stu-id="f8041-107">*ConfigurationData* \[in\]</span></span>  
<span data-ttu-id="f8041-108">A környezet konfigurációjának adatait.</span><span class="sxs-lookup"><span data-stu-id="f8041-108">The environment data for the configuration.</span></span>

<span data-ttu-id="f8041-109">*kényszerített* \[a\]</span><span class="sxs-lookup"><span data-stu-id="f8041-109">*force* \[in\]</span></span>  
<span data-ttu-id="f8041-110">**Igaz** kényszerítése a konfigurációját, és állítsa le.</span><span class="sxs-lookup"><span data-stu-id="f8041-110">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="f8041-111">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="f8041-111">Return value</span></span>
------------

<span data-ttu-id="f8041-112">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="f8041-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="f8041-113">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="f8041-113">Remarks</span></span>

<span data-ttu-id="f8041-114">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="f8041-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="f8041-115">Követelmények</span><span class="sxs-lookup"><span data-stu-id="f8041-115">Requirements</span></span>
------------
><span data-ttu-id="f8041-116">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="f8041-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="f8041-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="f8041-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="f8041-118">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="f8041-118">See also</span></span>


[<span data-ttu-id="f8041-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="f8041-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



