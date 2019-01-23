# LiteXHealthChecks
> LiteXHealthChecks is very small yet powerful and high-performance library used to check the status of a component in the application, such as a backend service, database or some internal state.


## Health checks for  :books:
- [Amazon S3](docs/AmazonS3.md)
- [Azure KeyVault](docs/AzureKeyVault.md)
- [Azure ServiceBus](docs/AzureServiceBus.md)
- [Azure Blob Storage](docs/AzureBlobStorage.md)
- [Azure File Storage](docs/AzureFileStorage.md)
- [Azure Queue Storage](docs/AzureQueueStorage.md)
- [MongoDb](docs/MongoDb.md)
- [MySql](docs/MySql.md)
- [Redis](docs/Redis.md)
- [SqlServer](docs/SqlServer.md)


## Features :pager:
- Easy to use
- Very light weight


## Basic Usage :page_facing_up:

### Step 1 : Install the package :package:

> Choose one kinds of sms provider type that you needs and install it via [Nuget](https://www.nuget.org/profiles/iamaashishpatel).
> To install LiteXHealthChecks, run the following command in the [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)

```Powershell
PM> Install-Package LiteX.HealthChecks.AmazonS3
PM> Install-Package LiteX.HealthChecks.AzureKeyVault
PM> Install-Package LiteX.HealthChecks.AzureServiceBus
PM> Install-Package LiteX.HealthChecks.AzureStorage.Blob
PM> Install-Package LiteX.HealthChecks.AzureStorage.File
PM> Install-Package LiteX.HealthChecks.AzureStorage.Queue
PM> Install-Package LiteX.HealthChecks.MongoDb
PM> Install-Package LiteX.HealthChecks.MySql
PM> Install-Package LiteX.HealthChecks.Redis
PM> Install-Package LiteX.HealthChecks.SqlServer
```


### Step 2 : Configuration 🔨 
> Different types of services have their own way to config.
> Here are samples that show you how to config.

##### 2.1 : AppSettings 
```js
{
  "Data": {
    "ConnectionStrings": {
      "AzureKeyVault": "--REPLACE WITH YOUR CONNECTION STRING--",
      "AzureServiceBus": "--REPLACE WITH YOUR CONNECTION STRING--",
      "AzureBlobStorage": "--REPLACE WITH YOUR CONNECTION STRING--",
      "AzureFileStorage": "--REPLACE WITH YOUR CONNECTION STRING--",
      "AzureQueueStorage": "--REPLACE WITH YOUR CONNECTION STRING--",
      "MongoDb": "--REPLACE WITH YOUR CONNECTION STRING--",
      "MySql": "--REPLACE WITH YOUR CONNECTION STRING--",
      "Redis": "--REPLACE WITH YOUR CONNECTION STRING--",
      "SqlServer": "--REPLACE WITH YOUR CONNECTION STRING--"
    }
  },
  "AmazonS3": {
    "AccessKey": "--REPLACE WITH YOUR AccessKey--",
    "SecretKey": "--REPLACE WITH YOUR SecretKey--",
    "BucketName": "--REPLACE WITH YOUR BucketName--"
  }
}
```

##### 2.2 : Configure Startup Class
```cs
public class Startup
{
    public IConfiguration Configuration { get; }

    public Startup(IConfiguration configuration)
    {
        Configuration = configuration;
    }

    public void ConfigureServices(IServiceCollection services)
    {
        #region Amazon S3

        // 1: Use default configuration
        services.AddHealthChecks()
            .AddAmazonS3(options =>
            {
                options.AccessKey = Configuration["AmazonS3:AccessKey"];
                options.SecretKey = Configuration["AmazonS3:SecretKey"];
                options.BucketName = Configuration["AmazonS3:BucketName"];
            }, name: "amazon-s3");

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddAmazonS3(options =>
            {
                options.AccessKey = Configuration["AmazonS3:AccessKey"];
                options.SecretKey = Configuration["AmazonS3:SecretKey"];
                options.BucketName = Configuration["AmazonS3:BucketName"];
            },
            name: "amazon-s3",
            failureStatus: HealthStatus.Degraded,
            tags: new string[] { "amazon-s3", "aws-s3", "s3", "amazon-s3" });

        #endregion

        #region Azure KeyVault

        // 1: Use default configuration
        services.AddHealthChecks()
            .AddAzureKeyVault(options =>
            {
                options
                .UseKeyVaultUrl(Configuration["Data:ConnectionStrings:AzureKeyVault"])
                .UseClientSecrets("client", "secret");
            }, name: "azure-keyvault");

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddAzureKeyVault(options =>
            {
                options
                .UseKeyVaultUrl(Configuration["Data:ConnectionStrings:AzureKeyVault"])
                .UseClientSecrets("client", "secret")
                .AddSecret("supercret");
            },
            name: "azure-keyvault",
            failureStatus: HealthStatus.Degraded,
            tags: new string[] { "azure", "keyvault", "key-vault", "azure-keyvault" });

        #endregion

        #region Azure ServiceBus

        // 1: Use default configuration
        services.AddHealthChecks()
            .AddAzureServiceBusQueue(Configuration["Data:ConnectionStrings:AzureServiceBus"], "queue1");

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddAzureServiceBusQueue(
                connectionString: Configuration["Data:ConnectionStrings:AzureServiceBus"],
                queueName: "queue1",
                name: "azure-servicebus-queue",
                failureStatus: HealthStatus.Degraded,
                tags: new string[] { "azure", "servicebus", "queue", "azure-servicebus-queue" });


        // 1: Use default configuration
        services.AddHealthChecks()
            .AddAzureServiceBusTopic(Configuration["Data:ConnectionStrings:AzureServiceBus"], "topic1");

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddAzureServiceBusTopic(
                connectionString: Configuration["Data:ConnectionStrings:AzureServiceBus"],
                topicName: "topic1",
                name: "azure-servicebus-topic",
                failureStatus: HealthStatus.Degraded,
                tags: new string[] { "azure", "servicebus", "topic", "azure-servicebus-topic" });

        #endregion

        #region Azure Blob Storage

        //1: Use default configuration
        services.AddHealthChecks()
            .AddAzureBlobStorage(Configuration["Data:ConnectionStrings:AzureBlobStorage"]);

        //OR
        //2: With all optional configuration
        services.AddHealthChecks()
            .AddAzureBlobStorage(
                connectionString: Configuration["Data:ConnectionStrings:AzureBlobStorage"],
                name: "azure-blob-storage",
                failureStatus: HealthStatus.Degraded,
                tags: new string[] { "azure", "storage", "blob", "azure-blob-storage" });

        #endregion

        #region Azure File Storage

        #endregion

        #region Azure Queue Storage

        // 1: Use default configuration
        services.AddHealthChecks()
            .AddAzureQueueStorage(Configuration["Data:ConnectionStrings:AzureQueueStorage"]);

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddAzureQueueStorage(
                connectionString: Configuration["Data:ConnectionStrings:AzureQueueStorage"],
                name: "azure-queue-storage",
                failureStatus: HealthStatus.Degraded,
                tags: new string[] { "azure", "storage", "queue", "azure-queue-storage" });

        #endregion

        #region MongoDB

        // 1: Use default configuration
        services.AddHealthChecks()
            .AddMongoDb(Configuration["Data:ConnectionStrings:MongoDb"]);

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddMongoDb(
                connectionString: Configuration["Data:ConnectionStrings:MongoDb"],
                name: "mongodb",
                failureStatus: HealthStatus.Unhealthy,
                tags: new string[] { "db", "nosql", "mongodb" });

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddMongoDb(
                connectionString: Configuration["Data:ConnectionStrings:MongoDb"],
                databaseName: "config",
                name: "mongodb",
                failureStatus: HealthStatus.Unhealthy,
                tags: new string[] { "db", "nosql", "mongodb" });

        #endregion

        #region MySql

        // 1: Use default configuration
        services.AddHealthChecks()
            .AddMySql(Configuration["Data:ConnectionStrings:MySql"]);

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddMySql(
                connectionString: Configuration["Data:ConnectionStrings:MySql"],
                name: "mysql",
                failureStatus: HealthStatus.Unhealthy,
                tags: new string[] { "db", "sql", "mysql" });

        #endregion

        #region Redis

        // 1: Use default configuration
        services.AddHealthChecks()
            .AddRedis(Configuration["Data:ConnectionStrings:Redis"]);

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddRedis(
                connectionString: Configuration["Data:ConnectionStrings:Redis"],
                name: "redis",
                failureStatus: HealthStatus.Degraded,
                tags: new string[] { "cache", "redis", "redisserver" });

        #endregion

        #region SqlServer

        // 1: Use default configuration
        services.AddHealthChecks()
            .AddSqlServer(Configuration["Data:ConnectionStrings:SqlServer"]);

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddSqlServer(
                connectionString: Configuration["Data:ConnectionStrings:SqlServer"],
                sqlQuery: "SELECT 1;",
                name: "sql-server",
                failureStatus: HealthStatus.Unhealthy,
                tags: new string[] { "db", "sql", "sqlserver" });

        #endregion

        #region ZZZZZ

        #endregion

        #region All in one

        services.AddHealthChecks()
            .AddSqlServer(connectionString: Configuration["Data:ConnectionStrings:Sample"])
            .AddCheck<RandomHealthCheck>("random")
            .AddAzureServiceBusQueue("Endpoint=sb://MYBUS.servicebus.windows.net/;SharedAccessKeyName=policy;", "queue1")
            .AddAzureServiceBusTopic("Endpoint=sb://unaidemo.servicebus.windows.net/;SharedAccessKeyName=olicy;", "topic1");

        #endregion

        services.AddMvc()
            .SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
    }

    public void Configure(IApplicationBuilder app, IHostingEnvironment env)
    {
        //app.UseHealthChecks("/health");

        app.UseHealthChecks("/health", new HealthCheckOptions()
        {
            Predicate = _ => true
        });

        app.UseHealthChecks("/healthz", new HealthCheckOptions()
        {
            Predicate = _ => true,
        });

        app.UseMvcWithDefaultRoute();
    }
}
```

### Step 3 : Use in Controller or Business layer :memo:

```cs
/// <summary>
/// Storage controller
/// </summary>
[Route("api/[controller]")]
public class StorageController : Controller
{
    #region Fields

    private readonly ILiteXBlobService _blobService;

    #endregion

    #region Ctor

    /// <summary>
    /// Ctor
    /// </summary>
    /// <param name="blobService"></param>
    public StorageController(ILiteXBlobService blobService)
    {
        _blobService = blobService;
    }

    #endregion

    #region Methods

    /// <summary>
    /// Get Storage Provider Type
    /// </summary>
    /// <returns></returns>
    [HttpGet]
    [Route("get-storage-provider-type")]
    public IActionResult GetStorageProviderType()
    {
        return Ok(_blobService.StorageProviderType.ToString());
    }


    /// <summary>
    /// Get blob list
    /// from default Container/Bucket
    /// </summary>
    /// <returns></returns>
    [HttpGet]
    [Route("get-blobs")]
    public async Task<IActionResult> GetBlobs()
    {
        List<BlobDescriptor> blobs = (await _blobService.GetBlobsAsync()).ToList();

        // sync
        //List<BlobDescriptor> blobs = _blobService.GetBlobs().ToList();

        return Ok(blobs);
    }

    /// <summary>
    /// Get blob list
    /// </summary>
    /// <returns></returns>
    [HttpGet]
    [Route("get-blobs/{containerOrBucketName}")]
    public async Task<IActionResult> GetBlobs(string containerOrBucketName)
    {
        List<BlobDescriptor> blobs = (await _blobService.GetBlobsAsync(containerOrBucketName)).ToList();

        // sync
        //List<BlobDescriptor> blobs = _blobService.GetBlobs(containerOrBucketName).ToList();

        return Ok(blobs);
    }


    /// <summary>
    /// Create/Replace blob file
    /// from default Container/Bucket
    /// </summary>
    /// <param name="file">Blob file</param>
    /// <param name="isPublic">Is Private or Public blob</param>
    /// <returns></returns>
    [HttpPost]
    [Route("upload-blob")]
    [AddSwaggerFileUploadButton]
    public async Task<IActionResult> UploadBlob(IFormFile file, bool isPublic = true)
    {
        string blobName = file.FileName;
        Stream stream = file.OpenReadStream();
        string contentType = file.ContentType;
        BlobProperties properties = new BlobProperties
        {
            ContentType = contentType,
            Security = isPublic ? BlobSecurity.Public : BlobSecurity.Private
        };

        var isUploaded = await _blobService.UploadBlobAsync(blobName, stream, properties);

        // sync
        //var isUploaded = _blobService.UploadBlob(blobName, stream, properties);

        return Ok(isUploaded);
    }

    /// <summary>
    /// Create/Replace blob file
    /// </summary>
    /// <param name="containerOrBucketName">Name of the Bucket/Container.</param>
    /// <param name="file">Blob file</param>
    /// <param name="isPublic">Is Private or Public blob</param>
    /// <returns></returns>
    [HttpPost]
    [Route("upload-blob/{containerOrBucketName}")]
    [AddSwaggerFileUploadButton]
    public async Task<IActionResult> UploadBlob(string containerOrBucketName, IFormFile file, bool isPublic = true)
    {
        string blobName = file.FileName;
        Stream stream = file.OpenReadStream();
        string contentType = file.ContentType;
        BlobProperties properties = new BlobProperties
        {
            ContentType = contentType,
            Security = isPublic ? BlobSecurity.Public : BlobSecurity.Private
        };

        var isUploaded = await _blobService.UploadBlobAsync(containerOrBucketName, blobName, stream, properties);

        // sync
        //var isUploaded = _blobService.UploadBlob(containerOrBucketName, blobName, stream, properties);

        return Ok(isUploaded);
    }


    /// <summary>
    /// Create/Replace blob file in directory/folder
    /// from default Container/Bucket
    /// </summary>
    /// <param name="directoryName">Name of directory/folder.</param>
    /// <param name="file">Blob file</param>
    /// <param name="isPublic">Is Private or Public blob</param>
    /// <returns></returns>
    [HttpPost]
    [Route("upload-blob-in-directory/{directoryName}")]
    [AddSwaggerFileUploadButton]
    public async Task<IActionResult> UploadBlobInDirectory(string directoryName, IFormFile file, bool isPublic = true)
    {
        string blobName = $"{directoryName}/{file.FileName}";
        Stream stream = file.OpenReadStream();
        string contentType = file.ContentType;
        BlobProperties properties = new BlobProperties
        {
            ContentType = contentType,
            Security = isPublic ? BlobSecurity.Public : BlobSecurity.Private
        };

        var isUploaded = await _blobService.UploadBlobAsync(blobName, stream, properties);

        // sync
        //var isUploaded = _blobService.UploadBlob(blobName, stream, properties);

        return Ok(isUploaded);
    }

    /// <summary>
    /// Create/Replace blob file in directory/folder
    /// </summary>
    /// <param name="containerOrBucketName">Name of the Bucket/Container.</param>
    /// <param name="directoryName">Name of directory/folder.</param>
    /// <param name="file">Blob file</param>
    /// <param name="isPublic">Is Private or Public blob</param>
    /// <returns></returns>
    [HttpPost]
    [Route("upload-blob-in-directory/{containerOrBucketName}/{directoryName}")]
    [AddSwaggerFileUploadButton]
    public async Task<IActionResult> UploadBlobInDirectory(string containerOrBucketName, string directoryName, IFormFile file, bool isPublic = true)
    {
        string blobName = $"{directoryName}/{file.FileName}";
        //string blobName = $"{directoryName}{Path.DirectorySeparatorChar}{file.FileName}";
        Stream stream = file.OpenReadStream();
        string contentType = file.ContentType;
        BlobProperties properties = new BlobProperties
        {
            ContentType = contentType,
            Security = isPublic ? BlobSecurity.Public : BlobSecurity.Private
        };

        var isUploaded = await _blobService.UploadBlobAsync(containerOrBucketName, blobName, stream, properties);

        // sync
        //var isUploaded = _blobService.UploadBlob(containerOrBucketName, blobName, stream, properties);

        return Ok(isUploaded);
    }


    /// <summary>
    /// Get blob file data (bytes or stream)
    /// from default Container/Bucket
    /// </summary>
    /// <param name="blobName">Name of the Blob.</param>
    /// <returns></returns>
    [HttpGet]
    [Route("download-blob/{blobName}")]
    public async Task<IActionResult> DownloadBlob(string blobName)
    {
        // get blob
        Stream stream = await _blobService.GetBlobAsync(blobName);

        // sync
        //Stream stream = _blobService.GetBlob(blobName);

        var response = File(stream, "application/octet-stream", blobName); // FileStreamResult
        return response;
    }

    /// <summary>
    /// Get blob file data (bytes or stream)
    /// </summary>
    /// <param name="containerOrBucketName">Name of the Bucket/Container.</param>
    /// <param name="blobName">Name of the Blob.</param>
    /// <returns></returns>
    [HttpGet]
    [Route("download-blob/{containerOrBucketName}/{blobName}")]
    public async Task<IActionResult> DownloadBlob(string containerOrBucketName, string blobName)
    {
        // get blob
        Stream stream = await _blobService.GetBlobAsync(containerOrBucketName, blobName);

        // sync
        //Stream stream = _blobService.GetBlob(containerOrBucketName, blobName);

        var response = File(stream, "application/octet-stream", blobName); // FileStreamResult
        return response;
    }


    /// <summary>
    /// Get blob url
    /// from default Container/Bucket
    /// </summary>
    /// <param name="blobName">Name of the Blob.</param>
    /// <returns></returns>
    [HttpGet]
    [Route("get-blob-url/{blobName}")]
    public async Task<IActionResult> GetBlobUrl(string blobName)
    {
        string blobUrl = await _blobService.GetBlobUrlAsync(blobName);

        // sync
        //string blobUrl = _blobService.GetBlobUrl(blobName);

        return Ok(blobUrl);
    }

    /// <summary>
    /// Get blob url
    /// </summary>
    /// <param name="containerOrBucketName">Name of the Bucket/Container.</param>
    /// <param name="blobName">Name of the Blob.</param>
    /// <returns></returns>
    [HttpGet]
    [Route("get-blob-url/{containerOrBucketName}/{blobName}")]
    public async Task<IActionResult> GetBlobUrl(string containerOrBucketName, string blobName)
    {
        string blobUrl = await _blobService.GetBlobUrlAsync(containerOrBucketName, blobName);

        // sync
        //string blobUrl = _blobService.GetBlobUrl(containerOrBucketName, blobName);

        return Ok(blobUrl);
    }


    /// <summary>
    /// Get blob SAS url
    /// from default Container/Bucket
    /// </summary>
    /// <param name="blobName">Name of the Blob.</param>
    /// <returns></returns>
    [HttpGet]
    [Route("get-blob-sasurl/{blobName}")]
    public async Task<IActionResult> GetBlobSasUrl(string blobName)
    {
        string blobUrl = await _blobService.GetBlobSasUrlAsync(blobName, DateTimeOffset.UtcNow.AddHours(2), BlobUrlAccess.Read);

        // sync
        //string blobUrl = _blobService.GetBlobSasUrl(blobName, DateTimeOffset.UtcNow.AddHours(2), BlobUrlAccess.Read);

        return Ok(blobUrl);
    }

    /// <summary>
    /// Get blob SAS url
    /// </summary>
    /// <param name="containerOrBucketName">Name of the Bucket/Container.</param>
    /// <param name="blobName">Name of the Blob.</param>
    /// <returns></returns>
    [HttpGet]
    [Route("get-blob-sasurl/{containerOrBucketName}/{blobName}")]
    public async Task<IActionResult> GetBlobSasUrl(string containerOrBucketName, string blobName)
    {
        string blobUrl = await _blobService.GetBlobSasUrlAsync(containerOrBucketName, blobName, DateTimeOffset.UtcNow.AddHours(2), BlobUrlAccess.Read);

        // sync
        //string blobUrl = _blobService.GetBlobSasUrl(containerOrBucketName, blobName, DateTimeOffset.UtcNow.AddHours(2), BlobUrlAccess.Read);

        return Ok(blobUrl);
    }


    /// <summary>
    /// Delete blob file
    /// from default Container/Bucket
    /// </summary>
    /// <param name="blobName">Name of the Blob.</param>
    /// <returns></returns>
    [HttpDelete]
    [Route("delete-blob/{blobName}")]
    public async Task<IActionResult> DeleteBlobFile(string blobName)
    {
        var isDeleted = await _blobService.DeleteBlobAsync(blobName);

        // sync
        //var isDeleted = _blobService.DeleteBlob(blobName);

        return Ok(isDeleted);
    }

    /// <summary>
    /// Delete blob file
    /// </summary>
    /// <param name="containerOrBucketName">Name of the Bucket/Container.</param>
    /// <param name="blobName">Name of the Blob.</param>
    /// <returns></returns>
    [HttpDelete]
    [Route("delete-blob/{containerOrBucketName}/{blobName}")]
    public async Task<IActionResult> DeleteBlobFile(string containerOrBucketName, string blobName)
    {
        var isDeleted = await _blobService.DeleteBlobAsync(containerOrBucketName, blobName);

        // sync
        //var isDeleted = _blobService.DeleteBlob(containerOrBucketName, blobName);

        return Ok(isDeleted);
    }


    /// <summary>
    /// Get blob metadata
    /// from default Container/Bucket
    /// </summary>
    /// <param name="blobName">Name of the Blob.</param>
    /// <returns></returns>
    [HttpGet]
    [Route("get-blob-metadata/{blobName}")]
    public async Task<IActionResult> GetBlobMetadata(string blobName)
    {
        BlobDescriptor blobDescriptor = await _blobService.GetBlobDescriptorAsync(blobName);

        // sync
        //BlobDescriptor blobDescriptor = _blobService.GetBlobDescriptor(blobName);

        var metadata = blobDescriptor.Metadata;

        return Ok(blobDescriptor);
    }

    /// <summary>
    /// Get blob metadata
    /// </summary>
    /// <param name="containerOrBucketName">Name of the Bucket/Container.</param>
    /// <param name="blobName">Name of the Blob.</param>
    /// <returns></returns>
    [HttpGet]
    [Route("get-blob-metadata/{containerOrBucketName}/{blobName}")]
    public async Task<IActionResult> GetBlobMetadata(string containerOrBucketName, string blobName)
    {
        BlobDescriptor blobDescriptor = await _blobService.GetBlobDescriptorAsync(containerOrBucketName, blobName);

        // sync
        //BlobDescriptor blobDescriptor = _blobService.GetBlobDescriptor(containerOrBucketName, blobName);

        var metadata = blobDescriptor.Metadata;

        return Ok(blobDescriptor);
    }


    /// <summary>
    /// Set blob metadata
    /// from default Container/Bucket
    /// </summary>
    /// <param name="blobName">Name of the Blob.</param>
    /// <returns></returns>
    [HttpPut]
    [Route("set-blob-metadata/{blobName}")]
    public async Task<IActionResult> SetBlobMetadata(string blobName)
    {
        IDictionary<string, string> metadata = new Dictionary<string, string>();

        BlobProperties properties = new BlobProperties()
        {
            ContentType = "",
            Metadata = metadata,
            ContentDisposition = "",
            Security = BlobSecurity.Public
        };

        var isSet = await _blobService.SetBlobPropertiesAsync(blobName, properties);

        // sync
        //var isSet = _blobService.SetBlobProperties(blobName, properties);

        return Ok(isSet);
    }

    /// <summary>
    /// Set blob metadata
    /// </summary>
    /// <param name="containerOrBucketName">Name of the Bucket/Container.</param>
    /// <param name="blobName">Name of the Blob.</param>
    /// <returns></returns>
    [HttpPut]
    [Route("set-blob-metadata/{containerOrBucketName}/{blobName}")]
    public async Task<IActionResult> SetBlobMetadata(string containerOrBucketName, string blobName)
    {
        IDictionary<string, string> metadata = new Dictionary<string, string>();

        BlobProperties properties = new BlobProperties()
        {
            ContentType = "",
            Metadata = metadata,
            ContentDisposition = "",
            Security = BlobSecurity.Public
        };

        var isSet = await _blobService.SetBlobPropertiesAsync(containerOrBucketName, blobName, properties);

        // sync
        //var isSet = _blobService.SetBlobProperties(containerOrBucketName, blobName, properties);

        return Ok(isSet);
    }


    /// <summary>
    /// Delete directory/folder from default Container/Bucket
    /// </summary>
    /// <param name="directoryName">Name of directory/folder.</param>
    /// <returns></returns>
    [HttpDelete]
    [Route("delete-directory/{directoryName}")]
    public async Task<IActionResult> DeleteDirectory(string directoryName)
    {
        var isDeleted = await _blobService.DeleteDirectoryAsync(directoryName);

        // sync
        //var isDeleted = _blobService.DeleteDirectory(directoryName);

        return Ok(isDeleted);
    }

    /// <summary>
    /// Delete directory/folder from Container/Bucket
    /// </summary>
    /// <param name="containerOrBucketName">Name of the Bucket/Container.</param>
    /// <param name="directoryName">Name of directory/folder.</param>
    /// <returns></returns>
    [HttpDelete]
    [Route("delete-directory/{containerOrBucketName}/{directoryName}")]
    public async Task<IActionResult> DeleteDirectory(string containerOrBucketName, string directoryName)
    {
        var isDeleted = await _blobService.DeleteDirectoryAsync(containerOrBucketName, directoryName);

        // sync
        //var isDeleted = _blobService.DeleteDirectory(containerOrBucketName, directoryName);

        return Ok(isDeleted);
    }


    /// <summary>
    /// Get number to total items/files in Container/Bucket
    /// </summary>
    /// <returns></returns>
    [HttpGet]
    [Route("get-container-or-bucket-item-count")]
    public async Task<IActionResult> GetContainerOrBucketItemCount()
    {
        var itemsCount = await _blobService.GetContainerItemCountAsync();

        // sync
        //var itemsCount = _blobService.GetContainerItemCount();

        return Ok(itemsCount);
    }

    /// <summary>
    /// Get number to total items/files in Container/Bucket
    /// </summary>
    /// <param name="containerOrBucketName">Name of the Bucket/Container.</param>
    /// <returns></returns>
    [HttpGet]
    [Route("get-container-or-bucket-item-count/{containerOrBucketName}")]
    public async Task<IActionResult> GetContainerOrBucketItemCount(string containerOrBucketName)
    {
        var itemsCount = await _blobService.GetContainerItemCountAsync(containerOrBucketName);

        // sync
        //var itemsCount = _blobService.GetContainerItemCount(containerOrBucketName);

        return Ok(itemsCount);
    }


    /// <summary>
    /// Get Container/Bucket size in bytes
    /// </summary>
    /// <returns></returns>
    [HttpGet]
    [Route("get-container-or-bucket-size")]
    public async Task<IActionResult> GetContainerOrBucketSize()
    {
        var size = await _blobService.GetContainerSizeAsync();

        // sync
        //var size = _blobService.GetContainerSize();

        return Ok(size);
    }

    /// <summary>
    /// Get Container/Bucket size in bytes
    /// </summary>
    /// <param name="containerOrBucketName">Name of the Bucket/Container.</param>
    /// <returns></returns>
    [HttpGet]
    [Route("get-container-or-bucket-size/{containerOrBucketName}")]
    public async Task<IActionResult> GetContainerOrBucketSize(string containerOrBucketName)
    {
        var size = await _blobService.GetContainerSizeAsync(containerOrBucketName);

        // sync
        //var size = _blobService.GetContainerSize(containerOrBucketName);

        return Ok(size);
    }


    /// <summary>
    /// Create Container/Bucket
    /// </summary>
    /// <param name="containerOrBucketName">Name of the Bucket/Container.</param>
    /// <returns></returns>
    [HttpGet]
    [Route("create-container-or-bucket/{containerOrBucketName}")]
    public async Task<IActionResult> CreateContainerOrBucket(string containerOrBucketName)
    {
        var isCreated = await _blobService.CreateContainerAsync(containerOrBucketName);

        // sync
        //var isCreated = _blobService.CreateContainer(containerOrBucketName);

        return Ok(isCreated);
    }

    /// <summary>
    /// Delete Container/Bucket
    /// </summary>
    /// <param name="containerOrBucketName">Name of the Bucket/Container.</param>
    /// <returns></returns>
    [HttpDelete]
    [Route("delete-container-or-bucket/{containerOrBucketName}")]
    public async Task<IActionResult> DeleteContainerOrBucket(string containerOrBucketName)
    {
        var isDeleted = await _blobService.DeleteContainerAsync(containerOrBucketName);

        // sync
        //var isDeleted = _blobService.DeleteContainer(containerOrBucketName);

        return Ok(isDeleted);
    }



    /// <summary>
    /// Get all Containers/Buckets
    /// </summary>
    /// <returns></returns>
    [HttpGet]
    [Route("get-all-containers-or-buckets")]
    public async Task<IActionResult> GetAllContainersOrBuckets()
    {
        var containers = await _blobService.GetAllContainersAsync();

        // sync
        //var containers = _blobService.GetAllContainers();

        return Ok(containers);
    }

    /// <summary>
    /// Delete all Containers/Buckets
    /// </summary>
    /// <returns></returns>
    [HttpDelete]
    [Route("delete-all-containers-or-buckets")]
    public async Task<IActionResult> DeleteAllContainersOrBuckets()
    {
        var isDeleted = await _blobService.DeleteAllContainersAsync();

        // sync
        //var isDeleted = _blobService.DeleteAllContainers();

        return Ok(isDeleted);
    }

    #endregion
}
```


## Todo List :clipboard:

#### Storage Providers

- [x] Azure
- [x] AmazonS3
- [x] Google Cloud
- [x] File System
- [x] Kvpbase

#### Basic Storage API

- [x] Get Blob SAS



#### Coming soon
- Get Container/Bucket size in bytes
- Get number of total items/files in Container/Bucket


---



## Support :telephone:
> Reach out to me at one of the following places!

- Email :envelope: at <a href="mailto:toaashishpatel@gmail.com" target="_blank">`toaashishpatel@gmail.com`</a>
- NuGet :package: at <a href="https://www.nuget.org/profiles/iamaashishpatel" target="_blank">`@iamaashishpatel`</a>



## Authors :boy:

* **Ashish Patel** - [A-Patel](https://github.com/a-patel)


##### Connect with me

| Linkedin | GitHub | Facebook | Twitter | Instagram | Tumblr | Website |
|----------|----------|----------|----------|----------|----------|----------|
| [![linkedin](https://cdnjs.cloudflare.com/ajax/libs/foundicons/3.0.0/svgs/fi-social-linkedin.svg)](https://www.linkedin.com/in/iamaashishpatel) | [![github](https://cdnjs.cloudflare.com/ajax/libs/foundicons/3.0.0/svgs/fi-social-github.svg)](https://github.com/a-patel) | [![facebook](https://cdnjs.cloudflare.com/ajax/libs/foundicons/3.0.0/svgs/fi-social-facebook.svg)](https://www.facebook.com/aashish.mrcool) | [![twitter](https://cdnjs.cloudflare.com/ajax/libs/foundicons/3.0.0/svgs/fi-social-twitter.svg)](https://twitter.com/aashish_mrcool) | [![instagram](https://cdnjs.cloudflare.com/ajax/libs/foundicons/3.0.0/svgs/fi-social-instagram.svg)](https://www.instagram.com/iamaashishpatel/) | [![tumblr](https://cdnjs.cloudflare.com/ajax/libs/foundicons/3.0.0/svgs/fi-social-tumblr.svg)](https://iamaashishpatel.tumblr.com/) | [![website](https://cdnjs.cloudflare.com/ajax/libs/foundicons/3.0.0/svgs/fi-social-blogger.svg)](http://aashishpatel.co.nf/) |
| | | | | | |



## Donations :dollar:

[![Buy Me A Coffee](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/iamaashishpatel)



## License :lock:

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details

