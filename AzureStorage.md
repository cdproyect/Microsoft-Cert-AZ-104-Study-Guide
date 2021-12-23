- [Azure Storage](#azure-storage)
  - [Azure storage services](#azure-storage-services)
    - [Storage account kinds](#storage-account-kinds)
    - [Replication strategies](#replication-strategies)
    - [Access storage](#access-storage)
    - [Configure a custom domain](#configure-a-custom-domain)
    - [Secure storage endpoints](#secure-storage-endpoints)
  - [Blob storage](#blob-storage)
    - [Blob service resources](#blob-service-resources)
    - [Blob access tiers](#blob-access-tiers)
    - [Blob lifecycle management rules](#blob-lifecycle-management-rules)
    - [Blob object replication](#blob-object-replication)
    - [Blob types](#blob-types)
    - [Blob upload tools](#blob-upload-tools)
    - [Blob Storage pricing](#blob-storage-pricing)
    - [Storage security strategies](#storage-security-strategies)
    - [Authorization options](#authorization-options)
    - [Identify URI and SAS paramenters](#identify-uri-and-sas-paramenters)
    - [Storage service encryption](#storage-service-encryption)
      - [Customer managed keys](#customer-managed-keys)
    - [Storage security best practices](#storage-security-best-practices)
      - [Risks](#risks)
      - [Recommendations](#recommendations)
    - [Storage access policies](#storage-access-policies)
    - [Storage SAS Example with C](#storage-sas-example-with-c)
  - [Azure Files and Azure File Sync](#azure-files-and-azure-file-sync)
    - [Compare files to blobs](#compare-files-to-blobs)
    - [Manage file shares](#manage-file-shares)
      - [Secure transfer required](#secure-transfer-required)
    - [File share snapshots](#file-share-snapshots)
      - [When to use snapshots](#when-to-use-snapshots)
    - [File Sync](#file-sync)
    - [File Sync components](#file-sync-components)
    - [Deploy Azure file Sync](#deploy-azure-file-sync)
# [Azure Storage](https://docs.microsoft.com/en-us/learn/modules/configure-storage-accounts/1-introduction)

Azure Storage is Microsoft's cloud storage solution for modern data storage scenarios. Azure Storage offers a massively scalable object store for data objects, a file system service for the cloud, a messaging store for reliable messaging, and a NoSQL store. Azure Storage is:

- **Durable and highly available.** Redundancy ensures that your data is safe during transient hardware failures. You replicate data across datacenters or geographical regions for protection from local catastrophe or natural disaster. Data replicated remains highly available during an unexpected outage.
- **Secure.** All data written to Azure Storage is encrypted by the service. Azure Storage provides you with fine-grained control over who has access to your data.
- **Scalable.** Azure Storage is designed to be massively scalable to meet the data storage and performance needs of today's applications.
- **Managed.** Microsoft Azure handles hardware maintenance, updates, and critical issues for you.
- **Accessible.** Data in Azure Storage is accessible from anywhere in the world over HTTP or HTTPS. Microsoft provides SDKs for Azure Storage in a various languages .NET, Java, Node.js, Python, PHP, Ruby, Go, and REST API. Azure Storage supports scripting in Azure PowerShell or Azure CLI. And the Azure portal and Azure Storage Explorer offer easy visual solutions for working with your data.

Azure Storage is a service that you can use to store files, messages, tables, and other types of information. You use Azure storage for applications like file shares. Developers use Azure storage for working data. Working data includes websites, mobile apps, and desktop applications. Azure storage is also used by IaaS virtual machines, and PaaS cloud services. You can generally think of Azure storage in three categories.

- **Storage for Virtual Machines.** Virtual machine storage includes disks and files. Disks are persistent block storage for Azure IaaS virtual machines. Files are fully managed file shares in the cloud.
- **Unstructured Data.** Unstructured data includes Blobs and Data Lake Store. Blobs are highly scalable, REST-based cloud object store. Data Lake Store is Hadoop Distributed File System (HDFS) as a service.
- **Structured Data.** Structured data includes Tables, Cosmos DB, and Azure SQL DB. Tables are a key/value, autoscaling NoSQL store. Cosmos DB is a globally distributed database service. Azure SQL DB is a fully managed database-as-a-service built on SQL.

General purpose storage accounts have two tiers: **Standard** and **Premium**.

- **Standard** storage accounts are backed by magnetic drives (HDD) and provide the lowest cost per GB. Use Standard storage for applications that require bulk storage or where data is infrequently accessed.
- **Premium** storage accounts are backed by solid-state drives (SSD) and offer consistent low-latency performance. Use Premium storage for Azure virtual machine disks with I/O-intensive applications, like databases.

---
Note

You can't convert a Standard storage account to a Premium storage or vice versa. You must create a new storage account with the desired type and copy data, if applicable, to a new storage account

---

## Azure storage services

Azure Storage includes these data services, each of which is accessed through a storage account.

- **Azure Containers (Blobs):** A massively scalable object store for text and binary data. It is ideal for:
  - Serving images or documents directly to a browser.
  - Storing files for distributed access.
  - Streaming video and audio.
  - Storaing data for backup and restore, disaster recovery, and archiving.
  - Storing data for analysis by an on-premises or Azure-hosted service.
- **Azure Files:** Managed file shares for cloud or on-premises deployments, that can be accessed by using the standard Server Message Block (SMB) protocol. One thing that distinguishes Azure Files from files on a corporate file share is that you can access the files from anywhere in the world using a URL that points to the file and includes a shared access signature (SAS) token. You can generate SAS tokens; they allow specific access to a private asset for a specific amount of time.
File shares can be used for many common scenarios:
  - Many on-premises applications use file shares. this feature makes it easier to migrate those applications that share data to Azure. If you mount the file share to the same drive letter that the on-premises application uses, the part of your application that accesses the file share should work with minimal, if any, changes.
  - Configuration files can be stored on a file share and accessed from multiple VMS. tools and utilities used by multiple developers in a group can be stored on a file share, ensuring that everybody can find them, and that they use the same version.
  - Diagnostic logs, metrics, and crash dumps are just three examples of data that can be written to a file share and processed or analyzed later.  

- **Azure Queues:** A messaging store for reliable messaging between application components. Queue messages can be up to 64 KB in size, and a queue can contain millions of messages. Queues are used to store lists of messages to be processed asynchronously.

- **Azure Tables:** A NoSQL store for schemaless storage of structured data. Azure Table storage is now part of Azure Cosmos DB. In addition to the existing Azure Table storage service, there is a new Azure Cosmos DB Table API offering that provides throughput-optimized tables, global distribution, and automatic secondary indexes. Table storage is ideal for storing structured, non-relational data.

### Storage account kinds

The kinds of storage accounts are:

|Storage account| Recommended usage
| - | - |
|Standard general-purpose v2| Most scenarios including Blob, File, Queue, Table, and Data Lake Storage.
|Premium block blobs| Block blob scenarios with high transactions rates, or scenarios that use smaller objects or require consistently low storage latency.
|Premium file shares| Enterprise or high-performance file share applications.
|Premium page blobs| Premium high-performance page blob scenarios.

---
Note

All storage accounts are encrypted using Storage Service Encryption (SSE) for data at rest

---

### Replication strategies

The following table provides a quick overview of the scope of durability and availability that each replication strategy will provide you for a given type of event (or event of similar impact).

|Scenario|LRS|ZRS|GRS/RA-GRS|GZRS/RA-GZRS|
| - | - | - | - | - |
| Node unavailability within a data center | Yes | Yes | Yes | Yes
| An entire data center (zonal or non-zonal) becomes unavailable | No | Yes | Yes | Yes
| A region-wide outage | No | No | Yes | Yes
| Read access to your data (in a remote, geo-replicated region) in the event of region-wide unavailability | No | No | Yes(with RA-GRS) | Yes(with RA-GZRS)
| Available in storage account types | GPv1, GPv2,Blob | GPv2 | GPv1, GPv2, Blob | GPv2
| Benefits | Lowest-cost | Synchronously replicates your data across three (3) storage clusters in a single region | Higher level of durability even if ther is a regional outage 99.9999999999999999% (16 9s) durability | Combines the high availability of zon-redundant storage with protection from gregional outages as provided by geo-redundant storage. You can continue to read and write data if an availability zone becomes unavailable or is unrecoverable. 

### Access storage

Every object that you store in Azure Storage has a unique URL address. The storage account name forms the subdomain of that address. The combination of subdomain and domain name, which is specific to each service, forms an endpoint for your storage account.

For example, if your storage account is named mystorageaccount, then the default endpoints for your storage account are:

- Container service: //mystorageaccount.blob.core.windows.net
- Table service: //mystorageaccount.table.core.windows.net
- Queue service: //mystorageaccount.queue.core.windows.net
- File service: //mystorageaccount.file.core.windows.net

The URL for accessing an object in a storage account is built by appending the object's location in the storage account to the endpoint. For example, to access myblob in the mycontainer, use this format: //mystorageaccount.blob.core.windows.net/mycontainer/myblob.

### [Configure a custom domain](https://docs.microsoft.com/en-us/learn/modules/configure-storage-accounts/6-access-storage)

You can configure a custom domain for accessing blob data in your Azure storage account. As mentioned previously, the default endpoint for Azure Blob storage is <storage-account-name>.blob.core.windows.net. You can also use the web endpoint that's generated as a part of the static websites feature. If you map a custom domain and subdomain, such as www.contoso.com, to the blob or web endpoint for your storage account, your users can use that domain to access blob data in your storage account. There are two ways to configure this service: Direct CNAME mapping and an intermediary domain.

### Secure storage endpoints 

The steps necessary to restrict network access to Azure services varies across services. For accessing a storage account, you would use the Firewalls and virtual networks blade to add the virtual networks that will have access. Notice you can also configure to allow access to one or more public IP ranges.

## Blob storage

### Blob service resources

Blog storage offers three types of resources:
- The storage account
- Containers in the storage account
- Blobs in a container

A container provides a grouping of a set of blobs. All blobs must be in a container. An account can contain an unlimited number of containers. A container can store an unlimited number of blobs. 

**Name:** The name may only contain lowercase letters, numbers, and hyphens, and must begin with a letter or a number. The name must also be between 3 and 63 characters long.

**Public access level:* Specifies whether data in the container may be accessed publicly. By default, container data is private to the account owner.

- Use **Private** to ensure there is no anonymous access to the container and blobs.
- Use **Blob** to allow anonymous public read access for blobs only.
- Use **Container** to allow anonymous public read and list access to the entire container, including the blobs.

### Blob access tiers

Azure Storage provides different options for accessing block blob data (as shown in the screenshot), based on usage patterns. Each access tier in Azure Storage is optimized for a particular pattern of data usage. By selecting the correct access tier for your needs, you can store your block blob data in the most cost-effective manner.

- **Hot.** The Hot tier is optimized for frequent access of objects in the storage account. New storage accounts are created in the Hot tier by default.

- **Cool.** The Cool tier is optimized for storing large amounts of data that is infrequently accessed and stored for at least 30 days. Storing data in the Cool tier is more cost-effective, but accessing that data may be more expensive than accessing data in the Hot tier.

- **Archive.** The Archive tier is optimized for data that can tolerate several hours of retrieval latency and will remain in the Archive tier for at least 180 days. The Archive tier is the most cost-effective option for storing data, but accessing that data is more expensive than accessing data in the Hot or Cool tiers.

### Blob lifecycle management rules

Data sets have unique lifecycles. Early in the lifecycle, people access some data often. But the need for access drops drastically as the data ages. Some data stays idle in the cloud and is rarely accessed once stored. Some data expires days or months after creation, while other data sets are actively read and modified throughout their lifetimes. Azure Blob storage lifecycle management offers a rich, rule-based policy for GPv2 and Blob storage accounts. Use the policy to transition your data to the appropriate access tiers or expire at the end of the data's lifecycle.

The lifecycle management policy lets you:

- Transition blobs to a cooler storage tier (hot to cool, hot to archive, or cool to archive) to optimize for performance and cost.
- Delete blobs at the end of their lifecycles.
- Define rules to be run once per day at the storage account level.
- Apply rules to containers or a subset of blobs.

### Blob object replication

Object replication asynchronously copies block blobs in a container according to rules that you configure. The contents of the blob, any versions associated with the blob, and the blob's metadata and properties are all copied from the source container to the destination container.

**Scenarios**

- Minimizing latency. Object replication can reduce latency for read requests by enabling clients to consume data from a region that is in closer physical proximity.
- Increase efficiency for compute workloads. With object replication, compute workloads can process the same sets of block blobs in different regions.
- Optimizing data distribution. You can process or analyze data in a single location and then replicate just the results to other regions.
- Optimizing costs. After your data has been replicated, you can reduce costs by moving it to the archive tier using life-cycle management policies.

**Considerations**

- Object replication requires that blob versioning is enabled on both the source and destination accounts.
- Object replication doesn't support blob snapshots. Any snapshots on a blob in the source account are not replicated to the destination account.
- Object replication is supported when the source and destination accounts are in the hot or cool tier. The source and destination accounts may be in different tiers.
- When you configure object replication, you create a replication policy that specifies the source storage account and the destination account. A replication policy includes one or more rules that specify a source container and a destination container and indicate which block blobs in the source container will be replicated.

### Blob types

A blob can be any type and size file. Azure Storage offers three types of blobs: block blobs, page blobs, and append blobs. You specify the blob type and access tier when you create the blob.

- **Block blobs (default)** consist of blocks of data assembled to make a blob. Most scenarios using Blob storage employ block blobs. Block blobs are ideal for storing text and binary data in the cloud, like files, images, and videos.
- **Append blobs** are like block blobs in that they are made up of blocks, but they are optimized for append operations, so they are useful for logging scenarios.
- **Page blobs** can be up to 8 TB in size and are more efficient for frequent read/write operations. Azure virtual machines use page blobs as OS and data disks.

### Blob upload tools

There are multiple methods to upload data to blob storage, including the following methods:

- **AzCopy** is an easy-to-use command-line tool for Windows and Linux that copies data to and from Blob storage, across containers, or across storage accounts.
- **The Azure Storage Data Movement library** is a .NET library for moving data between Azure Storage services. The AzCopy utility is built with the Data Movement library.
- **Azure Data Factory** supports copying data to and from Blob storage by using the account key, shared access signature, service principal, or managed identities for Azure resources authentications.
- **Blobfuse** is a virtual file system driver for Azure Blob storage. You can use blobfuse to access your existing block blob data in your Storage account through the Linux file system.
- **Azure Data Box Disk** is a service for transferring on-premises data to Blob storage when large datasets or network constraints make uploading data over the wire unrealistic. You can use Azure Data Box Disk to request solid-state disks (SSDs) from Microsoft. You can then copy your data to those disks and ship them back to Microsoft to be uploaded into Blob storage.
- **The Azure Import/Export** service provides a way to export large amounts of data from your storage account to hard drives that you provide and that Microsoft then ships back to you with your data.
- **Azure Storage Explorer**

### Blob Storage pricing

All storage accounts use a pricing model for blob storage based on the tier of each blob. When using a storage account, the following billing considerations apply:

- **Performance tiers:** The storage tier determines the amount of data stored and the cost of storing the data. As the performance tier gets cooler, the per-gigabyte cost decreases.
- **Data access costs:** Data access charges increase as the tier gets cooler. For data in the cool and archive storage tier, you are charged a per-gigabyte data access charge for reads.
- **Transaction costs:** There is a per-transaction charge for all tiers. The charge increases as the tier gets cooler.
- **Geo-Replication data transfer costs:** This charge only applies to accounts with geo-replication configured, including GRS and RA-GRS. Geo-replication data transfer incurs a per-gigabyte charge.
- **Outbound data transfer costs:** Outbound data transfers (data that is transferred out of an Azure region) incur billing for bandwidth usage on a per-gigabyte basis. This billing is consistent with general-purpose storage accounts.
- **Changing the storage tier:** Changing the account storage tier from cool to hot incurs a charge equal to reading all the data existing in the storage account. However, changing the account storage tier from hot to cool incurs a charge equal to writing all the data into the cool tier (GPv2 accounts only).

### Storage security strategies

Azure Storage provides a comprehensive set of security capabilities that together enable developers to build secure applications.

- **Encryption.** All data written to Azure Storage is automatically encrypted using Storage Service Encryption (SSE).

- **Authentication.** Azure Active Directory (Azure AD) and Role-Based Access Control (RBAC) are supported for Azure Storage for both resource management operations and data operations, as follows:

  - You can assign RBAC roles scoped to the storage account to security principals and use Azure AD to authorize resource management operations such as key management.
  - Azure AD integration is supported for data operations on the Blob and Queue services.

- **Data in transit.** Data can be secured in transit between an application and Azure by using Client-Side Encryption, HTTPS, or SMB 3.0.

- **Disk encryption.** OS and data disks used by Azure virtual machines can be encrypted using Azure Disk Encryption.

- **Shared Access Signatures.** Delegated access to the data objects in Azure Storage can be granted using Shared Access Signatures.

### Authorization options

[Tutorial here](https://docs.microsoft.com/en-gb/learn/modules/control-access-to-azure-storage-with-sas/2-authorization-options-azure-storage)

Every request made against a secured resource in the Blob, File, Queue, or Table service must be authorized. Authorization ensures that resources in your storage account are accessible only when you want them to be, and only to those users or applications to whom you grant access. Options for authorizing requests to Azure Storage include:

- **Azure Active Directory (Azure AD).** Azure AD is Microsoft's cloud-based identity and access management service. With Azure AD, you can assign fine-grained access to users, groups, or applications via role-based access control (RBAC).
- **Shared Key.** Shared Key authorization relies on your account access keys and other parameters to produce an encrypted signature string that is passed on the request in the Authorization header.
- **Shared access signatures.** Shared access signatures (SAS) delegate access to a particular resource in your account with specified permissions and over a specified time interval. A shared access signature (SAS) is a URI that grants restricted access rights to Azure Storage resources. You can provide a SAS to clients who shouldn't have access to your storage account key. By distributing a SAS URI to these clients, you grant them access to a resource for a specified period of time. SAS is a secure way to share your storage resources without compromising your account keys. a SAS give you granular control over the type of access you grant to clients who have the SAS, including:
  - An account-level SAS can delegate access to multiple storage services. For example, blob, file, queue, and table.
  - An interval over which the SAS is valid, including the start time and the expiry time.
  - The permissions granted by the SAS. For example, a SAS for a blob might grant read and write permissions to that blob, but not delete permissions.
  - There are two types of SAS: **account** and **service**. 
    - The account SAS delegates access to resources in one or more of the storage services.
    - The service SAS delegates access to a resource in just one of the storage services.
  - Optionally, you can also
    - Specify an IP address or range of IP addresses from which Azure Storage will accept the SAS. For example, you might specify a range of IP addresses belonging to your organization.
    - The protocol over which Azure Storage will accept the SAS. You can use this optional parameter to restrict access to clients using HTTPS.
  - A stored access policy can provide another level of control over service-level SAS on the server side. you can group shared access signatures and provide other restrictions by using policy.
  
- **Anonymous access to containers and blobs.** You can optionally make blob resources public at the container or blob level. A public container or blob is accessible to any user for anonymous read access. Read requests to public containers and blobs do not require authorization.

### Identify URI and SAS paramenters

When you create your SAS, a URI is created using parameters and tokens. The URI consists of your Storage Resource URI and the SAS token.

Below is an example URI.

```http
https://myaccount.blob.core.windows.net/?restype=service&comp=properties&sv=2015-04-05&ss=bf&srt=s&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https &sig=F%6GRVAZ5Cdj2Pw4txxxxx
```
Each parameter has a specific meaning

|Name|SAS Portion| Description
| - | - | - |
| Resource URI | https://myaccount.blob.core.windows.net/?restype=service&comp=properties | The Blob service endpoint, with parameters for getting service properties (when called with GET) or setting service properties (when called with SET).
| Storage services version | sv=2015-04-05 | For storage services version 2012-02-12 and later, this parameter indicates the version to use.
| Services | ss=bf | The SAS applies to the Blob and File services
| Resource types | srt=s | The SAS applies to service-level operations.
| Start time |  st=2015-04-29T22%3A18%3A26Z | Specified in UTC time. If you want the SAS to be valid immediately, omit the start time.
| Expiry time | se=2015-04-30T02%3A23%3A26Z | Specified in UTC time.
| Resource | sr=b | The resource is a blob.
| Permissions | sp=rw | The permissions grant access to read and write operations.
| IP Range | sip=168.1.5.60-168.1.5.70 | The range of IP addresses from which request will be accepted
| Protocol | spr=https | Only requests using HTTPS are permitted.
| Signature | sig=F%6GRVAZ5Cdj2Pw4tgU7IlSTkWgn7bUkkAg8P6HESXwmf%4B | Used to authenticate access to the blob. The signature is an HMAC computed over a string-to-sign and key using the SHA256 algorithm, and then encoded using Base64 encoding.

### Storage service encryption

Azure Storage Service Encryption (SSE) for data at rest protects your data by ensuring your organizational security and compliance commitments are met.

SSE automatically encrypts your data before persisting it to Azure-managed Disks, Azure Blob, Queue, Table storage, or Azure Files, and decrypts the data before retrieval.

SSE encryption, encryption at rest, decryption, and key management are transparent to users. All data written to the Azure storage platform is encrypted through 256-bit AES encryption, one of the strongest block ciphers available.

#### Customer managed keys

The Azure Key Vault can manage your encryption keys. You can create your own encryption keys and store them in a key vault, or you can use Azure Key Vault's APIs to generate encryption keys.

Customer-managed keys give you more flexibility and control. You can create, disable, audit, rotate, and define access controls.

---
Note

Customer-managed keys can be used with SSE. You can use either a new or existing key vault and key. The storage account and the key vault must be in the same region, but they can be in different subscriptions.

---

### Storage security best practices

#### Risks

When you use shared access signatures in your applications, you should be aware of two potential risks.

- If a SAS is compromised, it can be used by anyone who obtains it.
- If a SAS provided to a client application expires and the application is unable to retrieve a new SAS from your service, then the application's functionality may be hindered.

#### Recommendations

The following recommendations for using shared access signatures can help mitigate risks.

- **Always use HTTPS to create or distribute a SAS.** If a SAS is passed over HTTP and intercepted, an attacker could intercept and use the SAS. These man-in-the-middle attacks can compromise sensitive data or allow for data corruption by the malicious user.
- **Reference stored access policies where possible.** Stored access policies give you the option to revoke permissions without having to regenerate the storage account keys. Set the storage account key expiration date far out in the future.
- **Use near-term expiration times on an unplanned SAS.** In this way, even if a SAS is compromised, it's valid only for a short time. This practice is important if you can't reference a stored access policy. Near-term expiration times also limit the amount of data that can be written to a blob by limiting the time available to upload to it.
- **Have clients automatically renew the SAS if necessary.** Clients should renew the SAS well before the expiration date. Renewing early allows time for retries if the service providing the SAS is unavailable.
Be careful with SAS start time. If you set the start time for a SAS to now, then due to clock skew (differences in current time according to different machines), failures may be observed intermittently for the first few minutes. In general, set the start time to be at least 15 minutes in the past. Or, don't set it at all, which will make it valid immediately in all cases. The same generally applies to expiry time as well - remember that you may observe up to 15 minutes of clock skew in either direction on any request. For clients using a REST version prior to 2012-02-12, the maximum duration for a SAS that does not reference a stored access policy is 1 hour, and any policies specifying longer term than that will fail.
- **Be specific with the resource to be accessed.** A security best practice is to provide a user with the minimum required privileges. If a user only needs read access to a single entity, then grant them read access to that single entity, and not read/write/delete access to all entities. This also helps lessen the damage if a SAS is compromised because the SAS has less power in the hands of an attacker
- **Understand that your account will be billed for any usage, including that done with SAS.** If you provide write access to a blob, a user may choose to upload a 200-GB blob. If you've given them read access as well, they may choose to download it 10 times, incurring 2 TB in egress costs for you. Again, provide limited permissions to help mitigate the potential actions of malicious users. Use short-lived SAS to reduce this threat (but be mindful of clock skew on the end time).
- **Validate data written using SAS.** When a client application writes data to your storage account, keep in mind that there can be problems with that data. If your application requires that data be validated or authorized before it is ready to use, you should perform this validation after the data is written and before it is used by your application. This practice also protects against corrupt or malicious data being written to your account, either by a user who properly acquired the SAS, or by a user exploiting a leaked SAS.
- **Don't assume SAS is always the correct choice.** Sometimes the risks associated with a particular operation against your storage account outweigh the benefits of SAS. For such operations, create a middle-tier service that writes to your storage account after performing business rule validation, authentication, and auditing. Also, sometimes it's simpler to manage access in other ways. For example, if you want to make all blobs in a container publicly readable, you can make the container Public, rather than providing a SAS to every client for access.
- **Use Storage Analytics to monitor your application.** You can use logging and metrics to observe any spike in authentication failures due to an outage in your SAS provider service or to the inadvertent removal of a stored access policy.

### Storage access policies

You can create a stored access policy on four kinds of storage resources:

- Blob containers
- File shares
- Queues
- Tables
The stored access policy you create for a blob container can be used for all the blobs in the container and for the container itself. A stored access policy is created with the following properties:

- **Identifier:** The name you use to reference the stored access policy.
- **Start time:** A DateTimeOffset value for the date and time when the policy might start to be used. This value can be null.
- **Expiry time:** A DateTimeOffset value for the date and time when the policy expires. After this time, requests to the storage will fail with a 403 error-code message.
- **Permissions:** The list of permissions as a string that can be one or all of acdlrw.

### Storage SAS Example with C#

- [This is the link](https://github.com/MicrosoftDocs/mslearn-control-access-to-azure-storage-with-sas) to the git hub
- [This is the link to the lab](https://docs.microsoft.com/en-gb/learn/modules/control-access-to-azure-storage-with-sas/4-exercise-use-shared-access-signatures)


## Azure Files and Azure File Sync

### Compare files to blobs

File storage offers shared storage for applications using the industry standard SMB protocol. Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can also access file data in the share.

Applications running in Azure virtual machines or cloud services can mount a file storage share to access file data. This process is similar to how a desktop application would mount a typical SMB share. Any number of Azure virtual machines or roles can mount and access the File storage share simultaneously.

Common uses of file storage

- **Replace and supplement.** Azure Files can be used to completely replace or supplement traditional on-premises file servers or NAS devices.
- **Access anywhere.** Popular operating systems such as Windows, macOS, and Linux can directly mount Azure File shares wherever they are in the world.
- **Lift and shift.** Azure Files makes it easy to "lift and shift" applications to the cloud that expect a file share to store file application or user data.
- **Azure File Sync.** Azure File shares can also be replicated with Azure File Sync to Windows Servers, either on-premises or in the cloud, for performance and distributed caching of the data where it's being used.
- **Shared applications.** Storing shared application settings, for example in configuration files.
- **Diagnostic data.** Storing diagnostic data such as logs, metrics, and crash dumps in a shared location.
- **Tools and utilities.** Storing tools and utilities needed for developing or administering Azure virtual machines or cloud services.

Sometimes it is difficult to decide when to use file shares instead of blobs or disk shares. Take a minute to review this table that compares the different features.

| Feature | Description | When to use
| - | - | - |
| Azure Files | Provides an SMB interface, client libraries, and a REST interface that allows access from anywhere to stored files. | You want to "lift and shift" an application to the cloud that already uses the native file system APIs to share data between it and other applications running in Azure. You want to store development and debugging tools that need to be accessed from many virtual machines.
| Azure Blobs | Provides client libraries and a REST interface that allows unstructured data to be stored and accessed at a massive scale in block blobs.| You want your application to support streaming and random-access scenarios. You want to be able to access application data from anywhere.

Other distinguishing features, when selecting Azure files.

- Azure files are true directory objects. Azure blobs are a flat namespace.
- Azure files are accessed through file shares. Azure blobs are accessed through a container.
- Azure files provide shared access across multiple virtual machines. Azure disks are exclusive to a single virtual machine.

### Manage file shares

To access your files, you will need a storage account. After the storage account is created, provide the file share Name and the Quota. Quota refers to total size of files on the share.

#### Secure transfer required 

The secure transfer option enhances the security of your storage account by only allowing requests to the storage account by secure connection. 

### File share snapshots

Azure Files provides the capability to take share snapshots of file shares. Share snapshots capture a point-in-time, read-only copy of your data.

Share snapshot capability is provided at the file share level. Retrieval is provided at the individual file level, to allow for restoring individual files. You cannot delete a share that has share snapshots unless you delete all the share snapshots first.

Share snapshots are incremental in nature. Only the data that has changed after your most recent share snapshot is saved. Incremental snapshots minimizes the time required to create the share snapshot and saves on storage costs. Even though share snapshots are saved incrementally, you need to retain only the most recent share snapshot in order to restore the share.

#### When to use snapshots

- **Protection against application error and data corruption.** Applications that use file shares perform operations such as writing, reading, storage, transmission, and processing. When an application is misconfigured or an unintentional bug is introduced, accidental overwrite or damage can happen to a few blocks. To help protect against these scenarios, you can take a share snapshot before you deploy new application code. When a bug or application error is introduced with the new deployment, you can go back to a previous version of your data on that file share.
- **Protection against accidental deletions or unintended changes.** Imagine that you're working on a text file in a file share. After the text file is closed, you lose the ability to undo your changes. In these cases, you then need to recover a previous version of the file. You can use share snapshots to recover previous versions of the file if it's accidentally renamed or deleted.
- **General backup purposes.** After you create a file share, you can periodically create a share snapshot of the file share to use it for data backup. A share snapshot, when taken periodically, helps maintain previous versions of data that can be used for future audit requirements or disaster recovery.

### File Sync

Use Azure File Sync to centralize your organization's file shares in Azure Files, while keeping the flexibility, performance, and compatibility of an on-premises file server. Azure File Sync transforms Windows Server into a quick cache of your Azure file share. You can use any protocol that's available on Windows Server to access your data locally, including SMB, NFS, and FTPS. You can have as many caches as you need across the world.

There are many uses and advantages to file sync.

- **Lift and shift.** The ability to move applications that require access between Azure and on-premises systems. Provide write access to the same data across Windows Servers and Azure Files. This lets companies with multiple offices have a need to share files with all offices.
- **Branch Offices.** Branch offices need to backup files, or you need to setup a new server that will connect to Azure storage.
- **Backup and Disaster Recovery.** Once File Sync is implemented, Azure Backup will back up your on-premises data. Also, you can restore file metadata immediately and recall data as needed for rapid disaster recovery.
- **File Archiving.** Only recently accessed data is located on local servers. Non-used data moves to Azure in what is called Cloud Tiering.

---
Note

Cloud tiering is an optional feature of Azure File Sync in which frequently accessed files are cached locally on the server while all other files are tiered to Azure Files based on policy settings. When a file is tiered, the Azure File Sync file system replaces the file locally with a pointer, or reparse point. The reparse point represents a URL to the file in Azure Files. When a user opens a tiered file, Azure File Sync seamlessly recalls the file data from Azure Files without the user needing to know that the file is actually stored in Azure. Cloud Tiering files will have greyed icons with an offline O file attribute to let the user know the file is only in Azure.

---

### File Sync components

To gain the most from Azure File Sync, it's important to understand the terminology.

**Storage Sync Service.** The Storage Sync Service is the top-level Azure resource for Azure File Sync. The Storage Sync Service resource is a peer of the storage account resource, and can similarly be deployed to Azure resource groups. A distinct top-level resource from the storage account resource is required because the Storage Sync Service can create sync relationships with multiple storage accounts via multiple sync groups. A subscription can have multiple Storage Sync Service resources deployed.

**Sync group.** A sync group defines the sync topology for a set of files. Endpoints within a sync group are kept in sync with each other. If for example, you have two distinct sets of files that you want to manage with Azure File Sync, you would create two sync groups and add different endpoints to each sync group. A Storage Sync Service can host as many sync groups as you need.

**Registered server.** The registered server object represents a trust relationship between your server (or cluster) and the Storage Sync Service. You can register as many servers to a Storage Sync Service instance as you want.

**Azure File Sync agent.** The Azure File Sync agent is a downloadable package that enables Windows Server to be synced with an Azure file share. The Azure File Sync agent has three main components:

- FileSyncSvc.exe: The background Windows service that is responsible for monitoring changes on server endpoints, and for initiating sync sessions to Azure.

- StorageSync.sys: The Azure File Sync file system filter, which is responsible for tiering files to Azure Files (when cloud tiering is enabled).

- PowerShell management cmdlets: PowerShell cmdlets that you use to interact with the Microsoft.StorageSync Azure resource provider. You can find these at the following (default) locations:

  - C:\Program Files\Azure\StorageSyncAgent\StorageSync.Management.PowerShell.Cmdlets.dll
  - C:\Program Files\Azure\StorageSyncAgent\StorageSync.Management.ServerCmdlets.dll


- **Server endpoint.** A server endpoint represents a specific location on a registered server, such as a folder on a server volume. Multiple server endpoints can exist on the same volume if their namespaces do not overlap (for example, F:\sync1 and F:\sync2). You can configure cloud tiering policies individually for each server endpoint. You can create a server endpoint via a mountpoint. Note, mountpoints within the server endpoint are skipped. You can create a server endpoint on the system volume but, there are two limitations if you do so:

  - Cloud tiering cannot be enabled.
  - Rapid namespace restore (where the system quickly brings down the entire namespace and then starts to recall content) is not performed.
  - 
- **Cloud endpoint.** A cloud endpoint is an Azure file share that is part of a sync group. The entire Azure file share syncs, and an Azure file share can be a member of only one cloud endpoint. Therefore, an Azure file share can be a member of only one sync group. If you add an Azure file share that has an existing set of files as a cloud endpoint to a sync group, the existing files are merged with any other files that are already on other endpoints in the sync group.

### Deploy Azure file Sync

There are several high-level steps for configuring File Sync.

1. **Deploy the Storage Sync Service.** The Storage Sync Service can be deployed from the Azure portal. You will need to provide Name, Subscription, Resource Group, and Location.
1. **Prepare Windows Server to use with Azure File Sync.** For each server that you intend to use with Azure File Sync, including server nodes in a Failover Cluster, you will need to configure the server. Preparation steps include temporarily disabling Internet Explorer Enhanced Security and ensuring you have latest PowerShell version.
1. **Install the Azure File Sync Agent.** The Azure File Sync agent is a downloadable package that enables Windows Server to be synced with an Azure file share. The Azure File Sync agent installation package should install relatively quickly. We recommend that you keep the default installation path and that you enable Microsoft Update to keep Azure File Sync up to date.
1. **Register Windows Server with Storage Sync Service.** When the Azure File Sync agent installation is finished, the Server Registration UI automatically opens. Registering Windows Server with a Storage Sync Service establishes a trust relationship between your server (or cluster) and the Storage Sync Service. Registration requires your Subscription ID, Resource Group, and Storage Sync Service (created in step 1). A server (or cluster) can be registered with only one Storage Sync Service at a time.