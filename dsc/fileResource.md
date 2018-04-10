---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC-fájl erőforrás
ms.openlocfilehash: 7964eabe5f4585600ae80f3e5ff7439c0d954769
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-file-resource"></a><span data-ttu-id="d664f-103">A DSC-fájl erőforrás</span><span class="sxs-lookup"><span data-stu-id="d664f-103">DSC File Resource</span></span>

> <span data-ttu-id="d664f-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="d664f-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="d664f-105">A fájl erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a célcsomóponton lévő fájlokat és mappákat kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="d664f-105">The File resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage files and folders on the target node.</span></span>

><span data-ttu-id="d664f-106">**Megjegyzés:** Ha a **MatchSource** tulajdonsága **$false** (ez utóbbi érték az alapértelmezett érték), a tartalom másolása gyorsítótárba kerüljenek-e a konfiguráció alkalmazása először.</span><span class="sxs-lookup"><span data-stu-id="d664f-106">**Note:** If the **MatchSource** property is set to **$false** (which is the default value), the contents to be copied are cached the first time the configuration is applied.</span></span>
><span data-ttu-id="d664f-107">A konfiguráció további alkalmazások nem fogják keresni az frissített fájlok és/vagy mappák által megadott útvonal **SourcePath**.</span><span class="sxs-lookup"><span data-stu-id="d664f-107">Subsequent applications of the configuration will not check for updated files and/or folders in the path specified by **SourcePath**.</span></span> <span data-ttu-id="d664f-108">Ha szeretné-e a fájlokat vagy mappákat a frissítések keresése **SourcePath** minden alkalommal, amikor a konfiguráció alkalmazása, állítsa be **MatchSource** való **$true**.</span><span class="sxs-lookup"><span data-stu-id="d664f-108">If you want to check for updates to the files and/or folders in **SourcePath** every time the configuration is applied, set **MatchSource** to **$true**.</span></span>

## <a name="syntax"></a><span data-ttu-id="d664f-109">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="d664f-109">Syntax</span></span>
```
File [string] #ResourceName
{
    DestinationPath = [string]
    [ Attributes = [string[]] { Archive | Hidden | ReadOnly | System }]
    [ Checksum = [string] { CreatedDate | ModifiedDate | SHA-1 | SHA-256 | SHA-512 } ]
    [ Contents = [string] ]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Force = [bool] ]
    [ Recurse = [bool] ]
    [ DependsOn = [string[]] ]
    [ SourcePath = [string] ]
    [ Type = [string] { Directory | File } ]
    [ MatchSource = [bool] ]
}
```

## <a name="properties"></a><span data-ttu-id="d664f-110">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="d664f-110">Properties</span></span>

|  <span data-ttu-id="d664f-111">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="d664f-111">Property</span></span>  |  <span data-ttu-id="d664f-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="d664f-112">Description</span></span>   |
|---|---|
| <span data-ttu-id="d664f-113">DestinationPath</span><span class="sxs-lookup"><span data-stu-id="d664f-113">DestinationPath</span></span>| <span data-ttu-id="d664f-114">Azt jelzi, hogy a hely hol szeretne biztosítani a fájlok vagy könyvtárak állapotát.</span><span class="sxs-lookup"><span data-stu-id="d664f-114">Indicates the location where you want to ensure the state for a file or directory.</span></span>|
| <span data-ttu-id="d664f-115">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="d664f-115">Attributes</span></span>| <span data-ttu-id="d664f-116">Adja meg a kívánt állapot attribútumát a célként kijelölt fájl vagy könyvtár.</span><span class="sxs-lookup"><span data-stu-id="d664f-116">Specifies the desired state of the attributes for the targeted file or directory.</span></span>|
| <span data-ttu-id="d664f-117">Ellenőrzőösszeg</span><span class="sxs-lookup"><span data-stu-id="d664f-117">Checksum</span></span>| <span data-ttu-id="d664f-118">Azt jelzi, hogy az ellenőrzőösszeg-típust használ annak meghatározása, hogy két fájlok megegyeznek.</span><span class="sxs-lookup"><span data-stu-id="d664f-118">Indicates the checksum type to use when determining whether two files are the same.</span></span> <span data-ttu-id="d664f-119">Ha __ellenőrzőösszeg__ nincs megadva, csak a fájl vagy könyvtár neve Összehasonlításképpen szolgál.</span><span class="sxs-lookup"><span data-stu-id="d664f-119">If __Checksum__ is not specified, only the file or directory name is used for comparison.</span></span> <span data-ttu-id="d664f-120">Érvényes értékek a következők: SHA-1, SHA-256, SHA-512, createdDate, modifiedDate.</span><span class="sxs-lookup"><span data-stu-id="d664f-120">Valid values include: SHA-1, SHA-256, SHA-512, createdDate, modifiedDate.</span></span>|
| <span data-ttu-id="d664f-121">Tartalom</span><span class="sxs-lookup"><span data-stu-id="d664f-121">Contents</span></span>| <span data-ttu-id="d664f-122">Adja meg a fájlt, például egy adott karakterláncot.</span><span class="sxs-lookup"><span data-stu-id="d664f-122">Specifies the contents of a file, such as a particular string.</span></span>|
| <span data-ttu-id="d664f-123">hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="d664f-123">Credential</span></span>| <span data-ttu-id="d664f-124">Azt jelzi, a hitelesítő adatokat, amelyek hozzáférését az erőforrásokhoz, például a forrásfájlokat, kötelező, ha ilyen hozzáférés szükséges.</span><span class="sxs-lookup"><span data-stu-id="d664f-124">Indicates the credentials that are required to access resources, such as source files, if such access is required.</span></span>|
| <span data-ttu-id="d664f-125">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="d664f-125">Ensure</span></span>| <span data-ttu-id="d664f-126">Azt jelzi, hogy a fájl vagy könyvtár létezik-e.</span><span class="sxs-lookup"><span data-stu-id="d664f-126">Indicates if the file or directory exists.</span></span> <span data-ttu-id="d664f-127">Állítsa be ezt a tulajdonságot "Hiányzik", annak érdekében, hogy a fájl vagy könyvtár nem létezik.</span><span class="sxs-lookup"><span data-stu-id="d664f-127">Set this property to "Absent" to ensure that the file or directory does not exist.</span></span> <span data-ttu-id="d664f-128">Állítsa az értékét "Elérhető" Győződjön meg arról, hogy a fájl vagy könyvtár létezik.</span><span class="sxs-lookup"><span data-stu-id="d664f-128">Set it to "Present" to ensure that the file or directory does exist.</span></span> <span data-ttu-id="d664f-129">Az alapértelmezett érték az "Elérhető".</span><span class="sxs-lookup"><span data-stu-id="d664f-129">The default is "Present".</span></span>|
| <span data-ttu-id="d664f-130">Force</span><span class="sxs-lookup"><span data-stu-id="d664f-130">Force</span></span>| <span data-ttu-id="d664f-131">Egyes fájl műveletek (például a fájl felülírása vagy egy nem üres könyvtár törlése) hibát eredményez.</span><span class="sxs-lookup"><span data-stu-id="d664f-131">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="d664f-132">A kényszerített tulajdonság használatával felülbírálja az ilyen hibák.</span><span class="sxs-lookup"><span data-stu-id="d664f-132">Using the Force property overrides such errors.</span></span> <span data-ttu-id="d664f-133">Az alapértelmezett érték __$false__.</span><span class="sxs-lookup"><span data-stu-id="d664f-133">The default value is __$false__.</span></span>|
| <span data-ttu-id="d664f-134">Recurse</span><span class="sxs-lookup"><span data-stu-id="d664f-134">Recurse</span></span>| <span data-ttu-id="d664f-135">Azt jelzi, ha-e adva alkönyvtárak.</span><span class="sxs-lookup"><span data-stu-id="d664f-135">Indicates if subdirectories are included.</span></span> <span data-ttu-id="d664f-136">Ez a tulajdonság beállítása __$true__ annak jelzésére, hogy szeretné-e alkönyvtárakat is meg lehet adni.</span><span class="sxs-lookup"><span data-stu-id="d664f-136">Set this property to __$true__ to indicate that you want subdirectories to be included.</span></span> <span data-ttu-id="d664f-137">Az alapértelmezett érték __$false__.</span><span class="sxs-lookup"><span data-stu-id="d664f-137">The default is __$false__.</span></span> <span data-ttu-id="d664f-138">**Megjegyzés:**: Ez a tulajdonság csak akkor érvényes, ha a Type tulajdonság beállítása könyvtárba.</span><span class="sxs-lookup"><span data-stu-id="d664f-138">**Note**: This property is only valid when the Type property is set to Directory.</span></span>|
| <span data-ttu-id="d664f-139">dependsOn</span><span class="sxs-lookup"><span data-stu-id="d664f-139">DependsOn</span></span> | <span data-ttu-id="d664f-140">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="d664f-140">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="d664f-141">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="d664f-141">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="d664f-142">SourcePath</span><span class="sxs-lookup"><span data-stu-id="d664f-142">SourcePath</span></span>| <span data-ttu-id="d664f-143">Azt jelzi, hogy az elérési útja, amelyből a fájl vagy mappa erőforrás másolása.</span><span class="sxs-lookup"><span data-stu-id="d664f-143">Indicates the path from which to copy the file or folder resource.</span></span>|
| <span data-ttu-id="d664f-144">Típus</span><span class="sxs-lookup"><span data-stu-id="d664f-144">Type</span></span>| <span data-ttu-id="d664f-145">Azt jelzi, hogy az erőforrás konfigurálva-e egy könyvtár vagy fájl.</span><span class="sxs-lookup"><span data-stu-id="d664f-145">Indicates if the resource being configured is a directory or a file.</span></span> <span data-ttu-id="d664f-146">Ez azt jelzi, hogy az erőforrás egy könyvtár "Directory" tulajdonság értéke.</span><span class="sxs-lookup"><span data-stu-id="d664f-146">Set this property to "Directory" to indicate that the resource is a directory.</span></span> <span data-ttu-id="d664f-147">Állítsa az értékét "File" azt jelzi, hogy az erőforrás egy fájlt.</span><span class="sxs-lookup"><span data-stu-id="d664f-147">Set it to "File" to indicate that the resource is a file.</span></span> <span data-ttu-id="d664f-148">Az alapértelmezett érték: "File".</span><span class="sxs-lookup"><span data-stu-id="d664f-148">The default value is “File”.</span></span>|
| <span data-ttu-id="d664f-149">MatchSource</span><span class="sxs-lookup"><span data-stu-id="d664f-149">MatchSource</span></span>| <span data-ttu-id="d664f-150">Ha az alapértelmezett érték beállítása __$false__, majd a forrás (azaz fájlokat A, B és C) lévő fájlok nem kerülnek be a cél a konfiguráció alkalmazása először.</span><span class="sxs-lookup"><span data-stu-id="d664f-150">If set to the default value of __$false__, then any files on the source (say, files A, B, and C) will be added to the destination the first time the configuration is applied.</span></span> <span data-ttu-id="d664f-151">Ha egy új fájl (D) kerül a forrás-, az fog nem vehető fel a cél, akkor is, ha a konfiguráció alkalmazása újra később.</span><span class="sxs-lookup"><span data-stu-id="d664f-151">If a new file (D) is added to the source, it will not be added to the destination, even when the configuration is re-applied later.</span></span> <span data-ttu-id="d664f-152">Ha az érték __$true__, akkor minden alkalommal, amikor a konfiguráció alkalmazása, ezt követően a forrás (például D fájl ebben a példában) található új fájlokat vesznek fel a cél felé.</span><span class="sxs-lookup"><span data-stu-id="d664f-152">If the value is __$true__, then each time the configuration is applied, new files subsequently found on the source (such as file D in this example) are added to the destination.</span></span> <span data-ttu-id="d664f-153">Az alapértelmezett érték **$false**.</span><span class="sxs-lookup"><span data-stu-id="d664f-153">The default value is **$false**.</span></span>|

## <a name="example"></a><span data-ttu-id="d664f-154">Példa</span><span class="sxs-lookup"><span data-stu-id="d664f-154">Example</span></span>

<span data-ttu-id="d664f-155">A következő példa bemutatja, hogyan használja a fájl erőforrás annak érdekében, hogy egy könyvtárat az elérési úttal rendelkező `C:\Users\Public\Documents\DSCDemo\DemoSource` a forrás (például a "pull") a számítógépen megtalálható is (valamint minden alkönyvtár) célcsomóponton.</span><span class="sxs-lookup"><span data-stu-id="d664f-155">The following example shows how to use the File resource to ensure that a directory with the path `C:\Users\Public\Documents\DSCDemo\DemoSource` on a source computer (such as the “pull” server) is also present (along with all subdirectories) on the target node.</span></span> <span data-ttu-id="d664f-156">Egy megerősítő üzenet naplóba írás, ha a teljes és a annak érdekében, hogy fut-e a fájl-ellenőrzés művelet előtt a naplózási művelet egy utasítást tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="d664f-156">It also writes a confirmatory message to the log when complete and includes a statement to ensure that the file-checking operation runs prior to the logging operation.</span></span>

```powershell
Configuration FileResourceDemo
{
    Node "localhost"
    {
        File DirectoryCopy
        {
            Ensure = "Present"  # You can also set Ensure to "Absent"
            Type = "Directory" # Default is "File".
            Recurse = $true # Ensure presence of subdirectories, too
            SourcePath = "C:\Users\Public\Documents\DSCDemo\DemoSource"
            DestinationPath = "C:\Users\Public\Documents\DSCDemo\DemoDestination"
        }

        Log AfterDirectoryCopy
        {
            # The message below gets written to the Microsoft-Windows-Desired State Configuration/Analytic log
            Message = "Finished running the file resource with ID DirectoryCopy"
            DependsOn = "[File]DirectoryCopy" # This means run "DirectoryCopy" first.
        }
    }
}
```