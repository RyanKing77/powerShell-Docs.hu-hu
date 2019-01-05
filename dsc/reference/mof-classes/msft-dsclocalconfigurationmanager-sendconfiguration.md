---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály SendConfiguration metódusa
ms.openlocfilehash: 3529bc56ecba19ed0fbbf070a4e86d0692824d39
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048244"
---
# <a name="sendconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="7e781-103">Az MSFT_DSCLocalConfigurationManager osztály SendConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="7e781-103">SendConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="7e781-104">A konfigurációs dokumentum a felügyelt csomópont küld, és menti azt egy függőben lévő módosítást.</span><span class="sxs-lookup"><span data-stu-id="7e781-104">Sends the configuration document to the managed node and saves it as a pending change.</span></span>

## <a name="syntax"></a><span data-ttu-id="7e781-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="7e781-105">Syntax</span></span>

```mof
uint32 SendConfiguration(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="7e781-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="7e781-106">Parameters</span></span>

<span data-ttu-id="7e781-107">*ConfigurationData* \[a\] konfigurációjának a környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="7e781-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="7e781-108">*kényszerített* \[a\] **igaz** kényszerített leállítása a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="7e781-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="7e781-109">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="7e781-109">Return value</span></span>

<span data-ttu-id="7e781-110">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="7e781-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="7e781-111">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="7e781-111">Remarks</span></span>

<span data-ttu-id="7e781-112">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="7e781-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="7e781-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="7e781-113">Requirements</span></span>

<span data-ttu-id="7e781-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="7e781-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="7e781-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="7e781-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="7e781-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="7e781-116">See also</span></span>

[<span data-ttu-id="7e781-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="7e781-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)