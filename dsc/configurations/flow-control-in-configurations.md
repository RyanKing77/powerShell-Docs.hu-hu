---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Feltételes utasításokat és ciklusok konfigurációk
ms.openlocfilehash: 0073d94d28afbb45bb635442129a6cddde4c805a
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404175"
---
# <a name="conditional-statements-and-loops-in-configurations"></a>Feltételes utasításokat és ciklusok konfigurációk

Elvégezheti a [konfigurációk](configurations.md) dinamikusabb PowerShell folyamatvezérlési kulcsszó használatával. Ez a cikk bemutatja, használatáról és a feltételes utasításokat, hurkokat, hogy a konfigurációk több dinamikus. Egyidejű feltételes és a ciklusok [paraméterek](add-parameters-to-a-configuration.md) és [konfigurációs adatok](configData.md) lehetővé teszi több rugalmasságot és irányítást a konfigurációk fordítása közben.

Egy függvény vagy parancsfájl-blokk, mint belül egy konfigurációt bármilyen PowerShell nyelv is használhatja. A kimutatások használata csak kiértékelendő, amikor a konfigurációs fájl ".mof" fordítása hívja. Az alábbi példák fogalmak bemutatásához egyszerű forgatókönyvhöz. A rendszer elágaztatását ciklusok több gyakran használják a paramétereket és a konfigurációs adatokat.

Ez az egyszerű példában a **szolgáltatás** erőforrás letiltása a fordítás során hozza létre a ".mof" fájlt, amely fenntartja a jelenlegi állapotában a szolgáltatás aktuális állapotát kérdezi le.

> [!NOTE]
> A dinamikus erőforrás-blokk használatával fogja megelőzik az Intellisense hatékonyságát. A PowerShell-elemző nem tudja megállapítani, ha a megadott értékek elfogadható mindaddig, amíg a konfiguráció fordítását.

```powershell
Configuration ServiceState
{
    # It is best practice to explicitly import any resources used in your Configurations.
    Import-DSCResource -Name Service -Module PSDesiredStateConfiguration
    Node localhost
    {
        Service Spooler
        {
            Name = "Spooler"
            State = $(Get-Service -Name 'spooler').Status
            StartType = $(Get-Service -Name 'spooler').StartType
        }
    }
}
```

Ezenkívül létrehozhat egy **szolgáltatás** letiltása az aktuális gépen, minden szolgáltatás erőforrás-használata egy `foreach` ciklus.

```powershell
Configuration ServiceState
{
    # It is best practice to explicitly import any resources used in your Configurations.
    Import-DSCResource -Name Service -Module PSDesiredStateConfiguration
    Node localhost
    {
        Foreach ($service in $(Get-Service))
        {
            Service $service.Name
            {
                Name = $service.Name
                State = $service.Status
                StartType = $service.StartType
            }
        }
    }
}
```

Csak is létrehozhat, amely kapcsolódik az internethez, egy egyszerű használatával gépek konfigurációi `if` utasítást.

```powershell
Configuration ServiceState
{
    # It is best practice to explicitly import any resources used in your Configurations.
    Import-DSCResource -Name Service -Module PSDesiredStateConfiguration

    Foreach ($computer in @('Server01', 'Server02', 'Server03'))
    {
        if (Test-Connection -ComputerName $computer)
        {
            Node $computer
            {
                Service "Spooler"
                {
                    Name = "Spooler"
                    State = "Started"
                }
            }
        }
    }
}
```

> [!NOTE]
> A dinamikus erőforrás tiltása, ha a fenti példák hivatkozás az aktuális számítógép. Ebben a példában, amely a gép készít akkor a konfiguráció az lenne, nem a cél csomópont.

<!---
Mention Get-DSCConfigurationFromSystem
-->

## <a name="summary"></a>Összefoglalás

Az összegzés belül egy konfigurációt bármilyen PowerShell nyelv is használhatja.

Ez magában foglalja többek között:

- Egyéni objektumok
- Kivonattáblák
- Karakterlánc-manipuláció
- Távoli eljáráshívás
- A WMI és CIM
- Active Directory-objektumok
- és egyebek...

Konfigurációban meghatározott PowerShell kód ki lesz értékelve a fordítás során, de a szkriptben, amely tartalmazza a konfigurációs kódot is elhelyezhető. A konfigurációs blokkon kívül kód lesz végrehajtva, amikor importálja a konfigurációt.

## <a name="see-also"></a>Lásd még:

- [A konfigurációs paraméterek hozzáadása](add-parameters-to-a-configuration.md)
- [Konfigurációs adatok elkülönítése konfigurációk](configData.md)
