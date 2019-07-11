---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: MSFT_DSCLocalConfigurationManager osztály
ms.openlocfilehash: 09b30edd48384c0e8412e0e6ee926a719249c5b8
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726890"
---
# <a name="msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="ebe48-103">MSFT_DSCLocalConfigurationManager osztály</span><span class="sxs-lookup"><span data-stu-id="ebe48-103">MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="ebe48-104">A helyi Configuration Manager (LCM) Konfigurálása, amely az államok konfigurációs fájlja vezérli, és a konfiguráció alkalmazása a konfigurációs ügynök használatával.</span><span class="sxs-lookup"><span data-stu-id="ebe48-104">The Local Configuration Manager (LCM) that controls the states of configuration files and uses Configuration Agent to apply the configurations.</span></span>

<span data-ttu-id="ebe48-105">A következő szintaxist Managed Object Format (MOF) kódból egyszerűsödött, és tartalmazza az összes örökölt tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="ebe48-105">The following syntax is simplified from Managed Object Format (MOF) code and includes all of the inherited properties.</span></span>

## <a name="syntax"></a><span data-ttu-id="ebe48-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="ebe48-106">Syntax</span></span>

```
[ClassVersion("1.0.0"), dynamic, provider("dsccore"), AMENDMENT]
class MSFT_DSCLocalConfigurationManager
{
};
```

## <a name="members"></a><span data-ttu-id="ebe48-107">Tagok</span><span class="sxs-lookup"><span data-stu-id="ebe48-107">Members</span></span>

<span data-ttu-id="ebe48-108">A **MSFT_DSCLocalConfigurationManager** osztályt a következő tagja van:</span><span class="sxs-lookup"><span data-stu-id="ebe48-108">The **MSFT_DSCLocalConfigurationManager** class has the following members:</span></span>

- <span data-ttu-id="ebe48-109">[Módszerek] []</span><span class="sxs-lookup"><span data-stu-id="ebe48-109">[Methods][]</span></span>

### <a name="methods"></a><span data-ttu-id="ebe48-110">Metódusok</span><span class="sxs-lookup"><span data-stu-id="ebe48-110">Methods</span></span>

<span data-ttu-id="ebe48-111">A **MSFT_DSCLocalConfigurationManager** osztály rendelkezik, ezek a módszerek.</span><span class="sxs-lookup"><span data-stu-id="ebe48-111">The **MSFT_DSCLocalConfigurationManager** class has these methods.</span></span>

|<span data-ttu-id="ebe48-112">Módszer</span><span class="sxs-lookup"><span data-stu-id="ebe48-112">Method</span></span> |<span data-ttu-id="ebe48-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="ebe48-113">Description</span></span> |
|:--- |:---|
| [<span data-ttu-id="ebe48-114">ApplyConfiguration</span><span class="sxs-lookup"><span data-stu-id="ebe48-114">ApplyConfiguration</span></span>](msft-dsclocalconfigurationmanager-applyconfiguration.md)| <span data-ttu-id="ebe48-115">A konfigurációs ügynök használja a alkalmazni a konfigurációt, amely függőben van.</span><span class="sxs-lookup"><span data-stu-id="ebe48-115">Uses the Configuration Agent to apply the configuration that is pending.</span></span>|
| [<span data-ttu-id="ebe48-116">DisableDebugConfiguration</span><span class="sxs-lookup"><span data-stu-id="ebe48-116">DisableDebugConfiguration</span></span>](msft-dsclocalconfigurationmanager-disabledebugconfiguration.md)| <span data-ttu-id="ebe48-117">Letiltja a DSC-erőforrás hibakeresés.</span><span class="sxs-lookup"><span data-stu-id="ebe48-117">Disables DSC resource debugging.</span></span>|
| [<span data-ttu-id="ebe48-118">EnableDebugConfiguration</span><span class="sxs-lookup"><span data-stu-id="ebe48-118">EnableDebugConfiguration</span></span>](msft-dsclocalconfigurationmanager-enabledebugconfiguration.md)| <span data-ttu-id="ebe48-119">Lehetővé teszi a DSC-erőforrás hibakeresés.</span><span class="sxs-lookup"><span data-stu-id="ebe48-119">Enables DSC resource debugging.</span></span>|
| [<span data-ttu-id="ebe48-120">GetConfiguration</span><span class="sxs-lookup"><span data-stu-id="ebe48-120">GetConfiguration</span></span>](msft-dsclocalconfigurationmanager-getconfiguration.md)| <span data-ttu-id="ebe48-121">A konfigurációs dokumentum küldése a felügyelt csomóponthoz, és használja a **első** metódus a alkalmazni a konfigurációt a konfigurációs ügynök.</span><span class="sxs-lookup"><span data-stu-id="ebe48-121">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>|
| [<span data-ttu-id="ebe48-122">GetConfigurationResultOutput</span><span class="sxs-lookup"><span data-stu-id="ebe48-122">GetConfigurationResultOutput</span></span>](msft-dsclocalconfigurationmanager-getconfigurationresultoutput.md)| <span data-ttu-id="ebe48-123">Lekéri egy adott feladat vonatkozó konfigurációs ügynök kimenetét.</span><span class="sxs-lookup"><span data-stu-id="ebe48-123">Gets the Configuration Agent output relating to a specific job.</span></span>|
| [<span data-ttu-id="ebe48-124">GetConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="ebe48-124">GetConfigurationStatus</span></span>](msft-dsclocalconfigurationmanager-getconfigurationstatus.md)| <span data-ttu-id="ebe48-125">A konfigurációs ügyfélállapot előzményeinek lekérése.</span><span class="sxs-lookup"><span data-stu-id="ebe48-125">Get the configuration status history.</span></span>|
| [<span data-ttu-id="ebe48-126">GetMetaConfiguration</span><span class="sxs-lookup"><span data-stu-id="ebe48-126">GetMetaConfiguration</span></span>](msft-dsclocalconfigurationmanager-getmetaconfiguration.md)| <span data-ttu-id="ebe48-127">Szabályozhatja a konfigurációs ügynök LCM beállítások beolvasása.</span><span class="sxs-lookup"><span data-stu-id="ebe48-127">Gets the LCM settings that are used to control Configuration Agent.</span></span>|
| [<span data-ttu-id="ebe48-128">PerformRequiredConfigurationChecks</span><span class="sxs-lookup"><span data-stu-id="ebe48-128">PerformRequiredConfigurationChecks</span></span>](msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks.md)| <span data-ttu-id="ebe48-129">A konzisztencia-ellenőrzés indítása.</span><span class="sxs-lookup"><span data-stu-id="ebe48-129">Starts the consistency check.</span></span>|
| [<span data-ttu-id="ebe48-130">RemoveConfiguration</span><span class="sxs-lookup"><span data-stu-id="ebe48-130">RemoveConfiguration</span></span>](msft-dsclocalconfigurationmanager-removeconfiguration.md)| <span data-ttu-id="ebe48-131">Eltávolítja a konfigurációs fájlokat.</span><span class="sxs-lookup"><span data-stu-id="ebe48-131">Removes the configuration files.</span></span>|
| [<span data-ttu-id="ebe48-132">ResourceGet</span><span class="sxs-lookup"><span data-stu-id="ebe48-132">ResourceGet</span></span>](msft-dsclocalconfigurationmanager-resourceget.md)| <span data-ttu-id="ebe48-133">Közvetlenül meghívja a **első** metódus a DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="ebe48-133">Directly calls the **Get** method of a DSC resource.</span></span>|
| [<span data-ttu-id="ebe48-134">ResourceSet</span><span class="sxs-lookup"><span data-stu-id="ebe48-134">ResourceSet</span></span>](msft-dsclocalconfigurationmanager-resourceset.md)| <span data-ttu-id="ebe48-135">Közvetlenül meghívja a **beállítása** metódus a DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="ebe48-135">Directly calls the **Set** method of a DSC resource.</span></span>|
| [<span data-ttu-id="ebe48-136">ResourceTest</span><span class="sxs-lookup"><span data-stu-id="ebe48-136">ResourceTest</span></span>](msft-dsclocalconfigurationmanager-resourcetest.md)| <span data-ttu-id="ebe48-137">Közvetlenül meghívja a **teszt** metódus a DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="ebe48-137">Directly calls the **Test** method of a DSC resource.</span></span>|
| [<span data-ttu-id="ebe48-138">RollBack</span><span class="sxs-lookup"><span data-stu-id="ebe48-138">RollBack</span></span>](msft-dsclocalconfigurationmanager-rollback.md)| <span data-ttu-id="ebe48-139">Vissza az előző konfigurációs tekercsben.</span><span class="sxs-lookup"><span data-stu-id="ebe48-139">Rolls back to a previous configuration.</span></span>|
| [<span data-ttu-id="ebe48-140">SendConfiguration</span><span class="sxs-lookup"><span data-stu-id="ebe48-140">SendConfiguration</span></span>](msft-dsclocalconfigurationmanager-sendconfiguration.md)| <span data-ttu-id="ebe48-141">A konfigurációs dokumentum a felügyelt csomópont küld, és menti azt egy függőben lévő módosítást.</span><span class="sxs-lookup"><span data-stu-id="ebe48-141">Sends the configuration document to the managed node and saves it as a pending change.</span></span>|
| [<span data-ttu-id="ebe48-142">SendConfigurationApply</span><span class="sxs-lookup"><span data-stu-id="ebe48-142">SendConfigurationApply</span></span>](msft-dsclocalconfigurationmanager-sendconfigurationapply.md)| <span data-ttu-id="ebe48-143">A konfigurációs dokumentum a felügyelt csomópont küld, és a konfigurációs ügynök használja a alkalmazni a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="ebe48-143">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>|
| [<span data-ttu-id="ebe48-144">SendConfigurationApplyAsync</span><span class="sxs-lookup"><span data-stu-id="ebe48-144">SendConfigurationApplyAsync</span></span>](msft-dsclocalconfigurationmanager-sendconfigurationapplyasync.md)| <span data-ttu-id="ebe48-145">A konfigurációs dokumentum küldése a felügyelt csomóponthoz, és indítsa el a alkalmazni a konfigurációt a konfigurációs ügynök használatával.</span><span class="sxs-lookup"><span data-stu-id="ebe48-145">Send the configuration document to the managed node and start using the Configuration Agent to apply the configuration.</span></span> <span data-ttu-id="ebe48-146">GetConfigurationResultOutput használatával lekérheti az eredmény kimeneti.</span><span class="sxs-lookup"><span data-stu-id="ebe48-146">Use GetConfigurationResultOutput to retrieve result output.</span></span>|
| [<span data-ttu-id="ebe48-147">SendMetaConfigurationApply</span><span class="sxs-lookup"><span data-stu-id="ebe48-147">SendMetaConfigurationApply</span></span>](msft-dsclocalconfigurationmanager-sendmetaconfigurationapply.md)| <span data-ttu-id="ebe48-148">Az LCM beállítások, amelyek segítségével szabályozhatja a konfigurációs ügynök beállítása.</span><span class="sxs-lookup"><span data-stu-id="ebe48-148">Sets the LCM settings that are used to control the Configuration Agent.</span></span>|
| [<span data-ttu-id="ebe48-149">StopConfiguration</span><span class="sxs-lookup"><span data-stu-id="ebe48-149">StopConfiguration</span></span>](msft-dsclocalconfigurationmanager-stopconfiguration.md)| <span data-ttu-id="ebe48-150">Leállítja a konfigurációt, hogy folyamatban van.</span><span class="sxs-lookup"><span data-stu-id="ebe48-150">Stops the configuration that is in progress.</span></span>|
| [<span data-ttu-id="ebe48-151">TestConfiguration</span><span class="sxs-lookup"><span data-stu-id="ebe48-151">TestConfiguration</span></span>](msft-dsclocalconfigurationmanager-testconfiguration.md)| <span data-ttu-id="ebe48-152">A konfigurációs dokumentum a felügyelt csomópont küld, és ellenőrzi az aktuális konfiguráció ellen a dokumentumot.</span><span class="sxs-lookup"><span data-stu-id="ebe48-152">Sends the configuration document to the managed node and verifies the current configuration against the document.</span></span>|

## <a name="requirements"></a><span data-ttu-id="ebe48-153">Követelmények</span><span class="sxs-lookup"><span data-stu-id="ebe48-153">Requirements</span></span>

<span data-ttu-id="ebe48-154">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="ebe48-154">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="ebe48-155">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="ebe48-155">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>
