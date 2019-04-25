---
title: Egy bináris PowerShell-modul írása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eb4e72e6-24c4-42b6-b7b9-a62585c17f26
caps.latest.revision: 15
ms.openlocfilehash: 9ddb3bc172c66314603d2be4df5192a76c92e05d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62082226"
---
# <a name="how-to-write-a-powershell-binary-module"></a>Bináris PowerShell-modul írása

Egy bináris modul bármely szerelvény (.dll), amely tartalmazza a parancsmag osztályokat is lehet. Alapértelmezés szerint a szerelvényben lévő összes parancsmag importálása a bináris modul importálása. A parancsmagok, hozzon létre egy moduljegyzék, amelynek gyökérmodult a szerelvényben importált azonban korlátozhatja. (Például a jegyzékfájl CmdletsToExport kulcsa segítségével csak a szükséges parancsmagok exportálása.) Egy bináris modul emellett további fájlokat könyvtárszerkezete és más, hogy egyetlen a parancsmag nem hasznos felügyeleti információt is tartalmazhat.

Az alábbi eljárás ismerteti, hogyan hozhat létre, és a egy bináris PowerShell-modul telepítéséhez.

#### <a name="how-to-create-and-install-a-powershell-binary-module"></a>Hogyan hozhat létre, és a egy bináris PowerShell-modul telepítése

1. Hozzon létre egy bináris PowerShell megoldást (például az írt parancsmag C#), az a funkciók kell, és győződjön meg arról, hogy megfelelően fut-e.

   A kód szempontjából a bináris modulok középpontjában egyszerűen egy parancsmag sestavení. PowerShell valójában kezeli a egy egyetlen parancsmag szerelvény betöltése és a memóriából való eltávolítása nélkül további védhetik a fejlesztő hitelesítendő modulként. A parancsmag írt kapcsolatos további információkért lásd: [írása egy Windows PowerShell-parancsmag](../cmdlet/writing-a-windows-powershell-cmdlet.md).

2. Ha szükséges, hozzon létre, hogy a megoldás többi: (további parancsmag XML-fájlok és így tovább) és a egy moduljegyzék ismertetik azokat.

   Kívül a megoldásban a parancsmag szerelvényeket leíró, egy moduljegyzék is bemutatják, hogyan exportálja és importálja a modult szeretné, milyen parancsmagok lesz közzétéve és milyen további fájlok lépnek a modul. Ahogy korábban is hangsúlyoztuk azonban, a PowerShell egy bináris parancsmag például egy modult a következővel nincsenek további erőfeszítésekre is kezelheti. Egy moduljegyzék mint ilyen, az elsősorban több fájlok ötvözéséhez egyetlen csomagban, vagy explicit módon való közzététel – egy adott szerelvény. További információkért lásd: [írásával, egy PowerShell modul Manifest](http://msdn.microsoft.com/en-us/abe4c24b-e64e-4a61-81d5-18c4fceba0b6).

   A következő kódot egy rendkívül egyszerű C# kódblokk, amely ugyanebben a fájlban modulként használható három parancsmagokat tartalmazza.

   ```csharp
   using System.Management.Automation;           // Windows PowerShell namespace.

   namespace ModuleCmdlets
   {
     [Cmdlet(VerbsDiagnostic.Test,"BinaryModuleCmdlet1")]
     public class TestBinaryModuleCmdlet1Command : Cmdlet
     {
       protected override void BeginProcessing()
       {
         WriteObject("BinaryModuleCmdlet1 exported by the ModuleCmdlets module.");
       }
     }

     [Cmdlet(VerbsDiagnostic.Test, "BinaryModuleCmdlet2")]
     public class TestBinaryModuleCmdlet2Command : Cmdlet
     {
         protected override void BeginProcessing()
         {
             WriteObject("BinaryModuleCmdlet2 exported by the ModuleCmdlets module.");
         }
     }

     [Cmdlet(VerbsDiagnostic.Test, "BinaryModuleCmdlet3")]
     public class TestBinaryModuleCmdlet3Command : Cmdlet
     {
         protected override void BeginProcessing()
         {
             WriteObject("BinaryModuleCmdlet3 exported by the ModuleCmdlets module.");
         }
     }

   }
   ```

3. A megoldás csomagot, és mentse a csomag valahol a PowerShell-modul elérési úton.

   A `PSModulePath` globális környezeti változó ismerteti a PowerShell használatával keresse meg a modul alapértelmezett elérési utakat. Például egy gyakori útvonalat, ahová a modul a rendszer lenne `%SystemRoot%\users\<user>\Documents\WindowsPowerShell\Modules\<moduleName>`. Ha nem használja az alapértelmezett elérési utak, szüksége lesz, de explicit módon a modul a hely telepítése során. Győződjön meg arról, mentéséhez, a modul egy olyan mappa létrehozásához, mivel előfordulhat, hogy a mappa több szerelvényeket és a megoldás a fájlok tárolására van szüksége.

   Vegye figyelembe, hogy technikailag nem kell a modul telepítése bárhol a `PSModulePath` – most már egyszerűen, amely PowerShell modul az alapértelmezett helyére. Azonban akkor számít célszerű megtenni, kivéve, ha a modul valahol máshol tárolására szolgáló csak jó okkal. További információkért lásd: [egy PowerShell-modul telepítése](./installing-a-powershell-module.md) és [módosítása a PowerShell modul telepítési elérési út](./modifying-the-psmodulepath-installation-path.md).

4. Importálja a modult PowerShell hívásával [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module).

   A hívó [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) a modul betölti a memóriába aktív. Ha a PowerShell 3.0 használja, és később, egyszerűen történt a modul neve a kódot is importálni fogja azt. További információkért lásd: [egy PowerShell-modul importálása](./importing-a-powershell-module.md).

## <a name="importing-snap-in-assemblies-as-modules"></a>Importálás szerelvények beépülő modulként

Parancsmagok és szolgáltatók, a beépülő modul szerelvényeket tölthetők bináris modulként. A beépülő modul betöltődjenek, a bináris modulok, amikor szolgáltatók a beépülő modul és a parancsmagok érhetők el a felhasználóhoz, de a szerelvény beépülő modul osztályt a rendszer figyelmen kívül hagyja, és a beépülő modul nincs regisztrálva. Ennek eredményeképpen a Windows PowerShell által biztosított beépülő modul parancsmagjai nem észleli a beépülő modult annak ellenére, hogy a parancsmagok és szolgáltatók érhetők el a munkamenethez.

Ezenkívül formázását vagy típusú fájlokat, a beépülő modul által hivatkozott bináris modul részeként nem lehet importálni. A fájlok importálása a formázás és típusok létre kell hoznia egy moduljegyzék. Látható, [PowerShell-modul jegyzék írása](http://msdn.microsoft.com/en-us/abe4c24b-e64e-4a61-81d5-18c4fceba0b6).

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-modul írása](./writing-a-windows-powershell-module.md)
