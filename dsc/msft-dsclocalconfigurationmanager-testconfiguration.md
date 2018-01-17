---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály TestConfiguration módszer"
ms.openlocfilehash: 04f0f3146473dc71f492086449d9dce5467c55db
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="testconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="08cca-103">A MSFT_DSCLocalConfigurationManager osztály TestConfiguration módszer</span><span class="sxs-lookup"><span data-stu-id="08cca-103">TestConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="08cca-104">A konfigurációs dokumentum küld a felügyelt csomóponthoz, és a jelenlegi konfiguráció alapján a dokumentum ellenőrzi.</span><span class="sxs-lookup"><span data-stu-id="08cca-104">Sends the configuration document to the managed node and verifies the current configuration against the document.</span></span>

<a name="syntax"></a><span data-ttu-id="08cca-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="08cca-105">Syntax</span></span>
------

```mof
uint32 TestConfiguration(
  [in]  uint8                          configurationData[],
  [out] boolean                        InDesiredState,
  [out] MSFT_ResourceInDesiredState    ResourcesInDesiredState[],
  [out] MSFT_ResourceNotInDesiredState ResourcesNotInDesiredState[]
);
```

<a name="parameters"></a><span data-ttu-id="08cca-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="08cca-106">Parameters</span></span>
----------

<span data-ttu-id="08cca-107">*configurationData* \[a\]</span><span class="sxs-lookup"><span data-stu-id="08cca-107">*configurationData* \[in\]</span></span>  
<span data-ttu-id="08cca-108">A confuguration környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="08cca-108">Environment data for the confuguration.</span></span>

<span data-ttu-id="08cca-109">*InDesiredState* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="08cca-109">*InDesiredState* \[out\]</span></span>  
<span data-ttu-id="08cca-110">A visszatérési határozza meg, hogy a felügyelt csomóponthoz a konfigurációs dokumentum által meghatározott állapotban.</span><span class="sxs-lookup"><span data-stu-id="08cca-110">On return, specifies whether the managed node is in the state specified by the configuration document.</span></span>

<span data-ttu-id="08cca-111">*ResourcesInDesiredState* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="08cca-111">*ResourcesInDesiredState* \[out\]</span></span>  
<span data-ttu-id="08cca-112">A visszatérési, tartalmazza a beágyazott példányának a **MSFT_ResourceInDesiredState** osztály, amely meghatározza a kívánt állapot-erőforrást.</span><span class="sxs-lookup"><span data-stu-id="08cca-112">On return, contains an embedded instance of the **MSFT_ResourceInDesiredState** class that specifies resources that are in the desired state.</span></span>

<span data-ttu-id="08cca-113">*ResourcesNotInDesiredState* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="08cca-113">*ResourcesNotInDesiredState* \[out\]</span></span>  
<span data-ttu-id="08cca-114">A visszatérési, tartalmazza a beágyazott példányának a **MSFT_ResourceNotInDesiredState** osztály, amely meghatározza az erőforrásokat, amelyek nem a megfelelő állapotban van.</span><span class="sxs-lookup"><span data-stu-id="08cca-114">On return, contains an embedded instance of the **MSFT_ResourceNotInDesiredState** class that specifies resources that are not in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="08cca-115">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="08cca-115">Return value</span></span>
------------

<span data-ttu-id="08cca-116">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="08cca-116">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="08cca-117">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="08cca-117">Remarks</span></span>

<span data-ttu-id="08cca-118">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="08cca-118">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="08cca-119">Követelmények</span><span class="sxs-lookup"><span data-stu-id="08cca-119">Requirements</span></span>
------------
><span data-ttu-id="08cca-120">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="08cca-120">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="08cca-121">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="08cca-121">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="08cca-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="08cca-122">See also</span></span>


[<span data-ttu-id="08cca-123">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="08cca-123">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



