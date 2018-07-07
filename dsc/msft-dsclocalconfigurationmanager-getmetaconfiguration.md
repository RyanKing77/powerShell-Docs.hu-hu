---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály GetMetaConfiguration metódusa
ms.openlocfilehash: e14237ef68b95d68e2f14071aa1fa6ba0717f39f
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892841"
---
# <a name="getmetaconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="7d145-103">Az MSFT_DSCLocalConfigurationManager osztály GetMetaConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="7d145-103">GetMetaConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="7d145-104">Lekérdezi a helyi Configuration Manager-beállításokat, hogy a konfigurációs ügynök szabályozására szolgálnak.</span><span class="sxs-lookup"><span data-stu-id="7d145-104">Gets the local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

## <a name="syntax"></a><span data-ttu-id="7d145-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="7d145-105">Syntax</span></span>

```mof
uint32 GetMetaConfiguration(
  [out] MSFT_DSCMetaConfiguration MetaConfiguration
);
```

## <a name="parameters"></a><span data-ttu-id="7d145-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="7d145-106">Parameters</span></span>

<span data-ttu-id="7d145-107">*MetaConfiguration* \[ki\] return tartalmaz egy beágyazott példányát a **MSFT_DSCMetaConfiguration** osztály, amely meghatározza a beállításokat.</span><span class="sxs-lookup"><span data-stu-id="7d145-107">*MetaConfiguration* \[out\] On return, contains an embedded instance of the **MSFT_DSCMetaConfiguration** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="7d145-108">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="7d145-108">Return value</span></span>

<span data-ttu-id="7d145-109">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="7d145-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="7d145-110">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="7d145-110">Remarks</span></span>

<span data-ttu-id="7d145-111">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="7d145-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="7d145-112">Követelmények</span><span class="sxs-lookup"><span data-stu-id="7d145-112">Requirements</span></span>

<span data-ttu-id="7d145-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="7d145-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="7d145-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="7d145-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="7d145-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="7d145-115">See also</span></span>

[<span data-ttu-id="7d145-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="7d145-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)