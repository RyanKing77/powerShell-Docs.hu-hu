---
ms.date: 11/06/2018
contributor: JKeithB
keywords: katalógus, powershell, a parancsmag, psgallery, psget
title: Helyi PSRepositories használata
ms.openlocfilehash: 94824ea584c097838b24c6f2cd02407b6147a781
ms.sourcegitcommit: 91786b03704fbd2d185f674df0bc67faddfb6288
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/14/2018
ms.locfileid: "51619258"
---
# <a name="working-with-local-powershellget-repositories"></a><span data-ttu-id="d40ae-103">A PowerShellGet helyi tárház használata</span><span class="sxs-lookup"><span data-stu-id="d40ae-103">Working with local PowerShellGet Repositories</span></span>

<span data-ttu-id="d40ae-104">A PowerShellGet modul támogatási tárházak kívül a PowerShell-galériában.</span><span class="sxs-lookup"><span data-stu-id="d40ae-104">The PowerShellGet module support repositories other than the PowerShell Gallery.</span></span>
<span data-ttu-id="d40ae-105">Ezeket a parancsmagokat a következő forgatókönyvek megvalósítását teszik lehetővé:</span><span class="sxs-lookup"><span data-stu-id="d40ae-105">These cmdlets enable the following scenarios:</span></span>

- <span data-ttu-id="d40ae-106">PowerShell-modulok megbízható, előre ellenőrzött készletét támogatja a környezetben való használatra</span><span class="sxs-lookup"><span data-stu-id="d40ae-106">Support a trusted, pre-validated set of PowerShell modules for use in your environment</span></span>
- <span data-ttu-id="d40ae-107">PowerShell-modulok vagy parancsfájlok olyan CI/CD-folyamat tesztelése</span><span class="sxs-lookup"><span data-stu-id="d40ae-107">Testing a CI/CD pipeline that builds PowerShell modules or scripts</span></span>
- <span data-ttu-id="d40ae-108">PowerShell-szkriptek és modulok továbbítására rendszerek nem férnek hozzá az internethez</span><span class="sxs-lookup"><span data-stu-id="d40ae-108">Deliver PowerShell scripts and modules to systems that can't access the internet</span></span>

<span data-ttu-id="d40ae-109">Ez a cikk ismerteti, hogyan állítható be egy helyi PowerShell-tárház.</span><span class="sxs-lookup"><span data-stu-id="d40ae-109">This article describes how to set up a local PowerShell repository.</span></span> <span data-ttu-id="d40ae-110">A cikk emellett ismerteti a [OfflinePowerShellGetDeploy][] modulban elérhető PowerShell-galériából történő.</span><span class="sxs-lookup"><span data-stu-id="d40ae-110">The article also covers the [OfflinePowerShellGetDeploy][] module available from the PowerShell Gallery.</span></span> <span data-ttu-id="d40ae-111">Ez a modul tartalmazza a parancsmagok a PowerShellGet legújabb verziójának telepítéséhez a helyi tárházba.</span><span class="sxs-lookup"><span data-stu-id="d40ae-111">This module contains cmdlets to install the latest version of PowerShellGet into your local repository.</span></span>

## <a name="local-repository-types"></a><span data-ttu-id="d40ae-112">Helyi tárház típusa</span><span class="sxs-lookup"><span data-stu-id="d40ae-112">Local repository types</span></span>

<span data-ttu-id="d40ae-113">Kétféleképpen hozhat létre egy helyi PSRepository: NuGet server vagy a fájlmegosztásnak.</span><span class="sxs-lookup"><span data-stu-id="d40ae-113">There are two ways to create a local PSRepository: NuGet server or file share.</span></span> <span data-ttu-id="d40ae-114">Minden típusának van előnyeit és hátrányait:</span><span class="sxs-lookup"><span data-stu-id="d40ae-114">Each type has advantages and disadvantages:</span></span>

<span data-ttu-id="d40ae-115">NuGet-kiszolgáló</span><span class="sxs-lookup"><span data-stu-id="d40ae-115">NuGet Server</span></span>

| <span data-ttu-id="d40ae-116">Előnyök</span><span class="sxs-lookup"><span data-stu-id="d40ae-116">Advantages</span></span>| <span data-ttu-id="d40ae-117">Hátrányok</span><span class="sxs-lookup"><span data-stu-id="d40ae-117">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="d40ae-118">PowerShell-Galériabeli funkció szorosan utánozza</span><span class="sxs-lookup"><span data-stu-id="d40ae-118">Closely mimics PowerShellGallery functionality</span></span> | <span data-ttu-id="d40ae-119">Többrétegű alkalmazást szükséges műveletek tervezési és támogatás</span><span class="sxs-lookup"><span data-stu-id="d40ae-119">Multi-tier app requires operations planning & support</span></span> |
| <span data-ttu-id="d40ae-120">NuGet integrálja a Visual Studiót, más eszközök</span><span class="sxs-lookup"><span data-stu-id="d40ae-120">NuGet integrates with Visual Studio, other tools</span></span> | <span data-ttu-id="d40ae-121">Hitelesítési modellre és a szükséges NuGet-fiókok kezelése</span><span class="sxs-lookup"><span data-stu-id="d40ae-121">Authentication model and NuGet accounts management needed</span></span> |
| <span data-ttu-id="d40ae-122">NuGet támogatja a metaadatok `.Nupkg` csomagok</span><span class="sxs-lookup"><span data-stu-id="d40ae-122">NuGet supports metadata in `.Nupkg` packages</span></span> | <span data-ttu-id="d40ae-123">A közzétételhez API-kulcs felügyelet és karbantartás</span><span class="sxs-lookup"><span data-stu-id="d40ae-123">Publishing requires API Key management & maintenance</span></span> |
| <span data-ttu-id="d40ae-124">Itt a keresés, a felügyeleti csomag, stb.</span><span class="sxs-lookup"><span data-stu-id="d40ae-124">Provides search, package administration, etc.</span></span> | |

<span data-ttu-id="d40ae-125">Fájlmegosztás</span><span class="sxs-lookup"><span data-stu-id="d40ae-125">File Share</span></span>

| <span data-ttu-id="d40ae-126">Előnyök</span><span class="sxs-lookup"><span data-stu-id="d40ae-126">Advantages</span></span>| <span data-ttu-id="d40ae-127">Hátrányok</span><span class="sxs-lookup"><span data-stu-id="d40ae-127">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="d40ae-128">Állítsa be, biztonsági mentése és kezelése egyszerűen</span><span class="sxs-lookup"><span data-stu-id="d40ae-128">Easy to set up, back up, and maintain</span></span> | <span data-ttu-id="d40ae-129">A PowerShellGet által használt metaadatok nem érhető el</span><span class="sxs-lookup"><span data-stu-id="d40ae-129">Metadata used by PowerShellGet isn't available</span></span> |
| <span data-ttu-id="d40ae-130">Egyszerű biztonsági modell – felhasználói engedélyek a megosztáson</span><span class="sxs-lookup"><span data-stu-id="d40ae-130">Simple security model - user permissions on the share</span></span> | <span data-ttu-id="d40ae-131">Alapszintű fájlmegosztás túli felhasználói felület</span><span class="sxs-lookup"><span data-stu-id="d40ae-131">No UI beyond basic file share</span></span> |
| <span data-ttu-id="d40ae-132">Cserélje le a meglévő elemeket, például a korlátozások nélkül</span><span class="sxs-lookup"><span data-stu-id="d40ae-132">No constraints such as replacing existing items</span></span> | <span data-ttu-id="d40ae-133">Korlátozott biztonságot és, aki frissíti, hogy mi nincs rögzítés</span><span class="sxs-lookup"><span data-stu-id="d40ae-133">Limited security and no recording of who updates what</span></span> |

<span data-ttu-id="d40ae-134">A PowerShellGet működik, típusú és a verziója és a függőség telepítése megkeresése támogatja.</span><span class="sxs-lookup"><span data-stu-id="d40ae-134">PowerShellGet works with either type and supports locating versions and dependency installation.</span></span>
<span data-ttu-id="d40ae-135">Azonban az egyes szolgáltatásai számára a PowerShell-galériából nem érhetők el alap NuGet-kiszolgálók vagy fájlmegosztásokat.</span><span class="sxs-lookup"><span data-stu-id="d40ae-135">However, some features that work for the PowerShell Gallery aren't available for base NuGet servers or file shares.</span></span>

- <span data-ttu-id="d40ae-136">Minden csomag egy - parancsfájlokat, a modulok, a DSC-erőforrások vagy a szerepkörrel képességeket különbséget tenni.</span><span class="sxs-lookup"><span data-stu-id="d40ae-136">Everything is a package - no differentiation of scripts, modules, DSC resources, or role capabilities.</span></span>
- <span data-ttu-id="d40ae-137">Megosztás fájlkiszolgálók metaadatcsomagok, beleértve a címkék nem látható.</span><span class="sxs-lookup"><span data-stu-id="d40ae-137">File share servers can't see package metadata, including tags.</span></span>

## <a name="creating-a-local-repository"></a><span data-ttu-id="d40ae-138">Helyi tárház létrehozására</span><span class="sxs-lookup"><span data-stu-id="d40ae-138">Creating a local repository</span></span>

<span data-ttu-id="d40ae-139">A következő cikk a saját NuGet-kiszolgáló beállításának lépéseit sorolja fel.</span><span class="sxs-lookup"><span data-stu-id="d40ae-139">The following article lists the steps for setting up your own NuGet Server.</span></span>

- <span data-ttu-id="d40ae-140">[NuGet.Server][]</span><span class="sxs-lookup"><span data-stu-id="d40ae-140">[NuGet.Server][]</span></span>

<span data-ttu-id="d40ae-141">Kövesse a lépéseket azon csomagok hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="d40ae-141">Follow the steps up to the point of adding packages.</span></span> <span data-ttu-id="d40ae-142">A lépések a [egy csomag közzététele](#publishing-to-a-local-repository) terjed ki a cikk későbbi részében.</span><span class="sxs-lookup"><span data-stu-id="d40ae-142">The steps for [publishing a package](#publishing-to-a-local-repository) are covered later in this article.</span></span>

<span data-ttu-id="d40ae-143">Egy fájl fájlmegosztás-alapú adattárat ügyeljen arra, hogy a felhasználók rendelkeznek-e engedélyekkel a fájlmegosztás eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="d40ae-143">For a file share-based repository, make sure that your users have permissions to access the file share.</span></span>

## <a name="registering-a-local-repository"></a><span data-ttu-id="d40ae-144">A helyi tárház regisztrálása</span><span class="sxs-lookup"><span data-stu-id="d40ae-144">Registering a local repository</span></span>

<span data-ttu-id="d40ae-145">Egy adattár használata előtt regisztrálnia kell azt használatával a `Register-PSRepository` parancsot.</span><span class="sxs-lookup"><span data-stu-id="d40ae-145">Before a repository can be used, it must be registered using the `Register-PSRepository` command.</span></span>
<span data-ttu-id="d40ae-146">Az alábbi példákban a **InstallationPolicy** értékre van állítva *megbízható*, feltételezve, hogy megbízható-e a saját tárház.</span><span class="sxs-lookup"><span data-stu-id="d40ae-146">In the examples below, the **InstallationPolicy** is set to *Trusted*, on the assumption that you trust your own repository.</span></span>

```powershell
# Register a NuGet-based server
Register-PSRepository -Name LocalPSRepo -SourceLocation http://MyLocalNuget/Api/V2/ -ScriptSourceLocation http://MyLocalNuget/Api/V2 -InstallationPolicy Trusted

# Register a file share on my local machine
Register-PSRepository -Name LocalPSRepo -SourceLocation '\\localhost\PSRepoLocal\' -ScriptSourceLocation '\\localhost\PSRepoLocal\' -InstallationPolicy Trusted
```

<span data-ttu-id="d40ae-147">Jegyezze fel a különbség, hogy hogyan kezeli a a két parancs **ScriptSourceLocation**.</span><span class="sxs-lookup"><span data-stu-id="d40ae-147">Take note of the difference between how the two commands handle **ScriptSourceLocation**.</span></span> <span data-ttu-id="d40ae-148">Egy fájl fájlmegosztás-alapú tárházakhoz készült a **SourceLocation** és **ScriptSourceLocation** egyeznie kell.</span><span class="sxs-lookup"><span data-stu-id="d40ae-148">For a file share-based repositories, the **SourceLocation** and **ScriptSourceLocation** must match.</span></span> <span data-ttu-id="d40ae-149">Egy webes tárház kell lenniük különböző, így ebben a példában egy záró "/" adnak hozzá a **SourceLocation**.</span><span class="sxs-lookup"><span data-stu-id="d40ae-149">For a web-based repository, they must be different, so in this example a trailing "/" is added to the **SourceLocation**.</span></span>

<span data-ttu-id="d40ae-150">Ha azt szeretné, hogy az újonnan létrehozott PSRepository kell az alapértelmezett tárházban, akkor az összes többi PSRepositories kell regisztrációját.</span><span class="sxs-lookup"><span data-stu-id="d40ae-150">If you want the newly created PSRepository to be the default repository, you must unregister all other PSRepositories.</span></span> <span data-ttu-id="d40ae-151">Például:</span><span class="sxs-lookup"><span data-stu-id="d40ae-151">For example:</span></span>

```powershell
Unregister-PSRepository -Name PSGallery
```

> [!NOTE]
> <span data-ttu-id="d40ae-152">A tárház nevének "PSGallery" az a PowerShell-galériából használatra van fenntartva.</span><span class="sxs-lookup"><span data-stu-id="d40ae-152">The repository name 'PSGallery' is reserved for use by the PowerShell Gallery.</span></span> <span data-ttu-id="d40ae-153">PSGallery regisztrációját is, de nem használhat újra bármely más adattárból PSGallery nevét.</span><span class="sxs-lookup"><span data-stu-id="d40ae-153">You can unregister PSGallery, but you cannot reuse the name PSGallery for any other repository.</span></span>

<span data-ttu-id="d40ae-154">Ha a PSGallery visszaállítására van szüksége, futtassa a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="d40ae-154">If you need to restore the PSGallery, run the following command:</span></span>

```powershell
Register-PSRepository -Default
```

## <a name="publishing-to-a-local-repository"></a><span data-ttu-id="d40ae-155">A helyi tárházban való közzététel</span><span class="sxs-lookup"><span data-stu-id="d40ae-155">Publishing to a local repository</span></span>

<span data-ttu-id="d40ae-156">Miután regisztrálta a helyi PSRepository, akkor a helyi PSRepository tehetnek közzé.</span><span class="sxs-lookup"><span data-stu-id="d40ae-156">Once you've registered the local PSRepository, you can publish to your local PSRepository.</span></span> <span data-ttu-id="d40ae-157">Két fő közzétételi forgatókönyv közül választhat: közzététele saját modult, és a modulnak a PSGallery a közzététele.</span><span class="sxs-lookup"><span data-stu-id="d40ae-157">There are two main publishing scenarios: publishing your own module and publishing a module from the PSGallery.</span></span>

### <a name="publishing-a-module-you-authored"></a><span data-ttu-id="d40ae-158">Ön készített modul közzététele</span><span class="sxs-lookup"><span data-stu-id="d40ae-158">Publishing a module you authored</span></span>

<span data-ttu-id="d40ae-159">Használat `Publish-Module` és `Publish-Script` a modul közzétételére a helyi PSRepository végezhet el, a PowerShell-galéria azonos módon.</span><span class="sxs-lookup"><span data-stu-id="d40ae-159">Use `Publish-Module` and `Publish-Script` to publish your module to your local PSRepository the same way you do for the PowerShell Gallery.</span></span>

- <span data-ttu-id="d40ae-160">Adja meg a kód helyét</span><span class="sxs-lookup"><span data-stu-id="d40ae-160">Specify the location for your code</span></span>
- <span data-ttu-id="d40ae-161">Adja meg az API-kulcs</span><span class="sxs-lookup"><span data-stu-id="d40ae-161">Supply an API key</span></span>
- <span data-ttu-id="d40ae-162">Adja meg a tárház nevét.</span><span class="sxs-lookup"><span data-stu-id="d40ae-162">Specify the repository name.</span></span> <span data-ttu-id="d40ae-163">Például: `-PSRepository LocalPSRepo`</span><span class="sxs-lookup"><span data-stu-id="d40ae-163">For example, `-PSRepository LocalPSRepo`</span></span>

> [!NOTE]
> <span data-ttu-id="d40ae-164">Hozzon létre egy fiókot a NuGet-kiszolgálón, majd jelentkezzen be létrehozni és menteni az API-kulcsot.</span><span class="sxs-lookup"><span data-stu-id="d40ae-164">You must create an account in the NuGet server, then sign in to generate and save the API key.</span></span>
> <span data-ttu-id="d40ae-165">Egy fájlmegosztás NuGetApiKey értékét minden nem lehet üres karakterlánc használható.</span><span class="sxs-lookup"><span data-stu-id="d40ae-165">For a file share, use any non-blank string for the NuGetApiKey value.</span></span>

<span data-ttu-id="d40ae-166">Példák:</span><span class="sxs-lookup"><span data-stu-id="d40ae-166">Examples:</span></span>

```powershell
# Publish to a NuGet Server repository using my NuGetAPI key
Publish-Module -Path 'c:\projects\MyModule' -Repository LocalPsRepo -NuGetApiKey 'oy2bi4avlkjolp6bme6azdyssn6ps3iu7ib2qpiudrtbji'

# Publish to a file share repo - the NuGet API key must be a non-blank string
Publish-Module -Path 'c:\projects\MyModule' -Repository LocalPsRepo -NuGetApiKey 'AnyStringWillDo'
```

> [!IMPORTANT]
> <span data-ttu-id="d40ae-167">Ahhoz, hogy a biztonsági, API-kulcsok nem lehet változtatható parancsfájlokban.</span><span class="sxs-lookup"><span data-stu-id="d40ae-167">To ensure security, API keys should not be hard-coded in scripts.</span></span> <span data-ttu-id="d40ae-168">A biztonságos rendszert kell használnia.</span><span class="sxs-lookup"><span data-stu-id="d40ae-168">Use a secure key management system.</span></span>

### <a name="publishing-a-module-from-the-psgallery"></a><span data-ttu-id="d40ae-169">A modul a PSGallery közzététele</span><span class="sxs-lookup"><span data-stu-id="d40ae-169">Publishing a module from the PSGallery</span></span>

<span data-ttu-id="d40ae-170">A modul a PSGallery a helyi PSRepository való közzétételéhez használhatja a "Mentés-Package" parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="d40ae-170">To publish a module from the PSGallery to your local PSRepository, you can use the 'Save-Package' cmdlet.</span></span>

- <span data-ttu-id="d40ae-171">Adja meg a csomag nevét</span><span class="sxs-lookup"><span data-stu-id="d40ae-171">Specify the Name of the Package</span></span>
- <span data-ttu-id="d40ae-172">Adja meg a "NuGet" szolgáltatója</span><span class="sxs-lookup"><span data-stu-id="d40ae-172">Specify 'NuGet' as the Provider</span></span>
- <span data-ttu-id="d40ae-173">Adja meg a PSGallery helyeként a forrás (https://www.powershellgallery.com/api/v2)</span><span class="sxs-lookup"><span data-stu-id="d40ae-173">Specify the PSGallery location as the source (https://www.powershellgallery.com/api/v2)</span></span>
- <span data-ttu-id="d40ae-174">Adja meg az elérési útját a helyi tárház</span><span class="sxs-lookup"><span data-stu-id="d40ae-174">Specify the path to your local Repository</span></span>

<span data-ttu-id="d40ae-175">Példa:</span><span class="sxs-lookup"><span data-stu-id="d40ae-175">Example:</span></span>

```powershell
# Publish from the PSGallery to your local Repository
Save-Package -Name 'PackageName' -Provider Nuget -Source https://www.powershellgallery.com/api/v2 -Path '\\localhost\PSRepoLocal\'
```

<span data-ttu-id="d40ae-176">Ha a helyi PSRepository webes, egy további lépést használó nuget.exe közzétételéhez szükséges.</span><span class="sxs-lookup"><span data-stu-id="d40ae-176">If your local PSRepository is web-based, it requires an additional step that uses nuget.exe to publish.</span></span>

<span data-ttu-id="d40ae-177">A dokumentációt a [nuget.exe][].</span><span class="sxs-lookup"><span data-stu-id="d40ae-177">See the documentation for using [nuget.exe][].</span></span>

## <a name="installing-powershellget-on-a-disconnected-system"></a><span data-ttu-id="d40ae-178">A PowerShellGet telepítése kapcsolat nélküli rendszerre</span><span class="sxs-lookup"><span data-stu-id="d40ae-178">Installing PowerShellGet on a disconnected system</span></span>

<span data-ttu-id="d40ae-179">A PowerShellGet telepítése is nehézkes olyan környezetekben, amelyek az internetről leválasztását rendszerek igényelnek.</span><span class="sxs-lookup"><span data-stu-id="d40ae-179">Deploying PowerShellGet is difficult in environments that require systems to be disconnected from the internet.</span></span> <span data-ttu-id="d40ae-180">A PowerShellGet rendelkezik egy rendszerindítási folyamatot, amely telepíti a legújabb verziót az első alkalommal használják.</span><span class="sxs-lookup"><span data-stu-id="d40ae-180">PowerShellGet has a bootstrap process that installs the latest version the first time it's used.</span></span> <span data-ttu-id="d40ae-181">A PowerShell-galériából a OfflinePowerShellGetDeploy modul, amely támogatja a rendszerindítási folyamat-parancsmagokat kínál.</span><span class="sxs-lookup"><span data-stu-id="d40ae-181">The OfflinePowerShellGetDeploy module in the PowerShell Gallery provides cmdlets that support this bootstrap process.</span></span>

<span data-ttu-id="d40ae-182">Elindíthat egy kapcsolat nélküli üzembe helyezés, kell tennie:</span><span class="sxs-lookup"><span data-stu-id="d40ae-182">To bootstrap an offline deployment, you need to:</span></span>

- <span data-ttu-id="d40ae-183">Töltse le és telepítse a OfflinePowerShellGetDeploy az internethez csatlakozó system és a leválasztott rendszerek</span><span class="sxs-lookup"><span data-stu-id="d40ae-183">Download and install the OfflinePowerShellGetDeploy your internet-connected system and your disconnected systems</span></span>
- <span data-ttu-id="d40ae-184">A PowerShellGet és annak függőségeit, az internethez csatlakozó system használatával töltse le a `Save-PowerShellGetForOffline` parancsmag</span><span class="sxs-lookup"><span data-stu-id="d40ae-184">Download PowerShellGet and its dependencies on the internet-connected system using the `Save-PowerShellGetForOffline` cmdlet</span></span>
- <span data-ttu-id="d40ae-185">A leválasztott rendszerhez az internethez csatlakoztatott rendszer PowerShellGet és annak függőségeit másolása</span><span class="sxs-lookup"><span data-stu-id="d40ae-185">Copy PowerShellGet and its dependencies from the internet-connected system to the disconnected system</span></span>
- <span data-ttu-id="d40ae-186">Használja a `Install-PowerShellGetOffline` a PowerShellGet és annak függőségeit helyezze a megfelelő mappákat a leválasztott rendszeren</span><span class="sxs-lookup"><span data-stu-id="d40ae-186">Use the `Install-PowerShellGetOffline` on the disconnected system to place PowerShellGet and its dependencies into the proper folders</span></span>

<span data-ttu-id="d40ae-187">A következő parancsokat használja `Save-PowerShellGetForOffline` üzembe helyezhető egy mappa összes összetevő `f:\OfflinePowerShellGet`</span><span class="sxs-lookup"><span data-stu-id="d40ae-187">The following commands use `Save-PowerShellGetForOffline` to put all the components into a folder `f:\OfflinePowerShellGet`</span></span>

```powershell
# Requires -RunAsAdministrator
#Download the OfflinePowerShellGetDeploy to a location that can be accessed
# by both the connected and disconnected systems.
Save-Module -Name OfflinePowerShellGetDeploy -Path 'F:\' -Repository PSGallery
Import-Module F:\OfflinePowerShellGetDeploy

# Put PowerShellGet somewhere locally
Save-PowerShellGetForOffline -LocalFolder 'F:\OfflinePowerShellGet'
```

<span data-ttu-id="d40ae-188">Ezen a ponton, végezze el a tartalmát `F:\OfflinePowerShellGet` kapcsolat nélküli rendszerekhez érhető el.</span><span class="sxs-lookup"><span data-stu-id="d40ae-188">At this point, you must make the contents of `F:\OfflinePowerShellGet` available to your disconnected systems.</span></span> <span data-ttu-id="d40ae-189">Futtassa a `Install-PowerShellGetOffline` parancsmagot, hogy a kapcsolat nélküli rendszeren a PowerShellGet telepítése.</span><span class="sxs-lookup"><span data-stu-id="d40ae-189">Run the `Install-PowerShellGetOffline` cmdlet to install PowerShellGet on the disconnected system.</span></span>

> [!NOTE]
> <span data-ttu-id="d40ae-190">Fontos, hogy nem futtatja a PowerShellGet a PowerShell-munkamenetben, ezek a parancsok futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="d40ae-190">It is important that you do not run PowerShellGet in the PowerShell session before running these commands.</span></span> <span data-ttu-id="d40ae-191">A PowerShellGet abba a munkamenetbe betöltése után az összetevőket nem lehet frissíteni.</span><span class="sxs-lookup"><span data-stu-id="d40ae-191">Once PowerShellGet is loaded into the session, the components cannot be updated.</span></span> <span data-ttu-id="d40ae-192">Ha a PowerShellGet véletlenül elindítani, akkor lépjen ki, és indítsa újra a PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d40ae-192">If you do start PowerShellGet by mistake, exit and restart PowerShell.</span></span>

```powershell
Import-Module F:\OfflinePowerShellGetDeploy

Install-PowerShellGetOffline -LocalFolder 'F:\OfflinePowerShellGet'
```

<span data-ttu-id="d40ae-193">A parancsok futtatása után készen áll a helyi tárházra a PowerShellGet közzététele.</span><span class="sxs-lookup"><span data-stu-id="d40ae-193">After running these commands, you are ready to publish PowerShellGet to your local repository.</span></span>

```powershell
# Publish to a NuGet Server repository using my NuGetAPI key
Publish-Module -Path 'F:\OfflinePowershellGet' -Repository LocalPsRepo -NuGetApiKey 'oy2bi4avlkjolp6bme6azdyssn6ps3iu7ib2qpiudrtbji'

# Publish to a file share repo - the NuGet API key must be a non-blank string
Publish-Module -Path 'F:\OfflinePowerShellGet' -Repository LocalPsRepo -NuGetApiKey 'AnyStringWillDo'
```

> [!IMPORTANT]
> <span data-ttu-id="d40ae-194">Ahhoz, hogy a biztonsági, API-kulcsok nem lehet változtatható parancsfájlokban.</span><span class="sxs-lookup"><span data-stu-id="d40ae-194">To ensure security, API keys should not be hard-coded in scripts.</span></span> <span data-ttu-id="d40ae-195">A biztonságos rendszert kell használnia.</span><span class="sxs-lookup"><span data-stu-id="d40ae-195">Use a secure key management system.</span></span>

<!-- external links -->
[OfflinePowerShellGetDeploy]: https://www.powershellgallery.com/packages/OfflinePowerShellGetDeploy/0.1.1
[Nuget.Server]: /nuget/hosting-packages/nuget-server
[nuget.exe]: /nuget/tools/nuget-exe-cli-reference
