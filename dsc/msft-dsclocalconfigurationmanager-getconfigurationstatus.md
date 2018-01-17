---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály GetConfigurationStatus módszer"
ms.openlocfilehash: a41e7a15fc935c2cd5fd4cb66d0ab13509d5d4e0
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="getconfigurationstatus-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="cdd15-103">A MSFT_DSCLocalConfigurationManager osztály GetConfigurationStatus módszer</span><span class="sxs-lookup"><span data-stu-id="cdd15-103">GetConfigurationStatus method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="cdd15-104">A konfigurációs állapotának előzménye beolvasása.</span><span class="sxs-lookup"><span data-stu-id="cdd15-104">Get the configuration status history.</span></span>

<a name="syntax"></a><span data-ttu-id="cdd15-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="cdd15-105">Syntax</span></span>
------

```mof
uint32 GetConfigurationStatus(
  [in]  boolean                     All,
  [out] MSFT_DSCConfigurationStatus configurationStatus[]
);
```

<a name="parameters"></a><span data-ttu-id="cdd15-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="cdd15-106">Parameters</span></span>
----------

<span data-ttu-id="cdd15-107">*Minden* \[a\]</span><span class="sxs-lookup"><span data-stu-id="cdd15-107">*All* \[in\]</span></span>  
<span data-ttu-id="cdd15-108">**Igaz** Ha ez a módszer minden információt, a konfiguráció fut a gépen kell visszaadnia, beleértve a konfigurációs alkalmazás és a konzisztencia-ellenőrzést.</span><span class="sxs-lookup"><span data-stu-id="cdd15-108">**true** if this method should return information about all the configuration runs on the machine, including the configuration application and the consistency check.</span></span>

<span data-ttu-id="cdd15-109">*configurationStatus* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="cdd15-109">*configurationStatus* \[out\]</span></span>  
<span data-ttu-id="cdd15-110">A visszatérési, tartalmazza a beágyazott példányának a **MSFT_DSCConfigurationStatus** osztály, amely meghatározza a beállításokat.</span><span class="sxs-lookup"><span data-stu-id="cdd15-110">On return, contains an embedded instance of the **MSFT_DSCConfigurationStatus** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="cdd15-111">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="cdd15-111">Return value</span></span>
------------

<span data-ttu-id="cdd15-112">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="cdd15-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="cdd15-113">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="cdd15-113">Remarks</span></span>

<span data-ttu-id="cdd15-114">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="cdd15-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="cdd15-115">Követelmények</span><span class="sxs-lookup"><span data-stu-id="cdd15-115">Requirements</span></span>
------------
><span data-ttu-id="cdd15-116">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="cdd15-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="cdd15-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="cdd15-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="cdd15-118">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="cdd15-118">See also</span></span>


[<span data-ttu-id="cdd15-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="cdd15-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



