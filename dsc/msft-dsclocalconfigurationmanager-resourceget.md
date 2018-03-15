---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály ResourceGet módszer"
ms.openlocfilehash: 2c055b3fab468f85c9e2f91cf1eaf1a4353b4660
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="resourceget-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="f5361-103">A MSFT_DSCLocalConfigurationManager osztály ResourceGet módszer</span><span class="sxs-lookup"><span data-stu-id="f5361-103">ResourceGet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="f5361-104">Közvetlenül meghívja a **beolvasása** DSC erőforrás metódust.</span><span class="sxs-lookup"><span data-stu-id="f5361-104">Directly calls the **Get** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="f5361-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="f5361-105">Syntax</span></span>
------

```mof
uint32 ResourceGet(
  [in]  string           ResourceType,
  [in]  string           ModuleName,
  [in]  uint8            resourceProperty[],
  [out] OMI_BaseResource configurations
);
```

<a name="parameters"></a><span data-ttu-id="f5361-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="f5361-106">Parameters</span></span>
----------

<span data-ttu-id="f5361-107">*A ResourceType* \[a\]</span><span class="sxs-lookup"><span data-stu-id="f5361-107">*ResourceType* \[in\]</span></span>  
<span data-ttu-id="f5361-108">Hívása az erőforrás neve.</span><span class="sxs-lookup"><span data-stu-id="f5361-108">The name of the resource to call.</span></span>

<span data-ttu-id="f5361-109">*Modulnév* \[a\]</span><span class="sxs-lookup"><span data-stu-id="f5361-109">*ModuleName* \[in\]</span></span>  
<span data-ttu-id="f5361-110">A modul, amely tartalmazza a hívni az erőforrás neve.</span><span class="sxs-lookup"><span data-stu-id="f5361-110">The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="f5361-111">*resourceProperty* \[a\]</span><span class="sxs-lookup"><span data-stu-id="f5361-111">*resourceProperty* \[in\]</span></span>  
<span data-ttu-id="f5361-112">Adja meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve.</span><span class="sxs-lookup"><span data-stu-id="f5361-112">Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="f5361-113">Használja a [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) parancsmag az erőforrás-tulajdonságok és azok típusát.</span><span class="sxs-lookup"><span data-stu-id="f5361-113">Use the [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="f5361-114">*konfigurációk* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="f5361-114">*configurations* \[out\]</span></span>  
<span data-ttu-id="f5361-115">Térjen vissza tartalmazza a konfigurációk beágyazott példánya.</span><span class="sxs-lookup"><span data-stu-id="f5361-115">On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="f5361-116">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="f5361-116">Return value</span></span>
------------

<span data-ttu-id="f5361-117">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="f5361-117">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="f5361-118">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="f5361-118">Remarks</span></span>

<span data-ttu-id="f5361-119">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="f5361-119">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="f5361-120">Követelmények</span><span class="sxs-lookup"><span data-stu-id="f5361-120">Requirements</span></span>
------------
><span data-ttu-id="f5361-121">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="f5361-121">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="f5361-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="f5361-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="f5361-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="f5361-123">See also</span></span>


[<span data-ttu-id="f5361-124">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="f5361-124">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



