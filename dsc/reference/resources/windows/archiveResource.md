---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC archív erőforrás
ms.openlocfilehash: d5ccd242d000a0907c6768f30923764be6bf20a3
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62077551"
---
# <a name="dsc-archive-resource"></a><span data-ttu-id="2c7c2-103">DSC archív erőforrás</span><span class="sxs-lookup"><span data-stu-id="2c7c2-103">DSC Archive Resource</span></span>

> <span data-ttu-id="2c7c2-104">A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="2c7c2-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="2c7c2-105">Az archív erőforrás a Windows PowerShell Desired State Configuration (DSC), csomagolja ki az archív (.zip kiterjesztésű) fájlok egy adott elérési úton mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="2c7c2-105">The Archive resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to unpack archive (.zip) files at a specific path.</span></span>

## <a name="syntax"></a><span data-ttu-id="2c7c2-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="2c7c2-106">Syntax</span></span>
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

## <a name="properties"></a><span data-ttu-id="2c7c2-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="2c7c2-107">Properties</span></span>

|  <span data-ttu-id="2c7c2-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="2c7c2-108">Property</span></span>  |  <span data-ttu-id="2c7c2-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="2c7c2-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="2c7c2-110">Cél</span><span class="sxs-lookup"><span data-stu-id="2c7c2-110">Destination</span></span>| <span data-ttu-id="2c7c2-111">Itt adhatja meg a helyet, ahol szeretne biztosítani, ki kell olvasni az archívum tartalmát.</span><span class="sxs-lookup"><span data-stu-id="2c7c2-111">Specifies the location where you want to ensure the archive contents are extracted.</span></span>|
| <span data-ttu-id="2c7c2-112">Elérési út</span><span class="sxs-lookup"><span data-stu-id="2c7c2-112">Path</span></span>| <span data-ttu-id="2c7c2-113">Forrás elérési utat határozza meg az archív fájl.</span><span class="sxs-lookup"><span data-stu-id="2c7c2-113">Specifies the source path of the archive file.</span></span>|
| <span data-ttu-id="2c7c2-114">__Ellenőrzőösszeg__</span><span class="sxs-lookup"><span data-stu-id="2c7c2-114">__Checksum__</span></span>| <span data-ttu-id="2c7c2-115">Határozza meg, amely meghatározza, hogy-e az azonos két fájlt használni kívánt típusát.</span><span class="sxs-lookup"><span data-stu-id="2c7c2-115">Defines the type to use when determining whether two files are the same.</span></span> <span data-ttu-id="2c7c2-116">Ha __ellenőrzőösszeg__ nincs megadva, csak a fájl vagy könyvtár nevét használja az összehasonlítást.</span><span class="sxs-lookup"><span data-stu-id="2c7c2-116">If __Checksum__ is not specified, only the file or directory name is used for comparison.</span></span> <span data-ttu-id="2c7c2-117">Érvényes értékek a következők: Az SHA-1, SHA-256, SHA-512, createdDate, modifiedDate, egyik sem (alapértelmezett).</span><span class="sxs-lookup"><span data-stu-id="2c7c2-117">Valid values include: SHA-1, SHA-256, SHA-512, createdDate, modifiedDate, none (default).</span></span> <span data-ttu-id="2c7c2-118">Ha megad __ellenőrzőösszeg__ nélkül __ellenőrzése__, a konfigurálása sikertelen lesz.</span><span class="sxs-lookup"><span data-stu-id="2c7c2-118">If you specify __Checksum__ without __Validate__, the configuration will fail.</span></span>|
| <span data-ttu-id="2c7c2-119">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="2c7c2-119">Ensure</span></span>| <span data-ttu-id="2c7c2-120">Határozza meg, ellenőrizze, hogy az archívum tartalmát a __cél__.</span><span class="sxs-lookup"><span data-stu-id="2c7c2-120">Determines whether to check if the content of the archive exists at the __Destination__.</span></span> <span data-ttu-id="2c7c2-121">Ez a tulajdonság beállítása __jelen__ annak érdekében, hogy a tartalom létezik.</span><span class="sxs-lookup"><span data-stu-id="2c7c2-121">Set this property to __Present__ to ensure the contents exist.</span></span> <span data-ttu-id="2c7c2-122">Állítsa be __távol__ annak érdekében, még nem léteznek.</span><span class="sxs-lookup"><span data-stu-id="2c7c2-122">Set it to __Absent__ to ensure they do not exist.</span></span> <span data-ttu-id="2c7c2-123">Az alapértelmezett érték __jelen__.</span><span class="sxs-lookup"><span data-stu-id="2c7c2-123">The default value is __Present__.</span></span>|
| <span data-ttu-id="2c7c2-124">DependsOn</span><span class="sxs-lookup"><span data-stu-id="2c7c2-124">DependsOn</span></span> | <span data-ttu-id="2c7c2-125">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="2c7c2-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="2c7c2-126">Például, ha az erőforrás konfigurációs parancsprogram-blokkot, amelyet futtatni szeretne azonosítója először ResourceName és a típus azt __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="2c7c2-126">For example, if the ID of the resource configuration script block that you want to run first is ResourceName and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="2c7c2-127">Validate</span><span class="sxs-lookup"><span data-stu-id="2c7c2-127">Validate</span></span>| <span data-ttu-id="2c7c2-128">Az ellenőrzőösszeg-tulajdonság segítségével határozza meg, ha az archívum megfelel-e az aláírás.</span><span class="sxs-lookup"><span data-stu-id="2c7c2-128">Uses the Checksum property to determine if the archive matches the signature.</span></span> <span data-ttu-id="2c7c2-129">Az ellenőrzőösszeg érvényesítése nélkül adja meg, ha a konfiguráció sikertelen lesz.</span><span class="sxs-lookup"><span data-stu-id="2c7c2-129">If you specify Checksum without Validate, the configuration will fail.</span></span> <span data-ttu-id="2c7c2-130">Ha ellenőrzése ellenőrzőösszeg nélkül adja meg, SHA-256 ellenőrzőösszeg alapértelmezett használják.</span><span class="sxs-lookup"><span data-stu-id="2c7c2-130">If you specify Validate without Checksum, a SHA-256 checksum is used by default.</span></span>|
| <span data-ttu-id="2c7c2-131">Force</span><span class="sxs-lookup"><span data-stu-id="2c7c2-131">Force</span></span>| <span data-ttu-id="2c7c2-132">Bizonyos fájl műveletek (például fájl felülírása vagy egy nem üres könyvtár törlése) hibát eredményez.</span><span class="sxs-lookup"><span data-stu-id="2c7c2-132">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="2c7c2-133">A kényszerített tulajdonságot felülbírálja az ilyen hibák.</span><span class="sxs-lookup"><span data-stu-id="2c7c2-133">Using the Force property overrides such errors.</span></span> <span data-ttu-id="2c7c2-134">Az alapértelmezett érték: False.</span><span class="sxs-lookup"><span data-stu-id="2c7c2-134">The default value is False.</span></span>|

## <a name="example"></a><span data-ttu-id="2c7c2-135">Példa</span><span class="sxs-lookup"><span data-stu-id="2c7c2-135">Example</span></span>

<span data-ttu-id="2c7c2-136">Az alábbi példa bemutatja, hogyan biztosíthatja, hogy létezik Test.zip nevű archív fájl tartalmát, és egy adott célhelyen ki kell olvasni az archív erőforrás használatára.</span><span class="sxs-lookup"><span data-stu-id="2c7c2-136">The following example shows how to use the Archive resource to ensure that the contents of an archive file called Test.zip exist and are extracted at a given destination.</span></span>

```
Archive ArchiveExample {
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Path = "C:\Users\Public\Documents\Test.zip"
    Destination = "C:\Users\Public\Documents\ExtractionPath"
}
```