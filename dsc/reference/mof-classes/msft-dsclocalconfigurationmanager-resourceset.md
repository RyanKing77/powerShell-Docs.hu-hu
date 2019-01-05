---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály ResourceSet metódusa
ms.openlocfilehash: 2712b7ff0a19e643c1f343d436c084f8970c9dd4
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048447"
---
# <a name="resourceset-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="67f6d-103">Az MSFT_DSCLocalConfigurationManager osztály ResourceSet metódusa</span><span class="sxs-lookup"><span data-stu-id="67f6d-103">ResourceSet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="67f6d-104">Közvetlenül meghívja a **beállítása** metódus a DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="67f6d-104">Directly calls the **Set** method of a DSC resource.</span></span>

## <a name="syntax"></a><span data-ttu-id="67f6d-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="67f6d-105">Syntax</span></span>

```mof
uint32 ResourceSet(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean RebootRequired
);
```

## <a name="parameters"></a><span data-ttu-id="67f6d-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="67f6d-106">Parameters</span></span>

<span data-ttu-id="67f6d-107">*Erőforrástípus* \[a\] hívja az erőforrás nevét.</span><span class="sxs-lookup"><span data-stu-id="67f6d-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="67f6d-108">*ModuleName* \[a\] neve a modul, amely tartalmazza az erőforrás meghívásához.</span><span class="sxs-lookup"><span data-stu-id="67f6d-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="67f6d-109">*resourceProperty* \[a\] határozza meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve.</span><span class="sxs-lookup"><span data-stu-id="67f6d-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="67f6d-110">Használja a [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) parancsmaggal a erőforrás-tulajdonságok és azok típusát.</span><span class="sxs-lookup"><span data-stu-id="67f6d-110">Use the [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="67f6d-111">*RebootRequired* \[ki\] a visszaadandó, ez a tulajdonság értéke **igaz** , ha a cél-csomópont újra kell indítani.</span><span class="sxs-lookup"><span data-stu-id="67f6d-111">*RebootRequired* \[out\] On return, this property is set to **true** if the target node needs to be rebooted.</span></span>

## <a name="return-value"></a><span data-ttu-id="67f6d-112">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="67f6d-112">Return value</span></span>

<span data-ttu-id="67f6d-113">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="67f6d-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="67f6d-114">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="67f6d-114">Remarks</span></span>

<span data-ttu-id="67f6d-115">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="67f6d-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="67f6d-116">Követelmények</span><span class="sxs-lookup"><span data-stu-id="67f6d-116">Requirements</span></span>

<span data-ttu-id="67f6d-117">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="67f6d-117">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="67f6d-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="67f6d-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="67f6d-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="67f6d-119">See also</span></span>

[<span data-ttu-id="67f6d-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="67f6d-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)