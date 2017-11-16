---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály SendConfiguration módszer"
ms.openlocfilehash: 8457189538ceb0181a8e65b57a9fc3e911cbcec4
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="sendconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="2cd68-103">A MSFT_DSCLocalConfigurationManager osztály SendConfiguration módszer</span><span class="sxs-lookup"><span data-stu-id="2cd68-103">SendConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="2cd68-104">A konfigurációs dokumentum küld a felügyelt csomóponthoz, és menti a függőben lévő módosítása.</span><span class="sxs-lookup"><span data-stu-id="2cd68-104">Sends the configuration document to the managed node and saves it as a pending change.</span></span>

<a name="syntax"></a><span data-ttu-id="2cd68-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="2cd68-105">Syntax</span></span>
------

```mof
uint32 SendConfiguration(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="2cd68-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="2cd68-106">Parameters</span></span>
----------

<span data-ttu-id="2cd68-107">*ConfigurationData* \[a\]</span><span class="sxs-lookup"><span data-stu-id="2cd68-107">*ConfigurationData* \[in\]</span></span>  
<span data-ttu-id="2cd68-108">A környezet konfigurációjának adatait.</span><span class="sxs-lookup"><span data-stu-id="2cd68-108">The environment data for the configuration.</span></span>

<span data-ttu-id="2cd68-109">*kényszerített* \[a\]</span><span class="sxs-lookup"><span data-stu-id="2cd68-109">*force* \[in\]</span></span>  
<span data-ttu-id="2cd68-110">**Igaz** kényszerítése a konfigurációját, és állítsa le.</span><span class="sxs-lookup"><span data-stu-id="2cd68-110">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="2cd68-111">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="2cd68-111">Return value</span></span>
------------

<span data-ttu-id="2cd68-112">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="2cd68-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="2cd68-113">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="2cd68-113">Remarks</span></span>

<span data-ttu-id="2cd68-114">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="2cd68-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="2cd68-115">Követelmények</span><span class="sxs-lookup"><span data-stu-id="2cd68-115">Requirements</span></span>
------------
><span data-ttu-id="2cd68-116">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="2cd68-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="2cd68-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="2cd68-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="2cd68-118">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2cd68-118">See also</span></span>


[<span data-ttu-id="2cd68-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="2cd68-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



