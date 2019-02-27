---
title: Felügyeleti OData webes szolgáltatás létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 06b1b050-0bf7-48f5-ba05-43f489d597c0
caps.latest.revision: 10
ms.openlocfilehash: 476fce9fc087b870bad93a9204a820c5a84df99e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847249"
---
# <a name="creating-a-management-odata-web-service"></a>Management OData webszolgáltatás létrehozása

Felügyeleti ODATA IIS kiterjesztés egy olyan infrastruktúra létrehozásához egy ASP.NET webes szolgáltatás végpontot, amely elérhetővé teszi a felügyeleti adatok, a Windows PowerShell-parancsmagok és parancsfájlok, az OData webes szolgáltatás entitásokként keresztül érhetők el. Amely az OData-kérések feldolgozásáért és átalakítás őket, a Windows PowerShell-hívásnak hajtja végre. Termékcsoportjai hozhat létre olyan végpontok, amelyek teszik közzé a felügyeleti adatok adott csoportok létrehozása az infrastruktúra felett.

Töltse le és telepítse a [PswsRoleBasedPlugins](https://code.msdn.microsoft.com:443/windowsdesktop/PswsRoleBasedPlugins-9c79b75a) minta. Kövesse az utasításokat a webszolgáltatás üzembe helyezéséhez. A webszolgáltatás tesz elérhetővé a szolgáltatások és -folyamatok keretében létrehozási, olvasási, frissítési és törlési (CRUD) műveleteket. A web Service CRUD-kérelmek hívja meg, hogy a kért műveletek elvégzéséhez Windows PowerShell-parancsokat. A CRUD-műveletek és az alapjául szolgáló Windows PowerShell-parancsok közötti megfeleltetés két sémafájlok, schema.mof és schema.xml valósul meg. A schema.mof fájlja a [Distributed Management Task Force](https://www.dmtf.org/) (DMTF) által felügyelt objektum (MOF) standard. A schema.xml fájlja egy XML-séma leírt [erőforrás-leképezés séma](./resource-mapping-schema.md).

> [!IMPORTANT]
> Felügyeleti ODATA IIS kiterjesztés a Windows Server 2008 R2 SP1 engedélyezése előtt engedélyeznie kell a következő funkciókat.
>
> 1.  IIS-WebServerRole
> 2.  IIS-WebServer
> 3.  IIS-HttpTracing
> 4.  IIS-ManagementOData

## <a name="steps-for-creating-a-management-odata-web-service"></a>Egy felügyeleti OData webszolgáltatást létrehozásának lépései

A következő témakörök bemutatják, hogyan hozhat létre és telepíthet egy felügyeleti OData webszolgáltatást.

- [Erőforrások hozzáadása egy OData webszolgáltatáshoz](./adding-resources-to-a-management-odata-web-service.md)

- [Egyéni engedélyezési egy felügyeleti OData webszolgáltatást végrehajtása](./implementing-custom-authorization-for-a-management-odata-web-service.md)

- [Egy felügyeleti OData webszolgáltatást SessionConfiguration végrehajtása](./implementing-sessionconfiguration-for-a-management-odata-web-service.md)

- [A MOF-fájl egy felügyeleti OData webszolgáltatást a szerzői műveletek](./authoring-the-mof-schema-file-for-a-management-odata-web-service.md)

- [Szerzői műveletek esetében egy felügyeleti OData webszolgáltatást soubor schématu XML](./authoring-the-xml-schema-file-for-a-management-odata-web-service.md)

- [Egy felügyeleti OData web service Web.config fájljának készítése](./authoring-the-web-config-file-for-a-management-odata-web-service.md)

- [Egy felügyeleti OData web Service szolgáltatásának telepítése](./deploying-a-management-odata-web-service.md)

- [Felügyeleti OData entitások társítása](./associating-management-odata-entities.md)

## <a name="see-also"></a>Lásd még:

[Felügyeleti ODATA IIS kiterjesztés sémafájlok](./management-odata-iis-extension-schema-files.md)
