---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Konfigurációs adatok használata
ms.openlocfilehash: 19544494a547a06d87701b38585844cb11d03e33
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="using-configuration-data-in-dsc"></a><span data-ttu-id="c01cd-103">A DSC konfigurációs adatok használata</span><span class="sxs-lookup"><span data-stu-id="c01cd-103">Using configuration data in DSC</span></span>

><span data-ttu-id="c01cd-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="c01cd-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="c01cd-105">A beépített DSC használatával **ConfigurationData** paraméter, használhatja a konfigurációs adatok definiálhat.</span><span class="sxs-lookup"><span data-stu-id="c01cd-105">By using the built-in DSC **ConfigurationData** parameter, you can define data that can be used within a configuration.</span></span>
<span data-ttu-id="c01cd-106">Ez lehetővé teszi több csomópont vagy különböző környezetekben használható egyetlen konfiguráció létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="c01cd-106">This allows you to create a single configuration that can be used for multiple nodes or for different environments.</span></span>
<span data-ttu-id="c01cd-107">Például ha alkalmazást fejleszt, után egy konfigurációt használja a fejlesztési és éles környezetben is, is minden környezet adatainak megadása a konfigurációs adatok használatával.</span><span class="sxs-lookup"><span data-stu-id="c01cd-107">For example, if you are developing an application, you can use one configuration for both development and production environments, and use configuration data to specify data for each environment.</span></span>

<span data-ttu-id="c01cd-108">Ez a témakör ismerteti a szerkezete a **ConfigurationData** hibás.</span><span class="sxs-lookup"><span data-stu-id="c01cd-108">This topic describes the structure of the **ConfigurationData** hashtable.</span></span>
<span data-ttu-id="c01cd-109">Konfigurációs adatok használatára, tekintse meg a [konfigurációs és környezeti adatok elválasztó](separatingEnvData.md).</span><span class="sxs-lookup"><span data-stu-id="c01cd-109">For examples of how to use configuration data, see [Separating configuration and environment data](separatingEnvData.md).</span></span>

## <a name="the-configurationdata-common-parameter"></a><span data-ttu-id="c01cd-110">A ConfigurationData általános paraméter</span><span class="sxs-lookup"><span data-stu-id="c01cd-110">The ConfigurationData common parameter</span></span>

<span data-ttu-id="c01cd-111">A DSC-konfiguráció egy közös paramétert fogad, **ConfigurationData**, meg kell adnia a konfiguráció-fordítási mikor.</span><span class="sxs-lookup"><span data-stu-id="c01cd-111">A DSC configuration takes a common parameter, **ConfigurationData**, that you specify when you compile the configuration.</span></span>
<span data-ttu-id="c01cd-112">További információ a konfiguráció fordítása: [a DSC-konfigurációk](configurations.md).</span><span class="sxs-lookup"><span data-stu-id="c01cd-112">For information about compiling configurations, see [DSC configurations](configurations.md).</span></span>

<span data-ttu-id="c01cd-113">A **ConfigurationData** paraméter egy hasthtable, rendelkeznie kell legalább egy nevű kulcs **AllNodes**.</span><span class="sxs-lookup"><span data-stu-id="c01cd-113">The **ConfigurationData** parameter is a hasthtable that must have at least one key named **AllNodes**.</span></span>
<span data-ttu-id="c01cd-114">Egy vagy több kulcsot is rendelkezhet.</span><span class="sxs-lookup"><span data-stu-id="c01cd-114">It can also have one or more other keys.</span></span>

><span data-ttu-id="c01cd-115">**Megjegyzés:** ebben a témakörben szereplő példák egyetlen további kulcs használata (csak a megnevezett **AllNodes** kulcs) nevű `NonNodeData`, de további kulcsok tetszőleges számú, és nevezze függetlenül szeretné.</span><span class="sxs-lookup"><span data-stu-id="c01cd-115">**Note:** The examples in this topic use a single additional key (other than the named **AllNodes** key) named `NonNodeData`, but you can include any number of additional keys, and name them whatever you want.</span></span>

```powershell
$MyData =
@{
    AllNodes = @()
    NonNodeData = ""
}
```

<span data-ttu-id="c01cd-116">Értékét a **AllNodes** kulcs egy tömb.</span><span class="sxs-lookup"><span data-stu-id="c01cd-116">The value of the **AllNodes** key is an array.</span></span> <span data-ttu-id="c01cd-117">A tömb egyes elemei egyben rendelkeznie kell legalább egy nevű kulcs kivonattáblát **csomópontnév**:</span><span class="sxs-lookup"><span data-stu-id="c01cd-117">Each element of this array is also a hash table that must have at least one key named **NodeName**:</span></span>

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

<span data-ttu-id="c01cd-118">Más kulcsok minden egyes kivonattáblát is hozzáadhat:</span><span class="sxs-lookup"><span data-stu-id="c01cd-118">You can add other keys to each hash table as well:</span></span>

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

<span data-ttu-id="c01cd-119">Az összes csomópontra érvényes tulajdonság, tagja hozhat létre a **AllNodes** tömb, amely rendelkezik egy **csomópontnév** a `*`.</span><span class="sxs-lookup"><span data-stu-id="c01cd-119">To apply a property to all nodes, you can create a member of the **AllNodes** array that has a **NodeName** of `*`.</span></span>
<span data-ttu-id="c01cd-120">Például, hogy minden csomópont egy `LogPath` tulajdonság, sikerült ehhez:</span><span class="sxs-lookup"><span data-stu-id="c01cd-120">For example, to give every node a `LogPath` property, you could do this:</span></span>

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

<span data-ttu-id="c01cd-121">Ez megfelel a nevű tulajdonság hozzáadása `LogPath` értékkel rendelkező `"C:\Logs"` minden más blokkok (`VM-1`, `VM-2`, és `VM-3`).</span><span class="sxs-lookup"><span data-stu-id="c01cd-121">This is the equivalent of adding a property with a name of `LogPath` with a value of `"C:\Logs"` to each of the other blocks (`VM-1`, `VM-2`, and `VM-3`).</span></span>

## <a name="defining-the-configurationdata-hashtable"></a><span data-ttu-id="c01cd-122">A ConfigurationData szórótáblájában meghatározása</span><span class="sxs-lookup"><span data-stu-id="c01cd-122">Defining the ConfigurationData hashtable</span></span>

<span data-ttu-id="c01cd-123">Megadhat **ConfigurationData** vagy belül (ahogy az előző példák) egy konfigurációs parancsfájl fájlt változóként vagy külön `.psd1` fájlt.</span><span class="sxs-lookup"><span data-stu-id="c01cd-123">You can define **ConfigurationData** either as a variable within the same script file as a configuration (as in our previous examples) or in a separate `.psd1` file.</span></span>
<span data-ttu-id="c01cd-124">Meghatározásához **ConfigurationData** a egy `.psd1` fájlt, hozzon létre egy fájlt, amely csak a kivonattábla a konfigurációs adatok jelölő tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="c01cd-124">To define **ConfigurationData** in a `.psd1` file, create a file that contains only the hashtable that represents the configuration data.</span></span>

<span data-ttu-id="c01cd-125">Például létrehozhat egy fájlt `MyData.psd1` a következő tartalommal:</span><span class="sxs-lookup"><span data-stu-id="c01cd-125">For example, you could create a file named `MyData.psd1` with the following contents:</span></span>

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

## <a name="compiling-a-configuration-with-configuration-data"></a><span data-ttu-id="c01cd-126">A konfigurációs adatok konfiguráció fordítása</span><span class="sxs-lookup"><span data-stu-id="c01cd-126">Compiling a configuration with configuration data</span></span>

<span data-ttu-id="c01cd-127">Egy konfigurációt, amely meghatározta a konfigurációs adatok lefordításához át a konfigurációs adatokat az értékeként a **ConfigurationData** paraméter.</span><span class="sxs-lookup"><span data-stu-id="c01cd-127">To compile a configuration for which you have defined configuration data, you pass the configuration data as the value of the **ConfigurationData** parameter.</span></span>

<span data-ttu-id="c01cd-128">Ezzel létrehoz minden bejegyzés esetében MOF-fájlt a **AllNodes** tömb.</span><span class="sxs-lookup"><span data-stu-id="c01cd-128">This will create a MOF file for each entry in the **AllNodes** array.</span></span>
<span data-ttu-id="c01cd-129">Minden egyes MOF-fájlt nevű a `NodeName` a megfelelő tömb tétel tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="c01cd-129">Each MOF file will be named with the `NodeName` property of the corresponding array entry.</span></span>

<span data-ttu-id="c01cd-130">Például, mint a konfigurációs adatok megadása a `MyData.psd1` fájl újabb, a konfiguráció fordítása hozna létre, mindkét `VM-1.mof` és `VM-2.mof` fájlokat.</span><span class="sxs-lookup"><span data-stu-id="c01cd-130">For example, if you define configuration data as in the `MyData.psd1` file above, compiling a configuration would create both `VM-1.mof` and `VM-2.mof` files.</span></span>

### <a name="compiling-a-configuration-with-configuration-data-using-a-variable"></a><span data-ttu-id="c01cd-131">A konfiguráció fordítása és konfigurációs adatokat, a változó</span><span class="sxs-lookup"><span data-stu-id="c01cd-131">Compiling a configuration with configuration data using a variable</span></span>

<span data-ttu-id="c01cd-132">Konfigurációs adatok azonos változóként definiált használandó `.ps1` fájl beállításként, adja meg a változó nevét az értékeként a **ConfigurationData** paraméter, a konfiguráció fordítása során:</span><span class="sxs-lookup"><span data-stu-id="c01cd-132">To use configuration data that is defined as a variable in the same `.ps1` file as the configuration, you pass the variable name as the value of the **ConfigurationData** parameter when compiling the configuration:</span></span>

```powershell
MyDscConfiguration -ConfigurationData $MyData
```

### <a name="compiling-a-configuration-with-configuration-data-using-a-data-file"></a><span data-ttu-id="c01cd-133">A konfiguráció fordítása és konfigurációs adatokat, egy adatfájlt</span><span class="sxs-lookup"><span data-stu-id="c01cd-133">Compiling a configuration with configuration data using a data file</span></span>

<span data-ttu-id="c01cd-134">Egy .psd1 fájlban meghatározott konfigurációs adatok használatához adja meg az elérési útját és nevét, hogy a fájl értékeként a **ConfigurationData** paraméter, a konfiguráció fordítása során:</span><span class="sxs-lookup"><span data-stu-id="c01cd-134">To use configuration data that is defined in a .psd1 file, you pass the path and name of that file as the value of the **ConfigurationData** parameter when compiling the configuration:</span></span>

```powershell
MyDscConfiguration -ConfigurationData .\MyData.psd1
```

## <a name="using-configurationdata-variables-in-a-configuration"></a><span data-ttu-id="c01cd-135">Egy konfigurációs ConfigurationData változók használata</span><span class="sxs-lookup"><span data-stu-id="c01cd-135">Using ConfigurationData variables in a configuration</span></span>

<span data-ttu-id="c01cd-136">DSC nyújt három néhány speciális változó, amely egy konfigurációs parancsfájl használható: **$AllNodes**, **$Node**, és **$ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="c01cd-136">DSC provides three special variables that can be used in a configuration script: **$AllNodes**, **$Node**, and **$ConfigurationData**.</span></span>

- <span data-ttu-id="c01cd-137">**$AllNodes** hivatkozik a teljes gyűjteményt a meghatározott csomópontok **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="c01cd-137">**$AllNodes** refers to the entire collection of nodes defined in **ConfigurationData**.</span></span> <span data-ttu-id="c01cd-138">Szűrheti a **AllNodes** gyűjtemény segítségével **. WHERE()** és **. ForEach()**.</span><span class="sxs-lookup"><span data-stu-id="c01cd-138">You can filter the **AllNodes** collection by using **.Where()** and **.ForEach()**.</span></span>
- <span data-ttu-id="c01cd-139">**Csomópont** egy adott bejegyzés hivatkozik a **AllNodes** gyűjtemény után a szűrt **. WHERE()** vagy **. ForEach()**.</span><span class="sxs-lookup"><span data-stu-id="c01cd-139">**Node** refers to a particular entry in the **AllNodes** collection after it is filtered by using **.Where()** or **.ForEach()**.</span></span>
- <span data-ttu-id="c01cd-140">**ConfigurationData** hivatkozik a teljes kivonattábla a konfiguráció fordítása során átadott paraméterként.</span><span class="sxs-lookup"><span data-stu-id="c01cd-140">**ConfigurationData** refers to the entire hash table that is passed as the parameter when compiling a configuration.</span></span>

## <a name="using-non-node-data"></a><span data-ttu-id="c01cd-141">Nem-csomópont adatok használata</span><span class="sxs-lookup"><span data-stu-id="c01cd-141">Using non-node data</span></span>

<span data-ttu-id="c01cd-142">Mivel az előző példákban is láttuk a **ConfigurationData** hashtable rendelkezhet egy vagy több kulcsot mellett a szükséges **AllNodes** kulcs.</span><span class="sxs-lookup"><span data-stu-id="c01cd-142">As we've seen in previous examples, the **ConfigurationData** hashtable can have one or more keys in addition to the required **AllNodes** key.</span></span>
<span data-ttu-id="c01cd-143">Ebben a témakörben a példákban azt egyetlen további csomópont használja, és azt nevű `NonNodeData`.</span><span class="sxs-lookup"><span data-stu-id="c01cd-143">In the examples in this topic, we have used only a single additional node, and named it `NonNodeData`.</span></span>
<span data-ttu-id="c01cd-144">Azonban minden további kulcsok számának megadása, és bármilyen kívánt nevet őket.</span><span class="sxs-lookup"><span data-stu-id="c01cd-144">However, you can define any number of additional keys, and name them anything you want.</span></span>

<span data-ttu-id="c01cd-145">Például egy nem csomópont adatok használatával, lásd: [konfigurációs és környezeti adatok elválasztó](separatingEnvData.md).</span><span class="sxs-lookup"><span data-stu-id="c01cd-145">For an example of using non-node data, see [Separating configuration and environment data](separatingEnvData.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="c01cd-146">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c01cd-146">See Also</span></span>
- [<span data-ttu-id="c01cd-147">Konfigurációs adatokat a hitelesítő adatok beállításai</span><span class="sxs-lookup"><span data-stu-id="c01cd-147">Credentials Options in Configuration Data</span></span>](configDataCredentials.md)
- [<span data-ttu-id="c01cd-148">A DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="c01cd-148">DSC Configurations</span></span>](configurations.md)