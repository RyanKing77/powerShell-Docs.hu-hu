---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály ResourceTest metódusa
ms.openlocfilehash: 714bbb286ebbe4ed0f1faa15e03ac4b51a3ee87f
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34218858"
---
# <a name="resourcetest-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="59048-103">Az MSFT_DSCLocalConfigurationManager osztály ResourceTest metódusa</span><span class="sxs-lookup"><span data-stu-id="59048-103">ResourceTest method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="59048-104">Közvetlenül meghívja a **teszt** DSC erőforrás metódust.</span><span class="sxs-lookup"><span data-stu-id="59048-104">Directly calls the **Test** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="59048-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="59048-105">Syntax</span></span>
------

```mof
uint32 ResourceTest(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean InDesiredState
);
```

<a name="parameters"></a><span data-ttu-id="59048-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="59048-106">Parameters</span></span>
----------

<span data-ttu-id="59048-107">*A ResourceType* \[a\] hívni az erőforrás nevét.</span><span class="sxs-lookup"><span data-stu-id="59048-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="59048-108">*Modulnév* \[a\] az azt tartalmazó hívni a modul nevét.</span><span class="sxs-lookup"><span data-stu-id="59048-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="59048-109">*resourceProperty* \[a\] határozza meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve.</span><span class="sxs-lookup"><span data-stu-id="59048-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="59048-110">Használja a [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) parancsmag az erőforrás-tulajdonságok és azok típusát.</span><span class="sxs-lookup"><span data-stu-id="59048-110">Use the [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="59048-111">*InDesiredState* \[kimenő\] a return, ez a tulajdonság értéke **igaz** Ha a célcsomópont a megfelelő állapotban van.</span><span class="sxs-lookup"><span data-stu-id="59048-111">*InDesiredState* \[out\] On return, this property is set to **true** if the target node is in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="59048-112">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="59048-112">Return value</span></span>
------------

<span data-ttu-id="59048-113">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="59048-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="59048-114">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="59048-114">Remarks</span></span>

<span data-ttu-id="59048-115">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="59048-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="59048-116">Követelmények</span><span class="sxs-lookup"><span data-stu-id="59048-116">Requirements</span></span>
------------
><span data-ttu-id="59048-117">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="59048-117">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="59048-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="59048-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="59048-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="59048-119">See also</span></span>


[<span data-ttu-id="59048-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="59048-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)