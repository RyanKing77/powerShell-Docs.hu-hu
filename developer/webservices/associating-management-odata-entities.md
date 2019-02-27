---
title: Felügyeleti OData entitások társítása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 947a3add-3593-400d-8144-8b44c8adbe5e
caps.latest.revision: 5
ms.openlocfilehash: 44b718e024eb98ac562edb50076287a31f5edc6b
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850189"
---
# <a name="associating-management-odata-entities"></a>Management OData-entitások társítása

Gyakran hasznos két különböző felügyeleti OData-entitások közötti társítás létrehozása. Például egy felügyeleti OData-szolgáltatás képes entitások kategóriákba vannak rendezve termékek egy gyűjtemény felügyelő rendelkezik, és az entitások definiálása `Product` és `Category`. Ez a két entitás társításával ügyfél információkat szeretne kapni a termékeket egy kategória egy kéréssel a web Service.

A minta bemutatja, hogyan hozhat létre az entitások közötti társításokat letölthető [társítás minta](https://code.msdn.microsoft.com:443/windowsdesktop/Association-sample-0f0fa87e).

## <a name="creating-the-association-in-the-resource-schema-file"></a>A társítás létrehozása az erőforrás-fájl

A következő MOF két entitás határozza meg. Egymás közötti társítás hozunk létre.

```csharp
class Product {

[key] string ProductName;

// other fields ...
};

class Category {

[key] string CategoryName;

string Products[];

// other fields
}
```

A `Category` osztály olyan tulajdonságot, amely egy tömb, amely a kategóriához tartozó a termékek nevét határozza meg.

Két entitás társításához meg kell határoznia egy osztályt, a `Association` az erőforrás séma MOF-fájlt a szolgáltatás-attribútumban. Az osztály meg kell határoznia, hogy a két entitás kapcsolódó, nevű `ends` a társítás. Az alábbi példa bemutatja egy olyan osztály, amely meghatározza a kategória- és termékek entitások közötti társítás definíciója.

```csharp
[Association]
class ProductCategory {
Category ref theCategory;
Product ref theProducts;
}
```

A nyilatkozat az kategória osztályban termékek tulajdonság is meg kell változtatnia. Használja a `AssociationClass` kulcsszó használatával adja meg, hogy a tulajdonság egy társítás end. A tulajdonság is definiálni kell egy külön entitást, nem pedig egy karakterláncokból álló tömbre mutató hivatkozásként. Az ehhez a `ref` kulcsszót. Az alábbi példa bemutatja a tulajdonság meghatározása a társításhoz.

```csharp
class Sample_Category {

[key] string CategoryName;

[AssociationClass("Sample_ProductCategory"),ToEnd("theProducts")]
Sample_Product ref AssociatedProducts[];
};
```

Végezetül be kell állítania a társítás másik végén egy tulajdonsággal való hozzáadásával a `Product` osztály. Ez a hivatkozás vagy egy tömb, vagy egyetlen entitást. Feltételezve, hogy az egyes termékek csak egy kategóriába tartozik, a definíciót a következő lenne.

```csharp
class Sample_Product {

[key] string ProductName;
[AssociationClass("Sample_ProductCategory"),ToEnd("theCategory")]
Sample_Category ref AssociatedCategory;
};
```

A tulajdonságok, amelyek a társítás két vége navigációs tulajdonságok nevezzük.

#### <a name="steps-for-associating-entities-in-the-resource-schema-file"></a>Az erőforrás-fájl entitások társítása lépései

- A társítás osztály használatával definiálhatja a `Association` kulcsszót.

- Adja meg a társítás ends ahhoz, hogy a kapcsolódó entitások tulajdonságainak AssociationClass kulcsszó használatával.

## <a name="creating-the-association-in-the-resource-mapping-xml-file"></a>A társítás létrehozása az erőforrás-leképezés XML-fájl

Nincsenek három különböző esetekben érdemes figyelembe venni, amikor leképezi a társítást az erőforrás-leképezés XML-fájlban.

#### <a name="determining-how-to-associate-entities-in-the-resource-mapping-file"></a>Az erőforrás leképezési fájlban entitások társítása módjának meghatározása

- Ha a navigálási tulajdonság megtalálható az alapul szolgáló. A .NET-keretrendszer típus és a tulajdonságot tartalmaz külső kulcsok nincs közvetlen leképezés nem szükséges.

- Ha a navigálási tulajdonság nem létezik a .NET-keretrendszer típuson alapul, meg kell adnia egy parancsmag, amely lekéri a kulcsokat a társított példányok listáját. Hozzáadásával ehhez egy `Association` elem beágyazva a `CmdletImplementation` elem, az elem, amelyek meghatározzák a `cmdlets` a CRUD parancsok.

  ```xml
  Class Name=" Category">
     <CmdletImplementation>
        <Query> ... </Query>
        <Associations>
           <Field>
              <Name>AssociatedProducts</Name>
              <GetReference>
                 <Cmdlet>Get-ProductsInCategory</Cmdlet>
                 <ParameterForThisObject>Category</ParameterForThisObject>
              </GetReference>
           </Field>
        </Associations>
     </CmdletImplementation>
  </Class>
  ```

- A navigálási tulajdonság létezik, a .NET-keretrendszer típuson alapul, azonban figyelőobjektum-példányok helyett a külső kulcsok tartalmaz, akkor létre kell hoznia egy parancsmag (írásával egy Windows PowerShell funkcióval vagy szkript) a külső kulcsok lekéréséhez. Majd adja meg, hogy a parancsmag a erőforrás leképezési fájlban. Például a kulcsok lekéréséhez a szkript a következő módon jelenik meg.

  ```
  Param(
      [string] $Key
      )

  (get-category $key).AssociatedProducts

  ```

  És az XML-t az erőforrásfájl leképezés a következő módon jelenik meg.

  ```xml
  Class Name=" Category">
     <CmdletImplementation>
        <Query> ... </Query>
        <Associations>
           <Field>
              <Name>AssociatedProducts</Name>
              <GetReference>
                 <Cmdlet>Get-ProductsInCategory.ps1</Cmdlet>
                 <ParameterForThisObject>Category</ParameterForThisObject>
              </GetReference>
           </Field>
        </Associations>
     </CmdletImplementation>
  </Class>
  ```

- Adjon meg egy parancsmag a kapcsolódó entitások lekéréséhez, mellett parancsmagok hivatkozások eltávolítása a gyűjteményből, és adja hozzá is megadhatja. Az alábbi példa azt feltételezi, hogy létezik-e az Add-ProductToCategory és a Remove-ProductFromCategory parancsmagok (akkor is lehet definiálni a parancsfájlokban vagy függvényekhez az előző példában látható módon).

  ```xml
  Class Name="Sample.Category">
     <CmdletImplementation>
        <Query> ... </Query>
        <Associations>
           <Field>
              <Name>AssociatedProducts</Name>
              <GetReference>
  ...
              </GetReference>
        <AddReference>
     <CmdletName>"Add-ProductToCategory"</>
     <ParameterForThisObject>"Product"</>
     <ParameterForReferredObject>"Category"</>
        </AddReference>
        <RemoveReference>
     <CmdletName="Remove-ProductFromCategory"/>
     <ParameterForThisObject >"Product"</>
     <ParameterForReferredObject >"Category"</>
        </RemoveReference>
           </Field>
        </Associations>
     </CmdletImplementation>
  </Class>
  ```

## <a name="querying-associated-entities"></a>Kapcsolódó entitások lekérdezése

Az ügyfél lekérheti az adott lekérdezések létrehozásával egy entitáshoz társított példányok listáját.

#### <a name="constructing-queries-for-associated-entities"></a>Kapcsolódó entitások lekérdezések létrehozása

- Egy ügyfél kérhetnek kategória adatait anélkül, hogy a kapcsolódó termékeket beolvasása. Ha például a következő kérelmet lekérdezi a részleteit az `food` kategória.

  ```
  http://localhost:7000/MODataSvc/sample.svc/Category('food')
  ```

  A a kapcsolódó termékeket, a kategória (de nem a részleteket a kategória, az ügyfél a navigálási tulajdonságot megadja a kérésben.

  ```
  http://localhost:7000/MODataSvc/sample.svc/Category('food')/AssociatedProducts
  ```

- Csak a termékek URL lekéréséhez használja a `$links` minősítő a kérésben.

  ```
  http://localhost:7000/MODataSvc/sample.svc/Category('food')/$links/AssociatedProducts
  ```

- Az ügyfél megkaphassa a kategória részleteit és a kapcsolódó termékeket is használatával a `$expand` minősítője.

  ```
  http://localhost:7000/MODataSvc/sample.svc/Category('food')?$expand=AssociatedProducts
  ```

## <a name="see-also"></a>Lásd még:

[Felügyeleti OData IIS kiterjesztés webszolgáltatás létrehozása](./creating-a-management-odata-web-service.md)