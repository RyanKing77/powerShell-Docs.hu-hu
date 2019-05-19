---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
title: Új és frissített parancsmagok
ms.openlocfilehash: 9ec31c89c0bc4b111b40e2d4725fa0782a573204
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65856244"
---
# <a name="new-and-updated-cmdlets"></a>Új és frissített parancsmagok

A közösségi visszajelzések alapján megjelent új és frissített meglévő parancsmagok hozzáadtuk.

## <a name="archive-cmdlets"></a>Archív parancsmagok

Két új parancsmagot `Compress-Archive` és `Expand-Archive`, hagyjuk, hogy tömöríteni, és bontsa ki a ZIP-fájlokat.

További információkért lásd: a [Microsoft.Powershell.Archive](/powershell/module/microsoft.powershell.archive/) modul dokumentációjában talál.

## <a name="catalog-cmdlets"></a>Katalógusbeli parancsmagok

Két új parancsmag hozzáadva az Microsoft.PowerShell.Security modulban.

- [New-FileCatalog](/powershell/module/microsoft.powershell.security/New-FileCatalog)
- [Test-FileCatalog](/powershell/module/microsoft.powershell.security/Test-FileCatalog)

Ezek létrehozása és ellenőrzése Windows katalógusfájlok.

## <a name="clipboard-cmdlets"></a>Vágólap-parancsmagok

`Get-Clipboard` és `Set-Clipboard` könnyebben, tartalom, és a egy Windows PowerShell-munkamenetből átvitelét. A vágólap-parancsmagok támogatják a lemezképek, a hangfájlok, a fájl listák és a szöveg.

További információ:

- [Get-Clipboard](/powershell/module/Microsoft.PowerShell.Management/Get-Clipboard)
- [Set-Clipboard](/powershell/module/Microsoft.PowerShell.Management/Set-Clipboard)

## <a name="cryptographic-message-syntax-cms-cmdlets"></a>Titkosítási üzenet szintaxis-(CMS-) parancsmagok

A titkosítási üzenet szintaxis parancsmagok támogatják a titkosítási és visszafejtési a IETF szabvány formátum használatával titkosítási szempontból védelme érdekében üzenetet megfelelően tartalom [RFC5652](https://tools.ietf.org/html/rfc5652).

A standard szintű tartalomkezelő rendszer titkosítási valósítja meg a nyilvános kulcsú titkosítás, ahol a kulcsot használja a tartalom titkosításához (a *nyilvános kulcs*) és a kulcs használatával fejti vissza a tartalom (a *titkos kulcs*) jelennek meg.

A nyilvános kulcs széles körben történő megosztásának, és nem érzékeny adatokat. A nyilvános kulccsal titkosított tartalmat a titkos kulccsal csak visszafejteni. További információkért lásd: [nyilvános kulcsú titkosítással](https://en.wikipedia.org/wiki/Public-key_cryptography).

További információk:

- [Get-CmsMessage](/powershell/module/Microsoft.PowerShell.Security/Get-CmsMessage.md)
- [Protect-CmsMessage](/powershell/module/Microsoft.PowerShell.Security/Protect-CmsMessage.md)
- [Unprotect-CmsMessage](/powershell/module/Microsoft.PowerShell.Security/rotect-CmsMessage.md)

Tanúsítványok egyedi kulcshasználat azonosítója (EKU), például a "Kód aláírása" vagy 'Titkosítva Mail', azonosításához azokat az adatokat titkosítási tanúsítványok a PowerShell szükséges. A tanúsítványszolgáltató dokumentum titkosítási tanúsítványok megtekintéséhez használja a **DocumentEncryptionCert** dinamikus paraméterét `Get-ChildItem`:

```powershell
Get-ChildItem Cert:\CurrentUser -DocumentEncryptionCert -Recurse
```

## <a name="extract-and-parse-structured-objects-from-string-content"></a>Strukturált objektumok karakterlánc tartalom kibontása és elemzése

### <a name="convertfrom-string"></a>ConvertFrom-karakterlánc

Az új `ConvertFrom-String` parancsmag két módot támogat:

- Alapszintű tagolt-elemzés
- Automatikusan létrehozott példa adatvezérelt-elemzés

Tagolt elemzés, alapértelmezés szerint bontja a bemenet üres helyet, és a tulajdonságnevek rendel az eredményül kapott csoportok.

A **UpdateTemplate** paraméter menti a tanulási algoritmus eredményeit a sablonfájlt megjegyzést. Ez lehetővé teszi a learning feldolgozásához (a leglassabb fázis) egy egyszeri költség. Futó `ConvertFrom-String` a kódolt tanulási algoritmus tartalmazó sablonnal történő jelenleg szinte azonnali.

További információkért lásd: [ConvertFrom-karakterlánc](/powershell/module/Microsoft.PowerShell.Utility/ConvertFrom-String).

### <a name="convert-string"></a>Convert-String

`Convert-String` lehetővé teszi előtt és után keresse meg a szöveg kívánt példái. A parancsmag automatikusan formázza a szöveget.

További információkért lásd: [Convert-karakterlánc](/powershell/module/Microsoft.PowerShell.Utility/Convert-String).

## <a name="updates-to-fileinfo-object"></a>A FileInfo objektum frissítései

Fájlverzió-információkat is félrevezető lehet, különösen azokban az esetekben, ahol a fájl javítva lett. A WMF 5.0 ad hozzá új **FileVersionRaw** és **ProductVersionRaw** parancsfájl-tulajdonságok **FileInfo** objektumokat.
A powershell.exe (feltéve, hogy $pid a PowerShell-folyamat azonosítója) jelenik meg az alábbiakban a tulajdonságai:

```powershell
Get-Process -Id $pid -FileVersionInfo | Format-List *version*
```

```Output
FileVersionRaw    : 10.0.17763.1
ProductVersionRaw : 10.0.17763.1
FileVersion       : 10.0.17763.1 (WinBuild.160101.0800)
ProductVersion    : 10.0.17763.1
```

## <a name="format-hex"></a>Format-Hex

`Format-Hex` lehetővé teszi hexadecimális formátumú szöveg vagy bináris adatok megtekintését.

További információkért lásd: [hexadecimális formátumban](/powershell/module/microsoft.powershell.utility/format-hex).

## <a name="get-childitem-has--depth-parameter"></a>Get-ChildItem rendelkezik - Depth paraméterrel

`Get-ChildItem` most már rendelkezik egy **mélysége** paraméter való használatra **Recurse** a rekurzió korlátozása:

## <a name="modules-support-for-declaring-version-ranges-1-etc"></a>Modultámogatás a deklaráló verzió tartományok (1.* stb.)

Most már kombinálhatja **MinimumVersion** és **MaximumVersion** adott tartományon belüli modul importálásához. A paraméterek is támogatja a helyettesítő karaktereket.

```powershell
Import-Module psreadline -Verbose -MinimumVersion 1.0 -MaximumVersion 1.2.*
```

```Output
VERBOSE: Loading module from path 'C:\Program Files\WindowsPowerShell\Modules\psreadline\1.1\psreadline.psd1'.
VERBOSE: Importing cmdlet 'Get-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Get-PSReadlineOption'.
VERBOSE: Importing cmdlet 'Remove-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Set-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Set-PSReadlineOption'.
VERBOSE: Importing function 'PSConsoleHostReadline'.
```

## <a name="new-guid"></a>New-Guid

Számos olyan ahol youneed az egyedi azonosítója. A `New-GUID` parancsmaggal hozhat létre egy új GUID-ja egyszerű módszert kínál.

```powershell
New-Guid
```

```Output
Guid
----
e19d6ea5-3cc2-4db9-8095-0cdaed5a703d
```

## <a name="nonewline-parameter"></a>NoNewLine paraméter

`Out-File`, `Add-Content`, és `Set-Content` most már rendelkezik egy új **NoNewline** kapcsolót, amely egy új sor kihagyása után a kimenet. Például:

```powershell
"This is " | Out-File -FilePath Example.txt -NoNewline
"a single " | Add-Content -Path Example.txt -NoNewline
"sentence." | Add-Content -Path Example.txt -NoNewline
Get-Content .\Example.txt

```Output
This is a single sentence.
```

Nélkül **NoNewline** megadott, minden egyes töredék lenne külön sorban:

```powershell
"This is " | Out-File -FilePath Example.txt
"a single " | Add-Content -Path Example.txt
"sentence." | Add-Content -Path Example.txt
Get-Content .\Example.txt
```

```Output
This is
a single
sentence.
```

## <a name="interact-with-symbolic-links-using-improved-item-cmdlets"></a>Szimbolikus hivatkozások használata az Item-parancsmagokkal továbbfejlesztett kezelése

Az elem, valamint néhány kapcsolódó parancsmaghoz támogatja a szimbolikus hivatkozásokat volna terjeszteni.

### <a name="symbolic-link-files"></a>Szimbolikus hivatkozás fájlok

Ebben a példában létrehozunk egy új szimbolikus hivatkozást fájlt MySymLinkFile.txt $pshome\profile.ps1 hivatkozik, amely C:\Temp mappájában. Mindhárom példában ugyanazt az eredményt hozhat létre.

```powershell
New-Item -ItemType SymbolicLink -Path C:\Temp -Name MySymLinkFile.txt -Value $pshome\profile.ps1
New-Item -ItemType SymbolicLink -Path C:\Temp\MySymLinkFile.txt -Value $pshome\profile.ps1
New-Item -ItemType SymbolicLink -Name C:\Temp\MySymLinkFile.txt -Value $pshome\profile.ps1
```

### <a name="symbolic-link-directories"></a>Szimbolikus hivatkozás könyvtárak

Ebben a példában a $pshome mappára hivatkozik, amely C:\Temp mappájában MySymLinkDir nevű új szimbolikus hivatkozást könyvtárat hozunk létre. Mindhárom példában ugyanazt az eredményt hozhat létre.

```powershell
New-Item -ItemType SymbolicLink -Path C:\Temp -Name MySymLinkDir -Value $pshome
New-Item -ItemType SymbolicLink -Path C:\Temp\MySymLinkDir -Value $pshome
New-Item -ItemType SymbolicLink -Name C:\Temp\MySymLinkDir -Value $pshome
```

### <a name="hard-links"></a>A rögzített hivatkozások

Az azonos kombinációja **elérési** és **neve** engedélyezett a fent leírtak szerint.

```powershell
New-Item -ItemType HardLink -Path C:\Temp -Name MyHardLinkFile.txt -Value $pshome\profile.ps1
```

### <a name="directory-junctions"></a>Directory elhelyezni pontokra

Az azonos kombinációja **elérési** és **neve** engedélyezett a fent leírtak szerint.

```powershell
New-Item -ItemType Junction -Path C:\Temp\MyJunctionDir -Value $pshome
```

### <a name="get-childitem"></a>Get-ChildItem

`Get-ChildItem` most már jeleníti meg az "l" a **mód** tulajdonság, amely jelzi a szimbolikus hivatkozást fájl vagy könyvtár.

```powershell
Get-ChildItem C:\Temp | sort LastWriteTime -Descending

Directory: C:\Temp

Mode       LastWriteTime Length Name
----       ------------- ------ ----
-a---- 6/13/2014 3:00 PM     16 File.txt
d----- 6/13/2014 3:00 PM        Directory
-a---l 6/13/2014 3:21 PM      0 MySymLinkFile.txt
d----l 6/13/2014 3:22 PM        MySymLinkDir
-a---l 6/13/2014 3:23 PM  23304 MyHardLinkFile.txt
d----l 6/13/2014 3:24 PM        MyJunctionDir
```

### <a name="remove-item"></a>Remove-Item

Szimbolikus hivatkozások eltávolítása működik, mint bármely más elemtípus eltávolítása.

```powershell
Remove-Item C:\Temp\MySymLinkFile.txt
Remove-Item C:\Temp\MySymLinkDir
```

Használja a **kényszerített** paraméter segítségével távolítsa el a fájlokat a céloldali könyvtár és a szimbolikus hivatkozást.

```powershell
Remove-Item C:\Temp\MySymLinkDir -Force
```

## <a name="new-temporaryfile"></a>New-TemporaryFile

Egyes esetekben a parancsfájlok kell létrehoznia egy ideiglenes fájlt. Most már teheti ezt meg az `New-TemporaryFile` parancsmagot:

```powershell
$tempFile = New-TemporaryFile
$tempFile.FullName
```

```Output
C:\Users\user1\AppData\Local\Temp\tmp375.tmp
```

## <a name="network-switch-management-with-powershell"></a>Hálózati kapcsolók kezelése a PowerShell-lel

A hálózati kapcsoló, a WMF 5.0-s-ben bevezetett parancsmagjaival kapcsoló, a virtuális LAN (VLAN) és az alapszintű 2. rétegbeli hálózati kapcsoló port konfigurációja alkalmazhat a Windows Server 2012 R2-emblémával hitelesített hálózati kapcsolók. Ezek a parancsmagok használatával hajthatja végre:

- Globális váltson konfigurációs, például:
  - Gazdagép nevének beállítása
  - Set kapcsoló szalagcím
  - Konfigurációs megőrzése
  - Engedélyezi vagy letiltja a szolgáltatás

- VLAN-konfiguráció:
  - Hozzon létre vagy VLAN eltávolítása
  - Engedélyezheti vagy tilthatja le a VLAN
  - VLAN számbavétele
  - Rövid név beállítása egy VLAN-hoz

- 2. rétegbeli port konfigurációja:
  - Portok számbavétele
  - Engedélyezheti vagy tilthatja le a portok
  - Beállított port módok és tulajdonságai
  - Adja hozzá, vagy VLAN-Trönk vagy a hozzáférés a porton társítása

További információkért lásd: a [NetworkSwitchManager](/powershell/module/networkswitchmanager/) dokumentációját.

## <a name="generate-powershell-cmdlets-based-on-an-odata-endpoint-with-odatautils"></a>Az OData-végpont az ODataUtils alapján PowerShell-parancsmagok létrehozása

A ODataUtils modul lehetővé teszi, hogy a PowerShell-parancsmagok a REST-végpontokat, amelyek támogatják az OData generációja. A Microsoft.PowerShell.ODataUtils modul az alábbi szolgáltatásokat tartalmazza:

- Csatorna ügyféloldali, kiszolgálóoldali végpontról további információt.
- Ügyféloldali lapozási támogatása
- Kiszolgálóoldali szűrés használatával a – Select paraméter
- Webalkalmazás-kérelemfejlécek támogatása

A webalkalmazásproxy-parancsmagok által létrehozott a `Export-ODataEndPointProxy` parancsmag a kiszolgálóoldali OData-végpont a kiegészítő információt nyújt a **információk** stream.

```powershell
Import-Module Microsoft.PowerShell.ODataUtils -Force
$generatedProxyModuleDir = Join-Path -Path $env:SystemDrive -ChildPath 'ODataDemoProxy'
$uri = "http://services.odata.org/V3/(S(fhleiief23wrm5a5nhf542q5))/OData/OData.svc/"
Export-ODataEndpointProxy -Uri $uri -OutputModule $generatedProxyModuleDir -Force -AllowUnSecureConnection -Verbose -AllowClobber
```

A következő példában azt termékére beolvasása és a kimenetet a rögzítés a `$infoStream` változó.

Megadásával **IncludeTotalResponseCount** paramétert, a teljes száma az összes lekérjük a **termék** rekordok található a kiszolgálón.

```powershell
Import-Module $generatedProxyModuleDir -Force
$product = Get-Product -Top 1 -AllowUnsecureConnection -AllowAdditionalData -IncludeTotalResponseCount -InformationVariable infoStream
$additionalInfo = $infoStream.GetEnumerator() | % MessageData
$additionalInfo['odata.count']
```

A rekordok a kiszolgálóról az ügyféloldali lapozási támogatási használatával kaphat. Ez akkor hasznos, ha be kell szereznie egy nagy mennyiségű adatot a kiszolgálóról a hálózaton keresztül.

```powershell
$skipCount = 0
$batchSize = 3
while($skipCount -le $additionalInfo['odata.count'])
{
  Get-Product -AllowUnsecureConnection -AllowAdditionalData -Top $batchSize -Skip $skipCount
  $skipCount += $batchSize
}
```

A létrehozott webalkalmazásproxy-parancsmagok támogatják a **kiválasztása** paraméter csak a rekord tulajdonságokat, amelyeket az ügyfélnek kell fogadni egy szűrőt használt. A szűrés történik a kiszolgálón, amely csökkenti a hálózaton keresztül továbbított adatok mennyisége.

```powershell
Get-Product -Top 2 -AllowUnsecureConnection -AllowAdditionalData -Select Name
```

A `Export-ODataEndpointProxy` , valamint az általa létrehozott webalkalmazásproxy-parancsmagok mostantól támogatják a **fejlécek** paraméter. A fejléc a további információt az OData-végpont által várt channel használható.

A következő példában egy előfizetési kulcsot tartalmazó kivonattáblát megadott a **fejlécek** paraméter. Ez a jellemző példa, amely egy előfizetési kulcsot hitelesítéshez sebességhez szolgáltatásokhoz.

```powershell
Export-ODataEndpointProxy -Uri $endPointUri -OutputModule $generatedProxyModuleDir -Force -AllowUnSecureConnection -Verbose -Headers @{'subscription-key'='XXXX'}
```
