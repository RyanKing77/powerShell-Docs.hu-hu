---
title: Megjegyzés-alapú súgó kulcsszavak |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ab90ec96-77f5-42e3-9c7e-2f4156ec207f
caps.latest.revision: 6
ms.openlocfilehash: dbb6f7c4cbefeaaaec0747511f50192bcf08c20c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851470"
---
# <a name="comment-based-help-keywords"></a>Megjegyzésalapú súgótémakörök – kulcsszavak

Ez a témakör felsorolja, és a kulcsszavak a Megjegyzés-alapú súgó ismerteti.

## <a name="keywords-in-comment-based-help"></a>A Megjegyzés-alapú súgó kulcsszavak

Az alábbiakban érvényes Megjegyzés-alapú súgó kulcsszavakat. Általában szerepelnek együtt rendeltetése a súgótémakörök sorrendben szerepelnek. Ezek a kulcsszavak jelenhetnek meg a Megjegyzés-alapú súgó bármilyen sorrendben, és azok nem kis-és nagybetűket.

Vegye figyelembe, hogy a `.ExternalHelp` kulcsszó elsőbbséget élvez az összes megjegyzés-alapú súgó kulcsszó. Amikor `.ExternalHelp` szerepel, a [Microsoft.Powershell.Commands.Get-Help](/dotnet/api/Microsoft.PowerShell.Commands.Get-Help) parancsmag nem jelennek meg megjegyzés-alapú segítségre van szüksége, akkor is, ha nem találja a súgófájlban, amely megfelel a kulcsszó értékét.

`.Synopsis` A függvény vagy parancsfájl rövid leírását. Ezt a kulcsszót az alábbi témakörök csak egyszer használható.

`.Description` A függvény vagy parancsfájl részletes leírását. Ezt a kulcsszót az alábbi témakörök csak egyszer használható.

`.Parameter` *\<A paraméter-Name >* egy paraméter leírása. Megadhat egy `.Parameter` kulcsszó minden paraméter, a függvény vagy parancsfájl.

A `.Parameter` kulcsszavak jelenhetnek meg a megjegyzésblokkot bármilyen sorrendben, de a sorrend, amelyben a paraméterek megjelennek a `Param` utasítás vagy függvény deklarációjában határozza meg, amelyben a paraméterek megjelennek a Súgó-témakör. Paramétereket lévő Súgó-témakör sorrendjének módosításához a paramétereket a sorrendjének módosítása a `Param` utasítás vagy függvény deklarációjában.

A paraméter leírását úgy, hogy a megjegyzést is megadhat a `Param` utasítás közvetlenül a paraméter-változó neve előtt. Ha mindkettő egy `Param` utasítás Megjegyzés és a egy `.Parameter` kulcsszó, a társított leírása a `.Parameter` kulcsszó használható, és a `Param` utasítás Megjegyzés a rendszer figyelmen kívül hagyja.

`.Example` Egy mintául szolgáló parancs, amely a függvény vagy parancsfájl, követheti kimeneti és a egy leírást. Ismételje meg ezt a kulcsszót valamennyi példa.

`.Inputs` A Microsoft .NET-keretrendszer típusú, amely a függvény vagy parancsfájl átadható olyan parancsoknak objektumok. A bemeneti objektum leírását is használható.

`.Outputs` A .NET-keretrendszer típusa az objektumokat, a parancsmag adja vissza. A visszaadott objektumok leírását is használható.

`.Notes` További információ a függvény vagy parancsfájl.

`.Link` Egy kapcsolódó témakör neve. Ismételje meg ezt a kulcsszót minden kapcsolódó témakör. Ez a tartalom a Súgó-témakör kapcsolódó hivatkozások szakaszában jelenik meg.

A `.Link` kulcsszó tartalom tartalmazhat egy egységes erőforrás-azonosító (URI), a azonos Súgó-témakör online verzióját is. Az online verzió használata esetén megnyílik a `Online` Get-Help paraméterében. Az URI "http" vagy "https" kell kezdődnie.

`.Component` A technológia vagy szolgáltatás, amely a függvény vagy parancsfájl használ, vagy, amelyhez kapcsolódik. Ez a tartalom akkor jelenik meg, amikor a Get-Help parancsot tartalmazza a `Component` Get-Help paraméterében.

`.Role` A felhasználói szerepkör a Súgó-témakör. Ez a tartalom akkor jelenik meg, amikor a Get-Help parancsot tartalmazza a `Role` Get-Help paraméterében.

`.Functionality` A tervezett használattól, a függvény. Ez a tartalom akkor jelenik meg, amikor a Get-Help parancsot tartalmazza a `Functionality` Get-Help paraméterében.

`.ForwardHelpTargetName` `<Command-Name>` A megadott parancs tartozó súgó-témakör az átirányítások. Felhasználók átirányíthatja súgótémakör, beleértve egy függvényt, a parancsfájl, a parancsmag vagy a szolgáltató Súgó-témaköröket.

`.ForwardHelpCategory` `<Category>` Megadja az elem a Súgó kategória ForwardHelpTargetName. Érvényes értékek: Alias, a parancsmag, súgófájl, függvény, szolgáltató, általános, – gyakori kérdések, szószedet, ScriptCommand, ExternalScript, szűrő vagy az összes. Használja ezt a kulcsszót azonos nevű parancsok ütközések elkerülése érdekében.

`.RemoteHelpRunspace` `<PSSession-variable>` Itt adhatja meg, amely tartalmazza a Súgó-témakör egy munkamenetet. Adja meg egy változót, amely tartalmaz egy PSSession. Használja ezt a kulcsszót a `Export-PSSession` parancsmag a súgótémakörök megkereséséhez az exportált parancsokhoz.

`.ExternalHelp` `<XML Help File>` Adja meg az elérési út és/vagy XML-alapú súgófájlban a parancsfájlt vagy függvény neve.

A `.ExternalHelp` kulcsszó arra utasítja a [Microsoft.Powershell.Commands.Get-Help](/dotnet/api/Microsoft.PowerShell.Commands.Get-Help) parancsmag súgójának a parancsfájlokban vagy függvényekhez egy XML-alapú-fájlban. A **. ExternalHelp** kulcsszó használata szükséges, amikor egy XML-alapú súgó fájlt használ a parancsfájlokban vagy függvényekhez. Ennek hiányában `Get-Help` nem találja a súgófájlt a függvény vagy parancsfájl.

A `.ExternalHelp` kulcsszó elsőbbséget élvez az összes megjegyzés-alapú súgó kulcsszó. Amikor `.ExternalHelp` szerepel, a [Microsoft.Powershell.Commands.Get-Help](/dotnet/api/Microsoft.PowerShell.Commands.Get-Help) parancsmag nem jelennek meg megjegyzés-alapú segítségre van szüksége, akkor is, ha nem találja a súgófájlban, amely megfelel a kulcsszó értékét.

Ha a funkció exportálja egy szkriptmodulba értékét `.ExternalHelp` elérési út nélküli fájl-névnek kell lennie. `Get-Help` úgy tűnik, a modul a területibeállítás-specifikus alkönyvtára a fájlt. Nem vonatkoznak követelmények a fájlnévhez tartozó fájlszűrőkben, de az ajánlott eljárás, hogy használja a következő fájl nevének formátuma: `<ScriptModule>.psm1-help.xml`.

Ha a függvény nem egy modul társítva, tartalmaznia kell egy elérési út és fájlnév nevet az értékét a **. ExternalHelp** kulcsszót. Az XML-fájl megadott elérési útján felhasználói felületi kulturális környezet-specifikus alkönyvtárakat, ha `Get-Help` egy XML-fájl nevét a parancsfájl vagy a függvény megfelelően a nyelv tartalék szabványok számára hoztak létre a alkönyvtárak rekurzív módon keres Windows, ahogyan azt hajtja végre az XML-alapú súgó-témaköröket minden.

A parancsmag súgójában XML-alapú súgó fájlformátumot kapcsolatos további információkért lásd: [írása Windows PowerShell parancsmag segítségével](./writing-help-for-windows-powershell-cmdlets.md).