---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály ResourceGet metódusa
ms.openlocfilehash: 1b74adf2327af2e0f9416f1d00eac4e3b75e9013
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62078571"
---
# <a name="resourceget-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="b2cb5-103">Az MSFT_DSCLocalConfigurationManager osztály ResourceGet metódusa</span><span class="sxs-lookup"><span data-stu-id="b2cb5-103">ResourceGet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="b2cb5-104">Közvetlenül meghívja a **első** metódus a DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="b2cb5-104">Directly calls the **Get** method of a DSC resource.</span></span>

## <a name="syntax"></a><span data-ttu-id="b2cb5-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="b2cb5-105">Syntax</span></span>

```mof
uint32 ResourceGet(
  [in]  string           ResourceType,
  [in]  string           ModuleName,
  [in]  uint8            resourceProperty[],
  [out] OMI_BaseResource configurations
);
```

## <a name="parameters"></a><span data-ttu-id="b2cb5-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="b2cb5-106">Parameters</span></span>

<span data-ttu-id="b2cb5-107">*Erőforrástípus* \[a\] hívja az erőforrás nevét.</span><span class="sxs-lookup"><span data-stu-id="b2cb5-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="b2cb5-108">*ModuleName* \[a\] neve a modul, amely tartalmazza az erőforrás meghívásához.</span><span class="sxs-lookup"><span data-stu-id="b2cb5-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="b2cb5-109">*resourceProperty* \[a\] határozza meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve.</span><span class="sxs-lookup"><span data-stu-id="b2cb5-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="b2cb5-110">Használja a [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) parancsmaggal a erőforrás-tulajdonságok és azok típusát.</span><span class="sxs-lookup"><span data-stu-id="b2cb5-110">Use the [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="b2cb5-111">*konfigurációk* \[ki\] lépjen vissza, tartalmazza a konfigurációkat egy beágyazott példányát.</span><span class="sxs-lookup"><span data-stu-id="b2cb5-111">*configurations* \[out\] On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="b2cb5-112">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="b2cb5-112">Return value</span></span>

<span data-ttu-id="b2cb5-113">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="b2cb5-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="b2cb5-114">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="b2cb5-114">Remarks</span></span>

<span data-ttu-id="b2cb5-115">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="b2cb5-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="b2cb5-116">Követelmények</span><span class="sxs-lookup"><span data-stu-id="b2cb5-116">Requirements</span></span>

<span data-ttu-id="b2cb5-117">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="b2cb5-117">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="b2cb5-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="b2cb5-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="b2cb5-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b2cb5-119">See also</span></span>

[<span data-ttu-id="b2cb5-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="b2cb5-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)