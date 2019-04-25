---
title: HelpInfo XML-séma |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 74dcb396-c295-4457-b84c-4432bdaa8df3
caps.latest.revision: 7
ms.openlocfilehash: 0f965f4ee1ef92a6a538b52b4348c04366cabf66
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62082464"
---
# <a name="helpinfo-xml-schema"></a><span data-ttu-id="96f31-102">HelpInfo XML-séma</span><span class="sxs-lookup"><span data-stu-id="96f31-102">HelpInfo XML Schema</span></span>

<span data-ttu-id="96f31-103">Ez a témakör tartalmazza a frissíthető Súgó fájlok, gyakran nevezik "HelpInfo XML-fájlokat." XML-sémája</span><span class="sxs-lookup"><span data-stu-id="96f31-103">This topic contains the XML schema for Updatable Help Information files, commonly known as "HelpInfo XML files."</span></span>

## <a name="helpinfo-xml-schema"></a><span data-ttu-id="96f31-104">HelpInfo XML-séma</span><span class="sxs-lookup"><span data-stu-id="96f31-104">HelpInfo XML Schema</span></span>

<span data-ttu-id="96f31-105">HelpInfo XML-fájlok a következő XML-séma alapulnak.</span><span class="sxs-lookup"><span data-stu-id="96f31-105">HelpInfo XML files are based on the following XML schema.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<schema targetNamespace="http://schemas.microsoft.com/powershell/help/2010/05" xmlns="http://www.w3.org/2001/XMLSchema">
  <element name="HelpInfo">
    <complexType>
      <sequence>
        <element name="HelpContentURI" type="anyURI" minOccurs="1" maxOccurs="1" />
        <element name="SupportedUICultures" minOccurs="1" maxOccurs="1">
          <complexType>
            <sequence>
              <element name="UICulture" minOccurs="1" maxOccurs="unbounded">
                <complexType>
                  <sequence>
                    <element name="UICultureName" type="language" minOccurs="1" maxOccurs="1" />
                    <element name="UICultureVersion" type="string" minOccurs="1" maxOccurs="1" />
                  </sequence>
                </complexType>
              </element>
            </sequence>
          </complexType>
        </element>
      </sequence>
    </complexType>
  </element>
</schema>
```

## <a name="helpinfo-xml-elements"></a><span data-ttu-id="96f31-106">HelpInfo XML-elemek</span><span class="sxs-lookup"><span data-stu-id="96f31-106">HelpInfo XML Elements</span></span>

<span data-ttu-id="96f31-107">A HelpInfo XML-fájlt az alábbi elemeket tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="96f31-107">The HelpInfo XML file includes the following elements.</span></span>

<span data-ttu-id="96f31-108">HelpContentURI URI-ját a Súgó a modul CAB-fájlok helyét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="96f31-108">HelpContentURI Contains the URI of the location of the help CAB files for the module.</span></span> <span data-ttu-id="96f31-109">Az URI "http" vagy "https" kell kezdődnie.</span><span class="sxs-lookup"><span data-stu-id="96f31-109">The URI must begin with "http" or "https".</span></span> <span data-ttu-id="96f31-110">Az URI-t kell megadnia az interneten található, de a CAB-fájl neve nem tartalmazhat.</span><span class="sxs-lookup"><span data-stu-id="96f31-110">The URI should specify an Internet location, but must not include the CAB file name.</span></span> <span data-ttu-id="96f31-111">A **HelpContentURI** érték lehet azonos vagy eltérő a **HelpInfoURI** értéket.</span><span class="sxs-lookup"><span data-stu-id="96f31-111">The **HelpContentURI** value can be the  same or different from the **HelpInfoURI** value.</span></span>

<span data-ttu-id="96f31-112">A modul Súgó fájlok SupportedUICultures jelöli a felhasználói felület kulturális környezetek listája.</span><span class="sxs-lookup"><span data-stu-id="96f31-112">SupportedUICultures Represents the module help files in all UI cultures.</span></span> <span data-ttu-id="96f31-113">Tartalmaz **UICulture** elemek, amelyek mindegyike jelöli, hogy a modul egy megadott felhasználói felület kultúrafüggő részletei a Súgó-fájlokat.</span><span class="sxs-lookup"><span data-stu-id="96f31-113">Contains **UICulture** elements, each of which represents a set of help files for the module in a specified UI culture.</span></span>

<span data-ttu-id="96f31-114">UICulture egy sor egy megadott felhasználói felület kultúrafüggő részletei a modul súgófájlok jelöli.</span><span class="sxs-lookup"><span data-stu-id="96f31-114">UICulture Represents a set of help files for the module in a specified UI culture.</span></span> <span data-ttu-id="96f31-115">Adjon hozzá egy **UICulture** elem minden egyes felhasználói felületi kulturális környezet, amelyben a súgófájlok készültek.</span><span class="sxs-lookup"><span data-stu-id="96f31-115">Add a **UICulture** element for each UI culture in which the help files are written.</span></span>

<span data-ttu-id="96f31-116">UICultureName tartalmazza a felhasználói felület kulturális környezethez, amelyben a súgófájlok írt a nyelvi kódot.</span><span class="sxs-lookup"><span data-stu-id="96f31-116">UICultureName Contains the language code for the UI culture in which the help files are written.</span></span>

<span data-ttu-id="96f31-117">UICultureVersion "N1 a 4 részből verziószámát tartalmazza. N2. N3. N4 "formátum, amely a súgó CAB fájljának a felhasználói felület kultúrafüggő részletei a verziót jelöli.</span><span class="sxs-lookup"><span data-stu-id="96f31-117">UICultureVersion Contains a 4-part version number in "N1.N2.N3.N4" format that represents the version of the help CAB file in the UI culture.</span></span> <span data-ttu-id="96f31-118">Ez a verziószám növelése, amikor új segítséget a felhasználói felület kultúrafüggő részletei által meghatározott a CAB-fájlok feltöltése **UICultureName**.</span><span class="sxs-lookup"><span data-stu-id="96f31-118">Increment this version number whenever you upload new help CAB files in the UI culture that is specified by **UICultureName**.</span></span> <span data-ttu-id="96f31-119">Ez az érték kapcsolatos további információkért lásd: "Verzió Class (rendszer)" az MSDN webhelyen.</span><span class="sxs-lookup"><span data-stu-id="96f31-119">For more information about this value, see "Version Class (System)" in MSDN.</span></span>