---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály GetConfigurationResultOutput metódusa
ms.openlocfilehash: ea572a4a66befd4e4b8d83e2957632b1b5ed7d93
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893943"
---
# <a name="getconfigurationresultoutput-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="a7d34-103">Az MSFT_DSCLocalConfigurationManager osztály GetConfigurationResultOutput metódusa</span><span class="sxs-lookup"><span data-stu-id="a7d34-103">GetConfigurationResultOutput method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="a7d34-104">Lekéri egy adott feladathoz társított konfigurációs ügynök kimenetét.</span><span class="sxs-lookup"><span data-stu-id="a7d34-104">Gets the Configuration Agent output associated with a specific job.</span></span>

## <a name="syntax"></a><span data-ttu-id="a7d34-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="a7d34-105">Syntax</span></span>

```mof
uint32 GetConfigurationResultOutput(
  [in]  string                      jobId,
  [in]  uint8                       resumeOutputBookmark[],
  [out] MSFT_DSCConfigurationOutput output[]
);
```

## <a name="parameters"></a><span data-ttu-id="a7d34-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="a7d34-106">Parameters</span></span>

<span data-ttu-id="a7d34-107">*jobId* \[a\] az azonosító a feladat kimeneti adatok betöltéséhez.</span><span class="sxs-lookup"><span data-stu-id="a7d34-107">*jobId* \[in\] The ID of the job for which to get output data.</span></span>

<span data-ttu-id="a7d34-108">*resumeOutputBookmark* \[a\] Megadja, hogy a kimenet legyen-e az előző könyvjelző folytatása.</span><span class="sxs-lookup"><span data-stu-id="a7d34-108">*resumeOutputBookmark* \[in\] Specifies that the output should be a continuation from a previous bookmark.</span></span>

<span data-ttu-id="a7d34-109">*kimeneti* \[ki\] a megadott feladat kimenetét.</span><span class="sxs-lookup"><span data-stu-id="a7d34-109">*output* \[out\] The output for the specified job.</span></span>

## <a name="return-value"></a><span data-ttu-id="a7d34-110">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="a7d34-110">Return value</span></span>

<span data-ttu-id="a7d34-111">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="a7d34-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="a7d34-112">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="a7d34-112">Remarks</span></span>

<span data-ttu-id="a7d34-113">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="a7d34-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="a7d34-114">Követelmények</span><span class="sxs-lookup"><span data-stu-id="a7d34-114">Requirements</span></span>

<span data-ttu-id="a7d34-115">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="a7d34-115">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="a7d34-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="a7d34-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="a7d34-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="a7d34-117">See also</span></span>

[<span data-ttu-id="a7d34-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="a7d34-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)