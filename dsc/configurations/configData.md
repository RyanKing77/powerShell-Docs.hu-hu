---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Konfigurációs adatok használatával
ms.openlocfilehash: f2d25b9ced805fb4c91378ebfe840104eb6ce52a
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62080220"
---
# <a name="using-configuration-data-in-dsc"></a><span data-ttu-id="aa7c0-103">A DSC használata a konfigurációs adatok</span><span class="sxs-lookup"><span data-stu-id="aa7c0-103">Using configuration data in DSC</span></span>

> <span data-ttu-id="aa7c0-104">A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="aa7c0-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="aa7c0-105">A beépített DSC használatával **ConfigurationData** paraméterrel határozhatja meg belül a konfigurációs adatokat.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-105">By using the built-in DSC **ConfigurationData** parameter, you can define data that can be used within a configuration.</span></span>
<span data-ttu-id="aa7c0-106">Ez lehetővé teszi, hogy hozzon létre egy egyetlen konfigurációs több csomópont, vagy különböző környezetekben használható.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-106">This allows you to create a single configuration that can be used for multiple nodes or for different environments.</span></span>
<span data-ttu-id="aa7c0-107">Például ha egy olyan alkalmazást fejleszt, is egy konfigurációs fejlesztési és éles környezetben is használja, és adja meg az adatokat az egyes környezetekhez a konfigurációs adatok használatával.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-107">For example, if you are developing an application, you can use one configuration for both development and production environments, and use configuration data to specify data for each environment.</span></span>

<span data-ttu-id="aa7c0-108">Ez a témakör ismerteti a szerkezete a **ConfigurationData** kivonattábla.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-108">This topic describes the structure of the **ConfigurationData** hashtable.</span></span>
<span data-ttu-id="aa7c0-109">Konfigurációs adatok használatát bemutató példákért lásd [konfigurációs és környezeti adatok szétválasztása](separatingEnvData.md).</span><span class="sxs-lookup"><span data-stu-id="aa7c0-109">For examples of how to use configuration data, see [Separating configuration and environment data](separatingEnvData.md).</span></span>

## <a name="the-configurationdata-common-parameter"></a><span data-ttu-id="aa7c0-110">A gyakori ConfigurationData-paraméter</span><span class="sxs-lookup"><span data-stu-id="aa7c0-110">The ConfigurationData common parameter</span></span>

<span data-ttu-id="aa7c0-111">A DSC-konfiguráció paramétert egy közös, **ConfigurationData**, adjon meg mikor lefordítja a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-111">A DSC configuration takes a common parameter, **ConfigurationData**, that you specify when you compile the configuration.</span></span>
<span data-ttu-id="aa7c0-112">További információ a konfiguráció fordítása: [DSC-konfigurációk](configurations.md).</span><span class="sxs-lookup"><span data-stu-id="aa7c0-112">For information about compiling configurations, see [DSC configurations](configurations.md).</span></span>

<span data-ttu-id="aa7c0-113">A **ConfigurationData** paraméter nevű legalább egy kulccsal kell rendelkeznie a szórótábla **AllNodes**.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-113">The **ConfigurationData** parameter is a hashtable that must have at least one key named **AllNodes**.</span></span>
<span data-ttu-id="aa7c0-114">Egy vagy több kulcsot is rendelkezhet.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-114">It can also have one or more other keys.</span></span>

> [!NOTE]
> <span data-ttu-id="aa7c0-115">Ebben a témakörben szereplő példák egy további kulcs használata (a megnevezett eltérő **AllNodes** kulcs) nevű `NonNodeData`, de tetszőleges számú további kulcsokat, és adja nekik bármilyen kívánt.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-115">The examples in this topic use a single additional key (other than the named **AllNodes** key) named `NonNodeData`, but you can include any number of additional keys, and name them whatever you want.</span></span>

```powershell
$MyData =
@{
    AllNodes = @()
    NonNodeData = ""
}
```

<span data-ttu-id="aa7c0-116">Értékét a **AllNodes** kulcs egy tömb.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-116">The value of the **AllNodes** key is an array.</span></span> <span data-ttu-id="aa7c0-117">A tömb egyes elemei is, hogy az legalább egy kulcsot egy kivonattáblát **csomópontnév**:</span><span class="sxs-lookup"><span data-stu-id="aa7c0-117">Each element of this array is also a hash table that must have at least one key named **NodeName**:</span></span>

```powershell
$MyData =
@{
    AllNodes =
    @(
        @{
            NodeName = "VM-1"
        },


        @{
            NodeName = "VM-2"
        },


        @{
            NodeName = "VM-3"
        }
    );

    NonNodeData = ""
}
```

<span data-ttu-id="aa7c0-118">Más kulcsok minden egyes kivonattábla is hozzáadhat:</span><span class="sxs-lookup"><span data-stu-id="aa7c0-118">You can add other keys to each hash table as well:</span></span>

```powershell
$MyData =
@{
    AllNodes =
    @(
        @{
            NodeName = "VM-1"
            Role     = "WebServer"
        },


        @{
            NodeName = "VM-2"
            Role     = "SQLServer"
        },


        @{
            NodeName = "VM-3"
            Role     = "WebServer"
        }
    );

    NonNodeData = ""
}
```

<span data-ttu-id="aa7c0-119">Vlastnost összes csomópontjára érvényesek, tagja hozhat létre a **AllNodes** tömb, amely rendelkezik egy **csomópontnév** , `*`.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-119">To apply a property to all nodes, you can create a member of the **AllNodes** array that has a **NodeName** of `*`.</span></span>
<span data-ttu-id="aa7c0-120">Például, hogy minden csomópont egy `LogPath` tulajdonságot használja, ezt megteheti:</span><span class="sxs-lookup"><span data-stu-id="aa7c0-120">For example, to give every node a `LogPath` property, you could do this:</span></span>

```powershell
$MyData =
@{
    AllNodes =
    @(
        @{
            NodeName     = "*"
            LogPath      = "C:\Logs"
        },


        @{
            NodeName     = "VM-1"
            Role         = "WebServer"
            SiteContents = "C:\Site1"
            SiteName     = "Website1"
        },


        @{
            NodeName     = "VM-2"
            Role         = "SQLServer"
        },


        @{
            NodeName     = "VM-3"
            Role         = "WebServer"
            SiteContents = "C:\Site2"
            SiteName     = "Website3"
        }
    );
}
```

<span data-ttu-id="aa7c0-121">Ez megegyezik a hozzáad egy tulajdonságot nevű `LogPath` értékkel `"C:\Logs"` minden más blokkok (`VM-1`, `VM-2`, és `VM-3`).</span><span class="sxs-lookup"><span data-stu-id="aa7c0-121">This is the equivalent of adding a property with a name of `LogPath` with a value of `"C:\Logs"` to each of the other blocks (`VM-1`, `VM-2`, and `VM-3`).</span></span>

## <a name="defining-the-configurationdata-hashtable"></a><span data-ttu-id="aa7c0-122">A ConfigurationData kivonattábla meghatározása</span><span class="sxs-lookup"><span data-stu-id="aa7c0-122">Defining the ConfigurationData hashtable</span></span>

<span data-ttu-id="aa7c0-123">Definiálhat **ConfigurationData** vagy változóként belül (ahogy az előző példákban) egy konfigurációs parancsfájl fájlt vagy egy különálló `.psd1` fájlt.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-123">You can define **ConfigurationData** either as a variable within the same script file as a configuration (as in our previous examples) or in a separate `.psd1` file.</span></span>
<span data-ttu-id="aa7c0-124">Meghatározásához **ConfigurationData** a egy `.psd1` hozzon létre egy fájlt, amely csak a kivonattábla kulcsa, amely a konfigurációs adatokat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-124">To define **ConfigurationData** in a `.psd1` file, create a file that contains only the hashtable that represents the configuration data.</span></span>

<span data-ttu-id="aa7c0-125">Például létrehozhat egy fájlt `MyData.psd1` a következő tartalommal:</span><span class="sxs-lookup"><span data-stu-id="aa7c0-125">For example, you could create a file named `MyData.psd1` with the following contents:</span></span>

```powershell
@{
    AllNodes =
    @(
        @{
            NodeName    = 'VM-1'
            FeatureName = 'Web-Server'
        },

        @{
            NodeName    = 'VM-2'
            FeatureName = 'Hyper-V'
        }
    )
}
```

## <a name="compiling-a-configuration-with-configuration-data"></a><span data-ttu-id="aa7c0-126">A konfigurációs adatok-konfiguráció fordítása</span><span class="sxs-lookup"><span data-stu-id="aa7c0-126">Compiling a configuration with configuration data</span></span>

<span data-ttu-id="aa7c0-127">Amely meghatározta a konfigurációs adatok konfiguráció fordítása, át kell adnia a konfigurációs adatok értékeként a **ConfigurationData** paraméter.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-127">To compile a configuration for which you have defined configuration data, you pass the configuration data as the value of the **ConfigurationData** parameter.</span></span>

<span data-ttu-id="aa7c0-128">Ezzel létrehoz egy MOF-fájl minden bejegyzés esetében a **AllNodes** tömb.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-128">This will create a MOF file for each entry in the **AllNodes** array.</span></span>
<span data-ttu-id="aa7c0-129">Az egyes MOF-fájl neve lesz a `NodeName` a megfelelő tömb tétel tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-129">Each MOF file will be named with the `NodeName` property of the corresponding array entry.</span></span>

<span data-ttu-id="aa7c0-130">Például, mint a konfigurációs adatok megadása a `MyData.psd1` fájlban a fenti fordításáról hozna létre a mindkét `VM-1.mof` és `VM-2.mof` fájlokat.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-130">For example, if you define configuration data as in the `MyData.psd1` file above, compiling a configuration would create both `VM-1.mof` and `VM-2.mof` files.</span></span>

### <a name="compiling-a-configuration-with-configuration-data-using-a-variable"></a><span data-ttu-id="aa7c0-131">A konfigurációs adatok változóval fordításáról</span><span class="sxs-lookup"><span data-stu-id="aa7c0-131">Compiling a configuration with configuration data using a variable</span></span>

<span data-ttu-id="aa7c0-132">Konfigurációs adatok azonos változóként definiált használandó `.ps1` fájlt, a konfigurációt, át kell adnia a változó nevét értékeként a **ConfigurationData** paramétert, ha a konfiguráció fordítása:</span><span class="sxs-lookup"><span data-stu-id="aa7c0-132">To use configuration data that is defined as a variable in the same `.ps1` file as the configuration, you pass the variable name as the value of the **ConfigurationData** parameter when compiling the configuration:</span></span>

```powershell
MyDscConfiguration -ConfigurationData $MyData
```

### <a name="compiling-a-configuration-with-configuration-data-using-a-data-file"></a><span data-ttu-id="aa7c0-133">A konfigurációs adatok adatfájlt fordításáról</span><span class="sxs-lookup"><span data-stu-id="aa7c0-133">Compiling a configuration with configuration data using a data file</span></span>

<span data-ttu-id="aa7c0-134">Egy .psd1 fájlban meghatározott konfigurációs adatokat használja, át kell adnia az elérési útját és nevét, hogy a fájl értékeként a **ConfigurationData** paramétert, ha a konfiguráció fordítása:</span><span class="sxs-lookup"><span data-stu-id="aa7c0-134">To use configuration data that is defined in a .psd1 file, you pass the path and name of that file as the value of the **ConfigurationData** parameter when compiling the configuration:</span></span>

```powershell
MyDscConfiguration -ConfigurationData .\MyData.psd1
```

## <a name="using-configurationdata-variables-in-a-configuration"></a><span data-ttu-id="aa7c0-135">Egy konfigurációs ConfigurationData változók használata</span><span class="sxs-lookup"><span data-stu-id="aa7c0-135">Using ConfigurationData variables in a configuration</span></span>

<span data-ttu-id="aa7c0-136">DSC biztosít a következő különleges változók konfigurációs parancsfájl használható:</span><span class="sxs-lookup"><span data-stu-id="aa7c0-136">DSC provides the following special variables that can be used in a configuration script:</span></span>

- <span data-ttu-id="aa7c0-137">**$AllNodes** hivatkozik a teljes gyűjteményt a meghatározott csomópontok **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-137">**$AllNodes** refers to the entire collection of nodes defined in **ConfigurationData**.</span></span> <span data-ttu-id="aa7c0-138">Szűrheti a **AllNodes** gyűjtemény használatával **. WHERE()** és **. ForEach()**.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-138">You can filter the **AllNodes** collection by using **.Where()** and **.ForEach()**.</span></span>
- <span data-ttu-id="aa7c0-139">**ConfigurationData** hivatkozik a teljes kivonattáblában, amikor fordításáról átadott paraméterként.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-139">**ConfigurationData** refers to the entire hash table that is passed as the parameter when compiling a configuration.</span></span>
- <span data-ttu-id="aa7c0-140">**MyTypeName** tartalmazza a [konfigurációs](configurations.md) használt változó neve.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-140">**MyTypeName** contains the [configuration](configurations.md) name the variable is used in.</span></span> <span data-ttu-id="aa7c0-141">Például a konfigurációban `MyDscConfiguration`, a `$MyTypeName` fog rendelkezni a egy értéke `MyDscConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-141">For example, in the configuration `MyDscConfiguration`, the `$MyTypeName` will have a value of `MyDscConfiguration`.</span></span>
- <span data-ttu-id="aa7c0-142">**Csomópont** hivatkozik egy adott bejegyzést a **AllNodes** gyűjtemény után az szűrve van **. WHERE()** vagy **. ForEach()**.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-142">**Node** refers to a particular entry in the **AllNodes** collection after it is filtered by using **.Where()** or **.ForEach()**.</span></span>
  - <span data-ttu-id="aa7c0-143">Tudjon meg többet ezekről az eljárásokról a [about_arrays](/powershell/reference/3.0/Microsoft.PowerShell.Core/About/about_Arrays.md)</span><span class="sxs-lookup"><span data-stu-id="aa7c0-143">You can read more about these methods in [about_arrays](/powershell/reference/3.0/Microsoft.PowerShell.Core/About/about_Arrays.md)</span></span>

## <a name="using-non-node-data"></a><span data-ttu-id="aa7c0-144">Nem csomópont adatait használatával</span><span class="sxs-lookup"><span data-stu-id="aa7c0-144">Using non-node data</span></span>

<span data-ttu-id="aa7c0-145">Ahogy megtudtuk, a korábbi példákban a **ConfigurationData** kivonattábla rendelkezhet egy vagy több kulcsot mellett a szükséges **AllNodes** kulcsot.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-145">As we've seen in previous examples, the **ConfigurationData** hashtable can have one or more keys in addition to the required **AllNodes** key.</span></span>
<span data-ttu-id="aa7c0-146">Ebben a témakörben a példákban azt egyetlen további csomópont használt, és azt nevű `NonNodeData`.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-146">In the examples in this topic, we have used only a single additional node, and named it `NonNodeData`.</span></span>
<span data-ttu-id="aa7c0-147">Azonban tetszőleges számú további kulcsok definiálása, és adja nekik bármit.</span><span class="sxs-lookup"><span data-stu-id="aa7c0-147">However, you can define any number of additional keys, and name them anything you want.</span></span>

<span data-ttu-id="aa7c0-148">Nem csomópont adatait használatának példájáért lásd [konfigurációs és környezeti adatok szétválasztása](separatingEnvData.md).</span><span class="sxs-lookup"><span data-stu-id="aa7c0-148">For an example of using non-node data, see [Separating configuration and environment data](separatingEnvData.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="aa7c0-149">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="aa7c0-149">See Also</span></span>

- [<span data-ttu-id="aa7c0-150">A konfigurációs adatok hitelesítő adatok beállításai</span><span class="sxs-lookup"><span data-stu-id="aa7c0-150">Credentials Options in Configuration Data</span></span>](configDataCredentials.md)
- [<span data-ttu-id="aa7c0-151">DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="aa7c0-151">DSC Configurations</span></span>](configurations.md)