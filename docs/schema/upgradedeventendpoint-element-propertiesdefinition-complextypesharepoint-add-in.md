---
title: UpgradedEventEndpoint element (PropertiesDefinition complexType)
manager: soliver
ms.date: 9/17/2015
ms.audience: Developer
ms.topic: article
ms.prod: sharepoint
ms.localizationpriority: medium
ms.assetid: 09a93d44-d295-47bb-f91c-d243178b0f53
---

# UpgradedEventEndpoint element (PropertiesDefinition complexType) 

(SharePoint Add-in Manifest)

**Applies to**: SharePoint Add-ins | SharePoint Foundation 2013 | SharePoint Server 2013

The Url of the upgraded event receiver endpoint.

> [!NOTE] 
> The string `app` appears as part of or all of some element, attribute, and file names because SharePoint Add-ins were originally called "apps for SharePoint." To ensure backward compatibility, the schemas have not been changed.

## Element information

|   |   |
|---|---|
| **Element type**  | UrlElementDefinition |
| **Namespace**  | `http://schemas.microsoft.com/sharepoint/2012/app/manifest` |
| **Schema file**  | appmanifest.xsd |

## Definition

```XML
        <xs:element name="UpgradedEventEndpoint"  type="UrlElementDefinition"
         minOccurs="0"
         maxOccurs="1"
        >
        </xs:element>
```        

## Elements and attributes

If the schema defines specific requirements, such as **sequence**, **minOccurs**, **maxOccurs**, and **choice**, see the definition section.

### Parent elements

<table>
<colgroup>
<col width="30%" />
<col width="30%" />
<col width="40%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><p>Element</p></th>
<th align="left"><p>Type</p></th>
<th align="left"><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="properties-element-appdefinition-complextypesharepoint-add-in-manifest.md">Properties</a></p></td>
<td align="left"><p><a href="propertiesdefinition-complextype-sharepoint-add-in-manifest.md">PropertiesDefinition</a></p></td>
<td align="left"><p>Contains information that is global to the add-in.</p></td>
</tr>
</tbody>
</table>

### Child elements

None.

### Attributes

None.

<br/>

<br/>


