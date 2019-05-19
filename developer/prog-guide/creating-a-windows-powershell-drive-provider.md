---
title: A Windows PowerShell meghajtót szolgáltató létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- drive providers [PowerShell Programmer's Guide]
- providers [PowerShell Programmer's Guide], drive provider
- drives [PowerShell Programmer's Guide]
ms.assetid: 2b446841-6616-4720-9ff8-50801d7576ed
caps.latest.revision: 6
ms.openlocfilehash: 2696d78cae7739310b7684161b597ce436dabe92
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65855201"
---
# <a name="creating-a-windows-powershell-drive-provider"></a>Windows PowerShelles meghajtószolgáltató létrehozása

Ez a témakör ismerteti, hogyan hozhat létre egy Windows PowerShell meghajtót szolgáltató, amely lehetővé teszi egy data store eléréséhez keresztül egy Windows PowerShell meghajtót. Az ilyen típusú szolgáltató is nevezik szolgáltatók a Windows PowerShell meghajtót. A Windows PowerShell-meghajtók, a szolgáltató által használt adja meg az azt jelenti, hogy csatlakozni az adattárhoz.

Az itt leírtak szerint a Windows PowerShell meghajtószolgáltató egy Microsoft Access-adatbázis hozzáférést biztosít. A szolgáltató, a Windows PowerShell meghajtót jelöl az adatbázisban (lehetőség a meghajtószolgáltató tetszőleges számú meghajtók hozzáadása), a legfelső szintű tárolókat a meghajtó képviselik a táblák az adatbázisban, és a tárolók elemeket képviseli sora a táblák.

## <a name="defining-the-windows-powershell-provider-class"></a>A Windows PowerShell-szolgáltatóban osztály meghatározása

A meghajtószolgáltató definiálnia kell egy .NET-osztályt, amely az a [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) alaposztály. Íme a meghajtó-szolgáltató az osztálydefiníció:

[!code-csharp[AccessDBProviderSample02.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample02/AccessDBProviderSample02.cs#L29-L30 "AccessDBProviderSample02.cs")]

Figyelje meg, hogy ebben a példában a [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) attribútum határozza meg a szolgáltató és a Windows PowerShell adott funkciók felhasználóbarát nevét, amely a szolgáltató elérhetővé teszi a Windows PowerShell-modul a parancs feldolgozása közben. A lehetséges értékek a szolgáltató képességei határozzák meg a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumerálása. A meghajtó-szolgáltató nem támogatja ezeket a képességeket bármelyikét.

## <a name="defining-base-functionality"></a>Alapfunkciók meghatározása

Leírtak szerint [terv a Windows PowerShell-szolgáltatóban](./designing-your-windows-powershell-provider.md), a [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) származik a [ System.Management.Automation.Provider.Cmdletprovider](/dotnet/api/System.Management.Automation.Provider.CmdletProvider) alaposztály, amely meghatározza a módszereket, inicializálása és a szolgáltató uninitializing szükséges. Munkamenet-specifikus inicializálási információk hozzáadása és a szolgáltató által használt erőforrások felszabadítása funkció megvalósítását, lásd: [alapvető Windows PowerShell-szolgáltató létrehozása](./creating-a-basic-windows-powershell-provider.md). A legtöbb szolgáltatók (beleértve a szolgáltató az itt leírtak szerint) is használják, ez a funkció Windows PowerShell által biztosított alapértelmezett megvalósítása.

## <a name="creating-drive-state-information"></a>Meghajtó állapota adatok létrehozása

Összes Windows PowerShell-szolgáltató minősülnek állapot nélküli, ami azt jelenti, hogy a meghajtószolgáltató kell létrehozni, amely a Windows PowerShell-modul által van szükség, ha meghívja a szolgáltató kapcsolatos állapotinformációkat.

A meghajtó szolgáltató állapotinformációkat tartalmaz a kapcsolat az adatbázissal, hogy a meghajtó információi részeként. A következő kódot, amely ezt az információt a módjára látható a [System.Management.Automation.PSDriveinfo](/dotnet/api/System.Management.Automation.PSDriveInfo) objektum, amely ismerteti a meghajtó:

[!code-csharp[AccessDBProviderSample02.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample02/AccessDBProviderSample02.cs#L130-L151 "AccessDBProviderSample02.cs")]

## <a name="creating-a-drive"></a>A meghajtó létrehozása

Ahhoz, hogy a meghajtó létrehozása a Windows PowerShell-modul, a meghajtó a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) metódust. Az alábbi kód megvalósítását mutatja be a [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) a meghajtószolgáltató módszer:

[!code-csharp[AccessDBProviderSample02.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample02/AccessDBProviderSample02.cs#L42-L84 "AccessDBProviderSample02.cs")]

A felülbírálási ennek a módszernek a következőket kell tennie:

- Ellenőrizze, hogy a [System.Management.Automation.PSDriveinfo.Root*](/dotnet/api/System.Management.Automation.PSDriveInfo.Root) tag létezik, és az adattár egy kapcsolat lehet tenni.

- Meghajtó létrehozása, és töltse fel a kapcsolatot tag támogatja, a `New-PSDrive` parancsmagot.

- Ellenőrizze a [System.Management.Automation.PSDriveinfo](/dotnet/api/System.Management.Automation.PSDriveInfo) objektum a javasolt meghajtó.

- Módosítsa a [System.Management.Automation.PSDriveinfo](/dotnet/api/System.Management.Automation.PSDriveInfo) objektum, amely leírja, hogy a meghajtó bármely szükséges teljesítmény és megbízhatóság információt, vagy adjon meg további adatokat a hívók használja a meghajtót.

- Hibák kezeléséhez a [System.Management.Automation.Provider.Cmdletprovider.WriteError](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteError) metódust, és ezután lépjen vissza `null`.

  Ez a módszer vagy a meghajtó információi átadott, a metódus vagy egy szolgáltatóhoz tartozó verzióját, adja vissza.

## <a name="attaching-dynamic-parameters-to-newdrive"></a>Dinamikus paraméterek NewDrive csatolása

A `New-PSDrive` parancsmag támogatja a meghajtószolgáltató szükség lehet további paramétereket. Ezek a dinamikus paraméterek csatlakoztatása a parancsmagot, a szolgáltató valósítja meg a [System.Management.Automation.Provider.Drivecmdletprovider.Newdrivedynamicparameters*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDriveDynamicParameters) metódust. Ez a módszer, amely rendelkezik a tulajdonságokat és mezőket az attribútumok hasonlít egy parancsmag osztály elemzés objektumot adja vissza vagy egy [System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum.

Ez a meghajtó-szolgáltató nem bírálja felül ezt a módszert. Az alábbi kód azonban ez a módszer alapértelmezett megvalósítását mutatja be:

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidernewdrivedynamicparameters](Msh_samplestestcmdlets#testprovidernewdrivedynamicparameters)]  -->

## <a name="removing-a-drive"></a>A meghajtó eltávolítása

Gombra kattintva zárja be az adatbázis-kapcsolat, a meghajtó a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Drivecmdletprovider.Removedrive*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) metódust. Ez a módszer bármely szolgáltatóhoz tartozó információk törlése után a meghajtó a kapcsolat bezárása.

Az alábbi kód megvalósítását mutatja be a [System.Management.Automation.Provider.Drivecmdletprovider.Removedrive*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) a meghajtószolgáltató módszer:

[!code-csharp[AccessDBProviderSample02.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample02/AccessDBProviderSample02.cs#L91-L116 "AccessDBProviderSample02.cs")]

Ha a meghajtó is távolítható el, a metódus adja vissza a keresztül a metódusnak átadott adatokat a `drive` paraméter. Ha a meghajtó nem távolítható el, a metódus kivételt írási és visszatér `null`. A szolgáltató nem bírálja felül ezt a módszert, ha ez a módszer alapértelmezett megvalósítása, az csak a kapott bemenetként a meghajtó információi adja vissza.

## <a name="initializing-default-drives"></a>Alapértelmezett inicializálása meghajtók

A meghajtó szolgáltató valósítja meg a [System.Management.Automation.Provider.Drivecmdletprovider.Initializedefaultdrives*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.InitializeDefaultDrives) metódus meghajtót csatlakoztatni. Az Active Directory-szolgáltató lehet például az alapértelmezett névhasználati környezethez, ha a számítógép egy tartomány tagja a meghajtót csatlakoztatni.

Ezzel a módszerrel kapcsolatos inicializált meghajtóinformáció gyűjteménye, vagy egy üres gyűjteményt adja vissza. Ez a metódus meghívása után a Windows PowerShell-modul hívások történik a [System.Management.Automation.Provider.Cmdletprovider.Start*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Start) metódusnak a felülbírásával inicializálhatja a szolgáltató.

Ez a meghajtó-szolgáltató nem bírálja felül a [System.Management.Automation.Provider.Drivecmdletprovider.Initializedefaultdrives*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.InitializeDefaultDrives) metódust. Azonban a következő kód bemutatja a alapértelmezett implementációja, amely egy meghajtó üres gyűjteményt adja vissza:

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testproviderinitializedefaultdrives](Msh_samplestestcmdlets#testproviderinitializedefaultdrives)]  -->

#### <a name="things-to-remember-about-implementing-initializedefaultdrives"></a>Megjegyzendő InitializeDefaultDrives megvalósításával kapcsolatos tudnivalók

Az összes meghajtó-szolgáltatók a felhasználó segítségével a fejlesztőcsapatok legfelső szintű meghajtót kell csatlakoztatni. A meghajtó gyökérkönyvtárára szolgáljanak más csatlakoztatott meghajtók gyökerek helyek előfordulhat, hogy listája. Az Active Directory-szolgáltató előfordulhat, hogy hozzon létre például egy meghajtón található a névhasználati környezet felsoroló a `namingContext` attribútumok a legfelső szintű elosztott rendszer környezet (DSE). Ez segít a felhasználóknak felderíteni az többi meghajtón csatlakoztatási pontokat.

## <a name="code-sample"></a>Kódminta

Teljes minta kódja, lásd: [AccessDbProviderSample02 kódminta](./accessdbprovidersample02-code-sample.md).

## <a name="testing-the-windows-powershell-drive-provider"></a>A Windows PowerShell meghajtót szolgáltató tesztelése

Ha a Windows PowerShell-szolgáltató regisztrálva van a Windows PowerShell-lel, tesztelheti a támogatott parancsmagok futtatásával a parancssorban, beleértve azok a parancsmagok származtatását által elérhetővé tett. Most tesztelheti a minta meghajtószolgáltató.

1. Futtassa a `Get-PSProvider` , győződjön meg arról, hogy megtalálható-e a AccessDB meghajtószolgáltató szolgáltatók listájának beolvasásához:

   **PS> `Get-PSProvider`**

   A következő eredmény jelenik meg:

   ```output
   Name                 Capabilities                  Drives
   ----                 ------------                  ------
   AccessDB             None                          {}
   Alias                ShouldProcess                 {Alias}
   Environment          ShouldProcess                 {Env}
   FileSystem           Filter, ShouldProcess         {C, Z}
   Function             ShouldProcess                 {function}
   Registry             ShouldProcess                 {HKLM, HKCU}
   ```

2. Győződjön meg arról, hogy egy adatbázis-kiszolgáló neve (DSN) létezik az adatbázis elérésével a **adatforrások** része a **felügyeleti eszközök** az operációs rendszerhez. Az a **felhasználói DSN** táblát, kattintson duplán a **MS Access-adatbázis** , és adja hozzá a meghajtó elérési útja C:\ps\northwind.mdb.

3. Hozzon létre egy új meghajtót a minta meghajtószolgáltató használatával:

   **PS > új psdrive-név mydb-c:\ps\northwind.mdb - psprovider AccessDb gyökér**

   A következő eredmény jelenik meg:

   ```output
   Name     Provider     Root                   CurrentLocation
   ----     --------     ----                   ---------------
   mydb     AccessDB     c:\ps\northwind.mdb
   ```

4. A kapcsolat ellenőrzéséhez. A kapcsolat definiálva van, amelynek a meghajtót, mert azt a Get-PDDrive parancsmaggal ellenőrizheti.

   > [!NOTE]
   > Nem lehet a felhasználó a meghajtó-szolgáltató még használni, a szolgáltatót, hogy a kapcsolati van szüksége a tároló funkciókat. További információkért lásd: [létrehozása a Windows PowerShell-tároló szolgáltató](./creating-a-windows-powershell-container-provider.md).

   **PS > .connection (get-psdrive mydb)**

   A következő eredmény jelenik meg:

   ```output
   ConnectionString  : Driver={Microsoft Access Driver (*.mdb)};DBQ=c:\ps\northwind.mdb
   ConnectionTimeout : 15
   Database          : c:\ps\northwind
   DataSource        : ACCESS
   ServerVersion     : 04.00.0000
   Driver            : odbcjt32.dll
   State             : Open
   Site              :
   Container         :
   ```

5. Távolítsa el a meghajtót, és kilépés a rendszerhéjból:

   **PS > remove-psdrive mydb**

   **PS > Kilépés**

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-szolgáltató létrehozása](./how-to-create-a-windows-powershell-provider.md)

[A Windows PowerShell-szolgáltató tervezése](./designing-your-windows-powershell-provider.md)

[Egy alapszintű Windows PowerShell-szolgáltató létrehozása](./creating-a-basic-windows-powershell-provider.md)