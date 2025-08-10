# Olympics_2024_DataEngineering_ProjectWithAzureDevops
An end-to-end Azure &amp; Databricks data pipeline using the Olympics 2024 dataset. Ingested data with ADF into a medallion architecture, applied governance via Unity Catalog, and transformed data with Delta Live Tables using CDC for SCD Type 1. Delivered curated datasets to Databricks SQL Warehouse and Azure Synapse for advanced analytics.

## PROJECT OVERVIW
The Azure Olympics 2024 Data Engineering Project is an end-to-end data pipeline built on Azure and Databricks using the Olympics 2024 dataset. The project was managed with Azure DevOps, where I implemented CI/CD pipelines for automated deployments and reproducibility. Data ingestion was handled through Azure Data Factory (ADF), with raw data stored in the Bronze container of Azure Data Lake following the Medallion Architecture. To ensure governance and security, I utilised Unity Catalog for access control and lineage. From there, I performed data cleaning and transformation in Databricks, refining the data into Silver and Gold layers. For the Gold layer, I implemented Delta Live Tables (DLT) as an automated ETL framework, and integrated the Change Data Capture (CDC) API to manage Slowly Changing Dimensions (SCD Type 1) for the athletes table. Finally, I delivered curated streaming pipeline datasets for analysis by loading into both Databricks SQL Warehouse and Azure Synapse Analytics, enabling flexible BI and reporting. This project highlights my skills in cloud data engineering, data governance, CI/CD, and modern ETL design with Delta Lake.

<img width="1444" height="902" alt="Olympics2024data" src="https://github.com/user-attachments/assets/ad31a3b9-32cf-412b-9f5b-261910c41345" />


## Creating And Ingesting Olympics Source Data with ADF and Azure Devops

Before ingesting data, I set up Azure DevOps and created a dedicated branch to manage version control and streamline the CI/CD process
<img width="1434" height="764" alt="Screenshot 2025-09-25 at 02 03 23" src="https://github.com/user-attachments/assets/c831fb5d-6f3f-4f19-b4a3-617f8653dac5" />
.
<img width="1434" height="764" alt="Screenshot 2025-09-25 at 02 03 06" src="https://github.com/user-attachments/assets/168e615a-355f-44fe-b1ad-709a81f1a141" />

<img width="1434" height="764" alt="Screenshot 2025-09-25 at 02 03 15" src="https://github.com/user-attachments/assets/2deb25ed-a0e0-42dd-ac1b-2504a7b2114c" />
<img width="1434" height="764" alt="Screenshot 2025-09-25 at 02 21 04" src="https://github.com/user-attachments/assets/a10e9c27-17db-43a6-be19-2b0337fad110" />

Now that our branch is created the next step was ingesting our data from the source

<img width="1434" height="764" alt="Screenshot 2025-09-25 at 02 06 23" src="https://github.com/user-attachments/assets/3d9c7f62-6053-4f9b-ac17-4112744ba561" />

<img width="1434" height="764" alt="Screenshot 2025-09-25 at 02 07 35" src="https://github.com/user-attachments/assets/d7996ee0-26ec-458d-967f-0070512494c3" />

My pipeline ingested the source data successfully using the ForEach activity, after which I returned to Azure DevOps to review my commits and ensure proper version tracking.

<img width="1434" height="764" alt="Screenshot 2025-09-25 at 03 00 18" src="https://github.com/user-attachments/assets/83ee6218-c12f-4d0f-8783-0a0cb0e73499" />


<img width="1434" height="764" alt="Screenshot 2025-09-25 at 03 05 50" src="https://github.com/user-attachments/assets/f67e7561-883f-4528-ae80-8e4862f3f86c" />

<img width="1434" height="764" alt="Screenshot 2025-09-25 at 03 57 24" src="https://github.com/user-attachments/assets/92e5ac83-234e-4323-b4a9-1e5b39cea417" />

## The ARM Template

<img width="1434" height="764" alt="Screenshot 2025-09-25 at 04 08 39" src="https://github.com/user-attachments/assets/0d79c303-ed47-48a2-8588-0ef9e05bb50c" />

## Phase 2 Transformations

For the next stage of data transformation, since Unity Catalog was already enabled across my Databricks workspace, minimal configuration was required. I created a catalog and defined external locations for the raw data stored in my Bronze containers to organize and manage access effectively.

<img width="1434" height="764" alt="Screenshot 2025-09-25 at 17 13 07" src="https://github.com/user-attachments/assets/80f6671c-0676-4720-81c3-537b57ea5343" />
<img width="1434" height="764" alt="Screenshot 2025-09-25 at 17 13 36" src="https://github.com/user-attachments/assets/12c5fe83-e4ff-489b-9363-4d5fff742eb2" />
<img width="1434" height="764" alt="Screenshot 2025-09-25 at 17 13 19" src="https://github.com/user-attachments/assets/447b9ff0-d4a6-4620-8ada-4a40f832af94" />

With the external locations in place, I began reading and transforming the Olympics data to prepare it for the Silver and Gold layers of the pipeline.

<img width="1434" height="764" alt="Screenshot 2025-09-27 at 00 20 04" src="https://github.com/user-attachments/assets/847ec31d-9215-427f-812a-e7ebb6675b47" />

## SERVING- GOLD LAYER(DLT & CDC CAPTURE)
After transforming the data, reading and writing it to our Data Lake, and saving the cleaned datasets as tables in Databricks, the next step was to serve the final curated datasets. For this, I utilized Delta Live Tables (DLT), a declarative ETL framework, along with CDC apply_changes to automate Slowly Changing Dimensions for our master table, the athletes table also setting expectations for some of my other tables as I was wary of Null Values present.


<img width="1434" height="764" alt="Screenshot 2025-09-27 at 02 51 09" src="https://github.com/user-attachments/assets/3927a747-2a9f-485b-b55c-63358be99f0f" />

<img width="1434" height="764" alt="Screenshot 2025-09-27 at 02 51 17" src="https://github.com/user-attachments/assets/e0417f01-aebc-44d8-9eb5-6e547dd4d63f" />

<img width="1434" height="764" alt="Screenshot 2025-09-27 at 17 53 27" src="https://github.com/user-attachments/assets/bd85fba6-2e92-4733-9f94-417d591957ba" />

## The Final Pipeline
Thanks to DLT it made everything automated all i needed to do was set the expectations for data quality and also check that SCD Type 1(Upsert) was implemented 
<img width="1434" height="764" alt="Screenshot 2025-09-27 at 05 56 17" src="https://github.com/user-attachments/assets/16b7d95a-1911-4fb1-83bb-1322e713f77c" />

SCD Type 1(Upsert) was implemented
<img width="1434" height="764" alt="Screenshot 2025-09-27 at 06 02 35" src="https://github.com/user-attachments/assets/14d3a277-76a4-4402-9e63-2b14e3d8128a" />

Since our data passed all Data Quality Checks, it is now verified and ready to be served to data analysts and scientists for reporting and analysis.
<img width="1434" height="764" alt="Screenshot 2025-09-27 at 06 03 10" src="https://github.com/user-attachments/assets/22c64557-fd31-428b-9289-f6eb05209031" />
<img width="1434" height="764" alt="Screenshot 2025-09-27 at 06 02 45" src="https://github.com/user-attachments/assets/e0ee12dc-b419-408a-81a3-0b58bf212df0" />
<img width="1434" height="726" alt="Screenshot 2025-09-27 at 18 02 23" src="https://github.com/user-attachments/assets/c35dfe7c-2d87-4d57-ab3e-7094e275c1c5" />

## Databricks Warehousing
For reporting, I tested the curated datasets using the Serverless SQL Warehouse in Databricks to ensure they were ready for analysis and visualization.
<img width="1434" height="764" alt="Screenshot 2025-09-27 at 15 30 38" src="https://github.com/user-attachments/assets/531b9eec-a7e7-4696-b171-cccea32395e6" />
<img width="1434" height="764" alt="Screenshot 2025-09-27 at 15 31 11" src="https://github.com/user-attachments/assets/9c991875-866c-4695-bf47-cde606ae5688" />
<img width="1434" height="764" alt="Screenshot 2025-09-27 at 15 31 30" src="https://github.com/user-attachments/assets/5cfccb30-9eca-4316-bc45-d1cdd2356573" />
<img width="1434" height="764" alt="Screenshot 2025-09-27 at 15 31 46" src="https://github.com/user-attachments/assets/5f31daf5-44aa-4490-92d2-aba5dd1a4598" />
<img width="1434" height="764" alt="Screenshot 2025-09-27 at 15 36 21" src="https://github.com/user-attachments/assets/b4b6babb-a95a-41a2-bc9a-432ba433af01" />

## BI Partner Connect
Thanks to Databricks Partner Connect, I was able to provide the BI connector to the Data Analyst, enabling them to directly query and visualize the cleaned data in Power BI with ease—without needing to rely on the SQL Data Warehouse. Followed after was loading my data in Synapse Warehouse thus, the conclusion of my project.

## Synapse Warehousing
To provide additional flexibility, I loaded the curated data into Synapse Analytics using the OPENROWSET() function, bringing the final datasets from the Data Lake into Synapse for analysis and reporting.
<img width="1434" height="764" alt="Screenshot 2025-09-27 at 16 48 59" src="https://github.com/user-attachments/assets/960537ca-0a1c-476e-a207-13c45efd4e61" />

<img width="1434" height="764" alt="Screenshot 2025-09-27 at 16 33 23" src="https://github.com/user-attachments/assets/db710c4d-538a-4df5-9fec-cd75668a2060" />
<img width="1434" height="764" alt="Screenshot 2025-09-27 at 16 44 33" src="https://github.com/user-attachments/assets/86b54323-621a-4de8-afc6-6e4d2cf056d8" />
<img width="1434" height="764" alt="Screenshot 2025-09-27 at 16 45 07" src="https://github.com/user-attachments/assets/6e7415d9-3621-4346-a480-7a301818d4d1" />
<img width="1434" height="764" alt="Screenshot 2025-09-27 at 16 45 53" src="https://github.com/user-attachments/assets/3c66a546-126f-43d8-b241-0e7c2801c994" />
<img width="1434" height="764" alt="Screenshot 2025-09-27 at 16 48 49" src="https://github.com/user-attachments/assets/c479aee0-9dd4-4e7b-8d4a-8bc9567d8f4e" />
<img width="1434" height="764" alt="Screenshot 2025-09-27 at 16 49 56" src="https://github.com/user-attachments/assets/08b67027-9fed-4980-9132-dda4750aede8" />
<img width="1434" height="764" alt="Screenshot 2025-09-27 at 16 50 54" src="https://github.com/user-attachments/assets/f3828516-840f-48f1-8dcc-9bb141bc09f7" />

In my project, I chose to use views instead of tables in Synapse for the presentation layer because they provide abstraction and simplicity, hiding the complexity of the underlying raw and transformed data while making it easier for analysts to query. Views are lightweight and flexible, allowing quick updates to schema or business logic without the need to reload or duplicate data. This aligns with best practices in modern data architectures, where tables handle persistence at the raw and curated layers, while views expose clean, business-friendly models to end users. By doing this, I was able to balance performance with usability, showcasing how Synapse can still leverage optimized underlying storage while offering analyst-ready models. For my GitHub portfolio, using views also better communicates design thinking, highlighting my ability to present data in a way that aligns with real-world reporting and analytics needs rather than just displaying raw storage as soon after completion of project resource group will be deleted, although in production and future portfolio project this would be a different case as there are major instance in data loading in Synapse Workspace, in which I will demonstrate my skills in creating and presenting external tables.

