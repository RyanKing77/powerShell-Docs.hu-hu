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
# <a name="configuring-role-based-authorization"></a>A szerepköralapú hitelesítés konfigurálása

Ez a témakör bemutatja, hogyan lehet a szerepkör-alapú engedélyezési szabályzatot konfigurálni ahhoz a minta megvalósítása a [Microsoft.Management.Odata.Customauthorization](/dotnet/api/Microsoft.Management.Odata.CustomAuthorization) felület ismertetett [egyéni megvalósítása Felügyeleti OData IIS kiterjesztés engedélyezési](./implementing-custom-authorization-for-a-management-odata-web-service.md).

Ebben a példában a minta felügyeleti OData-alkalmazás által az engedélyezési házirend meghatározásához használt XML-fájlba fogja konfigurálni. Létrehoz két szerepkört, és társítsa ezeket a szerepköröket a munkafolyamatokat tartalmazó eltérő Windows PowerShell-modulok. Az XML-fájlt meghatározó sémát jelenik meg, [szerepkör-alapú engedélyezési konfigurációs séma](./role-based-authorization-configuration-schema.md).

## <a name="modifying-the-rbacconfigurationxml-file"></a>A RBacConfiguration.xml fájl módosítása

Ez a fájl határozza meg a hitelesítési szabályzatot az alkalmazáshoz. Szerepkörök használatával definiáltak `Group` csomópontok. A `Group` a csomópont definiálja a Windows PowerShell-parancsok csoporthoz rendelt felhasználók által futtatható. Felhasználók hozzárendelése csoportokhoz `User` csomópontok.

Ezekben a példákban fel fog venni egy modult a rendszergazda `Group` csomópontot, és a felhasználó hozzáadása az egyes csoportokhoz.

#### <a name="adding-a-module-to-a-group-node"></a>Egy csoport csomópontot ad hozzá egy modul

1. Hozzon létre egy fájlt **RBacConfiguration.xml** egy szövegszerkesztőben. Ez a fájl a webszolgáltatás főalkalmazása könyvtárba menteni. Helyezze be a következő szöveget a fájlban.

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

2. A fájl tartalmaz két `Group` csomópontok. Ezek képviselik a ebben a példában használt két lehetséges szerepkör a `NonAdminGroup` és a `AdminGroup` szerepköröket.

   Közvetlenül a záró után `Cmdlets` az első címke `Group` csomópont, adja hozzá a következő XML-kódot:

   ```xml
   <Modules>
           <Module>C:\Windows\System32\WindowsPowerShell\v1.0\Modules\ServerManager\ServerManager.psd1</Module>
         </Modules>
   ```

#### <a name="adding-a-user-to-a-group-node"></a>Felhasználók hozzáadása egy csoport csomópontot

1. Nyissa meg a **RBacConfiguration.xml** fájlt egy szövegszerkesztőben. Ez a fájl található a következő mappában: C:\\\inetpub\wwwroot\Modata Ha nem változtatta meg a végpont neve a telepítés előtt.

2. Közvetlenül a záró címke után a `Users` csomópont, adja hozzá a következő XML-kódot:

   ```xml
   <User Name="UserName" GroupName="AdminGroup" AuthenticationType="Basic" DomainName="DomainName"/>
   ```

3. Közvetlenül az előző lépésben az XML-fájl hozzáadása után adja hozzá a következő XML-kódot:

   ```xml
   <User Name="UserName" GroupName="NonAdminGroup" AuthenticationType="Basic" DomainName="DomainName"/>
   ```