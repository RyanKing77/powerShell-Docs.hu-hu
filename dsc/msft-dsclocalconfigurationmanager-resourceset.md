---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály ResourceSet módszer"
ms.openlocfilehash: 9cd9c1b3f58a5862db6c4eea0488423b8dfe7310
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="resourceset-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="598bb-103">A MSFT_DSCLocalConfigurationManager osztály ResourceSet módszer</span><span class="sxs-lookup"><span data-stu-id="598bb-103">ResourceSet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="598bb-104">Közvetlenül meghívja a **beállítása** DSC erőforrás metódust.</span><span class="sxs-lookup"><span data-stu-id="598bb-104">Directly calls the **Set** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="598bb-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="598bb-105">Syntax</span></span>
------

```mof
uint32 ResourceSet(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean RebootRequired
);
```

<a name="parameters"></a><span data-ttu-id="598bb-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="598bb-106">Parameters</span></span>
----------

<span data-ttu-id="598bb-107">*A ResourceType* \[a\]</span><span class="sxs-lookup"><span data-stu-id="598bb-107">*ResourceType* \[in\]</span></span>  
<span data-ttu-id="598bb-108">Hívása az erőforrás neve.</span><span class="sxs-lookup"><span data-stu-id="598bb-108">The name of the resource to call.</span></span>

<span data-ttu-id="598bb-109">*Modulnév* \[a\]</span><span class="sxs-lookup"><span data-stu-id="598bb-109">*ModuleName* \[in\]</span></span>  
<span data-ttu-id="598bb-110">A modul, amely tartalmazza a hívni az erőforrás neve.</span><span class="sxs-lookup"><span data-stu-id="598bb-110">The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="598bb-111">*resourceProperty* \[a\]</span><span class="sxs-lookup"><span data-stu-id="598bb-111">*resourceProperty* \[in\]</span></span>  
<span data-ttu-id="598bb-112">Adja meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve.</span><span class="sxs-lookup"><span data-stu-id="598bb-112">Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="598bb-113">Használja a [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) parancsmag az erőforrás-tulajdonságok és azok típusát.</span><span class="sxs-lookup"><span data-stu-id="598bb-113">Use the [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="598bb-114">*RebootRequired* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="598bb-114">*RebootRequired* \[out\]</span></span>  
<span data-ttu-id="598bb-115">A return, ez a tulajdonság értéke **igaz** Ha célcsomóponton újra kell indítani.</span><span class="sxs-lookup"><span data-stu-id="598bb-115">On return, this property is set to **true** if the target node needs to be rebooted.</span></span>

## <a name="return-value"></a><span data-ttu-id="598bb-116">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="598bb-116">Return value</span></span>
------------

<span data-ttu-id="598bb-117">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="598bb-117">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="598bb-118">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="598bb-118">Remarks</span></span>

<span data-ttu-id="598bb-119">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="598bb-119">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="598bb-120">Követelmények</span><span class="sxs-lookup"><span data-stu-id="598bb-120">Requirements</span></span>
------------
><span data-ttu-id="598bb-121">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="598bb-121">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="598bb-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="598bb-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="598bb-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="598bb-123">See also</span></span>


[<span data-ttu-id="598bb-124">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="598bb-124">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)

 

 



