---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály ResourceSet metódusa
ms.openlocfilehash: 0c9c1d33117067d76d61036d5839f0b676eb4a97
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="resourceset-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="95568-103">Az MSFT_DSCLocalConfigurationManager osztály ResourceSet metódusa</span><span class="sxs-lookup"><span data-stu-id="95568-103">ResourceSet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="95568-104">Közvetlenül meghívja a **beállítása** DSC erőforrás metódust.</span><span class="sxs-lookup"><span data-stu-id="95568-104">Directly calls the **Set** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="95568-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="95568-105">Syntax</span></span>
------

```mof
uint32 ResourceSet(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean RebootRequired
);
```

<a name="parameters"></a><span data-ttu-id="95568-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="95568-106">Parameters</span></span>
----------

<span data-ttu-id="95568-107">*A ResourceType* \[a\] hívni az erőforrás nevét.</span><span class="sxs-lookup"><span data-stu-id="95568-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="95568-108">*Modulnév* \[a\] az azt tartalmazó hívni a modul nevét.</span><span class="sxs-lookup"><span data-stu-id="95568-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="95568-109">*resourceProperty* \[a\] határozza meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve.</span><span class="sxs-lookup"><span data-stu-id="95568-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="95568-110">Használja a [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) parancsmag az erőforrás-tulajdonságok és azok típusát.</span><span class="sxs-lookup"><span data-stu-id="95568-110">Use the [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="95568-111">*RebootRequired* \[kimenő\] a return, ez a tulajdonság értéke **igaz** Ha célcsomóponton újra kell indítani.</span><span class="sxs-lookup"><span data-stu-id="95568-111">*RebootRequired* \[out\] On return, this property is set to **true** if the target node needs to be rebooted.</span></span>

## <a name="return-value"></a><span data-ttu-id="95568-112">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="95568-112">Return value</span></span>
------------

<span data-ttu-id="95568-113">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="95568-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="95568-114">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="95568-114">Remarks</span></span>

<span data-ttu-id="95568-115">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="95568-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="95568-116">Követelmények</span><span class="sxs-lookup"><span data-stu-id="95568-116">Requirements</span></span>
------------
><span data-ttu-id="95568-117">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="95568-117">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="95568-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="95568-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="95568-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="95568-119">See also</span></span>


[<span data-ttu-id="95568-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="95568-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)