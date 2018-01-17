---
ms.date: 2017-10-13
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Szükségeskonfiguráció-State konfigurálása – áttekintés döntéshozók számára"
ms.openlocfilehash: ae545ead0718def44d5a17708d254b872691e1d3
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="desired-state-configuration-overview-for-engineers"></a>A mérnökök szükségeskonfiguráció-State konfigurálása – áttekintés

Ez a dokumentum célja a fejlesztői és a műveletek a csapatok tájékozódjon a PowerShell szükséges konfiguráló (DSC).
A DSC értéke magasabb szintű nézetét biztosítja, lásd: [kívánt állapot beállítása – áttekintés döntéshozók számára](decisionMaker.md)

## <a name="benefits-of-desired-state-configuration"></a>Célállapot-konfiguráció előnyei

A DSC-ből van:

- A Windows scripting összetettsége csökkentése
- Iteráció sebességének növelése

A "folyamatos üzembe helyezés" fogalmát egyre fontosabbá válik.
Folyamatos üzembe helyezés azt jelenti, hogy lehetővé teszi naponta sokszor gyakran, és eközben telepítését.
A következő központi telepítések célja nem javítsa ki a valami, hanem valami gyorsan közzétett beolvasása.
Új szolgáltatások első működésbe fejlesztési keresztül lehető legzökkenőmentesebben és megbízhatóan, lehető, idő-az-értéket az új üzleti logika csökken.

Az áthelyezés felhőre, magában foglalja a központi telepítési megoldás, amely használja az "deklaratív" sablon modell, ahol egy befejezési állapotot környezet deklarálva szöveg, és egy központi telepítési motor közzétett felé.
Ez a telepítési módszer lehetővé teszi a gyors módosítása, a méretezés, a rugalmasság hiba fenyegetés elleni mert tetszőleges időpontban a központi telepítés is egységesen megismételhető befejezési állapota nem biztosítására.
Eszközök és szolgáltatások, amely támogatja az ilyen stílusú műveletek az automatizálás létrehozását módosítások választ.

A DSC platform, amely biztosítja a deklaratív és idempotent (ismételhető) központi telepítés, konfigurációs és megfelelési.
A DSC-platform lehetővé teszi, hogy biztosítsa, hogy az Adatközpont összetevői a helyes konfiguráció, ezzel elkerülheti a hibákat, és megakadályozza, hogy a költséges telepítési hibákat.
A DSC-konfigurációk kezelésének alkalmazáskód részeként, DSC engedélyezi a folyamatos üzembe helyezés.
A DSC-konfiguráció az alkalmazást, amely biztosítja, hogy az alkalmazás telepítéséhez szükséges a Tudásbázis mindig naprakész és használatra kész részeként frissíteni kell.

## <a name="i-have-powershell-why-do-i-need-desired-state-configuration"></a>"Kell PowerShell, miért szükséges a célállapot-konfiguráció?"

A DSC-konfigurációk külön leképezés, vagy "Mi szeretnék", a végrehajtási, vagy a "hogyan szeretnék teheti meg."
Ez azt jelenti, hogy az erőforrások végrehajtási logikáját tartalmazza.
Felhasználóknak nem kell tudja, hogyan kell megvalósítani, vagy egy szolgáltatás telepítéséhez, ha az adott funkcióhoz tartozó DSC erőforrás érhető el.
Ez lehetővé teszi a felhasználó számára a központi telepítés szerkezete összpontosítanak.

Tegyük fel PowerShell-parancsfájlok kell kinéznie:
```powershell
# Create a share in Windows Server 8
New-SmbShare -Name MyShare -Path C:\Demo\Temp -FullAccess Alice -ReadAccess Bob
```
Ez a parancsfájl az egyszerű, érthető és magától értetődő.
Azonban ha kísérli meg, hogy a parancsfájl üzembe helyezésre, futtatja a több problémák.
Mi történik, ha futtatott parancsfájl kétszer szerepel egy sor?
Mi történik, ha Bálint korábban teljes hozzáféréssel a megosztáshoz való?

Kiegyensúlyozása érdekében ezeket a problémákat, a parancsfájl "tényleges" verziója közelebb valahogy fog kinézni:
```powershell
# But actually creating a share in an idempotent way would be

$shareExists = $false
$smbShare = Get-SmbShare -Name $Name -ErrorAction SilentlyContinue
if($smbShare -ne $null)
{
    Write-Verbose -Message "Share with name $Name exists"
    $shareExists = $true
}

if ($shareExists -eq $false)
{
    Write-Verbose "Creating share $Name to ensure it is Present"
    New-SmbShare @psboundparameters
}
else
{
    # Need to call either Set-SmbShare or *ShareAccess cmdlets
    if ($psboundparameters.ContainsKey("ChangeAccess"))
    {
       #...etc, etc, etc
    }
}
```

Ez a parancsfájl bőven logika és hibakezelés összetettebb.
A parancsfájl nem összetettebb, mert, amelyek már nem figyelmezteti a felhasználókat arra mit kész, de *menete*.

Az alapul szolgáló logikai kiveszik számítógépnél, és DSC teszi tetszés kész.

```powershell
# A configuration is a special kind of PowerShell function
Configuration Sample_Share
{
   Import-DscResource -Module xSmbShare
   # Nodes are the endpoint we wish to configure
   # A Configuration block can have zero or more Node blocks
   Node $NodeName
   {
      # Next, specify one or more resource blocks
      # Resources are simply PowerShell modules that
      # implement the logic of "how" to execute a task
      xSmbShare MySMBShare
      {
          Ensure      = "Present"
          Name        = "MyShare"
          Path        = "C:\Demo\Temp"
          ReadAccess  = "Alice"
          FullAccess  = "Bob"
          Description = "This is an updated description for this share"
      }
   }
}
#Run the function to compile the configuration
Sample_Share
#Pass the configuration to the nodes we defined and configure them
Start-DscConfiguration Sample_Share
```

Ez a parancsfájl megfelelően formázott és magától értetődő olvasási.
A logikai elágazások és hibakezelés is jelen a [erőforrás](resources.md) végrehajtására, de a parancsfájl készítője láthatatlan.

## <a name="separating-environment-from-structure"></a>Elválasztó struktúra környezete

DevOps közös mintát, hogy több környezet központi telepítéshez.
Előfordulhat például, a "fejlesztői" környezetében gyorsan prototípus új kódot használja.
A kód a "fejlesztői" környezetből kerül, a "test" környezetbe, ahol mások új működésének ellenőrzéséhez.
Végezetül a kód "termék", vagy az élő webhelyet éles környezetben állapotba kerül.

A DSC-konfigurációk megfeleljen a fejlesztői-teszt-termék folyamat használatával [konfigurációs adatok](configData.md).
Ez további kivonatolja a struktúra a konfigurációját a felügyelt csomópontok közötti különbség.
Például megadhatja a konfigurációkat, amelyek egy SQL server, az IIS-kiszolgáló és egy középső rétegbeli kiszolgáló szükséges.
Függetlenül attól, milyen csomópont ebben a konfigurációban a különböző adatra kap három elemek mindig jelen lesznek.
Konfigurációs adatok segítségével pont összes három elem ugyanahhoz a géphez, külön, a három elemek egy tesztkörnyezetben, a három különböző gépek fejlesztői környezet felé, és végül a termék környezet mindegyik üzemi kiszolgáló felé.
A különböző környezetekben való központi telepítéséhez hívhat meg **Start-DscConfiguration** a megfelelő konfigurációs adatokkal a cél környezet.

## <a name="see-also"></a>Lásd még:

[Konfigurációk](configurations.md)

[Konfigurációs adatok](configData.md)

[Erőforrások](resources.md)
