---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály ResourceSet metódusa
ms.openlocfilehash: 2712b7ff0a19e643c1f343d436c084f8970c9dd4
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404320"
---
# <a name="resourceset-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="6e6e2-103">Az MSFT_DSCLocalConfigurationManager osztály ResourceSet metódusa</span><span class="sxs-lookup"><span data-stu-id="6e6e2-103">ResourceSet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="6e6e2-104">Közvetlenül meghívja a **beállítása** metódus a DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="6e6e2-104">Directly calls the **Set** method of a DSC resource.</span></span>

## <a name="syntax"></a><span data-ttu-id="6e6e2-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="6e6e2-105">Syntax</span></span>

```mof
uint32 ResourceSet(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean RebootRequired
);
```

## <a name="parameters"></a><span data-ttu-id="6e6e2-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="6e6e2-106">Parameters</span></span>

<span data-ttu-id="6e6e2-107">*Erőforrástípus* \[a\] hívja az erőforrás nevét.</span><span class="sxs-lookup"><span data-stu-id="6e6e2-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="6e6e2-108">*ModuleName* \[a\] neve a modul, amely tartalmazza az erőforrás meghívásához.</span><span class="sxs-lookup"><span data-stu-id="6e6e2-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="6e6e2-109">*resourceProperty* \[a\] határozza meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve.</span><span class="sxs-lookup"><span data-stu-id="6e6e2-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="6e6e2-110">Használja a [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) parancsmaggal a erőforrás-tulajdonságok és azok típusát.</span><span class="sxs-lookup"><span data-stu-id="6e6e2-110">Use the [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="6e6e2-111">*RebootRequired* \[ki\] a visszaadandó, ez a tulajdonság értéke **igaz** , ha a cél-csomópont újra kell indítani.</span><span class="sxs-lookup"><span data-stu-id="6e6e2-111">*RebootRequired* \[out\] On return, this property is set to **true** if the target node needs to be rebooted.</span></span>

## <a name="return-value"></a><span data-ttu-id="6e6e2-112">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="6e6e2-112">Return value</span></span>

<span data-ttu-id="6e6e2-113">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="6e6e2-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="6e6e2-114">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="6e6e2-114">Remarks</span></span>

<span data-ttu-id="6e6e2-115">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="6e6e2-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="6e6e2-116">Követelmények</span><span class="sxs-lookup"><span data-stu-id="6e6e2-116">Requirements</span></span>

<span data-ttu-id="6e6e2-117">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="6e6e2-117">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="6e6e2-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="6e6e2-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="6e6e2-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="6e6e2-119">See also</span></span>

[<span data-ttu-id="6e6e2-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="6e6e2-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)