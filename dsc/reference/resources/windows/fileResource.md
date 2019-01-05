---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-File erőforrás
ms.openlocfilehash: e5f7a91e5f19c8c7bbada090804d8f29a7cfedd5
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048523"
---
# <a name="dsc-file-resource"></a><span data-ttu-id="579bd-103">DSC-File erőforrás</span><span class="sxs-lookup"><span data-stu-id="579bd-103">DSC File Resource</span></span>

> <span data-ttu-id="579bd-104">Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="579bd-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="579bd-105">A fájl erőforrás a Windows PowerShell Desired State Configuration (DSC) lehetővé teszi a fájlok és mappák célcsomóponton kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="579bd-105">The File resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage files and folders on the target node.</span></span>

><span data-ttu-id="579bd-106">**Megjegyzés:** Ha a **MatchSource** tulajdonsága **$false** (amely a az alapértelmezett érték), a tartalmát, másolja a gyorsítótárazza a rendszer először a konfiguráció alkalmazása.</span><span class="sxs-lookup"><span data-stu-id="579bd-106">**Note:** If the **MatchSource** property is set to **$false** (which is the default value), the contents to be copied are cached the first time the configuration is applied.</span></span>
><span data-ttu-id="579bd-107">A konfiguráció további alkalmazásokat nem ellenőrzi a frissített fájlok és/vagy mappák által megadott útvonal **SourcePath**.</span><span class="sxs-lookup"><span data-stu-id="579bd-107">Subsequent applications of the configuration will not check for updated files and/or folders in the path specified by **SourcePath**.</span></span> <span data-ttu-id="579bd-108">Ha szeretné-e a fájlok és/vagy mappákat a frissítések keresése **SourcePath** minden alkalommal, amikor a konfigurációs van érvényben, állítsa be **MatchSource** való **$true**.</span><span class="sxs-lookup"><span data-stu-id="579bd-108">If you want to check for updates to the files and/or folders in **SourcePath** every time the configuration is applied, set **MatchSource** to **$true**.</span></span>

## <a name="syntax"></a><span data-ttu-id="579bd-109">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="579bd-109">Syntax</span></span>
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

## <a name="properties"></a><span data-ttu-id="579bd-110">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="579bd-110">Properties</span></span>

|  <span data-ttu-id="579bd-111">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="579bd-111">Property</span></span>  |  <span data-ttu-id="579bd-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="579bd-112">Description</span></span>   |
|---|---|
| <span data-ttu-id="579bd-113">DestinationPath</span><span class="sxs-lookup"><span data-stu-id="579bd-113">DestinationPath</span></span>| <span data-ttu-id="579bd-114">Azt jelzi, hogy a hely, ahol szeretne biztosítani egy fájl vagy könyvtár állapota.</span><span class="sxs-lookup"><span data-stu-id="579bd-114">Indicates the location where you want to ensure the state for a file or directory.</span></span>|
| <span data-ttu-id="579bd-115">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="579bd-115">Attributes</span></span>| <span data-ttu-id="579bd-116">Itt adhatja meg a kívánt állapotra a célként megadott fájl vagy könyvtár attribútumait.</span><span class="sxs-lookup"><span data-stu-id="579bd-116">Specifies the desired state of the attributes for the targeted file or directory.</span></span>|
| <span data-ttu-id="579bd-117">Ellenőrzőösszeg</span><span class="sxs-lookup"><span data-stu-id="579bd-117">Checksum</span></span>| <span data-ttu-id="579bd-118">Annak meghatározása,-e az azonos két fájlt használandó ellenőrzőösszeg típusát jelzi.</span><span class="sxs-lookup"><span data-stu-id="579bd-118">Indicates the checksum type to use when determining whether two files are the same.</span></span> <span data-ttu-id="579bd-119">Ha __ellenőrzőösszeg__ nincs megadva, csak a fájl vagy könyvtár nevét használja az összehasonlítást.</span><span class="sxs-lookup"><span data-stu-id="579bd-119">If __Checksum__ is not specified, only the file or directory name is used for comparison.</span></span> <span data-ttu-id="579bd-120">Érvényes értékek a következők: Az SHA-1, SHA-256, SHA-512, createdDate, modifiedDate.</span><span class="sxs-lookup"><span data-stu-id="579bd-120">Valid values include: SHA-1, SHA-256, SHA-512, createdDate, modifiedDate.</span></span>|
| <span data-ttu-id="579bd-121">Tartalom</span><span class="sxs-lookup"><span data-stu-id="579bd-121">Contents</span></span>| <span data-ttu-id="579bd-122">Itt adhatja meg, például egy adott karakterláncot egy fájl tartalmát.</span><span class="sxs-lookup"><span data-stu-id="579bd-122">Specifies the contents of a file, such as a particular string.</span></span>|
| <span data-ttu-id="579bd-123">Hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="579bd-123">Credential</span></span>| <span data-ttu-id="579bd-124">A hitelesítő adatokat, amelyek szükségesek a hozzáférési erőforrások, például a forrásfájlokat, azt jelzi, ha ilyen hozzáférésre szüksége.</span><span class="sxs-lookup"><span data-stu-id="579bd-124">Indicates the credentials that are required to access resources, such as source files, if such access is required.</span></span>|
| <span data-ttu-id="579bd-125">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="579bd-125">Ensure</span></span>| <span data-ttu-id="579bd-126">Azt jelzi, hogy a fájl vagy könyvtár létezik-e.</span><span class="sxs-lookup"><span data-stu-id="579bd-126">Indicates if the file or directory exists.</span></span> <span data-ttu-id="579bd-127">Állítsa be ezt a tulajdonságot a "Hiányzó" annak érdekében, hogy a fájl vagy könyvtár nem létezik.</span><span class="sxs-lookup"><span data-stu-id="579bd-127">Set this property to "Absent" to ensure that the file or directory does not exist.</span></span> <span data-ttu-id="579bd-128">Állítsa a "E" Győződjön meg arról, hogy a fájl vagy könyvtár létezik.</span><span class="sxs-lookup"><span data-stu-id="579bd-128">Set it to "Present" to ensure that the file or directory does exist.</span></span> <span data-ttu-id="579bd-129">Az alapértelmezett érték "E".</span><span class="sxs-lookup"><span data-stu-id="579bd-129">The default is "Present".</span></span>|
| <span data-ttu-id="579bd-130">Force</span><span class="sxs-lookup"><span data-stu-id="579bd-130">Force</span></span>| <span data-ttu-id="579bd-131">Bizonyos fájl műveletek (például fájl felülírása vagy egy nem üres könyvtár törlése) hibát eredményez.</span><span class="sxs-lookup"><span data-stu-id="579bd-131">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="579bd-132">A kényszerített tulajdonságot felülbírálja az ilyen hibák.</span><span class="sxs-lookup"><span data-stu-id="579bd-132">Using the Force property overrides such errors.</span></span> <span data-ttu-id="579bd-133">Az alapértelmezett érték __$false__.</span><span class="sxs-lookup"><span data-stu-id="579bd-133">The default value is __$false__.</span></span>|
| <span data-ttu-id="579bd-134">Parancs recurse kapcsolójának</span><span class="sxs-lookup"><span data-stu-id="579bd-134">Recurse</span></span>| <span data-ttu-id="579bd-135">Azt jelzi, ha alkönyvtárakat tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="579bd-135">Indicates if subdirectories are included.</span></span> <span data-ttu-id="579bd-136">Ez a tulajdonság beállítása __$true__ jelzi, hogy szeretné-e alkönyvtárak fogja tartalmazni.</span><span class="sxs-lookup"><span data-stu-id="579bd-136">Set this property to __$true__ to indicate that you want subdirectories to be included.</span></span> <span data-ttu-id="579bd-137">Az alapértelmezett érték __$false__.</span><span class="sxs-lookup"><span data-stu-id="579bd-137">The default is __$false__.</span></span> <span data-ttu-id="579bd-138">**Megjegyzés:**: Ez a tulajdonság csak akkor érvényes, ha a tulajdonság beállítása könyvtárba.</span><span class="sxs-lookup"><span data-stu-id="579bd-138">**Note**: This property is only valid when the Type property is set to Directory.</span></span>|
| <span data-ttu-id="579bd-139">DependsOn</span><span class="sxs-lookup"><span data-stu-id="579bd-139">DependsOn</span></span> | <span data-ttu-id="579bd-140">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="579bd-140">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="579bd-141">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="579bd-141">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="579bd-142">SourcePath</span><span class="sxs-lookup"><span data-stu-id="579bd-142">SourcePath</span></span>| <span data-ttu-id="579bd-143">Azt jelzi, hogy az elérési utat, amelyről a fájl vagy mappa erőforrás másolásához.</span><span class="sxs-lookup"><span data-stu-id="579bd-143">Indicates the path from which to copy the file or folder resource.</span></span>|
| <span data-ttu-id="579bd-144">Típus</span><span class="sxs-lookup"><span data-stu-id="579bd-144">Type</span></span>| <span data-ttu-id="579bd-145">Azt jelzi, hogy az erőforráshoz konfigurált egy könyvtárat vagy fájl.</span><span class="sxs-lookup"><span data-stu-id="579bd-145">Indicates if the resource being configured is a directory or a file.</span></span> <span data-ttu-id="579bd-146">Ez azt jelzi, hogy az erőforrás egy könyvtárat a "Directory" tulajdonság értéke.</span><span class="sxs-lookup"><span data-stu-id="579bd-146">Set this property to "Directory" to indicate that the resource is a directory.</span></span> <span data-ttu-id="579bd-147">Állítsa a "File" azt jelzi, hogy az erőforrás egy fájlt.</span><span class="sxs-lookup"><span data-stu-id="579bd-147">Set it to "File" to indicate that the resource is a file.</span></span> <span data-ttu-id="579bd-148">Az alapértelmezett érték: "File".</span><span class="sxs-lookup"><span data-stu-id="579bd-148">The default value is “File”.</span></span>|
| <span data-ttu-id="579bd-149">MatchSource</span><span class="sxs-lookup"><span data-stu-id="579bd-149">MatchSource</span></span>| <span data-ttu-id="579bd-150">Ha az alapértelmezett értékre állítva __$false__, majd a forrás (pl.: fájlok A, B és C) lévő fájlok az első alkalommal a konfiguráció alkalmazása hozzáadódik a célhelyen.</span><span class="sxs-lookup"><span data-stu-id="579bd-150">If set to the default value of __$false__, then any files on the source (say, files A, B, and C) will be added to the destination the first time the configuration is applied.</span></span> <span data-ttu-id="579bd-151">(D) új fájl kerül, a forrás-, ha azt fogja nem vehető fel a cél, akkor is, ha a konfiguráció alkalmazása újra később.</span><span class="sxs-lookup"><span data-stu-id="579bd-151">If a new file (D) is added to the source, it will not be added to the destination, even when the configuration is re-applied later.</span></span> <span data-ttu-id="579bd-152">Ha az érték __$true__, akkor minden alkalommal, amikor a konfigurációs van érvényben, ezt követően a forrás (például D fájl ebben a példában) található új fájlokat adnak hozzá a célhelyen.</span><span class="sxs-lookup"><span data-stu-id="579bd-152">If the value is __$true__, then each time the configuration is applied, new files subsequently found on the source (such as file D in this example) are added to the destination.</span></span> <span data-ttu-id="579bd-153">Az alapértelmezett érték **$false**.</span><span class="sxs-lookup"><span data-stu-id="579bd-153">The default value is **$false**.</span></span>|

## <a name="example"></a><span data-ttu-id="579bd-154">Példa</span><span class="sxs-lookup"><span data-stu-id="579bd-154">Example</span></span>

<span data-ttu-id="579bd-155">Az alábbi példa bemutatja, hogyan használhatja a File resource annak érdekében, hogy egy könyvtárat az elérési útját `C:\Users\Public\Documents\DSCDemo\DemoSource` egy forrást a számítógépen (például a "PULL parancs" kiszolgáló) is jelen (együtt az összes alkönyvtár) célcsomóponton.</span><span class="sxs-lookup"><span data-stu-id="579bd-155">The following example shows how to use the File resource to ensure that a directory with the path `C:\Users\Public\Documents\DSCDemo\DemoSource` on a source computer (such as the “pull” server) is also present (along with all subdirectories) on the target node.</span></span> <span data-ttu-id="579bd-156">Ez is egy megerősítő üzenetet írja a naplóba, amikor végzett és a egy nyilatkozatot, győződjön meg arról, hogy fut-e a fájl-ellenőrzés műveletet a naplózási művelet előtt.</span><span class="sxs-lookup"><span data-stu-id="579bd-156">It also writes a confirmatory message to the log when complete and includes a statement to ensure that the file-checking operation runs prior to the logging operation.</span></span>

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