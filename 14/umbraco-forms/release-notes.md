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

This section contains the release notes for Umbraco Forms 14 including all changes for this version.

#### [**14.0.2**](https://github.com/umbraco/Umbraco.Forms.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F14.0.2) **(June 11th 2024)**

* Fixed issue with upload of text file for the prevalue source based on file contents.

#### [**14.0.1**](https://github.com/umbraco/Umbraco.Forms.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F14.0.1) **(June 6th 2024)**

* Ensured local links are parsed when HTML fields are returned in the delivery API results for form definitions [#1227](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1227).
* Restored target used to generate local configuration schema information [#1226](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1226).
* Resolved duplicate approval occuring when record is approved via a workflow [#1223](https://github.com/umbraco/Umbraco.Forms.Issues/issues/1223).
* Added some missing localization keys and translations.
* Fixed description of management API on Swagger UI.
* Fixed display of specific form access list for user and group security.

#### [**14.0.0**](https://github.com/umbraco/Umbraco.Forms.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F14.0.0) **(May 30th 2024)**

* Compatibility with Umbraco 14
  * See full details of breaking changes under the [Version-specific Upgrade Guide](upgrading/version-specific.md).

## Umbraco.Forms.Deploy

#### **14.0.0** **(May 30th 2024)**

* Compatibility with Umbraco 14, Forms 14 and Deploy 14.

## Legacy release notes

You can find the release notes for versions out of support in the [Legacy documentation on Github](https://github.com/umbraco/UmbracoDocs/blob/umbraco-eol-versions/11/umbraco-forms/release-notes.md) and [Umbraco Forms Package page](https://our.umbraco.com/packages/developer-tools/umbraco-forms/).
