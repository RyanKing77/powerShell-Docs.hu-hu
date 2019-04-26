---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Konfigurációs és környezeti adatok szétválasztása
ms.openlocfilehash: 305a766fec81d4ea4afce187756188b067a2048b
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62080033"
---
# <a name="separating-configuration-and-environment-data"></a><span data-ttu-id="5426f-103">Konfigurációs és környezeti adatok szétválasztása</span><span class="sxs-lookup"><span data-stu-id="5426f-103">Separating configuration and environment data</span></span>

><span data-ttu-id="5426f-104">A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="5426f-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="5426f-105">Konfigurációs adatok használatával magát a konfigurációból DSC konfigurációban használt adatokat hasznos lehet.</span><span class="sxs-lookup"><span data-stu-id="5426f-105">It can be useful to separate the data used in a DSC configuration from the configuration itself by using configuration data.</span></span>
<span data-ttu-id="5426f-106">Ezzel az eljárással egy egyetlen konfigurációs több környezethez is használhatja.</span><span class="sxs-lookup"><span data-stu-id="5426f-106">By doing this, you can use a single configuration for multiple environments.</span></span>

<span data-ttu-id="5426f-107">Például ha egy olyan alkalmazást fejleszt, is egy konfigurációs fejlesztési és éles környezetben is használja, és adja meg az adatokat az egyes környezetekhez a konfigurációs adatok használatával.</span><span class="sxs-lookup"><span data-stu-id="5426f-107">For example, if you are developing an application, you can use one configuration for both development and production environments, and use configuration data to specify data for each environment.</span></span>

## <a name="what-is-configuration-data"></a><span data-ttu-id="5426f-108">Mi az konfigurációs adatokat?</span><span class="sxs-lookup"><span data-stu-id="5426f-108">What is configuration data?</span></span>

<span data-ttu-id="5426f-109">Konfigurációs adatok, amely egy kivonattáblát meghatározott, és ha ez a konfiguráció fordítása a DSC-konfiguráció átadott adatokat.</span><span class="sxs-lookup"><span data-stu-id="5426f-109">Configuration data is data that is defined in a hashtable and passed to a DSC configuration when you compile that configuration.</span></span>

<span data-ttu-id="5426f-110">Részletes leírását a **ConfigurationData** kivonattábla, lásd: [-konfigurációs adatok](configData.md).</span><span class="sxs-lookup"><span data-stu-id="5426f-110">For a detailed description of the **ConfigurationData** hashtable, see [Using configuration data](configData.md).</span></span>

## <a name="a-simple-example"></a><span data-ttu-id="5426f-111">Egy egyszerű példa</span><span class="sxs-lookup"><span data-stu-id="5426f-111">A simple example</span></span>

<span data-ttu-id="5426f-112">Lássunk erre egy nagyon egyszerű példa, hogy ennek működését.</span><span class="sxs-lookup"><span data-stu-id="5426f-112">Let's look at a very simple example to see how this works.</span></span>
<span data-ttu-id="5426f-113">Hozunk létre, amely biztosítja, hogy egyetlen konfigurációval **IIS** megtalálható az egyes csomópontokat, és hogy **Hyper-V** -e a többi:</span><span class="sxs-lookup"><span data-stu-id="5426f-113">We'll create a single configuration that ensures that **IIS** is present on some nodes, and that **Hyper-V** is present on others:</span></span>

```powershell
Configuration MyDscConfiguration {

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        WindowsFeature IISInstall {
            Ensure = 'Present'
            Name   = 'Web-Server'
        }

    }
    Node $AllNodes.Where{$_.Role -eq "VMHost"}.NodeName
    {
        WindowsFeature HyperVInstall {
            Ensure = 'Present'
            Name   = 'Hyper-V'
        }
    }
}

$MyData =
@{
    AllNodes =
    @(
        @{
            NodeName    = 'VM-1'
            Role = 'WebServer'
        },

        @{
            NodeName    = 'VM-2'
            Role = 'VMHost'
        }
    )
}

MyDscConfiguration -ConfigurationData $MyData
```

<span data-ttu-id="5426f-114">Ez a szkript utolsó sorában lefordítja a konfigurációt, átmenő `$MyData` értékeként **ConfigurationData** paraméter.</span><span class="sxs-lookup"><span data-stu-id="5426f-114">The last line in this script compiles the configuration, passing `$MyData` as the value **ConfigurationData** parameter.</span></span>

<span data-ttu-id="5426f-115">Az eredmény az lesz, hogy két MOF-fájlt hoz létre:</span><span class="sxs-lookup"><span data-stu-id="5426f-115">The result is that two MOF files are created:</span></span>

```
    Directory: C:\DscTests\MyDscConfiguration


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/31/2017   5:09 PM           1968 VM-1.mof
-a----        3/31/2017   5:09 PM           1970 VM-2.mof
```

<span data-ttu-id="5426f-116">`$MyData` Adja meg a két másik csomópont, és saját `NodeName` és `Role`.</span><span class="sxs-lookup"><span data-stu-id="5426f-116">`$MyData` specifies two different nodes, each with its own `NodeName` and `Role`.</span></span> <span data-ttu-id="5426f-117">A konfiguráció dinamikusan létrehoz **csomópont** blokkolja a csomópontok gyűjteményei, lekéri a végrehajtásával `$MyData` (pontosabban `$AllNodes`) és szűri az adott gyűjtemény ellen a `Role` tulajdonság...</span><span class="sxs-lookup"><span data-stu-id="5426f-117">The configuration dynamically creates **Node** blocks by taking the collection of nodes it gets from `$MyData` (specifically, `$AllNodes`) and filters that collection against the `Role` property..</span></span>

## <a name="using-configuration-data-to-define-development-and-production-environments"></a><span data-ttu-id="5426f-118">Konfigurációs adatok segítségével határozza meg a fejlesztési és éles környezetekben</span><span class="sxs-lookup"><span data-stu-id="5426f-118">Using configuration data to define development and production environments</span></span>

<span data-ttu-id="5426f-119">Nézzük meg, amely egyetlen-konfigurációt használ, állítsa be a fejlesztési és éles környezetben is webhely teljes példát.</span><span class="sxs-lookup"><span data-stu-id="5426f-119">Let's look at a complete example that uses a single configuration to set up both development and production environments of a website.</span></span> <span data-ttu-id="5426f-120">A fejlesztési környezetben az IIS és az SQL Server telepítve egyetlen csomóponton.</span><span class="sxs-lookup"><span data-stu-id="5426f-120">In the development environment, both IIS and SQL Server are installed on a single nodes.</span></span> <span data-ttu-id="5426f-121">Az éles környezetben az IIS és az SQL Server telepítése a külön csomópontokon.</span><span class="sxs-lookup"><span data-stu-id="5426f-121">In the production environment, IIS and SQL Server are installed on separate nodes.</span></span> <span data-ttu-id="5426f-122">Adja meg az adatokat a két különböző környezetek használjuk .psd1 konfigurációs adatfájlt.</span><span class="sxs-lookup"><span data-stu-id="5426f-122">We'll use a configuration data .psd1 file to specify the data for the two different environments.</span></span>

### <a name="configuration-data-file"></a><span data-ttu-id="5426f-123">Konfigurációs adatfájlt</span><span class="sxs-lookup"><span data-stu-id="5426f-123">Configuration data file</span></span>

<span data-ttu-id="5426f-124">A fejlesztési és éles környezeti adatok fogunk meghatározni egy nevű fájl `DevProdEnvData.psd1` módon:</span><span class="sxs-lookup"><span data-stu-id="5426f-124">We'll define the development and production environment data in a file named `DevProdEnvData.psd1` as follows:</span></span>

```powershell
@{

    AllNodes = @(

        @{
            NodeName        = "*"
            SQLServerName   = "MySQLServer"
            SqlSource       = "C:\Software\Sql"
            DotNetSrc       = "C:\Software\sxs"
        WebSiteName     = "New website"
        },

        @{
            NodeName        = "Prod-SQL"
            Role            = "MSSQL"
        },

        @{
            NodeName        = "Prod-IIS"
            Role            = "Web"
            SiteContents    = "C:\Website\Prod\SiteContents\"
            SitePath        = "\\Prod-IIS\Website\"
        },

        @{
            NodeName         = "Dev"
            Role             = "MSSQL", "Web"
            SiteContents     = "C:\Website\Dev\SiteContents\"
            SitePath         = "\\Dev\Website\"
        }
    )
}
```

### <a name="configuration-script-file"></a><span data-ttu-id="5426f-125">Konfigurációs parancsfájl</span><span class="sxs-lookup"><span data-stu-id="5426f-125">Configuration script file</span></span>

<span data-ttu-id="5426f-126">Most a konfigurációban, amelyhez definiálva van egy `.ps1` fájlt, hogy a csomópontok meghatározott szűrése `DevProdEnvData.psd1` betöltött szerepe (`MSSQL`, `Dev`, vagy mindkettőt), és ennek megfelelően konfigurálhatja őket.</span><span class="sxs-lookup"><span data-stu-id="5426f-126">Now, in the configuration, which is defined in a `.ps1` file, we filter the nodes we defined in `DevProdEnvData.psd1` by their role (`MSSQL`, `Dev`, or both), and configure them accordingly.</span></span>
<span data-ttu-id="5426f-127">A fejlesztési környezet rendelkezik az SQL Server és az IIS egy csomóponton, míg az éles környezet őket két különböző csomópontokon.</span><span class="sxs-lookup"><span data-stu-id="5426f-127">The development environment has both the SQL Server and IIS on one node, while the production environment has them on two different nodes.</span></span>
<span data-ttu-id="5426f-128">A webhely tartalma is nem egyezik, azokat a `SiteContents` tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="5426f-128">The site contents is also different, as specified by the `SiteContents` properties.</span></span>

<span data-ttu-id="5426f-129">A konfigurációs parancsfájl végén található a konfigurációs nevezzük (lefordítani a MOF-dokumentumba), adja `DevProdEnvData.psd1` , a `$ConfigurationData` paraméter.</span><span class="sxs-lookup"><span data-stu-id="5426f-129">At the end of the configuration script, we call the configuration (compile it into a MOF document), passing `DevProdEnvData.psd1` as the `$ConfigurationData` parameter.</span></span>

><span data-ttu-id="5426f-130">**Megjegyzés:** Ez a konfiguráció megköveteli a modulok `xSqlPs` és `xWebAdministration` a célcsomópont kell telepíteni.</span><span class="sxs-lookup"><span data-stu-id="5426f-130">**Note:** This configuration requires the modules `xSqlPs` and `xWebAdministration` to be installed on the target node.</span></span>

<span data-ttu-id="5426f-131">Határozzon meg egy nevű fájl a konfiguráció `MyWebApp.ps1`:</span><span class="sxs-lookup"><span data-stu-id="5426f-131">Let's define the configuration in a file named `MyWebApp.ps1`:</span></span>

```powershell
Configuration MyWebApp
{
    Import-DscResource -Module PSDesiredStateConfiguration
    Import-DscResource -Module xSqlPs
    Import-DscResource -Module xWebAdministration

    Node $AllNodes.Where{$_.Role -contains "MSSQL"}.NodeName
   {
        # Install prerequisites
        WindowsFeature installdotNet35
        {
            Ensure      = "Present"
            Name        = "Net-Framework-Core"
            Source      = "c:\software\sxs"
        }

        # Install SQL Server
        xSqlServerInstall InstallSqlServer
        {
            InstanceName = $Node.SQLServerName
            SourcePath   = $Node.SqlSource
            Features     = "SQLEngine,SSMS"
            DependsOn    = "[WindowsFeature]installdotNet35"

        }
   }

   Node $AllNodes.Where{$_.Role -contains "Web"}.NodeName
   {
        # Install the IIS role
        WindowsFeature IIS
        {
            Ensure       = 'Present'
            Name         = 'Web-Server'
        }

        # Install the ASP .NET 4.5 role
        WindowsFeature AspNet45
        {
            Ensure       = 'Present'
            Name         = 'Web-Asp-Net45'

        }

        # Stop the default website
        xWebsite DefaultSite
        {
            Ensure       = 'Present'
            Name         = 'Default Web Site'
            State        = 'Stopped'
            PhysicalPath = 'C:\inetpub\wwwroot'
            DependsOn    = '[WindowsFeature]IIS'

        }

        # Copy the website content
        File WebContent

        {
            Ensure          = 'Present'
            SourcePath      = $Node.SiteContents
            DestinationPath = $Node.SitePath
            Recurse         = $true
            Type            = 'Directory'
            DependsOn       = '[WindowsFeature]AspNet45'

        }


        # Create the new Website

        xWebsite NewWebsite

        {

            Ensure          = 'Present'
            Name            = $Node.WebSiteName
            State           = 'Started'
            PhysicalPath    = $Node.SitePath
            DependsOn       = '[File]WebContent'
        }

    }

}

MyWebApp -ConfigurationData DevProdEnvData.psd1
```

<span data-ttu-id="5426f-132">Amikor futtatja ezt a konfigurációt, jönnek létre három MOF-fájlok (egy mindegyik nevű bejegyzést a **AllNodes** tömb):</span><span class="sxs-lookup"><span data-stu-id="5426f-132">When you run this configuration, three MOF files are created (one for each named entry in the **AllNodes** array):</span></span>

```
    Directory: C:\DscTests\MyWebApp


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/31/2017   5:47 PM           2944 Prod-SQL.mof
-a----        3/31/2017   5:47 PM           6994 Dev.mof
-a----        3/31/2017   5:47 PM           5338 Prod-IIS.mof
```

## <a name="using-non-node-data"></a><span data-ttu-id="5426f-133">Nem csomópont adatait használatával</span><span class="sxs-lookup"><span data-stu-id="5426f-133">Using non-node data</span></span>

<span data-ttu-id="5426f-134">További kulcsokat is hozzáadhat a **ConfigurationData** kivonattábla, amely nem egy csomóponthoz egyedi adatok.</span><span class="sxs-lookup"><span data-stu-id="5426f-134">You can add additional keys to the **ConfigurationData** hashtable for data that is not specific to a node.</span></span>
<span data-ttu-id="5426f-135">A következő konfiguráció biztosítja, hogy két webhely jelenlétét.</span><span class="sxs-lookup"><span data-stu-id="5426f-135">The following configuration ensures the presence of two websites.</span></span>
<span data-ttu-id="5426f-136">Minden olyan webhelyhez adatok vannak meghatározva a **AllNodes** tömb.</span><span class="sxs-lookup"><span data-stu-id="5426f-136">Data for each website are defined in the **AllNodes** array.</span></span>
<span data-ttu-id="5426f-137">A fájl `Config.xml` történik meg mindkét webhely, ezért egy kiegészítő kulcs nevű meghatározzuk `NonNodeData`.</span><span class="sxs-lookup"><span data-stu-id="5426f-137">The file `Config.xml` is used for both websites, so we define it in an additional key with the name `NonNodeData`.</span></span>
<span data-ttu-id="5426f-138">Vegye figyelembe, hogy azt szeretné, és tetszőleges nevet adhat őket azt szeretné, tetszőleges számú további kulcsok is.</span><span class="sxs-lookup"><span data-stu-id="5426f-138">Note that you can have as many additional keys as you want, and you can name them anything you want.</span></span>
<span data-ttu-id="5426f-139">`NonNodeData` egy fenntartott szó, nem csak mi azt úgy döntött, hogy a további kulcs neve.</span><span class="sxs-lookup"><span data-stu-id="5426f-139">`NonNodeData` is not a reserved word, it is just what we decided to name the additional key.</span></span>

<span data-ttu-id="5426f-140">A speciális változó keresztül elérhető további kulcsok **$ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="5426f-140">You access additional keys by using the special variable **$ConfigurationData**.</span></span>
<span data-ttu-id="5426f-141">Ebben a példában `ConfigFileContents` a vonal érhető el:</span><span class="sxs-lookup"><span data-stu-id="5426f-141">In this example, `ConfigFileContents` is accessed with the line:</span></span>
```powershell
 Contents = $ConfigurationData.NonNodeData.ConfigFileContents
 ```
 <span data-ttu-id="5426f-142">az a `File` erőforrás letiltása.</span><span class="sxs-lookup"><span data-stu-id="5426f-142">in the `File` resource block.</span></span>


```powershell
$MyData =
@{
    AllNodes =
    @(
        @{
            NodeName           = “*”
            LogPath            = “C:\Logs”
        },

        @{
            NodeName = “VM-1”
            SiteContents = “C:\Site1”
            SiteName = “Website1”
        },


        @{
            NodeName = “VM-2”;
            SiteContents = “C:\Site2”
            SiteName = “Website2”
        }
    );

    NonNodeData =
    @{
        ConfigFileContents = (Get-Content C:\Template\Config.xml)
     }
}

configuration WebsiteConfig
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    node $AllNodes.NodeName
    {
        xWebsite Site
        {
            Name         = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure       = “Present”
        }

        File ConfigFile
        {
            DestinationPath = $Node.SiteContents + “\\config.xml”
            Contents = $ConfigurationData.NonNodeData.ConfigFileContents
        }
    }
}
```


## <a name="see-also"></a><span data-ttu-id="5426f-143">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5426f-143">See Also</span></span>
- [<span data-ttu-id="5426f-144">Konfigurációs adatok használatával</span><span class="sxs-lookup"><span data-stu-id="5426f-144">Using configuration data</span></span>](configData.md)
- [<span data-ttu-id="5426f-145">A konfigurációs adatok hitelesítő adatok beállításai</span><span class="sxs-lookup"><span data-stu-id="5426f-145">Credentials Options in Configuration Data</span></span>](configDataCredentials.md)
- [<span data-ttu-id="5426f-146">DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="5426f-146">DSC Configurations</span></span>](configurations.md)
