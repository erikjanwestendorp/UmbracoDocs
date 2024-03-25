---
description: >-
  Get an overview of the things changed and fixed in each version of Umbraco Forms.
---

# Release Notes

In this section, we have summarized the changes to Umbraco Forms released in each version. Each version is presented with a link to the [Forms issue tracker](https://github.com/umbraco/Umbraco.Forms.Issues/issues) showing a list of issues resolved in the release. We also link to the individual issues themselves from the detail.

If there are any breaking changes or other issues to be aware of when upgrading they are also noted here.

{% hint style="info" %}
If you are upgrading to a new major version, you can find information about the breaking changes in the [Version Specific Upgrade Notes](upgrading/version-specific.md) article.
{% endhint %}

## Release History

This section contains the release notes for Umbraco Forms 13 including all changes for this version.

#### [**13.1.1**](https://github.com/umbraco/Umbraco.Forms.Issues/issues?q=label%3Arelease%2F13.1.1+is%3Aclosed) **(March 22nd 2024)**

* Fixes regression issue with form validation where two forms are rendered on a single page [#1189](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1189).

#### [**13.1.0**](https://github.com/umbraco/Umbraco.Forms.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F13.1.0) **(March 19th 2024)**

With the introduction of webhooks in Umbraco 13, we've made an update to Forms to allow workflow execution events to trigger webhooks. Workflows are operations that you can associate with form submission, approval, or rejection actions. You can use these where you need to notify external systems of the success or failure of a workflow. Read more on [Umbraco Forms Webhooks](./developer/webhooks.md).

We've added an update that will help customers using Forms within locked down production environments.

And there are a couple of further additions to improve the performance and accessibility of the product.

**Features implemented and issues resolved in 13.1.0**

* Added webhooks for workflow execution events [#1151](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1151).
* Added support for a proxied request when using reCAPTCHA 3 [#1159](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1159).
* Added a configurable option to ensure accessibility requirements with regard to fieldsets are adhered to [#1163](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1163).
    * Read more about this configuration setting [here](./developer/configuration/README.md#mandatoryfieldsetlegends).
* Added a cachebuster querystring based on the current product version to rendered script dependencies [#773](https://github.com/umbraco/Umbraco.Forms.Issues/issues/773).
* Ensured that client-side conditions logic correctly implements "is" with multiple values, such that the condition passes if one and only one matching value is found [#1173](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1173).
* Fixed closing of theme picker dialog [#1174](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1174).
* Fixed rendering of translated dictionary items used for form captions [#1175](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1175).
* Applied multiple click protection for form submissions for installations using the aspnet-validation library [#1182](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1182).

#### [**13.0.2**](https://github.com/umbraco/Umbraco.Forms.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F13.0.2) **(February 20th 2024)**

* Ensured UI for the upload of a text file for a prevalue source only allows the selection of expected .txt files.
* Handled potential null value for prevalues for a form definition following an upgrade [#1157](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1157)
* Fixed handling of API and traditional form posts in reCAPTCHA 3 checks [#1150](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1150)
* Fixed display of validation error when a duplicate form field alias is created [#1152](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1152)
* Fixed issue where file uploads weren't removed as records were deleted.
* Updated Microsoft.Data.SqlClient dependency due to reported security advisory.

#### [**13.0.1**](https://github.com/umbraco/Umbraco.Forms.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F13.0.1) **(January 16th 2024)**

* Added configuration value `TitleAndDescription:AllowUnsafeHtmlRendering` to allow tighter security for HTML rendering of text entered in the "Title and description" field type.
    * See further details on the [configuration page](./developer/configuration/README.md#AllowUnsafeHtmlRendering).
* Rendered dictionary translations of field captions in backoffice entries view [#1131](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1131).
* Ensured valid format string before rendering validation methods with placeholders [#1132](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1132).
* Ensured the creation of the forms to content relation type is idempotent and created with consistent GUID [#1137](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1137).
* Ensured Examine re-index user interface completes when no records are available for indexing [#1137](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1137).
* Fixed issue where use of a custom field HTML ID attribute prefix breaks conditional logic in multi-page forms [#1138](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1138).
* Added support for record based magic string replacement in the post-submission message [#1133](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1133).
* Tightens up the null checks when reading form definition JSON for prevalue captions [#1140](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1140).
* Added configuration value `DisableRelationTracking` to allow relation tracking between forms and content to be disabled.
    * See further details on the [configuration page](./developer/configuration/README.md#DisableRelationTracking).
* Added configuration value `TrackRenderedFormsStorageMethod` to allow use of `HttpContext.Items` over `TempData` when tracking rendered forms [#1144](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1144).
    * See further details on the [configuration page](./developer/configuration/README.md#TrackRenderedFormsStorageMethod) and the [rendering scripts page](./developer//rendering-scripts.md).
* Resolved an out of range exception when a condition hides all fields on the final page of a multi-page form.
* Fixed issue with swapping between plain and rich text when configuring the post-submission message [#1145](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1145).

#### [**13.0.0**](https://github.com/umbraco/Umbraco.Forms.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F13.0.0) **(December 14th 2023)**

* Compatibility with Umbraco 13
  * See full details of breaking changes under the [version specific upgrade guide](upgrading/version-specific.md#version-13).
* Ran registered server-side file validators on file uploads.

## Umbraco.Forms.Deploy

#### [13.0.1] (March 19th 2024)

* Added migrator to support changes in Form field prevalues when importing from older Umbraco versions

## Legacy release notes

You can find the release notes for versions out of support in the [Legacy documentation on Github](https://github.com/umbraco/UmbracoDocs/blob/umbraco-eol-versions/11/umbraco-forms/release-notes.md) and [Umbraco Forms Package page](https://our.umbraco.com/packages/developer-tools/umbraco-forms/).
