---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály GetConfiguration módszer"
ms.openlocfilehash: 96676a76a0302543e5e4a214c82ed952d7f52a71
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="getconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="36d82-103">A MSFT_DSCLocalConfigurationManager osztály GetConfiguration módszer</span><span class="sxs-lookup"><span data-stu-id="36d82-103">GetConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="36d82-104">A konfigurációs dokumentum küld a felügyelt csomóponthoz, és használja a **beolvasása** módszert a beállítások a konfigurációs ügynök.</span><span class="sxs-lookup"><span data-stu-id="36d82-104">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="36d82-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="36d82-105">Syntax</span></span>
------

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

<a name="parameters"></a><span data-ttu-id="36d82-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="36d82-106">Parameters</span></span>
----------

<span data-ttu-id="36d82-107">*configurationData* \[a\]</span><span class="sxs-lookup"><span data-stu-id="36d82-107">*configurationData* \[in\]</span></span>  
<span data-ttu-id="36d82-108">Megadja a konfigurációs adatokat küldhet.</span><span class="sxs-lookup"><span data-stu-id="36d82-108">Specifies the configuration data to send.</span></span>

<span data-ttu-id="36d82-109">*konfigurációk* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="36d82-109">*configurations* \[out\]</span></span>  
<span data-ttu-id="36d82-110">Térjen vissza tartalmazza a konfigurációk beágyazott példánya.</span><span class="sxs-lookup"><span data-stu-id="36d82-110">On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="36d82-111">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="36d82-111">Return value</span></span>
------------

<span data-ttu-id="36d82-112">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="36d82-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="36d82-113">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="36d82-113">Remarks</span></span>

<span data-ttu-id="36d82-114">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="36d82-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="36d82-115">Követelmények</span><span class="sxs-lookup"><span data-stu-id="36d82-115">Requirements</span></span>
------------
><span data-ttu-id="36d82-116">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="36d82-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="36d82-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="36d82-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="36d82-118">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="36d82-118">See also</span></span>


[<span data-ttu-id="36d82-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="36d82-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
 

 



