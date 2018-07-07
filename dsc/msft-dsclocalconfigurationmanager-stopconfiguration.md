---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály StopConfiguration metódusa
ms.openlocfilehash: 1cd887d205967c3d282143df4e6199027639230e
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893875"
---
# <a name="stopconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="06070-103">Az MSFT_DSCLocalConfigurationManager osztály StopConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="06070-103">StopConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="06070-104">Leállítja a módosítás folyamatban van.</span><span class="sxs-lookup"><span data-stu-id="06070-104">Stops the configuration change that is in progress.</span></span>

## <a name="syntax"></a><span data-ttu-id="06070-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="06070-105">Syntax</span></span>

```mof
uint32 StopConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="06070-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="06070-106">Parameters</span></span>

<span data-ttu-id="06070-107">*kényszerített* \[a\] **igaz** kényszerített leállítása a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="06070-107">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="06070-108">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="06070-108">Return value</span></span>

<span data-ttu-id="06070-109">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="06070-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="06070-110">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="06070-110">Remarks</span></span>

<span data-ttu-id="06070-111">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="06070-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="06070-112">Követelmények</span><span class="sxs-lookup"><span data-stu-id="06070-112">Requirements</span></span>

<span data-ttu-id="06070-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="06070-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="06070-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="06070-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="06070-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="06070-115">See also</span></span>

[<span data-ttu-id="06070-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="06070-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)