---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály GetConfigurationResultOutput metódusa
ms.openlocfilehash: ea572a4a66befd4e4b8d83e2957632b1b5ed7d93
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404295"
---
# <a name="getconfigurationresultoutput-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="cfd09-103">Az MSFT_DSCLocalConfigurationManager osztály GetConfigurationResultOutput metódusa</span><span class="sxs-lookup"><span data-stu-id="cfd09-103">GetConfigurationResultOutput method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="cfd09-104">Lekéri egy adott feladathoz társított konfigurációs ügynök kimenetét.</span><span class="sxs-lookup"><span data-stu-id="cfd09-104">Gets the Configuration Agent output associated with a specific job.</span></span>

## <a name="syntax"></a><span data-ttu-id="cfd09-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="cfd09-105">Syntax</span></span>

```mof
uint32 GetConfigurationResultOutput(
  [in]  string                      jobId,
  [in]  uint8                       resumeOutputBookmark[],
  [out] MSFT_DSCConfigurationOutput output[]
);
```

## <a name="parameters"></a><span data-ttu-id="cfd09-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="cfd09-106">Parameters</span></span>

<span data-ttu-id="cfd09-107">*jobId* \[a\] az azonosító a feladat kimeneti adatok betöltéséhez.</span><span class="sxs-lookup"><span data-stu-id="cfd09-107">*jobId* \[in\] The ID of the job for which to get output data.</span></span>

<span data-ttu-id="cfd09-108">*resumeOutputBookmark* \[a\] Megadja, hogy a kimenet legyen-e az előző könyvjelző folytatása.</span><span class="sxs-lookup"><span data-stu-id="cfd09-108">*resumeOutputBookmark* \[in\] Specifies that the output should be a continuation from a previous bookmark.</span></span>

<span data-ttu-id="cfd09-109">*kimeneti* \[ki\] a megadott feladat kimenetét.</span><span class="sxs-lookup"><span data-stu-id="cfd09-109">*output* \[out\] The output for the specified job.</span></span>

## <a name="return-value"></a><span data-ttu-id="cfd09-110">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="cfd09-110">Return value</span></span>

<span data-ttu-id="cfd09-111">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="cfd09-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="cfd09-112">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="cfd09-112">Remarks</span></span>

<span data-ttu-id="cfd09-113">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="cfd09-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="cfd09-114">Követelmények</span><span class="sxs-lookup"><span data-stu-id="cfd09-114">Requirements</span></span>

<span data-ttu-id="cfd09-115">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="cfd09-115">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="cfd09-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="cfd09-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="cfd09-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="cfd09-117">See also</span></span>

[<span data-ttu-id="cfd09-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="cfd09-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)