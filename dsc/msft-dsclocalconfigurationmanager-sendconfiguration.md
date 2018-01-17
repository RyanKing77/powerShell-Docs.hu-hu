---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály SendConfiguration módszer"
ms.openlocfilehash: 72c59b5aad293fa561146e5ad6822f27f40f321f
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="sendconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="8939d-103">A MSFT_DSCLocalConfigurationManager osztály SendConfiguration módszer</span><span class="sxs-lookup"><span data-stu-id="8939d-103">SendConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="8939d-104">A konfigurációs dokumentum küld a felügyelt csomóponthoz, és menti a függőben lévő módosítása.</span><span class="sxs-lookup"><span data-stu-id="8939d-104">Sends the configuration document to the managed node and saves it as a pending change.</span></span>

<a name="syntax"></a><span data-ttu-id="8939d-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="8939d-105">Syntax</span></span>
------

```mof
uint32 SendConfiguration(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="8939d-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="8939d-106">Parameters</span></span>
----------

<span data-ttu-id="8939d-107">*ConfigurationData* \[a\]</span><span class="sxs-lookup"><span data-stu-id="8939d-107">*ConfigurationData* \[in\]</span></span>  
<span data-ttu-id="8939d-108">A környezet konfigurációjának adatait.</span><span class="sxs-lookup"><span data-stu-id="8939d-108">The environment data for the configuration.</span></span>

<span data-ttu-id="8939d-109">*kényszerített* \[a\]</span><span class="sxs-lookup"><span data-stu-id="8939d-109">*force* \[in\]</span></span>  
<span data-ttu-id="8939d-110">**Igaz** kényszerítése a konfigurációját, és állítsa le.</span><span class="sxs-lookup"><span data-stu-id="8939d-110">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="8939d-111">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="8939d-111">Return value</span></span>
------------

<span data-ttu-id="8939d-112">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="8939d-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="8939d-113">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="8939d-113">Remarks</span></span>

<span data-ttu-id="8939d-114">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="8939d-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="8939d-115">Követelmények</span><span class="sxs-lookup"><span data-stu-id="8939d-115">Requirements</span></span>
------------
><span data-ttu-id="8939d-116">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="8939d-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="8939d-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="8939d-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="8939d-118">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="8939d-118">See also</span></span>


[<span data-ttu-id="8939d-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="8939d-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



