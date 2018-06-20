---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály GetMetaConfiguration metódusa
ms.openlocfilehash: ebf2b65f152c622ccf42e12545b0048a0b96d963
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219776"
---
# <a name="getmetaconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="4407f-103">Az MSFT_DSCLocalConfigurationManager osztály GetMetaConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="4407f-103">GetMetaConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="4407f-104">A helyi Configuration Manager-beállításainak konfigurálása ügynök használt beolvasása.</span><span class="sxs-lookup"><span data-stu-id="4407f-104">Gets the local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

<a name="syntax"></a><span data-ttu-id="4407f-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="4407f-105">Syntax</span></span>
------

```mof
uint32 GetMetaConfiguration(
  [out] MSFT_DSCMetaConfiguration MetaConfiguration
);
```

<a name="parameters"></a><span data-ttu-id="4407f-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="4407f-106">Parameters</span></span>
----------

<span data-ttu-id="4407f-107">*Metakonfigurációját* \[kimenő\] return tartalmaz beágyazott példányának a **MSFT_DSCMetaConfiguration** osztály, amely meghatározza a beállításokat.</span><span class="sxs-lookup"><span data-stu-id="4407f-107">*MetaConfiguration* \[out\] On return, contains an embedded instance of the **MSFT_DSCMetaConfiguration** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="4407f-108">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="4407f-108">Return value</span></span>
------------

<span data-ttu-id="4407f-109">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="4407f-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="4407f-110">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="4407f-110">Remarks</span></span>

<span data-ttu-id="4407f-111">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="4407f-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="4407f-112">Követelmények</span><span class="sxs-lookup"><span data-stu-id="4407f-112">Requirements</span></span>
------------
><span data-ttu-id="4407f-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="4407f-113">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="4407f-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="4407f-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="4407f-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="4407f-115">See also</span></span>


[<span data-ttu-id="4407f-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="4407f-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)