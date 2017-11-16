---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály SendMetaConfigurationApply módszer"
ms.openlocfilehash: d8ddc9d99f0d74ad907a6e39ae0e8ac14159be16
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="sendmetaconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="b6bd8-103">A MSFT_DSCLocalConfigurationManager osztály SendMetaConfigurationApply módszer</span><span class="sxs-lookup"><span data-stu-id="b6bd8-103">SendMetaConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="b6bd8-104">Beállítja a helyi Configuration Manager beállítások konfigurációs ügynök használt.</span><span class="sxs-lookup"><span data-stu-id="b6bd8-104">Sets the Local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

<a name="syntax"></a><span data-ttu-id="b6bd8-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="b6bd8-105">Syntax</span></span>
------

```mof
uint32 SendMetaConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="b6bd8-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="b6bd8-106">Parameters</span></span>
----------

<span data-ttu-id="b6bd8-107">*ConfigurationData* \[a\]</span><span class="sxs-lookup"><span data-stu-id="b6bd8-107">*ConfigurationData* \[in\]</span></span>  
<span data-ttu-id="b6bd8-108">A környezet konfigurációjának adatait.</span><span class="sxs-lookup"><span data-stu-id="b6bd8-108">The environment data for the configuration.</span></span>

<span data-ttu-id="b6bd8-109">*kényszerített* \[a\]</span><span class="sxs-lookup"><span data-stu-id="b6bd8-109">*force* \[in\]</span></span>  
<span data-ttu-id="b6bd8-110">**Igaz** kényszerítése a konfigurációját, és állítsa le.</span><span class="sxs-lookup"><span data-stu-id="b6bd8-110">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="b6bd8-111">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="b6bd8-111">Return value</span></span>
------------

<span data-ttu-id="b6bd8-112">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="b6bd8-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="b6bd8-113">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="b6bd8-113">Remarks</span></span>

<span data-ttu-id="b6bd8-114">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="b6bd8-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="b6bd8-115">Követelmények</span><span class="sxs-lookup"><span data-stu-id="b6bd8-115">Requirements</span></span>
------------
><span data-ttu-id="b6bd8-116">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="b6bd8-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="b6bd8-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="b6bd8-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="b6bd8-118">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b6bd8-118">See also</span></span>


[<span data-ttu-id="b6bd8-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="b6bd8-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



