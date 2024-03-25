---
description: Connect to Cloud environment's Azure Blob Storage programmatically.
---

# Connect and Upload Files Programmatically to Azure Blob Storage

## Connect to Azure Blob Storage programmatically

This article provides the steps needed to programmatically connect to your Umbraco Cloud Environment's Azure Blob Storage containers, to persist files programmatically. You will need access to the Blob Storage credentials to authenticate and find the files created programmatically in the Azure Blob Storage.

By the end of this article you will have connected and uploaded a file to your Cloud Blob Storage. The list of the files within the folder will only be available on the Azure Storage so they are not visible publicly. This is with the exception of each individual file that can be shared publicly via the `*.blob.core.windows.net` URL.

{% hint style="info" %}
An alternative to this guide is to use [Umbraco Storage Providers](https://github.com/umbraco/Umbraco.StorageProviders) package or `MediaFileManager.FileSystem` abstraction from the [Custom File Systems (IFileSystem)](https://docs.umbraco.com/umbraco-cms/extending/filesystemproviders#accessing-the-media-file-system-from-code) article.
{% endhint %}

Follow these steps to get started:

1. Clone down your Umbraco Cloud Project. You can find more information on how to clone a project in the [Working Locally](../working-locally.md) article.
2. Run your project.
3. Install `Azure.Storage.Blobs` package on your project. You can do it either via NuGet Package Manager on Visual Studio or install it via [NuGet](https://www.nuget.org/packages/Azure.Storage.Blobs/).
4. Run the project to complete the installation of the package.
5. Add a new class called `BlobStorageService` which serves as a service that has a method to connect to Blob Storage:

{% code title="BlobStorageService.cs" lineNumbers="true" %}
```csharp
using Azure.Storage.Blobs;

namespace UmbracoProject
{
    public class BlobStorageService
    {
        public BlobContainerClient GetContainerClient(string connectionString, string containerName)
        {
            BlobServiceClient blobServiceClient = new BlobServiceClient(connectionString);
            BlobContainerClient containerClient = blobServiceClient.GetBlobContainerClient(containerName);
            return containerClient;

        }
    }
}
```
{% endcode %}

6. Add a new class called `BlobStorageComposer` to inject the service:

{% code title="BlobStorageComposer.cs" lineNumbers="true" %}
```csharp
using Umbraco.Cms.Core.Composing;

namespace UmbracoProject;

public class BlobStorageComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
    {
        builder.Services.AddScoped<BlobStorageService>();

    }
}
```
{% endcode %}

7. Add a new class called `BlobStorageController` which serves as the Surface Controller:

{% code title="BlobStorageController.cs" lineNumbers="true" %}
```csharp
using Azure.Storage.Blobs;
using Microsoft.AspNetCore.Mvc;
using Umbraco.Cms.Core.Cache;
using Umbraco.Cms.Core.Logging;
using Umbraco.Cms.Core.Routing;
using Umbraco.Cms.Core.Services;
using Umbraco.Cms.Core.Web;
using Umbraco.Cms.Infrastructure.Persistence;
using Umbraco.Cms.Web.Website.Controllers;

namespace UmbracoProject;

public class BlobStorageController : SurfaceController
{

    private readonly BlobStorageService _blobStorageService;

    public BlobStorageController(
        IUmbracoContextAccessor umbracoContextAccessor,
        IUmbracoDatabaseFactory databaseFactory,
        ServiceContext services,
        AppCaches appCaches,
        IProfilingLogger profilingLogger,
        IPublishedUrlProvider publishedUrlProvider,
        BlobStorageService blobStorageService)
        : base(umbracoContextAccessor, databaseFactory, services, appCaches, profilingLogger, publishedUrlProvider)
    {
        _blobStorageService = blobStorageService;
    }

    // access the endpoint in backoffice via /umbraco/surface/BlobStorage/BlobUpdate
    public async Task<IActionResult> BlobUpdate()
    {

        string SASUrl = "Replace this with the Shared access signature URL (SAS) from Umbraco Cloud settings"; 
        string containerName = "Replace this with the Container Name from the Umbraco Cloud settings"; 

        string connectionString = $"BlobEndpoint={SASUrl}";

        BlobContainerClient containerClient = _blobStorageService.GetContainerClient(connectionString, containerName);

        string localPath = "data";
        Directory.CreateDirectory(localPath);
        string fileName = Guid.NewGuid().ToString() + ".txt";
        string localFilePath = Path.Combine(localPath, fileName);

        try
        {
            // Write some content to the file
            await using (StreamWriter writer = new StreamWriter(localFilePath))
            {
                await writer.WriteLineAsync("Hello, World! This file is created programatically!");
            }

        }
        catch (Exception)
        {
            // ignored
        }

        // Get a reference to a blob
        string blobName = "FolderProgramatically/" + Guid.NewGuid().ToString() + ".txt"; //the blobName can be anything
        BlobClient blobClient = containerClient.GetBlobClient(blobName);

        Console.WriteLine("Uploading to Blob storage as blob:\n\t {0}\n", blobClient.Uri);

        // Upload data from the local file
        await blobClient.UploadAsync(localFilePath, true);

        return Content("Check your Blob Storage to see your new file!");
    }

}
```
{% endcode %}

Here, the controller is used to create a directory named `FolderProgramatically` and a `.txt` file in Azure Blob Storage.

{% hint style="warning" %}
In the above code, update the `SASUrl` and `containerName` values with your own from the Umbraco Cloud Settings. To find these values, refer to the instructions in the [Connect to Azure Storage Explorer to upload files manually](connect-to-azure-storage-explorer.md#getting-the-credentials) article.

You can also secure the values in **Secrets Management** in the project **Settings** on Umbraco Cloud so you do not store them in code. For more information, see the [Secrets Management](../project-settings/secrets-management.md) article.
{% endhint %}

8. Run the project.
9. Visit the `{{yourProjectURL}}/umbraco/surface/BlobStorage/BlobUpdate` endpoint in the backoffice of your project to manually trigger the creation of the file to the Blob Storage.
10. [Connect to your Blob Storage](connect-to-azure-storage-explorer.md) and there you will find the folder and file that has been created programmatically:

![Blob folder created programmatically](images/blob-folder-created-programatically.png)

## References

For more information, see the following articles from Microsoft:

* [Get started with Azure Blob Storage and .NET](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blob-dotnet-get-started)
* [Quickstart: Azure Blob Storage client library for .NET](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-dotnet)
