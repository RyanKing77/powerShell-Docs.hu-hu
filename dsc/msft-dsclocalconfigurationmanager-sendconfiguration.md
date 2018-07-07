---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály SendConfiguration metódusa
ms.openlocfilehash: 3529bc56ecba19ed0fbbf070a4e86d0692824d39
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892443"
---
# <a name="sendconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="4b496-103">Az MSFT_DSCLocalConfigurationManager osztály SendConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="4b496-103">SendConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="4b496-104">A konfigurációs dokumentum a felügyelt csomópont küld, és menti azt egy függőben lévő módosítást.</span><span class="sxs-lookup"><span data-stu-id="4b496-104">Sends the configuration document to the managed node and saves it as a pending change.</span></span>

## <a name="syntax"></a><span data-ttu-id="4b496-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="4b496-105">Syntax</span></span>

```mof
uint32 SendConfiguration(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="4b496-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="4b496-106">Parameters</span></span>

<span data-ttu-id="4b496-107">*ConfigurationData* \[a\] konfigurációjának a környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="4b496-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="4b496-108">*kényszerített* \[a\] **igaz** kényszerített leállítása a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="4b496-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="4b496-109">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="4b496-109">Return value</span></span>

<span data-ttu-id="4b496-110">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="4b496-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="4b496-111">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="4b496-111">Remarks</span></span>

<span data-ttu-id="4b496-112">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="4b496-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="4b496-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="4b496-113">Requirements</span></span>

<span data-ttu-id="4b496-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="4b496-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="4b496-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="4b496-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="4b496-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="4b496-116">See also</span></span>

[<span data-ttu-id="4b496-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="4b496-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)