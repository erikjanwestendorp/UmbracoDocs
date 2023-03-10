---
description: Follow this guide when upgrading your Cloud project to a new major version of Umbraco CMS. For example when upgrading from 10 to 11.
---

# Major Upgrades

{% hint style="info" %}
**Are you using any custom packages or code on your Umbraco Cloud project?**

You need to ensure that any packages you use are available in the latest version of Umbraco. You also need to ensure that your custom code is valid with the new .NET Framework version.

**Breaking Changes**

Make sure you know the [Breaking changes](https://docs.umbraco.com/umbraco-cms/fundamentals/setup/upgrading/version-specific#breaking-changes) in the latest version of Umbraco CMS.

**Upgrading from Umbraco 9**

If upgrading from Umbraco 9 to a later major version, follow the dropdowns named: _**"Upgrading from Umbraco 9"**_ in the steps of the guide.

These are extra steps needed when going from Umbraco 9 to the latest major.
{% endhint %}

## Prerequisites

* Follow the **requirements** for [local development](https://docs.umbraco.com/umbraco-cms/fundamentals/setup/requirements#local-development).
* A Umbraco Cloud project running **the latest version of Umbraco**
* The **latest** .[NET version](https://dotnet.microsoft.com/en-us/download/visual-studio-sdks) is installed locally.
* **At least 2 environments** on your Cloud project.
* A backup of your project database.
  * Directly from your environment. See the [Database backups](../databases/backups.md) article,
  * Or clone down, restore the project, and backup the local database.

## Video Tutorial

{% embed url="https://www.youtube-nocookie.com/embed/80qwWxoNuKU" %}
Video Tutorial
{% endembed %}

## Step 1: Enable .NET

* Go to the project in the Umbraco Cloud portal.
* Navigate to **Settings** -> **Advanced**.
* Scroll down to the **Runtime Settings** section.
* **Ensure that the latest version of .NET is enabled** for each environment on your Cloud project.

<figure><img src="../../.gitbook/assets/runtime-settings.png" alt=""><figcaption><p>Runtime settings</p></figcaption></figure>

## Step 2: Clone down your environment

* Clone down the **Development** environment.
* Build and run the [project locally](../set-up/working-locally.md#running-the-site-locally).
* Log in to the backoffice.
* Restore content from your Cloud environment.

## Step 3: Upgrade the project locally using Visual Studio

* Open your project in Visual Studio - use the `csproj` file in the `/src/UmbracoProject` folder.
* Right-click your project solution in **Solution Explorer**.
* Select **Properties**.

<figure><img src="images/Solution-Explorer.png" alt=""><figcaption></figcaption></figure>

* Select the same **.Net** **Target Framework** drop-down in the **General** section of the **Application** tab as on your Cloud project.

![Target Framework](images/Target-Framework.png)

* Go to **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution...**.
* Navigate to the **Updates** tab.
* Checkmark all packages made **by Umbraco**:
  * Umbraco.Cms
  * Umbraco.Deploy.Cloud
  * Umbraco.Deploy.Contrib
  * Umbraco.Forms
  * Umbraco.Deploy.Forms
  * Umbraco.Cloud.Identity.Cms
* Checkmark the `Microsoft.Extensions.DependencyInjection.Abstractions` package if it appears in the list.
* Select **Update**.

![All packages checked in the Visual Studio Package manager and ready for update](images/check-all-packages-2.png)

{% hint style="info" %}
If you have more projects in your solution or other packages, make sure that these are also updated to support the latest .NET framework.
{% endhint %}

<details>

<summary>Upgrading from Umbraco 9 - Update program.cs, appSettings.json and remove files.</summary>

*   Update the `Program` class in the `Program.cs` file to the following:\
    using Umbraco.Cms.Web.Common.Hosting;

    ```

    public class Program
        {
            public static void Main(string[] args)
                => CreateHostBuilder(args)
                    .Build()
                    .Run();

            public static IHostBuilder CreateHostBuilder(string[] args) =>
                Host.CreateDefaultBuilder(args)
                    .ConfigureUmbracoDefaults()
                    .ConfigureWebHostDefaults(webBuilder =>
                    {
                        webBuilder.UseStaticWebAssets();
                        webBuilder.UseStartup<Startup>();
                    });
        }
    ```
* Re-enable the appsettings IntelliSense by updating your schema reference in the **appsettings.json** file from:

```json
"$schema": "./umbraco/config/appsettings-schema.json",
```

To:

```json
"$schema": "./appsettings-schema.json",
```

Apply this change to the following files as well:

* **appsettings.Development.json**
* **appsettings.Production.json**
* **appsettings.Staging.json**

Remove the following files and folders _manually_ from your local project:

* `/wwwroot/umbraco`
* `/umbraco/PartialViewMacros`
* `/umbraco/UmbracoBackOffice`
* `/umbraco/UmbracoInstall`
* `/umbraco/UmbracoWebsite`
* `/umbraco/config/lang`

</details>

## Step 4: Finishing the Upgrade

* Enable the [Unattended Upgrades](https://docs.umbraco.com/umbraco-cms/fundamentals/setup/upgrading#run-an-unattended-upgrade) feature.
* Run the **project locally**.
* Log in to the Umbraco backoffice to **verify the upgrade** has happened.
* **Disable** the Unattended Upgrades feature.
* **Build and run** the project to verify everything works as expected.

![Target Framework](images/verify-v10-upgrade-locally.png)

Once the Umbraco project runs locally without any errors, the next step is to deploy and test on the Cloud Development environment.

<details>
    
<summary>Upgrading from Umbraco 9 - Remove files from the development environment.</summary>

* `/wwwroot/umbraco`
* `/umbraco/PartialViewMacros`
* `/umbraco/UmbracoBackOffice`
* `/umbraco/UmbracoInstall`
* `/umbraco/UmbracoWebsite`
* `/umbraco/config/lang`

The files and folder above need to be removed on the **Development** environment through `KUDU` -> `Debug Console` -> `CMD` -> `Site` -> from both the `repository` and `wwwroot` folders.

<img src="https://user-images.githubusercontent.com/83591955/210218172-b32a6be9-9b2a-48c4-8ed7-676068f72946.png" alt="image" data-size="original">

</details>

* Push the changes to the **Development** environment. See the [Deploying from local to your environments](../deployment/local-to-cloud.md) article.
* Test **everything** in the **Development** environment.

We highly recommend that you go through everything in your Development environment. This can help you identify any potential errors after the upgrade, and ensure that you are not deploying any issues onto your Live environment.

## Step 5: Going live

<details>

<summary>Upgrading from Umbraco 9 - Remove files from staging/live the environment.</summary>

Before deploying the upgrade to your next environment, you will need to remove the folders you also removed from Kudu on your Development environment.

The files are:

* `/wwwroot/umbraco`
* `/umbraco/PartialViewMacros`
* `/umbraco/UmbracoBackOffice`
* `/umbraco/UmbracoInstall`
* `/umbraco/UmbracoWebsite`
* `/umbraco/config/lang`

They need to be removed through `KUDU` -> `Debug Console` -> `CMD` -> `Site` -> from both the `repository` and `wwwroot` folders.

<img src="https://user-images.githubusercontent.com/83591955/210218090-9b72fc05-cfe3-442f-8045-a90e5b8a9e89.png" alt="image" data-size="original">

</details>

Once everything works as expected in the development environment, you can push the upgrade to the live environment.

* [Working locally with Umbraco Cloud](../set-up/working-locally.md)
* [KUDU on Umbraco Cloud](../set-up/power-tools/)
