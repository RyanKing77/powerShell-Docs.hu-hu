---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály SendConfiguration metódusa
ms.openlocfilehash: 3529bc56ecba19ed0fbbf070a4e86d0692824d39
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62078384"
---
# <a name="sendconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="03b69-103">Az MSFT_DSCLocalConfigurationManager osztály SendConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="03b69-103">SendConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="03b69-104">A konfigurációs dokumentum a felügyelt csomópont küld, és menti azt egy függőben lévő módosítást.</span><span class="sxs-lookup"><span data-stu-id="03b69-104">Sends the configuration document to the managed node and saves it as a pending change.</span></span>

## <a name="syntax"></a><span data-ttu-id="03b69-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="03b69-105">Syntax</span></span>

```mof
uint32 SendConfiguration(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="03b69-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="03b69-106">Parameters</span></span>

<span data-ttu-id="03b69-107">*ConfigurationData* \[a\] konfigurációjának a környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="03b69-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="03b69-108">*kényszerített* \[a\] **igaz** kényszerített leállítása a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="03b69-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="03b69-109">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="03b69-109">Return value</span></span>

<span data-ttu-id="03b69-110">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="03b69-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="03b69-111">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="03b69-111">Remarks</span></span>

<span data-ttu-id="03b69-112">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="03b69-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="03b69-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="03b69-113">Requirements</span></span>

<span data-ttu-id="03b69-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="03b69-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="03b69-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="03b69-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="03b69-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="03b69-116">See also</span></span>

[<span data-ttu-id="03b69-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="03b69-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)