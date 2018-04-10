---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály ResourceTest metódusa
ms.openlocfilehash: f03a034329a9cde5cd44dbaf42ba1789c2b8f4f9
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="resourcetest-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="73f3e-103">Az MSFT_DSCLocalConfigurationManager osztály ResourceTest metódusa</span><span class="sxs-lookup"><span data-stu-id="73f3e-103">ResourceTest method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="73f3e-104">Közvetlenül meghívja a **teszt** DSC erőforrás metódust.</span><span class="sxs-lookup"><span data-stu-id="73f3e-104">Directly calls the **Test** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="73f3e-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="73f3e-105">Syntax</span></span>
------

```mof
uint32 ResourceTest(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean InDesiredState
);
```

<a name="parameters"></a><span data-ttu-id="73f3e-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="73f3e-106">Parameters</span></span>
----------

<span data-ttu-id="73f3e-107">*A ResourceType* \[a\] hívni az erőforrás nevét.</span><span class="sxs-lookup"><span data-stu-id="73f3e-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="73f3e-108">*Modulnév* \[a\] az azt tartalmazó hívni a modul nevét.</span><span class="sxs-lookup"><span data-stu-id="73f3e-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="73f3e-109">*resourceProperty* \[a\] határozza meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve.</span><span class="sxs-lookup"><span data-stu-id="73f3e-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="73f3e-110">Használja a [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) parancsmag az erőforrás-tulajdonságok és azok típusát.</span><span class="sxs-lookup"><span data-stu-id="73f3e-110">Use the [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="73f3e-111">*InDesiredState* \[kimenő\] a return, ez a tulajdonság értéke **igaz** Ha a célcsomópont a megfelelő állapotban van.</span><span class="sxs-lookup"><span data-stu-id="73f3e-111">*InDesiredState* \[out\] On return, this property is set to **true** if the target node is in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="73f3e-112">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="73f3e-112">Return value</span></span>
------------

<span data-ttu-id="73f3e-113">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="73f3e-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="73f3e-114">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="73f3e-114">Remarks</span></span>

<span data-ttu-id="73f3e-115">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="73f3e-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="73f3e-116">Követelmények</span><span class="sxs-lookup"><span data-stu-id="73f3e-116">Requirements</span></span>
------------
><span data-ttu-id="73f3e-117">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="73f3e-117">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="73f3e-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="73f3e-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="73f3e-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="73f3e-119">See also</span></span>


[<span data-ttu-id="73f3e-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="73f3e-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)