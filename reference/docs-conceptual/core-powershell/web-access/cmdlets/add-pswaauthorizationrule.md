---
ms.topic: reference
keywords: PowerShell parancsmag
ms.date: 12/12/2016
title: Add-PswaAuthorizationRule
schema: 2.0.0
ms.openlocfilehash: b8020f8b034ab24d79a96da3908e9b63bf017cd9
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="add-pswaauthorizationrule"></a><span data-ttu-id="b6476-103">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="b6476-103">Add-PswaAuthorizationRule</span></span>

## <a name="synopsis"></a><span data-ttu-id="b6476-104">ÖSSZEGZÉST</span><span class="sxs-lookup"><span data-stu-id="b6476-104">SYNOPSIS</span></span>

<span data-ttu-id="b6476-105">Új engedélyezési szabály hozzáadása a Windows PowerShell® Web Access engedélyezési szabályok készletéhez.</span><span class="sxs-lookup"><span data-stu-id="b6476-105">Adds a new authorization rule to the Windows PowerShell® Web Access authorization rule set.</span></span>

## <a name="syntax"></a><span data-ttu-id="b6476-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="b6476-106">Syntax</span></span>

### <a name="usergroupnamecomputergroupname"></a><span data-ttu-id="b6476-107">UserGroupNameComputerGroupName</span><span class="sxs-lookup"><span data-stu-id="b6476-107">UserGroupNameComputerGroupName</span></span>
```
Add-PswaAuthorizationRule -ComputerGroupName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usergroupnamecomputername"></a><span data-ttu-id="b6476-108">UserGroupNameComputerName</span><span class="sxs-lookup"><span data-stu-id="b6476-108">UserGroupNameComputerName</span></span>
```
Add-PswaAuthorizationRule -ComputerName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputergroupname"></a><span data-ttu-id="b6476-109">UserNameComputerGroupName</span><span class="sxs-lookup"><span data-stu-id="b6476-109">UserNameComputerGroupName</span></span>
```
Add-PswaAuthorizationRule [-UserName] <String[]> -ComputerGroupName <String> -ConfigurationName <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputername"></a><span data-ttu-id="b6476-110">UserNameComputerName</span><span class="sxs-lookup"><span data-stu-id="b6476-110">UserNameComputerName</span></span>
```
Add-PswaAuthorizationRule [-UserName] <String[]> [-ComputerName] <String> [-ConfigurationName] <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="b6476-111">LEÍRÁS</span><span class="sxs-lookup"><span data-stu-id="b6476-111">DESCRIPTION</span></span>

<span data-ttu-id="b6476-112">A **Add-PswaAuthorizationRule** parancsmag új felhatalmazási szabály hozzáadása a Windows PowerShell® Web Access engedélyezési szabályok készletéhez.</span><span class="sxs-lookup"><span data-stu-id="b6476-112">The **Add-PswaAuthorizationRule** cmdlet adds a new authorization rule to the Windows PowerShell® Web Access authorization rule set.</span></span>

<span data-ttu-id="b6476-113">A felhasználók, számítógépek és a szabály a Windows PowerShell végpontokat kell megadnia.</span><span class="sxs-lookup"><span data-stu-id="b6476-113">You must specify the users, computers, and Windows PowerShell endpoints for this rule.</span></span> <span data-ttu-id="b6476-114">Megadhatja a felhasználók és számítógépek egyes felhasználói fiókok és a számítógép nevét, vagy csoportok megadása.</span><span class="sxs-lookup"><span data-stu-id="b6476-114">You can specify both users and computers either by individual user accounts and computer names, or by specifying groups.</span></span>

<span data-ttu-id="b6476-115">Egy számítógép, amely egy Active Directory-tartományhoz csatlakozik a parancsmag a szabály létrehozásához használ a számítógép biztonsági azonosítóját (SID).</span><span class="sxs-lookup"><span data-stu-id="b6476-115">For a computer that is joined to an Active Directory domain, the cmdlet uses the security identifier (SID) of the computer to create the rule.</span></span>
<span data-ttu-id="b6476-116">Ez lehetővé teszi, hogy egy rövid nevet, egy teljesen minősített tartománynevét (FQDN) vagy IP-címet a **számítógépnév** mezőjét a bejelentkezési oldalon.</span><span class="sxs-lookup"><span data-stu-id="b6476-116">This allows you to use a short name, a fully qualified domain name (FQDN), or an IP address for the **Computer Name** field on the sign-in page.</span></span>

<span data-ttu-id="b6476-117">Egy számítógép, amely nem csatlakozik egy Active Directory-tartomány a parancsmag a szabály a számítógép nevét, a rendszergazda által biztosított segítségével hoz létre.</span><span class="sxs-lookup"><span data-stu-id="b6476-117">For a computer that is not joined to an Active Directory domain, the cmdlet creates the rule using the computer name provided by the administrator.</span></span> <span data-ttu-id="b6476-118">Sikeres csatlakozás a számítógéphez, hogy a végfelhasználó biztosítania kell a számítógép neve pontosan, ahogyan az a szabály megjelenik.</span><span class="sxs-lookup"><span data-stu-id="b6476-118">To successfully connect to this machine, the end user must provide the computer name exactly as it appears in the rule.</span></span>

<span data-ttu-id="b6476-119">Ha több számítógépet, ezzel a névvel, a hálózaton, rövid neve egynél több számítógép tudja oldani.</span><span class="sxs-lookup"><span data-stu-id="b6476-119">If there are multiple computers with the same name on the network, then short name can resolve to more than one computer.</span></span> <span data-ttu-id="b6476-120">Ez vezethet kétértelműség egy kapcsolat.</span><span class="sxs-lookup"><span data-stu-id="b6476-120">This can lead to ambiguity when establishing a connection.</span></span> <span data-ttu-id="b6476-121">Például, ha a szabály létezik a munkacsoportban működő számítógép nevű "*kiszolgáló1*" és nevű új számítógép *server1.contoso.com* csatlakozik a hálózathoz, az engedélyezési szabályok segítségével érvényesítés sikeres, és A Windows PowerShell Web Access megkísérli a kapcsolatot a következő nevű számítógépet "*kiszolgáló1*".</span><span class="sxs-lookup"><span data-stu-id="b6476-121">For example, if a rule exists for the workgroup computer named "*Server1*” and a new computer named *server1.contoso.com* is joined to the network, validation using the authorization rules succeeds and Windows PowerShell Web Access attempts to establish a connection to the computer named “*Server1*”.</span></span> <span data-ttu-id="b6476-122">Nem garantált, hogy a kapcsolatot létesíteni a megadott munkacsoportban működő számítógép; a kísérlet sikerült meg a workgroup vagy a nevű számítógépet "*kiszolgáló1*".</span><span class="sxs-lookup"><span data-stu-id="b6476-122">It is not guaranteed that the connection is established with the specified workgroup computer; the attempt could be made on either the workgroup or the domain computer named "*Server1*".</span></span> <span data-ttu-id="b6476-123">Kétértelműség csökkentése érdekében javasoljuk, hogy a célszámítógép, amikor csak lehetséges az engedélyezési szabály létrehozásához használja a teljes Tartománynevet.</span><span class="sxs-lookup"><span data-stu-id="b6476-123">To reduce ambiguity, it is recommended that you use the FQDN for the destination computer whenever possible to create an authorization rule.</span></span>

<span data-ttu-id="b6476-124">Az engedélyezési szabályok kiértékelése elsődleges bejelentkezési hitelesítő adatait a Windows PowerShell Web Access a felhasználók nem a másodlagos hitelesítő (hitelesítő adatok a második készlet megtalálható a **választható csatlakozási beállítások** szakasza a bejelentkezési oldal).</span><span class="sxs-lookup"><span data-stu-id="b6476-124">The authorization rules evaluate the primary sign-in credential of the Windows PowerShell Web Access users, not the alternate credentials (the second set of credentials found in the **Optional connection settings** section of the sign-in page).</span></span> <span data-ttu-id="b6476-125">Példa erre lásd: Példa 6.</span><span class="sxs-lookup"><span data-stu-id="b6476-125">For an example of this, see Example 6.</span></span>

## <a name="parameters"></a><span data-ttu-id="b6476-126">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="b6476-126">Parameters</span></span>

### <a name="-computergroupnameltstringgt"></a><span data-ttu-id="b6476-127">-ComputerGroupName&lt;karakterlánc&gt;</span><span class="sxs-lookup"><span data-stu-id="b6476-127">-ComputerGroupName&lt;String&gt;</span></span>

<span data-ttu-id="b6476-128">Adja meg egy számítógépcsoport nevét, amelyhez ez a szabály engedélyezi a hozzáférést az Active Directory tartományi szolgáltatások (AD DS) vagy helyi csoportot.</span><span class="sxs-lookup"><span data-stu-id="b6476-128">Specifies the name of a computer group in Active Directory Domain Services (AD DS) or local groups to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="b6476-129">Aliasok</span><span class="sxs-lookup"><span data-stu-id="b6476-129">Aliases</span></span>                              | <span data-ttu-id="b6476-130">nincs</span><span class="sxs-lookup"><span data-stu-id="b6476-130">none</span></span>                                 |
| <span data-ttu-id="b6476-131">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="b6476-131">Required?</span></span>                            | <span data-ttu-id="b6476-132">Igaz</span><span class="sxs-lookup"><span data-stu-id="b6476-132">true</span></span>                                 |
| <span data-ttu-id="b6476-133">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="b6476-133">Position?</span></span>                            | <span data-ttu-id="b6476-134">nevű</span><span class="sxs-lookup"><span data-stu-id="b6476-134">named</span></span>                                |
| <span data-ttu-id="b6476-135">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="b6476-135">Default Value</span></span>                        | <span data-ttu-id="b6476-136">nincs</span><span class="sxs-lookup"><span data-stu-id="b6476-136">none</span></span>                                 |
| <span data-ttu-id="b6476-137">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="b6476-137">Accept Pipeline Input?</span></span>               | <span data-ttu-id="b6476-138">Igaz (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b6476-138">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="b6476-139">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="b6476-139">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="b6476-140">hamis</span><span class="sxs-lookup"><span data-stu-id="b6476-140">false</span></span>                                |

### <a name="-computernameltstringgt"></a><span data-ttu-id="b6476-141">-ComputerName&lt;karakterlánc&gt;</span><span class="sxs-lookup"><span data-stu-id="b6476-141">-ComputerName&lt;String&gt;</span></span>

<span data-ttu-id="b6476-142">A számítógép neve, amelyhez ez a szabály engedélyezi a hozzáférést.</span><span class="sxs-lookup"><span data-stu-id="b6476-142">Specifies the computer name to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="b6476-143">Aliasok</span><span class="sxs-lookup"><span data-stu-id="b6476-143">Aliases</span></span>                              | <span data-ttu-id="b6476-144">nincs</span><span class="sxs-lookup"><span data-stu-id="b6476-144">none</span></span>                                 |
| <span data-ttu-id="b6476-145">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="b6476-145">Required?</span></span>                            | <span data-ttu-id="b6476-146">Igaz</span><span class="sxs-lookup"><span data-stu-id="b6476-146">true</span></span>                                 |
| <span data-ttu-id="b6476-147">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="b6476-147">Position?</span></span>                            | <span data-ttu-id="b6476-148">nevű</span><span class="sxs-lookup"><span data-stu-id="b6476-148">named</span></span>                                |
| <span data-ttu-id="b6476-149">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="b6476-149">Default Value</span></span>                        | <span data-ttu-id="b6476-150">nincs</span><span class="sxs-lookup"><span data-stu-id="b6476-150">none</span></span>                                 |
| <span data-ttu-id="b6476-151">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="b6476-151">Accept Pipeline Input?</span></span>               | <span data-ttu-id="b6476-152">Igaz (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b6476-152">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="b6476-153">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="b6476-153">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="b6476-154">hamis</span><span class="sxs-lookup"><span data-stu-id="b6476-154">false</span></span>                                |

### <a name="-configurationnameltstringgt"></a><span data-ttu-id="b6476-155">-ConfigurationName&lt;String&gt;</span><span class="sxs-lookup"><span data-stu-id="b6476-155">-ConfigurationName&lt;String&gt;</span></span>

<span data-ttu-id="b6476-156">Megadja a nevét, a Windows PowerShell munkamenet-konfiguráció, más néven futási térből, amelyhez ez a szabály engedélyezi a hozzáférést.</span><span class="sxs-lookup"><span data-stu-id="b6476-156">Specifies the name of the Windows PowerShell session configuration, also known as runspace, to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="b6476-157">Aliasok</span><span class="sxs-lookup"><span data-stu-id="b6476-157">Aliases</span></span>                              | <span data-ttu-id="b6476-158">nincs</span><span class="sxs-lookup"><span data-stu-id="b6476-158">none</span></span>                                 |
| <span data-ttu-id="b6476-159">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="b6476-159">Required?</span></span>                            | <span data-ttu-id="b6476-160">Igaz</span><span class="sxs-lookup"><span data-stu-id="b6476-160">true</span></span>                                 |
| <span data-ttu-id="b6476-161">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="b6476-161">Position?</span></span>                            | <span data-ttu-id="b6476-162">nevű</span><span class="sxs-lookup"><span data-stu-id="b6476-162">named</span></span>                                |
| <span data-ttu-id="b6476-163">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="b6476-163">Default Value</span></span>                        | <span data-ttu-id="b6476-164">nincs</span><span class="sxs-lookup"><span data-stu-id="b6476-164">none</span></span>                                 |
| <span data-ttu-id="b6476-165">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="b6476-165">Accept Pipeline Input?</span></span>               | <span data-ttu-id="b6476-166">Igaz (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b6476-166">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="b6476-167">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="b6476-167">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="b6476-168">hamis</span><span class="sxs-lookup"><span data-stu-id="b6476-168">false</span></span>                                |

### <a name="-credentialltpscredentialgt"></a><span data-ttu-id="b6476-169">-Credential&lt;PSCredential&gt;</span><span class="sxs-lookup"><span data-stu-id="b6476-169">-Credential&lt;PSCredential&gt;</span></span>

<span data-ttu-id="b6476-170">Megadja a **PSCredential** objektum, amely a Windows PowerShell Web Access engedélyezési szabályok módosítása használni kívánt felhasználói fiók.</span><span class="sxs-lookup"><span data-stu-id="b6476-170">Specifies a **PSCredential** object for a user account that you want to use to change Windows PowerShell Web Access authorization rules.</span></span> <span data-ttu-id="b6476-171">Ha nem adja hozzá ezt a paramétert, a parancsmag használja az aktuálisan bejelentkezett felhasználói fiók.</span><span class="sxs-lookup"><span data-stu-id="b6476-171">If you do not add this parameter, the cmdlet uses the currently logged-on user account.</span></span> <span data-ttu-id="b6476-172">A beolvasandó egy **PSCredential** objektum, amely pedig szükséges, adja hozzá az engedélyezési szabályok távolról, futtassa a [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="b6476-172">To get a **PSCredential** object, which is required to add authorization rules remotely, run the [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) cmdlet.</span></span>

|||
|-|-|
| <span data-ttu-id="b6476-173">Aliasok</span><span class="sxs-lookup"><span data-stu-id="b6476-173">Aliases</span></span>                              | <span data-ttu-id="b6476-174">nincs</span><span class="sxs-lookup"><span data-stu-id="b6476-174">none</span></span>                                 |
| <span data-ttu-id="b6476-175">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="b6476-175">Required?</span></span>                            | <span data-ttu-id="b6476-176">hamis</span><span class="sxs-lookup"><span data-stu-id="b6476-176">false</span></span>                                |
| <span data-ttu-id="b6476-177">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="b6476-177">Position?</span></span>                            | <span data-ttu-id="b6476-178">nevű</span><span class="sxs-lookup"><span data-stu-id="b6476-178">named</span></span>                                |
| <span data-ttu-id="b6476-179">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="b6476-179">Default Value</span></span>                        | <span data-ttu-id="b6476-180">nincs</span><span class="sxs-lookup"><span data-stu-id="b6476-180">none</span></span>                                 |
| <span data-ttu-id="b6476-181">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="b6476-181">Accept Pipeline Input?</span></span>               | <span data-ttu-id="b6476-182">hamis</span><span class="sxs-lookup"><span data-stu-id="b6476-182">false</span></span>                                |
| <span data-ttu-id="b6476-183">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="b6476-183">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="b6476-184">hamis</span><span class="sxs-lookup"><span data-stu-id="b6476-184">false</span></span>                                |

### <a name="-force"></a><span data-ttu-id="b6476-185">-Force</span><span class="sxs-lookup"><span data-stu-id="b6476-185">-Force</span></span>

<span data-ttu-id="b6476-186">A felhasználó jóváhagyásának kérése nélkül futtatja a parancsot. \\</span><span class="sxs-lookup"><span data-stu-id="b6476-186">Forces the command to run without asking for user confirmation.\\</span></span>
<span data-ttu-id="b6476-187">Ezenkívül rendszer is kérni fogja a megerősítő egy egyszerű vagy rövid számítógép nevét (például a nevet, amely nem egy tartománynevet vagy nincs teljesen minősített) beírásakor.</span><span class="sxs-lookup"><span data-stu-id="b6476-187">In addition, it also prompts for confirmation when you enter a simple or short computer name (such as a name that is not a domain name or is not fully qualified).</span></span> <span data-ttu-id="b6476-188">Jóváhagyás biztonsági okokból van szükség, hogy az egyszerű név segítségével adja hozzá a számítógépet, csak ha a számítógép egy munkacsoport.</span><span class="sxs-lookup"><span data-stu-id="b6476-188">Confirmation is requested for security reasons, so that you can use the simple name to add a computer only if the computer is in a workgroup.</span></span>

|||
|-|-|
| <span data-ttu-id="b6476-189">Aliasok</span><span class="sxs-lookup"><span data-stu-id="b6476-189">Aliases</span></span>                              | <span data-ttu-id="b6476-190">nincs</span><span class="sxs-lookup"><span data-stu-id="b6476-190">none</span></span>                                 |
| <span data-ttu-id="b6476-191">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="b6476-191">Required?</span></span>                            | <span data-ttu-id="b6476-192">hamis</span><span class="sxs-lookup"><span data-stu-id="b6476-192">false</span></span>                                |
| <span data-ttu-id="b6476-193">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="b6476-193">Position?</span></span>                            | <span data-ttu-id="b6476-194">nevű</span><span class="sxs-lookup"><span data-stu-id="b6476-194">named</span></span>                                |
| <span data-ttu-id="b6476-195">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="b6476-195">Default Value</span></span>                        | <span data-ttu-id="b6476-196">nincs</span><span class="sxs-lookup"><span data-stu-id="b6476-196">none</span></span>                                 |
| <span data-ttu-id="b6476-197">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="b6476-197">Accept Pipeline Input?</span></span>               | <span data-ttu-id="b6476-198">hamis</span><span class="sxs-lookup"><span data-stu-id="b6476-198">false</span></span>                                |
| <span data-ttu-id="b6476-199">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="b6476-199">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="b6476-200">hamis</span><span class="sxs-lookup"><span data-stu-id="b6476-200">false</span></span>                                |

### <a name="-rulenameltstringgt"></a><span data-ttu-id="b6476-201">-RuleName&lt;String&gt;</span><span class="sxs-lookup"><span data-stu-id="b6476-201">-RuleName&lt;String&gt;</span></span>

<span data-ttu-id="b6476-202">Megadja a szabály rövid nevét.</span><span class="sxs-lookup"><span data-stu-id="b6476-202">Specifies the friendly name for this rule.</span></span>

|||
|-|-|
| <span data-ttu-id="b6476-203">Aliasok</span><span class="sxs-lookup"><span data-stu-id="b6476-203">Aliases</span></span>                              | <span data-ttu-id="b6476-204">nincs</span><span class="sxs-lookup"><span data-stu-id="b6476-204">none</span></span>                                 |
| <span data-ttu-id="b6476-205">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="b6476-205">Required?</span></span>                            | <span data-ttu-id="b6476-206">hamis</span><span class="sxs-lookup"><span data-stu-id="b6476-206">false</span></span>                                |
| <span data-ttu-id="b6476-207">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="b6476-207">Position?</span></span>                            | <span data-ttu-id="b6476-208">nevű</span><span class="sxs-lookup"><span data-stu-id="b6476-208">named</span></span>                                |
| <span data-ttu-id="b6476-209">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="b6476-209">Default Value</span></span>                        | <span data-ttu-id="b6476-210">nincs</span><span class="sxs-lookup"><span data-stu-id="b6476-210">none</span></span>                                 |
| <span data-ttu-id="b6476-211">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="b6476-211">Accept Pipeline Input?</span></span>               | <span data-ttu-id="b6476-212">Igaz (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b6476-212">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="b6476-213">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="b6476-213">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="b6476-214">hamis</span><span class="sxs-lookup"><span data-stu-id="b6476-214">false</span></span>                                |

### <a name="-usergroupnameltstringgt"></a><span data-ttu-id="b6476-215">-UserGroupName&lt;String\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="b6476-215">-UserGroupName&lt;String\[\]&gt;</span></span>

<span data-ttu-id="b6476-216">Megadja egy vagy több felhasználói csoport nevét az AD DS vagy helyi csoportot, amelyhez ez a szabály engedélyezi a hozzáférést.</span><span class="sxs-lookup"><span data-stu-id="b6476-216">Specifies the name of one or more user groups in AD DS or local groups to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="b6476-217">Aliasok</span><span class="sxs-lookup"><span data-stu-id="b6476-217">Aliases</span></span>                              | <span data-ttu-id="b6476-218">nincs</span><span class="sxs-lookup"><span data-stu-id="b6476-218">none</span></span>                                 |
| <span data-ttu-id="b6476-219">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="b6476-219">Required?</span></span>                            | <span data-ttu-id="b6476-220">Igaz</span><span class="sxs-lookup"><span data-stu-id="b6476-220">true</span></span>                                 |
| <span data-ttu-id="b6476-221">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="b6476-221">Position?</span></span>                            | <span data-ttu-id="b6476-222">nevű</span><span class="sxs-lookup"><span data-stu-id="b6476-222">named</span></span>                                |
| <span data-ttu-id="b6476-223">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="b6476-223">Default Value</span></span>                        | <span data-ttu-id="b6476-224">nincs</span><span class="sxs-lookup"><span data-stu-id="b6476-224">none</span></span>                                 |
| <span data-ttu-id="b6476-225">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="b6476-225">Accept Pipeline Input?</span></span>               | <span data-ttu-id="b6476-226">Igaz (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b6476-226">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="b6476-227">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="b6476-227">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="b6476-228">hamis</span><span class="sxs-lookup"><span data-stu-id="b6476-228">false</span></span>                                |

### <a name="-usernameltstringgt"></a><span data-ttu-id="b6476-229">-UserName&lt;karakterlánc\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="b6476-229">-UserName&lt;String\[\]&gt;</span></span>

<span data-ttu-id="b6476-230">Itt adhatja meg, amelyhez ez a szabály engedélyezi a hozzáférést egy vagy több felhasználó.</span><span class="sxs-lookup"><span data-stu-id="b6476-230">Specifies one or more users to which this rule grants access.</span></span> <span data-ttu-id="b6476-231">A felhasználónév lehet egy helyi felhasználói fiók az átjáró számítógépre vagy egy felhasználót az Active Directory tartományi Szolgáltatásokban.</span><span class="sxs-lookup"><span data-stu-id="b6476-231">The user name can be a local user account on the gateway computer or a user in AD DS.</span></span>
<span data-ttu-id="b6476-232">A formátum `domain\user` vagy `computer\user`.</span><span class="sxs-lookup"><span data-stu-id="b6476-232">The format is `domain\user` or `computer\user`.</span></span>

|||
|-|-|
| <span data-ttu-id="b6476-233">Aliasok</span><span class="sxs-lookup"><span data-stu-id="b6476-233">Aliases</span></span>                              | <span data-ttu-id="b6476-234">nincs</span><span class="sxs-lookup"><span data-stu-id="b6476-234">none</span></span>                                 |
| <span data-ttu-id="b6476-235">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="b6476-235">Required?</span></span>                            | <span data-ttu-id="b6476-236">Igaz</span><span class="sxs-lookup"><span data-stu-id="b6476-236">true</span></span>                                 |
| <span data-ttu-id="b6476-237">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="b6476-237">Position?</span></span>                            | <span data-ttu-id="b6476-238">1</span><span class="sxs-lookup"><span data-stu-id="b6476-238">1</span></span>                                    |
| <span data-ttu-id="b6476-239">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="b6476-239">Default Value</span></span>                        | <span data-ttu-id="b6476-240">nincs</span><span class="sxs-lookup"><span data-stu-id="b6476-240">none</span></span>                                 |
| <span data-ttu-id="b6476-241">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="b6476-241">Accept Pipeline Input?</span></span>               | <span data-ttu-id="b6476-242">Igaz (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b6476-242">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="b6476-243">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="b6476-243">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="b6476-244">hamis</span><span class="sxs-lookup"><span data-stu-id="b6476-244">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="b6476-245">&lt;Általánosparaméterek&gt;</span><span class="sxs-lookup"><span data-stu-id="b6476-245">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="b6476-246">Ez a parancsmag a következő általános paramétereket támogatja:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer és - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="b6476-246">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="b6476-247">További információkért lásd: [about_CommonParameters](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_commonparameters).</span><span class="sxs-lookup"><span data-stu-id="b6476-247">For more information, see [about_CommonParameters](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_commonparameters).</span></span>

## <a name="inputs"></a><span data-ttu-id="b6476-248">BEMENETEK</span><span class="sxs-lookup"><span data-stu-id="b6476-248">INPUTS</span></span>

### <a name="string"></a><span data-ttu-id="b6476-249">Karakterlánc</span><span class="sxs-lookup"><span data-stu-id="b6476-249">String</span></span>

<span data-ttu-id="b6476-250">Ez a parancsmag egy karakterláncot vagy karakterláncok fogad el bemenetként.</span><span class="sxs-lookup"><span data-stu-id="b6476-250">This cmdlet accepts a string or an array of strings as input.</span></span>

### <a name="string"></a><span data-ttu-id="b6476-251">Karakterlánc\[\]</span><span class="sxs-lookup"><span data-stu-id="b6476-251">String\[\]</span></span>

<span data-ttu-id="b6476-252">Ez a parancsmag egy karakterláncot vagy karakterláncok fogad el bemenetként.</span><span class="sxs-lookup"><span data-stu-id="b6476-252">This cmdlet accepts a string or an array of strings as input.</span></span>

## <a name="outputs"></a><span data-ttu-id="b6476-253">Kimenetek</span><span class="sxs-lookup"><span data-stu-id="b6476-253">Outputs</span></span>

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a><span data-ttu-id="b6476-254">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="b6476-254">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule</span></span>

<span data-ttu-id="b6476-255">Ez a parancsmag adja vissza az engedélyezési szabály objektum.</span><span class="sxs-lookup"><span data-stu-id="b6476-255">This cmdlet returns the an authorization rule object.</span></span>

## <a name="examples"></a><span data-ttu-id="b6476-256">PÉLDÁK</span><span class="sxs-lookup"><span data-stu-id="b6476-256">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="b6476-257">1. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="b6476-257">EXAMPLE 1</span></span>

<span data-ttu-id="b6476-258">Ez a példa engedélyezi a hozzáférést a munkamenet-konfigurációjához *PSWAEndpoint*, egy korlátozott futási térrel, *KISZ2* lévő felhasználók számára a *SMAdmins* csoport. \\</span><span class="sxs-lookup"><span data-stu-id="b6476-258">This example grants access to the session configuration *PSWAEndpoint*, a restricted runspace, on *srv2* for users in the *SMAdmins* group.\\</span></span>
<span data-ttu-id="b6476-259">**Megjegyzés:**: A számítógép nevét egy teljesen minősített tartománynevét (FQDN) kell lennie.</span><span class="sxs-lookup"><span data-stu-id="b6476-259">**Note**: The computer name must be a fully qualified domain name (FQDN).</span></span> <span data-ttu-id="b6476-260">A rendszergazdák egy korlátozott munkamenet-konfiguráció vagy a parancsmagok és a végfelhasználók futtatott feladatok korlátozott tartománya futási térben határozza meg.</span><span class="sxs-lookup"><span data-stu-id="b6476-260">Administrators define a restricted session configuration or runspace, which is a limited range of cmdlets and tasks that end users can run.</span></span> <span data-ttu-id="b6476-261">Egy korlátozott futási térrel definiálása megakadályozhatja a felhasználók hozzáférhessenek más számítógépekhez, amely nem áll az engedélyezett Windows PowerShell® térben, így rendelkezésre több biztonságos kapcsolatot.</span><span class="sxs-lookup"><span data-stu-id="b6476-261">Defining a restricted runspace can prevent users from accessing other computers that are not in the allowed Windows PowerShell® runspace, thus offering a more secure connection.</span></span> <span data-ttu-id="b6476-262">A munkamenet-konfigurációk további információkért lásd: [about_session_configuration_files](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configurations) vagy a [telepítése és használata a Windows PowerShell Web Access](../install-and-use-windows-powershell-web-access.md).</span><span class="sxs-lookup"><span data-stu-id="b6476-262">For more information on session configurations, see [about_Session_Configurations](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configurations) or the [Install and Use Windows PowerShell Web Access](../install-and-use-windows-powershell-web-access.md).</span></span>

```PowerShell
Add-PswaAuthorizationRule -ComputerName srv2.contoso.com -UserGroupName contoso\SMAdmins -ConfigurationName PSWAEndpoint
```

### <a name="example-2"></a><span data-ttu-id="b6476-263">2. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="b6476-263">EXAMPLE 2</span></span>

<span data-ttu-id="b6476-264">Ebben a példában az alapértelmezett Windows PowerShell munkamenet-konfiguráció, hozzáférést biztosít a `Microsoft.PowerShell`a *KISZ2* a felhasználók számára a felhasználókhoz, contoso nevű\\felhasználó1, contoso\\felhasználó2, és a contoso\\Felhasználó3.</span><span class="sxs-lookup"><span data-stu-id="b6476-264">This example grants access to the default Windows PowerShell session configuration, `Microsoft.PowerShell`, on *srv2* for users in the users named contoso\\user1, contoso\\user2, and contoso\\user3.</span></span> <span data-ttu-id="b6476-265">Ez a parancsmag három szabályokat (1 / személy) hoz létre.</span><span class="sxs-lookup"><span data-stu-id="b6476-265">This cmdlet creates three rules (1 per person).</span></span>

```PowerShell
Add-PswaAuthorizationRule –UserName contoso\user1, contoso\user2, contoso\user3 –ComputerName srv2.contoso.com -ConfigurationName Microsoft.PowerShell
```

### <a name="example-3"></a><span data-ttu-id="b6476-266">3. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="b6476-266">EXAMPLE 3</span></span>

<span data-ttu-id="b6476-267">Ez a példa bemutatja, hogyan a felhasználótól, felhasználói név értékek keresztül a feldolgozási sor.</span><span class="sxs-lookup"><span data-stu-id="b6476-267">This example illustrates how to input user name values via the pipeline.</span></span>

```
"contoso\user1","contoso\user2" | Add-pswaAuthorizationRule –ComputerName srv2.contoso.com –ConfigurationName Microsoft.PowerShell
```

### <a name="example-4"></a><span data-ttu-id="b6476-268">4. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="b6476-268">EXAMPLE 4</span></span>

<span data-ttu-id="b6476-269">Ez a példa bemutatja, hogyan minden paraméter láncból értékek tegye meg a tulajdonság nevét.</span><span class="sxs-lookup"><span data-stu-id="b6476-269">This example illustrates how all parameters take values from pipeline by property name.</span></span>

````PowerShell
$o = New-Object -TypeName PSObject |
    Add-Member -Type NoteProperty -Name "UserName" -Value "contoso\user1" -PassThru |
    Add-Member -Type NoteProperty -Name "ComputerName" -Value "srv2.contoso.com" -PassThru |
    Add-Member -Type NoteProperty -Name "ConfigurationName" -Value "Microsoft.PowerShell" –PassThru

$o | Add-PswaAuthorizationRule -UserName contoso\user1 -ConfigurationName Microsoft.PowerShell
````

### <a name="example-5"></a><span data-ttu-id="b6476-270">5. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="b6476-270">EXAMPLE 5</span></span>

<span data-ttu-id="b6476-271">Ebben a példában a szabály nevű a helyi felhasználó hozzáadása *PswaServer\\ChrisLocal* nevű kiszolgálóra való hozzáférés *srv1.contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="b6476-271">This example adds a rule to allow the local user named *PswaServer\\ChrisLocal* access to the server named *srv1.contoso.com*.</span></span>

<span data-ttu-id="b6476-272">Ez a példa bemutatja, egy olyan forgatókönyvet, amelyben az átjáró a munkacsoport és a célszámítógép tartományban van.</span><span class="sxs-lookup"><span data-stu-id="b6476-272">This example illustrates a scenario where the gateway is in a workgroup and the destination computer is in a domain.</span></span> <span data-ttu-id="b6476-273">Az engedélyezési szabály vonatkozik a helyi felhasználók az átjárón.</span><span class="sxs-lookup"><span data-stu-id="b6476-273">The authorization rule applies to the local users on the gateway.</span></span> <span data-ttu-id="b6476-274">A Windows PowerShell Web Access bejelentkezési oldal, a sikeres hitelesítést végezni, a felhasználónak meg kell adnia egy második együttesét a hitelesítő adatokat a **választható csatlakozási beállítások** területen.</span><span class="sxs-lookup"><span data-stu-id="b6476-274">On the Windows PowerShell Web Access sign-in page, to successfully authenticate, the user must provide a second set of credentials in the **Optional connection settings** area.</span></span> <span data-ttu-id="b6476-275">Az átjárókiszolgáló használ a további hitelesítő adatok hitelesíteni a felhasználót a célszámítógépen, a kiszolgáló nevű *srv1.contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="b6476-275">The gateway server uses the additional set of credentials to authenticate the user on the destination computer, a server named *srv1.contoso.com*.</span></span>

````
Add-PswaAuthorizationRule –UserName PswaServer\ChrisLocal –ComputerName srv1.contoso.com –ConfigurationName Microsoft.PowerShell
````

### <a name="example-6"></a><span data-ttu-id="b6476-276">6. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="b6476-276">EXAMPLE 6</span></span>

<span data-ttu-id="b6476-277">Ebben a példában minden végpontok hozzáférést biztosít minden felhasználó az összes olyan számítógépen.</span><span class="sxs-lookup"><span data-stu-id="b6476-277">This example allows all users access to all endpoints on all computers.</span></span>
<span data-ttu-id="b6476-278">Ez lényegében kikapcsolja az engedélyezési szabályok. \\</span><span class="sxs-lookup"><span data-stu-id="b6476-278">This essentially turns off authorization rules.\\</span></span>
<span data-ttu-id="b6476-279">**Megjegyzés:**: használja a `*` helyettesítő karakter használata nem ajánlott a biztonsági szempontból kényes központi telepítések és csak kell figyelembe venni a tesztkörnyezetek vagy központi telepítések szerepel, ahol a biztonsági mérsékelhető.</span><span class="sxs-lookup"><span data-stu-id="b6476-279">**Note**: Use of the `*` wildcard character is not recommended for security-sensitive deployments and should only be considered for test environments or used in deployments where security can be relaxed.</span></span>

````PowerShell
Add-PswaAuthorizationRule –UserName * -ComputerName * -ConfigurationName *
````

## <a name="see-also"></a><span data-ttu-id="b6476-280">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b6476-280">See Also</span></span>

- <span data-ttu-id="b6476-281">[Get-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592891(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="b6476-281">[Get-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592891(v=wps.630).aspx)</span></span>
- <span data-ttu-id="b6476-282">[Remove-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592893(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="b6476-282">[Remove-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592893(v=wps.630).aspx)</span></span>
- <span data-ttu-id="b6476-283">[Test-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592892(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="b6476-283">[Test-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592892(v=wps.630).aspx)</span></span>
- <span data-ttu-id="b6476-284">[Install-PswaWebApplication](https://technet.microsoft.com/en-us/library/jj592894(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="b6476-284">[Install-PswaWebApplication](https://technet.microsoft.com/en-us/library/jj592894(v=wps.630).aspx)</span></span>
- [<span data-ttu-id="b6476-285">Tag hozzáadása</span><span class="sxs-lookup"><span data-stu-id="b6476-285">Add-Member</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=113280)
- [<span data-ttu-id="b6476-286">New-Object</span><span class="sxs-lookup"><span data-stu-id="b6476-286">New-Object</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=113355)
- [<span data-ttu-id="b6476-287">Get-Credential</span><span class="sxs-lookup"><span data-stu-id="b6476-287">Get-Credential</span></span>](http://go.microsoft.com/fwlink/?LinkID=293936)