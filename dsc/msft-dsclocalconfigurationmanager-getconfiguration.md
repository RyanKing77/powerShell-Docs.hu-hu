---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály GetConfiguration módszer"
ms.openlocfilehash: 60f4b49575dbb28ce74af0500e6982ec5d2e7a66
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="getconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="9a906-103">A MSFT_DSCLocalConfigurationManager osztály GetConfiguration módszer</span><span class="sxs-lookup"><span data-stu-id="9a906-103">GetConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="9a906-104">A konfigurációs dokumentum küld a felügyelt csomóponthoz, és használja a **beolvasása** módszert a beállítások a konfigurációs ügynök.</span><span class="sxs-lookup"><span data-stu-id="9a906-104">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="9a906-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="9a906-105">Syntax</span></span>
------

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

<a name="parameters"></a><span data-ttu-id="9a906-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="9a906-106">Parameters</span></span>
----------

<span data-ttu-id="9a906-107">*configurationData* \[a\]</span><span class="sxs-lookup"><span data-stu-id="9a906-107">*configurationData* \[in\]</span></span>  
<span data-ttu-id="9a906-108">Megadja a konfigurációs adatokat küldhet.</span><span class="sxs-lookup"><span data-stu-id="9a906-108">Specifies the configuration data to send.</span></span>

<span data-ttu-id="9a906-109">*konfigurációk* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="9a906-109">*configurations* \[out\]</span></span>  
<span data-ttu-id="9a906-110">Térjen vissza tartalmazza a konfigurációk beágyazott példánya.</span><span class="sxs-lookup"><span data-stu-id="9a906-110">On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="9a906-111">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="9a906-111">Return value</span></span>
------------

<span data-ttu-id="9a906-112">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="9a906-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="9a906-113">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="9a906-113">Remarks</span></span>

<span data-ttu-id="9a906-114">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="9a906-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="9a906-115">Követelmények</span><span class="sxs-lookup"><span data-stu-id="9a906-115">Requirements</span></span>
------------
><span data-ttu-id="9a906-116">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="9a906-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="9a906-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="9a906-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="9a906-118">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9a906-118">See also</span></span>


[<span data-ttu-id="9a906-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="9a906-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
 

 



