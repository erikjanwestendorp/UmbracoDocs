# Redirect API

This is the read-only API for delivering redirects, caused by moving or renaming content in the Umbraco backoffice, to any app, website, device, or platform.

## Cultures

To request redirects in a specific language, a culture parameter can be specified. When no culture is specified it's treated as invariant and the default language will be returned.

### Access via an Accept-Language header

```http
GET https://cdn.umbraco.io/redirect
Accept-Language: en-US
```

### Access via a Query String parameter

```http
GET https://cdn.umbraco.io/redirect?culture=en-US
```

## Common Headers

```http
Accept-Language: {culture}
Api-Version: 2.3
Umb-Project-Alias: {project-alias}
```

## Errors

If an error occurs, you will receive a HTTP status code along with an API error code and an error message in the response body.

| Status Code | Error Code                 | Message                                                                                                                                                       |
| ----------- | -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 400         | AmbiguousCulture           | The following cultures were requested: {cultures}. At most, only a single culture may be specified. Please update the intended culture and retry the request. |
| 400         | LanguageForCultureNotFound | Could not find a language for culture {culture}.                                                                                                              |
| 401         | Unauthorized               | Authorization has been denied for this request.                                                                                                               |
| 500         | InternalServerError        | Internal server error.                                                                                                                                        |

**JSON example**:

```json
{
  "error": {
    "code": "LanguageForCultureNotFound",
    "message": "Could not find a language for culture en-GB."
  }
}
```

## Get all redirects

Get all redirect URLs.

The key is the URL of the content and the values are the URLs redirecting to the content.

**URL**: `/redirect`

**Method**: `GET`

**Query Strings**

```
?page={integer=1}
?pageSize={integer=10}
```

{% hint style="info" %}
The maximum page size is 1000.
{% endhint %}

### Success Response

**Code**: 200

**Content Example**:

```json
{
    "redirects": {
        "/root5/": [
            "/root4",
            "/root3",
            "/root2",
            "/root"
        ],
        "/root5/child/": [
            "/root4/child",
            "/root3/child",
            "/root2/child",
            "/root/child"
        ]
    },
    "_totalItems": 2,
    "_totalPages": 1,
    "_page": 1,
    "_pageSize": 10,
    "_links": {
        "self": {
            "href": "https://cdn.umbraco.io/redirect?page=1&pageSize=10"
        }
    }
}
```


## Get content by redirect URL

Get the destination URL and redirect URLs for a given path.

**URL**: `/redirect/redirecturl?url={url}`

**Method**: `GET`

### Success Response

**Code**: 200

**Content Example**:

```json
{
    "url": "/home",
    "redirectUrls": [
        "/home-redirect-example-1",
        "/home-redirect-example-2"
    ]
}
```