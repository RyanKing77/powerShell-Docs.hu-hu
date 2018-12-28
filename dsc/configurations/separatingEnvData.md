---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Konfigurációs és környezeti adatok szétválasztása
ms.openlocfilehash: 24a92e5e4f15959498b57a1488a688d5548f3585
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404189"
---
# <a name="separating-configuration-and-environment-data"></a>Konfigurációs és környezeti adatok szétválasztása

>Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

Konfigurációs adatok használatával magát a konfigurációból DSC konfigurációban használt adatokat hasznos lehet.
Ezzel az eljárással egy egyetlen konfigurációs több környezethez is használhatja.

Például ha egy olyan alkalmazást fejleszt, is egy konfigurációs fejlesztési és éles környezetben is használja, és adja meg az adatokat az egyes környezetekhez a konfigurációs adatok használatával.

## <a name="what-is-configuration-data"></a>Mi az konfigurációs adatokat?

Konfigurációs adatok, amely egy kivonattáblát meghatározott, és ha ez a konfiguráció fordítása a DSC-konfiguráció átadott adatokat.

Részletes leírását a **ConfigurationData** kivonattábla, lásd: [-konfigurációs adatok](configData.md).

## <a name="a-simple-example"></a>Egy egyszerű példa

Lássunk erre egy nagyon egyszerű példa, hogy ennek működését.
Hozunk létre, amely biztosítja, hogy egyetlen konfigurációval **IIS** megtalálható az egyes csomópontokat, és hogy **Hyper-V** -e a többi:

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

Ez a szkript utolsó sorában lefordítja a konfigurációt, átmenő `$MyData` értékeként **ConfigurationData** paraméter.

Az eredmény az lesz, hogy két MOF-fájlt hoz létre:

```
    Directory: C:\DscTests\MyDscConfiguration


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/31/2017   5:09 PM           1968 VM-1.mof
-a----        3/31/2017   5:09 PM           1970 VM-2.mof
```

`$MyData` Adja meg a két másik csomópont, és saját `NodeName` és `Role`. A konfiguráció dinamikusan létrehoz **csomópont** blokkolja a csomópontok gyűjteményei, lekéri a végrehajtásával `$MyData` (pontosabban `$AllNodes`) és szűri az adott gyűjtemény ellen a `Role` tulajdonság...

## <a name="using-configuration-data-to-define-development-and-production-environments"></a>Konfigurációs adatok segítségével határozza meg a fejlesztési és éles környezetekben

Nézzük meg, amely egyetlen-konfigurációt használ, állítsa be a fejlesztési és éles környezetben is webhely teljes példát. A fejlesztési környezetben az IIS és az SQL Server telepítve egyetlen csomóponton. Az éles környezetben az IIS és az SQL Server telepítése a külön csomópontokon. Adja meg az adatokat a két különböző környezetek használjuk .psd1 konfigurációs adatfájlt.

 ### <a name="configuration-data-file"></a>Konfigurációs adatfájlt

A fejlesztési és éles környezeti adatok fogunk meghatározni egy nevű fájl `DevProdEnvData.psd1` módon:

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

### <a name="configuration-script-file"></a>Konfigurációs parancsfájl

Most a konfigurációban, amelyhez definiálva van egy `.ps1` fájlt, hogy a csomópontok meghatározott szűrése `DevProdEnvData.psd1` betöltött szerepe (`MSSQL`, `Dev`, vagy mindkettőt), és ennek megfelelően konfigurálhatja őket.
A fejlesztési környezet rendelkezik az SQL Server és az IIS egy csomóponton, míg az éles környezet őket két különböző csomópontokon.
A webhely tartalma is nem egyezik, azokat a `SiteContents` tulajdonságait.

A konfigurációs parancsfájl végén található a konfigurációs nevezzük (lefordítani a MOF-dokumentumba), adja `DevProdEnvData.psd1` , a `$ConfigurationData` paraméter.

>**Megjegyzés:** Ez a konfiguráció megköveteli a modulok `xSqlPs` és `xWebAdministration` a célcsomópont kell telepíteni.

Határozzon meg egy nevű fájl a konfiguráció `MyWebApp.ps1`:

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

Amikor futtatja ezt a konfigurációt, jönnek létre három MOF-fájlok (egy mindegyik nevű bejegyzést a **AllNodes** tömb):

```
    Directory: C:\DscTests\MyWebApp


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/31/2017   5:47 PM           2944 Prod-SQL.mof
-a----        3/31/2017   5:47 PM           6994 Dev.mof
-a----        3/31/2017   5:47 PM           5338 Prod-IIS.mof
```

## <a name="using-non-node-data"></a>Nem csomópont adatait használatával

További kulcsokat is hozzáadhat a **ConfigurationData** kivonattábla, amely nem egy csomóponthoz egyedi adatok.
A következő konfiguráció biztosítja, hogy két webhely jelenlétét.
Minden olyan webhelyhez adatok vannak meghatározva a **AllNodes** tömb.
A fájl `Config.xml` történik meg mindkét webhely, ezért egy kiegészítő kulcs nevű meghatározzuk `NonNodeData`.
Vegye figyelembe, hogy azt szeretné, és tetszőleges nevet adhat őket azt szeretné, tetszőleges számú további kulcsok is.
`NonNodeData` egy fenntartott szó, nem csak mi azt úgy döntött, hogy a további kulcs neve.

A speciális változó keresztül elérhető további kulcsok **$ConfigurationData**.
Ebben a példában `ConfigFileContents` a vonal érhető el:
```powershell
 Contents = $ConfigurationData.NonNodeData.ConfigFileContents
 ```
 az a `File` erőforrás letiltása.


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


## <a name="see-also"></a>Lásd még:
- [Konfigurációs adatok használatával](configData.md)
- [A konfigurációs adatok hitelesítő adatok beállításai](configDataCredentials.md)
- [DSC-konfigurációk](configurations.md)
