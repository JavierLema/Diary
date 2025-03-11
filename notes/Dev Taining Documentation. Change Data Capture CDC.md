---
tags: [Dev Training]
title: Dev Taining Documentation. Change Data Capture CDC
created: '2022-11-28T15:39:48.298Z'
modified: '2024-11-05T08:54:07.925Z'
---

# Dev Taining Documentation. Change Data Capture CDC
- https://docs.google.com/document/d/1Q1aJJbX3D_vRn5mzywwmnf2hOV6Z_CgpeIkGtzG0O3w/edit#heading=h.s422etnzug7j

## More interesting links
- https://learn.microsoft.com/en-us/sql/relational-databases/track-changes/about-change-data-capture-sql-server?view=sql-server-ver16
- https://www.sqlshack.com/change-data-capture-for-auditing-sql-server/
- https://hevodata.com/learn/sql-server-cdc/

### Database Schema
IndexingJob... Tables and CDC table located at RFEDEV (in DEV environment) - Tables - System Tables

### CDC has a two main modules:
- **SQL Server CDC** => It's a SQL Server component to track all Insert, Update and Delete transactions and save in a tables of CDC Schema.
- **JobServer CDC Background Processes**:
    - **Indexing CDC Job** => This job listen CDC Schema changes and insert into a queues tables.
    - **Indexing Update Jobs** => This job listen changes on queues tables and insert into a Indexing CDC Jobs (Semantic enrichment markup and indexing all content to advice ElasticSearch)
    - **Indexing Rebuild Jobs** => This jobs are used to full ElasticSearch indexes reindexation.
    - **CDC process Task** => This task is responsible the database content keep synchronized. For example, if a parent content is deleted, child contents and holdings for this need to be deleted, so this is what this process task does.

### Involved classes
- **VLIndexingComponent.cs** => The main class acts as a container for all indexing jobs (CDC, update and rebuild).
- **VLIndexingJob.cs** => This is the base class to implemented all infrastructure for running different job types.
- **IndexingUpdateJob.cs** => This file contains a specific classes for implementing the logic for Indexing Update Jobs.
- **CDC files** => All CDC files located at VLShared project on ChangeDataCapture folder

## Indexing Queues 
### Priority:
- Content = 1 => The more tricky one because the number of them is variable depending on the number of content imports running at a specific moment.
- ContentHolding = 2
- LibraryDocument = 3

## CDC Processing
https://docs.google.com/document/d/1LSyvuX9P89rOKxkCVL4fuuBHYlO3ZKBxGryt-23hIyI/edit#heading=h.cdhm4hidv279

### Introduction
Describes a process to maintance the consistency between DB and ElasticSearch with JobServer. To make this it's neccesary process SQL Transaction Log and make all update/insert/delete operation into ElasticServer, for this last step CCC uses a JobServerTasks.

### Content of CDC Tables.
- ***_$operation***
    * 1 => Delete Statement
    * 2 => Insert Statement
    * 3 => Value before Update Statement
    * 4 => Value after Update Statement
    

### CDC SQL procedures and scripts
- Show what database has enabled the CDC: 
    ```
        USE master
        SELECT database_id, [name], is_cdc_enabled  FROM sys.databases where is_cdc_enabled = 1`
    ```
- To enable CDC at database: 
    ``` 
        USE <Database> 
        EXEC sys.sp_cdc_enable_db 
    ```
- To show tables with CDC activated
    ``` 
        USE <Database> 
        SELECT [name], is_tracked_by_cdc FROM sys.tables where is_tracked_by_cdc = 1
    ```
- To create new CDC track with custom columns to captured. Example to create a tracker from ***LibraryDocument*** table
    ```
        EXECUTE sys.sp_cdc_enable_table 
            @source_schema = N'dbo', 
            @source_name = N'LibraryDocument', 
            @role_name = N'cdc_user', 
            @capture_instance = N'dbo_LibraryDocument', 
            @supports_net_changes = 0, 
            @index_name = 'PK_LibraryDocument',
            @captured_column_list = N'LibraryDocumentId,Title,DocumentType,RefDocId,AssociatedOrderId,OwnerId,PublicationDate,ContentType,DocLink,CreatedTime,CreatedBy,ModifiedTime,ModifiedBy,ClientId';
    ```
- To disable a table CDC tracker. Example to disable a tracker from ***LibraryDocument*** table
    ```
        EXECUTE sys.sp_cdc_disable_table @source_schema = N'dbo', @source_name = N'LibraryDocument', @capture_instance = N'dbo_LibraryDocument';
    ```
