---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: ResourceSet metódusa
ms.openlocfilehash: 18364027b249e502e1f0b8802d9f3e031c7b07ce
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727091"
---
# <a name="resourceset-method"></a><span data-ttu-id="3dc8f-103">ResourceSet metódusa</span><span class="sxs-lookup"><span data-stu-id="3dc8f-103">ResourceSet method</span></span>

<span data-ttu-id="3dc8f-104">Közvetlenül meghívja a **beállítása** metódus a DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="3dc8f-104">Directly calls the **Set** method of a DSC resource.</span></span>

## <a name="syntax"></a><span data-ttu-id="3dc8f-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="3dc8f-105">Syntax</span></span>

```mof
uint32 ResourceSet(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean RebootRequired
);
```

## <a name="parameters"></a><span data-ttu-id="3dc8f-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="3dc8f-106">Parameters</span></span>

<span data-ttu-id="3dc8f-107">*Erőforrástípus* \[a\] hívja az erőforrás nevét.</span><span class="sxs-lookup"><span data-stu-id="3dc8f-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="3dc8f-108">*ModuleName* \[a\] neve a modul, amely tartalmazza az erőforrás meghívásához.</span><span class="sxs-lookup"><span data-stu-id="3dc8f-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="3dc8f-109">*resourceProperty* \[a\] határozza meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve.</span><span class="sxs-lookup"><span data-stu-id="3dc8f-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="3dc8f-110">Használja a [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) parancsmaggal a erőforrás-tulajdonságok és azok típusát.</span><span class="sxs-lookup"><span data-stu-id="3dc8f-110">Use the [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="3dc8f-111">*RebootRequired* \[ki\] a visszaadandó, ez a tulajdonság értéke **igaz** , ha a cél-csomópont újra kell indítani.</span><span class="sxs-lookup"><span data-stu-id="3dc8f-111">*RebootRequired* \[out\] On return, this property is set to **true** if the target node needs to be rebooted.</span></span>

## <a name="return-value"></a><span data-ttu-id="3dc8f-112">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="3dc8f-112">Return value</span></span>

<span data-ttu-id="3dc8f-113">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="3dc8f-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="3dc8f-114">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="3dc8f-114">Remarks</span></span>

<span data-ttu-id="3dc8f-115">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="3dc8f-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="3dc8f-116">Követelmények</span><span class="sxs-lookup"><span data-stu-id="3dc8f-116">Requirements</span></span>

<span data-ttu-id="3dc8f-117">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="3dc8f-117">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="3dc8f-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="3dc8f-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="3dc8f-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="3dc8f-119">See also</span></span>

[<span data-ttu-id="3dc8f-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="3dc8f-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
