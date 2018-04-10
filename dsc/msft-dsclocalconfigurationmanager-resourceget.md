---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály ResourceGet metódusa
ms.openlocfilehash: 3fd7ae54eb3ae782156dc4619ee0b6905dfb1212
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="resourceget-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="5d929-103">Az MSFT_DSCLocalConfigurationManager osztály ResourceGet metódusa</span><span class="sxs-lookup"><span data-stu-id="5d929-103">ResourceGet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="5d929-104">Közvetlenül meghívja a **beolvasása** DSC erőforrás metódust.</span><span class="sxs-lookup"><span data-stu-id="5d929-104">Directly calls the **Get** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="5d929-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="5d929-105">Syntax</span></span>
------

```mof
uint32 ResourceGet(
  [in]  string           ResourceType,
  [in]  string           ModuleName,
  [in]  uint8            resourceProperty[],
  [out] OMI_BaseResource configurations
);
```

<a name="parameters"></a><span data-ttu-id="5d929-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="5d929-106">Parameters</span></span>
----------

<span data-ttu-id="5d929-107">*A ResourceType* \[a\] hívni az erőforrás nevét.</span><span class="sxs-lookup"><span data-stu-id="5d929-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="5d929-108">*Modulnév* \[a\] az azt tartalmazó hívni a modul nevét.</span><span class="sxs-lookup"><span data-stu-id="5d929-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="5d929-109">*resourceProperty* \[a\] határozza meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve.</span><span class="sxs-lookup"><span data-stu-id="5d929-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="5d929-110">Használja a [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) parancsmag az erőforrás-tulajdonságok és azok típusát.</span><span class="sxs-lookup"><span data-stu-id="5d929-110">Use the [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="5d929-111">*konfigurációk* \[kimenő\] vissza, tartalmazza a konfigurációk beágyazott példánya.</span><span class="sxs-lookup"><span data-stu-id="5d929-111">*configurations* \[out\] On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="5d929-112">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="5d929-112">Return value</span></span>
------------

<span data-ttu-id="5d929-113">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="5d929-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="5d929-114">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="5d929-114">Remarks</span></span>

<span data-ttu-id="5d929-115">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="5d929-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="5d929-116">Követelmények</span><span class="sxs-lookup"><span data-stu-id="5d929-116">Requirements</span></span>
------------
><span data-ttu-id="5d929-117">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="5d929-117">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="5d929-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="5d929-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="5d929-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5d929-119">See also</span></span>


[<span data-ttu-id="5d929-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="5d929-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)