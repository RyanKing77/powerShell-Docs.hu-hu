---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály ResourceGet metódusa
ms.openlocfilehash: 30cbaa907d4dc3a921c9e5fe61ffddc5d61c2347
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34187867"
---
# <a name="resourceget-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="bb1f4-103">Az MSFT_DSCLocalConfigurationManager osztály ResourceGet metódusa</span><span class="sxs-lookup"><span data-stu-id="bb1f4-103">ResourceGet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="bb1f4-104">Közvetlenül meghívja a **beolvasása** DSC erőforrás metódust.</span><span class="sxs-lookup"><span data-stu-id="bb1f4-104">Directly calls the **Get** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="bb1f4-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="bb1f4-105">Syntax</span></span>
------

```mof
uint32 ResourceGet(
  [in]  string           ResourceType,
  [in]  string           ModuleName,
  [in]  uint8            resourceProperty[],
  [out] OMI_BaseResource configurations
);
```

<a name="parameters"></a><span data-ttu-id="bb1f4-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="bb1f4-106">Parameters</span></span>
----------

<span data-ttu-id="bb1f4-107">*A ResourceType* \[a\] hívni az erőforrás nevét.</span><span class="sxs-lookup"><span data-stu-id="bb1f4-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="bb1f4-108">*Modulnév* \[a\] az azt tartalmazó hívni a modul nevét.</span><span class="sxs-lookup"><span data-stu-id="bb1f4-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="bb1f4-109">*resourceProperty* \[a\] határozza meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve.</span><span class="sxs-lookup"><span data-stu-id="bb1f4-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="bb1f4-110">Használja a [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) parancsmag az erőforrás-tulajdonságok és azok típusát.</span><span class="sxs-lookup"><span data-stu-id="bb1f4-110">Use the [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="bb1f4-111">*konfigurációk* \[kimenő\] vissza, tartalmazza a konfigurációk beágyazott példánya.</span><span class="sxs-lookup"><span data-stu-id="bb1f4-111">*configurations* \[out\] On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="bb1f4-112">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="bb1f4-112">Return value</span></span>
------------

<span data-ttu-id="bb1f4-113">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="bb1f4-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="bb1f4-114">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="bb1f4-114">Remarks</span></span>

<span data-ttu-id="bb1f4-115">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="bb1f4-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="bb1f4-116">Követelmények</span><span class="sxs-lookup"><span data-stu-id="bb1f4-116">Requirements</span></span>
------------
><span data-ttu-id="bb1f4-117">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="bb1f4-117">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="bb1f4-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="bb1f4-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="bb1f4-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="bb1f4-119">See also</span></span>


[<span data-ttu-id="bb1f4-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="bb1f4-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)