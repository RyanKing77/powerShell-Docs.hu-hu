---
title: Szerzői műveletek esetében egy felügyeleti OData webszolgáltatást soubor schématu XML |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3e83c9d9-6d06-4247-94d9-e3bfd4013b11
caps.latest.revision: 4
ms.openlocfilehash: a806d012097d107b6cc35710b9a93f2b27dd1ace
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848194"
---
# <a name="authoring-the-xml-schema-file-for-a-management-odata-web-service"></a><span data-ttu-id="3fe01-102">Egy Management OData webszolgáltatás XML-sémájának szerkesztése</span><span class="sxs-lookup"><span data-stu-id="3fe01-102">Authoring the XML schema file for a Management OData web service</span></span>

<span data-ttu-id="3fe01-103">Az erőforrások definiálása után a webszolgáltatás megmutatják (lásd: [a MOF-fájl számára egy felügyeleti OData webszolgáltatást szerzői](./authoring-the-mof-schema-file-for-a-management-odata-web-service.md)), leképezheti ezeket az erőforrásokat az alapul szolgáló Windows PowerShell-parancsmagokat, amelyek alkalmazzák a a támogatott Hozzon létre egy XML-fájlt, amely megfelel-e az egyes erőforrások műveletek a [erőforrás-leképezés séma](./resource-mapping-schema.md).</span><span class="sxs-lookup"><span data-stu-id="3fe01-103">After you define the resources your web service will expose (see [Authoring the MOF schema file for a Management OData web service](./authoring-the-mof-schema-file-for-a-management-odata-web-service.md)), you map those resources to the underlying Windows PowerShell cmdlets that implement the supported operations for each resource by creating an XML file that conforms to the [Resource Mapping Schema](./resource-mapping-schema.md).</span></span> <span data-ttu-id="3fe01-104">Az XML-fájlt is megadja az erőforrások eléréséhez az ügyfél által használt URL-címeket.</span><span class="sxs-lookup"><span data-stu-id="3fe01-104">The XML file also specifies the URLs that are used by the client to access the resources.</span></span>

## <a name="mappng-resources-to-urls"></a><span data-ttu-id="3fe01-105">Mappng erőforrások URL-címek</span><span class="sxs-lookup"><span data-stu-id="3fe01-105">Mappng resources to URLs</span></span>

<span data-ttu-id="3fe01-106">Az XML-fájl első része a MOF-fájl a azok eléréséhez használt URL-címekhez meghatározott erőforrásokat használja a képezi le.</span><span class="sxs-lookup"><span data-stu-id="3fe01-106">The first part of the XML file maps the resources defined in the MOF schema file to the URLs that are used to access them.</span></span> <span data-ttu-id="3fe01-107">Az alábbi példa bemutatja a leképezéseket.</span><span class="sxs-lookup"><span data-stu-id="3fe01-107">The following example shows that mapping.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ResourceMetadata xmlns="http://schemas.microsoft.com/powershell-web-services/2010/09">
    <SchemaNamespace>PswsTest</SchemaNamespace>
    <ContainerName>PSWSEntityContainer</ContainerName>
    <Resources>
        <Resource>
            <RelativeUrl>Service</RelativeUrl>
            <Class>PswsTest_Service</Class>
        </Resource>
        <Resource>
            <RelativeUrl>Process</RelativeUrl>
            <Class>PswsTest_Process</Class>
        </Resource>
    </Resources>
```

## <a name="mapping-cmdlets-to-crud-operations"></a><span data-ttu-id="3fe01-108">Parancsmagok leképezése CRUD-műveletek</span><span class="sxs-lookup"><span data-stu-id="3fe01-108">Mapping cmdlets to CRUD operations</span></span>

<span data-ttu-id="3fe01-109">Majd adja meg a parancsmagok, amelyek megfelelnek a CRUD (létrehozása, olvasása, frissítése és törlése) műveletek, amelyek támogatják az erőforrásokat.</span><span class="sxs-lookup"><span data-stu-id="3fe01-109">You then specify the cmdlets that correspond to the CRUD (create, read, update, and delete) operations that the resources support.</span></span> <span data-ttu-id="3fe01-110">Az a felügyeleti OData [erőforrás-leképezés séma](./resource-mapping-schema.md), a CRUD-műveletek a következőképpen vannak leképezve.</span><span class="sxs-lookup"><span data-stu-id="3fe01-110">In the Management OData [Resource Mapping Schema](./resource-mapping-schema.md), the CRUD operations are mapped as follows.</span></span>

|<span data-ttu-id="3fe01-111">CRUD-parancs</span><span class="sxs-lookup"><span data-stu-id="3fe01-111">CRUD command</span></span>|<span data-ttu-id="3fe01-112">XML-elem</span><span class="sxs-lookup"><span data-stu-id="3fe01-112">XML element</span></span>|
|------------------|-----------------|
|<span data-ttu-id="3fe01-113">Létrehozás</span><span class="sxs-lookup"><span data-stu-id="3fe01-113">Create</span></span>|<span data-ttu-id="3fe01-114">Létrehozás</span><span class="sxs-lookup"><span data-stu-id="3fe01-114">Create</span></span>|
|<span data-ttu-id="3fe01-115">Olvasás</span><span class="sxs-lookup"><span data-stu-id="3fe01-115">Read</span></span>|<span data-ttu-id="3fe01-116">Lekérdezés</span><span class="sxs-lookup"><span data-stu-id="3fe01-116">Query</span></span>|
|<span data-ttu-id="3fe01-117">Frissítés</span><span class="sxs-lookup"><span data-stu-id="3fe01-117">Update</span></span>|<span data-ttu-id="3fe01-118">Frissítés</span><span class="sxs-lookup"><span data-stu-id="3fe01-118">Update</span></span>|
|<span data-ttu-id="3fe01-119">Törlés</span><span class="sxs-lookup"><span data-stu-id="3fe01-119">Delete</span></span>|<span data-ttu-id="3fe01-120">Törlés</span><span class="sxs-lookup"><span data-stu-id="3fe01-120">Delete</span></span>|

<span data-ttu-id="3fe01-121">Az alábbi példa mutatja a létrehozás, Olvasás és frissítési műveleteket a leképezéseket a `Service` erőforrás.</span><span class="sxs-lookup"><span data-stu-id="3fe01-121">The following example shows the mappings for the Create, Read, and Update operations on the `Service` resource.</span></span>

```xml
<ClassImplementations>
        <Class>
            <Name>PswsTest_Service</Name>
            <CmdletImplementation>
                <Query>
                    <Cmdlet>Get-Service</Cmdlet>
                        <FieldParameterMap>
                            <Field>
                                <FieldName>ServiceName</FieldName>
                                <ParameterName>Name</ParameterName>
                            </Field>
                        </FieldParameterMap>
                        <ParameterSets>
                            <ParameterSet>
                                <Name>Default</Name>
                                <Parameter><Name>Name</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>ComputerName</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>Include</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>Exclude</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>ErrorVariable</Name></Parameter>
                                <Parameter><Name>WarningVariable</Name></Parameter>
                                <Parameter><Name>OutVariable</Name></Parameter>
                                <Parameter><Name>OutBuffer</Name></Parameter>
                            </ParameterSet>
                            <ParameterSet>
                                <Name>DisplayName</Name>
                                <Parameter><Name>DisplayName</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>ComputerName</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>Include</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>Exclude</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>ErrorVariable</Name></Parameter>
                                <Parameter><Name>WarningVariable</Name></Parameter>
                                <Parameter><Name>OutVariable</Name></Parameter>
                                <Parameter><Name>OutBuffer</Name></Parameter>
                            </ParameterSet>
                            <ParameterSet>
                                <Name>InputObject</Name>
                                <Parameter><Name>ComputerName</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>Include</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>Exclude</Name><Type>System.String[]</Type></Parameter>
                                <Parameter><Name>ErrorVariable</Name></Parameter>
                                <Parameter><Name>WarningVariable</Name></Parameter>
                                <Parameter><Name>OutVariable</Name></Parameter>
                                <Parameter><Name>OutBuffer</Name></Parameter>
                        </ParameterSet>
                    </ParameterSets>
                </Query>
                <Update>
                    <Cmdlet>Set-Service</Cmdlet>
                    <FieldParameterMap>
                        <Field>
                            <FieldName>ServiceName</FieldName>
                            <ParameterName>Name</ParameterName>
                        </Field>
                    </FieldParameterMap>
                    <ParameterSets>
                        <ParameterSet>
                            <Name>Name</Name>
                            <Parameter><Name>ComputerName</Name><Type>System.String[]</Type></Parameter>
                            <Parameter><Name>Name</Name></Parameter>
                            <Parameter><Name>DisplayName</Name></Parameter>
                            <Parameter><Name>Description</Name></Parameter>
                            <Parameter><Name>Status</Name></Parameter>
                            <Parameter><Name>ErrorVariable</Name></Parameter>
                            <Parameter><Name>WarningVariable</Name></Parameter>
                            <Parameter><Name>OutVariable</Name></Parameter>
                            <Parameter><Name>OutBuffer</Name></Parameter>
                        </ParameterSet>
                        <ParameterSet>
                            <Name>InputObject</Name>
                            <Parameter><Name>ComputerName</Name><Type>System.String[]</Type></Parameter>
                            <Parameter><Name>DisplayName</Name></Parameter>
                            <Parameter><Name>Description</Name></Parameter>
                        </ParameterSet>
                    </ParameterSets>
                </Update>
                <Create>
                    <Cmdlet>New-Service</Cmdlet>
                    <FieldParameterMap>
                        <Field>
                            <FieldName>ServiceName</FieldName>
                            <ParameterName>Name</ParameterName>
                        </Field>
                    </FieldParameterMap>
                    <ParameterSets>
                        <ParameterSet>
                            <Name>__AllParameterSets</Name>
                            <Parameter><Name>BinaryPathName</Name></Parameter>
                            <Parameter><Name>Name</Name></Parameter>
                            <Parameter><Name>DisplayName</Name></Parameter>
                            <Parameter><Name>Description</Name></Parameter>
                            <Parameter><Name>DependsOn</Name></Parameter>
                            <Parameter><Name>ErrorVariable</Name></Parameter>
                            <Parameter><Name>WarningVariable</Name></Parameter>
                            <Parameter><Name>OutVariable</Name></Parameter>
                            <Parameter><Name>OutBuffer</Name></Parameter>
                        </ParameterSet>
                    </ParameterSets>
                </Create>
            </CmdletImplementation>
        </Class>
```

## <a name="see-also"></a><span data-ttu-id="3fe01-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="3fe01-122">See Also</span></span>

[<span data-ttu-id="3fe01-123">A MOF-fájl egy felügyeleti OData webszolgáltatást a szerzői műveletek</span><span class="sxs-lookup"><span data-stu-id="3fe01-123">Authoring the MOF schema file for a Management OData web service</span></span>](./authoring-the-mof-schema-file-for-a-management-odata-web-service.md)

[<span data-ttu-id="3fe01-124">Erőforrás a leképezési sémában</span><span class="sxs-lookup"><span data-stu-id="3fe01-124">Resource Mapping Schema</span></span>](./resource-mapping-schema.md)

[<span data-ttu-id="3fe01-125">Felügyeleti OData webes szolgáltatás létrehozása</span><span class="sxs-lookup"><span data-stu-id="3fe01-125">Creating a Management OData Web Service</span></span>](./creating-a-management-odata-web-service.md)