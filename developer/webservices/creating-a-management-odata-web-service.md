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
# <a name="creating-a-management-odata-web-service"></a><span data-ttu-id="3ae74-102">Management OData webszolgáltatás létrehozása</span><span class="sxs-lookup"><span data-stu-id="3ae74-102">Creating a Management OData Web Service</span></span>

<span data-ttu-id="3ae74-103">Felügyeleti ODATA IIS kiterjesztés egy olyan infrastruktúra létrehozásához egy ASP.NET webes szolgáltatás végpontot, amely elérhetővé teszi a felügyeleti adatok, a Windows PowerShell-parancsmagok és parancsfájlok, az OData webes szolgáltatás entitásokként keresztül érhetők el.</span><span class="sxs-lookup"><span data-stu-id="3ae74-103">Management ODATA IIS Extension is an infrastructure for creating an ASP.NET web service end point that exposes your management data, accessed through Windows PowerShell cmdlets and scripts, as OData Web service entities.</span></span> <span data-ttu-id="3ae74-104">Amely az OData-kérések feldolgozásáért és átalakítás őket, a Windows PowerShell-hívásnak hajtja végre.</span><span class="sxs-lookup"><span data-stu-id="3ae74-104">It does that by processing OData requests and converting them into a Windows PowerShell invocation.</span></span> <span data-ttu-id="3ae74-105">Termékcsoportjai hozhat létre olyan végpontok, amelyek teszik közzé a felügyeleti adatok adott csoportok létrehozása az infrastruktúra felett.</span><span class="sxs-lookup"><span data-stu-id="3ae74-105">Product teams can build on top of this infrastructure to create endpoints that expose specific sets of management data.</span></span>

<span data-ttu-id="3ae74-106">Töltse le és telepítse a [PswsRoleBasedPlugins](https://code.msdn.microsoft.com:443/windowsdesktop/PswsRoleBasedPlugins-9c79b75a) minta.</span><span class="sxs-lookup"><span data-stu-id="3ae74-106">Download and install the [PswsRoleBasedPlugins](https://code.msdn.microsoft.com:443/windowsdesktop/PswsRoleBasedPlugins-9c79b75a) sample.</span></span> <span data-ttu-id="3ae74-107">Kövesse az utasításokat a webszolgáltatás üzembe helyezéséhez.</span><span class="sxs-lookup"><span data-stu-id="3ae74-107">Follow the instructions to deploy the web service.</span></span> <span data-ttu-id="3ae74-108">A webszolgáltatás tesz elérhetővé a szolgáltatások és -folyamatok keretében létrehozási, olvasási, frissítési és törlési (CRUD) műveleteket.</span><span class="sxs-lookup"><span data-stu-id="3ae74-108">This web service exposes Services and Processes through Create, Read, Update, and Delete (CRUD) operations.</span></span> <span data-ttu-id="3ae74-109">A web Service CRUD-kérelmek hívja meg, hogy a kért műveletek elvégzéséhez Windows PowerShell-parancsokat.</span><span class="sxs-lookup"><span data-stu-id="3ae74-109">CRUD requests made to the web service invoke  Windows PowerShell commands that perform the requested operations.</span></span> <span data-ttu-id="3ae74-110">A CRUD-műveletek és az alapjául szolgáló Windows PowerShell-parancsok közötti megfeleltetés két sémafájlok, schema.mof és schema.xml valósul meg.</span><span class="sxs-lookup"><span data-stu-id="3ae74-110">A mapping between the CRUD operations and the underlying Windows PowerShell commands is implemented by two schema files, schema.mof and schema.xml.</span></span> <span data-ttu-id="3ae74-111">A schema.mof fájlja a [Distributed Management Task Force](https://www.dmtf.org/) (DMTF) által felügyelt objektum (MOF) standard.</span><span class="sxs-lookup"><span data-stu-id="3ae74-111">The schema.mof file uses the [Distributed Management  Task Force](https://www.dmtf.org/) (DMTF) Managed Object (MOF) standard.</span></span> <span data-ttu-id="3ae74-112">A schema.xml fájlja egy XML-séma leírt [erőforrás-leképezés séma](./resource-mapping-schema.md).</span><span class="sxs-lookup"><span data-stu-id="3ae74-112">The schema.xml file uses an XML schema that is described in [Resource Mapping Schema](./resource-mapping-schema.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3ae74-113">Felügyeleti ODATA IIS kiterjesztés a Windows Server 2008 R2 SP1 engedélyezése előtt engedélyeznie kell a következő funkciókat.</span><span class="sxs-lookup"><span data-stu-id="3ae74-113">Before you enabling Management ODATA IIS Extension on Windows Server 2008 R2 SP1, the following features must be enabled.</span></span>
>
> 1.  <span data-ttu-id="3ae74-114">IIS-WebServerRole</span><span class="sxs-lookup"><span data-stu-id="3ae74-114">IIS-WebServerRole</span></span>
> 2.  <span data-ttu-id="3ae74-115">IIS-WebServer</span><span class="sxs-lookup"><span data-stu-id="3ae74-115">IIS-WebServer</span></span>
> 3.  <span data-ttu-id="3ae74-116">IIS-HttpTracing</span><span class="sxs-lookup"><span data-stu-id="3ae74-116">IIS-HttpTracing</span></span>
> 4.  <span data-ttu-id="3ae74-117">IIS-ManagementOData</span><span class="sxs-lookup"><span data-stu-id="3ae74-117">IIS-ManagementOData</span></span>

## <a name="steps-for-creating-a-management-odata-web-service"></a><span data-ttu-id="3ae74-118">Egy felügyeleti OData webszolgáltatást létrehozásának lépései</span><span class="sxs-lookup"><span data-stu-id="3ae74-118">Steps for creating a Management OData web service</span></span>

<span data-ttu-id="3ae74-119">A következő témakörök bemutatják, hogyan hozhat létre és telepíthet egy felügyeleti OData webszolgáltatást.</span><span class="sxs-lookup"><span data-stu-id="3ae74-119">The following topics describe how to create and deploy a Management OData web service.</span></span>

- [<span data-ttu-id="3ae74-120">Erőforrások hozzáadása egy OData webszolgáltatáshoz</span><span class="sxs-lookup"><span data-stu-id="3ae74-120">Adding Resources to a Management OData Web Service</span></span>](./adding-resources-to-a-management-odata-web-service.md)

- [<span data-ttu-id="3ae74-121">Egyéni engedélyezési egy felügyeleti OData webszolgáltatást végrehajtása</span><span class="sxs-lookup"><span data-stu-id="3ae74-121">Implementing Custom Authorization for a Management OData web service</span></span>](./implementing-custom-authorization-for-a-management-odata-web-service.md)

- [<span data-ttu-id="3ae74-122">Egy felügyeleti OData webszolgáltatást SessionConfiguration végrehajtása</span><span class="sxs-lookup"><span data-stu-id="3ae74-122">Implementing SessionConfiguration for a Management OData web service</span></span>](./implementing-sessionconfiguration-for-a-management-odata-web-service.md)

- [<span data-ttu-id="3ae74-123">A MOF-fájl egy felügyeleti OData webszolgáltatást a szerzői műveletek</span><span class="sxs-lookup"><span data-stu-id="3ae74-123">Authoring the MOF schema file for a Management OData web service</span></span>](./authoring-the-mof-schema-file-for-a-management-odata-web-service.md)

- [<span data-ttu-id="3ae74-124">Szerzői műveletek esetében egy felügyeleti OData webszolgáltatást soubor schématu XML</span><span class="sxs-lookup"><span data-stu-id="3ae74-124">Authoring the XML schema file for a Management OData web service</span></span>](./authoring-the-xml-schema-file-for-a-management-odata-web-service.md)

- [<span data-ttu-id="3ae74-125">Egy felügyeleti OData web service Web.config fájljának készítése</span><span class="sxs-lookup"><span data-stu-id="3ae74-125">Authoring the Web.config file for a Management OData web service</span></span>](./authoring-the-web-config-file-for-a-management-odata-web-service.md)

- [<span data-ttu-id="3ae74-126">Egy felügyeleti OData web Service szolgáltatásának telepítése</span><span class="sxs-lookup"><span data-stu-id="3ae74-126">Deploying a Management OData web service</span></span>](./deploying-a-management-odata-web-service.md)

- [<span data-ttu-id="3ae74-127">Felügyeleti OData entitások társítása</span><span class="sxs-lookup"><span data-stu-id="3ae74-127">Associating Management OData Entities</span></span>](./associating-management-odata-entities.md)

## <a name="see-also"></a><span data-ttu-id="3ae74-128">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="3ae74-128">See Also</span></span>

[<span data-ttu-id="3ae74-129">Felügyeleti ODATA IIS kiterjesztés sémafájlok</span><span class="sxs-lookup"><span data-stu-id="3ae74-129">Management ODATA IIS Extension Schema Files</span></span>](./management-odata-iis-extension-schema-files.md)
