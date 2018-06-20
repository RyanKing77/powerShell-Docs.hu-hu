---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály TestConfiguration metódusa
ms.openlocfilehash: 2df04d317bd5e7a5c2a713d92be57c5c9a9f5e8c
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219011"
---
# <a name="testconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="c0df2-103">Az MSFT_DSCLocalConfigurationManager osztály TestConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="c0df2-103">TestConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="c0df2-104">A konfigurációs dokumentum küld a felügyelt csomóponthoz, és a jelenlegi konfiguráció alapján a dokumentum ellenőrzi.</span><span class="sxs-lookup"><span data-stu-id="c0df2-104">Sends the configuration document to the managed node and verifies the current configuration against the document.</span></span>

<a name="syntax"></a><span data-ttu-id="c0df2-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="c0df2-105">Syntax</span></span>
------

```mof
uint32 TestConfiguration(
  [in]  uint8                          configurationData[],
  [out] boolean                        InDesiredState,
  [out] MSFT_ResourceInDesiredState    ResourcesInDesiredState[],
  [out] MSFT_ResourceNotInDesiredState ResourcesNotInDesiredState[]
);
```

<a name="parameters"></a><span data-ttu-id="c0df2-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="c0df2-106">Parameters</span></span>
----------

<span data-ttu-id="c0df2-107">*configurationData* \[a\] a confuguration környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="c0df2-107">*configurationData* \[in\] Environment data for the confuguration.</span></span>

<span data-ttu-id="c0df2-108">*InDesiredState* \[kimenő\] a return határozza meg, hogy a felügyelt csomóponthoz a konfigurációs dokumentum által meghatározott állapotban.</span><span class="sxs-lookup"><span data-stu-id="c0df2-108">*InDesiredState* \[out\] On return, specifies whether the managed node is in the state specified by the configuration document.</span></span>

<span data-ttu-id="c0df2-109">*ResourcesInDesiredState* \[kimenő\] return tartalmaz beágyazott példányának a **MSFT_ResourceInDesiredState** osztály, amely meghatározza a kívánt állapot-erőforrást.</span><span class="sxs-lookup"><span data-stu-id="c0df2-109">*ResourcesInDesiredState* \[out\] On return, contains an embedded instance of the **MSFT_ResourceInDesiredState** class that specifies resources that are in the desired state.</span></span>

<span data-ttu-id="c0df2-110">*ResourcesNotInDesiredState* \[kimenő\] return tartalmaz beágyazott példányának a **MSFT_ResourceNotInDesiredState** osztály, amely meghatározza az erőforrásokat, amelyek nem a megfelelő állapotban van.</span><span class="sxs-lookup"><span data-stu-id="c0df2-110">*ResourcesNotInDesiredState* \[out\] On return, contains an embedded instance of the **MSFT_ResourceNotInDesiredState** class that specifies resources that are not in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="c0df2-111">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="c0df2-111">Return value</span></span>
------------

<span data-ttu-id="c0df2-112">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="c0df2-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="c0df2-113">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="c0df2-113">Remarks</span></span>

<span data-ttu-id="c0df2-114">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="c0df2-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="c0df2-115">Követelmények</span><span class="sxs-lookup"><span data-stu-id="c0df2-115">Requirements</span></span>
------------
><span data-ttu-id="c0df2-116">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="c0df2-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="c0df2-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="c0df2-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="c0df2-118">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c0df2-118">See also</span></span>


[<span data-ttu-id="c0df2-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="c0df2-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)