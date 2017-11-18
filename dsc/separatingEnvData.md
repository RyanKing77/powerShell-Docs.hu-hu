---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Konfigurációs és környezeti adatok elkülönítése"
ms.openlocfilehash: 861a4cecc28b2d93b2cfa2743d47ee0e5025e1f4
ms.sourcegitcommit: 60c6f9d8cf316e6d5b285854e6e5641ac7648f3f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/17/2017
---
# <a name="separating-configuration-and-environment-data"></a>Konfigurációs és környezeti adatok elkülönítése

>Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A konfigurációból, magát a DSC-konfiguráció a konfigurációs adatok használt adatokat külön hasznos lehet.
Ennek hatására egyetlen konfigurációja több környezetekben is használhatja.

Például ha alkalmazást fejleszt, után egy konfigurációt használja a fejlesztési és éles környezetben is, is minden környezet adatainak megadása a konfigurációs adatok használatával.

## <a name="what-is-configuration-data"></a>Mi az a konfigurációs adatokat?

Konfigurációs adatok definiálva egy a, és ha ez a konfiguráció fordítása a DSC-konfiguráció átadott adatokat.

Részletes leírása a **ConfigurationData** hashtable, lásd: [konfigurációs adatok](configData.md).

## <a name="a-simple-example"></a>Egy egyszerű példa

Egy nagyon egyszerű példa megtekintéséhez, ennek működéséről vizsgáljuk meg. Hozzon létre, amely biztosítja, hogy egyetlen konfigurációja **IIS** -e egyes csomópontok, és hogy a **Hyper-V** -e a többi: 

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

Ez a parancsfájl utolsó sorában lefordítja a konfigurációt, hogy `$MyData` értékeként **ConfigurationData** paraméter.

Az eredménye, hogy két MOF-fájlok jönnek létre:

```
    Directory: C:\DscTests\MyDscConfiguration


Mode                LastWriteTime         Length Name                                                                                                                    
----                -------------         ------ ----                                                                                                                    
-a----        3/31/2017   5:09 PM           1968 VM-1.mof                                                                                                                
-a----        3/31/2017   5:09 PM           1970 VM-2.mof  
```
 
`$MyData`Adja meg a két másik csomópont, saját `NodeName` és `Role`. A konfigurációs dinamikusan létrehoz **csomópont** blokkok azt lekérése csomópontok gyűjteménye megtételével `$MyData` (pontosabban `$AllNodes`) és elleni gyűjteménynek szűrése a `Role` tulajdonság...

## <a name="using-configuration-data-to-define-development-and-production-environments"></a>Konfigurációs adatok használatával megadhatók a fejlesztési és éles környezetben

Vizsgáljuk meg egy teljes példa, amely egyetlen konfigurációja használja fejlesztési és éles környezetben is webhely beállításához. A fejlesztési környezetet az IIS és az SQL Server egyetlen csomópontján telepítve. Az éles környezetben az IIS és az SQL Server telepítve vannak az önálló csomópontra. Adja meg az adatokat a két különböző környezetek használjuk .psd1 konfigurációs adatfájlt.

 ### <a name="configuration-data-file"></a>Konfigurációs adatok fájl

A fejlesztési és éles környezeti adatok fogunk meghatározni a egy fájl namd `DevProdEnvData.psd1` az alábbiak szerint:

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

Most, a konfigurációban, amelyhez definiálva van egy `.ps1` fájl, azt a csomópontok a meghatározott szűrése `DevProdEnvData.psd1` szerepe (`MSSQL`, `Dev`, vagy mindkettőt), és ennek megfelelően konfigurálja. A fejlesztési környezet rendelkezik az SQL Server és az IIS egy csomóponton, míg az éles környezetben őket két különböző csomópontokon. A webhely teljes tartalmát is nem egyezik, leírtak szerint a `SiteContents` tulajdonságok.

A konfigurációs parancsfájl végén a konfigurációs nevezzük (lefordítani a MOF-dokumentumba), adja `DevProdEnvData.psd1` , a `$ConfigurationData` paraméter.

>**Megjegyzés:** ebben a konfigurációban kell a modulok `xSqlPs` és `xWebAdministration` célcsomóponton kell telepíteni.

Is határozza meg a konfigurációs nevű fájlba `MyWebApp.ps1`:

```powershell
Configuration MyWebApp
{
    Import-DscResource -Module PSDesiredStateConfiguration
    Import-DscResource -Module xSqlPs
    Import-DscResource -Module xWebAdministration

    Node $AllNodes.Where{$_.Role -contains "MSSQL"}.Nodename
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

Ez a konfiguráció futtatásakor három MOF-fájlok jönnek létre (egy mindegyik nevű bejegyzést a **AllNodes** tömb):

```
    Directory: C:\DscTests\MyWebApp


Mode                LastWriteTime         Length Name                                                                                                                    
----                -------------         ------ ----                                                                                                                    
-a----        3/31/2017   5:47 PM           2944 Prod-SQL.mof                                                                                                            
-a----        3/31/2017   5:47 PM           6994 Dev.mof                                                                                                                 
-a----        3/31/2017   5:47 PM           5338 Prod-IIS.mof
```

## <a name="using-non-node-data"></a>Nem-csomópont adatok használata

További kulcsokat is hozzáadhat a **ConfigurationData** kivonattábla, amely nem egy csomópont vonatkozó adatok.
A következő konfigurációs két webhely jelenléte biztosítja.
Minden webhelyre vonatkozóan adatok definiálják a **AllNodes** tömb.
A fájl `Config.xml` mindkét webhely szolgál, ezért azt meg nevű kulcsot `NonNodeData`.
Ne feledje, hogy akkor is, mint, akkor a fájl nevét bármilyen tetszőleges számú további kulcsok.
`NonNodeData`egy fenntartott szó, nincs csak mi döntöttünk a további kulcs neve.

A speciális változó használatával éri el további kulcsok **$ConfigurationData**.
Ebben a példában `ConfigFileContents` a sor segítségével érhető el:
```powershell
 Contents = $ConfigurationData.NonNodeData.ConfigFileContents
 ```
 az a `File` erőforrás blokkot.


```powershell
$MyData = 
@{
    AllNodes = 
    @(
        @{
            NodeName           = “*”
            LogPath            = “C:\Logs”
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
            Name         = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure       = “Present”
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
- [Konfigurációs adatok használata](configData.md)
- [Konfigurációs adatokat a hitelesítő adatok beállításai](configDataCredentials.md)
- [A DSC-konfigurációk](configurations.md)

