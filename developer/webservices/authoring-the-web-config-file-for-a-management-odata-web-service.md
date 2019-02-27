---
title: Egy felügyeleti OData web service Web.config fájljának szerzői |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d569f5d5-9746-40c0-be5e-f218bc4560f7
caps.latest.revision: 4
ms.openlocfilehash: f52953ee091f05df5f355719ecba788d3d5ee055
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847312"
---
# <a name="authoring-the-webconfig-file-for-a-management-odata-web-service"></a>Egy Management OData webszolgáltatás Web.config-fájljának szerkesztése

Mielőtt központilag telepíthetné a Management OData webszolgáltatást, konfigurálnia kell a web.config fájlban az XML-séma fájlokat és a DLL-fájlok, amelyek alkalmazzák a [Microsoft.Management.Odata.Customauthorization](/dotnet/api/Microsoft.Management.Odata.CustomAuthorization) és [ System.Management.Automation.Remoting.Pssessionconfiguration](/dotnet/api/System.Management.Automation.Remoting.PSSessionConfiguration) felületek.

## <a name="sample-config-file"></a>Minta konfigurációs fájl

Az alábbiakban látható egy példa a web service web.config fájljának néz ki.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
   <configSections>
      <section name="managementOdata" type="Microsoft.Management.Odata.Core.DSConfiguration, Microsoft.Management.OData, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35, processorArchitecture=MSIL" />
   </configSections>
   <managementOdata schemaFileName="Schema.mof" resourceMappingFileName="Schema.xml">
      <customAuthorization type="Microsoft.Samples.Management.OData.RoleBasedPlugins.CustomAuthorization" assembly=".\Microsoft.Samples.Management.OData.RoleBasedPlugins.dll" />
      <powershell>
         <sessionConfiguration type="Microsoft.Samples.Management.OData.RoleBasedPlugins.SessionConfiguration" assembly=".\Microsoft.Samples.Management.OData.RoleBasedPlugins.dll" />
      </powershell>
      <commandInvocation enabled="true" />
      <wcfDataServicesConfig>
      </wcfDataServicesConfig>
   </managementOdata>
   <system.serviceModel>
      <behaviors>
         <serviceBehaviors>
            <behavior>
                  <serviceAuthorization serviceAuthorizationManagerType="Microsoft.Management.Odata.Core.CustomAuthorizationManager, Microsoft.Management.OData, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35" />
            </behavior>
         </serviceBehaviors>
      </behaviors>
      <serviceHostingEnvironment aspNetCompatibilityEnabled="true" />
   </system.serviceModel>
   <system.webServer>
      <security>
         <authentication>
            <anonymousAuthentication enabled="false" />
            <basicAuthentication enabled="true" />
            <windowsAuthentication enabled="false" />
         </authentication>
      </security>
  </system.webServer>
</configuration>

```

## <a name="see-also"></a>Lásd még:

[Egyéni engedélyezési egy felügyeleti OData webszolgáltatást végrehajtása](./implementing-custom-authorization-for-a-management-odata-web-service.md)

[Egy felügyeleti OData webszolgáltatást SessionConfiguration végrehajtása](./implementing-sessionconfiguration-for-a-management-odata-web-service.md)

[A MOF-fájl egy felügyeleti OData webszolgáltatást a szerzői műveletek](./authoring-the-mof-schema-file-for-a-management-odata-web-service.md)

[Szerzői műveletek esetében egy felügyeleti OData webszolgáltatást soubor schématu XML](./authoring-the-xml-schema-file-for-a-management-odata-web-service.md)

[Felügyeleti OData webes szolgáltatás létrehozása](./creating-a-management-odata-web-service.md)