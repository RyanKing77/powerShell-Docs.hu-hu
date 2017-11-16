---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály TestConfiguration módszer"
ms.openlocfilehash: 8e9986837aaf41b1396a2399c58675bc51b0b708
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="testconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="ebf2b-103">A MSFT_DSCLocalConfigurationManager osztály TestConfiguration módszer</span><span class="sxs-lookup"><span data-stu-id="ebf2b-103">TestConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="ebf2b-104">A konfigurációs dokumentum küld a felügyelt csomóponthoz, és a jelenlegi konfiguráció alapján a dokumentum ellenőrzi.</span><span class="sxs-lookup"><span data-stu-id="ebf2b-104">Sends the configuration document to the managed node and verifies the current configuration against the document.</span></span>

<a name="syntax"></a><span data-ttu-id="ebf2b-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="ebf2b-105">Syntax</span></span>
------

```mof
uint32 TestConfiguration(
  [in]  uint8                          configurationData[],
  [out] boolean                        InDesiredState,
  [out] MSFT_ResourceInDesiredState    ResourcesInDesiredState[],
  [out] MSFT_ResourceNotInDesiredState ResourcesNotInDesiredState[]
);
```

<a name="parameters"></a><span data-ttu-id="ebf2b-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="ebf2b-106">Parameters</span></span>
----------

<span data-ttu-id="ebf2b-107">*configurationData* \[a\]</span><span class="sxs-lookup"><span data-stu-id="ebf2b-107">*configurationData* \[in\]</span></span>  
<span data-ttu-id="ebf2b-108">A confuguration környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="ebf2b-108">Environment data for the confuguration.</span></span>

<span data-ttu-id="ebf2b-109">*InDesiredState* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="ebf2b-109">*InDesiredState* \[out\]</span></span>  
<span data-ttu-id="ebf2b-110">A visszatérési határozza meg, hogy a felügyelt csomóponthoz a konfigurációs dokumentum által meghatározott állapotban.</span><span class="sxs-lookup"><span data-stu-id="ebf2b-110">On return, specifies whether the managed node is in the state specified by the configuration document.</span></span>

<span data-ttu-id="ebf2b-111">*ResourcesInDesiredState* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="ebf2b-111">*ResourcesInDesiredState* \[out\]</span></span>  
<span data-ttu-id="ebf2b-112">A visszatérési, tartalmazza a beágyazott példányának a **MSFT_ResourceInDesiredState** osztály, amely meghatározza a kívánt állapot-erőforrást.</span><span class="sxs-lookup"><span data-stu-id="ebf2b-112">On return, contains an embedded instance of the **MSFT_ResourceInDesiredState** class that specifies resources that are in the desired state.</span></span>

<span data-ttu-id="ebf2b-113">*ResourcesNotInDesiredState* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="ebf2b-113">*ResourcesNotInDesiredState* \[out\]</span></span>  
<span data-ttu-id="ebf2b-114">A visszatérési, tartalmazza a beágyazott példányának a **MSFT_ResourceNotInDesiredState** osztály, amely meghatározza az erőforrásokat, amelyek nem a megfelelő állapotban van.</span><span class="sxs-lookup"><span data-stu-id="ebf2b-114">On return, contains an embedded instance of the **MSFT_ResourceNotInDesiredState** class that specifies resources that are not in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="ebf2b-115">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="ebf2b-115">Return value</span></span>
------------

<span data-ttu-id="ebf2b-116">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="ebf2b-116">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="ebf2b-117">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="ebf2b-117">Remarks</span></span>

<span data-ttu-id="ebf2b-118">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="ebf2b-118">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="ebf2b-119">Követelmények</span><span class="sxs-lookup"><span data-stu-id="ebf2b-119">Requirements</span></span>
------------
><span data-ttu-id="ebf2b-120">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="ebf2b-120">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="ebf2b-121">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="ebf2b-121">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="ebf2b-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ebf2b-122">See also</span></span>


[<span data-ttu-id="ebf2b-123">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="ebf2b-123">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



