---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxArchive erőforrás
ms.openlocfilehash: 800954478f149e29c22d1a88304c3be9950f109a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684870"
---
# <a name="dsc-for-linux-nxarchive-resource"></a>DSC, a Linux nxArchive erőforrás

A **nxArchive** erőforrás a PowerShell Desired State Configuration (DSC), csomagolja ki az archív (.tar, .zip kiterjesztésű) fájlok egy adott elérési úton található egy Linux-csomóponton mechanizmust biztosít.

## <a name="syntax"></a>Szintaxis

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

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság |  Leírás |
|---|---|
| SourcePath| Forrás elérési utat határozza meg az archív fájl. Ez lehet egy .tar .zip, vagy a. tar.gz fájlt. |
| DestinationPath| Itt adhatja meg a helyet, ahol szeretne biztosítani, ki kell olvasni az archívum tartalmát.|
| Ellenőrzőösszeg| Határozza meg, amely meghatározza, hogy a forrás-archívumot frissítve lett-e használni kívánt típusát. Értékek a következők: "ctime", "mtime", vagy a "md5". Az alapértelmezett érték: "md5".|
| Force| Bizonyos fájl műveletek (például fájl felülírása vagy egy nem üres könyvtár törlése) hibát eredményez. Használatával a **kényszerített** tulajdonság felülbírálja az ilyen hibák. Az alapértelmezett érték **$false**.|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.|
| Győződjön meg, hogy| Határozza meg, ellenőrizze, hogy az archívum tartalmát a **cél**. Ezzel a tulajdonsággal, "E" annak érdekében, hogy a tartalom létezik. Állítsa a "Hiányzó" annak érdekében, még nem léteznek. Az alapértelmezett érték: "E".|

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan használható a **nxArchive** erőforrást, győződjön meg arról, hogy archív fájl tartalmának neve `website.tar` létezik, és a egy adott célhelyen ki kell olvasni.

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