---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály ResourceGet metódusa
ms.openlocfilehash: 1b74adf2327af2e0f9416f1d00eac4e3b75e9013
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687747"
---
# <a name="resourceget-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="b1d7c-103">Az MSFT_DSCLocalConfigurationManager osztály ResourceGet metódusa</span><span class="sxs-lookup"><span data-stu-id="b1d7c-103">ResourceGet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="b1d7c-104">Közvetlenül meghívja a **első** metódus a DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="b1d7c-104">Directly calls the **Get** method of a DSC resource.</span></span>

## <a name="syntax"></a><span data-ttu-id="b1d7c-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="b1d7c-105">Syntax</span></span>

```mof
uint32 ResourceGet(
  [in]  string           ResourceType,
  [in]  string           ModuleName,
  [in]  uint8            resourceProperty[],
  [out] OMI_BaseResource configurations
);
```

## <a name="parameters"></a><span data-ttu-id="b1d7c-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="b1d7c-106">Parameters</span></span>

<span data-ttu-id="b1d7c-107">*Erőforrástípus* \[a\] hívja az erőforrás nevét.</span><span class="sxs-lookup"><span data-stu-id="b1d7c-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="b1d7c-108">*ModuleName* \[a\] neve a modul, amely tartalmazza az erőforrás meghívásához.</span><span class="sxs-lookup"><span data-stu-id="b1d7c-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="b1d7c-109">*resourceProperty* \[a\] határozza meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve.</span><span class="sxs-lookup"><span data-stu-id="b1d7c-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="b1d7c-110">Használja a [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) parancsmaggal a erőforrás-tulajdonságok és azok típusát.</span><span class="sxs-lookup"><span data-stu-id="b1d7c-110">Use the [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="b1d7c-111">*konfigurációk* \[ki\] lépjen vissza, tartalmazza a konfigurációkat egy beágyazott példányát.</span><span class="sxs-lookup"><span data-stu-id="b1d7c-111">*configurations* \[out\] On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="b1d7c-112">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="b1d7c-112">Return value</span></span>

<span data-ttu-id="b1d7c-113">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="b1d7c-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="b1d7c-114">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="b1d7c-114">Remarks</span></span>

<span data-ttu-id="b1d7c-115">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="b1d7c-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="b1d7c-116">Követelmények</span><span class="sxs-lookup"><span data-stu-id="b1d7c-116">Requirements</span></span>

<span data-ttu-id="b1d7c-117">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="b1d7c-117">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="b1d7c-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="b1d7c-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="b1d7c-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b1d7c-119">See also</span></span>

[<span data-ttu-id="b1d7c-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="b1d7c-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)