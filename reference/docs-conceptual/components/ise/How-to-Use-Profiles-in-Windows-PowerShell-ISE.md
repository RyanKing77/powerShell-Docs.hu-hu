---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Profilok használata a Windows PowerShell ISE-ben
ms.openlocfilehash: 28354f39aaaa577cec69c1b3f62cfe16ef091218
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030605"
---
# <a name="how-to-use-profiles-in-windows-powershell-ise"></a>Profilok használata a Windows PowerShell ISE-ben

Ez a témakör ismerteti a profilok használata a Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE). Azt javasoljuk, hogy ebben a szakaszban található feladatok végrehajtása, előtt tekintse át [about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles), vagy írja be, a konzol ablaktáblában `Get-Help about_Profiles` nyomja le az ENTER **ENTER**.

A profil a Windows PowerShell ISE parancsfájl, amely akkor fut automatikusan, amikor új munkamenet indításához.  Egy vagy több Windows PowerShell-profilok létrehozása a Windows PowerShell ISE-ben, és ezek segítségével a konfigurálása a Windows PowerShell vagy a Windows PowerShell ISE környezetben hozzáadása használatát, a változók, aliasok, Funkciók, és a szín és betűtípus előkészítése rendelkezésre álló kívánt beállításai. A profil hatással van minden Windows PowerShell ISE-munkamenetet, amely a megkezdése.

> [!NOTE]
> A Windows PowerShell végrehajtási házirend határozza meg, hogy parancsfájlok futtatásához, és egy profil betöltése. Az alapértelmezett végrehajtási házirendet "Tiltott" Megakadályozza, hogy az összes parancsfájl futtatását, beleértve a profilok. Ha a "Tiltott" szabályzatot használja, akkor a profil nem tölthető be. További információ a végrehajtási házirend: [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).

## <a name="selecting-a-profile-to-use-in-the-windows-powershell-ise"></a>A Windows PowerShell ISE-ben használandó profil kiválasztása

Windows PowerShell ISE-ben támogatja a profilok az aktuális felhasználó és minden felhasználó számára. Ezen kívül a Windows PowerShell-profilok, amelyek a alkalmazni a minden gazdagép támogatja.

A profilt, amelyet használhat Windows PowerShell és a Windows PowerShell ISE-ben használatáról határozza meg.

- Ha csak a Windows PowerShell ISE használatával futtassa a Windows Powershellt, majd mentse összes elemet az ISE-specifikus profilok, például a Windows PowerShell ISE- vagy Windows PowerShell ISE AllUsersCurrentHost profil a CurrentUserCurrentHost egyikében.

- Ha több gazdagép program használatával futtassa a Windows Powershellt, a functions, aliasok, változók és parancsok mentse a profilt, amely hatással van az összes gazdagép-programok, például a CurrentUserAllHosts vagy AllUsersAllHosts profilban, és mentse az ISE-specifikus szolgáltatásokat, például a szín- és betűtípus testreszabása a Windows PowerShell ISE-ben vagy a AllUsersCurrentHost profilt CurrentUserCurrentHost profilját a Windows PowerShell ISE-ben.

Az alábbiakban a profilok létrehozott és használt Windows PowerShell ISE-ben. Az egyes profilok menti a saját egyedi elérési útja.

| Profil típusa | Profil elérési útja |
| --- | --- |
| **Aktuális felhasználó, a PowerShell ISE-ben**| `$PROFILE.CurrentUserCurrentHost`, vagy `$PROFILE` |
| **Minden felhasználó, a PowerShell ISE-ben**| `$PROFILE.AllUsersCurrentHost` |
| **Aktuális felhasználó, minden gazdagép**| `$PROFILE.CurrentUserAllHosts` |
| **Minden felhasználó, minden gazdagép** | `$PROFILE.AllUsersAllHosts` |

## <a name="to-create-a-new-profile"></a>Új profil létrehozása

Hozzon létre egy új "aktuális felhasználó Windows PowerShell ISE-ben" a profil, futtassa a következő parancsot:

```powershell
if (!(Test-Path -Path $PROFILE ))
{ New-Item -Type File -Path $PROFILE -Force }
```

Hozzon létre egy új "Minden felhasználó, Windows PowerShell ISE-ben" profil, futtassa a következő parancsot:

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersCurrentHost))
{ New-Item -Type File -Path $PROFILE.AllUsersCurrentHost -Force }
```

Egy új "aktuális felhasználó összes tároló" profil létrehozásához a következő parancs futtatásával:

```powershell
if (!(Test-Path -Path $PROFILE.CurrentUserAllHosts))
{ New-Item -Type File -Path $PROFILE.CurrentUserAllHosts -Force }
```

"Minden felhasználó az összes tároló" új profil létrehozásához, írja be:

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersAllHosts))
{ New-Item -Type File -Path $PROFILE.AllUsersAllHosts -Force }
```

## <a name="to-edit-a-profile"></a>Profil szerkesztése

1. Nyissa meg a profil, futtassa a parancsot psedit a változót, amely meghatározza a szerkeszteni kívánt profilt. Nyissa meg az "aktuális felhasználó, Windows PowerShell ISE-ben" például írja be a profil: `psEdit $PROFILE`

2. A profil kívánt elemeket. Az alábbiakban néhány példa a kezdéshez:

   - A konzol ablaktáblájában, a fájl profiltípust kék alapértelmezett hátterének színét módosítani: `$psISE.Options.OutputPaneBackground = 'blue'` . A $psISE változó kapcsolatos további információkért lásd: [Windows PowerShell ISE objektummodell-hivatkozás](object-model/The-ISE-Object-Model-Hierarchy.md).

   - Betűméret megváltoztatása 20-ra, a profil fájlt be a következőt: `$psISE.Options.FontSize =20`

3. A profil fájlt, a menteni a **fájl** menüben kattintson a **mentése**. A Windows PowerShell ISE-ben következő megnyitásakor a testre szabást érvényesek.

## <a name="see-also"></a>Lásd még:

- [about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles)
- [A Windows PowerShell ISE bemutatása](Introducing-the-Windows-PowerShell-ISE.md)
