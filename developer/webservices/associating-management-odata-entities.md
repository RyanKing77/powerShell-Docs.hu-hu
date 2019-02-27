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
# <a name="associating-management-odata-entities"></a><span data-ttu-id="be1c0-102">Management OData-entitások társítása</span><span class="sxs-lookup"><span data-stu-id="be1c0-102">Associating Management OData Entities</span></span>

<span data-ttu-id="be1c0-103">Gyakran hasznos két különböző felügyeleti OData-entitások közötti társítás létrehozása.</span><span class="sxs-lookup"><span data-stu-id="be1c0-103">It is often useful to create an association between two different Management OData entities.</span></span> <span data-ttu-id="be1c0-104">Például egy felügyeleti OData-szolgáltatás képes entitások kategóriákba vannak rendezve termékek egy gyűjtemény felügyelő rendelkezik, és az entitások definiálása `Product` és `Category`.</span><span class="sxs-lookup"><span data-stu-id="be1c0-104">For example, a Management OData service could have entities that manage a catalogue of products that are organized in categories, and define the entities `Product` and `Category`.</span></span> <span data-ttu-id="be1c0-105">Ez a két entitás társításával ügyfél információkat szeretne kapni a termékeket egy kategória egy kéréssel a web Service.</span><span class="sxs-lookup"><span data-stu-id="be1c0-105">By associating these two entities, a client can get information about all of the products in a category with a single request to the web service.</span></span>

<span data-ttu-id="be1c0-106">A minta bemutatja, hogyan hozhat létre az entitások közötti társításokat letölthető [társítás minta](https://code.msdn.microsoft.com:443/windowsdesktop/Association-sample-0f0fa87e).</span><span class="sxs-lookup"><span data-stu-id="be1c0-106">A sample that shows how to create associations between entities can be downloaded at [Association sample](https://code.msdn.microsoft.com:443/windowsdesktop/Association-sample-0f0fa87e).</span></span>

## <a name="creating-the-association-in-the-resource-schema-file"></a><span data-ttu-id="be1c0-107">A társítás létrehozása az erőforrás-fájl</span><span class="sxs-lookup"><span data-stu-id="be1c0-107">Creating the Association in the resource schema file</span></span>

<span data-ttu-id="be1c0-108">A következő MOF két entitás határozza meg.</span><span class="sxs-lookup"><span data-stu-id="be1c0-108">The following MOF defines two entities.</span></span> <span data-ttu-id="be1c0-109">Egymás közötti társítás hozunk létre.</span><span class="sxs-lookup"><span data-stu-id="be1c0-109">We will create an association between them.</span></span>

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

<span data-ttu-id="be1c0-110">A `Category` osztály olyan tulajdonságot, amely egy tömb, amely a kategóriához tartozó a termékek nevét határozza meg.</span><span class="sxs-lookup"><span data-stu-id="be1c0-110">The `Category` class defines a property that is an array of the names of the products that belong to that category.</span></span>

<span data-ttu-id="be1c0-111">Két entitás társításához meg kell határoznia egy osztályt, a `Association` az erőforrás séma MOF-fájlt a szolgáltatás-attribútumban.</span><span class="sxs-lookup"><span data-stu-id="be1c0-111">To associate two entities, you must define a class with the `Association` attribute in the resource schema MOF file for the service.</span></span> <span data-ttu-id="be1c0-112">Az osztály meg kell határoznia, hogy a két entitás kapcsolódó, nevű `ends` a társítás.</span><span class="sxs-lookup"><span data-stu-id="be1c0-112">The class must define the two entities to be associated, called `ends` of the association.</span></span> <span data-ttu-id="be1c0-113">Az alábbi példa bemutatja egy olyan osztály, amely meghatározza a kategória- és termékek entitások közötti társítás definíciója.</span><span class="sxs-lookup"><span data-stu-id="be1c0-113">The following example shows a definition of a class that defines an association between the Category and Products entities.</span></span>

```csharp
[Association]
class ProductCategory {
Category ref theCategory;
Product ref theProducts;
}
```

<span data-ttu-id="be1c0-114">A nyilatkozat az kategória osztályban termékek tulajdonság is meg kell változtatnia.</span><span class="sxs-lookup"><span data-stu-id="be1c0-114">You must also change the declaration of the Products property in the Category class.</span></span> <span data-ttu-id="be1c0-115">Használja a `AssociationClass` kulcsszó használatával adja meg, hogy a tulajdonság egy társítás end.</span><span class="sxs-lookup"><span data-stu-id="be1c0-115">You use the `AssociationClass` keyword to specify that the property is one end of the association.</span></span> <span data-ttu-id="be1c0-116">A tulajdonság is definiálni kell egy külön entitást, nem pedig egy karakterláncokból álló tömbre mutató hivatkozásként.</span><span class="sxs-lookup"><span data-stu-id="be1c0-116">The property must also be defined as a reference to a separate entity, rather than an array of strings.</span></span> <span data-ttu-id="be1c0-117">Az ehhez a `ref` kulcsszót.</span><span class="sxs-lookup"><span data-stu-id="be1c0-117">You do this by using the `ref` keyword.</span></span> <span data-ttu-id="be1c0-118">Az alábbi példa bemutatja a tulajdonság meghatározása a társításhoz.</span><span class="sxs-lookup"><span data-stu-id="be1c0-118">The following example shows the property definition for the association.</span></span>

```csharp
class Sample_Category {

[key] string CategoryName;

[AssociationClass("Sample_ProductCategory"),ToEnd("theProducts")]
Sample_Product ref AssociatedProducts[];
};
```

<span data-ttu-id="be1c0-119">Végezetül be kell állítania a társítás másik végén egy tulajdonsággal való hozzáadásával a `Product` osztály.</span><span class="sxs-lookup"><span data-stu-id="be1c0-119">Finally, you must declare the other end of the association by adding a property definition to the `Product` class.</span></span> <span data-ttu-id="be1c0-120">Ez a hivatkozás vagy egy tömb, vagy egyetlen entitást.</span><span class="sxs-lookup"><span data-stu-id="be1c0-120">This is a reference to either an array or to a single entity.</span></span> <span data-ttu-id="be1c0-121">Feltételezve, hogy az egyes termékek csak egy kategóriába tartozik, a definíciót a következő lenne.</span><span class="sxs-lookup"><span data-stu-id="be1c0-121">Assuming that each product belongs to only one category, the definition would be as follows.</span></span>

```csharp
class Sample_Product {

[key] string ProductName;
[AssociationClass("Sample_ProductCategory"),ToEnd("theCategory")]
Sample_Category ref AssociatedCategory;
};
```

<span data-ttu-id="be1c0-122">A tulajdonságok, amelyek a társítás két vége navigációs tulajdonságok nevezzük.</span><span class="sxs-lookup"><span data-stu-id="be1c0-122">The properties that represent the two ends of the association are called navigation properties.</span></span>

#### <a name="steps-for-associating-entities-in-the-resource-schema-file"></a><span data-ttu-id="be1c0-123">Az erőforrás-fájl entitások társítása lépései</span><span class="sxs-lookup"><span data-stu-id="be1c0-123">Steps for associating entities in the resource schema file</span></span>

- <span data-ttu-id="be1c0-124">A társítás osztály használatával definiálhatja a `Association` kulcsszót.</span><span class="sxs-lookup"><span data-stu-id="be1c0-124">Define the association as a class by using the `Association` keyword.</span></span>

- <span data-ttu-id="be1c0-125">Adja meg a társítás ends ahhoz, hogy a kapcsolódó entitások tulajdonságainak AssociationClass kulcsszó használatával.</span><span class="sxs-lookup"><span data-stu-id="be1c0-125">Define the ends of the association by using the AssociationClass keyword to qualify properties of the associated entities.</span></span>

## <a name="creating-the-association-in-the-resource-mapping-xml-file"></a><span data-ttu-id="be1c0-126">A társítás létrehozása az erőforrás-leképezés XML-fájl</span><span class="sxs-lookup"><span data-stu-id="be1c0-126">Creating the association in the resource mapping XML file</span></span>

<span data-ttu-id="be1c0-127">Nincsenek három különböző esetekben érdemes figyelembe venni, amikor leképezi a társítást az erőforrás-leképezés XML-fájlban.</span><span class="sxs-lookup"><span data-stu-id="be1c0-127">There are three different cases to consider when mapping an association in the resource mapping XML file.</span></span>

#### <a name="determining-how-to-associate-entities-in-the-resource-mapping-file"></a><span data-ttu-id="be1c0-128">Az erőforrás leképezési fájlban entitások társítása módjának meghatározása</span><span class="sxs-lookup"><span data-stu-id="be1c0-128">Determining how to associate entities in the resource mapping file</span></span>

- <span data-ttu-id="be1c0-129">Ha a navigálási tulajdonság megtalálható az alapul szolgáló.</span><span class="sxs-lookup"><span data-stu-id="be1c0-129">If the navigation property is present in the underlying.</span></span> <span data-ttu-id="be1c0-130">A .NET-keretrendszer típus és a tulajdonságot tartalmaz külső kulcsok nincs közvetlen leképezés nem szükséges.</span><span class="sxs-lookup"><span data-stu-id="be1c0-130">.NET Framework type, and that property contains foreign keys, no explicit mapping is necessary.</span></span>

- <span data-ttu-id="be1c0-131">Ha a navigálási tulajdonság nem létezik a .NET-keretrendszer típuson alapul, meg kell adnia egy parancsmag, amely lekéri a kulcsokat a társított példányok listáját.</span><span class="sxs-lookup"><span data-stu-id="be1c0-131">If the navigation property does not exist in the underlying .NET Framework type, you must specify a cmdlet that retrieves the list of keys of the associated instances.</span></span> <span data-ttu-id="be1c0-132">Hozzáadásával ehhez egy `Association` elem beágyazva a `CmdletImplementation` elem, az elem, amelyek meghatározzák a `cmdlets` a CRUD parancsok.</span><span class="sxs-lookup"><span data-stu-id="be1c0-132">You do this by adding an `Association` element nested under the `CmdletImplementation` element, following the elements that define the `cmdlets` for the other CRUD commands.</span></span>

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

- <span data-ttu-id="be1c0-133">A navigálási tulajdonság létezik, a .NET-keretrendszer típuson alapul, azonban figyelőobjektum-példányok helyett a külső kulcsok tartalmaz, akkor létre kell hoznia egy parancsmag (írásával egy Windows PowerShell funkcióval vagy szkript) a külső kulcsok lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="be1c0-133">If the navigation property does exist in the underlying .NET Framework type, but it contains object instances instead of foreign keys, then you must create a cmdlet (by writing a Windows PowerShell function or script) to retrieve the foreign keys.</span></span> <span data-ttu-id="be1c0-134">Majd adja meg, hogy a parancsmag a erőforrás leképezési fájlban.</span><span class="sxs-lookup"><span data-stu-id="be1c0-134">You then specify that cmdlet in the resource mapping file.</span></span> <span data-ttu-id="be1c0-135">Például a kulcsok lekéréséhez a szkript a következő módon jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="be1c0-135">For example, the script to retrieve the keys would look like the following.</span></span>

  ```
  Param(
      [string] $Key
      )

  (get-category $key).AssociatedProducts

  ```

  <span data-ttu-id="be1c0-136">És az XML-t az erőforrásfájl leképezés a következő módon jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="be1c0-136">And the XML in the resource mapping file would look like the following.</span></span>

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

- <span data-ttu-id="be1c0-137">Adjon meg egy parancsmag a kapcsolódó entitások lekéréséhez, mellett parancsmagok hivatkozások eltávolítása a gyűjteményből, és adja hozzá is megadhatja.</span><span class="sxs-lookup"><span data-stu-id="be1c0-137">In addition to specifying a cmdlet to retrieve the associated entities, you can also specify cmdlets to add and remove references from the collection.</span></span> <span data-ttu-id="be1c0-138">Az alábbi példa azt feltételezi, hogy létezik-e az Add-ProductToCategory és a Remove-ProductFromCategory parancsmagok (akkor is lehet definiálni a parancsfájlokban vagy függvényekhez az előző példában látható módon).</span><span class="sxs-lookup"><span data-stu-id="be1c0-138">The following example assumes that the Add-ProductToCategory and Remove-ProductFromCategory cmdlets exist (they can also be defined in a script or function as in the previous example).</span></span>

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

## <a name="querying-associated-entities"></a><span data-ttu-id="be1c0-139">Kapcsolódó entitások lekérdezése</span><span class="sxs-lookup"><span data-stu-id="be1c0-139">Querying associated entities</span></span>

<span data-ttu-id="be1c0-140">Az ügyfél lekérheti az adott lekérdezések létrehozásával egy entitáshoz társított példányok listáját.</span><span class="sxs-lookup"><span data-stu-id="be1c0-140">The client can retrieve a list of the instances associated with an entity by creating specific queries.</span></span>

#### <a name="constructing-queries-for-associated-entities"></a><span data-ttu-id="be1c0-141">Kapcsolódó entitások lekérdezések létrehozása</span><span class="sxs-lookup"><span data-stu-id="be1c0-141">Constructing queries for associated entities</span></span>

- <span data-ttu-id="be1c0-142">Egy ügyfél kérhetnek kategória adatait anélkül, hogy a kapcsolódó termékeket beolvasása.</span><span class="sxs-lookup"><span data-stu-id="be1c0-142">A client can request the details of a category without retrieving its associated products.</span></span> <span data-ttu-id="be1c0-143">Ha például a következő kérelmet lekérdezi a részleteit az `food` kategória.</span><span class="sxs-lookup"><span data-stu-id="be1c0-143">For example, the following request gets details of the `food` category.</span></span>

  ```
  http://localhost:7000/MODataSvc/sample.svc/Category('food')
  ```

  <span data-ttu-id="be1c0-144">A a kapcsolódó termékeket, a kategória (de nem a részleteket a kategória, az ügyfél a navigálási tulajdonságot megadja a kérésben.</span><span class="sxs-lookup"><span data-stu-id="be1c0-144">To get the associated products of the category (but not details of the category itself, the client specifies the navigation property in the request.</span></span>

  ```
  http://localhost:7000/MODataSvc/sample.svc/Category('food')/AssociatedProducts
  ```

- <span data-ttu-id="be1c0-145">Csak a termékek URL lekéréséhez használja a `$links` minősítő a kérésben.</span><span class="sxs-lookup"><span data-stu-id="be1c0-145">To retrieve only URLs of the products, use the `$links` qualifier in the request.</span></span>

  ```
  http://localhost:7000/MODataSvc/sample.svc/Category('food')/$links/AssociatedProducts
  ```

- <span data-ttu-id="be1c0-146">Az ügyfél megkaphassa a kategória részleteit és a kapcsolódó termékeket is használatával a `$expand` minősítője.</span><span class="sxs-lookup"><span data-stu-id="be1c0-146">The client can get both the category details and its associated products by using the `$expand` qualifier.</span></span>

  ```
  http://localhost:7000/MODataSvc/sample.svc/Category('food')?$expand=AssociatedProducts
  ```

## <a name="see-also"></a><span data-ttu-id="be1c0-147">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="be1c0-147">See Also</span></span>

[<span data-ttu-id="be1c0-148">Felügyeleti OData IIS kiterjesztés webszolgáltatás létrehozása</span><span class="sxs-lookup"><span data-stu-id="be1c0-148">Creating a Management OData IIS Extension Web Service</span></span>](./creating-a-management-odata-web-service.md)