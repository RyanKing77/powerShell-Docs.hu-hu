---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A Linux nxFile erőforrás DSC"
ms.openlocfilehash: e4916414e4de29ab15d9c82c492671ebc16d5412
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-for-linux-nxfile-resource"></a><span data-ttu-id="081bf-103">A Linux nxFile erőforrás DSC</span><span class="sxs-lookup"><span data-stu-id="081bf-103">DSC for Linux nxFile Resource</span></span>

<span data-ttu-id="081bf-104">A **nxFile** erőforrás a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) mechanizmust biztosít a fájlok és könyvtárak egy Linux-csomóponton kezelése.</span><span class="sxs-lookup"><span data-stu-id="081bf-104">The **nxFile** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to to manage files and directories on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="081bf-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="081bf-105">Syntax</span></span>

```
nxFile <string> #ResourceName
{
    DestinationPath = <string>
    [ SourcePath = <string> ]
    [ Ensure = <string> { Absent | Present }  ]
    [ Type = <string> { directory | file | link } ]
    [ Contents = <string> ]
    [ Checksum = <string> { ctime | mtime | md5 }  ]
    [ Recurse = <bool> ]
    [ Force = <bool> ]
    [ Links = <string> { follow | manage } ]
    [ Group = <string> ]
    [ Mode = <string> ]
    [ Owner = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="081bf-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="081bf-106">Properties</span></span>

|  <span data-ttu-id="081bf-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="081bf-107">Property</span></span> |  <span data-ttu-id="081bf-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="081bf-108">Description</span></span> | 
|---|---|
| <span data-ttu-id="081bf-109">DestinationPath</span><span class="sxs-lookup"><span data-stu-id="081bf-109">DestinationPath</span></span>| <span data-ttu-id="081bf-110">Adja meg a helyet, ahol szeretne biztosítani egy fájl vagy könyvtár állapotát.</span><span class="sxs-lookup"><span data-stu-id="081bf-110">Specifies the location where you want to ensure the state for a file or directory.</span></span>| 
| <span data-ttu-id="081bf-111">SourcePath</span><span class="sxs-lookup"><span data-stu-id="081bf-111">SourcePath</span></span>| <span data-ttu-id="081bf-112">Elérési útja, amelyből a fájl vagy mappa erőforrás másolása.</span><span class="sxs-lookup"><span data-stu-id="081bf-112">Specifies the path from which to copy the file or folder resource.</span></span> <span data-ttu-id="081bf-113">Előfordulhat, hogy az elérési út egy helyi elérési utat, vagy egy `http/https/ftp` URL-CÍMÉT.</span><span class="sxs-lookup"><span data-stu-id="081bf-113">This path may be a local path, or an `http/https/ftp` URL.</span></span> <span data-ttu-id="081bf-114">Távoli `http/https/ftp` URL-címei csak támogatással értékének a **típus** tulajdonság egy fájl.</span><span class="sxs-lookup"><span data-stu-id="081bf-114">Remote `http/https/ftp` URLs are only supported when the value of the **Type** property is file.</span></span>| 
| <span data-ttu-id="081bf-115">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="081bf-115">Ensure</span></span>| <span data-ttu-id="081bf-116">Meghatározza, hogy ellenőrizze, hogy a fájl létezik-e.</span><span class="sxs-lookup"><span data-stu-id="081bf-116">Determines whether to check if the file exists.</span></span> <span data-ttu-id="081bf-117">Ezt a tulajdonságot "Elérhető" annak érdekében, hogy a fájl létezik-e beállítva.</span><span class="sxs-lookup"><span data-stu-id="081bf-117">Set this property to "Present" to ensure the file exists.</span></span> <span data-ttu-id="081bf-118">Állítsa az értékét "Hiányzik", annak érdekében, hogy a fájl nem létezik.</span><span class="sxs-lookup"><span data-stu-id="081bf-118">Set it to "Absent" to ensure the file does not exist.</span></span> <span data-ttu-id="081bf-119">Az alapértelmezett érték: "Elérhető".</span><span class="sxs-lookup"><span data-stu-id="081bf-119">The default value is "Present".</span></span>| 
| <span data-ttu-id="081bf-120">Típus</span><span class="sxs-lookup"><span data-stu-id="081bf-120">Type</span></span>| <span data-ttu-id="081bf-121">Meghatározza, hogy az erőforrás konfigurálva-e a könyvtár vagy fájl.</span><span class="sxs-lookup"><span data-stu-id="081bf-121">Specifies whether the resource being configured is a directory or a file.</span></span> <span data-ttu-id="081bf-122">Ez azt jelzi, hogy az erőforrás egy könyvtár "directory" tulajdonság értéke.</span><span class="sxs-lookup"><span data-stu-id="081bf-122">Set this property to "directory" to indicate that the resource is a directory.</span></span> <span data-ttu-id="081bf-123">Állítsa be a következő "fájl" azt jelzi, hogy az erőforrás egy fájlt.</span><span class="sxs-lookup"><span data-stu-id="081bf-123">Set it to "file" to indicate that the resource is a file.</span></span> <span data-ttu-id="081bf-124">Az alapértelmezett érték: "fájl"</span><span class="sxs-lookup"><span data-stu-id="081bf-124">The default value is "file"</span></span>| 
| <span data-ttu-id="081bf-125">Tartalom</span><span class="sxs-lookup"><span data-stu-id="081bf-125">Contents</span></span>| <span data-ttu-id="081bf-126">Adja meg a fájlt, például egy adott karakterláncot.</span><span class="sxs-lookup"><span data-stu-id="081bf-126">Specifies the contents of a file, such as a particular string.</span></span>| 
| <span data-ttu-id="081bf-127">Ellenőrzőösszeg</span><span class="sxs-lookup"><span data-stu-id="081bf-127">Checksum</span></span>| <span data-ttu-id="081bf-128">Annak meghatározása, hogy két fájlok megegyeznek használandó típust határozza meg.</span><span class="sxs-lookup"><span data-stu-id="081bf-128">Defines the type to use when determining whether two files are the same.</span></span> <span data-ttu-id="081bf-129">Ha **ellenőrzőösszeg** nincs megadva, csak a fájl vagy könyvtár neve Összehasonlításképpen szolgál.</span><span class="sxs-lookup"><span data-stu-id="081bf-129">If **Checksum** is not specified, only the file or directory name is used for comparison.</span></span> <span data-ttu-id="081bf-130">Értékek: "ctime", "mtime" vagy "md5".</span><span class="sxs-lookup"><span data-stu-id="081bf-130">Values are: "ctime", "mtime", or "md5".</span></span>| 
| <span data-ttu-id="081bf-131">Recurse</span><span class="sxs-lookup"><span data-stu-id="081bf-131">Recurse</span></span>| <span data-ttu-id="081bf-132">Azt jelzi, ha-e adva alkönyvtárak.</span><span class="sxs-lookup"><span data-stu-id="081bf-132">Indicates if subdirectories are included.</span></span> <span data-ttu-id="081bf-133">Ez a tulajdonság beállítása **$true** annak jelzésére, hogy szeretné-e alkönyvtárakat is meg lehet adni.</span><span class="sxs-lookup"><span data-stu-id="081bf-133">Set this property to **$true** to indicate that you want subdirectories to be included.</span></span> <span data-ttu-id="081bf-134">Az alapértelmezett érték **$false**.</span><span class="sxs-lookup"><span data-stu-id="081bf-134">The default is **$false**.</span></span> <span data-ttu-id="081bf-135">**Megjegyzés:** Ez a tulajdonság érvénytelen, csak ha a **típus** tulajdonsága könyvtár.</span><span class="sxs-lookup"><span data-stu-id="081bf-135">**Note:** This property is only valid when the **Type** property is set to directory.</span></span>| 
| <span data-ttu-id="081bf-136">Force</span><span class="sxs-lookup"><span data-stu-id="081bf-136">Force</span></span>| <span data-ttu-id="081bf-137">Egyes fájl műveletek (például a fájl felülírása vagy egy nem üres könyvtár törlése) hibát eredményez.</span><span class="sxs-lookup"><span data-stu-id="081bf-137">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="081bf-138">Használja a **kényszerített** a tulajdonság felülírja az ilyen hibák.</span><span class="sxs-lookup"><span data-stu-id="081bf-138">Using the **Force** property overrides such errors.</span></span> <span data-ttu-id="081bf-139">Az alapértelmezett érték **$false**.</span><span class="sxs-lookup"><span data-stu-id="081bf-139">The default value is **$false**.</span></span>| 
| <span data-ttu-id="081bf-140">Hivatkozások</span><span class="sxs-lookup"><span data-stu-id="081bf-140">Links</span></span>| <span data-ttu-id="081bf-141">Adja meg a kívánt viselkedés a szimbolikus csatolást.</span><span class="sxs-lookup"><span data-stu-id="081bf-141">Specifies the desired behavior for symbolic links.</span></span> <span data-ttu-id="081bf-142">Állítsa ezt a tulajdonságot "követi" szimbolikus hivatkozásokat követve, és a hivatkozások célkiszolgáló kezelésére (például.</span><span class="sxs-lookup"><span data-stu-id="081bf-142">Set this property to "follow" to follow symbolic links and act on the links target (for example.</span></span> <span data-ttu-id="081bf-143">másolja a fájlt a hivatkozás helyett).</span><span class="sxs-lookup"><span data-stu-id="081bf-143">copy the file instead of the link).</span></span> <span data-ttu-id="081bf-144">Állítsa ezt a tulajdonságot "kezelése" való működésre hivatkozásra (például.</span><span class="sxs-lookup"><span data-stu-id="081bf-144">Set this property to "manage" to act on the link (for example.</span></span> <span data-ttu-id="081bf-145">maga a kapcsolat másolása).</span><span class="sxs-lookup"><span data-stu-id="081bf-145">copy the link itself).</span></span> <span data-ttu-id="081bf-146">Állítsa ezt a tulajdonságot a "Mellőzés" gombra figyelmen kívül hagyja a szimbolikus csatolást.</span><span class="sxs-lookup"><span data-stu-id="081bf-146">Set this property to "ignore" to ignore symbolic links.</span></span>| 
| <span data-ttu-id="081bf-147">Group</span><span class="sxs-lookup"><span data-stu-id="081bf-147">Group</span></span>| <span data-ttu-id="081bf-148">Neve a **csoport** tulajdonosa a fájl vagy könyvtár.</span><span class="sxs-lookup"><span data-stu-id="081bf-148">The name of the **Group** to own the file or directory.</span></span>| 
| <span data-ttu-id="081bf-149">Mód</span><span class="sxs-lookup"><span data-stu-id="081bf-149">Mode</span></span>| <span data-ttu-id="081bf-150">Adja meg a kívánt engedélyeket az erőforrás oktális vagy szimbolikus jelöléssel.</span><span class="sxs-lookup"><span data-stu-id="081bf-150">Specifies the desired permissions for the resource, in octal or symbolic notation.</span></span> <span data-ttu-id="081bf-151">(például: 777 vagy rwxrwxrwx).</span><span class="sxs-lookup"><span data-stu-id="081bf-151">(for example, 777 or rwxrwxrwx).</span></span> <span data-ttu-id="081bf-152">Szimbolikus jelölésével, ha nem adja meg az első karakter, amely megadja, hogy a fájl vagy könyvtár.</span><span class="sxs-lookup"><span data-stu-id="081bf-152">If using symbolic notation, do not provide the first character which indicates directory or file.</span></span>| 
| <span data-ttu-id="081bf-153">dependsOn</span><span class="sxs-lookup"><span data-stu-id="081bf-153">DependsOn</span></span> | <span data-ttu-id="081bf-154">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="081bf-154">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="081bf-155">Például ha a **azonosító** az erőforrás konfigurációs futtatni kívánt először parancsprogramblokkja **ResourceName** és annak típusa **ResourceType**, ez a szintaxis a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="081bf-155">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 

## <a name="additional-information"></a><span data-ttu-id="081bf-156">További információ</span><span class="sxs-lookup"><span data-stu-id="081bf-156">Additional Information</span></span>


<span data-ttu-id="081bf-157">Linux és Windows használjon különböző sortörés karakterek a szöveg, fájljaiban alapértelmezés szerint, és ez pedig váratlan helyzeteket eredményezhet, néhány fájlt a rendelkező Linux számítógép konfigurálásakor __nxFile__.</span><span class="sxs-lookup"><span data-stu-id="081bf-157">Linux and Windows use different line break characters in text files by default, and this can cause unexpected results when configuring some files on a Linux computer with __nxFile__.</span></span> <span data-ttu-id="081bf-158">Több módon is kezelheti a Linux-fájl tartalma váratlan sortörés karakterek által okozott problémák elkerülésével:</span><span class="sxs-lookup"><span data-stu-id="081bf-158">There are multiple ways to manage the content of a Linux file while avoiding issues caused by unexpected line break characters:</span></span>

<span data-ttu-id="081bf-159">1. lépés: A fájl másolása távoli forrásból (http, https vagy ftp): hozzon létre egy Linux kívánt tartalmát, és tesztelése az elérhető web- vagy FTP-kiszolgálón konfigurálja a csomópontokon.</span><span class="sxs-lookup"><span data-stu-id="081bf-159">Step 1: Copy the file from a remote source (http, https, or ftp): create a file on Linux with the desired contents, and stage it on a web or ftp server accessible the node(s) you will configure.</span></span> <span data-ttu-id="081bf-160">Adja meg a __SourcePath__ tulajdonságot a __nxFile__ erőforrás a web- vagy ftp URL-címet, a fájl.</span><span class="sxs-lookup"><span data-stu-id="081bf-160">Define the __SourcePath__ property in the __nxFile__ resource with the web or ftp URL to the file.</span></span>

```
Import-DSCResource -Module nx
Node $Node
{
nxFile resolvConf
{
    SourcePath = "http://10.185.85.11/conf/resolv.conf"
    DestinationPath = "/etc/resolv.conf"
    Mode = "644"        
    Type = "file"
    
}
        
}
```


<span data-ttu-id="081bf-161">2. lépés:, Olvassa el a PowerShell-parancsfájlt, a fájl tartalmát [Get-tartalom](https://technet.microsoft.com/en-us/library/hh849787.aspx) beállítás után a __$OFS__ tulajdonság használata a Linux sortörés karaktert.</span><span class="sxs-lookup"><span data-stu-id="081bf-161">Step 2: Read the file contents in the PowerShell script with [Get-Content](https://technet.microsoft.com/en-us/library/hh849787.aspx) after setting the __$OFS__ property to use the Linux line-break character.</span></span>


```
Import-DSCResource -Module nx
Node $Node
{
$OFS = "`n"
$Contents = Get-Content C:\temp\resolv.conf

nxFile resolvConf
{
    DestinationPath = "/etc/resolv.conf"
    Mode = "644"        
    Type = "file"
    Contents = "$Contents"
}

}
```


<span data-ttu-id="081bf-162">3. lépés: A PowerShell funkcióval cserélje le a Windows sortörést Linux sortörés karakterek.</span><span class="sxs-lookup"><span data-stu-id="081bf-162">Step 3: Use a PowerShell function to replace Windows line breaks with Linux line-break characters.</span></span>

```
Function LinuxString($inputStr){
    $outputStr = $inputStr.Replace("`r`n","`n")
    $ouputStr += "`n"
    Return $outputStr
}

Import-DSCResource -Module nx
Node $Node
{

$Contents = @'
search contoso.com
domain contoso.com
nameserver 10.185.85.11
'@

$Contents = LinuxString $Contents

nxFile resolvConf
{
    DestinationPath = "/etc/resolv.conf"
    Mode = "644"        
    Type = "file"
    Contents = $Contents
    
}
}
```

## <a name="example"></a><span data-ttu-id="081bf-163">Példa</span><span class="sxs-lookup"><span data-stu-id="081bf-163">Example</span></span>

<span data-ttu-id="081bf-164">Az alábbi példa biztosítja, hogy a könyvtár `/opt/mydir` létezik, és, hogy létezik-e a megadott tartalom fájl ebben a könyvtárban.</span><span class="sxs-lookup"><span data-stu-id="081bf-164">The following example ensures that the directory `/opt/mydir` exists, and that a file with specified contents exists this directory.</span></span>

```
Import-DSCResource -Module nx 

Node $node {
nxFile DirectoryExample
{
   Ensure = "Present"
   DestinationPath = "/opt/mydir"
   Type = "Directory"
}

nxFile FileExample
{
    Ensure = "Present"
    Destinationpath = "/opt/mydir/myfile"
    Contents=@"
#!/bin/bash`necho "hello world"`n
"@ 
    Mode = “755”
    DependsOn = "[nxFile]DirectoryExample"
} 
}
```

