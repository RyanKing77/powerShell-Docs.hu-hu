---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 64a00e041bbeeea117db43116b486e83dfe923b0
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62085830"
---
# <a name="new-built-in-dsc-resources"></a><span data-ttu-id="aa58a-102">Új beépített DSC-erőforrások</span><span class="sxs-lookup"><span data-stu-id="aa58a-102">New built-in DSC resources</span></span>

<span data-ttu-id="aa58a-103">4 új DSC-erőforrásokat a WMF 5.0 RTM-re van:</span><span class="sxs-lookup"><span data-stu-id="aa58a-103">WMF 5.0 RTM has 4 new DSC resources:</span></span>
* <span data-ttu-id="aa58a-104">WindowsFeatureSet</span><span class="sxs-lookup"><span data-stu-id="aa58a-104">WindowsFeatureSet</span></span>
* <span data-ttu-id="aa58a-105">WindowsOptionalFeatureSet</span><span class="sxs-lookup"><span data-stu-id="aa58a-105">WindowsOptionalFeatureSet</span></span>
* <span data-ttu-id="aa58a-106">ServiceSet</span><span class="sxs-lookup"><span data-stu-id="aa58a-106">ServiceSet</span></span>
* <span data-ttu-id="aa58a-107">ProcessSet</span><span class="sxs-lookup"><span data-stu-id="aa58a-107">ProcessSet</span></span>

<span data-ttu-id="aa58a-108">Ezek az erőforrások egyetlen erőforrás-hívás használatával több példány konfigurálása egyszerű módot biztosítanak.</span><span class="sxs-lookup"><span data-stu-id="aa58a-108">These resources provide an easy way to configure multiple instances using a single resource call.</span></span>

## <a name="windowsfeatureset"></a><span data-ttu-id="aa58a-109">WindowsFeatureSet</span><span class="sxs-lookup"><span data-stu-id="aa58a-109">WindowsFeatureSet</span></span>

```powershell
# Get the syntax of WindowsFeatureSet resource
Get-DscResource -Module psdesiredstateconfiguration -Name WindowsFeatureSet -Syntax

WindowsFeatureSet [String] #ResourceName
{
    [DependsOn = [String[]]]
    Name = [String[]]
    [Ensure = [String]]
    [Source = [String]]
    [IncludeAllSubFeature = [Boolean]]
    [Credential = [PSCredential]]
    [LogPath = [String]]
}
```

## <a name="windowsoptionalfeatureset"></a><span data-ttu-id="aa58a-110">WindowsOptionalFeatureSet</span><span class="sxs-lookup"><span data-stu-id="aa58a-110">WindowsOptionalFeatureSet</span></span>

```powershell
# Get the syntax of WindowsOptionalFeatureSet resource
Get-DscResource -Module psdesiredstateconfiguration -Name WindowsOptionalFeatureSet -Syntax

WindowsOptionalFeatureSet [String] #ResourceName
{
    [DependsOn = [String[]]]
    Name = [String[]]
    Ensure = [String]
    [Source = [String[]]]
    [RemoveFilesOnDisable = [Boolean]]
    [LogPath = [String]]
    [NoWindowsUpdateCheck = [Boolean]]
    [LogLevel = [String]]
}
```

## <a name="serviceset"></a><span data-ttu-id="aa58a-111">ServiceSet</span><span class="sxs-lookup"><span data-stu-id="aa58a-111">ServiceSet</span></span>

```powershell
# Get the syntax of ServiceSet resource
Get-DscResource -Module psdesiredstateconfiguration -Name ServiceSet -Syntax

ServiceSet [String] #ResourceName
{
    [DependsOn = [String[]]]
    Name = [String[]]
    [StartupType = [String]]
    [BuiltInAccount = [String]]
    [State = [String]]
    [Ensure = [String]]
    [Credential = [PSCredential]]
}
```

## <a name="processset"></a><span data-ttu-id="aa58a-112">ProcessSet</span><span class="sxs-lookup"><span data-stu-id="aa58a-112">ProcessSet</span></span>

```powershell
# Get the syntax of ProcessSet resource
Get-DscResource -Module psdesiredstateconfiguration -Name ProcessSet -Syntax

ProcessSet [String] #ResourceName
{
    [DependsOn = [String[]]]
    Path = [String[]]
    [Credential = [PSCredential]]
    [Ensure = [String]]
    [StandardOutputPath = [String]]
    [StandardErrorPath = [String]]
    [StandardInputPath = [String]]
    [WorkingDirectory = [String]]
}
```
