---
title: Szerepkör-alapú hitelesítést konfigurálása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2933a6ca-fe92-4ba2-97ee-ef0f0d5fdfcf
caps.latest.revision: 8
ms.openlocfilehash: b73284adb4bf228510bf8134aa4c6a10561b7ea2
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849328"
---
# <a name="configuring-role-based-authorization"></a><span data-ttu-id="7ffff-102">A szerepköralapú hitelesítés konfigurálása</span><span class="sxs-lookup"><span data-stu-id="7ffff-102">Configuring Role-based Authorization</span></span>

<span data-ttu-id="7ffff-103">Ez a témakör bemutatja, hogyan lehet a szerepkör-alapú engedélyezési szabályzatot konfigurálni ahhoz a minta megvalósítása a [Microsoft.Management.Odata.Customauthorization](/dotnet/api/Microsoft.Management.Odata.CustomAuthorization) felület ismertetett [egyéni megvalósítása Felügyeleti OData IIS kiterjesztés engedélyezési](./implementing-custom-authorization-for-a-management-odata-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="7ffff-103">This topic demonstrates how to configure the role-based authorization policy for the sample implementation of the [Microsoft.Management.Odata.Customauthorization](/dotnet/api/Microsoft.Management.Odata.CustomAuthorization) interface described in [Implementing Custom Authorization for Management OData IIS Extension](./implementing-custom-authorization-for-a-management-odata-web-service.md).</span></span>

<span data-ttu-id="7ffff-104">Ebben a példában a minta felügyeleti OData-alkalmazás által az engedélyezési házirend meghatározásához használt XML-fájlba fogja konfigurálni.</span><span class="sxs-lookup"><span data-stu-id="7ffff-104">In this example, you will configure an XML file that is used by the sample Management OData application to define the authorization policy.</span></span> <span data-ttu-id="7ffff-105">Létrehoz két szerepkört, és társítsa ezeket a szerepköröket a munkafolyamatokat tartalmazó eltérő Windows PowerShell-modulok.</span><span class="sxs-lookup"><span data-stu-id="7ffff-105">You will create two roles and associate different Windows PowerShell modules that contain workflows with those roles.</span></span> <span data-ttu-id="7ffff-106">Az XML-fájlt meghatározó sémát jelenik meg, [szerepkör-alapú engedélyezési konfigurációs séma](./role-based-authorization-configuration-schema.md).</span><span class="sxs-lookup"><span data-stu-id="7ffff-106">The schema that defines the XML file is listed at [Role-Based Authorization Configuration Schema](./role-based-authorization-configuration-schema.md).</span></span>

## <a name="modifying-the-rbacconfigurationxml-file"></a><span data-ttu-id="7ffff-107">A RBacConfiguration.xml fájl módosítása</span><span class="sxs-lookup"><span data-stu-id="7ffff-107">Modifying the RBacConfiguration.xml File</span></span>

<span data-ttu-id="7ffff-108">Ez a fájl határozza meg a hitelesítési szabályzatot az alkalmazáshoz.</span><span class="sxs-lookup"><span data-stu-id="7ffff-108">This file defines the authorization policy for the application.</span></span> <span data-ttu-id="7ffff-109">Szerepkörök használatával definiáltak `Group` csomópontok.</span><span class="sxs-lookup"><span data-stu-id="7ffff-109">Roles are defined by using `Group` nodes.</span></span> <span data-ttu-id="7ffff-110">A `Group` a csomópont definiálja a Windows PowerShell-parancsok csoporthoz rendelt felhasználók által futtatható.</span><span class="sxs-lookup"><span data-stu-id="7ffff-110">A `Group` node defines the Windows PowerShell commands that users assigned to that group can run.</span></span> <span data-ttu-id="7ffff-111">Felhasználók hozzárendelése csoportokhoz `User` csomópontok.</span><span class="sxs-lookup"><span data-stu-id="7ffff-111">Users are assigned to groups by using `User` nodes.</span></span>

<span data-ttu-id="7ffff-112">Ezekben a példákban fel fog venni egy modult a rendszergazda `Group` csomópontot, és a felhasználó hozzáadása az egyes csoportokhoz.</span><span class="sxs-lookup"><span data-stu-id="7ffff-112">In these examples, you will add a module to the Administrator `Group` node, and add a user to each group.</span></span>

#### <a name="adding-a-module-to-a-group-node"></a><span data-ttu-id="7ffff-113">Egy csoport csomópontot ad hozzá egy modul</span><span class="sxs-lookup"><span data-stu-id="7ffff-113">Adding a Module to a Group Node</span></span>

1. <span data-ttu-id="7ffff-114">Hozzon létre egy fájlt **RBacConfiguration.xml** egy szövegszerkesztőben.</span><span class="sxs-lookup"><span data-stu-id="7ffff-114">Create a file named **RBacConfiguration.xml** in a text editor.</span></span> <span data-ttu-id="7ffff-115">Ez a fájl a webszolgáltatás főalkalmazása könyvtárba menteni.</span><span class="sxs-lookup"><span data-stu-id="7ffff-115">This file should be saved to the main application directory for your web service.</span></span> <span data-ttu-id="7ffff-116">Helyezze be a következő szöveget a fájlban.</span><span class="sxs-lookup"><span data-stu-id="7ffff-116">Insert the following text in the file.</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <RbacConfiguration>
     <Groups>
       <!--Group consists of the following:
         Name:  Name of the group
         UserName (Optional): Windows Identity user name
         Password (Optional): Password of the Windows user name
         DomainName (Optional): Domain for the user. For local machine account either do not include them or give the machine name. Do not give empty string
         MapIncomingUser (Optional): Boolean value indicating whether to execute cmdlet in the context of network client.

         User credentials and MapIncomingUser=true are exclusive.
       -->
       <Group Name="NonAdminGroup" MapIncomingUser="true">
         <Cmdlets>
           <Cmdlet>Get-Service</Cmdlet>
           <Cmdlet>Set-Service</Cmdlet>
           <Cmdlet>Get-Process</Cmdlet>
           <Cmdlet>Get-Item</Cmdlet>
           <Cmdlet>New-Item</Cmdlet>
           <Cmdlet>Get-Command</Cmdlet>
           <Cmdlet>ConvertTo-Xml</Cmdlet>
           <Cmdlet>ConvertTo-Json</Cmdlet>
           <Cmdlet>ConvertFrom-Json</Cmdlet>
         </Cmdlets>
       </Group>
       <Group Name="AdminGroup" MapIncomingUser="true">
         <Cmdlets>
           <Cmdlet>Get-Service</Cmdlet>
           <Cmdlet>Get-Process</Cmdlet>
           <Cmdlet>Get-Item</Cmdlet>
           <Cmdlet>New-Item</Cmdlet>
           <Cmdlet>Get-Command</Cmdlet>
           <Cmdlet>ConvertTo-Xml</Cmdlet>
           <Cmdlet>ConvertTo-Json</Cmdlet>
           <Cmdlet>ConvertFrom-Json</Cmdlet>
         </Cmdlets>
         <Modules>
           <Module>C:\Windows\System32\WindowsPowerShell\v1.0\Modules\ServerManager\ServerManager.psd1</Module>
         </Modules>
       </Group>
     </Groups>
     <Users>
       <!-- User consists of the following :
         Name: Name of the user. If a user is from a cer
         AuthenticationType: Authentication type used.
         DomainName (Optional): Domain for the user
       -->
       <User Name="localNonAdmin" AuthenticationType="Basic" GroupName="NonAdminGroup" />
       <User Name="localAdmin" AuthenticationType="Basic" GroupName="AdminGroup" />
     </Users>
   </RbacConfiguration>
   ```

2. <span data-ttu-id="7ffff-117">A fájl tartalmaz két `Group` csomópontok.</span><span class="sxs-lookup"><span data-stu-id="7ffff-117">The file contains two `Group` nodes.</span></span> <span data-ttu-id="7ffff-118">Ezek képviselik a ebben a példában használt két lehetséges szerepkör a `NonAdminGroup` és a `AdminGroup` szerepköröket.</span><span class="sxs-lookup"><span data-stu-id="7ffff-118">These represent the two roles used in this example, the `NonAdminGroup` and the `AdminGroup` roles.</span></span>

   <span data-ttu-id="7ffff-119">Közvetlenül a záró után `Cmdlets` az első címke `Group` csomópont, adja hozzá a következő XML-kódot:</span><span class="sxs-lookup"><span data-stu-id="7ffff-119">Directly after the closing `Cmdlets` tag in the first `Group` node, add the following XML:</span></span>

   ```xml
   <Modules>
           <Module>C:\Windows\System32\WindowsPowerShell\v1.0\Modules\ServerManager\ServerManager.psd1</Module>
         </Modules>
   ```

#### <a name="adding-a-user-to-a-group-node"></a><span data-ttu-id="7ffff-120">Felhasználók hozzáadása egy csoport csomópontot</span><span class="sxs-lookup"><span data-stu-id="7ffff-120">Adding a User to a Group Node</span></span>

1. <span data-ttu-id="7ffff-121">Nyissa meg a **RBacConfiguration.xml** fájlt egy szövegszerkesztőben.</span><span class="sxs-lookup"><span data-stu-id="7ffff-121">Open the **RBacConfiguration.xml** file in a text editor.</span></span> <span data-ttu-id="7ffff-122">Ez a fájl található a következő mappában: C:\\\inetpub\wwwroot\Modata Ha nem változtatta meg a végpont neve a telepítés előtt.</span><span class="sxs-lookup"><span data-stu-id="7ffff-122">This file is located in the folder C:\\\inetpub\wwwroot\Modata  if you did not change the endpoint name before installation.</span></span>

2. <span data-ttu-id="7ffff-123">Közvetlenül a záró címke után a `Users` csomópont, adja hozzá a következő XML-kódot:</span><span class="sxs-lookup"><span data-stu-id="7ffff-123">Directly after the closing tag in the `Users` node, add the following XML:</span></span>

   ```xml
   <User Name="UserName" GroupName="AdminGroup" AuthenticationType="Basic" DomainName="DomainName"/>
   ```

3. <span data-ttu-id="7ffff-124">Közvetlenül az előző lépésben az XML-fájl hozzáadása után adja hozzá a következő XML-kódot:</span><span class="sxs-lookup"><span data-stu-id="7ffff-124">Directly after the XML added in the previous step, add the following XML:</span></span>

   ```xml
   <User Name="UserName" GroupName="NonAdminGroup" AuthenticationType="Basic" DomainName="DomainName"/>
   ```