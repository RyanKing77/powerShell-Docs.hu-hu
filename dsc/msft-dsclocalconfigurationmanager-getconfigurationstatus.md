---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály GetConfigurationStatus módszer"
ms.openlocfilehash: e02ed81a7b8436323bc68aaa2587a445e6a5adf9
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="getconfigurationstatus-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="33c7d-103">A MSFT_DSCLocalConfigurationManager osztály GetConfigurationStatus módszer</span><span class="sxs-lookup"><span data-stu-id="33c7d-103">GetConfigurationStatus method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="33c7d-104">A konfigurációs állapotának előzménye beolvasása.</span><span class="sxs-lookup"><span data-stu-id="33c7d-104">Get the configuration status history.</span></span>

<a name="syntax"></a><span data-ttu-id="33c7d-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="33c7d-105">Syntax</span></span>
------

```mof
uint32 GetConfigurationStatus(
  [in]  boolean                     All,
  [out] MSFT_DSCConfigurationStatus configurationStatus[]
);
```

<a name="parameters"></a><span data-ttu-id="33c7d-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="33c7d-106">Parameters</span></span>
----------

<span data-ttu-id="33c7d-107">*Minden* \[a\]</span><span class="sxs-lookup"><span data-stu-id="33c7d-107">*All* \[in\]</span></span>  
<span data-ttu-id="33c7d-108">**Igaz** Ha ez a módszer minden információt, a konfiguráció fut a gépen kell visszaadnia, beleértve a konfigurációs alkalmazás és a konzisztencia-ellenőrzést.</span><span class="sxs-lookup"><span data-stu-id="33c7d-108">**true** if this method should return information about all the configuration runs on the machine, including the configuration application and the consistency check.</span></span>

<span data-ttu-id="33c7d-109">*configurationStatus* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="33c7d-109">*configurationStatus* \[out\]</span></span>  
<span data-ttu-id="33c7d-110">A visszatérési, tartalmazza a beágyazott példányának a **MSFT_DSCConfigurationStatus** osztály, amely meghatározza a beállításokat.</span><span class="sxs-lookup"><span data-stu-id="33c7d-110">On return, contains an embedded instance of the **MSFT_DSCConfigurationStatus** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="33c7d-111">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="33c7d-111">Return value</span></span>
------------

<span data-ttu-id="33c7d-112">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="33c7d-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="33c7d-113">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="33c7d-113">Remarks</span></span>

<span data-ttu-id="33c7d-114">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="33c7d-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="33c7d-115">Követelmények</span><span class="sxs-lookup"><span data-stu-id="33c7d-115">Requirements</span></span>
------------
><span data-ttu-id="33c7d-116">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="33c7d-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="33c7d-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="33c7d-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="33c7d-118">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="33c7d-118">See also</span></span>


[<span data-ttu-id="33c7d-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="33c7d-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



