---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A Linux nxArchive erőforrás DSC
ms.openlocfilehash: 142f0317914f1bd3a0523d706b19662f3f64c8b6
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-for-linux-nxarchive-resource"></a>A Linux nxArchive erőforrás DSC

A **nxArchive** a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) erőforrás (.tar, .zip) archív fájlok egy adott elérési úton egy Linux-csomóponton kicsomagolásához mechanizmust biztosít.

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
| SourcePath| Az archív fájl a forrás elérési útját adja meg. Ez legyen a .tar .zip, vagy a. tar.gz fájlt. |
| DestinationPath| Adja meg a helyét az archív tartalom kibontása biztosításához.|
| Ellenőrzőösszeg| Határozza meg a típust használ annak meghatározása, hogy a forrás archív frissítve lett. Értékek: "ctime", "mtime" vagy "md5". Az alapértelmezett érték: "md5".|
| Force| Egyes fájl műveletek (például a fájl felülírása vagy egy nem üres könyvtár törlése) hibát eredményez. Használja a **kényszerített** a tulajdonság felülírja az ilyen hibák. Az alapértelmezett érték **$false**.|
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például ha a **azonosító** az erőforrás konfigurációs futtatni kívánt először parancsprogramblokkja **ResourceName** és annak típusa **ResourceType**, ez a szintaxis a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.|
| Győződjön meg arról| Meghatározza, hogy ellenőrizze, hogy létezik-e a tartalom az archívum a **cél**. Állítsa be ezt a tulajdonságot "Elérhető" annak érdekében, hogy a tartalom található. Állítsa az értékét "Hiányzik", annak érdekében, hogy azok nem léteznek. Az alapértelmezett érték: "Elérhető".|

## <a name="example"></a>Példa

A következő példa bemutatja, hogyan használható a **nxArchive** erőforrást, győződjön meg arról, hogy az archív fájl tartalmának neve `website.tar` létezik, és ki kell olvasni a megadott célhelyen.

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