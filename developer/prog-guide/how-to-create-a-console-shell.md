---
title: Hogyan hozhat létre egy konzol Shell |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Make-Shell [PowerShell Programmer's Guide]
ms.assetid: 6c24dd44-a8ec-421d-ac86-90912e1a8cc6
caps.latest.revision: 5
ms.openlocfilehash: 7166881bd1403ea8c81ec2928321f6b93e3ac58d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845058"
---
# <a name="how-to-create-a-console-shell"></a>Konzolfelület létrehozása

Windows PowerShell márka-Shell eszközt, más néven a "ügyeljen-csomag", a konzol rendszerhéj, amely nem bővíthető létrehozásához használt biztosít. Az új eszköz használatával létrehozott parancskörnyezet később egy Windows PowerShell beépülő modullal nem bővíthetők.

## <a name="syntax"></a>Szintaxis

Íme a márka-Shell a márka-fájlon belüli futtatásához használt szintaxis.

```
make-shell
  -out n.exe
  -namespace ns
  [ -lib libdirectory1[,libdirectory2,..] ]
  [ -reference ca1.dll[,ca2.dll,...] ]
  [ -formatdata fd1.format.ps1xml[,fd2.format.ps1xml,...] ]
  [ -typedata td1.type.ps1xml[,td2.type.ps1xml,...] ]
  [ -source c1.cs [,c2.cs,...] ]
  [ -authorizationmanager authorizationManagerType ]
  [ -win32icon i.ico ]
  [ -initscript p.ps1 ]
  [ -builtinscript s1.ps1[,s2.ps1,...] ]
  [ -resource resourcefile.txt ]
  [ -cscflags cscFlags ]
  [ -? | -help ]
```

## <a name="parameters"></a>Paraméterek

Íme a paramétereket a márka-Shell rövid leírását.

> [!CAUTION]
> UNC elérési útvonalat szerelvények nem támogatottak a márka-Shell által.

|Paraméter|Leírás|
|---------------|-----------------|
|-meghatározott n.exe|Kötelező megadni. A rendszerhéj előállításához neve. Az elérési út van megadva, ez a paraméter részeként.<br /><br /> Márka-shell fog ".exe" hozzáfűzése ezt az értéket, ha nincs megadva. **Figyelmeztetés:**  Hozzon létre egy kimeneti fájl neve megegyezik a hivatkozott .dll fájl. Ha megpróbálja ezt, a márka-Shell eszköz létrehoz egy .cs ugyanazzal a névvel, amely felülírja a parancsmag forráskód .cs fájlt.|
|névtér - ns|Kötelező megadni. A használandó névteret a származtatott [System.Management.Automation.Runspaces.Runspaceconfiguration](/dotnet/api/System.Management.Automation.Runspaces.RunspaceConfiguration) osztály, amely a márka kit állít elő, és lefordítja.|
|-lib libdirectory1 [, libdirectory2,..]|A könyvtárak a .NET-szerelvények, beleértve a Windows PowerShell-szerelvényeket, által meghatározott szerelvényeket keresésben a `reference` paraméter, egy másik szerelvény által közvetetten hivatkozott szerelvényeket és a .NET rendszer szerelvényeket.|
|-hivatkozást ca1.dll[,ca2.dll,...]|A szerelvények a rendszerhéj bevonni vesszővel tagolt listája. Ezekkel a szerelvényekkel tartalmaz minden parancsmag és a szolgáltató szerelvényeket, valamint erőforrás szerelvényeket, amelyek be kell tölteni. Ha ez a paraméter nincs megadva, a rendszerhéj jön létre, amely csak a fő parancsmagjainak és a Windows PowerShell által biztosított szolgáltatókat tartalmazza.<br /><br /> A szerelvények a teljes elérési útja is meg kell adni, ellenkező esetben ezek keresendő által megadott elérési út használatával a `lib` paraméter.|
|-formatdata fd1.format.ps1xml[,fd2.format.ps1xml,...]|Adatok formázása a rendszerhéj bevonni a vesszővel tagolt listája. Ha ez a paraméter nincs megadva, a rendszerhéj jön létre, amely csak a Windows PowerShell által biztosított formátumú adatokat tartalmazza.|
|-typedata td1.type.ps1xml[,td2.type.ps1xml,...]|Írja be adatokat a rendszerhéj bevonni vesszővel tagolt listája. Ha ez a paraméter nincs megadva, a rendszerhéj jön létre, amely csak a Windows PowerShell által biztosított típusú adatokat tartalmaz.|
|-adatforrás c1.cs [, c2.cs,...]|Egy fájl, amely tartalmazza a rendszerhéj létrehozásához szükséges forrás kód rendszerhéj fejlesztője által készített neve.<br /><br /> A forrásfájl is tartalmazhatja a következő forrás-kódot:<br /><br /> – Az engedélyezési manager megvalósítása, amely felülbírálja az alapértelmezett Engedélyezéskezelő. (Ez sikerült is meg kell adni egy szerelvény lefordítva.)<br />-Szerelvény tájékoztató attribútum nyilatkozatok: például AssemblyCompanyAttribute, AssemblyCopyrightAttribute, AssemblyFileVersionAttribute, AssemblyInformationalVersionAttribute, AssemblyProductAttribute, és AssemblyTrademarkAttribute.|
|-authorizationmanager authorizationManagerType|A típus, amely tartalmazza a kezelő engedélyezési végrehajtására. Ez is definiálva a forráskódban, vagy egy szerelvény lefordítva (azokat a `reference` paraméter). Ha ez a paraméter nincs megadva, az alapértelmezett biztonsági manager szolgál. Az értéknek kell lennie a teljes típusnév, többek között a névtereket.|
|-win32icon i.ico|Az .exe fájlra a parancshéj ikonjára. Ha nincs megadva, a rendszerhéj rendelkezik az ikont, amely a c# fordítóprogram (ha van ilyen) tartalmazza.|
|-initscript p.ps1|A rendszerhéj indítási profilját. A fájl megtalálható "mint-akkor"; érvényesség-ellenőrzés nélkül márka-Shell végzi el.|
|-builtinscript s1.ps1[,s2.ps1,...]|A rendszerhéj-parancsfájlok beépített listája. Ezek a szkriptek felderített előtt parancsfájl elérési útján, és azok tartalmát nem lehet módosítani, a rendszerhéj a létrehozása után.<br /><br /> A fájlok szerepelnek "mint-akkor"; érvényesség-ellenőrzés nélkül márka-Shell végzi el.|
|-erőforrás resourcefile.txt|A rendszerhéj Súgó és transzparens erőforrásait tartalmazó .txt fájlt. Az első erőforrásra ShellHelp neve, és tartalmazza a szöveg jelenik meg, ha a rendszerhéj meghívása a `help` paraméter. A második erőforrás ShellBanner neve, és a szöveg és a rendszerhéj interaktív módban való megnyitásakor megjelenő szerzői jogi információ tartalmazza.<br /><br /> Ha ez a paraméter nincs megadva, vagy nem találhatók meg ezeket az erőforrásokat, majd egy általános Súgó és transzparens szolgálnak.|
|-cscflags cscFlags|Kell adni a jelzők az C# fordító (csc.exe). Ezek továbbítja a rendszer változatlan marad. Ha ezt a paramétert tartalmaz szóközöket, akkor az idézőjelek kell körül.|
|-?<br /><br /> – Súgó|A szerzői jogi üzenet és a márka-rendszerhéj parancssori kapcsolók jeleníti meg.|
|-verbose|Részletes információit jeleníti meg a rendszerhéj létrehozása közben.|

## <a name="see-also"></a>Lásd még:

[Windows PowerShell programozói útmutató](./windows-powershell-programmer-s-guide.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)