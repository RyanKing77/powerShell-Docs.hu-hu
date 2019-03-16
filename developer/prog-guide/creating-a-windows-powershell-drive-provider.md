---
title: A Windows PowerShell meghajtót szolgáltató létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- drive providers [PowerShell Programmer's Guide]
- providers [PowerShell Programmer's Guide], drive provider
- drives [PowerShell Programmer's Guide]
ms.assetid: 2b446841-6616-4720-9ff8-50801d7576ed
caps.latest.revision: 6
ms.openlocfilehash: 174d3a6860790295e1b73f32d9c1bad46b653917
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58055649"
---
# <a name="creating-a-windows-powershell-drive-provider"></a><span data-ttu-id="588fa-102">Windows PowerShelles meghajtószolgáltató létrehozása</span><span class="sxs-lookup"><span data-stu-id="588fa-102">Creating a Windows PowerShell Drive Provider</span></span>

<span data-ttu-id="588fa-103">Ez a témakör ismerteti, hogyan hozhat létre egy Windows PowerShell meghajtót szolgáltató, amely lehetővé teszi egy data store eléréséhez keresztül egy Windows PowerShell meghajtót.</span><span class="sxs-lookup"><span data-stu-id="588fa-103">This topic describes how to create a Windows PowerShell drive provider that provides a way to access a data store through a Windows PowerShell drive.</span></span> <span data-ttu-id="588fa-104">Az ilyen típusú szolgáltató is nevezik szolgáltatók a Windows PowerShell meghajtót.</span><span class="sxs-lookup"><span data-stu-id="588fa-104">This type of provider is also referred to as Windows PowerShell drive providers.</span></span> <span data-ttu-id="588fa-105">A Windows PowerShell-meghajtók, a szolgáltató által használt adja meg az azt jelenti, hogy csatlakozni az adattárhoz.</span><span class="sxs-lookup"><span data-stu-id="588fa-105">The Windows PowerShell drives used by the provider provide the means to connect to the data store.</span></span>

<span data-ttu-id="588fa-106">Az itt leírtak szerint a Windows PowerShell meghajtószolgáltató egy Microsoft Access-adatbázis hozzáférést biztosít.</span><span class="sxs-lookup"><span data-stu-id="588fa-106">The Windows PowerShell drive provider described here provides access to a Microsoft Access database.</span></span> <span data-ttu-id="588fa-107">A szolgáltató, a Windows PowerShell meghajtót jelöl az adatbázisban (lehetőség a meghajtószolgáltató tetszőleges számú meghajtók hozzáadása), a legfelső szintű tárolókat a meghajtó képviselik a táblák az adatbázisban, és a tárolók elemeket képviseli sora a táblák.</span><span class="sxs-lookup"><span data-stu-id="588fa-107">For this provider, the Windows PowerShell drive represents the database (it is possible to add any number of drives to a drive provider), the top-level containers of the drive represent the tables in the database, and the items of the containers represent the rows in the tables.</span></span>

<span data-ttu-id="588fa-108">Itt van ez a témakör szakaszai listáját.</span><span class="sxs-lookup"><span data-stu-id="588fa-108">Here is a list of the sections in this topic.</span></span> <span data-ttu-id="588fa-109">Ha nem ismeri a Windows PowerShell meghajtót szolgáltató írása, olvassa el az ezekben a szakaszokban a sorrendben jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="588fa-109">If you are unfamiliar with writing a Windows PowerShell drive provider, read these sections in the order that they appear.</span></span> <span data-ttu-id="588fa-110">Azonban ha ismeri, a meghajtó szolgáltató írása, nyissa meg közvetlenül a keresett információt.</span><span class="sxs-lookup"><span data-stu-id="588fa-110">However, if you are familiar with writing a drive provider, please go directly to the information that you need.</span></span>

- [<span data-ttu-id="588fa-111">A Windows PowerShell-szolgáltatóban osztály meghatározása</span><span class="sxs-lookup"><span data-stu-id="588fa-111">Defining the Windows PowerShell Provider Class</span></span>](#Defining-the-Windows-PowerShell-Provider-Class)

- [<span data-ttu-id="588fa-112">Alapfunkciók meghatározása</span><span class="sxs-lookup"><span data-stu-id="588fa-112">Defining Base Functionality</span></span>](#Defining-Base-Functionality)

- [<span data-ttu-id="588fa-113">Meghajtó állapota adatok létrehozása</span><span class="sxs-lookup"><span data-stu-id="588fa-113">Creating Drive State Information</span></span>](#Creating-Drive-State-Information)

- [<span data-ttu-id="588fa-114">A meghajtó létrehozása</span><span class="sxs-lookup"><span data-stu-id="588fa-114">Creating a Drive</span></span>](#Creating-a-Drive)

- [<span data-ttu-id="588fa-115">Dinamikus paraméterek NewDrive csatolása</span><span class="sxs-lookup"><span data-stu-id="588fa-115">Attaching Dynamic Parameters to NewDrive</span></span>](#Attaching-Dynamic-Parameters-to-NewDrive)

- [<span data-ttu-id="588fa-116">A meghajtó eltávolítása</span><span class="sxs-lookup"><span data-stu-id="588fa-116">Removing a Drive</span></span>](#Removing-a-Drive)

- [<span data-ttu-id="588fa-117">Alapértelmezett inicializálása meghajtók</span><span class="sxs-lookup"><span data-stu-id="588fa-117">Initializing Default Drives</span></span>](#Initializing-Default-Drives)

- [<span data-ttu-id="588fa-118">Kódminta</span><span class="sxs-lookup"><span data-stu-id="588fa-118">Code Sample</span></span>](#Code-Sample)

- [<span data-ttu-id="588fa-119">A Windows PowerShell meghajtót szolgáltató tesztelése</span><span class="sxs-lookup"><span data-stu-id="588fa-119">Testing the Windows PowerShell Drive Provider</span></span>](#Testing-the-Windows-PowerShell-Drive-Provider)

## <a name="defining-the-windows-powershell-provider-class"></a><span data-ttu-id="588fa-120">A Windows PowerShell-szolgáltatóban osztály meghatározása</span><span class="sxs-lookup"><span data-stu-id="588fa-120">Defining the Windows PowerShell Provider Class</span></span>

<span data-ttu-id="588fa-121">A meghajtószolgáltató definiálnia kell egy .NET-osztályt, amely az a [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) alaposztály.</span><span class="sxs-lookup"><span data-stu-id="588fa-121">Your drive provider must define a .NET class that derives from the [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) base class.</span></span> <span data-ttu-id="588fa-122">Íme a meghajtó-szolgáltató az osztálydefiníció:</span><span class="sxs-lookup"><span data-stu-id="588fa-122">Here is the class definition for this drive provider:</span></span>

[!code-csharp[AccessDBProviderSample02.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample02/AccessDBProviderSample02.cs#L29-L30 "AccessDBProviderSample02.cs")]

<span data-ttu-id="588fa-123">Figyelje meg, hogy ebben a példában a [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) attribútum határozza meg a szolgáltató és a Windows PowerShell adott funkciók felhasználóbarát nevét, amely a szolgáltató elérhetővé teszi a Windows PowerShell-modul a parancs feldolgozása közben.</span><span class="sxs-lookup"><span data-stu-id="588fa-123">Notice that in this example, the [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) attribute specifies a user-friendly name for the provider and the Windows PowerShell specific capabilities that the provider exposes to the Windows PowerShell runtime during command processing.</span></span> <span data-ttu-id="588fa-124">A lehetséges értékek a szolgáltató képességei határozzák meg a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumerálása.</span><span class="sxs-lookup"><span data-stu-id="588fa-124">The possible values for the provider capabilities are defined by the [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumeration.</span></span> <span data-ttu-id="588fa-125">A meghajtó-szolgáltató nem támogatja ezeket a képességeket bármelyikét.</span><span class="sxs-lookup"><span data-stu-id="588fa-125">This drive provider does not support any of these capabilities.</span></span>

## <a name="defining-base-functionality"></a><span data-ttu-id="588fa-126">Alapfunkciók meghatározása</span><span class="sxs-lookup"><span data-stu-id="588fa-126">Defining Base Functionality</span></span>

<span data-ttu-id="588fa-127">Leírtak szerint [terv a Windows PowerShell-szolgáltatóban](./designing-your-windows-powershell-provider.md), a [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) származik a [ System.Management.Automation.Provider.Cmdletprovider](/dotnet/api/System.Management.Automation.Provider.CmdletProvider) alaposztály, amely meghatározza a módszereket, inicializálása és a szolgáltató uninitializing szükséges.</span><span class="sxs-lookup"><span data-stu-id="588fa-127">As described in [Design Your Windows PowerShell Provider](./designing-your-windows-powershell-provider.md), the [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) class derives from the [System.Management.Automation.Provider.Cmdletprovider](/dotnet/api/System.Management.Automation.Provider.CmdletProvider) base class that defines the methods needed for initializing and uninitializing the provider.</span></span> <span data-ttu-id="588fa-128">Munkamenet-specifikus inicializálási információk hozzáadása és a szolgáltató által használt erőforrások felszabadítása funkció megvalósítását, lásd: [alapvető Windows PowerShell-szolgáltató létrehozása](./creating-a-basic-windows-powershell-provider.md).</span><span class="sxs-lookup"><span data-stu-id="588fa-128">To implement functionality for adding session-specific initialization information and for releasing resources that are used by the provider, see [Creating a Basic Windows PowerShell Provider](./creating-a-basic-windows-powershell-provider.md).</span></span> <span data-ttu-id="588fa-129">A legtöbb szolgáltatók (beleértve a szolgáltató az itt leírtak szerint) is használják, ez a funkció Windows PowerShell által biztosított alapértelmezett megvalósítása.</span><span class="sxs-lookup"><span data-stu-id="588fa-129">However, most providers (including the provider described here) can use the default implementation of this functionality that is provided by Windows PowerShell.</span></span>

## <a name="creating-drive-state-information"></a><span data-ttu-id="588fa-130">Meghajtó állapota adatok létrehozása</span><span class="sxs-lookup"><span data-stu-id="588fa-130">Creating Drive State Information</span></span>

<span data-ttu-id="588fa-131">Összes Windows PowerShell-szolgáltató minősülnek állapot nélküli, ami azt jelenti, hogy a meghajtószolgáltató kell létrehozni, amely a Windows PowerShell-modul által van szükség, ha meghívja a szolgáltató kapcsolatos állapotinformációkat.</span><span class="sxs-lookup"><span data-stu-id="588fa-131">All Windows PowerShell providers are considered stateless, which means that your drive provider needs to create any state information that is needed by the Windows PowerShell runtime when it calls your provider.</span></span>

<span data-ttu-id="588fa-132">A meghajtó szolgáltató állapotinformációkat tartalmaz a kapcsolat az adatbázissal, hogy a meghajtó információi részeként.</span><span class="sxs-lookup"><span data-stu-id="588fa-132">For this drive provider, state information includes the connection to the database that is kept as part of the drive information.</span></span> <span data-ttu-id="588fa-133">A következő kódot, amely ezt az információt a módjára látható a [System.Management.Automation.PSDriveinfo](/dotnet/api/System.Management.Automation.PSDriveInfo) objektum, amely ismerteti a meghajtó:</span><span class="sxs-lookup"><span data-stu-id="588fa-133">Here is code that shows how this information is stored in the [System.Management.Automation.PSDriveinfo](/dotnet/api/System.Management.Automation.PSDriveInfo) object that describes the drive:</span></span>

[!code-csharp[AccessDBProviderSample02.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample02/AccessDBProviderSample02.cs#L130-L151 "AccessDBProviderSample02.cs")]

## <a name="creating-a-drive"></a><span data-ttu-id="588fa-134">A meghajtó létrehozása</span><span class="sxs-lookup"><span data-stu-id="588fa-134">Creating a Drive</span></span>

<span data-ttu-id="588fa-135">Ahhoz, hogy a meghajtó létrehozása a Windows PowerShell-modul, a meghajtó a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) metódust.</span><span class="sxs-lookup"><span data-stu-id="588fa-135">To allow the Windows PowerShell runtime to create a drive, the drive provider must implement the [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) method.</span></span> <span data-ttu-id="588fa-136">Az alábbi kód megvalósítását mutatja be a [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) a meghajtószolgáltató módszer:</span><span class="sxs-lookup"><span data-stu-id="588fa-136">The following code shows the implementation of the [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) method for this drive provider:</span></span>

[!code-csharp[AccessDBProviderSample02.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample02/AccessDBProviderSample02.cs#L42-L84 "AccessDBProviderSample02.cs")]

<span data-ttu-id="588fa-137">A felülbírálási ennek a módszernek a következőket kell tennie:</span><span class="sxs-lookup"><span data-stu-id="588fa-137">Your override of this method should do the following:</span></span>

- <span data-ttu-id="588fa-138">Ellenőrizze, hogy a [System.Management.Automation.PSDriveinfo.Root\*](/dotnet/api/System.Management.Automation.PSDriveInfo.Root) tag létezik, és az adattár egy kapcsolat lehet tenni.</span><span class="sxs-lookup"><span data-stu-id="588fa-138">Verify that the [System.Management.Automation.PSDriveinfo.Root\*](/dotnet/api/System.Management.Automation.PSDriveInfo.Root) member exists and that a connection to the data store can be made.</span></span>

- <span data-ttu-id="588fa-139">Meghajtó létrehozása, és töltse fel a kapcsolatot tag támogatja, a `New-PSDrive` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="588fa-139">Create a drive and populate the connection member, in support of the `New-PSDrive` cmdlet.</span></span>

- <span data-ttu-id="588fa-140">Ellenőrizze a [System.Management.Automation.PSDriveinfo](/dotnet/api/System.Management.Automation.PSDriveInfo) objektum a javasolt meghajtó.</span><span class="sxs-lookup"><span data-stu-id="588fa-140">Validate the [System.Management.Automation.PSDriveinfo](/dotnet/api/System.Management.Automation.PSDriveInfo) object for the proposed drive.</span></span>

- <span data-ttu-id="588fa-141">Módosítsa a [System.Management.Automation.PSDriveinfo](/dotnet/api/System.Management.Automation.PSDriveInfo) objektum, amely leírja, hogy a meghajtó bármely szükséges teljesítmény és megbízhatóság információt, vagy adjon meg további adatokat a hívók használja a meghajtót.</span><span class="sxs-lookup"><span data-stu-id="588fa-141">Modify the [System.Management.Automation.PSDriveinfo](/dotnet/api/System.Management.Automation.PSDriveInfo) object that describes the drive with any required performance or reliability information, or provide extra data for callers using the drive.</span></span>

- <span data-ttu-id="588fa-142">Hibák kezeléséhez a [System.Management.Automation.Provider.Cmdletprovider.WriteError](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteError) metódust, és ezután lépjen vissza `null`.</span><span class="sxs-lookup"><span data-stu-id="588fa-142">Handle failures using the [System.Management.Automation.Provider.Cmdletprovider.WriteError](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteError) method and then return `null`.</span></span>

  <span data-ttu-id="588fa-143">Ez a módszer vagy a meghajtó információi átadott, a metódus vagy egy szolgáltatóhoz tartozó verzióját, adja vissza.</span><span class="sxs-lookup"><span data-stu-id="588fa-143">This method returns either the drive information that was passed to the method or a provider-specific version of it.</span></span>

## <a name="attaching-dynamic-parameters-to-newdrive"></a><span data-ttu-id="588fa-144">Dinamikus paraméterek NewDrive csatolása</span><span class="sxs-lookup"><span data-stu-id="588fa-144">Attaching Dynamic Parameters to NewDrive</span></span>

<span data-ttu-id="588fa-145">A `New-PSDrive` parancsmag támogatja a meghajtószolgáltató szükség lehet további paramétereket.</span><span class="sxs-lookup"><span data-stu-id="588fa-145">The `New-PSDrive` cmdlet supported by your drive provider might require additional parameters.</span></span> <span data-ttu-id="588fa-146">Ezek a dinamikus paraméterek csatlakoztatása a parancsmagot, a szolgáltató valósítja meg a [System.Management.Automation.Provider.Drivecmdletprovider.Newdrivedynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDriveDynamicParameters) metódust.</span><span class="sxs-lookup"><span data-stu-id="588fa-146">To attach these dynamic parameters to the cmdlet, the provider implements the [System.Management.Automation.Provider.Drivecmdletprovider.Newdrivedynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDriveDynamicParameters) method.</span></span> <span data-ttu-id="588fa-147">Ez a módszer, amely rendelkezik a tulajdonságokat és mezőket az attribútumok hasonlít egy parancsmag osztály elemzés objektumot adja vissza vagy egy [System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum.</span><span class="sxs-lookup"><span data-stu-id="588fa-147">This method returns an object that has properties and fields with parsing attributes similar to a cmdlet class or a [System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) object.</span></span>

<span data-ttu-id="588fa-148">Ez a meghajtó-szolgáltató nem bírálja felül ezt a módszert.</span><span class="sxs-lookup"><span data-stu-id="588fa-148">This drive provider does not override this method.</span></span> <span data-ttu-id="588fa-149">Az alábbi kód azonban ez a módszer alapértelmezett megvalósítását mutatja be:</span><span class="sxs-lookup"><span data-stu-id="588fa-149">However, the following code shows the default implementation of this method:</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidernewdrivedynamicparameters](Msh_samplestestcmdlets#testprovidernewdrivedynamicparameters)]  -->

## <a name="removing-a-drive"></a><span data-ttu-id="588fa-150">A meghajtó eltávolítása</span><span class="sxs-lookup"><span data-stu-id="588fa-150">Removing a Drive</span></span>

<span data-ttu-id="588fa-151">Gombra kattintva zárja be az adatbázis-kapcsolat, a meghajtó a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Drivecmdletprovider.Removedrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) metódust.</span><span class="sxs-lookup"><span data-stu-id="588fa-151">To close the database connection, the drive provider must implement the [System.Management.Automation.Provider.Drivecmdletprovider.Removedrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) method.</span></span> <span data-ttu-id="588fa-152">Ez a módszer bármely szolgáltatóhoz tartozó információk törlése után a meghajtó a kapcsolat bezárása.</span><span class="sxs-lookup"><span data-stu-id="588fa-152">This method closes the connection to the drive after cleaning up any provider-specific information.</span></span>

<span data-ttu-id="588fa-153">Az alábbi kód megvalósítását mutatja be a [System.Management.Automation.Provider.Drivecmdletprovider.Removedrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) a meghajtószolgáltató módszer:</span><span class="sxs-lookup"><span data-stu-id="588fa-153">The following code shows the implementation of the [System.Management.Automation.Provider.Drivecmdletprovider.Removedrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) method for this drive provider:</span></span>

[!code-csharp[AccessDBProviderSample02.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample02/AccessDBProviderSample02.cs#L91-L116 "AccessDBProviderSample02.cs")]

<span data-ttu-id="588fa-154">Ha a meghajtó is távolítható el, a metódus adja vissza a keresztül a metódusnak átadott adatokat a `drive` paraméter.</span><span class="sxs-lookup"><span data-stu-id="588fa-154">If the drive can be removed, the method should return the information passed to the method through the `drive` parameter.</span></span> <span data-ttu-id="588fa-155">Ha a meghajtó nem távolítható el, a metódus kivételt írási és visszatér `null`.</span><span class="sxs-lookup"><span data-stu-id="588fa-155">If the drive cannot be removed, the method should write an exception and then return `null`.</span></span> <span data-ttu-id="588fa-156">A szolgáltató nem bírálja felül ezt a módszert, ha ez a módszer alapértelmezett megvalósítása, az csak a kapott bemenetként a meghajtó információi adja vissza.</span><span class="sxs-lookup"><span data-stu-id="588fa-156">If your provider does not override this method, the default implementation of this method just returns the drive information passed as input.</span></span>

## <a name="initializing-default-drives"></a><span data-ttu-id="588fa-157">Alapértelmezett inicializálása meghajtók</span><span class="sxs-lookup"><span data-stu-id="588fa-157">Initializing Default Drives</span></span>

<span data-ttu-id="588fa-158">A meghajtó szolgáltató valósítja meg a [System.Management.Automation.Provider.Drivecmdletprovider.Initializedefaultdrives\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.InitializeDefaultDrives) metódus meghajtót csatlakoztatni.</span><span class="sxs-lookup"><span data-stu-id="588fa-158">Your drive provider implements the [System.Management.Automation.Provider.Drivecmdletprovider.Initializedefaultdrives\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.InitializeDefaultDrives) method to mount drives.</span></span> <span data-ttu-id="588fa-159">Az Active Directory-szolgáltató lehet például az alapértelmezett névhasználati környezethez, ha a számítógép egy tartomány tagja a meghajtót csatlakoztatni.</span><span class="sxs-lookup"><span data-stu-id="588fa-159">For example, the Active Directory provider might mount a drive for the default naming context if the computer is joined to a domain.</span></span>

<span data-ttu-id="588fa-160">Ezzel a módszerrel kapcsolatos inicializált meghajtóinformáció gyűjteménye, vagy egy üres gyűjteményt adja vissza.</span><span class="sxs-lookup"><span data-stu-id="588fa-160">This method returns a collection of drive information about the initialized drives, or an empty collection.</span></span> <span data-ttu-id="588fa-161">Ez a metódus meghívása után a Windows PowerShell-modul hívások történik a [System.Management.Automation.Provider.Cmdletprovider.Start\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Start) metódusnak a felülbírásával inicializálhatja a szolgáltató.</span><span class="sxs-lookup"><span data-stu-id="588fa-161">The call to this method is made after the Windows PowerShell runtime calls the [System.Management.Automation.Provider.Cmdletprovider.Start\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Start) method to initialize the provider.</span></span>

<span data-ttu-id="588fa-162">Ez a meghajtó-szolgáltató nem bírálja felül a [System.Management.Automation.Provider.Drivecmdletprovider.Initializedefaultdrives\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.InitializeDefaultDrives) metódust.</span><span class="sxs-lookup"><span data-stu-id="588fa-162">This drive provider does not override the [System.Management.Automation.Provider.Drivecmdletprovider.Initializedefaultdrives\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.InitializeDefaultDrives) method.</span></span> <span data-ttu-id="588fa-163">Azonban a következő kód bemutatja a alapértelmezett implementációja, amely egy meghajtó üres gyűjteményt adja vissza:</span><span class="sxs-lookup"><span data-stu-id="588fa-163">However, the following code shows the default implementation, which returns an empty drive collection:</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testproviderinitializedefaultdrives](Msh_samplestestcmdlets#testproviderinitializedefaultdrives)]  -->

#### <a name="things-to-remember-about-implementing-initializedefaultdrives"></a><span data-ttu-id="588fa-164">Megjegyzendő InitializeDefaultDrives megvalósításával kapcsolatos tudnivalók</span><span class="sxs-lookup"><span data-stu-id="588fa-164">Things to Remember About Implementing InitializeDefaultDrives</span></span>

<span data-ttu-id="588fa-165">Az összes meghajtó-szolgáltatók a felhasználó segítségével a fejlesztőcsapatok legfelső szintű meghajtót kell csatlakoztatni.</span><span class="sxs-lookup"><span data-stu-id="588fa-165">All drive providers should mount a root drive to help the user with discoverability.</span></span> <span data-ttu-id="588fa-166">A meghajtó gyökérkönyvtárára szolgáljanak más csatlakoztatott meghajtók gyökerek helyek előfordulhat, hogy listája.</span><span class="sxs-lookup"><span data-stu-id="588fa-166">The root drive might list locations that serve as roots for other mounted drives.</span></span> <span data-ttu-id="588fa-167">Az Active Directory-szolgáltató előfordulhat, hogy hozzon létre például egy meghajtón található a névhasználati környezet felsoroló a `namingContext` attribútumok a legfelső szintű elosztott rendszer környezet (DSE).</span><span class="sxs-lookup"><span data-stu-id="588fa-167">For example, the Active Directory provider might create a drive that lists the naming contexts found in the `namingContext` attributes on the root Distributed System Environment (DSE).</span></span> <span data-ttu-id="588fa-168">Ez segít a felhasználóknak felderíteni az többi meghajtón csatlakoztatási pontokat.</span><span class="sxs-lookup"><span data-stu-id="588fa-168">This helps users discover mount points for other drives.</span></span>

## <a name="code-sample"></a><span data-ttu-id="588fa-169">Kódminta</span><span class="sxs-lookup"><span data-stu-id="588fa-169">Code Sample</span></span>

<span data-ttu-id="588fa-170">Teljes minta kódja, lásd: [AccessDbProviderSample02 kódminta](./accessdbprovidersample02-code-sample.md).</span><span class="sxs-lookup"><span data-stu-id="588fa-170">For complete sample code, see [AccessDbProviderSample02 Code Sample](./accessdbprovidersample02-code-sample.md).</span></span>

## <a name="testing-the-windows-powershell-drive-provider"></a><span data-ttu-id="588fa-171">A Windows PowerShell meghajtót szolgáltató tesztelése</span><span class="sxs-lookup"><span data-stu-id="588fa-171">Testing the Windows PowerShell Drive Provider</span></span>

<span data-ttu-id="588fa-172">Ha a Windows PowerShell-szolgáltató regisztrálva van a Windows PowerShell-lel, tesztelheti a támogatott parancsmagok futtatásával a parancssorban, beleértve azok a parancsmagok származtatását által elérhetővé tett.</span><span class="sxs-lookup"><span data-stu-id="588fa-172">When your Windows PowerShell provider has been registered with Windows PowerShell, you can test it by running the supported cmdlets on the command line, including any cmdlets made available by derivation.</span></span> <span data-ttu-id="588fa-173">Most tesztelheti a minta meghajtószolgáltató.</span><span class="sxs-lookup"><span data-stu-id="588fa-173">Let's test the sample drive provider.</span></span>

1. <span data-ttu-id="588fa-174">Futtassa a `Get-PSProvider` , győződjön meg arról, hogy megtalálható-e a AccessDB meghajtószolgáltató szolgáltatók listájának beolvasásához:</span><span class="sxs-lookup"><span data-stu-id="588fa-174">Run the `Get-PSProvider` cmdlet to retrieve the list of providers to ensure that the AccessDB drive provider is present:</span></span>

   <span data-ttu-id="588fa-175">**PS> `Get-PSProvider`**</span><span class="sxs-lookup"><span data-stu-id="588fa-175">**PS> `Get-PSProvider`**</span></span>

   <span data-ttu-id="588fa-176">A következő eredmény jelenik meg:</span><span class="sxs-lookup"><span data-stu-id="588fa-176">The following output appears:</span></span>

   ```output
   Name                 Capabilities                  Drives
   ----                 ------------                  ------
   AccessDB             None                          {}
   Alias                ShouldProcess                 {Alias}
   Environment          ShouldProcess                 {Env}
   FileSystem           Filter, ShouldProcess         {C, Z}
   Function             ShouldProcess                 {function}
   Registry             ShouldProcess                 {HKLM, HKCU}
   ```

2. <span data-ttu-id="588fa-177">Győződjön meg arról, hogy egy adatbázis-kiszolgáló neve (DSN) létezik az adatbázis elérésével a **adatforrások** része a **felügyeleti eszközök** az operációs rendszerhez.</span><span class="sxs-lookup"><span data-stu-id="588fa-177">Ensure that a database server name (DSN) exists for the database by accessing the **Data Sources** portion of the **Administrative Tools** for the operating system.</span></span> <span data-ttu-id="588fa-178">Az a **felhasználói DSN** táblát, kattintson duplán a **MS Access-adatbázis** , és adja hozzá a meghajtó elérési útja C:\ps\northwind.mdb.</span><span class="sxs-lookup"><span data-stu-id="588fa-178">In the **User DSN** table, double-click **MS Access Database** and add the drive path C:\ps\northwind.mdb.</span></span>

3. <span data-ttu-id="588fa-179">Hozzon létre egy új meghajtót a minta meghajtószolgáltató használatával:</span><span class="sxs-lookup"><span data-stu-id="588fa-179">Create a new drive using the sample drive provider:</span></span>

   <span data-ttu-id="588fa-180">**PS > új psdrive-név mydb-c:\ps\northwind.mdb - psprovider AccessDb gyökér**</span><span class="sxs-lookup"><span data-stu-id="588fa-180">**PS> new-psdrive -name mydb -root c:\ps\northwind.mdb -psprovider AccessDb**</span></span>

   <span data-ttu-id="588fa-181">A következő eredmény jelenik meg:</span><span class="sxs-lookup"><span data-stu-id="588fa-181">The following output appears:</span></span>

   ```output
   Name     Provider     Root                   CurrentLocation
   ----     --------     ----                   ---------------
   mydb     AccessDB     c:\ps\northwind.mdb
   ```

4. <span data-ttu-id="588fa-182">A kapcsolat ellenőrzéséhez.</span><span class="sxs-lookup"><span data-stu-id="588fa-182">Validate the connection.</span></span> <span data-ttu-id="588fa-183">A kapcsolat definiálva van, amelynek a meghajtót, mert azt a Get-PDDrive parancsmaggal ellenőrizheti.</span><span class="sxs-lookup"><span data-stu-id="588fa-183">Because the connection is defined as a member of the drive, you can check it using the Get-PDDrive cmdlet.</span></span>

   > [!NOTE]
   > <span data-ttu-id="588fa-184">Nem lehet a felhasználó a meghajtó-szolgáltató még használni, a szolgáltatót, hogy a kapcsolati van szüksége a tároló funkciókat.</span><span class="sxs-lookup"><span data-stu-id="588fa-184">The user cannot yet interact with the provider as a drive, as the provider needs container functionality for that interaction.</span></span> <span data-ttu-id="588fa-185">További információkért lásd: [létrehozása a Windows PowerShell-tároló szolgáltató](./creating-a-windows-powershell-container-provider.md).</span><span class="sxs-lookup"><span data-stu-id="588fa-185">For more information, see [Creating a Windows PowerShell Container Provider](./creating-a-windows-powershell-container-provider.md).</span></span>

   <span data-ttu-id="588fa-186">**PS > .connection (get-psdrive mydb)**</span><span class="sxs-lookup"><span data-stu-id="588fa-186">**PS> (get-psdrive mydb).connection**</span></span>

   <span data-ttu-id="588fa-187">A következő eredmény jelenik meg:</span><span class="sxs-lookup"><span data-stu-id="588fa-187">The following output appears:</span></span>

   ```output
   ConnectionString  : Driver={Microsoft Access Driver (*.mdb)};DBQ=c:\ps\northwind.mdb
   ConnectionTimeout : 15
   Database          : c:\ps\northwind
   DataSource        : ACCESS
   ServerVersion     : 04.00.0000
   Driver            : odbcjt32.dll
   State             : Open
   Site              :
   Container         :
   ```

5. <span data-ttu-id="588fa-188">Távolítsa el a meghajtót, és kilépés a rendszerhéjból:</span><span class="sxs-lookup"><span data-stu-id="588fa-188">Remove the drive and exit the shell:</span></span>

   <span data-ttu-id="588fa-189">**PS > remove-psdrive mydb**</span><span class="sxs-lookup"><span data-stu-id="588fa-189">**PS> remove-psdrive mydb**</span></span>

   <span data-ttu-id="588fa-190">**PS > Kilépés**</span><span class="sxs-lookup"><span data-stu-id="588fa-190">**PS> exit**</span></span>

## <a name="see-also"></a><span data-ttu-id="588fa-191">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="588fa-191">See Also</span></span>

[<span data-ttu-id="588fa-192">Windows PowerShell-szolgáltató létrehozása</span><span class="sxs-lookup"><span data-stu-id="588fa-192">Creating Windows PowerShell Providers</span></span>](./how-to-create-a-windows-powershell-provider.md)

[<span data-ttu-id="588fa-193">A Windows PowerShell-szolgáltató tervezése</span><span class="sxs-lookup"><span data-stu-id="588fa-193">Design Your Windows PowerShell Provider</span></span>](./designing-your-windows-powershell-provider.md)

[<span data-ttu-id="588fa-194">Egy alapszintű Windows PowerShell-szolgáltató létrehozása</span><span class="sxs-lookup"><span data-stu-id="588fa-194">Creating a Basic Windows PowerShell Provider</span></span>](./creating-a-basic-windows-powershell-provider.md)