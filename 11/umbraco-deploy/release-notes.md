# Release Notes

In this section we have summarised the changes to Umbraco Deploy released in each version. Each version is presented with a link to the [Deploy issue tracker](https://github.com/umbraco/Umbraco.Deploy.Issues/issues) showing a list of issues resolved in the release.  We also link to the individual issues themselves from the detail.

If there are any breaking changes or other issues to be aware of when upgrading they are also noted here.

We've listed here all changes going back to March 2021 for Deploy 4 and above. For details of releases prior to this date, or older versions, please refer to the [package page on our.umbraco.com](https://our.umbraco.com/packages/developer-tools/umbraco-deploy/).

## Release History

### [Deploy 4.7.3](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.7.3) (February 21st 2023)

*   All items listed under the 9.5.3, 10.1.3 and 11.0.1 releases (other than those indicated as only applying to higher versions).

### Deploy Contrib 4.2.1 (February 21st 2023)

*   All items listed under the 9.1.1, 10.1.1 and 11.0.1 releases (other than those indicated as only applying to higher versions).

### [Deploy 9.5.3](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.5.3), [10.1.3](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F10.1.3) and [11.0.1](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F10.1.2) (February 14th 2023)

*   Applied various updates to improve performance and reduce likelihood of timeouts when transferring or restoring items in bulk [#128](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/128) [#152](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/152) [#148](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/148) [#110](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/110) [#106](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/106)
    *   Added a task to set signatures via the backoffice settings dashboard, ensuring these are calculated and cached before a restore is commenced.
    *   Provided a configuration option to allow for use of the media file metadata instead of file contents when calculating a checksum.
    *   Made a new default behaviour which can be tweaked via configuration, of loading all relations into memory once we know we are processing a lot of artifact signatures, and doing look-ups for the relations for each entity from there.
    *   Optimised the retrieval of relations ensuring excluded relation types aren't retrieved and then filtered in memory.
    *   Updated the default configuration to exclude the document/media "dependency" relations that were introduced in an earlier minor version of Umbraco 10, and aren't required for including in deployment operations.
    *   Added a configuration value to allow skipping of "path too long" exceptions with media files (so the media item will be created, but with no file attached).
    *   Providing a custom message in the case of a hosting environment hard timeout with information and links to options for resolution.
*   Fixed issue with the Forms add-on that wasn't transferring conditionals on pages or workflows, nor the "contains sensitive data" flag [#158](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/158) [#154](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/154)
*   Fixed display of _IgnoreBrokenDependencies_ setting in the management dashboard (10+) [#151](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/151)
*   Ensured schema files are not generated for member groups when configured to not export them [#150](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/150)
*   Fixed display child nodes indicator for tree picker used for selecting items in the remote environment [#146](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/146)
*   Added additional logging to indicate which item and pass causes a processing failure if and when one occurs [#144](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/144)
*   Tidied up initialization markers [#102](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/102)

### Deploy Contrib 9.1.1, 10.1.1 and 11.0.1 (February 14th 2023)

*   Block grid editor support and fix for null reference exception (10+)
*   Further caching for deploy operations.

### [Deploy 4.7.2](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.7.2), [9.5.2](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.5.2) and [10.1.2](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F10.1.2) (November 15th 2022)

*   Added batch settings option providing resolution to large content or media transfers hitting Azure service limit [#128](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/128)

### [Deploy 4.7.1](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.7.1), [9.5.1](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.5.1) and [10.1.1](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F10.1.1) (October 18th 2022)

*   Resolved issue with media restore when database items exist and files don't (backport fix to V4) [#123](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/123)
*   Fixed issue with use of HTTP timeout setting (V9+)

### [Deploy 4.7.0](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.7.0), [9.5.0](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.5.0) and [10.1.0](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F10.1.0) (September 22nd 2022)

*   All changes listed under 4.7.0-rc001, 9.5.0-rc001 and 10.1.0-rc001
*   Fixed issue with scheduled publish date being time shifted on deployments when source and target servers are running in different timezones.
*   Fixed issue with transfer for members of a given type (V10 only) [#139](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/139)

### Deploy Contrib 4.2.0, 9.1.0 and 10.1.0 (September 22nd 2022)

*   All changes listed under 4.2.0-rc001, 9.1.0-rc001 and 10.1.0-rc001
*   Fixed issue with transfer of nested content string values using item templates (i.e. commencing with "{{") that were erroneously considered as JSON.

### [Deploy 4.7.0-rc001](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.7.0), [9.5.0-rc001](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.5.0) and [10.1.0-rc001](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F10.1.0) (September 7th 2022)

*   Introduced and used caching in deploy operations to improve performance.
*   Increased default and added setting for disk operation timeouts [#135](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/135)
*   Single language content transfers [#132](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/132)
*   Scheduled content transfers.
*   Corrected transfer of unpublished content status [#131](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/131)
*   Improved UX and descriptions in back-office settings dashboard [#118](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/118)
*   Added ability to download Deploy artifacts (.uda files) as a zip archive from the management dashboard.
*   Added sort options to the schema comparison view in the management dashboard [#115](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/115)
*   Indented the JSON representation of data type configuration details in the .uda files for ease of review [#85](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/85)
*   Fixed issue with transfer of Forms prevalue sources from text files that include captions.
*   Ensured document type validation messages are transferred between environments [#137](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/137)

### Deploy Contrib 4.2.0-rc001, 9.1.0-rc001 and 10.1.0-rc001 (September 7th 2022)

*   Used caching in value connectors to improve performance.

### [Deploy 4.6.2](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.6.2), [9.4.2](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.4.2) and [10.0.3](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F10.0.3) (August 16th 2022)

*   Aligned Git URL displayed in back-office with that in Cloud Portal (V4 only) [#136](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/136)
*   Fixed issue with deployment of root node value for Umbraco Forms's "save as Umbraco node" workflow [#133](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/133)
*   Fixed incorrect availability of workspace restore in production environment (V9 and V10 only)
*   Added close button to "Transfer now" dialog
*   Resolved registration of deployable types to support configuration for "back-office edition".

### [Deploy 4.6.1,](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.6.1) [9.4.1](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.4.1) and [10.0.2](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F10.0.2) (July 12th 2022)

*   Resolved issue with media restore when database items exist and files don't [#123](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/123)
*   Added details of failed deployment to deploy dashboard [#120](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/120)
*   Added copy button for deploy log in the back-office [#121](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/121)
*   Fixed typo in UI [#113](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/113)
*   Ensured signature refresh on data type move into or out of folder [#125](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/125)
*   Fixed selection of workspace for compare dialog
*   Optimized existence checks in connectors
*   Restore missing partial restore option in content and media tree roots (V9+)
*   Fixed extract trigger URL in PowerShell script distributed with Deploy On-Premise (V9+)
*   Improved deserialization of exceptions for clearer reporting (V9+)

### Deploy Contrib 4.1.2, 9.0.2, 10.0.1 (July 12th 2022)

*   Optimized existence checks in connectors

### [Deploy 10.0.1](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F10.0.1) (June 29th 2022)

*   Fixed issue with deployment of content using variant properties [#126](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/126)

### [Deploy 10.0.0](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F10.0.0) (June 16th 2022)

*   Compatibility with .NET 6 and Umbraco 10

### Deploy Contrib 4.1.1 (April 26th 2022)

*   Fixes issue with deployment of nested content properties within doc type grid editor values. [#82](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/82)

### [Deploy 4.6.0](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.6.0) [and](https://github.com/umbraco/Umbraco.Forms.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F8.12.0) [9.4.0](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.4.0) (April 26th 2022)

*   All changes listed under 4.6.0-rc001 and 9.4.0-rc001
*   Retained compact JSON formatting when transferring grid values

### [Deploy 4.6.0-rc001](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.6.0) and [9.4.0-rc001](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.4.0) (April 12th 2022)

*   Enhancements to content comparison dialog [#101](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/101)[](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/65)
*   Partial restore for Forms and third-party plugins [#100](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/100)
*   Display of configuration information and schema comparison on the deploy "settings" dashboard.
*   Deployment of culture & hostname details [#107](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/107)
*   Optional, automated clear of memory cache
*   Resolved issue with empty value deployment of content based on the tags property editor [#104](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/104)
*   Resolved issue with redirect functionality when records are deployed between environments (part of CMS [#10066](https://github.com/umbraco/Umbraco-CMS/issues/10066))
*   Surfaced information about configuration for the ignore of broken dependencies in the dialog that presents the error information
*   Fixed a CSS rendering issue for the deploy content dashboard's workspace display, when more than four environments are available.
*   Fixed issue with deployment of empty tags data [#104](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/104)

### [Deploy 9.3.1](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.3.1) (March 22nd 2022)**

*   Adds support for deploying new relation type property introduced in CMS 9.4
*   Fixes layout issue on workspaces dashboard when more than 4 environments are configured.

### [Deploy 4.5.0](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.5.0) and [9.3.0](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.3.0) (March 8th 2022)

*   All changes from 4.5.0-rc001 and 9.3.0-rc001
*   Fixed bug with deployments of templates involving alias renames

### [Deploy 4.5.0-rc001](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.5.0) and [9.3.0-rc001](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.3.0) (February 15th 2022)

*   Content comparison dialog [#65](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/65)
*   Back-office deployment of members and member groups.
*   Added support for deployment of history clean-up settings on document types (V4 only)

### [Deploy 4.4.4](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.4.4) and [9.2.3](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.2.3) (February 15th 2022)

*   Fixed content transfer issue when public access login and error pages are created below the protected page [#99](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/99)
*   Fixed issue with clashing permission letter for "queue for transfer" menu option (V4 only) [#95](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/95)

### [Deploy 4.4.3](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.4.3) and [9.2.2](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.2.2) (January 25th 2022)

*   Fixed ambiguous match exception when deploying forms (V4 only) [#97](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/97)
*   Fixed issue with "live edit" component and scheduled publishing (V9 only) [#98](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/98)
*   Amends to timing of file operation initialization to ensure third party components complete setup (V9 only).
*   Added .NET 6 version of environment variable syntax for Umbraco Cloud configuration settings.

### [Deploy 9.2.1](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.2.1) (January 11th 2022)

*   Fixed issue with clashing permission letter for "queue for transfer" menu option [#95](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/95)
*   Fixed link to open project in Cloud portal [#94](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/94)

### [Deploy 2.1.6](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.4.2) (January 11th 2022)

*   Improved reliability of extractions triggered from Umbraco Cloud git deployment operations by introducing a new marker file used only on start-up (back-port from 4.4.0).

### [Deploy 4.4.2](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.4.2) (December 21st 2021)

*   Fixed issue with extractions triggered from uda files generated from older versions without property group aliases. [#92](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/92)
*   Fixed timing issue for initiation of reading of file system triggers impacting third party Deploy integrations. [#91](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/91)

### [Deploy 9.2.0](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.2.0) (December 7th 2021)

*   Fixed issue relating to deployment of image alt text within the rich text editor. [#87](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/87)
*   Added support for deployment of history clean-up settings on document types.
*   Fixes display of git clone URL in the backoffice dashboard. [#88](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/88)
*   Updates connection string initialization to earlier in the pipeline to ensure it's available for external component configuration.
*   Fixed casing of Deploy folder in App\_Plugins referenced from the custom "no nodes" page.

### [Deploy 4.4.1](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.4.1) (December 7th 2021)

*   Fixed issue relating to deployment of image alt text within the rich text editor. [#87](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/87)

### [Deploy 2.1.5](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F2.1.5) (December 7th 2021)

*   Fixed issue relating to deployment of data types with prevalues on Umbraco 7. [#20](https://github.com/umbraco/Umbraco.Cloud.Issues/issues/20) [#45](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/45) [#89](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/89)

### [Deploy 4.4.0](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.4.0) and [9.1.0](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.1.0) (November 16th 2021)

*   All updates listed under 4.4.0-rc001/2 and 9.1.0-rc001/2.[](https://github.com/umbraco/Umbraco.Forms.Issues/issues/669)

### [Deploy 4.4.0-rc002](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.4.0) and [9.1.0-rc002](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.1.0) (November 8th 2021)

*   Fixed issue with restore of empty tab alias  [#84](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/84)

### [Deploy 4.4.0-rc001](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.4.0) and [9.1.0-rc001](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.1.0) (November 2nd 2021)

*   Separate operations for "tree" and "workspace" restore  [#66](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/66)
*   Finer configuration options for ignoring broken dependencies [#81](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/81)
*   Removed the redundant and misleading deploy operations available on the form "entries" menu item. [#83](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/83)
*   Fixed issue with operations involving Form prevalue sources using XPath. [#69​](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/69)
*   Fixed issue with restore options when Forms 8.8 is used with form definitions stored on disk. [#76](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/76)
*   Improved reliability of extractions triggered from Umbraco Cloud git deployment operations by introducing a new marker file used only on start-up.
*   Improved reliability of extractions on new Cloud infrastructure by wrapping and throttling the file system watcher events.
*   Fixed issues with styling and scripts on the custom “no content” page displayed when Deploy is used.
*   Fixed issue with language deployment when fallbacks are configured.
*   Improved the error reporting when authorization fails between environments (V9 only). [#77](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/77)

### [Deploy 9.0.1](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F9.0.1) (October 12th 2021)

*   Removed import document type option [#73](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/73)
*   Resolved globalization discrepancy leading to schema mismatch reports [#72](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/72)
*   Set appropriate environment defaults for package migration schema and content installation [#74](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/74) [#75](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/75)

### [Deploy 4.3.0](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.3.0) (October 7th 2021)

*   Added support for deployment of CMS tabs and groups
*   Fixed issue with JSON detection causing issues using square brackets in grid content [#70](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/70)

### Deploy 9.0.0 (September 27th 2021)

*   V9 release on .NET 5 compatible with CMS V9.

### [Deploy 4.2.0](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.2.0) (September 14th 2021)

*   All updates listed for 4.2.0-rc001
*   Fixed issue with deploying Form prevalues with Forms versions < 8.5 [#23](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/23)[](https://github.com/umbraco/Umbraco.Forms.Issues/issues/110)

### Deploy 2.1.4 and 4.1.4 (September 7th 2021)

*   Resolution of issue with failed extractions on vNext infrastructure.

### [Deploy 4.2.0-rc001](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.2.0+) (August 19th 2021)

*   Added support for deployment of form folders [#75 (Forms)](https://github.com/umbraco/Umbraco.Forms.Issues/issues/75)
*   Added support for back-office transfer of data from custom packages or solutions 
*   Provided option for deploying dictionary items "as content" [#17](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/17) [#56](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/56)
*   List multiple dependency errors when deploying or restoring [#5](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/5)
*   Add additional detail about deployment errors into logs [#40](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/40)
*   Alter structure of .uda files to put name and alias at the top [#50](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/50)
*   Fixed issue with removal of used macro parameter when restoring [#53](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/53)
*   Add deep-link to deploy dashboard from transfer queue, so will be shown on click from "open transfer queue" (if CMS version supports deep dashboard links) [#57](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/57)
*   Added value connector for new media picker [#58](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/58)
*   Added refresh button to queue [#61](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/61)
*   Fixed issue with changing casing of template aliases [#63](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/63)
*   Added clear signature operation for minor updates of Deploy or CMS
*   Fixed issue with forms deployment where workflows are deleted via code.

### Deploy 4.1.3 (August 3rd 2021)

*   Resolution of issue with failed extractions on vNext infrastructure.

### Deploy 2.0.18 + 2.1.3 (July 6th 2021)

*   Updating Cloud vNext related configuration

### [Deploy 4.1.1](https://github.com/umbraco/Umbraco.Deploy.Issues/issues?q=is%3Aissue+is%3Aclosed+label%3Arelease%2F4.1.1+) (April 27th 2021)

*   Added serialization converter for control of number of decimal places - #465 (internal)
*   Resolved issue with deployment of content schedule - #445 (internal) and [#31](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/31)
*   Resolved issue with unnecessary empty records being created in destination database - #444 (internal)
*   Resolved issue with transfer of content templates when variants are enabled - #385 (internal)
*   Resolved issues with content restore progress not updating when custom dashboards are installed - [#39](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/39) and [#47](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/47)
*   Resolved issue with deployment of changes to default language - [#32](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/32)
*   Resolved issue with deployment of empty values not replacing previously entered content - [#1](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/1)
*   Removed "transfer now" button from users that don't have permission to "queue for transfer" - [#25](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/25)
*   Added deployment of member only property type properties (e.g. "view on profile") - [#21](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/21)
*   Cleared pre-values cache on form deployments - [#43](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/43)
*   Ensured datatype move action triggered serialization and allows deployment to target environment - [#10](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/10)
*   Resolve UI issue where dialog closes if not accurate on selecting node from target environment for restore - [#4](https://github.com/umbraco/Umbraco.Deploy.Issues/issues/4)

### Deploy 4.1.0 (March 25th 2021)

*   Management dashboard for triggering and viewing status of deployment operations
*   Release of Deploy On-Premises

### Deploy 4.0.1 (March 23rd 2021)

*   Enabling Deploy 4 to work in new Cloud infrastructure