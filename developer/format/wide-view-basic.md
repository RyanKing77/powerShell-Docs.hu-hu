---
title: Széles nézet (alapszintű) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9abb63b8-6d02-4e24-9c0e-2d15a04e9051
caps.latest.revision: 8
ms.openlocfilehash: 7a36f548a3eccdf2c9cad04a8bfe28bf4e8d6dfd
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083739"
---
# <a name="wide-view-basic"></a><span data-ttu-id="b1d12-102">Széles nézet (Alapszintű)</span><span class="sxs-lookup"><span data-stu-id="b1d12-102">Wide View (Basic)</span></span>

<span data-ttu-id="b1d12-103">Ez a példa bemutatja, hogyan valósíthat meg egy alapszintű széles nézet, amely megjeleníti a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) által visszaadott objektumok a `Get-Service` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="b1d12-103">This example shows how to implement a basic wide view that displays the [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) objects returned by the `Get-Service` cmdlet.</span></span> <span data-ttu-id="b1d12-104">Egy széles nézet az összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="b1d12-104">For more information about the components of a wide view, see [Creating a Wide View](./creating-a-wide-view.md).</span></span>

### <a name="to-load-this-formatting-file"></a><span data-ttu-id="b1d12-105">Ez a formázási fájl betöltése</span><span class="sxs-lookup"><span data-stu-id="b1d12-105">To load this formatting file</span></span>

1. <span data-ttu-id="b1d12-106">Az XML-fájl másolása a példa című fejezetet a témakör egy szövegfájlba.</span><span class="sxs-lookup"><span data-stu-id="b1d12-106">Copy the XML from the Example section of this topic into a text file.</span></span>

2. <span data-ttu-id="b1d12-107">Mentse a fájlt.</span><span class="sxs-lookup"><span data-stu-id="b1d12-107">Save the text file.</span></span> <span data-ttu-id="b1d12-108">Adja hozzá a `format.ps1xml` kiterjesztést a fájl formázási fájlként az azonosításához.</span><span class="sxs-lookup"><span data-stu-id="b1d12-108">Be sure to add the `format.ps1xml` extension to the file to identify it as a formatting file.</span></span>

3. <span data-ttu-id="b1d12-109">Nyissa meg a Windows Powershellt, és futtassa a következő parancsot betölteni a formázási fájlt az aktuális munkamenetbe: `Update-formatdata -prependpath PathToFormattingFile`.</span><span class="sxs-lookup"><span data-stu-id="b1d12-109">Open Windows PowerShell, and run the following command to load the formatting file into the current session: `Update-formatdata -prependpath PathToFormattingFile`.</span></span>

   > [!WARNING]
   > <span data-ttu-id="b1d12-110">A formázási fájl olyan objektum, amely már definiálva van egy Windows PowerShell formázási fájl megjelenítését határozza meg.</span><span class="sxs-lookup"><span data-stu-id="b1d12-110">This formatting file defines the display of an object that is already defined by a Windows PowerShell formatting file.</span></span> <span data-ttu-id="b1d12-111">Kell használnia a `prependPath` paramétert, ha futtatja a parancsmagot, és nem tölthető be, a formázást modulként fájlt.</span><span class="sxs-lookup"><span data-stu-id="b1d12-111">You must use the `prependPath` parameter when you run the cmdlet, and you cannot load this formatting file as a module.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="b1d12-112">Azt ismerteti</span><span class="sxs-lookup"><span data-stu-id="b1d12-112">Demonstrates</span></span>

<span data-ttu-id="b1d12-113">Ez a fájl formázási mutat be a következő XML-elemeket:</span><span class="sxs-lookup"><span data-stu-id="b1d12-113">This formatting file demonstrates the following XML elements:</span></span>

- <span data-ttu-id="b1d12-114">A [neve](./name-element-for-view-format.md) elem a nézet.</span><span class="sxs-lookup"><span data-stu-id="b1d12-114">The [Name](./name-element-for-view-format.md) element for the view.</span></span>

- <span data-ttu-id="b1d12-115">A [ViewSelectedBy](./viewselectedby-element-format.md) elem, amely meghatározza, milyen objektumok jelennek meg a nézet által.</span><span class="sxs-lookup"><span data-stu-id="b1d12-115">The [ViewSelectedBy](./viewselectedby-element-format.md) element that defines what objects are displayed by the view.</span></span>

- <span data-ttu-id="b1d12-116">A [WideItem](./wideitem-element-for-widecontrol-format.md) elem, amely meghatározza, milyen tulajdonság szerint a nézet jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="b1d12-116">The [WideItem](./wideitem-element-for-widecontrol-format.md) element that defines what property is displayed by the view.</span></span>

## <a name="example"></a><span data-ttu-id="b1d12-117">Példa</span><span class="sxs-lookup"><span data-stu-id="b1d12-117">Example</span></span>

<span data-ttu-id="b1d12-118">A következő XML formátumú értékét jeleníti meg a széles nézet határozza meg a [System.Serviceprocess.Servicecontroller.Servicename](/dotnet/api/System.ServiceProcess.ServiceController.ServiceName) tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="b1d12-118">The following XML defines a wide view that displays the value of the [System.Serviceprocess.Servicecontroller.Servicename](/dotnet/api/System.ServiceProcess.ServiceController.ServiceName) property.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>

<Configuration>
  <ViewDefinitions>
    <View>
      <Name>ServiceWideView</Name>
      <ViewSelectedBy>
        <TypeName>System.ServiceProcess.ServiceController</TypeName>
      </ViewSelectedBy>
      <WideControl>
        <WideEntries>
          <WideEntry>
            <WideItem>
              <PropertyName>ServiceName</PropertyName>
            </WideItem>
          </WideEntry>
        </WideEntries>
      </WideControl>
    </View>
  </ViewDefinitions>
</Configuration>
```

<span data-ttu-id="b1d12-119">Az alábbi példa bemutatja, hogyan jelenítse meg a Windows PowerShell a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) után betöltődik a formátumfájlban objektumokat.</span><span class="sxs-lookup"><span data-stu-id="b1d12-119">The following example shows how Windows PowerShell displays the [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) objects after this format file is loaded.</span></span>

```powershell
Get-Service f*
```

```output
Fax                      FCSAM
fdPHost                  FDResPub
FontCache                FontCache3.0.0.0
FSysAgent                FwcAgent
```

## <a name="see-also"></a><span data-ttu-id="b1d12-120">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b1d12-120">See Also</span></span>

[<span data-ttu-id="b1d12-121">Példák a formázási fájlok</span><span class="sxs-lookup"><span data-stu-id="b1d12-121">Examples of Formatting Files</span></span>](./examples-of-formatting-files.md)

[<span data-ttu-id="b1d12-122">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="b1d12-122">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
