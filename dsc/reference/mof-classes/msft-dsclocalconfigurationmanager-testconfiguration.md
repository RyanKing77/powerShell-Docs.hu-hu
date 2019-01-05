---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály TestConfiguration metódusa
ms.openlocfilehash: d746832b01310f43a7aae33dd0fa70c0928bb3e0
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048255"
---
# <a name="testconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="7bf0f-103">Az MSFT_DSCLocalConfigurationManager osztály TestConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="7bf0f-103">TestConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="7bf0f-104">A konfigurációs dokumentum a felügyelt csomópont küld, és ellenőrzi az aktuális konfiguráció ellen a dokumentumot.</span><span class="sxs-lookup"><span data-stu-id="7bf0f-104">Sends the configuration document to the managed node and verifies the current configuration against the document.</span></span>

## <a name="syntax"></a><span data-ttu-id="7bf0f-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="7bf0f-105">Syntax</span></span>

```mof
uint32 TestConfiguration(
  [in]  uint8                          configurationData[],
  [out] boolean                        InDesiredState,
  [out] MSFT_ResourceInDesiredState    ResourcesInDesiredState[],
  [out] MSFT_ResourceNotInDesiredState ResourcesNotInDesiredState[]
);
```

## <a name="parameters"></a><span data-ttu-id="7bf0f-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="7bf0f-106">Parameters</span></span>

<span data-ttu-id="7bf0f-107">*configurationData* \[a\] confuguration a környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="7bf0f-107">*configurationData* \[in\] Environment data for the confuguration.</span></span>

<span data-ttu-id="7bf0f-108">*InDesiredState* \[ki\] lépjen vissza, a Megadja, hogy a kezelt csomópontok a konfigurációs dokumentum által meghatározott állapotban van-e.</span><span class="sxs-lookup"><span data-stu-id="7bf0f-108">*InDesiredState* \[out\] On return, specifies whether the managed node is in the state specified by the configuration document.</span></span>

<span data-ttu-id="7bf0f-109">*ResourcesInDesiredState* \[ki\] return tartalmaz egy beágyazott példányát a **MSFT_ResourceInDesiredState** osztály, amely meghatározza az erőforrást, amely a kívánt állapotban.</span><span class="sxs-lookup"><span data-stu-id="7bf0f-109">*ResourcesInDesiredState* \[out\] On return, contains an embedded instance of the **MSFT_ResourceInDesiredState** class that specifies resources that are in the desired state.</span></span>

<span data-ttu-id="7bf0f-110">*ResourcesNotInDesiredState* \[ki\] return tartalmaz egy beágyazott példányát a **MSFT_ResourceNotInDesiredState** osztály, amely megadja az erőforrások, amelyek nem a kívánt állapotban.</span><span class="sxs-lookup"><span data-stu-id="7bf0f-110">*ResourcesNotInDesiredState* \[out\] On return, contains an embedded instance of the **MSFT_ResourceNotInDesiredState** class that specifies resources that are not in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="7bf0f-111">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="7bf0f-111">Return value</span></span>

<span data-ttu-id="7bf0f-112">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="7bf0f-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="7bf0f-113">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="7bf0f-113">Remarks</span></span>

<span data-ttu-id="7bf0f-114">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="7bf0f-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="7bf0f-115">Követelmények</span><span class="sxs-lookup"><span data-stu-id="7bf0f-115">Requirements</span></span>

<span data-ttu-id="7bf0f-116">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="7bf0f-116">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="7bf0f-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="7bf0f-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="7bf0f-118">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="7bf0f-118">See also</span></span>

[<span data-ttu-id="7bf0f-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="7bf0f-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)