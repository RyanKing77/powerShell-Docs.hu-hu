---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A Linux nxFile erőforrás DSC
ms.openlocfilehash: 41b5ebde299c47b38d7a6e7f71607332b24ca0e4
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-for-linux-nxfile-resource"></a>A Linux nxFile erőforrás DSC

A **nxFile** erőforrás a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) mechanizmust biztosít a fájlok és könyvtárak egy Linux-csomóponton kezelése.

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
| DestinationPath| Adja meg a helyet, ahol szeretne biztosítani egy fájl vagy könyvtár állapotát.|
| SourcePath| Elérési útja, amelyből a fájl vagy mappa erőforrás másolása. Előfordulhat, hogy az elérési út egy helyi elérési utat, vagy egy `http/https/ftp` URL-CÍMÉT. Távoli `http/https/ftp` URL-címei csak támogatással értékének a **típus** tulajdonság egy fájl.|
| Győződjön meg arról| Meghatározza, hogy ellenőrizze, hogy a fájl létezik-e. Ezt a tulajdonságot "Elérhető" annak érdekében, hogy a fájl létezik-e beállítva. Állítsa az értékét "Hiányzik", annak érdekében, hogy a fájl nem létezik. Az alapértelmezett érték: "Elérhető".|
| Típus| Meghatározza, hogy az erőforrás konfigurálva-e a könyvtár vagy fájl. Ez azt jelzi, hogy az erőforrás egy könyvtár "directory" tulajdonság értéke. Állítsa be a következő "fájl" azt jelzi, hogy az erőforrás egy fájlt. Az alapértelmezett érték: "fájl"|
| Tartalom| Adja meg a fájlt, például egy adott karakterláncot.|
| Ellenőrzőösszeg| Annak meghatározása, hogy két fájlok megegyeznek használandó típust határozza meg. Ha **ellenőrzőösszeg** nincs megadva, csak a fájl vagy könyvtár neve Összehasonlításképpen szolgál. Értékek: "ctime", "mtime" vagy "md5".|
| Recurse| Azt jelzi, ha-e adva alkönyvtárak. Ez a tulajdonság beállítása **$true** annak jelzésére, hogy szeretné-e alkönyvtárakat is meg lehet adni. Az alapértelmezett érték **$false**. **Megjegyzés:** Ez a tulajdonság érvénytelen, csak ha a **típus** tulajdonsága könyvtár.|
| Force| Egyes fájl műveletek (például a fájl felülírása vagy egy nem üres könyvtár törlése) hibát eredményez. Használja a **kényszerített** a tulajdonság felülírja az ilyen hibák. Az alapértelmezett érték **$false**.|
| Hivatkozások| Adja meg a kívánt viselkedés a szimbolikus csatolást. Állítsa ezt a tulajdonságot "követi" szimbolikus hivatkozásokat követve, és a hivatkozások célkiszolgáló kezelésére (például. másolja a fájlt a hivatkozás helyett). Állítsa ezt a tulajdonságot "kezelése" való működésre hivatkozásra (például. maga a kapcsolat másolása). Állítsa ezt a tulajdonságot a "Mellőzés" gombra figyelmen kívül hagyja a szimbolikus csatolást.|
| Group| Neve a **csoport** tulajdonosa a fájl vagy könyvtár.|
| Mód| Adja meg a kívánt engedélyeket az erőforrás oktális vagy szimbolikus jelöléssel. (például: 777 vagy rwxrwxrwx). Szimbolikus jelölésével, ha nem adja meg az első karakter, amely megadja, hogy a fájl vagy könyvtár.|
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például ha a **azonosító** az erőforrás konfigurációs futtatni kívánt először parancsprogramblokkja **ResourceName** és annak típusa **ResourceType**, ez a szintaxis a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="additional-information"></a>További információ


Linux és Windows használjon különböző sortörés karakterek a szöveg, fájljaiban alapértelmezés szerint, és ez pedig váratlan helyzeteket eredményezhet, néhány fájlt a rendelkező Linux számítógép konfigurálásakor __nxFile__. Több módon is kezelheti a Linux-fájl tartalma váratlan sortörés karakterek által okozott problémák elkerülésével:

1. lépés: A fájl másolása távoli forrásból (http, https vagy ftp): hozzon létre egy Linux kívánt tartalmát, és tesztelése az elérhető web- vagy FTP-kiszolgálón konfigurálja a csomópontokon. Adja meg a __SourcePath__ tulajdonságot a __nxFile__ erőforrás a web- vagy ftp URL-címet, a fájl.

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


2. lépés:, Olvassa el a PowerShell-parancsfájlt, a fájl tartalmát [Get-tartalom](https://technet.microsoft.com/library/hh849787.aspx) beállítás után a __$OFS__ tulajdonság használata a Linux sortörés karaktert.


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


3. lépés: A PowerShell funkcióval cserélje le a Windows sortörést Linux sortörés karakterek.

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

Az alábbi példa biztosítja, hogy a könyvtár `/opt/mydir` létezik, és, hogy létezik-e a megadott tartalom fájl ebben a könyvtárban.

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