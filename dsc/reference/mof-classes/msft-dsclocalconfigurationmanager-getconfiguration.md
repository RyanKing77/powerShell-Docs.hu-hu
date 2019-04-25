---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály GetConfiguration metódusa
ms.openlocfilehash: ae31ac30c152c96707b764ddaf00c924806afcfc
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62078653"
---
# <a name="getconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="a00e0-103">Az MSFT_DSCLocalConfigurationManager osztály GetConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="a00e0-103">GetConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="a00e0-104">A konfigurációs dokumentum küldése a felügyelt csomóponthoz, és használja a **első** metódus a alkalmazni a konfigurációt a konfigurációs ügynök.</span><span class="sxs-lookup"><span data-stu-id="a00e0-104">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="a00e0-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="a00e0-105">Syntax</span></span>

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

## <a name="parameters"></a><span data-ttu-id="a00e0-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="a00e0-106">Parameters</span></span>

<span data-ttu-id="a00e0-107">*configurationData* \[a\] adja meg a konfigurációs adatokat küldhet.</span><span class="sxs-lookup"><span data-stu-id="a00e0-107">*configurationData* \[in\] Specifies the configuration data to send.</span></span>

<span data-ttu-id="a00e0-108">*konfigurációk* \[ki\] lépjen vissza, tartalmazza a konfigurációkat egy beágyazott példányát.</span><span class="sxs-lookup"><span data-stu-id="a00e0-108">*configurations* \[out\] On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="a00e0-109">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="a00e0-109">Return value</span></span>

<span data-ttu-id="a00e0-110">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="a00e0-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="a00e0-111">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="a00e0-111">Remarks</span></span>

<span data-ttu-id="a00e0-112">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="a00e0-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="a00e0-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="a00e0-113">Requirements</span></span>

<span data-ttu-id="a00e0-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="a00e0-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="a00e0-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="a00e0-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="a00e0-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="a00e0-116">See also</span></span>

[<span data-ttu-id="a00e0-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="a00e0-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)