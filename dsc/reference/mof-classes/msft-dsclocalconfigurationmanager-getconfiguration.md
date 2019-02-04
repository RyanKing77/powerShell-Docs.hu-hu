---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály GetConfiguration metódusa
ms.openlocfilehash: ae31ac30c152c96707b764ddaf00c924806afcfc
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687208"
---
# <a name="getconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="70f13-103">Az MSFT_DSCLocalConfigurationManager osztály GetConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="70f13-103">GetConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="70f13-104">A konfigurációs dokumentum küldése a felügyelt csomóponthoz, és használja a **első** metódus a alkalmazni a konfigurációt a konfigurációs ügynök.</span><span class="sxs-lookup"><span data-stu-id="70f13-104">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="70f13-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="70f13-105">Syntax</span></span>

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

## <a name="parameters"></a><span data-ttu-id="70f13-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="70f13-106">Parameters</span></span>

<span data-ttu-id="70f13-107">*configurationData* \[a\] adja meg a konfigurációs adatokat küldhet.</span><span class="sxs-lookup"><span data-stu-id="70f13-107">*configurationData* \[in\] Specifies the configuration data to send.</span></span>

<span data-ttu-id="70f13-108">*konfigurációk* \[ki\] lépjen vissza, tartalmazza a konfigurációkat egy beágyazott példányát.</span><span class="sxs-lookup"><span data-stu-id="70f13-108">*configurations* \[out\] On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="70f13-109">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="70f13-109">Return value</span></span>

<span data-ttu-id="70f13-110">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="70f13-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="70f13-111">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="70f13-111">Remarks</span></span>

<span data-ttu-id="70f13-112">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="70f13-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="70f13-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="70f13-113">Requirements</span></span>

<span data-ttu-id="70f13-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="70f13-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="70f13-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="70f13-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="70f13-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="70f13-116">See also</span></span>

[<span data-ttu-id="70f13-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="70f13-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)