---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály GetConfigurationResultOutput módszer"
ms.openlocfilehash: f6106bb28dc20004b5bbb6df2d8e719cf0c453f0
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="getconfigurationresultoutput-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="ef6b3-103">A MSFT_DSCLocalConfigurationManager osztály GetConfigurationResultOutput módszer</span><span class="sxs-lookup"><span data-stu-id="ef6b3-103">GetConfigurationResultOutput method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="ef6b3-104">Egy adott feladattal társított konfigurációs ügynök kimenetének beolvasása.</span><span class="sxs-lookup"><span data-stu-id="ef6b3-104">Gets the Configuration Agent output associated with a specific job.</span></span>

<a name="syntax"></a><span data-ttu-id="ef6b3-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="ef6b3-105">Syntax</span></span>
------

```mof
uint32 GetConfigurationResultOutput(
  [in]  string                      jobId,
  [in]  uint8                       resumeOutputBookmark[],
  [out] MSFT_DSCConfigurationOutput output[]
);
```

<a name="parameters"></a><span data-ttu-id="ef6b3-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="ef6b3-106">Parameters</span></span>
----------

<span data-ttu-id="ef6b3-107">*a JobId értékének* \[a\]</span><span class="sxs-lookup"><span data-stu-id="ef6b3-107">*jobId* \[in\]</span></span>  
<span data-ttu-id="ef6b3-108">A feladatot, amelynek a kimeneti adatok azonosítója.</span><span class="sxs-lookup"><span data-stu-id="ef6b3-108">The ID of the job for which to get output data.</span></span>

<span data-ttu-id="ef6b3-109">*resumeOutputBookmark* \[a\]</span><span class="sxs-lookup"><span data-stu-id="ef6b3-109">*resumeOutputBookmark* \[in\]</span></span>  
<span data-ttu-id="ef6b3-110">Megadhatja, hogy a kimenet az előző könyvjelző folytatása.</span><span class="sxs-lookup"><span data-stu-id="ef6b3-110">Specifies that the output should be a continuation from a previous bookmark.</span></span>

<span data-ttu-id="ef6b3-111">*kimeneti* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="ef6b3-111">*output* \[out\]</span></span>  
<span data-ttu-id="ef6b3-112">A megadott feladathoz tartozó kimenete.</span><span class="sxs-lookup"><span data-stu-id="ef6b3-112">The output for the specified job.</span></span>

## <a name="return-value"></a><span data-ttu-id="ef6b3-113">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="ef6b3-113">Return value</span></span>
------------

<span data-ttu-id="ef6b3-114">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="ef6b3-114">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="ef6b3-115">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="ef6b3-115">Remarks</span></span>

<span data-ttu-id="ef6b3-116">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="ef6b3-116">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="ef6b3-117">Követelmények</span><span class="sxs-lookup"><span data-stu-id="ef6b3-117">Requirements</span></span>
------------
><span data-ttu-id="ef6b3-118">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="ef6b3-118">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="ef6b3-119">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="ef6b3-119">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="ef6b3-120">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ef6b3-120">See also</span></span>


[<span data-ttu-id="ef6b3-121">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="ef6b3-121">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)

 

 



