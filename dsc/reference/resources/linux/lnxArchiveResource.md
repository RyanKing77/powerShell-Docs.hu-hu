---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxArchive erőforrás
ms.openlocfilehash: 800954478f149e29c22d1a88304c3be9950f109a
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048474"
---
# <a name="dsc-for-linux-nxarchive-resource"></a><span data-ttu-id="4dd66-103">DSC, a Linux nxArchive erőforrás</span><span class="sxs-lookup"><span data-stu-id="4dd66-103">DSC for Linux nxArchive Resource</span></span>

<span data-ttu-id="4dd66-104">A **nxArchive** erőforrás a PowerShell Desired State Configuration (DSC), csomagolja ki az archív (.tar, .zip kiterjesztésű) fájlok egy adott elérési úton található egy Linux-csomóponton mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="4dd66-104">The **nxArchive** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to unpack archive (.tar, .zip) files at a specific path on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="4dd66-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="4dd66-105">Syntax</span></span>

```
nxArchive <string> #ResourceName
{
    SourcePath = <string>
    DestinationPath = <string>
    [ Checksum = <string> { ctime | mtime | md5 }  ]
    [ Force = <bool> ]
    [ DependsOn = <string[]> ]
    [ Ensure = <string> { Absent | Present }  ]
}
```

## <a name="properties"></a><span data-ttu-id="4dd66-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="4dd66-106">Properties</span></span>

|  <span data-ttu-id="4dd66-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="4dd66-107">Property</span></span> |  <span data-ttu-id="4dd66-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="4dd66-108">Description</span></span> |
|---|---|
| <span data-ttu-id="4dd66-109">SourcePath</span><span class="sxs-lookup"><span data-stu-id="4dd66-109">SourcePath</span></span>| <span data-ttu-id="4dd66-110">Forrás elérési utat határozza meg az archív fájl.</span><span class="sxs-lookup"><span data-stu-id="4dd66-110">Specifies the source path of the archive file.</span></span> <span data-ttu-id="4dd66-111">Ez lehet egy .tar .zip, vagy a. tar.gz fájlt.</span><span class="sxs-lookup"><span data-stu-id="4dd66-111">This should be a .tar, .zip, or .tar.gz file.</span></span> |
| <span data-ttu-id="4dd66-112">DestinationPath</span><span class="sxs-lookup"><span data-stu-id="4dd66-112">DestinationPath</span></span>| <span data-ttu-id="4dd66-113">Itt adhatja meg a helyet, ahol szeretne biztosítani, ki kell olvasni az archívum tartalmát.</span><span class="sxs-lookup"><span data-stu-id="4dd66-113">Specifies the location where you want to ensure the archive contents are extracted.</span></span>|
| <span data-ttu-id="4dd66-114">Ellenőrzőösszeg</span><span class="sxs-lookup"><span data-stu-id="4dd66-114">Checksum</span></span>| <span data-ttu-id="4dd66-115">Határozza meg, amely meghatározza, hogy a forrás-archívumot frissítve lett-e használni kívánt típusát.</span><span class="sxs-lookup"><span data-stu-id="4dd66-115">Defines the type to use when determining whether the source archive has been updated.</span></span> <span data-ttu-id="4dd66-116">Értékek a következők: "ctime", "mtime", vagy a "md5".</span><span class="sxs-lookup"><span data-stu-id="4dd66-116">Values are: "ctime", "mtime", or "md5".</span></span> <span data-ttu-id="4dd66-117">Az alapértelmezett érték: "md5".</span><span class="sxs-lookup"><span data-stu-id="4dd66-117">The default value is "md5".</span></span>|
| <span data-ttu-id="4dd66-118">Force</span><span class="sxs-lookup"><span data-stu-id="4dd66-118">Force</span></span>| <span data-ttu-id="4dd66-119">Bizonyos fájl műveletek (például fájl felülírása vagy egy nem üres könyvtár törlése) hibát eredményez.</span><span class="sxs-lookup"><span data-stu-id="4dd66-119">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="4dd66-120">Használatával a **kényszerített** tulajdonság felülbírálja az ilyen hibák.</span><span class="sxs-lookup"><span data-stu-id="4dd66-120">Using the **Force** property overrides such errors.</span></span> <span data-ttu-id="4dd66-121">Az alapértelmezett érték **$false**.</span><span class="sxs-lookup"><span data-stu-id="4dd66-121">The default value is **$false**.</span></span>|
| <span data-ttu-id="4dd66-122">DependsOn</span><span class="sxs-lookup"><span data-stu-id="4dd66-122">DependsOn</span></span> | <span data-ttu-id="4dd66-123">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="4dd66-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="4dd66-124">Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="4dd66-124">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="4dd66-125">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="4dd66-125">Ensure</span></span>| <span data-ttu-id="4dd66-126">Határozza meg, ellenőrizze, hogy az archívum tartalmát a **cél**.</span><span class="sxs-lookup"><span data-stu-id="4dd66-126">Determines whether to check if the content of the archive exists at the **Destination**.</span></span> <span data-ttu-id="4dd66-127">Ezzel a tulajdonsággal, "E" annak érdekében, hogy a tartalom létezik.</span><span class="sxs-lookup"><span data-stu-id="4dd66-127">Set this property to "Present" to ensure the contents exist.</span></span> <span data-ttu-id="4dd66-128">Állítsa a "Hiányzó" annak érdekében, még nem léteznek.</span><span class="sxs-lookup"><span data-stu-id="4dd66-128">Set it to "Absent" to ensure they do not exist.</span></span> <span data-ttu-id="4dd66-129">Az alapértelmezett érték: "E".</span><span class="sxs-lookup"><span data-stu-id="4dd66-129">The default value is "Present".</span></span>|

## <a name="example"></a><span data-ttu-id="4dd66-130">Példa</span><span class="sxs-lookup"><span data-stu-id="4dd66-130">Example</span></span>

<span data-ttu-id="4dd66-131">Az alábbi példa bemutatja, hogyan használható a **nxArchive** erőforrást, győződjön meg arról, hogy archív fájl tartalmának neve `website.tar` létezik, és a egy adott célhelyen ki kell olvasni.</span><span class="sxs-lookup"><span data-stu-id="4dd66-131">The following example shows how to use the **nxArchive** resource to ensure that the contents of an archive file called `website.tar` exist and are extracted at a given destination.</span></span>

```
Import-DSCResource -Module nx

nxFile SyncArchiveFromWeb
{
   Ensure = "Present"
   SourcePath = “http://release.contoso.com/releases/website.tar”
   DestinationPath = "/usr/release/staging/website.tar"
   Type = "File"
   Checksum = “mtime”
}

nxArchive SyncWebDir
{
   SourcePath = “/usr/release/staging/website.tar”
   DestinationPath = “/usr/local/apache2/htdocs/”
   Force = $false
   DependsOn = "[nxFile]SyncArchiveFromWeb"
}
```