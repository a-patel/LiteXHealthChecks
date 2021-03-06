# LiteX HealthChecks

> LiteXHealthChecks is very small yet powerful and high-performance library used to check the status of a component in the application, such as a backend service, database or some internal state.





## Health checks for  :books:

- [SqlServer](docs/SqlServer.md) [![](https://img.shields.io/nuget/dt/LiteX.HealthChecks.SqlServer.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.SqlServer/) [![](https://img.shields.io/nuget/v/LiteX.HealthChecks.SqlServer.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.SqlServer/)
- [MySql](docs/MySql.md) [![](https://img.shields.io/nuget/dt/LiteX.HealthChecks.MySql.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.MySql/) [![](https://img.shields.io/nuget/v/LiteX.HealthChecks.MySql.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.MySql/)
- [PostgreSql](docs/PostgreSql.md) [![](https://img.shields.io/nuget/dt/LiteX.HealthChecks.PostgreSql.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.PostgreSql/) [![](https://img.shields.io/nuget/v/LiteX.HealthChecks.PostgreSql.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.PostgreSql/)
- [MariaDB](docs/MariaDB.md) [![](https://img.shields.io/nuget/dt/LiteX.HealthChecks.MariaDB.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.MariaDB/) [![](https://img.shields.io/nuget/v/LiteX.HealthChecks.MariaDB.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.MariaDB/)
- [MongoDB](docs/MongoDB.md) [![](https://img.shields.io/nuget/dt/LiteX.HealthChecks.MongoDb.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.MongoDb/) [![](https://img.shields.io/nuget/v/LiteX.HealthChecks.MongoDb.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.MongoDb/)
- [DynamoDB](docs/DynamoDB.md) [![](https://img.shields.io/nuget/dt/LiteX.HealthChecks.DynamoDB.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.DynamoDB/) [![](https://img.shields.io/nuget/v/LiteX.HealthChecks.DynamoDB.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.DynamoDB/)
- [CosmosDB](docs/CosmosDB.md) [![](https://img.shields.io/nuget/dt/LiteX.HealthChecks.CosmosDB.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.CosmosDB/) [![](https://img.shields.io/nuget/v/LiteX.HealthChecks.CosmosDB.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.CosmosDB/)
- [Amazon S3](docs/AmazonS3.md) [![](https://img.shields.io/nuget/dt/LiteX.HealthChecks.AmazonS3.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.AmazonS3/) [![](https://img.shields.io/nuget/v/LiteX.HealthChecks.AmazonS3.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.AmazonS3/)
- [Azure KeyVault](docs/AzureKeyVault.md) [![](https://img.shields.io/nuget/dt/LiteX.HealthChecks.AzureKeyVault.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.AzureKeyVault/) [![](https://img.shields.io/nuget/v/LiteX.HealthChecks.AzureKeyVault.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.AzureKeyVault/)
- [Azure ServiceBus](docs/AzureServiceBus.md) [![](https://img.shields.io/nuget/dt/LiteX.HealthChecks.AzureServiceBus.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.AzureServiceBus/) [![](https://img.shields.io/nuget/v/LiteX.HealthChecks.AzureServiceBus.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.AzureServiceBus/)
- [Azure Blob Storage](docs/AzureBlobStorage.md) [![](https://img.shields.io/nuget/dt/LiteX.HealthChecks.AzureStorage.Blob.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.AzureStorage.Blob/) [![](https://img.shields.io/nuget/v/LiteX.HealthChecks.AzureStorage.Blob.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.AzureStorage.Blob/)
- [Azure Queue Storage](docs/AzureQueueStorage.md) [![](https://img.shields.io/nuget/dt/LiteX.HealthChecks.AzureStorage.Queue.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.AzureStorage.Queue/) [![](https://img.shields.io/nuget/v/LiteX.HealthChecks.AzureStorage.Queue.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.AzureStorage.Queue/)
- [Redis](docs/Redis.md) [![](https://img.shields.io/nuget/dt/LiteX.HealthChecks.Redis.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.Redis/) [![](https://img.shields.io/nuget/v/LiteX.HealthChecks.Redis.svg)](https://www.nuget.org/packages/LiteX.HealthChecks.Redis/)



## Features :pager:

- Easy to use
- Very light weight
- Latest SDKs
- .NETStandard 2.0



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
PM> Install-Package LiteX.HealthChecks.CosmosDB
PM> Install-Package LiteX.HealthChecks.MongoDB
PM> Install-Package LiteX.HealthChecks.MySql
PM> Install-Package LiteX.HealthChecks.MariaDB
PM> Install-Package LiteX.HealthChecks.PostgreSql
PM> Install-Package LiteX.HealthChecks.DynamoDB
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
      "CosmosDB": "--REPLACE WITH YOUR CONNECTION STRING--",
      "MongoDB": "--REPLACE WITH YOUR CONNECTION STRING--",
      "MySql": "--REPLACE WITH YOUR CONNECTION STRING--",
      "MariaDB": "--REPLACE WITH YOUR CONNECTION STRING--",
      "PostgreSql": "--REPLACE WITH YOUR CONNECTION STRING--",
      "DynamoDB": "--REPLACE WITH YOUR CONNECTION STRING--",
      "Redis": "--REPLACE WITH YOUR CONNECTION STRING--",
      "SqlServer": "--REPLACE WITH YOUR CONNECTION STRING--"
    }
  },
  "AmazonS3": {
    "AccessKey": "--REPLACE WITH YOUR AccessKey--",
    "SecretKey": "--REPLACE WITH YOUR SecretKey--",
    "BucketName": "--REPLACE WITH YOUR BucketName--"
  },
  "DynamoDB": {
    "AccessKey": "--REPLACE WITH YOUR AccessKey--",
    "SecretKey": "--REPLACE WITH YOUR SecretKey--",
    //"RegionEndpoint": "--REPLACE WITH YOUR RegionEndpoint--" // USE 'Amazon.RegionEndpoint.CNNorth1' in configuration code
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
                .UseKeyVaultUrl(Configuration["AzureKeyVault:KeyVaultUrl"])
                .AddSecret("my-secret")
                .UseClientSecrets(Configuration["AzureKeyVault:ClientId"], Configuration["AzureKeyVault:ClientSecret"]);
            }, name: "azure-keyvault");

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddAzureKeyVault(options =>
            {
                options
                .UseKeyVaultUrl(Configuration["AzureKeyVault:KeyVaultUrl"])
                .UseClientSecrets("client", "secret");
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

        // 1: Use default configuration
        services.AddHealthChecks()
            .AddAzureBlobStorage(Configuration["Data:ConnectionStrings:AzureBlobStorage"]);

        // OR
        // 2: With all optional configuration
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

        #region CosmosDB

        // 1: Use default configuration
        services.AddHealthChecks()
            .AddCosmosDB(Configuration["Data:ConnectionStrings:CosmosDB"]);

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddCosmosDB(
                connectionString: Configuration["Data:ConnectionStrings:CosmosDB"],
                name: "cosmosdb",
                failureStatus: HealthStatus.Unhealthy,
                tags: new string[] { "db", "nosql", "cosmosdb" });

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

        #region MariaDB

        // 1: Use default configuration
        services.AddHealthChecks()
            .AddMariaDB(Configuration["Data:ConnectionStrings:MariaDB"]);

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddMariaDB(
                connectionString: Configuration["Data:ConnectionStrings:MariaDB"],
                name: "mariadb",
                failureStatus: HealthStatus.Unhealthy,
                tags: new string[] { "db", "sql", "mariadb" });

        #endregion

        #region PostgreSql

        // 1: Use default configuration
        services.AddHealthChecks()
            .AddPostgreSql(Configuration["Data:ConnectionStrings:PostgreSql"]);

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddPostgreSql(
                connectionString: Configuration["Data:ConnectionStrings:PostgreSql"],
                name: "postgresql",
                failureStatus: HealthStatus.Unhealthy,
                tags: new string[] { "db", "sql", "postgresql" });

        #endregion

        #region DynamoDB

        // 1: Use default configuration
        services.AddHealthChecks()
            .AddDynamoDB(options =>
            {
                options.AccessKey = Configuration["DynamoDB:AccessKey"];
                options.SecretKey = Configuration["DynamoDB:SecretKey"];
                options.RegionEndpoint = Amazon.RegionEndpoint.CNNorth1;
            }, name: "dynamodb");

        // OR
        // 2: With all optional configuration
        services.AddHealthChecks()
            .AddDynamoDB(options =>
            {
                options.AccessKey = Configuration["DynamoDB:AccessKey"];
                options.SecretKey = Configuration["DynamoDB:SecretKey"];
                options.RegionEndpoint = Amazon.RegionEndpoint.CNNorth1;
            },
            name: "dynamodb",
            failureStatus: HealthStatus.Degraded,
            tags: new string[] { "nosql", "dynamodb", "aws-dynamodb", "amazon-dynamodb" });

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

        #region All in one

        services.AddHealthChecks()
            .AddSqlServer(connectionString: Configuration["Data:ConnectionStrings:Sample"])
            .AddCheck<RandomHealthCheck>("random")
            .AddAzureServiceBusQueue("Endpoint=sb://MYBUS.servicebus.windows.net/;SharedAccessKeyName=policy;", "que1")
            .AddAzureServiceBusTopic("Endpoint=sb://unaidemo.servicebus.windows.net/;SharedAccessKeyName=olicy;", "to1");

        #endregion

        services.AddMvc()
            .SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
    }

    public void Configure(IApplicationBuilder app, IHostingEnvironment env)
    {
        app.UseHealthChecks("/health");

        app.UseMvcWithDefaultRoute();
    }
}
```



#### Coming soon

- Many health check for other services
- .NET Standard 2.1 support
- .NET 5.0 support





---





## Give a Star! :star:

Feel free to request an issue on github if you find bugs or request a new feature. Your valuable feedback is much appreciated to better improve this project. If you find this useful, please give it a star to show your support for this project.



## Support :telephone:

> Reach out to me at one of the following places!

- Email :envelope: at <a href="mailto:toaashishpatel@gmail.com" target="_blank">`toaashishpatel@gmail.com`</a>
- NuGet :package: at <a href="https://www.nuget.org/profiles/iamaashishpatel" target="_blank">`@iamaashishpatel`</a>



## Author :boy:

* **Ashish Patel** - [A-Patel](https://github.com/a-patel)


##### Connect with me

| Linkedin | Website | Medium | NuGet | GitHub | Microsoft | Facebook | Twitter | Instagram | Tumblr |
|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|
| [![linkedin](https://img.icons8.com/ios-filled/96/000000/linkedin.png)](https://www.linkedin.com/in/iamaashishpatel) | [![website](https://img.icons8.com/wired/96/000000/domain.png)](https://aashishpatel.netlify.app/) | [![medium](https://img.icons8.com/ios-filled/96/000000/medium-monogram.png)](https://medium.com/@iamaashishpatel) | [![nuget](https://img.icons8.com/windows/96/000000/nuget.png)](https://nuget.org/profiles/iamaashishpatel) | [![github](https://img.icons8.com/ios-glyphs/96/000000/github.png)](https://github.com/a-patel) | [![microsoft](https://img.icons8.com/ios-filled/90/000000/microsoft.png)](https://docs.microsoft.com/en-us/users/iamaashishpatel) | [![facebook](https://img.icons8.com/ios-filled/90/000000/facebook.png)](https://www.facebook.com/aashish.mrcool) | [![twitter](https://img.icons8.com/ios-filled/96/000000/twitter.png)](https://twitter.com/aashish_mrcool) | [![instagram](https://img.icons8.com/ios-filled/90/000000/instagram-new.png)](https://www.instagram.com/iamaashishpatel/) | [![tumblr](https://img.icons8.com/ios-filled/96/000000/tumblr--v1.png)](https://iamaashishpatel.tumblr.com/) |



## Donate :dollar:

If you find this project useful — or just feeling generous, consider buying me a beer or a coffee. Cheers! :beers: :coffee:

| PayPal | BMC | Patreon |
| ------------- | ------------- | ------------- |
| [![PayPal](https://www.paypalobjects.com/webstatic/en_US/btn/btn_donate_pp_142x27.png)](https://www.paypal.me/iamaashishpatel) | [![Buy Me A Coffee](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/iamaashishpatel) | [![Patreon](https://c5.patreon.com/external/logo/become_a_patron_button.png)](https://www.patreon.com/iamaashishpatel) |



## License :lock:

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
