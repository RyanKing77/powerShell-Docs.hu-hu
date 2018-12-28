---
ms.date: 10/13/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A célállapot-konfiguráció áttekintése mérnökök számára
ms.openlocfilehash: 0e599c2218cd2df29dbd0529006be5e1ef17ce5f
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404456"
---
# <a name="desired-state-configuration-overview-for-engineers"></a>A célállapot-konfiguráció áttekintése mérnökök számára

Ez a dokumentum célja fejlesztői és műveleti csapatok, hogy tájékozódjon a PowerShell Desired State Configuration (DSC).
A DSC értéke magasabb szintű nézetét biztosítja, lásd: [Desired State Configuration áttekintése döntéshozók számára](decisionMaker.md)

## <a name="benefits-of-desired-state-configuration"></a>Desired State Configuration előnyei

DSC létezik:

- Parancsprogramok használata a Windows a összetettségének csökkentése
- Ismétlés sebességének növelése

"Folyamatos üzembe helyezés" fogalma egyre fontosabbá válik.
Folyamatos üzembe helyezés helyezheti üzembe az alkalmazásokat gyakran, esetleg naponta többször jelenti.
Ezeket az üzemelő példányokat célját olyan nem hibajavítási, de valami gyorsan beolvasása.
Új funkciók első keresztül fejlesztést, a művelet legzökkenőmentesebben és megbízhatóan, amennyire csak lehetséges, csökkenti a idő teremthet értéket az új üzleti logikát.

Az áthelyezés a felhő-számítástechnika azt jelenti, egy központi telepítési megoldás, amely már használja egy "deklaratív" sablon modell, ahol befejezési állapota környezet deklarálva szöveget, és egy üzembe helyezési motorban közzétett felé.
Ez a telepítési módszer lehetővé teszi, hogy gyors változások, ipari méretekben, és meghibásodási fenyegetés elleni ezzel járó rugalmasságot mivel bármikor az üzemelő példány folyamatosan megismételhető biztosításához egy befejezési állapotot.
Eszközöket és szolgáltatásokat, amelyek támogatják ezt az automatizálás operations stílusát létrehozása adott válasz ezeket a módosításokat.

DSC platform, amely biztosítja a deklaratív és idempotens (megismételhető) telepítési, konfigurációs és irányítópultja.
A DSC-platform segítségével győződjön meg arról, hogy az Adatközpont alkotóelemei rendelkezik-e a megfelelő konfigurációt, mivel ezzel elkerülheti a hibákat, és megakadályozza a költséges telepítési hibákat.
DSC-konfigurációk kezelésére az alkalmazás kódjának részeként, DSC folyamatos üzembe helyezés lehetővé teszi.
A DSC-konfiguráció az alkalmazást, amely biztosítja, hogy a ismereteket szerezhet az alkalmazás központi telepítése mindig naprakész, és készen áll a használatra részeként kell frissíteni.

## <a name="i-have-powershell-why-do-i-need-desired-state-configuration"></a>"PowerShell-lel, miért szükséges a Desired State Configuration van szükségem?"

DSC-konfigurációk külön szándékot, vagy a "mit szeretne ehhez", a végrehajtási, vagy a "hogyan szeretnék működtet."
Ez azt jelenti, hogy az erőforrások végrehajtási logikájának tartalmazza.
Útmutató megvalósítása vagy üzembe helyezése egy funkció, ha egy adott szolgáltatáshoz tartozó DSC erőforrás érhető el a felhasználók nem rendelkeznek.
Ez lehetővé teszi a felhasználó számára a központi telepítés összpontosítanak.

Tegyük fel PowerShell-parancsfájlokat kell kinéznie:
```powershell
# Create a share in Windows Server 8
New-SmbShare -Name MyShare -Path C:\Demo\Temp -FullAccess Alice -ReadAccess Bob
```
Ez a szkript akkor egyszerű, érthető és könnyen érthető megjegyzésblokkok írására.
Azonban ha a szkript üzembe helyezése éles környezetben, fog futtatni több problémákat.
Mi történik, amely kétszer egy sort a szkript futása?
Mi történik, ha Bob korábban hozzáférhettek a megosztást?

A meghiúsult lépések kompenzációjához ezeket a problémákat, a parancsfájl egy "valódi" verzióját közelebb a következőhöz hasonlóan fog kinézni:
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

Ez a szkript akkor bőven logikai és a hibakezelés összetettebb.
A parancsfájl összetettebb, mert meg van már nem figyelmezteti a szándékainak kész, de *menete*.

DSC lehetővé teszi, hogy tegyük fel, hogy mit szeretne kész, és az alapul szolgáló logikai azonnal emeli ki.

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
          ReadAccess  = "Bob"
          FullAccess  = "Alice"
          Description = "This is an updated description for this share"
      }
   }
}
#Run the function to compile the configuration
Sample_Share
#Pass the configuration to the nodes we defined and configure them
Start-DscConfiguration Sample_Share
```

Ez a szkript akkor tisztán formázott és könnyen érthető megjegyzésblokkok írására olvasni.
A logikai elérési utak és a hibakezelés is jelen a [erőforrás](../resources/resources.md) végrehajtására, de a parancsfájlt a szerzője, láthatatlan.

## <a name="separating-environment-from-structure"></a>Struktúra környezetben szétválasztása

A fejlesztési és üzemeltetési egyik központi telepítés több környezetet.
Előfordulhat például, a "fejlesztés" környezet segítségével gyorsan prototípus új kódot.
A kód a "fejlesztés" környezetből kerül egy "teszt" környezetben, ahol mások ellenőrizze-e az új funkciókat.
Végül a kód az "éles", vagy az élő webhelyet éles környezetbe kerül.

DSC-konfigurációk megfeleljen a dev-test-éles folyamat használatával [konfigurációs adatok](../configurations/configData.md).
Ez további kivonatolja a struktúra a konfiguráció a kezelt csomópontok közötti különbség.
Például megadhat egy-egy SQL server, az IIS-kiszolgáló és egy középső rétegbeli kiszolgáló szükséges konfigurációját.
Függetlenül attól, hogy milyen csomópontok a konfiguráció a különböző darabok kapja ezek három elem mindig lesz található.
Konfigurációs adatok segítségével pont felé ugyanarra a gépre a tesztkörnyezetben, három különböző gépek ki a három elem külön fejlesztési környezetre vonatkozó összes három elemet, és végül az éles környezet összes az éles kiszolgálók felé.
A különböző környezetekben való üzembe helyezéséhez hívhat **Start-DscConfiguration** -célozni kívánt környezetre a megfelelő konfigurációs adatokat.

## <a name="see-also"></a>Lásd még:

[Konfigurációk](../configurations/configurations.md)

[Konfigurációs adatok](../configurations/configData.md)

[Erőforrások](../resources/resources.md)
