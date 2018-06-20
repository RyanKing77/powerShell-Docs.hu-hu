---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály GetConfigurationStatus metódusa
ms.openlocfilehash: 725b1a2a62510a4e9b59aabdec8a7e502c737bfc
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34221765"
---
# <a name="getconfigurationstatus-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="941b3-103">Az MSFT_DSCLocalConfigurationManager osztály GetConfigurationStatus metódusa</span><span class="sxs-lookup"><span data-stu-id="941b3-103">GetConfigurationStatus method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="941b3-104">A konfigurációs állapotának előzménye beolvasása.</span><span class="sxs-lookup"><span data-stu-id="941b3-104">Get the configuration status history.</span></span>

<a name="syntax"></a><span data-ttu-id="941b3-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="941b3-105">Syntax</span></span>
------

```mof
uint32 GetConfigurationStatus(
  [in]  boolean                     All,
  [out] MSFT_DSCConfigurationStatus configurationStatus[]
);
```

<a name="parameters"></a><span data-ttu-id="941b3-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="941b3-106">Parameters</span></span>
----------

<span data-ttu-id="941b3-107">*Minden* \[a\] **igaz** Ha ez a módszer minden információt, a konfiguráció fut a gépen kell visszaadnia, beleértve a konfigurációs alkalmazás és a konzisztencia-ellenőrzést.</span><span class="sxs-lookup"><span data-stu-id="941b3-107">*All* \[in\] **true** if this method should return information about all the configuration runs on the machine, including the configuration application and the consistency check.</span></span>

<span data-ttu-id="941b3-108">*configurationStatus* \[kimenő\] return tartalmaz beágyazott példányának a **MSFT_DSCConfigurationStatus** osztály, amely meghatározza a beállításokat.</span><span class="sxs-lookup"><span data-stu-id="941b3-108">*configurationStatus* \[out\] On return, contains an embedded instance of the **MSFT_DSCConfigurationStatus** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="941b3-109">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="941b3-109">Return value</span></span>
------------

<span data-ttu-id="941b3-110">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="941b3-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="941b3-111">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="941b3-111">Remarks</span></span>

<span data-ttu-id="941b3-112">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="941b3-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="941b3-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="941b3-113">Requirements</span></span>
------------
><span data-ttu-id="941b3-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="941b3-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="941b3-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="941b3-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="941b3-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="941b3-116">See also</span></span>


[<span data-ttu-id="941b3-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="941b3-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)