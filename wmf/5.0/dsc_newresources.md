---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 64a00e041bbeeea117db43116b486e83dfe923b0
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688258"
---
# <a name="new-built-in-dsc-resources"></a><span data-ttu-id="d7840-102">Új beépített DSC-erőforrások</span><span class="sxs-lookup"><span data-stu-id="d7840-102">New built-in DSC resources</span></span>

<span data-ttu-id="d7840-103">4 új DSC-erőforrásokat a WMF 5.0 RTM-re van:</span><span class="sxs-lookup"><span data-stu-id="d7840-103">WMF 5.0 RTM has 4 new DSC resources:</span></span>
* <span data-ttu-id="d7840-104">WindowsFeatureSet</span><span class="sxs-lookup"><span data-stu-id="d7840-104">WindowsFeatureSet</span></span>
* <span data-ttu-id="d7840-105">WindowsOptionalFeatureSet</span><span class="sxs-lookup"><span data-stu-id="d7840-105">WindowsOptionalFeatureSet</span></span>
* <span data-ttu-id="d7840-106">ServiceSet</span><span class="sxs-lookup"><span data-stu-id="d7840-106">ServiceSet</span></span>
* <span data-ttu-id="d7840-107">ProcessSet</span><span class="sxs-lookup"><span data-stu-id="d7840-107">ProcessSet</span></span>

<span data-ttu-id="d7840-108">Ezek az erőforrások egyetlen erőforrás-hívás használatával több példány konfigurálása egyszerű módot biztosítanak.</span><span class="sxs-lookup"><span data-stu-id="d7840-108">These resources provide an easy way to configure multiple instances using a single resource call.</span></span>

## <a name="windowsfeatureset"></a><span data-ttu-id="d7840-109">WindowsFeatureSet</span><span class="sxs-lookup"><span data-stu-id="d7840-109">WindowsFeatureSet</span></span>

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

## <a name="windowsoptionalfeatureset"></a><span data-ttu-id="d7840-110">WindowsOptionalFeatureSet</span><span class="sxs-lookup"><span data-stu-id="d7840-110">WindowsOptionalFeatureSet</span></span>

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

## <a name="serviceset"></a><span data-ttu-id="d7840-111">ServiceSet</span><span class="sxs-lookup"><span data-stu-id="d7840-111">ServiceSet</span></span>

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

## <a name="processset"></a><span data-ttu-id="d7840-112">ProcessSet</span><span class="sxs-lookup"><span data-stu-id="d7840-112">ProcessSet</span></span>

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
