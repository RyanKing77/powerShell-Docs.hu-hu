---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC-archívum erőforrás"
ms.openlocfilehash: 0e9515f801888233148afcf1dbaebf85b28a6d79
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-archive-resource"></a><span data-ttu-id="a5452-103">A DSC-archívum erőforrás</span><span class="sxs-lookup"><span data-stu-id="a5452-103">DSC Archive Resource</span></span>

> <span data-ttu-id="a5452-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="a5452-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="a5452-105">Az archív erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a kicsomagolásához (.zip) archív fájlok egy adott elérési úton.</span><span class="sxs-lookup"><span data-stu-id="a5452-105">The Archive resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to unpack archive (.zip) files at a specific path.</span></span>

## <a name="syntax"></a><span data-ttu-id="a5452-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="a5452-106">Syntax</span></span>
```MOF
Archive [string] #ResourceName
{
    Destination = [string]
    Path = [string]
    [ Checksum = [string] { CreatedDate | ModifiedDate | SHA-1 | SHA-256 | SHA-512 } ]
    [ DependsOn = [string[]] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Force = [bool] ]
    [ Validate = [bool] ]
}
```

## <a name="properties"></a><span data-ttu-id="a5452-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="a5452-107">Properties</span></span>

|  <span data-ttu-id="a5452-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="a5452-108">Property</span></span>  |  <span data-ttu-id="a5452-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="a5452-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="a5452-110">Cél</span><span class="sxs-lookup"><span data-stu-id="a5452-110">Destination</span></span>| <span data-ttu-id="a5452-111">Adja meg a helyét az archív tartalom kibontása biztosításához.</span><span class="sxs-lookup"><span data-stu-id="a5452-111">Specifies the location where you want to ensure the archive contents are extracted.</span></span>|
| <span data-ttu-id="a5452-112">Elérési út</span><span class="sxs-lookup"><span data-stu-id="a5452-112">Path</span></span>| <span data-ttu-id="a5452-113">Az archív fájl a forrás elérési útját adja meg.</span><span class="sxs-lookup"><span data-stu-id="a5452-113">Specifies the source path of the archive file.</span></span>|
| <span data-ttu-id="a5452-114">__Ellenőrzőösszeg__</span><span class="sxs-lookup"><span data-stu-id="a5452-114">__Checksum__</span></span>| <span data-ttu-id="a5452-115">Annak meghatározása, hogy két fájlok megegyeznek használandó típust határozza meg.</span><span class="sxs-lookup"><span data-stu-id="a5452-115">Defines the type to use when determining whether two files are the same.</span></span> <span data-ttu-id="a5452-116">Ha __ellenőrzőösszeg__ nincs megadva, csak a fájl vagy könyvtár neve Összehasonlításképpen szolgál.</span><span class="sxs-lookup"><span data-stu-id="a5452-116">If __Checksum__ is not specified, only the file or directory name is used for comparison.</span></span> <span data-ttu-id="a5452-117">Érvényes értékek a következők: SHA-1, SHA-256, SHA-512, createdDate, modifiedDate, nincs (alapértelmezett).</span><span class="sxs-lookup"><span data-stu-id="a5452-117">Valid values include: SHA-1, SHA-256, SHA-512, createdDate, modifiedDate, none (default).</span></span> <span data-ttu-id="a5452-118">Ha megad __ellenőrzőösszeg__ nélkül __ellenőrzése__, a konfiguráció sikertelen lesz.</span><span class="sxs-lookup"><span data-stu-id="a5452-118">If you specify __Checksum__ without __Validate__, the configuration will fail.</span></span>|
| <span data-ttu-id="a5452-119">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="a5452-119">Ensure</span></span>| <span data-ttu-id="a5452-120">Meghatározza, hogy ellenőrizze, hogy létezik-e a tartalom az archívum a __cél__.</span><span class="sxs-lookup"><span data-stu-id="a5452-120">Determines whether to check if the content of the archive exists at the __Destination__.</span></span> <span data-ttu-id="a5452-121">Ez a tulajdonság beállítása __jelen__ annak érdekében, hogy a tartalom található.</span><span class="sxs-lookup"><span data-stu-id="a5452-121">Set this property to __Present__ to ensure the contents exist.</span></span> <span data-ttu-id="a5452-122">Állítsa az értékét __távol__ annak érdekében, hogy azok nem léteznek.</span><span class="sxs-lookup"><span data-stu-id="a5452-122">Set it to __Absent__ to ensure they do not exist.</span></span> <span data-ttu-id="a5452-123">Az alapértelmezett érték __jelen__.</span><span class="sxs-lookup"><span data-stu-id="a5452-123">The default value is __Present__.</span></span>|
| <span data-ttu-id="a5452-124">dependsOn</span><span class="sxs-lookup"><span data-stu-id="a5452-124">DependsOn</span></span> | <span data-ttu-id="a5452-125">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="a5452-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="a5452-126">Például ha erőforrás konfigurációs parancsprogram-blokk futtatni kívánt azonosító először ResourceName és annak típusára is __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="a5452-126">For example, if the ID of the resource configuration script block that you want to run first is ResourceName and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="a5452-127">Ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="a5452-127">Validate</span></span>| <span data-ttu-id="a5452-128">Az ellenőrzőösszeg-tulajdonság segítségével határozza meg, ha az archívum megfelel-e az aláírás.</span><span class="sxs-lookup"><span data-stu-id="a5452-128">Uses the Checksum property to determine if the archive matches the signature.</span></span> <span data-ttu-id="a5452-129">Ha megadja az ellenőrzőösszeg-érvényesítés nélkül, a konfiguráció sikertelen lesz.</span><span class="sxs-lookup"><span data-stu-id="a5452-129">If you specify Checksum without Validate, the configuration will fail.</span></span> <span data-ttu-id="a5452-130">Ha megad nélkül ellenőrzőösszegének ellenőrzése, SHA-256 ellenőrzőösszeg alapértelmezett használja.</span><span class="sxs-lookup"><span data-stu-id="a5452-130">If you specify Validate without Checksum, a SHA-256 checksum is used by default.</span></span>|
| <span data-ttu-id="a5452-131">Force</span><span class="sxs-lookup"><span data-stu-id="a5452-131">Force</span></span>| <span data-ttu-id="a5452-132">Egyes fájl műveletek (például a fájl felülírása vagy egy nem üres könyvtár törlése) hibát eredményez.</span><span class="sxs-lookup"><span data-stu-id="a5452-132">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="a5452-133">A kényszerített tulajdonság használatával felülbírálja az ilyen hibák.</span><span class="sxs-lookup"><span data-stu-id="a5452-133">Using the Force property overrides such errors.</span></span> <span data-ttu-id="a5452-134">Az alapértelmezett értéke False.</span><span class="sxs-lookup"><span data-stu-id="a5452-134">The default value is False.</span></span>|

## <a name="example"></a><span data-ttu-id="a5452-135">Példa</span><span class="sxs-lookup"><span data-stu-id="a5452-135">Example</span></span>

<span data-ttu-id="a5452-136">A következő példa bemutatja, hogyan használható az archív erőforrás győződjön meg arról, hogy egy Test.zip nevű archív fájl létezik-e, és ki kell olvasni a megadott célhelyen.</span><span class="sxs-lookup"><span data-stu-id="a5452-136">The following example shows how to use the Archive resource to ensure that the contents of an archive file called Test.zip exist and are extracted at a given destination.</span></span>

```
Archive ArchiveExample {
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Path = "C:\Users\Public\Documents\Test.zip"
    Destination = "C:\Users\Public\Documents\ExtractionPath"
}
```

