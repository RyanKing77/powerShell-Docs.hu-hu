---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály StopConfiguration módszer"
ms.openlocfilehash: f0b550615b20f07f99c8ed7009805c45794bfe22
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="stopconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="8ca8d-103">A MSFT_DSCLocalConfigurationManager osztály StopConfiguration módszer</span><span class="sxs-lookup"><span data-stu-id="8ca8d-103">StopConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="8ca8d-104">Leállítja a folyamatban lévő konfigurációs módosítást.</span><span class="sxs-lookup"><span data-stu-id="8ca8d-104">Stops the configuration change that is in progress.</span></span>

<a name="syntax"></a><span data-ttu-id="8ca8d-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="8ca8d-105">Syntax</span></span>
------

```mof
uint32 StopConfiguration(
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="8ca8d-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="8ca8d-106">Parameters</span></span>
----------

<span data-ttu-id="8ca8d-107">*kényszerített* \[a\]</span><span class="sxs-lookup"><span data-stu-id="8ca8d-107">*force* \[in\]</span></span>  
<span data-ttu-id="8ca8d-108">**Igaz** kényszerítése a konfigurációját, és állítsa le.</span><span class="sxs-lookup"><span data-stu-id="8ca8d-108">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="8ca8d-109">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="8ca8d-109">Return value</span></span>
------------

<span data-ttu-id="8ca8d-110">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="8ca8d-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="8ca8d-111">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="8ca8d-111">Remarks</span></span>

<span data-ttu-id="8ca8d-112">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="8ca8d-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="8ca8d-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="8ca8d-113">Requirements</span></span>
------------
><span data-ttu-id="8ca8d-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="8ca8d-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="8ca8d-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="8ca8d-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="8ca8d-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="8ca8d-116">See also</span></span>


[<span data-ttu-id="8ca8d-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="8ca8d-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



