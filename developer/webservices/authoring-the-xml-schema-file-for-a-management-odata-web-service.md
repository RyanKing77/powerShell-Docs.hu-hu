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
# <a name="authoring-the-xml-schema-file-for-a-management-odata-web-service"></a>Egy Management OData webszolgáltatás XML-sémájának szerkesztése

Az erőforrások definiálása után a webszolgáltatás megmutatják (lásd: [a MOF-fájl számára egy felügyeleti OData webszolgáltatást szerzői](./authoring-the-mof-schema-file-for-a-management-odata-web-service.md)), leképezheti ezeket az erőforrásokat az alapul szolgáló Windows PowerShell-parancsmagokat, amelyek alkalmazzák a a támogatott Hozzon létre egy XML-fájlt, amely megfelel-e az egyes erőforrások műveletek a [erőforrás-leképezés séma](./resource-mapping-schema.md). Az XML-fájlt is megadja az erőforrások eléréséhez az ügyfél által használt URL-címeket.

## <a name="mappng-resources-to-urls"></a>Mappng erőforrások URL-címek

Az XML-fájl első része a MOF-fájl a azok eléréséhez használt URL-címekhez meghatározott erőforrásokat használja a képezi le. Az alábbi példa bemutatja a leképezéseket.

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

## <a name="mapping-cmdlets-to-crud-operations"></a>Parancsmagok leképezése CRUD-műveletek

Majd adja meg a parancsmagok, amelyek megfelelnek a CRUD (létrehozása, olvasása, frissítése és törlése) műveletek, amelyek támogatják az erőforrásokat. Az a felügyeleti OData [erőforrás-leképezés séma](./resource-mapping-schema.md), a CRUD-műveletek a következőképpen vannak leképezve.

|CRUD-parancs|XML-elem|
|------------------|-----------------|
|Létrehozás|Létrehozás|
|Olvasás|Lekérdezés|
|Frissítés|Frissítés|
|Törlés|Törlés|

Az alábbi példa mutatja a létrehozás, Olvasás és frissítési műveleteket a leképezéseket a `Service` erőforrás.

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

## <a name="see-also"></a>Lásd még:

[A MOF-fájl egy felügyeleti OData webszolgáltatást a szerzői műveletek](./authoring-the-mof-schema-file-for-a-management-odata-web-service.md)

[Erőforrás a leképezési sémában](./resource-mapping-schema.md)

[Felügyeleti OData webes szolgáltatás létrehozása](./creating-a-management-odata-web-service.md)