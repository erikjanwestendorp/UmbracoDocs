---
description: >-
  Details an integration available for Zapier, built and maintained by Umbraco
  HQ.
---

# Zapier

This integration provides a dashboard interface that allows users to visualize registered subscription hooks. When a Zap is turned on, the subscription hook is saved into the database; turning off the Zap will remove the registered subscription hook.

When content gets published, the content type is looked up in the subscription hooks list from the database. If a record is found, a POST request will be sent to the webhook URL with details of the current node. This will cause the Zap's trigger to be invoked, triggering the assigned actions of the Zap.

A **Zap** is an automated workflow that connects apps and services together. Each Zap consists of a trigger and one or more actions.

## Package Links

* [NuGet install](https://www.nuget.org/packages/Umbraco.Cms.Integrations.Automation.Zapier)
* [Source code](https://github.com/umbraco/Umbraco.Cms.Integrations/tree/main/src/Umbraco.Cms.Integrations.Automation.Zapier)
* [Umbraco marketplace listing](https://marketplace.umbraco.com/package/umbraco.cms.integrations.automation.zapier)

## Minimum version requirements

### Umbraco CMS

| Major      | Minor/Patch |
| ---------- | ----------- |
| Version 8  | 8.5.4       |
| Version 9  | 9.0.1       |
| Version 10 | 10.0.0      |
| Version 11 | 11.0.0      |

## Authentication

For this integration, the authentication is managed on Zapier's side by using the Umbraco Marketplace app.

The trigger event to be used by this integration is _New Content Published_.

When creating the Zap trigger, you will be prompted to enter a username, password, and URL for your Umbraco website. Alternatively, you can use an API key.

If the following setting is present, the API key-based authentication will take precedence and will be the main method of authorization.

{% tabs %}
{% tab title="Versions 9 and above" %}
{% code title="appsettings.json" %}
```json
"Umbraco": {
  "CMS": {
    "Integrations": {
      "Automation": {
        "Zapier": {
          "Settings": {
            "ApiKey": "[your_api_key]"
          }
        }
      }
    }
  }
}
```
{% endcode %}
{% endtab %}

{% tab title="Version 8" %}
{% code title="web.config" %}
```xml
<appSettings>
  <add key="Umbraco.Cms.Integrations.Automation.Zapier.ApiKey" value="[your_api_key]" />
</appSettings>
```
{% endcode %}
{% endtab %}
{% endtabs %}

If no API key is present, the Umbraco application will validate the credentials entered and return a message in case the validation fails.

To enhance security, you can specify a User Group that the user connecting needs to be a part of, by adding the following setting in the configuration file.

{% tabs %}
{% tab title="Versions 9 and above" %}
{% code title="appsettings.json" %}
```json
"Umbraco": {
  "CMS": {
    "Integrations": {
      "Automation": {
        "Zapier": {
          "Settings": {
            ...
            "UserGroup": "[your User Group]"
          }
        }
      }
    }
  }
}
```
{% endcode %}
{% endtab %}

{% tab title="Version 8" %}
{% code title="web.config" %}
```xml
<appSettings>
  <add key="Umbraco.Cms.Integrations.Automation.Zapier.UserGroup" value="[your User Group]" />
</appSettings>
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Working With the Zapier Cms Integration

In the _Content_ area of the backoffice, find the _Zapier Integrations_ dashboard.

The dashboard is composed of two sections:

* Content Properties - Zapier details and input fields for adding content configurations
* Registered Subscription Hooks - a list of registered entities.

The _Trigger Webhook_ action will send a test request to the Zap trigger, enabling the preview of requests in the Zap setup workflow.
