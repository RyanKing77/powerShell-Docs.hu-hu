---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály ResourceGet módszer"
ms.openlocfilehash: df90cb6859413c94be992c8cbc30171e9bd3d6de
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="resourceget-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="4c4f4-103">A MSFT_DSCLocalConfigurationManager osztály ResourceGet módszer</span><span class="sxs-lookup"><span data-stu-id="4c4f4-103">ResourceGet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="4c4f4-104">Közvetlenül meghívja a **beolvasása** DSC erőforrás metódust.</span><span class="sxs-lookup"><span data-stu-id="4c4f4-104">Directly calls the **Get** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="4c4f4-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="4c4f4-105">Syntax</span></span>
------

```mof
uint32 ResourceGet(
  [in]  string           ResourceType,
  [in]  string           ModuleName,
  [in]  uint8            resourceProperty[],
  [out] OMI_BaseResource configurations
);
```

<a name="parameters"></a><span data-ttu-id="4c4f4-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="4c4f4-106">Parameters</span></span>
----------

<span data-ttu-id="4c4f4-107">*A ResourceType* \[a\]</span><span class="sxs-lookup"><span data-stu-id="4c4f4-107">*ResourceType* \[in\]</span></span>  
<span data-ttu-id="4c4f4-108">Hívása az erőforrás neve.</span><span class="sxs-lookup"><span data-stu-id="4c4f4-108">The name of the resource to call.</span></span>

<span data-ttu-id="4c4f4-109">*Modulnév* \[a\]</span><span class="sxs-lookup"><span data-stu-id="4c4f4-109">*ModuleName* \[in\]</span></span>  
<span data-ttu-id="4c4f4-110">A modul, amely tartalmazza a hívni az erőforrás neve.</span><span class="sxs-lookup"><span data-stu-id="4c4f4-110">The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="4c4f4-111">*resourceProperty* \[a\]</span><span class="sxs-lookup"><span data-stu-id="4c4f4-111">*resourceProperty* \[in\]</span></span>  
<span data-ttu-id="4c4f4-112">Adja meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve.</span><span class="sxs-lookup"><span data-stu-id="4c4f4-112">Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="4c4f4-113">Használja a [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) parancsmag az erőforrás-tulajdonságok és azok típusát.</span><span class="sxs-lookup"><span data-stu-id="4c4f4-113">Use the [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="4c4f4-114">*konfigurációk* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="4c4f4-114">*configurations* \[out\]</span></span>  
<span data-ttu-id="4c4f4-115">Térjen vissza tartalmazza a konfigurációk beágyazott példánya.</span><span class="sxs-lookup"><span data-stu-id="4c4f4-115">On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="4c4f4-116">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="4c4f4-116">Return value</span></span>
------------

<span data-ttu-id="4c4f4-117">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="4c4f4-117">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="4c4f4-118">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="4c4f4-118">Remarks</span></span>

<span data-ttu-id="4c4f4-119">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="4c4f4-119">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="4c4f4-120">Követelmények</span><span class="sxs-lookup"><span data-stu-id="4c4f4-120">Requirements</span></span>
------------
><span data-ttu-id="4c4f4-121">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="4c4f4-121">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="4c4f4-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="4c4f4-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="4c4f4-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="4c4f4-123">See also</span></span>


[<span data-ttu-id="4c4f4-124">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="4c4f4-124">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



