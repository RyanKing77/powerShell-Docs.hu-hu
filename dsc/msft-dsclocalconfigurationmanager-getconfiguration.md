---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály GetConfiguration metódusa
ms.openlocfilehash: 46eec896df643996bea5f2c371a9294034caae6b
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34218416"
---
# <a name="getconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="00fb7-103">Az MSFT_DSCLocalConfigurationManager osztály GetConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="00fb7-103">GetConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="00fb7-104">A konfigurációs dokumentum küld a felügyelt csomóponthoz, és használja a **beolvasása** módszert a beállítások a konfigurációs ügynök.</span><span class="sxs-lookup"><span data-stu-id="00fb7-104">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="00fb7-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="00fb7-105">Syntax</span></span>
------

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

<a name="parameters"></a><span data-ttu-id="00fb7-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="00fb7-106">Parameters</span></span>
----------

<span data-ttu-id="00fb7-107">*configurationData* \[a\] határozza meg a konfigurációs adatok küldése.</span><span class="sxs-lookup"><span data-stu-id="00fb7-107">*configurationData* \[in\] Specifies the configuration data to send.</span></span>

<span data-ttu-id="00fb7-108">*konfigurációk* \[kimenő\] vissza, tartalmazza a konfigurációk beágyazott példánya.</span><span class="sxs-lookup"><span data-stu-id="00fb7-108">*configurations* \[out\] On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="00fb7-109">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="00fb7-109">Return value</span></span>
------------

<span data-ttu-id="00fb7-110">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="00fb7-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="00fb7-111">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="00fb7-111">Remarks</span></span>

<span data-ttu-id="00fb7-112">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="00fb7-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="00fb7-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="00fb7-113">Requirements</span></span>
------------
><span data-ttu-id="00fb7-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="00fb7-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="00fb7-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="00fb7-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="00fb7-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="00fb7-116">See also</span></span>


[<span data-ttu-id="00fb7-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="00fb7-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)