---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály GetMetaConfiguration módszer"
ms.openlocfilehash: 695be4ee6490567295fda0cc44635870362d24b8
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="getmetaconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="6045d-103">A MSFT_DSCLocalConfigurationManager osztály GetMetaConfiguration módszer</span><span class="sxs-lookup"><span data-stu-id="6045d-103">GetMetaConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="6045d-104">A helyi Configuration Manager-beállításainak konfigurálása ügynök használt beolvasása.</span><span class="sxs-lookup"><span data-stu-id="6045d-104">Gets the local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

<a name="syntax"></a><span data-ttu-id="6045d-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="6045d-105">Syntax</span></span>
------

```mof
uint32 GetMetaConfiguration(
  [out] MSFT_DSCMetaConfiguration MetaConfiguration
);
```

<a name="parameters"></a><span data-ttu-id="6045d-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="6045d-106">Parameters</span></span>
----------

<span data-ttu-id="6045d-107">*Metakonfigurációját* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="6045d-107">*MetaConfiguration* \[out\]</span></span>  
<span data-ttu-id="6045d-108">A visszatérési, tartalmazza a beágyazott példányának a **MSFT_DSCMetaConfiguration** osztály, amely meghatározza a beállításokat.</span><span class="sxs-lookup"><span data-stu-id="6045d-108">On return, contains an embedded instance of the **MSFT_DSCMetaConfiguration** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="6045d-109">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="6045d-109">Return value</span></span>
------------

<span data-ttu-id="6045d-110">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="6045d-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="6045d-111">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="6045d-111">Remarks</span></span>

<span data-ttu-id="6045d-112">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="6045d-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="6045d-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="6045d-113">Requirements</span></span>
------------
><span data-ttu-id="6045d-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="6045d-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="6045d-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="6045d-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="6045d-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="6045d-116">See also</span></span>


[<span data-ttu-id="6045d-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="6045d-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



