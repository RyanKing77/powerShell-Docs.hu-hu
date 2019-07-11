---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: ResourceTest metódusa
ms.openlocfilehash: ff06fd645a94055e79aa0f8d20f2f06e16483720
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727070"
---
# <a name="resourcetest-method"></a><span data-ttu-id="28e01-103">ResourceTest metódusa</span><span class="sxs-lookup"><span data-stu-id="28e01-103">ResourceTest method</span></span>

<span data-ttu-id="28e01-104">Közvetlenül meghívja a **teszt** metódus a DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="28e01-104">Directly calls the **Test** method of a DSC resource.</span></span>

## <a name="syntax"></a><span data-ttu-id="28e01-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="28e01-105">Syntax</span></span>

```mof
uint32 ResourceTest(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean InDesiredState
);
```

## <a name="parameters"></a><span data-ttu-id="28e01-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="28e01-106">Parameters</span></span>

<span data-ttu-id="28e01-107">*Erőforrástípus* \[a\] hívja az erőforrás nevét.</span><span class="sxs-lookup"><span data-stu-id="28e01-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="28e01-108">*ModuleName* \[a\] neve a modul, amely tartalmazza az erőforrás meghívásához.</span><span class="sxs-lookup"><span data-stu-id="28e01-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="28e01-109">*resourceProperty* \[a\] határozza meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve.</span><span class="sxs-lookup"><span data-stu-id="28e01-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="28e01-110">Használja a [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) parancsmaggal a erőforrás-tulajdonságok és azok típusát.</span><span class="sxs-lookup"><span data-stu-id="28e01-110">Use the [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="28e01-111">*InDesiredState* \[ki\] a visszaadandó, ez a tulajdonság értéke **igaz** Ha a célcsomópont a kívánt állapotban van.</span><span class="sxs-lookup"><span data-stu-id="28e01-111">*InDesiredState* \[out\] On return, this property is set to **true** if the target node is in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="28e01-112">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="28e01-112">Return value</span></span>

<span data-ttu-id="28e01-113">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="28e01-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="28e01-114">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="28e01-114">Remarks</span></span>

<span data-ttu-id="28e01-115">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="28e01-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="28e01-116">Követelmények</span><span class="sxs-lookup"><span data-stu-id="28e01-116">Requirements</span></span>

<span data-ttu-id="28e01-117">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="28e01-117">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="28e01-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="28e01-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="28e01-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="28e01-119">See also</span></span>

[<span data-ttu-id="28e01-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="28e01-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
