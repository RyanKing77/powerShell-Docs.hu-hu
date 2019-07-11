---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: GetConfigurationStatus metódusa
ms.openlocfilehash: 83b30ba2612d962fcf2fa658d07d18fb2d91ccc7
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67734511"
---
# <a name="getconfigurationstatus-method"></a><span data-ttu-id="61296-103">GetConfigurationStatus metódusa</span><span class="sxs-lookup"><span data-stu-id="61296-103">GetConfigurationStatus method</span></span>

<span data-ttu-id="61296-104">A konfigurációs ügyfélállapot előzményeinek lekérése.</span><span class="sxs-lookup"><span data-stu-id="61296-104">Get the configuration status history.</span></span>

## <a name="syntax"></a><span data-ttu-id="61296-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="61296-105">Syntax</span></span>

```mof
uint32 GetConfigurationStatus(
  [in]  boolean                     All,
  [out] MSFT_DSCConfigurationStatus configurationStatus[]
);
```

## <a name="parameters"></a><span data-ttu-id="61296-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="61296-106">Parameters</span></span>

<span data-ttu-id="61296-107">*Az összes* \[a\] **igaz** Ha ez a módszer minden információt, a konfiguráció fut a gépen kell visszaadnia, többek között a konfigurációs alkalmazás és a konzisztencia-ellenőrzést.</span><span class="sxs-lookup"><span data-stu-id="61296-107">*All* \[in\] **true** if this method should return information about all the configuration runs on the machine, including the configuration application and the consistency check.</span></span>

<span data-ttu-id="61296-108">*configurationStatus* \[ki\] return tartalmaz egy beágyazott példányát a **MSFT_DSCConfigurationStatus** osztály, amely meghatározza a beállításokat.</span><span class="sxs-lookup"><span data-stu-id="61296-108">*configurationStatus* \[out\] On return, contains an embedded instance of the **MSFT_DSCConfigurationStatus** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="61296-109">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="61296-109">Return value</span></span>

<span data-ttu-id="61296-110">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="61296-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="61296-111">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="61296-111">Remarks</span></span>

<span data-ttu-id="61296-112">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="61296-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="61296-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="61296-113">Requirements</span></span>

<span data-ttu-id="61296-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="61296-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="61296-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="61296-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="61296-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="61296-116">See also</span></span>

[<span data-ttu-id="61296-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="61296-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
