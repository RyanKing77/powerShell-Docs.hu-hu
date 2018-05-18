---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály GetConfigurationResultOutput metódusa
ms.openlocfilehash: 73d10a8b44e5056e3fce1598518630a84aff6ceb
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="getconfigurationresultoutput-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="75661-103">Az MSFT_DSCLocalConfigurationManager osztály GetConfigurationResultOutput metódusa</span><span class="sxs-lookup"><span data-stu-id="75661-103">GetConfigurationResultOutput method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="75661-104">Egy adott feladattal társított konfigurációs ügynök kimenetének beolvasása.</span><span class="sxs-lookup"><span data-stu-id="75661-104">Gets the Configuration Agent output associated with a specific job.</span></span>

<a name="syntax"></a><span data-ttu-id="75661-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="75661-105">Syntax</span></span>
------

```mof
uint32 GetConfigurationResultOutput(
  [in]  string                      jobId,
  [in]  uint8                       resumeOutputBookmark[],
  [out] MSFT_DSCConfigurationOutput output[]
);
```

<a name="parameters"></a><span data-ttu-id="75661-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="75661-106">Parameters</span></span>
----------

<span data-ttu-id="75661-107">*a JobId értékének* \[a\] a feladatot, amelynek a kimeneti adatok beolvasása a azonosítója.</span><span class="sxs-lookup"><span data-stu-id="75661-107">*jobId* \[in\] The ID of the job for which to get output data.</span></span>

<span data-ttu-id="75661-108">*resumeOutputBookmark* \[a\] megadhatja, hogy a kimenet az előző könyvjelző folytatása.</span><span class="sxs-lookup"><span data-stu-id="75661-108">*resumeOutputBookmark* \[in\] Specifies that the output should be a continuation from a previous bookmark.</span></span>

<span data-ttu-id="75661-109">*kimeneti* \[kimenő\] a feladat kimenetét.</span><span class="sxs-lookup"><span data-stu-id="75661-109">*output* \[out\] The output for the specified job.</span></span>

## <a name="return-value"></a><span data-ttu-id="75661-110">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="75661-110">Return value</span></span>
------------

<span data-ttu-id="75661-111">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="75661-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="75661-112">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="75661-112">Remarks</span></span>

<span data-ttu-id="75661-113">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="75661-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="75661-114">Követelmények</span><span class="sxs-lookup"><span data-stu-id="75661-114">Requirements</span></span>
------------
><span data-ttu-id="75661-115">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="75661-115">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="75661-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="75661-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="75661-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="75661-117">See also</span></span>


[<span data-ttu-id="75661-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="75661-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)