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
ms.openlocfilehash: 151b7125afe1b0d386467a0e5f89225716857ac2
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62080883"
---
# <a name="windows-powershell-provider-quickstart"></a><span data-ttu-id="00de0-102">Windows PowerShell-szolgáltató – Gyors üzembe helyezés</span><span class="sxs-lookup"><span data-stu-id="00de0-102">Windows PowerShell Provider Quickstart</span></span>

<span data-ttu-id="00de0-103">Ez a témakör bemutatja, hogyan hozhat létre egy Windows PowerShell-szolgáltatóban, amely rendelkezik az új meghajtó létrehozása alapvető funkciói.</span><span class="sxs-lookup"><span data-stu-id="00de0-103">This topic explains how to create a Windows PowerShell provider that has basic functionality of creating a new drive.</span></span> <span data-ttu-id="00de0-104">Szolgáltatók kapcsolatos általános információkért lásd: [Windows PowerShell-szolgáltató áttekintése](./windows-powershell-provider-overview.md).</span><span class="sxs-lookup"><span data-stu-id="00de0-104">For general information about providers, see [Windows PowerShell Provider Overview](./windows-powershell-provider-overview.md).</span></span> <span data-ttu-id="00de0-105">A teljes funkcionalitásával szolgáltatók példák: [szolgáltató minták](./provider-samples.md).</span><span class="sxs-lookup"><span data-stu-id="00de0-105">For examples of providers with more complete functionality, see [Provider Samples](./provider-samples.md).</span></span>

## <a name="writing-a-basic-provider"></a><span data-ttu-id="00de0-106">Egy alapszintű szolgáltató írása</span><span class="sxs-lookup"><span data-stu-id="00de0-106">Writing a basic provider</span></span>

<span data-ttu-id="00de0-107">Egy Windows PowerShell-szolgáltatóban a lehető legegyszerűbb funkcióit, hogy hozzon létre, és távolítsa el a meghajtók.</span><span class="sxs-lookup"><span data-stu-id="00de0-107">The most basic functionality of a Windows PowerShell provider is to create and remove drives.</span></span> <span data-ttu-id="00de0-108">Ebben a példában megvalósítása a [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) és [System.Management.Automation.Provider.Drivecmdletprovider.Removedrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) módszerek a [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) osztály.</span><span class="sxs-lookup"><span data-stu-id="00de0-108">In this example, we implement the [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) and [System.Management.Automation.Provider.Drivecmdletprovider.Removedrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) methods of the [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) class.</span></span> <span data-ttu-id="00de0-109">Hogyan lehet egy szolgáltató osztályban deklaráljon is megjelenik.</span><span class="sxs-lookup"><span data-stu-id="00de0-109">You will also see how to declare a provider class.</span></span>

<span data-ttu-id="00de0-110">Ha egy szolgáltató ír, alapértelmezett meghajtó-meghajtó, amely automatikusan létrejönnek, amikor a szolgáltató érhető el is megadhat.</span><span class="sxs-lookup"><span data-stu-id="00de0-110">When you write a provider, you can specify default drives-drives that are created automatically when the provider is available.</span></span> <span data-ttu-id="00de0-111">Is meghatározhat egy metódussal hoz létre az új meghajtókat, amelyek ezt a szolgáltatót.</span><span class="sxs-lookup"><span data-stu-id="00de0-111">You also define a method to create new drives that use that provider.</span></span>

<span data-ttu-id="00de0-112">Ebben a témakörben megadott példák alapján vannak a [AccessDBProviderSample02](./accessdbprovidersample02.md) minta, nagyobb a minta azt jelöli, a Windows PowerShell meghajtót az Access-adatbázisok része.</span><span class="sxs-lookup"><span data-stu-id="00de0-112">The examples provided in this topic are based on the [AccessDBProviderSample02](./accessdbprovidersample02.md) sample, which is part of a larger sample that represents an Access database as a Windows PowerShell drive.</span></span>

### <a name="setting-up-the-project"></a><span data-ttu-id="00de0-113">A projekt beállítása</span><span class="sxs-lookup"><span data-stu-id="00de0-113">Setting up the project</span></span>

<span data-ttu-id="00de0-114">A Visual Studióban hozzon létre egy AccessDBProviderSample nevű osztálytár projektet.</span><span class="sxs-lookup"><span data-stu-id="00de0-114">In Visual Studio, create a Class Library project named AccessDBProviderSample.</span></span> <span data-ttu-id="00de0-115">A következő lépéseket a projekt konfigurálásához, hogy a Windows PowerShell elindul, és a szolgáltató tölti be a munkamenet lesz, amikor hozhat létre, és indítsa el a projektet.</span><span class="sxs-lookup"><span data-stu-id="00de0-115">Complete the following steps to configure your project so that Windows PowerShell will start, and the provider will be loaded into the session, when you build and start your project.</span></span>

##### <a name="configure-the-provider-project"></a><span data-ttu-id="00de0-116">A szolgáltató projekt konfigurálása</span><span class="sxs-lookup"><span data-stu-id="00de0-116">Configure the provider project</span></span>

1. <span data-ttu-id="00de0-117">A System.Management.Automation szerelvény hozzáadása a projekthez referenciaként.</span><span class="sxs-lookup"><span data-stu-id="00de0-117">Add the System.Management.Automation assembly as a reference to your project.</span></span>

2. <span data-ttu-id="00de0-118">Kattintson a **Project > AccessDBProviderSample tulajdonságai > Debug**.</span><span class="sxs-lookup"><span data-stu-id="00de0-118">Click **Project > AccessDBProviderSample Properties > Debug**.</span></span> <span data-ttu-id="00de0-119">A **Spustit projekt**, kattintson a **kezdő külső program**, és keresse meg a Windows PowerShell futtatható fájl (általában c:\Windows\System32\WindowsPowerShell\v1.0\\. powershell.exe).</span><span class="sxs-lookup"><span data-stu-id="00de0-119">In **Start project**, click **Start external program**, and navigate to the Windows PowerShell executable (typically c:\Windows\System32\WindowsPowerShell\v1.0\\.powershell.exe).</span></span>

3. <span data-ttu-id="00de0-120">A **Start beállításai**, írja be a következőt a **parancssori argumentumok** mezőbe: `-noexit -command "[reflection.assembly]::loadFrom(AccessDBProviderSample.dll' ) | import-module"`</span><span class="sxs-lookup"><span data-stu-id="00de0-120">Under **Start Options**, enter the following into the **Command line arguments** box: `-noexit -command "[reflection.assembly]::loadFrom(AccessDBProviderSample.dll' ) | import-module"`</span></span>

### <a name="declaring-the-provider-class"></a><span data-ttu-id="00de0-121">A szolgáltató osztálya deklaráló</span><span class="sxs-lookup"><span data-stu-id="00de0-121">Declaring the provider class</span></span>

<span data-ttu-id="00de0-122">A szolgáltató származik a [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) osztály.</span><span class="sxs-lookup"><span data-stu-id="00de0-122">Our provider derives from the [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) class.</span></span> <span data-ttu-id="00de0-123">A legtöbb valós funkció (elérése és elemek módosítása, navigáljon az adattár és beszerzésének és beállításának elemek tartalma) biztosító szolgáltatók célosztályából származik a [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) osztály.</span><span class="sxs-lookup"><span data-stu-id="00de0-123">Most providers that provide real functionality (accessing and manipulating items, navigating the data store, and getting and setting content of items) derive from the [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) class.</span></span>

<span data-ttu-id="00de0-124">Adja meg, hogy az osztály származik, mellett [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider), kell-e megadhat azt a [ System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) a példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="00de0-124">In addition to specifying that the class derives from [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider), you must decorate it with the [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) as shown in the example.</span></span>

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

### <a name="implementing-newdrive"></a><span data-ttu-id="00de0-125">Végrehajtási NewDrive</span><span class="sxs-lookup"><span data-stu-id="00de0-125">Implementing NewDrive</span></span>

<span data-ttu-id="00de0-126">A [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) módszer a Windows PowerShell motor nevezzük, amikor egy felhasználó meghívja a [Microsoft.PowerShell.Commands.New-PSDrive](/dotnet/api/Microsoft.PowerShell.Commands.New-PSDrive)parancsmagot, adja meg a szolgáltató neve.</span><span class="sxs-lookup"><span data-stu-id="00de0-126">The [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) method is called by the Windows PowerShell engine when a user calls the [Microsoft.PowerShell.Commands.New-PSDrive](/dotnet/api/Microsoft.PowerShell.Commands.New-PSDrive) cmdlet specifying the name of your provider.</span></span> <span data-ttu-id="00de0-127">A PSDriveInfo paramétert a Windows PowerShell-motor, és a módszer a Windows PowerShell-motor az új meghajtó adja vissza.</span><span class="sxs-lookup"><span data-stu-id="00de0-127">The PSDriveInfo parameter is passed by the Windows PowerShell engine, and the method returns the new drive to the Windows PowerShell engine.</span></span> <span data-ttu-id="00de0-128">Ez a módszer a fent létrehozott osztályon belül kell deklarálni.</span><span class="sxs-lookup"><span data-stu-id="00de0-128">This method must be declared within the class created above.</span></span>

<span data-ttu-id="00de0-129">A metódus először ellenőrzi, hogy mind a meghajtó objektum létezik, és a meghajtó, amely lettek átadva a legfelső szintű, visszaadó `null` Ha valamelyiken nem.</span><span class="sxs-lookup"><span data-stu-id="00de0-129">The method first checks to make sure both the drive object and the drive root that were passed in exist, returning `null` if either of them do not.</span></span> <span data-ttu-id="00de0-130">Majd használatával a belső osztály AccessDBPSDriveInfo konstruktor hozzon létre egy új meghajtót, és a egy kapcsolatot az Access-adatbázishoz a meghajtót jelöli.</span><span class="sxs-lookup"><span data-stu-id="00de0-130">It then uses a constructor of the internal class AccessDBPSDriveInfo to create a new drive and a connection to the Access database the drive represents.</span></span>

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

<span data-ttu-id="00de0-131">Az alábbiakban látható a AccessDBPSDriveInfo belső osztály, amely tartalmazza az új meghajtó létrehozásához használt konstruktort, és a meghajtó állapot adatait tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="00de0-131">The following is the AccessDBPSDriveInfo internal class that includes the constructor used to create a new drive, and contains the state information for the drive.</span></span>

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

### <a name="implementing-removedrive"></a><span data-ttu-id="00de0-132">Végrehajtási RemoveDrive</span><span class="sxs-lookup"><span data-stu-id="00de0-132">Implementing RemoveDrive</span></span>

<span data-ttu-id="00de0-133">A [System.Management.Automation.Provider.Drivecmdletprovider.Removedrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) módszer a Windows PowerShell motor nevezzük, amikor egy felhasználó meghívja a [Microsoft.PowerShell.Commands.Remove-PSDrive](/dotnet/api/Microsoft.PowerShell.Commands.Remove-PSDrive) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="00de0-133">The [System.Management.Automation.Provider.Drivecmdletprovider.Removedrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) method is called by the Windows PowerShell engine when a user calls the [Microsoft.PowerShell.Commands.Remove-PSDrive](/dotnet/api/Microsoft.PowerShell.Commands.Remove-PSDrive) cmdlet.</span></span> <span data-ttu-id="00de0-134">Ez a szolgáltató metódus lezárja a kapcsolatot az Access-adatbázishoz.</span><span class="sxs-lookup"><span data-stu-id="00de0-134">The method in this provider closes the connection to the Access database.</span></span>

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