# LiteX HealthChecks
> LiteXHealthChecks is very small yet powerful and high-performance library used to check the status of a component in the application, such as a backend service, database or some internal state.


## Health checks for  :books:
- [Amazon S3](docs/AmazonS3.md) - coming soon
- [Azure KeyVault](docs/AzureKeyVault.md) - coming soon
- [Azure ServiceBus](docs/AzureServiceBus.md)
- [Azure Blob Storage](docs/AzureBlobStorage.md)
- [Azure File Storage](docs/AzureFileStorage.md) - coming soon
- [Azure Queue Storage](docs/AzureQueueStorage.md)
- [CosmosDB](docs/CosmosDB.md) - coming soon
- [MongoDB](docs/MongoDB.md)
- [MySql](docs/MySql.md)
- [MariaDB](docs/MariaDB.md)
- [PostgreSql](docs/PostgreSql.md)
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
PM> Install-Package LiteX.HealthChecks.CosmosDB
PM> Install-Package LiteX.HealthChecks.MongoDB
PM> Install-Package LiteX.HealthChecks.MySql
PM> Install-Package LiteX.HealthChecks.MariaDB
PM> Install-Package LiteX.HealthChecks.PostgreSql
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
            .AddCheck<OtherHealthCheck>("other")
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



#### Coming soon
- Many health check for other services


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

