---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály GetConfigurationResultOutput módszer"
ms.openlocfilehash: 09862fd3c19e1e517c9bf5df878113ba3f10d8a6
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="getconfigurationresultoutput-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="21fa5-103">A MSFT_DSCLocalConfigurationManager osztály GetConfigurationResultOutput módszer</span><span class="sxs-lookup"><span data-stu-id="21fa5-103">GetConfigurationResultOutput method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="21fa5-104">Egy adott feladattal társított konfigurációs ügynök kimenetének beolvasása.</span><span class="sxs-lookup"><span data-stu-id="21fa5-104">Gets the Configuration Agent output associated with a specific job.</span></span>

<a name="syntax"></a><span data-ttu-id="21fa5-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="21fa5-105">Syntax</span></span>
------

```mof
uint32 GetConfigurationResultOutput(
  [in]  string                      jobId,
  [in]  uint8                       resumeOutputBookmark[],
  [out] MSFT_DSCConfigurationOutput output[]
);
```

<a name="parameters"></a><span data-ttu-id="21fa5-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="21fa5-106">Parameters</span></span>
----------

<span data-ttu-id="21fa5-107">*a JobId értékének* \[a\]</span><span class="sxs-lookup"><span data-stu-id="21fa5-107">*jobId* \[in\]</span></span>  
<span data-ttu-id="21fa5-108">A feladatot, amelynek a kimeneti adatok azonosítója.</span><span class="sxs-lookup"><span data-stu-id="21fa5-108">The ID of the job for which to get output data.</span></span>

<span data-ttu-id="21fa5-109">*resumeOutputBookmark* \[a\]</span><span class="sxs-lookup"><span data-stu-id="21fa5-109">*resumeOutputBookmark* \[in\]</span></span>  
<span data-ttu-id="21fa5-110">Megadhatja, hogy a kimenet az előző könyvjelző folytatása.</span><span class="sxs-lookup"><span data-stu-id="21fa5-110">Specifies that the output should be a continuation from a previous bookmark.</span></span>

<span data-ttu-id="21fa5-111">*kimeneti* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="21fa5-111">*output* \[out\]</span></span>  
<span data-ttu-id="21fa5-112">A megadott feladathoz tartozó kimenete.</span><span class="sxs-lookup"><span data-stu-id="21fa5-112">The output for the specified job.</span></span>

## <a name="return-value"></a><span data-ttu-id="21fa5-113">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="21fa5-113">Return value</span></span>
------------

<span data-ttu-id="21fa5-114">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="21fa5-114">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="21fa5-115">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="21fa5-115">Remarks</span></span>

<span data-ttu-id="21fa5-116">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="21fa5-116">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="21fa5-117">Követelmények</span><span class="sxs-lookup"><span data-stu-id="21fa5-117">Requirements</span></span>
------------
><span data-ttu-id="21fa5-118">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="21fa5-118">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="21fa5-119">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="21fa5-119">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="21fa5-120">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="21fa5-120">See also</span></span>


[<span data-ttu-id="21fa5-121">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="21fa5-121">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)

 

 



