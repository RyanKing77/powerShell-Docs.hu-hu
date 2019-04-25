---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxFile erőforrás
ms.openlocfilehash: 80969ba2ea6247fcd616a301d951403a840c851d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62078027"
---
# <a name="dsc-for-linux-nxfile-resource"></a><span data-ttu-id="050c1-103">DSC, a Linux nxFile erőforrás</span><span class="sxs-lookup"><span data-stu-id="050c1-103">DSC for Linux nxFile Resource</span></span>

<span data-ttu-id="050c1-104">A **nxFile** erőforrás a PowerShell Desired State Configuration (DSC) lehetővé teszi a fájlok és könyvtárak egy Linux-csomóponton kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="050c1-104">The **nxFile** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage files and directories on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="050c1-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="050c1-105">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="050c1-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="050c1-106">Properties</span></span>

|  <span data-ttu-id="050c1-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="050c1-107">Property</span></span> |  <span data-ttu-id="050c1-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="050c1-108">Description</span></span> |
|---|---|
| <span data-ttu-id="050c1-109">DestinationPath</span><span class="sxs-lookup"><span data-stu-id="050c1-109">DestinationPath</span></span>| <span data-ttu-id="050c1-110">Itt adhatja meg a helyet, ahol szeretne biztosítani egy fájl vagy könyvtár állapota.</span><span class="sxs-lookup"><span data-stu-id="050c1-110">Specifies the location where you want to ensure the state for a file or directory.</span></span>|
| <span data-ttu-id="050c1-111">SourcePath</span><span class="sxs-lookup"><span data-stu-id="050c1-111">SourcePath</span></span>| <span data-ttu-id="050c1-112">Itt adhatja meg az elérési utat, amelyről a fájl vagy mappa erőforrás másolásához.</span><span class="sxs-lookup"><span data-stu-id="050c1-112">Specifies the path from which to copy the file or folder resource.</span></span> <span data-ttu-id="050c1-113">Az elérési út lehet egy helyi elérési utat, vagy egy `http/https/ftp` URL-CÍMÉT.</span><span class="sxs-lookup"><span data-stu-id="050c1-113">This path may be a local path, or an `http/https/ftp` URL.</span></span> <span data-ttu-id="050c1-114">Távoli `http/https/ftp` URL-címek csak olyan támogatással értékét a **típus** tulajdonság fájlt.</span><span class="sxs-lookup"><span data-stu-id="050c1-114">Remote `http/https/ftp` URLs are only supported when the value of the **Type** property is file.</span></span>|
| <span data-ttu-id="050c1-115">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="050c1-115">Ensure</span></span>| <span data-ttu-id="050c1-116">Ellenőrizze, hogy létezik-e a fájl határozza meg.</span><span class="sxs-lookup"><span data-stu-id="050c1-116">Determines whether to check if the file exists.</span></span> <span data-ttu-id="050c1-117">Ezzel a tulajdonsággal, "E" annak érdekében, hogy a fájl létezik.</span><span class="sxs-lookup"><span data-stu-id="050c1-117">Set this property to "Present" to ensure the file exists.</span></span> <span data-ttu-id="050c1-118">Állítsa a "Hiányzó" annak érdekében, hogy a fájl nem létezik.</span><span class="sxs-lookup"><span data-stu-id="050c1-118">Set it to "Absent" to ensure the file does not exist.</span></span> <span data-ttu-id="050c1-119">Az alapértelmezett érték: "E".</span><span class="sxs-lookup"><span data-stu-id="050c1-119">The default value is "Present".</span></span>|
| <span data-ttu-id="050c1-120">Típus</span><span class="sxs-lookup"><span data-stu-id="050c1-120">Type</span></span>| <span data-ttu-id="050c1-121">Megadja, hogy az erőforráshoz konfigurált egy könyvtárat vagy fájl.</span><span class="sxs-lookup"><span data-stu-id="050c1-121">Specifies whether the resource being configured is a directory or a file.</span></span> <span data-ttu-id="050c1-122">Ez azt jelzi, hogy az erőforrás egy könyvtárat a "directory" tulajdonság értéke.</span><span class="sxs-lookup"><span data-stu-id="050c1-122">Set this property to "directory" to indicate that the resource is a directory.</span></span> <span data-ttu-id="050c1-123">Állítsa be a "fájl" azt jelzi, hogy az erőforrás egy fájlt.</span><span class="sxs-lookup"><span data-stu-id="050c1-123">Set it to "file" to indicate that the resource is a file.</span></span> <span data-ttu-id="050c1-124">Az alapértelmezett érték: "fájl"</span><span class="sxs-lookup"><span data-stu-id="050c1-124">The default value is "file"</span></span>|
| <span data-ttu-id="050c1-125">Tartalom</span><span class="sxs-lookup"><span data-stu-id="050c1-125">Contents</span></span>| <span data-ttu-id="050c1-126">Itt adhatja meg, például egy adott karakterláncot egy fájl tartalmát.</span><span class="sxs-lookup"><span data-stu-id="050c1-126">Specifies the contents of a file, such as a particular string.</span></span>|
| <span data-ttu-id="050c1-127">Ellenőrzőösszeg</span><span class="sxs-lookup"><span data-stu-id="050c1-127">Checksum</span></span>| <span data-ttu-id="050c1-128">Határozza meg, amely meghatározza, hogy-e az azonos két fájlt használni kívánt típusát.</span><span class="sxs-lookup"><span data-stu-id="050c1-128">Defines the type to use when determining whether two files are the same.</span></span> <span data-ttu-id="050c1-129">Ha **ellenőrzőösszeg** nincs megadva, csak a fájl vagy könyvtár nevét használja az összehasonlítást.</span><span class="sxs-lookup"><span data-stu-id="050c1-129">If **Checksum** is not specified, only the file or directory name is used for comparison.</span></span> <span data-ttu-id="050c1-130">Értékek a következők: "ctime", "mtime", vagy a "md5".</span><span class="sxs-lookup"><span data-stu-id="050c1-130">Values are: "ctime", "mtime", or "md5".</span></span>|
| <span data-ttu-id="050c1-131">Parancs recurse kapcsolójának</span><span class="sxs-lookup"><span data-stu-id="050c1-131">Recurse</span></span>| <span data-ttu-id="050c1-132">Azt jelzi, ha alkönyvtárakat tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="050c1-132">Indicates if subdirectories are included.</span></span> <span data-ttu-id="050c1-133">Ez a tulajdonság beállítása **$true** jelzi, hogy szeretné-e alkönyvtárak fogja tartalmazni.</span><span class="sxs-lookup"><span data-stu-id="050c1-133">Set this property to **$true** to indicate that you want subdirectories to be included.</span></span> <span data-ttu-id="050c1-134">Az alapértelmezett érték **$false**.</span><span class="sxs-lookup"><span data-stu-id="050c1-134">The default is **$false**.</span></span> <span data-ttu-id="050c1-135">**Megjegyzés:** A tulajdonság csak akkor érvényes mikor a **típus** tulajdonsága könyvtár.</span><span class="sxs-lookup"><span data-stu-id="050c1-135">**Note:** This property is only valid when the **Type** property is set to directory.</span></span>|
| <span data-ttu-id="050c1-136">Force</span><span class="sxs-lookup"><span data-stu-id="050c1-136">Force</span></span>| <span data-ttu-id="050c1-137">Bizonyos fájl műveletek (például fájl felülírása vagy egy nem üres könyvtár törlése) hibát eredményez.</span><span class="sxs-lookup"><span data-stu-id="050c1-137">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="050c1-138">Használatával a **kényszerített** tulajdonság felülbírálja az ilyen hibák.</span><span class="sxs-lookup"><span data-stu-id="050c1-138">Using the **Force** property overrides such errors.</span></span> <span data-ttu-id="050c1-139">Az alapértelmezett érték **$false**.</span><span class="sxs-lookup"><span data-stu-id="050c1-139">The default value is **$false**.</span></span>|
| <span data-ttu-id="050c1-140">Hivatkozások</span><span class="sxs-lookup"><span data-stu-id="050c1-140">Links</span></span>| <span data-ttu-id="050c1-141">Itt adhatja meg a kívánt viselkedésre a szimbolikus hivatkozásokat.</span><span class="sxs-lookup"><span data-stu-id="050c1-141">Specifies the desired behavior for symbolic links.</span></span> <span data-ttu-id="050c1-142">Ezzel a tulajdonsággal "követi" hajtsa végre a szimbolikus hivatkozásokat, és reagálhat rájuk a hivatkozások cél (például.</span><span class="sxs-lookup"><span data-stu-id="050c1-142">Set this property to "follow" to follow symbolic links and act on the links target (for example.</span></span> <span data-ttu-id="050c1-143">másolja a fájlt a hivatkozás helyett).</span><span class="sxs-lookup"><span data-stu-id="050c1-143">copy the file instead of the link).</span></span> <span data-ttu-id="050c1-144">Ezzel a tulajdonsággal a "felügyelet" ahhoz, a hivatkozás (például.</span><span class="sxs-lookup"><span data-stu-id="050c1-144">Set this property to "manage" to act on the link (for example.</span></span> <span data-ttu-id="050c1-145">maga a hivatkozás másolása).</span><span class="sxs-lookup"><span data-stu-id="050c1-145">copy the link itself).</span></span> <span data-ttu-id="050c1-146">Állítsa be a "Mellőzés" gombra a szimbolikus hivatkozások figyelmen kívül ezt a tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="050c1-146">Set this property to "ignore" to ignore symbolic links.</span></span>|
| <span data-ttu-id="050c1-147">Csoport</span><span class="sxs-lookup"><span data-stu-id="050c1-147">Group</span></span>| <span data-ttu-id="050c1-148">Neve a **csoport** ahhoz a fájl vagy könyvtár.</span><span class="sxs-lookup"><span data-stu-id="050c1-148">The name of the **Group** to own the file or directory.</span></span>|
| <span data-ttu-id="050c1-149">Mód</span><span class="sxs-lookup"><span data-stu-id="050c1-149">Mode</span></span>| <span data-ttu-id="050c1-150">Adja meg a kívánt engedélyeket az erőforrás oktális vagy szimbolikus jelöléssel.</span><span class="sxs-lookup"><span data-stu-id="050c1-150">Specifies the desired permissions for the resource, in octal or symbolic notation.</span></span> <span data-ttu-id="050c1-151">(például: 777 vagy rwxrwxrwx).</span><span class="sxs-lookup"><span data-stu-id="050c1-151">(for example, 777 or rwxrwxrwx).</span></span> <span data-ttu-id="050c1-152">Szimbolikus megjelöléssel, ha nem ad meg az első karakter, ami azt jelzi, hogy könyvtárat vagy fájlt.</span><span class="sxs-lookup"><span data-stu-id="050c1-152">If using symbolic notation, do not provide the first character which indicates directory or file.</span></span>|
| <span data-ttu-id="050c1-153">DependsOn</span><span class="sxs-lookup"><span data-stu-id="050c1-153">DependsOn</span></span> | <span data-ttu-id="050c1-154">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="050c1-154">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="050c1-155">Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="050c1-155">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="additional-information"></a><span data-ttu-id="050c1-156">További információ</span><span class="sxs-lookup"><span data-stu-id="050c1-156">Additional Information</span></span>


<span data-ttu-id="050c1-157">A Linux és a Windows különböző sortörés karakterek található szöveges fájlok alapértelmezés szerint, és ez pedig váratlan helyzeteket eredményezhet, egy Linux rendszerű számítógépen az egyes fájlok konfigurálásakor __nxFile__.</span><span class="sxs-lookup"><span data-stu-id="050c1-157">Linux and Windows use different line break characters in text files by default, and this can cause unexpected results when configuring some files on a Linux computer with __nxFile__.</span></span> <span data-ttu-id="050c1-158">Kezelheti egy Linux-fájl tartalma váratlan sortörés karakterek által okozott problémák elkerülésével több módja is van:</span><span class="sxs-lookup"><span data-stu-id="050c1-158">There are multiple ways to manage the content of a Linux file while avoiding issues caused by unexpected line break characters:</span></span>

<span data-ttu-id="050c1-159">1. lépés: Másolja a fájlt egy távoli forrásból (http, https vagy ftp): hozzon létre egy Linux rendszeren a kívánt tartalma, és előkészítéséhez, web- vagy FTP-kiszolgálón elérhető konfigurálni fogja a csomópont.</span><span class="sxs-lookup"><span data-stu-id="050c1-159">Step 1: Copy the file from a remote source (http, https, or ftp): create a file on Linux with the desired contents, and stage it on a web or ftp server accessible the node(s) you will configure.</span></span> <span data-ttu-id="050c1-160">Adja meg a __SourcePath__ tulajdonságot a __nxFile__ erőforrás a web- vagy ftp URL-címet, a fájl.</span><span class="sxs-lookup"><span data-stu-id="050c1-160">Define the __SourcePath__ property in the __nxFile__ resource with the web or ftp URL to the file.</span></span>

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


<span data-ttu-id="050c1-161">2. lépés: Olvassa el a fájl tartalmát a PowerShell parancsfájl- [Get-tartalom](https://technet.microsoft.com/library/hh849787.aspx) beállítás után a __$OFS__ tulajdonság használata a Linux sortörés karakter.</span><span class="sxs-lookup"><span data-stu-id="050c1-161">Step 2: Read the file contents in the PowerShell script with [Get-Content](https://technet.microsoft.com/library/hh849787.aspx) after setting the __$OFS__ property to use the Linux line-break character.</span></span>


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


<span data-ttu-id="050c1-162">3. lépés: Cserélje le a sortöréseket Linux sortörés karakterek a Windows PowerShell függvény használható.</span><span class="sxs-lookup"><span data-stu-id="050c1-162">Step 3: Use a PowerShell function to replace Windows line breaks with Linux line-break characters.</span></span>

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

## <a name="example"></a><span data-ttu-id="050c1-163">Példa</span><span class="sxs-lookup"><span data-stu-id="050c1-163">Example</span></span>

<span data-ttu-id="050c1-164">Az alábbi példa biztosítja, hogy a könyvtár `/opt/mydir` létezik, és, hogy létezik-e a megadott tartalom nevű fájl ebben a címtárban.</span><span class="sxs-lookup"><span data-stu-id="050c1-164">The following example ensures that the directory `/opt/mydir` exists, and that a file with specified contents exists this directory.</span></span>

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