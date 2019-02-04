---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxFile erőforrás
ms.openlocfilehash: 80969ba2ea6247fcd616a301d951403a840c851d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688650"
---
# <a name="dsc-for-linux-nxfile-resource"></a>DSC, a Linux nxFile erőforrás

A **nxFile** erőforrás a PowerShell Desired State Configuration (DSC) lehetővé teszi a fájlok és könyvtárak egy Linux-csomóponton kezeléséhez.

## <a name="syntax"></a>Szintaxis

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

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság |  Leírás |
|---|---|
| DestinationPath| Itt adhatja meg a helyet, ahol szeretne biztosítani egy fájl vagy könyvtár állapota.|
| SourcePath| Itt adhatja meg az elérési utat, amelyről a fájl vagy mappa erőforrás másolásához. Az elérési út lehet egy helyi elérési utat, vagy egy `http/https/ftp` URL-CÍMÉT. Távoli `http/https/ftp` URL-címek csak olyan támogatással értékét a **típus** tulajdonság fájlt.|
| Győződjön meg, hogy| Ellenőrizze, hogy létezik-e a fájl határozza meg. Ezzel a tulajdonsággal, "E" annak érdekében, hogy a fájl létezik. Állítsa a "Hiányzó" annak érdekében, hogy a fájl nem létezik. Az alapértelmezett érték: "E".|
| Típus| Megadja, hogy az erőforráshoz konfigurált egy könyvtárat vagy fájl. Ez azt jelzi, hogy az erőforrás egy könyvtárat a "directory" tulajdonság értéke. Állítsa be a "fájl" azt jelzi, hogy az erőforrás egy fájlt. Az alapértelmezett érték: "fájl"|
| Tartalom| Itt adhatja meg, például egy adott karakterláncot egy fájl tartalmát.|
| Ellenőrzőösszeg| Határozza meg, amely meghatározza, hogy-e az azonos két fájlt használni kívánt típusát. Ha **ellenőrzőösszeg** nincs megadva, csak a fájl vagy könyvtár nevét használja az összehasonlítást. Értékek a következők: "ctime", "mtime", vagy a "md5".|
| Parancs recurse kapcsolójának| Azt jelzi, ha alkönyvtárakat tartalmaz. Ez a tulajdonság beállítása **$true** jelzi, hogy szeretné-e alkönyvtárak fogja tartalmazni. Az alapértelmezett érték **$false**. **Megjegyzés:** A tulajdonság csak akkor érvényes mikor a **típus** tulajdonsága könyvtár.|
| Force| Bizonyos fájl műveletek (például fájl felülírása vagy egy nem üres könyvtár törlése) hibát eredményez. Használatával a **kényszerített** tulajdonság felülbírálja az ilyen hibák. Az alapértelmezett érték **$false**.|
| Hivatkozások| Itt adhatja meg a kívánt viselkedésre a szimbolikus hivatkozásokat. Ezzel a tulajdonsággal "követi" hajtsa végre a szimbolikus hivatkozásokat, és reagálhat rájuk a hivatkozások cél (például. másolja a fájlt a hivatkozás helyett). Ezzel a tulajdonsággal a "felügyelet" ahhoz, a hivatkozás (például. maga a hivatkozás másolása). Állítsa be a "Mellőzés" gombra a szimbolikus hivatkozások figyelmen kívül ezt a tulajdonságot.|
| Csoport| Neve a **csoport** ahhoz a fájl vagy könyvtár.|
| Mód| Adja meg a kívánt engedélyeket az erőforrás oktális vagy szimbolikus jelöléssel. (például: 777 vagy rwxrwxrwx). Szimbolikus megjelöléssel, ha nem ad meg az első karakter, ami azt jelzi, hogy könyvtárat vagy fájlt.|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="additional-information"></a>További információ


A Linux és a Windows különböző sortörés karakterek található szöveges fájlok alapértelmezés szerint, és ez pedig váratlan helyzeteket eredményezhet, egy Linux rendszerű számítógépen az egyes fájlok konfigurálásakor __nxFile__. Kezelheti egy Linux-fájl tartalma váratlan sortörés karakterek által okozott problémák elkerülésével több módja is van:

1. lépés: Másolja a fájlt egy távoli forrásból (http, https vagy ftp): hozzon létre egy Linux rendszeren a kívánt tartalma, és előkészítéséhez, web- vagy FTP-kiszolgálón elérhető konfigurálni fogja a csomópont. Adja meg a __SourcePath__ tulajdonságot a __nxFile__ erőforrás a web- vagy ftp URL-címet, a fájl.

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


2. lépés: Olvassa el a fájl tartalmát a PowerShell parancsfájl- [Get-tartalom](https://technet.microsoft.com/library/hh849787.aspx) beállítás után a __$OFS__ tulajdonság használata a Linux sortörés karakter.


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


3. lépés: Cserélje le a sortöréseket Linux sortörés karakterek a Windows PowerShell függvény használható.

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

## <a name="example"></a>Példa

Az alábbi példa biztosítja, hogy a könyvtár `/opt/mydir` létezik, és, hogy létezik-e a megadott tartalom nevű fájl ebben a címtárban.

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