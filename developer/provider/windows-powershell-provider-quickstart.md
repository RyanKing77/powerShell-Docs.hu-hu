---
title: Windows PowerShell-szolgáltatóban a rövid útmutató |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3e879ba7-c334-460b-94a1-3e9b63d3d8de
caps.latest.revision: 5
ms.openlocfilehash: 949c0d63b1e5bca1bfe670362df4297c29e98fcc
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67734846"
---
# <a name="windows-powershell-provider-quickstart"></a>Windows PowerShell-szolgáltató – Gyors üzembe helyezés

Ez a témakör bemutatja, hogyan hozhat létre egy Windows PowerShell-szolgáltatóban, amely rendelkezik az új meghajtó létrehozása alapvető funkciói. Szolgáltatók kapcsolatos általános információkért lásd: [Windows PowerShell-szolgáltató áttekintése](./windows-powershell-provider-overview.md). A teljes funkcionalitásával szolgáltatók példák: [szolgáltató minták](./provider-samples.md).

## <a name="writing-a-basic-provider"></a>Egy alapszintű szolgáltató írása

Egy Windows PowerShell-szolgáltatóban a lehető legegyszerűbb funkcióit, hogy hozzon létre, és távolítsa el a meghajtók. Ebben a példában megvalósítása a [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) és [System.Management.Automation.Provider.Drivecmdletprovider.Removedrive*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) módszerek a [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) osztály. Hogyan lehet egy szolgáltató osztályban deklaráljon is megjelenik.

Ha egy szolgáltató ír, alapértelmezett meghajtó-meghajtó, amely automatikusan létrejönnek, amikor a szolgáltató érhető el is megadhat. Is meghatározhat egy metódussal hoz létre az új meghajtókat, amelyek ezt a szolgáltatót.

Ebben a témakörben megadott példák alapján vannak a [AccessDBProviderSample02](./accessdbprovidersample02.md) minta, nagyobb a minta azt jelöli, a Windows PowerShell meghajtót az Access-adatbázisok része.

### <a name="setting-up-the-project"></a>A projekt beállítása

A Visual Studióban hozzon létre egy AccessDBProviderSample nevű osztálytár projektet. A következő lépéseket a projekt konfigurálásához, hogy a Windows PowerShell elindul, és a szolgáltató tölti be a munkamenet lesz, amikor hozhat létre, és indítsa el a projektet.

##### <a name="configure-the-provider-project"></a>A szolgáltató projekt konfigurálása

1. A System.Management.Automation szerelvény hozzáadása a projekthez referenciaként.

2. Kattintson a **Project > AccessDBProviderSample tulajdonságai > Debug**. A **Spustit projekt**, kattintson a **kezdő külső program**, és keresse meg a Windows PowerShell futtatható fájl (általában c:\Windows\System32\WindowsPowerShell\v1.0\\. powershell.exe).

3. A **Start beállításai**, írja be a következőt a **parancssori argumentumok** mezőbe: `-noexit -command "[reflection.assembly]::loadFrom(AccessDBProviderSample.dll' ) | import-module"`

### <a name="declaring-the-provider-class"></a>A szolgáltató osztálya deklaráló

A szolgáltató származik a [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) osztály. A legtöbb valós funkció (elérése és elemek módosítása, navigáljon az adattár és beszerzésének és beállításának elemek tartalma) biztosító szolgáltatók célosztályából származik a [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) osztály.

Adja meg, hogy az osztály származik, mellett [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider), kell-e megadhat azt a [ System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) a példában látható módon.

```csharp
namespace Microsoft.Samples.PowerShell.Providers
{
  using System;
  using System.Data;
  using System.Data.Odbc;
  using System.IO;
  using System.Management.Automation;
  using System.Management.Automation.Provider;

  #region AccessDBProvider

  [CmdletProvider("AccessDB", ProviderCapabilities.None)]
  public class AccessDBProvider : DriveCmdletProvider
  {

}
}
```

### <a name="implementing-newdrive"></a>Végrehajtási NewDrive

A [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) módszer a Windows PowerShell motor nevezzük, amikor egy felhasználó meghívja a [Microsoft.PowerShell.Commands.NewPSDriveCommand](/dotnet/api/Microsoft.PowerShell.Commands.Newpsdrivecommand) parancsmagot, adja meg a szolgáltató neve. A PSDriveInfo paramétert a Windows PowerShell-motor, és a módszer a Windows PowerShell-motor az új meghajtó adja vissza. Ez a módszer a fent létrehozott osztályon belül kell deklarálni.

A metódus először ellenőrzi, hogy mind a meghajtó objektum létezik, és a meghajtó, amely lettek átadva a legfelső szintű, visszaadó `null` Ha valamelyiken nem. Majd használatával a belső osztály AccessDBPSDriveInfo konstruktor hozzon létre egy új meghajtót, és a egy kapcsolatot az Access-adatbázishoz a meghajtót jelöli.

```csharp
protected override PSDriveInfo NewDrive(PSDriveInfo drive)
    {
      // Check if the drive object is null.
      if (drive == null)
      {
        WriteError(new ErrorRecord(
                   new ArgumentNullException("drive"),
                   "NullDrive",
                   ErrorCategory.InvalidArgument,
                   null));

        return null;
      }

      // Check if the drive root is not null or empty
      // and if it is an existing file.
      if (String.IsNullOrEmpty(drive.Root) || (File.Exists(drive.Root) == false))
      {
        WriteError(new ErrorRecord(
                   new ArgumentException("drive.Root"),
                   "NoRoot",
                   ErrorCategory.InvalidArgument,
                   drive));

        return null;
      }

      // Create a new drive and create an ODBC connection to the new drive.
      AccessDBPSDriveInfo accessDBPSDriveInfo = new AccessDBPSDriveInfo(drive);
      OdbcConnectionStringBuilder builder = new OdbcConnectionStringBuilder();

      builder.Driver = "Microsoft Access Driver (*.mdb)";
      builder.Add("DBQ", drive.Root);

      OdbcConnection conn = new OdbcConnection(builder.ConnectionString);
      conn.Open();
      accessDBPSDriveInfo.Connection = conn;

      return accessDBPSDriveInfo;
    }
```

Az alábbiakban látható a AccessDBPSDriveInfo belső osztály, amely tartalmazza az új meghajtó létrehozásához használt konstruktort, és a meghajtó állapot adatait tartalmazza.

```csharp
internal class AccessDBPSDriveInfo : PSDriveInfo
  {
    /// <summary>
    /// A reference to the connection to the database.
    /// </summary>
    private OdbcConnection connection;

    /// <summary>
    /// Initializes a new instance of the AccessDBPSDriveInfo class.
    /// The constructor takes a single argument.
    /// </summary>
    /// <param name="driveInfo">Drive defined by this provider</param>
    public AccessDBPSDriveInfo(PSDriveInfo driveInfo)
           : base(driveInfo)
    {
    }

    /// <summary>
    /// Gets or sets the ODBC connection information.
    /// </summary>
    public OdbcConnection Connection
    {
        get { return this.connection; }
        set { this.connection = value; }
    }
  }
```

### <a name="implementing-removedrive"></a>Végrehajtási RemoveDrive

A [System.Management.Automation.Provider.Drivecmdletprovider.Removedrive*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) módszer a Windows PowerShell motor nevezzük, amikor egy felhasználó meghívja a [Microsoft.PowerShell.Commands.RemovePSDriveCommand ](/dotnet/api/Microsoft.PowerShell.Commands.removepsdrivecommand) parancsmagot. Ez a szolgáltató metódus lezárja a kapcsolatot az Access-adatbázishoz.

```csharp
protected override PSDriveInfo RemoveDrive(PSDriveInfo drive)
    {
      // Check if drive object is null.
      if (drive == null)
      {
        WriteError(new ErrorRecord(
                   new ArgumentNullException("drive"),
                   "NullDrive",
                   ErrorCategory.InvalidArgument,
                   drive));

        return null;
      }

      // Close the ODBC connection to the drive.
      AccessDBPSDriveInfo accessDBPSDriveInfo = drive as AccessDBPSDriveInfo;

      if (accessDBPSDriveInfo == null)
      {
         return null;
      }

      accessDBPSDriveInfo.Connection.Close();

      return accessDBPSDriveInfo;
    }
```