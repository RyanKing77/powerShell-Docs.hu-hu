---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 9a9bdac652512640209c20e3deb20d7abc0142c6
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219531"
---
# <a name="register-a-powershell-repository"></a>PowerShell-tárház regisztrálása
Beállíthatja, hogy PowerShellGet belső adattárak ellen. Ehhez használja az alábbi kiegészítésekkel:
- Register-PSRepository: A tárházat az aktuális felhasználó regisztrálja.
- Unregister-PSRepository: Eltávolítja az aktuális felhasználó számára regisztrált tára.
- Set-PSRepository: A regisztrált tárház értékeinek beállításához.
- Get-PSRepository: Az aktuális felhasználó számára regisztrált összes tárházak beolvasása.

A tárház regisztrálása után keresés- és telepítési-modul segítségével használható.

```powershell
\#Register a default repository
Register-PSRepository –Name DemoRepo –SourceLocation “https://www.myget.org/F/powershellgetdemo/api/v2” –PublishLocation “<https://www.myget.org/F/powershellgetdemo/api/v2>/package” –InstallationPolicy –Trusted

\#Get all of the registered repositories
Get-PSRepository
Name SourceLocation
---- --------------
PSGallery https://msconfiggallery.cloudapp...
DemoRepo https://www.myget.org/F/powershe...

\#Search only the new repository for modules
Find-Module -Repository DemoRepo
Repository Version Name
---------- ------- ----
DemoRepo 1.0.1 xActiveDirectory
DemoRepo 1.1.1 SomeModule

\#By default, PowerShellGet operates against all registered repositories when none is specified. In this example, the “SomeModule” module is installed from the DemoRepo.
Install-Module SomeModule

\#Removing a repository
Unregister-PSRepository DemoRepo
```
