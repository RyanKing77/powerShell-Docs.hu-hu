---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály ResourceTest módszer"
ms.openlocfilehash: 3c88f74c5f623502e8cbe0d7aa7390fca75569a9
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="resourcetest-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="a1986-103">A MSFT_DSCLocalConfigurationManager osztály ResourceTest módszer</span><span class="sxs-lookup"><span data-stu-id="a1986-103">ResourceTest method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="a1986-104">Közvetlenül meghívja a **teszt** DSC erőforrás metódust.</span><span class="sxs-lookup"><span data-stu-id="a1986-104">Directly calls the **Test** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="a1986-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="a1986-105">Syntax</span></span>
------

```mof
uint32 ResourceTest(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean InDesiredState
);
```

<a name="parameters"></a><span data-ttu-id="a1986-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="a1986-106">Parameters</span></span>
----------

<span data-ttu-id="a1986-107">*A ResourceType* \[a\]</span><span class="sxs-lookup"><span data-stu-id="a1986-107">*ResourceType* \[in\]</span></span>  
<span data-ttu-id="a1986-108">Hívása az erőforrás neve.</span><span class="sxs-lookup"><span data-stu-id="a1986-108">The name of the resource to call.</span></span>

<span data-ttu-id="a1986-109">*Modulnév* \[a\]</span><span class="sxs-lookup"><span data-stu-id="a1986-109">*ModuleName* \[in\]</span></span>  
<span data-ttu-id="a1986-110">A modul, amely tartalmazza a hívni az erőforrás neve.</span><span class="sxs-lookup"><span data-stu-id="a1986-110">The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="a1986-111">*resourceProperty* \[a\]</span><span class="sxs-lookup"><span data-stu-id="a1986-111">*resourceProperty* \[in\]</span></span>  
<span data-ttu-id="a1986-112">Adja meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve.</span><span class="sxs-lookup"><span data-stu-id="a1986-112">Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="a1986-113">Használja a [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) parancsmag az erőforrás-tulajdonságok és azok típusát.</span><span class="sxs-lookup"><span data-stu-id="a1986-113">Use the [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="a1986-114">*InDesiredState* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="a1986-114">*InDesiredState* \[out\]</span></span>  
<span data-ttu-id="a1986-115">A return, ez a tulajdonság értéke **igaz** Ha a célcsomópont a megfelelő állapotban van.</span><span class="sxs-lookup"><span data-stu-id="a1986-115">On return, this property is set to **true** if the target node is in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="a1986-116">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="a1986-116">Return value</span></span>
------------

<span data-ttu-id="a1986-117">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="a1986-117">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="a1986-118">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="a1986-118">Remarks</span></span>

<span data-ttu-id="a1986-119">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="a1986-119">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="a1986-120">Követelmények</span><span class="sxs-lookup"><span data-stu-id="a1986-120">Requirements</span></span>
------------
><span data-ttu-id="a1986-121">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="a1986-121">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="a1986-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="a1986-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="a1986-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="a1986-123">See also</span></span>


[<span data-ttu-id="a1986-124">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="a1986-124">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



