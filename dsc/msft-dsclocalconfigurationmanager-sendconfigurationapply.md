---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApply metódusa
ms.openlocfilehash: da3a08307122ab38ee4a6fd5d4a9b97579a988f7
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893171"
---
# <a name="sendconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="11d0e-103">Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApply metódusa</span><span class="sxs-lookup"><span data-stu-id="11d0e-103">SendConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="11d0e-104">A konfigurációs dokumentum a felügyelt csomópont küld, és a konfigurációs ügynök használja a alkalmazni a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="11d0e-104">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="11d0e-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="11d0e-105">Syntax</span></span>

```mof
uint32 SendConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="11d0e-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="11d0e-106">Parameters</span></span>

<span data-ttu-id="11d0e-107">*ConfigurationData* \[a\] konfigurációjának a környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="11d0e-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="11d0e-108">*kényszerített* \[a\] **igaz** kényszerített leállítása a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="11d0e-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="11d0e-109">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="11d0e-109">Return value</span></span>

<span data-ttu-id="11d0e-110">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="11d0e-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="11d0e-111">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="11d0e-111">Remarks</span></span>

<span data-ttu-id="11d0e-112">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="11d0e-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="11d0e-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="11d0e-113">Requirements</span></span>

<span data-ttu-id="11d0e-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="11d0e-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="11d0e-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="11d0e-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="11d0e-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="11d0e-116">See also</span></span>

[<span data-ttu-id="11d0e-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="11d0e-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)