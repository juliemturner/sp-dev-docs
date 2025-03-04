---
title: "FieldTypes element (Field Types)"
manager: soliver
ms.date: 3/9/2015
ms.audience: Developer
ms.topic: reference
ms.prod: sharepoint
ms.localizationpriority: medium
api_name:
- Field Types XML
ms.assetid: ebac779f-c7c5-401b-8503-e514cd96f5a7
description: Represents the collection of field types.
---

# FieldTypes element (Field Types)

**Applies to:** SharePoint 2016 | SharePoint Foundation 2013 | SharePoint Online | SharePoint Server 2013
  
Represents the collection of field types.
  
```XML
<FieldTypes>
</FieldTypes>
```

## Elements and attributes

The following sections describe attributes, child elements, and parent elements.

### Attributes

None
   
### Child elements

- [FieldType element (Field Types)](fieldtype-element-field-types.md)
   
### Parent elements

None
   
### Remarks

FieldType elements are configured fldtypes\*.xml files in %ProgramFiles%\Common Files\Microsoft Shared\web server extensions\15\TEMPLATE\XML.
  
## Example

The following example defines two custom field types. The example has been edited for clarity. 
  
> [!IMPORTANT]
> The **RenderPattern** and **PropertySchema** elements are obsolete. They are shown here solely to assist in the debugging of custom fields that were originally developed against earlier versions of SharePoint Foundation. 
  
> [!NOTE]
> The possible values for the `<Field Name="ParentType">` element are exactly the same as the possible values for the Type attribute of the [Field element (List)](field-element-list.md) element. 
  
```XML
<?xml version="1.0" encoding="utf-8" ?>
<FieldTypes>
  <FieldType>
    <Field Name="TypeName">SocialSecurityNumber</Field>
    <Field Name="ParentType">Text</Field>
    <Field Name="TypeDisplayName">Social Security Number</Field>
      …
    <RenderPattern Name="DisplayPattern">
       …
    </RenderPattern>
  </FieldType>
  <FieldType>
    <Field Name="TypeName">USAddress</Field>
    <Field Name="ParentType">MultiColumn</Field>
    <Field Name="TypeDisplayName">US Address</Field>
      …
    <PropertySchema>
      …
    </PropertySchema>
    <RenderPattern Name="DisplayPattern">
      …
    </RenderPattern>
  </FieldType>
</FieldTypes>
```

## See also

- [Custom Field Types](https://msdn.microsoft.com/library/1345b345-226d-443a-918f-af123a3c7b13%28Office.15%29.aspx) 
- [Custom Field Classes](https://msdn.microsoft.com/library/436a9d9b-7a6f-4e8f-86e8-f42ded85c069%28Office.15%29.aspx)
- [Custom Field Type Property Rendering](https://msdn.microsoft.com/library/a959ad5b-6f3a-462c-80b9-e2d00bb0d62a%28Office.15%29.aspx)
- [Custom Field Type Definition](https://msdn.microsoft.com/library/b3315997-671f-4c29-9518-48cc4592f205%28Office.15%29.aspx)
- [Walkthrough: Creating a Custom Field Type](https://msdn.microsoft.com/library/089a1b8a-cafc-4050-b445-16650602fe4f%28Office.15%29.aspx)

