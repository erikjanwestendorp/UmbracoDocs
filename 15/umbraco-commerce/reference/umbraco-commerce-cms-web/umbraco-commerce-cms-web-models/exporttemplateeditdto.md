---
title: ExportTemplateEditDto
description: API reference for ExportTemplateEditDto in Umbraco Commerce
---
## ExportTemplateEditDto

```csharp
public class ExportTemplateEditDto : ExportTemplateDto, IHasPath, INotificationModel
```

**Inheritance**

* Class [ExportTemplateDto](exporttemplatedto.md)
* interface [IHasPath](ihaspath.md)

**Namespace**
* [Umbraco.Commerce.Cms.Web.Models](README.md)

### Constructors

#### ExportTemplateEditDto

The default constructor.

```csharp
public ExportTemplateEditDto()
```


### Properties

#### Notifications

```csharp
public List<BackOfficeNotification> Notifications { get; set; }
```


---

#### Path

```csharp
public List<string> Path { get; set; }
```


<!-- DO NOT EDIT: generated by xmldocmd for Umbraco.Commerce.Cms.Web.dll -->