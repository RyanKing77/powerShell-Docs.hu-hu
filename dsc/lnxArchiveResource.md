---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A Linux nxArchive erőforrás DSC"
ms.openlocfilehash: da647432e14d2a4a3ceb2a36c7dee2dbfd350116
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-for-linux-nxarchive-resource"></a><span data-ttu-id="59419-103">A Linux nxArchive erőforrás DSC</span><span class="sxs-lookup"><span data-stu-id="59419-103">DSC for Linux nxArchive Resource</span></span>

<span data-ttu-id="59419-104">A **nxArchive** a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) erőforrás (.tar, .zip) archív fájlok egy adott elérési úton egy Linux-csomóponton kicsomagolásához mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="59419-104">The **nxArchive** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to unpack archive (.tar, .zip) files at a specific path on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="59419-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="59419-105">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="59419-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="59419-106">Properties</span></span>

|  <span data-ttu-id="59419-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="59419-107">Property</span></span> |  <span data-ttu-id="59419-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="59419-108">Description</span></span> | 
|---|---|
| <span data-ttu-id="59419-109">SourcePath</span><span class="sxs-lookup"><span data-stu-id="59419-109">SourcePath</span></span>| <span data-ttu-id="59419-110">Az archív fájl a forrás elérési útját adja meg.</span><span class="sxs-lookup"><span data-stu-id="59419-110">Specifies the source path of the archive file.</span></span> <span data-ttu-id="59419-111">Ez legyen a .tar .zip, vagy a. tar.gz fájlt.</span><span class="sxs-lookup"><span data-stu-id="59419-111">This should be a .tar, .zip, or .tar.gz file.</span></span> | 
| <span data-ttu-id="59419-112">DestinationPath</span><span class="sxs-lookup"><span data-stu-id="59419-112">DestinationPath</span></span>| <span data-ttu-id="59419-113">Adja meg a helyét az archív tartalom kibontása biztosításához.</span><span class="sxs-lookup"><span data-stu-id="59419-113">Specifies the location where you want to ensure the archive contents are extracted.</span></span>| 
| <span data-ttu-id="59419-114">Ellenőrzőösszeg</span><span class="sxs-lookup"><span data-stu-id="59419-114">Checksum</span></span>| <span data-ttu-id="59419-115">Határozza meg a típust használ annak meghatározása, hogy a forrás archív frissítve lett.</span><span class="sxs-lookup"><span data-stu-id="59419-115">Defines the type to use when determining whether the source archive has been updated.</span></span> <span data-ttu-id="59419-116">Értékek: "ctime", "mtime" vagy "md5".</span><span class="sxs-lookup"><span data-stu-id="59419-116">Values are: "ctime", "mtime", or "md5".</span></span> <span data-ttu-id="59419-117">Az alapértelmezett érték: "md5".</span><span class="sxs-lookup"><span data-stu-id="59419-117">The default value is "md5".</span></span>| 
| <span data-ttu-id="59419-118">Force</span><span class="sxs-lookup"><span data-stu-id="59419-118">Force</span></span>| <span data-ttu-id="59419-119">Egyes fájl műveletek (például a fájl felülírása vagy egy nem üres könyvtár törlése) hibát eredményez.</span><span class="sxs-lookup"><span data-stu-id="59419-119">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="59419-120">Használja a **kényszerített** a tulajdonság felülírja az ilyen hibák.</span><span class="sxs-lookup"><span data-stu-id="59419-120">Using the **Force** property overrides such errors.</span></span> <span data-ttu-id="59419-121">Az alapértelmezett érték **$false**.</span><span class="sxs-lookup"><span data-stu-id="59419-121">The default value is **$false**.</span></span>| 
| <span data-ttu-id="59419-122">dependsOn</span><span class="sxs-lookup"><span data-stu-id="59419-122">DependsOn</span></span> | <span data-ttu-id="59419-123">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="59419-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="59419-124">Például ha a **azonosító** az erőforrás konfigurációs futtatni kívánt először parancsprogramblokkja **ResourceName** és annak típusa **ResourceType**, ez a szintaxis a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="59419-124">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 
| <span data-ttu-id="59419-125">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="59419-125">Ensure</span></span>| <span data-ttu-id="59419-126">Meghatározza, hogy ellenőrizze, hogy létezik-e a tartalom az archívum a **cél**.</span><span class="sxs-lookup"><span data-stu-id="59419-126">Determines whether to check if the content of the archive exists at the **Destination**.</span></span> <span data-ttu-id="59419-127">Állítsa be ezt a tulajdonságot "Elérhető" annak érdekében, hogy a tartalom található.</span><span class="sxs-lookup"><span data-stu-id="59419-127">Set this property to "Present" to ensure the contents exist.</span></span> <span data-ttu-id="59419-128">Állítsa az értékét "Hiányzik", annak érdekében, hogy azok nem léteznek.</span><span class="sxs-lookup"><span data-stu-id="59419-128">Set it to "Absent" to ensure they do not exist.</span></span> <span data-ttu-id="59419-129">Az alapértelmezett érték: "Elérhető".</span><span class="sxs-lookup"><span data-stu-id="59419-129">The default value is "Present".</span></span>| 

## <a name="example"></a><span data-ttu-id="59419-130">Példa</span><span class="sxs-lookup"><span data-stu-id="59419-130">Example</span></span>

<span data-ttu-id="59419-131">A következő példa bemutatja, hogyan használható a **nxArchive** erőforrást, győződjön meg arról, hogy az archív fájl tartalmának neve `website.tar` létezik, és ki kell olvasni a megadott célhelyen.</span><span class="sxs-lookup"><span data-stu-id="59419-131">The following example shows how to use the **nxArchive** resource to ensure that the contents of an archive file called `website.tar` exist and are extracted at a given destination.</span></span>

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

