---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály ResourceSet módszer"
ms.openlocfilehash: 3486ef559102929f8d05994a4bf6e45d49a0c140
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="resourceset-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="93bd0-103">A MSFT_DSCLocalConfigurationManager osztály ResourceSet módszer</span><span class="sxs-lookup"><span data-stu-id="93bd0-103">ResourceSet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="93bd0-104">Közvetlenül meghívja a **beállítása** DSC erőforrás metódust.</span><span class="sxs-lookup"><span data-stu-id="93bd0-104">Directly calls the **Set** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="93bd0-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="93bd0-105">Syntax</span></span>
------

```mof
uint32 ResourceSet(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean RebootRequired
);
```

<a name="parameters"></a><span data-ttu-id="93bd0-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="93bd0-106">Parameters</span></span>
----------

<span data-ttu-id="93bd0-107">*A ResourceType* \[a\]</span><span class="sxs-lookup"><span data-stu-id="93bd0-107">*ResourceType* \[in\]</span></span>  
<span data-ttu-id="93bd0-108">Hívása az erőforrás neve.</span><span class="sxs-lookup"><span data-stu-id="93bd0-108">The name of the resource to call.</span></span>

<span data-ttu-id="93bd0-109">*Modulnév* \[a\]</span><span class="sxs-lookup"><span data-stu-id="93bd0-109">*ModuleName* \[in\]</span></span>  
<span data-ttu-id="93bd0-110">A modul, amely tartalmazza a hívni az erőforrás neve.</span><span class="sxs-lookup"><span data-stu-id="93bd0-110">The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="93bd0-111">*resourceProperty* \[a\]</span><span class="sxs-lookup"><span data-stu-id="93bd0-111">*resourceProperty* \[in\]</span></span>  
<span data-ttu-id="93bd0-112">Adja meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve.</span><span class="sxs-lookup"><span data-stu-id="93bd0-112">Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="93bd0-113">Használja a [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) parancsmag az erőforrás-tulajdonságok és azok típusát.</span><span class="sxs-lookup"><span data-stu-id="93bd0-113">Use the [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="93bd0-114">*RebootRequired* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="93bd0-114">*RebootRequired* \[out\]</span></span>  
<span data-ttu-id="93bd0-115">A return, ez a tulajdonság értéke **igaz** Ha célcsomóponton újra kell indítani.</span><span class="sxs-lookup"><span data-stu-id="93bd0-115">On return, this property is set to **true** if the target node needs to be rebooted.</span></span>

## <a name="return-value"></a><span data-ttu-id="93bd0-116">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="93bd0-116">Return value</span></span>
------------

<span data-ttu-id="93bd0-117">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="93bd0-117">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="93bd0-118">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="93bd0-118">Remarks</span></span>

<span data-ttu-id="93bd0-119">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="93bd0-119">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="93bd0-120">Követelmények</span><span class="sxs-lookup"><span data-stu-id="93bd0-120">Requirements</span></span>
------------
><span data-ttu-id="93bd0-121">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="93bd0-121">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="93bd0-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="93bd0-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="93bd0-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="93bd0-123">See also</span></span>


[<span data-ttu-id="93bd0-124">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="93bd0-124">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)

 

 



