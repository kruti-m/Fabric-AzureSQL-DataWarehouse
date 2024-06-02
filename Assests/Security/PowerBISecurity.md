# In this article we will cover:

* [PowerBI Security](#powerbi-security)
  * [PowerBI Embedded Analytics](#power-bi-embedded-analytics)

# PowerBi Security

Power BI is an online software service (SaaS, or Software as a Service) offering as part 
of Microsoft Fabric that lets you easily and quickly create self-service Business 
Intelligence dashboards, reports, semantic models, and visualizations.

|<img src='/Assests/Security/Media/PowerBiSecurity.PNG' width='1000' height='550'>|
| ----------- | 

Power BI uses two primary data storage resource types:</br>
• Azure Storage </br>
• Azure SQL Databases </br>
In most scenarios, Azure Storage is utilized to persist the data of Power BI artifacts, while Azure SQL Databases are used to persist artifact metadata. All data persisted by Power BI is encrypted by default using Microsoft-managed keys. Customer data stored in Azure SQL Databases is fully encrypted using [Azure SQL's Transparent Data Encryption (TDE)](https://learn.microsoft.com/azure/sql-database/transparent-data-encryption-azure-sql) technology. Customer data stored in Azure 
storage is encrypted using [Azure Storage Encryption](https://learn.microsoft.com/azure/storage/common/storage-service-encryption).

We roughly touched this topic under [Capacity Licenses and Features](/Assests/Security/CapacitySecurity.md/#capacity-license). All Power BI Premium capacities are automatically upgraded to support all the Fabric workloads.
> :memo: **Note:** Power BI Premium P SKUs support Microsoft Fabric. **A and EM SKUs only support Power BI items.**

To enable Power BI Premium (per-user), Go to the admin portal, then select “Users can try Microsoft Fabric paid features”.
|<img src='/Assests/Security/Media/EnablingPPUFabric.png' width='900' height='450'>|
| ----------- |

## Power BI Embedded Analytics

While Power BI as a service has its own [Power BI security whitepaper](https://learn.microsoft.com/power-bi/guidance/whitepaper-powerbi-security) published, this module focusses on the PowerBI Embedded Analytics offerings. Power BI embedded analytics allows you to embed Power BI content, such as reports, dashboards and tiles, into your application. Hence from a security view-point we will understand these and features to incorporate when using Fabric -> Power BI experience. 

Power BI Embedded has basically the same features as Power BI Premium. Power BI embedded analytics offers two solutions:

1. [Embed for your customers](https://learn.microsoft.com/power-bi/developer/embedded/embedded-analytics-power-bi#embed-for-your-customers)
2. [Embed for your organization](https://learn.microsoft.com/power-bi/developer/embedded/embedded-analytics-power-bi#embed-for-your-organization)

The artifact is embedded into an IFrame in the application or portal. An IFrame is not allowed to read or write data from the external web application or portal, and the communication with the IFrame is done by using the Power BI Client SDK using POST messages.

|<img src='/Assests/Security/Media/PowerBiEmbedded.PNG' width='520' height='300'>|
| ----------- | 

|Embed for your customers  |Embed for your organization  |
|---------|---------|
|Also known as **app owns data**         |Also known as **user owns data**         |
|Aimed at external users         |Aimed at internal users         |
|To authenticate app users, use your own authentication method        |App users authenticate against Microsoft Entra ID         |
|App users don't need a license         |Each app user needs a Power BI license         |
|Non-interactive authentication. Your app uses a *service principal* or a *master user* to authenticate        |Interactive authentication. Your app uses the app user's credentials to authenticate.  |

 You can leverage All Power BI Row Level Security (RLS) and object-level security (OLS) capabilities whether they access Power BI through the Power BI portal or through customized portals.

## Row Level Security(RLS)

Row-level security (RLS) enables you to use group membership or execution context to control access to rows in a database table. For example, you can ensure that workers access only those data rows that are pertinent to their department. Another example is to restrict customers' data access to only the data relevant to their company in a multi-tenant architecture.

Row-level security in Fabric Synapse Data Warehouse & and SQL analytics endpoint (in Lakehouse) supports predicate-based security. Filter predicates silently filter the rows available to read operations.

|<img src='/Assests/Security/Media/RLSConcept.PNG' width='400' height='200'>|
| ----------- | 

## Object Level Security(OLS)

### Embedding Setup Tool

What you can do is a quick run-down of you code with this [Embedding Setup Tool.](https://app.powerbi.com/embedsetup)
|Embed for your customers  |Embed for your organization  |
|---------|---------|
|<img src='/Assests/Security/Media/EmbeddCustomers.PNG' width='520' height='300'>|<img src='/Assests/Security/Media/EmbeddOrganization.PNG' width='520' height='300'>