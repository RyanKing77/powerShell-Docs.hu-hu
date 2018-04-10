---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály GetConfigurationStatus metódusa
ms.openlocfilehash: dde4ac003b346018561481e05ca7374475f9ff1d
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="getconfigurationstatus-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="97d2c-103">Az MSFT_DSCLocalConfigurationManager osztály GetConfigurationStatus metódusa</span><span class="sxs-lookup"><span data-stu-id="97d2c-103">GetConfigurationStatus method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="97d2c-104">A konfigurációs állapotának előzménye beolvasása.</span><span class="sxs-lookup"><span data-stu-id="97d2c-104">Get the configuration status history.</span></span>

<a name="syntax"></a><span data-ttu-id="97d2c-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="97d2c-105">Syntax</span></span>
------

```mof
uint32 GetConfigurationStatus(
  [in]  boolean                     All,
  [out] MSFT_DSCConfigurationStatus configurationStatus[]
);
```

<a name="parameters"></a><span data-ttu-id="97d2c-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="97d2c-106">Parameters</span></span>
----------

<span data-ttu-id="97d2c-107">*Minden* \[a\] **igaz** Ha ez a módszer minden információt, a konfiguráció fut a gépen kell visszaadnia, beleértve a konfigurációs alkalmazás és a konzisztencia-ellenőrzést.</span><span class="sxs-lookup"><span data-stu-id="97d2c-107">*All* \[in\] **true** if this method should return information about all the configuration runs on the machine, including the configuration application and the consistency check.</span></span>

<span data-ttu-id="97d2c-108">*configurationStatus* \[kimenő\] return tartalmaz beágyazott példányának a **MSFT_DSCConfigurationStatus** osztály, amely meghatározza a beállításokat.</span><span class="sxs-lookup"><span data-stu-id="97d2c-108">*configurationStatus* \[out\] On return, contains an embedded instance of the **MSFT_DSCConfigurationStatus** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="97d2c-109">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="97d2c-109">Return value</span></span>
------------

<span data-ttu-id="97d2c-110">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="97d2c-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="97d2c-111">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="97d2c-111">Remarks</span></span>

<span data-ttu-id="97d2c-112">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="97d2c-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="97d2c-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="97d2c-113">Requirements</span></span>
------------
><span data-ttu-id="97d2c-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="97d2c-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="97d2c-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="97d2c-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="97d2c-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="97d2c-116">See also</span></span>


[<span data-ttu-id="97d2c-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="97d2c-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)