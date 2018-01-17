---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály SendMetaConfigurationApply módszer"
ms.openlocfilehash: 350555220757b1939b1de34ab423e963635eb53c
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="sendmetaconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="e957c-103">A MSFT_DSCLocalConfigurationManager osztály SendMetaConfigurationApply módszer</span><span class="sxs-lookup"><span data-stu-id="e957c-103">SendMetaConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="e957c-104">Beállítja a helyi Configuration Manager beállítások konfigurációs ügynök használt.</span><span class="sxs-lookup"><span data-stu-id="e957c-104">Sets the Local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

<a name="syntax"></a><span data-ttu-id="e957c-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="e957c-105">Syntax</span></span>
------

```mof
uint32 SendMetaConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="e957c-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="e957c-106">Parameters</span></span>
----------

<span data-ttu-id="e957c-107">*ConfigurationData* \[a\]</span><span class="sxs-lookup"><span data-stu-id="e957c-107">*ConfigurationData* \[in\]</span></span>  
<span data-ttu-id="e957c-108">A környezet konfigurációjának adatait.</span><span class="sxs-lookup"><span data-stu-id="e957c-108">The environment data for the configuration.</span></span>

<span data-ttu-id="e957c-109">*kényszerített* \[a\]</span><span class="sxs-lookup"><span data-stu-id="e957c-109">*force* \[in\]</span></span>  
<span data-ttu-id="e957c-110">**Igaz** kényszerítése a konfigurációját, és állítsa le.</span><span class="sxs-lookup"><span data-stu-id="e957c-110">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="e957c-111">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="e957c-111">Return value</span></span>
------------

<span data-ttu-id="e957c-112">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="e957c-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="e957c-113">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="e957c-113">Remarks</span></span>

<span data-ttu-id="e957c-114">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="e957c-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="e957c-115">Követelmények</span><span class="sxs-lookup"><span data-stu-id="e957c-115">Requirements</span></span>
------------
><span data-ttu-id="e957c-116">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="e957c-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="e957c-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="e957c-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="e957c-118">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e957c-118">See also</span></span>


[<span data-ttu-id="e957c-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="e957c-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



