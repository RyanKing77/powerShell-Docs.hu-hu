---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály ResourceTest módszer"
ms.openlocfilehash: 73d7d543505a3768a0660084345d3858e055514f
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="resourcetest-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="5f7ac-103">A MSFT_DSCLocalConfigurationManager osztály ResourceTest módszer</span><span class="sxs-lookup"><span data-stu-id="5f7ac-103">ResourceTest method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="5f7ac-104">Közvetlenül meghívja a **teszt** DSC erőforrás metódust.</span><span class="sxs-lookup"><span data-stu-id="5f7ac-104">Directly calls the **Test** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="5f7ac-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="5f7ac-105">Syntax</span></span>
------

```mof
uint32 ResourceTest(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean InDesiredState
);
```

<a name="parameters"></a><span data-ttu-id="5f7ac-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="5f7ac-106">Parameters</span></span>
----------

<span data-ttu-id="5f7ac-107">*A ResourceType* \[a\]</span><span class="sxs-lookup"><span data-stu-id="5f7ac-107">*ResourceType* \[in\]</span></span>  
<span data-ttu-id="5f7ac-108">Hívása az erőforrás neve.</span><span class="sxs-lookup"><span data-stu-id="5f7ac-108">The name of the resource to call.</span></span>

<span data-ttu-id="5f7ac-109">*Modulnév* \[a\]</span><span class="sxs-lookup"><span data-stu-id="5f7ac-109">*ModuleName* \[in\]</span></span>  
<span data-ttu-id="5f7ac-110">A modul, amely tartalmazza a hívni az erőforrás neve.</span><span class="sxs-lookup"><span data-stu-id="5f7ac-110">The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="5f7ac-111">*resourceProperty* \[a\]</span><span class="sxs-lookup"><span data-stu-id="5f7ac-111">*resourceProperty* \[in\]</span></span>  
<span data-ttu-id="5f7ac-112">Adja meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve.</span><span class="sxs-lookup"><span data-stu-id="5f7ac-112">Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="5f7ac-113">Használja a [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) parancsmag az erőforrás-tulajdonságok és azok típusát.</span><span class="sxs-lookup"><span data-stu-id="5f7ac-113">Use the [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="5f7ac-114">*InDesiredState* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="5f7ac-114">*InDesiredState* \[out\]</span></span>  
<span data-ttu-id="5f7ac-115">A return, ez a tulajdonság értéke **igaz** Ha a célcsomópont a megfelelő állapotban van.</span><span class="sxs-lookup"><span data-stu-id="5f7ac-115">On return, this property is set to **true** if the target node is in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="5f7ac-116">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="5f7ac-116">Return value</span></span>
------------

<span data-ttu-id="5f7ac-117">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="5f7ac-117">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="5f7ac-118">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="5f7ac-118">Remarks</span></span>

<span data-ttu-id="5f7ac-119">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="5f7ac-119">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="5f7ac-120">Követelmények</span><span class="sxs-lookup"><span data-stu-id="5f7ac-120">Requirements</span></span>
------------
><span data-ttu-id="5f7ac-121">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="5f7ac-121">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="5f7ac-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="5f7ac-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="5f7ac-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5f7ac-123">See also</span></span>


[<span data-ttu-id="5f7ac-124">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="5f7ac-124">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



