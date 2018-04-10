---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály GetConfiguration metódusa
ms.openlocfilehash: 07d7db9dcc4288e6b72d5df37d82e44eb6f72ad2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="getconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="e00e8-103">Az MSFT_DSCLocalConfigurationManager osztály GetConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="e00e8-103">GetConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="e00e8-104">A konfigurációs dokumentum küld a felügyelt csomóponthoz, és használja a **beolvasása** módszert a beállítások a konfigurációs ügynök.</span><span class="sxs-lookup"><span data-stu-id="e00e8-104">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="e00e8-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="e00e8-105">Syntax</span></span>
------

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

<a name="parameters"></a><span data-ttu-id="e00e8-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="e00e8-106">Parameters</span></span>
----------

<span data-ttu-id="e00e8-107">*configurationData* \[a\] határozza meg a konfigurációs adatok küldése.</span><span class="sxs-lookup"><span data-stu-id="e00e8-107">*configurationData* \[in\] Specifies the configuration data to send.</span></span>

<span data-ttu-id="e00e8-108">*konfigurációk* \[kimenő\] vissza, tartalmazza a konfigurációk beágyazott példánya.</span><span class="sxs-lookup"><span data-stu-id="e00e8-108">*configurations* \[out\] On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="e00e8-109">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="e00e8-109">Return value</span></span>
------------

<span data-ttu-id="e00e8-110">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="e00e8-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="e00e8-111">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="e00e8-111">Remarks</span></span>

<span data-ttu-id="e00e8-112">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="e00e8-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="e00e8-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="e00e8-113">Requirements</span></span>
------------
><span data-ttu-id="e00e8-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="e00e8-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="e00e8-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="e00e8-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="e00e8-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e00e8-116">See also</span></span>


[<span data-ttu-id="e00e8-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="e00e8-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)