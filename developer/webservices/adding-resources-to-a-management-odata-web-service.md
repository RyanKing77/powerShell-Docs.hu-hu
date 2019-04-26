---
title: Erőforrások hozzáadása egy felügyeleti OData Web Service |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e620bf6d-76be-47b0-a7a8-f43418f30c60
caps.latest.revision: 6
ms.openlocfilehash: b81a32b867795ae51c3f5308c2f82c31ed2747fa
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62080781"
---
# <a name="adding-resources-to-a-management-odata-web-service"></a>Erőforrások hozzáadása egy Management OData webszolgáltatáshoz

Ez a példa bemutatja, hogyan-erőforrás hozzáadása egy meglévő felügyeleti OData web Service a Management OData séma Tervező használatával. A [PswsRoleBasedPlugins](https://code.msdn.microsoft.com:443/windowsdesktop/PswsRoleBasedPlugins-9c79b75a) minta létrehoz egy webszolgáltatás, amely elérhetővé teszi a folyamat és a kiszolgáló erőforrásait. Ebben a példában egy virtuális gép (VM) erőforrás adnak hozzá a web service.

## <a name="prerequisites"></a>Előfeltételek

Ez a témakör feltételezi, hogy letöltötte és telepítette a [PswsRoleBasedPlugins](https://code.msdn.microsoft.com:443/windowsdesktop/PswsRoleBasedPlugins-9c79b75a) leírtak szerint minta [egy Windows PowerShell webszolgáltatás létrehozása](./creating-a-management-odata-web-service.md), illetve, hogy letöltötte és telepítette a [Management OData-séma Designer](https://marketplace.visualstudio.com/items?itemName=jlisc0.ManagementODataSchemaDesigner). Ez a témakör azt is feltételezi, hogy a Hyper-V Windows PowerShell-modul telepítve azon a számítógépen, ahol beállíthatja a felügyeleti Odata-végpont.

## <a name="adding-vm-as-a-resource-to-the-web-service"></a>A Web Service erőforrás-alapú virtuális gép hozzáadása

Az első lépés, hogy a meglévő felügyeleti OData-végpont a séma importálása a séma-Tervező. A következő eljárás azt ismerteti, hogyan valósítható meg.

#### <a name="importing-an-existing-schema-into-the-schema-designer"></a>Egy meglévő sémák importálása a séma-Tervező

1. Nyissa meg a felügyeleti OData-séma Tervező.

2. Az a **fájl** menüjében válassza **fájl** ; **Új** ; **Fájl**. A **új fájl** párbeszédpanel jelenik meg.

3. Kattintson a **Management OData-modellen**, és kattintson a **nyílt**.

4. A fő ablakban kattintson a jobb gombbal, és kattintson a **sémafájl** ; **Importálás**. A **nyílt** párbeszédpanel jelenik meg.

5. Lépjen abba a mappába, ahol beállíthatja a felügyeleti OData webszolgáltatást a [PswsRoleBasedPlugins](https://code.msdn.microsoft.com:443/windowsdesktop/PswsRoleBasedPlugins-9c79b75a) minta. A megadott minta Windows PowerShell-parancsfájl segítségével állítsa be a végpont a parancsfájl módosítása nélkül, ha a mappa a következő **C:\inetpub\wwwroot\Modata**. Válassza ki a Schema.mof, és kattintson a **nyílt**.

   Ezen a ponton a Schema.mof és Schema.xml fájlok megnyitásához egy szövegszerkesztőben, és figyelje meg, hogy tartalmaznak-e a folyamat és a szolgáltatási erőforrások leképezéseit. A Schema.mof fájlja [Distributed Management Task Force](https://www.dmtf.org/) (DTMF) felügyelt objektum (MOF) standard. A schema.xml fájlja egy XML-séma leírt [erőforrás-leképezés séma](./resource-mapping-schema.md).

   Az alábbi eljárás ismerteti, hogyan lehet importálni a Hyper-V parancsmagok a a séma modellre.

#### <a name="importing-cmdlets-into-the-schema"></a>A séma importálása a parancsmagok

1. Kattintson a jobb gombbal egy üres területre a séma-Tervező ablakában, és kattintson a **Import parancsmagok**. A **parancsmag importálása varázsló** párbeszédpanel jelenik meg.

2. Győződjön meg arról, hogy **helyi számítógép** van jelölve, és kattintson a **tovább**.

3. Győződjön meg arról, hogy a Windows PowerShell-modul telepítve van-e kiválasztva, és a legördülő listából válassza ki a Hyper-V. Kattintson a **tovább**. Kattintson a **Tovább** gombra.

4. Az a **parancsmag főnév** listáról válassza ki **VM**. Kattintson a **tovább**

5. Ebben a példában azt csak a Get és Delete parancsok parancsmagokban fog kötődni. Törölje a **létrehozása** és **frissítés** jelölőnégyzeteket, és győződjön meg arról, a **első** és **törlése** jelölőnégyzetek be vannak jelölve. Győződjön meg arról, hogy a `Get-VM` parancsmag van kiválasztva a **első**, és a `Remove-VM` parancsmag van kiválasztva a **törlése**.

6. A virtuális gépeket kezelő parancsmagokat metaadatait nem határoz meg egy kimeneti típus, mert szüksége lesz a adja meg a kimeneti típus a parancsmag futtatásával. Válassza ki **adja meg a kimeneti típus** kattintson **parancsmag futtatásával**. A **parancsmag futtatása** párbeszédpanel jelenik meg. Kattintson a **Run** (Futtatás) parancsra. A **CLR-beli típus** mezőt a rendszer kitölti a `VirtualMachine` típusa. Kattintson a **OK**, majd kattintson a **tovább**.

7. Alapértelmezés szerint minden VirtualMachine objektum tulajdonságainak van jelölve. Minden tulajdonság nem szeretné az adatokat adja vissza, ha az erőforrás kérhet a webszolgáltatás részeként, törölheti. Kattintson a **Tovább** gombra.

8. Ki kell választania legalább egy tulajdonságot kulcsként használni. Válassza ki **neve** a listából, és kattintson a **tovább**.

9. A következő időszakban lehetővé teszi, hogy a felügyeleti OData-erőforrás tulajdonságainak leképezheti az alapul szolgáló parancsmagok tulajdonságait. A varázsló azonos tulajdonságai leképez alapértelmezés szerint. Ha például a `ComputerName` tulajdonság az erőforrás le van képezve a `ComputerName` tulajdonság a parancsmagok.  Ez lehetővé teszi, hogy adja meg a `ComputerName` egy kérés a webszolgáltatást, és a megadott értéket kell átadni a `Get-VM` parancsmag. `Id` és `Name` vannak leképezve, alapértelmezés szerint is.

   10. Kattintson a **tovább**, majd kattintson a **Befejezés**.

       A VM-erőforrás most már a séma-Tervező ablakában jelenik meg. A tulajdonságok és műveletek az erőforrással ellenőrizheti. Ezután a frissített sémafájlok exportálja a webszolgáltatás a virtuális könyvtárba.

#### <a name="exporting-schema-files-from-the-schema-designer"></a>A séma-tervezőből séma fájlok exportálása

1. Kattintson a jobb gombbal egy üres területre a séma-Tervező ablakában, és kattintson a **sémafájl** ; **Exportálása**. A **Mentés másként** párbeszédpanel jelenik meg.

2. Keresse meg az ugyanabban a könyvtárban, ahol a MOF-fájlt importált. A fájl neve megegyezik az eredeti MOF-fájlt (Schema.mof alapértelmezés szerint), és kattintson a **mentése**. Győződjön meg arról, hogy szeretné-e a meglévő fájl felülírásához.

   Bár ez a nem explicit módon meghatározott a **Mentés másként** párbeszédpanelen Ez felváltja a Schema.mof és a Schema.xml fájlokat.

## <a name="next-steps"></a>Következő lépések

Az új VM-erőforrás elérését a Management OData webszolgáltatást, előbb frissíteni kell a hozzáférést a Hyper-V Windows PowerShell-modul leírtak szerint RbacConfiguration.xml fájl [konfigurálása szerepkör-alapú hitelesítést](./configuring-role-based-authorization.md), és indítsa újra a webszolgáltatást is kell.