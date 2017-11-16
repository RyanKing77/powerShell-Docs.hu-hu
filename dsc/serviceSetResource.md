---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC ServiceSet erőforrás"
ms.openlocfilehash: 92fa4a442eb42e89195162b7831f1a96d40b84f5
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-serviceset-resource"></a>A DSC ServiceSet erőforrás

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0


A **ServiceSet** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a célcsomóponton szolgáltatások kezelésére. Az erőforrás egy [összetett erőforrás](authoringResourceComposite.md) , amely meghívja a [erőforrás szolgáltatás](serviceResource.md) minden egyes megadott szolgáltatás a `Name` tulajdonság.

Használja ezt az erőforrást, ha a számos szolgáltatását állapot konfigurálni szeretné.

## <a name="syntax"></a>Szintaxis

```
Service [string] #ResourceName
{
    Name = [string[]]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Ensure = [string] { Absent | Present }  ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
    
}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   | 
|---|---| 
| Név| Azt jelzi, hogy a szolgáltatás nevét. Vegye figyelembe, hogy egyes esetekben ez eltér a megjelenített nevek. Kaphat a szolgáltatások és az aktuális állapotát listáját a [Get-Service](https://technet.microsoft.com/en-us/library/hh849804.aspx) parancsmag.|
| StartupType| Azt jelzi, hogy a szolgáltatás indítási típusa. Ez a tulajdonság számára engedélyezett az értékek a következők: **automatikus**, **letiltott**, és **manuális**|  
| BuiltInAccount| Azt jelzi, hogy a bejelentkezési fiókot szeretné használni a szolgáltatásokat. Ez a tulajdonság számára engedélyezett az értékek a következők: **LocalService**, **LocalSystem**, és **NetworkService**.| 
| Állapot| Szeretne biztosítani a szolgáltatások állapotát jelzi: **leállítva** vagy **futtató**.| 
| Győződjön meg arról| Azt jelzi, hogy létezik-e a szolgáltatások a rendszeren. Ez a tulajdonság beállítása **távol** annak érdekében, hogy a szolgáltatások nem léteznek. Értékre állítaná **jelen** (az alapértelmezett érték) biztosítja, hogy létezik-e a cél szolgáltatások.|
| hitelesítő adatok| Azt jelzi, hogy a szolgáltatás-erőforrást fog futni a fiók hitelesítő adatait. Ez a tulajdonság és a **BuiltinAccount** tulajdonság nem használható együtt.| 
| dependsOn| Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az *ResourceName* és annak típusa *ResourceType*, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.| 



## <a name="example"></a>Példa

A következő konfigurációs elindítja a "Windows hang" és "Távoli asztali szolgáltatások" szolgáltatásokat.

```powershell
configuration ServiceSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        ServiceSet ServiceSetExample
        {
            Name        = @("TermService", "Audiosrv")
            StartupType = "Manual"
            State       = "Running"
        } 
    }
}
```

