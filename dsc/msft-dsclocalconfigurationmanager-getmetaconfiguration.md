---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály GetMetaConfiguration módszer"
ms.openlocfilehash: 4f209014e9fde5841a9bce743f5364e6677d1e41
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="getmetaconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="5c57a-103">A MSFT_DSCLocalConfigurationManager osztály GetMetaConfiguration módszer</span><span class="sxs-lookup"><span data-stu-id="5c57a-103">GetMetaConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="5c57a-104">A helyi Configuration Manager-beállításainak konfigurálása ügynök használt beolvasása.</span><span class="sxs-lookup"><span data-stu-id="5c57a-104">Gets the local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

<a name="syntax"></a><span data-ttu-id="5c57a-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="5c57a-105">Syntax</span></span>
------

```mof
uint32 GetMetaConfiguration(
  [out] MSFT_DSCMetaConfiguration MetaConfiguration
);
```

<a name="parameters"></a><span data-ttu-id="5c57a-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="5c57a-106">Parameters</span></span>
----------

<span data-ttu-id="5c57a-107">*Metakonfigurációját* \[kimenő\]</span><span class="sxs-lookup"><span data-stu-id="5c57a-107">*MetaConfiguration* \[out\]</span></span>  
<span data-ttu-id="5c57a-108">A visszatérési, tartalmazza a beágyazott példányának a **MSFT_DSCMetaConfiguration** osztály, amely meghatározza a beállításokat.</span><span class="sxs-lookup"><span data-stu-id="5c57a-108">On return, contains an embedded instance of the **MSFT_DSCMetaConfiguration** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="5c57a-109">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="5c57a-109">Return value</span></span>
------------

<span data-ttu-id="5c57a-110">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="5c57a-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="5c57a-111">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="5c57a-111">Remarks</span></span>

<span data-ttu-id="5c57a-112">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="5c57a-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="5c57a-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="5c57a-113">Requirements</span></span>
------------
><span data-ttu-id="5c57a-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="5c57a-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="5c57a-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="5c57a-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="5c57a-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5c57a-116">See also</span></span>


[<span data-ttu-id="5c57a-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="5c57a-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



