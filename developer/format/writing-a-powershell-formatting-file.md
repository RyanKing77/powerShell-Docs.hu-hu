---
title: A fájl formázása PowerShell írása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 39acce45-5144-43ba-894d-a4ce782fa67d
caps.latest.revision: 13
ms.openlocfilehash: f89f0009972d5237d71cb8f0d1c53cd0ae614b67
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847543"
---
# <a name="writing-a-powershell-formatting-file"></a><span data-ttu-id="88794-102">PowerShelles formázási fájl írása</span><span class="sxs-lookup"><span data-stu-id="88794-102">Writing a PowerShell Formatting File</span></span>

<span data-ttu-id="88794-103">"Egy PowerShell-formázás fájl írása" parancs fejlesztőknek szól, akik az írás-parancsmagok és funkciók, amelyek a parancssor az objektumok kimenete van.</span><span class="sxs-lookup"><span data-stu-id="88794-103">"Writing a PowerShell Formatting File" is for command developers who are writing cmdlets or functions that output objects to the command line.</span></span> <span data-ttu-id="88794-104">Formázási fájlokat adja meg, hogyan PowerShell jeleníti meg azokat az objektumokat a parancssorból.</span><span class="sxs-lookup"><span data-stu-id="88794-104">Formatting files define how PowerShell displays those objects at the command line.</span></span> <span data-ttu-id="88794-105">Ez a dokumentáció áttekintése a formázási fájlok, magyarázatát tartalmazza a fogalmakat, amelyek ezeket a fájlokat, XML, az XML-elemeket ezeket a fájlokat, és a egy hivatkozási szakaszban használt példák írásakor tisztában kell lennie.</span><span class="sxs-lookup"><span data-stu-id="88794-105">This documentation provides an overview of formatting files, an explanation of the concepts that you should understand when writing these files, examples of XML used in these files, and a reference section for the XML elements.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="88794-106">A szakasz tartalma</span><span class="sxs-lookup"><span data-stu-id="88794-106">In This Section</span></span>

<span data-ttu-id="88794-107">[– Áttekintés formázás](./formatting-file-overview.md) formátumú fájl elküldéséhez és a egy formázási fájlt, beleértve a közös szolgáltatásokat, amelyek a fájl formátuma nézeteket, amelyek a .NET-objektumokat, a különböző típusú általános összetevőinek és a egy a táblázatos nézetre definiáló XML egyszerűsített példa.</span><span class="sxs-lookup"><span data-stu-id="88794-107">[Formatting File Overview](./formatting-file-overview.md) Describes what a format file is and the general components of a formatting file, including common features that can be defined in the file, the different types of format views that can be defined for .NET objects, and a simplified example of the XML used to define a table view.</span></span>

<span data-ttu-id="88794-108">[Fájl fogalmak formázás](./formatting-file-concepts.md) olyan információk, amelyekre szüksége lehet tudni, hogy amikor létrehozása a saját formázás fájlokat, például nézetek, meghatározhatja a különböző típusú és speciális összetevői adott nézeteket létrehozták.</span><span class="sxs-lookup"><span data-stu-id="88794-108">[Formatting File Concepts](./formatting-file-concepts.md) Includes information that you might need to know when creating your own formatting files, such as the different types of views that you can define and special components of those views.</span></span>

<span data-ttu-id="88794-109">[Példák a formázás fájlok](./examples-of-formatting-files.md) biztosít XML példák néhány formázási fájlt, beleértve a táblázatos nézetre, a lista nézetben, és a egy széles nézet példákat, valamint bemutatják, hogyan kijelölés csoportok, a kiválasztási feltételek, például a jellemzők meghatározása és Gyakori vezérlők.</span><span class="sxs-lookup"><span data-stu-id="88794-109">[Examples of Formatting Files](./examples-of-formatting-files.md) Provides XML examples of several formatting files, including examples of a table view, a list view, and a wide view, as well as examples that show how to define features such as selection sets, selection conditions, and common controls.</span></span>

<span data-ttu-id="88794-110">[XML-hivatkozása formázása](./format-schema-xml-reference.md) Includes referencia-témakörök egy formázási fájlban használt XML-elemeket.</span><span class="sxs-lookup"><span data-stu-id="88794-110">[Format XML Reference](./format-schema-xml-reference.md) Includes reference topics for the XML elements used in a formatting file.</span></span>
