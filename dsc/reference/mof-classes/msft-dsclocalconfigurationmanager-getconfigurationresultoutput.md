---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: GetConfigurationResultOutput metódusa
ms.openlocfilehash: 480e710ce1a208253f0e664474c3e9bab296066a
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727126"
---
# <a name="getconfigurationresultoutput-method"></a><span data-ttu-id="0b4a9-103">GetConfigurationResultOutput metódusa</span><span class="sxs-lookup"><span data-stu-id="0b4a9-103">GetConfigurationResultOutput method</span></span>

<span data-ttu-id="0b4a9-104">Lekéri egy adott feladathoz társított konfigurációs ügynök kimenetét.</span><span class="sxs-lookup"><span data-stu-id="0b4a9-104">Gets the Configuration Agent output associated with a specific job.</span></span>

## <a name="syntax"></a><span data-ttu-id="0b4a9-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="0b4a9-105">Syntax</span></span>

```mof
uint32 GetConfigurationResultOutput(
  [in]  string                      jobId,
  [in]  uint8                       resumeOutputBookmark[],
  [out] MSFT_DSCConfigurationOutput output[]
);
```

## <a name="parameters"></a><span data-ttu-id="0b4a9-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="0b4a9-106">Parameters</span></span>

<span data-ttu-id="0b4a9-107">*jobId* \[a\] az azonosító a feladat kimeneti adatok betöltéséhez.</span><span class="sxs-lookup"><span data-stu-id="0b4a9-107">*jobId* \[in\] The ID of the job for which to get output data.</span></span>

<span data-ttu-id="0b4a9-108">*resumeOutputBookmark* \[a\] Megadja, hogy a kimenet legyen-e az előző könyvjelző folytatása.</span><span class="sxs-lookup"><span data-stu-id="0b4a9-108">*resumeOutputBookmark* \[in\] Specifies that the output should be a continuation from a previous bookmark.</span></span>

<span data-ttu-id="0b4a9-109">*kimeneti* \[ki\] a megadott feladat kimenetét.</span><span class="sxs-lookup"><span data-stu-id="0b4a9-109">*output* \[out\] The output for the specified job.</span></span>

## <a name="return-value"></a><span data-ttu-id="0b4a9-110">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="0b4a9-110">Return value</span></span>

<span data-ttu-id="0b4a9-111">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="0b4a9-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="0b4a9-112">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="0b4a9-112">Remarks</span></span>

<span data-ttu-id="0b4a9-113">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="0b4a9-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="0b4a9-114">Követelmények</span><span class="sxs-lookup"><span data-stu-id="0b4a9-114">Requirements</span></span>

<span data-ttu-id="0b4a9-115">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="0b4a9-115">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="0b4a9-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="0b4a9-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="0b4a9-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0b4a9-117">See also</span></span>

[<span data-ttu-id="0b4a9-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="0b4a9-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
