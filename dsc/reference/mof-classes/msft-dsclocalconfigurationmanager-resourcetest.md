---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály ResourceTest metódusa
ms.openlocfilehash: e7645b0c6b93b96cb01f72c1c92d468f7642ea13
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048462"
---
# <a name="resourcetest-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="34891-103">Az MSFT_DSCLocalConfigurationManager osztály ResourceTest metódusa</span><span class="sxs-lookup"><span data-stu-id="34891-103">ResourceTest method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="34891-104">Közvetlenül meghívja a **teszt** metódus a DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="34891-104">Directly calls the **Test** method of a DSC resource.</span></span>

## <a name="syntax"></a><span data-ttu-id="34891-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="34891-105">Syntax</span></span>

```mof
uint32 ResourceTest(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean InDesiredState
);
```

## <a name="parameters"></a><span data-ttu-id="34891-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="34891-106">Parameters</span></span>

<span data-ttu-id="34891-107">*Erőforrástípus* \[a\] hívja az erőforrás nevét.</span><span class="sxs-lookup"><span data-stu-id="34891-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="34891-108">*ModuleName* \[a\] neve a modul, amely tartalmazza az erőforrás meghívásához.</span><span class="sxs-lookup"><span data-stu-id="34891-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="34891-109">*resourceProperty* \[a\] határozza meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve.</span><span class="sxs-lookup"><span data-stu-id="34891-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="34891-110">Használja a [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) parancsmaggal a erőforrás-tulajdonságok és azok típusát.</span><span class="sxs-lookup"><span data-stu-id="34891-110">Use the [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="34891-111">*InDesiredState* \[ki\] a visszaadandó, ez a tulajdonság értéke **igaz** Ha a célcsomópont a kívánt állapotban van.</span><span class="sxs-lookup"><span data-stu-id="34891-111">*InDesiredState* \[out\] On return, this property is set to **true** if the target node is in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="34891-112">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="34891-112">Return value</span></span>

<span data-ttu-id="34891-113">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="34891-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="34891-114">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="34891-114">Remarks</span></span>

<span data-ttu-id="34891-115">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="34891-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="34891-116">Követelmények</span><span class="sxs-lookup"><span data-stu-id="34891-116">Requirements</span></span>

<span data-ttu-id="34891-117">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="34891-117">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="34891-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="34891-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="34891-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="34891-119">See also</span></span>

[<span data-ttu-id="34891-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="34891-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)