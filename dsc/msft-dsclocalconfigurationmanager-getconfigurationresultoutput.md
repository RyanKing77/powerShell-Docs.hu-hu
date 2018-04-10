---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály GetConfigurationResultOutput metódusa
ms.openlocfilehash: f4c2ddaa37cdafeff1a442f3f1fa656788a1c6c8
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="getconfigurationresultoutput-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="33f17-103">Az MSFT_DSCLocalConfigurationManager osztály GetConfigurationResultOutput metódusa</span><span class="sxs-lookup"><span data-stu-id="33f17-103">GetConfigurationResultOutput method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="33f17-104">Egy adott feladattal társított konfigurációs ügynök kimenetének beolvasása.</span><span class="sxs-lookup"><span data-stu-id="33f17-104">Gets the Configuration Agent output associated with a specific job.</span></span>

<a name="syntax"></a><span data-ttu-id="33f17-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="33f17-105">Syntax</span></span>
------

```mof
uint32 GetConfigurationResultOutput(
  [in]  string                      jobId,
  [in]  uint8                       resumeOutputBookmark[],
  [out] MSFT_DSCConfigurationOutput output[]
);
```

<a name="parameters"></a><span data-ttu-id="33f17-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="33f17-106">Parameters</span></span>
----------

<span data-ttu-id="33f17-107">*a JobId értékének* \[a\] a feladatot, amelynek a kimeneti adatok beolvasása a azonosítója.</span><span class="sxs-lookup"><span data-stu-id="33f17-107">*jobId* \[in\] The ID of the job for which to get output data.</span></span>

<span data-ttu-id="33f17-108">*resumeOutputBookmark* \[a\] megadhatja, hogy a kimenet az előző könyvjelző folytatása.</span><span class="sxs-lookup"><span data-stu-id="33f17-108">*resumeOutputBookmark* \[in\] Specifies that the output should be a continuation from a previous bookmark.</span></span>

<span data-ttu-id="33f17-109">*kimeneti* \[kimenő\] a feladat kimenetét.</span><span class="sxs-lookup"><span data-stu-id="33f17-109">*output* \[out\] The output for the specified job.</span></span>

## <a name="return-value"></a><span data-ttu-id="33f17-110">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="33f17-110">Return value</span></span>
------------

<span data-ttu-id="33f17-111">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="33f17-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="33f17-112">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="33f17-112">Remarks</span></span>

<span data-ttu-id="33f17-113">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="33f17-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="33f17-114">Követelmények</span><span class="sxs-lookup"><span data-stu-id="33f17-114">Requirements</span></span>
------------
><span data-ttu-id="33f17-115">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="33f17-115">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="33f17-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="33f17-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="33f17-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="33f17-117">See also</span></span>


[<span data-ttu-id="33f17-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="33f17-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)