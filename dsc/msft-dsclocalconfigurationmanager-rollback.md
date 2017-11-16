---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Visszaállítás metódus MSFT_DSCLocalConfigurationManager osztály"
ms.openlocfilehash: b8597e3eb7872d9894863fb02d927c9f475da44c
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="rollback-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="624ef-103">Visszaállítás metódus MSFT_DSCLocalConfigurationManager osztály</span><span class="sxs-lookup"><span data-stu-id="624ef-103">RollBack method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="624ef-104">Visszaállítja a konfigurációt egy korábbi verzióját.</span><span class="sxs-lookup"><span data-stu-id="624ef-104">Rolls back the configuration to a previous version.</span></span>

<a name="syntax"></a><span data-ttu-id="624ef-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="624ef-105">Syntax</span></span>
------

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

<a name="parameters"></a><span data-ttu-id="624ef-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="624ef-106">Parameters</span></span>
----------

<span data-ttu-id="624ef-107">*configurationNumber* \[a\]</span><span class="sxs-lookup"><span data-stu-id="624ef-107">*configurationNumber* \[in\]</span></span>  
<span data-ttu-id="624ef-108">Adja meg a kívánt konfigurációját.</span><span class="sxs-lookup"><span data-stu-id="624ef-108">Specifies the requested configuration.</span></span> 

## <a name="return-value"></a><span data-ttu-id="624ef-109">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="624ef-109">Return value</span></span>
------------

<span data-ttu-id="624ef-110">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="624ef-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="624ef-111">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="624ef-111">Remarks</span></span>

<span data-ttu-id="624ef-112">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="624ef-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="624ef-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="624ef-113">Requirements</span></span>
------------
><span data-ttu-id="624ef-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="624ef-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="624ef-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="624ef-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="624ef-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="624ef-116">See also</span></span>


[<span data-ttu-id="624ef-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="624ef-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



