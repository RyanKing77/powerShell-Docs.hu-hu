---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály GetConfigurationStatus metódusa
ms.openlocfilehash: c66ccc4eefaef2d0c3a68fa8a96c5abb9bda6e4c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686641"
---
# <a name="getconfigurationstatus-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="f0a4d-103">Az MSFT_DSCLocalConfigurationManager osztály GetConfigurationStatus metódusa</span><span class="sxs-lookup"><span data-stu-id="f0a4d-103">GetConfigurationStatus method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="f0a4d-104">A konfigurációs ügyfélállapot előzményeinek lekérése.</span><span class="sxs-lookup"><span data-stu-id="f0a4d-104">Get the configuration status history.</span></span>

## <a name="syntax"></a><span data-ttu-id="f0a4d-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="f0a4d-105">Syntax</span></span>

```mof
uint32 GetConfigurationStatus(
  [in]  boolean                     All,
  [out] MSFT_DSCConfigurationStatus configurationStatus[]
);
```

## <a name="parameters"></a><span data-ttu-id="f0a4d-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="f0a4d-106">Parameters</span></span>

<span data-ttu-id="f0a4d-107">*Az összes* \[a\] **igaz** Ha ez a módszer minden információt, a konfiguráció fut a gépen kell visszaadnia, többek között a konfigurációs alkalmazás és a konzisztencia-ellenőrzést.</span><span class="sxs-lookup"><span data-stu-id="f0a4d-107">*All* \[in\] **true** if this method should return information about all the configuration runs on the machine, including the configuration application and the consistency check.</span></span>

<span data-ttu-id="f0a4d-108">*configurationStatus* \[ki\] return tartalmaz egy beágyazott példányát a **MSFT_DSCConfigurationStatus** osztály, amely meghatározza a beállításokat.</span><span class="sxs-lookup"><span data-stu-id="f0a4d-108">*configurationStatus* \[out\] On return, contains an embedded instance of the **MSFT_DSCConfigurationStatus** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="f0a4d-109">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="f0a4d-109">Return value</span></span>

<span data-ttu-id="f0a4d-110">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="f0a4d-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="f0a4d-111">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="f0a4d-111">Remarks</span></span>

<span data-ttu-id="f0a4d-112">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="f0a4d-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="f0a4d-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="f0a4d-113">Requirements</span></span>

<span data-ttu-id="f0a4d-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="f0a4d-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="f0a4d-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="f0a4d-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="f0a4d-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="f0a4d-116">See also</span></span>

[<span data-ttu-id="f0a4d-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="f0a4d-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)