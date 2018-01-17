---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály StopConfiguration módszer"
ms.openlocfilehash: 66d00cb40750e91e4b369a2e8cebb449697406d9
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="stopconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="d3a97-103">A MSFT_DSCLocalConfigurationManager osztály StopConfiguration módszer</span><span class="sxs-lookup"><span data-stu-id="d3a97-103">StopConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="d3a97-104">Leállítja a folyamatban lévő konfigurációs módosítást.</span><span class="sxs-lookup"><span data-stu-id="d3a97-104">Stops the configuration change that is in progress.</span></span>

<a name="syntax"></a><span data-ttu-id="d3a97-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="d3a97-105">Syntax</span></span>
------

```mof
uint32 StopConfiguration(
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="d3a97-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="d3a97-106">Parameters</span></span>
----------

<span data-ttu-id="d3a97-107">*kényszerített* \[a\]</span><span class="sxs-lookup"><span data-stu-id="d3a97-107">*force* \[in\]</span></span>  
<span data-ttu-id="d3a97-108">**Igaz** kényszerítése a konfigurációját, és állítsa le.</span><span class="sxs-lookup"><span data-stu-id="d3a97-108">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="d3a97-109">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="d3a97-109">Return value</span></span>
------------

<span data-ttu-id="d3a97-110">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="d3a97-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="d3a97-111">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="d3a97-111">Remarks</span></span>

<span data-ttu-id="d3a97-112">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="d3a97-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="d3a97-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="d3a97-113">Requirements</span></span>
------------
><span data-ttu-id="d3a97-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="d3a97-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="d3a97-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="d3a97-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="d3a97-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d3a97-116">See also</span></span>


[<span data-ttu-id="d3a97-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="d3a97-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



