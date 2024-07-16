---
description: Tips to porting over API controllers from Umbraco 13 and below
---

# Porting old Umbraco APIs

Umbraco 14 has obsoleted or removed base classes that were widely adopted for building APIs in previous versions of Umbraco. This article outlines the recommended approach for porting over APIs that were created before Umbraco 14.

## Porting over `UmbracoApiController` implementations

`UmbracoApiController` is obsolete from Umbraco 14 and will be removed in Umbraco 15. The recommended approach is to base APIs on the ASP.NET Core `Controller` class instead.

`UmbracoApiController` would automatically route the API actions to `/umbraco/api/[ControllerName]/[ControllerAction]`. Moving forward, you control your API routes with the `[Route]` annotation.

If you rely on the route previously generated by `UmbracoApiController`, you can still create identical routes. For example, the following `Controller` implementation:

{% code title="ProductsController.cs" %}
```csharp
using Microsoft.AspNetCore.Mvc;

namespace UmbracoDocs.Samples;

[ApiController]
[Route("/umbraco/api/products")]
public class ProductsController : Controller
{
    [HttpGet("getall")]
    public IActionResult GetAll() => Ok(new[] { "Table", "Chair", "Desk", "Computer" });
}
```
{% endcode %}

...is routing-wise equivalent to this `UmbracoApiController` implementation:

{% code title="ProductsController.cs" %}
```csharp
using Microsoft.AspNetCore.Mvc;
using Umbraco.Cms.Web.Common.Controllers;

namespace UmbracoDocs.Samples;

public class ProductsController : UmbracoApiController
{
    public IActionResult GetAll() => Ok(new[] { "Table", "Chair", "Desk", "Computer" });
}
```
{% endcode %}

In both cases, the API endpoint will be available at `/umbraco/api/products/getall`.

## Porting over "plugin based" implementations

In previous versions of Umbraco, it was possible to route controllers to dedicated areas by annotating `UmbracoApiController` implementations with `[PluginController]`. This annotation would automatically route the API actions to `/Umbraco/[PluginAreaName]/[ControllerName]/[ActionName]`.

As this approach was based on `UmbracoApiController`, it is no longer viable - use the `[Route]` annotation instead. For example, the following `Controller` implementation:

{% code title="ProductsController.cs" %}
```csharp
using Microsoft.AspNetCore.Mvc;

namespace UmbracoDocs.Samples;

[ApiController]
[Route("/umbraco/shop/products")]
public class ProductsController : Controller
{
    [HttpGet("getall")]
    public IActionResult GetAll() => Ok(new[] { "Table", "Chair", "Desk", "Computer" });
}
```
{% endcode %}

...is routing wise equivalent to this `[PluginController]` annotated implementation:

{% code title="ProductsController.cs" %}
```csharp
using Microsoft.AspNetCore.Mvc;
using Umbraco.Cms.Web.Common.Attributes;
using Umbraco.Cms.Web.Common.Controllers;

namespace UmbracoDocs.Samples;

[PluginController("shop")]
public class ProductsController : UmbracoApiController
{
    public IActionResult GetAll() => Ok(new[] { "Table", "Chair", "Desk", "Computer" });
}
```
{% endcode %}

In both cases, the API endpoint will be available at `/umbraco/shop/products/getall`.

## Backoffice API Controllers

The `UmbracoAuthorizedApiController` and `UmbracoAuthorizedJsonController` base classes have been removed in Umbraco 14. Moving forward, backoffice APIs (also known as Management APIs) must be based on the `ManagementApiControllerBase`.

Read the [Creating a Backoffice API article](../tutorials/creating-a-backoffice-api/README.md) for a comprehensive guide to writing APIs for the Management API.